---
published: true
title:  "[LAIDD] DNA-seq processing pipeline: from FASTA to VCF"
date:   2023-04-05
categories: [bioinformatics]
tags: [bioinformatics]
---

> DNA Sequencing 결과인 FASTQ 파일을 변이 주석달기(Variant Annotation)까지 처리하는 과정을 간략히 정리합니다.
> 

이하 내용은 범문에듀케이션의 [유전체 데이터 분석 2: NGS편, 김주한 지음]을 참조하였습니다.

해당 도서에서는 우분투 가상머신 환경에서 실습이 이루어졌습니다. 

이 요약에서는 대략적인 파이프라인의 흐름만을 다루며 예시 코드들을 그대로 복사하여

결과를 얻을 수 없는 부분들이 존재합니다. 

각 tool들의 옵션 선택이나 사용법은 공식 페이지를 참고하시기 바랍니다. 

모든 코드는 우분투 리눅스 환경을 기반으로 합니다.<br/>


<br/>

## 파이프라인 설명(from FASTQ to VCF)

1. Reference Genome(.fasta) Indexing_bwa
2. Short Read Alignment_baw
3. Convert SAM to BAM_samtools
4. Mark Duplicated Read_picard 
5. GATK Input(.dict, .fai) Preparing_picard, samtools
6. Local Realignment_GATK
7. Quality Score(Phred score) Recalibration_GATK
8. Variant Calling_GATK
9. Variant Annotation
    1. Variant Level_ANNOVAR
    2. Gene Level_GENCODE, Ensemble, BioMart
    3. Disease Level_ClinVar, OMIM, COSMIC Census


<br/>
<br/>

## Reference Genome(.fasta) Indexing_bwa

```bash
$ bwa index reference.fa
```

사용하는 레퍼런스 게놈의 fasta파일의 indexing을 수행합니다.

indexing은 굉장히 큰 용량의 텍스트 파일인 레퍼런스 게놈 내 접근을 빠르게 하기 위함입니다. 

인간 게놈 전체의 인덱싱은 컴퓨터 사양에 따라 상당히 긴 시간을 소모할 수 있습니다.

결과로,

`genome.fa  genome.fa.amb  genome.fa.ann  genome.fa.bwt  genome.fa.pac  genome.fa.sa`

다음과 같은 확장자를 가진 파일들이 생성됩니다.  

<br/>
<br/>

## Short Read Alignment_baw

```bash
$ bwa mem reference.fa reads.fq > ex.sam
```

`reference.fa` 에 `reads.fq`(시퀀싱 파일)을 alignment하여 `ex.sam`로 결과를 저장합니다. 

이때 single-end는 하나의 인풋을 pair-end는 두 개의 인풋을 요구합니다.

 
<br/>
<br/>

## Convert SAM to BAM_samtools

```bash
$ samtools view -bhS ex.sam > ex.bam
```

-b: 인풋 파일을 bam 형식으로 변환

-h: 헤더를 유지

-S: 인풋이 sam 형식임을 의미

sam 형식의 파일을 bam 형식으로 변환 시, 용량이 1/3 정도 줄어듭니다. 

또한 계산속도에 있어서도 보통 bam 형식이 sam 형식에 비해 빠릅니다.

<br/>

### BAM file ordering

```bash
$ java jvm-args -jar picard.jar SortSam \
I=ex.bam \
O=sorted_ex.bam 
```

picard의 `SortSam` 툴을 이용하여 BAM 형식 파일을 정렬합니다.

이를 통해 빠른 자료처리와 GATK 사용이 가능합니다. 
<br/>
<br/>

## Mark Duplicated Read_picard

```bash
$ java jvm-args -jar picard.jar MarkDuplicates \
I=sorted_ex.bam
O=dedup_sorted_ex.bam
```

MarkDuplicate의 더 자세한 옵션은 공식 문서 참고 바랍니다.

Sequencing 과정의 PCR 증폭 등의 이유로 같은 read들이 생성됩니다. 

중복된 read들은 제거하는 이유는 

1. 시퀀싱 데이터의 bias를 줄이기 위해: 특정 영역 read들이 중복될 경우 해당 지역에 더 많은 variant가 존재하는 것처럼 보일 수 있습니다.
2. downstream analysis의 효율성을 증가: 불필요한 중복 연산을 제거합니다

<br/>
<br/>

## GATK Input(.dict, .fai) Preparing_picard, samtools

```bash
$ java jvm-args -jar picard.jar CreateSequenceDictionary \
R=reference.fa
O=reference.dict

$ samtools faidx reference.fa
```

GATK은 input으로 레퍼런스 게놈의 인덱스(.dict, .fai)를 요구할 수 있습니다.

> GATK은 Broad Institute에서 만든 NGS 데이터 분석을 위한 JAVA 기반 소프트웨어 라이브러리 입니다.  주로 Quality Score Recalibration, Local Alignment, Variant Calling에 활용됩니다. [https://gatk.broadinstitute.org/hc/en-us](https://gatk.broadinstitute.org/hc/en-us)
> 
<br/>
<br/>

## Local Realignment_GATK

```bash
# 서열의 재정렬이 필요한 부분(interval)을 결정합니다.
$ java jvm-args -jar GenomeAnalysisTK.jar \
-T RealignerTargetCreator \
-R reference.fa
-I dedup_sorted_ex.bam \
-o realigner.interval
```

Local Realignment가 필요하다고 판단되는 염색체 부분을 판단하여 `.interval` 로 저장합니다.

```bash
$ java jvm-args -jar GenomeAnalysisTK.jar \
-T IndelRealigner \
-R reference.fa
-I dedup_sorted_ex.bam \
-targetIntervals realigner.intervals \
-o realign_dedup_sorted_ex.bam
```

Alignment 과정은 주로 Multiple Sequence Alignment(MSA)로, 

mismatching을 최대한 줄이며 read의 처음부터 끝까지를 align 합니다.

하지만 이로 인해 gap을 적극적으로 수용하기 때문에 실제로는 Indel일 수 있는 부분이 mismatch될 수 있는 가능성이 높습니다. 

Local Realignment는 이와 반대로 gap이 가장 적은 = 가장 긴 부분이 매칭되는 자리에 서열을 align합니다. 따라서 Indel 판단에 더 적합하다고 할 수 있습니다. 

<br/>
<br/>

## Quality Score(Phred score) Recalibration_GATK

```bash
#recalibration table 생성
$ java jvm-args -jar GenomeAnalysisTK.jar \
-T BaseRecalibrator \
-R reference.fa \
-I realign_dedup_sorted_ex.bam \
-o recal.grp
```

```bash
#recal.grp 테이블을 이용하여 recalibration 한 이후의 table을 생성
$ java jvm-args -jar GenomeAnalysisTK.jar \
-T BaseRecalibrator \
-R reference.fa
-I realign_dedup_sorted_ex.bam \
-targetIntervals realigner.intervals \
-BQSR recal.grp \ #recalibration에 사용될 table 지정 옵션
-o post_recal.grp
```

시퀀싱 과정에서는 sequencing chemistry, base-calling algorithm, DNA 자체의 특성 등으로 인해 Qualith score에 오류가 있을 수 있습니다. 또한 각 시퀀싱 플랫폼에 따라서도 score이 차이나기도 합니다. 서로 다른 플랫폼의 시퀀싱 결과 간의 score 비교를 지양하는 것이 이런 이유입니다. 

Quality score Recalibration은 실제 염기과 기대되는 염기의 비교를 통해 염기에 부여된 Quality score를 보정합니다. 이를 통해 downstream analysis의 정확도를 높일 수 있습니다. 

```bash
#recalibration 정보를 bam file에 업데이트
$ java jvm-args -jar GenomeAnalysisTK.jar \
-T PrintReads\
-R reference.fa \
-I realign_dedup_sorted_ex.bam \
-BQSR post_recal.grp \
-o recal_realign_dedup_sorted_ex.bam
```
<br/>
<br/>

## Variant Calling_GATK

SNP나 Indel calling을 위해서 사용되는 툴로는 두 가지가 GATK에 존재합니다. 

1. UnifedGenotype: Bayesian genotype likelihood model 기반,  빠름, 많은 샘플에 적합
2. HaplotypeCaller: de-novo assembly 기반, 정확함, 느림

```bash
#UnifiedGenotyper
$ java jvm-args -jar GenomeAnalysisTK.jar \
-T UnifiedGenotyper \
-R reference.fa \
-I recal_realign_dedup_sorted_ex.bam \
-o gatk_ug.vcf \
```

`UnifiedGenotyper`  의 더 많은 옵션은 공식문서를 참고 바랍니다. 

```bash
#HaplotypeCaller
$ java jvm-args -jar GenomeAnalysisTK.jar \
-T HaplotypeCaller\
-R reference.fa \
-I recal_realign_dedup_sorted_ex.bam \
-o gatk_hc.vcf \
```

`HaplotypeCaller`의 더 많은 옵션은 공식문서를 참고 바랍니다. 

`UnifiedGenotyper`  로 얻은 SNP와 Indel variant들은 따로 선별하여 추출이 가능합니다. 

```bash
$ java jvm-args -jar GenomeAnalysisTK.jar \
-T SelectVariants \
-R reference.fa \
--variant gatk_raw_ug.vcf \
-o snp_gatk_ug.vcf \
-selectType SNP

$ java jvm-args -jar GenomeAnalysisTK.jar \
-T SelectVariants \
-R reference.fa \
--variant gatk_raw_ug.vcf \
-o indel_gatk_ug.vcf \
-selectType INDEL
```

분류된 SNP과 Indel은 `VariantFiltration`을 통해서 필터링하는 것이 가능합니다.

더 자세한 내용은 공식 문서를 참고 바랍니다.

[https://gatk.broadinstitute.org/hc/en-us/articles/360037434691-VariantFiltration](https://gatk.broadinstitute.org/hc/en-us/articles/360037434691-VariantFiltration)

<br/>
<br/>

## Variant Annotation

위 까지의 과정을 통해 FASTQ 파일에서 VCF 파일까지의 처리를 마쳤습니다.

VCF에는 Reference genome과 비교하여 얻은 SNP와 indel 변이가 들어있습니다. 

하지만 현재 상태에서 해당 변이들은 염색체 내 위치만으로 표현되어 있습니다. 

추가적인 생물학적 의미를 찾기 위해서는 해당 변이 부분이 어떤 유전자와 관련이 있는지, 

혹은 어떤 질병과 관련된 위치인지를 파악할 필요가 있습니다. 

이처럼 Variant에 의미를 부여하는 과정이 Variant Annotation 입니다. 

Variant Annotation은 세 가지 레벨에서 알아보도록 하겠습니다. 

### 1. Variant Level

이 레벨에서는 Variant가 유전자에 미치는 영향의 정도를 파악합니다. 

생물의 게놈에서는 다양한 이유로 하루에도 수많은 돌연변이를 발생합니다. 

하지만 모든 변이가 유전자의 발현이나 이후 번역될 단백질에 영향을 가지고 있는 것은 아닙니다.

따라서 유전자에 영향을 끼칠 가능성이 높은 Variant만을 선별하여 연구하는 것이 바람직합니다. 

유전자에 끼칠 영향력을 판단할 때 사용할 수 있는 세 가지 알고리즘을 소개합니다. 

- `SIFT`(Sorting Tolerant From Intolerant): 진화적으로 보존된 염기서열은 중요한 역할을 담당하는 위치일 가능성이 높습니다. 따라서 이곳의 변이는 해당 단백질 기능에 큰 영향을 끼칠 수 있습니다. `SIFT`는 Variant가 진화적으로 수용 가능한 지를 판별하는 알고리즘이라 할 수 있습니다.
- `PolyPhen2`: 단백질의 3차원적 구조를 추정하고 기계학습을 이용하여 Variant가 단백질의 기능과 구조에 영향을 끼칠지 추정하는 알고리즘 입니다.
- `CADD`: 가장 최근에 개발된 알고리즘으로 Variant와 관련된 여러 데이터베이스를 종합하여 해당 Variant의 영향을 추정합니다. 가장 종합적으로 Variant의 병인성을 판단합니다.

위 모든 알고리즘들은 `ANNOVAR`를 통해 vcf 형식에 annotation 이 가능합니다. 

[https://annovar.openbioinformatics.org/en/latest/](https://annovar.openbioinformatics.org/en/latest/)

`ANNOVAR` 패키지 내에서는 각 처리에 도움이 되는 Perl(.pl) 파일이 내장되어 있습니다. 

위 웹페이지의 가이드를 보면서 진행 가능합니다.  

결과로 vcf파일에 변이가 위치한 유전자의 이름(ensGene code), exon or intron인지 등이 표시됩니다. 

<br/>

### 2. Gene Level

ANNOVAR를 통해 찾아낸 각 변이의 유전자가 어떤 의미를 가지는지 데이터베이스를 통해 확인합니다. 

- BioMart: Ensemble 내의 모든 생물학적 정보를 유전자 이름을 통해 검색이 가능합니다. 또한 파이썬이나 R과의 연계를 제공한다는 장점이 있습니다.

- GeneCard: 유전자 위키피디아와 같은 데이터베이스 입니다. 유전자 이름을 검색하면 그와 관련된 정보들이 나열됩니다.

<br/>

### 3. Disease Level 

유전자가 어떤 특정 질병과 연관이 있는지 데이터베이스를 통해 확인합니다. 

- ClinVar: 변이와 임상적 표현형의 관계를 제공합니다. FTP 서버가 존재합니다.

- OMIM: 변이가 위치한 유전자와 질병의 연관성을 제공합니다.

- COSMIC Census: 암 관련 유전자(oncogene)의 데이터를 제공합니다.
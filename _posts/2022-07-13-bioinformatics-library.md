---
title:  "Bioinformatics Python libraries: 생물정보학 파이썬 라이브러리 정리"
date:   2022-07-13 
categories: [bioinformatics]
tags: [bioinformatics]
---

> This content is from “Bioinformatics with Python Cookbook

<br/>

이번 포스팅은 Bioinformatics 분석을 위해 사용되는 여러 Python 라이브러리나

소프트웨어를 정리해보도록 하겠습니다.  

라이브러리 별 간단한 소개와 목적을 추가합니다.  

<br/>


- **Anaconda**: 파이썬 가상 환경 활용을 위해 사용됩니다. Bioinformatics에 국한되지 않고 데이터 과학의 많은 경우에서 유용하게 사용됩니다. 가상 환경을 만들고 해당 환경 속에서 각 패키지의 버전을 관리하는 것이 가능합니다. 아래는 bioinformatics를 위해 유용한 conda channel들 입니다.
    - bioconda
    - conda-forge
<br/>

- **pandas**, **numpy**: 데이터를 엑셀과 같은 배열/행렬 형태로 저장, 처리하는데 유용합니다.
<br/>

- **Scipy**: 과학 기술 계산을 위해 사용됩니다. 위 numpy, pandas와 연계가 가능합니다. 미분방정식 해석, 방정식의 근 구하기, 표준 연속, 이산 확률분포 등을 포함해 다양한 통계적 툴을 제공합니다.
    - pandas, numpy와의 연계를 통해 MATLAB을 대체하는 것이 가능합니다.
<br/>

- **Biopython**: 오픈소스 API로, bioinformatics 소프트웨어 개발과 다양한 task 수행을 위한 함수들을 제공합니다. Sequece를 다루거나 Parsing에 활용됩니다. 또한 Bioinformatics 데이터베이스의 데이터를 가져올 수 있습니다.
<br/>

- **PyVCF**: VCF 파일 처리를 위해 사용됩니다. VCF 파일은 GATK, SAMtool과 같은 소프트웨어의 결과물로, SNPs, INDELs, CNVs와 같은 유전자 변이에 대한 정보를 담고 있습니다.
<br/>

- **rPY2**: 파이썬에서 R 언어를 사용할 수 있는 인터페이스를 제공합니다. R에서 사용하는 함수의 사용이 가능합니다. 하지만 파이썬과 R은 네임스페이스가 다르기 때문에 그에 대한 주의가 필요합니다.
    - 주피터 노트북의 경우, rPY2를 사용하지 않고 매직명령어를 통해 R 인터페이스가 가능합니다. 이 경우 `%%R` 로 시작하는 주피터 노트북의 cell 전체를 R 문법을 이용해 작성하는 것이 가능해 rPY2에 비해 직관적입니다.
<br/>

- **gzip**: .gz 형태로 공개된 bioinformatics 데이터의 압축을 풀 수 있습니다.
<br/>

- **collections**.**defaultdict**: dictionary object의 하위 클래스로, dictionary의 key 값의 기본 자료형을 지정할 수 있습니다. 이를 통해 지정되지 않은 key를 호출 할 경우 KeyError를 막고, 지정해둔 defaultdict의 빈 자료형을 출력합니다.
<br/>

- **pysam**: SAMtools C API의 파이썬 구현을 제공합니다. 이를 통해 SAM & BAM file에 접근이 가능합니다.
    - SAM & BAM file은 BWA, Bowtie, CLCAssemblyCell 등의 Alignment 소프트웨어의 output으로, alignment와 mapping 정보를 담고 있습니다.
<br/>

- **matplotlib**, **seaborn**: matplotlib은 파이썬에서 다양한 통계 시각화를 수행하는 라이브러리이며, seaborn은 matplotlib을 기반으로 더 다양한 통계적 도구가 포함되어 있습니다. numpy, pandas와 연계하여 사용이 가능합니다.
<br/>

- **tabix**: tabix는 GFF, BED, PSL, BAM과 같이 TAB 간격으로 구성된 파일의 빠른 인덱싱과 영역 검색이 가능합니다.
<br/>

- **HTSeq**: 다양한 NGS data 처리 기능을 제공합니다. FASTA, FASTQ, SAM, VCF, GFF, BED file의 처리가 가능하고 데이터 통계 요약, align, read counting 기능을 제공합니다.
<br/>

- **GFFUtils**: GFF, GTF file을 다루기 위한 기능을 제공합니다. 더 유연한 조작을 위해 sqlite3 database를 만드는 것이 가능합니다.
    - GFF & GTF file은 genomic annotation을 위해 사용됩니다. (= General Feature Format)
<br/>

- **requests**: REST API를 통한 각 데이터베이스 웹 요청을 좀 더 쉽게 할 수 있는 인터페이스를 제공합니다. Bioinformatics에서는 GO(gene ontology)를 불러오는데 사용될 수 있습니다.
<br/>

- **DendroPy**: 계통학을 위한 파이썬 라이브러리입니다. 계통학적 데이터와 계통수의 조작, 처리, 시뮬레이션을 위한 함수와 클래스가 제공됩니다.
    - Biopython에서도 비슷한 기능이 제공되며, 계통수 시각화 또한 biopython 쪽이 깔끔합니다
<br/>

- **MAFFT**, **MUSCLE**: MAFFT는 게놈 정렬, MUSCLE은 단백질 서열 정렬을 위해 사용됩니다. biopython에서 Bio.Align.Applications 모듈을 통해 제공됩니다.
<br/>

- **Bio**.**PDB**: 유명 단백질 구조 데이터베이스인 Protein Data Bank에서 사용되는 PDB 파일 형식을 다룰 수 있는 함수를 제공합니다.
    - 차세대 단백질 구조 모델 파일 형식인 mmCIF의 처리를 위한 함수도 포함되어 있습니다.
<br/>
    
- **PyMOL**: 분자의 3차원 이미지와 애니메이션을 만들 수 있는 오픈소스 시각화 파이썬 라이브러리입니다. python 문법을 통해 PyMOL의 포맷인 .pml의 스크립트를 작성합니다.
<br/>

- **Planemo**: 갤럭시 분석 도구 개발을 위해 사용됩니다.
<br/>

- **Airflow**: 오픈소스 워크플로우 관리 플랫폼으로 DAGs(directed acyclic graphs)를 이용하여 여러가지 task들의 스케줄링, 모니터링이 가능하다. 각 task들은 dependency와 relationship을 가지고 있고 이런 관계가 DAG를 통해 표현됩니다. 스트리밍 워크플로우와 같이 같이 동적으로 활발한 파이프라인 파이프라인 처리에는 적합하지 않습니다.
<br/>

- **h5py**: 대용량 데이터 저장 파일 형식인 HDF5(Hierarchical Data Format) 사용을 위한 파이썬 라이브러리입니다. 해당 패키지를 numpy & pandas와 연계하여 사용하는 것이 가능합니다.
<br/>

- **Dask**: 병렬 컴퓨팅을 위한 파이썬 라이브러리입니다. numpy, pandas와의 연계가 용이합니다. 가상 데이터프레임을 통해 모든 데이터를 메모리에 로드하지 않고 처리할 수 있게 하고, task scheduler를 통해 task 처리 방식을 결정할 수 있습니다. 병렬 처리 방식, 작업 프로세스 갯수 등을 조절 가능합니다.
<br/>

- **PySpark**: Scala 언어로 구현된 병렬처리 framework인 아파치 Spark의 Python API라고 할 수 있습니다. 병렬화 구현이 Dask에 비해 추상적이고, 기본적인 데이터 구조로 RDD(resillient distributed data)를 사용합니다. pandas 사용자의 경우, 문법적으로 Dask를 사용하는 것이 편할 수 있습니다.
<br/>

- **Cython**: Python과 C 언어의 연결을 위해 사용됩니다. 파이썬은 스크립트 언어이기 때문에 실시간 소스코드 해석, 동적 프로그래밍으로 인한 변수 타입 확인 등으로 인해 수행 시간이 컴파일러 언어인 C언어에 비해 느립니다. 이를 해결하기 위해 Cython은 파이썬 스크립트를 C언어로 컴파일하여 수행 속도를 향상시킵니다. C언어로 된 함수를 파이썬 문법으로 부르거나 파이썬 함수를 C언어로 컴파일 함으로써 반복문에서 시간이 많이 소요되는 작업의 속도를 높일 수 있습니다.
<br/>

- **Numba:** Python, Numpy 코드의 JIT(Just-In-Time) 컴파일 최적화를 위해 사용될 수 있습니다. 데코레이터로 장식된 함수만을 별도로 함수 호출 시 JIT 컴파일합니다. 이를 통해 해당 부분의 속도는 machine code 버전의 속도에 따르게 됩니다. 별도의 언어를 학습할 필요가 없다는 것이 장점이지만, 일부 자료형에 국한된다거나 pandas를 이해하지 못한다는 단점이 있습니다.
<br/>

- **Cytoscape**: molecular interaction network 시각화를 위한 오픈소스 플랫폼입니다. DNA, protein 등의 high-throughput expression data 간의 network를 쉽게 표현 가능합니다. 주로 KEGG 데이터베이스와 함께 사용됩니다.
    - py2cytoscape: Cytoscape와 Cytoscape.js에 파이썬 코드를 통해 접근하는 것을 돕는 라이브러리 입니다.
<br/>

- **NetworkX**: python을 통해 graph를 표현하기 위한 class와 함수를 제공합니다. NetworkX로 만들어진 그래프를 cytoscape로 시각화 하는 것이 가능합니다.
<br/>
<br/>

각 라이브러리는 conda 명령어를 통해 설치할 수 없는 것들도 존재합니다. 또 윈도우나 Mac OS 등의 OS에 따라 지원하지 않는 것이 존재할 수 있기 때문에, 각 라이브러리의 출처에서 확인하길 추천합니다. 해당 출처에서는 각 라이브러리에 대한 tutorial을 제공하고 있기 때문에, 필요한 라이브러리의 사용법을 확인하고 연습해 볼 수 있습니다.

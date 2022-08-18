---
published: true
title:  "[Review] Cancer immunotherapy: the beginning of the end of cancer?"
date:   2022-08-18 
categories: [biology]
tags: [biology]
---

From

> Farkona, S., Diamandis, E.P. & Blasutig, I.M. Cancer immunotherapy: the beginning of the end of cancer?. *BMC Med* **14**, 73 (2016). <https://doi.org/10.1186/s12916-016-0623-5>\

-   Cancer cell은 면역계의 감지를 피하기 위해 여러 resistance mechanism을 얻음
    -   local immune evasion
    -   induction of tolerance
    -   systemic disruption of T cell signaling
    -   immune editing : malignant cell의 인식이 pressure를 받아 less immunogenic and apoptosis-resistent neoplastic cell이 된다.
-   2010년대에 들어 여러 성공사례를 통해 발전 가능성이 가속됨
    -   2010: autologous cellular immunotherapy-sipuleucel-T

    -   2011: CTLA-4 antibody- ipilimumab

    -   2014: PD1 antibody

| strategy                         | mechanism & advantage                                                                                                           | disadvantage                                                                                       |
|------------------------|------------------------|------------------------|
| Cytokines                        |                                                                                                                                 |                                                                                                    |
| IL-2: interleukin 2              | 호스트의 면역계 자극                                                                                                            | 반응률이 낮고 systemic inflammation(침투성 염증)리스크가 있음                                      |
| IFL-a: interferon-alpha          | 호스트의 면역계 자극, 소수의 환자들은 장기적인 반응을 보임                                                                      | 낮은 반응률, High-dose toxity                                                                      |
| cell-based therapy               |                                                                                                                                 |                                                                                                    |
| Vaccines                         | 호스트의 면역계 자극, 최소한의 독성, outpatient(ambulatory) clinic = 환자의 장기간 병원 투숙 필요 없음                          | universal antigen이 없고 프로토콜의 효율과 반응성이 좋지 않음                                      |
| Adoptive cellular therapy(virus) | tumor antigen의 immune tolerance breaking 필요 없음, effector T cell에 반응 좋음, TIL infusion 이전에 lymphodepleting 과정 필요 | 활용이 melanoma에 한함, 장기간 안전성 검증이 안됨, 이상적인 cell population 발달 시간이 필요, 비쌈 |
| Immune checkpoint blockade       |                                                                                                                                 |                                                                                                    |
| Anti-CTLA-4 monoclonal antibody  | 기존 존재하는 anticancer T cell을 활성화 하거나 새로 만듬, overall survival 향상                                                | 소수의 환자만이 사용가능, 35%환자에게 부작용                                                       |
| Anti-PD1 and PDL1 antibody       | 치료효과가 장기간 지속, 다양한 암에 적용가능, CTLA-4에 비해 적은 부작용                                                         | 소수의 환자만이 사용가능                                                                           |

## Vaccines

-   이전부터 암을 유발하는 전염병(hepatitis B virus & human papillomavirus)의 예방 백신을 통해 암 백신 개발 가능성이 제시됨
-   dendritic cell(DC)는 가장 효과적인 antigen presenting cell이므로, 많은 양의 antigen을 DC에게 전달하면 tumor cell의 tolerance를 break할 수 있을 것이라 생각함
-   main issue: 어떤 antigen이 가장 이상적인가
    -   짧은 peptide와 full-length protein을 써봤지만 significant 하지않음
-   하나의 antigen을 찾는 것이 아니라 다양한 tumor antigen을 함께 투여하자
    -   cancer cell 혹은 그 용해물을 백신으로 사용하자
    -   문제: 치료 효과 부족으로 임상 3상 통과 불가능, cell-based vaccin은 암특이성이 떨어짐
-   Dendritic cell의 효과적은 Antigen presenting 능력을 이용하자(DC-based vaccin)
    -   환자의 DC 추출 이후 antigen을 넣어서 키우고 다시 투여
    -   sipuleucel-T가 4개월의 overall survival 상승으로 인해 FDA 승인을 받았음
    -   하지만, 복잡한 사용방식으로 인해 실제 의료현장 활용 안됨
-   문제점: tumor antigen이 환자에게 많이 발현되어야하고 일반 조직세포는 낮게 발현해야한다. 그런 antigen을 발견한다고 해도 T cell에게 전달하는 것이 쉽지 않고, 전달하더라도 T cell이 효과적인 면역반응을 이끌 수 있는지도 확실하지 않음
-   이상적인 것은 DC가 tumor-reactive CD8+ cytotoxic T cell 합성을 자극하는 것이지만, 그렇게 만들어진 cytotoxic T cell의 면역반응 효율성도 낙관적이지 않음

## Oncolytic virus therapy

-   OV는 tumor cell만을 죽이도록 디자인된 바이러스를 사용한 치료법
    -   감염으로 인한 tumor cell의 용해, 축소
    -   systemic anti-tumor immunity 발현
-   virus 게놈 조정 가능
    -   virulence gene 발현을 억제하는 프로모터 삽입
    -   pathogenic gene을 제거하여 성장을 멈추고 용해 유도
    -   immune cell recruitment를 자극하도록
    -   용해된 tumor cell로 인해 antigen이 분출되어 CD8+ 의 면역반응이 유도 될 수 있음
-   문제: tumor cell로 바이러스가 전달되기 전에 면역반응으로 제거 될 수 있음
-   여러가지 바이러스가 OV의 벡터로써 테스트 되었으며 그 중에는 원래 인간에게 전염성이 없는 것도 있음
-   T-VEC(Talimogene laherparepvec)
    -   modified oncolytic herpes simplex virus type 1
    -   두 가지 ICP34.5 유전자가 삭제됨 → neuronal involvement 방지
    -   GM-CSF 첨가 → APC recruitment 증가로 antitumor immunity 획득
    -   ICP47 제거 → 바이러스 복제, antigen presenting 활성화
    -   임상에서 효과가 입증되어 2015년 FDA 승인을 받음
-   disadvantage & limitations
    -   면역계 손상 환자는 투약 후 전개 될 antitumor immunity가 손상 되어있을 수 있음
    -   질병이 많이 진행된 환자에게 효율성이 떨어짐
    -   antiviral immunity를 피하기 위해 tumor에 지역적으로 투여됨
        -   injection이 힘든 위치의 종양에는 접근 불가능
        -   cancer의 metastasis를 고려하여 전역적인 투약이 효과적일 수 있음

## Adoptive cell therapy

-   lymphocyte를 환자에게서 추출, ex vivo(in vitro에서 형질전환) 이후 다시 투여
-   tumor antigen의 tolerance breaking 능력 + 높은 avidity effector T cell 생산 가능해짐
-   TIL infusion 이전에 lymphodepletion을 시행한다
    -   lymphodepletion: T cell 이외 면역세포나 억제성 사이토카인을 제거
    -   Treg나 MDSC(myeloid-derived suppressor cell)과 같은 immunosuppressive cell을 제거
    -   IL-7, IL-15와 같은 homeostatic cytokine의 제거
    -   이를 통해 TIL의 functionality가 향상된다(억제성 인자, 세포영향 감소)
    -   최근 IL-2(T-cell growth factor) administration을 동반한 TIL infusion 결과 치료 효과와 반응 기간이 증가하는 결과도 있음
-   disadvantages
    1.  lymphodepletion(특히 ablative radiation therapy 동반시)이 환자에게 치명적일 수 있음
    2.  이상적인 세포 배양을 위한 시간과 돈이 많이 듬
    3.  TIL therapy 적용이 melanoma에 한정됨
        -   다른 암도 시도했지만 melanoma에서만 치료효과가 있음
        -   melanoma의 높은 빈도의 돌연변이율이 높은 immunogenicity와 연관있음
-   연구중인 접근법

1.  **T cell receptor(TCR) T cell**

-   TCR-alpha, beta의 발현을 포함시킨다.
-   Human leukocyte antigen(HLA) peptide 을 가지는 tumor를 가지는 환자에게 적용가능
-   normal tissue가 같은 target antigen을 발현할 경우의 secondary destruction 문제

1.  **Chimeric antigen receptor(CAR) T cell**

-   tumor cell이 특정 antigen을 발현할 필요가 없음
    -   T cell에 target antigen을 인식가능한 antibody가 포함되어 있음, tumor의 어떤 potential cell surface antigen도 인식 가능

## Immune checkpoint blockade(면역 관문 억제제)

-   암 치료 이전에도 환자에게 endogenous immune response가 있지만 효과적이지 않음
    -   tumor의 tumor-specific T cell에 대한 tolerance
    -   tumor에서 T cell의 inhibitory receptor에 바인딩하는 ligand를 발현하여 기능을 떨어뜨리기 때문에.
-   immune checkpoint blockade는 immune-inhibitory pathway의 활성화를 막는 방법
-   CTLA-4: T-cell의 inhibitory receptor
-   anti-CTLA-4 antibody가 anti-tumor 특성을 이끄는 것을 확인한 이후 연구 진행
-   Ipilimumab: anti-CTLA-4 antibody가 2011년 FDA 승인을 받음
    -   적은 비율의 환자에게만 효과를 보였으나, 효과를 본 환자들에게는 significant 치료 효과와 long-lasting 효능을 보임
-   ipilimumab 문제점
    -   T cell expansion의 부족한 specificity로 인해 immune-related toxicity 가능성 있음
    -   ipilimumab response가 몇 달 후에 일어남, 다른 conventional cytotoxic therapy의 빠른 종양 억제에 비해 느림
-   PD1: antigen-stimulated T cell의 inhibitory receptor
    -   리간드로 PD-L1, PD-L2를 지님
-   PD1과 PD-L1 사이의 interaction을 막는 anti-PD1, anti-PD-L1 antibody가 T cell의 anti-tumor reponse를 강화함
-   pembrolizumab, nivolumab: anti-PD1 antibody
-   atezolizumab: anti-PD-L1 antibody
-   CTLA-4가 de novo immune response를 조절하는데 반해, PD1은 ongoing response를 조절함
-   또한, PD1의 특성으로 인해 CTLA-4에 비해 독성이 약하거나 컨트롤 가능함
-   연구 중인 immune checkpoint target
    -   lymphocyte activation gene 3 protein(LAG3)
    -   T cell immunoglobulin and mucin domain-containing 3 (TIM3) protein

## Combination therapies

-   환자 서브그룹은 단일 immunotherapy로 효과를 보이지만, 대부분의 경우 비교적 ineffective함
-   immunotherapy combination에 대한 연구가 활발히 진행 중

combining immune checkpoint inhibitors

-   CTLA-4와 PD1은 서로 다른 signaling pathway를 이용
    -   CTLA-4: dampening T cell priming
    -   PD1: block effecter T cell response within tissue
-   따라서 두 가지의 동시 사용이 가능할 것으로 기대되고, 동물실험 결과 향상된 항암효과를 보임
-   ipilimumab + nivolumab 동시 사용 임상 결과도 좋음, 3상 진행 중
-   하지만 부작용이나 독성 또한 강도와 빈도가 상승할 수 있기 때문에 장기간 검증이 필요함

combining immune checkpoint inhibitor + conventional therapies

-   conventional cytotoxic chemotherapy는 tumor의 immunosuppressive environment를 조절하기 때문에 immunotherapy 성능을 증가시킬 수 있음

-   또한 chemotherapy로 인한 tumor burden 감소의 이점을 이용 가능

-   하지만 chemotherapy에 따라 immunotherapy의 reponse를 방해하거나 adverse event를 늘릴 수 있음

-   vascular endothelial growth factor(VEGF) guided therapy와의 조합도 가능

-   VEFG role

    -   angiogenesis
    -   tumor 내 Treg와 MDSCs 증가
    -   lymphocyte의 intratumoral influx 감소
    -   DC maturation 억제

-   VEFG inhibition 약물(ex. bevacizumab) + ipilimumab의 조합

    -   실험 결과 좋은 임상 결과를 보임, 부작용도 controllable

-   bevacizumab + atezolizumab(PD-L1 antibody)

combining immunostimulatory antibodies

-   immunostimulatory antibody는 주로 TNF receptor superfamily를 타겟한다.
    -   해당 타겟 receptor들(OX40, 4-1BB)를 자극하는 역할
-   4-1BB는 CD4+ CD8+의 membrane glycoprotein
    -   T cell activation, growth, survival, effector function을 활성화함
    -   Urelumab, Utomilumab와 같은 약물이 단일 혹은 조합 사용되었을 때 항암 효과를 보이는 임상 실험 결과가 존재
-   OX40은 CD4+ CD8+의 costimulatory receptor
    -   T cell activation, survival, proliferation, cytokine production 활성화
    -   OX40 agonistic antibody 사용 시 advanced cancer treat을 보임
-   GITR(glucocorticoid-induced tumor necrosis factor receptor related gene)은 costimulatory molecule로 주로 Treg cell에서 발현됨.
    -   이것이 CD4+ CD8+, DC, monocyte, NK cell에서도 발현됨
    -   GITR ligand는 APC나 epithelial cell에서 높게 발현됨.
    -   자연적인 ligand나 GITR agonist antibody로 활성화 될 경우 anti-tumor therapy에 효과를 보임
    -   CTLA-4나 PD1 therapy와의 조합에서도 효과를 보임
-   (immune checkpoint blockade + cancer vaccines), (immune checkpoint blockade + OVs), (immune checkpoint blockade + T-VEC)등이 연구되고 있음
-   immune checkpoint blockade가 다양한 tumor type에 효과를 보이고 있기 때문에 immunotherapy combination의 backbone 역할을 하고 있음
    -   하지만 antitumor mechanism에 대한 정확한 이해가 부족할 경우, combination으로 인한 unforeseen sideffect가 있을 수 있다.

## Biomarkers in cancer immunotherapy

-   Immunotherapy는 cancer therapy의 게임체인저로 여겨지고 있지만, 오직 소수의 환자만이 반응을 보인다.
    -   따라서 올바른 patient selection을 위해 biomarker identification과 validation이 중요함.
-   highly mutagenized tumor의 mutational load가 neo-antigen-specific T cell response를 이끌어내 immunotherapy의 치료 반응에 기여함
    -   mutational frequency가 CTLA-4 thearpy의 clinical 반응과 비례하다는 연구 결과
    -   DNA repair pathway mutation이 anti-PD1 치료 효과와 비례
-   immunotherapy combination에 대한 환자의 반응이 환자의 immune milieu(환경)에 따라 다르다
    -   따라서 환자의 tumor microenvironment에 대한 genetic profiling을 고려하여 immunotherapy combination을 결정해야한다.
-   연구된 biomarkers
    -   Mutational load
    -   Lymphocyte infiltrates
    -   PD-L1 expression
    -   Genetic profiling

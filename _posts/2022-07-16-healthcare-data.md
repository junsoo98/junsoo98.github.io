---
published: true
title:  "Healthcare AI 모델에 사용 가능한 EHR data 정리"
date:   2022-07-16
categories: [cheminformatics]
tags: [cheminformatics]
---
<br/>

이번 포스팅에서는 healthcare AI 모델에 사용할 수 있는 여러가지 data를 정리해보려 합니다.  
<br/>


Electronic health recored(EHR)은 환자의 건강 상태와 관련된 정보를 담은 

patient’s paper의 digital version이라고 할 수 있습니다. 

예시로는 clinical note, diagnosis code, medication prescription 등이 있습니다.  

<br/>

EHR은 굉장히 많은 종류가 있고 이들을 두 가지 type으로 나누어 볼 수 있습니다. 
<br/>


**Structured** 와 **Unstructered**로 나눌 수 있는데, structured는 말 그대로 환자의 정보를

제한된 규칙이나 사전 정의된 형식에 따라 표현하는 것을 말하고, unstructered는 이에 해당하지

않는 모든 data들을 지칭합니다.   

<br/>


각 type의 data들의 예시를 정리해 보겠습니다. 
<br/>


- **Structured**:
    - Medical Code(international disease classification, ICD)(current precedure terminology, CPT)
    - Clinical Classification Software(CCS) code
    - Patient Demographics
    - Vital Sign
    - Social History (gender, smoking, etc.)

Structured 자료의 특징은 Sparsity와 Temporality를 가진다는 점입니다.  
 
<br/>


- **Unstructured**:
    - Clinical Note
    - Medication Prescription
    - Progress Note
    - Nursing Note
    - ECG report
    

Unstructured 자료의 특징은 High dimension이며, external knowledge를 해석에 필요로 할 수 있고,

환자의 privacy와 연관되어 있을 가능성이 높다는 것입니다.  

<br/>


추가적으로 Structured data에 속하는 여러 healthcare standard code들을 정리합니다.
<br/>


- Health data standard - 헬스케어 관련 구조적인 표현 code
    - ICD: international classification of disease. 질병, 증상, 처방에 대한 코드. hierarchical structure를 지님
    - CPT: current procedural terminology. medical service & procedure 표현
    - NDC: national drug code. FDA 관리
    - LOINC: logical observation identifier names and code. lab test에 대한 code.
    - SNOMED CT: Systematized Nomenclature Of Medicine Clinical Terms. 모든 medical terminology의 ontology에 대한 code.
    - CCS: ICD와 CPT 코드를 더 나은 statistical analysis를 위해 집계. *머신러닝을 위해 raw ICD or CPT code에 비해 informative 할 수 있음*
    - RxNorm: terminology system for drug and the associated software for mapping various mentions of drugs to normalized drug name.
    - UMLS: Unified Medical Language System.
        - Metathesaurus: ICD, CPT, LOINC, SNOMED, RXNorm을 포함
        - Semantic Network: 모든 concept의 network 제공
        - Lexical Tool

![healthcare.jpeg](/images/post-images/healthcare.jpeg)  

<br/>


다음으로는 In silico drug discovery에 사용 가능한 data들 또한 정리해보았습니다. 

- In silico drug discovery data
    - compound graph or sequence
    - protein target sequence
    - genome sequence
    - disease-related knowledge graph
  

<br/>
    

앞서 정리한 data들은 GNN나 RNN을 이용한 자연어 처리, 딥러닝을 통해 학습하여 환자에게 

환자 대상 약물의 독성 예측을 통해 medication recommendation을 하거나, 

새로운 약물을 위한 분자 간 interaction이나 toxicity 예측에 사용될 수 있습니다.
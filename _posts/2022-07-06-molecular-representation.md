---
published: true
title:  "[LAIDD] RDKit을 이용한 분자 구조 표현법과 fingerprint"
date:   2022-07-06
categories: [cheminformatics]
tags: [cheminformatics]
---

> 이 포스팅은 LAIDD 강원대 이주용 교수님의 “RDKit의 기초와 이를 이용한 화학정보학 실습”을 토대로 정리되었습니다.  

 
 

[https://www.rdkit.org/](https://www.rdkit.org/)

**RDKit**은 cheminformatics와 머신러닝을 위한 여러 기능을 포함하고 있는 파이썬 package입니다.

분자구조 표현 형식간 전환, fingerprint generation, similarity caculation부터

다양한 Descriptor calculation 함수들을 내장하고 있습니다. 

또한 머신러닝과 data sciencef를 위해 많이 사용되는 numpy, pandas, sklearn과 같은

다른 python package들과의 연계를 통해 분자나 화학반응을 prediction하는 모델 구축이 가능합니다.  






이번 포스팅은 간단한 RDkit 함수들과 추가적인 공부 source를 다루도록 하겠습니다.

## RDKit을 통해 분자 구조 format 표현

```python
!conda install -c conda-forge rdkit -y
import rdkit
```

아나콘다 설치 후 jupyter notebook 환경에서 위 코드를 통해 RDKit을 설치, import가 가능합니다. 

분자 구조 파일 형식에 대한 간단한 설명 이후 RDKit 함수로 넘어가도록 하겠습니다.  





화학 언어는 분자 구조의 2D diagram을 사용합니다. 하지만 이는 컴퓨터가 인식하기 좋은 

표현 방식이 아닙니다. 따라서 이를 간단한 string이나 벡터 형식으로 변환하는 것이 좋습니다. 

이를 위해 널리 사용되는 방식들은 다음과 같습니다.

- Linear notation
    - SMILES
    - InChI, InChIKey
- Connection table method
    - Molfile
    - SDF  
  
  
  
  


**SMILES**는 알파벳과 특수문자들로 이루어진 스트링으로 분자구조를 표현합니다.

2D 구조를 스트링으로 표현한다는 것으로 간단하고 직관적이라는 장점이 있습니다.

하지만 string이기 때문에 어떤 원소를 시작점으로 잡는지에 따라

같은 분자구조에서 여러 개의 SMILES 표현이 가능하다는 단점이 있습니다.

이를 해결하기 위해 Morgan algorithm을 통해 Canonical SMILES를 만듭니다.

Morgan algorithm을 간단히 표현하면 iteration을 통해 각 분자에 고유 숫자를 asign합니다. 

이 숫자는 각 원자들의 connectivity 값입니다. 이 값을 기준으로 원자들의 번호를 정합니다. 

morgan algorithm:[https://pubs.acs.org/doi/abs/10.1021/c160017a018](https://pubs.acs.org/doi/abs/10.1021/c160017a018)

SMILES는 몇가지 단점이 있습니다.

- 기업이 만든 것이기 때문에, 생성 알고리즘에 따라 조금씩 차이가 있습니다.
- 2D, 3D 구조에 대한 좌표값을 포함하지 않습니다.  
 
 
 
  

**InChI**는 기업 태생의 SMILES 대신 통합된 표준을 제시하기 위해 IUPAC이 만든 방식입니다.

SMILES의 단점을 커버하기 위해, 한 분자구조는 한 code만을 반환합니다. 

하지만 InChIKey의 단점은 분자구조가 복잡해질수록 string의 길이가 길어지고,

인터넷 서칭에 용이한 형식이 아니라는 점입니다.

이 단점을 보완하기 위해, Hashing algorithm을 통해 InChI를 변환한 것이

바로 **InChIKey** 입니다.  






지금까지 말한 것들은 Linear notation이라면, 이제 connection tables를 알아봅니다.

[https://en.wikipedia.org/wiki/Chemical_table_file#Molfile](https://en.wikipedia.org/wiki/Chemical_table_file#Molfile)

**molfile**은 한 파일에 한 분자의 구조 정보를 저장합니다. 

파일 안에는 여러 개의 table이 포함되어 있습니다. 

각 table은 

- header: 분자 이름 등의 정보
- atom table: 원자의 종류와 xyz 좌표 등의 정보
- bond block: 원자 간의 결합 정보
- properties block: 이외 분자 특성 정보

**SDFile**은 여러 개의 molfile을 연결하여 저장하는 형식입니다.  





이제 RDKit을 통해 분자를 표현해봅시다. 

```python
from rdkit import Chem
#Chem module에서는 mol file과 SMILES간의 변환, Chiral Center 찾기가 가능합니다.
m = Chem.MolFromSmiles('Cc1ccccc1') 
m
m = Chem.MolFromMolFile("./data/input.mol")
print(Chem.MolToMolBlock(m))
Chem.MolToSmiles(Chem.MolFromSmiles('Cc1ccccc1'))
```

`Chem` 모듈에는 분자 구조 포멧 간의 변환과 Chiral Center를 찾는 함수가 포함되어 있습니다.

`MolFromSmiles` : SMILES를 인풋으로 받아 해당 분자 구조를 저장하는 mol object를 반환

mol object 실행 시, 분자 구조 이미지를 출력합니다. 

`MolFromMolFile` : mol file path를 인풋으로 받아 mol object를 반환

`MolToMolBlock` : mol object의 mol file 형식 table을 반환 

`MolToSmiles` : mol object의 분자를 SMILES로 변환하여 반환   



```python
suppl = Chem.SDMolSupplier('data/5ht3ligs.sdf') 
#sdf 형식의 분자 파일 읽어오기 

import gzip 
inf = gzip.open('data/actives_5ht3.sdf.gz', 'rb') #rb옵션은 바이너리 옵션
gzsuppl=Chem.ForwardSDMolSupplier(inf)

```

mol file은 각 데이터베이스로부터 다운 받아 사용이 가능하다. 

PubChem: [https://pubchem.ncbi.nlm.nih.gov/](https://pubchem.ncbi.nlm.nih.gov/)

ChEMBL: [https://www.ebi.ac.uk/chembl/](https://www.ebi.ac.uk/chembl/)

하지만 주의할 점은 데이터베이스마다 각 원자에 수소를 생략하고 저장하는 경우가 있다는 점이다. 

따라서 차후 정확한 분석을 위해 mol file에 수소를 붙여주는 작업이 필요하다.  



```python
m = Chem.AddHs(m)
m = Chem.RemoveHs(m)
```

함수의 이름은 직관적이다. 

`AddHs` : mol object에 수소를 붙여 반환

`RemoveHs` : mol object에 붙은 수소를 떼서 반환  



## fingerprint  표현

앞서 언급한 것처럼, 화학 언어는 기본적으로 2D diagram을 이용합니다.

이것은 직관적인 장점이 있지만 컴퓨터를 이용한 계산은 느리다는 단점이 있습니다.

따라서 컴퓨터 친화적인 형태인 스트링이나 벡터로 표현합니다. 

fingerprint는 분자들간 구조의 유사도를 빠르게 측정하기 위해 사용됩니다.

2D diagram을 직접 비교하지 않고, 분자 구조의 특징을 뽑아내어 이를 통해 비교하는 것입니다. 

대표적인 두 가지 fragment code, MACCS keys 와 ECFPs를 살펴보겠습니다.  





**MACCS**(molecular access system)는 166-bits로 이루어진 

2D structure fingerprint이다. 분자 sub structure의 keys들을 통해 분자를 표현한다.

각 분자들은 166-bits의 binary bitstring 패턴으로 표현되기 때문에 이를 비교하여

각 분자들간의 유사도를 빠르게 측정할 수 있다. 

단점으로는 MACCS의 key들이 implementation에 따라 조금씩 다르다는 것이다.  






**ECFP**(Extended Connectivity FingerPrint)는 앞서 언급한 Morgan algorithm과

비슷한 과정을 이용한다. 

1. 각 원자들은 여러 특성을 고려하여 integer identifier number를 부여
2. 이후 morgan algorithm처럼 각 identifier를 업데이트
    - 이때 입력된 radius만큼의 substructure만을 고려
3. 중복 identifier 제거
4. 생성된 각 substructure identifier를 hashing으로 고정된 길이의 bit-string으로 변환
    - 길이는 1024나 2048 bits를 주로 사용

위 과정을 통해 분자 구조 패턴을 담은 sparse binary bit string을 얻을 수 있다. 

하지만 단점으로는 hashing을 사용하기 때문에 다른 identifier가 같은 bit에 담기는

bit collision이 일어날 수 있다.  








### RDKit을 통한 fingerprint 생성 

```python
from rdkit import DataStructs #rdkit fingerprint 생성 함수 포함 모듈 
Chem.RDKFingerprint(m)

from rdkit.Chem import MACCSkeys
MACCSkeys.GenMACCSKeys(m)

from rdkit.Chem import AllChem
AllChem.GetMorganFingerprint(m, 2) #두번째 매개변수로는 radius를 입력 
```

각 fingerprint generating 함수들은 mol object를 입력으로 받아 fingerprint를 반환한다.

`RDKFingerprint` : RDKit 내 topological fingerprint 생성 함수

`MACCSkeys.GenMACCSKeys` : MACCSkeys 모듈의 maccs keys 생성 함수 

 `AllChem.GetMorganFingerprint` : AllChem 모듈의 ECFP 생성 함수

생성된 fingerprint들은 `DataStructs` 모듈 내의 유사도 측정 함수를 통해 분자 구조 유사도를 

측정한다. 사용 가능한 유사도는 굉장히 많이 준비되어 있다.

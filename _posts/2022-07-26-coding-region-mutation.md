---
published: true
title:  "Coding Region Mutation 정리(Missense, Nonsense, Silent, Frame Shift, In-Frame mutation"
date:   2022-07-26 
categories: [bioinformatics]
tags: [bioinformatics]
---

이번 포스팅은 coding region의 mutation의 종류에 대해 적어보려 합니다.
<br/>


coding region은 전사, 번역을 통해 아미노산에 대응되는 유전자 서열이 존재하는 DNA, RNA 지역입니다. 

이 지역의 염기서열에 mutation이 생길 경우, 번역되는 단백질 서열에 영향을 미칠 수 있고

이것은 다양한 phenotype의 변화를 불러 일으킵니다.
<br/>
<br/>

다음은 TCGA 데이터의 환자들이 가진 mutation의 종류를 확인한 plot 입니다. 

![mutation_sort.jpeg](/images/post-images/mutation_sort.jpeg)

Missense mutation이 가장 많으며 다음으로 Silent, 3’UTR, Nonsense mutation이

뒤를 잇는 것을 볼 수 있습니다. 
<br/>

오늘은 이중 Missense, Nonsense, Silent, Frame Shift, In Frame에 대해 설명하려 합니다. 
<br/>

## Missense mutation

Missense mutation은 codon에서 하나의 nucleotide에 돌연변이가 생겨(point mutation)

번역 시 하나의 amino acid이 다른 단백질 서열이 합성되는 돌연변이입니다. 

nonsynonymous mutation이라 부를 수도 있습니다.

하나의 아미노산 서열 변경이 일어나므로, 서열 상의 위치에 따라 해당 돌연변이가

단백질 기능에 영향을 끼칠지 결정됩니다.

protein active site의 아미노산 변화는 단백질 기능의 심각한 변화를 이끌 수 있습니다. 
<br/>


## Nonsense mutation

Nonsense mutation은 nucleotide의 point mutation으로 인해 

codon이 stop codon(TAG, TAA, TGA)가 되는 돌연변이 입니다. 

이로 인해, 단축된 길이의 nonfunctional protein이 합성됩니다. 
<br/>


## Silent mutation

Silent mutation은 앞선 두 mutation과 같이 point mutation이 일어납니다.

하지만 mutation의 영향으로 아무런 변화가 일어나지 않습니다. 

이유는 RNA redundancy 때문입니다.

하나의 아미노산을 지정하는 codon은 한 개 이상입니다.   
<br/>  


예를 들어 Serine을 지정하는 codon은 UCC, UCU, UCA, UCG입니다.

만약 원래 UCC였던 codon이 point mutation으로 UCU가 되었다고 해도, 

결과적으로 번역되는 아미노산이 Serine임은 변하지 않습니다.

이런 mutation을 Silent mutation이라 합니다.   
<br/>


## Frame Shift & In-Frame mutation

Frame Shift mutation은 Indels와 연관 있습니다.

위 plot에서 Frame Shift Ins와 Frame Shift Del이 있는 것을 확인할 수 있습니다. 

insertions 혹은 deletions으로 인해 3개의 nucleotide 단위로 읽던

frame에 변화가 생기는 돌연변이가 Frame Shift mutation입니다. 

돌연변이의 영향으로 indels 이후의 서열에서는 원래 서열과 

완전히 다른 단백질이 번역될 수 있기 때문에 심각한 유전질병을 일으킬 수 있습니다. 

In-Frame mutation 또한 Indels로 인해 발생합니다.   
<br/>  


하지만 Frame Shift와 달리 돌연변이 이후 sequence reading frame에 

변화가 생기지 않는 돌연변이 입니다.   

예를 들어 하나의 codon을 이루는 3개의 nucleotide가 한번에 deletion 될 경우,

합성된 단백질은 원래의 것에서 하나의 아미노산이 빠진 단백질이 될 것입니다. 

이런 In-Frame mutation은 조건이 까다로운 만큼 흔치 않은 돌연변이임을 

위 plot을 통해 확인할 수 있습니다.   
<br/>  


유전자에 따라 In-Frame mutation의 빈도가 특별히 높을 수 있습니다.

예를 들어 oncogen 중 하나인 EGFR의 경우, 

exon 19에서의 In-Frame mutation(E19del)이 지배적으로 나타납니다. 
<br/>

---

위에 나열된 coding region의 돌연변이들은 Silent mutation가 아니라면 

합성되는 단백질의 아미노산 서열 변화로 인해 단백질 기능 변화를 유발합니다.

이는 암을 비롯한 치명적인 유전 질환의 원인이 되기 때문에 주목할 필요가 있습니다.  
<br/>  


또 다른 주목할 점은 돌연변이들이 나타나는 유전자 내 위치가 경향성을 가질 수 있다는 점입니다. 

아래 그림은 human cancer에서 가장 높은 빈도로 mutation 하는 oncogen 중 하나인

PIK3CA의 유전자 위치 내 Missense mutation 빈도를 표현한 histogram입니다.    


![pik3ca_position.jpeg](/images/post-images/pik3ca_position.jpeg)

위 plot을 통해 몇 군데 peak가 나타나는 것을 볼 수 있습니다.

이렇게 mutation이 빈번한게 일어나는 위치를 mutation hotspot이라 합니다. 

mutation hotspot을 암을 비롯한 유전 질환 치료에 활용할 수 있는 방안을 찾는 것도 

중요한 연구 주제 중 하나가 될 수 있을 것입니다.

---
title:  "[Standard] Paper Review : ACMG(genomics terminology standards)"
excerpt: "유전체 정보 표준화"

categories: [Study, Standard, Review]
tags:
  - [유전체, 유전, 표준, standardization, standard, CYP2D6]

toc: true
toc_sticky: true
 
date: 2022-12-09
last_modified_at: 2022-12-09
math: true
comments : true
mermaid: true
---

# ACMG TECHNICAL STANDARD
# Clinical pharmacogenomic testing and reporting: A technical standard of the American College of Medical Genetics and Genomics (ACMG)

---
## Abstract
- 이 문서는 publicly available resources를 요약하고 약물유전체학의 명명법, 검정, 결과의 해석, 보고와 관련한 최고의 시도들을 면밀히 제공하여 임상 약물유전체 검정을 발전시키기 위한 목적으로 관련한 resource를 제공한다.

## Background
### Purpose of pharmacogenomic testing
- clinical pharmacogenomic testing의 목적은 약물대사과정과 같은 약리학의 관점에서 개인간에 일어날 수 있는 여러 가능성과 연관된 genetic variants들을 검증하는 것이다.
- 주로 사용되는 테스트로는 pharmacokinetic방법과 pharmacodynamic 방법이 있다.
- pharmacokinetic
  - drug inactivation or activation
  - drug absorption, distribution, metabolism, elimination을 설명한다.
- pharmacodynamic
  - drug response
  - therapeutic response와 adverse event에 대한 활성의 메커니즘을 설명한다.
- pharmacogenomic biomarker
  - enzymes
  - receptor
  - ion channel
  - transporter protein
  - immune mediator
- 약물유전체적 검증을 drug response phenotype과 연관지어 해석하면 drug selection과 dosing decision에 도움을 준다.   
  - 특히, 특정 pharmacogenomic variants를 확인하면 치명적인 side effect를 야기하는 약물에 대한 처방을 피할 수 있다.
  - 이러한 pharmacogenomic variants는 non-standard dose of a medication으로도 환자에게 좋은 영향을 줄 수 있을지도 모른다.
  - 그래서 personalized or precision medicine or inidividualized drug therapy라고 불린다.
- clinical pharmacogenomic testing를 뒷받침하는 publicly available resource들은 많다.
  - PharmGKB(PharmacoGenomic KnowledgeBase) : international publicly accessible repository
    - gene-drug association에 대한 description과 reference 제공
    - gene-based dosing 가이드라인 제공
    - 약물유전체 정보 담은 lists approved drug labelling 제공
  - CPIC(Clinical Pharmacogenetics Implementation Consortium) : evidence-based gene/drug clinical practice guideline
    - pharmacogenomic testing이 수행되어야 하거나 testing 필요한 variants 연구에는 부적합
    - 대신, genetic test results를 특정 약물에 대하여 처방을 결정한다는 관점에서 해석하는 방법을 제공하여 약물치료효능을 최적화하는 데 도움을 줌
  - PharmVar(Pharmacogene Variation) : centralized data repository
    - high-quality variation data of pharmacogene 제공
    - 유전자 수 증대에 따른 대립형질 지정 체계나 명명법을 통일
  - FDA(Food and Drug Administration) Table of Pharmacogenomic Biomarkers in Drug Labelling
    - Approved Drug Labeling 내에서 체세포 및 생식세포 바이오마커를 제공
  - FDA Table of Pharmacogenetic Association은 clinical evidence에 기반한 3개의 germline gene-drug association table 제공
    - gene-drug associations with therapeutic management recommendation
    - gene-drug associations with potential impact on safety or response
    - gene-drug associations with pharmacokinetic relevance
  - CPIC와 FDA 제공 테이블은 겹치는 부분이 전혀 없다.
    - evidence와 criteria에 대한 evaluation이 society마다 다르기 때문
  - ACMG는 2012년 $\texttt{CYP2D6}$을 시작으로 가이드라인을 확장하여 표준을 제공한다.

### Pharmacogenomic nomenclature
- 특정 약물유전체에 대한 명명은 1배체형을 기준으로 정의한다. 
  - 1개나 그 이상의 SNV(Single Nucleotide Variant), 50개 뉴클레오타이드 이하의 삽입/결실로 구성된 1배체를 주로 말한다.
- star(*) alleles
  - combinations of sequence variants를 지정
  - $*1 \texttt{ allele}$ : default. tested variant가 발견되지 않은 경우
  - $\texttt{NAT2}$는 예외적으로 $*4 \texttt{ allele}$가 default이다.
  - 아미노산 변화, frame-shift, 스플라이싱이나 표현형에 영향을 주는 것들을 표현
    - core variant라 부른다.
    - clinical pharmacogenomic testing assay의 analytical target
- star allele may have 2 or more suballeles
  - 예) CYP2D6*4 is defined by c.506-1G>A splice variant(rs3892097, NC_000022.11:g.42128945C>T). 이는 기능 상실을 유도
  - 많은 haplotype에서 SNV가 추가된 조합이 많이 발견되는데, 이들이 CYP2D6*4 suballele이다.
    - core allele : CYP2D6*4
    - suballele : CYP2D6*4.001, *4.002, etc.
      - suballele는 numeric extension으로 표현된다.
      - star number에 기재된 suballele는 기능적으로는 동일한 것으로 간주한다.
  - CYP2D6*10의 core variant로 분류되는 또다른 사례가 있다. 
    - c.100C>T(p.Pro34Ser, rs1065852, NC_000022.11:g.42130692G>A)
- 두 variant c.506-1G>A와 c.100C>T가 동시에 발견되는 이형접합자는 diplotype을 CYP2D6*4/*10 또는 CYP2D6*1/*4으로 나타낸다.
  - 이는 variants들이 같은 염색체에 있는가(cis인가) 혹은 반대편의 염색체에 있는가(trans인가)에 따라 결정
  - 대부분의 CYP2D6 testing은 cis/trans를 결정하지는 않지만 주로 cis형이다.
  - 그러므로, 이형접합자 관찰 시 ACMG는 CYP2D6*1/*4로 표기하는 것을 더 권고한다.
- A>G/C/T같이 1개의 allele 이상을 갖는 variation site가 있으므로 database of single nucleotide polymorphisms(dbSNP) rs identifier는 유일한 표현을 제공하지 않는다. 
- 어떤 pharmacogenes는 CNV(Copy Number Variants)에 의해 영향을 받는다.
  - CNV에는 유전자 결실, 중복, multiplication, rearrangement 등이 포함된다.
- CNV는 주로 structual Variation에 의해 발생한다. 하지만, CYP2D6의 structual variation을 표기하는 표준화된 방법은 아직 없다.
  - CNV는 주로 multiplication sign과 the number of gene copies를 기재하여 표기한다.
  - 예를 들어, CYP2D6*1/*2 $\times$ 2는 전체 3개의 gene copy 중 같은 염색체에 있는 *2 allele에 2개의 copies가 있음을 말한다. 
  - CYP2D6*1/*36+*10은 전체 3개의 gene copy 중 염색체1이 CYP2D6*36 allele의 copy를 CYP2D6*10 allele와 나란히 갖는다는 것을 의미한다.
- PharmVar GeneFocus review series는 약물유전체 명명법에 대해 추가적인 정보를 제공하고 있다. 
  - CYP2D6, CYP2C19, CYP2B6, CYP2C9는 이미 알려져 있다.
- non-*1 genotype은 잠재적 리스크가 있는 표기법이다.
  - 예를 들어, CYP2D6*2 allele의 variants for the normal function는 2가지로 p.Arg296Cys (rs16947, NC_000022.11:g.42127941G>A)과 p.Ser486Thr(rs1135840, NC_000022.11:g.42126611C>G)이다. 
  - 이 2가지 variant는 CYP2D6*8, *11, *12, *17, *29, 기타 등등에도 나타난다. 
  - 이렇게 되면 nonfunctional allele를 normal function allele로 오분류하게 되고, 이는 부정확한 phenotype prediction을 야기한다.
  - 따라서 pharmacogenomic testing platform 개발 시 이러한 이슈들을 조심히 다루어야 한다.
---
## Pharmacogenomic Testing Methodologies
### Pharmacogenomic testing
- testing에 대한 분석 전략은 다양한 요소에 의해 결정된다.
  - 유전자의 복잡도
  - extent, frequency, type of genetic variation
  - time needed for return of the results
  
### Targeted pharmacogenomic testing
- Target Genotyping assays : PharmVar에서 제공되는 selected start allele haplotype만을 위한 test
- Rapid test result 필요 -> complexity를 제한하도록 assay를 설계한다.
- 하지만 많은 약물유전체 assay는 laboratory-developed test approach에 기반하는데, 이는 clinical testing laboratories에 의해 assay가 발전 및 검증, 수행된다.
  - 약물유전체 testing 제공하는 Clinical laboratories는 voluntary National Institute of Health Genetic Testing Registry에 있다.
- 대부분의 clinical pharmacogenomic testing은 특정 타겟 유전자와 variants들에 대한 분석이다. 
- Targeted genotyping은 직접 테스트되지 않는 variant나 allele는 인식하지 않기 때문에 negative genotyping result가 피실험체가 assay에서 보여지지 않는 또다른 variant를 가질 것이라는 가능성을 배제할 수는 없다.
  - 예를 들어, *1 result by a genotyping platform을 보고받았다 하자. 이는 targeted variants들 중 어떤 것도 인식되지 않았음을 의미하며, 그렇다고 해서 variant가 없다는 것을 의미하는 것은 아니라는 것이다.
- ACMG는 AMP(Association for Molecular Pathology), CAP(College of American Pathologists)로부터 제공된 가이드라인과 부합하도록 다음과 같은 targeted pharmacogenomic testing을 제안한다.
  - clinically relevant pharmacogene을 선택하고, 그러한 gene과 variant에 대한 선택을 뒷받침하는 evidence and rationale을 만들어라
  - 모집단에서의 allele 기능, allele 빈도와 availability of reference materials에 기반하여 clinically relevant variants들을 포함시켜라
  - test description의 targeted assay에 의해 인식된 모든 interrogated variants들을 나열하라

### Exome and genome sequencing
- ES(Exome Sequencing)-based test는 유전자의 코딩되는 부분에 대한 variant, 그리고 mRNA 스플라이싱에 영향을 줄 수도 있는 엑손과 인트론 접합 부위의 variant를 구분한다. 
- assay가 특정 non-coding variants를 인지하도록 계획된 것이 아니라면 deep intronic variants나 더 세세한 구분까지 가능하지는 않다.
- 하지만, 이는 GS(Genome Sequencing)이나 targeted next-generation sequencing-based gene panels로 이미 확인된다. 
- GS로 structural variant in drug metabolizing enzyme도 확인가능하다. 
  - 사실 GS보다는 quantative PCR이나 targeted array와 같은 gene-specific copy number assay를 더 많이 쓴다.
- 타겟 구분에 쓰이는 High throughput sequencing platform은 5'말단의 GC 반복이 많은 부분에 대해서는 한계가 있다. 
- 대부분의 연구실은 targeted pharmacogenomic testing 사용하고 있지만, 표준적 가이드라인이 없어서 조심스럽게 접근해야 한다.
- ACMG는 pharmacogenomic ES와 GS가 다음을 포함할 것을 권고하고 있다.
  - clinically relevant pharmacogenomic variants(가능하다면 haplotype인지 diplotype인지까지도)를 보고하고 이러한 gene과 variant의 선택을 뒷받침하는 evidence and rationale을 만들어라
  - assay로 인해 인식될 수 있는 SNVs나 CNVs와 같은 variant의 type을 구체화하라
  - 이러한 assay의 보고가능한 pharmacogenomic variant들과 한계를 기술하라
  
### Pharmacogene copy number variation
- Germline structural variant는 매우 다양하다. 
- Structural variant에 영향을 받는 가장 주목할 만한 약물유전체는 CYP2D6이다.
  - 22번 염색체의 CYP2D 유전자자리에 CYP2D7과 CYP2D8이 가까이 붙어있고, 이들의 감수 비대립 상동 재조합에 의해 CYP2D6 염색체 기능의 deletion, duplication, multiplication, conversion등이 발생할 수 있다.
  - 그밖에도 CYP2B6, CYP2C19, CYP2D6 CNV와 관련한 것들을 PharmVar의 gene page와 GeneFocus review에서 Structural Variation document를 통해 찾아볼 수 있다. 
- ACMG는 약물유전체의 testing과 reporting에 대하여 다음을 권고한다.
  - 적절하다고 여겨지는 임상 관련 약물유전자(그들의 star allele haplotype도 포함하여) CNV를 보고하라.
  - 가능하다면 에세이 기법을 통해 발견될 수 있는 CNV의 최소 사이즈도 기재하여라.
  - test description 과정에서 에세이 기법으로 발견될 수 있는 가능한 모든 CNV를 리스트업하라.
  - 현 지식의 단계, 복잡도, 가능성, 에세이 기법의 한계 등을 고려한다.

---
## Validation of a Clinical Pharmacogenomic Test
### Performance characteristics
- Validation 과정에서 약물유전체 플랫폼에 대한 performance characteristics를 수립해야만 한다.
- Accuracy, precision of results, analytical sensitivity and specificity, and the reportable ranges 이 performance characteristic에 포함된다.
- 최소 20개 이상의 Sample을 통해 accuracy evaluation이 이루어져야 하지만, 많을 수록 좋다.
  - Sample은 SNV, CNV 포함해서 alleles/haplotypes가 드러나야 한다.
  - Sample 수가 많을 수록 structural variant에 대한 analytical accuracy 입증에 용이해진다.

### Specimen types
- 초기 test validation은 가장 비슷한 specimen type로부터 시작되는 것이 좋다.
- 분석 과정에서 큰 변화가 없을 것 같다면, DNA source를 validate하기 위해 최소 알려진 3개의 샘플로 실행해볼 것을 권장한다.
- 상당한 변화가 예상된다면 새로운 validation for the new DNA source, in accordance with CAP requirements, is required.

### Reference materials
- genomic DNA samples were characeterized for pharmacogenes and consensus genotypes established.
- CYP2D6에 대한 대립유전자 관련 정보 보충을 위해 몇몇 프로젝트들이 노력 중
- Coriell Institute로부터 publicly available materials을 얻을 수 있다.
  
---
## Pharmacogenomic Reporting and Result Interpretation
### Pharmacogenomic reporting
- Centers for Disease Control and Prevention : 약물유전체 검증 보고는 geneticists들에게 투명성과 접근성을 보장할 수 있어야 한다.
  - Human Genome Organization Gene Nomenclature Committee 당 gene name을 포함시킨다.
  - variant's dbSNP rs identifier 포함시킨다.
  - Human Genome Variation Society nomenclature를 이용하여 sequence variant를 보고한다.
  - reference sequence를 포함시킨다.
  - test report에 variant and/or haplotype을 명시한다.
  - test로부터 발견된 variant와 haplotype을 리스트업 한다.
  - test의 limitation을 기재한다.
  - test description을 모두가 접근 가능하게 한다.
- 그 밖에도 많은 표준화 노력이 있어왔다.
- ACMG는 pharmacogenomic reporting에 대하여 다음을 권고한다.
  - Gene name 위해 HUGO Gene Nomenclature를 활용하라.
  - HGVS nomenclature를 이용하여 sequence variants를 보고하라.(dbSNP rs identifier에 대한 보고는 선택사항이다.)
  - reference sequence used to call variants를 명시하라.
  - test로부터 발견된 variant와 haplotype을 리스트업 한다.
  - test의 limitation을 기재한다.
  - test에서 발견될 수 있는 모든 variants나 haplotype들을 리스트업한다.
  - test description을 모두가 접근 가능하게 한다.

### Phenotype prediction from Pharmacogenomic test results
- Pharmacogenomic test는 patient phenotype이나 metabolizer status로 나타낸다.
- CPIC은 5가지 방안으로 drug metabolism gene을 나타낸다.
  - poor metabolizer
  - intermediate metabolizer
  - normal metabolizer(NM)
  - rapid metabolizer
  - ultrarapid metabolizer(UM)
- Phenotype prediction은 확인된 diplotype으로 구분된다.
  - 2 nonfunctional allele : poor metabolizer phenotype
  - 2 normal function or 1 decreased function allele : NM phenotype
  - 1 normal function allele with  1 nonfunctional allele or 2 decreased function allele : intermediate metabolizer phenotype
  - 3 copies of normal function allele : UM phenotype
- Example : CYP2D6 *1 /*2X2
  - total of 3 gene copies
  - CYP2D6*2 allele는 normal function을 가지므로, CYP2D6*1 allele와 중복되면 이는 UM phenotype이다.
- Example : CYP2D6 *1/*36+*10
  - total of 3 gene copies인 CNV-containing genotype
  - *36 allele는 nonfunctional allele이고 *10은 decreased functional allele이므로 NM phenotype이다.
- PharmGKB와 CPIC에서 제공하는 genotype to phenotype translation table이 있다.
- genotype to phenotype translation for certain pharmacogene(e.g. CYP2D6 and CYP2C9)를 쉽게 하기 위해 CPIC는 Phenotype Prediction을 위해 Activity Score(AS) System을 사용한다.
  - allele는 activity value에, sum of activity value = AS for the specific genotype
- ACMG는 CPIC AS system을 이용할 것을 권장한다.
  
### Clinical interpretation of pharmacogenomic variant
- 발전하고 있는 영역이고, 표준이 없다.
- ACMG는 FDA에서 발행한 pharmacogenomic tables that are stratified by level of evidence와 AMP의 recommendation을 모두 참고하여 pharmacogenomic interpretation and reporting을 할 것을 권고한다.
- 또한, FDA나 CPIC와 같이 엄밀하게 고증된 drug-gene pair resource를 활용할 것을 권장한다.
  - 적용가능한 genotype과 metabolizer phenotype을 보고하라.
  - identified genotype에 영향을 받는 medication을 반드시 리스트업하라.
  - 결과 기반하여 다른 치료법이 있다면 그것을 일반화한 statement를 제공하라.
  - actionable decision을 알려주는 resource들의 리스트를 제공하라.(FDA table이나 CPIC guideline 등)
  - 임상 약물유전체 테스트 보고서는 patient-specific dosing을 제공하면 안된다.
  - supportive evidence 기반한 FDA therapeutic management recommendations를 포함시켜라.
  - 임상약물유전체 보고서에 drug substrate와 variant에 의존하는 phenotypic prediction에 대한 accuracy를 명시하라.
  - drug-drug interaction이 metabolizer phenotype을 변형할 가능성이 있는지도 보고서에 포함시켜라.

### Examples of clinical pharmacogenomic guidelines
- Box2
- Box3
- Box4
- Box5
- Box6

---
## Conclusion
- 어렵지만, 많은 lab들이 잘 해내서 pharmacogenomic methodology를 잘 구축해봅시다.

## 어휘
- pharmacogenomic
  - 약물유전체학
- allele 
  - 대립 형질
- suballele
  - 부 대립 형질
- nomenclature
  - 명명법
- genotype
  - 유전자형
- phenotype
  - 표현형
- SNV 
  - 단일 염기 하나가 바뀐 것
- CNV
  - 복제수 변이. 유전자 특정 염기서열의 Copy number가 개체마다 차이를 보이는 현상
  - 중복 또는 삭제가 해당된다.
  
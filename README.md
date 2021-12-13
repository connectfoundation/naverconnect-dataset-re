#### This dataset is created by NAVER Connect Foundation. 

# RE (Relation Extraction)

## Overview

RE 데이터셋은 주어진 문서/문장에서 두 엔티티인 subject와 object가 정해졌을 때 그 둘 간의 관계를 파악하는 태스크(Relation Extraction)에 대한 데이터입니다.

(*해당 데이터셋은 한국어 자연어 이해 평가 벤치마크인 [KLUE](https://klue-benchmark.com/) 데이터셋의 일부이며, 기존 벤치마크와는 다름을 알립니다.*)

<br>

## 목차
1. 특징
2. 포맷
3. 각 성분에 대한 소개
4. 라이센스

<br>

## 1. 특징

RE 데이터셋의 label은 다음의 30가지 class 중 하나로 매핑되며, 이는 관계 추출에 대한 기존 연구인 [TACRED 데이터셋](https://nlp.stanford.edu/projects/tacred/)의 레이블 기준을 한국어 데이터에 맞게 재분배한 결과입니다. Subject로 활용되는 엔티티의 타입(type)은 기관(ORG) 혹은 인물(PER)이며, object로는 더욱 다양한 엔티티 타입들이 활용됩니다. 전체 레이블에는 *no_relation*도 포함됩니다.

```
no_relation(0), org:dissolved(1), org:founded(2), org:place_of_headquarters(3), org:alternate_names(4), org:member_of(5), org:members(6), org:political/religious_affiliation(7), org:product(8), org:founded_by(9),org:top_members/employees(10), org:number_of_employees/members(11), per:date_of_birth(12), per:date_of_death(13), per:place_of_birth(14), per:place_of_death(15), per:place_of_residence(16), per:origin(17), per:employee_of(18), per:schools_attended(19), per:alternate_names(20), per:parents(21), per:children(22), per:siblings(23), per:spouse(24), per:other_family(25), per:colleagues(26), per:product(27), per:religion(28), per:title(29),
 ```
 
상세한 레이블 분포는 [KLUE 논문](https://arxiv.org/abs/2105.09680)의 relation extraction 섹션에서 확인하실 수 있습니다.

<br>

## 2. 포맷

RE 데이터셋은 *.json* 형식으로 제공되며, 다음과 같은 구조를 가지고 있습니다.

```
{'guid': 'klue-re-v1_train_00000',
 'label': 0,
 'object_entity': {'word': '조지 해리슨',
  'start_idx': 13,
  'end_idx': 18,
  'type': 'PER'},
 'sentence': '〈Something〉는 조지 해리슨이 쓰고 비틀즈가 1969년 앨범 《Abbey Road》에 담은 노래다.',
 'source': 'wikipedia',
 'subject_entity': {'word': '비틀즈',
  'start_idx': 24,
  'end_idx': 26,
  'type': 'ORG'}}
  ```
  
  <br>
  
  ## 3. 각 성분에 대한 소개
 각 성분에 대한 설명 및 type은 다음과 같습니다. **굵은 글씨**로 표시된 성분들은 태스크 해결에 필수적인 요소들이며, **subject_entity**와 **object_entity** 성분은 각각 네 가지의 세부 항목을 가지고 있습니다. 알파벳 순서로 제공되는 *.json* 형식과 달리, 여기서는 실제 문제 해결에 사용되는 양상에 따라 성분들을 배열하였습니다.

|        **설명   대상**       | **데이터 타입** |                                     **설명**                                     |                                        **예시 데이터**                                        |    **비고**                                                 |
|:------------------------:|:-----------:|:----------------------------------------------------------------------------:|:-----------------------------------------------------------------------------------------:|-------------------------------------------------------------|
| **guid**                     | str         | 해당 인스턴스의 고유 아이디입니다.                                           | *'klue-re-v1_train_00000'*                                                                  |                                                             |
| source                   | str         | 문장이 발췌된 텍스트의 유형입니다.                                           | *'wikipedia'*                                                                               | 위키피디아, 정책 브리핑, 위키트리 중 하나의 소스 제공       |
| **sentence**                 | str         | 주어진 문장입니다.                                                           | *'〈Something〉는 조지 해리슨이 쓰고 비틀즈가 1969년 앨범   《Abbey Road》에 담은 노래다.'* |                                                             |
| **label**                    | int32       | 문장, subject, 그리고 object가 주어졌을 때, 이에 해당하는 관계를 나타냅니다. | 0                                                                                         | 관계 없음(no_relation)인 0을 포함하여 총 30개의 관계로 구성 |
| **subject_entity** || *{'word', 'start_idx', 'end_idx', 'type'}*|
| word      | str         | subject에 해당하는 단어입니다.                                               | *'비틀즈'*                                                                                  |                                                             |
| **start_idx** | int32       | subject 단어가 시작하는 위치를 나타냅니다.                                   | 24                                                                                        |                                                             |
| **end_idx**   | int32       | subject 단어가 끝나는 위치를 나타냅니다.                                     | 26                                                                                        |                                                             |
| type      | str         | subject의 개체명 타입이 주어집니다.                                          | *'ORG'*                                                                                     | subject의 개체명 타입으로는 PER과 ORG만 올 수 있음          |
| **object_entity** || *{'word', 'start_idx', 'end_idx', 'type'}*|  
| word       | str         | object에 해당하는 단어입니다.                                                | *'조지 해리슨'*                                                                             |                                                             |
| **start_idx**  | int32       | object 단어가 시작하는 위치를 나타냅니다.                                    | 13                                                                                        |                                                             |
| **end_idx**    | int32       | object 단어가 끝나는 위치를 나타냅니다.                                      | 18                                                                                        |                                                             |
| type       | str         | object의 개체명 타입이 주어집니다.                                           | *'PER'*                                                                                     | PER과 ORG가 아닌 다양한 개체명 타입이 올 수 있음            |

 
데이터셋 사이즈는 32,470개입니다.
 
 <br>
 
 ## 4. 라이센스
 
 [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)
 
 ### Contact
 
 작성자: 조원익 tsatsuki@snu.ac.kr

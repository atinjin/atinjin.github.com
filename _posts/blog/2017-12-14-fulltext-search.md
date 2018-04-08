---
layout: post
title: Full Text Search 해봤나요?
categories: blog
excerpt: Elasticsearc 없이 full-text search하기
tags: [fulltest, search, hibernate, tokenizer]
image:
  feature: 
comments: true
share: true
toc: true
modified: 2018-03-07T12:20:00+09:00
---

## Full-text Search
<figure class="half">
    <img src="../images/fulltextsearch.jpg">
    <figcaption>Full-text Search</figcaption>
</figure>

서점 관리 프로그램에선 책이름을 데이터 베이스에 저장하고 있습니다. 책 중에 "Refactoring: Improving the Design of Existing Code"라는 책이 있다고 한다면 사용자는 책의 정확한 제목보다는 비슷한 단어, 예를 들어 "refactor", "refactors", "refactored" , "refactoring"과 같은 단어를 사용하여 책을 찾고 싶어할 것입니다. 이와 같은 검색 기법을 “Word stemming”이라고 한다. 한국말로 “어간 추출”이다. 즉, 어근이 같은 관련 단어들을 이용하여 찾아내는 것입니다. 

Full-Text 검색은 텍스트를 다양한 방식으로 미리 분석하여 인덱싱을 해놓고 빠르게 자료를 검색해내는 기법을 말합니다. 위의 예와 같이 어근일 수도 있고, 비슷한 의미의 단어일 수도 있고, 반대말일 수도 있습니다. 한가지 공통된 특징은 텍스트를 검색 대상으로 하며, 사전에 관련 데이터를 가지고 인덱싱이 되어 있어야 한다는 것입니다.
이렇게 편리하고 강력한 기능을 지원해주는 Lucene이라는 라이브러리가 있습니다. 여기에 사용성을 더하기 위해서 ORM 프레임워크 Hibernate를 적용한 "Hibernate Search ORM"에 대해서 이야기해보려 합니다.

## Hibernate Search의 Full-text Search

Hiberanate-Search는 Lucene을 사용하여 Full-text Search 기능을 제공합니다. 가장 큰 장점은 ORM을 통해 손쉽게 설정, 인덱싱 및 쿼리가 가능하다는 것입니다. 궁합이 잘 맞는다고 할 수 있습니다.

### Lucene이란?
Full-Test 검색은 Hibernate가 지원해주는 것이 아니라 "Lucene"이라는 라이브러리를 사용하는 것입니다. 그렇기 때문에 기능을 사용하기 위해서는 먼저 Lucene이 무엇인지를 알아야 합니다.
Lucene은 인덱싱/검색 라이브러리입니다. 특징은 문자열만을 입력으로 받는다는 것이다. 문자열만을 입력으로 받기 때문에 문서 형식이 HTML,XML, PDF, Work이든 상관없이 분석이 가능합니다.

### Tokenization
Lucene은 긴 텍스트 문자열을 분석합니다. 이를 분석하기 위한 사전 작업이 바로 긴 문자열을 작은 단위로 나누는 것입니다. 나누는 작업을 “Tokenization”, 토큰화라고 합니다. 토큰을 기준으로 인덱싱을 하게 됩니다.

다음과 같은 post-tokenization을 예로 들 수 있습니다. 이런 기능들을 통해 구글에서 검색하는 것과 같은 효과를 얻을 수 있습니다.

1. *Stemming* – 어근별로 인덱싱을 하는 것입니다.  영어 기반 라이브러리가 잘 되어 있기 때문에 예를 들면 “자전거를 타다”라는 의미를 갖는 “bike”는 "bikes" 와 같이 실제 문장에서 쓰입니다. 이런 경우 “Stemming” Tokenizer는  "bike"로 바꿔서 인 덱싱합니다. can find both documents containing "bike" and those containing "bikes".
2. *Stop Words Filtering* – 의미를 이해하는데 불필요한 단어를 제거합니다. 이를 통해 인덱스 사이즈를 줄일 수 있습니다. 영어를 예를 들면  "a" , “the” 등과 같은 관사가 이런 부류에 속합니다.
3. *Text Normalization* – 영어의 경우에 쓰이는데 액센트  등과 같이 기타 정보를 표시하는 문자를 본래 문자로 변환하여 줍니다. 의미에 영향이 없는 정보를 없애는 Normalization 과정입니다.
4. *Synonym Expansion* – 유의어를 인덱스에 추가해줍니다. 유사 단어를 사용하여 검색할 수 있게 해줍니다.

### Core Analysis

Lucene의 Analyzer 클래스를 설정하여서 다양한 텍스트 인덱싱하여 검색할 수 있습니다.

1. Analyzer – 인덱싱과 검색에 쓰이는 TokenStream 을 생성해주는 기본 클래스입니다.
2. CharFilter – CharFilter 은 토큰화하기 전에 문자를 일괄적으로 변경할 때 쓰입니다. 변경된 문자와 offset(변이, 위치 차이) 값을 계산하게 됩니다. 
3. Tokenizer – 입력되는 텍스트를 Token으로 나누는 역할을 합니다. 대부분의 경우 Analyzer의 첫번째 필터로  Tokenizer를 사용합니다. (만약 사전에 변환 작업이 필요하다면 앞에 나온 CharFilter subclass 를 먼저 사용하면 됩니다.)
4. TokenFilter – A TokenFilter 는  Tokenizer.에 의해 생성된 토큰에 다음과 같은 변경을 적용할 때 쓰입니다.(deletion, stemming, synonym injection, case folding)
 
 지원하는 언어가 제한적이라는 것이 문제입니다. 그래도 한글에 대한 프로젝트들이 간간히 보입니다.
 
[한글 형태소 분석기 프로젝트](https://github.com/juncon/arirang.lucene-analyzer-5.0.0)

## Performace
실제 프로젝트에 사용하기 위해서 lucene이 기존 시스템에 미치는 영향을 분석해야 합니다.  Lucene을 적용할 경우 변경되는 사항은 바로 indexing 관련된 추가적인 Disk/CPU 사용입니다.

### Indexing File size
먼저 Storage 사용량을 측정해보았습니다.

#### Indexing Speed
- 4284.989746 documents/second
- Reindexed 10200 entities
- End indexing during 4719ms

1. Speed
  - 개발 노트북  intel i5
  - 초당 4800 (documents/sec)
2. Space (1000만건 일 경우)
  - whole re-indexing = 2083(sec) =  34분
  - 4.28MB * 1000 = 4280MB = 4.2 GB + a = 5GB
  - 20% space 증가 : Database Index 삭제시 가능(DB indexing 파일 줄어듬)
4. 적용 방안
  - reindexing은 특별한 경우에만(업데이트)
  - near-realtime indexing으로 충분
  - 실시간 이벤트의 경우 실제 DB 접근 불필요

## 예제 프로젝트
"백문이 불여일코딩"이죠. Spring boot + REST + Hibernate Search ORM 을 활용한 샘플 코드를 사용하여 간단히 테스트해 볼 수 있습니다.

https://github.com/atinjin/hibernate_search_example
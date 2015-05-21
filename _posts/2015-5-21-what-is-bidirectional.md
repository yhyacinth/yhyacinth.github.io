---
layout: post
title: bidi(Bidirectional)란 무엇인가?
categories: [general]
tags: [bidi, text, unicode]
description: 사전적 의미는 두 방향으로 움직일 수 있는 것을 말한다.
---

사전적 의미는 두 방향으로 움직일 수 있는 것을 말한다. 여기서는 텍스트의 Bidirectional에 대해 알아본다.

## Bidirectional text
텍스트에서 Bidirectional은 하나의 텍스트가 두 가지 방향성을 가지는 것을 말한다. 텍스트 방향성이란 right-to-left, left-to-right과 같이 문장을 읽고 쓰는 방향을 말한다. Bidirectional은 또한 우경식 배열(Boustrophedon; 각 줄마다 텍스트 방향성을 바꾼다.)을 가리키는데 쓰이기도 한다.

<br />
![pic](../../../../images/150521/boustrophedon.png "우경식 배열")

<우경식 문장 배열, 고대 그리스어의 예>

__boustrophedonically__: 한 방향(수평)으로 시작해서 줄의 끝에 이르면 다음 줄 부터는 방향을 반대로 바꾼다. 소가 밭을 가는 모습 같다고 하여 일본에서 우경식(牛耕式)이라는 말을 붙였다.

그리스 알파벳은 점차 LTR 패턴이 정착하게 되었다. 한 편, 아랍어와 히브리어는 RTL을 사용하게 되었다.

![pic](http://upload.wikimedia.org/wikipedia/commons/thumb/4/47/Writing_directions_of_the_world.svg/800px-Writing_directions_of_the_world.svg.png "Wikipedia")

<출처: 위키백과, 세계의 텍스트 방향성>

## 컴퓨터 프로그램의 경우
많은 컴퓨터 프로그램은 Bidirectional 텍스트를 정확히 보여주는데 실패한다. 예를 들어, 히브리어 이름 Sarah (שרה) 의 철자는, sin (ש) (가장 오른쪽에 나타난다.), 그리고 resh (ר), 마지막으로 heh (ה) (가장 왼쪽에 나타나야 한다.)가 된다. 하지만 어떤 프로그램에서는 이 히브리어 텍스트를 정 반대로 보여줄 수 있다.

## Bidirectional 문장 지원
Bidirectional 문장 지원은 컴퓨터에서 Bidirectional text를 정확히 보여주기 위한 기능이다. 이것은 종종 "BiDi" 또는 "bidi"로 줄여 말하기도 한다.

초기 컴퓨터는 오직 한 가지 쓰기 체계를 지원하도록(일반적으로 오직 라틴 알파벳의 left-to-right 기반으로) 설정되었다. 새로운 문자셋과 문자 인코딩이 추가되면서 다른 언어의 left-to-right 문장이 지원되었지만, 아랍어나 히브리어와 같은 right-to-left 문장을 지원하는 것은 쉽지 않은 일이었고, 두 가지를 섞는 것은 실용적이지도 않았다. Right-to-left 문장 지원은 문자 안에 읽기 쓰기 순서를 저장하는 ISO/IEC 8859-6 과 ISO/IEC 8859-8 같은 인코딩에서 소개되었다. 이것은 간단하게 left-to-right 표시 방향을 반대로 바꿀 수 있었지만, 대신 left-to-right 문장을 정확히 보여주는 능력을 희생하게 되었다. Bidirectional 문장 지원으로, 다른 문장이 같은 페이지에 있어도 쓰기 방향을 고려하지 않고 문장을 섞는 것이 가능해졌다.

특히, 유니코드 표준은 어떻게 RTL과 LTR이 섞인 문장을 인코딩하고 보여주는 방법에 대한 자세한 규칙과 함께 완전한 BiDi 지원을 위한 기반을 제공한다.

## 유니코드 BiDi 지원
유니코드 표준은 '논리적'으로 정렬된 문자들을 호출한다. 즉, '시각적'으로 나타나는 순서와는 대조적인 해석될 예정의 순서가 된다. 그리고, bidi 지원을 제공하기 위해, 유니코드는 논리적 문자 순서를 어떻게 정확한 시각적 표현으로 변환할 수 있는지 알고리즘을 규정했다. 이를 위해, 유니코드 인코딩 표준은 모든 문자를 네 가지 타입( 'strong', 'weak, 'neutral', 그리고 'explicit') 중 하나로 나눈다.

### 강한 문자(strong characters)
강한 문자는 명백한 방향성을 가진 것들이다. 이 문자 타입의 예는 대부분의 알파벳 문자, 음절 문자(일본어 가나가 대표적), 한자, 비 유럽 또는 비 아라비아 숫자, 문장 부호(그 문장에 고유한)를 포함한다.

### 약한 문자(weak characters)
약한 문자는 애매한 방향성을 가진 것들이다. 이 문자 타입의 예는 유럽 숫자 동 아라비아-인도 숫자, 수학 기호, 통화 기호, 많은 문장에서 일반적으로 사용되는 문장 부호(콜론, 콤마, 마침표 등) 등은 이 타입으로 떨어진다.

### 중립 문자(neutral characters)
중립 문자는 문맥이 없으면 방향성을 확정할 수 없는 문자들이다. 예를 들어 단락 구분, 탭, 스페이스 등을 포함한다.

### 명시적 포맷팅(explicit formatting)
명시적 포맷팅 문자("방향성 포맷팅 문자"라고 불리기도 한다.)는, 유니코드 알고리즘의 기본 동작에서 직접 순서를 수정할 수 있는 문자다. 이 문자들은 "marks", "embeddings", "isolates", 그리고 "overrides"로 세분화된다. 이 문자들의 효과는 단락 구분이 나오거나 "pop" 문자가 나올 때까지 지속된다.

#### marks
약한 문자가 다른 약한 문자 뒤에 오는 경우, 알고리즘은 첫번째 강한 이웃 문자를 본다. 때때로 이것은 의도하지 않은 표시 오류로 이어진다. 이러한 오류는 "의사 강한(pseudo-string)" 문자로 수정될 수 있는데, 이런 유니코드 제어 문자를 "mark" 라고 부른다. 마크 U+200E left-to-right mark, U+200F right-to-left mark 는 약한 문자가 쓰기 방향을 상속받는 위치에 삽입될 수 있다.

#### embeddings
"embedding" 방향성 포맷팅 문자는 명시적 포맷팅의 고전적인 유니코드 방식이며, 유니코드 6.3 처럼, 대신 "isolates" 를 권장하고 있다. 텍스트 일부의 "embeddings" 신호는 방향성이 다른 것으로 간주된다. embedding 포맷팅 범위 내의 문자는 주위의 텍스트와 독립적이지 않다. 또한, embedding 된 문자는 문자 바깥 순서에 영향을 줄 수 있다. 유니코드 6.3은 방향성 embedding은 대개 주위에 너무 강한 효과를 가져오며 따라서 필요 이상으로 사용하기 어렵다는 것을 밝혀냈다.

#### isolates
"isolate" 방향성 포맷팅 문자는 텍스트 일부의 방향성을 주위와 분리되면서 다르게 처리되도록 신호한다. 유니코드 6.3은 새 문서는 방향성 embedding 대신 이것을 사용하도록 권장한다. "embedding" 방향성 포맷팅 문자와는 달리 "isolate" 문자는 텍스트 범위 바깥의 순서에 영향을 주지 않는다.

#### overrides
"override" 방향성 포맷팅 문자는 부분 숫자 같은 특별한 경우를 허용한다(예를 들어 강제로 영어 숫자와 히브리어 문자를 혼합하여 RTL로 쓰게 만든다.). 그리고 가능하면 피하는 것이 좋다. "overrides"는 다른 포맷팅 안쪽에 중첩될 수 있다.

#### pops
"pop" 방향성 포맷팅 문자는 가장 최근 "embeddings", "overrides", "isolates"의 효과를 종료한다.

#### runs
알고리즘에서, 인접한 강한 문자들의 각 연속을 "run"이라고 부른다. 약한 문자가 두 같은 방향의 강한 문자의 사이에 위치해 있으면 그 방향을 상속받는다. 약한 문자가 두 다른 방향의 강한 문자의 사이에 위치해 있으면 주 문맥의 방향(LTR 문서의 문자는 LTR이 되고, RTL 문서의 문자는 RTL이 된다.)을 상속받는다.

### Table of BiDi-types
http://www.unicode.org/reports/tr9/#Directional_Formatting_Codes 참조

## 참조
- http://en.wikipedia.org/wiki/Bi-directional_text
- http://www.unicode.org/reports/tr9/ UNICODE BIDIRECTIONAL ALGORITHM


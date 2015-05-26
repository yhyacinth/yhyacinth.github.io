---
layout: post
title: 유니코드에 대해
categories: [general]
tags: [unicode]
description: 이 문서를 주의 깊게 읽으면 유니코드에 대한 이해를 크게 높일 수 있을 것입니다.
---

_이 문서를 주의 깊게 읽으면 유니코드에 대한 이해를 크게 높일 수 있을 것입니다._

## 유니코드 개요
> Unicode provides a unique number for every character,
> no matter what the platform,
> no matter what the program,
> no matter what the language.
>
> http://www.unicode.org/standard/WhatIsUnicode.html 

유니코드는 전 세계 모든 문자에 대해 플랫폼에 상관 없이, 프로그램에 상관 없이, 언어에 상관 없이 컴퓨터에서 일관되게 표현하고 다룰 수 있도록 설계된 산업 표준이다. 유니코드  컨소시엄에서 제정하며 유니코드 표준에는 ISO 10646 문자 집합, 문자 인코딩 방법, 문자 정보 데이터베이스, 문자들을 다루기 위한 알고리즘 등을 포함하고 있다.

유니코드의 목적은 현존하는 문자 인코딩 방법들을 모두 유니코드로 교체하려는 것이다. 기존의 인코딩들은 그 규모나 범위 면에서 한정되어 있고, 다국어 환경에서는 서로 호환되지 않는 문제점이 있었다. 유니코드가 다양한 문자 집합들을 통합하는 데 성공하면서 유니코드는 컴퓨터 소프트웨어의 국제화와 지역화에 널리 사용되게 되었다.

모든 문자들의 코드 값은 문자 코드표에서 확인할 수 있다.
http://www.unicode.org/charts/ 

### 버전
 - Unicode 1.0.0 - 1991년 10월
 - ...
 - Unicode 6.0 - 2010년 10월 11일
 - Unicode 6.1 - 2012년 2월 1일
 - Unicode 6.2 - 2012년 9월 27일
 - Unicode 6.3 - 2013년 9월 30일
 - Unicode 7.0 - 2014년 6월 16일

### 유니코드 평면
유니코드는 110만개 이상의 코드 포인트를 지정할 수 있다. 유니코드는 110만개 이상의 코드 포인트를 17개의 '평면(Plane)'으로 나누고 각 평면에서 256*256=65,536개의 문자를 지정할 수 있다. 0번 평면은 일반적으로 BMP(Basic Multilingual Plane)라고 하는 평면으로 BMP에는 거의 모든 근대 문자와 특수 문자가 포함되어 있으며, 그 중 대부분은 한글과 한중일 통합 한자들로 이루어져 있다.

![pic](../../../../images/150518/500px-Roadmap_to_Unicode_BMP.svg.png "BMP")

![pic](../../../../images/150518/bb688113.f03tm07(ko-kr).jpg "BMP")

< BMP(평면 0)의 유니코드 인코딩 배치 >

1번 평면은 보조 다국어 평면(Supplementary Multilingual Plane, SMP)으로 옛 문자나 음악 기호, 수학 기호 등에 쓰인다.

2번 평면은 보조 상형 문자 평면(Supplementary Ideographic Plane, SIP)으로 초기 유니코드에 포함되지 않은 한중일 통합 한자를 주로 담고 있다.

3번 평면인 3차 상형 문자 평면(Tertiary Ideographic Plane, TIP)은 갑골 문자, 금문, 소전 따위의 문자나 추가 한중일 통합 한자, 기타 옛 상형 문자 등을 위해 예약된 영역이다. 2015년 현재 3번 평면에는 아무 문자도 지정되지 않았다.

미지정 평면. 유니코드 4번 평면부터 13번 평면에는 2014년 현재 아무 문자나 기호도 지정되지 않았다.

14번 평면인 보조 특수 목적 평면(영어: Supplementary Special-purpose Plane, SSP)에는 2010년 현재 적은 수의 제어용 문자들이 들어 있다.

15번과 16번 두 평면은 사용자 영역으로, 특정 업체나 사용자 별로 할당하여 쓰게 되므로 소프트웨어간이나 글꼴간의 호환성이 보장되지 않는다.

### 유니코드의 인코딩 방식들
유니코드의 표현 방식은 유니코드 컨소시엄과 ISO 10646에 정의되어 있다. 대표적인 인코딩 방식은 UCS-2, UTF-8, UTF-16이 있다.

(UTF - Unicode Transformation Format, UCS - Universal Character Set)

## UCS
UCS는 ISO/IEC 10646으로 정의된 문자 인코딩의 국제 표준이다. UCS는 110만 개 이상의 코드가 있지만 일반적으로 첫 65535개(Basic Multilingual Plane, BMP, 기본 다국어 평면)만이 사용된다. 그리고 많은 코드 영역, 심지어 BMP 영역에서도 서로 다른 인코딩 형태와 미래의 확장성을 고려하여, 일부러 문자를 할당하지 않았다.

UCS-2는 초기 유니코드 표현 방식 중 하나로 각 문자들을 0 ~ 65535(0xFFFF) 사이의 코드 값으로 매겨놓고, 각 문자를 두 바이트로 표현한다. BMP 코드 영역만 표현할 수 있고, BMP 밖의 영역은 표현이 불가능하다. UCS-2를 확장하여 BMP 밖의 영역도 표시가 가능하게 한 인코딩으로 UTF-16이 있다.

UCS-4는 0xFFFFFFFF 까지의 코드 즉 4 바이트로 한 문자를 표현한다. 유니코드 값(코드 포인트)를 그대로 32비트로 표현한다. UTF-32도 같은 방식을 사용하는 인코딩이며 따라서 __USC-4와 UTF-32는 같다.__

## UTF-16
UTF-16은 기본 다국어 평면(BMP)에 해당하는 문자들은 그대로 16비트 값으로 인코딩된다. 이 때 인코딩된 바이트 스트링의 엔디언만 조심하면 된다. 그리고 BMP에 포함되지 않는 문자들은 특별히 정해진 방식으로 32비트 인코딩된다. 

그 자세한 방식은 다음과 같다.

BMP를 벗어나는 문제는 서러게이트(Surrogate) 문자 영역에 해당하는 두 개의 16비트 문자로 변환되어 한 쌍(즉 32비트)이 그 문자를 나타내게 된다. 유니코드의 기본 다국어 평면에 문자가 전혀 배정되어 있지 않은 영역이 2군데가 있는데 하나는 110110으로 시작하는 영역으로 U+D800부터 U+DB7F까지이고 다른 하나는 110111으로 시작하는 영역으로 U+DC00부터 U+DFFF까지의 영역이다. 전자는 High Surrogate 영역, 후자는 Low Surrogate 영역이라고 부른다. 따라서 UTF-16에서 110110이나 110111로 시작하는 경우 기본 다국어 평면 이외 문자라고 확신할 수 있을 것이다.

다음 같은 BMP 범위를 벗어나는 문자가 있다.


    Bit
    31            24|23           16|15            8|7             0|
    +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
    |0 0 0 0 0 0 0 0|0 0 0 z z z z z|x x x x x x y y|y y y y y y y y|
    +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

1) 가장 앞에서부터 110110을 붙인다.
2) 그 뒤에 z z z z z에서 1을 뺀 ZZZZ을 붙인다.
3) x x x x x x 를 붙인다. 여기까지 High-Surrogate가 된다.

    |15            8|7             0|
    +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
    |1 1 0 1 1 0 Z Z|Z Z x x x x x x|
    +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

4) 가장 앞에서부터 110111을 붙인다.
5) 나머지 y y y y y y y y y y를 붙인다. 여기가 Low-Surrogate가 된다.

    |15            8|7             0|
    +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
    |1 1 0 1 1 1 y y|y y y y y y y y|
    +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

이같이 두 개의 서러게이트 문자를 구성하는 방법으로 U+10FFFF 까지의 문자를 인코딩할 수 있다.

## UTF-8
UCS와 UTF-16의 문제점은 지나치게 많은 공간이 필요하다는 점과 기존 ASCII 체계와 호환성이 없다는 점이다. 첫 번째 문제는 컴퓨터 상에 존재하는 많은 글자들이 1바이트로 표현할 수 있는 글자들인데 이 글자들에 2바이트를 사용하는 것은 너무 낭비라는 지적이다. 두 번째 문제는 UCS-2나 UTF-16과 호환성을 위해서 기존 문서들을 모두 변환해야하는데 이 역시 문제라는 지적이다. 이 두 가지 문제를 동시에 해결하는 인코딩 방식이 UTF-8이다.

UTF-8은 켄 톰슨과 롭 파이크가 만든 가변 길이 문자 인코딩 방식이다. 본래 FSS-UTF(File System Safe UCS/Unicode Transformation Format)이란 이름으로 제안되었다.

UTF-8 인코딩은 유니코드 한 문자를 나타내기 위해 1바이트에서 4바이트까지를 사용한다. U+0000부터 U+007F범위에 있는 ASCII 문자는 UTF-8에서 1바이트 만으로 표시된다. 7비트 이상이 필요한 글자들은 다음 방식으로 바이트 수를 늘려간다.


    U+ 0 0 0 0 0 y y y | y y x x x x x x 의 글자들은 UTF-8 | 1 1 0 y y y y y | 1 0 x x x x x x |
    U+ z z z z y y y y | y y x x x x x x 의 글자들은 UTF-8 | 1 1 1 0 z z z z | 1 0 y y y y y y | 1 0 x x x x x x |
    U+ 0 0 0 w w w z z | z z z z y y y y | y y x x x x x x 의 글자들은 UTF-8 | 1 1 1 1 0 w w w | 1 0 z z z z z z | 1 0 y y y y y y | 1 0 x x x x x x |

첫 바이트는 110 또는 1110, 11110 으로 시작하고, 나머지 바이트는 10으로 시작한다.

결과적으로 첫 128 문자는 1바이트로 표시되고, 그 다음 1920 문자(발음 기호가 붙은 라틴 문자, 그리스 문자, 키릴 문자, 콥트 문자, 아르메니아 문자, 히브리 문자, 아랍 문자)는 2바이트로 표시되며, 나머지 문자들 중 BMP 안에 들어있는 것은 3바이트, 아닌 것은 4바이트로 표시된다. 

위 패턴을 사용하면 더 큰 코드 범위를 표시할 수도 있다. 원래 UTF-8은 6바이트까지의 코드 범위를 표현할 수 있었으나 2003년 11월 RFC 3629에서 유니코드에서 실제로 정의하는 U+10FFFF 까지의 글자만 표시할 수 있도록 제한하였다.

## 유니코드 정규화
### 개요
유니코드 정규화(Unicode normalization 또는 Unicode equivalence)는 모양이 같은 문자가 여러 개 있을 경우, 이를 기준에 따라 하나로 통합해주는 일을 가리킨다. 예를 들어 유니코드는 미리 합쳐진(precomposed) 문자와 따로 결합하는(combining) 문자가 공존하고 있다(예: 한글 자모 영역 [ㅎㅏㄴ]과 한글 음절 영역 [한]). 그리고 각 나라 마다 같은 한자에 다른 코드 값을 가지고 있다(한국어 亮 U+F977, CJKV 통합 한자 亮 U+4EAE). 이들을 적절한 방법으로 정규화하지 않으면 여러가지 문제가 생겨날 수 있다.

유니코드 정규화에 대한 건조한 레퍼런스 http://www.unicode.org/reports/tr15/

### 정규화 형태 Normalization Forms (NF)
| Form | Description |
| ---- | ---- |
| Normalization Form D (NFD) | 정준 분해 Canonical Decomposition |
| Normalization Form C (NFC) | 정준 분해한 뒤에, 다시 정준 결합 Canonical Decomposition, followed by Canonical Composition |
| Normalization Form KD (NFKD) | 호환 분해 Compatibility Decomposition |
| Normalization Form KC (NFKC) | 호환 분해한 뒤, 다시 정준 결합 Compatibility Decomposition, followed by Canonical Composition |

#### NFD
코드를 정준 분해한다.

 * 발음 구별 기호가 붙은 글자가 하나로 처리되어 있을 경우, 이를 기호별로 나눈다.
 * 한글을 한글 음절 영역(U+AC00~U+D7A3)으로 썼을 경우, 이를 첫가끝 코드로 나눈다.
 * 표준과 다른 조합 순서를 제대로 정렬한다.

예)

 * À (U+00C0) → A (U+0041) + ̀ (U+0300)
 * 위 (U+C704) → ㅇ (U+110B) + ᅱ (U+1171)

#### NFC
코드를 정준 분해한 뒤에, 다시 정준 결합한다.

 * 발음 구별 기호가 붙었을 경우, 이를 코드 하나로 처리한다.
 * 한글을 첫가끝 코드로 썼을 경우, 이를 한글 음절 영역(U+AC00~U+D7A3)으로 처리한다.

예)

 * A (U+0041) + ̀ (U+0300) → À (U+00C0)
 * ᄋ (U+110B) + ᅱ (U+1171) → 위 (U+C704)

#### NFKD
코드를 호환 분해한다.

 * 합자 처리된 알파벳 코드를 각 알파벳으로 분해한다.
 * 옛 알파벳을 현대 알파벳으로 바꾼다.
 
예)

 * ﬁ (U+FB01) → f (U+0066) + i (U+0069)

#### NFKC
코드를 호환 분해한 뒤에 다시 정준 결합한다.

 * 발음 구별 기호가 있는 옛 알파벳을 현대 알파벳으로 바꾼다.

예)

 * ẛ (U+1E9B) → ṡ (U+1E61)
 
#### 모든 기준에서 공통된 정규화 처리
* 한중일 호환 한자를 한중일월 통합 한자로 처리한다.
* 전용 기호를 모양이 같은 보편적인 기호로 바꾼다.

예)

 * 樂 (U+F914), 樂 (U+F95C), 樂 (U+F9BF) → 樂 (U+6A02)
 * Ω (U+2126, 옴) → Ω (U+03A9, 오메가)

#### 요약

1. NFD, NFKD를 거쳐서 최대한 분해한다.
2. 가능한 모든 비결합 문자와 뒤에 따라 오는 결합 문자, 그리고 그 뒤에 따라오는 비결합 문자에 대해 순서대로 결합을 시도한다.
3. 결합이 성공하면 뒤의 문자는 지우고 앞의 문자를 결합된 문자로 바꾼다. 이전에 실패한 결합은 다시 시도하지 않는다.
4. 결합을 시도할 때는 일반 분해 매핑의 역변환만 시도한다(예외도 있다.).

### 각 언어의 정규화 방법
#### Java
    import java.text.Normalizer;
    public class NormalizerTest {
        public static void main(String args[]) {
            String ui = "위";
            String nfd = Normalizer.normalize(ui, Normalizer.Form.NFD);
            String nfc = Normalizer.normalize(nfc, Normalizer.Form.NFC);
        }
    }
    
    => ui = U+C704
    => nfd = U+110B + U+1171
    => nfc = U+C704
    
#### Perl
    #!/usr/bin/perl
    use utf8;
    use Unicode::Normalize;
    
    my $ui = "위";
    my $nfd = NFD("위");
    my $nfc = NFC($nfd);
    
#### C#&nbsp;
    using System;
    using System.Text;
    
    string s1 = new String( new char[] { '\uC704' }
    string s2 = null;
    
    s1.IsNormalized();
    s1.IsNormalized(NormalizationForm.FormD));
    // False
    // False
    
    // Normalize to the default form(Form C)
    s2 = s1.Normalize();
    s2.IsNormalized(); // True
    
    // Normalize to Form D
    s2 = s1.Normalize(NormalizationForm.FormD);
    s2.IsNormalized(NormalizationForm.FormD)); // True
    
#### C++
    const int maxIterations = 10;
    LPWSTR strInput = L"위";
    LPWSTR strResult = NULL;
    HANDLE hHeap = GetProcessHeap();

    int iSizeEstimated = NormalizeString(NormalizationD, strInput, -1, NULL, 0);
    for (int i = 0; i < maxIterations; i++)
    {
        if (strResult)
            HeapFree(hHeap, 0, strResult);
        strResult = (LPWSTR)HeapAlloc(hHeap, 0, iSizeEstimated * sizeof (WCHAR));
        iSizeEstimated = NormalizeString(NormalizationD, strInput, -1, strResult, iSizeEstimated);
 
        if (iSizeEstimated > 0)
            break; // success 
    }    
    TRACE(L"%x", strInput[0]);
    TRACE(L"%x", strResult[0]);
    TRACE(L"%x", strResult[1]);
    
    => strInput = U+C704
    => strResult = U+110B + U+1171
    
Windows Vista >= only
https://msdn.microsoft.com/en-us/library/windows/desktop/dd319093(v=vs.85).aspx


## BOM
바이트 순서 표식(Byte Order Mark, BOM)은 유니코드에서 엔디언을 구별하기 위해 사용되는 문자로, 문자 값은 U+FEFF 이다.

유니코드 인코딩에서 문제가 되는 것은 바이트 순서 또는 엔디언이다. 즉 'A'를 00 48로 표현할 것인가 48 00으로 표현할 것인가? UTF-16, UTF-32 같은 인코딩에서는 엔디언의 종류에 따라 문자열의 값이 완전히 달라지므로, 문자열의 엔디언을 구별할 수 있는 표식이 필요하다. 이에 따라 유니코드 문자열 앞에 BOM 문자를 붙여, 엔디언을 구별한다.

UTF-8의 경우에는 엔디언 문제가 일어나지 않으므로 BOM을 붙여야 할 필요는 없다. 하지만 해당 자료가 UTF-8 인코딩이라는 표식으로 사용하는 경우도 있다. 특히 마이크로소프트의 많은 문서 편집기는 UTF-8 로 저장할 경우 자동으로 문서의 가장 앞부분에 BOM을 추가한다. 이와는 반대로 유닉스 계열 문서 편집기는 BOM을 사용하지 않는 경우가 보통이다. 이 경우 문서의 BOM을 잘못 인식하고 문제가 발생할 수도 있다.

각 유니코드 인코딩 방법에 따른 BOM 값은 다음과 같다.

BOM Table

| Encoding | Representation |
| ---- | ---- |
| UTF-8 | EF BB BF |
| UTF-16 빅 엔디언 | FE FF |
| UTF-16 리틀 엔디언 | FF FE |
| UTF-32 빅 엔디언 | 00 00 FE FF |
| UTF-32 리틀 엔디언 | FF FE 00 00 |
| SCSU | 0E FE FF |
| UTF-EBCDIC | DD 73 66 73 |
| BOCU-1 | FB EE 28 |


참조
----
- https://msdn.microsoft.com/ko-kr/goglobal/bb688113.aspx
- http://ko.wikipedia.org/wiki/UTF-16
- http://ko.wikipedia.org/wiki/바이트_순서_표식
- http://heyjimin.tistory.com/15
- https://msdn.microsoft.com/en-us/library/windows/desktop/dd374126(v=vs.85).aspx Using Unicode Normalization to Represent Strings
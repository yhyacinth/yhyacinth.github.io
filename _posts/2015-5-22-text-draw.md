---
layout: post
title: 프로그램 텍스트 출력 방법들
categories: [general]
tags: [text, library]
description: 몇 가지 많이 사용하는 텍스트 렌더링, 레이아웃 라이브러리가 있다.
---

## Win32 API
### LOGFONT structure
LOGFONT는 논리적 폰트의 특성을 정의한다.

    typedef struct tagLOGFONT {
      LONG  lfHeight;
      LONG  lfWidth;
      LONG  lfEscapement;
      LONG  lfOrientation;
      LONG  lfWeight;
      BYTE  lfItalic;
      BYTE  lfUnderline;
      BYTE  lfStrikeOut;
      BYTE  lfCharSet;
      BYTE  lfOutPrecision;
      BYTE  lfClipPrecision;
      BYTE  lfQuality;
      BYTE  lfPitchAndFamily;
      TCHAR lfFaceName[LF_FACESIZE];
    } LOGFONT, *PLOGFONT;

| 플래그 | 설명 |
| ---- | ---- |
| lfHeight | 글꼴 높이 |
| lfWidth | 글꼴 너비 |
| lfEscapement | 출력 각도 |
| lfOrientation | 각도 기준선 |
| lfWeight | 글꼴 굵기 |
| lfItalic | 이탤릭 여부 |
| lfUnderline | 밑줄 여부 |
| lfStrikeOut | 취소선 여부 |
| lfCharSet | 문자셋 |
| lfOutPrecision | 출력 정밀도 |
| lfClipPrecision | 클리핑 정밀도 |
| lfQuality | 출력 품질 |
| lfPitchAndFamily | 글꼴 Pitch 및 패밀리 |
| lfFaceName | 글꼴 이름 |
    
### TEXTMETRIC structure
TEXTMETRIC은 물리적 폰트 정보를 정의한다.

    typedef struct tagTEXTMETRIC {
      LONG  tmHeight;
      LONG  tmAscent;
      LONG  tmDescent;
      LONG  tmInternalLeading;
      LONG  tmExternalLeading;
      LONG  tmAveCharWidth;
      LONG  tmMaxCharWidth;
      LONG  tmWeight;
      LONG  tmOverhang;
      LONG  tmDigitizedAspectX;
      LONG  tmDigitizedAspectY;
      TCHAR tmFirstChar;
      TCHAR tmLastChar;
      TCHAR tmDefaultChar;
      TCHAR tmBreakChar;
      BYTE  tmItalic;
      BYTE  tmUnderlined;
      BYTE  tmStruckOut;
      BYTE  tmPitchAndFamily;
      BYTE  tmCharSet;
    } TEXTMETRIC, *PTEXTMETRIC;

| 플래그 | 설명 |
| ---- | ---- |
| tmHeight | 문자의 높이.(tmAscent와 tmDescent를 더한 값) |
| tmAscent | 기준 선의 윗쪽 높이 |
| tmDescent | 기준 선의 아래쪽 높이 |
| tmInternalLeading | tmHeight 안쪽의 여백 공간. 이 부분은 여백이며 실제 폰트가 그려지는 부분이 아니므로 문자열 출력에 의해 변경되지 않는 영역이다. 폰트 디자이너는 이 값을 0으로 설정해야 한다. |
| tmExternalLeading | tmHeight에는 포함되지 않는 여백. 문자열간의 줄간을 띄울 때 사용하는 부분. 실제 폰트가 그려지는 부분이 아니므로 문자열 출력에 의해 변경되지 않는다. |
| tmAveCharWidth | 문자들의 평균 폭 |
| tmMaxCharWidth | 최대 문자 폭 |
| tmWeight | 폰트의 두께 |
| tmOverhang | 볼드, 이탤릭 등의 강조에 의해 추가되는 여분의 폭. GDI는 이탤릭체 등과 같이 좌우로 좀 더 큰 폭을 가져야 하는 문자열을 출력할 때 원래 문자폭에 약간의 여분을 더 준다. 이 여분의 폭을 Overhang이라 한다. |
| tmDigitizedAspectX | 폰트가 만들어진 장치의 수평 종횡비 값 |
| tmDigitizedAspectY | 폰트가 만들어진 장치의 수직 종횡비 값. 수평, 수직 종횡비 값의 비. |
| tmFirstChar | 폰트에 정의된 첫 번째 문자 |
| tmLastChar | 폰트에 정의된 마지막 문자 |
| tmDefaultChar | 폰트에 정의되지 않은 문자를 출력할 때 사용되는 디폴트 문자. 보통 마침표나 사각박스가 사용된다. |
| tmBreakChar | 자동 개행과 justification에 사용되는 구분 문자. 보통 스페이스이다. |
| tmItalic | 이탤릭 스타일이 있으면 0이 아닌 값을 가진다. |
| tmUnderlined | 밑줄 스타일이 있으면 0이 아닌 값을 가진다. |
| tmStruckOut | 취소선 스타일이 있으면 0이 아닌 값을 가진다. |
| tmPitchAndFamily | 피치와 패밀리 |
| tmCharSet | 문자 셋 |

<br />
예를 들어 TEXTMETRIC을 구해 폰트의 정확한 높이를 계산해서 정확한 줄간을 띄울 수 있다.

### NEWTEXTMETRIC structure
NEWTEXTMETRIC은 물리적 폰트 정보를 정의한다.

    typedef struct tagNEWTEXTMETRIC {
    ...
    // TEXTMETRIC과 동일
      DWORD ntmFlags;
      UINT  ntmSizeEM;
      UINT  ntmCellHeight;
      UINT  ntmAvgWidth;
    } NEWTEXTMETRIC, *PNEWTEXTMETRIC;
    
### 차이
TEXTMETRIC은 폰트의 물리적인 정보를 가지고 있다. LOGFONT는 논리적인 정보를 가지고 있다. LOGFONT의 거의 모든 멤버를 TEXTMETRIC은 포함하고 있으며 TEXTMETRIC의 멤버와 기능이 LOGFONT보다 훨씬 많아 세세한 걸 다룰 수 있다. 간단한 제어를 할 때는 보통 LOGFONT를 사용하지만 세밀한 제어를 요구하면 TEXTMETRIC을 사용한다. TEXTMETRIC은 non-TrueType 폰트를 위한 구조체고 NEWTEXTMETRIC은 TrueType 폰트를 위한 구조체이다. NEWTEXTMETRIC은 TEXTMETRIC에서 네 가지 필드가 추가되었다.

## 텍스트 렌더 라이브러리
텍스트 렌더 라이브러리는 Win32 API TextOut으로 출력한 것과 효과는 유사하지만 출력 과정은 많이 다르다. 렌더 라이브러리는 폰트 파일을 뒤져 글자 모양을 찾고 외곽선을 추출한다. 그리고 해상도를 고려한 확대 배율을 적용하여 비트맵으로 바꾼 후 화면에 출력한 것이다. 안티 앨리어싱도 적용하여 배경과 글자가 부드럽게 조화를 이룬다. 텍스트에서 글리프 인덱스와 위치 포지션들의 집합으로 변환하는 것은 매우 어려운 작업이고 최선의 방법은 외부 라이브러리를 사용하는 것이다.

### FreeType
- http://freetype.org/ 
- 트루 타입, 오픈 타입, Type 1 등 다양한 폰트 파일로부터 글리프 정보를 추출하는 저수준의 폰트 분석 라이브러리
- 공개된 라이브러리이며 현재 최신 버전은 2.5.5 (2014-12-30)

http://www.soen.kr/lecture/library/freetype/freetype.htm

### Pango
- http://www.pango.org/
- 텍스트 레이아웃 및 렌더링 라이브러리
- 텍스트 레이아웃이 필요한 어느 곳에서나 통합될 수 있다(예: Cairo).

### Cairo
- http://cairographics.org/
- 벡터 그래픽 라이브러리
- 텍스트 처리는 내부적으로 Pango를 사용한다.

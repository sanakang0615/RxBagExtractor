# RxBagExtractor

RxBagExtractor 약봉투 사진을 OCR로 읽은 뒤, 해당 텍스트에서 약물명 관련 텍스트를 추출하는 파이썬 라이브러리입니다. 한글로 작성된 처방전 텍스트 처리에 최적화되어 있습니다. 

## Features

- **텍스트 필터링**: OCR로 읽은 텍스트에서 사용자가 지정한 정규 표현식에 따라 불필요한 텍스트를 제거합니다.
- **약물 이름 추출**: 주어진 텍스트에서 약물 이름만을 추출하는 기능을 제공합니다.

## Installation

```bash
pip install RxBagExtractor
```
## Usage

### Required Parameter

-   `ocr_text`: OCR로 읽은 후 얻은 텍스트로, 각 줄이 엔터로 구분된 긴 문자열입니다.

### Optional Parameters

-   `stopwords_customize`: 기본 불용어 리스트 외에 추가적으로 필터링하고 싶은 단어들을 문자열 리스트로 입력할 수 있습니다.
-   `patterns_exact_customize`: OCR 텍스트의 각 줄에서 정확히 매치되어야 할 정규 표현식을 포함하는 리스트. 각 항목은 `re.compile(r"정규표현식")` 형식으로 입력됩니다.
-   `patterns_include_customize`: OCR 텍스트의 각 줄에 이 정규표현식이 포함되어 있으면 해당 줄을 삭제합니다. `re.compile(r"정규표현식")` 형식으로 입력됩니다.

## Example
``` python
from RxBagExtractor import extractor

# 약봉투 사진에 대한 OCR 결과 텍스트
ocr_text = "여기에 OCR로 읽은 텍스트 입력"

# Parameter 정의
stopwords_customize = ['유아용', '방문시']
patterns_exact_customize = [re.compile(r"^\d{4}-\d{2}-\d{2}$")]
patterns_include_customize = [re.compile(r"^\d+-\d+-\d+$")]

# 함수 실행
result = extractor(ocr_text, stopwords_customize, patterns_exact_customize, patterns_include_customize)
print(result)
```
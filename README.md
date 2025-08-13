# extract-hwp

한글과컴퓨터의 HWP 파일(HWP 5.0 및 HWPX 형식)에서 텍스트를 추출하는 Python 라이브러리입니다.

## 특징

- **다중 포맷 지원**: HWP 5.0 (OLE) 및 HWPX (ZIP/XML) 파일 모두 지원
- **암호화 파일 감지**: 처리하기 전에 암호로 보호된 파일을 감지
- **구조화된 추출**: 텍스트 추출 시 단락 구조 보존
- **견고한 오류 처리**: 손상되거나 잘못된 파일에 대한 방어적 처리
- **유니코드 지원**: 한글 및 다국어 텍스트 완전 지원

## 설치

```bash
pip install extract-hwp
```

## 사용법

### 기본 사용법

```python
from extract_hwp import extract_text_from_hwp

# HWP 또는 HWPX 파일에서 텍스트 추출
text, error = extract_text_from_hwp("document.hwp")
if error is None:
    print(text)
else:
    print(f"오류: {error}")
```

### 포맷별 추출

```python
from extract_hwp import extract_text_from_hwpx, extract_text_from_hwp5

# HWPX 파일 전용
hwpx_text = extract_text_from_hwpx("document.hwpx")

# HWP 5.0 파일 전용
hwp5_text = extract_text_from_hwp5("document.hwp")
```

### 암호화 파일 감지

```python
from extract_hwp import is_hwp_file_password_protected

if is_hwp_file_password_protected("document.hwp"):
    print("파일이 암호로 보호되어 있습니다.")
else:
    text, error = extract_text_from_hwp("document.hwp")
```

## API 참조

### 핵심 함수

#### `extract_text_from_hwp(filepath)`

HWP/HWPX 파일에서 텍스트를 추출합니다 (통합 인터페이스).

**매개변수:**
- `filepath` (str): HWP 또는 HWPX 파일 경로

**반환값:**
- `tuple`: (추출된_텍스트, 오류_메시지). 성공시 오류_메시지는 None

**예외:**
- `FileNotFoundError`: 파일을 찾을 수 없음
- `PermissionError`: 파일 접근 권한이 없음
- `ValueError`: 지원하지 않는 파일 형식

### 포맷별 함수

#### `extract_text_from_hwpx(hwpx_file_path)`

HWPX 파일에서 텍스트를 추출합니다.

**매개변수:**
- `hwpx_file_path` (str): HWPX 파일 경로

**반환값:**
- `str`: 추출된 텍스트 (오류 시 빈 문자열)

#### `extract_text_from_hwp5(filepath)`

HWP 5.0 (OLE) 파일에서 텍스트를 추출합니다.

**매개변수:**
- `filepath` (str): HWP 파일 경로

**반환값:**
- `str`: 추출된 텍스트 (오류 시 빈 문자열)

### 암호화 감지 함수

#### `is_hwp_file_password_protected(filepath)`

HWP/HWPX 파일이 암호로 보호되어 있는지 확인합니다.

**매개변수:**
- `filepath` (str): 확인할 파일 경로

**반환값:**
- `bool`: 암호로 보호된 경우 True, 그렇지 않으면 False

## 지원 포맷

### HWP 5.0 (OLE 포맷)
- 확장자: `.hwp`
- 구조: OLE 복합 문서 형식
- 압축: zlib 압축 지원
- 특징: 바이너리 구조 분석을 통한 텍스트 추출

### HWPX (ZIP/XML 포맷)
- 확장자: `.hwpx`
- 구조: XML 문서가 포함된 ZIP 아카이브
- 특징: 구조화된 텍스트 추출을 위한 XML 파싱

## 의존성

- `olefile>=0.46`: HWP 5.0 OLE 파일 처리

## 개발

### 개발 환경 설정

```bash
# 저장소 복제
git clone https://github.com/thlee/extract-hwp.git
cd extract-hwp

# 의존성 설치
uv sync

# 개발 의존성 포함 설치
uv sync --extra dev
```

### 테스트

```bash
# 테스트 실행
pytest

# 커버리지 포함
pytest --cov=src/extract_hwp
```

### 코드 품질

```bash
# 코드 포맷팅
black src/ tests/

# 타입 검사
mypy src/
```

## 라이선스

BSD 3-Clause License - 자세한 내용은 [LICENSE](LICENSE) 파일을 참조하세요.

## 변경사항

버전 히스토리는 [CHANGELOG.md](CHANGELOG.md)에서 확인할 수 있습니다.
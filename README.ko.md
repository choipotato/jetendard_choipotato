# JetBrainsMono Potato

JetBrainsMono Potato는 **프로그래밍 리거처가 없는 한글 고정폭 폰트**입니다.

구성은 다음과 같습니다.

- **JetBrains Mono NL 2.304**: 영문/숫자/기호/코드 글리프
- **Pretendard 1.3.9**: 한글/CJK 글리프
- **JetBrainsMono Nerd Font Mono**: Nerd Font 심볼만 가져옴

핵심은 Nerd Font 쪽의 GSUB/프로그래밍 리거처를 가져오지 않는다는 점입니다.
기본 라틴 폰트는 공식 `JetBrainsMonoNL`을 사용하고, Nerd Font에서는 기본 폰트에 없는 인코딩된 심볼 글리프만 복사합니다.

한글/CJK 폭은 영문 고정폭의 정확히 2칸으로 맞추며 기본 시각 배율은 `1.15`입니다.

## 생성되는 폰트 패밀리

```text
JetBrainsMono Potato
```

대표 파일:

```text
fonts/ttf/JetBrainsMonoPotato-Regular.ttf
fonts/ttf/JetBrainsMonoPotato-Italic.ttf
fonts/ttf/JetBrainsMonoPotato-Bold.ttf
fonts/ttf/JetBrainsMonoPotato-BoldItalic.ttf
```

Thin부터 ExtraBold까지 upright/italic 전체 16개 변형을 빌드할 수 있습니다.

## 빌드

요구 사항:

- Python 3.12+
- `uv`

```bash
uv sync --all-groups
make download
make run
make test
```

`make download`은 필요한 업스트림 폰트를 자동으로 받습니다.

현재 고정 버전:

- JetBrains Mono: **2.304**
- Nerd Fonts: **v3.4.0**
- Pretendard: **1.3.9**

생성 위치:

- `fonts/ttf/JetBrainsMonoPotato-*.ttf`
- `fonts/otf/JetBrainsMonoPotato-*.otf`
- `fonts/webfont/JetBrainsMonoPotato-*.woff2`
- `fonts/webfont/jetbrainsmonopotato.css`

## CLI

```bash
uv run jetendard --help
```

주요 옵션:

- `--latin-dir`: 공식 `JetBrainsMonoNL-*.ttf`
- `--symbol-dir`: Nerd Font 심볼 donor용 `JetBrainsMonoNerdFontMono-*.ttf`
- `--cjk-dir`: `Pretendard-*.ttf`
- `--all`: 전체 16개 변형 빌드
- `--variants`: 특정 변형 지정
- `--weights`: 굵기 선택
- `--styles`: normal / italic 선택
- `--korean-scale`: 한글/CJK 시각 배율. 기본값 `1.15`

## No-ligature 정책

JetBrainsMono Potato는 리거처가 있는 JetBrains Mono가 아니라 **공식 `JetBrainsMonoNL`** 을 기반으로 합니다.

빌드 과정에서 추가하는 것은 다음뿐입니다.

1. Pretendard 한글/CJK 글리프
2. 기본 폰트에 없는 Nerd Font 심볼
3. 분해된 한글 Jamo 조합용 `ccmp`

Nerd Font의 GSUB 테이블은 가져오지 않으므로 `->`, `=>`, `==`, `!=` 같은 프로그래밍 리거처가 다시 들어오지 않습니다.

## 한글 폭

Pretendard 글리프는 JetBrains Mono의 units-per-em에 맞춰 정규화한 뒤 확대/중앙 정렬하고, advance width를 영문 2칸으로 고정합니다. 너무 큰 글리프는 clipping을 막기 위해 안전 범위 안으로 제한합니다.

Italic 변형에서는 JetBrains Mono 영문은 italic을 사용하지만 Pretendard 한글/CJK는 upright를 사용합니다.

## 라이선스

JetBrainsMono Potato는 SIL Open Font License 1.1 조건으로 배포합니다. JetBrains Mono, Nerd Fonts, Pretendard, 기존 Jetendard/Yeomil Mono의 저작권 및 reserved name 고지도 함께 확인하세요.

# JetBrainsMono Potato

JetBrainsMono Potato is a no-ligature Korean monospace font built from three upstream sources:

- **JetBrains Mono NL 2.304** for Latin, Greek, Cyrillic, punctuation, and code glyphs
- **Pretendard 1.3.9** for Korean/CJK glyphs
- **JetBrainsMono Nerd Font Mono** for Nerd Font symbols only

The important design rule is that programming ligatures are not imported. The base font is the official `JetBrainsMonoNL` family, and Nerd Font glyphs are copied only when their encoded codepoint is missing from that base font. Nerd Font GSUB features are not copied.

Korean/CJK glyphs are fitted into exactly two Latin monospace cells. The default visual scale is `1.15`.

## Output family

The generated family name is:

```text
JetBrainsMono Potato
```

Typical output files:

```text
fonts/ttf/JetBrainsMonoPotato-Regular.ttf
fonts/ttf/JetBrainsMonoPotato-Italic.ttf
fonts/ttf/JetBrainsMonoPotato-Bold.ttf
fonts/ttf/JetBrainsMonoPotato-BoldItalic.ttf
```

The full build covers Thin through ExtraBold, upright and italic.

## Build

Requirements:

- Python 3.12+
- `uv`

Then run:

```bash
uv sync --all-groups
make download
make run
make test
```

`make download` fetches the pinned upstream archives and extracts only the files needed by the build.

Current pinned versions:

- JetBrains Mono: **2.304**
- Nerd Fonts: **v3.4.0**
- Pretendard: **1.3.9**

Generated files are written to:

- `fonts/ttf/JetBrainsMonoPotato-*.ttf`
- `fonts/otf/JetBrainsMonoPotato-*.otf`
- `fonts/webfont/JetBrainsMonoPotato-*.woff2`
- `fonts/webfont/jetbrainsmonopotato.css`

## CLI

```bash
uv run jetendard --help
```

Important options:

- `--latin-dir`: official `JetBrainsMonoNL-*.ttf` sources
- `--symbol-dir`: `JetBrainsMonoNerdFontMono-*.ttf` files used only as symbol donors
- `--cjk-dir`: `Pretendard-*.ttf` sources
- `--all`: build all 16 variants
- `--variants`: build explicit variants
- `--weights`: select weights
- `--styles`: select normal / italic
- `--korean-scale`: Korean/CJK visual scale, default `1.15`

Examples:

```bash
uv run jetendard --all
uv run jetendard --weights Regular Bold --styles normal italic
uv run jetendard --variants Regular Light Bold
```

## No-ligature policy

JetBrainsMono Potato deliberately starts from `JetBrainsMonoNL`, not the ligature-enabled JetBrains Mono build.

The merge process adds only:

1. Pretendard Korean/CJK glyphs
2. missing encoded Nerd Font glyphs
3. a Hangul `ccmp` lookup used for decomposed Jamo composition

It does **not** import Nerd Font GSUB tables, so programming ligatures such as `->`, `=>`, `==`, and `!=` are not reintroduced.

## Korean metrics

Pretendard glyphs are normalized to the JetBrains Mono units-per-em, scaled visually, centered, and assigned an advance width of exactly two Latin cells. Oversized glyphs are capped to safe horizontal/vertical bounds to avoid clipping.

Italic variants use italic JetBrains Mono Latin glyphs with upright Pretendard Korean/CJK glyphs because Pretendard does not ship matching static italic Korean sources.

## License

JetBrainsMono Potato is distributed under the SIL Open Font License 1.1. Review the upstream JetBrains Mono, Nerd Fonts, Pretendard, and original Jetendard/Yeomil Mono projects for their copyright and reserved-name notices.

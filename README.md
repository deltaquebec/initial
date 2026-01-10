# Initial: Decorative Initial Capitals for LaTeX

**Configurable drop capitals with presets, image initials, and shaped text flow**

<p align="center"> 
<img src="/bts/initial-anatomy.png" alt="Anatomy of initial capital and paragraph, with package options">
</p>

The **initial** package provides decorative initial functionality through a key-value interface, supporting text and image initials, named presets, ante text, post text styling, sloped parshapes, and baseline grid alignment. Built on standard packages, derived from the premier [lettrine package](https://ctan.org/pkg/lettrine?lang=en) and the [novel class](https://ctan.org/pkg/novel?lang=en).

🔗 [Overleaf](https://www.overleaf.com/read/nqpfgddmjwdm#ffe750)

## Features

- **scalable drop caps**: configurable line depth with automatic height calculation;
- **image initials**: ornamental letters, illuminated capitals, PDF/PNG/JPG support;
- **ante text**: hanging text before the initial (opening quotes, punctuation) with optional scaling;
- **named presets**: define reusable configurations via `\newinitial{name}{key=value,...}`;
- **six positioning presets**: baseline/deep × in-margin/into-margin/hanging;
- **font styling**: bold, italic, smallcaps, slanted, arbitrary font commands;
- **color and contour**: direct color support plus contour effects;
- **sloped indentation**: non-rectangular text wraps via per-line slope;
- **afterlines region**: hanging-indent styles where lines past the initial align;
- **grid snapping**: round vertical space to baselineskip multiples;
- **accessibility**: actualtext support for image initials (PDF tagging);
- **clearance control**: explicit top/bottom spacing for paragraph isolation.


## Installation

```bash
# clone repository
git clone https://github.com/deltaquebec/initial.git

# copy .sty file to local texmf tree
cp initial/src/initial.sty ~/texmf/tex/latex/initial/

# update TeX filename database
texhash ~/texmf
```

Or place `initial.sty` in your project directory.


## Quick Start

### Basic usage

```latex
\documentclass{article}
\usepackage{initial}

\begin{document}

\initial{L}[orem ipsum] dolor sit amet, consectetur adipiscing elit.

\end{document}
```

### Common patterns

```latex
% 4-line red bold initial
\initial[lines=4, color=red, bold]{L}orem ipsum dolor sit amet, consectetur adipiscing elit. 

% image initial with accessibility
\initial[lines=5, actualtext=L]{ornamental-L.pdf}orem ipsum dolor sit amet, consectetur adipiscing elit.

% hanging opening quote
\initial[ante=", lines=3]{L}orem ipsum dolor sit amet, consectetur adipiscing elit.

% named preset for chapter openings
\newinitial{chapter}{lines=4, color=blue, post=textsc, gap=0.3em}
\initial[preset=chapter]{L}[orem] ipsum dolor sit amet, consectetur adipiscing elit.

% sloped text wrap
\initial[lines=4, slope=2pt]{L}orem ipsum dolor sit amet, consectetur adipiscing elit.
```


## Reference

### Dimensional parameters

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `lines` | int | 3 | number of lines the initial spans |
| `depth` | int | 0 | additional lines below baseline |
| `hoffset` | length | 0pt | horizontal offset |
| `voffset` | length | 0pt | vertical offset |
| `findent` | length | 0em | first line gap after initial |
| `nindent` | length | 0em | subsequent lines gap |
| `gap` | length | — | additive shift to both findent and nindent |
| `slope` | length | 0pt | per-line indent increment |
| `scale` | float | 1 | overall scale factor |
| `hstretch` | float | 1 | horizontal stretch |
| `vstretch` | float | 1 | vertical stretch |

### Afterlines region

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `afterlines` | int | 0 | lines in after-initial region |
| `afterindent` | length | 0pt | indent for after region |
| `afterslope` | length | 0pt | slope for after region |


### Typography

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `font` | command | — | font selection command |
| `bold` | bool | false | bold weight |
| `italic` | bool | false | italic shape |
| `smallcaps` | bool | false | small caps |
| `slanted` | bool | false | slanted shape |
| `color` | color | — | initial color (empty = inherit) |
| `contour` | bool | false | enable contour effect |
| `contourcolor` | color | white | contour color |
| `contoursize` | length | 0.3pt | contour thickness |

### Ante and post text

| Option | Type | Description |
|--------|------|-------------|
| `ante` | text | hanging ante, scaled to initial size |
| `ante*` | text | hanging ante, original size |
| `post` | string | textsc | styling for run-in text (textsc; textbf; textit; texttt; textsl; none) |


### Vertical clearance

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `tclearance` | length | 0pt | top clearance before paragraph |
| `bclearance` | length | 0pt | bottom clearance after paragraph |
| `textlines` | int | 0 | paragraph line count (for calculated spacing) |
| `grid` | bool | false | round vertical space to baselineskip multiple |

### Diacritics and accessibility

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `basecap` | bool | false | size to base cap height (diacritics overflow) |
| `actualtext` | text | — | accessibility text for image initials |

### Presets and debugging

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `preset` | name/int | — | named preset or legacy 1–6 |
| `box` | bool | false | show debug frame around initial |

## Numeric presets

Legacy numeric presets for quick positioning:

| Preset | Description |
|--------|-------------|
| 1 | baseline, contained in margin |
| 2 | baseline, shifted into margin |
| 3 | deep, in margin (default behavior) |
| 4 | deep, shifted into margin |
| 5 | hanging indent, baseline |
| 6 | hanging indent, deep |


## Provided commands

| Command | Description |
|---------|-------------|
| `\initial[options]{letter}[post]` | main command |
| `\newinitial{name}{key=value,...}` | define named preset |

### Exported dimensions

| Dimension | Description |
|-----------|-------------|
| `\initialboxwidth` | width of rendered initial box |
| `\initialboxheight` | height of rendered initial box |
| `\initialboxdepth` | depth of rendered initial box |


## Dependencies

`xparse`, `keyval`, `xstring`, `ifthen`, `graphicx`, `calc`, `etoolbox`, `xcolor`, `contour`

All dependencies are available in standard TeX distributions (TeX Live, MiKTeX).


## Compatibility

**Supported document classes:**
- `article`, `book`, `report` (full support);
- custom classes (generally works; test edge cases).

**Known limitations:**
- two-column documents need testing;
- deeply nested environments may affect parshape arithmetic;
- the ``basecap''' option for diacritics is more a workaround, not a solution;
- RTL formatting;
- snap-to-text boundaries for initial placements.
- no built-in kerning tables for specific letter pairs.

## Design Philosophy

### Why another lettrine?

The `lettrine` package is mature and handles edge cases accumulated over decades. This package exists because I wanted to understand TeX's paragraph shaping, box manipulation, and font metrics at a level that reading documentation does not necessarily provide; drop caps hit multiple subsystems simultaneously, and building one I had to contend with why `\smash` matters, how `\parshape` actually works, why `\llap` positions correctly where `\hbox to 0pt` does not, and so on.

I also wanted an in-house drop cap package for my own works that matched my intuition about the problem space, since it's a feature of typography I really like and care about, in addition to being a learning experience for deeper LaTeX design. So I derived from the experts, and learned much from it!

The documentation includes an extended historical section on decorated initials from Insular manuscripts through incunabula to CSS; probably more than anyone needs for a LaTeX package, but it was interesting to research and write about!

### What this does wrong

- no optical margin adjustment for specific letterforms;
- limited testing across document classes;
- parshape arithmetic is fragile in edge cases;
- solo project; arithmetic errors happen.

## Contributing

Contributions welcome:

1. check existing issues before opening new ones;
2. include minimal working examples for bug reports;
3. follow existing code style;
4. test with multiple document classes.

## Future work

- [ ] kerning tables for common letter pairs
- [ ] two-column document support
- [ ] integration with hanging punctuation packages
- [ ] RTL formatting
- [ ] improved diacritic handling

## Citation

```bibtex
@misc{initial2025,
  author = {Quigley, Daniel},
  title = {Initial: Drop Caps for LaTeX},
  year = {2025},
  url = {https://github.com/deltaquebec/initial},
  note = {LPPL 1.3c}
}
```

## Acknowledgments

This project draws conceptual inspiration from:

- **Daniel Flipo**
- **Robert Allgeyer**

Special thanks to:
- the LaTeX community for feedback and testing;
- all contributors who have helped improve these packages.


## License

**LaTeX Project Public License 1.3c**

This work may be distributed and/or modified under the conditions of the LaTeX Project Public License, either version 1.3c of this license or (at your option) any later version.


## Author

**Daniel Quigley**  
[dquigleydev@gmail.com](mailto:dquigleydev@gmail.com)  
[GitHub](https://github.com/deltaquebec)  
[Website](https://dquigley.dev)

---

**Version**: 1.2.0  
**Last updated**: January 2025  
**Status**: Active development

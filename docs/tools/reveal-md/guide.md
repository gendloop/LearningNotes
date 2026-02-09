# Guide

## Installation

`npm install -g reveal-md@6.1.4`

## Commands

* help
  * `reveal-md --help`
* start
  * `reveal-md slides.md`
  * `reveal-md slides.md -w`
* port
  * `reveal-md slides.md --port 8888`
* template
  * `reveal-md slides.md --template my-reveal-template.html`
  * `reveal-md slides.md --listing-template my-listing-template.html`
* => html
  * `reveal-md slides.md --static`
  * `reveal-md slides.md --static _site`
  * `reveal-md slides.md --static --static-dirs=res`
  * `reveal-md dir/ --static`
  * `reveal-md dir/ --static --glob '**/slides.md'`
  * `reveal-md slides.md --static _site --absolute-url https://example.com --featured-slide 5`
* => pdf
  * `reveal-md slides.md --print slides.pdf`
  * `reveal-md slides.md --print slides.pdf --print-size 1024x768`
  * `reveal-md slides.md --print slides.pdf --print-size A4`

## Theme

1. `beige`
2. `black-contrast`
3. `black`
4. `blood`
5. `dracula`
6. `league`
7. `moon`
8. `night`
9. `serif`
10. `simple`
11. `sky`
12. `solarized`
13. `white-contrast`
14. `white`
15. `white_contrast_compact_verbatim_headers`

## Animation

1. `none`
2. `fade`
3. `slide`
4. `convex`
5. `concave`

## Settings

```yaml
---
title                 : Slides
author                : gendloop
date                  : Jan. 20, 2023
theme                 : white_contrast_compact_verbatim_headers
highlightTheme        : vs
revealOptions:                          # https://revealjs.com/config/
    transition        : 'fade'          # none, fade, slide, convex, concave, zoom
    transitionSpeed   : 'default'       # default, fast, slow
    slideNumber       : true
    loop              : true
    autoSlide         : 5000            # milliseconds
    autoPlayMedia     : null            # null, true, false
    viewDistance      : 3
    mouseWheel        : true
    controls          : true
    controlsTutorial  : true
    separator         : "\n---\n"
    verticalSeparator : "\n----\n"
---

<style type="text/css">
h1, h2, h3, h4, h5, p, pre, code {
    text-align: left
}
.reveal {
    font-size: 28px;
}
.reveal pre code {
    font-size: 18px;
    line-height: 22px;
}
.reveal p code,
.reveal li code {
    font-size: 24px;
}
.reveal ul, .reveal ol {
    display: block;
}
.reveal img {
  border: 0 !important;
  box-shadow: none !important;
}
</style>

```

## References

1. [https://github.com/webpro/reveal-md?tab=readme-ov-file#markdown](https://github.com/webpro/reveal-md?tab=readme-ov-file#markdown)
2. [https://werty.cn/2020/01/JavaScript/Reveal%E7%BD%91%E9%A1%B5%E5%B9%BB%E7%81%AF%E7%89%87%E4%B8%AD%E6%96%87%E6%96%87%E6%A1%A3/](https://werty.cn/2020/01/JavaScript/Reveal%E7%BD%91%E9%A1%B5%E5%B9%BB%E7%81%AF%E7%89%87%E4%B8%AD%E6%96%87%E6%96%87%E6%A1%A3/)
3. [https://github.com/slhck/ffmpeg-encoding-course](https://github.com/slhck/ffmpeg-encoding-course)
4. [https://segmentfault.com/a/1190000042014461](https://segmentfault.com/a/1190000042014461)
[markdown - 如何利用 revealjs 快速写出漂亮的 PPT - 个人文章 - SegmentFault 思否.html](https://www.yuque.com/attachments/yuque/0/2024/html/22048361/1705674434136-c3ce70a9-e3ef-45c6-a202-3829bd761965.html)

---
title: Embedding multimedia files in R Markdown HTML documents
author: ''
date: '2020-03-11'
slug: embedding-multimedia-files-in-r-markdown-html-documents
categories:
  - Tutorial
tags:
  - R
  - R Markdown
  - Bookdown
  - HTML
  - Audio
  - Video
  - R-bloggers
subtitle: ''
summary: ''
authors: []
lastmod: ''
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

I am currently writing a comprehensive educational resource of all things music called [The Musican's Compendium](https://musicianscompendium.netlify.com) using [bookdown](https://github.com/rstudio/bookdown), an R package that can generate print-ready books and ebooks from R Markdown documents. My intention is to publish the book in web- and print-based formats, and to have audio and video supplements in the web version.

Fortunately, bookdown makes the former task easy to do. Simply run `bookdown::render_book("index.Rmd")` and HTML, PDF, and EPUB versions will be generated for you. And, for the most part, you won't need to worry about typesetting the PDF and EPUB versions; bookdown has you covered.

The latter task is also easy to do. Simply write raw HTML code into the body of your R Markdown document to embed any audio or video files into your book. After rendering your book, this code will turn into a media player in the HTML version, and will simply print the plain text between `<source>` and `</audio>` instead of a media player in the PDF and EPUB versions.

```html
<audio controls>
  <source src="Clair De Lune.mp3" type="audio/mpeg">
Your browser does not support the audio element.
</audio>
```

However, using raw HTML code to embed audio or video into your book presents four issues you might hope to avoid:

1. If you need multiple audio or video files embedded in your book, you will have to copy-paste and modify the raw HTML code to do so. And doing so increases the chance of making mistakes such as updating a variable name in one place but not in another, or copying only a portion of the code.

2. If the syntax requirements for the HTML code change, you will have to update that syntax everywhere you embedded an audio or video file.

3. It's more difficult to understand than it needs to be.

4. It's ugly!

These issues will be familiar to you if you have spent any time writing R code. Usually the solution is to wrap the code you're copy-pasting into a function; however, HTML does not use functions. R does though! All you need to do is wrap the code inside an R function.

Using the `embed_audio()` and `embed_video()` functions below, you simply call the function in the body of your R Markdown document like this: `` `r embed_audio("Clair De Lune.mp3")` `` wherever you want to embed your audio files, and like this: `` `r embed_video("Kiki's Delivery Service.mp4")` `` wherever you want to embed your video files.

When you knit or render your book, the files will be embedded in the HTML version but not in the PDF or EPUB versions. If you want placeholder text in the PDF or EPUB versions, just fill out the `` `r embed_audio(placeholder = "")` `` or `` `r embed_video(placeholder = "")` `` argument.

{{% alert note %}}
If you are using these functions with `bookdown` you may need to copy the directory of your media files to the `_book/` directory using `R.utils::copyDirectory(from = "audio/", to = "_book/audio")` somewhere in the build path of your book. The files do not seem to be included in the `_book/` directory after building the book otherwise.
{{% /alert %}}

***

## Embed audio function

### Description

A wrapper for the HTML5 `<audio>` element that either prints raw HTML code in HTML documents built by R Markdown or prints placeholder text in non-HTML documents built by R Markdown.

### Usage

`embed_audio(src, type = "audio/mpeg", attribute = "controls", placeholder = "")`

### Arguments
|                   |                                                                            |
| ----------------- | -------------------------------------------------------------------------- |
| `src`             | specifies the path to the file you wish to embed.                          |
| `type`            | specifies the file type. Valid arguments are "audio/mpeg", "audio/ogg", and                        "audio/wav".                                                               |
| `attribute`       | specifies whether audio controls, like play, pause, and volume should be                           displayed. Valid arguments are "controls" and "".                          |
| `placeholder`     | character string. specifies placeholder text when the audio player is                              unsupported.                                                               |

### Source code

```r
embed_audio <- function(src, type = "audio/mpeg", attribute = "controls",
                     placeholder = "") {
                        
  if (knitr::is_html_output()) {
    sprintf("<audio %3$s>
               <source src='%1$s' type='%2$s'>
            </audio>", src, type, attribute)
  } else print(placeholder)

}
```

***

## Embed video function

### Description

A wrapper for the HTML5 `<video>` element that either prints raw HTML code in HTML documents built by R Markdown or prints placeholder text in non-HTML documents built by R Markdown.

### Usage

`embed_video(src, type = "video/mp4", width = "320", height = "240", attribute = "controls", placeholder = "")`

### Arguments
|                   |                                                                            |
| ----------------- | -------------------------------------------------------------------------- |
| `src`             | specifies the path to the file you wish to embed.                          |
| `type`            | specifies the file type. Valid arguments are "video/mp4", "video/ogg", and                        "video/webm".                                                               |
| `width`           | sets the width of the video player in pixels. Always specify both the width and height arguments for videos.                                                                 |
| `height`          | sets the height of the video player in pixels.                             |
| `attribute`       | specifies whether video controls, like play, pause, and volume should be                           displayed. Valid arguments are "autoplay", "controls", "loop", "muted", "poster", "preload", and "". Attributes can be combined in a single string. See [here](https://www.w3schools.com/tags/tag_video.asp) for usage.                                  |
| `placeholder`     | character string. specifies placeholder text when the audio player is                              unsupported                                                                |

### Source code

```r
embed_video <- function(src, type = "video/mp4", width = "320", height = "240", 
                     attribute = "controls", placeholder = "") {
                        
  if (knitr::is_html_output()) {
    sprintf("<audio width='%3$s' height='%4$s' %5$s>
               <source src='%1$s' type='%2$s'>
            </audio>", src, type, width, height, attribute)
  } else print(placeholder)

}
```

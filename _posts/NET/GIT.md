---
title: Algebra
description: coordinates
categories:
- RT
tags:
- Math
permalink: /coords/
---


Git syno
https://kb.synology.com/en-sg/DSM/help/Git/git?version=7




Front end    
back end    
database  
----
# Ubuntu
- Houdini brak jakichs plików


- remote desktop is wrong


# Terminals
- PowerShell
- Comand Prompt
- GitBash
- Ubuntu (WSL)


[Linux command list 1](https://linuxcommand.org/index.php)     
[Linux command list 2](https://www.pcwdld.com/linux-commands-cheat-sheet)  

`sudo`  // Super-user do   
`mkdir` // make directory   
`ls` - list pliki
`ls -al` listuje jako lista

# BASH
Bourne again shell / Shell
can script
file.s or file

```
#!bash/usr/bin/bas`....
```
# Audio Video convertion
## ffmpeg:
- `ffmpeg -version`
- video > img `ffmpeg -ss 10:00 -i '/home/adam/Content_2022GDEVideo/VideoFile.mp4' -t 00:30 ./ImageFile_%04d.png`
- img > video `ffmpeg -r:v 24 -i "ImageFile_%04d.png" -codec:v libx264 -preset veryslow -pix_fmt yuv420p -crf 28 -an "VideoFile.mp4"`
- img > video, but every frame for 5 sek: `$ ffmpeg -r:v 1/5 -i "ImageFile_%04d.png" -r:v 24 -codec:v libx264  -preset veryslow
 -pix_fmt yuv420p -crf 28 -an "VideoFile.mp4"`


`ffmpeg -r:v 24 -i "./%04d.png" -codec:v libx264 -preset veryslow -pix_fmt yuv420p -crf 28 -an '/home/adam/Content_2022GDEVideo/VideoFile.mp4'`

 ffmpeg.exe -f image2 -framerate 25 -pattern_type sequence -start_number 1234 -r 3 -i Imgp%04d.jpg -s 720x480 test.avi
ffmpeg -start_number n -i test_%d.jpg -vcodec mpeg4 test.avi

 -r 3 option sets the framerate
 -s option rescales
https://hamelot.io/visualization/using-ffmpeg-to-convert-a-set-of-images-into-a-video/

## avconv
avconv -i "image-%d.jpg" -r 25 -c:v libx264 -crf 20  -pix_fmt yuv420p movie.mov
# Git:

# Git www :

# jekyll

```
C:\Users\Adam>cd C:\Users\Adam\TestjekyllB

C:\Users\Adam\TestjekyllB>bundle exec jekyll serve
Configuration file: C:/Users/Adam/TestjekyllB/_config.yml
            Source: C:/Users/Adam/TestjekyllB
       Destination: C:/Users/Adam/TestjekyllB/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
       Jekyll Feed: Generating feed for posts
                    done in 2.242 seconds.
 Auto-regeneration: enabled for 'C:/Users/Adam/TestjekyllB'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
[2020-08-22 03:08:51] ERROR `/favicon.ico' not found.
      Regenerating: 1 file(s) changed at 2020-08-22 03:49:35
                    _posts/2020-08-22-new_test_post.md
       Jekyll Feed: Generating feed for posts
                    ...done in 0.2397755 seconds.

      Regenerating: 1 file(s) changed at 2020-08-22 03:51:05
                    _posts/2020-08-22-new_test_post.md
       Jekyll Feed: Generating feed for posts
                    ...done in 0.0911485 seconds.
```


```

jekyll <subcommand> [options]

Options:
      -s, --source [DIR]  Source directory (defaults to ./)
      -d, --destination [DIR]  Destination directory (defaults to ./_site)
          --safe         Safe mode (defaults to false)
      -p, --plugins PLUGINS_DIR1[,PLUGINS_DIR2[,...]]  Plugins directory (defaults to ./_plugins)
          --layouts DIR  Layouts directory (defaults to ./_layouts)
          --profile      Generate a Liquid rendering profile
      -h, --help         Show this message
      -v, --version      Print the name and version
      -t, --trace        Show the full backtrace when an error occurs

Subcommands:
compose
docs
import
build, b              Build your site
clean                 Clean the site (removes site output and metadata file) without building.
doctor, hyde          Search site and print specific deprecation warnings
help                  Show the help message, optionally for a given subcommand.
new                   Creates a new Jekyll site scaffold in PATH
new-theme             Creates a new Jekyll theme scaffold
serve, server, s      Serve your site locally

```

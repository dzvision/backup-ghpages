---
layout: post
title: 如何给网页添加好看的HTML音乐播放器
categories: HTML
description: 
keywords: HTML, Audio Player
---


**目录**

* TOC
{:toc}

## 序
目前[MoePlayer/cPlayer](https://github.com/MoePlayer/cPlayer)可以达到想要的效果。

## 做法
在需要的位置用<div>，然后其余都放在底部Script里。  
DIV ID要和Script的element: document.getElementById('app')中相互对应  

```
<div id="app"></div>

### Script下 ###
<!-- 加载 cplayer 脚本 -->
<script src="https://cdn.jsdelivr.net/npm/cplayer/dist/cplayer.min.js"></script>
<script>
  let player = new cplayer({
    element: document.getElementById('app'),
    playlist: [
      {
        src: '歌曲资源链接...',
        poster: '封面链接...',
        name: '歌曲名称...',
        artist: '歌手名称...',
        lyric: '歌词...', ##例如abc.lrc
        sublyric: '副歌词，一般为翻译...'
      },
	  ##第二首歌
      {
        ...
      },
      ......
    ]
  })
</script>
```

完成



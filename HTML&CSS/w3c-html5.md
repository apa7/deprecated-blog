#W3C School HTML5 起步

2016-4-15 16:50
---

#视频

video 元素允许多个 source 元素。source 元素可以链接不同的视频文件。浏览器将使用第一个可识别的格式.
```html
<video width="320" height="240" controls="controls">
  <source src="movie.ogg" type="video/ogg">
  <source src="movie.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>
```


<table>
<tr>
<th>格式</th>
<th style="width:16%">IE</th>
<th style="width:16%">Firefox</th>
<th style="width:16%">Opera</th>
<th style="width:16%">Chrome</th>
<th style="width:16%">Safari</th>
</tr>

<tr>
<td>Ogg</td>
<td>No</td>
<td>3.5+</td>
<td>10.5+</td>
<td>5.0+</td>
<td>No</td>
</tr>

<tr>
<td>MPEG 4</td>
<td>9.0+</td>
<td>No</td>
<td>No</td>
<td>5.0+</td>
<td>3.0+</td>
</tr>

<tr>
<td>WebM</td>
<td>No</td>
<td>4.0+</td>
<td>10.6+</td>
<td>6.0+</td>
<td>No</td>
</tr>
</table>

#音频
```html
<audio controls="controls">
  <source src="song.ogg" type="audio/ogg">
  <source src="song.mp3" type="audio/mpeg">
Your browser does not support the audio tag.
</audio>
```

<table>
<tr>
<th>&nbsp;</th>
<th style="width:16%;">IE 9</th>
<th style="width:16%;">Firefox 3.5</th>
<th style="width:16%;">Opera 10.5</th>
<th style="width:16%;">Chrome 3.0</th>
<th style="width:16%;">Safari 3.0</th>
</tr>

<tr>
<td>Ogg Vorbis</td>
<td>&nbsp;</td>
<td>&#8730;</td>
<td>&#8730;</td>
<td>&#8730;</td>
<td>&nbsp;</td>
</tr>

<tr>
<td>MP3</td>
<td>&#8730;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&#8730;</td>
<td>&#8730;</td>
</tr>

<tr>
<td>Wav</td>
<td>&nbsp;</td>
<td>&#8730;</td>
<td>&#8730;</td>
<td>&nbsp;</td>
<td>&#8730;</td>
</tr>
</table>
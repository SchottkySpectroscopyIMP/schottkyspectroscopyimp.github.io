---
layout: post
title:  "Remote button pusher for IQ recorder has been established!"
date:   2018-05-22 00:13:54 +0800
author: SchoSpec

categories:
        - page update
tags:
        - platform
---

Hello, everybody! It's really good to see you this time.

We now can temporarily get rid of the blue screen of the IQ recorder with unknown reason. A remote-controllable button pusher has been established! The little but powerful device may help us a lot in the long struggle during the beamtime.

It is based on the mechanism of the <b>cam</b>, which we only uses a short part of the full turn of circular motion to reduce the space of the push rod's to-and-fro motion. The key to remote control is the `GPIO` library of `raspberry pi` and the `socket` of `Python-3`.

We also build a GUI as usual to get the user interaction easier and more intuitive.

<div>
<img src="https://raw.githubusercontent.com/SchottkySpectroscopyIMP/remote-buttonpusher/master/wiki-pic/buttonPusher.gif" alt="camStep" height="320" width="200" style="vertical-align:middle;">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<img src="https://raw.githubusercontent.com/SchottkySpectroscopyIMP/remote-buttonpusher/master/wiki-pic/buttonPusher_cam.JPG" alt="buttonPusher" height="320" width="440" style="vertical-align:middle;">
</div>

See the magic!

<iframe src='https://onedrive.live.com/embed?cid=64BDB670E3C9499C&resid=64BDB670E3C9499C%214840&authkey=ACuGPrTOyhfP5OY&em=2&wdAr=1.7777777777777776' width='610px' height='367px' frameborder='0'>这是嵌入 <a target='_blank' href='https://office.com'>Microsoft Office</a> 演示文稿，由 <a target='_blank' href='https://office.com/webapps'>Office Online</a> 支持。</iframe>

You can find more at our [`/Project/platform/data-acquisition/`]({{ "/project/platform/data-acquisition/" | relative_url }}). If you have some suggestions, don't hesitate to comment us.



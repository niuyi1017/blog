---
title: 4分钟50行代码实现一颗跳动的爱心
date: 2022-05-14 21:39:50
photos: [[https://niuyi-blog.oss-cn-hangzhou.aliyuncs.com/post-imgs/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20220514175859.png]]
tags: Bilibili
---
520要到了，花式表白一下？

<!--more--> 

### 视频

全网搜索：我叫牛一  

 B站：[4分钟50行代码实现一个跳动的红心](https://www.bilibili.com/video/BV1AR4y1P7vh)    
 小红书：[4分钟50行代码实现一个跳动的红心](https://www.xiaohongshu.com/discovery/item/627fb16f000000002103f3d5)  
 抖音：[4分钟50行代码实现一个跳动的红心](https://v.douyin.com/FassH4w/)  

 
### 源码
#### 1、普通版
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Red Heart</title>
  <style>
    body{
      display: flex;
      justify-content: center;
    }
    .box{
      height: 600px;
      width: 600px;
      animation: beat 1s infinite alternate;
      background: #ccc;
    }
    .part{
      height: 400px;
      width: 600px;
      background: red;
      border-radius: 200px 0 0 200px ;
      box-shadow: 0 0 200px red;
    }
    .left{
      transform: translate(0,200px);
    }
    .right{
      transform: rotate(90deg) translate(-300px, -100px);
    }
    @keyframes beat {
      from {
        transform: rotate(45deg) scale(.8);
      }
      to{
        transform: rotate(45deg) scale(1);
      }
    }
  </style>
</head>
<body>
    <div class="box">
      <div class="part left"></div>
      <div class="part right"></div>
    </div>
</body>
</html>
```
#### 2.动态计算日期版
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Red Heart</title>
  <style>
    body{
      display: flex;
      flex-direction: column;
      justify-content: space-around;
      align-items: center;
      height: 100vh;
      margin: 0;
      padding: 0;
    }
    .box{
      height: 600px;
      width: 600px;
      animation: beat 1s infinite alternate;
    }
    .part{
      height: 400px;
      width: 600px;
      background: red;
      border-radius: 200px 0 0 200px ;
      box-shadow: 0 0 200px red;
    }
    .left{
      transform: translate(0,200px);
    }
    .right{
      transform: rotate(90deg) translate(-300px, -100px);
    }
    h1{
      color: pink;
      font-size: 64px;
    }
    @keyframes beat {
      from {
        transform: rotate(45deg) scale(.8);
      }
      to{
        transform: rotate(45deg) scale(1);
      }
    }
  </style>
</head>
<body>
    <div class="box">
      <div class="part left"></div>
      <div class="part right"></div>
    </div>
    <h1>我们已经相恋<span id="days"></span>天了</h1>
    <script>
      window.onload = () => {
        const firstDay = new Date('2017-05-20').getTime()
        const now = new Date().getTime()
        const days = (now - firstDay) / (1000 * 60 * 60 * 24)
        document.querySelector('#days').innerHTML = Math.floor(days)
      } 
    </script>
</body>
</html>

```
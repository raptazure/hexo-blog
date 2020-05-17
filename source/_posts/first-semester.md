---
title: 记大一上
date: 2020-04-12 16:07:42
categories: 感想
tags: 回忆
---

<img src="first-semester/intro.jpg" width="900px">

$\quad$因为年级要求学生互评，需要制作一份 2-3 分钟的 PPT 展示自己大一上学期的成长与收获，感悟与体会，存在的缺点不足以及未来的规划打算（这不是公开处刑嘛(#`O′)，既然写完了，就发布到博客好了，也当作自己对前一阶段的小总结吧。

<!--more-->

$\quad$虽说让做 PPT，但是理论上任何 slideshow 都可以满足这一需求，作为 markdown 的重度爱好者（不是），去 GitHub 上逛了一圈选定了 remark，这样也便于移植啦！

- 话不多说，还是直接贴源码方便= =

```html
<!DOCTYPE html>
<html>
  <head>
    <title>我的大一上</title>
    <meta charset="utf-8" />
    <style>
      @import url(https://fonts.googleapis.com/css?family=Yanone + Kaffeesatz);
      @import url(
        https://fonts.googleapis.com/css?family=Droid + Serif:400,
        700,
        400italic
      );
      @import url(
        https://fonts.googleapis.com/css?family=Ubuntu + Mono:400,
        700,
        400italic
      );

      body {
        font-family: "Droid Serif";
      }

      h1,
      h2,
      h3 {
        font-family: "Yanone Kaffeesatz";
        font-weight: normal;
      }

      .remark-code,
      .remark-inline-code {
        font-family: "Ubuntu Mono";
      }

      .down {
        margin-top: 50px;
      }
    </style>
  </head>

  <body>
    <textarea id="source">

class: center, middle

# 记大一上...

### slideshow created using [remark](https://github.com/gnab/remark)

2191110314 刘浩然

---

### 崭新的大学生活

- 作为大学生活的开端，生活还算蛮丰富吧，除了渐渐适应住校生活，变得更独立自主以外，也尝试参加了不同的活动，比如：
    - 趣味运动会夹气球跑（准确说应该是跳= =）
    - 月海音乐晚会宣传视频剪辑和摄像工作（宣传部划水人士= =）
    - 校园马拉松（本来运动细胞就不发达的说= =）
    - 大一年度项目组长（慢着，这不算活动啊喂= =）
    - 嗯...大概还有其他一些零零散散的活动，就不列举了...
--
<div class="down">
- 我觉得在大学多尝试尝试几种活动其实还蛮不错的，毕竟多了一份对生活的体验吧，现在回头想想这半年参加的活动，可能比高中的总和还要多...
</div>

---

### 专业知识学习

- 这是上学期注重比较多的部分，其实也不是刻意，只是感觉喜欢就做得多一些，下面来分类聊一聊：
--

#### 方向选择
- 在大一上学期开始的时候，自己对于以后想做的事情还不是很清晰，为了早一些找到自己喜欢做的事情以便深入，也做了很多尝试，比如unity做个小游戏，拿python画个画（雾）等等，但是总有些三分钟热度的意思，直到遇到了能让我决定坚持下来的，并能称为自己喜欢的——
--

##### JavaScript / TypeScript
--

- 与其说喜欢这门语言，倒不如说是喜欢其背后的丰富生态，作为GitHub上repo数常年领先的语言，世界各地的人们都在为这门语言的发展做着自己的贡献。
- 不管是前端三大框架Vue（尤大赛高！），React，Angular，还是基于Node.js的服务端框架Express，Koa，Fastify，用于移动端开发的RN与Ionic，桌面开发的Electron，物联网领域的JonnyFive，人工智能领域的Tensorflow.js，都展示着社区的力量。再加上体会过用TS开发VSCode扩展的愉悦感，把自己喜欢的塔罗牌加入到编辑器中，让我更加坚定了决心。
--

- 在大一上这个时间点确定了努力的方向与要做的事情，真的蛮庆幸的吧。

---

#### 开源世界/技术分享

- 充分发挥自己瞎鼓捣的特质，结识linux，docker，vim，git与github等对我帮助很大
- 使用Hexo与GitHubPages搭建了自己的个人博客，目前与掘金平台持续更新中...
--

- 顺便借此机会，GitHub扩一波列呀~如果收到issue和PR其实很开心的，欢迎伙伴们来一起写代码~（占时间有些多，这块暂时就说这些啦

<img src="commit.png" width="800px">

---

### 基础课学习（数学）

- 这块做的自认为很不好，没有及时复习，最后考试周突击，导致某些考试课的绩点比较惨= =
- 所以自己以后也要加强对基础课的学习，特别是数学（就目前大一来说），当然专业基础课肯定更要好好学啦！
--

- 哦对了，体育好像也算基础课，还要多多运动！
--

- 所以这还关联到一个时间管理和分配的事情，这块自己做的也不是很好，常常由着自己的性子来，有种想做的事情才去做的感觉= =，以后大概要注意一下了

---

### 未来要做的事情

- 专业方面，首先要把实验室前端的工作做好吧，这也是一份责任，当然也是兴趣，所以要把前端学精一些，然后慢慢向后端扩展（Node.js)
--

- 基础课方面，前面也说过了，要合理分配时间，多多努力才行呀 
--

- 然后，希望能多交几个朋友(￣▽￣)""...也希望能坚持发展自己除编程外的兴趣，比如音乐和神秘学（玄学）等等，还要看想看的番
--

- 然后就是...希望今年也能和大家一起开心的写代码！

---


## 就是这些啦
## 谢谢大家！



    </textarea>
    <script src="https://remarkjs.com/downloads/remark-latest.min.js"></script>
    <script>
      var slideshow = remark.create();
    </script>
  </body>
</html>
```

- 其实还有很多很多其他的事情没有写上去，毕竟是公开展示嘛（嘿嘿）
- 总之加油加油啦！

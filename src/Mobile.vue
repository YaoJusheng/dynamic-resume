<template>
  <div id="app">
    <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
    <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
  </div>
</template>

<script>
import StyleEditor from "./components/StyleEditor";
import ResumeEditor from "./components/ResumeEditor";
import "./assets/reset.css";
export default {
  name: "app",
  components: {
    StyleEditor,
    ResumeEditor
  },
  data() {
    return {
      interval: 3,
      currentStyle: "",
      enableHtml: false,
      fullStyle: [
        `/*
* Inspired by http://strml.net/
* 大家好，我是老姚
* 每天都有很多人在求职的路上，在线简历必不可少。
* 这里跟个风，我也来写一份简历！
*/

/* 首先给所有元素加上过渡效果 */
* {
  transition: all .1s;
}

/* 设置背景颜色 */
html {
  color: rgb(222,222,222);
  background: rgb(0,43,54);
}

/* 设置边框 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  overflow: auto;
  width: 90vw;
  margin: 2.5vh 5vw;
  height: 90vh;
}

/* 设置高度 */
.styleEditor {
  height: 45vh;
}

/* 代码高亮 */
.token.selector{
  color: rgb(133,153,0);
}
.token.property{
  color: rgb(187,137,0);
}
.token.punctuation{
  color: yellow;
}
.token.function{
  color: rgb(42,161,152);
}

/* 加3D效果 */
html{
  perspective: 1000px;
}
.styleEditor {
  position: fixed; left: 0; top: 0;
  transform: rotateX(-10deg) translateZ(-50px) ;
}

/* 准备一个编辑器 */
.resumeEditor{
  position: fixed;
  top: 50%; left: 0;
  padding: .5em;  margin: 2.5vh;
  width: 95vw; height: 45vh;
  border: 1px solid;
  background: white; color: #222;
  overflow: auto;
}

/* 现在，开始写简历 */
`,
        `
/*将Markdown格式翻译成HTML
 *再对HTML加点样式
*/
.resumeEditor{
  padding: 2em;
}
.resumeEditor h2{
  display: inline-block;
  border-bottom: 1px solid;
  margin: 1em 0 .5em;
}
.resumeEditor h2 ~ p {
  margin: 6px 0;
  font-style: oblique;
}
.resumeEditor ul,.resumeEditor ol{
  list-style: none;
}
.resumeEditor ul> li::before{
  content: '•';
  margin-right: .5em;
}
.resumeEditor ul> li > pre {
  margin: 5px 0;
}
.resumeEditor ol {
  counter-reset: section;
}
.resumeEditor ol li::before {
  counter-increment: section;
  content: counters(section, ".") " ";
  margin-right: .5em;
}
.resumeEditor a {
  color: rgb(66, 165, 245);
}
.resumeEditor blockquote {
  margin: 1em;
  padding: .5em;
  background: #ddd;
}
`
      ],
      currentMarkdown: "",
      fullMarkdown: `
姚举生
----

Python开发工程师，全栈开发，目前在南京工作。

技能
----

* Python 开发
* Ruby 开发
* PHP 开发
* 前端、Node.js

工作经历
----

1. 南京软通动力
2. 智泰滕迪
3. ...

项目经验
----
1.Taidii 教育系统

+ **工具环境**：pycharm、Linux
+ **相关技术**：Python、Django、Mysql、Redis、JavaScript、Ajax、HTML、JSON、VUE
+ **项目描述**：
          本产品为少儿教育系统，分web端，APP端等，基于Django（rest-framework）框架，结合MySQL，Redis数据库，
      通过HTML+JavaScript+css样式向用户展示的学校信息，同时用户可以通过不同模块向服务器发送相应请求，
      服务器通过Ajax+JSON技术和客户端进行交互，收集用户信息，返回相应页面和信息，以供用户获取和下一步操作。 
+ **责任描述**：
  &emsp;  1）成长记录册照片显示优化，
  &emsp;  2）物资管理模块重构与整改，
  &emsp;  3）校园风采活动页展示、图片视频上传，
  &emsp;  4）课程表快速录入，问卷调查，
  &emsp;  5）中英文翻译，添加并设置权限，
  &emsp;  6）bug修改等：

2.Dialog日志分析

+ **工具环境**：pycharm、Windows
+ **相关技术**：Python、MongoDB、XML解析（xml.etree.ElementTree模块+lxml）
+ **项目描述**：
          通过接收终端日志或xml文件（模板），多线程代码解析不同xml模板，实现dom树的创建，解析xml（命令和回显），
      划分节点和属性（类型字段+值），按类型存入数据库，定制匹配规则，解析日志内容，匹配命令及参数，获取回显信息，
      分析类型字段的type值，判断合法性，提取错误信息，向上层反馈，做存入文本或数据库处理，并显示，供调用。
+ **责任描述**：xml解析，Node节点查找与匹配；数据库接口编写；日志解析与反馈；

3.仿真STA+CMS集中控制系统

+ **工具环境**：RubyMine、Windows
+ **相关技术**：ruby、sqlite、JavaScript、HTML5、CSS、Bootstrap、WLAN、802.11协议、802.1x认证协议等
+ **项目描述**：
          根据真实终端连接WLAN信号，模拟终端设备（PC）与模拟AP交互过程来实现仿真，关联模拟AP，
      终端特征导入open、wap2、dhcp、dot1x等流程真实报文，数据库存储相应报文格式；新建终端sta，
      选定流程，添加相应报文格式，编辑报文内容 ，发送模拟AP，AP侧对报文处理上传AC接受控制，同时回应sta，进入下一个流程；
      终端多样化（自定义终端、镜像发包器、固定终端），可根据需要进行选型，同时对终端信息以及报文内容进行编辑自定义修改，
      如模拟终端数，mac步长，是否持续重复上线流程，信号连接（信道、射频、功率、速率、mac等信息）、
      报文编辑修改（发送次数、流程选择，等待时间，超时时间，帧类型、源/目的mac、content，失败重传次数等）；
      对于关联信号选择，建立websocket，自动搜寻WiFi信号，以页面拖拽方式填入终端，模拟关联选择过程。
      CMS系统分三块：任务管理、终端管理、配置管理，三个模块协同工作，
      通过下发含有特定配置的指定终端的定时任务，对关联终端进行集中控制。
+ **责任描述**：
  &emsp;  1）解决ssid解码错误；
  &emsp;  2）dot1x认证流程状态机，收发报文机制前后台实现；
  &emsp;  3）优化wap2流程报文收发流程与四次握手；
  &emsp;  4）open流程DHCP收发机制优化，多终端上线提高成功率，增加失败重传机制；
  &emsp;  5）收报机制修改，提高收包成功率；
  &emsp;  6）添加open打流；
  &emsp;  7）多任务分批上线机制；
  &emsp;  8）CMS集中控制系统整改与设计；
  &emsp;  9）wpa2添加DHCP和打流；
  &emsp;  10）添加四次握手后报文交互中对数据帧的加解密；

4.PNF流水线部署

+ **工具环境**：pycharm、Windows、notepad++
+ **相关技术**：python、XML、YAML、INI等文件解析、远程控制与网络连接
+ **项目描述**：
          python搭建的一个PNF流水线部署工具，deploy分为四个部分：组件、子系统相关、反向集成、自动生成部署环境的配置，
      通过对env中XML和YAML的解析，自动生成config.ini配置文件，
      通过解析配置文件，部署相应的环境。
+ **责任描述**：
  &emsp;  1）对配置生成模块与部署模块进行代码重构（拆分功能，解耦，优化，提高代码复用率等）；
  &emsp;  2）添加反向集成种类；
  &emsp;  3）修改配置模板，增加进程查询，优化大包检测，添加自动部署；
  &emsp;  4）对sswm子系统（数字签名+非数字签名）流程适配修改，文件检测、端对端文件压缩上传与解析、进程监控；
  &emsp;  5）编写远程tar包替换工具（GUI）;
  &emsp;  6）编写黑白名单及特殊类型过滤工具;
  &emsp;  7）编写Linux命令行日志解析，命令与各类参数回显检测分析工具。

其他
----
1.**爬虫**

  - 网络信息采集
  - 简历分析与收集

2.**网站**

  + 购物 （python+web前端）
  + 微博客（python + tornado + web前端）
  + 个人博客（nodejs + 前端）
    &emsp;  1）[Hexo + yilia](https://github.com/YaoJusheng/hexo-theme-yilia-plus) 修改和完善
    &emsp;  2）[Hexo + next](https://github.com/YaoJusheng/hexo-theme-next) 修改和完善
    &emsp;  3）[Hexo + diaspora](https://github.com/YaoJusheng/hexo-theme-diaspora) 修改和完善
    &emsp;  4）[Hexo + landscape](https://github.com/YaoJusheng/hexo-theme-landscape) 修改和完善
    &emsp;  5）[Hexo + icarus](https://github.com/YaoJusheng/hexo-theme-icarus) 修改和完善
  + 简历（nodejs + 前端）：
    &emsp;  1）[静态简历-resume](https://github.com/YaoJusheng/resume)
    &emsp;  2）[静态简历-static-resume](https://github.com/YaoJusheng/static-resume)
    &emsp;  3）[简历制作-online-resume](https://github.com/YaoJusheng/online-resume)
    &emsp;  4）[动态简历-dynamic-resume](https://github.com/YaoJusheng/dynamic-resume)

3.**系统**

  - CMS系统开发（PHP + laravel）
  - ...

链接
----

* [GitHub](https://github.com/yaojusheng)
* [CSDN](https://blog.csdn.net/weixin_41599858)
* [我的博客1](https://blog.yaogro.cn)
* [我的博客2](https://yaojusheng.gitee.io/blog/)

> 如果你喜欢这个效果，Fork [我的项目](https://github.com/yaojusheng/dynamic-resume)，打造你自己的简历！

`
    };
  },
  created() {
    this.makeResume();
  },
  methods: {
    makeResume: async function() {
      await this.progressivelyShowStyle(0);
      await this.progressivelyShowResume();
      await this.progressivelyShowStyle(1);
      await this.showHtml();
      await this.progressivelyShowStyle(2);
    },
    showHtml: function() {
      return new Promise((resolve, reject) => {
        this.enableHtml = true;
        this.$nextTick(() => {
          this.$refs.resumeEditor.goTop();
        });
        resolve();
      });
    },
    progressivelyShowStyle(n) {
      return new Promise((resolve, reject) => {
        let interval = this.interval;
        let showStyle = async function() {
          let style = this.fullStyle[n];
          if (!style) {
            return;
          }
          // 计算前 n 个 style 的字符总数
          let length = this.fullStyle
            .filter((_, index) => index <= n)
            .map(item => item.length)
            .reduce((p, c) => p + c, 0);
          let prefixLength = length - style.length;
          if (this.currentStyle.length < length) {
            let l = this.currentStyle.length - prefixLength;
            let char = style.substring(l, l + 1) || " ";
            this.currentStyle += char;
            if (style.substring(l - 1, l) === "\n" && this.$refs.styleEditor) {
              this.$nextTick(() => {
                this.$refs.styleEditor.goBottom();
              });
            }
            setTimeout(showStyle, interval);
          } else {
            resolve();
          }
        }.bind(this);
        showStyle();
      });
    },
    progressivelyShowResume() {
      return new Promise((resolve, reject) => {
        let length = this.fullMarkdown.length;
        let interval = this.interval;
        let showResume = () => {
          if (this.currentMarkdown.length < length) {
            this.currentMarkdown = this.fullMarkdown.substring(
              0,
              this.currentMarkdown.length + 1
            );
            let lastChar = this.currentMarkdown[
              this.currentMarkdown.length - 1
            ];
            let prevChar = this.currentMarkdown[
              this.currentMarkdown.length - 2
            ];
            if (prevChar === "\n" && this.$refs.resumeEditor) {
              this.$nextTick(() => this.$refs.resumeEditor.goBottom());
            }
            setTimeout(showResume, interval);
          } else {
            resolve();
          }
        };
        showResume();
      });
    }
  }
};
</script>

<style scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  min-height: 100vh;
  position: relative;
}
html {
  min-height: 100vh;
}
* {
  box-sizing: border-box;
}
</style>
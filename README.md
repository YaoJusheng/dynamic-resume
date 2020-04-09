# 一个会动的简历模板



## 使用方法

``` bash
git clone https://github.com/YaoJusheng/dynamic-resume.git
cd dynamic-resume
npm install
npm run dev
```

## 部署方法


1. 编辑 config/index.js
    ```
    修改第 10 行的 assetsPublicPath，值为 `项目名/dist`。
    如果你没有修改项目名 dynamic-resume，则可跳过此步骤。
    ```

2. 编译、上传
    ``` bash
    npm run build
    git add .
    git commit -m "update"
    git push
    ```

3. 开启 GitHub Pages 功能
    - 1）.手动上传文件
    
    ```
    将生成的目标文件public/*上传到你的web服务器上。
    ```
    
    - 2）.命令部署

    新建gh-pages分支后，执行：
    ```bash
    npm run deploy
    ```




> 感谢 [jirengu-inc](https://github.com/jirengu-inc/animating-resume) 的简历工具.

> 感谢 [zhousiwei](https://gitee.com/zhousiwei/anires) 的补充。

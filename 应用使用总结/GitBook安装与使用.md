# GitBook

### 1.GitBook介绍
GitBook 是一个基于 Node.js 的命令行工具，支持 Markdown 和 AsciiDoc 两种语法格式，可以输出 HTML、PDF、eBook 等格式的电子书。所以可以把 GitBook 定义为文档格式转换工具。 

### 2. 本人使用环境

```markdown
1. windows10
2. Node version: 10.15.0
3. CLI version: 2.3.2
4. GitBook version: 3.2.3
5. NPM version 6.4.1
```
### 3. 安装环境

- 下载对应平台的[Node.js](https://nodejs.org/en/download/)安装
- 安装 GitBook
  - 打开命令行(Git bash)输入
  ``` bash
  $ npm install -g gitbook-cli
  ```
    ![命令安装GitBook](https://upload-images.jianshu.io/upload_images/1497424-d6c1f02d1c5912c9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  - 安装完之后，就会多了一个 gitbook 命令

### 4. 使用GitBook
- 进入到你需要构建的文件夹执行
```bash
$ gitbook init
```
  ![GitBook初始化](https://upload-images.jianshu.io/upload_images/1497424-b19884f859fae019.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


正常情况下会自动初始化GitBook到文件夹，如果报错`Error: EPERM: operation not permitted`则重新执行一遍。
- 执行完后，你会看到多了两个文件 —— `README.md` 和 `SUMMARY.md`，它们的作用如下：
`README.md` —— 书籍的介绍写在这个文件里
`SUMMARY.md` —— 书籍的目录结构在这里配置
- 编辑`SUMMARY.md`目录文件
  例如：

```
# 目录

* [前言](README.md)
* [第一章](Chapter1/README.md)
  * [第1节：衣](Chapter1/衣.md)
  * [第2节：食](Chapter1/食.md)
  * [第3节：住](Chapter1/住.md)
  * [第4节：行](Chapter1/行.md)
* [第二章](Chapter2/README.md)
* [第三章](Chapter3/README.md)
* [第四章](Chapter4/README.md)

```

- 从命令行中进入到构建的文件夹，文件夹中再次执行命令:
``` bash
  $ gitbook init
```
GitBook 会查找 `SUMMARY.md` 文件中描述的目录和文件，如果没有则会将其创建。
- 接着我们执行命令来预览这本书籍，
``` bash
  $ gitbook serve
```
执行命令后会对 Markdown 格式的文档进行转换，默认转换为 html 格式，最后提示 `“Serving book on http://localhost:4000”`。打开浏览器查看即可。

---
**提示：**
- 当你写得差不多，你可以执行命令构建书籍，
``` bash
  $ gitbook build
```
默认将生成的静态网站输出到 _book 目录。实际上，这一步也包含在 `gitbook serve `里面，因为它们是 HTML，所以 GitBook 通过 Node.js 给你提供服务了。 


### 5. 碰到的问题
- gitbook serve命令找不到**.js
```bash
Error: ENOENT: no such file or directory, stat 'D:\ZGLDoingGitRepository\DoingGit\_book\gitbook\gitbook-plugin-sharing\buttons.js'
```

```bash
Error: ENOENT: no such file or directory, stat 'D:\ZGLDoingGitRepository\DoingGit\_book\gitbook\gitbook-plugin-fontsettings\fontsettings.js'
```
![gitbook serve命令找不到**.js](https://upload-images.jianshu.io/upload_images/1497424-0d24b3365289460e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 解决办法：

找到`C:\Users\zgldo\.gitbook\versions\3.2.3\lib\output\website\copyPluginAssets.js`文件，将其112行改成`confirm：false`即可解决。

### 6. GitBook命令详情
#### 6.1 build 命令可以指定路径：

``` bash
$ gitbook build [书籍路径] [输出路径]
```

#### 6.2 serve 命令也可以指定端口：

``` bash
$ gitbook serve --port 2333
```

#### 6.3 生成 PDF 格式的电子书：

``` bash
$ gitbook pdf ./ ./JavaBook.pdf
```

#### 6.4 生成 epub 格式的电子书：

``` bash
$ gitbook epub ./ ./JavaBook.epub
```

#### 6.5 生成 mobi 格式的电子书：

``` bash
$ gitbook mobi ./ ./JavaBook.mobi
```

#### 6.6 查看GitBook版本

``` bash
$  gitbook -V  # V大写
```
---
建议添加到Github做版本管理控制


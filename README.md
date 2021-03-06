# md2html

把文件夹下的 Markdown 文件，转化成 GitHub 风格的 HTML。

（代码高亮我用了自己喜欢的 Pygments 风格 ==）

### 应用举例

比如 @judasn 的 [judasn/IntelliJ-IDEA-Tutorial: IntelliJ IDEA 简体中文专题教程](https://github.com/judasn/IntelliJ-IDEA-Tutorial)。
首先下载它的源码，解压后进入文件夹 `IntelliJ-IDEA-Tutorial`。

下载 [`md2html.jar`](https://github.com/district10/md2html/releases)，然后把 `jar` 文件放到根目录，
然后运行 `java -jar md2html.jar`（或者双击它），就有
`../IntelliJ-IDEA-Tutorial-master-publish` 文件夹。打开里面的 `README.html`（或者 `index.html`） 看效果。

我把生成的网页上传到了网盘，在线查看：<http://whudoc.qiniudn.com/2016/IntelliJ-IDEA-Tutorial>。

注：生成的 HTML 会自动转化 `.md` 路径为 `.html`。

## 安装使用

`jar` 文件的运行，需要 JRE（Java Runtime）的支持，可以在这里下载：[Download Free Java Software](https://java.com/en/download/)。

Pandoc 是内部用来转化 Markdown 的工具，下载地址：

-   Windows：<http://doi-2014.qiniudn.com/pandoc/pandoc-1.17.0.2-windows.msi> (20.4 MB)
-   Linux：<https://github.com/jgm/pandoc/releases/download/1.17/pandoc-1.17-1-amd64.deb> (19.9 MB)，安装指令：`sudo dpkg -i pandoc*.deb`
-   Mac OSX：<https://github.com/jgm/pandoc/releases/download/1.17.2/pandoc-1.17.2-osx.pkg> (35.9 MB)

### `md2html.jar` 使用

除了 `java -jar md2html.jar` 这种简单的使用，还可以指定一些参数，比如输入目录和输出目录，
下面是使用方法：

```bash
# 当前文件夹拷贝到 ../<当前文件夹名称>-publish，并转化其中的 .md 文件
$ java -jar md2html.jar

# 指定输入、输出文件夹
$ java -jar md2html.jar -i source_dir -o publish_dir
$ java -jar md2html.jar -input source_dir -output publish_dir
```

如果安装了浏览器自动更新的插件，比如 [Auto Reload :: Firefox 附加组件](https://addons.mozilla.org/zh-CN/firefox/addon/auto-reload/?src=api)，
还可以自动刷新。这样，把浏览器和编辑器对半放，然后运行 `jar` 程序，就可以实时预览了~

### `md2html.jar` 的打包:

#### 方法 1，利用 IntelliJ IDEA 的 Artifact

用 IntelliJ IDEA 打开这个工程应该就可以生成 `md2html.jar`。

#### 方法 2，利用 Makefile 打包

如果没有 `make`，安装之，下载地址：<https://github.com/whudoc/statics/raw/master/winbin/make.exe> (218 KB)，放到 %PATH%（比如 `C:\Windows\System32`）里即可。

如果没有 `zip`，安装之，下载地址：<https://github.com/whudoc/statics/raw/master/winbin/zip.exe> (298 KB)，放到 %PATH% 里即可。

最后，`make md2html.jar`，当前目录即有文件 `md2html.jar`。

（在 Windows 和 Linux 上测试通过，均可以正确生成 `jar` 包。）

## 更多参数的配置

可以输入 `java -jar md2html.jar -help` 查看帮助：

```
Usage:
    $ java -jar md2html.jar

Options:
    -i, -input <SOURCE DIRECTORY>
           specify root of markdown files
    -o, -output <DESTINATION DIRECTORY>
           specify root of output files
    -w, -watch
           watch mode
    -s, -silent
           silent mode
    -v, -verbose
           verbose mode
    -e, -expand
           expand markdown files
    -f, -fold
           fold markdown contents
    -g, -generateCodeFragment
           generate code fragment

More Usage Examples
   1. current dir to ../publish:
       $ java -jar md2html.jar -i . -o ../publish
   2. turn on watch, expand markdown
       $ java -jar md2html.jar -we
```

现在默认不 watch 了。

## Notice

如果出现乱码，请在运行 jar 文件的时候加上：`-Dfile.encoding=utf-8`。

参考：

-   [utf 8 - Setting the default Java character encoding? - Stack Overflow](http://stackoverflow.com/questions/361975/setting-the-default-java-character-encoding)

## TODO

更多的 options：

-   文件映射
    -   noDefaultFileMappings
    -   extraFileMappings
-   URL 映射
    -   noDefaultUrlMappings
    -   extraUrlMappings
-   CSS，JS
    -   noDefaultCSS
    -   noDefaultJS
    -   extraCSSs
    -   extraJSs
-   Debug 模式
    -   debug
-   GitHub Pages 兼容模式
    -   githubPagesCompatiable
-   分词和搜索
    -   [yanyiwu/cppjieba: "结巴"中文分词的C++版本](https://github.com/yanyiwu/cppjieba)
    -   [huaban/jieba-analysis: 结巴分词(java版)](https://github.com/huaban/jieba-analysis)
    -   [yanyiwu/simhash: 中文文档simhash值计算](https://github.com/yanyiwu/simhash)
    -   参考：[jQuery-based Local Search Engine for Hexo | HaHack](http://hahack.com/codes/local-search-engine-for-hexo/)
    -   自动 tagging 功能

最后，最重要的 TODO：不要 dive into this project。Try WebSock intead！学 Java，要全面不能囿于一室。

其他格式的处理，比如 org-mode。

## Credits

-   [Pandoc](https://github.com/jgm/pandoc)（Markdown 转化）
-   [Github Markdown CSS](https://github.com/sindresorhus/github-markdown-css)（Github 风格的 CSS）
-   jQuery，lazyload.js（图片延迟加载）
-   [我的笔记本](http://tangzx.qiniudn.com/notes/)（使用类似方法生成的 HTML，我复用了自己笔记的 js，css 以及 HTML 模板）

## TEST

这是增强的 Markdown，在 GitHub 上不能正确渲染。请本地查看。

（这部分功能还有些 bug。）

### 代码折叠功能

这部分会被隐藏 -<

:   doc1 是一个文档：[doc1.md](demo/doc1.md)。

    code1 是一段代码：[demo/code1.h](demo/code1.h)。

    code1 是一段代码：[demo/code1.h](demo/code1.h)。

    code1 是一段代码：[demo/code1.h](demo/code1.h)。

    code1 是一段代码：[demo/code1.h](demo/code1.h)。

    code1 是一段代码：[demo/code1.h](demo/code1.h)。

    code1 是一段代码：[demo/code1.h](demo/code1.h)。

    code1 是一段代码：[demo/code1.h](demo/code1.h)。

    喋喋不休，我要取关你！

这部分可以被隐藏，但初始化为打开 +<

:   doc1 是一个文档：[doc1.md](demo/doc1.md)。

    code1 是一段代码：[demo/code1.h](demo/code1.h)。

    code1 是一段代码：[demo/code1.h](demo/code1.h)。

    code1 是一段代码：[demo/code1.h](demo/code1.h)。

    code1 是一段代码：[demo/code1.h](demo/code1.h)。

    code1 是一段代码：[demo/code1.h](demo/code1.h)。

    code1 是一段代码：[demo/code1.h](demo/code1.h)。

    code1 是一段代码：[demo/code1.h](demo/code1.h)。

    喋喋不休，我要取关你！

### 文件引入

引入代码：

```cpp
@include <-=demo/code2.h=
```

诗句引入：

@include <-|   =demo/poem.txt=

Markdown 源码中如果没有“|”字符，引入后会合并行（所以这叫诗句引入）：

@include <-=demo/poem.txt=

多层次的引入还有一些环和 pading 的问题。

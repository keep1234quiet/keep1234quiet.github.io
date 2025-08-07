---
layout: post
title:  "修改已发布的VSCode插件better-align"
date:   2025-08-06 21:20:00 +0000
categories: vscode plugin
---

### 问题：
修改的插件是better-align，在编写Python代码的过程中，发现其无法对Python的注释进行格式化，也无法通过配置文件修改；

因此从其github下载源码，修改后重新编译实现；

修改后的better-align安装文件：
1.  [google drive 下载](https://links.jianshu.com/go?to=https://drive.google.com/file/d/1ZmCV5z0g-v0u54tqH0696CsNw_1ZRuoo/view?usp=sharing)
2.  [蓝奏云下载](https://links.jianshu.com/go?to=https://wwb.lanzouf.com/ib98I08m9r1i)

源码地址：[https://github.com/WarWithinMe/better-align](https://github.com/WarWithinMe/better-align)

由于原作者已将仓库归档，故自己来修改了，Issues里还是能看到有人有这个疑问的，其他有需求的小伙伴也可以自行修改；

修改源码目录下的`formatter.ts`文件

总共需要修改两处：

修改注释的条件判断：
```typescript
else if ( (char == "/" && (
          (next == "/" && (pos > 0 ? text.charAt(pos-1) : "") != ":") // only `//` but not `://`
        || next == "*")) || char == "#" )
```

新增下面这段代码：
```typescript
if(char == "#"){
  pos = text.length;
}
```

在better-align目录下使用命令`npm install`安装package.json中的包依赖，可能会遇到一些错误，网络问题导致包下载出错或是一些版本问题，自己百度解决就好；

安装库：`npm i vsce -g`

重新编译生成用于VSCode安装的文件：

安装方式：手动安装

注：安装过程中可能会遇到环境变量无法及时更新的问题，win10只要关闭CMD窗口后重新打开，环境变量就会自动刷新；但是win11好像不太行，我这里是安装了chocolatey，通过使用命令：`refreshenv`就可以了

### 遇到的一些问题：
1.  `readme.md` 文件中的SVG图标需要修改成HTTPS的才能编译通过；
2.  使用`npm install`安装依赖包的时候出了问题，这个链接指向的`vscode.d.ts`文件找不到，404了，但在`./node_modules/vscode`路径下这个文件是存在的，但是后来尝试编译也通过了，就没管他了；这个VS Code engine是可以在`package.json`文件中指定的，或需要结合自己本地的VSCode版本？这个我也不太确定；
3.  使用过程中还安装了一个脚手架`npm install -g yo generator-code`，这个是用于生成插件模板的，但我好像没用上；

### 参考链接：
1.  [https://www.cnblogs.com/zhaoqingqing/p/14823179.html](https://www.cnblogs.com/zhaoqingqing/p/14823179.html)
2.  [https://www.jianshu.com/p/e642856f6044](https://www.jianshu.com/p/e642856f6044)

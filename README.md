## 一、发布环境

### 测试环境
name: test  
url: `https://{app}.test.liruan.cn/`

### 预生产环境
name: beta  
url: `https://{app}.beta.liruan.cn/`

### 生产环境
name: prod  
url: `https://www.{app}.cn/` 或 `https://{app}.prod.liruan.cn/`

## 二、分支
### master
最为稳定，功能最为完整的，随时可发布的代码。可发布到 beta 和 prod，在 beta 上走查无误方可发布到 prod。

### develop
永远是功能最新最全的分支。新特性的起点。

### feature/*
新特性开发。

### release/*
发布到 test，提测、BUG 修复。

### hotfix/*
线上 BUG 修复。

## 三、流程

### 新特性开发
1. 接到一个新产品特性 a；
2. 从 develop 分出新分支 feature/a；
3. 在 feature/a 开发特性 a；
4. 完成开发后，请和 QA 一起进行 MSC（Mini Show Case），演示特性 a，并及时修复发现的问题；
5. MSC 完成后，结束特性 a，代码合并到 develop；

### 提测
![](images/merge.gif)

### 修复线上 BUG
1. 从 master 分出新分支 hotfix/v1.2.1；
2. 修复 BUG；
3. 完成 BUG 修复，结束 hotfix/v1.2.1，代码合并到 develop 和 master；

## 四、域名转发
如果 QA 因为某些原因，需要在 beta 或 prod 测试，建议其使用 fiddler 做域名转发。步骤如下：
> 请保证测试代码已发布至 test，且接口域名与项目域名不一致。
1. 切到 fiddler 右边面板的 AutoResponser；
2. 选中下面的 Enable Rules 和 Unmatched requests passthrough 复选框；
3. 点击 Add Rule；
4. 右下角第一个输入框输入：`regex:https://{app}.cn/(.*)`；
5. 第二个输入框输入：`http://{app}.test.liruan.cn/$1`；
6. 点击 Save；

## 五、注意
1. 用于发布的分支有 master、release/*，所以只能在这两个分支上构建代码，减少合并时的冲突；
2. 另外，可以在构建目录（如：dist）的上一级目录下放置 [.gitattributes](https://github.com/zhaotoday/product-workflow/blob/master/.gitattributes) 文件，减少构建代码冲突；

## 六、部署系统
推荐使用：[瓦力上线部署](https://walle-web.io/)

## 七、参考
- http://danielkummer.github.io/git-flow-cheatsheet/index.zh_CN.html
- http://www.imooc.com/learn/751  
- http://www.qianduan.org/post-447.html  
- http://danielkummer.github.io/git-flow-cheatsheet/index.zh_CN.html  
- https://raw.githubusercontent.com/arslanbilal/git-cheat-sheet/master/Img/git-flow-commands-without-flow.png  
- https://github.com/arslanbilal/git-cheat-sheet/blob/master/other-sheets/git-cheat-sheet-zh.md
- https://ourai.ws/posts/working-with-git-in-team/

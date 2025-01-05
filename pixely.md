# Pixely Launcher 像素启动器

## 介绍

### 这是什么

这是一个`Minecraft` `启动器`，其指一类能够创建、管理和启动`Minecraft` `实例`的桌面软件。

`Minecraft`是一个沙盒类电脑游戏。这个游戏有以下几个特点使其与一般的电脑游戏不同：

1. Minecraft使用Java编写。
2. Minecraft从最初发布直到现在的15年时间内经历了无数次版本/内容更新。
3. Minecraft的玩家社区非常活跃。
4. 结合1和3，基于Java易于反编译的特点，大量技术型玩家对游戏的Java二进制码进行了反编译和反混淆，为游戏制作了海量的修改插件（玩家们称之为`Mod`，取自Modification的前三个字母）。
5. 结合2和4，游戏版本的更新时常会破坏Mod的正常运行。因此，玩家和Mod制作者们经常会选择停留在某些特定旧版本而不更新。

因此，在Minecraft玩家群体之间有这么一个“最佳实践”：**将游戏像Python虚拟环境一样分成一个个“实例”：你可以创建一个最新版本游戏的实例来体验游戏的新内容，也可以创建一个较旧版本的实例，安装可用于这个版本的各种Mod，来体验玩家们创作的内容。**

而以上的工作，就需要通过特定的软件来实现了。Python有venv/Conda/pipenv，而对于Minecraft而言，对应的软件被叫做`启动器`。

### 如何实现

要实现创建、管理、启动Minecraft实例这些功能，一个启动器需要：

- 能够下载并安装游戏文件和Mod。
- 借助游戏开发者提供的API验证和登录游戏账号。
- 校验游戏文件，生成启动参数，并从JRE启动游戏。
- 提供一个简明的UI供用户使用。

## 项目结构
### light-engine
一个多线程异步的HTTP下载器。<br>
[github.com/pixely-dev-team/light-engine](https://github.com/Pixely-Dev-Team/light-engine)
### rasterizer-core
启动器核心功能库。
### rasterizer-cli
启动器命令行界面。
### pixely-desktop
使用Tauri框架构建的桌面应用，提供GUI。
### pixely-ui
React组件库。
### pixely-icon
图标库。
### photon
衍生项目。一个使用Tauri框架构建的简单的桌面HTTP下载器。主要目的是验证light-engine，同时熟悉Tauri的API及跨平台适配能力。

## rasterizer-cli

### rastr new
```
rastr new <instance-name> <minecraft-version>
```
新建实例

### rastr install
```
rastr install <instance-name> (--forge | --fabric | --qulit | --neoforge | --rift | --liteloader | --optifine) [version]
```
安装实例核心组件

### rastr launch
```
rastr launch <instance-name> [--account <username>] [--offline <username>] [--jre <path>] [--mem <size>] [--custom-args <args>]
```
启动实例

### rastr list
```
rastr list (--instances | --versions (--minecraft | --forge <minecraft-version> | --fabric <minecraft-version> | --qulit <minecraft-version> | --neoforge <minecraft-version> | --rift <minecraft-version> | --liteloader <minecraft-version> | --optifine <minecraft-version>) | --instance <instance-name> (--mods | --respacks | --shaders | --saves))
```

### rastr get
```
rastr get <instance-name> <mod | respack | datapack | shader> <name>
```
从Modrinth为指定实例获取内容

### rastr search
```
rastr search <mod | respack | datapack | shader> <search-term>
```
从Modrinth搜索内容

### rastr login
```
rastr login (--ms | --custom <url>)
```

### rastr manage
```
rastr manage <instance-name>
```
进入实例管理界面
```
$ rastr manage NebulaeCraft
rasterizer@NebulaeCraft >
```
在这里你可以直接下载Modrinth内容，列出已下载的内容或是所有的存档等，方便对实例进行管理。

### rastr conf
```
rastr conf (--get <key> | --set <key> <value> | --unset <key>)
```
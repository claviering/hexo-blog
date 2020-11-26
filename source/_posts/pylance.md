---
title: pylance 一款对 Python 快速，功能丰富的 VSCode 插件
date: 2020-11-26 17:00:29
tags:
- vscode
---

Pylance可与VScode中的Python插件一起使用的一个插件，以提供高性能的语言支持。 在后台，Pylance由Microsoft的静态类型检查工具Pyright提供支持。 使用Pyright，Pylance可以为Python IntelliSense体验提供丰富的类型信息，从而帮助您更快地编写更好的代码。

Pylance名称是Monty Python的Lancelot的一个小颂歌，Lancelot是第一个在圣杯中回答守门员问题的骑士。

[Github](https://github.com/microsoft/pylance-release)

## 快速开始

1. 安装Pylance扩展。
2. 打开一个Python（.py）文件，Pylance扩展名将被激活。
3. 当提示您将Pylance设置为默认语言服务器时，选择“是”。 这将更新您的首选项，也可以通过使用文本编辑器将“ python.languageServer”：“ Pylance”添加到settings.json文件中来手动进行。

## 功能

![ screencast ](screencap.gif)

Pylance为Python 3提供了一些很棒的功能，包括：

- 字串
- 签名帮助，带有类型信息
- 参数建议
- 代码补全
- 自动导入（以及添加和删除导入代码操作）
- 输入代码的时候报告代码错误和警告（诊断）
- 代码大纲
- 代码导航
- 类型检查模式
- 本地多个工作区支持
- IntelliCode 兼容性
- Jupyter Notebooks 兼容性
- 语法高亮

See the changelog for the latest release.

## 语法高亮

![](https://static01.imgkr.com/temp/5ef2524639934389b5041e84652af945.gif)

Visual Studio Code使用TextMate语法作为主要的标记引擎。 TextMate语法作为输入处理单个文件，并根据以正则表达式表示的词汇规则将其分解。

语义标记化允许语言服务器基于语言服务器有关如何在项目上下文中解析符号的知识来提供其他令牌信息。 主题可以选择使用语义标记来改善和完善语法中的语法突出显示。 编辑器将语义标记中的突出显示应用于语法中的突出显示。

这是一个语义突出显示可以添加的示例：

没有语法高亮:

![ semantic highlighting disabled ](https://static01.imgkr.com/temp/38ddc5418e0e4bc7b48f0946ab7fe9f8.png)

语法高亮:

![ semantic highlighting enabled ](https://static01.imgkr.com/temp/611f8bbd0fcd44b38b7e9cca0d510de6.png)

可以通过将Pylance语义标记类型和修饰符与所需颜色相关联，在settings.json中自定义语义颜色。


- 类型
    - class, enum
    - parameter, variable, property, enumMember
    - function, member
    - module
    - intrinsic
    - magicFunction (dunder methods)
    - selfParameter, clsParameter

- 修饰符
    - declaration
    - readonly, static, abstract
    - async
    - typeHint, typeHintComment
    - decorator
    - builtin

范围检查器工具使您可以探索源文件中存在哪些语义标记以及它们匹配的主题规则。

在settings.json中定制语义颜色的示例：

```
{
    "editor.semanticTokenColorCustomizations": {
        "[One Dark Pro]": { // Apply to this theme only
            "enabled": true,
            "rules": {
                "magicFunction:python": "#ee0000",
                "function.declaration:python": "#990000",
                "*.decorator:python": "#0000dd",
                "*.typeHint:python": "#5500aa",
                "*.typeHintComment:python": "#aaaaaa"
            }
        }
    }
}
```
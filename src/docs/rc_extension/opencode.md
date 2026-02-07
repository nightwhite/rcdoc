---
title: 配置在OpenCode使用
icon: mynaui:code-waves
order: 1
footer: false
---

## 手把手教你配置OpenCode

1. 下载 [OpenCode(带御三家+缓存)](/assets/file/opencode/QuickConfiguration.zip) 压缩包，解压后得到以下文件

![](/assets/image/rc_extension/opencode/rc-01.webp)

2. 打开 `opencode.json` 文件，分别为 `Gemini` `Claude` `GPT` 部分配置相应的APIKEY，保存配置文件

::: important
注意查看 [ApiKey生成](/docs/rc_quick_start/apikey.html#如何生成apikey) 教程，要生成正确渠道的key，`可用渠道` 记得选择 ，`可用模型` 保持默认即可
:::

![Gemini配置](/assets/image/rc_extension/opencode/rc-02.webp)

![Claude配置](/assets/image/rc_extension/opencode/rc-03.webp)

![GPT配置](/assets/image/rc_extension/opencode/rc-04.webp)

3. 找到OpenCode的配置文件夹

:::important
如果你是初次配置，请先使用以下命令在终端安装OpenCode，并运行一次
```bash
npm i -g opencode-ai
```

运行OpenCode
```bash
opencode
```
:::

> 首先打开你的终端程序，不管你是Windows还是MacOS系统
> 然后根据系统，运行下面的命令，打开opencode的配置文件夹

:::tabs
@tab Windows
CMD命令行：
```bash
start "" "%USERPROFILE%\.codex"
```

@tab MacOS
```bash
open "$HOME/.codex"
```
:::

![](/assets/image/rc_extension/opencode/rc-05.webp)

4. 将刚才你修改好的 `opencode.json` 与 `plugins` 目录复制到opencode的配置文件夹

![](/assets/image/rc_extension/opencode/rc-06.webp)

5. 在终端运行 `opencode` ，使用 `/models` 命令来查看配置是否成功

![](/assets/image/rc_extension/opencode/rc-07.webp)
---
title: Windows 系统下配置 WSL 运行 AI 终端
icon: mynaui:code-waves
order: 1
footer: false
---

## 什么是 WSL？为什么要配置 WSL？

WSL=Windows Subsystem For Linux，可以让你在 Windows 下几乎无感地运行 Linux 子系统，无需配置和运行虚拟机软件。
由于大部分 AI 原生在 Linux 系统上训练，使用 WSL 运行AI终端，通常能获得比直接在 Windows 上运行更好的体验。

## 配置 WSL


打开命令行并执行：

```bash
wsl --install
```

安装完成后，按提示配置用户并重启。重启后执行以下命令：

```bash
wsl -l -v
```

通常你会看到已经安装了一个 Ubuntu 作为默认发行版。
<img src="/assets/image/rc_extension/wsl/rc-1.webp" width="600" style="display:block;margin:0 auto;height:auto;" />
打开终端并输入 wsl 来连接到相应 wsl 
<img src="/assets/image/rc_extension/wsl/rc-2.webp" width="600" style="display:block;margin:0 auto;height:auto;" />

:::tip
如果输入 `wsl --install` 无反应，尝试用wsl.exe替换wsl
:::

:::tabs
@tab 卸载已经安装的发行版
```bash
wsl --unregister <DistributionName>
```

> 1.如果您想要卸载刚才安装的默认Ubuntu：
```bash
wsl --list --verbose
```

> 2.此时你应该会在命令行中看到已安装的发行版名称，如Ubuntu-24.04. 通过以下命令即可卸载
```
wsl --unregister Ubuntu-24.04
```

@tab 指定位置安装发行版
```bash
wsl --install <DistributionName> --location ""
```

> 1.在目标位置创建新文件夹，如D:\wsl
> 2.通过此命令安装Ubuntu-24.04
```bash
wsl --install Ubuntu-24.04 --location "D:\wsl"
```

@tab 更多相关参数
https://learn.microsoft.com/en-us/windows/wsl/basic-commands#install
:::



## 在WSL中使用Codex或其他AI终端
打开命令行，输入WSL登录到默认的WSL
由于WSL是全新的系统，你仍然需要重新安装你的AI终端。

> 首先安装nodejs和npm（此处使用nvm管理）:
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc

nvm install 22
nvm use 22
```

<img src="/assets/image/rc_extension/wsl/rc-3.webp" width="600" style="display:block;margin:0 auto;height:auto;" />

> 然后通过npm安装codex

```bash
npm install -g openai@codex
```

<img src="/assets/image/rc_extension/wsl/rc-4.webp" width="600" style="display:block;margin:0 auto;height:auto;" />

> WSL和Windows的配置文件不互通
> 因此，我们需要在WSL中导入一份配置文件

:::tabs
@tab 手动导入
> 1.手动复制以下路径中的.codex或.claude配置文件夹：
<img src="/assets/image/rc_extension/wsl/rc-5.webp" width="600" style="display:block;margin:0 auto;height:auto;" />

```bash
C:\Users\<your-user-name>
```


> 2.在资源管理器中输入以下路径（或从左下角小企鹅手动进入此路径）：

<img src="/assets/image/rc_extension/wsl/rc-6.webp" width="600" style="display:block;margin:0 auto;height:auto;" />

```bash
\\wsl.localhost\<Your-Distro-Name>\home\<Your-User-Name>
```

<img src="/assets/image/rc_extension/wsl/rc-7.webp" width="600" style="display:block;margin:0 auto;height:auto;" />
> 3.将刚才复制的文件夹粘贴到此文件夹下并重新启动AI终端即可

@tab 通过Windows下的CC-Switch导入

> 1.点击左上角的齿轮状设置按钮->高级->配置文件目录
<img src="/assets/image/rc_extension/wsl/rc-8.webp" width="600" style="display:block;margin:0 auto;height:auto;" />
> 2.将路径修改为(以Codex为例)

```bash
\\wsl.localhost\<Your-Distro-Name>\home\<Your-User-Name>\.codex
```
:::
 
> 现在你应该能够在windows目录中唤起wsl，然后在wsl中正常使用codex
> 如果你觉得麻烦，请看下一节
<img src="/assets/image/rc_extension/wsl/rc-9.webp" width="600" style="display:block;margin:0 auto;height:auto;" />


## 使用Vscode与WSL协作（以CodeX拓展为例）


:::tabs
@tab Vscode留在Windows中
**在不连接WSL，在windows目录下工作的前提下：**
<img src="/assets/image/rc_extension/wsl/rc-10.webp" width="600" style="display:block;margin:0 auto;height:auto;" />
如图所示，在Vscode Codex拓展右上角设置中点选Windows设置-在WSL中运行，然后重新加载vscode窗口即可
如右上角无相关设置：
使用ctrl+,进入vscode设置页面，搜索codex，点选"Run Codex In Windows Subsystem For Linux"设置即可



@tab Vscode连接到WSL
点击左下角的亮色 >< 状按钮

<img src="/assets/image/rc_extension/wsl/rc-11.webp" width="600" style="display:block;margin:0 auto;height:auto;" />

选择"Connect to WSL Using Distro"

<img src="/assets/image/rc_extension/wsl/rc-12.webp" width="600" style="display:block;margin:0 auto;height:auto;" />

选择你在上一节中迁移过配置文件的Linux发行版

<img src="/assets/image/rc_extension/wsl/rc-13.webp" width="600" style="display:block;margin:0 auto;height:auto;" />

此时，vscode已经连接到指定WSL.
重新安装CodeX CLI此时直接唤起CodeX拓展即可使用.
此时在terminal或扩展中唤起相应AI终端即可
**如发现拓展需登录，重新回看第二节：在WSL中使用Codex或其他AI终端 中的配置迁移部分**
:::

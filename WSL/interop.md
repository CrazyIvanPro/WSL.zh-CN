---
title: Windows 与 Linux 的互操作性
description: 介绍 Windows 与适用于 Linux 的 Windows 子系统上运行的 Linux 分发版之间的互操作性。
ms.date: 05/12/2020
ms.topic: article
ms.localizationpriority: high
ms.openlocfilehash: b1c7a64a86cf088159d1abee3b341328151428f6
ms.sourcegitcommit: 1b6191351bbf9e95f3c28fc67abe4bf1bcfd3336
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/13/2020
ms.locfileid: "83270841"
---
# <a name="windows-interoperability-with-linux"></a><span data-ttu-id="39902-103">Windows 与 Linux 的互操作性</span><span class="sxs-lookup"><span data-stu-id="39902-103">Windows interoperability with Linux</span></span>

<span data-ttu-id="39902-104">适用于 Linux 的 Windows 子系统 (WSL) 正在持续改进 Windows 与 Linux 之间的集成。</span><span class="sxs-lookup"><span data-stu-id="39902-104">The Windows Subsystem for Linux (WSL) is continuously improving integration between Windows and Linux.</span></span>  <span data-ttu-id="39902-105">您可以：</span><span class="sxs-lookup"><span data-stu-id="39902-105">You can:</span></span>

* <span data-ttu-id="39902-106">从 Linux 命令行（即 Ubuntu）运行 Windows 工具（即 notepad.exe）。</span><span class="sxs-lookup"><span data-stu-id="39902-106">Run Windows tools (ie. notepad.exe) from a Linux command line (ie. Ubuntu).</span></span>
* <span data-ttu-id="39902-107">从 Windows 命令行（即 PowerShell）运行 Linux 工具（即 grep）。</span><span class="sxs-lookup"><span data-stu-id="39902-107">Run Linux tools (ie. grep) from a Windows command line (ie. PowerShell).</span></span>
* <span data-ttu-id="39902-108">在 Windows 与 Windows 之间共享环境变量。</span><span class="sxs-lookup"><span data-stu-id="39902-108">Share environment variables between Linux and Windows.</span></span> <span data-ttu-id="39902-109">（版本 17063+）</span><span class="sxs-lookup"><span data-stu-id="39902-109">(Build 17063+)</span></span>

> [!NOTE]
> <span data-ttu-id="39902-110">如果运行的是创意者更新（2017 年 10 月的版本16299）或周年更新（2016 年 8 月的版本 14393），请跳转到 [Windows 10 的早期版本](#earlier-versions-of-windows-10)。</span><span class="sxs-lookup"><span data-stu-id="39902-110">If you're running Creators Update (Oct 2017, Build 16299) or Anniversary Update (Aug 2016, Build 14393), jump to the [Earlier versions of Windows 10](#earlier-versions-of-windows-10).</span></span>

## <a name="run-linux-tools-from-a-windows-command-line"></a><span data-ttu-id="39902-111">从 Windows 命令行运行 Linux 工具</span><span class="sxs-lookup"><span data-stu-id="39902-111">Run Linux tools from a Windows command line</span></span>

<span data-ttu-id="39902-112">使用 `wsl <command>`（或 `wsl.exe <command>`）从 Windows 命令提示符 (CMD) 或 PowerShell 运行 Linux 二进制文件。</span><span class="sxs-lookup"><span data-stu-id="39902-112">Run Linux binaries from the Windows Command Prompt (CMD) or PowerShell using `wsl <command>` (or `wsl.exe <command>`).</span></span>

<span data-ttu-id="39902-113">例如：</span><span class="sxs-lookup"><span data-stu-id="39902-113">For example:</span></span>

```powershell
C:\temp> wsl ls -la
<- contents of C:\temp ->
```

<span data-ttu-id="39902-114">以这种方式调用二进制文件：</span><span class="sxs-lookup"><span data-stu-id="39902-114">Binaries invoked in this way:</span></span>

* <span data-ttu-id="39902-115">使用当前 CMD 或 PowerShell 提示符中提到的同一工作目录。</span><span class="sxs-lookup"><span data-stu-id="39902-115">Use the same working directory as the current CMD or PowerShell prompt.</span></span>
* <span data-ttu-id="39902-116">以 WSL 默认用户的身份运行。</span><span class="sxs-lookup"><span data-stu-id="39902-116">Run as the WSL default user.</span></span>
* <span data-ttu-id="39902-117">拥有与调用方进程和终端相同的 Windows 管理权限。</span><span class="sxs-lookup"><span data-stu-id="39902-117">Have the same Windows administrative rights as the calling process and terminal.</span></span>

<span data-ttu-id="39902-118">`wsl`（或 `wsl.exe`）后面的 Linux 命令的处理方式与 WSL 中运行的任何命令的处理方式类似。</span><span class="sxs-lookup"><span data-stu-id="39902-118">The Linux command following `wsl` (or `wsl.exe`) is handled like any command run in WSL.</span></span>  <span data-ttu-id="39902-119">可以执行 sudo、管道处理和文件重定向等操作。</span><span class="sxs-lookup"><span data-stu-id="39902-119">Things such as sudo, piping, and file redirection work.</span></span>

<span data-ttu-id="39902-120">使用 sudo 更新默认 Linux 分发版的示例：</span><span class="sxs-lookup"><span data-stu-id="39902-120">Example using sudo to update your default Linux distribution:</span></span>

```powershell
C:\temp> wsl sudo apt-get update
```

<span data-ttu-id="39902-121">运行此命令后，将会列出默认的 Linux 分发版用户名，并将要求你输入密码。</span><span class="sxs-lookup"><span data-stu-id="39902-121">Your default Linux distribution user name will be listed after running this command and you will be asked for your password.</span></span> <span data-ttu-id="39902-122">正确输入密码后，分发版将下载更新。</span><span class="sxs-lookup"><span data-stu-id="39902-122">After entering your password correctly, your distribution will download updates.</span></span>

## <a name="mixing-linux-and-windows-commands"></a><span data-ttu-id="39902-123">混合 Linux 和 Windows 命令</span><span class="sxs-lookup"><span data-stu-id="39902-123">Mixing Linux and Windows commands</span></span>

<span data-ttu-id="39902-124">下面是几个使用 PowerShell 混合 Linux 和 Windows 命令的示例。</span><span class="sxs-lookup"><span data-stu-id="39902-124">Here are a few examples of mixing Linux and Windows commands using PowerShell.</span></span>

<span data-ttu-id="39902-125">若要使用 Linux 命令 `ls -la` 列出文件，并使用 PowerShell 命令 `findstr` 来筛选包含“git”的单词的结果，请组合这些命令：</span><span class="sxs-lookup"><span data-stu-id="39902-125">To use the Linux command `ls -la` to list files and the PowerShell command `findstr` to filter the results for words containing "git", combine the commands:</span></span>

```powershell
wsl ls -la | findstr "git"
```

<span data-ttu-id="39902-126">若要使用 PowerShell 命令 `dir` 列出文件，并使用 Linux 命令 `grep` 来筛选包含“git”的单词的结果，请组合这些命令：</span><span class="sxs-lookup"><span data-stu-id="39902-126">To use the PowerShell command `dir` to list files and the Linux command `grep` to filter the results for words containing "git", combine the commands:</span></span>

```powershell
C:\temp> dir | wsl grep git
```

<span data-ttu-id="39902-127">若要使用 Linux 命令 `ls -la` 列出文件，并使用 PowerShell 命令 `> out.txt` 将该列表输出到名为“out.txt”的文本文件，请组合这些命令：</span><span class="sxs-lookup"><span data-stu-id="39902-127">To use the Linux command `ls -la` to list files and the PowerShell command `> out.txt` to print that list to a text file named "out.txt", combine the commands:</span></span>

```powershell
C:\temp> wsl ls -la > out.txt
```

<span data-ttu-id="39902-128">传入 `wsl.exe` 的命令将按原样转发到 WSL 进程。</span><span class="sxs-lookup"><span data-stu-id="39902-128">The commands passed into `wsl.exe` are forwarded to the WSL process without modification.</span></span>  <span data-ttu-id="39902-129">文件路径必须以 WSL 格式指定。</span><span class="sxs-lookup"><span data-stu-id="39902-129">File paths must be specified in the WSL format.</span></span>

<span data-ttu-id="39902-130">若要使用 Linux 命令 `ls -la` 列出 `/proc/cpuinfo` Linux 文件系统路径中的文件，请使用 PowerShell：</span><span class="sxs-lookup"><span data-stu-id="39902-130">To use the Linux command `ls -la` to list files in the `/proc/cpuinfo` Linux file system path, using PowerShell:</span></span>

```powershell
C:\temp> wsl ls -la /proc/cpuinfo
```

<span data-ttu-id="39902-131">若要使用 Linux 命令 `ls -la` 列出 `C:\Program Files` Windows 文件系统路径中的文件，请使用 PowerShell：</span><span class="sxs-lookup"><span data-stu-id="39902-131">To use the Linux command `ls -la` to list files in the `C:\Program Files` Windows file system path, using PowerShell:</span></span>

```powershell
C:\temp> wsl ls -la "/mnt/c/Program Files"
```

## <a name="run-windows-tools-from-linux"></a><span data-ttu-id="39902-132">从 Linux 运行 Windows 工具</span><span class="sxs-lookup"><span data-stu-id="39902-132">Run Windows tools from Linux</span></span>

<span data-ttu-id="39902-133">WSL 可以使用 `[tool-name].exe` 直接从 WSL 命令行运行 Windows 工具。</span><span class="sxs-lookup"><span data-stu-id="39902-133">WSL can run Windows tools directly from the WSL command line using `[tool-name].exe`.</span></span>  <span data-ttu-id="39902-134">例如，`notepad.exe`。</span><span class="sxs-lookup"><span data-stu-id="39902-134">For example, `notepad.exe`.</span></span>

<!-- Craig - could you help add a section with an example here to explain this scenario: "To access your Linux files using a Windows tool, use `\\wsl$\<distroName>\'` as the file path." Currently it I can just enter `notepad.exe foo.txt` and it seems to work fine, so explaining a situation where the file path is needed would be helpful. -->

<span data-ttu-id="39902-135">以这种方式运行的应用程序具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="39902-135">Applications run this way have the following properties:</span></span>

* <span data-ttu-id="39902-136">按 WSL 命令提示保留工作目录（大部分情况下是这样 -- 下面所述的情况除外）。</span><span class="sxs-lookup"><span data-stu-id="39902-136">Retain the working directory as the WSL command prompt (for the most part -- exceptions are explained below).</span></span>
* <span data-ttu-id="39902-137">拥有与 WSL 进程相同的权限。</span><span class="sxs-lookup"><span data-stu-id="39902-137">Have the same permission rights as the WSL process.</span></span>
* <span data-ttu-id="39902-138">以活动 Windows 用户的身份运行。</span><span class="sxs-lookup"><span data-stu-id="39902-138">Run as the active Windows user.</span></span>
* <span data-ttu-id="39902-139">显示在 Windows 任务管理器中，就如同直接从 CMD 提示符执行的一样。</span><span class="sxs-lookup"><span data-stu-id="39902-139">Appear in the Windows Task Manager as if directly executed from the CMD prompt.</span></span>

<span data-ttu-id="39902-140">在 WSL 中运行的 Windows 可执行文件的处理方式类似于本机 Linux 可执行文件 - 管道处理、重定向，甚至后台处理都可按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="39902-140">Windows executables run in WSL are handled similarly to native Linux executables -- piping, redirects, and even backgrounding work as expected.</span></span>

<span data-ttu-id="39902-141">若要运行 Windows 工具 `ipconfig.exe`，请使用 Linux 工具 `grep` 筛选“IPv4”结果，并使用 Linux 工具 `cut` 删除列字段，请从 Linux 分发版（例如 Ubuntu）输入：</span><span class="sxs-lookup"><span data-stu-id="39902-141">To run the Windows tool `ipconfig.exe`, use the Linux tool `grep` to filter the "IPv4" results, and use the Linux tool `cut` to remove the column fields, from a Linux distribution (for example, Ubuntu) enter:</span></span>

```bash
ipconfig.exe | grep IPv4 | cut -d: -f2
```

<span data-ttu-id="39902-142">让我们尝试一个混合使用 Windows 和 Linux 命令的示例。</span><span class="sxs-lookup"><span data-stu-id="39902-142">Let's try an example mixing Windows and Linux commands.</span></span> <span data-ttu-id="39902-143">打开 Linux 分发版（即 Ubuntu）并创建文本文件：`touch foo.txt`。</span><span class="sxs-lookup"><span data-stu-id="39902-143">Open your Linux distribution (ie. Ubuntu) and create a text file: `touch foo.txt`.</span></span> <span data-ttu-id="39902-144">现在使用 Linux 命令 `ls -la` 列出直接文件及其创建详细信息，并使用 Windows PowerShell 工具 `findstr.exe` 来筛选结果，以便仅在结果中显示 `foo.txt` 文件：</span><span class="sxs-lookup"><span data-stu-id="39902-144">Now use the Linux command `ls -la` to list the direct files and their creation details, plus the Windows PowerShell tool `findstr.exe` to filter the results so only your `foo.txt` file shows in the results:</span></span>

```bash
ls -la | findstr.exe foo.txt
```

<span data-ttu-id="39902-145">Windows 工具必须包含文件扩展名，匹配文件大小写，并且可执行。</span><span class="sxs-lookup"><span data-stu-id="39902-145">Windows tools must include the file extension, match the file case, and be executable.</span></span>  <span data-ttu-id="39902-146">包含批处理脚本的不可执行文件。</span><span class="sxs-lookup"><span data-stu-id="39902-146">Non-executables including batch scripts.</span></span>  <span data-ttu-id="39902-147">`dir` 等 CMD 本机命令可与 `cmd.exe /C` 命令一起运行。</span><span class="sxs-lookup"><span data-stu-id="39902-147">CMD native commands like `dir` can be run with `cmd.exe /C` command.</span></span>

<span data-ttu-id="39902-148">例如，通过输入以下命令列出 Windows 文件系统 C:\ 目录的内容：</span><span class="sxs-lookup"><span data-stu-id="39902-148">For example, list the contents of your Windows files system C:\ directory, by entering:</span></span>

```bash
cmd.exe /C dir
```

<span data-ttu-id="39902-149">或者使用 `ping` 命令将回显请求发送到 microsoft.com 网站：</span><span class="sxs-lookup"><span data-stu-id="39902-149">Or use the `ping` command to send an echo request to the microsoft.com website:</span></span>

```bash
ping.exe www.microsoft.com
```

<span data-ttu-id="39902-150">参数将按原样传递到 Windows 二进制文件。</span><span class="sxs-lookup"><span data-stu-id="39902-150">Parameters are passed to the Windows binary unmodified.</span></span> <span data-ttu-id="39902-151">例如，以下命令将通过 `notepad.exe` 打开 `C:\temp\foo.txt`：</span><span class="sxs-lookup"><span data-stu-id="39902-151">As an example, the following command will open `C:\temp\foo.txt` in `notepad.exe`:</span></span>

```bash
notepad.exe "C:\temp\foo.txt"
```

<span data-ttu-id="39902-152">以下命令也会起作用：</span><span class="sxs-lookup"><span data-stu-id="39902-152">This will also work:</span></span>

```bash
notepad.exe C:\\temp\\foo.txt
```

## <a name="share-environment-variables-between-windows-and-wsl"></a><span data-ttu-id="39902-153">在 Windows 与 WSL 之间共享环境变量</span><span class="sxs-lookup"><span data-stu-id="39902-153">Share environment variables between Windows and WSL</span></span>

<span data-ttu-id="39902-154">WSL 和 Windows 共享一个特殊环境变量 `WSLENV`（为了桥接 Windows 和 WSL 上运行的 Linux 分发版而创建）。</span><span class="sxs-lookup"><span data-stu-id="39902-154">WSL and Windows share a special environment variable, `WSLENV`, created to bridge Windows and Linux distributions running on WSL.</span></span>

<span data-ttu-id="39902-155">`WSLENV` 变量的属性：</span><span class="sxs-lookup"><span data-stu-id="39902-155">Properties of `WSLENV` variable:</span></span>

* <span data-ttu-id="39902-156">它是共享的；它同时在 Windows 和 WSL 环境中存在。</span><span class="sxs-lookup"><span data-stu-id="39902-156">It is shared; it exists in both Windows and WSL environments.</span></span>
* <span data-ttu-id="39902-157">它是要在 Windows 与 WSL 之间共享的环境变量列表。</span><span class="sxs-lookup"><span data-stu-id="39902-157">It is a list of environment variables to share between Windows and WSL.</span></span>
* <span data-ttu-id="39902-158">它可以设置环境变量的格式，使其能够在 Windows 和 WSL 中正常运行。</span><span class="sxs-lookup"><span data-stu-id="39902-158">It can format environment variables to work well in Windows and WSL.</span></span>

> [!NOTE]
> <span data-ttu-id="39902-159">在 17063 以前，只有 WSL 可访问的 Windows 环境变量是 `PATH`（因此可以从 WSL 下启动 Win32 可执行文件）。</span><span class="sxs-lookup"><span data-stu-id="39902-159">Prior to 17063, only Windows environment variable that WSL could access was `PATH` (so you could launch Win32 executables from under WSL).</span></span> <span data-ttu-id="39902-160">从 17063 开始，`WSLENV` 开始受支持。</span><span class="sxs-lookup"><span data-stu-id="39902-160">Starting in 17063, `WSLENV` begins being supported.</span></span>

## <a name="wslenv-flags"></a><span data-ttu-id="39902-161">WSLENV 标志</span><span class="sxs-lookup"><span data-stu-id="39902-161">WSLENV flags</span></span>

<span data-ttu-id="39902-162">`WSLENV` 中有四个标志可以影响该环境变量的转换方式。</span><span class="sxs-lookup"><span data-stu-id="39902-162">There are four flags available in `WSLENV` to influence how the environment variable is translated.</span></span>

<span data-ttu-id="39902-163">`WSLENV` 标志：</span><span class="sxs-lookup"><span data-stu-id="39902-163">`WSLENV` flags:</span></span>

* <span data-ttu-id="39902-164">`/p` - 在 WSL/Linux 样式路径与 Win32 路径之间转换路径。</span><span class="sxs-lookup"><span data-stu-id="39902-164">`/p` - translates the path between WSL/Linux style paths and Win32 paths.</span></span>
* <span data-ttu-id="39902-165">`/l` - 指示环境变量是路径列表。</span><span class="sxs-lookup"><span data-stu-id="39902-165">`/l` - indicates the environment variable is a list of paths.</span></span>
* <span data-ttu-id="39902-166">`/u` - 指示仅当从 Win32 运行 WSL 时，才应包含此环境变量。</span><span class="sxs-lookup"><span data-stu-id="39902-166">`/u` - indicates that this environment variable should only be included when running WSL from Win32.</span></span>
* <span data-ttu-id="39902-167">`/w` - 指示仅当从 WSL 运行 Win32 时，才应包含此环境变量。</span><span class="sxs-lookup"><span data-stu-id="39902-167">`/w` - indicates that this environment variable should only be included when running Win32 from WSL.</span></span>

<span data-ttu-id="39902-168">可按需组合标志。</span><span class="sxs-lookup"><span data-stu-id="39902-168">Flags can be combined as needed.</span></span>

## <a name="disable-interoperability"></a><span data-ttu-id="39902-169">禁用互操作性</span><span class="sxs-lookup"><span data-stu-id="39902-169">Disable interoperability</span></span>

<span data-ttu-id="39902-170">用户可以使用 root 身份运行以下命令，禁用针对单个 WSL 会话运行 Windows 工具的功能：</span><span class="sxs-lookup"><span data-stu-id="39902-170">Users may disable the ability to run Windows tools for a single WSL session by running the following command as root:</span></span>

```bash
echo 0 > /proc/sys/fs/binfmt_misc/WSLInterop
```

<span data-ttu-id="39902-171">若要重新启用 Windows 二进制文件，请退出所有 WSL 会话并重新运行 bash.exe，或者以 root 身份运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="39902-171">To re-enable Windows binaries, exit all WSL sessions and re-run bash.exe or run the following command as root:</span></span>

```bash
echo 1 > /proc/sys/fs/binfmt_misc/WSLInterop
```

<span data-ttu-id="39902-172">每次切换 WSL 会话后，禁用互操作的结果不会持久保留 -- 启动新会话后，会再次启用互操作。</span><span class="sxs-lookup"><span data-stu-id="39902-172">Disabling interop will not persist between WSL sessions -- interop will be enabled again when a new session is launched.</span></span>

## <a name="earlier-versions-of-windows-10"></a><span data-ttu-id="39902-173">Windows 10 的早期版本</span><span class="sxs-lookup"><span data-stu-id="39902-173">Earlier versions of Windows 10</span></span>

<span data-ttu-id="39902-174">对于早期的 Windows 10 版本，互操作性命令有一些不同之处。</span><span class="sxs-lookup"><span data-stu-id="39902-174">There are several differences for the interoperability commands on earlier Windows 10 versions.</span></span> <span data-ttu-id="39902-175">如果运行的是创意者更新（2017 年10 月的版本 16299）或周年更新（2016 年 8 月的版本 14393），则建议你[更新到最新的 Windows 版本](ms-settings:windowsupdate)，但如果无法执行此操作，请了解下面概述的一些互操作差异。</span><span class="sxs-lookup"><span data-stu-id="39902-175">If you're running a Creators Update (Oct 2017, Build 16299), or Anniversary Update (Aug 2016, Build 14393) version of Windows 10, we recommend you [update to the latest Windows version](ms-settings:windowsupdate), but if that's not possible, we have outlined some of the interop differences below.</span></span>

<span data-ttu-id="39902-176">摘要：</span><span class="sxs-lookup"><span data-stu-id="39902-176">Summary:</span></span>

* <span data-ttu-id="39902-177">`bash.exe` 已替换为 `wsl.exe`。</span><span class="sxs-lookup"><span data-stu-id="39902-177">`bash.exe` has been replaced with `wsl.exe`.</span></span>
* <span data-ttu-id="39902-178">在 `wsl.exe` 中不需要指定用于运行单个命令的 `-c` 选项。</span><span class="sxs-lookup"><span data-stu-id="39902-178">`-c` option for running a single command isn't needed with `wsl.exe`.</span></span>
* <span data-ttu-id="39902-179">Windows 路径包含在 WSL `$PATH` 中。</span><span class="sxs-lookup"><span data-stu-id="39902-179">Windows path is included in the WSL `$PATH`.</span></span>
* <span data-ttu-id="39902-180">禁用互操作的过程未有变化。</span><span class="sxs-lookup"><span data-stu-id="39902-180">The process for disabling interop is unchanged.</span></span>

<span data-ttu-id="39902-181">可以从 Windows 命令提示或 PowerShell 运行 Linux 命令，但对于早期 Windows 版本，可能需要使用 `bash` 命令。</span><span class="sxs-lookup"><span data-stu-id="39902-181">Linux commands can be run from the Windows Command Prompt or from PowerShell, but for early Windows versions, you man need to use the `bash` command.</span></span> <span data-ttu-id="39902-182">例如：</span><span class="sxs-lookup"><span data-stu-id="39902-182">For example:</span></span>

```powershell
C:\temp> bash -c "ls -la"
```

<span data-ttu-id="39902-183">可按预期方式执行输入、管道处理和文件重定向等操作。</span><span class="sxs-lookup"><span data-stu-id="39902-183">Things such as input, piping, and file redirection work as expected.</span></span>

<span data-ttu-id="39902-184">传入 `bash -c` 的 WSL 命令将按原样转发到 WSL 进程。</span><span class="sxs-lookup"><span data-stu-id="39902-184">The WSL commands passed into `bash -c` are forwarded to the WSL process without modification.</span></span>  <span data-ttu-id="39902-185">必须以 WSL 格式指定文件路径，并且必须谨慎转义相关字符。</span><span class="sxs-lookup"><span data-stu-id="39902-185">File paths must be specified in the WSL format and care must be taken to escape relevant characters.</span></span> <span data-ttu-id="39902-186">例如：</span><span class="sxs-lookup"><span data-stu-id="39902-186">Example:</span></span>

```console
C:\temp> bash -c "ls -la /proc/cpuinfo"
```

<span data-ttu-id="39902-187">或...</span><span class="sxs-lookup"><span data-stu-id="39902-187">Or...</span></span>

```powershell
C:\temp> bash -c "ls -la \"/mnt/c/Program Files\""
```

<span data-ttu-id="39902-188">从早期的 Windows 10 版本中的 WSL 分发版调用 Windows 工具时，需要指定目录路径。</span><span class="sxs-lookup"><span data-stu-id="39902-188">When calling a Windows tool from a WSL distribution in an earlier version of Windows 10, you will need to specify the directory path.</span></span> <span data-ttu-id="39902-189">例如，在 WSL 命令行中，输入：</span><span class="sxs-lookup"><span data-stu-id="39902-189">For example, from your WSL command line, enter:</span></span>

```bash
/mnt/c/Windows/System32/notepad.exe
```

<span data-ttu-id="39902-190">在 WSL 中，这些可执行文件的处理方式类似于本机 Linux 可执行文件。</span><span class="sxs-lookup"><span data-stu-id="39902-190">In WSL, these executables are handled similar to native Linux executables.</span></span>  <span data-ttu-id="39902-191">这意味着，可按预期方式将目录添加到 Linux 路径，以及在命令之间进行管道处理。</span><span class="sxs-lookup"><span data-stu-id="39902-191">This means adding directories to the Linux path and piping between commands works as expected.</span></span>  <span data-ttu-id="39902-192">例如：</span><span class="sxs-lookup"><span data-stu-id="39902-192">For example:</span></span>

```bash
export PATH=$PATH:/mnt/c/Windows/System32
```
<span data-ttu-id="39902-193">或</span><span class="sxs-lookup"><span data-stu-id="39902-193">Or</span></span>

```bash
ipconfig.exe | grep IPv4 | cut -d: -f2
```

<span data-ttu-id="39902-194">Windows 二进制文件必须包含文件扩展名，匹配文件大小写，并且可执行。</span><span class="sxs-lookup"><span data-stu-id="39902-194">The Windows binary must include the file extension, match the file case, and be executable.</span></span>  <span data-ttu-id="39902-195">不可执行文件（包括批处理脚本）和 `dir` 等命令可与 `/mnt/c/Windows/System32/cmd.exe /C` 命令一起运行。</span><span class="sxs-lookup"><span data-stu-id="39902-195">Non-executables including batch scripts and command like `dir` can be run with `/mnt/c/Windows/System32/cmd.exe /C` command.</span></span> <span data-ttu-id="39902-196">例如：</span><span class="sxs-lookup"><span data-stu-id="39902-196">For example:</span></span>

```bash
/mnt/c/Windows/System32/cmd.exe /C dir
```

## <a name="additional-resources"></a><span data-ttu-id="39902-197">其他资源</span><span class="sxs-lookup"><span data-stu-id="39902-197">Additional resources</span></span>

* [<span data-ttu-id="39902-198">2016 年有关互操作性的 WSL 博客文章</span><span class="sxs-lookup"><span data-stu-id="39902-198">WSL blog post on interoperability from 2016</span></span>](https://blogs.msdn.microsoft.com/wsl/2016/10/19/windows-and-ubuntu-interoperability/)

---
title: "aaaInstall hello Azure CLI 1.0 |Microsoft 文件"
description: "安裝的 Mac、 Linux 及 Windows toostart 使用 Azure 服務的 hello Azure CLI 1.0"
editor: 
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: bdb776c8-7a76-4f3a-887c-236b4fffee10
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: rasquill
ms.openlocfilehash: a8cd4e38fde6e4b17a768a7caecd280cd91a70f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-cli-10"></a><span data-ttu-id="06007-103">安裝 hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="06007-103">Install hello Azure CLI 1.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="06007-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="06007-104">PowerShell</span></span>](/powershell/azure/overview)
> * [<span data-ttu-id="06007-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="06007-105">Azure CLI 1.0</span></span>](cli-install-nodejs.md)
> * [<span data-ttu-id="06007-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="06007-106">Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> <span data-ttu-id="06007-107">本主題描述如何 tooinstall hello Azure CLI 1.0，這建置在 nodeJs 並支援所有的傳統部署 API 呼叫以及大量的資源管理員部署活動。</span><span class="sxs-lookup"><span data-stu-id="06007-107">This topic describes how tooinstall hello Azure CLI 1.0, which is built on nodeJs and supports all classic deployment API calls as well as a large number of Resource Manager deployment activities.</span></span> <span data-ttu-id="06007-108">您應該使用 hello [Azure CLI 2.0](/cli/azure/overview)對於新的或預視 CLI 部署和管理。</span><span class="sxs-lookup"><span data-stu-id="06007-108">You should use hello [Azure CLI 2.0](/cli/azure/overview) for new or forward-looking CLI deployments and management.</span></span>

<span data-ttu-id="06007-109">快速安裝 hello Azure 命令列介面 (Azure CLI 1.0) toouse 一組的開放原始碼 shell 命令建立及管理 Microsoft Azure 中的資源。</span><span class="sxs-lookup"><span data-stu-id="06007-109">Quickly install hello Azure Command-Line Interface (Azure CLI 1.0) toouse a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span></span> <span data-ttu-id="06007-110">您有數個選項 tooinstall 這些跨平台工具在您的電腦上：</span><span class="sxs-lookup"><span data-stu-id="06007-110">You have several options tooinstall these cross-platform tools on your computer:</span></span>

* <span data-ttu-id="06007-111">**npm 封裝**-執行 npm （hello 適用於 JavaScript 的封裝管理員） tooinstall hello 最新 Azure CLI 1.0 封裝您的 Linux 發行版本或作業系統上。</span><span class="sxs-lookup"><span data-stu-id="06007-111">**npm package** - Run npm (hello package manager for JavaScript) tooinstall hello latest Azure CLI 1.0 package on your Linux distribution or OS.</span></span> <span data-ttu-id="06007-112">您的電腦上需要有 node.js 和 npm。</span><span class="sxs-lookup"><span data-stu-id="06007-112">Requires node.js and npm on your computer.</span></span>
* <span data-ttu-id="06007-113">**安裝程式** - 下載安裝程式以輕鬆在 Mac 或 Windows 上安裝。</span><span class="sxs-lookup"><span data-stu-id="06007-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span></span>
* <span data-ttu-id="06007-114">**Docker 容器**-開始使用 hello 已備妥執行 Docker 容器中的最新 CLI。</span><span class="sxs-lookup"><span data-stu-id="06007-114">**Docker container** - Start using hello latest CLI in a ready-to-run Docker container.</span></span> <span data-ttu-id="06007-115">您的電腦上需要有 Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="06007-115">Requires Docker host on your computer.</span></span>

<span data-ttu-id="06007-116">如需詳細的選項和背景，請參閱 hello 專案儲存機制上[GitHub](https://github.com/azure/azure-xplat-cli)。</span><span class="sxs-lookup"><span data-stu-id="06007-116">For more options and background, see hello project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span></span>

<span data-ttu-id="06007-117">Hello Azure CLI 1.0 安裝之後，[連接與您 Azure 訂用帳戶](xplat-cli-connect.md)和執行的 hello **azure**從命令列介面 （Bash、 終端機、 命令提示字元，等等） 的命令與 toowork您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="06007-117">Once hello Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run hello **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) toowork with your Azure resources.</span></span>

## <a name="option-1-install-an-npm-package"></a><span data-ttu-id="06007-118">選項 1：安裝 npm 套件</span><span class="sxs-lookup"><span data-stu-id="06007-118">Option 1: Install an npm package</span></span>
<span data-ttu-id="06007-119">tooinstall hello CLI 從 npm 套件，請確定您已下載並安裝 hello[最新版的 Node.js 及 npm](https://nodejs.org/en/download/package-manager/)。</span><span class="sxs-lookup"><span data-stu-id="06007-119">tooinstall hello CLI from an npm package, make sure you have downloaded and installed hello [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="06007-120">然後，執行**npm 安裝**tooinstall hello azure cli 封裝：</span><span class="sxs-lookup"><span data-stu-id="06007-120">Then, run **npm install** tooinstall hello azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="06007-121">在 Linux 發行版本，您可能需要 toouse **sudo** toosuccessfully 執行 hello **npm**命令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="06007-121">On Linux distributions, you might need toouse **sudo** toosuccessfully run hello **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="06007-122">如果您需要 tooinstall 或更新的 Node.js 及 npm Linux 發行版本或作業系統上的時，建議您安裝最新 Node.js LTS 版本 hello (4.x)。</span><span class="sxs-lookup"><span data-stu-id="06007-122">If you need tooinstall or update Node.js and npm on your Linux distribution or OS, we recommend that you install hello most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="06007-123">如果您使用較舊的版本，可能會發生安裝錯誤。</span><span class="sxs-lookup"><span data-stu-id="06007-123">If you use an older version, you might get installation errors.</span></span>

<span data-ttu-id="06007-124">如果您想要的話，下載 hello 最新的 Linux [tar 檔案][ linux-installer] hello npm 封裝在本機。</span><span class="sxs-lookup"><span data-stu-id="06007-124">If you prefer, download hello latest Linux [tar file][linux-installer] for hello npm package locally.</span></span> <span data-ttu-id="06007-125">然後，如下所示安裝 hello 下載的 npm 封裝 (在 Linux 發行版本中，您可能需要 toouse **sudo**):</span><span class="sxs-lookup"><span data-stu-id="06007-125">Then, install hello downloaded npm package as follows (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a><span data-ttu-id="06007-126">選項 2：使用安裝程式</span><span class="sxs-lookup"><span data-stu-id="06007-126">Option 2: Use an installer</span></span>
<span data-ttu-id="06007-127">如果您使用 Mac 或 Windows 的電腦，就有一個 hello 遵循 CLI 安裝程式可供下載：</span><span class="sxs-lookup"><span data-stu-id="06007-127">If you use a Mac or Windows computer, hello following CLI installers are available for download:</span></span>

* <span data-ttu-id="06007-128">[Mac OS X 安裝程式][mac-installer]</span><span class="sxs-lookup"><span data-stu-id="06007-128">[Mac OS X installer][mac-installer]</span></span>
* <span data-ttu-id="06007-129">[Windows MSI][windows-installer]</span><span class="sxs-lookup"><span data-stu-id="06007-129">[Windows MSI][windows-installer]</span></span>

> [!TIP]
> <span data-ttu-id="06007-130">在 Windows 中，您也可以下載 hello [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI。</span><span class="sxs-lookup"><span data-stu-id="06007-130">On Windows, you can also download hello [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI.</span></span> <span data-ttu-id="06007-131">Hello 選項 tooinstall 此安裝程式可讓其他 Azure SDK 和命令列工具，在安裝之後 hello CLI。</span><span class="sxs-lookup"><span data-stu-id="06007-131">This installer gives you hello option tooinstall additional Azure SDK and command-line tools after installing hello CLI.</span></span>

## <a name="option-3-use-a-docker-container"></a><span data-ttu-id="06007-132">選項 3：使用 Docker 容器</span><span class="sxs-lookup"><span data-stu-id="06007-132">Option 3: Use a Docker container</span></span>
<span data-ttu-id="06007-133">如果您已經設定您的電腦[Docker](https://docs.docker.com/engine/understanding-docker/)主機，您可以執行 hello Docker 容器中的最新 Azure CLI 1.0。</span><span class="sxs-lookup"><span data-stu-id="06007-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run hello latest Azure CLI 1.0 in a Docker container.</span></span> <span data-ttu-id="06007-134">執行 hello 下列命令 (在 Linux 發行版本中，您可能需要 toouse **sudo**):</span><span class="sxs-lookup"><span data-stu-id="06007-134">Run hello following command (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a><span data-ttu-id="06007-135">執行 Azure CLI 1.0 命令</span><span class="sxs-lookup"><span data-stu-id="06007-135">Run Azure CLI 1.0 commands</span></span>
<span data-ttu-id="06007-136">Hello Azure CLI 1.0 安裝之後，執行 hello **azure**命令從命令列的使用者介面 （Bash、 終端機、 命令提示字元，等等）。</span><span class="sxs-lookup"><span data-stu-id="06007-136">After hello Azure CLI 1.0 is installed, run hello **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span></span> <span data-ttu-id="06007-137">例如，toorun hello [說明] 命令，請 hello 下列輸入：</span><span class="sxs-lookup"><span data-stu-id="06007-137">For example, toorun hello help command, type hello following:</span></span>

```azurecli
azure help
```

> [!NOTE]
> <span data-ttu-id="06007-138">在某些 Linux 發行版本中，您可能會收到類似的錯誤太`/usr/bin/env: ‘node’: No such file or directory`。</span><span class="sxs-lookup"><span data-stu-id="06007-138">On some Linux distributions, you may receive an error similar too`/usr/bin/env: ‘node’: No such file or directory`.</span></span> <span data-ttu-id="06007-139">此錯誤訊息是來自最近安裝在 /usr/bin/nodejs 的 Node.js。</span><span class="sxs-lookup"><span data-stu-id="06007-139">This error comes from recent installations of Node.js being installed at /usr/bin/nodejs.</span></span> <span data-ttu-id="06007-140">toofix，建立符號連結太/usr/bin/節點執行此命令：</span><span class="sxs-lookup"><span data-stu-id="06007-140">toofix it, create a symbolic link too/usr/bin/node by running this command:</span></span>

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<span data-ttu-id="06007-141">toosee hello 版的 hello Azure CLI 1.0 安裝時，下列類型 hello:</span><span class="sxs-lookup"><span data-stu-id="06007-141">toosee hello version of hello Azure CLI 1.0 you installed, type hello following:</span></span>

```azurecli
azure --version
```

<span data-ttu-id="06007-142">您現在已經準備就緒！</span><span class="sxs-lookup"><span data-stu-id="06007-142">Now you are ready!</span></span> <span data-ttu-id="06007-143">所有 tooaccess 都 hello 與您自己的資源，CLI 命令 toowork [tooyour Azure 訂用帳戶連線從都 hello Azure CLI](xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="06007-143">tooaccess all hello CLI commands toowork with your own resources, [connect tooyour Azure subscription from hello Azure CLI](xplat-cli-connect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="06007-144">當您第一次使用 Azure CLI 時，您會看到訊息詢問您是否要 tooallow Microsoft toocollect 使用量資訊。</span><span class="sxs-lookup"><span data-stu-id="06007-144">When you first use Azure CLI, you see a message asking if you want tooallow Microsoft toocollect usage information.</span></span> <span data-ttu-id="06007-145">參與為自願性質。</span><span class="sxs-lookup"><span data-stu-id="06007-145">Participation is voluntary.</span></span> <span data-ttu-id="06007-146">如果您選擇 tooparticipate，您可以隨時執行停止`azure telemetry --disable`。</span><span class="sxs-lookup"><span data-stu-id="06007-146">If you choose tooparticipate, you can stop at any time by running `azure telemetry --disable`.</span></span> <span data-ttu-id="06007-147">在任何時候，tooenable 參與執行`azure telemetry --enable`。</span><span class="sxs-lookup"><span data-stu-id="06007-147">tooenable participation at any time, run `azure telemetry --enable`.</span></span>

## <a name="update-hello-cli"></a><span data-ttu-id="06007-148">更新 hello CLI</span><span class="sxs-lookup"><span data-stu-id="06007-148">Update hello CLI</span></span>
<span data-ttu-id="06007-149">Microsoft 經常發行更新的版本的 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="06007-149">Microsoft frequently releases updated versions of hello Azure CLI.</span></span> <span data-ttu-id="06007-150">重新安裝 hello CLI hello 安裝程式使用適用於您的作業系統，或執行 hello 最新的 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="06007-150">Reinstall hello CLI using hello installer for your operating system, or run hello latest Docker container.</span></span> <span data-ttu-id="06007-151">或者，如果您擁有 hello 最新版的 Node.js 及 npm 安裝，藉由輸入 hello 下列更新 (在 Linux 發行版本中，您可能需要 toouse **sudo**)。</span><span class="sxs-lookup"><span data-stu-id="06007-151">Or, if you have hello latest Node.js and npm installed, update by typing hello following (on Linux distributions you might need toouse **sudo**).</span></span>

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a><span data-ttu-id="06007-152">啟用 TAB 鍵自動完成</span><span class="sxs-lookup"><span data-stu-id="06007-152">Enable tab completion</span></span>
<span data-ttu-id="06007-153">針對 Mac 和 Linux 提供 CLI 命令 TAB 鍵自動完成支援。</span><span class="sxs-lookup"><span data-stu-id="06007-153">Tab completion of CLI commands is supported for Mac and Linux.</span></span>

<span data-ttu-id="06007-154">tooenable zsh，在執行：</span><span class="sxs-lookup"><span data-stu-id="06007-154">tooenable it in zsh, run:</span></span>

```bash
echo '. <(azure --completion)' >> .zshrc
```

<span data-ttu-id="06007-155">tooenable bash，在執行：</span><span class="sxs-lookup"><span data-stu-id="06007-155">tooenable it in bash, run:</span></span>

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a><span data-ttu-id="06007-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="06007-156">Next steps</span></span>
* <span data-ttu-id="06007-157">[從 hello CLI tooyour Azure 訂用帳戶連線](xplat-cli-connect.md)toocreate 及管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="06007-157">[Connect from hello CLI tooyour Azure subscription](xplat-cli-connect.md) toocreate and manage Azure resources.</span></span>
* <span data-ttu-id="06007-158">深入了解 hello Azure CLI toolearn 下載原始程式碼、 報告的問題，或參與 toohello 專案，請瀏覽 hello [hello Azure CLI 的 GitHub 儲存機制](https://github.com/azure/azure-xplat-cli)。</span><span class="sxs-lookup"><span data-stu-id="06007-158">toolearn more about hello Azure CLI, download source code, report problems, or contribute toohello project, visit hello [GitHub repository for hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="06007-159">如果您有使用 Azure CLI hello 或 Azure 的相關問題，請瀏覽 hello [Azure 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting)。</span><span class="sxs-lookup"><span data-stu-id="06007-159">If you have questions about using hello Azure CLI, or Azure, visit hello [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md

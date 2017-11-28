---
title: "安裝 Azure CLI 1.0 | Microsoft Docs"
description: "安裝適用於 Mac、Linux 和 Windows 的 Azure CLI 1.0，以開始使用 Azure 服務"
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
ms.openlocfilehash: 63b35ed25b809a16b61b685fd35aa67474b0a369
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="install-the-azure-cli-10"></a><span data-ttu-id="af178-103">安裝 Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="af178-103">Install the Azure CLI 1.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="af178-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="af178-104">PowerShell</span></span>](/powershell/azure/overview)
> * [<span data-ttu-id="af178-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="af178-105">Azure CLI 1.0</span></span>](cli-install-nodejs.md)
> * [<span data-ttu-id="af178-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="af178-106">Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> <span data-ttu-id="af178-107">本主題說明如何安裝 Azure CLI 1.0，它是以 NodeJS 為基礎而建置，並支援所有傳統部署 API 呼叫，以及大量的 Resource Manager 部署活動。</span><span class="sxs-lookup"><span data-stu-id="af178-107">This topic describes how to install the Azure CLI 1.0, which is built on nodeJs and supports all classic deployment API calls as well as a large number of Resource Manager deployment activities.</span></span> <span data-ttu-id="af178-108">針對新的或前瞻性的 CLI 部署及管理，您應該使用 [Azure CLI 2.0](/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="af178-108">You should use the [Azure CLI 2.0](/cli/azure/overview) for new or forward-looking CLI deployments and management.</span></span>

<span data-ttu-id="af178-109">快速安裝 Azure 命令列介面 (Azure CLI 1.0) 來使用一組開放原始碼的殼層命令，用於建立和管理 Microsoft Azure 中的資源。</span><span class="sxs-lookup"><span data-stu-id="af178-109">Quickly install the Azure Command-Line Interface (Azure CLI 1.0) to use a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span></span> <span data-ttu-id="af178-110">有數個選項可讓您在電腦上安裝這些跨平台工具︰</span><span class="sxs-lookup"><span data-stu-id="af178-110">You have several options to install these cross-platform tools on your computer:</span></span>

* <span data-ttu-id="af178-111">**npm 套件** - 執行 npm (適用於 JavaScript 的套件管理員) 來將最新的 Azure CLI 1.0 套件安裝在您的 Linux 散發套件或作業系統上。</span><span class="sxs-lookup"><span data-stu-id="af178-111">**npm package** - Run npm (the package manager for JavaScript) to install the latest Azure CLI 1.0 package on your Linux distribution or OS.</span></span> <span data-ttu-id="af178-112">您的電腦上需要有 node.js 和 npm。</span><span class="sxs-lookup"><span data-stu-id="af178-112">Requires node.js and npm on your computer.</span></span>
* <span data-ttu-id="af178-113">**安裝程式** - 下載安裝程式以輕鬆在 Mac 或 Windows 上安裝。</span><span class="sxs-lookup"><span data-stu-id="af178-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span></span>
* <span data-ttu-id="af178-114">**Docker 容器** - 在已就緒可執行的 Docker 容器中開始使用最新的 CLI。</span><span class="sxs-lookup"><span data-stu-id="af178-114">**Docker container** - Start using the latest CLI in a ready-to-run Docker container.</span></span> <span data-ttu-id="af178-115">您的電腦上需要有 Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="af178-115">Requires Docker host on your computer.</span></span>

<span data-ttu-id="af178-116">如需詳細的選項和背景，請參閱 [GitHub](https://github.com/azure/azure-xplat-cli)上的專案儲存機制。</span><span class="sxs-lookup"><span data-stu-id="af178-116">For more options and background, see the project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span></span>

<span data-ttu-id="af178-117">安裝好 Azure CLI 1.0 之後，[使用 Azure 訂用帳戶將其連接](xplat-cli-connect.md)，並從命令列介面 (Bash、終端機及命令提示字元等) 中執行 **azure** 命令以使用 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="af178-117">Once the Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run the **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) to work with your Azure resources.</span></span>

## <a name="option-1-install-an-npm-package"></a><span data-ttu-id="af178-118">選項 1：安裝 npm 套件</span><span class="sxs-lookup"><span data-stu-id="af178-118">Option 1: Install an npm package</span></span>
<span data-ttu-id="af178-119">若要從 npm 套件安裝 CLI，請確定已下載並安裝[最新的 Node.js 和 npm](https://nodejs.org/en/download/package-manager/)。</span><span class="sxs-lookup"><span data-stu-id="af178-119">To install the CLI from an npm package, make sure you have downloaded and installed the [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="af178-120">然後，執行 **npm 安裝**，以安裝 azure-cli 套件：</span><span class="sxs-lookup"><span data-stu-id="af178-120">Then, run **npm install** to install the azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="af178-121">在 Linux 散發套件上，您可能需要使用 **sudo**，才能順利執行 **npm** 命令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="af178-121">On Linux distributions, you might need to use **sudo** to successfully run the **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="af178-122">如果您需要在 Linux 散發套件或作業系統上安裝或更新 Node.js 和 npm，建議您安裝最新的 Node.js LTS 版本 (4.x)。</span><span class="sxs-lookup"><span data-stu-id="af178-122">If you need to install or update Node.js and npm on your Linux distribution or OS, we recommend that you install the most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="af178-123">如果您使用較舊的版本，可能會發生安裝錯誤。</span><span class="sxs-lookup"><span data-stu-id="af178-123">If you use an older version, you might get installation errors.</span></span>

<span data-ttu-id="af178-124">如果您喜歡，請將 npm 套件的最新 Linux [tar 檔案][linux-installer]下載到本機。</span><span class="sxs-lookup"><span data-stu-id="af178-124">If you prefer, download the latest Linux [tar file][linux-installer] for the npm package locally.</span></span> <span data-ttu-id="af178-125">然後，安裝下載的 npm 套件，如下所示 (在 Linux 散發套件上，您可能需要使用 **sudo**)：</span><span class="sxs-lookup"><span data-stu-id="af178-125">Then, install the downloaded npm package as follows (on Linux distributions you might need to use **sudo**):</span></span>

```bash
npm install -g <path to downloaded tar file>
```

## <a name="option-2-use-an-installer"></a><span data-ttu-id="af178-126">選項 2：使用安裝程式</span><span class="sxs-lookup"><span data-stu-id="af178-126">Option 2: Use an installer</span></span>
<span data-ttu-id="af178-127">如果您使用 Mac 或 Windows 電腦，則有下列 CLI 安裝程式可供下載︰</span><span class="sxs-lookup"><span data-stu-id="af178-127">If you use a Mac or Windows computer, the following CLI installers are available for download:</span></span>

* <span data-ttu-id="af178-128">[Mac OS X 安裝程式][mac-installer]</span><span class="sxs-lookup"><span data-stu-id="af178-128">[Mac OS X installer][mac-installer]</span></span>
* <span data-ttu-id="af178-129">[Windows MSI][windows-installer]</span><span class="sxs-lookup"><span data-stu-id="af178-129">[Windows MSI][windows-installer]</span></span>

> [!TIP]
> <span data-ttu-id="af178-130">在 Windows 中，您也可以下載 [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) 來安裝 CLI。</span><span class="sxs-lookup"><span data-stu-id="af178-130">On Windows, you can also download the [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) to install the CLI.</span></span> <span data-ttu-id="af178-131">這個安裝程式可讓您在安裝 CLI 之後，再選擇安裝額外的 Azure SDK 和命令列工具。</span><span class="sxs-lookup"><span data-stu-id="af178-131">This installer gives you the option to install additional Azure SDK and command-line tools after installing the CLI.</span></span>

## <a name="option-3-use-a-docker-container"></a><span data-ttu-id="af178-132">選項 3：使用 Docker 容器</span><span class="sxs-lookup"><span data-stu-id="af178-132">Option 3: Use a Docker container</span></span>
<span data-ttu-id="af178-133">如果您已將電腦設定為 [Docker (英文)](https://docs.docker.com/engine/understanding-docker/) 主機，您可以在 Docker 容器中執行最新的 Azure CLI 1.0。</span><span class="sxs-lookup"><span data-stu-id="af178-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run the latest Azure CLI 1.0 in a Docker container.</span></span> <span data-ttu-id="af178-134">執行下列命令 (在 Linux 散發套件上，您可能需要使用 **sudo**)：</span><span class="sxs-lookup"><span data-stu-id="af178-134">Run the following command (on Linux distributions you might need to use **sudo**):</span></span>

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a><span data-ttu-id="af178-135">執行 Azure CLI 1.0 命令</span><span class="sxs-lookup"><span data-stu-id="af178-135">Run Azure CLI 1.0 commands</span></span>
<span data-ttu-id="af178-136">安裝好 Azure CLI 1.0 之後，從命令列使用者介面 (Bash、終端機及命令提示字元等) 中執行 **azure** 命令。</span><span class="sxs-lookup"><span data-stu-id="af178-136">After the Azure CLI 1.0 is installed, run the **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span></span> <span data-ttu-id="af178-137">例如，若要執行 [說明] 命令，請輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="af178-137">For example, to run the help command, type the following:</span></span>

```azurecli
azure help
```

> [!NOTE]
> <span data-ttu-id="af178-138">在某些 Linux 散發套件上，您可能會收到類似 `/usr/bin/env: ‘node’: No such file or directory` 的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="af178-138">On some Linux distributions, you may receive an error similar to `/usr/bin/env: ‘node’: No such file or directory`.</span></span> <span data-ttu-id="af178-139">此錯誤訊息是來自最近安裝在 /usr/bin/nodejs 的 Node.js。</span><span class="sxs-lookup"><span data-stu-id="af178-139">This error comes from recent installations of Node.js being installed at /usr/bin/nodejs.</span></span> <span data-ttu-id="af178-140">若要修正此錯誤，請執行此命令來建立 /usr/bin/node 的符號連結︰</span><span class="sxs-lookup"><span data-stu-id="af178-140">To fix it, create a symbolic link to /usr/bin/node by running this command:</span></span>

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<span data-ttu-id="af178-141">若要查看您所安裝的 Azure CLI 1.0 版本，請輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="af178-141">To see the version of the Azure CLI 1.0 you installed, type the following:</span></span>

```azurecli
azure --version
```

<span data-ttu-id="af178-142">您現在已經準備就緒！</span><span class="sxs-lookup"><span data-stu-id="af178-142">Now you are ready!</span></span> <span data-ttu-id="af178-143">若要存取所有 CLI 命令以與您自己的資源搭配使用，請 [從 Azure CLI 連接到您的 Azure 訂用帳戶](xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="af178-143">To access all the CLI commands to work with your own resources, [connect to your Azure subscription from the Azure CLI](xplat-cli-connect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="af178-144">當您第一次使用 Azure CLI 時會看到一則訊息，詢問您是否要允許 Microsoft 收集使用情況資訊。</span><span class="sxs-lookup"><span data-stu-id="af178-144">When you first use Azure CLI, you see a message asking if you want to allow Microsoft to collect usage information.</span></span> <span data-ttu-id="af178-145">參與為自願性質。</span><span class="sxs-lookup"><span data-stu-id="af178-145">Participation is voluntary.</span></span> <span data-ttu-id="af178-146">如果您選擇參與，只要執行 `azure telemetry --disable`即可隨時停止參與。</span><span class="sxs-lookup"><span data-stu-id="af178-146">If you choose to participate, you can stop at any time by running `azure telemetry --disable`.</span></span> <span data-ttu-id="af178-147">只要執行 `azure telemetry --enable`即可隨時啟用參與。</span><span class="sxs-lookup"><span data-stu-id="af178-147">To enable participation at any time, run `azure telemetry --enable`.</span></span>

## <a name="update-the-cli"></a><span data-ttu-id="af178-148">更新 CLI</span><span class="sxs-lookup"><span data-stu-id="af178-148">Update the CLI</span></span>
<span data-ttu-id="af178-149">Microsoft 經常發行 Azure CLI 的更新版本。</span><span class="sxs-lookup"><span data-stu-id="af178-149">Microsoft frequently releases updated versions of the Azure CLI.</span></span> <span data-ttu-id="af178-150">請使用適用於您作業系統的安裝程式來重新安裝 CLI，或執行最新的 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="af178-150">Reinstall the CLI using the installer for your operating system, or run the latest Docker container.</span></span> <span data-ttu-id="af178-151">或者，如果您已安裝最新的 Node.js 和 npm，請輸入下列命令來進行更新 (在 Linux 散發套件上，您可能需要使用 **sudo**)。</span><span class="sxs-lookup"><span data-stu-id="af178-151">Or, if you have the latest Node.js and npm installed, update by typing the following (on Linux distributions you might need to use **sudo**).</span></span>

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a><span data-ttu-id="af178-152">啟用 TAB 鍵自動完成</span><span class="sxs-lookup"><span data-stu-id="af178-152">Enable tab completion</span></span>
<span data-ttu-id="af178-153">針對 Mac 和 Linux 提供 CLI 命令 TAB 鍵自動完成支援。</span><span class="sxs-lookup"><span data-stu-id="af178-153">Tab completion of CLI commands is supported for Mac and Linux.</span></span>

<span data-ttu-id="af178-154">若要在 zsh 中啟用它，請執行︰</span><span class="sxs-lookup"><span data-stu-id="af178-154">To enable it in zsh, run:</span></span>

```bash
echo '. <(azure --completion)' >> .zshrc
```

<span data-ttu-id="af178-155">若要在 bash 中啟用它，請執行︰</span><span class="sxs-lookup"><span data-stu-id="af178-155">To enable it in bash, run:</span></span>

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a><span data-ttu-id="af178-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="af178-156">Next steps</span></span>
* <span data-ttu-id="af178-157">[從 CLI 連接到您的 Azure 訂用帳戶](xplat-cli-connect.md) 來建立和管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="af178-157">[Connect from the CLI to your Azure subscription](xplat-cli-connect.md) to create and manage Azure resources.</span></span>
* <span data-ttu-id="af178-158">若要深入了解 Azure CLI、下載來源程式碼、回報問題，或是參與專案，請造訪 [Azure CLI 的 GitHub 儲存機制](https://github.com/azure/azure-xplat-cli)。</span><span class="sxs-lookup"><span data-stu-id="af178-158">To learn more about the Azure CLI, download source code, report problems, or contribute to the project, visit the [GitHub repository for the Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="af178-159">如果您有關於使用 Azure CLI 或 Azure 方面的問題，請造訪 [Azure 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting)。</span><span class="sxs-lookup"><span data-stu-id="af178-159">If you have questions about using the Azure CLI, or Azure, visit the [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md

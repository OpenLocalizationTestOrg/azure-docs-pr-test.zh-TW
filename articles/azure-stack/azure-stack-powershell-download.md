---
title: "從 GitHub 工具 aaaDownload Azure 堆疊 |Microsoft 文件"
description: "了解需要 Azure 堆疊 toowork 如何 toodownload 工具。"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: a88c97b0ef1dd70e63771f0607cc07ec7a00b533
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="download-azure-stack-tools-from-github"></a><span data-ttu-id="ac1f5-103">從 GitHub 下載 Azure Stack 工具</span><span class="sxs-lookup"><span data-stu-id="ac1f5-103">Download Azure Stack tools from GitHub</span></span>

<span data-ttu-id="ac1f5-104">AzureStack 工具是主控的 PowerShell 模組，您可以使用 toomanage 及部署資源 tooAzure 堆疊的 GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="ac1f5-104">AzureStack-Tools is a GitHub repository that hosts PowerShell modules that you can use toomanage and deploy resources tooAzure Stack.</span></span> <span data-ttu-id="ac1f5-105">您可以下載並使用這些 PowerShell 模組 toohello Azure 堆疊開發套件或 tooa windows 外部用戶端，如果您計劃 tooestablish VPN 連線能力。</span><span class="sxs-lookup"><span data-stu-id="ac1f5-105">You can download and use these PowerShell modules toohello Azure Stack Development Kit, or tooa windows-based external client if you are planning tooestablish VPN connectivity.</span></span> <span data-ttu-id="ac1f5-106">這些工具，tooobtain 複製 hello GitHub 儲存機制或下載 hello AzureStack 工具資料夾。</span><span class="sxs-lookup"><span data-stu-id="ac1f5-106">tooobtain these tools, clone hello GitHub repository or download hello AzureStack-Tools folder.</span></span> 

<span data-ttu-id="ac1f5-107">tooclone hello 儲存機制上，下載[Git](https://git-scm.com/download/win)適用於 Windows、 開啟 命令提示字元視窗並執行下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="ac1f5-107">tooclone hello repository, download [Git](https://git-scm.com/download/win) for Windows, open a Command Prompt window and run hello following script:</span></span>

```PowerShell
# Change directory toohello root directory 
cd \

# clone hello repository
git clone https://github.com/Azure/AzureStack-Tools.git --recursive

# Change toohello tools directory
cd AzureStack-Tools
```

<span data-ttu-id="ac1f5-108">toodownload hello 工具資料夾中，執行下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="ac1f5-108">toodownload hello tools folder, run hello following script:</span></span>

```PowerShell
# Change directory toohello root directory 
cd \

# Download hello tools archive
invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

# Expand hello downloaded files
expand-archive master.zip `
  -DestinationPath . `
  -Force

# Change toohello tools directory
cd AzureStack-Tools-master

```

## <a name="functionalities-provided-by-hello-modules"></a><span data-ttu-id="ac1f5-109">Hello 模組所提供的功能</span><span class="sxs-lookup"><span data-stu-id="ac1f5-109">Functionalities provided by hello modules</span></span>

<span data-ttu-id="ac1f5-110">hello AzureStack 工具儲存機制包含 PowerShell 模組，支援下列功能的 Azure 堆疊 hello:</span><span class="sxs-lookup"><span data-stu-id="ac1f5-110">hello AzureStack-Tools repository contains PowerShell modules that support hello following functionalities for Azure Stack:</span></span>  

| <span data-ttu-id="ac1f5-111">功能</span><span class="sxs-lookup"><span data-stu-id="ac1f5-111">Functionality</span></span> | <span data-ttu-id="ac1f5-112">說明</span><span class="sxs-lookup"><span data-stu-id="ac1f5-112">Description</span></span> | <span data-ttu-id="ac1f5-113">可以使用此模組的人員？</span><span class="sxs-lookup"><span data-stu-id="ac1f5-113">who can use this module?</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="ac1f5-114">雲端功能</span><span class="sxs-lookup"><span data-stu-id="ac1f5-114">Cloud capabilities</span></span>](azure-stack-validate-templates.md) | <span data-ttu-id="ac1f5-115">使用此模組 tooget hello 雲端功能的雲端。</span><span class="sxs-lookup"><span data-stu-id="ac1f5-115">Use this module tooget hello cloud capabilities of a cloud.</span></span> <span data-ttu-id="ac1f5-116">例如，您可以取得 hello 雲端功能，例如應用程式開發介面版本、 Azure 資源管理員資源、 VM 擴充功能等 Azure 堆疊] 和 [使用此模組的 Azure 雲端。</span><span class="sxs-lookup"><span data-stu-id="ac1f5-116">For example, you can get hello cloud capabilities such as API version, Azure Resource Manager resources, VM extensions etc. for Azure Stack and Azure clouds using this module.</span></span> | <span data-ttu-id="ac1f5-117">雲端系統管理員和使用者。</span><span class="sxs-lookup"><span data-stu-id="ac1f5-117">Cloud administrators and users.</span></span> |
| [<span data-ttu-id="ac1f5-118">Azure Stack 計算系統管理</span><span class="sxs-lookup"><span data-stu-id="ac1f5-118">Azure Stack compute administration</span></span>](azure-stack-add-vm-image.md) | <span data-ttu-id="ac1f5-119">使用此模組 tooadd 或商場 hello Azure 堆疊移除的 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="ac1f5-119">Use this module tooadd or remove a VM image from hello Azure Stack marketplace.</span></span> | <span data-ttu-id="ac1f5-120">雲端系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ac1f5-120">Cloud administrators.</span></span> |
| [<span data-ttu-id="ac1f5-121">Azure Stack 基礎結構系統管理</span><span class="sxs-lookup"><span data-stu-id="ac1f5-121">Azure Stack Infrastructure administration</span></span>](https://github.com/Azure/AzureStack-Tools/blob/master/Infrastructure/README.md) | <span data-ttu-id="ac1f5-122">使用此模組 toomanage 堆疊 Azure 基礎結構的 Vm、 警示、 更新等。</span><span class="sxs-lookup"><span data-stu-id="ac1f5-122">Use this module toomanage Azure Stack infrastructure VMs, alerts, updates etc.</span></span> |  <span data-ttu-id="ac1f5-123">雲端系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ac1f5-123">Cloud administrators.</span></span>|
| [<span data-ttu-id="ac1f5-124">適用於 Azure Stack 的 Resource Manager 原則</span><span class="sxs-lookup"><span data-stu-id="ac1f5-124">Resource Manager policy for Azure Stack</span></span>](azure-stack-policy-module.md) | <span data-ttu-id="ac1f5-125">使用此模組 tooconfigure Azure 訂用帳戶或 Azure 資源群組以 hello 相同 Azure 堆疊的版本控制和服務可用性。</span><span class="sxs-lookup"><span data-stu-id="ac1f5-125">Use this module tooconfigure an Azure subscription or an Azure resource group with hello same versioning and service availability as Azure Stack.</span></span> | <span data-ttu-id="ac1f5-126">雲端系統管理員和使用者</span><span class="sxs-lookup"><span data-stu-id="ac1f5-126">Cloud administrators and users</span></span> |
| [<span data-ttu-id="ac1f5-127">註冊 Azure</span><span class="sxs-lookup"><span data-stu-id="ac1f5-127">Register with Azure</span></span>](azure-stack-register.md) | <span data-ttu-id="ac1f5-128">搭配 Azure 使用此模組 tooregister 開發的組件執行個體。</span><span class="sxs-lookup"><span data-stu-id="ac1f5-128">Use this module tooregister your development kit instance with Azure.</span></span> <span data-ttu-id="ac1f5-129">在註冊之後，您可以下載從 Azure 的 hello marketplace 項目，並在 Azure 堆疊中使用它們。</span><span class="sxs-lookup"><span data-stu-id="ac1f5-129">After registering, you can download hello marketplace items from Azure and use them in Azure Stack.</span></span> | <span data-ttu-id="ac1f5-130">雲端系統管理員</span><span class="sxs-lookup"><span data-stu-id="ac1f5-130">Cloud administrators</span></span> |
| [<span data-ttu-id="ac1f5-131">Azure Stack 部署</span><span class="sxs-lookup"><span data-stu-id="ac1f5-131">Azure Stack deployment</span></span>](azure-stack-run-powershell-script.md) | <span data-ttu-id="ac1f5-132">使用此模組 tooprepare hello Azure 堆疊主機電腦 toodeploy，並使用 hello Azure 堆疊的虛擬硬碟 Disk(VHD) 映像重新部署。</span><span class="sxs-lookup"><span data-stu-id="ac1f5-132">Use this module tooprepare hello Azure Stack host computer toodeploy and redeploy by using hello Azure Stack Virtual Hard Disk(VHD) image.</span></span> | <span data-ttu-id="ac1f5-133">雲端系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ac1f5-133">Cloud administrators.</span></span> |
| [<span data-ttu-id="ac1f5-134">連接 tooAzure 堆疊</span><span class="sxs-lookup"><span data-stu-id="ac1f5-134">Connecting tooAzure Stack</span></span>](azure-stack-connect-powershell.md) | <span data-ttu-id="ac1f5-135">使用此模組 tooconnect tooan Azure 堆疊執行個體透過 PowerShell 和 tooconfigure VPN 連線能力 tooAzure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="ac1f5-135">Use this module tooconnect tooan Azure Stack instance through PowerShell and tooconfigure VPN connectivity tooAzure Stack.</span></span> | <span data-ttu-id="ac1f5-136">雲端系統管理員和使用者</span><span class="sxs-lookup"><span data-stu-id="ac1f5-136">Cloud administrators and users</span></span> |
| [<span data-ttu-id="ac1f5-137">Azure Stack 服務系統管理</span><span class="sxs-lookup"><span data-stu-id="ac1f5-137">Azure Stack service administration</span></span>](azure-stack-create-offer.md) | <span data-ttu-id="ac1f5-138">Azure 堆疊系統管理員可以使用跨計算、 儲存體、 網路和金鑰保存庫服務預設租用戶提供本模組 toocreate 無限制的配額。</span><span class="sxs-lookup"><span data-stu-id="ac1f5-138">Azure Stack administrators can use this module toocreate a default tenant offer with unlimited quota across Compute, Storage, Network, and Key Vault services.</span></span>   | <span data-ttu-id="ac1f5-139">雲端系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ac1f5-139">Cloud administrators.</span></span>|
| [<span data-ttu-id="ac1f5-140">範本驗證程式</span><span class="sxs-lookup"><span data-stu-id="ac1f5-140">Template validator</span></span>](azure-stack-validate-templates.md) | <span data-ttu-id="ac1f5-141">如果現有或新的範本可以部署的 tooAzure 堆疊，請使用此模組 tooverify。</span><span class="sxs-lookup"><span data-stu-id="ac1f5-141">Use this module tooverify if an existing or a new template can be deployed tooAzure Stack.</span></span> | <span data-ttu-id="ac1f5-142">雲端系統管理員和使用者</span><span class="sxs-lookup"><span data-stu-id="ac1f5-142">Cloud administrators and users</span></span> |


## <a name="next-steps"></a><span data-ttu-id="ac1f5-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ac1f5-143">Next steps</span></span>
* [<span data-ttu-id="ac1f5-144">設定 hello Azure 堆疊使用者的 PowerShell 環境</span><span class="sxs-lookup"><span data-stu-id="ac1f5-144">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)   
* [<span data-ttu-id="ac1f5-145">透過 VPN 連接 tooAzure 堆疊開發套件</span><span class="sxs-lookup"><span data-stu-id="ac1f5-145">Connect tooAzure Stack Development Kit over a VPN</span></span>](azure-stack-connect-azure-stack.md)  

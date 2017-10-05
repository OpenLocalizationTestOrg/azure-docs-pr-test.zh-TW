---
title: "從 GitHub 下載 Azure Stack 工具 | Microsoft Docs"
description: "瞭解如何下載必要的工具來處理 Azure Stack。"
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
ms.openlocfilehash: 589d2ea1ffed9f8ac82793132d9c91efcc60a5fe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="download-azure-stack-tools-from-github"></a><span data-ttu-id="07971-103">從 GitHub 下載 Azure Stack 工具</span><span class="sxs-lookup"><span data-stu-id="07971-103">Download Azure Stack tools from GitHub</span></span>

<span data-ttu-id="07971-104">AzureStack-Tools 是裝載 PowerShell 模組的 GitHub 存放庫，可用來管理和部署至 Azure Stack 的資源。</span><span class="sxs-lookup"><span data-stu-id="07971-104">AzureStack-Tools is a GitHub repository that hosts PowerShell modules that you can use to manage and deploy resources to Azure Stack.</span></span> <span data-ttu-id="07971-105">您可以針對 Azure Stack 開發套件，或針對以 Windows 為基礎的外部用戶端 (如果您打算建立 VPN 連線能力) 下載並使用這些 PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="07971-105">You can download and use these PowerShell modules to the Azure Stack Development Kit, or to a windows-based external client if you are planning to establish VPN connectivity.</span></span> <span data-ttu-id="07971-106">若要取得這些工具，請複製 GitHub 存放庫或下載 AzureStack-Tools 資料夾。</span><span class="sxs-lookup"><span data-stu-id="07971-106">To obtain these tools, clone the GitHub repository or download the AzureStack-Tools folder.</span></span> 

<span data-ttu-id="07971-107">若要複製存放庫，請下載 [Git](https://git-scm.com/download/win) for Windows，開啟命令提示字元視窗，然後執行下列指令碼：</span><span class="sxs-lookup"><span data-stu-id="07971-107">To clone the repository, download [Git](https://git-scm.com/download/win) for Windows, open a Command Prompt window and run the following script:</span></span>

```PowerShell
# Change directory to the root directory 
cd \

# clone the repository
git clone https://github.com/Azure/AzureStack-Tools.git --recursive

# Change to the tools directory
cd AzureStack-Tools
```

<span data-ttu-id="07971-108">若要下載工具資料夾，請執行下列指令碼：</span><span class="sxs-lookup"><span data-stu-id="07971-108">To download the tools folder, run the following script:</span></span>

```PowerShell
# Change directory to the root directory 
cd \

# Download the tools archive
invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

# Expand the downloaded files
expand-archive master.zip `
  -DestinationPath . `
  -Force

# Change to the tools directory
cd AzureStack-Tools-master

```

## <a name="functionalities-provided-by-the-modules"></a><span data-ttu-id="07971-109">模組所提供的功能</span><span class="sxs-lookup"><span data-stu-id="07971-109">Functionalities provided by the modules</span></span>

<span data-ttu-id="07971-110">AzureStack-Tools 存放庫包含 PowerShell 模組，其支援下列 Azure Stack 功能：</span><span class="sxs-lookup"><span data-stu-id="07971-110">The AzureStack-Tools repository contains PowerShell modules that support the following functionalities for Azure Stack:</span></span>  

| <span data-ttu-id="07971-111">功能</span><span class="sxs-lookup"><span data-stu-id="07971-111">Functionality</span></span> | <span data-ttu-id="07971-112">說明</span><span class="sxs-lookup"><span data-stu-id="07971-112">Description</span></span> | <span data-ttu-id="07971-113">可以使用此模組的人員？</span><span class="sxs-lookup"><span data-stu-id="07971-113">who can use this module?</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="07971-114">雲端功能</span><span class="sxs-lookup"><span data-stu-id="07971-114">Cloud capabilities</span></span>](azure-stack-validate-templates.md) | <span data-ttu-id="07971-115">使用此模組來取得雲端的雲端功能。</span><span class="sxs-lookup"><span data-stu-id="07971-115">Use this module to get the cloud capabilities of a cloud.</span></span> <span data-ttu-id="07971-116">例如，您可以針對 Azure Stack 和使用此模組的 Azure 雲端取得雲端功能，例如 API 版本、Azure Resource Manager 資源、VM 擴充功能等。</span><span class="sxs-lookup"><span data-stu-id="07971-116">For example, you can get the cloud capabilities such as API version, Azure Resource Manager resources, VM extensions etc. for Azure Stack and Azure clouds using this module.</span></span> | <span data-ttu-id="07971-117">雲端系統管理員和使用者。</span><span class="sxs-lookup"><span data-stu-id="07971-117">Cloud administrators and users.</span></span> |
| [<span data-ttu-id="07971-118">Azure Stack 計算系統管理</span><span class="sxs-lookup"><span data-stu-id="07971-118">Azure Stack compute administration</span></span>](azure-stack-add-vm-image.md) | <span data-ttu-id="07971-119">使用此模組，從 Azure Stack Marketplace 新增或移除 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="07971-119">Use this module to add or remove a VM image from the Azure Stack marketplace.</span></span> | <span data-ttu-id="07971-120">雲端系統管理員。</span><span class="sxs-lookup"><span data-stu-id="07971-120">Cloud administrators.</span></span> |
| [<span data-ttu-id="07971-121">Azure Stack 基礎結構系統管理</span><span class="sxs-lookup"><span data-stu-id="07971-121">Azure Stack Infrastructure administration</span></span>](https://github.com/Azure/AzureStack-Tools/blob/master/Infrastructure/README.md) | <span data-ttu-id="07971-122">使用此模組來管理 Azure Stack 基礎結構 VM、警示、更新等。</span><span class="sxs-lookup"><span data-stu-id="07971-122">Use this module to manage Azure Stack infrastructure VMs, alerts, updates etc.</span></span> |  <span data-ttu-id="07971-123">雲端系統管理員。</span><span class="sxs-lookup"><span data-stu-id="07971-123">Cloud administrators.</span></span>|
| [<span data-ttu-id="07971-124">適用於 Azure Stack 的 Resource Manager 原則</span><span class="sxs-lookup"><span data-stu-id="07971-124">Resource Manager policy for Azure Stack</span></span>](azure-stack-policy-module.md) | <span data-ttu-id="07971-125">使用此模組來設定 Azure 訂用帳戶或 Azure 資源群組，包含與 Azure Stack 相同的版本和服務可用性。</span><span class="sxs-lookup"><span data-stu-id="07971-125">Use this module to configure an Azure subscription or an Azure resource group with the same versioning and service availability as Azure Stack.</span></span> | <span data-ttu-id="07971-126">雲端系統管理員和使用者</span><span class="sxs-lookup"><span data-stu-id="07971-126">Cloud administrators and users</span></span> |
| [<span data-ttu-id="07971-127">註冊 Azure</span><span class="sxs-lookup"><span data-stu-id="07971-127">Register with Azure</span></span>](azure-stack-register.md) | <span data-ttu-id="07971-128">搭配使用此模組與 Azure 來註冊您的開發套件執行個體。</span><span class="sxs-lookup"><span data-stu-id="07971-128">Use this module to register your development kit instance with Azure.</span></span> <span data-ttu-id="07971-129">註冊之後，您可以從 Azure 下載 Marketplace 項目，並在 Azure Stack 中使用它們。</span><span class="sxs-lookup"><span data-stu-id="07971-129">After registering, you can download the marketplace items from Azure and use them in Azure Stack.</span></span> | <span data-ttu-id="07971-130">雲端系統管理員</span><span class="sxs-lookup"><span data-stu-id="07971-130">Cloud administrators</span></span> |
| [<span data-ttu-id="07971-131">Azure Stack 部署</span><span class="sxs-lookup"><span data-stu-id="07971-131">Azure Stack deployment</span></span>](azure-stack-run-powershell-script.md) | <span data-ttu-id="07971-132">搭配使用此模組與 Azure Stack 虛擬硬碟 (VHD) 映像，準備要部署與重新部署的 Azure Stack 主機電腦。</span><span class="sxs-lookup"><span data-stu-id="07971-132">Use this module to prepare the Azure Stack host computer to deploy and redeploy by using the Azure Stack Virtual Hard Disk(VHD) image.</span></span> | <span data-ttu-id="07971-133">雲端系統管理員。</span><span class="sxs-lookup"><span data-stu-id="07971-133">Cloud administrators.</span></span> |
| [<span data-ttu-id="07971-134">連線至 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="07971-134">Connecting to Azure Stack</span></span>](azure-stack-connect-powershell.md) | <span data-ttu-id="07971-135">使用此模組，透過 PowerShell 連線至 Azure Stack 執行個體，並設定 Azure Stack 的 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="07971-135">Use this module to connect to an Azure Stack instance through PowerShell and to configure VPN connectivity to Azure Stack.</span></span> | <span data-ttu-id="07971-136">雲端系統管理員和使用者</span><span class="sxs-lookup"><span data-stu-id="07971-136">Cloud administrators and users</span></span> |
| [<span data-ttu-id="07971-137">Azure Stack 服務系統管理</span><span class="sxs-lookup"><span data-stu-id="07971-137">Azure Stack service administration</span></span>](azure-stack-create-offer.md) | <span data-ttu-id="07971-138">Azure 堆疊系統管理員可以使用此模組建立跨計算、 儲存體、 網路和金鑰保存庫服務預設租用戶提供無限制的配額。</span><span class="sxs-lookup"><span data-stu-id="07971-138">Azure Stack administrators can use this module to create a default tenant offer with unlimited quota across Compute, Storage, Network, and Key Vault services.</span></span>   | <span data-ttu-id="07971-139">雲端系統管理員。</span><span class="sxs-lookup"><span data-stu-id="07971-139">Cloud administrators.</span></span>|
| [<span data-ttu-id="07971-140">範本驗證程式</span><span class="sxs-lookup"><span data-stu-id="07971-140">Template validator</span></span>](azure-stack-validate-templates.md) | <span data-ttu-id="07971-141">使用此模組來確認現有或新範本是否可以部署到 Azure Stack。</span><span class="sxs-lookup"><span data-stu-id="07971-141">Use this module to verify if an existing or a new template can be deployed to Azure Stack.</span></span> | <span data-ttu-id="07971-142">雲端系統管理員和使用者</span><span class="sxs-lookup"><span data-stu-id="07971-142">Cloud administrators and users</span></span> |


## <a name="next-steps"></a><span data-ttu-id="07971-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="07971-143">Next steps</span></span>
* [<span data-ttu-id="07971-144">設定 Azure Stack 使用者的 PowerShell 環境</span><span class="sxs-lookup"><span data-stu-id="07971-144">Configure the Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)   
* [<span data-ttu-id="07971-145">透過 VPN 連線至 Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="07971-145">Connect to Azure Stack Development Kit over a VPN</span></span>](azure-stack-connect-azure-stack.md)  

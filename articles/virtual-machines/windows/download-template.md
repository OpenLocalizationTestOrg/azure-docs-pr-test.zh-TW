---
title: "下載 Azure VM 的範本 | Microsoft Docs"
description: "下載 VM 的範本以協助在 Resource Manager 部署模型中進行自動化部署"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 51ef4f51-0942-4249-afea-4a3f87ce1ff8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 9e4c0c3cf0e233447369a24b1d5fe27495abd1cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="download-the-template-for-a-vm"></a><span data-ttu-id="02a1e-103">下載 VM 的範本</span><span class="sxs-lookup"><span data-stu-id="02a1e-103">Download the template for a VM</span></span>
<span data-ttu-id="02a1e-104">當您使用入口網站或 PowerShell 在 Azure 中建立 VM 時，系統會自動為您建立 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="02a1e-104">When you create a VM in Azure using the portal or PowerShell, a Resource Manager template is automatically created for you.</span></span> <span data-ttu-id="02a1e-105">您可以使用此範本快速地重複部署。</span><span class="sxs-lookup"><span data-stu-id="02a1e-105">You can use this template to quickly duplicate a deployment.</span></span> <span data-ttu-id="02a1e-106">範本包含資源群組中所有資源的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="02a1e-106">The template contains information about all of the resources in a resource group.</span></span> <span data-ttu-id="02a1e-107">針對虛擬機器，這表示範本包含針對支援該資源群組中 VM 而建立的所有項目，包括網路功能資源。</span><span class="sxs-lookup"><span data-stu-id="02a1e-107">For a virtual machine, this means the template contains everything that is created in support of the VM in that resource group, including the networking resources.</span></span>

## <a name="download-the-template-using-the-portal"></a><span data-ttu-id="02a1e-108">使用入口網站下載範本</span><span class="sxs-lookup"><span data-stu-id="02a1e-108">Download the template using the portal</span></span>
1. <span data-ttu-id="02a1e-109">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="02a1e-109">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="02a1e-110">在 [中樞] 功能表上，選取 [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="02a1e-110">One the hub menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="02a1e-111">然後從清單中選取虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="02a1e-111">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="02a1e-112">選取 [自動化指令碼]。</span><span class="sxs-lookup"><span data-stu-id="02a1e-112">Select **Automation script**.</span></span>
5. <span data-ttu-id="02a1e-113">選取 [下載]，將 .zip 檔儲存到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="02a1e-113">Select **Download** and save the .zip file to your local computer.</span></span>
6. <span data-ttu-id="02a1e-114">開啟 .zip 檔，並將檔案解壓縮至資料夾。</span><span class="sxs-lookup"><span data-stu-id="02a1e-114">Open the .zip file and extract the files to a folder.</span></span> <span data-ttu-id="02a1e-115">.Zip 檔會包含︰</span><span class="sxs-lookup"><span data-stu-id="02a1e-115">The .zip file will contain:</span></span>
   
   * <span data-ttu-id="02a1e-116">deploy.ps1</span><span class="sxs-lookup"><span data-stu-id="02a1e-116">deploy.ps1</span></span>
   * <span data-ttu-id="02a1e-117">deploy.sh</span><span class="sxs-lookup"><span data-stu-id="02a1e-117">deploy.sh</span></span> 
   * <span data-ttu-id="02a1e-118">deployer.rb</span><span class="sxs-lookup"><span data-stu-id="02a1e-118">deployer.rb</span></span>
   * <span data-ttu-id="02a1e-119">DeploymentHelper.cs</span><span class="sxs-lookup"><span data-stu-id="02a1e-119">DeploymentHelper.cs</span></span>
   * <span data-ttu-id="02a1e-120">parameters.json</span><span class="sxs-lookup"><span data-stu-id="02a1e-120">parameters.json</span></span>
   * <span data-ttu-id="02a1e-121">template.json</span><span class="sxs-lookup"><span data-stu-id="02a1e-121">template.json</span></span>

<span data-ttu-id="02a1e-122">template.json 檔案為範本。</span><span class="sxs-lookup"><span data-stu-id="02a1e-122">The template.json file is the template.</span></span>

## <a name="download-the-template-using-powershell"></a><span data-ttu-id="02a1e-123">使用 PowerShell 下載範本</span><span class="sxs-lookup"><span data-stu-id="02a1e-123">Download the template using PowerShell</span></span>
<span data-ttu-id="02a1e-124">您也可以使用 [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet 下載 .json 範本檔案。</span><span class="sxs-lookup"><span data-stu-id="02a1e-124">You can also download the .json template file using the [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span></span> <span data-ttu-id="02a1e-125">您可以使用 `-path` 參數來提供 .json 檔的檔名和路徑。</span><span class="sxs-lookup"><span data-stu-id="02a1e-125">You can use the `-path` parameter to provide the filename and path for the .json file.</span></span> <span data-ttu-id="02a1e-126">這個範例示範如何將名為 **myResourceGroup** 的資源群組範本下載至本機電腦上的 **C:\users\public\downloads** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="02a1e-126">This example shows how to download the template for the resource group named **myResourceGroup** to the **C:\users\public\downloads** folder on your local computer.</span></span>

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a><span data-ttu-id="02a1e-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="02a1e-127">Next steps</span></span>
<span data-ttu-id="02a1e-128">若要了解有關使用範本部署資源的詳細資訊，請參閱 [Resource Manager 範本逐步解說](../../azure-resource-manager/resource-manager-template-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="02a1e-128">To learn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>


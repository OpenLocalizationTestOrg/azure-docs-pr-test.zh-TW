---
title: "Azure VM 的 aaaDownload hello 範本 |Microsoft 文件"
description: "下載 hello templatefor VM toohelp 與自動化 hello Resource Manager 部署模型中的部署"
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
ms.openlocfilehash: 86fd05f67409019b5e5c9023881745047860eee1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-template-for-a-vm"></a><span data-ttu-id="e678d-103">下載適用於 VM 的 hello 範本</span><span class="sxs-lookup"><span data-stu-id="e678d-103">Download hello template for a VM</span></span>
<span data-ttu-id="e678d-104">當您在 Azure 中建立 VM 時使用 hello 入口網站或 PowerShell，資源管理員範本會自動為您建立。</span><span class="sxs-lookup"><span data-stu-id="e678d-104">When you create a VM in Azure using hello portal or PowerShell, a Resource Manager template is automatically created for you.</span></span> <span data-ttu-id="e678d-105">您可以使用此範本 tooquickly 重複部署。</span><span class="sxs-lookup"><span data-stu-id="e678d-105">You can use this template tooquickly duplicate a deployment.</span></span> <span data-ttu-id="e678d-106">hello 範本包含所有資源群組中的 hello 資源的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e678d-106">hello template contains information about all of hello resources in a resource group.</span></span> <span data-ttu-id="e678d-107">虛擬機器，這表示 hello 範本包含所有以該資源群組，包括 hello 網路功能資源中的 hello VM 支援建立的項目。</span><span class="sxs-lookup"><span data-stu-id="e678d-107">For a virtual machine, this means hello template contains everything that is created in support of hello VM in that resource group, including hello networking resources.</span></span>

## <a name="download-hello-template-using-hello-portal"></a><span data-ttu-id="e678d-108">下載 hello 範本使用 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="e678d-108">Download hello template using hello portal</span></span>
1. <span data-ttu-id="e678d-109">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="e678d-109">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e678d-110">一個 hello 中樞功能表中，選取**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="e678d-110">One hello hub menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="e678d-111">從 [hello] 清單中選取 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e678d-111">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="e678d-112">選取 [自動化指令碼]。</span><span class="sxs-lookup"><span data-stu-id="e678d-112">Select **Automation script**.</span></span>
5. <span data-ttu-id="e678d-113">選取**下載**並儲存 hello.zip 檔案 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="e678d-113">Select **Download** and save hello .zip file tooyour local computer.</span></span>
6. <span data-ttu-id="e678d-114">開啟 hello.zip 檔案，並擷取 hello files tooa 資料夾。</span><span class="sxs-lookup"><span data-stu-id="e678d-114">Open hello .zip file and extract hello files tooa folder.</span></span> <span data-ttu-id="e678d-115">hello.zip 檔案會包含：</span><span class="sxs-lookup"><span data-stu-id="e678d-115">hello .zip file will contain:</span></span>
   
   * <span data-ttu-id="e678d-116">deploy.ps1</span><span class="sxs-lookup"><span data-stu-id="e678d-116">deploy.ps1</span></span>
   * <span data-ttu-id="e678d-117">deploy.sh</span><span class="sxs-lookup"><span data-stu-id="e678d-117">deploy.sh</span></span> 
   * <span data-ttu-id="e678d-118">deployer.rb</span><span class="sxs-lookup"><span data-stu-id="e678d-118">deployer.rb</span></span>
   * <span data-ttu-id="e678d-119">DeploymentHelper.cs</span><span class="sxs-lookup"><span data-stu-id="e678d-119">DeploymentHelper.cs</span></span>
   * <span data-ttu-id="e678d-120">parameters.json</span><span class="sxs-lookup"><span data-stu-id="e678d-120">parameters.json</span></span>
   * <span data-ttu-id="e678d-121">template.json</span><span class="sxs-lookup"><span data-stu-id="e678d-121">template.json</span></span>

<span data-ttu-id="e678d-122">hello 範本 hello template.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="e678d-122">hello template.json file is hello template.</span></span>

## <a name="download-hello-template-using-powershell"></a><span data-ttu-id="e678d-123">下載 hello 範本使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="e678d-123">Download hello template using PowerShell</span></span>
<span data-ttu-id="e678d-124">您也可以下載 hello.json 範本檔案使用 hello[匯出 AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e678d-124">You can also download hello .json template file using hello [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span></span> <span data-ttu-id="e678d-125">您可以使用 hello`-path`參數 tooprovide hello 檔名和路徑 hello.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="e678d-125">You can use hello `-path` parameter tooprovide hello filename and path for hello .json file.</span></span> <span data-ttu-id="e678d-126">這個範例會示範如何 hello 資源群組的 toodownload hello 範本命名**myResourceGroup** toohello **C:\users\public\downloads**在本機電腦上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="e678d-126">This example shows how toodownload hello template for hello resource group named **myResourceGroup** toohello **C:\users\public\downloads** folder on your local computer.</span></span>

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a><span data-ttu-id="e678d-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e678d-127">Next steps</span></span>
<span data-ttu-id="e678d-128">toolearn 進一步了解部署資源使用範本，請參閱[資源管理員範本逐步解說](../../azure-resource-manager/resource-manager-template-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="e678d-128">toolearn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>


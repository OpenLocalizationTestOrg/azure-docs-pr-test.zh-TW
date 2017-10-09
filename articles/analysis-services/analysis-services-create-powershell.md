---
title: "Azure Analysis Services 伺服器使用 PowerShell aaaCreate |Microsoft 文件"
description: "了解如何 toocreate Azure Analysis Services 伺服器使用 PowerShell"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/01/2017
ms.author: owend
ms.custom: mvc
ms.openlocfilehash: 269b78983410f773d47c4cea34d6d353b19f9e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a><span data-ttu-id="8b023-103">使用 PowerShell 來建立 Azure Analysis Services 伺服器</span><span class="sxs-lookup"><span data-stu-id="8b023-103">Create an Azure Analysis Services server by using PowerShell</span></span>

<span data-ttu-id="8b023-104">本快速入門說明如何使用 PowerShell，從 hello 命令列 toocreate Azure Analysis Services 伺服器中的[Azure 資源群組](../azure-resource-manager/resource-group-overview.md)您 Azure 訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="8b023-104">This quickstart describes using PowerShell from hello command line toocreate an Azure Analysis Services server in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in your Azure subscription.</span></span>

<span data-ttu-id="8b023-105">此工作需要 Azure PowerShell 模組 4.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8b023-105">This task requires Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="8b023-106">toofind hello 版本，執行` Get-Module -ListAvailable AzureRM`。</span><span class="sxs-lookup"><span data-stu-id="8b023-106">toofind hello version, run ` Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="8b023-107">tooinstall 或升級，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="8b023-107">tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

> [!NOTE]
> <span data-ttu-id="8b023-108">建立伺服器可能會導致新的可計費服務。</span><span class="sxs-lookup"><span data-stu-id="8b023-108">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="8b023-109">詳細資訊，請參閱 toolearn [Analysis Services 定價](https://azure.microsoft.com/pricing/details/analysis-services/)。</span><span class="sxs-lookup"><span data-stu-id="8b023-109">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b023-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="8b023-110">Prerequisites</span></span>
<span data-ttu-id="8b023-111">toocomplete 本快速入門中，您需要：</span><span class="sxs-lookup"><span data-stu-id="8b023-111">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="8b023-112">**Azure 訂用帳戶**： 瀏覽[Azure 免費試用](https://azure.microsoft.com/offers/ms-azr-0044p/)toocreate 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8b023-112">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="8b023-113">**Azure Active Directory**：您的訂用帳戶必須與 Azure Active Directory 租用戶相關聯，而且您必須在該目錄中有一個帳戶。</span><span class="sxs-lookup"><span data-stu-id="8b023-113">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant and you must have an account in that directory.</span></span> <span data-ttu-id="8b023-114">詳細資訊，請參閱 toolearn[驗證和使用者權限](analysis-services-manage-users.md)。</span><span class="sxs-lookup"><span data-stu-id="8b023-114">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>

## <a name="import-azurermanalysisservices-module"></a><span data-ttu-id="8b023-115">Import AzureRm.AnalysisServices 模組</span><span class="sxs-lookup"><span data-stu-id="8b023-115">Import AzureRm.AnalysisServices module</span></span>
<span data-ttu-id="8b023-116">toocreate 訂用帳戶中的伺服器，使用 hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)元件的模組。</span><span class="sxs-lookup"><span data-stu-id="8b023-116">toocreate a server in your subscription, you use hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  component module.</span></span> <span data-ttu-id="8b023-117">Hello AzureRm.AnalysisServices 模組載入您的 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="8b023-117">Load hello AzureRm.AnalysisServices module into your PowerShell session.</span></span>

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-tooazure"></a><span data-ttu-id="8b023-118">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="8b023-118">Sign in tooAzure</span></span>

<span data-ttu-id="8b023-119">使用 hello 登入 Azure 訂用帳戶 tooyour[新增 AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount)命令。</span><span class="sxs-lookup"><span data-stu-id="8b023-119">Sign in tooyour Azure subscription by using hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command.</span></span> <span data-ttu-id="8b023-120">Hello 螢幕上依照指示操作。</span><span class="sxs-lookup"><span data-stu-id="8b023-120">Follow hello on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="8b023-121">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="8b023-121">Create a resource group</span></span>
 
<span data-ttu-id="8b023-122">[Azure 資源群組](../azure-resource-manager/resource-group-overview.md)是在其中以群組方式部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="8b023-122">An [Azure resource group](../azure-resource-manager/resource-group-overview.md) is a logical container where Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="8b023-123">當您建立伺服器時，必須指定您訂用帳戶中的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8b023-123">When you create your server, you must specify a resource group in your subscription.</span></span> <span data-ttu-id="8b023-124">如果您還沒有資源群組，您可以建立一個新使用 hello[新增 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)命令。</span><span class="sxs-lookup"><span data-stu-id="8b023-124">If you do not already have a resource group, you can create a new one by using hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="8b023-125">hello 下列範例會建立名為的資源群組`myResourceGroup`hello 美國西部區域中。</span><span class="sxs-lookup"><span data-stu-id="8b023-125">hello following example creates a resource group named `myResourceGroup` in hello West US region.</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a><span data-ttu-id="8b023-126">建立伺服器</span><span class="sxs-lookup"><span data-stu-id="8b023-126">Create a server</span></span>

<span data-ttu-id="8b023-127">建立新的伺服器使用 hello[新增 AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver)命令。</span><span class="sxs-lookup"><span data-stu-id="8b023-127">Create a new server by using hello [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="8b023-128">hello 下列範例會建立名為 myServer myResourceGroup，在 hello 美國西部區域中，在 hello D1 層的伺服器，並指定philipc@adventureworks.com身為伺服器管理員。</span><span class="sxs-lookup"><span data-stu-id="8b023-128">hello following example creates a server named myServer in myResourceGroup, in hello West US region, at hello D1 tier, and specifies philipc@adventureworks.com as a server administrator.</span></span>

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a><span data-ttu-id="8b023-129">清除資源</span><span class="sxs-lookup"><span data-stu-id="8b023-129">Clean up resources</span></span>

<span data-ttu-id="8b023-130">您可以從您的訂用帳戶移除 hello 伺服器使用 hello[移除 AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver)命令。</span><span class="sxs-lookup"><span data-stu-id="8b023-130">You can remove hello server from your subscription by using hello [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="8b023-131">如果您繼續進行本集合中的其他快速入門和教學課程，請勿移除您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="8b023-131">If you continue with other quickstarts and tutorials in this collection, do not remove your server.</span></span> <span data-ttu-id="8b023-132">hello 下列範例會移除 hello hello 先前步驟中建立的伺服器。</span><span class="sxs-lookup"><span data-stu-id="8b023-132">hello following example removes hello server created in hello previous step.</span></span>


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="8b023-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8b023-133">Next steps</span></span>
<span data-ttu-id="8b023-134">[使用 PowerShell 管理 Azure Analysis Services](analysis-services-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="8b023-134">[Manage Azure Analysis Services with PowerShell](analysis-services-powershell.md) </span></span>  
<span data-ttu-id="8b023-135">[從 SSDT 部署模型](analysis-services-deploy.md) </span><span class="sxs-lookup"><span data-stu-id="8b023-135">[Deploy a model from SSDT](analysis-services-deploy.md) </span></span>  
[<span data-ttu-id="8b023-136">在 Azure 入口網站中建立模型</span><span class="sxs-lookup"><span data-stu-id="8b023-136">Create a model in Azure portal</span></span>](analysis-services-create-model-portal.md)
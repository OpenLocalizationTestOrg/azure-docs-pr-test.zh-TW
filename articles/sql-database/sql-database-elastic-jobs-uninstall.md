---
title: "如何解除安裝彈性資料庫工作工具"
description: "如何解除安裝彈性資料庫工作工具"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: bfc9d820-edbd-4fca-bfbf-1f339cfcc448
ms.service: sql-database
ms.workload: sql-database
ms.custom: scale out apps
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: ae7f0bce452a0a86f6f1e4d9b0c93a0fa1727f21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="d2b61-103">解除安裝彈性資料庫工作元件</span><span class="sxs-lookup"><span data-stu-id="d2b61-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="d2b61-104">**彈性資料庫工作** 元件可以使用入口網站或 PowerShell 解除安裝。</span><span class="sxs-lookup"><span data-stu-id="d2b61-104">**Elastic Database jobs** components can be uninstalled using either the Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-the-azure-portal"></a><span data-ttu-id="d2b61-105">使用 Azure 入口網站解除安裝彈性資料庫工作元件</span><span class="sxs-lookup"><span data-stu-id="d2b61-105">Uninstall Elastic Database jobs components using the Azure portal</span></span>
1. <span data-ttu-id="d2b61-106">開啟 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="d2b61-106">Open the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d2b61-107">瀏覽至包含 **彈性資料庫工作** 元件的訂用帳戶，也就是彈性資料庫工作元件安裝所在的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d2b61-107">Navigate to the subscription that contains **Elastic Database jobs** components, namely the subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="d2b61-108">按一下 [瀏覽]，然後按一下 [資源群組]。</span><span class="sxs-lookup"><span data-stu-id="d2b61-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="d2b61-109">選取名為 "__ElasticDatabaseJob" 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d2b61-109">Select the resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="d2b61-110">刪除資源群組。</span><span class="sxs-lookup"><span data-stu-id="d2b61-110">Delete the resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="d2b61-111">使用 PowerShell 解除安裝彈性資料庫作業元件</span><span class="sxs-lookup"><span data-stu-id="d2b61-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="d2b61-112">啟動 Microsoft Azure PowerShell 命令視窗，並且瀏覽至 Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x 資料夾底下的工具子目錄：輸入 **cd tools**。</span><span class="sxs-lookup"><span data-stu-id="d2b61-112">Launch a Microsoft Azure PowerShell command window and navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="d2b61-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span><span class="sxs-lookup"><span data-stu-id="d2b61-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span></span>
2. <span data-ttu-id="d2b61-114">執行 .\UninstallElasticDatabaseJobs.ps1 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="d2b61-114">Execute the .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="d2b61-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="d2b61-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="d2b61-116">或者，假設安裝元件時使用預設值，則直接執行下列指令碼：</span><span class="sxs-lookup"><span data-stu-id="d2b61-116">Or simply, execute the following script, assuming default values where used on installation of the components:</span></span>

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "The Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing the Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing the Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a><span data-ttu-id="d2b61-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d2b61-117">Next steps</span></span>
<span data-ttu-id="d2b61-118">若要重新安裝彈性資料庫工作，請參閱 [安裝彈性資料庫工作服務](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="d2b61-118">To re-install Elastic Database jobs, see [Installing the Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="d2b61-119">如需彈性資料庫工作的概觀，請參閱 [彈性資料庫工作概觀](sql-database-elastic-jobs-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d2b61-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->



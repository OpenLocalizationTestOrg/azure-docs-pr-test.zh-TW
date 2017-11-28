---
title: "aaaHow toouninstall 彈性資料庫工作的工具"
description: "如何 toouninstall hello 彈性資料庫工作的工具"
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
ms.openlocfilehash: 3bc1e889d5042bc3eaa9fd9da89816737e0b8df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="3418d-103">解除安裝彈性資料庫工作元件</span><span class="sxs-lookup"><span data-stu-id="3418d-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="3418d-104">**彈性資料庫工作**可以解除安裝元件使用 hello 入口網站或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="3418d-104">**Elastic Database jobs** components can be uninstalled using either hello Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a><span data-ttu-id="3418d-105">解除安裝使用 hello Azure 入口網站的彈性資料庫工作元件</span><span class="sxs-lookup"><span data-stu-id="3418d-105">Uninstall Elastic Database jobs components using hello Azure portal</span></span>
1. <span data-ttu-id="3418d-106">開啟 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="3418d-106">Open hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3418d-107">瀏覽 toohello 訂用帳戶包含**彈性資料庫工作**元件，也就是 hello 的彈性資料庫工作元件已安裝的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3418d-107">Navigate toohello subscription that contains **Elastic Database jobs** components, namely hello subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="3418d-108">按一下 [瀏覽]，然後按一下 [資源群組]。</span><span class="sxs-lookup"><span data-stu-id="3418d-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="3418d-109">名為"__ElasticDatabaseJob"hello 選取資源群組。</span><span class="sxs-lookup"><span data-stu-id="3418d-109">Select hello resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="3418d-110">刪除 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="3418d-110">Delete hello resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="3418d-111">使用 PowerShell 解除安裝彈性資料庫作業元件</span><span class="sxs-lookup"><span data-stu-id="3418d-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="3418d-112">啟動 Microsoft Azure PowerShell 命令視窗並瀏覽 toohello 工具子資料夾下的目錄 hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x： 型別**cd 工具**。</span><span class="sxs-lookup"><span data-stu-id="3418d-112">Launch a Microsoft Azure PowerShell command window and navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="3418d-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span><span class="sxs-lookup"><span data-stu-id="3418d-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span></span>
2. <span data-ttu-id="3418d-114">執行 hello.\UninstallElasticDatabaseJobs.ps1 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="3418d-114">Execute hello .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="3418d-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="3418d-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="3418d-116">只要，執行下列指令碼，假設預設的 hello 或 hello 元件的安裝上使用的值：</span><span class="sxs-lookup"><span data-stu-id="3418d-116">Or simply, execute hello following script, assuming default values where used on installation of hello components:</span></span>

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "hello Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing hello Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing hello Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a><span data-ttu-id="3418d-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3418d-117">Next steps</span></span>
<span data-ttu-id="3418d-118">toore 安裝彈性資料庫作業，請參閱[安裝 hello 彈性資料庫工作服務](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="3418d-118">toore-install Elastic Database jobs, see [Installing hello Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="3418d-119">如需彈性資料庫工作的概觀，請參閱 [彈性資料庫工作概觀](sql-database-elastic-jobs-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3418d-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->



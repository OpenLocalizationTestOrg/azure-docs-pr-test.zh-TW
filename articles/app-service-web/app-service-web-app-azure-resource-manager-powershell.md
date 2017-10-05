---
title: "適用於 Azure Web 應用程式的 Azure Resource Manager 架構 PowerShell 命令 | Microsoft Docs"
description: "深入了解如何使用新的 Azure Resource Manager 架構 PowerShell 命令來管理 Azure Web Apps"
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 8d574f051a327ba0409e6f25a5886af673d3d5e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-powershell-to-manage-azure-web-apps"></a><span data-ttu-id="a68c5-103">使用 Azure Resource Manager 架構 PowerShell 來管理 Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="a68c5-103">Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a68c5-104">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a68c5-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="a68c5-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a68c5-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="a68c5-106">Microsoft Azure PowerShell 1.0.0 版已加入新的命令，讓使用者能夠使用 Azure Resource Manager 架構 PowerShell 命令來管理 Web Apps。</span><span class="sxs-lookup"><span data-stu-id="a68c5-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give the user the ability to use Azure Resource Manager-based PowerShell commands to manage Web Apps.</span></span>

<span data-ttu-id="a68c5-107">若要深入了解如何管理資源群組，請參閱 [搭配使用 Azure PowerShell 與 Azure Resource Manager](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="a68c5-107">To learn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="a68c5-108">若要深入了解適用於 PowerShell Cmdlet 的完整參數和選項清單，請參閱 [Web App Azure Resource Manager 架構 PowerShell Cmdlet 的完整 Cmdlet 參考](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="a68c5-108">To learn about the full list of parameters and options for the PowerShell cmdlets, see the [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="a68c5-109">管理 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="a68c5-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="a68c5-110">建立 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="a68c5-110">Create an App Service Plan</span></span>
<span data-ttu-id="a68c5-111">若要建立 App Service 方案，請使用 **New-AzureRmAppServicePlan** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a68c5-111">To create an app service plan, use the **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="a68c5-112">以下是不同參數的說明︰</span><span class="sxs-lookup"><span data-stu-id="a68c5-112">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="a68c5-113">**Name**：App Service 方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="a68c5-113">**Name**: name of the app service plan.</span></span>
* <span data-ttu-id="a68c5-114">**Location**：服務方案名稱。</span><span class="sxs-lookup"><span data-stu-id="a68c5-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="a68c5-115">**ResourceGroupName**：包含新建立的 App Service 方案的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a68c5-115">**ResourceGroupName**: resource group that includes the newly created app service plan.</span></span>
* <span data-ttu-id="a68c5-116">**Tier**︰想要的定價層 (預設值是 [免費]，其他選項包括 [共用]、[基本]、[標準] 和 [進階])。</span><span class="sxs-lookup"><span data-stu-id="a68c5-116">**Tier**:  the desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="a68c5-117">**WorkerSize**︰背景工作大小 (如果 Tier 參數指定為 [基本]、[標準] 或 [進階]，則預設值為 [小型]。</span><span class="sxs-lookup"><span data-stu-id="a68c5-117">**WorkerSize**: the size of workers (Default is small if the Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="a68c5-118">其他選項為 [中型] 和 [大型])。</span><span class="sxs-lookup"><span data-stu-id="a68c5-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="a68c5-119">**NumberofWorkers**︰App Service 方案中的背景工作數目 (預設值為 1)。</span><span class="sxs-lookup"><span data-stu-id="a68c5-119">**NumberofWorkers**: the number of workers in the app service plan (Default value is 1).</span></span> 

<span data-ttu-id="a68c5-120">使用此 Cmdlet 的範例︰</span><span class="sxs-lookup"><span data-stu-id="a68c5-120">Example to use this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="a68c5-121">在 App Service 環境中建立 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="a68c5-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="a68c5-122">若要在 App Service 環境中建立 App Service 方案，可以使用相同的 **New-AzureRmAppServicePlan** 命令搭配額外的參數，來指定 ASE 的名稱和 ASE 的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="a68c5-122">To create an app service plan in an app service environment, use the same command **New-AzureRmAppServicePlan** command with extra parameters to specify the ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="a68c5-123">使用此 Cmdlet 的範例︰</span><span class="sxs-lookup"><span data-stu-id="a68c5-123">Example to use this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="a68c5-124">若要深入了解 App Service 環境，請查看 [App Service 環境簡介](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="a68c5-124">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="a68c5-125">列出現有的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="a68c5-125">List Existing App Service Plans</span></span>
<span data-ttu-id="a68c5-126">若要列出現有的 App Service 方案，請使用 **Get-AzureRmAppServicePlan** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a68c5-126">To list the existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="a68c5-127">若要列出您訂用帳戶下方的所有 App Service 方案，請使用：</span><span class="sxs-lookup"><span data-stu-id="a68c5-127">To list all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="a68c5-128">若要列出特定資源群組之下的所有 App Service 方案，請使用︰</span><span class="sxs-lookup"><span data-stu-id="a68c5-128">To list all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="a68c5-129">若要取得特定的 App Service 方案，請使用︰</span><span class="sxs-lookup"><span data-stu-id="a68c5-129">To get a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="a68c5-130">設定現有的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="a68c5-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="a68c5-131">若要變更現有 App Service 方案的設定，請使用 **Set-AzureRmAppServicePlan** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a68c5-131">To change the settings for an existing app service plan, use the **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="a68c5-132">您可以變更層級、背景工作大小和背景工作數目</span><span class="sxs-lookup"><span data-stu-id="a68c5-132">You can change the tier, worker size, and the number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="a68c5-133">調整 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="a68c5-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="a68c5-134">若要調整現有的 App Service 方案，請使用：</span><span class="sxs-lookup"><span data-stu-id="a68c5-134">To scale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-the-worker-size-of-an-app-service-plan"></a><span data-ttu-id="a68c5-135">變更 App Service 方案的背景工作大小</span><span class="sxs-lookup"><span data-stu-id="a68c5-135">Changing the worker size of an App Service Plan</span></span>
<span data-ttu-id="a68c5-136">若要變更現有 App Service 方案中的背景工作大小，請使用︰</span><span class="sxs-lookup"><span data-stu-id="a68c5-136">To change the size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-the-tier-of-an-app-service-plan"></a><span data-ttu-id="a68c5-137">變更 App Service 方案的層級</span><span class="sxs-lookup"><span data-stu-id="a68c5-137">Changing the Tier of an App Service Plan</span></span>
<span data-ttu-id="a68c5-138">若要變更現有 App Service 方案的層級，請使用︰</span><span class="sxs-lookup"><span data-stu-id="a68c5-138">To change the tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="a68c5-139">刪除現有的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="a68c5-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="a68c5-140">若要刪除現有的 App Service 方案，需要先移動或刪除所有已指派的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a68c5-140">To delete an existing app service plan, all assigned web apps need to be moved or deleted first.</span></span> <span data-ttu-id="a68c5-141">然後使用 **Remove-AzureRmAppServicePlan** Cmdlet，就可以刪除 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="a68c5-141">Then using the **Remove-AzureRmAppServicePlan** cmdlet you can delete the app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="a68c5-142">管理 App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="a68c5-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="a68c5-143">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a68c5-143">Create a Web App</span></span>
<span data-ttu-id="a68c5-144">若要建立 Web 應用程式，請使用 **New-AzureRmWebApp** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a68c5-144">To create a web app, use the **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="a68c5-145">以下是不同參數的說明︰</span><span class="sxs-lookup"><span data-stu-id="a68c5-145">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="a68c5-146">**Name**：Web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="a68c5-146">**Name**: name for the web app.</span></span>
* <span data-ttu-id="a68c5-147">**AppServicePlan**︰用來裝載 Web 應用程式的服務方案名稱。</span><span class="sxs-lookup"><span data-stu-id="a68c5-147">**AppServicePlan**: name for the service plan used to host the web app.</span></span>
* <span data-ttu-id="a68c5-148">**ResourceGroupName**：裝載 App Service 方案的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a68c5-148">**ResourceGroupName**: resource group that hosts the App service plan.</span></span>
* <span data-ttu-id="a68c5-149">**Location**：Web 應用程式位置。</span><span class="sxs-lookup"><span data-stu-id="a68c5-149">**Location**: the web app location.</span></span>

<span data-ttu-id="a68c5-150">使用此 Cmdlet 的範例︰</span><span class="sxs-lookup"><span data-stu-id="a68c5-150">Example to use this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="a68c5-151">在 App Service 環境中建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a68c5-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="a68c5-152">在 App Service 環境 (ASE) 中建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a68c5-152">To create a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="a68c5-153">使用相同的 **New-AzureRmWebApp** 命令搭配額外的參數，來指定 ASE 名稱和 ASE 所屬的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="a68c5-153">Use the same **New-AzureRmWebApp** command with extra parameters to specify the ASE name and the resource group name that the ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="a68c5-154">若要深入了解 App Service 環境，請查看 [App Service 環境簡介](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="a68c5-154">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="a68c5-155">刪除現有的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a68c5-155">Delete an existing Web App</span></span>
<span data-ttu-id="a68c5-156">若要刪除現有的 Web 應用程式，您可以使用 **Remove-AzureRmWebApp** Cmdlet，還必須指定 Web 應用程式名稱和資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="a68c5-156">To delete an existing web app you can use the **Remove-AzureRmWebApp** cmdlet, you need to specify the name of the web app and the resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="a68c5-157">列出現有的 Web Apps</span><span class="sxs-lookup"><span data-stu-id="a68c5-157">List existing Web Apps</span></span>
<span data-ttu-id="a68c5-158">若要列出現有的 Web 應用程式，請使用 **Get-AzureRmWebApp** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a68c5-158">To list the existing web apps, use the **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="a68c5-159">若要列出您的訂用帳戶之下的所有 Web 應用程式，請使用︰</span><span class="sxs-lookup"><span data-stu-id="a68c5-159">To list all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="a68c5-160">若要列出特定資源群組之下的所有 Web 應用程式，請使用︰</span><span class="sxs-lookup"><span data-stu-id="a68c5-160">To list all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="a68c5-161">若要取得特定的 Web 應用程式，請使用︰</span><span class="sxs-lookup"><span data-stu-id="a68c5-161">To get a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="a68c5-162">設定現有的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a68c5-162">Configure an existing Web App</span></span>
<span data-ttu-id="a68c5-163">若要變更現有 Web 應用程式的設定和組態，請使用 **Set-AzureRmWebApp** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a68c5-163">To change the settings and configurations for an existing web app, use the **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="a68c5-164">如需完整的參數清單，請查看 [Cmdlet 參考連結](https://msdn.microsoft.com/library/mt652487.aspx)</span><span class="sxs-lookup"><span data-stu-id="a68c5-164">For a full list of parameters, check the [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="a68c5-165">範例 (1)：使用此 Cmdlet 來變更連接字串</span><span class="sxs-lookup"><span data-stu-id="a68c5-165">Example (1): use this cmdlet to change connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="a68c5-166">範例 (2)：新增或變更應用程式設定</span><span class="sxs-lookup"><span data-stu-id="a68c5-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="a68c5-167">範例 (3)：將 Web 應用程式設定為在 64 位元模式下執行</span><span class="sxs-lookup"><span data-stu-id="a68c5-167">Example (3):  set the web app to run in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-the-state-of-an-existing-web-app"></a><span data-ttu-id="a68c5-168">變更現有 Web 應用程式的狀態</span><span class="sxs-lookup"><span data-stu-id="a68c5-168">Change the state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="a68c5-169">重新啟動 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a68c5-169">Restart a web app</span></span>
<span data-ttu-id="a68c5-170">若要重新啟動 Web 應用程式，您必須指定 Web 應用程式的名稱和資源群組。</span><span class="sxs-lookup"><span data-stu-id="a68c5-170">To restart a web app, you must specify the name and resource group of the web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="a68c5-171">停止 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a68c5-171">Stop a web app</span></span>
<span data-ttu-id="a68c5-172">若要停止 Web 應用程式，您必須指定 Web 應用程式的名稱和資源群組。</span><span class="sxs-lookup"><span data-stu-id="a68c5-172">To stop a web app, you must specify the name and resource group of the web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="a68c5-173">啟動 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a68c5-173">Start a web app</span></span>
<span data-ttu-id="a68c5-174">若要啟動 Web 應用程式，您必須指定 Web 應用程式的名稱和資源群組。</span><span class="sxs-lookup"><span data-stu-id="a68c5-174">To start a web app, you must specify the name and resource group of the web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="a68c5-175">管理 Web 應用程式發行設定檔</span><span class="sxs-lookup"><span data-stu-id="a68c5-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="a68c5-176">每個 Web 應用程式都有發佈設定檔可用來發佈您的應用程式，並可在發行設定檔上執行許多作業。</span><span class="sxs-lookup"><span data-stu-id="a68c5-176">Each web app has a publishing profile that can be used to publish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="a68c5-177">取得發行設定檔</span><span class="sxs-lookup"><span data-stu-id="a68c5-177">Get Publishing Profile</span></span>
<span data-ttu-id="a68c5-178">若要取得 Web 應用程式的發行設定檔，請使用︰</span><span class="sxs-lookup"><span data-stu-id="a68c5-178">To get the publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="a68c5-179">這個命令會將發佈設定檔回應至命令列，以及將發行設定檔輸出至文字檔案。</span><span class="sxs-lookup"><span data-stu-id="a68c5-179">This command echoes the publishing profile to the command line as well output the publishing profile to a text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="a68c5-180">重設發行設定檔</span><span class="sxs-lookup"><span data-stu-id="a68c5-180">Reset Publishing Profile</span></span>
<span data-ttu-id="a68c5-181">若要同時對 Web 應用程式的 FTP 和 Web 部署重設發行密碼，使用︰</span><span class="sxs-lookup"><span data-stu-id="a68c5-181">To reset both the publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="a68c5-182">管理 Web 應用程式憑證</span><span class="sxs-lookup"><span data-stu-id="a68c5-182">Manage Web App Certificates</span></span>
<span data-ttu-id="a68c5-183">若要深入了解如何管理 Web 應用程式憑證，請參閱 [使用 PowerShell 的 SSL 憑證繫結](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="a68c5-183">To learn about how to manage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="a68c5-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a68c5-184">Next Steps</span></span>
* <span data-ttu-id="a68c5-185">若要深入了解 Azure Resource Manager PowerShell 支援，請參閱 [搭配使用 Azure PowerShell 與 Azure Resource Manager](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="a68c5-185">To learn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="a68c5-186">若要深入了解 App Service 環境，請參閱 [App Service 環境簡介](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="a68c5-186">To learn about App Service Environments, see [Introduction to App Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="a68c5-187">若要深入了解如何使用 PowerShell 來管理 App Service SSL 憑證，請參閱 [使用 PowerShell 的 SSL 憑證繫結](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="a68c5-187">To learn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="a68c5-188">若要了解適用於 Azure Web Apps 的 Azure Resource Manager 架構 PowerShell Cmdlet，請參閱 [Web Apps Azure Resource Manager PowerShell Cmdlet 的 Azure Cmdlet 參考](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="a68c5-188">To learn about the full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="a68c5-189">若要了解如何使用 CLI 管理 App Service，請參閱[使用適用於 Azure Web 應用程式的 Azure Resource Manager 架構 XPlat CLI。](app-service-web-app-azure-resource-manager-xplat-cli.md)</span><span class="sxs-lookup"><span data-stu-id="a68c5-189">To learn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>


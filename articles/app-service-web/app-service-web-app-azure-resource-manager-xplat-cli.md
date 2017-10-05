---
title: "適用於 Azure Web 應用程式的 Azure Resource Manager 架構跨平台命令列工具 | Microsoft Docs"
description: "深入了解如何使用新的 Azure Resource Manager 架構跨平台命令列工具來管理 Azure Web Apps。"
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 7a03e1417617453c43edcc3787da10d171359757
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a><span data-ttu-id="ebfd5-103">使用適用於 Azure App Service 的 Azure Resource Manager 架構 XPlat CLI</span><span class="sxs-lookup"><span data-stu-id="ebfd5-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ebfd5-104">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ebfd5-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="ebfd5-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebfd5-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)

<span data-ttu-id="ebfd5-106">隨著 Microsoft Azure 跨平台命令列工具 0.10.5 版的推出，已增加新的命令。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-106">With the release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span></span> <span data-ttu-id="ebfd5-107">這些命令讓使用者能夠使用 Azure Resource Manager 架構 PowerShell 命令來管理 App Service。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-107">These commands give the user the ability to use Azure Resource Manager-based PowerShell commands to manage App Service.</span></span>

<span data-ttu-id="ebfd5-108">若要了解如何管理資源群組，請參閱[使用 Azure CLI 管理 Azure 資源和資源群組](../azure-resource-manager/xplat-cli-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-108">To learn about managing Resource Groups, see [Use the Azure CLI to manage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span></span> 

> [!NOTE] 
> <span data-ttu-id="ebfd5-109">此外，請試用以 Python 所撰寫、可供資源管理部署模型使用的新一代 CLI [Azure CLI 2.0](https://github.com/Azure/azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-109">Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for the resource management deployment model.</span></span>
>
>

## <a name="managing-app-service-plans"></a><span data-ttu-id="ebfd5-110">管理 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="ebfd5-110">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="ebfd5-111">建立 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="ebfd5-111">Create an App Service Plan</span></span>
<span data-ttu-id="ebfd5-112">若要建立 App Service 方案，請使用 **azure appserviceplan create** 命令。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-112">To create an app service plan, use the **azure appserviceplan create** command.</span></span>

<span data-ttu-id="ebfd5-113">以下是不同參數的說明︰</span><span class="sxs-lookup"><span data-stu-id="ebfd5-113">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="ebfd5-114">**--resource-group**：包含新建立之 App Service 方案的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-114">**--resource-group**: resource group that includes the newly created app service plan.</span></span>
* <span data-ttu-id="ebfd5-115">**--name**：App Service 方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-115">**--name**: name of the app service plan.</span></span>
* <span data-ttu-id="ebfd5-116">**--location**：App Service 方案位置。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-116">**--location**: app service plan location.</span></span>
* <span data-ttu-id="ebfd5-117">**--sku**：所需的定價 sku (選項包括︰F1 (免費)。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-117">**--sku**:  the desired pricing sku (The options are: F1 (Free).</span></span> <span data-ttu-id="ebfd5-118">D1 (共用)。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-118">D1 (Shared).</span></span> <span data-ttu-id="ebfd5-119">B1 (基本小型)、B2 (基本中型) 和 B3 (基本大型)。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span></span> <span data-ttu-id="ebfd5-120">S1 (標準小型)、S2 (標準中型) 和 S3 (標準大型)。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span></span> <span data-ttu-id="ebfd5-121">P1 (進階小型)、P2 (進階中型) 和 P3 (進階大型)。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span></span>
* <span data-ttu-id="ebfd5-122">**-instances**︰App Service 方案中的背景工作角色數目 (預設值為 1)。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-122">**--instances**: the number of workers in the app service plan (Default value is 1).</span></span>

<span data-ttu-id="ebfd5-123">使用此 Cmdlet 的範例︰</span><span class="sxs-lookup"><span data-stu-id="ebfd5-123">Example to use this cmdlet:</span></span>

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="ebfd5-124">建立 Linux App Service 方案</span><span class="sxs-lookup"><span data-stu-id="ebfd5-124">Create a Linux App Service Plan</span></span>

<span data-ttu-id="ebfd5-125">使用相同 **azure appserviceplan create** 命令，搭配額外的參數 **-islinux true**。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-125">Using the same **azure appserviceplan create** command, with the extra parameter **--islinux true**.</span></span> <span data-ttu-id="ebfd5-126">注意 [Linux 上的 App Service 簡介](app-service-linux-intro.md)中所述的限制和區域</span><span class="sxs-lookup"><span data-stu-id="ebfd5-126">Note the restrictions and regions outlined in [Introduction to App Service on Linux](app-service-linux-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="ebfd5-127">列出現有的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="ebfd5-127">List Existing App Service Plans</span></span>
<span data-ttu-id="ebfd5-128">若要列出現有的 App Service 方案，請使用 **azure appserviceplan list** 命令。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-128">To list the existing app service plans, use **azure appserviceplan list** command.</span></span>

<span data-ttu-id="ebfd5-129">若要列出特定資源群組之下的所有 App Service 方案，請使用︰</span><span class="sxs-lookup"><span data-stu-id="ebfd5-129">To list all app service plans under a specific resource group, use:</span></span>

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="ebfd5-130">若要取得特定的 App Service 方案，請使用 **azure appserviceplan show** 命令：</span><span class="sxs-lookup"><span data-stu-id="ebfd5-130">To get a specific app service plan, use **azure appserviceplan show** command:</span></span>

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="ebfd5-131">設定現有的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="ebfd5-131">Configure an existing App Service Plan</span></span>
<span data-ttu-id="ebfd5-132">若要變更現有 App Service 方案的設定，請使用 **azure appserviceplan config** 命令。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-132">To change the settings for an existing app service plan, use the **azure appserviceplan config** command.</span></span> <span data-ttu-id="ebfd5-133">您可以變更 sku 和背景工作角色數目</span><span class="sxs-lookup"><span data-stu-id="ebfd5-133">You can change the sku, and the number of workers</span></span> 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="ebfd5-134">調整 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="ebfd5-134">Scaling an App Service Plan</span></span>
<span data-ttu-id="ebfd5-135">若要調整現有的 App Service 方案，請使用：</span><span class="sxs-lookup"><span data-stu-id="ebfd5-135">To scale an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-the-sku-of-an-app-service-plan"></a><span data-ttu-id="ebfd5-136">變更 App Service 方案的 SKU</span><span class="sxs-lookup"><span data-stu-id="ebfd5-136">Changing the SKU of an App Service Plan</span></span>
<span data-ttu-id="ebfd5-137">若要變更現有 App Service 方案的 sku，請使用︰</span><span class="sxs-lookup"><span data-stu-id="ebfd5-137">To change the sku of an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="ebfd5-138">刪除現有的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="ebfd5-138">Delete an existing App Service Plan</span></span>
<span data-ttu-id="ebfd5-139">若要刪除現有的 App Service 方案，需要先移動或刪除所有已指派的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-139">To delete an existing app service plan, all assigned apps need to be moved or deleted first.</span></span> <span data-ttu-id="ebfd5-140">然後使用 **azure webapp delete** 命令，就可以刪除 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-140">Then using the **azure webapp delete** command you can delete the app service plan.</span></span>

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a><span data-ttu-id="ebfd5-141">管理 App Service 應用程式</span><span class="sxs-lookup"><span data-stu-id="ebfd5-141">Managing App Service apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="ebfd5-142">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ebfd5-142">Create a web app</span></span>
<span data-ttu-id="ebfd5-143">若要建立 Web 應用程式，請使用 **azure webapp create** 命令。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-143">To create a web app, use the **azure webapp create** command.</span></span>

<span data-ttu-id="ebfd5-144">以下是不同參數的說明︰</span><span class="sxs-lookup"><span data-stu-id="ebfd5-144">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="ebfd5-145">**--name**：Web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-145">**--name**: name for the web app.</span></span>
* <span data-ttu-id="ebfd5-146">**-plan**︰用來裝載 Web 應用程式的服務方案名稱。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-146">**--plan**: name for the service plan used to host the web app.</span></span>
* <span data-ttu-id="ebfd5-147">**--resource-group**：裝載 App Service 方案的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-147">**--resource-group**: resource group that hosts the App service plan.</span></span>
* <span data-ttu-id="ebfd5-148">**--location**：Web 應用程式位置。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-148">**--location**: the web app location.</span></span>

<span data-ttu-id="ebfd5-149">使用此 Cmdlet 的範例︰</span><span class="sxs-lookup"><span data-stu-id="ebfd5-149">Example to use this cmdlet:</span></span>

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a><span data-ttu-id="ebfd5-150">刪除現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="ebfd5-150">Delete an existing app</span></span>
<span data-ttu-id="ebfd5-151">若要刪除現有的應用程式，您可以使用 **azure webapp delete** 命令。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-151">To delete an existing app, you can use the **azure webapp delete** command.</span></span> <span data-ttu-id="ebfd5-152">您需要指定應用程式的名稱和資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-152">You need to specify the name of the app and the resource group name.</span></span>

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a><span data-ttu-id="ebfd5-153">列出現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="ebfd5-153">List existing apps</span></span>
<span data-ttu-id="ebfd5-154">若要列出現有的應用程式，請使用 **azure webapp list** 命令。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-154">To list the existing apps, use the **azure webapp list** command.</span></span>

<span data-ttu-id="ebfd5-155">若要列出特定資源群組中的所有應用程式，請使用︰</span><span class="sxs-lookup"><span data-stu-id="ebfd5-155">To list all apps in a specific resource group, use:</span></span>

    azure webapp list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="ebfd5-156">若要取得特定的應用程式，請使用 **azure webapp show** 命令。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-156">To get a specific app, use the **azure webapp show** command.</span></span>

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a><span data-ttu-id="ebfd5-157">設定現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="ebfd5-157">Configure an existing app</span></span>
<span data-ttu-id="ebfd5-158">若要變更現有應用程式的設定和組態，請使用 **azure webapp config set** 命令。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-158">To change the settings and configurations for an existing app, use the **azure webapp config set** command.</span></span>

<span data-ttu-id="ebfd5-159">範例 (1)：變更應用程式的 php 版本</span><span class="sxs-lookup"><span data-stu-id="ebfd5-159">Example (1): change the php version of a app</span></span> 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

<span data-ttu-id="ebfd5-160">範例 (2)：新增或變更應用程式設定</span><span class="sxs-lookup"><span data-stu-id="ebfd5-160">Example (2): add or change app settings</span></span>

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

<span data-ttu-id="ebfd5-161">若想知道還可變更其他哪些組態，請使用 **azure webapp config set -h** 命令。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-161">To know what other configuration can be changed, use the **azure webapp config set -h** command.</span></span>

### <a name="change-the-state-of-an-existing-app"></a><span data-ttu-id="ebfd5-162">變更現有應用程式的狀態</span><span class="sxs-lookup"><span data-stu-id="ebfd5-162">Change the state of an existing app</span></span>
#### <a name="restart-an-app"></a><span data-ttu-id="ebfd5-163">重新啟動應用程式</span><span class="sxs-lookup"><span data-stu-id="ebfd5-163">Restart an app</span></span>
<span data-ttu-id="ebfd5-164">若要重新啟動應用程式，您必須指定應用程式的名稱和資源群組。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-164">To restart an app, you must specify the name and resource group of the app.</span></span>

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a><span data-ttu-id="ebfd5-165">停止應用程式</span><span class="sxs-lookup"><span data-stu-id="ebfd5-165">Stop an app</span></span>
<span data-ttu-id="ebfd5-166">若要停止應用程式，您必須指定應用程式的名稱和資源群組。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-166">To stop an app, you must specify the name and resource group of the app.</span></span>

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a><span data-ttu-id="ebfd5-167">啟動應用程式</span><span class="sxs-lookup"><span data-stu-id="ebfd5-167">Start an app</span></span>
<span data-ttu-id="ebfd5-168">若要啟動應用程式，您必須指定應用程式的名稱和資源群組。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-168">To start an app, you must specify the name and resource group of the app.</span></span>

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a><span data-ttu-id="ebfd5-169">管理應用程式的發行設定檔</span><span class="sxs-lookup"><span data-stu-id="ebfd5-169">Manage publishing profiles of an app</span></span>
<span data-ttu-id="ebfd5-170">每個應用程式都有可用來發佈程式碼的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-170">Each app has a publishing profile that can be used to publish your code.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="ebfd5-171">取得發行設定檔</span><span class="sxs-lookup"><span data-stu-id="ebfd5-171">Get Publishing Profile</span></span>
<span data-ttu-id="ebfd5-172">若要取得應用程式的發行設定檔，請使用︰</span><span class="sxs-lookup"><span data-stu-id="ebfd5-172">To get the publishing profile for a app, use:</span></span>

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

<span data-ttu-id="ebfd5-173">此命令會將發行設定檔使用者名稱和密碼回應到命令列。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-173">This command echoes the publishing profile username and password to the command line.</span></span>

### <a name="manage-app-hostnames"></a><span data-ttu-id="ebfd5-174">管理應用程式主機名稱</span><span class="sxs-lookup"><span data-stu-id="ebfd5-174">Manage app hostnames</span></span>
<span data-ttu-id="ebfd5-175">若要管理應用程式的主機名稱繫結，請使用 **azure webapp config hostnames** 命令</span><span class="sxs-lookup"><span data-stu-id="ebfd5-175">To manage hostname bindings for your app, use the **azure webapp config hostnames** command</span></span>  

#### <a name="list-hostname-bindings"></a><span data-ttu-id="ebfd5-176">列出主機名稱繫結</span><span class="sxs-lookup"><span data-stu-id="ebfd5-176">List hostname bindings</span></span>
<span data-ttu-id="ebfd5-177">若要取得應用程式目前的主機名稱繫結，請使用︰</span><span class="sxs-lookup"><span data-stu-id="ebfd5-177">To get the current hostname bindings for an app, use:</span></span>

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a><span data-ttu-id="ebfd5-178">新增主機名稱繫結</span><span class="sxs-lookup"><span data-stu-id="ebfd5-178">Add hostname bindings</span></span>
<span data-ttu-id="ebfd5-179">若要將主機名稱繫結新增至應用程式，請使用︰</span><span class="sxs-lookup"><span data-stu-id="ebfd5-179">To add hostname bindings to an app, use:</span></span>

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a><span data-ttu-id="ebfd5-180">刪除主機名稱繫結</span><span class="sxs-lookup"><span data-stu-id="ebfd5-180">Delete hostname bindings</span></span>
<span data-ttu-id="ebfd5-181">若要刪除主機名稱繫結，請使用︰</span><span class="sxs-lookup"><span data-stu-id="ebfd5-181">To delete hostname bindings, use:</span></span>

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a><span data-ttu-id="ebfd5-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ebfd5-182">Next Steps</span></span>
* <span data-ttu-id="ebfd5-183">若要了解 Azure Resource Manager 支援，請參閱[使用 Azure CLI 管理 Azure 資源和資源群組](../azure-resource-manager/xplat-cli-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="ebfd5-183">To learn about Azure Resource Manager CLI support, see [Use the Azure CLI to manage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span></span>
* <span data-ttu-id="ebfd5-184">若要了解如何使用 PowerShell 管理 App Service，請參閱[使用 Azure Resource Manager 架構 PowerShell 來管理 Azure Web Apps。](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="ebfd5-184">To learn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span></span>
* <span data-ttu-id="ebfd5-185">若要了解 Linux 上的 Azure App Service，請參閱 [Linux 上的 App Service 簡介](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="ebfd5-185">To learn about Azure App Service on Linux, see [Introduction to App Service on Linux](app-service-linux-intro.md)</span></span>

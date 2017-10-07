---
title: "aaaAzure Azure Web 應用程式的資源管理員型跨平台命令列工具 |Microsoft 文件"
description: "了解如何 toouse 會 hello 新的 Azure 資源管理員為基礎的跨平台命令列工具 toomanage Azure Web 應用程式。"
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
ms.openlocfilehash: 5f5e03edcb01154aef3bd220cd27358f69656ef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a><span data-ttu-id="8347d-103">使用適用於 Azure App Service 的 Azure Resource Manager 架構 XPlat CLI</span><span class="sxs-lookup"><span data-stu-id="8347d-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8347d-104">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8347d-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="8347d-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8347d-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)

<span data-ttu-id="8347d-106">Hello 版的 Microsoft Azure 跨平台命令列工具版本 0.10.5，已加入新的命令。</span><span class="sxs-lookup"><span data-stu-id="8347d-106">With hello release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span></span> <span data-ttu-id="8347d-107">這些命令可讓 hello 使用者 hello 能力 toouse Azure 資源管理員為基礎的 PowerShell 命令 toomanage 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="8347d-107">These commands give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage App Service.</span></span>

<span data-ttu-id="8347d-108">toolearn 有關管理資源群組，請參閱[使用 hello Azure CLI toomanage Azure 資源與資源群組](../azure-resource-manager/xplat-cli-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="8347d-108">toolearn about managing Resource Groups, see [Use hello Azure CLI toomanage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span></span> 

> [!NOTE] 
> <span data-ttu-id="8347d-109">此外，試試看[Azure CLI 2.0](https://github.com/Azure/azure-cli)、 下一代 CLI Python 撰寫 hello 資源管理部署模型。</span><span class="sxs-lookup"><span data-stu-id="8347d-109">Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for hello resource management deployment model.</span></span>
>
>

## <a name="managing-app-service-plans"></a><span data-ttu-id="8347d-110">管理 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="8347d-110">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="8347d-111">建立 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="8347d-111">Create an App Service Plan</span></span>
<span data-ttu-id="8347d-112">toocreate 的應用程式服務計劃中，使用 hello **azure appserviceplan 建立**命令。</span><span class="sxs-lookup"><span data-stu-id="8347d-112">toocreate an app service plan, use hello **azure appserviceplan create** command.</span></span>

<span data-ttu-id="8347d-113">以下是 hello 不同參數的說明：</span><span class="sxs-lookup"><span data-stu-id="8347d-113">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="8347d-114">**-資源群組**： 包含 hello 新建立的應用程式服務計劃的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8347d-114">**--resource-group**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="8347d-115">**-名稱**: hello 應用程式服務方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="8347d-115">**--name**: name of hello app service plan.</span></span>
* <span data-ttu-id="8347d-116">**--location**：App Service 方案位置。</span><span class="sxs-lookup"><span data-stu-id="8347d-116">**--location**: app service plan location.</span></span>
* <span data-ttu-id="8347d-117">**-sku**: hello 預期定價的 sku (hello 選項包括： F1 (Free)。</span><span class="sxs-lookup"><span data-stu-id="8347d-117">**--sku**:  hello desired pricing sku (hello options are: F1 (Free).</span></span> <span data-ttu-id="8347d-118">D1 (共用)。</span><span class="sxs-lookup"><span data-stu-id="8347d-118">D1 (Shared).</span></span> <span data-ttu-id="8347d-119">B1 (基本小型)、B2 (基本中型) 和 B3 (基本大型)。</span><span class="sxs-lookup"><span data-stu-id="8347d-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span></span> <span data-ttu-id="8347d-120">S1 (標準小型)、S2 (標準中型) 和 S3 (標準大型)。</span><span class="sxs-lookup"><span data-stu-id="8347d-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span></span> <span data-ttu-id="8347d-121">P1 (進階小型)、P2 (進階中型) 和 P3 (進階大型)。</span><span class="sxs-lookup"><span data-stu-id="8347d-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span></span>
* <span data-ttu-id="8347d-122">**-執行個體**: hello hello （預設值為 1） 的應用程式服務方案中的背景工作數目。</span><span class="sxs-lookup"><span data-stu-id="8347d-122">**--instances**: hello number of workers in hello app service plan (Default value is 1).</span></span>

<span data-ttu-id="8347d-123">範例 toouse 這個指令程式：</span><span class="sxs-lookup"><span data-stu-id="8347d-123">Example toouse this cmdlet:</span></span>

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="8347d-124">建立 Linux App Service 方案</span><span class="sxs-lookup"><span data-stu-id="8347d-124">Create a Linux App Service Plan</span></span>

<span data-ttu-id="8347d-125">使用 hello 相同**azure appserviceplan 建立**命令，以 hello 額外的參數**-islinux true**。</span><span class="sxs-lookup"><span data-stu-id="8347d-125">Using hello same **azure appserviceplan create** command, with hello extra parameter **--islinux true**.</span></span> <span data-ttu-id="8347d-126">請注意 hello 事項中所述的區域[簡介 tooApp Linux 上的服務](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="8347d-126">Note hello restrictions and regions outlined in [Introduction tooApp Service on Linux](app-service-linux-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="8347d-127">列出現有的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="8347d-127">List Existing App Service Plans</span></span>
<span data-ttu-id="8347d-128">toolist hello 現有 app service 方案，使用**azure appserviceplan 清單**命令。</span><span class="sxs-lookup"><span data-stu-id="8347d-128">toolist hello existing app service plans, use **azure appserviceplan list** command.</span></span>

<span data-ttu-id="8347d-129">toolist 所有應用程式服務方案的特定資源群組下，使用：</span><span class="sxs-lookup"><span data-stu-id="8347d-129">toolist all app service plans under a specific resource group, use:</span></span>

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="8347d-130">使用特定的應用程式服務方案，tooget **azure appserviceplan 顯示**命令：</span><span class="sxs-lookup"><span data-stu-id="8347d-130">tooget a specific app service plan, use **azure appserviceplan show** command:</span></span>

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="8347d-131">設定現有的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="8347d-131">Configure an existing App Service Plan</span></span>
<span data-ttu-id="8347d-132">toochange hello 設定現有的應用程式服務方案，使用 hello **azure appserviceplan config**命令。</span><span class="sxs-lookup"><span data-stu-id="8347d-132">toochange hello settings for an existing app service plan, use hello **azure appserviceplan config** command.</span></span> <span data-ttu-id="8347d-133">您可以變更 hello sku 和 hello 背景工作數目</span><span class="sxs-lookup"><span data-stu-id="8347d-133">You can change hello sku, and hello number of workers</span></span> 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="8347d-134">調整 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="8347d-134">Scaling an App Service Plan</span></span>
<span data-ttu-id="8347d-135">tooscale 現有應用程式服務計劃，請使用：</span><span class="sxs-lookup"><span data-stu-id="8347d-135">tooscale an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-hello-sku-of-an-app-service-plan"></a><span data-ttu-id="8347d-136">變更 hello SKU 的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="8347d-136">Changing hello SKU of an App Service Plan</span></span>
<span data-ttu-id="8347d-137">toochange hello sku 的現有應用程式服務計劃，使用：</span><span class="sxs-lookup"><span data-stu-id="8347d-137">toochange hello sku of an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="8347d-138">刪除現有的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="8347d-138">Delete an existing App Service Plan</span></span>
<span data-ttu-id="8347d-139">toodelete 現有的應用程式服務方案，所有指派的應用程式需要 toobe 移動或刪除第一次。</span><span class="sxs-lookup"><span data-stu-id="8347d-139">toodelete an existing app service plan, all assigned apps need toobe moved or deleted first.</span></span> <span data-ttu-id="8347d-140">然後使用 hello **azure webapp 刪除**命令，您可以刪除 hello 應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="8347d-140">Then using hello **azure webapp delete** command you can delete hello app service plan.</span></span>

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a><span data-ttu-id="8347d-141">管理 App Service 應用程式</span><span class="sxs-lookup"><span data-stu-id="8347d-141">Managing App Service apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="8347d-142">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="8347d-142">Create a web app</span></span>
<span data-ttu-id="8347d-143">toocreate web 應用程式，使用 hello **azure webapp 建立**命令。</span><span class="sxs-lookup"><span data-stu-id="8347d-143">toocreate a web app, use hello **azure webapp create** command.</span></span>

<span data-ttu-id="8347d-144">以下是 hello 不同參數的說明：</span><span class="sxs-lookup"><span data-stu-id="8347d-144">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="8347d-145">**-名稱**: hello web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="8347d-145">**--name**: name for hello web app.</span></span>
* <span data-ttu-id="8347d-146">**-計劃**: hello 服務計劃使用 toohost hello web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="8347d-146">**--plan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="8347d-147">**-資源群組**： 裝載 hello 應用程式服務計劃的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8347d-147">**--resource-group**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="8347d-148">**-位置**: hello web 應用程式位置。</span><span class="sxs-lookup"><span data-stu-id="8347d-148">**--location**: hello web app location.</span></span>

<span data-ttu-id="8347d-149">範例 toouse 這個指令程式：</span><span class="sxs-lookup"><span data-stu-id="8347d-149">Example toouse this cmdlet:</span></span>

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a><span data-ttu-id="8347d-150">刪除現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="8347d-150">Delete an existing app</span></span>
<span data-ttu-id="8347d-151">toodelete 現有的應用程式，您可以使用 hello **azure webapp 刪除**命令。</span><span class="sxs-lookup"><span data-stu-id="8347d-151">toodelete an existing app, you can use hello **azure webapp delete** command.</span></span> <span data-ttu-id="8347d-152">您需要 toospecify hello hello 應用程式名稱和 hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="8347d-152">You need toospecify hello name of hello app and hello resource group name.</span></span>

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a><span data-ttu-id="8347d-153">列出現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="8347d-153">List existing apps</span></span>
<span data-ttu-id="8347d-154">toolist hello 現有應用程式，請使用 hello **azure webapp 清單**命令。</span><span class="sxs-lookup"><span data-stu-id="8347d-154">toolist hello existing apps, use hello **azure webapp list** command.</span></span>

<span data-ttu-id="8347d-155">toolist 特定資源群組中的所有應用程式使用：</span><span class="sxs-lookup"><span data-stu-id="8347d-155">toolist all apps in a specific resource group, use:</span></span>

    azure webapp list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="8347d-156">tooget 特定的應用程式，使用 hello **azure webapp 顯示**命令。</span><span class="sxs-lookup"><span data-stu-id="8347d-156">tooget a specific app, use hello **azure webapp show** command.</span></span>

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a><span data-ttu-id="8347d-157">設定現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="8347d-157">Configure an existing app</span></span>
<span data-ttu-id="8347d-158">toochange hello 設定和設定現有的應用程式，以使用 hello **azure webapp 組態集**命令。</span><span class="sxs-lookup"><span data-stu-id="8347d-158">toochange hello settings and configurations for an existing app, use hello **azure webapp config set** command.</span></span>

<span data-ttu-id="8347d-159">範例 (1): 變更應用程式的 hello php 版本</span><span class="sxs-lookup"><span data-stu-id="8347d-159">Example (1): change hello php version of a app</span></span> 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

<span data-ttu-id="8347d-160">範例 (2)：新增或變更應用程式設定</span><span class="sxs-lookup"><span data-stu-id="8347d-160">Example (2): add or change app settings</span></span>

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

<span data-ttu-id="8347d-161">您可以變更哪些其他組態，tooknow 使用 hello **azure webapp 組態集-h**命令。</span><span class="sxs-lookup"><span data-stu-id="8347d-161">tooknow what other configuration can be changed, use hello **azure webapp config set -h** command.</span></span>

### <a name="change-hello-state-of-an-existing-app"></a><span data-ttu-id="8347d-162">變更現有的應用程式的 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="8347d-162">Change hello state of an existing app</span></span>
#### <a name="restart-an-app"></a><span data-ttu-id="8347d-163">重新啟動應用程式</span><span class="sxs-lookup"><span data-stu-id="8347d-163">Restart an app</span></span>
<span data-ttu-id="8347d-164">toorestart 應用程式，您必須指定 hello hello 應用程式的名稱和資源群組。</span><span class="sxs-lookup"><span data-stu-id="8347d-164">toorestart an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a><span data-ttu-id="8347d-165">停止應用程式</span><span class="sxs-lookup"><span data-stu-id="8347d-165">Stop an app</span></span>
<span data-ttu-id="8347d-166">toostop 應用程式，您必須指定 hello hello 應用程式的名稱和資源群組。</span><span class="sxs-lookup"><span data-stu-id="8347d-166">toostop an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a><span data-ttu-id="8347d-167">啟動應用程式</span><span class="sxs-lookup"><span data-stu-id="8347d-167">Start an app</span></span>
<span data-ttu-id="8347d-168">toostart 應用程式，您必須指定 hello hello 應用程式的名稱和資源群組。</span><span class="sxs-lookup"><span data-stu-id="8347d-168">toostart an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a><span data-ttu-id="8347d-169">管理應用程式的發行設定檔</span><span class="sxs-lookup"><span data-stu-id="8347d-169">Manage publishing profiles of an app</span></span>
<span data-ttu-id="8347d-170">每個應用程式具有發行設定檔可能是使用的 toopublish 您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="8347d-170">Each app has a publishing profile that can be used toopublish your code.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="8347d-171">取得發行設定檔</span><span class="sxs-lookup"><span data-stu-id="8347d-171">Get Publishing Profile</span></span>
<span data-ttu-id="8347d-172">發行設定檔，應用程式中，使用 tooget hello:</span><span class="sxs-lookup"><span data-stu-id="8347d-172">tooget hello publishing profile for a app, use:</span></span>

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

<span data-ttu-id="8347d-173">此命令會回應 hello 發行設定檔的使用者名稱和密碼 toohello 命令列。</span><span class="sxs-lookup"><span data-stu-id="8347d-173">This command echoes hello publishing profile username and password toohello command line.</span></span>

### <a name="manage-app-hostnames"></a><span data-ttu-id="8347d-174">管理應用程式主機名稱</span><span class="sxs-lookup"><span data-stu-id="8347d-174">Manage app hostnames</span></span>
<span data-ttu-id="8347d-175">toomanage 應用程式的主機名稱繫結使用 hello **azure webapp 設定 hostname**命令</span><span class="sxs-lookup"><span data-stu-id="8347d-175">toomanage hostname bindings for your app, use hello **azure webapp config hostnames** command</span></span>  

#### <a name="list-hostname-bindings"></a><span data-ttu-id="8347d-176">列出主機名稱繫結</span><span class="sxs-lookup"><span data-stu-id="8347d-176">List hostname bindings</span></span>
<span data-ttu-id="8347d-177">tooget hello 目前主機名稱繫結的應用程式，使用：</span><span class="sxs-lookup"><span data-stu-id="8347d-177">tooget hello current hostname bindings for an app, use:</span></span>

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a><span data-ttu-id="8347d-178">新增主機名稱繫結</span><span class="sxs-lookup"><span data-stu-id="8347d-178">Add hostname bindings</span></span>
<span data-ttu-id="8347d-179">tooadd 主機名稱繫結 tooan 應用程式，使用：</span><span class="sxs-lookup"><span data-stu-id="8347d-179">tooadd hostname bindings tooan app, use:</span></span>

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a><span data-ttu-id="8347d-180">刪除主機名稱繫結</span><span class="sxs-lookup"><span data-stu-id="8347d-180">Delete hostname bindings</span></span>
<span data-ttu-id="8347d-181">toodelete 主機名稱繫結，請使用：</span><span class="sxs-lookup"><span data-stu-id="8347d-181">toodelete hostname bindings, use:</span></span>

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a><span data-ttu-id="8347d-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8347d-182">Next Steps</span></span>
* <span data-ttu-id="8347d-183">toolearn 有關 Azure 資源管理員 CLI 支援，請參閱[使用 hello Azure CLI toomanage Azure 資源與資源群組。](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="8347d-183">toolearn about Azure Resource Manager CLI support, see [Use hello Azure CLI toomanage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span></span>
* <span data-ttu-id="8347d-184">toolearn 有關管理應用程式服務使用 PowerShell，請參閱[Using Azure Resource Manager-Based PowerShell tooManage Azure Web 應用程式。](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="8347d-184">toolearn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span></span>
* <span data-ttu-id="8347d-185">toolearn 有關 Azure App Service on Linux，請參閱[簡介 tooApp Linux 上的服務](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="8347d-185">toolearn about Azure App Service on Linux, see [Introduction tooApp Service on Linux](app-service-linux-intro.md)</span></span>

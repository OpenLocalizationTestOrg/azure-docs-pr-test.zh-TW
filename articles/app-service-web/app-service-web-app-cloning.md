---
title: "aaaWeb 應用程式複製使用 PowerShell"
description: "深入了解如何 tooclone Web 應用程式 toonew Web 應用程式使用 PowerShell。"
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: f9a5cfa1-fbb0-41e6-95d1-75d457347a35
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: b8882370d6db6939f8e4473ccc1414091bdcb8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a><span data-ttu-id="eb9ff-103">使用 PowerShell 複製 Azure App Service App</span><span class="sxs-lookup"><span data-stu-id="eb9ff-103">Azure App Service App Cloning Using PowerShell</span></span>
<span data-ttu-id="eb9ff-104">與 Microsoft Azure PowerShell hello 版本 1.1.0 版的新選項已加入 tooNew AzureRMWebApp、 可讓現有的 Web 應用程式 tooa 新建立的應用程式在不同的區域或 hello hello 使用者 hello 能力 tooclone 相同的區域。</span><span class="sxs-lookup"><span data-stu-id="eb9ff-104">With hello release of Microsoft Azure PowerShell version 1.1.0 a new option has been added tooNew-AzureRMWebApp that would give hello user hello ability tooclone an existing Web App tooa newly created app in a different region or in hello same region.</span></span> <span data-ttu-id="eb9ff-105">這可讓客戶 toodeploy 的應用程式的數字跨越不同地區，快速且輕鬆地。</span><span class="sxs-lookup"><span data-stu-id="eb9ff-105">This will enable customers toodeploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="eb9ff-106">應用程式複製目前僅支援 Premium 層 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="eb9ff-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="eb9ff-107">新功能使用 hello hello 相同限制 Web 應用程式備份功能，請參閱 <<c0> [ 備份 web 應用程式在 Azure App Service 中](web-sites-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="eb9ff-107">hello new feature uses hello same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="eb9ff-108">有關使用 Azure Resource Manager toolearn 基礎的 Azure PowerShell cmdlet toomanage 您 Web 應用程式的簽入[Azure 資源管理員的 Azure Web 應用程式架構 PowerShell 命令](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="eb9ff-108">toolearn about using Azure Resource Manager based Azure PowerShell cmdlets toomanage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="cloning-an-existing-app"></a><span data-ttu-id="eb9ff-109">複製現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="eb9ff-109">Cloning an existing App</span></span>
<span data-ttu-id="eb9ff-110">案例： 在美國中南部地區中的現有 web 應用程式，hello 使用者希望 tooclone hello 內容 tooa 新 web 應用程式在美國中北部地區。</span><span class="sxs-lookup"><span data-stu-id="eb9ff-110">Scenario: An existing web app in South Central US region, hello user would like tooclone hello contents tooa new web app in North Central US region.</span></span> <span data-ttu-id="eb9ff-111">這可以透過 hello Azure 資源管理員版本 hello PowerShell cmdlet toocreate 新的 web 應用程式與 hello-SourceWebApp 選項完成。</span><span class="sxs-lookup"><span data-stu-id="eb9ff-111">This can be accomplished by using hello Azure Resource Manager version of hello PowerShell cmdlet toocreate a new web app with hello -SourceWebApp option.</span></span>

<span data-ttu-id="eb9ff-112">了解 hello 資源群組名稱，其中包含 hello 來源 web 應用程式，我們可以使用下列 PowerShell 命令 tooget hello 來源 web 應用程式的資訊 （在此情況下名為來源 webapp） hello:</span><span class="sxs-lookup"><span data-stu-id="eb9ff-112">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="eb9ff-113">新的 App Service 方案 toocreate，我們可以使用如 hello 下列範例所示新增 AzureRmAppServicePlan 命令</span><span class="sxs-lookup"><span data-stu-id="eb9ff-113">toocreate a new App Service Plan, we can use New-AzureRmAppServicePlan command as in hello following example</span></span>

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

<span data-ttu-id="eb9ff-114">使用 hello 新增 AzureRmWebApp 命令，我們可以在 hello 美國中北部區域中，建立 hello 新 web 應用程式，並將它連接 tooan App Service 方案現有 premium 層，此外，我們也可以使用相同的資源群組為 hello 來源 web 應用程式，或定義新的資源群組的 hellohello 下列示範：</span><span class="sxs-lookup"><span data-stu-id="eb9ff-114">Using hello New-AzureRmWebApp command, we can create hello new web app in hello North Central US region, and tie it tooan existing premium tier App Service Plan, moreover we can use hello same resource group as hello source web app, or define a new resource group, hello following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

<span data-ttu-id="eb9ff-115">包括所有相關聯的部署位置的現有 web 應用程式，hello 使用者將需要 toouse tooclone hello IncludeSourceWebAppSlots 參數，下列 PowerShell 命令的 hello 示範 hello 使用該參數以 hello 新增 AzureRmWebApp 命令：</span><span class="sxs-lookup"><span data-stu-id="eb9ff-115">tooclone an existing web app including all associated deployment slots, hello user will need toouse hello IncludeSourceWebAppSlots parameter, hello following PowerShell command demonstrates hello use of that parameter with hello New-AzureRmWebApp command:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

<span data-ttu-id="eb9ff-116">tooclone hello 內現有的 web 應用程式相同的區域，hello 使用者將需要新的資源群組和新的應用程式服務計劃在 hello toocreate 相同的區域，然後使用下列 PowerShell 命令 tooclone hello web 應用程式的 hello</span><span class="sxs-lookup"><span data-stu-id="eb9ff-116">tooclone an existing web app within hello same region, hello user will need toocreate a new resource group and a new app service plan in hello same region, and then using hello following PowerShell command tooclone hello web app</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a><span data-ttu-id="eb9ff-117">複製現有的應用程式 tooan App Service 環境</span><span class="sxs-lookup"><span data-stu-id="eb9ff-117">Cloning an existing App tooan App Service Environment</span></span>
<span data-ttu-id="eb9ff-118">案例： 在美國中南部地區中的現有 web 應用程式，hello 使用者希望 tooclone hello 內容 tooa 新 web 應用程式 tooan 現有應用程式服務環境 (ASE)。</span><span class="sxs-lookup"><span data-stu-id="eb9ff-118">Scenario: An existing web app in South Central US region, hello user would like tooclone hello contents tooa new web app tooan existing App Service Environment (ASE).</span></span>

<span data-ttu-id="eb9ff-119">了解 hello 資源群組名稱，其中包含 hello 來源 web 應用程式，我們可以使用下列 PowerShell 命令 tooget hello 來源 web 應用程式的資訊 （在此情況下名為來源 webapp） hello:</span><span class="sxs-lookup"><span data-stu-id="eb9ff-119">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="eb9ff-120">了解 hello ASE 名稱和 hello hello ASE 所屬的資源群組名稱，hello 使用者可以使用 toocreate hello 新 web 應用程式在 hello 現有 ASE，遵循 hello 示範 hello 新增 AzureRmWebApp 命令：</span><span class="sxs-lookup"><span data-stu-id="eb9ff-120">Knowing hello ASE's name, and hello resource group name that hello ASE belongs to, hello user can use hello New-AzureRmWebApp command toocreate hello new web app in hello existing ASE, hello following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

<span data-ttu-id="eb9ff-121">hello 位置參數是必要項，因為 toolegacy 原因，但 hello 案例在 ase 中建立應用程式將會忽略它。</span><span class="sxs-lookup"><span data-stu-id="eb9ff-121">hello Location parameter is required due toolegacy reason, but in hello case of creating an app in an ASE it will be ignored.</span></span> 

## <a name="cloning-an-existing-app-slot"></a><span data-ttu-id="eb9ff-122">複製現有的應用程式位置</span><span class="sxs-lookup"><span data-stu-id="eb9ff-122">Cloning an existing App Slot</span></span>
<span data-ttu-id="eb9ff-123">案例： hello 使用者希望 tooclone 現有的 Web 應用程式位置 tooeither 新的 Web 應用程式或新的 Web 應用程式位置。</span><span class="sxs-lookup"><span data-stu-id="eb9ff-123">Scenario: hello user would like tooclone an existing Web App Slot tooeither a new Web App or a new Web App slot.</span></span> <span data-ttu-id="eb9ff-124">新的 Web 應用程式可以在 hello hello 與 hello 原始 Web 應用程式的位置，或不同區域中相同的區域。</span><span class="sxs-lookup"><span data-stu-id="eb9ff-124">hello new Web App can be in hello same region as hello original Web App slot or in a different region.</span></span>

<span data-ttu-id="eb9ff-125">了解 hello 資源群組名稱，其中包含 hello 來源 web 應用程式，我們可以使用下列 PowerShell 命令 tooget hello 來源 web 應用程式位置的資訊 （在此情況下名為來源 webappslot） 繫結 tooWeb 應用程式來源 webapp hello:</span><span class="sxs-lookup"><span data-stu-id="eb9ff-125">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app slot's information (in this case named source-webappslot) tied tooWeb App source-webapp:</span></span>

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

<span data-ttu-id="eb9ff-126">hello 下列示範如何建立 hello 來源 web 應用程式 tooa 新 web 應用程式的複本：</span><span class="sxs-lookup"><span data-stu-id="eb9ff-126">hello following demonstrates creating a clone of hello source web app tooa new web app:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a><span data-ttu-id="eb9ff-127">設定流量管理員同時複製應用程式</span><span class="sxs-lookup"><span data-stu-id="eb9ff-127">Configuring Traffic Manager while cloning a App</span></span>
<span data-ttu-id="eb9ff-128">建立多區域 web 應用程式，並設定 Azure Traffic Manager tooroute 流量 tooall 這些 web 應用程式，會在複製您擁有現有的 web 應用程式時，客戶的應用程式是高可用性，n 的重要案例 tooinsure hello 選項 tooconnect 這兩個 web應用程式 tooeither 新的流量管理員設定檔或現有-請注意，只有 Azure 資源管理員的支援流量管理員。</span><span class="sxs-lookup"><span data-stu-id="eb9ff-128">Creating multi-region web apps and configuring Azure Traffic Manager tooroute traffic tooall these web apps, is a n important scenario tooinsure that customers' apps are highly available, when cloning an existing web app you have hello option tooconnect both web apps tooeither a new traffic manager profile or an existing one - note that only Azure Resource Manager version of Traffic Manager is supported.</span></span>

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a><span data-ttu-id="eb9ff-129">建立新流量管理員設定檔同時複製應用程式</span><span class="sxs-lookup"><span data-stu-id="eb9ff-129">Creating a new Traffic Manager profile while cloning a App</span></span>
<span data-ttu-id="eb9ff-130">案例： hello 使用者希望 tooclone web 應用程式 tooanother 區域，設定 Azure 資源管理員流量管理員設定檔包含兩個 web 應用程式時。</span><span class="sxs-lookup"><span data-stu-id="eb9ff-130">Scenario: hello user would like tooclone an web app tooanother region, while configuring an Azure Resource Manager traffic manager profile that include both web apps.</span></span> <span data-ttu-id="eb9ff-131">hello 以下會示範建立複製品的 hello 來源 web 應用程式 tooa 新 web 應用程式設定新的 Traffic Manager 設定檔時：</span><span class="sxs-lookup"><span data-stu-id="eb9ff-131">hello following demonstrates creating a clone of hello source web app tooa new web app while configuring a new Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-tooan-existing-traffic-manager-profile"></a><span data-ttu-id="eb9ff-132">加入新複製的 Web 應用程式 tooan 現有流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="eb9ff-132">Adding new cloned Web App tooan existing Traffic Manager profile</span></span>
<span data-ttu-id="eb9ff-133">案例： hello 使用者已經有 Azure 資源管理員流量管理員設定檔，他希望 tooadd web 應用程式做為端點。</span><span class="sxs-lookup"><span data-stu-id="eb9ff-133">Scenario: hello user already have an Azure Resource Manager traffic manager profile that he would like tooadd both web apps as endpoints.</span></span> <span data-ttu-id="eb9ff-134">toodo 因此，我們必須先 tooassemble hello 現有流量管理員設定檔識別碼，我們必須 hello 訂用帳戶 id、 資源群組名稱和 hello 現有流量管理員設定檔名稱。</span><span class="sxs-lookup"><span data-stu-id="eb9ff-134">toodo so, we first need tooassemble hello existing traffic manager profile id, we will need hello subscription id, resource group name and hello existing traffic manager profile name.</span></span>

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

<span data-ttu-id="eb9ff-135">有 hello traffic manger 識別碼之後, hello 以下會示範建立 hello 來源 web 應用程式 tooa 新 web 應用程式的複製，同時將它們加入 tooan 現有流量管理員設定檔：</span><span class="sxs-lookup"><span data-stu-id="eb9ff-135">After having hello traffic manger id, hello following demonstrates creating a clone of hello source web app tooa new web app while adding them tooan existing Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a><span data-ttu-id="eb9ff-136">目前的限制</span><span class="sxs-lookup"><span data-stu-id="eb9ff-136">Current Restrictions</span></span>
<span data-ttu-id="eb9ff-137">這項功能目前為預覽狀態，我們目前正在處理 tooadd 新功能經過一段時間，hello 清單後面是 hello hello 複製應用程式的目前版本的已知的限制：</span><span class="sxs-lookup"><span data-stu-id="eb9ff-137">This feature is currently in preview, we are working tooadd new capabilities over time, hello following list are hello known restrictions on hello current version of app cloning:</span></span>

* <span data-ttu-id="eb9ff-138">不會複製自動調整設定</span><span class="sxs-lookup"><span data-stu-id="eb9ff-138">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="eb9ff-139">不會複製備份排程設定</span><span class="sxs-lookup"><span data-stu-id="eb9ff-139">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="eb9ff-140">不會複製 VNET 設定</span><span class="sxs-lookup"><span data-stu-id="eb9ff-140">VNET settings are not cloned</span></span>
* <span data-ttu-id="eb9ff-141">App Insights 不會自動上設定 hello 目的地 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="eb9ff-141">App Insights are not automatically set up on hello destination web app</span></span>
* <span data-ttu-id="eb9ff-142">不會複製簡單驗證設定</span><span class="sxs-lookup"><span data-stu-id="eb9ff-142">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="eb9ff-143">不會複製 Kudu 延伸模組</span><span class="sxs-lookup"><span data-stu-id="eb9ff-143">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="eb9ff-144">不會複製 TiP 規則</span><span class="sxs-lookup"><span data-stu-id="eb9ff-144">TiP rules are not cloned</span></span>
* <span data-ttu-id="eb9ff-145">不會複製資料庫內容</span><span class="sxs-lookup"><span data-stu-id="eb9ff-145">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="eb9ff-146">參考</span><span class="sxs-lookup"><span data-stu-id="eb9ff-146">References</span></span>
* [<span data-ttu-id="eb9ff-147">適用於 Azure Web 應用程式的 Azure Resource Manager 架構 PowerShell 命令</span><span class="sxs-lookup"><span data-stu-id="eb9ff-147">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="eb9ff-148">使用 Azure 入口網站複製 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="eb9ff-148">Web App Cloning using Azure Portal</span></span>](app-service-web-app-cloning-portal.md)
* [<span data-ttu-id="eb9ff-149">在 Azure App Service 中備份 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="eb9ff-149">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="eb9ff-150">Azure Resource Manager 的 Azure 流量管理員支援預覽</span><span class="sxs-lookup"><span data-stu-id="eb9ff-150">Azure Resource Manager support for Azure Traffic Manager Preview</span></span>](../traffic-manager/traffic-manager-powershell-arm.md)
* [<span data-ttu-id="eb9ff-151">簡介 tooApp Service 環境</span><span class="sxs-lookup"><span data-stu-id="eb9ff-151">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="eb9ff-152">搭配使用 Azure PowerShell 與 Azure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="eb9ff-152">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)


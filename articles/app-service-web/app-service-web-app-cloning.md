---
title: "使用 PowerShell 複製 Web 應用程式"
description: "了解如何使用 PowerShell，將您的 Web Apps 複製到新的 Web Apps。"
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
ms.openlocfilehash: d47d5a2f7d2462525bf37718a234e222b4f64e6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a><span data-ttu-id="01e8a-103">使用 PowerShell 複製 Azure App Service App</span><span class="sxs-lookup"><span data-stu-id="01e8a-103">Azure App Service App Cloning Using PowerShell</span></span>
<span data-ttu-id="01e8a-104">隨著 Microsoft Azure PowerShell 版本 1.1.0 的發行，為 New-AzureRMWebApp 加入了新選項，可讓使用者將現有的 Web 應用程式複製到在不同區域或在相同區域中新建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="01e8a-104">With the release of Microsoft Azure PowerShell version 1.1.0 a new option has been added to New-AzureRMWebApp that would give the user the ability to clone an existing Web App to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="01e8a-105">這可讓客戶輕鬆且快速地跨不同區域部署許多 app。</span><span class="sxs-lookup"><span data-stu-id="01e8a-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="01e8a-106">應用程式複製目前僅支援 Premium 層 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="01e8a-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="01e8a-107">新的功能使用與 Web Apps 備份功能相同的限制，請參閱 [在 Azure App Service 中備份 Web 應用程式](web-sites-backup.md)。</span><span class="sxs-lookup"><span data-stu-id="01e8a-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="01e8a-108">若要了解如何使用 Azure Resource Manager 架構 Azure PowerShell Cmdlet 來管理您的 Web Apps，請查看 [適用於 Azure Web App 的 Azure Resource Manager 架構 PowerShell 命令](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="01e8a-108">To learn about using Azure Resource Manager based Azure PowerShell cmdlets to manage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="cloning-an-existing-app"></a><span data-ttu-id="01e8a-109">複製現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="01e8a-109">Cloning an existing App</span></span>
<span data-ttu-id="01e8a-110">案例：使用者想要將位在美國中南部區域的現有 Web 應用程式內容複製到位在美國中北部區域的新 Web 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="01e8a-110">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app in North Central US region.</span></span> <span data-ttu-id="01e8a-111">使用 Azure Resource Manager 版本 PowerShell Cmdlet 利用 -SourceWebApp 選項來建立新的 Web 應用程式，即可實現此目的。</span><span class="sxs-lookup"><span data-stu-id="01e8a-111">This can be accomplished by using the Azure Resource Manager version of the PowerShell cmdlet to create a new web app with the -SourceWebApp option.</span></span>

<span data-ttu-id="01e8a-112">了解包含來源 Web 應用程式的資源群組名稱，我們可以使用下列 PowerShell 命令來取得來源 Web 應用程式的資訊 (在此情況下名為 source-webapp)：</span><span class="sxs-lookup"><span data-stu-id="01e8a-112">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="01e8a-113">若要建立新的 App Service 方案，我們可以使用 New-AzureRmAppServicePlan 命令，如下列範例所示</span><span class="sxs-lookup"><span data-stu-id="01e8a-113">To create a new App Service Plan, we can use New-AzureRmAppServicePlan command as in the following example</span></span>

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

<span data-ttu-id="01e8a-114">使用 New-AzureRmWebApp 命令，我們可以在美國中北部區域中建立新的 Web 應用程式，並將它連接至現有的 Premium 層 App Service 方案，而且我們可以使用相同的資源群組作為來源 Web 應用程式，或定義新的資源群組，範例如下：</span><span class="sxs-lookup"><span data-stu-id="01e8a-114">Using the New-AzureRmWebApp command, we can create the new web app in the North Central US region, and tie it to an existing premium tier App Service Plan, moreover we can use the same resource group as the source web app, or define a new resource group, the following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

<span data-ttu-id="01e8a-115">若要複製現有的 Web 應用程式 (包括所有相關聯的部署位置)，使用者必須使用 IncludeSourceWebAppSlots 參數，以下 PowerShell 命令示範如何使用該參數搭配 New-AzureRmWebApp 命令：</span><span class="sxs-lookup"><span data-stu-id="01e8a-115">To clone an existing web app including all associated deployment slots, the user will need to use the IncludeSourceWebAppSlots parameter, the following PowerShell command demonstrates the use of that parameter with the New-AzureRmWebApp command:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

<span data-ttu-id="01e8a-116">若要在相同區域中複製現有的 Web 應用程式，使用者必須在相同區域中建立新資源群組和新的 App Service 方案，然後使用下列 PowerShell 命令來複製 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="01e8a-116">To clone an existing web app within the same region, the user will need to create a new resource group and a new app service plan in the same region, and then using the following PowerShell command to clone the web app</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="01e8a-117">複製現有應用程式至 App Service 環境</span><span class="sxs-lookup"><span data-stu-id="01e8a-117">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="01e8a-118">案例：使用者想要將位在美國中南部區域的現有 Web 應用程式的內容複製到現有的 App Service 環境 (ASE) 的新 Web 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="01e8a-118">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app to an existing App Service Environment (ASE).</span></span>

<span data-ttu-id="01e8a-119">了解包含來源 Web 應用程式的資源群組名稱，我們可以使用下列 PowerShell 命令來取得來源 Web 應用程式的資訊 (在此情況下名為 source-webapp)：</span><span class="sxs-lookup"><span data-stu-id="01e8a-119">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="01e8a-120">知道 ASE 的名稱和 ASE 所屬的資源群組名稱，使用者可以使用 New-AzureRmWebApp 命令在現有的 ASE 中建立新的 Web 應用程式，以下示範：</span><span class="sxs-lookup"><span data-stu-id="01e8a-120">Knowing the ASE's name, and the resource group name that the ASE belongs to, the user can use the New-AzureRmWebApp command to create the new web app in the existing ASE, the following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

<span data-ttu-id="01e8a-121">由於使用舊版，必須提供位置參數；但如果是在 ASE 中建立應用程式，則將會忽略它。</span><span class="sxs-lookup"><span data-stu-id="01e8a-121">The Location parameter is required due to legacy reason, but in the case of creating an app in an ASE it will be ignored.</span></span> 

## <a name="cloning-an-existing-app-slot"></a><span data-ttu-id="01e8a-122">複製現有的應用程式位置</span><span class="sxs-lookup"><span data-stu-id="01e8a-122">Cloning an existing App Slot</span></span>
<span data-ttu-id="01e8a-123">案例：使用者想要將現有 Web 應用程式位置複製到新 Web 應用程式或新的 Web 應用程式位置。</span><span class="sxs-lookup"><span data-stu-id="01e8a-123">Scenario: The user would like to clone an existing Web App Slot to either a new Web App or a new Web App slot.</span></span> <span data-ttu-id="01e8a-124">新的 Web 應用程式可以在與原始的 Web 應用程式位置位於相同區域或不同區域中。</span><span class="sxs-lookup"><span data-stu-id="01e8a-124">The new Web App can be in the same region as the original Web App slot or in a different region.</span></span>

<span data-ttu-id="01e8a-125">了解包含來源 Web 應用程式的資源群組名稱，我們可以使用下列 PowerShell 命令來取得繫結至 Web App source-webapp 之來源 Web 應用程式的位置資訊 (在此情況下名為 source-webapp)：</span><span class="sxs-lookup"><span data-stu-id="01e8a-125">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app slot's information (in this case named source-webappslot) tied to Web App source-webapp:</span></span>

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

<span data-ttu-id="01e8a-126">以下示範建立來源 Web 應用程式的複製到新的 Web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="01e8a-126">The following demonstrates creating a clone of the source web app to a new web app:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a><span data-ttu-id="01e8a-127">設定流量管理員同時複製應用程式</span><span class="sxs-lookup"><span data-stu-id="01e8a-127">Configuring Traffic Manager while cloning a App</span></span>
<span data-ttu-id="01e8a-128">建立多重區域 Web 應用程式，並設定 Azure 流量管理員，將流量路由到這些 Web 應用程式，重要的案例是確保客戶的應用程式為高可用性，當複製現有的 Web 應用程式時，您可以選擇將兩個 Web 應用程式連接到新的流量管理員設定檔或現有的設定檔 - 請注意，僅支援 Azure Resource Manager 版本的流量管理員。</span><span class="sxs-lookup"><span data-stu-id="01e8a-128">Creating multi-region web apps and configuring Azure Traffic Manager to route traffic to all these web apps, is a n important scenario to insure that customers' apps are highly available, when cloning an existing web app you have the option to connect both web apps to either a new traffic manager profile or an existing one - note that only Azure Resource Manager version of Traffic Manager is supported.</span></span>

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a><span data-ttu-id="01e8a-129">建立新流量管理員設定檔同時複製應用程式</span><span class="sxs-lookup"><span data-stu-id="01e8a-129">Creating a new Traffic Manager profile while cloning a App</span></span>
<span data-ttu-id="01e8a-130">案例：使用者想要將 Web 應用程式複製到另一個區域中，同時設定包含兩個 Web 應用程式的 Azure Resource Manager 流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="01e8a-130">Scenario: The user would like to clone an web app to another region, while configuring an Azure Resource Manager traffic manager profile that include both web apps.</span></span> <span data-ttu-id="01e8a-131">以下示範建立來源 Web 應用程式的複製到新的 Web 應用程式，同時設定新流量管理員設定檔：</span><span class="sxs-lookup"><span data-stu-id="01e8a-131">The following demonstrates creating a clone of the source web app to a new web app while configuring a new Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-to-an-existing-traffic-manager-profile"></a><span data-ttu-id="01e8a-132">加入新複製的 Web 應用程式至現有的流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="01e8a-132">Adding new cloned Web App to an existing Traffic Manager profile</span></span>
<span data-ttu-id="01e8a-133">案例：使用者已經有他想要將兩個 Web 應用程式加入為端點的 Azure Resource Manager 流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="01e8a-133">Scenario: The user already have an Azure Resource Manager traffic manager profile that he would like to add both web apps as endpoints.</span></span> <span data-ttu-id="01e8a-134">若要這樣做，我們必須先組合將現有的流量管理員設定檔的識別碼，我們需要訂用帳戶訂用帳戶識別碼、資源群組名稱和現有的流量管理員設定檔名稱。</span><span class="sxs-lookup"><span data-stu-id="01e8a-134">To do so, we first need to assemble the existing traffic manager profile id, we will need the subscription id, resource group name and the existing traffic manager profile name.</span></span>

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

<span data-ttu-id="01e8a-135">有了流量管理員識別碼之後，以下示範建立來源 Web 應用程式的複製到新的 Web 應用程式，同時將它們加入現有的流量管理員設定檔：</span><span class="sxs-lookup"><span data-stu-id="01e8a-135">After having the traffic manger id, the following demonstrates creating a clone of the source web app to a new web app while adding them to an existing Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a><span data-ttu-id="01e8a-136">目前的限制</span><span class="sxs-lookup"><span data-stu-id="01e8a-136">Current Restrictions</span></span>
<span data-ttu-id="01e8a-137">這項功能目前僅供預覽，我們正努力隨著時間加入新功能，以下是目前版本 App 複製已知的限制：</span><span class="sxs-lookup"><span data-stu-id="01e8a-137">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current version of app cloning:</span></span>

* <span data-ttu-id="01e8a-138">不會複製自動調整設定</span><span class="sxs-lookup"><span data-stu-id="01e8a-138">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="01e8a-139">不會複製備份排程設定</span><span class="sxs-lookup"><span data-stu-id="01e8a-139">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="01e8a-140">不會複製 VNET 設定</span><span class="sxs-lookup"><span data-stu-id="01e8a-140">VNET settings are not cloned</span></span>
* <span data-ttu-id="01e8a-141">未自動在目的地 Web 應用程式上設定 App Insights </span><span class="sxs-lookup"><span data-stu-id="01e8a-141">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="01e8a-142">不會複製簡單驗證設定</span><span class="sxs-lookup"><span data-stu-id="01e8a-142">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="01e8a-143">不會複製 Kudu 延伸模組</span><span class="sxs-lookup"><span data-stu-id="01e8a-143">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="01e8a-144">不會複製 TiP 規則</span><span class="sxs-lookup"><span data-stu-id="01e8a-144">TiP rules are not cloned</span></span>
* <span data-ttu-id="01e8a-145">不會複製資料庫內容</span><span class="sxs-lookup"><span data-stu-id="01e8a-145">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="01e8a-146">參考</span><span class="sxs-lookup"><span data-stu-id="01e8a-146">References</span></span>
* [<span data-ttu-id="01e8a-147">適用於 Azure Web 應用程式的 Azure Resource Manager 架構 PowerShell 命令</span><span class="sxs-lookup"><span data-stu-id="01e8a-147">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="01e8a-148">使用 Azure 入口網站複製 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="01e8a-148">Web App Cloning using Azure Portal</span></span>](app-service-web-app-cloning-portal.md)
* [<span data-ttu-id="01e8a-149">在 Azure App Service 中備份 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="01e8a-149">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="01e8a-150">Azure Resource Manager 的 Azure 流量管理員支援預覽</span><span class="sxs-lookup"><span data-stu-id="01e8a-150">Azure Resource Manager support for Azure Traffic Manager Preview</span></span>](../traffic-manager/traffic-manager-powershell-arm.md)
* [<span data-ttu-id="01e8a-151">App Service 環境簡介</span><span class="sxs-lookup"><span data-stu-id="01e8a-151">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="01e8a-152">搭配使用 Azure PowerShell 與 Azure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="01e8a-152">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)


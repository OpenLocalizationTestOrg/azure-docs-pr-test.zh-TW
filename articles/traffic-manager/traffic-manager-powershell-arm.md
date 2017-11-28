---
title: "aaaUsing PowerShell toomanage Traffic Manager Azure |Microsoft 文件"
description: "使用 PowerShell 透過 Azure Resource Manager 執行流量管理員"
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a><span data-ttu-id="4f32d-103">使用 PowerShell toomanage Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="4f32d-103">Using PowerShell toomanage Traffic Manager</span></span>

<span data-ttu-id="4f32d-104">Azure 資源管理員是在 Azure 中服務的 hello 慣用的管理介面。</span><span class="sxs-lookup"><span data-stu-id="4f32d-104">Azure Resource Manager is hello preferred management interface for services in Azure.</span></span> <span data-ttu-id="4f32d-105">您可以使用以 Azure Resource Manager 為基礎的 API 和工具來管理 Azure 流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="4f32d-105">Azure Traffic Manager profiles can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="resource-model"></a><span data-ttu-id="4f32d-106">資源模型</span><span class="sxs-lookup"><span data-stu-id="4f32d-106">Resource model</span></span>

<span data-ttu-id="4f32d-107">Azure 流量管理員使用名為「流量管理員設定檔」的設定集合進行設定。</span><span class="sxs-lookup"><span data-stu-id="4f32d-107">Azure Traffic Manager is configured using a collection of settings called a Traffic Manager profile.</span></span> <span data-ttu-id="4f32d-108">此設定檔包含 DNS 設定、 流量路由設定、 端點監視設定，以及一份服務端點 toowhich 流量路由傳送。</span><span class="sxs-lookup"><span data-stu-id="4f32d-108">This profile contains DNS settings, traffic routing settings, endpoint monitoring settings, and a list of service endpoints toowhich traffic is routed.</span></span>

<span data-ttu-id="4f32d-109">每個流量管理員設定檔都以 'TrafficManagerProfiles' 類型的資源表示。</span><span class="sxs-lookup"><span data-stu-id="4f32d-109">Each Traffic Manager profile is represented by a resource of type 'TrafficManagerProfiles'.</span></span> <span data-ttu-id="4f32d-110">在 hello REST API 層級，每個設定檔的 hello URI 如下所示：</span><span class="sxs-lookup"><span data-stu-id="4f32d-110">At hello REST API level, hello URI for each profile is as follows:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a><span data-ttu-id="4f32d-111">設定 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f32d-111">Setting up Azure PowerShell</span></span>

<span data-ttu-id="4f32d-112">這些指示使用 Microsoft Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="4f32d-112">These instructions use Microsoft Azure PowerShell.</span></span> <span data-ttu-id="4f32d-113">hello 下列文章說明如何 tooinstall 和設定 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="4f32d-113">hello following article explains how tooinstall and configure Azure PowerShell.</span></span>

* [<span data-ttu-id="4f32d-114">如何 tooinstall 和設定 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f32d-114">How tooinstall and configure Azure PowerShell</span></span>](/powershell/azure/overview)

<span data-ttu-id="4f32d-115">本文中的 hello 範例假設您有現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="4f32d-115">hello examples in this article assume that you have an existing resource group.</span></span> <span data-ttu-id="4f32d-116">您可以建立資源群組，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="4f32d-116">You can create a resource group using hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> <span data-ttu-id="4f32d-117">Azure Resource Manager 規定所有資源群組都要有位置。</span><span class="sxs-lookup"><span data-stu-id="4f32d-117">Azure Resource Manager requires that all resource groups have a location.</span></span> <span data-ttu-id="4f32d-118">Hello 預設會使用這個位置建立該資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="4f32d-118">This location is used as hello default for resources created in that resource group.</span></span> <span data-ttu-id="4f32d-119">不過，由於 Traffic Manager 設定檔的資源都是全域，不是地區，hello 所選擇的資源群組位置沒有任何影響有關 Azure Traffic Manager。</span><span class="sxs-lookup"><span data-stu-id="4f32d-119">However, since Traffic Manager profile resources are global, not regional, hello choice of resource group location has no impact on Azure Traffic Manager.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="4f32d-120">建立流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="4f32d-120">Create a Traffic Manager Profile</span></span>

<span data-ttu-id="4f32d-121">toocreate Traffic Manager 設定檔，使用 hello `New-AzureRmTrafficManagerProfile` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4f32d-121">toocreate a Traffic Manager profile, use hello `New-AzureRmTrafficManagerProfile` cmdlet:</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

<span data-ttu-id="4f32d-122">hello 下表描述 hello 參數：</span><span class="sxs-lookup"><span data-stu-id="4f32d-122">hello following table describes hello parameters:</span></span>

| <span data-ttu-id="4f32d-123">參數</span><span class="sxs-lookup"><span data-stu-id="4f32d-123">Parameter</span></span> | <span data-ttu-id="4f32d-124">說明</span><span class="sxs-lookup"><span data-stu-id="4f32d-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4f32d-125">名稱</span><span class="sxs-lookup"><span data-stu-id="4f32d-125">Name</span></span> |<span data-ttu-id="4f32d-126">hello hello Traffic Manager 設定檔資源的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="4f32d-126">hello resource name for hello Traffic Manager profile resource.</span></span> <span data-ttu-id="4f32d-127">中的設定檔 hello 相同資源群組必須具有唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="4f32d-127">Profiles in hello same resource group must have unique names.</span></span> <span data-ttu-id="4f32d-128">這個名稱是分開 hello 所使用的 DNS 查詢的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="4f32d-128">This name is separate from hello DNS name used for DNS queries.</span></span> |
| <span data-ttu-id="4f32d-129">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="4f32d-129">ResourceGroupName</span></span> |<span data-ttu-id="4f32d-130">hello hello 資源群組包含 hello 設定檔資源名稱。</span><span class="sxs-lookup"><span data-stu-id="4f32d-130">hello name of hello resource group containing hello profile resource.</span></span> |
| <span data-ttu-id="4f32d-131">TrafficRoutingMethod</span><span class="sxs-lookup"><span data-stu-id="4f32d-131">TrafficRoutingMethod</span></span> |<span data-ttu-id="4f32d-132">指定 hello 流量路由方法使用的 toodetermine 哪一個端點回應中傳回的 DNS 查詢。</span><span class="sxs-lookup"><span data-stu-id="4f32d-132">Specifies hello traffic-routing method used toodetermine which endpoint is returned in response a DNS query.</span></span> <span data-ttu-id="4f32d-133">可能的值為 'Performance'、'Weighted' 或 'Priority'。</span><span class="sxs-lookup"><span data-stu-id="4f32d-133">Possible values are 'Performance', 'Weighted' or 'Priority'.</span></span> |
| <span data-ttu-id="4f32d-134">RelativeDnsName</span><span class="sxs-lookup"><span data-stu-id="4f32d-134">RelativeDnsName</span></span> |<span data-ttu-id="4f32d-135">指定此 Traffic Manager 設定檔所提供的 hello DNS 名稱 hello 主機名稱部分。</span><span class="sxs-lookup"><span data-stu-id="4f32d-135">Specifies hello hostname portion of hello DNS name provided by this Traffic Manager profile.</span></span> <span data-ttu-id="4f32d-136">這個值會結合 hello Azure Traffic Manager tooform hello 完整的網域名稱 (FQDN) 的 hello 設定檔所使用的 DNS 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="4f32d-136">This value is combined with hello DNS domain name used by Azure Traffic Manager tooform hello fully qualified domain name (FQDN) of hello profile.</span></span> <span data-ttu-id="4f32d-137">例如，設定 'contoso' hello 值會變成 'contoso.trafficmanager.net。'</span><span class="sxs-lookup"><span data-stu-id="4f32d-137">For example, setting hello value of 'contoso' becomes 'contoso.trafficmanager.net.'</span></span> |
| <span data-ttu-id="4f32d-138">TTL</span><span class="sxs-lookup"><span data-stu-id="4f32d-138">TTL</span></span> |<span data-ttu-id="4f32d-139">指定 hello DNS--存留時間 (TTL)，以秒為單位。</span><span class="sxs-lookup"><span data-stu-id="4f32d-139">Specifies hello DNS Time-to-Live (TTL), in seconds.</span></span> <span data-ttu-id="4f32d-140">Hello 本機 DNS 解析程式和 DNS 用戶端，此 TTL 會通知此流量管理員設定檔的時間長度 toocache DNS 回應。</span><span class="sxs-lookup"><span data-stu-id="4f32d-140">This TTL informs hello Local DNS resolvers and DNS clients how long toocache DNS responses for this Traffic Manager profile.</span></span> |
| <span data-ttu-id="4f32d-141">MonitorProtocol</span><span class="sxs-lookup"><span data-stu-id="4f32d-141">MonitorProtocol</span></span> |<span data-ttu-id="4f32d-142">指定 hello 通訊協定 toouse toomonitor 端點健全狀況。</span><span class="sxs-lookup"><span data-stu-id="4f32d-142">Specifies hello protocol toouse toomonitor endpoint health.</span></span> <span data-ttu-id="4f32d-143">可能的值為 'HTTP' 和 'HTTPS'。</span><span class="sxs-lookup"><span data-stu-id="4f32d-143">Possible values are 'HTTP' and 'HTTPS'.</span></span> |
| <span data-ttu-id="4f32d-144">MonitorPort</span><span class="sxs-lookup"><span data-stu-id="4f32d-144">MonitorPort</span></span> |<span data-ttu-id="4f32d-145">指定 hello TCP 連接埠使用 toomonitor 端點健全狀況。</span><span class="sxs-lookup"><span data-stu-id="4f32d-145">Specifies hello TCP port used toomonitor endpoint health.</span></span> |
| <span data-ttu-id="4f32d-146">MonitorPath</span><span class="sxs-lookup"><span data-stu-id="4f32d-146">MonitorPath</span></span> |<span data-ttu-id="4f32d-147">指定 hello 路徑相對 toohello 端點網域名稱使用 tooprobe 端點健全狀態。</span><span class="sxs-lookup"><span data-stu-id="4f32d-147">Specifies hello path relative toohello endpoint domain name used tooprobe for endpoint health.</span></span> |

<span data-ttu-id="4f32d-148">hello cmdlet 在 Azure 中建立的 Traffic Manager 設定檔，並傳回對應的設定檔物件 tooPowerShell。</span><span class="sxs-lookup"><span data-stu-id="4f32d-148">hello cmdlet creates a Traffic Manager profile in Azure and returns a corresponding profile object tooPowerShell.</span></span> <span data-ttu-id="4f32d-149">此時，hello 設定檔不包含任何端點。</span><span class="sxs-lookup"><span data-stu-id="4f32d-149">At this point, hello profile does not contain any endpoints.</span></span> <span data-ttu-id="4f32d-150">如需新增端點 tooa Traffic Manager 設定檔的詳細資訊，請參閱[新增 Traffic Manager 端點](#adding-traffic-manager-endpoints)。</span><span class="sxs-lookup"><span data-stu-id="4f32d-150">For more information about adding endpoints tooa Traffic Manager profile, see [Adding Traffic Manager Endpoints](#adding-traffic-manager-endpoints).</span></span>

## <a name="get-a-traffic-manager-profile"></a><span data-ttu-id="4f32d-151">取得流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="4f32d-151">Get a Traffic Manager Profile</span></span>

<span data-ttu-id="4f32d-152">tooretrieve 現有的 Traffic Manager 設定檔物件，使用 hello `Get-AzureRmTrafficManagerProfle` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4f32d-152">tooretrieve an existing Traffic Manager profile object, use hello `Get-AzureRmTrafficManagerProfle` cmdlet:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="4f32d-153">此 Cmdlet 會傳回流量管理員設定檔物件。</span><span class="sxs-lookup"><span data-stu-id="4f32d-153">This cmdlet returns a Traffic Manager profile object.</span></span>

## <a name="update-a-traffic-manager-profile"></a><span data-ttu-id="4f32d-154">更新流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="4f32d-154">Update a Traffic Manager Profile</span></span>

<span data-ttu-id="4f32d-155">修改流量管理員設定檔需要 3 個步驟︰</span><span class="sxs-lookup"><span data-stu-id="4f32d-155">Modifying Traffic Manager profiles follows a 3-step process:</span></span>

1. <span data-ttu-id="4f32d-156">擷取 hello 設定檔使用`Get-AzureRmTrafficManagerProfile`或使用 hello 設定檔所傳回`New-AzureRmTrafficManagerProfile`。</span><span class="sxs-lookup"><span data-stu-id="4f32d-156">Retrieve hello profile using `Get-AzureRmTrafficManagerProfile` or use hello profile returned by `New-AzureRmTrafficManagerProfile`.</span></span>
2. <span data-ttu-id="4f32d-157">修改 hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="4f32d-157">Modify hello profile.</span></span> <span data-ttu-id="4f32d-158">您可以新增和移除端點，也可以變更端點或設定檔參數。</span><span class="sxs-lookup"><span data-stu-id="4f32d-158">You can add and remove endpoints or change endpoint or profile parameters.</span></span> <span data-ttu-id="4f32d-159">這些變更是離線作業。</span><span class="sxs-lookup"><span data-stu-id="4f32d-159">These changes are off-line operations.</span></span> <span data-ttu-id="4f32d-160">您只變更代表 hello 設定檔的記憶體中的 hello 本機物件。</span><span class="sxs-lookup"><span data-stu-id="4f32d-160">You are only changing hello local object in memory that represents hello profile.</span></span>
3. <span data-ttu-id="4f32d-161">認可您的變更使用 hello `Set-AzureRmTrafficManagerProfile` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4f32d-161">Commit your changes using hello `Set-AzureRmTrafficManagerProfile` cmdlet.</span></span>

<span data-ttu-id="4f32d-162">除非 RelativeDnsName hello 設定檔可以變更所有設定檔屬性。</span><span class="sxs-lookup"><span data-stu-id="4f32d-162">All profile properties can be changed except hello profile's RelativeDnsName.</span></span> <span data-ttu-id="4f32d-163">toochange hello RelativeDnsName，您必須刪除設定檔和新的設定檔，以新名稱。</span><span class="sxs-lookup"><span data-stu-id="4f32d-163">toochange hello RelativeDnsName, you must delete profile and a new profile with a new name.</span></span>

<span data-ttu-id="4f32d-164">hello 下列範例將示範如何 toochange hello 設定檔的 TTL:</span><span class="sxs-lookup"><span data-stu-id="4f32d-164">hello following example demonstrates how toochange hello profile's TTL:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="4f32d-165">流量管理員端點有三種類型：</span><span class="sxs-lookup"><span data-stu-id="4f32d-165">There are three types of Traffic Manager endpoints:</span></span>

1. <span data-ttu-id="4f32d-166">**Azure 端點**是 Azure 中託管的服務。</span><span class="sxs-lookup"><span data-stu-id="4f32d-166">**Azure endpoints** are services hosted in Azure</span></span>
2. <span data-ttu-id="4f32d-167">**外部端點**是 Azure 外部託管的服務。</span><span class="sxs-lookup"><span data-stu-id="4f32d-167">**External endpoints** are services hosted outside of Azure</span></span>
3. <span data-ttu-id="4f32d-168">**巢狀端點**Traffic Manager 設定檔使用的 tooconstruct 巢狀階層。</span><span class="sxs-lookup"><span data-stu-id="4f32d-168">**Nested endpoints** are used tooconstruct nested hierarchies of Traffic Manager profiles.</span></span> <span data-ttu-id="4f32d-169">巢狀端點可讓複雜的應用程式使用進階的流量路由設定。</span><span class="sxs-lookup"><span data-stu-id="4f32d-169">Nested endpoints enable advanced traffic-routing configurations for complex applications.</span></span>

<span data-ttu-id="4f32d-170">不論是這三種端點中的哪一種，您都可以透過兩種方式來新增端點：</span><span class="sxs-lookup"><span data-stu-id="4f32d-170">In all three cases, endpoints can be added in two ways:</span></span>

1. <span data-ttu-id="4f32d-171">使用先前所述的 3 步驟程序。</span><span class="sxs-lookup"><span data-stu-id="4f32d-171">Using a 3-step process described previously.</span></span> <span data-ttu-id="4f32d-172">這個方法的 hello 優點是可以在單一更新進行數個端點變更。</span><span class="sxs-lookup"><span data-stu-id="4f32d-172">hello advantage of this method is that several endpoint changes can be made in a single update.</span></span>
2. <span data-ttu-id="4f32d-173">使用 hello 新增 AzureRmTrafficManagerEndpoint cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4f32d-173">Using hello New-AzureRmTrafficManagerEndpoint cmdlet.</span></span> <span data-ttu-id="4f32d-174">這個 cmdlet 會在單一作業中加入端點 tooan 現有流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="4f32d-174">This cmdlet adds an endpoint tooan existing Traffic Manager profile in a single operation.</span></span>

## <a name="adding-azure-endpoints"></a><span data-ttu-id="4f32d-175">新增 Azure 端點</span><span class="sxs-lookup"><span data-stu-id="4f32d-175">Adding Azure Endpoints</span></span>

<span data-ttu-id="4f32d-176">Azure 端點會參考 Azure 中託管的服務。</span><span class="sxs-lookup"><span data-stu-id="4f32d-176">Azure endpoints reference services hosted in Azure.</span></span> <span data-ttu-id="4f32d-177">支援兩種 Azure 端點：</span><span class="sxs-lookup"><span data-stu-id="4f32d-177">Two types of Azure endpoints are supported:</span></span>

1. <span data-ttu-id="4f32d-178">Azure Web Apps </span><span class="sxs-lookup"><span data-stu-id="4f32d-178">Azure Web Apps</span></span>
2. <span data-ttu-id="4f32d-179">Azure PublicIpAddress 資源 （這可以是附加的 tooa 負載平衡器或虛擬機器 NIC）。</span><span class="sxs-lookup"><span data-stu-id="4f32d-179">Azure PublicIpAddress resources (which can be attached tooa load-balancer or a virtual machine NIC).</span></span> <span data-ttu-id="4f32d-180">hello PublicIpAddress 必須指派 toobe 使用 Traffic Manager 中的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="4f32d-180">hello PublicIpAddress must have a DNS name assigned toobe used in Traffic Manager.</span></span>

<span data-ttu-id="4f32d-181">不論是上述哪一種，都必須注意以下事項：</span><span class="sxs-lookup"><span data-stu-id="4f32d-181">In each case:</span></span>

* <span data-ttu-id="4f32d-182">hello 服務使用 hello 'targetResourceId' 參數所指定`Add-AzureRmTrafficManagerEndpointConfig`或`New-AzureRmTrafficManagerEndpoint`。</span><span class="sxs-lookup"><span data-stu-id="4f32d-182">hello service is specified using hello 'targetResourceId' parameter of `Add-AzureRmTrafficManagerEndpointConfig` or `New-AzureRmTrafficManagerEndpoint`.</span></span>
* <span data-ttu-id="4f32d-183">hello 'Target' 和 'EndpointLocation' 由隱含 hello TargetResourceId。</span><span class="sxs-lookup"><span data-stu-id="4f32d-183">hello 'Target' and 'EndpointLocation' are implied by hello TargetResourceId.</span></span>
* <span data-ttu-id="4f32d-184">指定 hello 'Weight' 是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="4f32d-184">Specifying hello 'Weight' is optional.</span></span> <span data-ttu-id="4f32d-185">加權時，才會使用 hello 設定檔是否設定的 toouse hello '加權' 流量路由方法。</span><span class="sxs-lookup"><span data-stu-id="4f32d-185">Weights are only used if hello profile is configured toouse hello 'Weighted' traffic-routing method.</span></span> <span data-ttu-id="4f32d-186">否則會予以忽略。</span><span class="sxs-lookup"><span data-stu-id="4f32d-186">Otherwise, they are ignored.</span></span> <span data-ttu-id="4f32d-187">如果指定，hello 值必須介於 1 到 1000年之間的數字。</span><span class="sxs-lookup"><span data-stu-id="4f32d-187">If specified, hello value must be a number between 1 and 1000.</span></span> <span data-ttu-id="4f32d-188">hello 預設值為 '1'。</span><span class="sxs-lookup"><span data-stu-id="4f32d-188">hello default value is '1'.</span></span>
* <span data-ttu-id="4f32d-189">指定 hello 'Priority' 是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="4f32d-189">Specifying hello 'Priority' is optional.</span></span> <span data-ttu-id="4f32d-190">Hello 設定檔是否設定的 toouse hello 'Priority' 流量路由方法時，才會使用優先順序。</span><span class="sxs-lookup"><span data-stu-id="4f32d-190">Priorities are only used if hello profile is configured toouse hello 'Priority' traffic-routing method.</span></span> <span data-ttu-id="4f32d-191">否則會予以忽略。</span><span class="sxs-lookup"><span data-stu-id="4f32d-191">Otherwise, they are ignored.</span></span> <span data-ttu-id="4f32d-192">有效值從 1 too1000 具有較低的值表示較高的優先順序。</span><span class="sxs-lookup"><span data-stu-id="4f32d-192">Valid values are from 1 too1000 with lower values indicating a higher priority.</span></span> <span data-ttu-id="4f32d-193">如果對某個端點指定值，則所有端點也都必須進行指定。</span><span class="sxs-lookup"><span data-stu-id="4f32d-193">If specified for one endpoint, they must be specified for all endpoints.</span></span> <span data-ttu-id="4f32d-194">如果省略，開始從 '1' 的預設值會套用 hello hello 端點所列的順序。</span><span class="sxs-lookup"><span data-stu-id="4f32d-194">If omitted, default values starting from '1' are applied in hello order that hello endpoints are listed.</span></span>

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a><span data-ttu-id="4f32d-195">範例 1︰使用 `Add-AzureRmTrafficManagerEndpointConfig` 新增 Web 應用程式端點</span><span class="sxs-lookup"><span data-stu-id="4f32d-195">Example 1: Adding Web App endpoints using `Add-AzureRmTrafficManagerEndpointConfig`</span></span>

<span data-ttu-id="4f32d-196">在此範例中，我們建立 Traffic Manager 設定檔，並加入兩個 Web 應用程式端點使用 hello `Add-AzureRmTrafficManagerEndpointConfig` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4f32d-196">In this example, we create a Traffic Manager profile and add two Web App endpoints using hello `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="4f32d-197">範例 2︰使用 `New-AzureRmTrafficManagerEndpoint` 新增 publicIpAddress 端點</span><span class="sxs-lookup"><span data-stu-id="4f32d-197">Example 2: Adding a publicIpAddress endpoint using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="4f32d-198">在此範例中，公用 IP 位址資源加入 toohello Traffic Manager 設定檔。</span><span class="sxs-lookup"><span data-stu-id="4f32d-198">In this example, a public IP address resource is added toohello Traffic Manager profile.</span></span> <span data-ttu-id="4f32d-199">hello 公用 IP 位址都必須有 DNS 名稱設定，而且可以繫結任一 toohello NIC 的 VM 或 tooa 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="4f32d-199">hello public IP address must have a DNS name configured, and can be bound either toohello NIC of a VM or tooa load balancer.</span></span>

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a><span data-ttu-id="4f32d-200">新增外部端點</span><span class="sxs-lookup"><span data-stu-id="4f32d-200">Adding External Endpoints</span></span>

<span data-ttu-id="4f32d-201">流量管理員會使用外部端點 toodirect 流量 tooservices Azure 外部所裝載。</span><span class="sxs-lookup"><span data-stu-id="4f32d-201">Traffic Manager uses external endpoints toodirect traffic tooservices hosted outside of Azure.</span></span> <span data-ttu-id="4f32d-202">如同 Azure 端點一樣，使用 `Add-AzureRmTrafficManagerEndpointConfig` 再接著使用 `Set-AzureRmTrafficManagerProfile`，或使用 `New-AzureRMTrafficManagerEndpoint`，都可以新增外部端點。</span><span class="sxs-lookup"><span data-stu-id="4f32d-202">As with Azure endpoints, external endpoints can be added either using `Add-AzureRmTrafficManagerEndpointConfig` followed by `Set-AzureRmTrafficManagerProfile`, or `New-AzureRMTrafficManagerEndpoint`.</span></span>

<span data-ttu-id="4f32d-203">指定外部端點時：</span><span class="sxs-lookup"><span data-stu-id="4f32d-203">When specifying external endpoints:</span></span>

* <span data-ttu-id="4f32d-204">必須使用 hello 'Target' 參數指定 hello 端點網域名稱</span><span class="sxs-lookup"><span data-stu-id="4f32d-204">hello endpoint domain name must be specified using hello 'Target' parameter</span></span>
* <span data-ttu-id="4f32d-205">如果使用 「 效能 」 流量路由方法 hello，hello 'EndpointLocation' 需要。</span><span class="sxs-lookup"><span data-stu-id="4f32d-205">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="4f32d-206">否則為選擇性。</span><span class="sxs-lookup"><span data-stu-id="4f32d-206">Otherwise it is optional.</span></span> <span data-ttu-id="4f32d-207">hello 值必須是[有效的 Azure 區域名稱](https://azure.microsoft.com/regions/)。</span><span class="sxs-lookup"><span data-stu-id="4f32d-207">hello value must be a [valid Azure region name](https://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="4f32d-208">hello '加權'，'Priority' 是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="4f32d-208">hello 'Weight' and 'Priority' are optional.</span></span>

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="4f32d-209">範例 1︰使用 `Add-AzureRmTrafficManagerEndpointConfig` 和 `Set-AzureRmTrafficManagerProfile` 新增外部端點</span><span class="sxs-lookup"><span data-stu-id="4f32d-209">Example 1: Adding external endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="4f32d-210">在此範例中，我們可以建立 Traffic Manager 設定檔、 新增兩個外部端點，以及認可 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="4f32d-210">In this example, we create a Traffic Manager profile, add two external endpoints, and commit hello changes.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="4f32d-211">範例 2︰使用 `New-AzureRmTrafficManagerEndpoint` 新增外部端點</span><span class="sxs-lookup"><span data-stu-id="4f32d-211">Example 2: Adding external endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="4f32d-212">在此範例中，我們加入外部端點 tooan 現有的設定檔。</span><span class="sxs-lookup"><span data-stu-id="4f32d-212">In this example, we add an external endpoint tooan existing profile.</span></span> <span data-ttu-id="4f32d-213">hello 設定檔來指定 hello 設定檔和資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="4f32d-213">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a><span data-ttu-id="4f32d-214">新增「巢狀」端點</span><span class="sxs-lookup"><span data-stu-id="4f32d-214">Adding 'Nested' endpoints</span></span>

<span data-ttu-id="4f32d-215">每個「流量管理員」設定檔皆指定一個流量路由方法。</span><span class="sxs-lookup"><span data-stu-id="4f32d-215">Each Traffic Manager profile specifies a single traffic-routing method.</span></span> <span data-ttu-id="4f32d-216">不過，有一些需要更複雜的流量路由比 hello 路由單一 Traffic Manager 設定檔所提供的案例。</span><span class="sxs-lookup"><span data-stu-id="4f32d-216">However, there are scenarios that require more sophisticated traffic routing than hello routing provided by a single Traffic Manager profile.</span></span> <span data-ttu-id="4f32d-217">您可以巢狀多個流量路由方法的 Traffic Manager 設定檔 toocombine hello 優點。</span><span class="sxs-lookup"><span data-stu-id="4f32d-217">You can nest Traffic Manager profiles toocombine hello benefits of more than one traffic-routing method.</span></span> <span data-ttu-id="4f32d-218">巢狀設定檔可讓您 toooverride hello 預設 Traffic Manager 行為 toosupport 較大和更複雜的應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="4f32d-218">Nested profiles allow you toooverride hello default Traffic Manager behavior toosupport larger and more complex application deployments.</span></span> <span data-ttu-id="4f32d-219">如需詳細範例，請參閱[巢狀流量管理員設定檔](traffic-manager-nested-profiles.md)。</span><span class="sxs-lookup"><span data-stu-id="4f32d-219">For more detailed examples, see [Nested Traffic Manager profiles](traffic-manager-nested-profiles.md).</span></span>

<span data-ttu-id="4f32d-220">巢狀的端點是在 hello 父系設定檔，使用特定端點的型別、 'NestedEndpoints' 設定。</span><span class="sxs-lookup"><span data-stu-id="4f32d-220">Nested endpoints are configured at hello parent profile, using a specific endpoint type, 'NestedEndpoints'.</span></span> <span data-ttu-id="4f32d-221">指定巢狀端點時︰</span><span class="sxs-lookup"><span data-stu-id="4f32d-221">When specifying nested endpoints:</span></span>

* <span data-ttu-id="4f32d-222">必須使用 hello 'targetResourceId' 參數指定 hello 端點</span><span class="sxs-lookup"><span data-stu-id="4f32d-222">hello endpoint must be specified using hello 'targetResourceId' parameter</span></span>
* <span data-ttu-id="4f32d-223">如果使用 「 效能 」 流量路由方法 hello，hello 'EndpointLocation' 需要。</span><span class="sxs-lookup"><span data-stu-id="4f32d-223">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="4f32d-224">否則為選擇性。</span><span class="sxs-lookup"><span data-stu-id="4f32d-224">Otherwise it is optional.</span></span> <span data-ttu-id="4f32d-225">hello 值必須是[有效的 Azure 區域名稱](http://azure.microsoft.com/regions/)。</span><span class="sxs-lookup"><span data-stu-id="4f32d-225">hello value must be a [valid Azure region name](http://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="4f32d-226">hello '加權'，'Priority' 是選擇性的與 Azure 的端點。</span><span class="sxs-lookup"><span data-stu-id="4f32d-226">hello 'Weight' and 'Priority' are optional, as for Azure endpoints.</span></span>
* <span data-ttu-id="4f32d-227">hello 'MinChildEndpoints' 參數是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="4f32d-227">hello 'MinChildEndpoints' parameter is optional.</span></span> <span data-ttu-id="4f32d-228">hello 預設值為 '1'。</span><span class="sxs-lookup"><span data-stu-id="4f32d-228">hello default value is '1'.</span></span> <span data-ttu-id="4f32d-229">Hello 可用的端點數目低於此臨界值時，如果 hello 父系設定檔會考慮 hello 子系的設定檔 '降低'，且 diverts 流量 toohello hello 父系設定檔中的其他端點。</span><span class="sxs-lookup"><span data-stu-id="4f32d-229">If hello number of available endpoints falls below this threshold, hello parent profile considers hello child profile 'degraded' and diverts traffic toohello other endpoints in hello parent profile.</span></span>

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="4f32d-230">範例 1︰使用 `Add-AzureRmTrafficManagerEndpointConfig` 和 `Set-AzureRmTrafficManagerProfile` 新增巢狀端點</span><span class="sxs-lookup"><span data-stu-id="4f32d-230">Example 1: Adding nested endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="4f32d-231">在此範例中，我們可以建立新的 Traffic Manager 子系和父系設定檔、 新增 hello 子系為巢狀的端點 toohello 父代，以及認可 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="4f32d-231">In this example, we create new Traffic Manager child and parent profiles, add hello child as a nested endpoint toohello parent, and commit hello changes.</span></span>

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="4f32d-232">為求簡潔，在此範例中，我們沒有新增任何其他端點 toohello 子系或父系設定檔。</span><span class="sxs-lookup"><span data-stu-id="4f32d-232">For brevity in this example, we did not add any other endpoints toohello child or parent profiles.</span></span>

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="4f32d-233">範例 2︰使用 `New-AzureRmTrafficManagerEndpoint` 新增巢狀端點</span><span class="sxs-lookup"><span data-stu-id="4f32d-233">Example 2: Adding nested endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="4f32d-234">在此範例中，我們會加入現有的子系設定檔為巢狀的端點 tooan 現有父系設定檔。</span><span class="sxs-lookup"><span data-stu-id="4f32d-234">In this example, we add an existing child profile as a nested endpoint tooan existing parent profile.</span></span> <span data-ttu-id="4f32d-235">hello 設定檔來指定 hello 設定檔和資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="4f32d-235">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a><span data-ttu-id="4f32d-236">更新流量管理員端點</span><span class="sxs-lookup"><span data-stu-id="4f32d-236">Update a Traffic Manager Endpoint</span></span>

<span data-ttu-id="4f32d-237">有兩種方式 tooupdate 現有流量管理員端點：</span><span class="sxs-lookup"><span data-stu-id="4f32d-237">There are two ways tooupdate an existing Traffic Manager endpoint:</span></span>

1. <span data-ttu-id="4f32d-238">取得 hello Traffic Manager 設定檔使用`Get-AzureRmTrafficManagerProfile`、 更新 hello 設定檔中的 hello 端點內容，以及認可 hello 變更使用`Set-AzureRmTrafficManagerProfile`。</span><span class="sxs-lookup"><span data-stu-id="4f32d-238">Get hello Traffic Manager profile using `Get-AzureRmTrafficManagerProfile`, update hello endpoint properties within hello profile, and commit hello changes using `Set-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="4f32d-239">這個方法沒有 hello 優點是能夠 tooupdate 在單一作業中的多個端點。</span><span class="sxs-lookup"><span data-stu-id="4f32d-239">This method has hello advantage of being able tooupdate more than one endpoint in a single operation.</span></span>
2. <span data-ttu-id="4f32d-240">取得 hello Traffic Manager 端點使用`Get-AzureRmTrafficManagerEndpoint`、 更新 hello 端點內容，以及認可使用的 hello 變更`Set-AzureRmTrafficManagerEndpoint`。</span><span class="sxs-lookup"><span data-stu-id="4f32d-240">Get hello Traffic Manager endpoint using `Get-AzureRmTrafficManagerEndpoint`, update hello endpoint properties, and commit hello changes using `Set-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="4f32d-241">這個方法是比較簡單，，因為它不需要對 hello 設定檔中的 hello 端點陣列進行索引。</span><span class="sxs-lookup"><span data-stu-id="4f32d-241">This method is simpler, since it does not require indexing into hello Endpoints array in hello profile.</span></span>

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="4f32d-242">範例 1︰使用 `Get-AzureRmTrafficManagerProfile` 和 `Set-AzureRmTrafficManagerProfile` 更新端點</span><span class="sxs-lookup"><span data-stu-id="4f32d-242">Example 1: Updating endpoints using `Get-AzureRmTrafficManagerProfile` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="4f32d-243">在此範例中，我們會修改現有的設定檔中的兩個端點上的 hello 優先順序。</span><span class="sxs-lookup"><span data-stu-id="4f32d-243">In this example, we modify hello priority on two endpoints within an existing profile.</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a><span data-ttu-id="4f32d-244">範例 2︰使用 `Get-AzureRmTrafficManagerEndpoint` 和 `Set-AzureRmTrafficManagerEndpoint` 更新端點</span><span class="sxs-lookup"><span data-stu-id="4f32d-244">Example 2: Updating an endpoint using `Get-AzureRmTrafficManagerEndpoint` and `Set-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="4f32d-245">在此範例中，我們會修改 hello 加權中現有的設定檔的單一端點。</span><span class="sxs-lookup"><span data-stu-id="4f32d-245">In this example, we modify hello weight of a single endpoint in an existing profile.</span></span>

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a><span data-ttu-id="4f32d-246">啟用和停用端點和設定檔</span><span class="sxs-lookup"><span data-stu-id="4f32d-246">Enabling and Disabling Endpoints and Profiles</span></span>

<span data-ttu-id="4f32d-247">Traffic Manager 可讓個別端點 toobe 啟用和停用，以及允許啟用及停用整個設定檔。</span><span class="sxs-lookup"><span data-stu-id="4f32d-247">Traffic Manager allows individual endpoints toobe enabled and disabled, as well as allowing enabling and disabling of entire profiles.</span></span>
<span data-ttu-id="4f32d-248">取得/更新/設定 hello 端點或設定檔的資源，就可以進行這些變更。</span><span class="sxs-lookup"><span data-stu-id="4f32d-248">These changes can be made by getting/updating/setting hello endpoint or profile resources.</span></span> <span data-ttu-id="4f32d-249">toostreamline 這些常見的作業，它們也支援透過專用 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4f32d-249">toostreamline these common operations, they are also supported via dedicated cmdlets.</span></span>

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a><span data-ttu-id="4f32d-250">範例 1：啟用和停用流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="4f32d-250">Example 1: Enabling and disabling a Traffic Manager profile</span></span>

<span data-ttu-id="4f32d-251">tooenable Traffic Manager 設定檔，使用`Enable-AzureRmTrafficManagerProfile`。</span><span class="sxs-lookup"><span data-stu-id="4f32d-251">tooenable a Traffic Manager profile, use `Enable-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="4f32d-252">可以使用設定檔物件，指定 hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="4f32d-252">hello profile can be specified using a profile object.</span></span> <span data-ttu-id="4f32d-253">hello 設定檔物件可以傳遞透過 hello 管線或使用 hello '-TrafficManagerProfile' 參數。</span><span class="sxs-lookup"><span data-stu-id="4f32d-253">hello profile object can be passed via hello pipeline or by using hello '-TrafficManagerProfile' parameter.</span></span> <span data-ttu-id="4f32d-254">在此範例中，我們會藉由 hello 設定檔和資源群組名稱指定 hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="4f32d-254">In this example, we specify hello profile by hello profile and resource group name.</span></span>

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="4f32d-255">toodisable Traffic Manager 設定檔：</span><span class="sxs-lookup"><span data-stu-id="4f32d-255">toodisable a Traffic Manager profile:</span></span>

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="4f32d-256">hello 停用 AzureRmTrafficManagerProfile cmdlet 會提示確認。</span><span class="sxs-lookup"><span data-stu-id="4f32d-256">hello Disable-AzureRmTrafficManagerProfile cmdlet prompts for confirmation.</span></span> <span data-ttu-id="4f32d-257">此提示可使用，以歸併 hello '-Force' 參數。</span><span class="sxs-lookup"><span data-stu-id="4f32d-257">This prompt can be suppressed using hello '-Force' parameter.</span></span>

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a><span data-ttu-id="4f32d-258">範例 2：啟用和停用流量管理員端點</span><span class="sxs-lookup"><span data-stu-id="4f32d-258">Example 2: Enabling and disabling a Traffic Manager endpoint</span></span>

<span data-ttu-id="4f32d-259">tooenable Traffic Manager 端點使用`Enable-AzureRmTrafficManagerEndpoint`。</span><span class="sxs-lookup"><span data-stu-id="4f32d-259">tooenable a Traffic Manager endpoint, use `Enable-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="4f32d-260">有兩種方式 toospecify hello 端點</span><span class="sxs-lookup"><span data-stu-id="4f32d-260">There are two ways toospecify hello endpoint</span></span>

1. <span data-ttu-id="4f32d-261">使用透過 hello 管線傳遞 TrafficManagerEndpoint 物件，或使用 hello '-TrafficManagerEndpoint' 參數</span><span class="sxs-lookup"><span data-stu-id="4f32d-261">Using a TrafficManagerEndpoint object passed via hello pipeline or using hello '-TrafficManagerEndpoint' parameter</span></span>
2. <span data-ttu-id="4f32d-262">使用 hello 端點名稱、 端點類型、 設定檔名稱和資源群組名稱：</span><span class="sxs-lookup"><span data-stu-id="4f32d-262">Using hello endpoint name, endpoint type, profile name, and resource group name:</span></span>

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="4f32d-263">同樣地，toodisable 流量管理員端點：</span><span class="sxs-lookup"><span data-stu-id="4f32d-263">Similarly, toodisable a Traffic Manager endpoint:</span></span>

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

<span data-ttu-id="4f32d-264">如同`Disable-AzureRmTrafficManagerProfile`，hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet 會提示確認。</span><span class="sxs-lookup"><span data-stu-id="4f32d-264">As with `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet prompts for confirmation.</span></span> <span data-ttu-id="4f32d-265">此提示可使用，以歸併 hello '-Force' 參數。</span><span class="sxs-lookup"><span data-stu-id="4f32d-265">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-endpoint"></a><span data-ttu-id="4f32d-266">停用流量管理員端點</span><span class="sxs-lookup"><span data-stu-id="4f32d-266">Delete a Traffic Manager Endpoint</span></span>

<span data-ttu-id="4f32d-267">tooremove 個別的端點，請使用 hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4f32d-267">tooremove individual endpoints, use hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span></span>

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="4f32d-268">這個 Cmdlet 會提示您確認。</span><span class="sxs-lookup"><span data-stu-id="4f32d-268">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="4f32d-269">此提示可使用，以歸併 hello '-Force' 參數。</span><span class="sxs-lookup"><span data-stu-id="4f32d-269">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-profile"></a><span data-ttu-id="4f32d-270">刪除流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="4f32d-270">Delete a Traffic Manager Profile</span></span>

<span data-ttu-id="4f32d-271">toodelete Traffic Manager 設定檔，使用 hello`Remove-AzureRmTrafficManagerProfile`指令程式，指定 hello 設定檔和資源群組名稱：</span><span class="sxs-lookup"><span data-stu-id="4f32d-271">toodelete a Traffic Manager profile, use hello `Remove-AzureRmTrafficManagerProfile` cmdlet, specifying hello profile and resource group names:</span></span>

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

<span data-ttu-id="4f32d-272">這個 Cmdlet 會提示您確認。</span><span class="sxs-lookup"><span data-stu-id="4f32d-272">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="4f32d-273">此提示可使用，以歸併 hello '-Force' 參數。</span><span class="sxs-lookup"><span data-stu-id="4f32d-273">This prompt can be suppressed using hello '-Force' parameter.</span></span>

<span data-ttu-id="4f32d-274">刪除 hello 設定檔 toobe 也可以使用設定檔物件來指定：</span><span class="sxs-lookup"><span data-stu-id="4f32d-274">hello profile toobe deleted can also be specified using a profile object:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

<span data-ttu-id="4f32d-275">也可輸送以下順序：</span><span class="sxs-lookup"><span data-stu-id="4f32d-275">This sequence can also be piped:</span></span>

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a><span data-ttu-id="4f32d-276">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4f32d-276">Next steps</span></span>

[<span data-ttu-id="4f32d-277">流量管理員監視</span><span class="sxs-lookup"><span data-stu-id="4f32d-277">Traffic Manager monitoring</span></span>](traffic-manager-monitoring.md)

[<span data-ttu-id="4f32d-278">流量管理員的效能考量</span><span class="sxs-lookup"><span data-stu-id="4f32d-278">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)

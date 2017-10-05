---
title: "使用 PowerShell 管理 Azure CDN | Microsoft Docs"
description: "了解如何使用 Azure PowerShell Cmdlet 管理 Azure CDN。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: fb6f57a5-6e26-4847-8fd9-b51fb05a79eb
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5bd2eed7b34cafa43e8f38279890405d4ae55568
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-cdn-with-powershell"></a><span data-ttu-id="71bd8-103">使用 PowerShell 管理 Azure CDN</span><span class="sxs-lookup"><span data-stu-id="71bd8-103">Manage Azure CDN with PowerShell</span></span>
<span data-ttu-id="71bd8-104">PowerShell 提供一種最具彈性的方法，以管理您的 Azure CDN 設定檔和端點。</span><span class="sxs-lookup"><span data-stu-id="71bd8-104">PowerShell provides one of the most flexible methods to manage your Azure CDN profiles and endpoints.</span></span>  <span data-ttu-id="71bd8-105">您可以用互動方式使用 PowerShell 或透過撰寫指令碼來自動進行管理工作。</span><span class="sxs-lookup"><span data-stu-id="71bd8-105">You can use PowerShell interactively or by writing scripts to automate management tasks.</span></span>  <span data-ttu-id="71bd8-106">本教學課程會示範數個您可透過 PowerShell 完成的最常見工作，以管理 Azure CDN 設定檔和端點。</span><span class="sxs-lookup"><span data-stu-id="71bd8-106">This tutorial demonstrates several of the most common tasks you can accomplish with PowerShell to manage your Azure CDN profiles and endpoints.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71bd8-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="71bd8-107">Prerequisites</span></span>
<span data-ttu-id="71bd8-108">若要使用 PowerShell 管理 Azure CDN 設定檔和端點，您必須安裝 Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="71bd8-108">To use PowerShell to manage your Azure CDN profiles and endpoints, you must have the Azure PowerShell module installed.</span></span>  <span data-ttu-id="71bd8-109">若要了解如何安裝 Azure PowerShell 及使用 `Login-AzureRmAccount` Cmdlet 連接至 Azure，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="71bd8-109">To learn how to install Azure PowerShell and connect to Azure using the `Login-AzureRmAccount` cmdlet, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71bd8-110">您必須先使用 `Login-AzureRmAccount` 登入，才能執行 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="71bd8-110">You must log in with `Login-AzureRmAccount` before you can execute Azure PowerShell cmdlets.</span></span>
> 
> 

## <a name="listing-the-azure-cdn-cmdlets"></a><span data-ttu-id="71bd8-111">列出 Azure CDN Cmdlet</span><span class="sxs-lookup"><span data-stu-id="71bd8-111">Listing the Azure CDN cmdlets</span></span>
<span data-ttu-id="71bd8-112">您可以使用 `Get-Command` Cmdlet 列出所有的 Azure CDN Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="71bd8-112">You can list all the Azure CDN cmdlets using the `Get-Command` cmdlet.</span></span>

```text
PS C:\> Get-Command -Module AzureRM.Cdn

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Get-AzureRmCdnCustomDomain                         2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnEndpointNameAvailability             2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnOrigin                               2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnProfileSsoUrl                        2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnCustomDomain                         2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Publish-AzureRmCdnEndpointContent                  2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnCustomDomain                      2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnEndpoint                          2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnProfile                           2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnOrigin                               2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Start-AzureRmCdnEndpoint                           2.0.0      AzureRm.Cdn
Cmdlet          Stop-AzureRmCdnEndpoint                            2.0.0      AzureRm.Cdn
Cmdlet          Test-AzureRmCdnCustomDomain                        2.0.0      AzureRm.Cdn
Cmdlet          Unpublish-AzureRmCdnEndpointContent                2.0.0      AzureRm.Cdn
```

## <a name="getting-help"></a><span data-ttu-id="71bd8-113">取得說明</span><span class="sxs-lookup"><span data-stu-id="71bd8-113">Getting help</span></span>
<span data-ttu-id="71bd8-114">您可以使用 `Get-Help` Cmdlet 取得這些 Cmdlet 的說明。</span><span class="sxs-lookup"><span data-stu-id="71bd8-114">You can get help with any of these cmdlets using the `Get-Help` cmdlet.</span></span>  <span data-ttu-id="71bd8-115">`Get-Help` 提供使用方式與語法，並選擇性地顯示範例。</span><span class="sxs-lookup"><span data-stu-id="71bd8-115">`Get-Help` provides usage and syntax, and optionally shows examples.</span></span>

```text
PS C:\> Get-Help Get-AzureRmCdnProfile

NAME
    Get-AzureRmCdnProfile

SYNOPSIS
    Gets an Azure CDN profile.


SYNTAX
    Get-AzureRmCdnProfile [-ProfileName <String>] [-ResourceGroupName <String>] [-InformationAction
    <ActionPreference>] [-InformationVariable <String>] [<CommonParameters>]


DESCRIPTION
    Gets an Azure CDN profile and all related information.


RELATED LINKS

REMARKS
    To see the examples, type: "get-help Get-AzureRmCdnProfile -examples".
    For more information, type: "get-help Get-AzureRmCdnProfile -detailed".
    For technical information, type: "get-help Get-AzureRmCdnProfile -full".

```

## <a name="listing-existing-azure-cdn-profiles"></a><span data-ttu-id="71bd8-116">列出現有的 Azure CDN 設定檔</span><span class="sxs-lookup"><span data-stu-id="71bd8-116">Listing existing Azure CDN profiles</span></span>
<span data-ttu-id="71bd8-117">不含任何參數的 `Get-AzureRmCdnProfile` Cmdlet 會擷取所有現有的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="71bd8-117">The `Get-AzureRmCdnProfile` cmdlet without any parameters retrieves all your existing CDN profiles.</span></span>

```powershell
Get-AzureRmCdnProfile
```

<span data-ttu-id="71bd8-118">此輸出可以輸送到 Cmdlet 以便列舉。</span><span class="sxs-lookup"><span data-stu-id="71bd8-118">This output can be piped to cmdlets for enumeration.</span></span>

```powershell
# Output the name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

<span data-ttu-id="71bd8-119">您也可以指定設定檔名稱和資源群組，以傳回單一設定檔。</span><span class="sxs-lookup"><span data-stu-id="71bd8-119">You can also return a single profile by specifying the profile name and resource group.</span></span>

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> <span data-ttu-id="71bd8-120">可能會有多個具有相同名稱的 CDN 設定檔，只要它們位於不同的資源群組即可。</span><span class="sxs-lookup"><span data-stu-id="71bd8-120">It is possible to have multiple CDN profiles with the same name, so long as they are in different resource groups.</span></span>  <span data-ttu-id="71bd8-121">省略 `ResourceGroupName` 參數會傳回所有具有相符名稱的設定檔。</span><span class="sxs-lookup"><span data-stu-id="71bd8-121">Omitting the `ResourceGroupName` parameter returns all profiles with a matching name.</span></span>
> 
> 

## <a name="listing-existing-cdn-endpoints"></a><span data-ttu-id="71bd8-122">列出現有的 CDN 端點</span><span class="sxs-lookup"><span data-stu-id="71bd8-122">Listing existing CDN endpoints</span></span>
<span data-ttu-id="71bd8-123">`Get-AzureRmCdnEndpoint` 可以擷取設定檔上的個別端點或所有端點。</span><span class="sxs-lookup"><span data-stu-id="71bd8-123">`Get-AzureRmCdnEndpoint` can retrieve an individual endpoint or all the endpoints on a profile.</span></span>  

```powershell
# Get a single endpoint.
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Get all of the endpoints on a given profile. 
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG

# Return all of the endpoints on all of the profiles.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint

# Return all of the endpoints in this subscription that are currently running.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Where-Object { $_.ResourceState -eq "Running" }
```

## <a name="creating-cdn-profiles-and-endpoints"></a><span data-ttu-id="71bd8-124">建立 CDN 設定檔和端點</span><span class="sxs-lookup"><span data-stu-id="71bd8-124">Creating CDN profiles and endpoints</span></span>
<span data-ttu-id="71bd8-125">`New-AzureRmCdnProfile` 和 `New-AzureRmCdnEndpoint` 用來建立 CDN 設定檔和端點。</span><span class="sxs-lookup"><span data-stu-id="71bd8-125">`New-AzureRmCdnProfile` and `New-AzureRmCdnEndpoint` are used to create CDN profiles and endpoints.</span></span>

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a><span data-ttu-id="71bd8-126">檢查端點名稱可用性</span><span class="sxs-lookup"><span data-stu-id="71bd8-126">Checking endpoint name availability</span></span>
<span data-ttu-id="71bd8-127">`Get-AzureRmCdnEndpointNameAvailability` 可傳回物件，指出端點名稱是否可用。</span><span class="sxs-lookup"><span data-stu-id="71bd8-127">`Get-AzureRmCdnEndpointNameAvailability` returns an object indicating if an endpoint name is available.</span></span>

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message to the console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a><span data-ttu-id="71bd8-128">新增自訂網域</span><span class="sxs-lookup"><span data-stu-id="71bd8-128">Adding a custom domain</span></span>
<span data-ttu-id="71bd8-129">`New-AzureRmCdnCustomDomain` 會將自訂網域名稱新增至現有端點。</span><span class="sxs-lookup"><span data-stu-id="71bd8-129">`New-AzureRmCdnCustomDomain` adds a custom domain name to an existing endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71bd8-130">您必須以[如何將自訂網域對應至內容傳遞網路 (CDN) 端點](cdn-map-content-to-custom-domain.md)中所述方式，透過您的 DNS 提供者設定 CNAME。</span><span class="sxs-lookup"><span data-stu-id="71bd8-130">You must set up the CNAME with your DNS provider as described in [How to map Custom Domain to Content Delivery Network (CDN) endpoint](cdn-map-content-to-custom-domain.md).</span></span>  <span data-ttu-id="71bd8-131">您可以先測試對應，然後使用 `Test-AzureRmCdnCustomDomain`修改端點。</span><span class="sxs-lookup"><span data-stu-id="71bd8-131">You can test the mapping before modifying your endpoint using `Test-AzureRmCdnCustomDomain`.</span></span>
> 
> 

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Check the mapping
$result = Test-AzureRmCdnCustomDomain -CdnEndpoint $endpoint -CustomDomainHostName "cdn.contoso.com"

# Create the custom domain on the endpoint
If($result.CustomDomainValidated){ New-AzureRmCdnCustomDomain -CustomDomainName Contoso -HostName "cdn.contoso.com" -CdnEndpoint $endpoint }
```

## <a name="modifying-an-endpoint"></a><span data-ttu-id="71bd8-132">修改端點</span><span class="sxs-lookup"><span data-stu-id="71bd8-132">Modifying an endpoint</span></span>
<span data-ttu-id="71bd8-133">`Set-AzureRmCdnEndpoint` 可修改現有的端點。</span><span class="sxs-lookup"><span data-stu-id="71bd8-133">`Set-AzureRmCdnEndpoint` modifies an existing endpoint.</span></span>

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save the changed endpoint and apply the changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a><span data-ttu-id="71bd8-134">清除/預先載入 CDN 資產</span><span class="sxs-lookup"><span data-stu-id="71bd8-134">Purging/Pre-loading CDN assets</span></span>
<span data-ttu-id="71bd8-135">`Unpublish-AzureRmCdnEndpointContent` 會清除快取的資產，而 `Publish-AzureRmCdnEndpointContent` 會在支援的端點上預先載入資產。</span><span class="sxs-lookup"><span data-stu-id="71bd8-135">`Unpublish-AzureRmCdnEndpointContent` purges cached assets, while `Publish-AzureRmCdnEndpointContent` pre-loads assets on supported endpoints.</span></span>

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a><span data-ttu-id="71bd8-136">啟動/停止 CDN 端點</span><span class="sxs-lookup"><span data-stu-id="71bd8-136">Starting/Stopping CDN endpoints</span></span>
<span data-ttu-id="71bd8-137">`Start-AzureRmCdnEndpoint` 和 `Stop-AzureRmCdnEndpoint` 可用來啟動和停止個別端點的端點群組。</span><span class="sxs-lookup"><span data-stu-id="71bd8-137">`Start-AzureRmCdnEndpoint` and `Stop-AzureRmCdnEndpoint` can be used to start and stop individual endpoints or groups of endpoints.</span></span>

```powershell
# Stop the cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a><span data-ttu-id="71bd8-138">刪除 CDN 資源</span><span class="sxs-lookup"><span data-stu-id="71bd8-138">Deleting CDN resources</span></span>
<span data-ttu-id="71bd8-139">`Remove-AzureRmCdnProfile` 和 `Remove-AzureRmCdnEndpoint` 可用來移除設定檔和端點。</span><span class="sxs-lookup"><span data-stu-id="71bd8-139">`Remove-AzureRmCdnProfile` and `Remove-AzureRmCdnEndpoint` can be used to remove profiles and endpoints.</span></span>

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all the endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a><span data-ttu-id="71bd8-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="71bd8-140">Next Steps</span></span>
<span data-ttu-id="71bd8-141">了解如何透過 [.NET](cdn-app-dev-net.md) 或 [Node.js](cdn-app-dev-node.md) 自動化 Azure CDN。</span><span class="sxs-lookup"><span data-stu-id="71bd8-141">Learn how to automate Azure CDN with [.NET](cdn-app-dev-net.md) or [Node.js](cdn-app-dev-node.md).</span></span>

<span data-ttu-id="71bd8-142">若要了解 CDN 功能，請參閱 [CDN 概觀](cdn-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="71bd8-142">To learn about CDN features, see [CDN Overview](cdn-overview.md).</span></span>


---
title: "使用 PowerShell 的 Azure CDN aaaManage |Microsoft 文件"
description: "了解如何 toouse hello Azure PowerShell cmdlet toomanage Azure CDN。"
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
ms.openlocfilehash: 269373136d4ef018e4d31f147456b4be2253b463
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-cdn-with-powershell"></a><span data-ttu-id="a83d7-103">使用 PowerShell 管理 Azure CDN</span><span class="sxs-lookup"><span data-stu-id="a83d7-103">Manage Azure CDN with PowerShell</span></span>
<span data-ttu-id="a83d7-104">PowerShell 提供其中一個最有彈性方法 toomanage hello 您的 Azure CDN 設定檔和端點。</span><span class="sxs-lookup"><span data-stu-id="a83d7-104">PowerShell provides one of hello most flexible methods toomanage your Azure CDN profiles and endpoints.</span></span>  <span data-ttu-id="a83d7-105">您可以使用 PowerShell，以互動方式或透過撰寫指令碼 tooautomate 管理工作。</span><span class="sxs-lookup"><span data-stu-id="a83d7-105">You can use PowerShell interactively or by writing scripts tooautomate management tasks.</span></span>  <span data-ttu-id="a83d7-106">本教學課程會示範數個 hello 最常見的工作可完成 PowerShell toomanage 與您的 Azure CDN 設定檔和端點。</span><span class="sxs-lookup"><span data-stu-id="a83d7-106">This tutorial demonstrates several of hello most common tasks you can accomplish with PowerShell toomanage your Azure CDN profiles and endpoints.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a83d7-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="a83d7-107">Prerequisites</span></span>
<span data-ttu-id="a83d7-108">toouse PowerShell toomanage 您的 Azure CDN 設定檔和端點，您必須擁有 hello Azure PowerShell 模組安裝。</span><span class="sxs-lookup"><span data-stu-id="a83d7-108">toouse PowerShell toomanage your Azure CDN profiles and endpoints, you must have hello Azure PowerShell module installed.</span></span>  <span data-ttu-id="a83d7-109">toolearn 如何 tooinstall Azure PowerShell，並連接使用 hello tooAzure`Login-AzureRmAccount`指令程式，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="a83d7-109">toolearn how tooinstall Azure PowerShell and connect tooAzure using hello `Login-AzureRmAccount` cmdlet, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a83d7-110">您必須先使用 `Login-AzureRmAccount` 登入，才能執行 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a83d7-110">You must log in with `Login-AzureRmAccount` before you can execute Azure PowerShell cmdlets.</span></span>
> 
> 

## <a name="listing-hello-azure-cdn-cmdlets"></a><span data-ttu-id="a83d7-111">列出 hello Azure CDN cmdlet</span><span class="sxs-lookup"><span data-stu-id="a83d7-111">Listing hello Azure CDN cmdlets</span></span>
<span data-ttu-id="a83d7-112">您可以列出所有的 hello Azure CDN cmdlet 使用 hello `Get-Command` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a83d7-112">You can list all hello Azure CDN cmdlets using hello `Get-Command` cmdlet.</span></span>

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

## <a name="getting-help"></a><span data-ttu-id="a83d7-113">取得說明</span><span class="sxs-lookup"><span data-stu-id="a83d7-113">Getting help</span></span>
<span data-ttu-id="a83d7-114">您可以取得說明與任何這些 cmdlet 使用 hello `Get-Help` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a83d7-114">You can get help with any of these cmdlets using hello `Get-Help` cmdlet.</span></span>  <span data-ttu-id="a83d7-115">`Get-Help` 提供使用方式與語法，並選擇性地顯示範例。</span><span class="sxs-lookup"><span data-stu-id="a83d7-115">`Get-Help` provides usage and syntax, and optionally shows examples.</span></span>

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
    toosee hello examples, type: "get-help Get-AzureRmCdnProfile -examples".
    For more information, type: "get-help Get-AzureRmCdnProfile -detailed".
    For technical information, type: "get-help Get-AzureRmCdnProfile -full".

```

## <a name="listing-existing-azure-cdn-profiles"></a><span data-ttu-id="a83d7-116">列出現有的 Azure CDN 設定檔</span><span class="sxs-lookup"><span data-stu-id="a83d7-116">Listing existing Azure CDN profiles</span></span>
<span data-ttu-id="a83d7-117">hello`Get-AzureRmCdnProfile`不含任何參數的 cmdlet 會擷取所有現有 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="a83d7-117">hello `Get-AzureRmCdnProfile` cmdlet without any parameters retrieves all your existing CDN profiles.</span></span>

```powershell
Get-AzureRmCdnProfile
```

<span data-ttu-id="a83d7-118">此輸出可以傳送的 toocmdlets 列舉。</span><span class="sxs-lookup"><span data-stu-id="a83d7-118">This output can be piped toocmdlets for enumeration.</span></span>

```powershell
# Output hello name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

<span data-ttu-id="a83d7-119">您也可以指定 hello 設定檔名稱和資源群組，以傳回單一設定檔。</span><span class="sxs-lookup"><span data-stu-id="a83d7-119">You can also return a single profile by specifying hello profile name and resource group.</span></span>

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> <span data-ttu-id="a83d7-120">可能的 toohave，只要它們是不同的資源群組中多個的 CDN 設定檔名稱相同的 hello 與它。</span><span class="sxs-lookup"><span data-stu-id="a83d7-120">It is possible toohave multiple CDN profiles with hello same name, so long as they are in different resource groups.</span></span>  <span data-ttu-id="a83d7-121">省略 hello`ResourceGroupName`參數會傳回具有相符名稱的所有設定檔。</span><span class="sxs-lookup"><span data-stu-id="a83d7-121">Omitting hello `ResourceGroupName` parameter returns all profiles with a matching name.</span></span>
> 
> 

## <a name="listing-existing-cdn-endpoints"></a><span data-ttu-id="a83d7-122">列出現有的 CDN 端點</span><span class="sxs-lookup"><span data-stu-id="a83d7-122">Listing existing CDN endpoints</span></span>
<span data-ttu-id="a83d7-123">`Get-AzureRmCdnEndpoint`可以擷取個別端點或設定檔上的所有 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="a83d7-123">`Get-AzureRmCdnEndpoint` can retrieve an individual endpoint or all hello endpoints on a profile.</span></span>  

```powershell
# Get a single endpoint.
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Get all of hello endpoints on a given profile. 
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG

# Return all of hello endpoints on all of hello profiles.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint

# Return all of hello endpoints in this subscription that are currently running.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Where-Object { $_.ResourceState -eq "Running" }
```

## <a name="creating-cdn-profiles-and-endpoints"></a><span data-ttu-id="a83d7-124">建立 CDN 設定檔和端點</span><span class="sxs-lookup"><span data-stu-id="a83d7-124">Creating CDN profiles and endpoints</span></span>
<span data-ttu-id="a83d7-125">`New-AzureRmCdnProfile`和`New-AzureRmCdnEndpoint`會使用的 toocreate CDN 設定檔和端點。</span><span class="sxs-lookup"><span data-stu-id="a83d7-125">`New-AzureRmCdnProfile` and `New-AzureRmCdnEndpoint` are used toocreate CDN profiles and endpoints.</span></span>

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a><span data-ttu-id="a83d7-126">檢查端點名稱可用性</span><span class="sxs-lookup"><span data-stu-id="a83d7-126">Checking endpoint name availability</span></span>
<span data-ttu-id="a83d7-127">`Get-AzureRmCdnEndpointNameAvailability` 可傳回物件，指出端點名稱是否可用。</span><span class="sxs-lookup"><span data-stu-id="a83d7-127">`Get-AzureRmCdnEndpointNameAvailability` returns an object indicating if an endpoint name is available.</span></span>

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message toohello console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a><span data-ttu-id="a83d7-128">新增自訂網域</span><span class="sxs-lookup"><span data-stu-id="a83d7-128">Adding a custom domain</span></span>
<span data-ttu-id="a83d7-129">`New-AzureRmCdnCustomDomain`加入自訂網域名稱 tooan 現有端點。</span><span class="sxs-lookup"><span data-stu-id="a83d7-129">`New-AzureRmCdnCustomDomain` adds a custom domain name tooan existing endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a83d7-130">您必須設定 hello CNAME 與您的 DNS 提供者中所述[如何 toomap 自訂網域 tooContent 傳遞網路 (CDN) 端點](cdn-map-content-to-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="a83d7-130">You must set up hello CNAME with your DNS provider as described in [How toomap Custom Domain tooContent Delivery Network (CDN) endpoint](cdn-map-content-to-custom-domain.md).</span></span>  <span data-ttu-id="a83d7-131">您可以測試 hello 對應之前修改程式端點，請使用`Test-AzureRmCdnCustomDomain`。</span><span class="sxs-lookup"><span data-stu-id="a83d7-131">You can test hello mapping before modifying your endpoint using `Test-AzureRmCdnCustomDomain`.</span></span>
> 
> 

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Check hello mapping
$result = Test-AzureRmCdnCustomDomain -CdnEndpoint $endpoint -CustomDomainHostName "cdn.contoso.com"

# Create hello custom domain on hello endpoint
If($result.CustomDomainValidated){ New-AzureRmCdnCustomDomain -CustomDomainName Contoso -HostName "cdn.contoso.com" -CdnEndpoint $endpoint }
```

## <a name="modifying-an-endpoint"></a><span data-ttu-id="a83d7-132">修改端點</span><span class="sxs-lookup"><span data-stu-id="a83d7-132">Modifying an endpoint</span></span>
<span data-ttu-id="a83d7-133">`Set-AzureRmCdnEndpoint` 可修改現有的端點。</span><span class="sxs-lookup"><span data-stu-id="a83d7-133">`Set-AzureRmCdnEndpoint` modifies an existing endpoint.</span></span>

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save hello changed endpoint and apply hello changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a><span data-ttu-id="a83d7-134">清除/預先載入 CDN 資產</span><span class="sxs-lookup"><span data-stu-id="a83d7-134">Purging/Pre-loading CDN assets</span></span>
<span data-ttu-id="a83d7-135">`Unpublish-AzureRmCdnEndpointContent` 會清除快取的資產，而 `Publish-AzureRmCdnEndpointContent` 會在支援的端點上預先載入資產。</span><span class="sxs-lookup"><span data-stu-id="a83d7-135">`Unpublish-AzureRmCdnEndpointContent` purges cached assets, while `Publish-AzureRmCdnEndpointContent` pre-loads assets on supported endpoints.</span></span>

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a><span data-ttu-id="a83d7-136">啟動/停止 CDN 端點</span><span class="sxs-lookup"><span data-stu-id="a83d7-136">Starting/Stopping CDN endpoints</span></span>
<span data-ttu-id="a83d7-137">`Start-AzureRmCdnEndpoint`和`Stop-AzureRmCdnEndpoint`可以使用的 toostart 並停止個別端點群組。</span><span class="sxs-lookup"><span data-stu-id="a83d7-137">`Start-AzureRmCdnEndpoint` and `Stop-AzureRmCdnEndpoint` can be used toostart and stop individual endpoints or groups of endpoints.</span></span>

```powershell
# Stop hello cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a><span data-ttu-id="a83d7-138">刪除 CDN 資源</span><span class="sxs-lookup"><span data-stu-id="a83d7-138">Deleting CDN resources</span></span>
<span data-ttu-id="a83d7-139">`Remove-AzureRmCdnProfile`和`Remove-AzureRmCdnEndpoint`可以是使用的 tooremove 設定檔和端點。</span><span class="sxs-lookup"><span data-stu-id="a83d7-139">`Remove-AzureRmCdnProfile` and `Remove-AzureRmCdnEndpoint` can be used tooremove profiles and endpoints.</span></span>

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all hello endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a><span data-ttu-id="a83d7-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a83d7-140">Next Steps</span></span>
<span data-ttu-id="a83d7-141">深入了解如何 tooautomate Azure CDN 與[.NET](cdn-app-dev-net.md)或[Node.js](cdn-app-dev-node.md)。</span><span class="sxs-lookup"><span data-stu-id="a83d7-141">Learn how tooautomate Azure CDN with [.NET](cdn-app-dev-net.md) or [Node.js](cdn-app-dev-node.md).</span></span>

<span data-ttu-id="a83d7-142">toolearn 需 CDN 功能，請參閱[CDN 概觀](cdn-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a83d7-142">toolearn about CDN features, see [CDN Overview](cdn-overview.md).</span></span>


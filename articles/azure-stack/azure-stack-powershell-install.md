---
title: "aaaInstall PowerShell for Azure 堆疊 |Microsoft 文件"
description: "深入了解如何 tooinstall PowerShell for Azure 堆疊。"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: sngun
ms.openlocfilehash: 60995af2168348638e2513ab941a4125ca5c624a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-powershell-for-azure-stack"></a><span data-ttu-id="76774-103">安裝適用於 Azure Stack 的 PowerShell</span><span class="sxs-lookup"><span data-stu-id="76774-103">Install PowerShell for Azure Stack</span></span>  

<span data-ttu-id="76774-104">Azure 堆疊相容 Azure PowerShell 模組是與 Azure 堆疊的必要的 toowork。</span><span class="sxs-lookup"><span data-stu-id="76774-104">Azure Stack compatible Azure PowerShell modules are required toowork with Azure Stack.</span></span> <span data-ttu-id="76774-105">本指南中，我們逐步引導您 hello 步驟需要 tooinstall PowerShell 的 Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="76774-105">In this guide, we walk you through hello steps required tooinstall PowerShell for Azure Stack.</span></span> <span data-ttu-id="76774-106">您可以使用本文從 hello Azure 堆疊開發套件，或是從 windows 的外部用戶端中所述，如果您透過 VPN 連線的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="76774-106">You can use hello steps described in this article either from hello Azure Stack Development Kit, or from a Windows-based external client if you are connected through VPN.</span></span>

<span data-ttu-id="76774-107">這篇文章包含詳細指示 tooinstall PowerShell 的 Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="76774-107">This article has detailed instructions tooinstall PowerShell for Azure Stack.</span></span> <span data-ttu-id="76774-108">不過，如果您想 tooquickly 安裝並設定 PowerShell 時，您可以使用 hello 指令碼中的 hello 提供[取得啟動並執行使用 PowerShell](azure-stack-powershell-configure-quickstart.md)主題。</span><span class="sxs-lookup"><span data-stu-id="76774-108">However, if you want tooquickly install and configure PowerShell, you can use hello script that is provided in hello [Get up and running with PowerShell](azure-stack-powershell-configure-quickstart.md) topic.</span></span> 

> [!NOTE]
> <span data-ttu-id="76774-109">下列步驟的 hello 需要 PowerShell 5.0。</span><span class="sxs-lookup"><span data-stu-id="76774-109">hello following steps require PowerShell 5.0.</span></span> <span data-ttu-id="76774-110">toocheck 您的版本、 執行 $PSVersionTable.PSVersion 和比較 hello 「 主要 」 版本。</span><span class="sxs-lookup"><span data-stu-id="76774-110">toocheck your version, run $PSVersionTable.PSVersion and compare hello "Major" version.</span></span>

<span data-ttu-id="76774-111">Azure 堆疊的 PowerShell 命令會透過 hello PowerShell 資源庫進行安裝。</span><span class="sxs-lookup"><span data-stu-id="76774-111">PowerShell commands for Azure Stack are installed through hello PowerShell gallery.</span></span> <span data-ttu-id="76774-112">tooregiser hello PSGallery 儲存機制、 開啟提升權限的 PowerShell 工作階段從 hello 開發套件，或從 windows 的外部用戶端透過 VPN 連線，然後執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="76774-112">tooregiser hello PSGallery repository, open an elevated PowerShell session from hello development kit or from a Windows-based external client if you are connected through VPN and run hello following command:</span></span>

```powershell
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted
```

## <a name="uninstall-existing-versions-of-powershell"></a><span data-ttu-id="76774-113">解除安裝現有的 PowerShell 版本</span><span class="sxs-lookup"><span data-stu-id="76774-113">Uninstall existing versions of PowerShell</span></span>

<span data-ttu-id="76774-114">在安裝之前 hello 必要的版本，請確定您在解除安裝任何現有的 Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="76774-114">Before installing hello required version, make sure that you uninstall any existing Azure PowerShell modules.</span></span> <span data-ttu-id="76774-115">您可以使用其中一種 hello 下列兩種方法來解除安裝這些設定：</span><span class="sxs-lookup"><span data-stu-id="76774-115">You can uninstall them by using one of hello following two methods:</span></span>

* <span data-ttu-id="76774-116">如果您計劃 tooestablish VPN 連線，toouninstall hello 現有 PowerShell 模組，會登入 toohello development kit 或 toohello Windows 架構的外部用戶端。</span><span class="sxs-lookup"><span data-stu-id="76774-116">toouninstall hello existing PowerShell modules, sign in toohello development kit, or toohello Windows-based external client if you are planning tooestablish a VPN connection.</span></span> <span data-ttu-id="76774-117">關閉所有 hello 作用中的 PowerShell 工作階段和執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="76774-117">Close all hello active PowerShell sessions and run hello following command:</span></span> 

   ```powershell
   Get-Module -ListAvailable | where-Object {$_.Name -like “Azure*”} | Uninstall-Module
   ```

* <span data-ttu-id="76774-118">登入 toohello development kit 或 toohello Windows 架構的外部用戶端如果您計劃 tooestablish VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="76774-118">Sign in toohello development kit, or toohello Windows-based external client if you are planning tooestablish a VPN connection.</span></span> <span data-ttu-id="76774-119">刪除從 hello 以"Azure"開頭的所有 hello 資料夾`C:\Program Files (x86)\WindowsPowerShell\Modules`和`C:\Users\AzureStackAdmin\Documents\WindowsPowerShell\Modules`資料夾。</span><span class="sxs-lookup"><span data-stu-id="76774-119">Delete all hello folders that start with "Azure" from hello `C:\Program Files (x86)\WindowsPowerShell\Modules` and `C:\Users\AzureStackAdmin\Documents\WindowsPowerShell\Modules` folders.</span></span> <span data-ttu-id="76774-120">刪除這些資料夾中移除任何現有的 PowerShell 模組，從 hello"AzureStackAdmin 」 與 「 全域 」 的使用者領域。</span><span class="sxs-lookup"><span data-stu-id="76774-120">Deleting these folders removes any existing PowerShell modules from hello "AzureStackAdmin" and "global" user scopes.</span></span> 

<span data-ttu-id="76774-121">hello 下列各節說明 hello 步驟需要的 tooinstall PowerShell for Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="76774-121">hello following sections describe hello steps required tooinstall PowerShell for Azure Stack.</span></span> <span data-ttu-id="76774-122">可在連線、部分連線或中斷連線案例中，於 Azure Stack 上安裝 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="76774-122">PowerShell can be installed on Azure Stack that is operated in connected, partially connected, or in a disconnected scenario.</span></span> 

## <a name="install-powershell-in-a-connected-scenario"></a><span data-ttu-id="76774-123">在連線案例中安裝 PowerShell</span><span class="sxs-lookup"><span data-stu-id="76774-123">Install PowerShell in a connected scenario</span></span> 

<span data-ttu-id="76774-124">透過 API 版本設定檔安裝 Azure Stack 相容的 AzureRM 模組。</span><span class="sxs-lookup"><span data-stu-id="76774-124">Azure Stack compatible AzureRM modules are installed through API version profiles.</span></span> <span data-ttu-id="76774-125">Azure 堆疊需要 hello **2017年-03-09-設定檔**API 版本設定檔，也就是可用安裝 hello AzureRM.Bootstrapper 模組。</span><span class="sxs-lookup"><span data-stu-id="76774-125">Azure Stack requires hello **2017-03-09-profile** API version profile, which is available by installing hello AzureRM.Bootstrapper module.</span></span> <span data-ttu-id="76774-126">API 版本設定檔和 hello cmdlet，提供關於 toolearn 參考 toohello[管理 API 版本設定檔](azure-stack-version-profiles.md)。</span><span class="sxs-lookup"><span data-stu-id="76774-126">toolearn about API version profiles and hello cmdlets provided by them, refer toohello [manage API version profiles](azure-stack-version-profiles.md).</span></span> <span data-ttu-id="76774-127">在加法 toohello AzureRM 模組中，您也應該安裝 hello Azure 堆疊專屬 PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="76774-127">In addition toohello AzureRM modules, you should also install hello Azure Stack-specific PowerShell modules.</span></span> <span data-ttu-id="76774-128">在開發工作站上執行下列 PowerShell 指令碼 tooinstall hello 這些模組：</span><span class="sxs-lookup"><span data-stu-id="76774-128">Run hello following PowerShell script tooinstall these modules on your development workstation:</span></span>

  ```powershell
  # Install hello AzureRM.Bootstrapper module. Select Yes when prompted tooinstall NuGet 
  Install-Module `
    -Name AzureRm.BootStrapper

  # Install and import hello API Version Profile required by Azure Stack into hello current PowerShell session.
  Use-AzureRmProfile `
    -Profile 2017-03-09-profile -Force

  Install-Module `
    -Name AzureStack `
    -RequiredVersion 1.2.10
  ```

<span data-ttu-id="76774-129">tooconfirm hello 安裝，請執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="76774-129">tooconfirm hello installation, run hello following command:</span></span>

  ```powershell
  Get-Module `
    -ListAvailable | where-Object {$_.Name -like “Azure*”}
  ```
  <span data-ttu-id="76774-130">如果 hello 安裝成功，會顯示 hello AzureRM 和 AzureStack 模組 hello 輸出中。</span><span class="sxs-lookup"><span data-stu-id="76774-130">If hello installation is successful, hello AzureRM and AzureStack modules are displayed in hello output.</span></span>

## <a name="install-powershell-in-a-disconnected-or-in-a-partially-connected-scenario"></a><span data-ttu-id="76774-131">在已中斷連線或部分連線案例中安裝 PowerShell</span><span class="sxs-lookup"><span data-stu-id="76774-131">Install PowerShell in a disconnected or in a partially connected scenario</span></span>

<span data-ttu-id="76774-132">在中斷連線的案例中，您必須先下載 hello PowerShell 模組 tooa 電腦具有網際網路連線，然後將其傳送 toohello Azure 堆疊開發套件進行安裝。</span><span class="sxs-lookup"><span data-stu-id="76774-132">In a disconnected scenario, you must first download hello PowerShell modules tooa machine that has internet connectivity, and then transfer them toohello Azure Stack Development Kit for installation.</span></span>

1. <span data-ttu-id="76774-133">登入 tooa 電腦，而且您的網際網路連線，使用下列指令碼 toodownload hello AzureRM，hello AzureStack 封裝到您的本機電腦上：</span><span class="sxs-lookup"><span data-stu-id="76774-133">Sign in tooa computer where you have internet connectivity and use hello following script toodownload hello AzureRM, and AzureStack packages onto your local computer:</span></span>

   ```powershell
   $Path = "<Path that is used toosave hello packages>"

   Save-Package `
     -ProviderName NuGet `
     -Source https://www.powershellgallery.com/api/v2 `
     -Name AzureRM `
     -Path $Path `
     -Force `
     -RequiredVersion 1.2.10

   Save-Package `
     -ProviderName NuGet `
     -Source https://www.powershellgallery.com/api/v2 `
     -Name AzureStack `
     -Path $Path `
     -Force `
     -RequiredVersion 1.2.10 
   ```

2. <span data-ttu-id="76774-134">複製 hello tooa USB 裝置透過下載封裝。</span><span class="sxs-lookup"><span data-stu-id="76774-134">Copy hello downloaded packages over tooa USB device.</span></span>

3. <span data-ttu-id="76774-135">登入 toohello 開發套件，並從 hello USB 裝置 tooa 位置 hello 開發套件複製 hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="76774-135">Sign in toohello development kit and copy hello packages from hello USB device tooa location on hello development kit.</span></span> 

4. <span data-ttu-id="76774-136">現在您必須註冊此位置為 hello 預設儲存機制，並從這個儲存機制安裝 hello AzureRM 和 AzureStack 模組：</span><span class="sxs-lookup"><span data-stu-id="76774-136">Now you must register this location as hello default repository and install hello AzureRM and AzureStack modules from this repository:</span></span>

   ```powershell
   $SourceLocation = "<Location on hello development kit that contains hello PowerShell packages>"
   $RepoName = "MyNuGetSource"

   Register-PSRepository `
     -Name $RepoName `
     -SourceLocation $SourceLocation `
     -InstallationPolicy Trusted

   ```powershell
   Install-Module AzureRM `
     -Repository $RepoName

   Install-Module AzureStack `
     -Repository $RepoName 
   ```

## <a name="next-steps"></a><span data-ttu-id="76774-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="76774-137">Next steps</span></span>

* [<span data-ttu-id="76774-138">從 GitHub 下載 Azure Stack 工具</span><span class="sxs-lookup"><span data-stu-id="76774-138">Download Azure Stack tools from GitHub</span></span>](azure-stack-powershell-download.md)
* [<span data-ttu-id="76774-139">設定 hello Azure 堆疊使用者的 PowerShell 環境</span><span class="sxs-lookup"><span data-stu-id="76774-139">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)  
* [<span data-ttu-id="76774-140">設定 hello Azure 堆疊操作員的 PowerShell 環境</span><span class="sxs-lookup"><span data-stu-id="76774-140">Configure hello Azure Stack operator's PowerShell environment</span></span>](azure-stack-powershell-configure-admin.md) 
* [<span data-ttu-id="76774-141">在 Azure Stack 中管理 API 版本設定檔</span><span class="sxs-lookup"><span data-stu-id="76774-141">Manage API version profiles in Azure Stack</span></span>](azure-stack-version-profiles.md)  

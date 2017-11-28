---
title: "在 Azure 堆疊 aaaUsing API 版本設定檔 |Microsoft 文件"
description: "了解 Azure Stack 中的 API 版本設定檔。"
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
ms.date: 03/21/2017
ms.author: sngun
ms.openlocfilehash: cb54a683054f08fd123bcb6245d88aaa30c29882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-api-version-profiles-in-azure-stack"></a><span data-ttu-id="49a1f-103">管理 Azure Stack 中的 API 版本設定檔</span><span class="sxs-lookup"><span data-stu-id="49a1f-103">Manage API version profiles in Azure Stack</span></span>

<span data-ttu-id="49a1f-104">API 版本設定檔提供方式 toomanage Azure 和 Azure 堆疊之間的版本差異。</span><span class="sxs-lookup"><span data-stu-id="49a1f-104">API version profiles provide a way toomanage version differences between Azure and Azure Stack.</span></span> <span data-ttu-id="49a1f-105">API 版本設定檔是一組具有特定 API 版本的 AzureRM PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="49a1f-105">An API version profile is a set of AzureRM PowerShell modules with specific API versions.</span></span> <span data-ttu-id="49a1f-106">每個雲端平台都有一組支援的 API 版本設定檔。</span><span class="sxs-lookup"><span data-stu-id="49a1f-106">Each cloud platform has a set of supported API version profiles.</span></span> <span data-ttu-id="49a1f-107">例如，Azure 堆疊支援特定的日期設定檔版本例如**2017年-03-09-設定檔**，和 Azure 支援 hello**最新**API 版本設定檔。</span><span class="sxs-lookup"><span data-stu-id="49a1f-107">For example, Azure Stack supports a specific dated profile version such as  **2017-03-09-profile**, and Azure supports hello **latest** API version profile.</span></span> <span data-ttu-id="49a1f-108">當您安裝設定檔時，hello 對應 toohello 的 AzureRM PowerShell 模組指定設定檔會安裝。</span><span class="sxs-lookup"><span data-stu-id="49a1f-108">When you install a profile, hello AzureRM PowerShell modules that correspond toohello specified profile are installed.</span></span>

## <a name="install-hello-powershell-module-required-toouse-api-version-profiles"></a><span data-ttu-id="49a1f-109">安裝 hello PowerShell 模組所需 toouse API 版本設定檔</span><span class="sxs-lookup"><span data-stu-id="49a1f-109">Install hello PowerShell module required toouse API version profiles</span></span>

<span data-ttu-id="49a1f-110">hello **AzureRM.Bootstrapper**可透過 PowerShell 資源庫 hello 的模組提供 PowerShell cmdlet 的必要的 toowork 使用的 API 版本設定檔。</span><span class="sxs-lookup"><span data-stu-id="49a1f-110">hello **AzureRM.Bootstrapper** module that is available through hello PowerShell Gallery provides PowerShell cmdlets that are required toowork with API version profiles.</span></span> <span data-ttu-id="49a1f-111">使用下列 cmdlet tooinstall hello AzureRM.Bootstrapper 模組 hello:</span><span class="sxs-lookup"><span data-stu-id="49a1f-111">Use hello following cmdlet tooinstall hello AzureRM.Bootstrapper module:</span></span>

```PowerShell
Install-Module -Name AzureRm.BootStrapper
```
<span data-ttu-id="49a1f-112">hello AzureRM.Bootstrapper 模組目前處於預覽狀態。詳細資料和功能會主旨 toochange。</span><span class="sxs-lookup"><span data-stu-id="49a1f-112">hello AzureRM.Bootstrapper module is in preview; details and functionality are subject toochange.</span></span> <span data-ttu-id="49a1f-113">toodownload 並安裝 hello 最新版本中執行下列 cmdlet 的 hello hello PowerShell 資源庫，此模組：</span><span class="sxs-lookup"><span data-stu-id="49a1f-113">toodownload and install hello latest version of this module from hello PowerShell Gallery, run hello following cmdlet:</span></span>

```PowerShell
Update-Module -Name "AzureRm.BootStrapper"
```

## <a name="install-a-profile"></a><span data-ttu-id="49a1f-114">安裝設定檔</span><span class="sxs-lookup"><span data-stu-id="49a1f-114">Install a profile</span></span>

<span data-ttu-id="49a1f-115">使用 hello**安裝 AzureRmProfile** cmdlet 搭配 hello **2017年-03-09-設定檔**API 版本設定檔 tooinstall hello AzureRM 模組所需的 Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="49a1f-115">Use hello **Install-AzureRmProfile** cmdlet with hello **2017-03-09-profile** API version profile tooinstall hello AzureRM modules required by Azure Stack.</span></span> <span data-ttu-id="49a1f-116">請注意，hello Azure 堆疊雲端系統管理員模組不會安裝這個應用程式開發介面版本設定檔，而且應該先安裝它們個別的 hello hello 步驟 3 中指定[安裝 PowerShell Azure 堆疊以](azure-stack-powershell-install.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="49a1f-116">Note that hello Azure Stack cloud administrator modules are not installed with this API version profile, and they should be installed separately as specified in hello Step 3 of hello [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) article.</span></span>

```PowerShell 
Install-AzureRMProfile -Profile 2017-03-09-profile
```
## <a name="install-and-import-modules-in-a-profile"></a><span data-ttu-id="49a1f-117">安裝並匯入設定檔中的模組</span><span class="sxs-lookup"><span data-stu-id="49a1f-117">Install and import modules in a profile</span></span>

<span data-ttu-id="49a1f-118">使用 hello**使用 AzureRmProfile**的 API 版本設定檔相關聯的 cmdlet tooinstall 和匯入模組。</span><span class="sxs-lookup"><span data-stu-id="49a1f-118">Use hello **Use-AzureRmProfile** cmdlet tooinstall and import modules that are associated with an API version profile.</span></span> <span data-ttu-id="49a1f-119">在一個 PowerShell 工作階段中只能匯入一個 API 版本設定檔。</span><span class="sxs-lookup"><span data-stu-id="49a1f-119">You can import only one API version profile in a PowerShell session.</span></span> <span data-ttu-id="49a1f-120">tooimport 不同的應用程式開發介面版本設定檔，您就必須開啟新的 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="49a1f-120">tooimport a different API version profile, you must open a new PowerShell session.</span></span> <span data-ttu-id="49a1f-121">hello 使用 AzureRMProfile 指令程式會執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="49a1f-121">hello Use-AzureRMProfile cmdlet runs hello following tasks:</span></span>  
1. <span data-ttu-id="49a1f-122">檢查如果 hello 與相關聯的 hello PowerShell 模組指定的 API 版本設定檔會安裝在 hello 目前範圍中。</span><span class="sxs-lookup"><span data-stu-id="49a1f-122">Checks if hello PowerShell modules associated with hello specified API version profile are installed in hello current scope.</span></span>  
2. <span data-ttu-id="49a1f-123">下載並安裝 hello 模組，如果尚未安裝。</span><span class="sxs-lookup"><span data-stu-id="49a1f-123">Downloads and installs hello modules if they are not already installed.</span></span>   
3. <span data-ttu-id="49a1f-124">匯入到目前 PowerShell 工作階段 hello hello 模組。</span><span class="sxs-lookup"><span data-stu-id="49a1f-124">Imports hello modules into hello current PowerShell session.</span></span> 

```PowerShell
# Installs and imports hello specified API version profile into hello current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser

# Installs and imports hello specified API version profile into hello current PowerShell session without any prompts
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser -Force
```

<span data-ttu-id="49a1f-125">tooinstall 和匯入選取的 API 版本設定檔，執行 hello 使用 AzureRMProfile 指令程式以 hello AzureRM 模組**模組**參數：</span><span class="sxs-lookup"><span data-stu-id="49a1f-125">tooinstall and import selected AzureRM modules from an API version profile, run hello Use-AzureRMProfile cmdlet with hello **Module** parameter:</span></span>

```PowerShell
# Installs and imports hello compute, Storage and Network modules from hello specified API version profile into your current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Module AzureRM.Compute, AzureRM.Storage, AzureRM.Network
```

## <a name="get-hello-installed-profiles"></a><span data-ttu-id="49a1f-126">取得安裝的 hello 設定檔</span><span class="sxs-lookup"><span data-stu-id="49a1f-126">Get hello installed profiles</span></span>

<span data-ttu-id="49a1f-127">使用 hello **Get AzureRmProfile** cmdlet tooget hello 清單可用的 API 版本設定檔：</span><span class="sxs-lookup"><span data-stu-id="49a1f-127">Use hello **Get-AzureRmProfile** cmdlet tooget hello list of available API version profiles:</span></span> 

```PowerShell
# lists all API version profiles provided by hello AzureRM.BootStrapper module.
Get-AzureRmProfile -ListAvailable 

# lists hello API version profiles which are installed on your machine
Get-AzureRmProfile
```
## <a name="update-profiles"></a><span data-ttu-id="49a1f-128">更新設定檔</span><span class="sxs-lookup"><span data-stu-id="49a1f-128">Update profiles</span></span>

<span data-ttu-id="49a1f-129">使用 hello**更新 AzureRmProfile**模組中可用的 API 版本設定檔 toohello 最新版本中的 cmdlet tooupdate hello 模組 hello PSGallery。</span><span class="sxs-lookup"><span data-stu-id="49a1f-129">Use hello **Update-AzureRmProfile** cmdlet tooupdate hello modules in an API version profile toohello latest version of modules that are available in hello PSGallery.</span></span> <span data-ttu-id="49a1f-130">建議 tooalways 執行 hello**更新 AzureRmProfile**匯入模組時，指令程式在新的 PowerShell 工作階段 tooavoid 相衝突。</span><span class="sxs-lookup"><span data-stu-id="49a1f-130">It's recommended tooalways run hello **Update-AzureRmProfile** cmdlet in a new PowerShell session tooavoid conflicts when importing modules.</span></span> <span data-ttu-id="49a1f-131">hello 更新 AzureRmProfile 指令程式會執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="49a1f-131">hello Update-AzureRmProfile cmdlet runs hello following tasks:</span></span>

1. <span data-ttu-id="49a1f-132">檢查是否 hello 最新版本的模組會安裝在 hello hello 目前領域中指定 API 版本設定檔。</span><span class="sxs-lookup"><span data-stu-id="49a1f-132">Checks if hello latest versions of modules are installed in hello given API version profile for hello current scope.</span></span>  
2. <span data-ttu-id="49a1f-133">會提示您 tooinstall 如果尚未安裝。</span><span class="sxs-lookup"><span data-stu-id="49a1f-133">Prompts you tooinstall if they are not already installed.</span></span>  
3. <span data-ttu-id="49a1f-134">安裝和更新的 hello 模組匯入到 hello 目前 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="49a1f-134">Installs and imports hello updated modules into hello current PowerShell session.</span></span>  

```PowerShell
Update-AzureRmProfile -Profile 2017-03-09-profile
```

<span data-ttu-id="49a1f-135">tooremove hello 先前已安裝版本的 hello 模組，然後再更新 toohello 最新可用版本，就會使用 hello 更新 AzureRmProfile cmdlet，以及 hello **-RemovePreviousVersions**參數：</span><span class="sxs-lookup"><span data-stu-id="49a1f-135">tooremove hello previously installed versions of hello modules before updating toohello latest available version, use hello Update-AzureRmProfile cmdlet along with hello **-RemovePreviousVersions** parameter:</span></span>

```PowerShell 
Update-AzureRmProfile -Profile 2017-03-09-profile -RemovePreviousVersions
```

<span data-ttu-id="49a1f-136">此 cmdlet 會執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="49a1f-136">This cmdlet runs hello following tasks:</span></span>  

1. <span data-ttu-id="49a1f-137">檢查是否 hello 最新版本的模組會安裝在 hello hello 目前領域中指定 API 版本設定檔。</span><span class="sxs-lookup"><span data-stu-id="49a1f-137">Checks if hello latest versions of modules are installed in hello given API version profile for hello current scope.</span></span>  
2. <span data-ttu-id="49a1f-138">從目前的 API 版本設定檔 hello 和 hello 目前 PowerShell 工作階段中移除 hello 較舊版本的模組。</span><span class="sxs-lookup"><span data-stu-id="49a1f-138">Removes hello older versions of modules from hello current API version profile and in hello current PowerShell session.</span></span>  
4. <span data-ttu-id="49a1f-139">會提示您 tooinstall hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="49a1f-139">prompts you tooinstall hello latest version.</span></span>  
5. <span data-ttu-id="49a1f-140">安裝和更新的 hello 模組匯入到 hello 目前 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="49a1f-140">Installs and imports hello updated modules into hello current PowerShell session.</span></span>  
 
## <a name="uninstall-profiles"></a><span data-ttu-id="49a1f-141">將設定檔解除安裝</span><span class="sxs-lookup"><span data-stu-id="49a1f-141">Uninstall profiles</span></span>

<span data-ttu-id="49a1f-142">使用 hello**解除安裝 AzureRmProfile** cmdlet toouninstall hello 指定 API 版本設定檔。</span><span class="sxs-lookup"><span data-stu-id="49a1f-142">Use hello **Uninstall-AzureRmProfile** cmdlet toouninstall hello specified API version profile.</span></span>

```PowerShell 
Uninstall-AzureRmProfile -Profile 2017-03-09-profile
```

## <a name="next-steps"></a><span data-ttu-id="49a1f-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="49a1f-143">Next steps</span></span>
* [<span data-ttu-id="49a1f-144">安裝 Azure Stack 適用的 PowerShell</span><span class="sxs-lookup"><span data-stu-id="49a1f-144">Install PowerShell for Azure Stack</span></span>](azure-stack-powershell-install.md)
* [<span data-ttu-id="49a1f-145">設定 hello Azure 堆疊使用者的 PowerShell 環境</span><span class="sxs-lookup"><span data-stu-id="49a1f-145">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)  

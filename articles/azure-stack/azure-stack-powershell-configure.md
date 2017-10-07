---
title: "搭配 Azure 堆疊 aaaConfigure PowerShell |Microsoft 文件"
description: "深入了解如何 tooconfigure PowerShell for Azure 堆疊。"
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
ms.date: 07/16/2017
ms.author: sngun
ms.openlocfilehash: bc40869abe453cef4854daaf11605efd94a66c99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-powershell-for-use-with-azure-stack"></a><span data-ttu-id="d2e22-103">設定 Azure 堆疊搭配使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2e22-103">Configure PowerShell for use with Azure Stack</span></span> 

<span data-ttu-id="d2e22-104">本文將說明使用 PowerShell hello 步驟需要的 tooconnect tooan Azure 堆疊開發套件執行個體。</span><span class="sxs-lookup"><span data-stu-id="d2e22-104">This article describes hello steps required tooconnect tooan Azure Stack Development Kit instance by using PowerShell.</span></span> <span data-ttu-id="d2e22-105">您連接之後，您可以存取 hello 入口網站，並部署透過 PowerShell 的資源。</span><span class="sxs-lookup"><span data-stu-id="d2e22-105">After you connect, you can access hello portal and deploy resources through PowerShell.</span></span> <span data-ttu-id="d2e22-106">您可以使用本文從 hello 開發套件，或是從 windows 的外部用戶端中所述，如果您透過 VPN 連線的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="d2e22-106">You can use hello steps described in this article either from hello development kit, or from a Windows-based external client if you are connected through VPN.</span></span>

<span data-ttu-id="d2e22-107">這篇文章包含詳細指示 tooconfigure PowerShell 的 Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="d2e22-107">This article has detailed instructions tooconfigure PowerShell for Azure Stack.</span></span> <span data-ttu-id="d2e22-108">不過，如果您想 tooquickly 安裝並設定 PowerShell 時，您可以使用提供 hello hello 指令碼[取得啟動並執行使用 PowerShell](azure-stack-powershell-configure-quickstart.md)主題。</span><span class="sxs-lookup"><span data-stu-id="d2e22-108">However, if you want tooquickly install and configure PowerShell, you can use hello script provided in hello [Get up and running with PowerShell](azure-stack-powershell-configure-quickstart.md) topic.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d2e22-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="d2e22-109">Prerequisites</span></span>
* <span data-ttu-id="d2e22-110">安裝 [Azure Stack 相容的 Azure PowerShell 模組](azure-stack-powershell-install.md)。</span><span class="sxs-lookup"><span data-stu-id="d2e22-110">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
* <span data-ttu-id="d2e22-111">下載 hello [Azure 堆疊的工具需要的 toowork](azure-stack-powershell-download.md)。</span><span class="sxs-lookup"><span data-stu-id="d2e22-111">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span>  

## <a name="import-hello-connect-powershell-module"></a><span data-ttu-id="d2e22-112">匯入 hello Connect PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="d2e22-112">Import hello Connect PowerShell module</span></span>

<span data-ttu-id="d2e22-113">下載所需的 hello 之後工具，巡覽 toohello 下載資料夾，然後匯入 hello**連接**PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="d2e22-113">After you download hello required tools, navigate toohello downloaded folder and import hello **Connect** PowerShell module.</span></span> <span data-ttu-id="d2e22-114">tooimport hello Connect 模組，執行下列命令，在提升權限的 PowerShell 工作階段中的 hello:</span><span class="sxs-lookup"><span data-stu-id="d2e22-114">tooimport hello Connect module, run hello following command in an elevated PowerShell session:</span></span>

```PowerShell
Set-ExecutionPolicy RemoteSigned
Import-Module .\Connect\AzureStack.Connect.psm1
```

## <a name="configure-hello-powershell-environment"></a><span data-ttu-id="d2e22-115">設定 hello PowerShell 環境</span><span class="sxs-lookup"><span data-stu-id="d2e22-115">Configure hello PowerShell environment</span></span>

<span data-ttu-id="d2e22-116">tooconfigure Azure 堆疊環境中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="d2e22-116">tooconfigure your Azure Stack environment, do hello following:</span></span>

1. <span data-ttu-id="d2e22-117">註冊您 Azure 堆疊的執行個體使用其中一種 hello 下列指令程式為目標的 AzureRM 環境：</span><span class="sxs-lookup"><span data-stu-id="d2e22-117">Register an AzureRM environment that targets your Azure Stack instance by using one of hello following cmdlets:</span></span>

   * <span data-ttu-id="d2e22-118">**雲端系統管理環境**</span><span class="sxs-lookup"><span data-stu-id="d2e22-118">**Cloud administrative environment**</span></span>

       ```PowerShell
       Add-AzureRMEnvironment `
         -Name "AzureStackAdmin" `
         -ArmEndpoint "https://adminmanagement.local.azurestack.external"
       ```

   * <span data-ttu-id="d2e22-119">**使用者環境**</span><span class="sxs-lookup"><span data-stu-id="d2e22-119">**User environment**</span></span>

       ```PowerShell
       Add-AzureRMEnvironment `
         -Name "AzureStackUser" `
         -ArmEndpoint "https://management.local.azurestack.external" 
       ```
   
   <span data-ttu-id="d2e22-120">您已註冊 hello AzureRM 環境之後，您可以使用 Azure 堆疊環境中的所有 hello AzureRM cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d2e22-120">After you've registered hello AzureRM environment, you can use all hello AzureRM cmdlets in your Azure Stack environment.</span></span> <span data-ttu-id="d2e22-121">hello 的 hello 前一個 cmdlet 的輸出是以 hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="d2e22-121">hello output of hello previous cmdlet is shown in hello following screenshot:</span></span>

   ![取得環境的詳細資料](media/azure-stack-powershell-configure/getenvdetails.png)

2. <span data-ttu-id="d2e22-123">設定 hello GraphEndpointResourceId 值使用其中一種 hello 下列 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d2e22-123">Set hello GraphEndpointResourceId value by using one of hello following cmdlets:</span></span>
   
   * <span data-ttu-id="d2e22-124">**Azure Active Directory (Azure AD)**</span><span class="sxs-lookup"><span data-stu-id="d2e22-124">**Azure Active Directory (Azure AD)**</span></span>
   
      * <span data-ttu-id="d2e22-125">Hello**雲端系統管理環境**，使用：</span><span class="sxs-lookup"><span data-stu-id="d2e22-125">For hello **cloud administrative environment**, use:</span></span>
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackAdmin" `
          -GraphAudience "https://graph.windows.net/"
        ```
        
      * <span data-ttu-id="d2e22-126">Hello**使用者環境**，使用：</span><span class="sxs-lookup"><span data-stu-id="d2e22-126">For hello **user environment**, use:</span></span>
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackUser" `
          -GraphAudience "https://graph.windows.net/"
        ```

   * <span data-ttu-id="d2e22-127">**Active Directory Federation Services**</span><span class="sxs-lookup"><span data-stu-id="d2e22-127">**Active Directory Federation Services**</span></span>
   
      * <span data-ttu-id="d2e22-128">Hello**雲端系統管理環境**，使用：</span><span class="sxs-lookup"><span data-stu-id="d2e22-128">For hello **cloud administrative environment**, use:</span></span>
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackAdmin" `
          -GraphAudience "https://graph.local.azurestack.external/" `
          -EnableAdfsAuthentication:$true
        ```
        
      * <span data-ttu-id="d2e22-129">Hello**使用者環境**，使用：</span><span class="sxs-lookup"><span data-stu-id="d2e22-129">For hello **user environment**, use:</span></span>
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackUser" `
          -GraphAudience "https://graph.local.azurestack.external/" `
          -EnableAdfsAuthentication:$true
        ```

3. <span data-ttu-id="d2e22-130">取得 hello 是使用的 toodeploy Azure 堆疊的 hello Active Directory 租用戶的 GUID 值。</span><span class="sxs-lookup"><span data-stu-id="d2e22-130">Get hello GUID value of hello Active Directory tenant that is used toodeploy Azure Stack.</span></span> <span data-ttu-id="d2e22-131">如果您可以使用部署 Azure 堆疊環境：</span><span class="sxs-lookup"><span data-stu-id="d2e22-131">If your Azure Stack environment is deployed by using:</span></span>  

   * <span data-ttu-id="d2e22-132">**Azure Active Directory (Azure AD)**</span><span class="sxs-lookup"><span data-stu-id="d2e22-132">**Azure Active Directory (Azure AD)**</span></span>
   
      * <span data-ttu-id="d2e22-133">tooaccess hello**雲端系統管理環境**，使用：</span><span class="sxs-lookup"><span data-stu-id="d2e22-133">tooaccess hello **cloud administrative environment**, use:</span></span>
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
          -EnvironmentName "AzureStackAdmin"
        ```

      * <span data-ttu-id="d2e22-134">tooaccess hello**使用者環境**，使用：</span><span class="sxs-lookup"><span data-stu-id="d2e22-134">tooaccess hello **user environment**, use:</span></span>
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
          -EnvironmentName "AzureStackUser"
        ```

   * <span data-ttu-id="d2e22-135">**Active Directory Federation Services**</span><span class="sxs-lookup"><span data-stu-id="d2e22-135">**Active Directory Federation Services**</span></span>
   
      * <span data-ttu-id="d2e22-136">tooaccess hello**雲端系統管理環境**，使用：</span><span class="sxs-lookup"><span data-stu-id="d2e22-136">tooaccess hello **cloud administrative environment**, use:</span></span>
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -ADFS `
          -EnvironmentName "AzureStackAdmin"
        ```

      * <span data-ttu-id="d2e22-137">tooaccess hello**使用者環境**，使用：</span><span class="sxs-lookup"><span data-stu-id="d2e22-137">tooaccess hello **user environment**, use:</span></span>
        ```PowerShell 
        $TenantID = Get-AzsDirectoryTenantId `
          -ADFS `
          -EnvironmentName "AzureStackUser" 
        ```

## <a name="sign-in-tooazure-stack"></a><span data-ttu-id="d2e22-138">登入 tooAzure 堆疊</span><span class="sxs-lookup"><span data-stu-id="d2e22-138">Sign in tooAzure Stack</span></span>

<span data-ttu-id="d2e22-139">使用登入 toohello Azure 堆疊環境的 hello 下列兩個 cmdlet 其中一個：</span><span class="sxs-lookup"><span data-stu-id="d2e22-139">Sign in toohello Azure Stack environment by using one of hello following two cmdlets:</span></span>

   * <span data-ttu-id="d2e22-140">在 toohello toosign**系統管理網站**，使用：</span><span class="sxs-lookup"><span data-stu-id="d2e22-140">toosign in toohello **administrative portal**, use:</span></span>
    
       ```PowerShell
       Login-AzureRmAccount `
         -EnvironmentName "AzureStackAdmin" `
         -TenantId $TenantID 
       ```

   * <span data-ttu-id="d2e22-141">在 toohello toosign**使用者入口網站**，使用：</span><span class="sxs-lookup"><span data-stu-id="d2e22-141">toosign in toohello **user portal**, use:</span></span>

       ```PowerShell
       Login-AzureRmAccount `
         -EnvironmentName "AzureStackUser" `
         -TenantId $TenantID 
       ```

## <a name="register-resource-providers"></a><span data-ttu-id="d2e22-142">註冊資源提供者</span><span class="sxs-lookup"><span data-stu-id="d2e22-142">Register resource providers</span></span>

<span data-ttu-id="d2e22-143">登入 toohello 系統管理員或使用者入口網站後，您可以發出對 hello 註冊資源提供者執行的作業。</span><span class="sxs-lookup"><span data-stu-id="d2e22-143">After you sign in toohello administrator or user portal, you can issue operations against hello registered resource providers.</span></span> <span data-ttu-id="d2e22-144">根據預設，所有的 hello 基礎資源提供者都登錄在 hello 預設提供者訂用帳戶 （hello 雲端系統管理員的訂用帳戶）。</span><span class="sxs-lookup"><span data-stu-id="d2e22-144">By default, all hello foundational resource providers are registered in hello Default Provider Subscription (hello cloud administrator's subscription).</span></span>

<span data-ttu-id="d2e22-145">當您操作沒有任何透過 hello 入口網站部署的資源，新建立的使用者訂用帳戶的 hello 資源提供者不是自動註冊。</span><span class="sxs-lookup"><span data-stu-id="d2e22-145">When you operate on a newly created user subscription, which doesn’t have any resources deployed through hello portal, hello resource providers aren't automatically registered.</span></span> <span data-ttu-id="d2e22-146">您應該明確地註冊 hello 資源提供者，使用下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="d2e22-146">You should explicitly register hello resource providers by using hello following script:</span></span>

```powershell

foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```


## <a name="next-steps"></a><span data-ttu-id="d2e22-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d2e22-147">Next steps</span></span>
* [<span data-ttu-id="d2e22-148">開發適用於 Azure Stack 的範本</span><span class="sxs-lookup"><span data-stu-id="d2e22-148">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
* [<span data-ttu-id="d2e22-149">使用 PowerShell 部署範本</span><span class="sxs-lookup"><span data-stu-id="d2e22-149">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)

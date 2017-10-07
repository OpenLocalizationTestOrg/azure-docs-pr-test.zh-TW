---
title: "aaaConfigure hello Azure 堆疊使用者的 PowerShell 環境 |Microsoft 文件"
description: "設定 hello Azure 堆疊使用者的 PowerShell 環境"
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
ms.date: 08/18/2017
ms.author: sngun
ms.openlocfilehash: 8e7ccea24a1917d349ab06e0abe29f534b47b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-azure-stack-users-powershell-environment"></a><span data-ttu-id="fb421-103">設定 hello Azure 堆疊使用者的 PowerShell 環境</span><span class="sxs-lookup"><span data-stu-id="fb421-103">Configure hello Azure Stack user's PowerShell environment</span></span>

<span data-ttu-id="fb421-104">作為 Azure Stack 使用者，您可以設定您 Azure Stack 開發套件的 PowerShell 環境。</span><span class="sxs-lookup"><span data-stu-id="fb421-104">As an Azure Stack user, you can configure your Azure Stack Development Kit's PowerShell environment.</span></span> <span data-ttu-id="fb421-105">設定之後，您可以使用 PowerShell toomanage 堆疊 Azure 資源，例如訂閱 toooffers、 建立虛擬機器、 部署 Azure 資源管理員範本等。本主題是已設定領域的 toouse 與僅限 hello 使用者環境，如果您想要設定 PowerShell tooset hello 雲端運算子環境，請參閱 toohello[設定 hello Azure 堆疊操作員的 PowerShell 環境](azure-stack-powershell-configure-admin.md)主題。</span><span class="sxs-lookup"><span data-stu-id="fb421-105">After you configure, you can use PowerShell toomanage Azure Stack resources such as subscribe toooffers, create virtual machines, deploy Azure Resource Manager templates,  etc. This topic is scoped toouse with hello user environments only, if you want tooset up PowerShell for hello cloud operator environment, refer toohello [Configure hello Azure Stack operator's PowerShell environment](azure-stack-powershell-configure-admin.md) topic.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fb421-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="fb421-106">Prerequisites</span></span> 

<span data-ttu-id="fb421-107">執行下列必要條件 hello 從 hello[開發套件](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop)，或從 Windows 的外部用戶端如果您是[透過 VPN 連線](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span><span class="sxs-lookup"><span data-stu-id="fb421-107">Run hello following prerequisites either from hello [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="fb421-108">安裝 [Azure Stack 相容的 Azure PowerShell 模組](azure-stack-powershell-install.md)。</span><span class="sxs-lookup"><span data-stu-id="fb421-108">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
* <span data-ttu-id="fb421-109">下載 hello [Azure 堆疊的工具需要的 toowork](azure-stack-powershell-download.md)。</span><span class="sxs-lookup"><span data-stu-id="fb421-109">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span> 

## <a name="configure-hello-user-environment-and-sign-in-tooazure-stack"></a><span data-ttu-id="fb421-110">設定 hello 使用者環境並登入 tooAzure 堆疊</span><span class="sxs-lookup"><span data-stu-id="fb421-110">Configure hello user environment and sign in tooAzure Stack</span></span>

<span data-ttu-id="fb421-111">根據部署 (Azure AD 或 AD FS)，執行下列指令碼 tooconfigure PowerShell 的 Azure 堆疊 hello hello 類型：</span><span class="sxs-lookup"><span data-stu-id="fb421-111">Based on hello type of deployment (Azure AD or AD FS), run one of hello following script tooconfigure PowerShell for Azure Stack:</span></span>

### <a name="azure-active-directory-aad-based-deployments"></a><span data-ttu-id="fb421-112">以 Azure Active Directory (AAD) 為基礎的驗證</span><span class="sxs-lookup"><span data-stu-id="fb421-112">Azure Active Directory (AAD) based deployments</span></span>
       
  ```powershell
  # Navigate toohello downloaded folder and import hello **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackUser" `
    -ArmEndpoint "https://management.local.azurestack.external"

  # Set hello GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackUser" `
    -GraphAudience "https://graph.windows.net/"

  # Get hello Active Directory tenantId that is used toodeploy Azure Stack
  $TenantID = Get-AzsDirectoryTenantId `
    -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
    -EnvironmentName "AzureStackUser"

  # Sign in tooyour environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackUser" `
    -TenantId $TenantID 
   ```

### <a name="active-directory-federation-services-ad-fs-based-deployments"></a><span data-ttu-id="fb421-113">以 Active Directory Federation Services (AD FS) 為基礎的部署</span><span class="sxs-lookup"><span data-stu-id="fb421-113">Active Directory Federation Services (AD FS) based deployments</span></span> 
          
  ```powershell
  # Navigate toohello downloaded folder and import hello **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackUser" `
    -ArmEndpoint "https://management.local.azurestack.external"

  # Set hello GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackUser" `
    -GraphAudience "https://graph.local.azurestack.external/" `
    -EnableAdfsAuthentication:$true

  # Get hello Active Directory tenantId that is used toodeploy Azure Stack     
  $TenantID = Get-AzsDirectoryTenantId `
    -ADFS `
    -EnvironmentName "AzureStackUser"

  # Sign in tooyour environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackUser" `
    -TenantId $TenantID 
  ```

## <a name="register-resource-providers"></a><span data-ttu-id="fb421-114">註冊資源提供者</span><span class="sxs-lookup"><span data-stu-id="fb421-114">Register resource providers</span></span>

<span data-ttu-id="fb421-115">新建立的使用者訂用帳戶沒有任何透過 hello 入口網站部署的資源時，不自動註冊 hello 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="fb421-115">When operating on a newly created user subscription that doesn’t have any resources deployed through hello portal, hello resource providers aren't automatically registered.</span></span> <span data-ttu-id="fb421-116">您應該明確地進行註冊使用下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="fb421-116">You should explicitly register them by using hello following script:</span></span>

```powershell
foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```

## <a name="test-hello-connectivity"></a><span data-ttu-id="fb421-117">測試 hello 連線</span><span class="sxs-lookup"><span data-stu-id="fb421-117">Test hello connectivity</span></span>

<span data-ttu-id="fb421-118">現在我們有設定的所有項目，讓我們使用 Azure 堆疊內的 PowerShell toocreate 資源。</span><span class="sxs-lookup"><span data-stu-id="fb421-118">Now that we've got everything set up, let's use PowerShell toocreate resources within Azure Stack.</span></span> <span data-ttu-id="fb421-119">例如，您可以建立應用程式的資源群組，並新增虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fb421-119">For example, you can create a resource group for an application and add a virtual machine.</span></span> <span data-ttu-id="fb421-120">使用下列命令 toocreate 資源群組的 hello 名為"MyResourceGroup 」:</span><span class="sxs-lookup"><span data-stu-id="fb421-120">Use hello following command toocreate a resource group named "MyResourceGroup":</span></span>

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a><span data-ttu-id="fb421-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fb421-121">Next steps</span></span>
* [<span data-ttu-id="fb421-122">開發適用於 Azure Stack 的範本</span><span class="sxs-lookup"><span data-stu-id="fb421-122">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
* [<span data-ttu-id="fb421-123">使用 PowerShell 部署範本</span><span class="sxs-lookup"><span data-stu-id="fb421-123">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)

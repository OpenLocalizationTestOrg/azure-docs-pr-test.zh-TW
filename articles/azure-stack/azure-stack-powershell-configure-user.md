---
title: "設定 Azure Stack 使用者的 PowerShell 環境 | Microsoft Docs"
description: "設定 Azure Stack 使用者的 PowerShell 環境"
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
ms.openlocfilehash: dabbd83fb35397f2cf90fac5957d299f0c5d446e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configure-the-azure-stack-users-powershell-environment"></a><span data-ttu-id="1be4b-103">設定 Azure Stack 使用者的 PowerShell 環境</span><span class="sxs-lookup"><span data-stu-id="1be4b-103">Configure the Azure Stack user's PowerShell environment</span></span>

<span data-ttu-id="1be4b-104">作為 Azure Stack 使用者，您可以設定您 Azure Stack 開發套件的 PowerShell 環境。</span><span class="sxs-lookup"><span data-stu-id="1be4b-104">As an Azure Stack user, you can configure your Azure Stack Development Kit's PowerShell environment.</span></span> <span data-ttu-id="1be4b-105">設定之後，可以使用 PowerShell 管理 Azure Stack 資源，例如訂閱產品、建立虛擬機器、部署 Azure Resource Manager 範本等。本主題僅說明使用者環境的使用，若要為雲端操作員環境設定 PowerShell，請參閱[設定 Azure Stack 操作員的 PowerShell 環境](azure-stack-powershell-configure-admin.md)主題。</span><span class="sxs-lookup"><span data-stu-id="1be4b-105">After you configure, you can use PowerShell to manage Azure Stack resources such as subscribe to offers, create virtual machines, deploy Azure Resource Manager templates,  etc. This topic is scoped to use with the user environments only, if you want to set up PowerShell for the cloud operator environment, refer to the [Configure the Azure Stack operator's PowerShell environment](azure-stack-powershell-configure-admin.md) topic.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1be4b-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="1be4b-106">Prerequisites</span></span> 

<span data-ttu-id="1be4b-107">從[開發套件](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop)，或從 Windows 型外部用戶端 (如果您是[透過 VPN 連線](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn))，執行下列先決條件：</span><span class="sxs-lookup"><span data-stu-id="1be4b-107">Run the following prerequisites either from the [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="1be4b-108">安裝 [Azure Stack 相容的 Azure PowerShell 模組](azure-stack-powershell-install.md)。</span><span class="sxs-lookup"><span data-stu-id="1be4b-108">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  
* <span data-ttu-id="1be4b-109">下載[處理 Azure Stack 所需的工具](azure-stack-powershell-download.md)。</span><span class="sxs-lookup"><span data-stu-id="1be4b-109">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span> 

## <a name="configure-the-user-environment-and-sign-in-to-azure-stack"></a><span data-ttu-id="1be4b-110">設定使用者環境並登入 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="1be4b-110">Configure the user environment and sign in to Azure Stack</span></span>

<span data-ttu-id="1be4b-111">根據部署類型 (Azure AD 或 AD FS)，執行下列其中一個指令碼來設定 Azure Stack 的 PowerShell：</span><span class="sxs-lookup"><span data-stu-id="1be4b-111">Based on the type of deployment (Azure AD or AD FS), run one of the following script to configure PowerShell for Azure Stack:</span></span>

### <a name="azure-active-directory-aad-based-deployments"></a><span data-ttu-id="1be4b-112">以 Azure Active Directory (AAD) 為基礎的驗證</span><span class="sxs-lookup"><span data-stu-id="1be4b-112">Azure Active Directory (AAD) based deployments</span></span>
       
  ```powershell
  # Navigate to the downloaded folder and import the **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackUser" `
    -ArmEndpoint "https://management.local.azurestack.external"

  # Set the GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackUser" `
    -GraphAudience "https://graph.windows.net/"

  # Get the Active Directory tenantId that is used to deploy Azure Stack
  $TenantID = Get-AzsDirectoryTenantId `
    -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
    -EnvironmentName "AzureStackUser"

  # Sign in to your environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackUser" `
    -TenantId $TenantID 
   ```

### <a name="active-directory-federation-services-ad-fs-based-deployments"></a><span data-ttu-id="1be4b-113">以 Active Directory Federation Services (AD FS) 為基礎的部署</span><span class="sxs-lookup"><span data-stu-id="1be4b-113">Active Directory Federation Services (AD FS) based deployments</span></span> 
          
  ```powershell
  # Navigate to the downloaded folder and import the **Connect** PowerShell module
  Set-ExecutionPolicy RemoteSigned
  Import-Module .\Connect\AzureStack.Connect.psm1

  # Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackUser" `
    -ArmEndpoint "https://management.local.azurestack.external"

  # Set the GraphEndpointResourceId value
  Set-AzureRmEnvironment `
    -Name "AzureStackUser" `
    -GraphAudience "https://graph.local.azurestack.external/" `
    -EnableAdfsAuthentication:$true

  # Get the Active Directory tenantId that is used to deploy Azure Stack     
  $TenantID = Get-AzsDirectoryTenantId `
    -ADFS `
    -EnvironmentName "AzureStackUser"

  # Sign in to your environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackUser" `
    -TenantId $TenantID 
  ```

## <a name="register-resource-providers"></a><span data-ttu-id="1be4b-114">註冊資源提供者</span><span class="sxs-lookup"><span data-stu-id="1be4b-114">Register resource providers</span></span>

<span data-ttu-id="1be4b-115">在新建的使用者訂用帳戶 (沒有透過入口網站部署任何資源) 上操作時，不會自動註冊資源提供者。</span><span class="sxs-lookup"><span data-stu-id="1be4b-115">When operating on a newly created user subscription that doesn’t have any resources deployed through the portal, the resource providers aren't automatically registered.</span></span> <span data-ttu-id="1be4b-116">您應使用下列指令碼明確地進行註冊：</span><span class="sxs-lookup"><span data-stu-id="1be4b-116">You should explicitly register them by using the following script:</span></span>

```powershell
foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```

## <a name="test-the-connectivity"></a><span data-ttu-id="1be4b-117">測試連線</span><span class="sxs-lookup"><span data-stu-id="1be4b-117">Test the connectivity</span></span>

<span data-ttu-id="1be4b-118">一切都已準備就緒，接下來我們要使用 PowerShell 在 Azure Stack 中建立資源。</span><span class="sxs-lookup"><span data-stu-id="1be4b-118">Now that we've got everything set up, let's use PowerShell to create resources within Azure Stack.</span></span> <span data-ttu-id="1be4b-119">例如，您可以建立應用程式的資源群組，並新增虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1be4b-119">For example, you can create a resource group for an application and add a virtual machine.</span></span> <span data-ttu-id="1be4b-120">若要建立名為 "MyResourceGroup" 的資源群組，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="1be4b-120">Use the following command to create a resource group named "MyResourceGroup":</span></span>

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a><span data-ttu-id="1be4b-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1be4b-121">Next steps</span></span>
* [<span data-ttu-id="1be4b-122">開發適用於 Azure Stack 的範本</span><span class="sxs-lookup"><span data-stu-id="1be4b-122">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
* [<span data-ttu-id="1be4b-123">使用 PowerShell 部署範本</span><span class="sxs-lookup"><span data-stu-id="1be4b-123">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)

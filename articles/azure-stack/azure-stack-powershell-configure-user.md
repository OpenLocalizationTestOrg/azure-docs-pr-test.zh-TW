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
# <a name="configure-the-azure-stack-users-powershell-environment"></a>設定 Azure Stack 使用者的 PowerShell 環境

作為 Azure Stack 使用者，您可以設定您 Azure Stack 開發套件的 PowerShell 環境。 設定之後，可以使用 PowerShell 管理 Azure Stack 資源，例如訂閱產品、建立虛擬機器、部署 Azure Resource Manager 範本等。本主題僅說明使用者環境的使用，若要為雲端操作員環境設定 PowerShell，請參閱[設定 Azure Stack 操作員的 PowerShell 環境](azure-stack-powershell-configure-admin.md)主題。 

## <a name="prerequisites"></a>必要條件 

從[開發套件](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop)，或從 Windows 型外部用戶端 (如果您是[透過 VPN 連線](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn))，執行下列先決條件：

* 安裝 [Azure Stack 相容的 Azure PowerShell 模組](azure-stack-powershell-install.md)。  
* 下載[處理 Azure Stack 所需的工具](azure-stack-powershell-download.md)。 

## <a name="configure-the-user-environment-and-sign-in-to-azure-stack"></a>設定使用者環境並登入 Azure Stack

根據部署類型 (Azure AD 或 AD FS)，執行下列其中一個指令碼來設定 Azure Stack 的 PowerShell：

### <a name="azure-active-directory-aad-based-deployments"></a>以 Azure Active Directory (AAD) 為基礎的驗證
       
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

### <a name="active-directory-federation-services-ad-fs-based-deployments"></a>以 Active Directory Federation Services (AD FS) 為基礎的部署 
          
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

## <a name="register-resource-providers"></a>註冊資源提供者

在新建的使用者訂用帳戶 (沒有透過入口網站部署任何資源) 上操作時，不會自動註冊資源提供者。 您應使用下列指令碼明確地進行註冊：

```powershell
foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```

## <a name="test-the-connectivity"></a>測試連線

一切都已準備就緒，接下來我們要使用 PowerShell 在 Azure Stack 中建立資源。 例如，您可以建立應用程式的資源群組，並新增虛擬機器。 若要建立名為 "MyResourceGroup" 的資源群組，請使用下列命令：

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a>後續步驟
* [開發適用於 Azure Stack 的範本](azure-stack-develop-templates.md)
* [使用 PowerShell 部署範本](azure-stack-deploy-template-powershell.md)
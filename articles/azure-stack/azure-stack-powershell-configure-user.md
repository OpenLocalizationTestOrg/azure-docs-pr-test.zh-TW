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
# <a name="configure-hello-azure-stack-users-powershell-environment"></a>設定 hello Azure 堆疊使用者的 PowerShell 環境

作為 Azure Stack 使用者，您可以設定您 Azure Stack 開發套件的 PowerShell 環境。 設定之後，您可以使用 PowerShell toomanage 堆疊 Azure 資源，例如訂閱 toooffers、 建立虛擬機器、 部署 Azure 資源管理員範本等。本主題是已設定領域的 toouse 與僅限 hello 使用者環境，如果您想要設定 PowerShell tooset hello 雲端運算子環境，請參閱 toohello[設定 hello Azure 堆疊操作員的 PowerShell 環境](azure-stack-powershell-configure-admin.md)主題。 

## <a name="prerequisites"></a>必要條件 

執行下列必要條件 hello 從 hello[開發套件](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop)，或從 Windows 的外部用戶端如果您是[透過 VPN 連線](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):

* 安裝 [Azure Stack 相容的 Azure PowerShell 模組](azure-stack-powershell-install.md)。  
* 下載 hello [Azure 堆疊的工具需要的 toowork](azure-stack-powershell-download.md)。 

## <a name="configure-hello-user-environment-and-sign-in-tooazure-stack"></a>設定 hello 使用者環境並登入 tooAzure 堆疊

根據部署 (Azure AD 或 AD FS)，執行下列指令碼 tooconfigure PowerShell 的 Azure 堆疊 hello hello 類型：

### <a name="azure-active-directory-aad-based-deployments"></a>以 Azure Active Directory (AAD) 為基礎的驗證
       
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

### <a name="active-directory-federation-services-ad-fs-based-deployments"></a>以 Active Directory Federation Services (AD FS) 為基礎的部署 
          
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

## <a name="register-resource-providers"></a>註冊資源提供者

新建立的使用者訂用帳戶沒有任何透過 hello 入口網站部署的資源時，不自動註冊 hello 資源提供者。 您應該明確地進行註冊使用下列指令碼的 hello:

```powershell
foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```

## <a name="test-hello-connectivity"></a>測試 hello 連線

現在我們有設定的所有項目，讓我們使用 Azure 堆疊內的 PowerShell toocreate 資源。 例如，您可以建立應用程式的資源群組，並新增虛擬機器。 使用下列命令 toocreate 資源群組的 hello 名為"MyResourceGroup 」:

```powershell
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a>後續步驟
* [開發適用於 Azure Stack 的範本](azure-stack-develop-templates.md)
* [使用 PowerShell 部署範本](azure-stack-deploy-template-powershell.md)

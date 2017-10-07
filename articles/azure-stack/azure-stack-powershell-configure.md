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
# <a name="configure-powershell-for-use-with-azure-stack"></a>設定 Azure 堆疊搭配使用 PowerShell 

本文將說明使用 PowerShell hello 步驟需要的 tooconnect tooan Azure 堆疊開發套件執行個體。 您連接之後，您可以存取 hello 入口網站，並部署透過 PowerShell 的資源。 您可以使用本文從 hello 開發套件，或是從 windows 的外部用戶端中所述，如果您透過 VPN 連線的 hello 步驟。

這篇文章包含詳細指示 tooconfigure PowerShell 的 Azure 堆疊。 不過，如果您想 tooquickly 安裝並設定 PowerShell 時，您可以使用提供 hello hello 指令碼[取得啟動並執行使用 PowerShell](azure-stack-powershell-configure-quickstart.md)主題。 

## <a name="prerequisites"></a>必要條件
* 安裝 [Azure Stack 相容的 Azure PowerShell 模組](azure-stack-powershell-install.md)。  
* 下載 hello [Azure 堆疊的工具需要的 toowork](azure-stack-powershell-download.md)。  

## <a name="import-hello-connect-powershell-module"></a>匯入 hello Connect PowerShell 模組

下載所需的 hello 之後工具，巡覽 toohello 下載資料夾，然後匯入 hello**連接**PowerShell 模組。 tooimport hello Connect 模組，執行下列命令，在提升權限的 PowerShell 工作階段中的 hello:

```PowerShell
Set-ExecutionPolicy RemoteSigned
Import-Module .\Connect\AzureStack.Connect.psm1
```

## <a name="configure-hello-powershell-environment"></a>設定 hello PowerShell 環境

tooconfigure Azure 堆疊環境中，執行下列 hello:

1. 註冊您 Azure 堆疊的執行個體使用其中一種 hello 下列指令程式為目標的 AzureRM 環境：

   * **雲端系統管理環境**

       ```PowerShell
       Add-AzureRMEnvironment `
         -Name "AzureStackAdmin" `
         -ArmEndpoint "https://adminmanagement.local.azurestack.external"
       ```

   * **使用者環境**

       ```PowerShell
       Add-AzureRMEnvironment `
         -Name "AzureStackUser" `
         -ArmEndpoint "https://management.local.azurestack.external" 
       ```
   
   您已註冊 hello AzureRM 環境之後，您可以使用 Azure 堆疊環境中的所有 hello AzureRM cmdlet。 hello 的 hello 前一個 cmdlet 的輸出是以 hello 下列螢幕擷取畫面所示：

   ![取得環境的詳細資料](media/azure-stack-powershell-configure/getenvdetails.png)

2. 設定 hello GraphEndpointResourceId 值使用其中一種 hello 下列 cmdlet:
   
   * **Azure Active Directory (Azure AD)**
   
      * Hello**雲端系統管理環境**，使用：
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackAdmin" `
          -GraphAudience "https://graph.windows.net/"
        ```
        
      * Hello**使用者環境**，使用：
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackUser" `
          -GraphAudience "https://graph.windows.net/"
        ```

   * **Active Directory Federation Services**
   
      * Hello**雲端系統管理環境**，使用：
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackAdmin" `
          -GraphAudience "https://graph.local.azurestack.external/" `
          -EnableAdfsAuthentication:$true
        ```
        
      * Hello**使用者環境**，使用：
        ```powershell
        Set-AzureRmEnvironment `
          -Name "AzureStackUser" `
          -GraphAudience "https://graph.local.azurestack.external/" `
          -EnableAdfsAuthentication:$true
        ```

3. 取得 hello 是使用的 toodeploy Azure 堆疊的 hello Active Directory 租用戶的 GUID 值。 如果您可以使用部署 Azure 堆疊環境：  

   * **Azure Active Directory (Azure AD)**
   
      * tooaccess hello**雲端系統管理環境**，使用：
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
          -EnvironmentName "AzureStackAdmin"
        ```

      * tooaccess hello**使用者環境**，使用：
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
          -EnvironmentName "AzureStackUser"
        ```

   * **Active Directory Federation Services**
   
      * tooaccess hello**雲端系統管理環境**，使用：
        ```PowerShell
        $TenantID = Get-AzsDirectoryTenantId `
          -ADFS `
          -EnvironmentName "AzureStackAdmin"
        ```

      * tooaccess hello**使用者環境**，使用：
        ```PowerShell 
        $TenantID = Get-AzsDirectoryTenantId `
          -ADFS `
          -EnvironmentName "AzureStackUser" 
        ```

## <a name="sign-in-tooazure-stack"></a>登入 tooAzure 堆疊

使用登入 toohello Azure 堆疊環境的 hello 下列兩個 cmdlet 其中一個：

   * 在 toohello toosign**系統管理網站**，使用：
    
       ```PowerShell
       Login-AzureRmAccount `
         -EnvironmentName "AzureStackAdmin" `
         -TenantId $TenantID 
       ```

   * 在 toohello toosign**使用者入口網站**，使用：

       ```PowerShell
       Login-AzureRmAccount `
         -EnvironmentName "AzureStackUser" `
         -TenantId $TenantID 
       ```

## <a name="register-resource-providers"></a>註冊資源提供者

登入 toohello 系統管理員或使用者入口網站後，您可以發出對 hello 註冊資源提供者執行的作業。 根據預設，所有的 hello 基礎資源提供者都登錄在 hello 預設提供者訂用帳戶 （hello 雲端系統管理員的訂用帳戶）。

當您操作沒有任何透過 hello 入口網站部署的資源，新建立的使用者訂用帳戶的 hello 資源提供者不是自動註冊。 您應該明確地註冊 hello 資源提供者，使用下列指令碼的 hello:

```powershell

foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    } 
```


## <a name="next-steps"></a>後續步驟
* [開發適用於 Azure Stack 的範本](azure-stack-develop-templates.md)
* [使用 PowerShell 部署範本](azure-stack-deploy-template-powershell.md)

---
title: "aaaRegister Azure 堆疊 |Microsoft 文件"
description: "使用您的 Azure 訂用帳戶註冊 Azure Stack。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: erikje
ms.openlocfilehash: 3a3c8e82bec3e1e26ecfe591ecc27b2b91f6f91e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="register-azure-stack-with-your-azure-subscription"></a>使用您的 Azure 訂用帳戶註冊 Azure Stack

Azure Active Directory 部署，您可以向 Azure 堆疊從 Azure 和商務資料回報 tooMicrosoft tooset Azure toodownload marketplace 項目。 

> [!NOTE]
>建議註冊，因為它可讓您 tootest 重要 Azure 堆疊功能，例如 marketplace 新聞訂閱和使用方式報表。 註冊 Azure 堆疊之後，用法就是報告的 tooAzure 商務。 您可以查看您用於註冊 hello 訂用帳戶底下。 Azure Stack 開發套件使用者將不需針對回報的任何使用方式支付費用。
>


## <a name="get-azure-subscription"></a>取得 Azure 訂用帳戶

使用 Azure 註冊 Azure Stack 之前，您必須：

- hello Azure 訂用帳戶的訂用帳戶 ID。 tooget hello ID，登入 tooAzure，按一下**更多服務** > **訂閱**，按一下您想要 toouse，hello 訂用帳戶，並在**Essentials**您可以尋找 hello**訂用帳戶 ID**。 目前不支援中國、德國，和美國政府雲端訂用帳戶。
- hello 使用者名稱和密碼是 hello 訂用帳戶擁有者的帳戶 （MSA/2FA 帳戶支援）
- hello hello Azure 訂用帳戶的 Azure Active Directory。 將滑鼠游標停留在您的顯示圖片在 hello 右上角的 hello Azure 入口網站，您可以在 Azure 中找到此目錄。 
- 已註冊的 hello Azure 堆疊資源提供者 (請參閱 hello**註冊的 Azure 堆疊資源提供者**下面章節以取得詳細資料)

如果您沒有符合這些需求的 Azure 訂用帳戶，則可以[在這裡建立免費的 Azure 帳戶](https://azure.microsoft.com/en-us/free/?b=17.06)。 註冊 Azure Stack 不會對您的 Azure 訂用帳戶收取任何費用。



## <a name="register-azure-stack-resource-provider-in-azure"></a>在 Azure 中註冊 Azure Stack 資源提供者
> [!NOTE] 
> 此步驟只需要 toobe 完成一次在 Azure 堆疊環境中。
>

1. 以系統管理員身分啟動 PowerShell ISE。
2. 登入 Azure 帳戶擁有者之 hello toohello Azure 訂用帳戶-EnvironmentName 參數設定得 「 AzureCloud"。
3. 註冊 hello Azure 資源提供者 」 Microsoft.AzureStack"。

範例： 
```Powershell
Login-AzureRmAccount -EnvironmentName "AzureCloud"
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.AzureStack -Force
```


## <a name="register-azure-stack-with-azure"></a>向 Azure 註冊 Azure Stack

> [!NOTE]
>所有的這些步驟必須完成 hello 主機電腦上。
>

1. [安裝適用於 Azure Stack 的 PowerShell](azure-stack-powershell-install.md)。 
2. 複製 hello [RegisterWithAzure.ps1 指令碼](https://go.microsoft.com/fwlink/?linkid=842959)tooa 資料夾 （例如 C:\Temp)。
3. 以系統管理員身分啟動 PowerShell ISE。    
4. 執行 hello RegisterWithAzure.ps1 指令碼，取代下列預留位置 hello:
    - *YourAccountName* hello hello Azure 訂用帳戶擁有者
    - *YourID*是您想要 toouse tooregister Azure 堆疊的 hello Azure 訂用帳戶 ID
    - *YourDirectory* hello 您 Azure 訂用帳戶所屬的 Azure Active Directory 租用戶名稱。

    ```powershell
    RegisterWithAzure.ps1 -azureSubscriptionId YourID -azureDirectoryTenantName YourDirectory -azureAccountId YourAccountName
    ```
    
    例如：
    
    ```powershell
    C:\temp\RegisterWithAzure.ps1 -azureSubscriptionId "5e0ae55d-0b7a-47a3-afbc-8b372650abd3" `
    -azureDirectoryTenantName "contoso.onmicrosoft.com" `
    -azureAccountId serviceadmin@contoso.onmicrosoft.com
    ```
    
5. 在 hello 兩個提示出現時，按 Enter 鍵。
6. 在 hello 登入快顯視窗中，輸入您 Azure 訂用帳戶的認證。

## <a name="verify-hello-registration"></a>確認 hello 註冊

1. 登入 toohello 管理員入口網站 (https://adminportal.local.azurestack.external)。
2. 按一下 [更多服務]  >  [市集管理]  >  [從 Azure 新增]。
3. 如果您看到 Azure 提供的項目清單 (例如 WordPress)，則表示啟用已成功。

## <a name="next-steps"></a>後續步驟

[連接 tooAzure 堆疊](azure-stack-connect-azure-stack.md)


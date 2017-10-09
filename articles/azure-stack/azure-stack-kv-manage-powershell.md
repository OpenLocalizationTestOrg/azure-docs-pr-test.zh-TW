---
title: "使用 PowerShell 的 Azure 堆疊中的金鑰保存庫 aaaManage |Microsoft 文件"
description: "深入了解如何使用 PowerShell 的 Azure 堆疊中的金鑰保存庫 toomanage。"
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
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 37adddf8da02766559f4d61134a9d5ce47377da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-in-azure-stack-using-powershell"></a>使用 PowerShell 管理 Azure Stack 中的金鑰保存庫

這篇文章可協助您取得啟動的 toocreate 並使用 PowerShell 管理 Azure 堆疊中的金鑰保存庫。 本文中所述的 hello 金鑰保存庫 PowerShell cmdlet 可用 hello Azure PowerShell SDK 的一部分。 hello 下列各節說明 hello PowerShell cmdlet 的必要的 toocreate 保存庫，儲存和管理密碼編譯金鑰和密碼，以及授權 hello 保存庫中的使用者或應用程式 tooinvoke 作業。 

## <a name="prerequisites"></a>必要條件
* [安裝適用於 Azure Stack 的 PowerShell](azure-stack-powershell-install.md)  
* Azure 堆疊雲端系統管理員必須具有[建立優惠](azure-stack-create-offer.md)包含 hello 金鑰保存庫服務。  
* 使用者必須[訂閱 tooan 優惠](azure-stack-subscribe-plan-provision-vm.md)包含 hello 金鑰保存庫服務。 
* [設定 hello Azure 堆疊使用者的 PowerShell 環境](azure-stack-powershell-configure-user.md)

## <a name="enable-your-tenant-subscription-for-vault-operations"></a>針對保存庫作業啟用您的租用戶訂用帳戶

您可以發出對金鑰保存庫的任何作業之前，您會需要您租用戶訂用帳戶已啟用的 tooensure 保存庫作業。 tooverify，執行下列命令的 hello:

```PowerShell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -Autosize
```
**輸出**

如果您的訂用帳戶已啟用保存庫作業，hello 輸出會顯示 「 RegistrationState 」 等於 「 已註冊 」 的金鑰保存庫的所有資源類型。

![註冊狀態](media/azure-stack-kv-manage-powershell/image1.png)

如果不是 hello 情況下，叫用下列命令 tooregister hello 金鑰保存庫服務您的訂用帳戶中的 hello:

```PowerShell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault
```

**輸出**

Hello 註冊成功時，如果 hello 會傳回下列輸出：

![註冊](media/azure-stack-kv-manage-powershell/image2.png)

hello 下列章節假設您金鑰保存庫服務註冊 hello 使用者訂用帳戶內。 當叫用金鑰保存庫命令，如果您收到錯誤:"hello 訂用帳戶未註冊的 toouse 命名空間 ' Microsoft.KeyVault"然後，請確認您有[啟用 hello 金鑰保存庫資源提供者](#enable-your-tenant-subscription-for-vault-operations)根據指示先前所述。

## <a name="create-a-key-vault"></a>建立金鑰保存庫 

建立金鑰保存庫之前，請先建立資源群組，使所有金鑰保存庫相關的資源都存在於資源群組中。 使用下列命令 toocreate 新的資源群組的 hello:

```PowerShell
New-AzureRmResourceGroup -Name “VaultRG” -Location local -verbose -Force

```

**輸出**

![新的資源群組](media/azure-stack-kv-manage-powershell/image3.png)

現在，使用 hello**新增 AzureRMKeyVault**命令 toocreate hello 您稍早建立的資源群組中的金鑰保存庫。 這個 Cmdlet 會讀取三個必要參數：資源群組名稱、金鑰保存庫名稱和地理位置。 

執行下列命令 toocreate hello 金鑰保存庫：

```PowerShell
New-AzureRmKeyVault -VaultName “Vault01” -ResourceGroupName “VaultRG” -Location local -verbose
```
**輸出**

![新增金鑰保存庫](media/azure-stack-kv-manage-powershell/image4.png)

hello 這個命令的輸出會顯示您所建立的 hello 金鑰保存庫 hello 屬性。 當應用程式存取此保存庫時，它會使用 hello**保存庫 URI** hello 輸出中所示的屬性。 比方說，是 hello 保存庫 URI 這裡**https://vault01.vault.local.azurestack.external**。 透過 REST API 與此金鑰保存庫互動的應用程式必須使用此 URI。

在以 ADFS 為基礎的部署中，使用 PowerShell 建立金鑰保存庫時，可能會收到警告，指出「未設定存取原則， 沒有使用者或應用程式有存取權限 toouse 此保存庫 」。 tooresolve 此問題，可以設定由 hello 保存庫的存取原則使用 hello [Set-azurermkeyvaultaccesspolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret)命令：

```PowerShell
# Obtain hello security identifier(SID) of hello active directory user
$adUser = Get-ADUser -Filter "Name -eq '{Active directory user name}'"
$objectSID = $adUser.SID.Value 

#Set hello key vault access policy
Set-AzureRmKeyVaultAccessPolicy -VaultName "{key vault name}" -ResourceGroupName "{resource group name}" -ObjectId "{object SID}" -PermissionsToKeys {permissionsToKeys} -PermissionsToSecrets {permissionsToSecrets} -BypassObjectIdValidation 
```

## <a name="manage-keys-and-secrets"></a>管理金鑰和祕密

建立保存庫之後, 使用下列步驟 toocreate hello 和管理金鑰和秘密 hello 保存庫中。

### <a name="create-a-key"></a>建立金鑰

使用 hello **Add-azurekeyvaultkey**命令 toocreate 或匯入軟體保護的金鑰在金鑰保存庫。 

```PowerShell
Add-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01” -verbose -Destination Software
```
hello**目的地**參數用 toospecify hello 金鑰是軟體保護。 已成功建立 hello 金鑰時，hello 命令會輸出 hello 的 hello 建立金鑰的詳細資料。

**輸出**

![新金鑰](media/azure-stack-kv-manage-powershell/image5.png)

您現在可以參考 hello 利用其 URI 建立金鑰。 如果您建立或匯入具有相同名稱做為現有的索引鍵的索引鍵，hello 原始金鑰的 hello 新機碼中指定的 hello 值來更新。  您可以使用 hello 特定版本，以存取 hello 前一版的 hello 金鑰的 URI。 例如， 

* 使用**https://vault10.vault.local.azurestack.external:443/索引鍵/key01** tooalways 取得 hello 目前版本  
* 使用**https://vault010.vault.local.azurestack.external:443/索引鍵/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** tooget 此特定版本

### <a name="get-a-key"></a>取得金鑰

使用 hello **Get AzureKeyVaultKey**命令 tooread 索引鍵和其詳細資料。

```PowerShell
Get-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01”
```

### <a name="create-a-secret"></a>建立祕密

使用 hello**組 AzureKeyVaultSecret**命令 toocreate 或更新密碼，以在保存庫中的。 如果它不存在，而且如果它已經建立 hello 密碼的新版本，會建立密碼。

```PowerShell
$secretvalue = ConvertTo-SecureString “User@123” -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01” -SecretValue $secretvalue
```

**輸出**

![建立祕密](media/azure-stack-kv-manage-powershell/image6.png)

### <a name="get-a-secret"></a>取得祕密

使用 hello **Get AzureKeyVaultSecret**命令 tooread 金鑰保存庫中的密碼。 此命令可傳回所有或特定版本的祕密。 

```PowerShell
Get-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01”
```

您可以建立金鑰和密碼之後，授權外部應用程式 toouse 它們。

## <a name="authorize-an-application-toouse-a-key-or-secret"></a>授權的應用程式 toouse 金鑰或密碼

tooauthorize 應用程式 tooaccess 索引鍵或在 hello 的秘密金鑰保存庫，使用 hello **Set-azurermkeyvaultaccesspolicy**命令。
比方說，如果保存庫名稱是 ContosoKeyVault 和 hello 應用程式想 tooauthorize 具有 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed 的用戶端識別碼。 執行下列命令 tooauthorize hello 應用程式的 hello。 您可以選擇性地指定 hello **PermissionsToKeys**參數 tooset 權限的使用者、 應用程式或安全性群組：

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign
```

如果您想 tooauthorize 該相同的應用程式 tooread 密碼在您的保存庫中，執行下列 cmdlet 的 hello:

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300 -PermissionsToKeys Get
```

## <a name="next-steps"></a>後續步驟
* [使用存放在 Key Vault 中的密碼來部署 VM](azure-stack-kv-deploy-vm-with-secret.md)  
* [使用存放在 Key Vault 中的憑證來部署 VM](azure-stack-kv-push-secret-into-vm.md) 

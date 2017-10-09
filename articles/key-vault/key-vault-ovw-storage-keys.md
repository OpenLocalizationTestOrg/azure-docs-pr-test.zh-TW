---
ms.assetid: 
title: "aaaAzure 金鑰保存庫儲存體帳戶金鑰"
description: "儲存體帳戶金鑰提供與 Azure 金鑰保存庫金鑰型的存取 tooAzure 儲存體帳戶即可無縫整合在一起。"
ms.topic: article
services: key-vault
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/25/2017
ms.openlocfilehash: becdf97798a08164c48d3a7a14aea6ca54085c9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-storage-account-keys"></a>Azure Key Vault 儲存體帳戶金鑰

Azure 金鑰保存庫儲存體帳戶金鑰，才能開發人員必須 toomanage 自己的 Azure 儲存體帳戶 (ASA) 索引鍵和旋轉它們，以手動方式或透過外部的自動化。 現在，Key Vault 儲存體帳戶金鑰會實作為 [Key Vault 密碼](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets)，以便向 Azure 儲存體帳戶進行驗證。 

hello ASA 項重要功能管理您密碼旋轉，並不必 hello 直接連絡 ASA 機碼與藉由提供共用存取簽章 (SAS) 做為方法。 

如需 Azure 儲存體帳戶的更多一般資訊，請參閱[關於 Azure 儲存體帳戶](https://docs.microsoft.com/azure/storage/storage-create-storage-account) 。

## <a name="supporting-interfaces"></a>支援的介面

hello Azure 儲存體帳戶金鑰 」 功能是一開始可透過 hello 其餘部分，.NET / C# 和 PowerShell 介面。 如需詳細資訊，請參閱 [Key Vault 參考](https://docs.microsoft.com/azure/key-vault/)。


## <a name="storage-account-keys-behavior"></a>儲存體帳戶金鑰行為

### <a name="what-key-vault-manages"></a>Key Vault 的管理內容

當您使用儲存體帳戶金鑰時，Key Vault 會代表您執行幾個內部管理功能。

1. Azure Key Vault 會管理 Azure 儲存體帳戶 (ASA) 的金鑰。 
    - Azure Key Vault 可在內部列出 (同步) Azure 儲存體帳戶金鑰。  
    - Azure 金鑰保存庫會重新產生 （旋轉） 定期 hello 索引鍵。 
    - 索引鍵的值永遠不會傳回回應 toocaller 中。 
    - Azure Key Vault 會管理儲存體帳戶和傳統儲存體帳戶的金鑰。 
2. Azure 金鑰保存庫可讓您、 hello 保存庫/物件擁有者、 toocreate SAS （帳戶或服務 SAS） 定義。 
    - 使用 SAS 定義建立 hello SAS 值會傳回做為密碼，透過 hello REST URI 路徑。 如需詳細資訊，請參閱 [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations) (Azure Key Vault 儲存體帳戶作業)。

### <a name="naming-guidance"></a>命名指導方針

儲存體帳戶名稱必須介於 3 到 24 個字元的長度，而且只能包含數字和小寫字母。  
 
SAS 定義名稱的長度必須是 1-102 個字元，而且只能包含 0-9、a-z、A-Z。

## <a name="developer-experience"></a>開發人員體驗 

### <a name="before-azure-key-vault-storage-keys"></a>Azure Key Vault 儲存體金鑰之前 

開發人員使用 tooneed toodo hello 與儲存體帳戶金鑰 tooget 存取 tooAzure 儲存體的做法。 
 
 ```
//create storage account using connection string containing account name 
// and hello storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a>Azure Key Vault 儲存體金鑰之後 

```
//Please make sure tooset storage permissions appropriately on your key vault
Set-AzureRmKeyVaultAccessPolicy -VaultName 'yourVault' -ObjectId yourObjectId -PermissionsToStorage all

//Use PowerShell command tooget Secret URI 

Set-AzureKeyVaultManagedStorageSasDefinition -Service Blob -ResourceType Container,Service -VaultName yourKV  
-AccountName msak01 -Name blobsas1 -Protocol HttpsOnly -ValidityPeriod ([System.Timespan]::FromDays(1)) -Permission Read,List

//Get SAS token from Key Vault

var secret = await kv.GetSecretAsync("SecretUri");

// Create new storage credentials using hello SAS token. 

var accountSasCredential = new StorageCredentials(secret.Value); 

// Use credentials and hello Blob storage endpoint toocreate a new Blob service client. 

var accountWithSas = new CloudStorageAccount(accountSasCredential, new Uri ("https://myaccount.blob.core.windows.net/"), null, null, null); 

var blobClientWithSas = accountWithSas.CreateCloudBlobClient(); 
 
// If SAS token is about tooexpire then Get sasToken again from Key Vault and update it.

accountSasCredential.UpdateSASToken(sasToken);

  ```
 
 ### <a name="developer-best-practices"></a>開發人員最佳做法 

- 只允許金鑰保存庫 toomanage ASA 金鑰。 請勿嘗試 toomanage 它們自己，您會干擾金鑰保存庫的處理程序。 
- 不允許 ASA 金鑰 toobe 受多個金鑰保存庫的物件。 
- 如果您需要 toomanually 重新產生 ASA 金鑰，我們建議您重新它們產生透過金鑰保存庫。 

## <a name="getting-started"></a>開始使用

### <a name="setup-for-role-based-access-control-rbac-permissions"></a>設定角色型存取控制 (RBAC) 權限

金鑰保存庫中需要的權限太*清單*和*重新產生*儲存體帳戶金鑰。 設定這些權限使用下列步驟的 hello:

- 取得 Key Vault 的 ObjectId： 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- 指定儲存體 Key 運算子角色 tooAzure 金鑰保存庫身分識別： 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > 針對傳統的帳戶類型，設定 hello 角色參數太*「 傳統儲存體帳戶金鑰運算子服務角色 」*。

### <a name="storage-account-onboarding"></a>儲存體帳戶登入 

範例： 做為金鑰保存庫物件的擁有者，您將加入儲存體帳戶物件 tooyour Azure 金鑰保存庫 tooonboard 儲存體帳戶。

在上線期間，金鑰保存庫需要 tooverify hello 的 hello 登入帳戶的身分識別也有權限*清單*和太*重新產生*儲存體金鑰。 若要 tooverify 這些權限、 金鑰保存庫 OBO （上代表的） 語彙基元從取得 hello 驗證服務，對象設定 tooAzure 資源管理員，並讓*清單*索引鍵呼叫 toohello Azure 儲存體服務。 如果 hello*清單*呼叫就會失敗，hello 物件建立失敗，HTTP 狀態碼為金鑰保存庫*禁止*。 在這種方式中所列的 hello 機碼會使用金鑰保存庫的實體儲存體快取。 

金鑰保存庫必須確認具備 hello 識別*重新產生*之後才能重新產生金鑰的擁有權的權限。 tooverify hello 身分識別，經由 OBO 語彙基元，以及 hello 金鑰保存庫的第一個合作對象識別具有這些權限：

- 金鑰保存庫列出 hello 儲存體帳戶資源的 RBAC 權限。
- 金鑰保存庫驗證透過規則運算式比對的動作和非動作 hello 回應。 

在 [Key Vault - 受管理的儲存體帳戶金鑰範例](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167)中尋找一些支援的範例。

如果 hello 識別沒有*重新產生*權限，或如果不需要金鑰保存庫的第一個合作對象識別*清單*或*重新產生*權限，則 hello 登入要求會失敗並傳回適當的錯誤程式碼和訊息。 

當您使用第一方、 PowerShell 或 CLI 原生用戶端應用程式時，只會運作嗨 OBO 語彙基元。

## <a name="other-applications"></a>其他應用程式

- SAS 權杖，建構使用金鑰保存庫儲存體帳戶金鑰，會提供更多的控制的存取 tooan Azure 儲存體帳戶。 如需詳細資訊，請參閱[使用共用存取簽章](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)。

## <a name="see-also"></a>另請參閱

- [關於金鑰、密碼與憑證](https://docs.microsoft.com/rest/api/keyvault/)
- [Key Vault 小組部落格](https://blogs.technet.microsoft.com/kv/)

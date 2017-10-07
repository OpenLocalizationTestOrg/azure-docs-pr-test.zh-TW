---
title: "開始使用 Azure 堆疊中的金鑰保存庫的 aaaGetting |Microsoft 文件"
description: "開始使用 Azure 堆疊金鑰保存庫"
services: azure-stack
documentationcenter: 
author: rlfmendes
manager: natmack
editor: 
ms.assetid: b973be33-2fc1-4ee6-976a-84ed270e7254
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: ricardom
ms.openlocfilehash: 66ae55291951ee0c673ba2b50ea4aecb3df19a88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-key-vault"></a>開始使用金鑰保存庫
本章節描述 hello 步驟 toocreate 保存庫、 管理金鑰和密碼，以及驗證 Azure 堆疊中的 hello 保存庫中的使用者或應用程式 tooinvoke 作業。 hello 下列步驟假設存在租用戶的訂用帳戶，而且 KeyVault 服務註冊該訂用帳戶內。 所有的 hello 範例命令會根據 hello KeyVault cmdlet 可用 hello Azure PowerShell SDK 的一部分。

## <a name="enabling-hello-tenant-subscription-for-vault-operations"></a>啟用 hello 保存庫作業的租用戶訂用帳戶
您可以發出對任何保存庫作業之前，您需要您的訂用帳戶已啟用的 tooensure 保存庫作業。 您可以藉由發出下列 PowerShell 命令的 hello，確認：

    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -AutoSize

hello 的 hello 上述命令的輸出應該 hello 的每個資料列的 「 註冊 」 狀態報告 「 已註冊 」。

    ProviderNamespace RegistrationState ResourceTypes Locations
    Microsoft.KeyVault Registered {operations} {local}
    Microsoft.KeyVault Registered {vaults} {local}
    Microsoft.KeyVault Registered {vaults/secrets} {local}


 如果不是 hello 案例，您應該叫用命令 tooregister hello KeyVault 服務您的訂用帳戶內之後的 hello:

    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault

而且 hello 下列 hello hello 命令輸出：

    ProviderNamespace : Microsoft.KeyVault
    RegistrationState : Registered
    ResourceTypes : {operations, vaults, vaults/secrets}
    Locations : {local}


> [!NOTE]
> 如果您收到 hello 錯誤:"*hello 訂用帳戶未註冊使用 Azure Key Vault*「 叫用時 KeyVault 指令程式，請確認您已啟用 hello KeyVault 資源提供者，依上述指示。
> 
> 

## <a name="creating-a-hardened-container-a-vault-in-azure-stack-toostore-and-manage-cryptographic-keys-and-secrets"></a>建立 Azure 堆疊 toostore 強行寫入的容器 （保存庫） 和管理密碼編譯金鑰和密碼
在訂單 toocreate 保存庫，租用戶應該先建立資源群組。 hello 下列 PowerShell 命令的資源群組，然後再保存庫中建立資源群組。 hello 範例也包含 hello 從該 cmdlet 的典型輸出。

### <a name="creating-a-resource-group"></a>建立資源群組：
    New-AzureRmResourceGroup -Name vaultrg010 -Location local -Verbose -Force

輸出：

    VERBOSE: Performing hello operation "Replacing resource group ..." on target "".
    VERBOSE: 12:52:51 PM - Created resource group 'vaultrg010' in location 'local'
    ResourceGroupName : vaultrg010
    Location : local
    ProvisioningState : Succeeded
    Tags :
    ResourceId : /subscriptions/fa881715-3802-42cc-a54e-a06adf61584d/resourceGroups/vaultrg010


### <a name="creating-a-vault"></a>建立保存庫：
    New-AzureRmKeyVault -VaultName vault010 -ResourceGroupName vaultrg010 -Location local -Verbose

輸出：

    VaultUri : https://vault010.vault.local.azurestack.global
    TenantId : 5454420b-2e38-4b9e-8b56-1712d321cf33
    TenantName : 5454420b-2e38-4b9e-8b56-1712d321cf33
    Sku : Standard
    EnabledForDeployment : False
    EnabledForTemplateDeployment : False
    EnabledForDiskEncryption : False
    AccessPolicies : {5454420b-2e38-4b9e-8b56-1712d321cf33}
    AccessPoliciesText :
    Tenant ID : 5454420b-2e38-4b9e-8b56-1712d321cf33
    Object ID : ca342e90-f6aa-435b-a11c-dfe5ef0bfeeb
    Application ID :
    Display Name : Tenant Admin (tenantadmin1@msazurestack.onmicrosoft.com)
    Permissions tooKeys : get, create, delete, list, update, import, backup, restore
    Permissions tooSecrets : all
    OriginalVault : Microsoft.Azure.Management.KeyVault.Vault
    ResourceId : /subscriptions/fa881715-3802-42cc-a54e-a06adf61584d/resourceGroups/vaultrg010/providers/Microsoft.KeyVault/vaults/vault010
    VaultName : vault010
    ResourceGroupName : vaultrg010
    Location : local
    Tags : {}
    TagsTable :

此 cmdlet 的 hello 輸出會顯示您剛才建立的 hello 金鑰保存庫的內容。 hello 兩個最重要的屬性包括：

* **保存庫名稱**: hello 範例中，這是**vault010**。 您將在其他金鑰保存庫 Cmdlet 中使用此名稱。
* **保存庫 URI**: hello 範例中，這是 https://vault010.vault.local.azurestack.global。 透過其 REST API 使用保存庫的應用程式必須使用此 URI。

現在已授權的 tooperform 保存庫上此金鑰的任何作業，就會是您的 Azure 帳戶。 而且，沒有其他人有此授權。

## <a name="operating-on-keys-and-secrets"></a>操作金鑰和密碼
在建立之後的保存庫下方步驟 toocreate 後續 hello 管理金鑰和密碼：

### <a name="creating-a-key"></a>建立金鑰
在排序 toocreate 金鑰，請使用 hello **Add-azurekeyvaultkey**每 hello 以下的範例。 成功建立金鑰後, hello cmdlet 會輸出 hello 新建立的索引鍵的詳細資料。

    Add-AzureKeyVaultKey -VaultName \$vaultName -Name\$keyVaultKeyName -Verbose -Destination Software

hello 以下是 hello 輸出 hello *Add-azurekeyvaultkey* cmdlet:

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

您現在可以參考此機碼，您建立或上傳 tooAzure 金鑰保存庫中，使用它的 URI。 使用**https://vault010.vault.local.azurestack.global:443/索引鍵/keyVaultKeyName001** tooalways 取得 hello 目前版本，並使用**https://vault010.vault.local.azurestack.global:443/機碼 /keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff** tooget 這個特定的版本。

### <a name="retrieving-a-key"></a>擷取機碼
使用 hello **Get AzureKeyVaultKey** tooretrieve 下列範例 hello 的索引鍵和其每個詳細資料：

    Get-AzureKeyVaultKey -VaultName vault010 -Name keyVaultKeyName001

hello 以下是 Get AzureKeyVaultKey hello 輸出

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

### <a name="setting-a-secret"></a>設定密碼
    $secretvalue = ConvertTo-SecureString 'User@123' -AsPlainText -Force
    Set-AzureKeyVaultSecret -Name MySecret-VaultName vault010 -SecretValue $secretvalue

輸出

    Vault Name : vault010
    Name : MySecret
    Version : 65a387f2ed4a416180e852b970846f5b
    Id : https://vault010.vault.local.azurestack.global:443/secrets/MySecret/65a387f2ed4a416180e852b970846f5b
    Enabled : True
    Expires :
    Not Before :
    Created : 8/17/2016 10:49:52 PM
    Updated : 8/17/2016 10:49:52 PM
    Content Type :
    Tags : 

### <a name="retrieving-a-secret"></a>擷取密碼
    Get-AzureKeyVaultSecret -VaultName vault010

輸出

    Vault Name : vault010
    Name : MySecret
    Version :
    Id : https://vault010.vault.local.azurestack.global:443/secrets/MySecret
    Enabled : True
    Expires :
    Not Before :
    Created : 8/17/2016 10:49:52 PM
    Updated : 8/17/2016 10:49:52 PM
    Content Type :
    Tags :

現在，您的金鑰保存庫和金鑰或密碼已準備好應用程式 toouse。
您必須授權應用程式 toouse 它們。

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a>授權 hello 應用程式 toouse hello 金鑰或密碼
tooauthorize hello 應用程式 tooaccess hello hello 使用 hello Set-保存庫中金鑰或密碼**AzureRmKeyVaultAccessPolicy** cmdlet。

比方說，如果您的保存庫名稱是*ContosoKeyVault*和 hello 應用程式要有 tooauthorize*用戶端識別碼*的*8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed*，而且您想 tooauthorize hello 應用程式 toodecrypt 並登入要執行 hello 下列在您的保存庫中的金鑰：

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

如果您想 tooauthorize 該相同的應用程式 tooread 密碼在您的保存庫中，執行下列 hello:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get


## <a name="next-steps"></a>後續步驟
[使用金鑰保存庫密碼部署 VM](azure-stack-kv-deploy-vm-with-secret.md)

[使用 Key Vault 憑證部署 VM](azure-stack-kv-push-secret-into-vm.md)


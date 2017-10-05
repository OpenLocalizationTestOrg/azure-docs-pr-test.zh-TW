---
title: "開始使用 Azure 堆疊中的金鑰保存庫 |Microsoft 文件"
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
ms.openlocfilehash: 32fad3ce17c877db661573e67c9cb5948b3c78fa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-key-vault"></a>開始使用金鑰保存庫
本章節描述的步驟來建立保存庫、 管理金鑰和密碼，以及授權的使用者或應用程式叫用 Azure 堆疊中保存庫中的作業。 下列步驟假設存在租用戶的訂用帳戶，而且 KeyVault 服務註冊該訂用帳戶內。 所有範例命令會都根據可用的 KeyVault cmdlet Azure PowerShell SDK 的一部分。

## <a name="enabling-the-tenant-subscription-for-vault-operations"></a>啟用保存庫作業的租用戶訂用帳戶
您可以發出對任何保存庫作業之前，您需要確定您的訂用帳戶已啟用保存庫作業。 您可以藉由發出下列 PowerShell 命令，確認：

    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -AutoSize

上述命令的輸出應該報告 「 已註冊 」 為每個資料列的 「 註冊 」 狀態。

    ProviderNamespace RegistrationState ResourceTypes Locations
    Microsoft.KeyVault Registered {operations} {local}
    Microsoft.KeyVault Registered {vaults} {local}
    Microsoft.KeyVault Registered {vaults/secrets} {local}


 如果不是大小寫，您應叫用註冊 KeyVault 服務會在您的訂用帳戶內的下列命令：

    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault

與下列項目是命令的輸出：

    ProviderNamespace : Microsoft.KeyVault
    RegistrationState : Registered
    ResourceTypes : {operations, vaults, vaults/secrets}
    Locations : {local}


> [!NOTE]
> 如果您收到錯誤:"*訂用帳戶未註冊使用 Azure Key Vault*「 叫用時 KeyVault 指令程式，請確認您已啟用上述指示每 KeyVault 資源提供者。
> 
> 

## <a name="creating-a-hardened-container-a-vault-in-azure-stack-to-store-and-manage-cryptographic-keys-and-secrets"></a>建立 Azure 來儲存和管理密碼編譯金鑰和密碼的堆疊中的強化的容器 （保存庫）
若要建立保存庫，租用戶應先建立資源群組。 下列 PowerShell 命令會建立該資源群組中的資源群組，然後再保存庫。 此範例也會包含該 cmdlet 的典型輸出。

### <a name="creating-a-resource-group"></a>建立資源群組：
    New-AzureRmResourceGroup -Name vaultrg010 -Location local -Verbose -Force

輸出：

    VERBOSE: Performing the operation "Replacing resource group ..." on target "".
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
    Permissions to Keys : get, create, delete, list, update, import, backup, restore
    Permissions to Secrets : all
    OriginalVault : Microsoft.Azure.Management.KeyVault.Vault
    ResourceId : /subscriptions/fa881715-3802-42cc-a54e-a06adf61584d/resourceGroups/vaultrg010/providers/Microsoft.KeyVault/vaults/vault010
    VaultName : vault010
    ResourceGroupName : vaultrg010
    Location : local
    Tags : {}
    TagsTable :

此 Cmdlet 的輸出會顯示您剛剛建立的金鑰保存庫屬性。 兩個最重要屬性是：

* **保存庫名稱**： 在此範例中，這是**vault010**。 您將在其他金鑰保存庫 Cmdlet 中使用此名稱。
* **保存庫 URI**： 在範例中，這是 https://vault010.vault.local.azurestack.global。 透過其 REST API 使用保存庫的應用程式必須使用此 URI。

您的 Azure 帳戶現已取得在此金鑰保存庫上執行任何作業的授權。 而且，沒有其他人有此授權。

## <a name="operating-on-keys-and-secrets"></a>操作金鑰和密碼
建立保存庫之後，請遵循下列步驟來建立管理金鑰和密碼：

### <a name="creating-a-key"></a>建立金鑰
若要建立索引鍵，使用**Add-azurekeyvaultkey**依下列範例。 成功金鑰在建立之後，此 cmdlet 會輸出新建立的金鑰詳細資料。

    Add-AzureKeyVaultKey -VaultName \$vaultName -Name\$keyVaultKeyName -Verbose -Destination Software

以下是輸出*Add-azurekeyvaultkey* cmdlet:

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

透過使用其 URI，您現在可以參照您所建立或上傳至 Azure 金鑰保存庫的金鑰。 使用**https://vault010.vault.local.azurestack.global:443/索引鍵/keyVaultKeyName001**一律取得最新版本，並使用**https://vault010.vault.local.azurestack.global:443/機碼 /keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff**取得特定版本。

### <a name="retrieving-a-key"></a>擷取機碼
使用**Get AzureKeyVaultKey**擷取索引鍵和其依下列範例的詳細資料：

    Get-AzureKeyVaultKey -VaultName vault010 -Name keyVaultKeyName001

以下是 Get AzureKeyVaultKey 的輸出

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

現在，您可以在應用程式中使用金鑰保存庫和金鑰或密碼。
您必須授權應用程式才能使用他們。

## <a name="authorize-the-application-to-use-the-key-or-secret"></a>授權應用程式使用金鑰或密碼
若要授權應用程式存取金鑰或密碼保存庫中的，請使用 Set-**AzureRmKeyVaultAccessPolicy** cmdlet。

例如，如果您的保存庫名稱是*ContosoKeyVault* ，而且您想要授權應用程式*用戶端識別碼*的*8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed*，而且您要授權應用程式解密及使用您的保存庫，執行下列命令中的金鑰簽署：

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

如果您想要授權該相同的應用程式讀取您保存庫中的機密資料，請執行以下命令：

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get


## <a name="next-steps"></a>後續步驟
[使用金鑰保存庫密碼部署 VM](azure-stack-kv-deploy-vm-with-secret.md)

[使用 Key Vault 憑證部署 VM](azure-stack-kv-push-secret-into-vm.md)


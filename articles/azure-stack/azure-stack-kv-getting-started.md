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
# <a name="getting-started-with-key-vault"></a><span data-ttu-id="37aab-103">開始使用金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="37aab-103">Getting started with Key Vault</span></span>
<span data-ttu-id="37aab-104">本章節描述的步驟來建立保存庫、 管理金鑰和密碼，以及授權的使用者或應用程式叫用 Azure 堆疊中保存庫中的作業。</span><span class="sxs-lookup"><span data-stu-id="37aab-104">This section describes the steps to create a vault, manage keys and secrets as well as authorize users or applications to invoke operations in the vault in Azure Stack.</span></span> <span data-ttu-id="37aab-105">下列步驟假設存在租用戶的訂用帳戶，而且 KeyVault 服務註冊該訂用帳戶內。</span><span class="sxs-lookup"><span data-stu-id="37aab-105">The following steps assume a tenant subscription exists and KeyVault service is registered within that subscription.</span></span> <span data-ttu-id="37aab-106">所有範例命令會都根據可用的 KeyVault cmdlet Azure PowerShell SDK 的一部分。</span><span class="sxs-lookup"><span data-stu-id="37aab-106">All the example commands are based on the KeyVault cmdlets available as part of the Azure PowerShell SDK.</span></span>

## <a name="enabling-the-tenant-subscription-for-vault-operations"></a><span data-ttu-id="37aab-107">啟用保存庫作業的租用戶訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="37aab-107">Enabling the tenant subscription for Vault operations</span></span>
<span data-ttu-id="37aab-108">您可以發出對任何保存庫作業之前，您需要確定您的訂用帳戶已啟用保存庫作業。</span><span class="sxs-lookup"><span data-stu-id="37aab-108">Before you can issue operations against any vault, you need to ensure that your subscription is enabled for vault operations.</span></span> <span data-ttu-id="37aab-109">您可以藉由發出下列 PowerShell 命令，確認：</span><span class="sxs-lookup"><span data-stu-id="37aab-109">You can confirm that by issuing the following PowerShell command:</span></span>

    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -AutoSize

<span data-ttu-id="37aab-110">上述命令的輸出應該報告 「 已註冊 」 為每個資料列的 「 註冊 」 狀態。</span><span class="sxs-lookup"><span data-stu-id="37aab-110">The output of the above command should report “Registered” for the “Registration” state of every row.</span></span>

    ProviderNamespace RegistrationState ResourceTypes Locations
    Microsoft.KeyVault Registered {operations} {local}
    Microsoft.KeyVault Registered {vaults} {local}
    Microsoft.KeyVault Registered {vaults/secrets} {local}


 <span data-ttu-id="37aab-111">如果不是大小寫，您應叫用註冊 KeyVault 服務會在您的訂用帳戶內的下列命令：</span><span class="sxs-lookup"><span data-stu-id="37aab-111">If that’s not the case, you should invoke the following command to register the KeyVault service within your subscription:</span></span>

    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault

<span data-ttu-id="37aab-112">與下列項目是命令的輸出：</span><span class="sxs-lookup"><span data-stu-id="37aab-112">And the folowing is the output of the command:</span></span>

    ProviderNamespace : Microsoft.KeyVault
    RegistrationState : Registered
    ResourceTypes : {operations, vaults, vaults/secrets}
    Locations : {local}


> [!NOTE]
> <span data-ttu-id="37aab-113">如果您收到錯誤:"*訂用帳戶未註冊使用 Azure Key Vault*「 叫用時 KeyVault 指令程式，請確認您已啟用上述指示每 KeyVault 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="37aab-113">If you get the error: "*The subscription is not registered with Azure Key Vault*" when invoking KeyVault cmdlets, please confirm you have enabled the KeyVault resource provider per instructions above.</span></span>
> 
> 

## <a name="creating-a-hardened-container-a-vault-in-azure-stack-to-store-and-manage-cryptographic-keys-and-secrets"></a><span data-ttu-id="37aab-114">建立 Azure 來儲存和管理密碼編譯金鑰和密碼的堆疊中的強化的容器 （保存庫）</span><span class="sxs-lookup"><span data-stu-id="37aab-114">Creating a hardened container (a vault) in Azure Stack to store and manage cryptographic keys and secrets</span></span>
<span data-ttu-id="37aab-115">若要建立保存庫，租用戶應先建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="37aab-115">In order to create a Vault, a tenant should first create a resource group.</span></span> <span data-ttu-id="37aab-116">下列 PowerShell 命令會建立該資源群組中的資源群組，然後再保存庫。</span><span class="sxs-lookup"><span data-stu-id="37aab-116">The following PowerShell commands create a resource group and then a Vault in that Resource Group.</span></span> <span data-ttu-id="37aab-117">此範例也會包含該 cmdlet 的典型輸出。</span><span class="sxs-lookup"><span data-stu-id="37aab-117">The example also includes the typical output from that cmdlet.</span></span>

### <a name="creating-a-resource-group"></a><span data-ttu-id="37aab-118">建立資源群組：</span><span class="sxs-lookup"><span data-stu-id="37aab-118">Creating a resource group:</span></span>
    New-AzureRmResourceGroup -Name vaultrg010 -Location local -Verbose -Force

<span data-ttu-id="37aab-119">輸出：</span><span class="sxs-lookup"><span data-stu-id="37aab-119">Output:</span></span>

    VERBOSE: Performing the operation "Replacing resource group ..." on target "".
    VERBOSE: 12:52:51 PM - Created resource group 'vaultrg010' in location 'local'
    ResourceGroupName : vaultrg010
    Location : local
    ProvisioningState : Succeeded
    Tags :
    ResourceId : /subscriptions/fa881715-3802-42cc-a54e-a06adf61584d/resourceGroups/vaultrg010


### <a name="creating-a-vault"></a><span data-ttu-id="37aab-120">建立保存庫：</span><span class="sxs-lookup"><span data-stu-id="37aab-120">Creating a vault:</span></span>
    New-AzureRmKeyVault -VaultName vault010 -ResourceGroupName vaultrg010 -Location local -Verbose

<span data-ttu-id="37aab-121">輸出：</span><span class="sxs-lookup"><span data-stu-id="37aab-121">Output:</span></span>

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

<span data-ttu-id="37aab-122">此 Cmdlet 的輸出會顯示您剛剛建立的金鑰保存庫屬性。</span><span class="sxs-lookup"><span data-stu-id="37aab-122">The output of this cmdlet shows properties of the key vault that you’ve just created.</span></span> <span data-ttu-id="37aab-123">兩個最重要屬性是：</span><span class="sxs-lookup"><span data-stu-id="37aab-123">The two most important properties are:</span></span>

* <span data-ttu-id="37aab-124">**保存庫名稱**： 在此範例中，這是**vault010**。</span><span class="sxs-lookup"><span data-stu-id="37aab-124">**Vault Name**: In the example, this is **vault010**.</span></span> <span data-ttu-id="37aab-125">您將在其他金鑰保存庫 Cmdlet 中使用此名稱。</span><span class="sxs-lookup"><span data-stu-id="37aab-125">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="37aab-126">**保存庫 URI**： 在範例中，這是 https://vault010.vault.local.azurestack.global。</span><span class="sxs-lookup"><span data-stu-id="37aab-126">**Vault URI**: In the example, this is https://vault010.vault.local.azurestack.global.</span></span> <span data-ttu-id="37aab-127">透過其 REST API 使用保存庫的應用程式必須使用此 URI。</span><span class="sxs-lookup"><span data-stu-id="37aab-127">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="37aab-128">您的 Azure 帳戶現已取得在此金鑰保存庫上執行任何作業的授權。</span><span class="sxs-lookup"><span data-stu-id="37aab-128">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="37aab-129">而且，沒有其他人有此授權。</span><span class="sxs-lookup"><span data-stu-id="37aab-129">As yet, nobody else is.</span></span>

## <a name="operating-on-keys-and-secrets"></a><span data-ttu-id="37aab-130">操作金鑰和密碼</span><span class="sxs-lookup"><span data-stu-id="37aab-130">Operating on Keys and Secrets</span></span>
<span data-ttu-id="37aab-131">建立保存庫之後，請遵循下列步驟來建立管理金鑰和密碼：</span><span class="sxs-lookup"><span data-stu-id="37aab-131">After creating a vault, follow the below steps to create manage keys and secrets:</span></span>

### <a name="creating-a-key"></a><span data-ttu-id="37aab-132">建立金鑰</span><span class="sxs-lookup"><span data-stu-id="37aab-132">Creating a key</span></span>
<span data-ttu-id="37aab-133">若要建立索引鍵，使用**Add-azurekeyvaultkey**依下列範例。</span><span class="sxs-lookup"><span data-stu-id="37aab-133">In order to create a key, use the **Add-AzureKeyVaultKey** per the example below.</span></span> <span data-ttu-id="37aab-134">成功金鑰在建立之後，此 cmdlet 會輸出新建立的金鑰詳細資料。</span><span class="sxs-lookup"><span data-stu-id="37aab-134">After successful key creation, the cmdlet will output the newly created key details.</span></span>

    Add-AzureKeyVaultKey -VaultName \$vaultName -Name\$keyVaultKeyName -Verbose -Destination Software

<span data-ttu-id="37aab-135">以下是輸出*Add-azurekeyvaultkey* cmdlet:</span><span class="sxs-lookup"><span data-stu-id="37aab-135">The following is the output of the *Add-AzureKeyVaultKey* cmdlet:</span></span>

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

<span data-ttu-id="37aab-136">透過使用其 URI，您現在可以參照您所建立或上傳至 Azure 金鑰保存庫的金鑰。</span><span class="sxs-lookup"><span data-stu-id="37aab-136">You can now reference this key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="37aab-137">使用**https://vault010.vault.local.azurestack.global:443/索引鍵/keyVaultKeyName001**一律取得最新版本，並使用**https://vault010.vault.local.azurestack.global:443/機碼 /keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff**取得特定版本。</span><span class="sxs-lookup"><span data-stu-id="37aab-137">Use **https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001** to always get the current version; and use **https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff** to get this specific version.</span></span>

### <a name="retrieving-a-key"></a><span data-ttu-id="37aab-138">擷取機碼</span><span class="sxs-lookup"><span data-stu-id="37aab-138">Retrieving a key</span></span>
<span data-ttu-id="37aab-139">使用**Get AzureKeyVaultKey**擷取索引鍵和其依下列範例的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="37aab-139">Use the **Get-AzureKeyVaultKey** to retrieve a key and its details per the following example:</span></span>

    Get-AzureKeyVaultKey -VaultName vault010 -Name keyVaultKeyName001

<span data-ttu-id="37aab-140">以下是 Get AzureKeyVaultKey 的輸出</span><span class="sxs-lookup"><span data-stu-id="37aab-140">The following is the output of Get-AzureKeyVaultKey</span></span>

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

### <a name="setting-a-secret"></a><span data-ttu-id="37aab-141">設定密碼</span><span class="sxs-lookup"><span data-stu-id="37aab-141">Setting a secret</span></span>
    $secretvalue = ConvertTo-SecureString 'User@123' -AsPlainText -Force
    Set-AzureKeyVaultSecret -Name MySecret-VaultName vault010 -SecretValue $secretvalue

<span data-ttu-id="37aab-142">輸出</span><span class="sxs-lookup"><span data-stu-id="37aab-142">Output</span></span>

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

### <a name="retrieving-a-secret"></a><span data-ttu-id="37aab-143">擷取密碼</span><span class="sxs-lookup"><span data-stu-id="37aab-143">Retrieving a secret</span></span>
    Get-AzureKeyVaultSecret -VaultName vault010

<span data-ttu-id="37aab-144">輸出</span><span class="sxs-lookup"><span data-stu-id="37aab-144">Output</span></span>

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

<span data-ttu-id="37aab-145">現在，您可以在應用程式中使用金鑰保存庫和金鑰或密碼。</span><span class="sxs-lookup"><span data-stu-id="37aab-145">Now, your key vault and key or secret is ready for applications to use.</span></span>
<span data-ttu-id="37aab-146">您必須授權應用程式才能使用他們。</span><span class="sxs-lookup"><span data-stu-id="37aab-146">You must authorize applications to use them.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="37aab-147">授權應用程式使用金鑰或密碼</span><span class="sxs-lookup"><span data-stu-id="37aab-147">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="37aab-148">若要授權應用程式存取金鑰或密碼保存庫中的，請使用 Set-**AzureRmKeyVaultAccessPolicy** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="37aab-148">To authorize the application to access the key or secret in the vault, use the Set-**AzureRmKeyVaultAccessPolicy** cmdlet.</span></span>

<span data-ttu-id="37aab-149">例如，如果您的保存庫名稱是*ContosoKeyVault* ，而且您想要授權應用程式*用戶端識別碼*的*8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed*，而且您要授權應用程式解密及使用您的保存庫，執行下列命令中的金鑰簽署：</span><span class="sxs-lookup"><span data-stu-id="37aab-149">For example, if your vault name is *ContosoKeyVault* and the application you want to authorize has a *Client ID* of *8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed*, and you want to authorize the application to decrypt and sign with keys in your vault, run the following:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

<span data-ttu-id="37aab-150">如果您想要授權該相同的應用程式讀取您保存庫中的機密資料，請執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="37aab-150">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get


## <a name="next-steps"></a><span data-ttu-id="37aab-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="37aab-151">Next steps</span></span>
[<span data-ttu-id="37aab-152">使用金鑰保存庫密碼部署 VM</span><span class="sxs-lookup"><span data-stu-id="37aab-152">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)

[<span data-ttu-id="37aab-153">使用 Key Vault 憑證部署 VM</span><span class="sxs-lookup"><span data-stu-id="37aab-153">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)


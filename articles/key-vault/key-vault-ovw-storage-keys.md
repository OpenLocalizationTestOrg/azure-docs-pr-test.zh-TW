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
# <a name="azure-key-vault-storage-account-keys"></a><span data-ttu-id="e4757-103">Azure Key Vault 儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="e4757-103">Azure Key Vault Storage Account Keys</span></span>

<span data-ttu-id="e4757-104">Azure 金鑰保存庫儲存體帳戶金鑰，才能開發人員必須 toomanage 自己的 Azure 儲存體帳戶 (ASA) 索引鍵和旋轉它們，以手動方式或透過外部的自動化。</span><span class="sxs-lookup"><span data-stu-id="e4757-104">Before Azure Key Vault Storage Account Keys, developers had toomanage their own Azure Storage Account (ASA) keys and rotate them manually or through an external automation.</span></span> <span data-ttu-id="e4757-105">現在，Key Vault 儲存體帳戶金鑰會實作為 [Key Vault 密碼](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets)，以便向 Azure 儲存體帳戶進行驗證。</span><span class="sxs-lookup"><span data-stu-id="e4757-105">Now, Key Vault Storage Account Keys are implemented as [Key Vault secrets](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) for authenticating with an Azure Storage Account.</span></span> 

<span data-ttu-id="e4757-106">hello ASA 項重要功能管理您密碼旋轉，並不必 hello 直接連絡 ASA 機碼與藉由提供共用存取簽章 (SAS) 做為方法。</span><span class="sxs-lookup"><span data-stu-id="e4757-106">hello ASA key feature manages secret rotation for you and removes hello need for your direct contact with an ASA key by offering Shared Access Signatures (SAS) as a method.</span></span> 

<span data-ttu-id="e4757-107">如需 Azure 儲存體帳戶的更多一般資訊，請參閱[關於 Azure 儲存體帳戶](https://docs.microsoft.com/azure/storage/storage-create-storage-account) 。</span><span class="sxs-lookup"><span data-stu-id="e4757-107">For more general information on Azure Storage Accounts, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span></span>

## <a name="supporting-interfaces"></a><span data-ttu-id="e4757-108">支援的介面</span><span class="sxs-lookup"><span data-stu-id="e4757-108">Supporting interfaces</span></span>

<span data-ttu-id="e4757-109">hello Azure 儲存體帳戶金鑰 」 功能是一開始可透過 hello 其餘部分，.NET / C# 和 PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="e4757-109">hello Azure Storage Account keys feature is initially available through hello REST, .NET/C# and PowerShell interfaces.</span></span> <span data-ttu-id="e4757-110">如需詳細資訊，請參閱 [Key Vault 參考](https://docs.microsoft.com/azure/key-vault/)。</span><span class="sxs-lookup"><span data-stu-id="e4757-110">For more information, see [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>


## <a name="storage-account-keys-behavior"></a><span data-ttu-id="e4757-111">儲存體帳戶金鑰行為</span><span class="sxs-lookup"><span data-stu-id="e4757-111">Storage account keys behavior</span></span>

### <a name="what-key-vault-manages"></a><span data-ttu-id="e4757-112">Key Vault 的管理內容</span><span class="sxs-lookup"><span data-stu-id="e4757-112">What Key Vault manages</span></span>

<span data-ttu-id="e4757-113">當您使用儲存體帳戶金鑰時，Key Vault 會代表您執行幾個內部管理功能。</span><span class="sxs-lookup"><span data-stu-id="e4757-113">Key Vault performs several internal management functions on your behalf when you use Storage Account Keys.</span></span>

1. <span data-ttu-id="e4757-114">Azure Key Vault 會管理 Azure 儲存體帳戶 (ASA) 的金鑰。</span><span class="sxs-lookup"><span data-stu-id="e4757-114">Azure Key Vault manages keys of an Azure Storage Account (ASA).</span></span> 
    - <span data-ttu-id="e4757-115">Azure Key Vault 可在內部列出 (同步) Azure 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="e4757-115">Internally, Azure Key Vault can list (sync) keys with an Azure Storage Account.</span></span>  
    - <span data-ttu-id="e4757-116">Azure 金鑰保存庫會重新產生 （旋轉） 定期 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e4757-116">Azure Key Vault regenerates (rotates) hello keys periodically.</span></span> 
    - <span data-ttu-id="e4757-117">索引鍵的值永遠不會傳回回應 toocaller 中。</span><span class="sxs-lookup"><span data-stu-id="e4757-117">Key values are never returned in response toocaller.</span></span> 
    - <span data-ttu-id="e4757-118">Azure Key Vault 會管理儲存體帳戶和傳統儲存體帳戶的金鑰。</span><span class="sxs-lookup"><span data-stu-id="e4757-118">Azure Key Vault manages keys of both Storage Accounts and Classic Storage Accounts.</span></span> 
2. <span data-ttu-id="e4757-119">Azure 金鑰保存庫可讓您、 hello 保存庫/物件擁有者、 toocreate SAS （帳戶或服務 SAS） 定義。</span><span class="sxs-lookup"><span data-stu-id="e4757-119">Azure Key Vault allows you, hello vault/object owner, toocreate SAS (account or service SAS) definitions.</span></span> 
    - <span data-ttu-id="e4757-120">使用 SAS 定義建立 hello SAS 值會傳回做為密碼，透過 hello REST URI 路徑。</span><span class="sxs-lookup"><span data-stu-id="e4757-120">hello SAS value, created using SAS definition, is returned as a secret via hello REST URI path.</span></span> <span data-ttu-id="e4757-121">如需詳細資訊，請參閱 [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations) (Azure Key Vault 儲存體帳戶作業)。</span><span class="sxs-lookup"><span data-stu-id="e4757-121">For more information, see [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span></span>

### <a name="naming-guidance"></a><span data-ttu-id="e4757-122">命名指導方針</span><span class="sxs-lookup"><span data-stu-id="e4757-122">Naming guidance</span></span>

<span data-ttu-id="e4757-123">儲存體帳戶名稱必須介於 3 到 24 個字元的長度，而且只能包含數字和小寫字母。</span><span class="sxs-lookup"><span data-stu-id="e4757-123">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>  
 
<span data-ttu-id="e4757-124">SAS 定義名稱的長度必須是 1-102 個字元，而且只能包含 0-9、a-z、A-Z。</span><span class="sxs-lookup"><span data-stu-id="e4757-124">A SAS definition name must be 1-102 characters in length containing only 0-9, a-z, A-Z.</span></span>

## <a name="developer-experience"></a><span data-ttu-id="e4757-125">開發人員體驗</span><span class="sxs-lookup"><span data-stu-id="e4757-125">Developer experience</span></span> 

### <a name="before-azure-key-vault-storage-keys"></a><span data-ttu-id="e4757-126">Azure Key Vault 儲存體金鑰之前</span><span class="sxs-lookup"><span data-stu-id="e4757-126">Before Azure Key Vault Storage Keys</span></span> 

<span data-ttu-id="e4757-127">開發人員使用 tooneed toodo hello 與儲存體帳戶金鑰 tooget 存取 tooAzure 儲存體的做法。</span><span class="sxs-lookup"><span data-stu-id="e4757-127">Developers used tooneed toodo hello following practices with a storage account key tooget access tooAzure storage.</span></span> 
 
 ```
//create storage account using connection string containing account name 
// and hello storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a><span data-ttu-id="e4757-128">Azure Key Vault 儲存體金鑰之後</span><span class="sxs-lookup"><span data-stu-id="e4757-128">After Azure Key Vault Storage Keys</span></span> 

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
 
 ### <a name="developer-best-practices"></a><span data-ttu-id="e4757-129">開發人員最佳做法</span><span class="sxs-lookup"><span data-stu-id="e4757-129">Developer best practices</span></span> 

- <span data-ttu-id="e4757-130">只允許金鑰保存庫 toomanage ASA 金鑰。</span><span class="sxs-lookup"><span data-stu-id="e4757-130">Only allow Key Vault toomanage your ASA keys.</span></span> <span data-ttu-id="e4757-131">請勿嘗試 toomanage 它們自己，您會干擾金鑰保存庫的處理程序。</span><span class="sxs-lookup"><span data-stu-id="e4757-131">Do not attempt toomanage them yourself, you will interfere with Key Vault's processes.</span></span> 
- <span data-ttu-id="e4757-132">不允許 ASA 金鑰 toobe 受多個金鑰保存庫的物件。</span><span class="sxs-lookup"><span data-stu-id="e4757-132">Do not allow ASA keys toobe managed by more than one Key Vault object.</span></span> 
- <span data-ttu-id="e4757-133">如果您需要 toomanually 重新產生 ASA 金鑰，我們建議您重新它們產生透過金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="e4757-133">If you need toomanually regenerate your ASA keys, we recommend that you regenerate them via Key Vault.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="e4757-134">開始使用</span><span class="sxs-lookup"><span data-stu-id="e4757-134">Getting started</span></span>

### <a name="setup-for-role-based-access-control-rbac-permissions"></a><span data-ttu-id="e4757-135">設定角色型存取控制 (RBAC) 權限</span><span class="sxs-lookup"><span data-stu-id="e4757-135">Setup for role-based access control (RBAC) permissions</span></span>

<span data-ttu-id="e4757-136">金鑰保存庫中需要的權限太*清單*和*重新產生*儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="e4757-136">Key Vault needs permissions too*list* and *regenerate* keys for a storage account.</span></span> <span data-ttu-id="e4757-137">設定這些權限使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e4757-137">Set up these permissions using hello following steps:</span></span>

- <span data-ttu-id="e4757-138">取得 Key Vault 的 ObjectId：</span><span class="sxs-lookup"><span data-stu-id="e4757-138">Get ObjectId of Key Vault:</span></span> 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- <span data-ttu-id="e4757-139">指定儲存體 Key 運算子角色 tooAzure 金鑰保存庫身分識別：</span><span class="sxs-lookup"><span data-stu-id="e4757-139">Assign Storage Key Operator role tooAzure Key Vault Identity:</span></span> 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > <span data-ttu-id="e4757-140">針對傳統的帳戶類型，設定 hello 角色參數太*「 傳統儲存體帳戶金鑰運算子服務角色 」*。</span><span class="sxs-lookup"><span data-stu-id="e4757-140">For a classic account type, set hello role parameter too*"Classic Storage Account Key Operator Service Role"*.</span></span>

### <a name="storage-account-onboarding"></a><span data-ttu-id="e4757-141">儲存體帳戶登入</span><span class="sxs-lookup"><span data-stu-id="e4757-141">Storage account onboarding</span></span> 

<span data-ttu-id="e4757-142">範例： 做為金鑰保存庫物件的擁有者，您將加入儲存體帳戶物件 tooyour Azure 金鑰保存庫 tooonboard 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4757-142">Example: As a Key Vault object owner you add a storage account object tooyour Azure Key Vault tooonboard a storage account.</span></span>

<span data-ttu-id="e4757-143">在上線期間，金鑰保存庫需要 tooverify hello 的 hello 登入帳戶的身分識別也有權限*清單*和太*重新產生*儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="e4757-143">During onboarding, Key Vault needs tooverify that hello identity of hello onboarding account has permissions too*list* and too*regenerate* storage keys.</span></span> <span data-ttu-id="e4757-144">若要 tooverify 這些權限、 金鑰保存庫 OBO （上代表的） 語彙基元從取得 hello 驗證服務，對象設定 tooAzure 資源管理員，並讓*清單*索引鍵呼叫 toohello Azure 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="e4757-144">In order tooverify these permissions, Key Vault gets an OBO (On Behalf Of) token from hello authentication service, audience set tooAzure Resource Manager, and makes a *list* key call toohello Azure Storage service.</span></span> <span data-ttu-id="e4757-145">如果 hello*清單*呼叫就會失敗，hello 物件建立失敗，HTTP 狀態碼為金鑰保存庫*禁止*。</span><span class="sxs-lookup"><span data-stu-id="e4757-145">If hello *list* call fails, hello Key Vault object creation fails with a HTTP status code of *Forbidden*.</span></span> <span data-ttu-id="e4757-146">在這種方式中所列的 hello 機碼會使用金鑰保存庫的實體儲存體快取。</span><span class="sxs-lookup"><span data-stu-id="e4757-146">hello keys listed in this fashion are cached with your key vault entity storage.</span></span> 

<span data-ttu-id="e4757-147">金鑰保存庫必須確認具備 hello 識別*重新產生*之後才能重新產生金鑰的擁有權的權限。</span><span class="sxs-lookup"><span data-stu-id="e4757-147">Key Vault must verify that hello identity has *regenerate* permissions before it can take ownership of regenerating your keys.</span></span> <span data-ttu-id="e4757-148">tooverify hello 身分識別，經由 OBO 語彙基元，以及 hello 金鑰保存庫的第一個合作對象識別具有這些權限：</span><span class="sxs-lookup"><span data-stu-id="e4757-148">tooverify that hello identity, via OBO token, as well as hello Key Vault first party identity has these permissions:</span></span>

- <span data-ttu-id="e4757-149">金鑰保存庫列出 hello 儲存體帳戶資源的 RBAC 權限。</span><span class="sxs-lookup"><span data-stu-id="e4757-149">Key Vault lists RBAC permissions on hello storage account resource.</span></span>
- <span data-ttu-id="e4757-150">金鑰保存庫驗證透過規則運算式比對的動作和非動作 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="e4757-150">Key Vault validates hello response via regular expression matching of actions and non-actions.</span></span> 

<span data-ttu-id="e4757-151">在 [Key Vault - 受管理的儲存體帳戶金鑰範例](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167)中尋找一些支援的範例。</span><span class="sxs-lookup"><span data-stu-id="e4757-151">Find some supporting examples at [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span></span>

<span data-ttu-id="e4757-152">如果 hello 識別沒有*重新產生*權限，或如果不需要金鑰保存庫的第一個合作對象識別*清單*或*重新產生*權限，則 hello 登入要求會失敗並傳回適當的錯誤程式碼和訊息。</span><span class="sxs-lookup"><span data-stu-id="e4757-152">If hello identity does not have *regenerate* permissions or if Key Vault's first party identity doesn’t have *list* or *regenerate* permission, then hello onboarding request fails returning an appropriate error code and message.</span></span> 

<span data-ttu-id="e4757-153">當您使用第一方、 PowerShell 或 CLI 原生用戶端應用程式時，只會運作嗨 OBO 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="e4757-153">hello OBO token will only work when you use first-party, native client applications of either PowerShell or CLI.</span></span>

## <a name="other-applications"></a><span data-ttu-id="e4757-154">其他應用程式</span><span class="sxs-lookup"><span data-stu-id="e4757-154">Other applications</span></span>

- <span data-ttu-id="e4757-155">SAS 權杖，建構使用金鑰保存庫儲存體帳戶金鑰，會提供更多的控制的存取 tooan Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4757-155">SAS tokens, constructed using Key Vault storage account keys, provide even more controlled access tooan Azure storage account.</span></span> <span data-ttu-id="e4757-156">如需詳細資訊，請參閱[使用共用存取簽章](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)。</span><span class="sxs-lookup"><span data-stu-id="e4757-156">For more information, see [Using shared access signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

## <a name="see-also"></a><span data-ttu-id="e4757-157">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e4757-157">See also</span></span>

- [<span data-ttu-id="e4757-158">關於金鑰、密碼與憑證</span><span class="sxs-lookup"><span data-stu-id="e4757-158">About keys, secrets, and certificates</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
- [<span data-ttu-id="e4757-159">Key Vault 小組部落格</span><span class="sxs-lookup"><span data-stu-id="e4757-159">Key Vault Team Blog</span></span>](https://blogs.technet.microsoft.com/kv/)

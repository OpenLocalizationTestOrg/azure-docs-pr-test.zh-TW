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
# <a name="manage-key-vault-in-azure-stack-using-powershell"></a><span data-ttu-id="229d8-103">使用 PowerShell 管理 Azure Stack 中的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="229d8-103">Manage Key Vault in Azure Stack using PowerShell</span></span>

<span data-ttu-id="229d8-104">這篇文章可協助您取得啟動的 toocreate 並使用 PowerShell 管理 Azure 堆疊中的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="229d8-104">This article helps you get started toocreate and manage Key Vault in Azure Stack by using PowerShell.</span></span> <span data-ttu-id="229d8-105">本文中所述的 hello 金鑰保存庫 PowerShell cmdlet 可用 hello Azure PowerShell SDK 的一部分。</span><span class="sxs-lookup"><span data-stu-id="229d8-105">hello Key Vault PowerShell cmdlets described in this article are available as a part of hello Azure PowerShell SDK.</span></span> <span data-ttu-id="229d8-106">hello 下列各節說明 hello PowerShell cmdlet 的必要的 toocreate 保存庫，儲存和管理密碼編譯金鑰和密碼，以及授權 hello 保存庫中的使用者或應用程式 tooinvoke 作業。</span><span class="sxs-lookup"><span data-stu-id="229d8-106">hello following sections describe hello PowerShell cmdlets that are required toocreate a vault, store, and manage cryptographic keys and secrets as well as authorize users or applications tooinvoke operations in hello vault.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="229d8-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="229d8-107">Prerequisites</span></span>
* [<span data-ttu-id="229d8-108">安裝適用於 Azure Stack 的 PowerShell</span><span class="sxs-lookup"><span data-stu-id="229d8-108">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* <span data-ttu-id="229d8-109">Azure 堆疊雲端系統管理員必須具有[建立優惠](azure-stack-create-offer.md)包含 hello 金鑰保存庫服務。</span><span class="sxs-lookup"><span data-stu-id="229d8-109">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes hello Key Vault service.</span></span>  
* <span data-ttu-id="229d8-110">使用者必須[訂閱 tooan 優惠](azure-stack-subscribe-plan-provision-vm.md)包含 hello 金鑰保存庫服務。</span><span class="sxs-lookup"><span data-stu-id="229d8-110">Users must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that includes hello Key Vault service.</span></span> 
* [<span data-ttu-id="229d8-111">設定 hello Azure 堆疊使用者的 PowerShell 環境</span><span class="sxs-lookup"><span data-stu-id="229d8-111">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)

## <a name="enable-your-tenant-subscription-for-vault-operations"></a><span data-ttu-id="229d8-112">針對保存庫作業啟用您的租用戶訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="229d8-112">Enable your tenant subscription for vault operations</span></span>

<span data-ttu-id="229d8-113">您可以發出對金鑰保存庫的任何作業之前，您會需要您租用戶訂用帳戶已啟用的 tooensure 保存庫作業。</span><span class="sxs-lookup"><span data-stu-id="229d8-113">Before you can issue any operations against a key vault, you need tooensure that your tenant subscription is enabled for vault operations.</span></span> <span data-ttu-id="229d8-114">tooverify，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="229d8-114">tooverify, run hello following command:</span></span>

```PowerShell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -Autosize
```
<span data-ttu-id="229d8-115">**輸出**</span><span class="sxs-lookup"><span data-stu-id="229d8-115">**Output**</span></span>

<span data-ttu-id="229d8-116">如果您的訂用帳戶已啟用保存庫作業，hello 輸出會顯示 「 RegistrationState 」 等於 「 已註冊 」 的金鑰保存庫的所有資源類型。</span><span class="sxs-lookup"><span data-stu-id="229d8-116">If your subscription is enabled for vault operations, hello output shows “RegistrationState” equals “Registered” for all resource types of a key vault.</span></span>

![註冊狀態](media/azure-stack-kv-manage-powershell/image1.png)

<span data-ttu-id="229d8-118">如果不是 hello 情況下，叫用下列命令 tooregister hello 金鑰保存庫服務您的訂用帳戶中的 hello:</span><span class="sxs-lookup"><span data-stu-id="229d8-118">If that’s not hello case, invoke hello following command tooregister hello Key Vault service in your subscription:</span></span>

```PowerShell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault
```

<span data-ttu-id="229d8-119">**輸出**</span><span class="sxs-lookup"><span data-stu-id="229d8-119">**Output**</span></span>

<span data-ttu-id="229d8-120">Hello 註冊成功時，如果 hello 會傳回下列輸出：</span><span class="sxs-lookup"><span data-stu-id="229d8-120">If hello registration is successful, hello following output is returned:</span></span>

![註冊](media/azure-stack-kv-manage-powershell/image2.png)

<span data-ttu-id="229d8-122">hello 下列章節假設您金鑰保存庫服務註冊 hello 使用者訂用帳戶內。</span><span class="sxs-lookup"><span data-stu-id="229d8-122">hello following sections assume Key Vault service is registered within hello user subscription.</span></span> <span data-ttu-id="229d8-123">當叫用金鑰保存庫命令，如果您收到錯誤:"hello 訂用帳戶未註冊的 toouse 命名空間 ' Microsoft.KeyVault"然後，請確認您有[啟用 hello 金鑰保存庫資源提供者](#enable-your-tenant-subscription-for-vault-operations)根據指示先前所述。</span><span class="sxs-lookup"><span data-stu-id="229d8-123">When invoking key vault commands, if you get an error- "hello subscription is not registered toouse namespace ‘Microsoft.KeyVault" then, confirm that you have [enabled hello Key Vault resource provider](#enable-your-tenant-subscription-for-vault-operations) as per instructions mentioned earlier.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="229d8-124">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="229d8-124">Create a key vault</span></span> 

<span data-ttu-id="229d8-125">建立金鑰保存庫之前，請先建立資源群組，使所有金鑰保存庫相關的資源都存在於資源群組中。</span><span class="sxs-lookup"><span data-stu-id="229d8-125">Before you create a key vault, create a resource group so that all key vault related resources exist in a resource group.</span></span> <span data-ttu-id="229d8-126">使用下列命令 toocreate 新的資源群組的 hello:</span><span class="sxs-lookup"><span data-stu-id="229d8-126">Use hello following command toocreate a new resource group:</span></span>

```PowerShell
New-AzureRmResourceGroup -Name “VaultRG” -Location local -verbose -Force

```

<span data-ttu-id="229d8-127">**輸出**</span><span class="sxs-lookup"><span data-stu-id="229d8-127">**Output**</span></span>

![新的資源群組](media/azure-stack-kv-manage-powershell/image3.png)

<span data-ttu-id="229d8-129">現在，使用 hello**新增 AzureRMKeyVault**命令 toocreate hello 您稍早建立的資源群組中的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="229d8-129">Now, use hello **New-AzureRMKeyVault** command toocreate a key vault in hello resource group that you created earlier.</span></span> <span data-ttu-id="229d8-130">這個 Cmdlet 會讀取三個必要參數：資源群組名稱、金鑰保存庫名稱和地理位置。</span><span class="sxs-lookup"><span data-stu-id="229d8-130">This command reads three mandatory parameters- resource group name, key vault name, and geographic location.</span></span> 

<span data-ttu-id="229d8-131">執行下列命令 toocreate hello 金鑰保存庫：</span><span class="sxs-lookup"><span data-stu-id="229d8-131">Run hello following command toocreate a key vault:</span></span>

```PowerShell
New-AzureRmKeyVault -VaultName “Vault01” -ResourceGroupName “VaultRG” -Location local -verbose
```
<span data-ttu-id="229d8-132">**輸出**</span><span class="sxs-lookup"><span data-stu-id="229d8-132">**Output**</span></span>

![新增金鑰保存庫](media/azure-stack-kv-manage-powershell/image4.png)

<span data-ttu-id="229d8-134">hello 這個命令的輸出會顯示您所建立的 hello 金鑰保存庫 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="229d8-134">hello output of this command shows hello properties of hello key vault that you created.</span></span> <span data-ttu-id="229d8-135">當應用程式存取此保存庫時，它會使用 hello**保存庫 URI** hello 輸出中所示的屬性。</span><span class="sxs-lookup"><span data-stu-id="229d8-135">When an application accesses this vault, it uses hello **Vault URI** property shown in hello output.</span></span> <span data-ttu-id="229d8-136">比方說，是 hello 保存庫 URI 這裡**https://vault01.vault.local.azurestack.external**。</span><span class="sxs-lookup"><span data-stu-id="229d8-136">For example, hello vault URI here is **https://vault01.vault.local.azurestack.external**.</span></span> <span data-ttu-id="229d8-137">透過 REST API 與此金鑰保存庫互動的應用程式必須使用此 URI。</span><span class="sxs-lookup"><span data-stu-id="229d8-137">Applications interacting with this key vault through REST API must use this URI.</span></span>

<span data-ttu-id="229d8-138">在以 ADFS 為基礎的部署中，使用 PowerShell 建立金鑰保存庫時，可能會收到警告，指出「未設定存取原則，</span><span class="sxs-lookup"><span data-stu-id="229d8-138">In ADFS-based deployments, when you create a key vault by using PowerShell, you might receive a warning that says "Access policy is not set.</span></span> <span data-ttu-id="229d8-139">沒有使用者或應用程式有存取權限 toouse 此保存庫 」。</span><span class="sxs-lookup"><span data-stu-id="229d8-139">No user or application has access permission toouse this vault".</span></span> <span data-ttu-id="229d8-140">tooresolve 此問題，可以設定由 hello 保存庫的存取原則使用 hello [Set-azurermkeyvaultaccesspolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret)命令：</span><span class="sxs-lookup"><span data-stu-id="229d8-140">tooresolve this issue, set an access policy for hello vault by using hello [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret) command:</span></span>

```PowerShell
# Obtain hello security identifier(SID) of hello active directory user
$adUser = Get-ADUser -Filter "Name -eq '{Active directory user name}'"
$objectSID = $adUser.SID.Value 

#Set hello key vault access policy
Set-AzureRmKeyVaultAccessPolicy -VaultName "{key vault name}" -ResourceGroupName "{resource group name}" -ObjectId "{object SID}" -PermissionsToKeys {permissionsToKeys} -PermissionsToSecrets {permissionsToSecrets} -BypassObjectIdValidation 
```

## <a name="manage-keys-and-secrets"></a><span data-ttu-id="229d8-141">管理金鑰和祕密</span><span class="sxs-lookup"><span data-stu-id="229d8-141">Manage keys and secrets</span></span>

<span data-ttu-id="229d8-142">建立保存庫之後, 使用下列步驟 toocreate hello 和管理金鑰和秘密 hello 保存庫中。</span><span class="sxs-lookup"><span data-stu-id="229d8-142">After creating a vault, use hello following steps toocreate and manage keys and secrets within hello vault.</span></span>

### <a name="create-a-key"></a><span data-ttu-id="229d8-143">建立金鑰</span><span class="sxs-lookup"><span data-stu-id="229d8-143">Create a key</span></span>

<span data-ttu-id="229d8-144">使用 hello **Add-azurekeyvaultkey**命令 toocreate 或匯入軟體保護的金鑰在金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="229d8-144">Use hello **Add-AzureKeyVaultKey** command toocreate or import a software protected key in a key vault.</span></span> 

```PowerShell
Add-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01” -verbose -Destination Software
```
<span data-ttu-id="229d8-145">hello**目的地**參數用 toospecify hello 金鑰是軟體保護。</span><span class="sxs-lookup"><span data-stu-id="229d8-145">hello **Destination** parameter is used toospecify that hello key is software protected.</span></span> <span data-ttu-id="229d8-146">已成功建立 hello 金鑰時，hello 命令會輸出 hello 的 hello 建立金鑰的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="229d8-146">When hello key is successfully created, hello command outputs hello details of hello created key.</span></span>

<span data-ttu-id="229d8-147">**輸出**</span><span class="sxs-lookup"><span data-stu-id="229d8-147">**Output**</span></span>

![新金鑰](media/azure-stack-kv-manage-powershell/image5.png)

<span data-ttu-id="229d8-149">您現在可以參考 hello 利用其 URI 建立金鑰。</span><span class="sxs-lookup"><span data-stu-id="229d8-149">You can now reference hello created key by using its URI.</span></span> <span data-ttu-id="229d8-150">如果您建立或匯入具有相同名稱做為現有的索引鍵的索引鍵，hello 原始金鑰的 hello 新機碼中指定的 hello 值來更新。</span><span class="sxs-lookup"><span data-stu-id="229d8-150">If you create or import a key that has same name as an existing key, hello original key is updated with hello values that are specified in hello new key.</span></span>  <span data-ttu-id="229d8-151">您可以使用 hello 特定版本，以存取 hello 前一版的 hello 金鑰的 URI。</span><span class="sxs-lookup"><span data-stu-id="229d8-151">You can access hello previous version by using hello version-specific URI of hello key.</span></span> <span data-ttu-id="229d8-152">例如，</span><span class="sxs-lookup"><span data-stu-id="229d8-152">For example,</span></span> 

* <span data-ttu-id="229d8-153">使用**https://vault10.vault.local.azurestack.external:443/索引鍵/key01** tooalways 取得 hello 目前版本</span><span class="sxs-lookup"><span data-stu-id="229d8-153">Use **https://vault10.vault.local.azurestack.external:443/keys/key01** tooalways get hello current version</span></span>  
* <span data-ttu-id="229d8-154">使用**https://vault010.vault.local.azurestack.external:443/索引鍵/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** tooget 此特定版本</span><span class="sxs-lookup"><span data-stu-id="229d8-154">Use **https://vault010.vault.local.azurestack.external:443/keys/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** tooget this specific version</span></span>

### <a name="get-a-key"></a><span data-ttu-id="229d8-155">取得金鑰</span><span class="sxs-lookup"><span data-stu-id="229d8-155">Get a key</span></span>

<span data-ttu-id="229d8-156">使用 hello **Get AzureKeyVaultKey**命令 tooread 索引鍵和其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="229d8-156">Use hello **Get-AzureKeyVaultKey** command tooread a key and its details.</span></span>

```PowerShell
Get-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01”
```

### <a name="create-a-secret"></a><span data-ttu-id="229d8-157">建立祕密</span><span class="sxs-lookup"><span data-stu-id="229d8-157">Create a secret</span></span>

<span data-ttu-id="229d8-158">使用 hello**組 AzureKeyVaultSecret**命令 toocreate 或更新密碼，以在保存庫中的。</span><span class="sxs-lookup"><span data-stu-id="229d8-158">Use hello **Set-AzureKeyVaultSecret** command toocreate or update a secret in a vault.</span></span> <span data-ttu-id="229d8-159">如果它不存在，而且如果它已經建立 hello 密碼的新版本，會建立密碼。</span><span class="sxs-lookup"><span data-stu-id="229d8-159">A secret is created if it doesn’t already exist, and a new version of hello secret is created if it already exists.</span></span>

```PowerShell
$secretvalue = ConvertTo-SecureString “User@123” -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01” -SecretValue $secretvalue
```

<span data-ttu-id="229d8-160">**輸出**</span><span class="sxs-lookup"><span data-stu-id="229d8-160">**Output**</span></span>

![建立祕密](media/azure-stack-kv-manage-powershell/image6.png)

### <a name="get-a-secret"></a><span data-ttu-id="229d8-162">取得祕密</span><span class="sxs-lookup"><span data-stu-id="229d8-162">Get a secret</span></span>

<span data-ttu-id="229d8-163">使用 hello **Get AzureKeyVaultSecret**命令 tooread 金鑰保存庫中的密碼。</span><span class="sxs-lookup"><span data-stu-id="229d8-163">Use hello **Get-AzureKeyVaultSecret** command tooread a secret in a key vault.</span></span> <span data-ttu-id="229d8-164">此命令可傳回所有或特定版本的祕密。</span><span class="sxs-lookup"><span data-stu-id="229d8-164">This command can return all or specific versions of a secret.</span></span> 

```PowerShell
Get-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01”
```

<span data-ttu-id="229d8-165">您可以建立金鑰和密碼之後，授權外部應用程式 toouse 它們。</span><span class="sxs-lookup"><span data-stu-id="229d8-165">After creating keys and secrets, you can authorize external applications toouse them.</span></span>

## <a name="authorize-an-application-toouse-a-key-or-secret"></a><span data-ttu-id="229d8-166">授權的應用程式 toouse 金鑰或密碼</span><span class="sxs-lookup"><span data-stu-id="229d8-166">Authorize an application toouse a key or secret</span></span>

<span data-ttu-id="229d8-167">tooauthorize 應用程式 tooaccess 索引鍵或在 hello 的秘密金鑰保存庫，使用 hello **Set-azurermkeyvaultaccesspolicy**命令。</span><span class="sxs-lookup"><span data-stu-id="229d8-167">tooauthorize an application tooaccess a key or secret in hello key vault, use hello **Set-AzureRmKeyVaultAccessPolicy** command.</span></span>
<span data-ttu-id="229d8-168">比方說，如果保存庫名稱是 ContosoKeyVault 和 hello 應用程式想 tooauthorize 具有 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed 的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="229d8-168">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a Client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed.</span></span> <span data-ttu-id="229d8-169">執行下列命令 tooauthorize hello 應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="229d8-169">Run hello following command tooauthorize hello application.</span></span> <span data-ttu-id="229d8-170">您可以選擇性地指定 hello **PermissionsToKeys**參數 tooset 權限的使用者、 應用程式或安全性群組：</span><span class="sxs-lookup"><span data-stu-id="229d8-170">Optionally, you can specify hello **PermissionsToKeys** parameter tooset permissions for a user, application, or a security group:</span></span>

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign
```

<span data-ttu-id="229d8-171">如果您想 tooauthorize 該相同的應用程式 tooread 密碼在您的保存庫中，執行下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="229d8-171">If you want tooauthorize that same application tooread secrets in your vault, run hello following cmdlet:</span></span>

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300 -PermissionsToKeys Get
```

## <a name="next-steps"></a><span data-ttu-id="229d8-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="229d8-172">Next Steps</span></span>
* [<span data-ttu-id="229d8-173">使用存放在 Key Vault 中的密碼來部署 VM</span><span class="sxs-lookup"><span data-stu-id="229d8-173">Deploy a VM with password stored in a Key Vault</span></span>](azure-stack-kv-deploy-vm-with-secret.md)  
* [<span data-ttu-id="229d8-174">使用存放在 Key Vault 中的憑證來部署 VM</span><span class="sxs-lookup"><span data-stu-id="229d8-174">Deploy a VM with certificate stored in Key Vault</span></span>](azure-stack-kv-push-secret-into-vm.md) 

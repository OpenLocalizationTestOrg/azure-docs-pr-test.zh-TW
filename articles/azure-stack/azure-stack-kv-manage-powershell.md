---
title: "使用 PowerShell 管理 Azure Stack 中的金鑰保存庫 | Microsoft Docs"
description: "了解如何使用 PowerShell 管理 Azure Stack 中的金鑰保存庫。"
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
ms.openlocfilehash: 71320f8c55d014db6843e6247c53cc07832efc32
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manage-key-vault-in-azure-stack-using-powershell"></a><span data-ttu-id="5456a-103">使用 PowerShell 管理 Azure Stack 中的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="5456a-103">Manage Key Vault in Azure Stack using PowerShell</span></span>

<span data-ttu-id="5456a-104">本文可協助您使用 PowerShell，開始建立和管理 Azure Stack 中的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="5456a-104">This article helps you get started to create and manage Key Vault in Azure Stack by using PowerShell.</span></span> <span data-ttu-id="5456a-105">本文中所述的金鑰保存庫 PowerShell Cmdlet 會隨附於 Azure PowerShell SDK 中。</span><span class="sxs-lookup"><span data-stu-id="5456a-105">The Key Vault PowerShell cmdlets described in this article are available as a part of the Azure PowerShell SDK.</span></span> <span data-ttu-id="5456a-106">下列章節說明建立保存庫、儲存和管理密碼編譯金鑰和祕密，以及授權用者或應用程式叫用保存庫中的作業，所需的 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5456a-106">The following sections describe the PowerShell cmdlets that are required to create a vault, store, and manage cryptographic keys and secrets as well as authorize users or applications to invoke operations in the vault.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5456a-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="5456a-107">Prerequisites</span></span>
* [<span data-ttu-id="5456a-108">安裝適用於 Azure Stack 的 PowerShell</span><span class="sxs-lookup"><span data-stu-id="5456a-108">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* <span data-ttu-id="5456a-109">Azure 堆疊雲端系統管理員必須具有[建立優惠](azure-stack-create-offer.md)包含金鑰保存庫服務。</span><span class="sxs-lookup"><span data-stu-id="5456a-109">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes the Key Vault service.</span></span>  
* <span data-ttu-id="5456a-110">使用者必須[訂閱產品](azure-stack-subscribe-plan-provision-vm.md)，且其包含「金鑰保存庫」服務。</span><span class="sxs-lookup"><span data-stu-id="5456a-110">Users must [subscribe to an offer](azure-stack-subscribe-plan-provision-vm.md) that includes the Key Vault service.</span></span> 
* [<span data-ttu-id="5456a-111">設定 Azure Stack 使用者的 PowerShell 環境</span><span class="sxs-lookup"><span data-stu-id="5456a-111">Configure the Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)

## <a name="enable-your-tenant-subscription-for-vault-operations"></a><span data-ttu-id="5456a-112">針對保存庫作業啟用您的租用戶訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5456a-112">Enable your tenant subscription for vault operations</span></span>

<span data-ttu-id="5456a-113">在您可以發出對金鑰保存庫的任何作業之前，需要先確保已針對保存庫作業啟用您的租用戶訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5456a-113">Before you can issue any operations against a key vault, you need to ensure that your tenant subscription is enabled for vault operations.</span></span> <span data-ttu-id="5456a-114">若要確認，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="5456a-114">To verify, run the following command:</span></span>

```PowerShell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -Autosize
```
<span data-ttu-id="5456a-115">**輸出**</span><span class="sxs-lookup"><span data-stu-id="5456a-115">**Output**</span></span>

<span data-ttu-id="5456a-116">若已針對保存庫作業啟用訂用帳戶，則針對金鑰保存庫的所有資源類型，輸出會顯示「RegistrationState」等於「已註冊」。</span><span class="sxs-lookup"><span data-stu-id="5456a-116">If your subscription is enabled for vault operations, the output shows “RegistrationState” equals “Registered” for all resource types of a key vault.</span></span>

![註冊狀態](media/azure-stack-kv-manage-powershell/image1.png)

<span data-ttu-id="5456a-118">若非如此，請叫用下列命令，註冊您訂用帳戶中的金鑰保存庫服務：</span><span class="sxs-lookup"><span data-stu-id="5456a-118">If that’s not the case, invoke the following command to register the Key Vault service in your subscription:</span></span>

```PowerShell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault
```

<span data-ttu-id="5456a-119">**輸出**</span><span class="sxs-lookup"><span data-stu-id="5456a-119">**Output**</span></span>

<span data-ttu-id="5456a-120">如果註冊成功，會傳回下列輸出：</span><span class="sxs-lookup"><span data-stu-id="5456a-120">If the registration is successful, the following output is returned:</span></span>

![註冊](media/azure-stack-kv-manage-powershell/image2.png)

<span data-ttu-id="5456a-122">下列各節會假設已在使用者訂用帳戶內註冊金鑰保存庫服務。</span><span class="sxs-lookup"><span data-stu-id="5456a-122">The following sections assume Key Vault service is registered within the user subscription.</span></span> <span data-ttu-id="5456a-123">叫用金鑰保存庫命令時，如果您收到錯誤訊息「訂用帳戶未註冊成可使用命名空間 Microsoft.KeyVault」，則請確認您已按照先前所述的指示，[啟用金鑰保存庫的資源提供者](#enable-your-tenant-subscription-for-vault-operations)。</span><span class="sxs-lookup"><span data-stu-id="5456a-123">When invoking key vault commands, if you get an error- "The subscription is not registered to use namespace ‘Microsoft.KeyVault" then, confirm that you have [enabled the Key Vault resource provider](#enable-your-tenant-subscription-for-vault-operations) as per instructions mentioned earlier.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="5456a-124">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="5456a-124">Create a key vault</span></span> 

<span data-ttu-id="5456a-125">建立金鑰保存庫之前，請先建立資源群組，使所有金鑰保存庫相關的資源都存在於資源群組中。</span><span class="sxs-lookup"><span data-stu-id="5456a-125">Before you create a key vault, create a resource group so that all key vault related resources exist in a resource group.</span></span> <span data-ttu-id="5456a-126">請使用下列命令以建立新的資源群組：</span><span class="sxs-lookup"><span data-stu-id="5456a-126">Use the following command to create a new resource group:</span></span>

```PowerShell
New-AzureRmResourceGroup -Name “VaultRG” -Location local -verbose -Force

```

<span data-ttu-id="5456a-127">**輸出**</span><span class="sxs-lookup"><span data-stu-id="5456a-127">**Output**</span></span>

![新的資源群組](media/azure-stack-kv-manage-powershell/image3.png)

<span data-ttu-id="5456a-129">現在，使用 **New-AzureRMKeyVault** 命令，在稍早建立的資源群組中建立金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="5456a-129">Now, use the **New-AzureRMKeyVault** command to create a key vault in the resource group that you created earlier.</span></span> <span data-ttu-id="5456a-130">這個 Cmdlet 會讀取三個必要參數：資源群組名稱、金鑰保存庫名稱和地理位置。</span><span class="sxs-lookup"><span data-stu-id="5456a-130">This command reads three mandatory parameters- resource group name, key vault name, and geographic location.</span></span> 

<span data-ttu-id="5456a-131">請執行下列命令以建立金鑰保存庫：</span><span class="sxs-lookup"><span data-stu-id="5456a-131">Run the following command to create a key vault:</span></span>

```PowerShell
New-AzureRmKeyVault -VaultName “Vault01” -ResourceGroupName “VaultRG” -Location local -verbose
```
<span data-ttu-id="5456a-132">**輸出**</span><span class="sxs-lookup"><span data-stu-id="5456a-132">**Output**</span></span>

![新增金鑰保存庫](media/azure-stack-kv-manage-powershell/image4.png)

<span data-ttu-id="5456a-134">此命令的輸出會顯示您所建立的金鑰保存庫屬性。</span><span class="sxs-lookup"><span data-stu-id="5456a-134">The output of this command shows the properties of the key vault that you created.</span></span> <span data-ttu-id="5456a-135">應用程式存取此保存庫時，會使用此輸出中所顯示的 [保存庫 URI] 屬性。</span><span class="sxs-lookup"><span data-stu-id="5456a-135">When an application accesses this vault, it uses the **Vault URI** property shown in the output.</span></span> <span data-ttu-id="5456a-136">例如，這裡的保存庫 URI是 **https://vault01.vault.local.azurestack.external**。</span><span class="sxs-lookup"><span data-stu-id="5456a-136">For example, the vault URI here is **https://vault01.vault.local.azurestack.external**.</span></span> <span data-ttu-id="5456a-137">透過 REST API 與此金鑰保存庫互動的應用程式必須使用此 URI。</span><span class="sxs-lookup"><span data-stu-id="5456a-137">Applications interacting with this key vault through REST API must use this URI.</span></span>

<span data-ttu-id="5456a-138">在以 ADFS 為基礎的部署中，使用 PowerShell 建立金鑰保存庫時，可能會收到警告，指出「未設定存取原則，</span><span class="sxs-lookup"><span data-stu-id="5456a-138">In ADFS-based deployments, when you create a key vault by using PowerShell, you might receive a warning that says "Access policy is not set.</span></span> <span data-ttu-id="5456a-139">使用者或應用程式沒有使用此保存庫的存取權」。</span><span class="sxs-lookup"><span data-stu-id="5456a-139">No user or application has access permission to use this vault".</span></span> <span data-ttu-id="5456a-140">若要解決此問題，請使用 [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret) 命令，設定保存庫的存取原則：</span><span class="sxs-lookup"><span data-stu-id="5456a-140">To resolve this issue, set an access policy for the vault by using the [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret) command:</span></span>

```PowerShell
# Obtain the security identifier(SID) of the active directory user
$adUser = Get-ADUser -Filter "Name -eq '{Active directory user name}'"
$objectSID = $adUser.SID.Value 

#Set the key vault access policy
Set-AzureRmKeyVaultAccessPolicy -VaultName "{key vault name}" -ResourceGroupName "{resource group name}" -ObjectId "{object SID}" -PermissionsToKeys {permissionsToKeys} -PermissionsToSecrets {permissionsToSecrets} -BypassObjectIdValidation 
```

## <a name="manage-keys-and-secrets"></a><span data-ttu-id="5456a-141">管理金鑰和祕密</span><span class="sxs-lookup"><span data-stu-id="5456a-141">Manage keys and secrets</span></span>

<span data-ttu-id="5456a-142">建立保存庫之後，請使用下列步驟來建立並管理保存庫內的金鑰和祕密。</span><span class="sxs-lookup"><span data-stu-id="5456a-142">After creating a vault, use the following steps to create and manage keys and secrets within the vault.</span></span>

### <a name="create-a-key"></a><span data-ttu-id="5456a-143">建立金鑰</span><span class="sxs-lookup"><span data-stu-id="5456a-143">Create a key</span></span>

<span data-ttu-id="5456a-144">使用 **Add-AzureKeyVaultKey** 命令，建立或匯入金鑰保存庫中受到軟體保護的金鑰。</span><span class="sxs-lookup"><span data-stu-id="5456a-144">Use the **Add-AzureKeyVaultKey** command to create or import a software protected key in a key vault.</span></span> 

```PowerShell
Add-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01” -verbose -Destination Software
```
<span data-ttu-id="5456a-145">[目的地] 參數用來指定金鑰受到軟體保護。</span><span class="sxs-lookup"><span data-stu-id="5456a-145">The **Destination** parameter is used to specify that the key is software protected.</span></span> <span data-ttu-id="5456a-146">成功建立金鑰時，命令會輸出所建立金鑰的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5456a-146">When the key is successfully created, the command outputs the details of the created key.</span></span>

<span data-ttu-id="5456a-147">**輸出**</span><span class="sxs-lookup"><span data-stu-id="5456a-147">**Output**</span></span>

![新金鑰](media/azure-stack-kv-manage-powershell/image5.png)

<span data-ttu-id="5456a-149">您現在可以使用其 URI 參考建立的金鑰。</span><span class="sxs-lookup"><span data-stu-id="5456a-149">You can now reference the created key by using its URI.</span></span> <span data-ttu-id="5456a-150">如果您建立或匯入與現有金鑰名稱相同的金鑰，就會以新金鑰中指定的值來更新原始金鑰。</span><span class="sxs-lookup"><span data-stu-id="5456a-150">If you create or import a key that has same name as an existing key, the original key is updated with the values that are specified in the new key.</span></span>  <span data-ttu-id="5456a-151">您可以使用金鑰的版本特定 URI 來存取先前的版本。</span><span class="sxs-lookup"><span data-stu-id="5456a-151">You can access the previous version by using the version-specific URI of the key.</span></span> <span data-ttu-id="5456a-152">例如，</span><span class="sxs-lookup"><span data-stu-id="5456a-152">For example,</span></span> 

* <span data-ttu-id="5456a-153">使用 **https://vault10.vault.local.azurestack.external:443/keys/key01** 一律會取得目前的版本</span><span class="sxs-lookup"><span data-stu-id="5456a-153">Use **https://vault10.vault.local.azurestack.external:443/keys/key01** to always get the current version</span></span>  
* <span data-ttu-id="5456a-154">使用 **https://vault010.vault.local.azurestack.external:443/keys/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** 則可取得此特定版本</span><span class="sxs-lookup"><span data-stu-id="5456a-154">Use **https://vault010.vault.local.azurestack.external:443/keys/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** to get this specific version</span></span>

### <a name="get-a-key"></a><span data-ttu-id="5456a-155">取得金鑰</span><span class="sxs-lookup"><span data-stu-id="5456a-155">Get a key</span></span>

<span data-ttu-id="5456a-156">使用 **Get AzureKeyVaultKey** 命令可讀金鑰取及其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5456a-156">Use the **Get-AzureKeyVaultKey** command to read a key and its details.</span></span>

```PowerShell
Get-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01”
```

### <a name="create-a-secret"></a><span data-ttu-id="5456a-157">建立祕密</span><span class="sxs-lookup"><span data-stu-id="5456a-157">Create a secret</span></span>

<span data-ttu-id="5456a-158">使用 **Set-AzureKeyVaultSecret** 命令可建立或更新保存庫中的祕密。</span><span class="sxs-lookup"><span data-stu-id="5456a-158">Use the **Set-AzureKeyVaultSecret** command to create or update a secret in a vault.</span></span> <span data-ttu-id="5456a-159">如果祕密不存在，則會建立祕密；如果已經存在，則會建立新版本的祕密。</span><span class="sxs-lookup"><span data-stu-id="5456a-159">A secret is created if it doesn’t already exist, and a new version of the secret is created if it already exists.</span></span>

```PowerShell
$secretvalue = ConvertTo-SecureString “User@123” -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01” -SecretValue $secretvalue
```

<span data-ttu-id="5456a-160">**輸出**</span><span class="sxs-lookup"><span data-stu-id="5456a-160">**Output**</span></span>

![建立祕密](media/azure-stack-kv-manage-powershell/image6.png)

### <a name="get-a-secret"></a><span data-ttu-id="5456a-162">取得祕密</span><span class="sxs-lookup"><span data-stu-id="5456a-162">Get a secret</span></span>

<span data-ttu-id="5456a-163">使用 **Get-AzureKeyVaultSecret** 命令可讀取金鑰保存庫中的祕密。</span><span class="sxs-lookup"><span data-stu-id="5456a-163">Use the **Get-AzureKeyVaultSecret** command to read a secret in a key vault.</span></span> <span data-ttu-id="5456a-164">此命令可傳回所有或特定版本的祕密。</span><span class="sxs-lookup"><span data-stu-id="5456a-164">This command can return all or specific versions of a secret.</span></span> 

```PowerShell
Get-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01”
```

<span data-ttu-id="5456a-165">建立金鑰和祕密之後，您可以授權讓外部應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="5456a-165">After creating keys and secrets, you can authorize external applications to use them.</span></span>

## <a name="authorize-an-application-to-use-a-key-or-secret"></a><span data-ttu-id="5456a-166">授權應用程式使用金鑰或祕密</span><span class="sxs-lookup"><span data-stu-id="5456a-166">Authorize an application to use a key or secret</span></span>

<span data-ttu-id="5456a-167">若要授權讓應用程式存取金鑰保存庫中的金鑰或祕密，請使用 **Set-AzureRmKeyVaultAccessPolicy** 命令。</span><span class="sxs-lookup"><span data-stu-id="5456a-167">To authorize an application to access a key or secret in the key vault, use the **Set-AzureRmKeyVaultAccessPolicy** command.</span></span>
<span data-ttu-id="5456a-168">例如，如果您的保存庫名稱是 ContosoKeyVault 且您想要授權的應用程式用戶端 ID 是 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed。</span><span class="sxs-lookup"><span data-stu-id="5456a-168">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a Client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed.</span></span> <span data-ttu-id="5456a-169">請執行下列命令來授權應用程式。</span><span class="sxs-lookup"><span data-stu-id="5456a-169">Run the following command to authorize the application.</span></span> <span data-ttu-id="5456a-170">或者，您也可以指定 **PermissionsToKeys** 參數以設定使用者、應用程式或安全性群組的權限：</span><span class="sxs-lookup"><span data-stu-id="5456a-170">Optionally, you can specify the **PermissionsToKeys** parameter to set permissions for a user, application, or a security group:</span></span>

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign
```

<span data-ttu-id="5456a-171">如果您想要授權該相同的應用程式讀取您保存庫中的祕密，請執行以下 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="5456a-171">If you want to authorize that same application to read secrets in your vault, run the following cmdlet:</span></span>

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300 -PermissionsToKeys Get
```

## <a name="next-steps"></a><span data-ttu-id="5456a-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5456a-172">Next Steps</span></span>
* [<span data-ttu-id="5456a-173">使用存放在 Key Vault 中的密碼來部署 VM</span><span class="sxs-lookup"><span data-stu-id="5456a-173">Deploy a VM with password stored in a Key Vault</span></span>](azure-stack-kv-deploy-vm-with-secret.md)  
* [<span data-ttu-id="5456a-174">使用存放在 Key Vault 中的憑證來部署 VM</span><span class="sxs-lookup"><span data-stu-id="5456a-174">Deploy a VM with certificate stored in Key Vault</span></span>](azure-stack-kv-push-secret-into-vm.md) 

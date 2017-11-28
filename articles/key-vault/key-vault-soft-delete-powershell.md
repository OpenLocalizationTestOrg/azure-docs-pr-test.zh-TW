---
ms.assetid: 
title: "Azure Key Vault - 如何以 PowerShell 使用虛刪除"
description: "以 PowerShell 程式碼片段進行虛刪除的使用案例範例"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/21/2017
ms.author: bruceper
ms.openlocfilehash: 8cf0674f7eb139e50da4a3c22a8d8376a86b0dcc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-key-vault-soft-delete-with-powershell"></a><span data-ttu-id="9c3a1-103">如何使用 Key Vault 虛刪除與 PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c3a1-103">How to use Key Vault soft-delete with PowerShell</span></span>

<span data-ttu-id="9c3a1-104">Azure Key Vault 的虛刪除功能可復原已刪除的保存庫和保存庫物件。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="9c3a1-105">具體而言，虛刪除解決下列案例：</span><span class="sxs-lookup"><span data-stu-id="9c3a1-105">Specifically, soft-delete addresses the following scenarios:</span></span>

- <span data-ttu-id="9c3a1-106">可復原的 Key Vault 刪除支援</span><span class="sxs-lookup"><span data-stu-id="9c3a1-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="9c3a1-107">支援可復原的金鑰保存庫物件刪除；金鑰、密碼和憑證</span><span class="sxs-lookup"><span data-stu-id="9c3a1-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c3a1-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="9c3a1-108">Prerequisites</span></span>

- <span data-ttu-id="9c3a1-109">Azure PowerShell 4.0.0 或更新版本 - 如果您尚未安裝，請安裝 Azure PowerShell，並將它與 Azure 訂用帳戶建立關聯，請參閱[如何安裝和設定 Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-109">Azure PowerShell 4.0.0 or later - If you don't have this already setup, install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span> 

>[!NOTE]
> <span data-ttu-id="9c3a1-110">載入您的環境的**可能**是過期版本的 Key Vault PowerShell 輸出格式檔案，而不是正確版本。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-110">There is an outdated version of our Key Vault PowerShell output formatting file that **may** be loaded into your environment instead of the correct version.</span></span> <span data-ttu-id="9c3a1-111">我們預計 PowerShell 的更新版本會包含輸出格式所需的更正，屆時將更新此主題。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-111">We are anticipating an updated version of PowerShell to contain the needed correction for the output formatting and will update this topic at that time.</span></span> <span data-ttu-id="9c3a1-112">如果您遇到此格式問題，目前的因應措施是：</span><span class="sxs-lookup"><span data-stu-id="9c3a1-112">The current workaround, should you encounter this formatting problem, is:</span></span>
> - <span data-ttu-id="9c3a1-113">如果您注意到您看不到此主題中所述的已啟用虛刪除的屬性，請使用下列查詢：`$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-113">Use the following query if you notice you're not seeing the soft-delete enabled property described in this topic: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span></span>


<span data-ttu-id="9c3a1-114">如需 PowerShell 的 Key Vault 特定參考資訊，請參閱 [Azure Key Vault PowerShell 參考](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0)。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-114">For Key Vault specific refernece information for PowerShell, see [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="9c3a1-115">所需的權限</span><span class="sxs-lookup"><span data-stu-id="9c3a1-115">Required permissions</span></span>

<span data-ttu-id="9c3a1-116">Key Vault 作業透過角色型存取控制 (RBAC) 權限來分別管理，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9c3a1-116">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="9c3a1-117">作業</span><span class="sxs-lookup"><span data-stu-id="9c3a1-117">Operation</span></span> | <span data-ttu-id="9c3a1-118">說明</span><span class="sxs-lookup"><span data-stu-id="9c3a1-118">Description</span></span> | <span data-ttu-id="9c3a1-119">使用者權限</span><span class="sxs-lookup"><span data-stu-id="9c3a1-119">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="9c3a1-120">列出</span><span class="sxs-lookup"><span data-stu-id="9c3a1-120">List</span></span>|<span data-ttu-id="9c3a1-121">列出已刪除的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-121">Lists deleted key vaults.</span></span>|<span data-ttu-id="9c3a1-122">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="9c3a1-122">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="9c3a1-123">復原</span><span class="sxs-lookup"><span data-stu-id="9c3a1-123">Recover</span></span>|<span data-ttu-id="9c3a1-124">還原已刪除的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-124">Restores a deleted key vault.</span></span>|<span data-ttu-id="9c3a1-125">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="9c3a1-125">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="9c3a1-126">清除</span><span class="sxs-lookup"><span data-stu-id="9c3a1-126">Purge</span></span>|<span data-ttu-id="9c3a1-127">永久移除已刪除的金鑰保存庫和其所有內容。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-127">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="9c3a1-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="9c3a1-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="9c3a1-129">如需權限和存取控制的詳細資訊，請參閱[保護您的金鑰保存庫](key-vault-secure-your-key-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-129">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="9c3a1-130">啟用虛刪除</span><span class="sxs-lookup"><span data-stu-id="9c3a1-130">Enabling soft-delete</span></span>

<span data-ttu-id="9c3a1-131">若要能夠復原已刪除的金鑰保存庫或儲存在金鑰保存庫中的物件，您必須先為該金鑰保存庫啟用虛刪除。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-131">To be able to recover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="9c3a1-132">現有的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="9c3a1-132">Existing key vault</span></span>

<span data-ttu-id="9c3a1-133">對於名為 ContosoVault 的現有金鑰保存庫啟用虛刪除，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-133">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="9c3a1-134">目前，您需要使用 Azure Resource Manager 資源操作來直接寫入 Key Vault 資源的 *enableSoftDelete* 屬性。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-134">Currently you need to use Azure Resource Manager resource manipulation to directly write the *enableSoftDelete* property to the Key Vault resource.</span></span>

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a><span data-ttu-id="9c3a1-135">新的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="9c3a1-135">New key vault</span></span>

<span data-ttu-id="9c3a1-136">為新的金鑰保存庫啟用虛刪除是在建立時完成，方法是新增虛刪除啟用旗標到您的 create 命令。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-136">Enabling soft-delete for a new key vault is done at creation time by adding the soft-delete enable flag to your create command.</span></span>

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="9c3a1-137">驗證啟用虛刪除</span><span class="sxs-lookup"><span data-stu-id="9c3a1-137">Verify soft-delete enablement</span></span>

<span data-ttu-id="9c3a1-138">若要驗證金鑰保存庫已啟用虛刪除，請執行 *get* 命令，並尋找「虛刪除已啟用?」</span><span class="sxs-lookup"><span data-stu-id="9c3a1-138">To verify that a key vault has soft-delete enabled, run the *get* command and look for the 'Soft Delete Enabled?'</span></span> <span data-ttu-id="9c3a1-139">屬性，及其設定 true 或 false。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-139">attribute and its setting, true or false.</span></span>

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="9c3a1-140">刪除虛刪除所保護的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="9c3a1-140">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="9c3a1-141">刪除 (或移除) 金鑰保存庫的命令維持不變，但它的行為會根據您是否已啟用虛刪除而改變。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-141">The command to delete (or remove) a key vault remains the same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
><span data-ttu-id="9c3a1-142">如果您先前針對沒有啟用虛刪除的金鑰保存庫執行命令，您將永久刪除此金鑰保存庫及其所有的內容，並且沒有任何選項可以復原。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-142">If you run the previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="9c3a1-143">虛刪除如何保護您的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="9c3a1-143">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="9c3a1-144">已啟用虛刪除：</span><span class="sxs-lookup"><span data-stu-id="9c3a1-144">With soft-delete enabled:</span></span>

- <span data-ttu-id="9c3a1-145">刪除金鑰保存庫時，它會從其資源群組中移除，並放置於僅與其建立所在位置建立關聯的保留命名空間。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-145">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with the location where it was created.</span></span> 
- <span data-ttu-id="9c3a1-146">已刪除的金鑰保存庫中的物件，例如金鑰、密碼和憑證都無法存取，並且只要包含的金鑰保存庫處於已刪除狀態便維持不變。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-146">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in the deleted state.</span></span> 
- <span data-ttu-id="9c3a1-147">已刪除狀態中的金鑰保存庫 DNS 名稱仍會被保留，因此無法以相同的名稱建立新的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-147">The DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="9c3a1-148">您可以檢視與您的訂用帳戶建立關聯的已刪除狀態金鑰保存庫，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="9c3a1-148">You may view deleted state key vaults, associated with your subscription, using the following command:</span></span>

```powershell
PS C:\> Get-AzureRmKeyVault -InRemovedStateVault 

Name           : ContosoVault
Location             : westus
Id                   : /subscriptions/xxx/providers/Microsoft.KeyVault/locations/westus/deletedVaults/ContosoVault
Resource ID          : /subscriptions/xxx/resourceGroups/ContosoVault/providers/Microsoft.KeyVault/vaults/ContosoVault
Deletion Date        : 5/9/2017 12:14:14 AM
Scheduled Purge Date : 8/7/2017 12:14:14 AM
Tags                 :
```

<span data-ttu-id="9c3a1-149">輸出中的「資源識別碼」是指此保存庫的原始資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-149">The *Resource ID* in the output refers to the original resource ID of this vault.</span></span> <span data-ttu-id="9c3a1-150">因為此金鑰保存庫目前處於已刪除狀態，所以沒有具有該資源識別碼的資源存在。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-150">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="9c3a1-151">「識別碼」欄位可以用來在復原或清除時識別資源。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-151">The *Id* field can be used to identify the resource when recovering, or purging.</span></span> <span data-ttu-id="9c3a1-152">「排定清除日期」欄位指出如果對這個已刪除的保存庫不採取任何動作，何時將永久刪除 (清除) 保存庫。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-152">The *Scheduled Purge Date* field indicates when the vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="9c3a1-153">用來計算「排定清除日期」的預設保留期間為 90 天。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-153">The default retention period, used to calculate the *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="9c3a1-154">復原金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="9c3a1-154">Recovering a key vault</span></span>

<span data-ttu-id="9c3a1-155">若要復原金鑰保存庫，您需要指定金鑰保存庫名稱、資源群組和位置。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-155">To recover a key vault, you need to specify the key vault name, resource group, and location.</span></span> <span data-ttu-id="9c3a1-156">請記下已刪除之金鑰保存庫的位置和資源群組，因為您需要這些才能進行金鑰保存庫復原程序。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-156">Note the location and the resource group of the deleted key vault as you need these for a key vault recovery process.</span></span>

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

<span data-ttu-id="9c3a1-157">在金鑰保存庫復原之後，結果會是新的資源，並具有金鑰保存庫的原始資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-157">When a key vault is recovered, the result is a new resource with the key vault's original resource ID.</span></span> <span data-ttu-id="9c3a1-158">如果金鑰保存庫存在的資源群組已被移除，則必須先建立具有相同名稱的新資源群組，才能復原金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-158">If the resource group where the key vault existed has been removed, a new resource group with same name must be created before the key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="9c3a1-159">金鑰保存庫物件和虛刪除</span><span class="sxs-lookup"><span data-stu-id="9c3a1-159">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="9c3a1-160">對於已啟用虛刪除的金鑰保存庫 'ContosoVault'，其中的金鑰 'ContosoFirstKey'，以下為該金鑰的刪除方式。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-160">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="9c3a1-161">在金鑰保存庫啟用虛刪除的情況下，已刪除的金鑰仍會看似已刪除，例外情況是當您明確地列出或擷取已刪除的金鑰時。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-161">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="9c3a1-162">對於已刪除狀態的金鑰，大部分作業會失敗，只除了列出、復原或清除已刪除的金鑰時例外。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-162">Most operations on a key in the deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="9c3a1-163">例如，若要要求列出金鑰保存庫中的已刪除金鑰，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="9c3a1-163">For example, to request to list deleted keys in a key vault, use the following command:</span></span>

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a><span data-ttu-id="9c3a1-164">轉換狀態</span><span class="sxs-lookup"><span data-stu-id="9c3a1-164">Transition state</span></span> 

<span data-ttu-id="9c3a1-165">當您刪除金鑰保存庫中的金鑰，並且已啟用虛刪除時，可能需要幾秒鐘的時間讓轉換完成。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-165">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for the transition to complete.</span></span> <span data-ttu-id="9c3a1-166">在此轉換狀態期間，可能會出現金鑰不在使用中狀態或已刪除狀態。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-166">During this transition state, it may appear that the key is not in the active state or the deleted state.</span></span> <span data-ttu-id="9c3a1-167">此命令會列出名為 'ContosoVault' 的金鑰保存庫中，所有已刪除的金鑰。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-167">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```powershell
  Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
  Vault Name           : ContosoVault
  Name                 : ContosoFirstKey
  Id                   : https://ContosoVault.vault.azure.net:443/keys/ContosoFirstKey
  Deleted Date         : 2/14/2017 8:20:52 PM
  Scheduled Purge Date : 5/15/2017 8:20:52 PM
  Enabled              : True
  Expires              :
  Not Before           :
  Created              : 2/14/2017 8:16:07 PM
  Updated              : 2/14/2017 8:16:07 PM
  Tags                 :
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="9c3a1-168">對金鑰保存庫物件使用虛刪除</span><span class="sxs-lookup"><span data-stu-id="9c3a1-168">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="9c3a1-169">就像金鑰保存庫，已刪除的金鑰、密碼或憑證仍然會維時在已刪除狀態長達 90 天，除非加以復原或清除。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-169">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up to 90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="9c3a1-170">之間的信任</span><span class="sxs-lookup"><span data-stu-id="9c3a1-170">Keys</span></span>

<span data-ttu-id="9c3a1-171">復原已刪除的金鑰：</span><span class="sxs-lookup"><span data-stu-id="9c3a1-171">To recover a deleted key:</span></span>

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="9c3a1-172">永久刪除金鑰：</span><span class="sxs-lookup"><span data-stu-id="9c3a1-172">To permanently delete a key:</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
><span data-ttu-id="9c3a1-173">清除金鑰會永久刪除它，這表示它將無法復原。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-173">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="9c3a1-174">**復原**和**清除**動作在金鑰保存庫存取原則中有自己的相關聯權限。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-174">The **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="9c3a1-175">使用者或服務主體若要能夠執行**復原**或**清除**動作，必須在金鑰保存庫存取原則中有該物件 (金鑰或密碼) 的個別權限。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-175">For a user or service principal to be able to execute a **recover** or **purge** action they must have the respective permission for that object (key or secret) in the key vault access policy.</span></span> <span data-ttu-id="9c3a1-176">根據預設，**清除**權限不會在 'all' 捷徑用於授與所有權限給使用者時，新增到金鑰保存庫的存取原則。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-176">By default, the **purge** permission is not added to a key vault's access policy when the 'all' shortcut is used to grant all permissions to a user.</span></span> <span data-ttu-id="9c3a1-177">您必須明確授與**清除**權限。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-177">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="9c3a1-178">例如，下列命令授與 user@contoso.com 對 *ContosoVault* 中的金鑰執行數種作業的權限，這其中包括**清除**。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-178">For example, the following command grants user@contoso.com permission to perform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="9c3a1-179">設定金鑰保存庫存取原則</span><span class="sxs-lookup"><span data-stu-id="9c3a1-179">Set a key vault access policy</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> <span data-ttu-id="9c3a1-180">如果您有現有的金鑰保存庫，且剛剛啟用虛刪除，您可能沒有**復原**和**清除**權限。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-180">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="9c3a1-181">密碼</span><span class="sxs-lookup"><span data-stu-id="9c3a1-181">Secrets</span></span>

<span data-ttu-id="9c3a1-182">就像金鑰，金鑰保存庫中的密碼會有自己的操作指令。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-182">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="9c3a1-183">以下是刪除、列出、復原和清除密碼的命令。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-183">Following, are the commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="9c3a1-184">刪除名為 SQLPassword 的密碼：</span><span class="sxs-lookup"><span data-stu-id="9c3a1-184">Delete a secret named SQLPassword:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- <span data-ttu-id="9c3a1-185">列出金鑰保存庫中的所有已刪除密碼：</span><span class="sxs-lookup"><span data-stu-id="9c3a1-185">List all deleted secrets in a key vault:</span></span> 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- <span data-ttu-id="9c3a1-186">復原已刪除狀態的密碼：</span><span class="sxs-lookup"><span data-stu-id="9c3a1-186">Recover a secret in the deleted state:</span></span> 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- <span data-ttu-id="9c3a1-187">清除已刪除狀態的密碼：</span><span class="sxs-lookup"><span data-stu-id="9c3a1-187">Purge a secret in deleted state:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
><span data-ttu-id="9c3a1-188">清除密碼會永久刪除它，這表示它將無法復原。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-188">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="9c3a1-189">清除金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="9c3a1-189">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="9c3a1-190">金鑰保存庫物件</span><span class="sxs-lookup"><span data-stu-id="9c3a1-190">Key vault objects</span></span>

<span data-ttu-id="9c3a1-191">清除金鑰、密碼或憑證會永久刪除它，這表示它將無法復原。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-191">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="9c3a1-192">不過，包含已刪除之物件的金鑰保存庫會維持不變，金鑰保存庫中的所有其他物件也是。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-192">The key vault that contained the deleted object will however remain intact as will all other objects in the key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="9c3a1-193">金鑰保存庫作為容器</span><span class="sxs-lookup"><span data-stu-id="9c3a1-193">Key vaults as containers</span></span>
<span data-ttu-id="9c3a1-194">當清除金鑰保存庫時，它的所有內容，包括金鑰、密碼和憑證，都會永久刪除。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-194">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="9c3a1-195">若要清除金鑰保存庫，請使用 `Remove-AzureRmKeyVault` 命令與 `-InRemovedState` 選項，並使用 `-Location location` 引數指定已刪除之金鑰保存庫的位置。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-195">To purge a key vault, use the `Remove-AzureRmKeyVault` command with the option `-InRemovedState` and by specifying the location of the deleted key vault with the `-Location location` argument.</span></span> <span data-ttu-id="9c3a1-196">您可以使用命令 `Get-AzureRmKeyVault -InRemovedState` 找到已刪除之保存庫的位置。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-196">You can find the location of a deleted vault using the command `Get-AzureRmKeyVault -InRemovedState`.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
><span data-ttu-id="9c3a1-197">清除金鑰保存庫會永久刪除它，這表示它將無法復原。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-197">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="9c3a1-198">所需的清除權限</span><span class="sxs-lookup"><span data-stu-id="9c3a1-198">Purge permissions required</span></span>
- <span data-ttu-id="9c3a1-199">若要清除已刪除的金鑰保存庫，以便保存庫和其所有內容永久移除，使用者需要執行 *Microsoft.KeyVault/locations/deletedVaults/purge/action* 作業的 RBAC 權限。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-199">To purge a deleted key vault, such that the vault and all its contents are permanently removed, the user needs RBAC permission to perform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="9c3a1-200">若要列出已刪除的金鑰保存庫，使用者需要執行 *Microsoft.KeyVault/deletedVaults/read* 作業的 RBAC 權限。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-200">To list the deleted key, the vault a user needs RBAC permission to perform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="9c3a1-201">根據預設，只有訂用帳戶管理員擁有這些權限。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-201">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="9c3a1-202">排定的清除</span><span class="sxs-lookup"><span data-stu-id="9c3a1-202">Scheduled purge</span></span>

<span data-ttu-id="9c3a1-203">列出您的已刪除金鑰保存庫物件，會顯示它們排定要由金鑰保存庫清除的時間。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-203">Listing your deleted key vault objects shows when they are schedled to be purged by Key Vault.</span></span> <span data-ttu-id="9c3a1-204">「排定清除日期」欄位指出如果不採取任何動作，何時將永久刪除金鑰保存庫物件。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-204">The *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="9c3a1-205">根據預設，已刪除的金鑰保存庫物件的保留期限為 90 天。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-205">By default, the retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="9c3a1-206">已清除的保存庫物件，由其「排定清除日期」欄位觸發，會永久刪除。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-206">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="9c3a1-207">無法復原。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-207">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="9c3a1-208">其他資源</span><span class="sxs-lookup"><span data-stu-id="9c3a1-208">Other resources</span></span>

- <span data-ttu-id="9c3a1-209">如需 Key Vault 的虛刪除功能概觀，請參閱 [Azure Key Vault 虛刪除概觀](key-vault-ovw-soft-delete.md)。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-209">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="9c3a1-210">如需 Azure Key Vault 使用的一般概觀，請參閱[開始使用 Azure Key Vault](key-vault-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="9c3a1-210">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>


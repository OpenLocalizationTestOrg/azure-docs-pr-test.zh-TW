---
ms.assetid: 
title: "aaaAzure 金鑰保存庫-如何 toouse 虛刪除使用 PowerShell"
description: "以 PowerShell 程式碼片段進行虛刪除的使用案例範例"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/21/2017
ms.author: bruceper
ms.openlocfilehash: 4968b700a14f764ea1be7de2bf3697664f255f95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-powershell"></a><span data-ttu-id="81da0-103">如何 toouse 金鑰保存庫虛刪除使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="81da0-103">How toouse Key Vault soft-delete with PowerShell</span></span>

<span data-ttu-id="81da0-104">Azure Key Vault 的虛刪除功能可復原已刪除的保存庫和保存庫物件。</span><span class="sxs-lookup"><span data-stu-id="81da0-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="81da0-105">具體來說，虛刪除位址 hello 下列案例：</span><span class="sxs-lookup"><span data-stu-id="81da0-105">Specifically, soft-delete addresses hello following scenarios:</span></span>

- <span data-ttu-id="81da0-106">可復原的 Key Vault 刪除支援</span><span class="sxs-lookup"><span data-stu-id="81da0-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="81da0-107">支援可復原的金鑰保存庫物件刪除；金鑰、密碼和憑證</span><span class="sxs-lookup"><span data-stu-id="81da0-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81da0-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="81da0-108">Prerequisites</span></span>

- <span data-ttu-id="81da0-109">Azure PowerShell 4.0.0 或更新版本-如果沒有此已經安裝，安裝 Azure PowerShell，然後將它與您 Azure 訂用帳戶產生關聯，請參閱[如何 tooinstall 和設定 Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="81da0-109">Azure PowerShell 4.0.0 or later - If you don't have this already setup, install Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span> 

>[!NOTE]
> <span data-ttu-id="81da0-110">沒有過期的版本，我們金鑰保存庫 PowerShell 的輸出格式的檔案，**可能**先載入到您的環境，而不是 hello 正確版本。</span><span class="sxs-lookup"><span data-stu-id="81da0-110">There is an outdated version of our Key Vault PowerShell output formatting file that **may** be loaded into your environment instead of hello correct version.</span></span> <span data-ttu-id="81da0-111">我們會預期 PowerShell toocontain hello 的更新的版本需要更正 hello 輸出格式，並將更新本主題在該時間。</span><span class="sxs-lookup"><span data-stu-id="81da0-111">We are anticipating an updated version of PowerShell toocontain hello needed correction for hello output formatting and will update this topic at that time.</span></span> <span data-ttu-id="81da0-112">hello 目前的因應措施，您應該會發生這個格式的問題是：</span><span class="sxs-lookup"><span data-stu-id="81da0-112">hello current workaround, should you encounter this formatting problem, is:</span></span>
> - <span data-ttu-id="81da0-113">使用下列查詢，如果您注意到您看不到 hello 虛刪除的 hello 啟用本主題中所述的屬性： `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`。</span><span class="sxs-lookup"><span data-stu-id="81da0-113">Use hello following query if you notice you're not seeing hello soft-delete enabled property described in this topic: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span></span>


<span data-ttu-id="81da0-114">如需 PowerShell 的 Key Vault 特定參考資訊，請參閱 [Azure Key Vault PowerShell 參考](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0)。</span><span class="sxs-lookup"><span data-stu-id="81da0-114">For Key Vault specific refernece information for PowerShell, see [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="81da0-115">所需的權限</span><span class="sxs-lookup"><span data-stu-id="81da0-115">Required permissions</span></span>

<span data-ttu-id="81da0-116">Key Vault 作業透過角色型存取控制 (RBAC) 權限來分別管理，如下所示：</span><span class="sxs-lookup"><span data-stu-id="81da0-116">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="81da0-117">作業</span><span class="sxs-lookup"><span data-stu-id="81da0-117">Operation</span></span> | <span data-ttu-id="81da0-118">說明</span><span class="sxs-lookup"><span data-stu-id="81da0-118">Description</span></span> | <span data-ttu-id="81da0-119">使用者權限</span><span class="sxs-lookup"><span data-stu-id="81da0-119">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="81da0-120">列出</span><span class="sxs-lookup"><span data-stu-id="81da0-120">List</span></span>|<span data-ttu-id="81da0-121">列出已刪除的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="81da0-121">Lists deleted key vaults.</span></span>|<span data-ttu-id="81da0-122">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="81da0-122">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="81da0-123">復原</span><span class="sxs-lookup"><span data-stu-id="81da0-123">Recover</span></span>|<span data-ttu-id="81da0-124">還原已刪除的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="81da0-124">Restores a deleted key vault.</span></span>|<span data-ttu-id="81da0-125">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="81da0-125">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="81da0-126">清除</span><span class="sxs-lookup"><span data-stu-id="81da0-126">Purge</span></span>|<span data-ttu-id="81da0-127">永久移除已刪除的金鑰保存庫和其所有內容。</span><span class="sxs-lookup"><span data-stu-id="81da0-127">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="81da0-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="81da0-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="81da0-129">如需權限和存取控制的詳細資訊，請參閱[保護您的金鑰保存庫](key-vault-secure-your-key-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="81da0-129">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="81da0-130">啟用虛刪除</span><span class="sxs-lookup"><span data-stu-id="81da0-130">Enabling soft-delete</span></span>

<span data-ttu-id="81da0-131">toobe 無法 toorecover 已刪除的金鑰保存庫或物件儲存在金鑰保存庫，您必須先啟用虛刪除該金鑰的保存庫。</span><span class="sxs-lookup"><span data-stu-id="81da0-131">toobe able toorecover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="81da0-132">現有的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="81da0-132">Existing key vault</span></span>

<span data-ttu-id="81da0-133">對於名為 ContosoVault 的現有金鑰保存庫啟用虛刪除，如下所示。</span><span class="sxs-lookup"><span data-stu-id="81da0-133">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="81da0-134">目前您需要 toouse Azure 資源管理員資源操作 toodirectly 寫入 hello *enableSoftDelete*屬性 toohello 金鑰保存庫資源。</span><span class="sxs-lookup"><span data-stu-id="81da0-134">Currently you need toouse Azure Resource Manager resource manipulation toodirectly write hello *enableSoftDelete* property toohello Key Vault resource.</span></span>

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a><span data-ttu-id="81da0-135">新的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="81da0-135">New key vault</span></span>

<span data-ttu-id="81da0-136">啟用虛刪除新的金鑰保存庫是在建立時新增 hello 虛刪除啟用旗標 tooyour 建立命令。</span><span class="sxs-lookup"><span data-stu-id="81da0-136">Enabling soft-delete for a new key vault is done at creation time by adding hello soft-delete enable flag tooyour create command.</span></span>

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="81da0-137">驗證啟用虛刪除</span><span class="sxs-lookup"><span data-stu-id="81da0-137">Verify soft-delete enablement</span></span>

<span data-ttu-id="81da0-138">tooverify 的金鑰保存庫已虛刪除啟用，執行 hello*取得*命令，並尋找 hello ' 虛刪除 Enabled？ '</span><span class="sxs-lookup"><span data-stu-id="81da0-138">tooverify that a key vault has soft-delete enabled, run hello *get* command and look for hello 'Soft Delete Enabled?'</span></span> <span data-ttu-id="81da0-139">屬性，及其設定 true 或 false。</span><span class="sxs-lookup"><span data-stu-id="81da0-139">attribute and its setting, true or false.</span></span>

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="81da0-140">刪除虛刪除所保護的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="81da0-140">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="81da0-141">hello 命令 toodelete （或移除） 金鑰保存庫會維持的 hello 相同，但其行為變更會根據您是否已啟用虛刪除與否。</span><span class="sxs-lookup"><span data-stu-id="81da0-141">hello command toodelete (or remove) a key vault remains hello same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
><span data-ttu-id="81da0-142">如果您要執行 hello 的金鑰保存庫，但是沒有啟用虛刪除的前一個命令，您將永久刪除此金鑰保存庫並不使用任何選項，復原所有的內容。</span><span class="sxs-lookup"><span data-stu-id="81da0-142">If you run hello previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="81da0-143">虛刪除如何保護您的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="81da0-143">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="81da0-144">已啟用虛刪除：</span><span class="sxs-lookup"><span data-stu-id="81da0-144">With soft-delete enabled:</span></span>

- <span data-ttu-id="81da0-145">刪除金鑰保存庫時，它會從其資源群組中移除，並放置於僅保留命名空間建立所在的 hello 位置相關聯。</span><span class="sxs-lookup"><span data-stu-id="81da0-145">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with hello location where it was created.</span></span> 
- <span data-ttu-id="81da0-146">已刪除的索引鍵中的物件保存庫，例如金鑰、 密碼和憑證，都無法存取，以及其包含的金鑰保存庫在 hello 刪除狀態時維持不變。</span><span class="sxs-lookup"><span data-stu-id="81da0-146">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in hello deleted state.</span></span> 
- <span data-ttu-id="81da0-147">hello DNS 名稱的金鑰保存庫中已刪除狀態是仍保留，因此無法建立新的金鑰保存庫相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="81da0-147">hello DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="81da0-148">您可以檢視已刪除的狀態金鑰保存庫，您的訂用帳戶，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="81da0-148">You may view deleted state key vaults, associated with your subscription, using hello following command:</span></span>

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

<span data-ttu-id="81da0-149">hello*資源識別碼*在 hello 輸出是指 toohello 此保存庫的原始資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="81da0-149">hello *Resource ID* in hello output refers toohello original resource ID of this vault.</span></span> <span data-ttu-id="81da0-150">因為此金鑰保存庫目前處於已刪除狀態，所以沒有具有該資源識別碼的資源存在。</span><span class="sxs-lookup"><span data-stu-id="81da0-150">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="81da0-151">hello*識別碼*欄位可以是復原，或清除時，使用的 tooidentify hello 資源。</span><span class="sxs-lookup"><span data-stu-id="81da0-151">hello *Id* field can be used tooidentify hello resource when recovering, or purging.</span></span> <span data-ttu-id="81da0-152">hello*排定清除日期*欄位會指出何時將永久刪除 hello 保存庫 （清除） 如果此刪除保存庫會不採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="81da0-152">hello *Scheduled Purge Date* field indicates when hello vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="81da0-153">hello 預設保留期間，已使用 toocalculate hello*排定清除日期*，為 90 天。</span><span class="sxs-lookup"><span data-stu-id="81da0-153">hello default retention period, used toocalculate hello *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="81da0-154">復原金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="81da0-154">Recovering a key vault</span></span>

<span data-ttu-id="81da0-155">toorecover 金鑰保存庫，您需要 toospecify hello 金鑰保存庫名稱、 資源群組和位置。</span><span class="sxs-lookup"><span data-stu-id="81da0-155">toorecover a key vault, you need toospecify hello key vault name, resource group, and location.</span></span> <span data-ttu-id="81da0-156">請記下 hello 位置和 hello 的 hello 刪除金鑰保存庫的資源群組，您需要這些序號進行金鑰保存庫復原程序。</span><span class="sxs-lookup"><span data-stu-id="81da0-156">Note hello location and hello resource group of hello deleted key vault as you need these for a key vault recovery process.</span></span>

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

<span data-ttu-id="81da0-157">當復原金鑰的保存庫時，hello 結果會是新的資源，並提供原始 hello 金鑰保存庫的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="81da0-157">When a key vault is recovered, hello result is a new resource with hello key vault's original resource ID.</span></span> <span data-ttu-id="81da0-158">如果已經移除了 hello hello 金鑰保存庫的存在其中的資源群組，就必須建立新的資源群組具有相同名稱 hello 金鑰保存庫可以在復原之前。</span><span class="sxs-lookup"><span data-stu-id="81da0-158">If hello resource group where hello key vault existed has been removed, a new resource group with same name must be created before hello key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="81da0-159">金鑰保存庫物件和虛刪除</span><span class="sxs-lookup"><span data-stu-id="81da0-159">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="81da0-160">對於已啟用虛刪除的金鑰保存庫 'ContosoVault'，其中的金鑰 'ContosoFirstKey'，以下為該金鑰的刪除方式。</span><span class="sxs-lookup"><span data-stu-id="81da0-160">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="81da0-161">在金鑰保存庫啟用虛刪除的情況下，已刪除的金鑰仍會看似已刪除，例外情況是當您明確地列出或擷取已刪除的金鑰時。</span><span class="sxs-lookup"><span data-stu-id="81da0-161">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="81da0-162">除了列出的已刪除的索引鍵、 將其復原或清除它，將會失敗 hello 刪除狀態中的索引鍵上的大部分作業。</span><span class="sxs-lookup"><span data-stu-id="81da0-162">Most operations on a key in hello deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="81da0-163">比方說，toorequest toolist 刪除金鑰在金鑰保存庫中，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="81da0-163">For example, toorequest toolist deleted keys in a key vault, use hello following command:</span></span>

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a><span data-ttu-id="81da0-164">轉換狀態</span><span class="sxs-lookup"><span data-stu-id="81da0-164">Transition state</span></span> 

<span data-ttu-id="81da0-165">當您刪除金鑰保存庫中的索引鍵與啟用虛刪除時，可能需要數秒鐘，讓 hello 轉換 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="81da0-165">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for hello transition toocomplete.</span></span> <span data-ttu-id="81da0-166">在此轉換狀態，它可能會出現該 hello 索引鍵不在 hello 作用中狀態或 hello 刪除狀態。</span><span class="sxs-lookup"><span data-stu-id="81da0-166">During this transition state, it may appear that hello key is not in hello active state or hello deleted state.</span></span> <span data-ttu-id="81da0-167">此命令會列出名為 'ContosoVault' 的金鑰保存庫中，所有已刪除的金鑰。</span><span class="sxs-lookup"><span data-stu-id="81da0-167">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

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

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="81da0-168">對金鑰保存庫物件使用虛刪除</span><span class="sxs-lookup"><span data-stu-id="81da0-168">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="81da0-169">就像金鑰保存庫，已刪除的索引鍵，密碼或憑證仍然會在已刪除狀態向上 too90 天除非加以復原，或清除它。</span><span class="sxs-lookup"><span data-stu-id="81da0-169">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up too90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="81da0-170">之間的信任</span><span class="sxs-lookup"><span data-stu-id="81da0-170">Keys</span></span>

<span data-ttu-id="81da0-171">toorecover 已刪除的索引鍵：</span><span class="sxs-lookup"><span data-stu-id="81da0-171">toorecover a deleted key:</span></span>

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="81da0-172">toopermanently 刪除機碼：</span><span class="sxs-lookup"><span data-stu-id="81da0-172">toopermanently delete a key:</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
><span data-ttu-id="81da0-173">清除金鑰會永久刪除它，這表示它將無法復原。</span><span class="sxs-lookup"><span data-stu-id="81da0-173">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="81da0-174">hello**復原**和**清除**動作具有自己在金鑰保存庫的存取原則相關聯的權限。</span><span class="sxs-lookup"><span data-stu-id="81da0-174">hello **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="81da0-175">為使用者或服務主體 toobe 無法 tooexecute**復原**或**清除**它們必須 hello 金鑰保存庫的存取原則中個別 hello （金鑰或密碼），該物件權限的動作。</span><span class="sxs-lookup"><span data-stu-id="81da0-175">For a user or service principal toobe able tooexecute a **recover** or **purge** action they must have hello respective permission for that object (key or secret) in hello key vault access policy.</span></span> <span data-ttu-id="81da0-176">根據預設，hello**清除**權限不會加入 tooa 金鑰保存庫的存取原則時 hello 'all' 的快顯使用的 toogrant tooa 使用者所有的權限。</span><span class="sxs-lookup"><span data-stu-id="81da0-176">By default, hello **purge** permission is not added tooa key vault's access policy when hello 'all' shortcut is used toogrant all permissions tooa user.</span></span> <span data-ttu-id="81da0-177">您必須明確授與**清除**權限。</span><span class="sxs-lookup"><span data-stu-id="81da0-177">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="81da0-178">例如，下列命令授與來 hellouser@contoso.com權限 tooperform 多個作業中的索引鍵*ContosoVault*包括**清除**。</span><span class="sxs-lookup"><span data-stu-id="81da0-178">For example, hello following command grants user@contoso.com permission tooperform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="81da0-179">設定金鑰保存庫存取原則</span><span class="sxs-lookup"><span data-stu-id="81da0-179">Set a key vault access policy</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> <span data-ttu-id="81da0-180">如果您有現有的金鑰保存庫，且剛剛啟用虛刪除，您可能沒有**復原**和**清除**權限。</span><span class="sxs-lookup"><span data-stu-id="81da0-180">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="81da0-181">密碼</span><span class="sxs-lookup"><span data-stu-id="81da0-181">Secrets</span></span>

<span data-ttu-id="81da0-182">就像金鑰，金鑰保存庫中的密碼會有自己的操作指令。</span><span class="sxs-lookup"><span data-stu-id="81da0-182">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="81da0-183">遵循，是 hello 命令，以刪除、 列出、 復原，並清除密碼。</span><span class="sxs-lookup"><span data-stu-id="81da0-183">Following, are hello commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="81da0-184">刪除名為 SQLPassword 的密碼：</span><span class="sxs-lookup"><span data-stu-id="81da0-184">Delete a secret named SQLPassword:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- <span data-ttu-id="81da0-185">列出金鑰保存庫中的所有已刪除密碼：</span><span class="sxs-lookup"><span data-stu-id="81da0-185">List all deleted secrets in a key vault:</span></span> 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- <span data-ttu-id="81da0-186">復原密碼，以處於已刪除的 hello:</span><span class="sxs-lookup"><span data-stu-id="81da0-186">Recover a secret in hello deleted state:</span></span> 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- <span data-ttu-id="81da0-187">清除已刪除狀態的密碼：</span><span class="sxs-lookup"><span data-stu-id="81da0-187">Purge a secret in deleted state:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
><span data-ttu-id="81da0-188">清除密碼會永久刪除它，這表示它將無法復原。</span><span class="sxs-lookup"><span data-stu-id="81da0-188">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="81da0-189">清除金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="81da0-189">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="81da0-190">金鑰保存庫物件</span><span class="sxs-lookup"><span data-stu-id="81da0-190">Key vault objects</span></span>

<span data-ttu-id="81da0-191">清除金鑰、密碼或憑證會永久刪除它，這表示它將無法復原。</span><span class="sxs-lookup"><span data-stu-id="81da0-191">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="81da0-192">將會在 hello 金鑰保存庫中的所有其他物件，包含 hello 刪除物件的 hello 金鑰保存庫會不過維持不變。</span><span class="sxs-lookup"><span data-stu-id="81da0-192">hello key vault that contained hello deleted object will however remain intact as will all other objects in hello key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="81da0-193">金鑰保存庫作為容器</span><span class="sxs-lookup"><span data-stu-id="81da0-193">Key vaults as containers</span></span>
<span data-ttu-id="81da0-194">當清除金鑰保存庫時，它的所有內容，包括金鑰、密碼和憑證，都會永久刪除。</span><span class="sxs-lookup"><span data-stu-id="81da0-194">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="81da0-195">toopurge 金鑰保存庫中，使用 hello`Remove-AzureRmKeyVault`命令與 hello 選項`-InRemovedState`和藉由指定的金鑰保存庫刪除 hello hello 位置以 hello`-Location location`引數。</span><span class="sxs-lookup"><span data-stu-id="81da0-195">toopurge a key vault, use hello `Remove-AzureRmKeyVault` command with hello option `-InRemovedState` and by specifying hello location of hello deleted key vault with hello `-Location location` argument.</span></span> <span data-ttu-id="81da0-196">您可以找到使用 hello 命令刪除保存庫的 hello 位置`Get-AzureRmKeyVault -InRemovedState`。</span><span class="sxs-lookup"><span data-stu-id="81da0-196">You can find hello location of a deleted vault using hello command `Get-AzureRmKeyVault -InRemovedState`.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
><span data-ttu-id="81da0-197">清除金鑰保存庫會永久刪除它，這表示它將無法復原。</span><span class="sxs-lookup"><span data-stu-id="81da0-197">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="81da0-198">所需的清除權限</span><span class="sxs-lookup"><span data-stu-id="81da0-198">Purge permissions required</span></span>
- <span data-ttu-id="81da0-199">toopurge 已刪除的金鑰保存庫，使得 hello 保存庫和其所有內容都將會永久移除，hello 使用者需要 RBAC 權限 tooperform *Microsoft.KeyVault/locations/deletedVaults/purge/action*作業。</span><span class="sxs-lookup"><span data-stu-id="81da0-199">toopurge a deleted key vault, such that hello vault and all its contents are permanently removed, hello user needs RBAC permission tooperform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="81da0-200">toolist hello 刪除金鑰，hello 保存庫的使用者需要 RBAC 權限 tooperform *Microsoft.KeyVault/deletedVaults/read*權限。</span><span class="sxs-lookup"><span data-stu-id="81da0-200">toolist hello deleted key, hello vault a user needs RBAC permission tooperform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="81da0-201">根據預設，只有訂用帳戶管理員擁有這些權限。</span><span class="sxs-lookup"><span data-stu-id="81da0-201">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="81da0-202">排定的清除</span><span class="sxs-lookup"><span data-stu-id="81da0-202">Scheduled purge</span></span>

<span data-ttu-id="81da0-203">列出您已刪除的金鑰保存庫的物件顯示它們 schedled toobe 清除金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="81da0-203">Listing your deleted key vault objects shows when they are schedled toobe purged by Key Vault.</span></span> <span data-ttu-id="81da0-204">hello*排定清除日期*欄位會指出當您將永久刪除這項金鑰保存庫物件，如果未不採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="81da0-204">hello *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="81da0-205">根據預設，已刪除的金鑰保存庫物件的 hello 保留期限為 90 天。</span><span class="sxs-lookup"><span data-stu-id="81da0-205">By default, hello retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="81da0-206">已清除的保存庫物件，由其「排定清除日期」欄位觸發，會永久刪除。</span><span class="sxs-lookup"><span data-stu-id="81da0-206">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="81da0-207">無法復原。</span><span class="sxs-lookup"><span data-stu-id="81da0-207">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="81da0-208">其他資源</span><span class="sxs-lookup"><span data-stu-id="81da0-208">Other resources</span></span>

- <span data-ttu-id="81da0-209">如需 Key Vault 的虛刪除功能概觀，請參閱 [Azure Key Vault 虛刪除概觀](key-vault-ovw-soft-delete.md)。</span><span class="sxs-lookup"><span data-stu-id="81da0-209">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="81da0-210">如需 Azure Key Vault 使用的一般概觀，請參閱[開始使用 Azure Key Vault](key-vault-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="81da0-210">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>


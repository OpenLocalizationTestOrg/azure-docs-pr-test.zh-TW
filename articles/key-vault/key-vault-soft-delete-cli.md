---
ms.assetid: 
title: "aaaAzure 金鑰保存庫-如何 toouse 虛刪除與 CLI"
description: "以 CLI 程式碼片段進行虛刪除的使用案例範例"
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 672f5210ab119c244ca712f0bb80b653b50ea79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-cli"></a><span data-ttu-id="fcd1e-103">如何 toouse 金鑰保存庫虛刪除與 CLI</span><span class="sxs-lookup"><span data-stu-id="fcd1e-103">How toouse Key Vault soft-delete with CLI</span></span>

<span data-ttu-id="fcd1e-104">Azure Key Vault 的虛刪除功能可復原已刪除的保存庫和保存庫物件。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="fcd1e-105">具體來說，虛刪除位址 hello 下列案例：</span><span class="sxs-lookup"><span data-stu-id="fcd1e-105">Specifically, soft-delete addresses hello following scenarios:</span></span>

- <span data-ttu-id="fcd1e-106">可復原的 Key Vault 刪除支援</span><span class="sxs-lookup"><span data-stu-id="fcd1e-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="fcd1e-107">支援可復原的金鑰保存庫物件刪除；金鑰、密碼和憑證</span><span class="sxs-lookup"><span data-stu-id="fcd1e-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcd1e-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="fcd1e-108">Prerequisites</span></span>

- <span data-ttu-id="fcd1e-109">Azure CLI 2.0 - 如果您沒有為您的環境進行此安裝，請參閱[使用 CLI 2.0 管理金鑰保存庫](key-vault-manage-with-cli2.md)。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-109">Azure CLI 2.0 - If you don't have this setup for your environment, see [Manage Key Vault using CLI 2.0](key-vault-manage-with-cli2.md).</span></span>

<span data-ttu-id="fcd1e-110">如需 CLI 的金鑰保存庫特定參考資訊，請參閱 [Azure CLI 2.0 金鑰保存庫參考](https://docs.microsoft.com/cli/azure/keyvault)。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-110">For Key Vault specific reference information for CLI, see [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="fcd1e-111">所需的權限</span><span class="sxs-lookup"><span data-stu-id="fcd1e-111">Required permissions</span></span>

<span data-ttu-id="fcd1e-112">Key Vault 作業透過角色型存取控制 (RBAC) 權限來分別管理，如下所示：</span><span class="sxs-lookup"><span data-stu-id="fcd1e-112">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="fcd1e-113">作業</span><span class="sxs-lookup"><span data-stu-id="fcd1e-113">Operation</span></span> | <span data-ttu-id="fcd1e-114">說明</span><span class="sxs-lookup"><span data-stu-id="fcd1e-114">Description</span></span> | <span data-ttu-id="fcd1e-115">使用者權限</span><span class="sxs-lookup"><span data-stu-id="fcd1e-115">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="fcd1e-116">列出</span><span class="sxs-lookup"><span data-stu-id="fcd1e-116">List</span></span>|<span data-ttu-id="fcd1e-117">列出已刪除的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-117">Lists deleted key vaults.</span></span>|<span data-ttu-id="fcd1e-118">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="fcd1e-118">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="fcd1e-119">復原</span><span class="sxs-lookup"><span data-stu-id="fcd1e-119">Recover</span></span>|<span data-ttu-id="fcd1e-120">還原已刪除的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-120">Restores a deleted key vault.</span></span>|<span data-ttu-id="fcd1e-121">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="fcd1e-121">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="fcd1e-122">清除</span><span class="sxs-lookup"><span data-stu-id="fcd1e-122">Purge</span></span>|<span data-ttu-id="fcd1e-123">永久移除已刪除的金鑰保存庫和其所有內容。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-123">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="fcd1e-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="fcd1e-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="fcd1e-125">如需權限和存取控制的詳細資訊，請參閱[保護您的金鑰保存庫](key-vault-secure-your-key-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-125">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="fcd1e-126">啟用虛刪除</span><span class="sxs-lookup"><span data-stu-id="fcd1e-126">Enabling soft-delete</span></span>

<span data-ttu-id="fcd1e-127">toobe 無法 toorecover 已刪除的金鑰保存庫或物件儲存在金鑰保存庫，您必須先啟用虛刪除該金鑰的保存庫。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-127">toobe able toorecover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="fcd1e-128">現有的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="fcd1e-128">Existing key vault</span></span>

<span data-ttu-id="fcd1e-129">對於名為 ContosoVault 的現有金鑰保存庫啟用虛刪除，如下所示。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-129">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="fcd1e-130">目前您需要 toouse Azure 資源管理員資源操作 toodirectly 寫入 hello *enableSoftDelete*屬性 toohello 金鑰保存庫資源。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-130">Currently you need toouse Azure Resource Manager resource manipulation toodirectly write hello *enableSoftDelete* property toohello Key Vault resource.</span></span>

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a><span data-ttu-id="fcd1e-131">新的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="fcd1e-131">New key vault</span></span>

<span data-ttu-id="fcd1e-132">啟用虛刪除新的金鑰保存庫是在建立時新增 hello 虛刪除啟用旗標 tooyour 建立命令。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-132">Enabling soft-delete for a new key vault is done at creation time by adding hello soft-delete enable flag tooyour create command.</span></span>

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="fcd1e-133">驗證啟用虛刪除</span><span class="sxs-lookup"><span data-stu-id="fcd1e-133">Verify soft-delete enablement</span></span>

<span data-ttu-id="fcd1e-134">tooverify 的金鑰保存庫已虛刪除啟用，執行 hello*顯示*命令，並尋找 hello ' 虛刪除 Enabled？ '</span><span class="sxs-lookup"><span data-stu-id="fcd1e-134">tooverify that a key vault has soft-delete enabled, run hello *show* command and look for hello 'Soft Delete Enabled?'</span></span> <span data-ttu-id="fcd1e-135">屬性，及其設定 true 或 false。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-135">attribute and its setting, true or false.</span></span>

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="fcd1e-136">刪除虛刪除所保護的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="fcd1e-136">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="fcd1e-137">hello 命令 toodelete （或移除） 金鑰保存庫會維持的 hello 相同，但其行為變更會根據您是否已啟用虛刪除與否。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-137">hello command toodelete (or remove) a key vault remains hello same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
><span data-ttu-id="fcd1e-138">如果您要執行 hello 的金鑰保存庫，但是沒有啟用虛刪除的前一個命令，您將永久刪除此金鑰保存庫並不使用任何選項，復原所有的內容。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-138">If you run hello previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="fcd1e-139">虛刪除如何保護您的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="fcd1e-139">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="fcd1e-140">已啟用虛刪除：</span><span class="sxs-lookup"><span data-stu-id="fcd1e-140">With soft-delete enabled:</span></span>

- <span data-ttu-id="fcd1e-141">刪除金鑰保存庫時，它會從其資源群組中移除，並放置於僅保留命名空間建立所在的 hello 位置相關聯。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-141">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with hello location where it was created.</span></span> 
- <span data-ttu-id="fcd1e-142">已刪除的索引鍵中的物件保存庫，例如金鑰、 密碼和憑證，都無法存取，以及其包含的金鑰保存庫在 hello 刪除狀態時維持不變。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-142">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in hello deleted state.</span></span> 
- <span data-ttu-id="fcd1e-143">hello DNS 名稱的金鑰保存庫中已刪除狀態是仍保留，因此無法建立新的金鑰保存庫相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-143">hello DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="fcd1e-144">您可以檢視已刪除的狀態金鑰保存庫，您的訂用帳戶，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="fcd1e-144">You may view deleted state key vaults, associated with your subscription, using hello following command:</span></span>

```azurecli
az keyvault list-deleted
```

<span data-ttu-id="fcd1e-145">hello*資源識別碼*在 hello 輸出是指 toohello 此保存庫的原始資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-145">hello *Resource ID* in hello output refers toohello original resource ID of this vault.</span></span> <span data-ttu-id="fcd1e-146">因為此金鑰保存庫目前處於已刪除狀態，所以沒有具有該資源識別碼的資源存在。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-146">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="fcd1e-147">hello*識別碼*欄位可以是復原，或清除時，使用的 tooidentify hello 資源。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-147">hello *Id* field can be used tooidentify hello resource when recovering, or purging.</span></span> <span data-ttu-id="fcd1e-148">hello*排定清除日期*欄位會指出何時將永久刪除 hello 保存庫 （清除） 如果此刪除保存庫會不採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-148">hello *Scheduled Purge Date* field indicates when hello vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="fcd1e-149">hello 預設保留期間，已使用 toocalculate hello*排定清除日期*，為 90 天。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-149">hello default retention period, used toocalculate hello *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="fcd1e-150">復原金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="fcd1e-150">Recovering a key vault</span></span>

<span data-ttu-id="fcd1e-151">toorecover 金鑰保存庫，您需要 toospecify hello 金鑰保存庫名稱、 資源群組和位置。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-151">toorecover a key vault, you need toospecify hello key vault name, resource group, and location.</span></span> <span data-ttu-id="fcd1e-152">請記下 hello 位置和 hello 的 hello 刪除金鑰保存庫的資源群組，您需要這些序號進行金鑰保存庫復原程序。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-152">Note hello location and hello resource group of hello deleted key vault as you need these for a key vault recovery process.</span></span>

```azurecli
az keyvault recover --location westus --name ContosoVault
```

<span data-ttu-id="fcd1e-153">當復原金鑰的保存庫時，hello 結果會是新的資源，並提供原始 hello 金鑰保存庫的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-153">When a key vault is recovered, hello result is a new resource with hello key vault's original resource ID.</span></span> <span data-ttu-id="fcd1e-154">如果已經移除了 hello hello 金鑰保存庫的存在其中的資源群組，就必須建立新的資源群組具有相同名稱 hello 金鑰保存庫可以在復原之前。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-154">If hello resource group where hello key vault existed has been removed, a new resource group with same name must be created before hello key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="fcd1e-155">金鑰保存庫物件和虛刪除</span><span class="sxs-lookup"><span data-stu-id="fcd1e-155">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="fcd1e-156">對於已啟用虛刪除的金鑰保存庫 'ContosoVault'，其中的金鑰 'ContosoFirstKey'，以下為該金鑰的刪除方式。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-156">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="fcd1e-157">在金鑰保存庫啟用虛刪除的情況下，已刪除的金鑰仍會看似已刪除，例外情況是當您明確地列出或擷取已刪除的金鑰時。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-157">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="fcd1e-158">除了列出的已刪除的索引鍵、 將其復原或清除它，將會失敗 hello 刪除狀態中的索引鍵上的大部分作業。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-158">Most operations on a key in hello deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="fcd1e-159">比方說，toorequest toolist 刪除金鑰在金鑰保存庫中，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="fcd1e-159">For example, toorequest toolist deleted keys in a key vault, use hello following command:</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a><span data-ttu-id="fcd1e-160">轉換狀態</span><span class="sxs-lookup"><span data-stu-id="fcd1e-160">Transition state</span></span> 

<span data-ttu-id="fcd1e-161">當您刪除金鑰保存庫中的索引鍵與啟用虛刪除時，可能需要數秒鐘，讓 hello 轉換 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-161">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for hello transition toocomplete.</span></span> <span data-ttu-id="fcd1e-162">在此轉換狀態，它可能會出現該 hello 索引鍵不在 hello 作用中狀態或 hello 刪除狀態。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-162">During this transition state, it may appear that hello key is not in hello active state or hello deleted state.</span></span> <span data-ttu-id="fcd1e-163">此命令會列出名為 'ContosoVault' 的金鑰保存庫中，所有已刪除的金鑰。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-163">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="fcd1e-164">對金鑰保存庫物件使用虛刪除</span><span class="sxs-lookup"><span data-stu-id="fcd1e-164">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="fcd1e-165">就像金鑰保存庫，已刪除的索引鍵，密碼或憑證仍然會在已刪除狀態向上 too90 天除非加以復原，或清除它。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-165">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up too90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="fcd1e-166">之間的信任</span><span class="sxs-lookup"><span data-stu-id="fcd1e-166">Keys</span></span>

<span data-ttu-id="fcd1e-167">toorecover 已刪除的索引鍵：</span><span class="sxs-lookup"><span data-stu-id="fcd1e-167">toorecover a deleted key:</span></span>

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="fcd1e-168">toopermanently 刪除機碼：</span><span class="sxs-lookup"><span data-stu-id="fcd1e-168">toopermanently delete a key:</span></span>

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="fcd1e-169">清除金鑰會永久刪除它，這表示它將無法復原。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-169">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="fcd1e-170">hello**復原**和**清除**動作具有自己在金鑰保存庫的存取原則相關聯的權限。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-170">hello **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="fcd1e-171">為使用者或服務主體 toobe 無法 tooexecute**復原**或**清除**它們必須 hello 金鑰保存庫的存取原則中個別 hello （金鑰或密碼），該物件權限的動作。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-171">For a user or service principal toobe able tooexecute a **recover** or **purge** action they must have hello respective permission for that object (key or secret) in hello key vault access policy.</span></span> <span data-ttu-id="fcd1e-172">根據預設，hello**清除**權限不會加入 tooa 金鑰保存庫的存取原則時 hello 'all' 的快顯使用的 toogrant tooa 使用者所有的權限。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-172">By default, hello **purge** permission is not added tooa key vault's access policy when hello 'all' shortcut is used toogrant all permissions tooa user.</span></span> <span data-ttu-id="fcd1e-173">您必須明確授與**清除**權限。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-173">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="fcd1e-174">例如，下列命令授與來 hellouser@contoso.com權限 tooperform 多個作業中的索引鍵*ContosoVault*包括**清除**。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-174">For example, hello following command grants user@contoso.com permission tooperform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="fcd1e-175">設定金鑰保存庫存取原則</span><span class="sxs-lookup"><span data-stu-id="fcd1e-175">Set a key vault access policy</span></span>

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> <span data-ttu-id="fcd1e-176">如果您有現有的金鑰保存庫，且剛剛啟用虛刪除，您可能沒有**復原**和**清除**權限。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-176">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="fcd1e-177">密碼</span><span class="sxs-lookup"><span data-stu-id="fcd1e-177">Secrets</span></span>

<span data-ttu-id="fcd1e-178">就像金鑰，金鑰保存庫中的密碼會有自己的操作指令。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-178">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="fcd1e-179">遵循，是 hello 命令，以刪除、 列出、 復原，並清除密碼。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-179">Following, are hello commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="fcd1e-180">刪除名為 SQLPassword 的密碼：</span><span class="sxs-lookup"><span data-stu-id="fcd1e-180">Delete a secret named SQLPassword:</span></span> 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- <span data-ttu-id="fcd1e-181">列出金鑰保存庫中的所有已刪除密碼：</span><span class="sxs-lookup"><span data-stu-id="fcd1e-181">List all deleted secrets in a key vault:</span></span> 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- <span data-ttu-id="fcd1e-182">復原密碼，以處於已刪除的 hello:</span><span class="sxs-lookup"><span data-stu-id="fcd1e-182">Recover a secret in hello deleted state:</span></span> 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- <span data-ttu-id="fcd1e-183">清除已刪除狀態的密碼：</span><span class="sxs-lookup"><span data-stu-id="fcd1e-183">Purge a secret in deleted state:</span></span> 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="fcd1e-184">清除密碼會永久刪除它，這表示它將無法復原。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-184">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="fcd1e-185">清除金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="fcd1e-185">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="fcd1e-186">金鑰保存庫物件</span><span class="sxs-lookup"><span data-stu-id="fcd1e-186">Key vault objects</span></span>

<span data-ttu-id="fcd1e-187">清除金鑰、密碼或憑證會永久刪除它，這表示它將無法復原。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-187">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="fcd1e-188">將會在 hello 金鑰保存庫中的所有其他物件，包含 hello 刪除物件的 hello 金鑰保存庫會不過維持不變。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-188">hello key vault that contained hello deleted object will however remain intact as will all other objects in hello key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="fcd1e-189">金鑰保存庫作為容器</span><span class="sxs-lookup"><span data-stu-id="fcd1e-189">Key vaults as containers</span></span>
<span data-ttu-id="fcd1e-190">當清除金鑰保存庫時，它的所有內容，包括金鑰、密碼和憑證，都會永久刪除。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-190">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="fcd1e-191">toopurge 金鑰保存庫中，使用 hello`az keyvault purge`命令。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-191">toopurge a key vault, use hello `az keyvault purge` command.</span></span> <span data-ttu-id="fcd1e-192">您可以找到 hello 位置您訂用帳戶已刪除金鑰保存庫使用 hello 命令`az keyvault list-deleted`。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-192">You can find hello location your subscription's deleted key vaults using hello command `az keyvault list-deleted`.</span></span>

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
><span data-ttu-id="fcd1e-193">清除金鑰保存庫會永久刪除它，這表示它將無法復原。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-193">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="fcd1e-194">所需的清除權限</span><span class="sxs-lookup"><span data-stu-id="fcd1e-194">Purge permissions required</span></span>
- <span data-ttu-id="fcd1e-195">toopurge 已刪除的金鑰保存庫，使得 hello 保存庫和其所有內容都將會永久移除，hello 使用者需要 RBAC 權限 tooperform *Microsoft.KeyVault/locations/deletedVaults/purge/action*作業。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-195">toopurge a deleted key vault, such that hello vault and all its contents are permanently removed, hello user needs RBAC permission tooperform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="fcd1e-196">toolist hello 刪除金鑰，hello 保存庫的使用者需要 RBAC 權限 tooperform *Microsoft.KeyVault/deletedVaults/read*權限。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-196">toolist hello deleted key, hello vault a user needs RBAC permission tooperform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="fcd1e-197">根據預設，只有訂用帳戶管理員擁有這些權限。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-197">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="fcd1e-198">排定的清除</span><span class="sxs-lookup"><span data-stu-id="fcd1e-198">Scheduled purge</span></span>

<span data-ttu-id="fcd1e-199">列出您已刪除的金鑰保存庫的物件顯示它們 schedled toobe 清除金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-199">Listing your deleted key vault objects shows when they are schedled toobe purged by Key Vault.</span></span> <span data-ttu-id="fcd1e-200">hello*排定清除日期*欄位會指出當您將永久刪除這項金鑰保存庫物件，如果未不採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-200">hello *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="fcd1e-201">根據預設，已刪除的金鑰保存庫物件的 hello 保留期限為 90 天。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-201">By default, hello retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="fcd1e-202">已清除的保存庫物件，由其「排定清除日期」欄位觸發，會永久刪除。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-202">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="fcd1e-203">無法復原。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-203">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="fcd1e-204">其他資源</span><span class="sxs-lookup"><span data-stu-id="fcd1e-204">Other resources</span></span>

- <span data-ttu-id="fcd1e-205">如需 Key Vault 的虛刪除功能概觀，請參閱 [Azure Key Vault 虛刪除概觀](key-vault-ovw-soft-delete.md)。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-205">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="fcd1e-206">如需 Azure Key Vault 使用的一般概觀，請參閱[開始使用 Azure Key Vault](key-vault-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="fcd1e-206">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>


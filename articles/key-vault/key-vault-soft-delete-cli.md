---
ms.assetid: 
title: "Azure Key Vault - 如何以 CLI 使用虛刪除"
description: "以 CLI 程式碼片段進行虛刪除的使用案例範例"
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 3ee2c5dfb99d734cde25894174466b8e49823c67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-key-vault-soft-delete-with-cli"></a><span data-ttu-id="3bd30-103">如何以 CLI 使用金鑰保存庫虛刪除</span><span class="sxs-lookup"><span data-stu-id="3bd30-103">How to use Key Vault soft-delete with CLI</span></span>

<span data-ttu-id="3bd30-104">Azure Key Vault 的虛刪除功能可復原已刪除的保存庫和保存庫物件。</span><span class="sxs-lookup"><span data-stu-id="3bd30-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="3bd30-105">具體而言，虛刪除解決下列案例：</span><span class="sxs-lookup"><span data-stu-id="3bd30-105">Specifically, soft-delete addresses the following scenarios:</span></span>

- <span data-ttu-id="3bd30-106">可復原的 Key Vault 刪除支援</span><span class="sxs-lookup"><span data-stu-id="3bd30-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="3bd30-107">支援可復原的金鑰保存庫物件刪除；金鑰、密碼和憑證</span><span class="sxs-lookup"><span data-stu-id="3bd30-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3bd30-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="3bd30-108">Prerequisites</span></span>

- <span data-ttu-id="3bd30-109">Azure CLI 2.0 - 如果您沒有為您的環境進行此安裝，請參閱[使用 CLI 2.0 管理金鑰保存庫](key-vault-manage-with-cli2.md)。</span><span class="sxs-lookup"><span data-stu-id="3bd30-109">Azure CLI 2.0 - If you don't have this setup for your environment, see [Manage Key Vault using CLI 2.0](key-vault-manage-with-cli2.md).</span></span>

<span data-ttu-id="3bd30-110">如需 CLI 的金鑰保存庫特定參考資訊，請參閱 [Azure CLI 2.0 金鑰保存庫參考](https://docs.microsoft.com/cli/azure/keyvault)。</span><span class="sxs-lookup"><span data-stu-id="3bd30-110">For Key Vault specific reference information for CLI, see [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="3bd30-111">所需的權限</span><span class="sxs-lookup"><span data-stu-id="3bd30-111">Required permissions</span></span>

<span data-ttu-id="3bd30-112">Key Vault 作業透過角色型存取控制 (RBAC) 權限來分別管理，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3bd30-112">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="3bd30-113">作業</span><span class="sxs-lookup"><span data-stu-id="3bd30-113">Operation</span></span> | <span data-ttu-id="3bd30-114">說明</span><span class="sxs-lookup"><span data-stu-id="3bd30-114">Description</span></span> | <span data-ttu-id="3bd30-115">使用者權限</span><span class="sxs-lookup"><span data-stu-id="3bd30-115">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="3bd30-116">列出</span><span class="sxs-lookup"><span data-stu-id="3bd30-116">List</span></span>|<span data-ttu-id="3bd30-117">列出已刪除的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="3bd30-117">Lists deleted key vaults.</span></span>|<span data-ttu-id="3bd30-118">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="3bd30-118">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="3bd30-119">復原</span><span class="sxs-lookup"><span data-stu-id="3bd30-119">Recover</span></span>|<span data-ttu-id="3bd30-120">還原已刪除的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="3bd30-120">Restores a deleted key vault.</span></span>|<span data-ttu-id="3bd30-121">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="3bd30-121">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="3bd30-122">清除</span><span class="sxs-lookup"><span data-stu-id="3bd30-122">Purge</span></span>|<span data-ttu-id="3bd30-123">永久移除已刪除的金鑰保存庫和其所有內容。</span><span class="sxs-lookup"><span data-stu-id="3bd30-123">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="3bd30-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="3bd30-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="3bd30-125">如需權限和存取控制的詳細資訊，請參閱[保護您的金鑰保存庫](key-vault-secure-your-key-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="3bd30-125">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="3bd30-126">啟用虛刪除</span><span class="sxs-lookup"><span data-stu-id="3bd30-126">Enabling soft-delete</span></span>

<span data-ttu-id="3bd30-127">若要能夠復原已刪除的金鑰保存庫或儲存在金鑰保存庫中的物件，您必須先為該金鑰保存庫啟用虛刪除。</span><span class="sxs-lookup"><span data-stu-id="3bd30-127">To be able to recover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="3bd30-128">現有的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="3bd30-128">Existing key vault</span></span>

<span data-ttu-id="3bd30-129">對於名為 ContosoVault 的現有金鑰保存庫啟用虛刪除，如下所示。</span><span class="sxs-lookup"><span data-stu-id="3bd30-129">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="3bd30-130">目前，您需要使用 Azure Resource Manager 資源操作來直接寫入 Key Vault 資源的 *enableSoftDelete* 屬性。</span><span class="sxs-lookup"><span data-stu-id="3bd30-130">Currently you need to use Azure Resource Manager resource manipulation to directly write the *enableSoftDelete* property to the Key Vault resource.</span></span>

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a><span data-ttu-id="3bd30-131">新的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="3bd30-131">New key vault</span></span>

<span data-ttu-id="3bd30-132">為新的金鑰保存庫啟用虛刪除是在建立時完成，方法是新增虛刪除啟用旗標到您的 create 命令。</span><span class="sxs-lookup"><span data-stu-id="3bd30-132">Enabling soft-delete for a new key vault is done at creation time by adding the soft-delete enable flag to your create command.</span></span>

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="3bd30-133">驗證啟用虛刪除</span><span class="sxs-lookup"><span data-stu-id="3bd30-133">Verify soft-delete enablement</span></span>

<span data-ttu-id="3bd30-134">若要驗證金鑰保存庫已啟用虛刪除，請執行 *show* 命令，並尋找「虛刪除已啟用?」</span><span class="sxs-lookup"><span data-stu-id="3bd30-134">To verify that a key vault has soft-delete enabled, run the *show* command and look for the 'Soft Delete Enabled?'</span></span> <span data-ttu-id="3bd30-135">屬性，及其設定 true 或 false。</span><span class="sxs-lookup"><span data-stu-id="3bd30-135">attribute and its setting, true or false.</span></span>

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="3bd30-136">刪除虛刪除所保護的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="3bd30-136">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="3bd30-137">刪除 (或移除) 金鑰保存庫的命令維持不變，但它的行為會根據您是否已啟用虛刪除而改變。</span><span class="sxs-lookup"><span data-stu-id="3bd30-137">The command to delete (or remove) a key vault remains the same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
><span data-ttu-id="3bd30-138">如果您先前針對沒有啟用虛刪除的金鑰保存庫執行命令，您將永久刪除此金鑰保存庫及其所有的內容，並且沒有任何選項可以復原。</span><span class="sxs-lookup"><span data-stu-id="3bd30-138">If you run the previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="3bd30-139">虛刪除如何保護您的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="3bd30-139">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="3bd30-140">已啟用虛刪除：</span><span class="sxs-lookup"><span data-stu-id="3bd30-140">With soft-delete enabled:</span></span>

- <span data-ttu-id="3bd30-141">刪除金鑰保存庫時，它會從其資源群組中移除，並放置於僅與其建立所在位置建立關聯的保留命名空間。</span><span class="sxs-lookup"><span data-stu-id="3bd30-141">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with the location where it was created.</span></span> 
- <span data-ttu-id="3bd30-142">已刪除的金鑰保存庫中的物件，例如金鑰、密碼和憑證都無法存取，並且只要包含的金鑰保存庫處於已刪除狀態便維持不變。</span><span class="sxs-lookup"><span data-stu-id="3bd30-142">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in the deleted state.</span></span> 
- <span data-ttu-id="3bd30-143">已刪除狀態中的金鑰保存庫 DNS 名稱仍會被保留，因此無法以相同的名稱建立新的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="3bd30-143">The DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="3bd30-144">您可以檢視與您的訂用帳戶建立關聯的已刪除狀態金鑰保存庫，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="3bd30-144">You may view deleted state key vaults, associated with your subscription, using the following command:</span></span>

```azurecli
az keyvault list-deleted
```

<span data-ttu-id="3bd30-145">輸出中的「資源識別碼」是指此保存庫的原始資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="3bd30-145">The *Resource ID* in the output refers to the original resource ID of this vault.</span></span> <span data-ttu-id="3bd30-146">因為此金鑰保存庫目前處於已刪除狀態，所以沒有具有該資源識別碼的資源存在。</span><span class="sxs-lookup"><span data-stu-id="3bd30-146">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="3bd30-147">「識別碼」欄位可以用來在復原或清除時識別資源。</span><span class="sxs-lookup"><span data-stu-id="3bd30-147">The *Id* field can be used to identify the resource when recovering, or purging.</span></span> <span data-ttu-id="3bd30-148">「排定清除日期」欄位指出如果對這個已刪除的保存庫不採取任何動作，何時將永久刪除 (清除) 保存庫。</span><span class="sxs-lookup"><span data-stu-id="3bd30-148">The *Scheduled Purge Date* field indicates when the vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="3bd30-149">用來計算「排定清除日期」的預設保留期間為 90 天。</span><span class="sxs-lookup"><span data-stu-id="3bd30-149">The default retention period, used to calculate the *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="3bd30-150">復原金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="3bd30-150">Recovering a key vault</span></span>

<span data-ttu-id="3bd30-151">若要復原金鑰保存庫，您需要指定金鑰保存庫名稱、資源群組和位置。</span><span class="sxs-lookup"><span data-stu-id="3bd30-151">To recover a key vault, you need to specify the key vault name, resource group, and location.</span></span> <span data-ttu-id="3bd30-152">請記下已刪除之金鑰保存庫的位置和資源群組，因為您需要這些才能進行金鑰保存庫復原程序。</span><span class="sxs-lookup"><span data-stu-id="3bd30-152">Note the location and the resource group of the deleted key vault as you need these for a key vault recovery process.</span></span>

```azurecli
az keyvault recover --location westus --name ContosoVault
```

<span data-ttu-id="3bd30-153">在金鑰保存庫復原之後，結果會是新的資源，並具有金鑰保存庫的原始資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="3bd30-153">When a key vault is recovered, the result is a new resource with the key vault's original resource ID.</span></span> <span data-ttu-id="3bd30-154">如果金鑰保存庫存在的資源群組已被移除，則必須先建立具有相同名稱的新資源群組，才能復原金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="3bd30-154">If the resource group where the key vault existed has been removed, a new resource group with same name must be created before the key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="3bd30-155">金鑰保存庫物件和虛刪除</span><span class="sxs-lookup"><span data-stu-id="3bd30-155">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="3bd30-156">對於已啟用虛刪除的金鑰保存庫 'ContosoVault'，其中的金鑰 'ContosoFirstKey'，以下為該金鑰的刪除方式。</span><span class="sxs-lookup"><span data-stu-id="3bd30-156">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="3bd30-157">在金鑰保存庫啟用虛刪除的情況下，已刪除的金鑰仍會看似已刪除，例外情況是當您明確地列出或擷取已刪除的金鑰時。</span><span class="sxs-lookup"><span data-stu-id="3bd30-157">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="3bd30-158">對於已刪除狀態的金鑰，大部分作業會失敗，只除了列出、復原或清除已刪除的金鑰時例外。</span><span class="sxs-lookup"><span data-stu-id="3bd30-158">Most operations on a key in the deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="3bd30-159">例如，若要要求列出金鑰保存庫中的已刪除金鑰，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="3bd30-159">For example, to request to list deleted keys in a key vault, use the following command:</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a><span data-ttu-id="3bd30-160">轉換狀態</span><span class="sxs-lookup"><span data-stu-id="3bd30-160">Transition state</span></span> 

<span data-ttu-id="3bd30-161">當您刪除金鑰保存庫中的金鑰，並且已啟用虛刪除時，可能需要幾秒鐘的時間讓轉換完成。</span><span class="sxs-lookup"><span data-stu-id="3bd30-161">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for the transition to complete.</span></span> <span data-ttu-id="3bd30-162">在此轉換狀態期間，可能會出現金鑰不在使用中狀態或已刪除狀態。</span><span class="sxs-lookup"><span data-stu-id="3bd30-162">During this transition state, it may appear that the key is not in the active state or the deleted state.</span></span> <span data-ttu-id="3bd30-163">此命令會列出名為 'ContosoVault' 的金鑰保存庫中，所有已刪除的金鑰。</span><span class="sxs-lookup"><span data-stu-id="3bd30-163">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="3bd30-164">對金鑰保存庫物件使用虛刪除</span><span class="sxs-lookup"><span data-stu-id="3bd30-164">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="3bd30-165">就像金鑰保存庫，已刪除的金鑰、密碼或憑證仍然會維時在已刪除狀態長達 90 天，除非加以復原或清除。</span><span class="sxs-lookup"><span data-stu-id="3bd30-165">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up to 90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="3bd30-166">之間的信任</span><span class="sxs-lookup"><span data-stu-id="3bd30-166">Keys</span></span>

<span data-ttu-id="3bd30-167">復原已刪除的金鑰：</span><span class="sxs-lookup"><span data-stu-id="3bd30-167">To recover a deleted key:</span></span>

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="3bd30-168">永久刪除金鑰：</span><span class="sxs-lookup"><span data-stu-id="3bd30-168">To permanently delete a key:</span></span>

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="3bd30-169">清除金鑰會永久刪除它，這表示它將無法復原。</span><span class="sxs-lookup"><span data-stu-id="3bd30-169">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="3bd30-170">**復原**和**清除**動作在金鑰保存庫存取原則中有自己的相關聯權限。</span><span class="sxs-lookup"><span data-stu-id="3bd30-170">The **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="3bd30-171">使用者或服務主體若要能夠執行**復原**或**清除**動作，必須在金鑰保存庫存取原則中有該物件 (金鑰或密碼) 的個別權限。</span><span class="sxs-lookup"><span data-stu-id="3bd30-171">For a user or service principal to be able to execute a **recover** or **purge** action they must have the respective permission for that object (key or secret) in the key vault access policy.</span></span> <span data-ttu-id="3bd30-172">根據預設，**清除**權限不會在 'all' 捷徑用於授與所有權限給使用者時，新增到金鑰保存庫的存取原則。</span><span class="sxs-lookup"><span data-stu-id="3bd30-172">By default, the **purge** permission is not added to a key vault's access policy when the 'all' shortcut is used to grant all permissions to a user.</span></span> <span data-ttu-id="3bd30-173">您必須明確授與**清除**權限。</span><span class="sxs-lookup"><span data-stu-id="3bd30-173">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="3bd30-174">例如，下列命令授與 user@contoso.com 對 *ContosoVault* 中的金鑰執行數種作業的權限，這其中包括**清除**。</span><span class="sxs-lookup"><span data-stu-id="3bd30-174">For example, the following command grants user@contoso.com permission to perform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="3bd30-175">設定金鑰保存庫存取原則</span><span class="sxs-lookup"><span data-stu-id="3bd30-175">Set a key vault access policy</span></span>

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> <span data-ttu-id="3bd30-176">如果您有現有的金鑰保存庫，且剛剛啟用虛刪除，您可能沒有**復原**和**清除**權限。</span><span class="sxs-lookup"><span data-stu-id="3bd30-176">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="3bd30-177">密碼</span><span class="sxs-lookup"><span data-stu-id="3bd30-177">Secrets</span></span>

<span data-ttu-id="3bd30-178">就像金鑰，金鑰保存庫中的密碼會有自己的操作指令。</span><span class="sxs-lookup"><span data-stu-id="3bd30-178">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="3bd30-179">以下是刪除、列出、復原和清除密碼的命令。</span><span class="sxs-lookup"><span data-stu-id="3bd30-179">Following, are the commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="3bd30-180">刪除名為 SQLPassword 的密碼：</span><span class="sxs-lookup"><span data-stu-id="3bd30-180">Delete a secret named SQLPassword:</span></span> 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- <span data-ttu-id="3bd30-181">列出金鑰保存庫中的所有已刪除密碼：</span><span class="sxs-lookup"><span data-stu-id="3bd30-181">List all deleted secrets in a key vault:</span></span> 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- <span data-ttu-id="3bd30-182">復原已刪除狀態的密碼：</span><span class="sxs-lookup"><span data-stu-id="3bd30-182">Recover a secret in the deleted state:</span></span> 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- <span data-ttu-id="3bd30-183">清除已刪除狀態的密碼：</span><span class="sxs-lookup"><span data-stu-id="3bd30-183">Purge a secret in deleted state:</span></span> 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="3bd30-184">清除密碼會永久刪除它，這表示它將無法復原。</span><span class="sxs-lookup"><span data-stu-id="3bd30-184">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="3bd30-185">清除金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="3bd30-185">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="3bd30-186">金鑰保存庫物件</span><span class="sxs-lookup"><span data-stu-id="3bd30-186">Key vault objects</span></span>

<span data-ttu-id="3bd30-187">清除金鑰、密碼或憑證會永久刪除它，這表示它將無法復原。</span><span class="sxs-lookup"><span data-stu-id="3bd30-187">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="3bd30-188">不過，包含已刪除之物件的金鑰保存庫會維持不變，金鑰保存庫中的所有其他物件也是。</span><span class="sxs-lookup"><span data-stu-id="3bd30-188">The key vault that contained the deleted object will however remain intact as will all other objects in the key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="3bd30-189">金鑰保存庫作為容器</span><span class="sxs-lookup"><span data-stu-id="3bd30-189">Key vaults as containers</span></span>
<span data-ttu-id="3bd30-190">當清除金鑰保存庫時，它的所有內容，包括金鑰、密碼和憑證，都會永久刪除。</span><span class="sxs-lookup"><span data-stu-id="3bd30-190">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="3bd30-191">若要清除金鑰保存庫，請使用 `az keyvault purge` 命令。</span><span class="sxs-lookup"><span data-stu-id="3bd30-191">To purge a key vault, use the `az keyvault purge` command.</span></span> <span data-ttu-id="3bd30-192">您可以使用命令 `az keyvault list-deleted` 找到訂用帳戶的已刪除金鑰保存庫的位置。</span><span class="sxs-lookup"><span data-stu-id="3bd30-192">You can find the location your subscription's deleted key vaults using the command `az keyvault list-deleted`.</span></span>

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
><span data-ttu-id="3bd30-193">清除金鑰保存庫會永久刪除它，這表示它將無法復原。</span><span class="sxs-lookup"><span data-stu-id="3bd30-193">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="3bd30-194">所需的清除權限</span><span class="sxs-lookup"><span data-stu-id="3bd30-194">Purge permissions required</span></span>
- <span data-ttu-id="3bd30-195">若要清除已刪除的金鑰保存庫，以便保存庫和其所有內容永久移除，使用者需要執行 *Microsoft.KeyVault/locations/deletedVaults/purge/action* 作業的 RBAC 權限。</span><span class="sxs-lookup"><span data-stu-id="3bd30-195">To purge a deleted key vault, such that the vault and all its contents are permanently removed, the user needs RBAC permission to perform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="3bd30-196">若要列出已刪除的金鑰保存庫，使用者需要執行 *Microsoft.KeyVault/deletedVaults/read* 作業的 RBAC 權限。</span><span class="sxs-lookup"><span data-stu-id="3bd30-196">To list the deleted key, the vault a user needs RBAC permission to perform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="3bd30-197">根據預設，只有訂用帳戶管理員擁有這些權限。</span><span class="sxs-lookup"><span data-stu-id="3bd30-197">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="3bd30-198">排定的清除</span><span class="sxs-lookup"><span data-stu-id="3bd30-198">Scheduled purge</span></span>

<span data-ttu-id="3bd30-199">列出您的已刪除金鑰保存庫物件，會顯示它們排定要由金鑰保存庫清除的時間。</span><span class="sxs-lookup"><span data-stu-id="3bd30-199">Listing your deleted key vault objects shows when they are schedled to be purged by Key Vault.</span></span> <span data-ttu-id="3bd30-200">「排定清除日期」欄位指出如果不採取任何動作，何時將永久刪除金鑰保存庫物件。</span><span class="sxs-lookup"><span data-stu-id="3bd30-200">The *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="3bd30-201">根據預設，已刪除的金鑰保存庫物件的保留期限為 90 天。</span><span class="sxs-lookup"><span data-stu-id="3bd30-201">By default, the retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="3bd30-202">已清除的保存庫物件，由其「排定清除日期」欄位觸發，會永久刪除。</span><span class="sxs-lookup"><span data-stu-id="3bd30-202">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="3bd30-203">無法復原。</span><span class="sxs-lookup"><span data-stu-id="3bd30-203">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="3bd30-204">其他資源</span><span class="sxs-lookup"><span data-stu-id="3bd30-204">Other resources</span></span>

- <span data-ttu-id="3bd30-205">如需 Key Vault 的虛刪除功能概觀，請參閱 [Azure Key Vault 虛刪除概觀](key-vault-ovw-soft-delete.md)。</span><span class="sxs-lookup"><span data-stu-id="3bd30-205">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="3bd30-206">如需 Azure Key Vault 使用的一般概觀，請參閱[開始使用 Azure Key Vault](key-vault-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="3bd30-206">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>


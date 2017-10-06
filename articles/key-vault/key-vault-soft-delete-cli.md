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
# <a name="how-toouse-key-vault-soft-delete-with-cli"></a>如何 toouse 金鑰保存庫虛刪除與 CLI

Azure Key Vault 的虛刪除功能可復原已刪除的保存庫和保存庫物件。 具體來說，虛刪除位址 hello 下列案例：

- 可復原的 Key Vault 刪除支援
- 支援可復原的金鑰保存庫物件刪除；金鑰、密碼和憑證

## <a name="prerequisites"></a>必要條件

- Azure CLI 2.0 - 如果您沒有為您的環境進行此安裝，請參閱[使用 CLI 2.0 管理金鑰保存庫](key-vault-manage-with-cli2.md)。

如需 CLI 的金鑰保存庫特定參考資訊，請參閱 [Azure CLI 2.0 金鑰保存庫參考](https://docs.microsoft.com/cli/azure/keyvault)。

## <a name="required-permissions"></a>所需的權限

Key Vault 作業透過角色型存取控制 (RBAC) 權限來分別管理，如下所示：

| 作業 | 說明 | 使用者權限 |
|:--|:--|:--|
|列出|列出已刪除的金鑰保存庫。|Microsoft.KeyVault/deletedVaults/read|
|復原|還原已刪除的金鑰保存庫。|Microsoft.KeyVault/vaults/write|
|清除|永久移除已刪除的金鑰保存庫和其所有內容。|Microsoft.KeyVault/locations/deletedVaults/purge/action|

如需權限和存取控制的詳細資訊，請參閱[保護您的金鑰保存庫](key-vault-secure-your-key-vault.md)。

## <a name="enabling-soft-delete"></a>啟用虛刪除

toobe 無法 toorecover 已刪除的金鑰保存庫或物件儲存在金鑰保存庫，您必須先啟用虛刪除該金鑰的保存庫。

### <a name="existing-key-vault"></a>現有的金鑰保存庫

對於名為 ContosoVault 的現有金鑰保存庫啟用虛刪除，如下所示。 

>[!NOTE]
>目前您需要 toouse Azure 資源管理員資源操作 toodirectly 寫入 hello *enableSoftDelete*屬性 toohello 金鑰保存庫資源。

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a>新的金鑰保存庫

啟用虛刪除新的金鑰保存庫是在建立時新增 hello 虛刪除啟用旗標 tooyour 建立命令。

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a>驗證啟用虛刪除

tooverify 的金鑰保存庫已虛刪除啟用，執行 hello*顯示*命令，並尋找 hello ' 虛刪除 Enabled？ ' 屬性，及其設定 true 或 false。

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a>刪除虛刪除所保護的金鑰保存庫

hello 命令 toodelete （或移除） 金鑰保存庫會維持的 hello 相同，但其行為變更會根據您是否已啟用虛刪除與否。

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
>如果您要執行 hello 的金鑰保存庫，但是沒有啟用虛刪除的前一個命令，您將永久刪除此金鑰保存庫並不使用任何選項，復原所有的內容。

### <a name="how-soft-delete-protects-your-key-vaults"></a>虛刪除如何保護您的金鑰保存庫

已啟用虛刪除：

- 刪除金鑰保存庫時，它會從其資源群組中移除，並放置於僅保留命名空間建立所在的 hello 位置相關聯。 
- 已刪除的索引鍵中的物件保存庫，例如金鑰、 密碼和憑證，都無法存取，以及其包含的金鑰保存庫在 hello 刪除狀態時維持不變。 
- hello DNS 名稱的金鑰保存庫中已刪除狀態是仍保留，因此無法建立新的金鑰保存庫相同的名稱。  

您可以檢視已刪除的狀態金鑰保存庫，您的訂用帳戶，使用下列命令的 hello:

```azurecli
az keyvault list-deleted
```

hello*資源識別碼*在 hello 輸出是指 toohello 此保存庫的原始資源識別碼。 因為此金鑰保存庫目前處於已刪除狀態，所以沒有具有該資源識別碼的資源存在。 hello*識別碼*欄位可以是復原，或清除時，使用的 tooidentify hello 資源。 hello*排定清除日期*欄位會指出何時將永久刪除 hello 保存庫 （清除） 如果此刪除保存庫會不採取任何動作。 hello 預設保留期間，已使用 toocalculate hello*排定清除日期*，為 90 天。

## <a name="recovering-a-key-vault"></a>復原金鑰保存庫

toorecover 金鑰保存庫，您需要 toospecify hello 金鑰保存庫名稱、 資源群組和位置。 請記下 hello 位置和 hello 的 hello 刪除金鑰保存庫的資源群組，您需要這些序號進行金鑰保存庫復原程序。

```azurecli
az keyvault recover --location westus --name ContosoVault
```

當復原金鑰的保存庫時，hello 結果會是新的資源，並提供原始 hello 金鑰保存庫的資源識別碼。 如果已經移除了 hello hello 金鑰保存庫的存在其中的資源群組，就必須建立新的資源群組具有相同名稱 hello 金鑰保存庫可以在復原之前。

## <a name="key-vault-objects-and-soft-delete"></a>金鑰保存庫物件和虛刪除

對於已啟用虛刪除的金鑰保存庫 'ContosoVault'，其中的金鑰 'ContosoFirstKey'，以下為該金鑰的刪除方式。

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

在金鑰保存庫啟用虛刪除的情況下，已刪除的金鑰仍會看似已刪除，例外情況是當您明確地列出或擷取已刪除的金鑰時。 除了列出的已刪除的索引鍵、 將其復原或清除它，將會失敗 hello 刪除狀態中的索引鍵上的大部分作業。 

比方說，toorequest toolist 刪除金鑰在金鑰保存庫中，使用下列命令的 hello:

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a>轉換狀態 

當您刪除金鑰保存庫中的索引鍵與啟用虛刪除時，可能需要數秒鐘，讓 hello 轉換 toocomplete。 在此轉換狀態，它可能會出現該 hello 索引鍵不在 hello 作用中狀態或 hello 刪除狀態。 此命令會列出名為 'ContosoVault' 的金鑰保存庫中，所有已刪除的金鑰。

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a>對金鑰保存庫物件使用虛刪除

就像金鑰保存庫，已刪除的索引鍵，密碼或憑證仍然會在已刪除狀態向上 too90 天除非加以復原，或清除它。 

#### <a name="keys"></a>之間的信任

toorecover 已刪除的索引鍵：

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

toopermanently 刪除機碼：

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
>清除金鑰會永久刪除它，這表示它將無法復原。

hello**復原**和**清除**動作具有自己在金鑰保存庫的存取原則相關聯的權限。 為使用者或服務主體 toobe 無法 tooexecute**復原**或**清除**它們必須 hello 金鑰保存庫的存取原則中個別 hello （金鑰或密碼），該物件權限的動作。 根據預設，hello**清除**權限不會加入 tooa 金鑰保存庫的存取原則時 hello 'all' 的快顯使用的 toogrant tooa 使用者所有的權限。 您必須明確授與**清除**權限。 例如，下列命令授與來 hellouser@contoso.com權限 tooperform 多個作業中的索引鍵*ContosoVault*包括**清除**。

#### <a name="set-a-key-vault-access-policy"></a>設定金鑰保存庫存取原則

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> 如果您有現有的金鑰保存庫，且剛剛啟用虛刪除，您可能沒有**復原**和**清除**權限。

#### <a name="secrets"></a>密碼

就像金鑰，金鑰保存庫中的密碼會有自己的操作指令。 遵循，是 hello 命令，以刪除、 列出、 復原，並清除密碼。

- 刪除名為 SQLPassword 的密碼： 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- 列出金鑰保存庫中的所有已刪除密碼： 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- 復原密碼，以處於已刪除的 hello: 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- 清除已刪除狀態的密碼： 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
>清除密碼會永久刪除它，這表示它將無法復原。

## <a name="purging-and-key-vaults"></a>清除金鑰保存庫

### <a name="key-vault-objects"></a>金鑰保存庫物件

清除金鑰、密碼或憑證會永久刪除它，這表示它將無法復原。 將會在 hello 金鑰保存庫中的所有其他物件，包含 hello 刪除物件的 hello 金鑰保存庫會不過維持不變。 

### <a name="key-vaults-as-containers"></a>金鑰保存庫作為容器
當清除金鑰保存庫時，它的所有內容，包括金鑰、密碼和憑證，都會永久刪除。 toopurge 金鑰保存庫中，使用 hello`az keyvault purge`命令。 您可以找到 hello 位置您訂用帳戶已刪除金鑰保存庫使用 hello 命令`az keyvault list-deleted`。

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
>清除金鑰保存庫會永久刪除它，這表示它將無法復原。

### <a name="purge-permissions-required"></a>所需的清除權限
- toopurge 已刪除的金鑰保存庫，使得 hello 保存庫和其所有內容都將會永久移除，hello 使用者需要 RBAC 權限 tooperform *Microsoft.KeyVault/locations/deletedVaults/purge/action*作業。 
- toolist hello 刪除金鑰，hello 保存庫的使用者需要 RBAC 權限 tooperform *Microsoft.KeyVault/deletedVaults/read*權限。 
- 根據預設，只有訂用帳戶管理員擁有這些權限。 

### <a name="scheduled-purge"></a>排定的清除

列出您已刪除的金鑰保存庫的物件顯示它們 schedled toobe 清除金鑰保存庫。 hello*排定清除日期*欄位會指出當您將永久刪除這項金鑰保存庫物件，如果未不採取任何動作。 根據預設，已刪除的金鑰保存庫物件的 hello 保留期限為 90 天。

>[!NOTE]
>已清除的保存庫物件，由其「排定清除日期」欄位觸發，會永久刪除。 無法復原。

## <a name="other-resources"></a>其他資源

- 如需 Key Vault 的虛刪除功能概觀，請參閱 [Azure Key Vault 虛刪除概觀](key-vault-ovw-soft-delete.md)。
- 如需 Azure Key Vault 使用的一般概觀，請參閱[開始使用 Azure Key Vault](key-vault-get-started.md)。


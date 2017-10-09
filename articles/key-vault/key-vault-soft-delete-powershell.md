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
# <a name="how-toouse-key-vault-soft-delete-with-powershell"></a>如何 toouse 金鑰保存庫虛刪除使用 PowerShell

Azure Key Vault 的虛刪除功能可復原已刪除的保存庫和保存庫物件。 具體來說，虛刪除位址 hello 下列案例：

- 可復原的 Key Vault 刪除支援
- 支援可復原的金鑰保存庫物件刪除；金鑰、密碼和憑證

## <a name="prerequisites"></a>必要條件

- Azure PowerShell 4.0.0 或更新版本-如果沒有此已經安裝，安裝 Azure PowerShell，然後將它與您 Azure 訂用帳戶產生關聯，請參閱[如何 tooinstall 和設定 Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview)。 

>[!NOTE]
> 沒有過期的版本，我們金鑰保存庫 PowerShell 的輸出格式的檔案，**可能**先載入到您的環境，而不是 hello 正確版本。 我們會預期 PowerShell toocontain hello 的更新的版本需要更正 hello 輸出格式，並將更新本主題在該時間。 hello 目前的因應措施，您應該會發生這個格式的問題是：
> - 使用下列查詢，如果您注意到您看不到 hello 虛刪除的 hello 啟用本主題中所述的屬性： `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`。


如需 PowerShell 的 Key Vault 特定參考資訊，請參閱 [Azure Key Vault PowerShell 參考](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0)。

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

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a>新的金鑰保存庫

啟用虛刪除新的金鑰保存庫是在建立時新增 hello 虛刪除啟用旗標 tooyour 建立命令。

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a>驗證啟用虛刪除

tooverify 的金鑰保存庫已虛刪除啟用，執行 hello*取得*命令，並尋找 hello ' 虛刪除 Enabled？ ' 屬性，及其設定 true 或 false。

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a>刪除虛刪除所保護的金鑰保存庫

hello 命令 toodelete （或移除） 金鑰保存庫會維持的 hello 相同，但其行為變更會根據您是否已啟用虛刪除與否。

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
>如果您要執行 hello 的金鑰保存庫，但是沒有啟用虛刪除的前一個命令，您將永久刪除此金鑰保存庫並不使用任何選項，復原所有的內容。

### <a name="how-soft-delete-protects-your-key-vaults"></a>虛刪除如何保護您的金鑰保存庫

已啟用虛刪除：

- 刪除金鑰保存庫時，它會從其資源群組中移除，並放置於僅保留命名空間建立所在的 hello 位置相關聯。 
- 已刪除的索引鍵中的物件保存庫，例如金鑰、 密碼和憑證，都無法存取，以及其包含的金鑰保存庫在 hello 刪除狀態時維持不變。 
- hello DNS 名稱的金鑰保存庫中已刪除狀態是仍保留，因此無法建立新的金鑰保存庫相同的名稱。  

您可以檢視已刪除的狀態金鑰保存庫，您的訂用帳戶，使用下列命令的 hello:

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

hello*資源識別碼*在 hello 輸出是指 toohello 此保存庫的原始資源識別碼。 因為此金鑰保存庫目前處於已刪除狀態，所以沒有具有該資源識別碼的資源存在。 hello*識別碼*欄位可以是復原，或清除時，使用的 tooidentify hello 資源。 hello*排定清除日期*欄位會指出何時將永久刪除 hello 保存庫 （清除） 如果此刪除保存庫會不採取任何動作。 hello 預設保留期間，已使用 toocalculate hello*排定清除日期*，為 90 天。

## <a name="recovering-a-key-vault"></a>復原金鑰保存庫

toorecover 金鑰保存庫，您需要 toospecify hello 金鑰保存庫名稱、 資源群組和位置。 請記下 hello 位置和 hello 的 hello 刪除金鑰保存庫的資源群組，您需要這些序號進行金鑰保存庫復原程序。

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

當復原金鑰的保存庫時，hello 結果會是新的資源，並提供原始 hello 金鑰保存庫的資源識別碼。 如果已經移除了 hello hello 金鑰保存庫的存在其中的資源群組，就必須建立新的資源群組具有相同名稱 hello 金鑰保存庫可以在復原之前。

## <a name="key-vault-objects-and-soft-delete"></a>金鑰保存庫物件和虛刪除

對於已啟用虛刪除的金鑰保存庫 'ContosoVault'，其中的金鑰 'ContosoFirstKey'，以下為該金鑰的刪除方式。

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

在金鑰保存庫啟用虛刪除的情況下，已刪除的金鑰仍會看似已刪除，例外情況是當您明確地列出或擷取已刪除的金鑰時。 除了列出的已刪除的索引鍵、 將其復原或清除它，將會失敗 hello 刪除狀態中的索引鍵上的大部分作業。 

比方說，toorequest toolist 刪除金鑰在金鑰保存庫中，使用下列命令的 hello:

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a>轉換狀態 

當您刪除金鑰保存庫中的索引鍵與啟用虛刪除時，可能需要數秒鐘，讓 hello 轉換 toocomplete。 在此轉換狀態，它可能會出現該 hello 索引鍵不在 hello 作用中狀態或 hello 刪除狀態。 此命令會列出名為 'ContosoVault' 的金鑰保存庫中，所有已刪除的金鑰。

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

### <a name="using-soft-delete-with-key-vault-objects"></a>對金鑰保存庫物件使用虛刪除

就像金鑰保存庫，已刪除的索引鍵，密碼或憑證仍然會在已刪除狀態向上 too90 天除非加以復原，或清除它。 

#### <a name="keys"></a>之間的信任

toorecover 已刪除的索引鍵：

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

toopermanently 刪除機碼：

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
>清除金鑰會永久刪除它，這表示它將無法復原。

hello**復原**和**清除**動作具有自己在金鑰保存庫的存取原則相關聯的權限。 為使用者或服務主體 toobe 無法 tooexecute**復原**或**清除**它們必須 hello 金鑰保存庫的存取原則中個別 hello （金鑰或密碼），該物件權限的動作。 根據預設，hello**清除**權限不會加入 tooa 金鑰保存庫的存取原則時 hello 'all' 的快顯使用的 toogrant tooa 使用者所有的權限。 您必須明確授與**清除**權限。 例如，下列命令授與來 hellouser@contoso.com權限 tooperform 多個作業中的索引鍵*ContosoVault*包括**清除**。

#### <a name="set-a-key-vault-access-policy"></a>設定金鑰保存庫存取原則

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> 如果您有現有的金鑰保存庫，且剛剛啟用虛刪除，您可能沒有**復原**和**清除**權限。

#### <a name="secrets"></a>密碼

就像金鑰，金鑰保存庫中的密碼會有自己的操作指令。 遵循，是 hello 命令，以刪除、 列出、 復原，並清除密碼。

- 刪除名為 SQLPassword 的密碼： 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- 列出金鑰保存庫中的所有已刪除密碼： 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- 復原密碼，以處於已刪除的 hello: 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- 清除已刪除狀態的密碼： 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
>清除密碼會永久刪除它，這表示它將無法復原。

## <a name="purging-and-key-vaults"></a>清除金鑰保存庫

### <a name="key-vault-objects"></a>金鑰保存庫物件

清除金鑰、密碼或憑證會永久刪除它，這表示它將無法復原。 將會在 hello 金鑰保存庫中的所有其他物件，包含 hello 刪除物件的 hello 金鑰保存庫會不過維持不變。 

### <a name="key-vaults-as-containers"></a>金鑰保存庫作為容器
當清除金鑰保存庫時，它的所有內容，包括金鑰、密碼和憑證，都會永久刪除。 toopurge 金鑰保存庫中，使用 hello`Remove-AzureRmKeyVault`命令與 hello 選項`-InRemovedState`和藉由指定的金鑰保存庫刪除 hello hello 位置以 hello`-Location location`引數。 您可以找到使用 hello 命令刪除保存庫的 hello 位置`Get-AzureRmKeyVault -InRemovedState`。

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
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


---
title: "aaaRestore 金鑰保存庫金鑰] 和 [密碼加密使用 Azure Backup 的 Vm |Microsoft 文件"
description: "深入了解如何 toorestore 金鑰保存庫金鑰和密碼中使用 PowerShell 的 Azure 備份"
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 45214083-d5fc-4eb3-a367-0239dc59e0f6
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 659b2f647493ffcc9494caee111c8bd584ef9c7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a>使用 Azure 備份還原已加密 VM 的金鑰保存庫金鑰與密碼
這篇文章討論有關使用 Azure VM 備份 tooperform 還原加密的 Azure Vm，如果您的金鑰和密碼不存在 hello 金鑰保存庫中。 如果您想 toomaintain 金鑰 （金鑰加密） 的個別複本，而且 hello 的密碼 （BitLocker 加密金鑰） 還原 VM，也可以使用下列步驟。

## <a name="prerequisites"></a>必要條件
* **備份已加密的 VM** - 已使用 Azure 備份將已加密的 Azure VM 備份。 Hello 發行項，請參閱[管理使用 PowerShell 的 Azure Vm 的備份與還原](backup-azure-vms-automation.md)如需詳細資訊 toobackup 加密 Azure Vm 的方式。
* **設定 Azure 金鑰保存庫**– toowhich 金鑰，請確定該金鑰的保存庫，並還原密碼需要 toobe 已經存在。 Hello 發行項，請參閱[開始使用 Azure 金鑰保存庫](../key-vault/key-vault-get-started.md)如需金鑰保存庫的管理詳細資訊。
* **還原磁碟** - 請確定您已使用 [PowerShell 步驟](backup-azure-vms-automation.md#restore-an-azure-vm)觸發還原作業，以還原加密 VM 的磁碟。 這是因為此作業會產生的 JSON 檔案包含金鑰和密碼的加密 hello VM toobe 還原您儲存體帳戶中。

## <a name="get-key-and-secret-from-azure-backup"></a>從 Azure 備份取得金鑰和祕密

> [!NOTE]
> 一旦 hello 加密 VM 磁碟已還原，請確認：
> 1. $details 填入還原磁碟作業詳細資料，如中所述[還原 hello 磁碟 區段中的 PowerShell 步驟](backup-azure-vms-automation.md#restore-an-azure-vm)
> 2. 應該從還原的硬碟建立 VM**金鑰和密碼是還原的 tookey 保存庫之後**。
>
>

查詢 hello 還原 hello 工作詳細資料的磁碟內容。

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

設定 hello Azure 儲存體的內容，並還原加密的 VM 包含金鑰和秘密提示問題的詳細資料的 JSON 組態檔。

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a>還原金鑰
上述的 hello 目的地路徑中產生 hello JSON 檔案，一旦從 hello JSON 產生金鑰 blob 檔案和摘要它 toorestore 金鑰 cmdlet tooput hello 金鑰 (KEK) hello 金鑰保存庫中。

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a>還原密碼
JSON 檔案使用 hello tooget 秘密名稱和值在上面所產生，以及摘要它 tooset 秘密 cmdlet tooput hello 密碼 (BEK) hello 金鑰保存庫中。 **如果使用 BEK 和 KEK 加密您的 VM，請使用下列 Cmdlet。**

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

如果您的 VM 是**加密僅使用 BEK**、 從 hello JSON 產生密碼的 blob 檔案和摘要它 toorestore 秘密 cmdlet tooput hello 密碼 (BEK) 在 hello 金鑰保存庫。

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. $Secretname 值可透過參考 $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl toohello 輸出，並使用密碼之後的文字/例如輸出秘密 URL https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 的秘密名稱是 B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. Hello 標記 DiskEncryptionKeyFileName 值是做為密碼的名稱相同。
>
>

## <a name="create-virtual-machine-from-restored-disk"></a>從已還原的磁碟建立虛擬機器
如果您已備份加密使用 Azure VM 備份的 VM，hello PowerShell cmdlet 上述說明您可以還原金鑰和秘密後 toohello 金鑰保存庫。 之後進行還原，請參閱 hello 文章[管理使用 PowerShell 的 Azure Vm 的備份與還原](backup-azure-vms-automation.md#create-a-vm-from-restored-disks)toocreate 加密 Vm 從還原的磁碟、 金鑰和密碼。

## <a name="legacy-approach"></a>舊版方法
上述的 hello 方法將適用於所有 hello 復原點。 不過，hello 舊的復原點，從取得金鑰和秘密資訊的方法，可適用於早於 2017 年 7 月 11，對於使用 BEK 和 KEK 加密的 Vm 的復原點。 一旦使用 [PowerShell 步驟](backup-azure-vms-automation.md#restore-an-azure-vm)完成加密 VM 的還原磁碟作業後，確保 $rp 填入有效的值。

### <a name="restore-key"></a>還原金鑰
使用下列 cmdlet tooget 金鑰 (KEK) 資訊的復原點的 hello 和摘要它 toorestore 金鑰 cmdlet tooput 回 hello 金鑰保存庫中。

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a>還原密碼
使用下列 cmdlet tooget 密碼 (BEK) 資訊的復原點的 hello 和摘要它 tooset 秘密 cmdlet tooput 回 hello 金鑰保存庫中。

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. $Secretname 值可以藉由參考 rp1 toohello 輸出取得。KeyAndSecretDetails.SecretUrl 和密碼之後，使用文字 / 例如輸出秘密 URL 為 https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 且密碼名稱為B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. Hello 標記 DiskEncryptionKeyFileName 值是做為密碼的名稱相同。
> 3. DiskEncryptionKeyEncryptionKeyURL 值可以從金鑰保存庫還原回 hello 金鑰，並使用之後取得[Get AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet
>
>

## <a name="next-steps"></a>後續步驟
之後還原金鑰和秘密後 tookey 保存庫，請參閱 hello 文章[管理使用 PowerShell 的 Azure Vm 的備份與還原](backup-azure-vms-automation.md#create-a-vm-from-restored-disks)toocreate 加密 Vm 從還原的磁碟、 金鑰和密碼。

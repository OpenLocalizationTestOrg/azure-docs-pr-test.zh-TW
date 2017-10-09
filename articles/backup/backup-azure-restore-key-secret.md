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
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a><span data-ttu-id="5aa92-103">使用 Azure 備份還原已加密 VM 的金鑰保存庫金鑰與密碼</span><span class="sxs-lookup"><span data-stu-id="5aa92-103">Restore Key Vault key and secret for encrypted VMs using Azure Backup</span></span>
<span data-ttu-id="5aa92-104">這篇文章討論有關使用 Azure VM 備份 tooperform 還原加密的 Azure Vm，如果您的金鑰和密碼不存在 hello 金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="5aa92-104">This article talks about using Azure VM Backup tooperform restore of encrypted Azure VMs, if your key and secret do not exist in hello key vault.</span></span> <span data-ttu-id="5aa92-105">如果您想 toomaintain 金鑰 （金鑰加密） 的個別複本，而且 hello 的密碼 （BitLocker 加密金鑰） 還原 VM，也可以使用下列步驟。</span><span class="sxs-lookup"><span data-stu-id="5aa92-105">These steps can also be used if you want toomaintain a separate copy of key (Key Encryption Key) and secret (BitLocker Encryption Key) for hello restored VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5aa92-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="5aa92-106">Prerequisites</span></span>
* <span data-ttu-id="5aa92-107">**備份已加密的 VM** - 已使用 Azure 備份將已加密的 Azure VM 備份。</span><span class="sxs-lookup"><span data-stu-id="5aa92-107">**Backup encrypted VMs** - Encrypted Azure VMs have been backed up using Azure Backup.</span></span> <span data-ttu-id="5aa92-108">Hello 發行項，請參閱[管理使用 PowerShell 的 Azure Vm 的備份與還原](backup-azure-vms-automation.md)如需詳細資訊 toobackup 加密 Azure Vm 的方式。</span><span class="sxs-lookup"><span data-stu-id="5aa92-108">Refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) for details about how toobackup encrypted Azure VMs.</span></span>
* <span data-ttu-id="5aa92-109">**設定 Azure 金鑰保存庫**– toowhich 金鑰，請確定該金鑰的保存庫，並還原密碼需要 toobe 已經存在。</span><span class="sxs-lookup"><span data-stu-id="5aa92-109">**Configure Azure Key Vault** – Ensure that key vault toowhich keys and secrets need toobe restored is already present.</span></span> <span data-ttu-id="5aa92-110">Hello 發行項，請參閱[開始使用 Azure 金鑰保存庫](../key-vault/key-vault-get-started.md)如需金鑰保存庫的管理詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5aa92-110">Refer hello article [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md) for details about key vault management.</span></span>
* <span data-ttu-id="5aa92-111">**還原磁碟** - 請確定您已使用 [PowerShell 步驟](backup-azure-vms-automation.md#restore-an-azure-vm)觸發還原作業，以還原加密 VM 的磁碟。</span><span class="sxs-lookup"><span data-stu-id="5aa92-111">**Restore disk** - Ensure that you have triggered restore job for restoring disks for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm).</span></span> <span data-ttu-id="5aa92-112">這是因為此作業會產生的 JSON 檔案包含金鑰和密碼的加密 hello VM toobe 還原您儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="5aa92-112">This is because this job generates a JSON file in your storage account containing keys and secrets for hello encrypted VM toobe restored.</span></span>

## <a name="get-key-and-secret-from-azure-backup"></a><span data-ttu-id="5aa92-113">從 Azure 備份取得金鑰和祕密</span><span class="sxs-lookup"><span data-stu-id="5aa92-113">Get key and secret from Azure Backup</span></span>

> [!NOTE]
> <span data-ttu-id="5aa92-114">一旦 hello 加密 VM 磁碟已還原，請確認：</span><span class="sxs-lookup"><span data-stu-id="5aa92-114">Once disk has been restored for hello encrypted VM, ensure that:</span></span>
> 1. <span data-ttu-id="5aa92-115">$details 填入還原磁碟作業詳細資料，如中所述[還原 hello 磁碟 區段中的 PowerShell 步驟](backup-azure-vms-automation.md#restore-an-azure-vm)</span><span class="sxs-lookup"><span data-stu-id="5aa92-115">$details is populated with restore disk job details, as mentioned in [PowerShell steps in Restore hello Disks section](backup-azure-vms-automation.md#restore-an-azure-vm)</span></span>
> 2. <span data-ttu-id="5aa92-116">應該從還原的硬碟建立 VM**金鑰和密碼是還原的 tookey 保存庫之後**。</span><span class="sxs-lookup"><span data-stu-id="5aa92-116">VM should be created from restored disks only **after key and secret is restored tookey vault**.</span></span>
>
>

<span data-ttu-id="5aa92-117">查詢 hello 還原 hello 工作詳細資料的磁碟內容。</span><span class="sxs-lookup"><span data-stu-id="5aa92-117">Query hello restored disk properties for hello job details.</span></span>

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

<span data-ttu-id="5aa92-118">設定 hello Azure 儲存體的內容，並還原加密的 VM 包含金鑰和秘密提示問題的詳細資料的 JSON 組態檔。</span><span class="sxs-lookup"><span data-stu-id="5aa92-118">Set hello Azure storage context and restore JSON configuration file containing key and secret details for encrypted VM.</span></span>

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a><span data-ttu-id="5aa92-119">還原金鑰</span><span class="sxs-lookup"><span data-stu-id="5aa92-119">Restore key</span></span>
<span data-ttu-id="5aa92-120">上述的 hello 目的地路徑中產生 hello JSON 檔案，一旦從 hello JSON 產生金鑰 blob 檔案和摘要它 toorestore 金鑰 cmdlet tooput hello 金鑰 (KEK) hello 金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="5aa92-120">Once hello JSON file is generated in hello destination path mentioned above, generate key blob file from hello JSON and feed it toorestore key cmdlet tooput hello key (KEK) back in hello key vault.</span></span>

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a><span data-ttu-id="5aa92-121">還原密碼</span><span class="sxs-lookup"><span data-stu-id="5aa92-121">Restore secret</span></span>
<span data-ttu-id="5aa92-122">JSON 檔案使用 hello tooget 秘密名稱和值在上面所產生，以及摘要它 tooset 秘密 cmdlet tooput hello 密碼 (BEK) hello 金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="5aa92-122">Use hello JSON file generated above tooget secret name and value and feed it tooset secret cmdlet tooput hello secret (BEK) back in hello key vault.</span></span> <span data-ttu-id="5aa92-123">**如果使用 BEK 和 KEK 加密您的 VM，請使用下列 Cmdlet。**</span><span class="sxs-lookup"><span data-stu-id="5aa92-123">**Use these cmdlets if your VM is encrypted using BEK and KEK.**</span></span>

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

<span data-ttu-id="5aa92-124">如果您的 VM 是**加密僅使用 BEK**、 從 hello JSON 產生密碼的 blob 檔案和摘要它 toorestore 秘密 cmdlet tooput hello 密碼 (BEK) 在 hello 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="5aa92-124">If your VM is **encrypted using BEK only**, generate secret blob file from hello JSON and feed it toorestore secret cmdlet tooput hello secret (BEK) back in hello key vault.</span></span>

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. <span data-ttu-id="5aa92-125">$Secretname 值可透過參考 $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl toohello 輸出，並使用密碼之後的文字/例如輸出秘密 URL https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 的秘密名稱是 B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="5aa92-125">Value for $secretname can be obtained by referring toohello output of $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="5aa92-126">Hello 標記 DiskEncryptionKeyFileName 值是做為密碼的名稱相同。</span><span class="sxs-lookup"><span data-stu-id="5aa92-126">Value of hello tag DiskEncryptionKeyFileName is same as secret name.</span></span>
>
>

## <a name="create-virtual-machine-from-restored-disk"></a><span data-ttu-id="5aa92-127">從已還原的磁碟建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5aa92-127">Create virtual machine from restored disk</span></span>
<span data-ttu-id="5aa92-128">如果您已備份加密使用 Azure VM 備份的 VM，hello PowerShell cmdlet 上述說明您可以還原金鑰和秘密後 toohello 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="5aa92-128">If you have backed up encrypted VM using Azure VM Backup, hello PowerShell cmdlets mentioned above help you restore key and secret back toohello key vault.</span></span> <span data-ttu-id="5aa92-129">之後進行還原，請參閱 hello 文章[管理使用 PowerShell 的 Azure Vm 的備份與還原](backup-azure-vms-automation.md#create-a-vm-from-restored-disks)toocreate 加密 Vm 從還原的磁碟、 金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="5aa92-129">After restoring them, refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate encrypted VMs from restored disk, key, and secret.</span></span>

## <a name="legacy-approach"></a><span data-ttu-id="5aa92-130">舊版方法</span><span class="sxs-lookup"><span data-stu-id="5aa92-130">Legacy approach</span></span>
<span data-ttu-id="5aa92-131">上述的 hello 方法將適用於所有 hello 復原點。</span><span class="sxs-lookup"><span data-stu-id="5aa92-131">hello approach mentioned above would work for all hello recovery points.</span></span> <span data-ttu-id="5aa92-132">不過，hello 舊的復原點，從取得金鑰和秘密資訊的方法，可適用於早於 2017 年 7 月 11，對於使用 BEK 和 KEK 加密的 Vm 的復原點。</span><span class="sxs-lookup"><span data-stu-id="5aa92-132">However, hello older approach of getting key and secret information from recovery point, would be valid for recovery points older than July 11, 2017 for VMs encrypted using BEK and KEK.</span></span> <span data-ttu-id="5aa92-133">一旦使用 [PowerShell 步驟](backup-azure-vms-automation.md#restore-an-azure-vm)完成加密 VM 的還原磁碟作業後，確保 $rp 填入有效的值。</span><span class="sxs-lookup"><span data-stu-id="5aa92-133">Once restore disk job is complete for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm), ensure that $rp is populated with a valid value.</span></span>

### <a name="restore-key"></a><span data-ttu-id="5aa92-134">還原金鑰</span><span class="sxs-lookup"><span data-stu-id="5aa92-134">Restore key</span></span>
<span data-ttu-id="5aa92-135">使用下列 cmdlet tooget 金鑰 (KEK) 資訊的復原點的 hello 和摘要它 toorestore 金鑰 cmdlet tooput 回 hello 金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="5aa92-135">Use hello following cmdlets tooget key (KEK) information from recovery point and feed it toorestore key cmdlet tooput it back in hello key vault.</span></span>

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a><span data-ttu-id="5aa92-136">還原密碼</span><span class="sxs-lookup"><span data-stu-id="5aa92-136">Restore secret</span></span>
<span data-ttu-id="5aa92-137">使用下列 cmdlet tooget 密碼 (BEK) 資訊的復原點的 hello 和摘要它 tooset 秘密 cmdlet tooput 回 hello 金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="5aa92-137">Use hello following cmdlets tooget secret (BEK) information from recovery point and feed it tooset secret cmdlet tooput it back in hello key vault.</span></span>

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. <span data-ttu-id="5aa92-138">$Secretname 值可以藉由參考 rp1 toohello 輸出取得。KeyAndSecretDetails.SecretUrl 和密碼之後，使用文字 / 例如輸出秘密 URL 為 https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 且密碼名稱為B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="5aa92-138">Value for $secretname can be obtained by referring toohello output of $rp1.KeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="5aa92-139">Hello 標記 DiskEncryptionKeyFileName 值是做為密碼的名稱相同。</span><span class="sxs-lookup"><span data-stu-id="5aa92-139">Value of hello tag DiskEncryptionKeyFileName is same as secret name.</span></span>
> 3. <span data-ttu-id="5aa92-140">DiskEncryptionKeyEncryptionKeyURL 值可以從金鑰保存庫還原回 hello 金鑰，並使用之後取得[Get AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span><span class="sxs-lookup"><span data-stu-id="5aa92-140">Value for DiskEncryptionKeyEncryptionKeyURL can be obtained from key vault after restoring hello keys back and using [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="5aa92-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5aa92-141">Next steps</span></span>
<span data-ttu-id="5aa92-142">之後還原金鑰和秘密後 tookey 保存庫，請參閱 hello 文章[管理使用 PowerShell 的 Azure Vm 的備份與還原](backup-azure-vms-automation.md#create-a-vm-from-restored-disks)toocreate 加密 Vm 從還原的磁碟、 金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="5aa92-142">After restoring key and secret back tookey vault, refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate encrypted VMs from restored disk, key and secret.</span></span>

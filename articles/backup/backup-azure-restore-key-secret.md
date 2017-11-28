---
title: "使用 Azure 備份還原已加密 VM 的金鑰保存庫金鑰與密碼 | Microsoft Docs"
description: "了解如何使用 PowerShell 以 Azure 備份還原金鑰保存庫金鑰與密碼"
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
ms.openlocfilehash: f2db3449187d655248b13198b268841052570626
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a><span data-ttu-id="47c07-103">使用 Azure 備份還原已加密 VM 的金鑰保存庫金鑰與密碼</span><span class="sxs-lookup"><span data-stu-id="47c07-103">Restore Key Vault key and secret for encrypted VMs using Azure Backup</span></span>
<span data-ttu-id="47c07-104">本文將討論如果您的金鑰和密碼不存在於金鑰保存庫中時，如何使用 Azure VM 備份還原已加密的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="47c07-104">This article talks about using Azure VM Backup to perform restore of encrypted Azure VMs, if your key and secret do not exist in the key vault.</span></span> <span data-ttu-id="47c07-105">這些步驟也可用於您想要為已還原的 VM 另外維護一份金鑰 (金鑰加密金鑰) 與密碼 (BitLocker 加密金鑰) 時。</span><span class="sxs-lookup"><span data-stu-id="47c07-105">These steps can also be used if you want to maintain a separate copy of key (Key Encryption Key) and secret (BitLocker Encryption Key) for the restored VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47c07-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="47c07-106">Prerequisites</span></span>
* <span data-ttu-id="47c07-107">**備份已加密的 VM** - 已使用 Azure 備份將已加密的 Azure VM 備份。</span><span class="sxs-lookup"><span data-stu-id="47c07-107">**Backup encrypted VMs** - Encrypted Azure VMs have been backed up using Azure Backup.</span></span> <span data-ttu-id="47c07-108">請參閱[使用 PowerShell 部署和管理 Resource Manager 部署之 VM 的備份](backup-azure-vms-automation.md)一文，以取得如何將已加密 Azure VM 備份的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="47c07-108">Refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) for details about how to backup encrypted Azure VMs.</span></span>
* <span data-ttu-id="47c07-109">**設定 Azure 金鑰保存庫** – 先確定金鑰保存庫已存在，才能將金鑰和密碼還原至該金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="47c07-109">**Configure Azure Key Vault** – Ensure that key vault to which keys and secrets need to be restored is already present.</span></span> <span data-ttu-id="47c07-110">請參閱[開始使用 Azure 金鑰保存庫](../key-vault/key-vault-get-started.md)一文，以取得金鑰保存庫管理的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="47c07-110">Refer the article [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md) for details about key vault management.</span></span>
* <span data-ttu-id="47c07-111">**還原磁碟** - 請確定您已使用 [PowerShell 步驟](backup-azure-vms-automation.md#restore-an-azure-vm)觸發還原作業，以還原加密 VM 的磁碟。</span><span class="sxs-lookup"><span data-stu-id="47c07-111">**Restore disk** - Ensure that you have triggered restore job for restoring disks for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm).</span></span> <span data-ttu-id="47c07-112">這是因為此作業會在您的儲存體帳戶中產生 JSON 檔案，其中包含要還原之加密 VM 的金鑰和祕密。</span><span class="sxs-lookup"><span data-stu-id="47c07-112">This is because this job generates a JSON file in your storage account containing keys and secrets for the encrypted VM to be restored.</span></span>

## <a name="get-key-and-secret-from-azure-backup"></a><span data-ttu-id="47c07-113">從 Azure 備份取得金鑰和祕密</span><span class="sxs-lookup"><span data-stu-id="47c07-113">Get key and secret from Azure Backup</span></span>

> [!NOTE]
> <span data-ttu-id="47c07-114">一旦還原加密 VM 的磁碟後，請確定：</span><span class="sxs-lookup"><span data-stu-id="47c07-114">Once disk has been restored for the encrypted VM, ensure that:</span></span>
> 1. <span data-ttu-id="47c07-115">系統會將還原磁碟作業詳細資料填入 $details，如[還原 [磁碟] 區段中的 PowerShell 步驟](backup-azure-vms-automation.md#restore-an-azure-vm)中所述</span><span class="sxs-lookup"><span data-stu-id="47c07-115">$details is populated with restore disk job details, as mentioned in [PowerShell steps in Restore the Disks section](backup-azure-vms-automation.md#restore-an-azure-vm)</span></span>
> 2. <span data-ttu-id="47c07-116">僅在**將金鑰和秘密還原至金鑰保存庫之後**，才應該從還原的硬碟建立 VM。</span><span class="sxs-lookup"><span data-stu-id="47c07-116">VM should be created from restored disks only **after key and secret is restored to key vault**.</span></span>
>
>

<span data-ttu-id="47c07-117">查詢工作詳細資料的已還原磁碟內容。</span><span class="sxs-lookup"><span data-stu-id="47c07-117">Query the restored disk properties for the job details.</span></span>

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

<span data-ttu-id="47c07-118">設定 Azure 儲存體內容並還原 JSON 組態檔，其中包含加密 VM 之金鑰和秘密的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="47c07-118">Set the Azure storage context and restore JSON configuration file containing key and secret details for encrypted VM.</span></span>

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a><span data-ttu-id="47c07-119">還原金鑰</span><span class="sxs-lookup"><span data-stu-id="47c07-119">Restore key</span></span>
<span data-ttu-id="47c07-120">一旦在上述目的地路徑中產生 JSON 檔案後，請從 JSON 產生金鑰 blob 檔案，並將其饋送至還原金鑰 Cmdlet，以將金鑰 (KEK) 放回金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="47c07-120">Once the JSON file is generated in the destination path mentioned above, generate key blob file from the JSON and feed it to restore key cmdlet to put the key (KEK) back in the key vault.</span></span>

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a><span data-ttu-id="47c07-121">還原密碼</span><span class="sxs-lookup"><span data-stu-id="47c07-121">Restore secret</span></span>
<span data-ttu-id="47c07-122">使用上面所產生的 JSON 檔案來取得秘密名稱和值，並將其饋送至設定祕密 Cmdlet，以將祕密 (BEK) 放回金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="47c07-122">Use the JSON file generated above to get secret name and value and feed it to set secret cmdlet to put the secret (BEK) back in the key vault.</span></span> <span data-ttu-id="47c07-123">**如果使用 BEK 和 KEK 加密您的 VM，請使用下列 Cmdlet。**</span><span class="sxs-lookup"><span data-stu-id="47c07-123">**Use these cmdlets if your VM is encrypted using BEK and KEK.**</span></span>

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

<span data-ttu-id="47c07-124">如果**只使用 BEK 加密**您的 VM，請從 JSON 產生密碼 Blob 檔案並提供給還原密碼 Cmdlet，以將密碼 (BEK) 放回金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="47c07-124">If your VM is **encrypted using BEK only**, generate secret blob file from the JSON and feed it to restore secret cmdlet to put the secret (BEK) back in the key vault.</span></span>

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. <span data-ttu-id="47c07-125">可透過參考 $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl 的輸出，並使用祕密之後的文字來取得 $secretname 的值/ 例如輸出秘密 URL 是 https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 且祕密名稱是 B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="47c07-125">Value for $secretname can be obtained by referring to the output of $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="47c07-126">DiskEncryptionKeyFileName 標記的值與祕密名稱相同。</span><span class="sxs-lookup"><span data-stu-id="47c07-126">Value of the tag DiskEncryptionKeyFileName is same as secret name.</span></span>
>
>

## <a name="create-virtual-machine-from-restored-disk"></a><span data-ttu-id="47c07-127">從已還原的磁碟建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="47c07-127">Create virtual machine from restored disk</span></span>
<span data-ttu-id="47c07-128">如果您已使用 Azure VM 備份將已加密的 VM 備份，上述的 PowerShell Cmdlet 可幫助您將金鑰與密碼還原回金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="47c07-128">If you have backed up encrypted VM using Azure VM Backup, the PowerShell cmdlets mentioned above help you restore key and secret back to the key vault.</span></span> <span data-ttu-id="47c07-129">還原金鑰與密碼後，請參閱[使用 PowerShell 管理 Azure VM 的備份和還原](backup-azure-vms-automation.md#create-a-vm-from-restored-disks)一文，從已還原的磁碟、金鑰和密碼建立加密的 VM。</span><span class="sxs-lookup"><span data-stu-id="47c07-129">After restoring them, refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to create encrypted VMs from restored disk, key, and secret.</span></span>

## <a name="legacy-approach"></a><span data-ttu-id="47c07-130">舊版方法</span><span class="sxs-lookup"><span data-stu-id="47c07-130">Legacy approach</span></span>
<span data-ttu-id="47c07-131">上述方法可適用於所有復原點。</span><span class="sxs-lookup"><span data-stu-id="47c07-131">The approach mentioned above would work for all the recovery points.</span></span> <span data-ttu-id="47c07-132">不過，從復原點取得金鑰和密碼資訊的較舊方法，對於 2017 年 7 月 11 日以前使用 BEK 和 KEK 加密之 VM 的復原點仍有效。</span><span class="sxs-lookup"><span data-stu-id="47c07-132">However, the older approach of getting key and secret information from recovery point, would be valid for recovery points older than July 11, 2017 for VMs encrypted using BEK and KEK.</span></span> <span data-ttu-id="47c07-133">一旦使用 [PowerShell 步驟](backup-azure-vms-automation.md#restore-an-azure-vm)完成加密 VM 的還原磁碟作業後，確保 $rp 填入有效的值。</span><span class="sxs-lookup"><span data-stu-id="47c07-133">Once restore disk job is complete for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm), ensure that $rp is populated with a valid value.</span></span>

### <a name="restore-key"></a><span data-ttu-id="47c07-134">還原金鑰</span><span class="sxs-lookup"><span data-stu-id="47c07-134">Restore key</span></span>
<span data-ttu-id="47c07-135">使用下列 Cmdlet 從復原點取得金鑰 (KEK) 資訊，並將其饋送至還原金鑰 Cmdlet 以放回金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="47c07-135">Use the following cmdlets to get key (KEK) information from recovery point and feed it to restore key cmdlet to put it back in the key vault.</span></span>

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a><span data-ttu-id="47c07-136">還原密碼</span><span class="sxs-lookup"><span data-stu-id="47c07-136">Restore secret</span></span>
<span data-ttu-id="47c07-137">使用下列 Cmdlet 從復原點取得祕密 (BEK) 資訊，並將其饋送至設定祕密 Cmdlet 以放回金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="47c07-137">Use the following cmdlets to get secret (BEK) information from recovery point and feed it to set secret cmdlet to put it back in the key vault.</span></span>

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. <span data-ttu-id="47c07-138">可透過參考 $rp1.KeyAndSecretDetails.SecretUrl 的輸出，並使用祕密之後的文字來取得 $secretname 的值/ 例如輸出秘密 URL 是 https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 且祕密名稱是 B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="47c07-138">Value for $secretname can be obtained by referring to the output of $rp1.KeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="47c07-139">DiskEncryptionKeyFileName 標記的值與祕密名稱相同。</span><span class="sxs-lookup"><span data-stu-id="47c07-139">Value of the tag DiskEncryptionKeyFileName is same as secret name.</span></span>
> 3. <span data-ttu-id="47c07-140">還原回金鑰並使用 [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) Cmdlet 後，便可從金鑰保存庫取得 DiskEncryptionKeyEncryptionKeyURL 的值</span><span class="sxs-lookup"><span data-stu-id="47c07-140">Value for DiskEncryptionKeyEncryptionKeyURL can be obtained from key vault after restoring the keys back and using [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="47c07-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="47c07-141">Next steps</span></span>
<span data-ttu-id="47c07-142">將金鑰與祕密還原回金鑰保存庫後，請參閱[使用 PowerShell 管理 Azure VM 的備份和還原](backup-azure-vms-automation.md#create-a-vm-from-restored-disks)一文，從已還原的磁碟、金鑰和祕密建立加密的 VM。</span><span class="sxs-lookup"><span data-stu-id="47c07-142">After restoring key and secret back to key vault, refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to create encrypted VMs from restored disk, key and secret.</span></span>

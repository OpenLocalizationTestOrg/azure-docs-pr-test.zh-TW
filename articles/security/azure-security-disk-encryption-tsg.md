---
title: "磁碟加密疑難排解 aaaAzure |Microsoft 文件"
description: "本文提供的疑難排解秘訣適用於 Windows 及 Linux IaaS VM 適用的 Microsoft Azure 磁碟加密。"
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: ce0e23bd-07eb-43af-a56c-aa1a73bdb747
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: devtiw
ms.openlocfilehash: 2ecb8df1fb869e3bf8f3be4be4494e6485e75695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-troubleshooting-guide"></a><span data-ttu-id="22bd4-103">Azure 磁碟加密疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="22bd4-103">Azure Disk Encryption Troubleshooting Guide</span></span>

<span data-ttu-id="22bd4-104">此指南適用於資訊技術 (IT) 專業人員，資訊安全性分析師和雲端系統管理員的組織使用 Azure 磁碟加密，而且需要指引 tootroubleshoot 磁碟加密相關的問題。</span><span class="sxs-lookup"><span data-stu-id="22bd4-104">This guide is for information technology (IT) professionals, information security analysts, and cloud administrators whose organizations are using Azure disk encryption and need guidance tootroubleshoot disk-encryption related issues.</span></span>

## <a name="troubleshooting-linux-os-disk-encryption"></a><span data-ttu-id="22bd4-105">針對 Linux OS 磁碟加密進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="22bd4-105">Troubleshooting Linux OS disk encryption</span></span>

<span data-ttu-id="22bd4-106">Linux OS 磁碟加密，必須取消掛接 hello 作業系統磁碟機先前 toorunning 透過 hello 完整磁碟加密程序。</span><span class="sxs-lookup"><span data-stu-id="22bd4-106">Linux OS disk encryption must unmount hello OS drive prior toorunning it through hello full disk encryption process.</span></span>   <span data-ttu-id="22bd4-107">如果不行，錯誤訊息為 「 失敗之後 toounmount...」</span><span class="sxs-lookup"><span data-stu-id="22bd4-107">If it cannot, an error message of "failed toounmount after…"</span></span> <span data-ttu-id="22bd4-108">可能的 toooccur 錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="22bd4-108">error message is likely toooccur.</span></span>

<span data-ttu-id="22bd4-109">在已從其支援內建資源庫映像修改或變更的目標 VM 環境中嘗試 OS 磁碟加密時，這是最有可能的。</span><span class="sxs-lookup"><span data-stu-id="22bd4-109">This is most likely when OS disk encryption is attempted on a target VM environment that has been modified or changed from its supported stock gallery image.</span></span>  <span data-ttu-id="22bd4-110">偏離 hello 支援映像，這可能會干擾 hello 擴充功能的能力 toounmount hello 作業系統磁碟機的範例包括：</span><span class="sxs-lookup"><span data-stu-id="22bd4-110">Examples of deviations from hello supported image, which can interfere with hello extension’s ability toounmount hello OS drive include:</span></span>
- <span data-ttu-id="22bd4-111">不再符合支援的檔案系統和/或資料分割配置的自訂映像。</span><span class="sxs-lookup"><span data-stu-id="22bd4-111">Customized images that no longer match a supported file system and/or partitioning scheme.</span></span>
- <span data-ttu-id="22bd4-112">與應用程式，例如防毒軟體、 Docker、 SAP、 MongoDB、 或 Apache Cassandra hello OS 先前 tooencryption 中執行的自訂映像。</span><span class="sxs-lookup"><span data-stu-id="22bd4-112">Customized images with applications such as antivirus, Docker, SAP, MongoDB, or Apache Cassandra running in hello OS prior tooencryption.</span></span>  <span data-ttu-id="22bd4-113">這些應用程式是難以 tooterminate，而且當它們保留開啟檔案控制代碼 toohello 作業系統磁碟機，hello 磁碟機不能卸載，造成失敗。</span><span class="sxs-lookup"><span data-stu-id="22bd4-113">These applications are difficult tooterminate, and when they retain open file handles toohello OS drive, hello drive cannot be unmounted, causing failure.</span></span>
- <span data-ttu-id="22bd4-114">自訂指令碼中執行的關閉的時間相近 toohello 加密步驟可能會妨礙，而且會導致此失敗。</span><span class="sxs-lookup"><span data-stu-id="22bd4-114">Custom scripts that run in close time proximity toohello encryption step can interfere and cause this failure.</span></span> <span data-ttu-id="22bd4-115">這可能發生資源管理員範本可定義多個擴充功能 tooexecute 同時，或自訂指令碼延伸或其他動作執行時同時 toodisk 加密。</span><span class="sxs-lookup"><span data-stu-id="22bd4-115">This can happen when a Resource Manager template defines multiple extensions tooexecute simultaneously, or when a custom script extension or other action is run simultaneously toodisk encryption.</span></span>   <span data-ttu-id="22bd4-116">序列化和隔離這類步驟可能解決 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="22bd4-116">Serializing and isolating such steps may resolve hello issue.</span></span>
- <span data-ttu-id="22bd4-117">當 SELinux 已停用先前 tooenabling 加密時，hello 卸載步驟會失敗。</span><span class="sxs-lookup"><span data-stu-id="22bd4-117">When SELinux has not been disabled prior tooenabling encryption, hello unmount step fails.</span></span>  <span data-ttu-id="22bd4-118">完成加密後，即可重新啟用 SELinux。</span><span class="sxs-lookup"><span data-stu-id="22bd4-118">SELinux can be re-enabled after encryption has completed.</span></span>
- <span data-ttu-id="22bd4-119">當 hello OS 磁碟正在使用 LVM 配置 （雖然可以有限的 LVM 資料磁碟支援，但是 LVM OS 磁碟將不會）</span><span class="sxs-lookup"><span data-stu-id="22bd4-119">When hello OS disk is using an LVM scheme (although limited LVM data disk support is available, LVM OS disk is not)</span></span>
- <span data-ttu-id="22bd4-120">當未符合最小記憶體需求時 (OS 磁碟加密建議為 7 GB)</span><span class="sxs-lookup"><span data-stu-id="22bd4-120">When minimum memory requirements are not met (7GB is suggested for OS disk encryption)</span></span>
- <span data-ttu-id="22bd4-121">當資料磁碟機已遞迴掛接於 /mnt/ directory 下，或彼此掛接 (例如，/mnt/data1、/mnt/data2、/data3 + /data3/data4 等等)</span><span class="sxs-lookup"><span data-stu-id="22bd4-121">When data drives have been recursively mounted under /mnt/ directory, or each other (for example, /mnt/data1, /mnt/data2, /data3 + /data3/data4, etc.)</span></span>
- <span data-ttu-id="22bd4-122">未符合其他 Linux 適用的 Azure 磁碟加密[必要條件](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)時</span><span class="sxs-lookup"><span data-stu-id="22bd4-122">When other Azure Disk Encryption [prerequisites](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) for Linux are not met</span></span>

## <a name="unable-tooencrypt"></a><span data-ttu-id="22bd4-123">無法 tooencrypt</span><span class="sxs-lookup"><span data-stu-id="22bd4-123">Unable tooencrypt</span></span>

<span data-ttu-id="22bd4-124">在某些情況下，toobe 停滯於 「 啟動 OS 磁碟加密 」 和 SSH 已停用，會顯示 hello Linux 磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="22bd4-124">In some cases, hello Linux disk encryption appears toobe stuck at "OS disk encryption started" and SSH is disabled.</span></span> <span data-ttu-id="22bd4-125">此程序可能需要 3-16 小時 toocomplete 上內建資源庫映像之間。</span><span class="sxs-lookup"><span data-stu-id="22bd4-125">This process can take between 3-16 hours toocomplete on a stock gallery image.</span></span>  <span data-ttu-id="22bd4-126">如果加入多個 TB 大小的資料磁碟，hello 程序可能需要天。</span><span class="sxs-lookup"><span data-stu-id="22bd4-126">If multi-TB size data disks are added, hello process may take days.</span></span> <span data-ttu-id="22bd4-127">hello Linux 作業系統磁碟加密順序暫時取消掛接 hello 作業系統磁碟機，並且執行整個 OS 磁碟 hello，裝載在加密狀態之前以區塊加密。</span><span class="sxs-lookup"><span data-stu-id="22bd4-127">hello Linux OS disk encryption sequence unmounts hello OS drive temporarily, and performs block by block encryption of hello entire OS disk, before remounting it in its encrypted state.</span></span>   <span data-ttu-id="22bd4-128">不同於 Windows 上的 Azure 磁碟加密，Linux 磁碟加密不允許同時使用 hello VM hello 加密進行中時。</span><span class="sxs-lookup"><span data-stu-id="22bd4-128">Unlike Azure Disk Encryption on Windows, Linux Disk Encryption does not allow concurrent use of hello VM while hello encryption is in progress.</span></span>  <span data-ttu-id="22bd4-129">hello hello VM，包括 hello 大小 hello 磁碟和標準或進階 (SSD) 儲存體是否支援 hello 儲存體帳戶的效能特性可能會大幅影響 hello 所需時間 toocomplete 加密。</span><span class="sxs-lookup"><span data-stu-id="22bd4-129">hello performance characteristics of hello VM, including hello size of hello disk and whether hello storage account is backed by standard or premium (SSD) storage, can greatly influence hello time required toocomplete encryption.</span></span>

<span data-ttu-id="22bd4-130">toocheck 狀態 hello ProgressMessage 欄位傳回的 hello [Get AzureRmVmDiskEncryptionStatus](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus)可輪詢命令。</span><span class="sxs-lookup"><span data-stu-id="22bd4-130">toocheck status, hello ProgressMessage field returned from hello [Get-AzureRmVmDiskEncryptionStatus](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) command can be polled.</span></span>   <span data-ttu-id="22bd4-131">Hello 作業系統磁碟機已加密，hello VM 便會進入服務的狀態，與 SSH 也是已停用的 tooprevent 任何中斷 toohello 的進行中程序。</span><span class="sxs-lookup"><span data-stu-id="22bd4-131">While hello OS drive is being encrypted, hello VM enters a servicing state, and SSH is also disabled tooprevent any disruption toohello ongoing process.</span></span>  <span data-ttu-id="22bd4-132">正在進行，之後數小時稍後 VMRestartPending 訊息，提示 toorestart hello VM 加密時，將報告 EncryptionInProgress hello 多數的 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="22bd4-132">EncryptionInProgress will be reported for hello majority of hello time while encryption is in progress, followed several hours later with a VMRestartPending message prompting toorestart hello VM.</span></span>  <span data-ttu-id="22bd4-133">例如：</span><span class="sxs-lookup"><span data-stu-id="22bd4-133">For example:</span></span>


```
PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : EncryptionInProgress
DataVolumesEncrypted       : EncryptionInProgress
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk encryption started

PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : VMRestartPending
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk successfully encrypted, please reboot hello VM
```

<span data-ttu-id="22bd4-134">一次出現提示 tooreboot hello VM，並重新啟動 hello VM，並提供 hello 重新開機，以及在 hello 目標上執行的最後步驟 toobe 2-3 分鐘之後, hello 狀態訊息會指出最後完成加密。</span><span class="sxs-lookup"><span data-stu-id="22bd4-134">Once prompted tooreboot hello VM, and after restarting hello VM, and giving 2-3 minutes for hello reboot and for final steps toobe performed on hello target, hello status message will indicate that encryption has finally completed.</span></span>   <span data-ttu-id="22bd4-135">一旦可以使用此訊息，hello 加密作業系統磁碟機是預期的 toobe 就緒供使用，以及可用的 hello VM toobe 一次。</span><span class="sxs-lookup"><span data-stu-id="22bd4-135">Once this message is available, hello encrypted OS drive is expected toobe ready for use and for hello VM toobe usable again.</span></span>

<span data-ttu-id="22bd4-136">萬一其中未看到此順序，或開機資訊、 進度訊息或其他錯誤指示器報告 OS 加密未能 hello 中間 （例如如果您看到 「 無法 toounmount 」 本指南中所述之錯誤的 hello），此程序建議 toorestore hello VM 後 toohello 快照式或取得 tooencryption 立即先前的備份。</span><span class="sxs-lookup"><span data-stu-id="22bd4-136">In cases where this sequence was not seen, or if boot information, progress message, or other error indicators report that OS encryption has failed in hello middle of this process (for example if you are seeing hello "failed toounmount" error described in this guide), it is recommended toorestore hello VM back toohello snapshot or backup taken immediately prior tooencryption.</span></span>  <span data-ttu-id="22bd4-137">先前 toohello 下一次嘗試，它會建議的 toore-評估 hello VM hello 特性，並確定所有必要條件已都滿足。</span><span class="sxs-lookup"><span data-stu-id="22bd4-137">Prior toohello next attempt, it is suggested toore-evaluate hello characteristics of hello VM and ensure that all prerequisites are satisfied.</span></span>

## <a name="troubleshooting-azure-disk-encryption-behind-a-firewall"></a><span data-ttu-id="22bd4-138">針對防火牆後方的 Azure 磁碟加密進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="22bd4-138">Troubleshooting Azure Disk Encryption behind a Firewall</span></span>
<span data-ttu-id="22bd4-139">當連線受到 hello 延伸 tooperform 防火牆、 proxy 需求，或是網路安全性群組 (nsg) 設定，hello 能力需要工作可以被中斷。</span><span class="sxs-lookup"><span data-stu-id="22bd4-139">When connectivity is restricted by a firewall, proxy requirement, or network security group (NSG) settings, hello ability of hello extension tooperform needed tasks can be disrupted.</span></span>   <span data-ttu-id="22bd4-140">這會導致例如 「 hello VM 上無法使用擴充狀態 」 的狀態訊息和失敗 toofinish 可預期案例中。</span><span class="sxs-lookup"><span data-stu-id="22bd4-140">This can result in status messages such as "Extension status not available on hello VM" and in expected scenarios failing toofinish.</span></span>  <span data-ttu-id="22bd4-141">hello 以下各節會有一些常見的防火牆問題，您可能需要調查。</span><span class="sxs-lookup"><span data-stu-id="22bd4-141">hello sections that follow has some common firewall issues that you may investigate.</span></span>

### <a name="network-security-groups"></a><span data-ttu-id="22bd4-142">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="22bd4-142">Network security groups</span></span>
<span data-ttu-id="22bd4-143">套用任何網路安全性群組群組設定仍然必須允許 hello 端點 toomeet hello 記載網路組態[必要條件](https://docs.microsoft.com/azure/security/azure-security-disk-encryption#prerequisites)磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="22bd4-143">Any network security group settings applied must still allow hello endpoint toomeet hello documented network configuration [prerequisites](https://docs.microsoft.com/azure/security/azure-security-disk-encryption#prerequisites) for disk encryption.</span></span>

### <a name="azure-keyvault-behind-firewall"></a><span data-ttu-id="22bd4-144">防火牆後方的 Azure Keyvault</span><span class="sxs-lookup"><span data-stu-id="22bd4-144">Azure Keyvault behind firewall</span></span>
<span data-ttu-id="22bd4-145">hello VM 必須能夠 tooaccess 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="22bd4-145">hello VM must be able tooaccess key vault.</span></span> <span data-ttu-id="22bd4-146">Tooguidance 上存取 tookey 錯誤由 hello 維護在防火牆之後，請參閱[金鑰保存庫](https://docs.microsoft.com/azure/key-vault/key-vault-access-behind-firewall)小組。</span><span class="sxs-lookup"><span data-stu-id="22bd4-146">Refer tooguidance on access tookey fault from behind a firewall that is maintained by hello [Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-access-behind-firewall) team.</span></span>

### <a name="linux-package-management-behind-firewall"></a><span data-ttu-id="22bd4-147">防火牆後方的 Linux 套件管理</span><span class="sxs-lookup"><span data-stu-id="22bd4-147">Linux package management behind firewall</span></span>
<span data-ttu-id="22bd4-148">在執行階段，適用於 Linux 的 Azure 磁碟加密依賴 hello 目標發佈的封裝管理系統需要 tooinstall 必要條件元件先前 tooenabling 加密。</span><span class="sxs-lookup"><span data-stu-id="22bd4-148">At run time, Azure Disk Encryption for Linux relies on hello target distribution’s package management system tooinstall needed prerequisite components prior tooenabling encryption.</span></span>  <span data-ttu-id="22bd4-149">如果防火牆設定導致無法 toodownload hello VM 和安裝這些元件，都必須後續失敗。</span><span class="sxs-lookup"><span data-stu-id="22bd4-149">If firewall settings prevent hello VM from being able toodownload and install these components, then subsequent failures are expected.</span></span>    <span data-ttu-id="22bd4-150">這可能會因發佈 hello 步驟 tooconfigure。</span><span class="sxs-lookup"><span data-stu-id="22bd4-150">hello steps tooconfigure this may vary by distribution.</span></span>  <span data-ttu-id="22bd4-151">在 Red Hat 上，在需要 Proxy 時，請務必確保已正確地設定您的訂用帳戶管理員和 Yum。</span><span class="sxs-lookup"><span data-stu-id="22bd4-151">On Red Hat, when a proxy is required, ensuring that subscription-manager and yum are set up properly is vital.</span></span>  <span data-ttu-id="22bd4-152">請參閱[此](https://access.redhat.com/solutions/189533) Red Hat 關於本主題的技術支援文件。</span><span class="sxs-lookup"><span data-stu-id="22bd4-152">See [this](https://access.redhat.com/solutions/189533) Red Hat support article on this topic.</span></span>  

## <a name="troubleshooting-windows-server-2016-server-core"></a><span data-ttu-id="22bd4-153">針對 Windows Server 2016 Server Core 進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="22bd4-153">Troubleshooting Windows Server 2016 Server Core</span></span>

<span data-ttu-id="22bd4-154">在 Windows Server 2016 Server Core 上不是預設可用的 hello bdehdcfg 元件。</span><span class="sxs-lookup"><span data-stu-id="22bd4-154">On Windows Server 2016 Server Core, hello bdehdcfg component is not available by default.</span></span> <span data-ttu-id="22bd4-155">Azure 磁碟加密需要此元件。</span><span class="sxs-lookup"><span data-stu-id="22bd4-155">This component is required by Azure Disk Encryption.</span></span>

<span data-ttu-id="22bd4-156">tooworkaround 這個問題，請複製 hello hello Server Core 映像的 Windows Server 2016 資料中心 VM toohello c:\windows\system32 資料夾中的下列 4 個檔案：</span><span class="sxs-lookup"><span data-stu-id="22bd4-156">tooworkaround this issue, copy hello following 4 files from a Windows Server 2016 Data Center VM toohello c:\windows\system32 folder of hello Server Core image:</span></span>

```
bdehdcfg.exe
bdehdcfglib.dll
bdehdcfglib.dll.mui
bdehdcfg.exe.mui
```

<span data-ttu-id="22bd4-157">然後，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="22bd4-157">Then, run hello following command:</span></span>

```
bdehdcfg.exe -target default
```

<span data-ttu-id="22bd4-158">這會建立 550 MB 的系統磁碟分割，然後重新開機後，您可以使用 Diskpart toocheck hello 磁碟區，並繼續進行。</span><span class="sxs-lookup"><span data-stu-id="22bd4-158">This will create a 550MB system partition and then after a reboot, you can use Diskpart toocheck hello volumes, and proceed.</span></span>  

<span data-ttu-id="22bd4-159">例如：</span><span class="sxs-lookup"><span data-stu-id="22bd4-159">For example:</span></span>

```
DISKPART> list vol

  Volume ###  Ltr  Label        Fs     Type        Size     Status     Info
  ----------  ---  -----------  -----  ----------  -------  ---------  --------
  Volume 0     C                NTFS   Partition    126 GB  Healthy    Boot
  Volume 1                      NTFS   Partition    550 MB  Healthy    System
  Volume 2     D   Temporary S  NTFS   Partition     13 GB  Healthy    Pagefile
```
## <a name="see-also"></a><span data-ttu-id="22bd4-160">另請參閱</span><span class="sxs-lookup"><span data-stu-id="22bd4-160">See also</span></span>
<span data-ttu-id="22bd4-161">在本文件中，您已了解 Azure 磁碟加密中一些常見的問題有關的詳細資訊及如何 tootroubleshoot。</span><span class="sxs-lookup"><span data-stu-id="22bd4-161">In this document, you learned more about some common issues in Azure disk encryption, and how tootroubleshoot.</span></span> <span data-ttu-id="22bd4-162">如需此服務和其功能的相關資訊，請閱讀：</span><span class="sxs-lookup"><span data-stu-id="22bd4-162">For more information about this service and its capability read:</span></span>

- [<span data-ttu-id="22bd4-163">在 Azure 資訊安全中心套用磁碟加密</span><span class="sxs-lookup"><span data-stu-id="22bd4-163">Apply disk encryption in Azure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [<span data-ttu-id="22bd4-164">加密 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="22bd4-164">Encrypt an Azure Virtual Machine</span></span>](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [<span data-ttu-id="22bd4-165">Azure 資料靜態加密</span><span class="sxs-lookup"><span data-stu-id="22bd4-165">Azure Data Encryption-at-Rest</span></span>](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)

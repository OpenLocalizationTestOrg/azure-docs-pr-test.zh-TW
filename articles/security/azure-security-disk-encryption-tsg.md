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
# <a name="azure-disk-encryption-troubleshooting-guide"></a>Azure 磁碟加密疑難排解指南

此指南適用於資訊技術 (IT) 專業人員，資訊安全性分析師和雲端系統管理員的組織使用 Azure 磁碟加密，而且需要指引 tootroubleshoot 磁碟加密相關的問題。

## <a name="troubleshooting-linux-os-disk-encryption"></a>針對 Linux OS 磁碟加密進行疑難排解

Linux OS 磁碟加密，必須取消掛接 hello 作業系統磁碟機先前 toorunning 透過 hello 完整磁碟加密程序。   如果不行，錯誤訊息為 「 失敗之後 toounmount...」 可能的 toooccur 錯誤訊息。

在已從其支援內建資源庫映像修改或變更的目標 VM 環境中嘗試 OS 磁碟加密時，這是最有可能的。  偏離 hello 支援映像，這可能會干擾 hello 擴充功能的能力 toounmount hello 作業系統磁碟機的範例包括：
- 不再符合支援的檔案系統和/或資料分割配置的自訂映像。
- 與應用程式，例如防毒軟體、 Docker、 SAP、 MongoDB、 或 Apache Cassandra hello OS 先前 tooencryption 中執行的自訂映像。  這些應用程式是難以 tooterminate，而且當它們保留開啟檔案控制代碼 toohello 作業系統磁碟機，hello 磁碟機不能卸載，造成失敗。
- 自訂指令碼中執行的關閉的時間相近 toohello 加密步驟可能會妨礙，而且會導致此失敗。 這可能發生資源管理員範本可定義多個擴充功能 tooexecute 同時，或自訂指令碼延伸或其他動作執行時同時 toodisk 加密。   序列化和隔離這類步驟可能解決 hello 問題。
- 當 SELinux 已停用先前 tooenabling 加密時，hello 卸載步驟會失敗。  完成加密後，即可重新啟用 SELinux。
- 當 hello OS 磁碟正在使用 LVM 配置 （雖然可以有限的 LVM 資料磁碟支援，但是 LVM OS 磁碟將不會）
- 當未符合最小記憶體需求時 (OS 磁碟加密建議為 7 GB)
- 當資料磁碟機已遞迴掛接於 /mnt/ directory 下，或彼此掛接 (例如，/mnt/data1、/mnt/data2、/data3 + /data3/data4 等等)
- 未符合其他 Linux 適用的 Azure 磁碟加密[必要條件](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)時

## <a name="unable-tooencrypt"></a>無法 tooencrypt

在某些情況下，toobe 停滯於 「 啟動 OS 磁碟加密 」 和 SSH 已停用，會顯示 hello Linux 磁碟加密。 此程序可能需要 3-16 小時 toocomplete 上內建資源庫映像之間。  如果加入多個 TB 大小的資料磁碟，hello 程序可能需要天。 hello Linux 作業系統磁碟加密順序暫時取消掛接 hello 作業系統磁碟機，並且執行整個 OS 磁碟 hello，裝載在加密狀態之前以區塊加密。   不同於 Windows 上的 Azure 磁碟加密，Linux 磁碟加密不允許同時使用 hello VM hello 加密進行中時。  hello hello VM，包括 hello 大小 hello 磁碟和標準或進階 (SSD) 儲存體是否支援 hello 儲存體帳戶的效能特性可能會大幅影響 hello 所需時間 toocomplete 加密。

toocheck 狀態 hello ProgressMessage 欄位傳回的 hello [Get AzureRmVmDiskEncryptionStatus](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus)可輪詢命令。   Hello 作業系統磁碟機已加密，hello VM 便會進入服務的狀態，與 SSH 也是已停用的 tooprevent 任何中斷 toohello 的進行中程序。  正在進行，之後數小時稍後 VMRestartPending 訊息，提示 toorestart hello VM 加密時，將報告 EncryptionInProgress hello 多數的 hello 時間。  例如：


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

一次出現提示 tooreboot hello VM，並重新啟動 hello VM，並提供 hello 重新開機，以及在 hello 目標上執行的最後步驟 toobe 2-3 分鐘之後, hello 狀態訊息會指出最後完成加密。   一旦可以使用此訊息，hello 加密作業系統磁碟機是預期的 toobe 就緒供使用，以及可用的 hello VM toobe 一次。

萬一其中未看到此順序，或開機資訊、 進度訊息或其他錯誤指示器報告 OS 加密未能 hello 中間 （例如如果您看到 「 無法 toounmount 」 本指南中所述之錯誤的 hello），此程序建議 toorestore hello VM 後 toohello 快照式或取得 tooencryption 立即先前的備份。  先前 toohello 下一次嘗試，它會建議的 toore-評估 hello VM hello 特性，並確定所有必要條件已都滿足。

## <a name="troubleshooting-azure-disk-encryption-behind-a-firewall"></a>針對防火牆後方的 Azure 磁碟加密進行疑難排解
當連線受到 hello 延伸 tooperform 防火牆、 proxy 需求，或是網路安全性群組 (nsg) 設定，hello 能力需要工作可以被中斷。   這會導致例如 「 hello VM 上無法使用擴充狀態 」 的狀態訊息和失敗 toofinish 可預期案例中。  hello 以下各節會有一些常見的防火牆問題，您可能需要調查。

### <a name="network-security-groups"></a>網路安全性群組
套用任何網路安全性群組群組設定仍然必須允許 hello 端點 toomeet hello 記載網路組態[必要條件](https://docs.microsoft.com/azure/security/azure-security-disk-encryption#prerequisites)磁碟加密。

### <a name="azure-keyvault-behind-firewall"></a>防火牆後方的 Azure Keyvault
hello VM 必須能夠 tooaccess 金鑰保存庫。 Tooguidance 上存取 tookey 錯誤由 hello 維護在防火牆之後，請參閱[金鑰保存庫](https://docs.microsoft.com/azure/key-vault/key-vault-access-behind-firewall)小組。

### <a name="linux-package-management-behind-firewall"></a>防火牆後方的 Linux 套件管理
在執行階段，適用於 Linux 的 Azure 磁碟加密依賴 hello 目標發佈的封裝管理系統需要 tooinstall 必要條件元件先前 tooenabling 加密。  如果防火牆設定導致無法 toodownload hello VM 和安裝這些元件，都必須後續失敗。    這可能會因發佈 hello 步驟 tooconfigure。  在 Red Hat 上，在需要 Proxy 時，請務必確保已正確地設定您的訂用帳戶管理員和 Yum。  請參閱[此](https://access.redhat.com/solutions/189533) Red Hat 關於本主題的技術支援文件。  

## <a name="troubleshooting-windows-server-2016-server-core"></a>針對 Windows Server 2016 Server Core 進行疑難排解

在 Windows Server 2016 Server Core 上不是預設可用的 hello bdehdcfg 元件。 Azure 磁碟加密需要此元件。

tooworkaround 這個問題，請複製 hello hello Server Core 映像的 Windows Server 2016 資料中心 VM toohello c:\windows\system32 資料夾中的下列 4 個檔案：

```
bdehdcfg.exe
bdehdcfglib.dll
bdehdcfglib.dll.mui
bdehdcfg.exe.mui
```

然後，執行下列命令的 hello:

```
bdehdcfg.exe -target default
```

這會建立 550 MB 的系統磁碟分割，然後重新開機後，您可以使用 Diskpart toocheck hello 磁碟區，並繼續進行。  

例如：

```
DISKPART> list vol

  Volume ###  Ltr  Label        Fs     Type        Size     Status     Info
  ----------  ---  -----------  -----  ----------  -------  ---------  --------
  Volume 0     C                NTFS   Partition    126 GB  Healthy    Boot
  Volume 1                      NTFS   Partition    550 MB  Healthy    System
  Volume 2     D   Temporary S  NTFS   Partition     13 GB  Healthy    Pagefile
```
## <a name="see-also"></a>另請參閱
在本文件中，您已了解 Azure 磁碟加密中一些常見的問題有關的詳細資訊及如何 tootroubleshoot。 如需此服務和其功能的相關資訊，請閱讀：

- [在 Azure 資訊安全中心套用磁碟加密](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [加密 Azure 虛擬機器](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Azure 資料靜態加密](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)

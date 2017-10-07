---
title: "aaaAzure 疑難排解 Azure 至 Azure 複寫問題和錯誤的站台復原 |Microsoft 文件"
description: "對於複寫 Azure 虛擬機器進行嚴重損壞修復時發生的錯誤和問題進行疑難排解"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/10/2017
ms.author: sujayt
ms.openlocfilehash: bca957dd0f40e6b16e68913caf522f3431c55bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-to-azure-vm-replication-issues"></a>Azure 至 Azure VM 複寫問題的疑難排解

這篇文章描述 hello 複寫和復原 Azure 虛擬機器從一個區域 tooanother 區域時，Azure Site Recovery 中常見的問題，並說明如何 tootroubleshoot 它們。 如需有關支援的組態的詳細資訊，請參閱 hello[複寫 Azure Vm 支援矩陣](site-recovery-support-matrix-azure-to-azure.md)。

## <a name="azure-resource-quota-issues-error-code-150097"></a>Azure 資源配額問題 (錯誤碼 150097)
您的訂用帳戶應啟用的 toocreate Azure Vm，您在為您的災害復原區域計劃 toouse hello 目標區域中。 此外，您的訂用帳戶應該具有足夠的配額啟用 toocreate 特定大小的 Vm。 根據預設，站台復原來挑選 hello hello 目標工作者角色 hello 來源 VM 的相同大小。 Hello 相符大小無法使用，系統會自動挑選 hello 最接近的可能大小。 如果沒有支援來源 VM 組態的相符大小，則會出現下列錯誤訊息：

**錯誤碼** | **可能的原因** | **建議**
--- | --- | ---
150097<br></br>**訊息**: hello 虛擬機器 VmName 無法啟用複寫。 | -您的訂用帳戶識別碼可能不被啟用 toocreate hello 目標區域位置中的所有 Vm。</br></br>-您的訂用帳戶 ID 可能不會啟用，或在 hello 目標區域位置沒有足夠配額 toocreate 特定 VM 大小。</br></br>-符合 hello 來源 VM NIC 計數 (2) 的適當目標 VM 大小找不到 hello 訂用帳戶 id hello 目標區域位置中。| 請連絡[Azure 計費支援](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request)訂用帳戶建立 hello tooenable VM 所需的 hello 目標位置中的 VM 大小。 啟用之後，重試 hello 操作時失敗。

### <a name="fix-hello-problem"></a>修正 hello 問題
您可以連絡[Azure 計費支援](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request)tooenable 您訂用帳戶 toocreate hello 目標位置中的必要大小的 Vm。

如果 hello 目標位置有容量條件約束，停用複寫，並啟用它 tooa 訂用帳戶具有足夠的配額 toocreate hello 所需大小的 Vm 的不同位置。

## <a name="trusted-root-certificates-error-code-151066"></a>受信任的根憑證 (錯誤碼 151066)

如果所有 hello 最受信任的根憑證不存在於 hello VM 上，將 [啟用複寫] 的工作可能會失敗。 沒有 hello 憑證，hello 驗證和授權的 Site Recovery 服務呼叫從 hello VM 會失敗。 出現 hello 的 hello 失敗 [啟用複寫] 站台復原作業的錯誤訊息：

**錯誤碼** | **可能的原因** | **建議**
--- | --- | ---
151066<br></br>**訊息**：Site Recovery 組態失敗。 | hello 所需的受信任的根憑證，用來授權和驗證不存在於 hello 機器上。 | -執行 hello Windows 作業系統的 VM，請確定該 hello 受信任的根憑證存在於 hello 電腦上。 如需資訊，請參閱[設定受信任根目錄和不允許的憑證](https://technet.microsoft.com/library/dn265983.aspx)。<br></br>-若為執行 hello Linux 作業系統的 VM，請遵循 hello 指引 hello Linux 作業系統版本的散發者所發行的受信任的根憑證。

### <a name="fix-hello-problem"></a>修正 hello 問題
**Windows**

Hello VM 上安裝所有 hello 最新 Windows 更新 hello 機器上沒有所有 hello 受信任的根憑證。 如果您在中斷連線的環境，請遵循 hello 標準 Windows update 程序在您的組織 tooget hello 的憑證。 在 hello 必要 hello VM 上的憑證沒有安全性的理由 hello 呼叫 toohello Site Recovery 服務將會失敗。

Hello Vm 上，請遵循一般 Windows update 管理 hello 或您的組織 tooget 所有最新的根憑證 hello 與 hello 更新憑證撤銷清單中的憑證更新管理程序。

tooverify 的 hello 問題已解決，請 toologin.microsoftonline.com 從瀏覽器在 VM 中。

**Linux**

請遵循您的 Linux 散發者 tooget hello 最受信任的根憑證與 hello 最新憑證撤銷清單 hello VM 上的所提供的 hello 指引。

由於 SuSE Linux 使用 symlink toomaintain 憑證清單，請遵循下列步驟：

1.  以根使用者身分登入。

2.  請執行這個命令：

      ``# cd /etc/ssl/certs``

3.  toosee hello Symantec 根 CA 憑證是否存在，或不是，執行下列命令：

      ``# ls VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

4.  如果找不到 hello 檔案，請執行下列命令：

      ``# wget https://www.symantec.com/content/dam/symantec/docs/other-resources/verisign-class-3-public-primary-certification-authority-g5-en.pem -O VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

      ``# c_rehash``

5.  -> VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem toocreate b204d74a.0 的符號連結之後，執行此命令：

      ``# ln -s  VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem b204d74a.0``

6.  如果這個命令有 hello 下列輸出，請檢查 toosee。 如果沒有，您有 toocreate 符號連結：

      ``# ls -l | grep Baltimore
      -rw-r--r-- 1 root root   1303 Apr  7  2016 Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 04:47 3ad48a91.0 -> Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 05:01 653b494a.0 -> Baltimore_CyberTrust_Root.pem``

7. 如果符號連結 653b494a.0 不存在，請使用此命令 toocreate 符號連結：

      ``# ln -s Baltimore_CyberTrust_Root.pem 653b494a.0``


## <a name="outbound-connectivity-for-site-recovery-urls-or-ip-ranges-error-code-151037-or-151072"></a>Site Recovery URL 或 IP 範圍的輸出連線能力 (錯誤碼 151037 或 151072)

Url 或 IP 範圍的傳出連線 toospecific 站台復原複寫 toowork，則需要從 hello VM。 如果您的 VM 位於防火牆或使用網路安全性 (nsg) 規則 toocontrol 輸出連線，您可能會看到其中一個錯誤訊息：

**錯誤碼** | **可能的原因** | **建議**
--- | --- | ---
151037<br></br>**訊息**： 無法 tooregister Azure Site recovery 的虛擬機器。 | -您在上 hello VM 使用 NSG toocontrol 對外存取和 hello 所需的 IP 範圍不是在對外存取的允許清單。</br></br>-您正在使用協力廠商防火牆工具，而且 hello 所需的 IP 範圍/Url 不在允許清單中。</br>| -如果您使用防火牆 proxy toocontrol 輸出網路連線 hello VM 上，確認該 hello 必要條件的 Url，或資料中心 IP 範圍是在允許清單中。 如需資訊，請參閱[防火牆 Proxy 指引](https://aka.ms/a2a-firewall-proxy-guidance)。</br></br>-如果您在 hello VM 上使用 NSG 規則 toocontrol 傳出的網路連線，請確定 hello 必要條件的資料中心 IP 範圍會在允許清單中。 如需資訊，請參閱[網路安全性群組指引](https://aka.ms/a2a-nsg-guidance)。
151072<br></br>**訊息**：Site Recovery 組態失敗。 | 連接不可以是已建立的 tooSite 復原服務端點。 | -如果您使用防火牆 proxy toocontrol 輸出網路連線 hello VM 上，確認該 hello 必要條件的 Url，或資料中心 IP 範圍是在允許清單中。 如需資訊，請參閱[防火牆 Proxy 指引](https://aka.ms/a2a-firewall-proxy-guidance)。</br></br>-如果您在 hello VM 上使用 NSG 規則 toocontrol 傳出的網路連線，請確定 hello 必要條件的資料中心 IP 範圍會在允許清單中。 如需資訊，請參閱[網路安全性群組指引](https://aka.ms/a2a-nsg-guidance)。

### <a name="fix-hello-problem"></a>修正 hello 問題
toowhitelist [hello 需要 Url](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-urls)或 hello[所需的 IP 範圍](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-ip-ranges)，hello 中的 hello 步驟[網路指引文件](site-recovery-azure-to-azure-networking-guidance.md)。

## <a name="disk-not-found-in-hello-machine-error-code-150039"></a>Hello 機器 （錯誤碼 150039） 中找不到磁碟

新的磁碟附加的 toohello VM，必須先初始化。

**錯誤碼** | **可能的原因** | **建議**
--- | --- | ---
150039<br></br>**訊息**： 邏輯單元編號 (LUN) (LUNValue) 的 Azure 資料磁碟 (DiskName) (DiskURI) 未對應的 tooa hello 具有 hello VM 內報告從對應的磁碟相同的 LUN 值。 | -新的資料磁碟附加的 toohello VM 但它未初始化。</br></br>-hello hello VM 內的資料磁碟未正確地回報 hello LUN 值在哪一個 hello 磁碟已附加的 toohello VM。| 確定 hello 資料磁碟都已初始化，然後重試 hello 作業。</br></br>對於 Windows：[連接並初始化新的磁碟](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk)。</br></br>對於 Linux：[在 Linux 中初始化新的資料磁碟](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux)。

### <a name="fix-hello-problem"></a>修正 hello 問題
確定 hello 資料磁碟已經過初始化，然後重試 hello 作業：

- 對於 Windows：[連接並初始化新的磁碟](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk)。
- 對於 Linux：[在 Linux 中初始化新的資料磁碟](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux)。

如果 hello 問題持續發生，請連絡支援。


## <a name="unable-toosee-hello-azure-vm-for-selection-in-enable-replication"></a>無法 toosee hello Azure VM 的 「 啟用複寫 」 中的選取範圍

您可能看不見您的 Azure VM，因此無法在[啟用複寫：步驟 2](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines) 中選取。 此問題可能是由於在 hello Azure VM 上剩餘的 toostale Site Recovery 設定。 在下列情況下的 hello Azure VM 上時，可以保留設定過時 hello:

- 您使用站台復原中啟用 hello Azure VM 的複寫，然後刪除 hello Site Recovery 保存庫明確停用 hello VM 上的複寫。
- 您使用站台復原中啟用 hello Azure VM 的複寫，然後刪除 hello 資源群組中包含 hello Site Recovery 保存庫，而不明確停用 hello VM 上的複寫。

### <a name="fix-hello-problem"></a>修正 hello 問題

您可以使用[移除過時 ASR 組態指令碼](https://gallery.technet.microsoft.com/Azure-Recovery-ASR-script-3a93f412)和移除 hello Azure VM 上的 hello 過時 Site Recovery 設定。 您應該會看見 hello 中的 VM[啟用複寫： 步驟 2](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines)移除 hello 設定過時之後。


## <a name="next-steps"></a>後續步驟
[複寫 Azure 虛擬機器](site-recovery-replicate-azure-to-azure.md)

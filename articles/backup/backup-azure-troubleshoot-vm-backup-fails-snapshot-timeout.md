---
title: "針對 Azure 備份失敗：無法使用客體代理程式狀態進行疑難排解 | Microsoft Docs"
description: "徵狀、 原因和解決方案的 Azure 備份失敗相關 tooerror： 無法與 hello VM 代理程式通訊"
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
keywords: "Azure 備份; VM 代理程式; 網路連線;"
ms.assetid: 4b02ffa4-c48e-45f6-8363-73d536be4639
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: genli;markgal;
ms.openlocfilehash: 724c61ba80d0a9ef91a5f8543ae72bb86968881b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-backup-failure-issues-with-agent-andor-extension"></a>針對 Azure 備份失敗進行疑難排解：與代理程式和/或擴充功能相關的問題

這篇文章會提供解決備份失敗的疑難排解步驟 toohelp 相關 tooproblems 在與 VM 代理程式和延伸模組的通訊。

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="vm-agent-unable-toocommunicate-with-azure-backup"></a>VM 代理程式無法 toocommunicate 向 Azure 備份
您可以註冊及排程 hello Azure 備份服務的 VM 之後，備份會藉由通訊以 hello VM 代理程式 tootake 時間點快照集初始化 hello 工作。 任何 hello 下列條件可能會讓 hello 快照集從觸發，而這可能會接著 tooBackup 失敗。 請遵循下列疑難排解 hello 指定順序中的步驟，然後重試您的作業。
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>原因 1: [hello VM 有沒有網際網路存取](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>原因 2: [hello 代理程式安裝在 hello VM，但沒有回應 （適用於 Windows Vm)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>原因 3: [hello hello VM 中安裝的代理程式為最新 （適用於 Linux Vm)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>原因 4: [hello 快照集的狀態無法擷取或無法取得快照](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>原因 5: [hello 備用分機號碼失敗 tooupdate 或載入](#the-backup-extension-fails-to-update-or-load)

## <a name="snapshot-operation-failed-due-toono-network-connectivity-on-hello-virtual-machine"></a>快照集作業失敗，因為 toono hello 虛擬機器上的網路連線
您可以註冊及排程 hello Azure 備份服務的 VM 之後，備份會藉由通訊與 hello VM 備用分機號碼 tootake 的時間點快照集初始化 hello 工作。 任何 hello 下列條件可能會讓 hello 快照集從觸發，而這可能會接著 tooBackup 失敗。 請遵循下列疑難排解 hello 指定順序中的步驟，然後重試您的作業。
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>原因 1: [hello VM 有沒有網際網路存取](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>原因 2: [hello 快照集的狀態無法擷取或無法取得快照](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-3-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>原因 3: [hello 備用分機號碼失敗 tooupdate 或載入](#the-backup-extension-fails-to-update-or-load)

## <a name="vmsnapshot-extension-operation-failed"></a>VMSnapshot 擴充作業失敗

您可以註冊及排程 hello Azure 備份服務的 VM 之後，備份會藉由通訊與 hello VM 備用分機號碼 tootake 的時間點快照集初始化 hello 工作。 任何 hello 下列條件可能會讓 hello 快照集從觸發，而這可能會接著 tooBackup 失敗。 請遵循下列疑難排解 hello 指定順序中的步驟，然後重試您的作業。
##### <a name="cause-1-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>原因 1: [hello 快照集的狀態無法擷取或無法取得快照](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-2-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>原因 2: [hello 備用分機號碼失敗 tooupdate 或載入](#the-backup-extension-fails-to-update-or-load)
##### <a name="cause-3-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>原因 3: [hello VM 有沒有網際網路存取](#the-vm-has-no-internet-access)
##### <a name="cause-4-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>原因 4: [hello 代理程式安裝在 hello VM，但沒有回應 （適用於 Windows Vm)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-5-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>原因 5: [hello hello VM 中安裝的代理程式為最新 （適用於 Linux Vm)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)

## <a name="unable-tooperform-hello-operation-as-hello-vm-agent-is-not-responsive"></a>無法 tooperform hello 操作，因為 hello VM 代理程式沒有回應

您可以註冊及排程 hello Azure 備份服務的 VM 之後，備份會藉由通訊與 hello VM 備用分機號碼 tootake 的時間點快照集初始化 hello 工作。 任何 hello 下列條件可能會讓 hello 快照集從觸發，而這可能會接著 tooBackup 失敗。 請遵循下列疑難排解 hello 指定順序中的步驟，然後重試您的作業。
##### <a name="cause-1-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>原因 1: [hello 代理程式安裝在 hello VM，但沒有回應 （適用於 Windows Vm)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-2-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>原因 2: [hello hello VM 中安裝的代理程式為最新 （適用於 Linux Vm)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-3-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>原因 3: [hello VM 有沒有網際網路存取](#the-vm-has-no-internet-access)

## <a name="backup-failed-with-an-internal-error---please-retry-hello-operation-in-a-few-minutes"></a>備份失敗，發生內部錯誤-請重試幾分鐘的時間中的 hello 作業

您可以註冊及排程 hello Azure 備份服務的 VM 之後，備份會藉由通訊與 hello VM 備用分機號碼 tootake 的時間點快照集初始化 hello 工作。 任何 hello 下列條件可能會讓 hello 快照集從觸發，而這可能會接著 tooBackup 失敗。 請遵循下列疑難排解 hello 指定順序中的步驟，然後重試您的作業。
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>原因 1: [hello VM 有沒有網際網路存取](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-agent-installed-in-hello-vm-but-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>原因 2: [hello （適用於 Windows Vm)，但沒有回應 hello VM 中安裝的代理程式](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>原因 3: [hello hello VM 中安裝的代理程式為最新 （適用於 Linux Vm)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>原因 4: [hello 快照集的狀態無法擷取或無法取得快照](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>原因 5: [hello 備用分機號碼失敗 tooupdate 或載入](#the-backup-extension-fails-to-update-or-load)


## <a name="causes-and-solutions"></a>原因和解決方案

### <a name="hello-vm-has-no-internet-access"></a>hello VM 有沒有網際網路存取
每個 hello 部署需求，hello VM 已無法存取網際網路，或防止存取 toohello Azure 基礎結構中適當的限制。

toofunction hello 備份延伸模組，需要正確地連接 toohello Azure 公用 IP 位址。 hello 延伸模組會將命令 tooan Azure 儲存體端點 (HTTP URL) toomanage hello 的快照集 hello VM。 如果公用網際網路，最後備份失敗的任何存取 toohello hello 延伸模組。

####  <a name="solution"></a>方案
此處所列的 hello 方法的其中一個 try tooresolve hello 問題。
##### <a name="allow-access-toohello-azure-datacenter-ip-ranges"></a>允許存取 toohello Azure 資料中心 IP 範圍

1. 取得 hello[的 Azure 資料中心 Ip 清單](https://www.microsoft.com/download/details.aspx?id=41653)tooallow 的存取權。
2. 藉由執行 hello 解除封鎖 hello Ip**新增 NetRoute** hello 提升權限的 PowerShell 視窗中的 Azure VM 中的 cmdlet。 以系統管理員身分執行 hello 指令程式。
3. tooallow 存取 toohello Ip 時，會將規則 toohello 網路安全性群組，如果有的話。

##### <a name="create-a-path-for-http-traffic-tooflow"></a>建立 HTTP 流量 tooflow 的路徑

1. 如果您的網路限制已備妥 （例如，網路安全性群組），將部署 HTTP proxy 伺服器 tooroute hello 流量。
2. hello HTTP proxy 伺服器，從 tooallow 存取 toohello 網際網路加入規則 toohello 網路安全性群組，如果有的話。

toolearn tooset VM 備份的 HTTP proxy 的請參閱[準備 Azure 虛擬機器註冊您的環境 tooback](backup-azure-vms-prepare.md#using-an-http-proxy-for-vm-backups)。

如果您使用受管理的磁碟，您可能需要其他通訊埠 (8443) 開啟 hello 防火牆上。

### <a name="hello-agent-installed-in-hello-vm-but-unresponsive-for-windows-vms"></a>hello （適用於 Windows Vm)，但沒有回應 hello VM 中安裝的代理程式

#### <a name="solution"></a>方案
hello VM 代理程式可能已損毀或 hello 服務可能已停止。 重新安裝 hello VM 代理程式可取得 hello 最新版本，然後重新啟動 hello 通訊。

1. 請確認服務 (services.msc) 中執行的 Windows 客體代理程式服務是否 hello 虛擬機器。 請嘗試重新啟動 hello Windows 客體代理程式服務，並起始 hello 備份<br>
2. 如果在服務中看不到，請在 [程式和功能] 中確認您是否已安裝 Windows 客體代理程式服務。
4. 如果您是在 程式和功能解除安裝無法 tooview hello Windows 客體代理程式。
5. 下載並安裝 hello[最新版本的代理程式 MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。 您需要系統管理員權限 toocomplete hello 安裝。
6. 您應該會無法 tooview 服務中的 Windows 客體代理程式服務
7. 嘗試執行上-要求/臨機操作備份 hello 入口網站中，按一下 [立即備份]。

另請確認您的虛擬機器具有 **[hello 系統中安裝.NET 4.5](https://docs.microsoft.com/en-us/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed)**。 它是 hello VM 代理程式 toocommunicate 與 hello 服務所需

### <a name="hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vms"></a>hello hello VM 中安裝的代理程式為最新 （適用於 Linux Vm)

#### <a name="solution"></a>方案
針對 Linux VM，與代理程式或擴充功能相關的多數失敗是由於會影響過時 VM 代理程式的問題所造成。 tootroubleshoot 這個問題，請遵循下列一般指導方針：

1. 請依照指示 hello[更新 hello Linux VM 代理程式](../virtual-machines/linux/update-agent.md)。

 >[!NOTE]
 >我們*強烈建議*您更新 hello 代理程式只能透過發佈儲存機制。 我們不建議直接從 GitHub 下載 hello 代理程式程式碼，並更新它。 如果 hello 最新的代理程式無法使用您的散發，請連絡散發支援的指示 tooinstall 它。 hello 最近代理程式，請移 toohello toocheck [Windows Azure Linux 代理程式](https://github.com/Azure/WALinuxAgent/releases)hello GitHub 儲存機制中的頁面。

2. 請確定該 hello Azure 代理程式正在執行 hello VM 上執行下列命令的 hello:`ps -e`

 如果未執行 hello 程序，使用它重新啟動 hello 下列命令：

 * 針對 Ubuntu：`service walinuxagent start`
 * 針對其他散發套件︰`service waagent start`

3. [Hello 自動重新啟動代理程式設定](https://github.com/Azure/WALinuxAgent/wiki/Known-Issues#mitigate_agent_crash)。
4. 執行新的測試備份。 如果 hello 失敗持續發生，請收集 hello hello 客戶的 VM 中的下列記錄檔：

   * /var/lib/waagent/*.xml
   * /var/log/waagent.log
   * /var/log/azure/*

如果我們需要 waagent 的詳細資訊記錄，請遵循下列步驟：

1. 在 hello /etc/waagent.conf 檔案中，找出 hello 下列行：**啟用詳細資訊記錄 (y | n)**
2. 變更 hello **Logs.Verbose**值 *n* 太*y*。
3. 儲存 hello 變更，然後遵循本節中的 hello 上一個步驟，以重新啟動 waagent。

### <a name="hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>無法擷取 hello 快照集的狀態，或無法取得快照
hello VM 備份依賴發行的快照集命令 toohello 基礎儲存體帳戶。 備份可能會失敗，因為它有沒有存取 toohello 儲存體帳戶或延遲 hello hello 快照集工作執行。

#### <a name="solution"></a>方案
hello 下列條件可能會導致快照集工作失敗：

| 原因 | 方案 |
| --- | --- |
| hello VM 已設定的 SQL Server 備份。 | 根據預設，hello VM 備份會在 Windows Vm 上，執行 VSS 完整備份。 在執行以 SQL Server 為基礎的伺服器並設定了 SQL Server 備份的 VM 上，可能會發生快照延遲執行。<br><br>如果您因為快照集問題發生備份失敗，設定下列登錄機碼的 hello:<br><br>**[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT] "USEVSSCOPYBACKUP"="TRUE"** |
| 因為 hello VM 關閉在 RDP，hello VM 狀態將無法正確地報告。 | 如果您關閉 hello VM 中遠端桌面通訊協定 (RDP) 時，請檢查 hello 入口 toodetermine hello VM 狀態是否正確。 如果不正確，請關閉 hello 入口網站中的 hello VM 使用 hello**關機**hello VM 儀表板上的選項。 |
| 從相同的雲端服務的 hello 許多 Vm 在 hello 向上設定 tooback 相同的時間。 | 它是最佳的作法 toospread 出 hello 備份排程的 Vm 從 hello 相同雲端服務。 |
| hello VM 正在以高 CPU 或記憶體使用量。 | 如果 hello VM 執行 CPU 使用量高 （超過 90%) 或高記憶體使用量，hello 快照集工作排入佇列，以及延遲，而且它最後會逾時。在此情況下，請嘗試隨選備份。 |
| hello VM 無法從 DHCP 取得 hello 網狀架構主機位址。 | Hello IaaS VM 備份 toowork hello 客體內，就必須啟用 DHCP。  如果 hello VM 無法收到 hello 網狀架構主機位址 DHCP 回應 245，無法下載或執行任何擴充功能。 如果您需要靜態私人 ip 位址，您應該透過 hello 平台來進行設定。 hello 內啟用 VM 應該保持的 hello 的 DHCP 選項。 如需詳細資訊，請參閱[設定靜態內部私人 IP 位址](../virtual-network/virtual-networks-reserved-private-ip.md)。 |

### <a name="hello-backup-extension-fails-tooupdate-or-load"></a>hello 備用分機號碼失敗 tooupdate 或載入
如果無法載入擴充功能，備份就會因為無法取得快照而失敗。

#### <a name="solution"></a>方案

**取得 Windows 客體：**確認 hello iaasvmprovider 服務已啟用並啟動類型為*自動*。 如果 hello 服務未以這種方式設定，啟用 toodetermine 是否 hello 下一個備份都會成功。

**Linux 客體的：**確認 hello 最新版本的 Linux （備份所使用的 hello 副檔名） 的 VMSnapshot 是 1.0.91.0。<br>


如果 tooupdate 或負載，還是無法 hello 備用分機號碼，您可以強制 hello VMSnapshot 延伸 toobe 解除安裝 hello 延伸模組重新載入。 hello 下一次備份的嘗試將重新載入 hello 延伸模組。

toouninstall hello 擴充功能，請勿遵循 hello:

1. 移 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 找出 hello VM 時，備份的相關問題。
3. 按一下 [設定] 。
4. 按一下 [擴充功能]。
5. 按一下 [Vmsnapshot 擴充功能]。
6. 按一下 [解除安裝]。

此程序會導致 hello 延伸 toobe hello 下一個備份期間重新安裝。


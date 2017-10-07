---
title: "aaaMonitor 及疑難排解虛擬機器和實體伺服器的保護 |Microsoft 文件"
description: "Azure Site Recovery 會協調 hello 複寫、 容錯移轉和復原的虛擬機器位於內部部署伺服器 tooAzure 或次要資料中心。 使用此發行項 toomonitor 和疑難排解 Virtual Machine Manager 或 HYPER-V 站台保護。"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 0fc8e368-0c0e-4bb1-9d50-cffd5ad0853f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: d790375db5f30e98f009c8d8272558188c51934c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-troubleshoot-protection-for-virtual-machines-and-physical-servers"></a>監視和疑難排解虛擬機器與實體伺服器的保護
此監視和疑難排解指南可協助您了解如何 tootrack 複寫健全狀況及疑難排解技術的 Azure Site Recovery。

## <a name="understand-hello-components"></a>了解 hello 元件
### <a name="vmware-virtual-machine-or-physical-server-site-deployment-for-replication-between-on-premises-and-azure"></a>用於在內部部署和 Azure 之間複寫的 VMware 虛擬機器或實體網站部署
在內部部署 VMware 虛擬機器或實體伺服器和 Azure 之間的資料庫復原 tooset，您需要 tooset hello 組態伺服器、 主要目標伺服器和虛擬機器或伺服器上的處理序伺服器元件。 當您啟用 hello 來源伺服器的保護時，Azure Site Recovery 會安裝 Microsoft Azure 應用程式服務的 hello 行動應用程式功能。 在內部部署中斷之後及 hello 來源伺服器容錯移轉 tooAzure，客戶必須 tooset 在 Azure 中的處理序伺服器和內部部署 toorebuild hello 在內部部署的來源伺服器上的主要目標伺服器。

![VMware/Physical site deployment for replication between on-premises and Azure](media/site-recovery-monitoring-and-troubleshooting/image18.png)

### <a name="virtual-machine-manager-site-deployment-for-replication-between-on-premises-sites"></a>用於在內部部署網站之間複寫的 Virtual Machine Manager 網站部署
兩個資料庫復原 tooset 內部部署位置，您需要 toodownload hello Azure Site Recovery 提供者，並將它安裝在 hello Virtual Machine Manager 伺服器。 hello 提供者需要網際網路連線 tooensure 觸發從 hello Azure 入口網站的所有 hello 作業都取得翻譯的 tooon 內部作業。

![用於在內部部署網站之間複寫的 Virtual Machine Manager 網站部署](media/site-recovery-monitoring-and-troubleshooting/image1.png)

### <a name="virtual-machine-manager-site-deployment-for-replication-between-on-premises-locations-and-azure"></a>用於在內部部署位置和 Azure 之間複寫的 Virtual Machine Manager 網站部署
當您設定在內部部署位置與 Azure 之間的資料庫復原時，您需要 toodownload hello Azure Site Recovery 提供者，並將它安裝在 hello Virtual Machine Manager 伺服器。 您也需要 tooinstall hello Azure 復原服務代理程式，這需要 toobe 安裝在每一部 HYPER-V 主機上。 [深入了解](site-recovery-hyper-v-azure-architecture.md)以取得詳細資訊。

![用於在內部部署位置和 Azure 之間複寫的 Virtual Machine Manager 網站部署](media/site-recovery-monitoring-and-troubleshooting/image2.png)

### <a name="hyper-v-site-deployment-for-replication-between-on-premises-locations-and-azure"></a>用於在內部部署位置和 Azure 之間複寫的 Hyper-V 網站部署
此程序是類似的 tooVirtual Machine Manager 部署。 hello 只差別 hello Azure Site Recovery provider 和 Azure 復原服務代理程式取得本身 hello HYPER-V 主機上安裝。 [深入了解](site-recovery-hyper-v-azure-architecture.md)。 。

## <a name="monitor-configuration-protection-and-recovery-operations"></a>監視組態、保護和復原作業
Azure Site Recovery 中的每個作業會稽核和追蹤在 hello**作業** 索引標籤。如需任何設定、 保護或復原錯誤，請移 toohello**作業**索引標籤上，尋找失敗。

![hello 工作 索引標籤中的 hello 失敗篩選](media/site-recovery-monitoring-and-troubleshooting/image3.png)

如果您發現下 hello 失敗**作業**索引標籤上，按一下 hello 作業，然後按一下**錯誤詳細資料**該工作。

![hello 錯誤詳細資料 按鈕](media/site-recovery-monitoring-and-troubleshooting/image4.png)

hello 錯誤詳細資料可協助您識別可能的原因及 hello 問題的建議事項。

![Dialog box that shows error details for a specific job](media/site-recovery-monitoring-and-troubleshooting/image5.png)

在 hello 前一個範例中，另一個作業正在進行中似乎 toobe 造成 hello 保護組態 toofail。 解決依據 hello 建議的 hello 問題，然後按一下 **RESART** tooinitiate hello 操作。

![hello hello 工作 索引標籤中重新啟動 按鈕](media/site-recovery-monitoring-and-troubleshooting/image6.png)

hello**重新啟動**選項不適用於所有作業。 如果作業沒有 hello**重新啟動**選項，請返回 toohello 物件並取消復原 hello 操作。 您可以取消正在進行中的任何作業使用 hello**取消** 按鈕。

![hello 取消按鈕](media/site-recovery-monitoring-and-troubleshooting/image7.png)

## <a name="monitor-replication-health-for-virtual-machines"></a>監視虛擬機器的複寫健康情況
您可以在每個受保護的 hello 實體使用 hello Azure 入口網站 tooremotely 監視 Azure Site Recovery 提供者。 按一下 受保護項目，然後按一下VMM 雲端 或 保護群組。 hello **VMM 雲端** 索引標籤只適用於以 Virtual Machine Manager 上的部署。 其他情況下，受保護的 hello 實體受到 hello**保護群組** 索引標籤。

![hello VMM 雲端和保護群組選項](media/site-recovery-monitoring-and-troubleshooting/image8.png)

您可以按一下 受保護的實體下 hello 個別雲端或保護群組 toosee hello 底部窗格中會顯示所有可用的作業。

![Available options for a selected protected entity](media/site-recovery-monitoring-and-troubleshooting/image9.png)

在 hello 上一個螢幕擷取畫面所示，hello 虛擬機器健全狀況是**重大**。 您可以按一下 hello**錯誤詳細資料**hello 底部 toosee hello 錯誤上的按鈕。 根據 hello**可能的原因**和**建議**，解決 hello 問題。

![hello 錯誤詳細資料 按鈕](media/site-recovery-monitoring-and-troubleshooting/image10.png)

![錯誤和 hello 錯誤詳細資料 對話方塊中的建議](media/site-recovery-monitoring-and-troubleshooting/image11.png)

> [!NOTE]
> 如果任何使用中的作業正在進行中或失敗，請移 toohello**作業**以提及先前 tooview hello 的錯誤特定工作的方式檢視。
>
>

## <a name="troubleshoot-on-premises-hyper-v-issues"></a>疑難排解內部部署 Hyper-V 問題
連接 toohello 在內部部署 HYPER-V manager 主控台中，選取 hello 虛擬機器，並查看 hello 複寫健全狀況。

![Hello HYPER-V manager 主控台中的選項 tooview 複寫健全狀況](media/site-recovery-monitoring-and-troubleshooting/image12.png)

在此案例中，[複寫健康情況] 是 [嚴重]。 Hello 虛擬機器，以滑鼠右鍵按一下，然後按一下**複寫** > **檢視複寫健康情況**toosee hello 詳細資料。

![Replication health for a specific virtual machine](media/site-recovery-monitoring-and-troubleshooting/image13.png)

如果暫停 hello 虛擬機器的複寫，hello 虛擬機器，以滑鼠右鍵按一下，然後按一下**複寫** > **繼續複寫**。

![選項 tooresume hello HYPER-V manager 主控台中，複寫](media/site-recovery-monitoring-and-troubleshooting/image19.png)

如果虛擬機器移轉新增的 HYPER-V 主機內 hello 叢集或獨立電腦，而且已透過 Azure Site Recovery 設定 hello HYPER-V 主機，不會受到影響的 hello 虛擬機器複寫。 請確定該 hello 新的 HYPER-V 主機符合先決條件 hello 和已使用 Azure Site Recovery。

### <a name="event-log"></a>事件記錄檔
| 事件來源 | 詳細資料 |
| --- |:--- |
| **Applications and Service Logs/Microsoft/VirtualMachineManager/Server/Admin** (Virtual Machine Manager 伺服器) |提供許多不同的虛擬機器管理員問題的有用記錄 tootroubleshoot。 |
| **Applications and Service Logs/MicrosoftAzureRecoveryServices/Replication** (Hyper-V 主機) |提供有用的記錄 tootroubleshoot 許多 Microsoft Azure Recovery Services Agent 問題。 <br/> ![Location of Replication event source for Hyper-V host](media/site-recovery-monitoring-and-troubleshooting/eventviewer03.png) |
| **Applications and Service Logs/Microsoft/Azure Site Recovery/Provider/Operational** (Hyper-V 主機) |提供有用的記錄 tootroubleshoot 許多 Microsoft Azure Site Recovery 服務問題。 <br/> ![Location of Operational event source for Hyper-V host](media/site-recovery-monitoring-and-troubleshooting/eventviewer02.png) |
| **Applications and Service Logs/Microsoft/Windows/Hyper-V-VMMS/Admin** (Hyper-V 主機) |提供有用的記錄 tootroubleshoot 許多 HYPER-V 虛擬機器管理問題。 <br/> ![Location of Virtual Machine Manager event source for Hyper-V host](media/site-recovery-monitoring-and-troubleshooting/eventviewer01.png) |

### <a name="hyper-v-replication-logging-options"></a>Hyper-V 複寫記錄選項
有關 tooHyper HYPER-V 複寫的所有事件都會都記錄在 hello Hyper-v-V-VMMS\\系統管理記錄檔位於 Applications and Services Logs\\Microsoft\\Windows。 此外，您可以啟用 hello HYPER-V 虛擬機器管理服務的分析記錄檔。 此記錄 tooenable，首先請 hello 分析和偵錯記錄在 hello 事件檢視器中檢視。 開啟 事件檢視器，然後按一下檢視 > 顯示分析與偵錯記錄檔。

![hello 顯示分析與偵錯記錄檔選項](media/site-recovery-monitoring-and-troubleshooting/image14.png)

在 **Hyper-V-VMMS** 底下可看到 [分析] 記錄檔。

![在 hello 事件檢視器樹狀目錄中的 hello 分析記錄](media/site-recovery-monitoring-and-troubleshooting/image15.png)

在 hello**動作** 窗格中，按一下 **啟用記錄**。 啟用之後，它會在 [效能監視器] 中顯示為 [資料收集器集合工具] 底下的 [事件追蹤工作階段]。

![Hello 效能監視器 」 樹狀目錄中的事件追蹤工作階段](media/site-recovery-monitoring-and-troubleshooting/image16.png)

tooview hello 所收集的資訊，請先停止 停用 hello 記錄檔的 hello 追蹤工作階段。 儲存 hello 記錄和事件檢視器中再次開啟或使用其他工具 tooconvert 它所需。

## <a name="reach-out-for-microsoft-support"></a>連絡 Microsoft 支援
### <a name="log-collection"></a>記錄檔集合
Virtual Machine Manager 的站台保護，請參閱太[使用支援診斷平台 (SDP) 工具的 Azure Site Recovery 記錄檔收集](http://social.technet.microsoft.com/wiki/contents/articles/28198.asr-data-collection-and-analysis-using-the-vmm-support-diagnostics-platform-sdp-tool.aspx)toocollect hello 所需的記錄檔。

如需 HYPER-V 站台保護，下載[工具](https://dcupload.microsoft.com/tools/win7files/DIAG_ASRHyperV_global.DiagCab)和執行 hello HYPER-V 主機 toocollect hello 記錄檔。

如需 VMware/實體伺服器案例中，請參閱太[VMware 與實體站台保護 Azure 站台復原記錄檔收集](http://social.technet.microsoft.com/wiki/contents/articles/30677.azure-site-recovery-log-collection-for-vmware-and-physical-site-protection.aspx)toocollect hello 所需的記錄檔。

hello 工具會收集 %localappdata%\elevateddiagnostics 下隨機命名子資料夾中的本機 hello 記錄檔。

![從 Hyper-V 網站保護顯示的範例步驟。](media/site-recovery-monitoring-and-troubleshooting/animate01.gif)

### <a name="open-a-support-ticket"></a>開啟支援票證
Azure Site Recovery 的支援票證 tooraise 連接 tooAzure 支援使用 URL 在<http://aka.ms/getazuresupport>。

## <a name="kb-articles"></a>知識庫文章
* [Toopreserve hello 磁碟機代號受保護的虛擬機器容錯移轉，或是移轉 tooAzure 方式](http://support.microsoft.com/kb/3031135)
* [如何 toomanage 內部 tooAzure 保護網路頻寬使用量](https://support.microsoft.com/kb/3056159)
* [Azure Site Recovery:"hello 叢集資源不在 「 錯誤時嘗試 tooenable 虛擬機器的保護](http://support.microsoft.com/kb/3010979)
* [了解及疑難排解 Hyper-V 複寫指南](http://social.technet.microsoft.com/wiki/contents/articles/21948.hyper-v-replica-troubleshooting-guide.aspx)

## <a name="common-azure-site-recovery-errors-and-their-resolutions"></a>Azure Site Recovery 的常見錯誤和其解決方式
以下是常見的錯誤及其解決方案。 每個錯誤都載明於個別的 wiki 頁面中。

### <a name="general"></a>一般
* <span style="color:green;">NEW</span> [作業失敗，發生錯誤「作業正在進行中。」錯誤 505、514、532。](http://social.technet.microsoft.com/wiki/contents/articles/32190.azure-site-recovery-jobs-failing-with-error-an-operation-is-in-progress-error-505-514-532.aspx)
* <span style="color:green;">新</span>[工作失敗，錯誤"伺服器未連接的 toohello 網際網路 」。錯誤 25018。](http://social.technet.microsoft.com/wiki/contents/articles/32192.azure-site-recovery-jobs-failing-with-error-server-isn-t-connected-to-the-internet-error-25018.aspx)

### <a name="setup"></a>設定
* [hello Virtual Machine Manager 伺服器無法註冊到期 tooan 內部錯誤。請如需 hello 錯誤的詳細資訊，參閱 toohello hello Site Recovery 入口網站的 jobs 檢視。執行安裝程式再次 tooregister hello 伺服器。](http://social.technet.microsoft.com/wiki/contents/articles/25570.the-vmm-server-cannot-be-registered-due-to-an-internal-error-please-refer-to-the-jobs-view-in-the-site-recovery-portal-for-more-details-on-the-error-run-setup-again-to-register-the-server.aspx)
* [連接不可以是已建立的 toohello HYPER-V 復原管理員保存庫。確認 hello proxy 設定，或稍後再試。](http://social.technet.microsoft.com/wiki/contents/articles/25571.a-connection-cant-be-established-to-the-hyper-v-recovery-manager-vault-verify-the-proxy-settings-or-try-again-later.aspx)

### <a name="configuration"></a>組態
* [無法 toocreate 保護群組： 擷取伺服器 hello 清單時發生錯誤。](http://blogs.technet.com/b/somaning/archive/2015/08/12/unable-to-create-the-protection-group-in-azure-site-recovery-portal.aspx)
* [HYPER-V 主機叢集包含至少一個靜態網路介面卡，或沒有已連線的介面卡設定的 toouse DHCP。](http://social.technet.microsoft.com/wiki/contents/articles/25498.hyper-v-host-cluster-contains-at-least-one-static-network-adapter-or-no-connected-adapters-are-configured-to-use-dhcp.aspx)
* [Virtual Machine Manager 沒有權限 toocomplete 動作。](http://social.technet.microsoft.com/wiki/contents/articles/31110.vmm-does-not-have-permissions-to-complete-an-action.aspx)
* [無法選取 hello 設定保護時的 hello 訂用帳戶內的儲存體帳戶。](http://social.technet.microsoft.com/wiki/contents/articles/32027.can-t-select-the-storage-account-within-the-subscription-while-configuring-protection.aspx)

### <a name="protection"></a>保護
* <span style="color:green;">新</span>[發生失敗，錯誤"hello 虛擬機器無法設定保護 」 的啟用保護。錯誤 60007、40003。](http://social.technet.microsoft.com/wiki/contents/articles/32194.azure-site-recovery-enable-protection-failing-with-error-protection-couldn-t-be-configured-for-the-virtual-machine-error-60007-40003.aspx)
* <span style="color:green;">新</span>[啟用保護失敗，錯誤"hello 虛擬機器無法啟用保護 」。錯誤 70094。](http://social.technet.microsoft.com/wiki/contents/articles/32195.azure-site-recovery-enable-protection-failing-with-error-protection-couldn-t-be-enabled-for-the-virtual-machine-error-70094.aspx)
* <span style="color:green;">新</span>[即時移轉錯誤 23848-hello 虛擬機器即將使用類型 Live 移動 toobe。這可能會破壞 hello 虛擬機器的 hello 復原保護狀態。](http://social.technet.microsoft.com/wiki/contents/articles/32021.live-migration-error-23848-the-virtual-machine-is-going-to-be-moved-using-type-live-this-could-break-the-recovery-protection-status-of-the-virtual-machine.aspx)
* [啟用保護失敗，因為主機電腦上未安裝代理程式。](http://social.technet.microsoft.com/wiki/contents/articles/31105.enable-protection-failed-since-agent-not-installed-on-host-machine.aspx)
* [無法找到 hello 複本虛擬機器適合的主機-由於 toolow 計算資源。](http://social.technet.microsoft.com/wiki/contents/articles/25501.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-low-compute-resources.aspx)
* [無法找到 hello 複本虛擬機器適合的主機-由於 toono 連接的邏輯網路。](http://social.technet.microsoft.com/wiki/contents/articles/25502.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-no-logical-network-attached.aspx)
* [無法連線 toohello 複本主機電腦-無法建立連線。](http://social.technet.microsoft.com/wiki/contents/articles/31106.cannot-connect-to-the-replica-host-machine-connection-could-not-be-established.aspx)

### <a name="recovery"></a>復原
* Virtual Machine Manager 無法完成 hello 主機操作：
  * [容錯移轉虛擬機器的 toohello 選取復原點： 一般拒絕存取錯誤。](http://social.technet.microsoft.com/wiki/contents/articles/25504.fail-over-to-the-selected-recovery-point-for-virtual-machine-general-access-denied-error.aspx)
  * [HYPER-V 失敗的 toofail toohello 透過選取虛擬機器的復原點： 作業已中止。請嘗試較新的復原點。(0x80004004)。](http://social.technet.microsoft.com/wiki/contents/articles/25503.hyper-v-failed-to-fail-over-to-the-selected-recovery-point-for-virtual-machine-operation-aborted-try-a-more-recent-recovery-point-0x80004004.aspx)
  * 與 hello 伺服器的連線無法建立 (0x00002EFD)。
    * [HYPER-V 失敗 tooenable 反轉複寫虛擬機器。](http://social.technet.microsoft.com/wiki/contents/articles/25505.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-reverse-replication-for-virtual-machine.aspx)
    * [虛擬機器的虛擬機器的 HYPER-V 失敗的 tooenable 複寫。](http://social.technet.microsoft.com/wiki/contents/articles/25506.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-replication-for-virtual-machine-virtual-machine.aspx)
  * [無法認可虛擬機器的容錯移轉。](http://social.technet.microsoft.com/wiki/contents/articles/25508.could-not-commit-failover-for-virtual-machine.aspx)
* [hello 復原方案包含不是供規劃的容錯移轉的虛擬機器。](http://social.technet.microsoft.com/wiki/contents/articles/25509.the-recovery-plan-contains-virtual-machines-which-are-not-ready-for-planned-failover.aspx)
* [hello 虛擬機器未準備好進行規劃的容錯移轉。](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)
* [虛擬機器並未執行，而且未關閉電源。](http://social.technet.microsoft.com/wiki/contents/articles/25510.virtual-machine-is-not-running-and-is-not-powered-off.aspx)
* [虛擬機器上發生頻外作業且認可容錯移轉失敗。](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)
* 測試容錯移轉
  * [無法起始容錯移轉，因為正在進行測試容錯移轉。](http://social.technet.microsoft.com/wiki/contents/articles/31111.failover-could-not-be-initiated-since-test-failover-is-in-progress.aspx)
* <span style="color:green;">新</span>容錯移轉逾時 'PreFailoverWorkflow task WaitForScriptExecutionTaskTimeout' 因為 toohello 上 hello 與 hello 虛擬機器或 hello 子網路 toowhich hello 機器的網路安全性群組相關聯的組態設定屬於。 請參閱太['PreFailoverWorkflow task WaitForScriptExecutionTaskTimeout'](https://aka.ms/troubleshoot-nsg-issue-azure-site-recovery)如需詳細資訊。

### <a name="configuration-server-process-server-master-target"></a>組態伺服器、處理伺服器、主要目標
* [hello ESXi 主機的 hello PS/CS 裝載為 VM 會失敗，紫色死亡的螢幕。](http://social.technet.microsoft.com/wiki/contents/articles/31107.vmware-esxi-host-experiences-a-purple-screen-of-death.aspx)

### <a name="remote-desktop-troubleshooting-after-failover"></a>容錯移轉之後的遠端桌面疑難排解
* 許多客戶有面臨問題 tooconnect toohello 容錯移轉 Azure 中虛擬機器。 [疑難排解文件 tooRDP hello 虛擬機器使用 hello](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx)。

#### <a name="adding-a-public-ip-on-a-resource-manager-virtual-machine"></a>將公用 IP 新增到資源管理員虛擬機器上
如果 hello**連接**hello 入口網站中的按鈕會呈暗灰色，並且您不是透過 Express Route 或站對站 VPN 連線的連線的 tooAzure，您需要 toocreate 再指派虛擬機器的公用 IP 位址，才能使用遠端桌面/共用殼層。 然後，您可以加入公用 IP hello hello 虛擬機器網路介面上。  

![新增公用 IP hello 網路介面上容錯移轉虛擬機器](media/site-recovery-monitoring-and-troubleshooting/createpublicip.gif)

---
title: "在站台復原 aaaTest 容錯移轉 tooAzure |Microsoft 文件"
description: "了解如何從內部部署 tooAzure 執行測試容錯移轉"
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: fa0a93f409cc9f2c2c06c2d91c65971dc90c507f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="test--failover-tooazure-in-site-recovery"></a>在站台復原中測試容錯移轉 tooAzure



本文提供資訊，以使用 Azure 做為 hello 復原站台的站台復原所保護的指示執行測試容錯移轉或虛擬機器和實體伺服器的 DR 訓練。

將任何註解或問題張貼在本文中，或在 hello hello 下方[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

測試容錯移轉已執行 toovalidate 複寫策略，或執行災害復原訓練，沒有任何資料遺失或停機時間。 Hello 進行中的複寫或實際執行環境上測試容錯移轉不會有任何影響。 測試容錯移轉可在虛擬機器或[復原計劃](site-recovery-create-recovery-plans.md)上執行。 當觸發測試容錯移轉，您會需要 toospecify hello 網路 toowhich 測試虛擬機器會連接到。 一旦觸發測試容錯移轉時，您可以追蹤進度 hello**作業**頁面。  


## <a name="supported-scenarios"></a>支援的案例
除了支援所有的部署案例中測試容錯移轉[舊版 VMware 站台 tooAzure](site-recovery-vmware-to-azure-classic-legacy.md)。 虛擬機器已移轉 tooAzure 時，也不是支援測試容錯移轉。  


## <a name="run-a-test-failover"></a>執行測試容錯移轉
此程序描述如何 toorun 測試容錯移轉的復原計劃。 或者您也可以使用 hello 適當的選項，在其上執行測試容錯移轉的一部電腦。

![Test Failover](./media/site-recovery-test-failover-to-azure/TestFailover.png)


1. 選取 [復原方案]  >  *recoveryplan_name*。 按一下 [測試容錯移轉] 。
1. 選取**復原點**toofailover 至。 您可以使用其中一個 hello 下列選項：
    1.  **最新版處理**: hello 復原計劃 toohello 最新復原點的站台復原服務已經處理的所有虛擬機器都容錯移轉這個選項。 當您在進行測試容錯移轉的虛擬機器時，也會顯示 hello 最新的已處理的復原點的時間戳記。 如果您要復原計劃的容錯移轉，您可以移 tooindividual 虛擬機器，並查看**最新復原點**磚 tooget 這項資訊。 當沒有時間 tooprocess hello 未處理的資料時，此選項提供低 RTO （復原時間目標） 容錯移轉選項。
    1.  **最新的應用程式一致**: hello 復原計劃 toohello 最新應用程式一致復原點的站台復原服務已經處理的所有虛擬機器都容錯移轉這個選項。 當您在進行測試容錯移轉的虛擬機器時，也會顯示 hello 最新的應用程式一致復原點的時間戳記。 如果您要復原計劃的容錯移轉，您可以移 tooindividual 虛擬機器，並查看**最新復原點**磚 tooget 這項資訊。
    1.  **最新**： 此選項會先處理所有 hello 資料它們容錯移轉 tooit 之前已傳送的 tooSite 復原服務 toocreate 每部虛擬機器的復原點。 此選項提供 hello 最低 RPO （復原點目標），為 hello 建立虛擬機器容錯移轉將會有所有的 hello 資料之後已觸發 hello 容錯移轉時，複寫 tooSite 復原服務。
    1.  **已處理最近的多部虛擬機器**：此選項僅適用於至少一部虛擬機器已啟動多部虛擬機器一致性的復原計劃。 虛擬機器屬於複寫群組容錯移轉 toohello 最新通用多重 VM 一致性復原點。 其他虛擬機器容錯移轉 tootheir 最近處理過的復原點。  
    1.  **最近的多部虛擬機器應用程式一致**：此選項僅適用於至少一部虛擬機器已啟動多部虛擬機器一致性的復原計劃。 虛擬機器屬於複寫群組容錯移轉 toohello 最新通用多部 VM 應用程式一致復原點。 其他虛擬機器容錯移轉 tootheir 最新應用程式一致復原點。 
    1.  **自訂**： 如果您在進行測試容錯移轉的虛擬機器，則您可以使用此選項 toofailover tooa 特定的復原點。
1. 選取**Azure 虛擬網路**： 提供 Azure 虛擬網路會建立 hello 測試虛擬機器的位置。 站台復原嘗試 toocreate 測試虛擬機器中相同名稱的子網路，以及使用 hello 與中提供的相同 IP**計算與網路**hello 虛擬機器的設定。 如果相同名稱的子網路不是 hello 為測試容錯移轉時，所提供的 Azure 虛擬網路中可用的則依字母順序建立 hello 第一個子網路中測試虛擬機器。 如果 hello 子網路中沒有相同的 IP，虛擬機器取得另一個 hello 子網路中可用的 IP 位址。 請參閱此節以[瞭解更多詳細資訊](#creating-a-network-for-test-failover)
1. 如果您要容錯移轉 tooAzure 和啟用的資料加密，請在**加密金鑰**選取 hello 時啟用資料加密提供者安裝期間發出的憑證。 如果您尚未啟用 hello 虛擬機器上的加密，您可以忽略這個步驟。
1. Hello 上追蹤容錯移轉的進度**作業** 索引標籤。您應該能夠 toosee hello 測試複本機器 hello Azure 入口網站中。
1. tooinitiate hello 虛擬機器的 RDP 連線，您將需要太[新增公用 ip](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) hello hello 的網路介面無法容錯移轉虛擬機器。 如果您容錯移轉 tooa 傳統虛擬機器，則您需要[將端點加入](../virtual-machines/windows/classic/setup-endpoints.md)上連接埠 3389
1. 一旦您完成時，按一下 **清除測試容錯移轉**hello 復原計劃。 在**備忘稿**記錄及儲存與 hello 測試容錯移轉相關聯的任何觀察。 這會刪除 hello 測試容錯移轉期間所建立的虛擬機器。


> [!TIP]
> 站台復原嘗試 toocreate 測試虛擬機器中相同名稱的子網路，以及使用 hello 與中提供的相同 IP**計算與網路**hello 虛擬機器的設定。 如果相同名稱的子網路不是 hello 為測試容錯移轉時，所提供的 Azure 虛擬網路中可用的則依字母順序建立 hello 第一個子網路中測試虛擬機器。 Hello 目標 IP 是 hello 選擇子網路的一部分，如果站台復原會嘗試 toocreate hello 測試容錯移轉虛擬機器使用 hello 目標 IP。 如果 hello 目標 IP 不屬於 hello 選擇子網路測試容錯移轉虛擬機器會建立在 hello 選擇子網路中使用任何可用的 IP。
>
>

## <a name="test-failover-job"></a>測試容錯移轉作業

![Test Failover](./media/site-recovery-test-failover-to-azure/TestFailoverJob.png)

觸發測試容錯移轉時會執行下列步驟︰

1. 先決條件檢查︰這個步驟可確保符合容錯移轉所需的所有條件
1. 容錯移轉： 此步驟中處理 hello 資料，並讓它準備好，以便可以建立 Azure 虛擬機器，不使用。 如果您已選擇**最新**復原點，此步驟中建立的復原點從 toohello 服務已傳送的 hello 資料。
1. 開始： 此步驟中建立 Azure 虛擬機器使用 hello hello 上一個步驟中處理的資料。

## <a name="time-taken-for-failover"></a>容錯移轉所花費的時間

在某些情況下，虛擬機器的容錯移轉需要其他中繼步驟的程序通常需要約 8 too10 分鐘 toocomplete。 這些情況如下所示︰

* VMware 虛擬機器使用的 hello 9.8 比舊的行動服務版本
* 實體伺服器
* VMware Linux 虛擬機器
* 如同實體伺服器般受到保護的 Hyper-V 虛擬機器
* 沒有以下驅動程式作為開機驅動程式的 VMware 虛擬機器
    * storvsc
    * vmbus
    * storflt
    * intelide
    * atapi
* 沒有啟用 DHCP 服務的 VMware 虛擬機器，無論其是否正在使用 DHCP 或靜態 IP 位址

在所有 hello 其他情況下此中繼步驟並不需要與 hello hello 容錯移轉所花費的時間會顯著降低。


## <a name="creating-a-network-for-test-failover"></a>建立測試容錯移轉的網路
建議當您在進行測試容錯移轉，您會選擇與您在中提供您生產復原站台的網路隔離的網路**計算與網路**hello 虛擬機器的設定。 根據預設，當您建立 Azure 虛擬網路時，它會與其他網路隔離。 此網路應模擬您的實際執行網路︰

1. 測試網路應有相同數目的子網路與生產網路中，並以您的生產網路中的 hello 子網路的名稱相同的 hello。
1. 測試網路應該使用 hello 與生產網路的相同的 IP 範圍。
1. 更新 hello hello hello 作為目標 IP hello DNS 虛擬機器在您所提供的 IP 為測試網路的 DNS**計算與網路**設定。 如需詳細資訊，請參閱 [Active Directory 測試容錯移轉考量](site-recovery-active-directory.md#test-failover-considerations) 一節。


## <a name="test-failover-tooa-production-network-on-recovery-site"></a>測試容錯移轉 tooa 復原站台上的實際執行網路
建議當您在進行測試容錯移轉，您會選擇不同於您在中提供您生產復原站台網路的網路**計算與網路**hello 虛擬機器的設定。 如果您真的想 toovalidate 結束 tooend 中失敗的網路連線，但容錯移轉虛擬機器，請注意下列點 hello:

1. 請確定該 hello 主要虛擬機器已關閉，當您在進行 hello 測試容錯移轉。 如果您不要這樣做，將會以 hello 的兩部虛擬機器相同網路在 hello hello 中執行的相同身分識別相同的時間，可能會導致 tooundesired 後果。
1. Hello 測試容錯移轉虛擬機器進行任何變更將會遺失時您清除 hello 測試容錯移轉虛擬機器。 這些變更將不會複寫後 toohello 主要虛擬機器。
1. 這種方式，測試的實際執行應用程式的潛在客戶 tooa 停機時間。 Hello 應用程式的使用者應該 toonot 使用 hello 應用程式時 hello DR 向下切入正在進行中會被要求。  



## <a name="prepare-active-directory-and-dns"></a>準備 Active Directory 和 DNS
toorun 應用程式測試的測試容錯移轉，您會需要 hello 生產 Active Directory 環境的複本在您的測試環境中。 如需詳細資訊，請參閱 [Active Directory 測試容錯移轉考量](site-recovery-active-directory.md#test-failover-considerations) 一節。

## <a name="prepare-tooconnect-tooazure-vms-after-failover"></a>準備容錯移轉之後 tooconnect tooAzure Vm

如果您想 tooconnect tooAzure Vm 使用 RDP 容錯移轉之後，請確定您執行 hello hello 表中摘要說明的動作。

**容錯移轉** | **位置** | **動作**
--- | --- | ---
**執行 Windows 的 Azure VM** | 在容錯移轉前的內部部署機器上 | tooaccess hello Azure VM 上 hello 網際網路、 啟用 RDP，請確定的 TCP 和 UDP 規則會加入 hello**公用**，並允許 RDP **Windows 防火牆** > **允許應用程式**，針對所有設定檔。<br/><br/> 透過站對站連線，tooaccess hello 機器上啟用 RDP，並確定 hello 中允許的 RDP **Windows 防火牆** -> **允許應用程式和功能**如**網域和私人**網路。<br/><br/>  請確定 hello 作業系統的 SAN 原則設定太**OnlineAll**。 [深入了解](https://support.microsoft.com/kb/3031135)。<br/><br/> 請確定沒有任何 Windows 更新擱置中的 hello 虛擬機器上時觸發容錯移轉。 容錯移轉，您就可以 toologin toohello 虛擬機器 hello 更新作業完成之前，可能會啟動 Windows update。 <br/><br/>
**執行 Windows 的 Azure VM** | 在容錯移轉後的 Azure VM 上 | 傳統的虛擬機器，[加入公用端點](../virtual-machines/windows/classic/setup-endpoints.md)hello RDP 通訊協定 （連接埠 3389）<br/><br/>  若是在 Resource Manager 虛擬機器上，請[新增公用 IP](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine)。<br/><br/> hello 網路安全性群組規則上 hello 容錯移轉 VM，而且 hello 它所連接的 Azure 子網路 toowhich 需要 tooallow 連入連線 toohello RDP 連接埠。<br/><br/> 資源管理員虛擬機器，您可以檢查**開機診斷**toolook 在 hello 虛擬機器的螢幕擷取畫面<br/><br/> 如果您無法連接，請檢查該 VM 正在執行中的 hello，然後查看這些[疑難排解提示](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx)。<br/><br/>
**執行 Linux 的 Azure VM** | 在容錯移轉前的內部部署機器上 | 請確定該 hello hello Azure VM 上的 Secure Shell 服務會自動設定 toostart，在系統開機。<br/><br/> 請檢查防火牆規則允許 SSH 連線 tooit。
**執行 Linux 的 Azure VM** | 容錯移轉後的 Azure VM | hello 網路安全性群組規則上 hello 容錯移轉 VM，而且 hello 它所連接的 Azure 子網路 toowhich 需要 tooallow 連入連線 toohello SSH 連接埠。<br/><br/> 傳統的虛擬機器，[加入公用端點](../virtual-machines/windows/classic/setup-endpoints.md)應該建立，tooallow hello SSH 連接埠 （TCP 連接埠 22 依預設） 上的連入連線。<br/><br/> 若是在 Resource Manager 虛擬機器上，請[新增公用 IP](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine)。<br/><br/> 資源管理員虛擬機器，您可以檢查**開機診斷**toolook 在 hello 虛擬機器的螢幕擷取畫面<br/><br/>



## <a name="next-steps"></a>後續步驟
一旦您成功嘗試測試容錯移轉之後，您就可以嘗試執行[容錯移轉](site-recovery-failover.md)。

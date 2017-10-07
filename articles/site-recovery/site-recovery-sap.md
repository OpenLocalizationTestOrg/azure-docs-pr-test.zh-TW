---
title: "aaaProtect 使用 Azure Site Recovery 的多層式 SAP NetWeaver 應用程式部署 |Microsoft 文件"
description: "本文說明如何 tooprotect SAP NetWeaver 應用程式部署使用 Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: manayar
ms.openlocfilehash: 34651c7b14d23a44005372f4f923c401e0224231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protect-a-multi-tier-sap-netweaver-application-deployment-using-azure-site-recovery"></a>使用 Azure Site Recovery 保護多層式 SAP NetWeaver 應用程式部署

大部分的大型與中型 SAP 部署都有某種形式的災害復原方案。  更多的核心商務處理程序是移動 （如 SAP) tooapplications 增加 hello 重要性強固和可測試的災害復原解決方案。  Azure Site Recovery 已完善測試而且整合的 SAP 應用程式，而且超過 hello 功能大部分在內部部署災害復原方案，在降低擁有權總成本 (TCO) 比競爭解決方案。
使用 Azure Site Recovery，您可以：
* 啟用 SAP NetWeaver 和非 NetWeaver 實際執行應用程式內部，藉由複寫元件 tooAzure 的保護。
* 啟用保護，藉由複寫元件 tooanother Azure 資料中心內執行 Azure 的 SAP NetWeaver 和非 NetWeaver 生產應用程式。
* 使用站台復原 toomigrate 您 SAP 部署 tooAzure 簡化雲端移轉。
* 藉由建立隨選生產複本來測試 SAP 應用程式，簡化 SAP 專案升級、測試和原型設計。

本文說明如何 tooprotect SAP NetWeaver 應用程式部署使用[Azure Site Recovery](site-recovery-overview.md)。 本文章涵蓋 hello 保護藉由複寫 tooanother 使用 Azure Site Recovery，hello 支援案例和組態，Azure 資料中心的三層式 SAP NetWeaver 部署在 Azure 上的最佳作法和如何 tooperform 容錯移轉，同時測試實際的容錯移轉和容錯移轉 （災害復原演練）。


## <a name="prerequisites"></a>必要條件
開始之前，請確定您了解 hello 下列：

1. [複寫虛擬機器 tooAzure](azure-to-azure-walkthrough-enable-replication.md)
2. 如何太[設計與復原網路](site-recovery-azure-to-azure-networking-guidance.md)
3. [執行測試容錯移轉 tooAzure](azure-to-azure-walkthrough-test-failover.md)
4. [執行容錯移轉 tooAzure](site-recovery-failover.md)
5. 如何太[複寫的網域控制站](site-recovery-active-directory.md)
6. 如何太[複寫 SQL Server](site-recovery-sql.md)

## <a name="supported-scenarios"></a>支援的案例
使用 Azure Site Recovery 中，您可以實作下列案例的 hello 災害復原解決方案：
* 架構在一個 Azure 資料中心複寫 tooanother (Azure-Azure DR) 的 Azure 資料中心執行的 SAP 系統[這裡](https://aka.ms/asr-a2a-architecture)。
* 執行 VMWare （或實體） 的伺服器上的 SAP 系統的內部複寫 tooa DR 網站，在 Azure 資料中心 (VMware-Azure DR)，這需要一些額外的元件，因為架構[這裡](https://aka.ms/asr-v2a-architecture)。
* 在 HYPER-V 上執行的 SAP 系統的內部複寫 tooa DR 網站，在 Azure 資料中心 (Hyper-v-V-至 Azure DR)，這需要一些額外的元件，因為架構[這裡](https://aka.ms/asr-h2a-architecture)。

這份文件會使用 hello 第一個案例-Azure-Azure DR-toodemonstrate Azure Site Recovery 的 SAP 災害復原功能。 Azure Site Recovery 的複寫與應用程式無關，是針對其他情況下的預期的 toohold hello 所述的程序。

### <a name="required-foundation-services"></a>必要的基礎服務
此文件案例中所有已部署以下列 foundation 服務部署的 hello:
* ExpressRoute 或站對站虛擬私人網路 (VPN)
* 至少有一個 Active Directory 網域控制站和 DNS 伺服器在 Azure 中執行

建議您使用上述 hello 基礎結構會建立先前 toodeploying Azure Site Recovery。


## <a name="typical-sap-application-deployment"></a>典型 SAP 應用程式部署
大型的 SAP 客戶通常部署之間 6 too20 個別的 SAP 應用程式。  這些應用程式的大部分取決於 hello SAP NetWeaver ABAP 或 Java 引擎。  這些核心 NetWeaver 應用程式 (有些通常是非 SAP 應用程式) 是由許多小型特定非 NetWeaver SAP 獨立引擎支援。  

它是關鍵 tooinventory hello SAP 執行所有應用程式中的橫向與 toodetermine hello 部署模式 （2 層或 3 層）、 版本、 修補程式，大小、 變換率，以及磁碟持續性需求。

![部署模式](./media/site-recovery-sap/sap-typical-deployment.png)

hello SAP 資料庫保存層應該保護透過 hello 原生 DBMS 工具，例如 SQL Server AlwaysOn、 Oracle DataGuard 或 HANA 系統複寫。 hello 用戶端層也不受 Azure Site Recovery 中，但會影響此圖層，例如 DNS 傳播延遲、 安全性和遠端存取 toohello DR 資料中心的重要 tooconsider 主題。

Azure Site Recovery 會為 hello 建議 hello 應用程式層，其中包括 (A) SCS 的方案。 其他應用程式等非 NetWeaver SAP 應用程式和非 SAP 應用程式組成 hello 整體 SAP 部署環境，也應該與 Azure Site Recovery 保護。

## <a name="replicate-virtual-machines"></a>複寫虛擬機器
請遵循[本指南](azure-to-azure-walkthrough-enable-replication.md)toostart 複寫所有 hello SAP 應用程式的虛擬機器 toohello Azure DR 資料中心。

如果您使用靜態 ip 位址，您可以指定您想 hello hello 運算和網路設定中網路介面卡區段中的虛擬機器 tootake hello IP。

![目標 IP](./media/site-recovery-sap/sap-static-ip.png)


## <a name="creating-a-recovery-plan"></a>建立復原計劃
復原計劃可讓您排序 hello 容錯移轉維護應用程式一致性是多層式應用程式，因此，在各層。 請依照下列所述的 hello 步驟[這裡](site-recovery-create-recovery-plans.md)時建立多層式 web 應用程式的復原計劃。

### <a name="adding-scripts-toohello-recovery-plan"></a>加入指令碼 toohello 復原計劃
您可能需要 toodo hello Azure 虛擬機器後測試容錯移轉/容錯移轉的某些作業的應用程式 toofunction 正確。 您可以自動化 hello post 容錯移轉作業，例如更新 DNS 項目，以及變更繫結和連接，藉由新增 hello 復原計劃中的對應的指令碼中所述[本文](site-recovery-create-recovery-plans.md#add-scripts)。

### <a name="dns-update"></a>DNS 更新
如果通常 hello DNS 設定為動態 DNS 更新時，則虛擬機器更新 hello DNS hello 新 ip 之後啟動。 如果您想 tooadd 以 hello 明確步驟 tooupdate DNS 新 hello 虛擬機器的 Ip 再新增這[指令碼在 DNS 中的 tooupdate IP](https://aka.ms/asr-dns-update)作為復原計畫群組後動作。  

## <a name="example-azure-to-azure-deployment"></a>Azure 對 Azure 部署範例
Hello 圖 hello Azure Site Recovery Azure-Azure DR 案例中會說明：
* 主要資料中心是新加坡 （Azure 南東亞洲） 中的 hello 與 hello DR 資料中心是香港特別行政區 （Azure 東亞）。  在此案例中，擁有兩部在新加坡以同步模式執行 SQL Server AlwaysOn 的 VM，即可提供本機高可用性。
* 檔案共用 ASCS hello 可以是使用的 tooprovide HA hello SAP 單一失敗點。 檔案共用 ASCS 不需要叢集共用磁碟，而且不需要 SIOS 等應用程式。
* Hello DBMS 層的 DR 保護是利用非同步複寫來達成。
* 這個案例顯示 「 對稱 DR"– 使用的詞彙 toodescribe DR 方案中的實際執行的相同複本，因此 hello DR SQL Server 方案的本機高可用性。 hello 對稱 DR 使用並非強制性的 hello 資料庫層級，而且許多客戶利用 hello 彈性的雲端部署 toobuild 本機的高可用性節點快速 DR 事件之後。
* hello 圖表描述 SAP NetWeaver ASCS hello 和複寫的 Azure Site Recovery 的應用程式伺服器層。

![複寫案例](./media/site-recovery-sap/sap-replication-scenario.png)

## <a name="doing-a-test-failover"></a>執行測試容錯移轉
請遵循[本指南](azure-to-azure-walkthrough-test-failover.md)toodo 測試容錯移轉。

1.  移 tooAzure 入口網站，然後選取您的復原服務保存庫。
2.  按一下 hello 針對 SAP 應用程式 (s) 建立的復原計劃。
3.  按一下 [測試容錯移轉]。
4.  選取的復原點和 Azure 虛擬網路 toostart hello 測試容錯移轉程序。
5.  一旦 hello 次要環境已啟動，您可以執行您的驗證。
6.  Hello 驗證完成後，按一下 [清除測試容錯移轉]，並 tooclean hello 容錯移轉環境。

## <a name="doing-a-failover"></a>執行容錯移轉
當您在進行容錯移轉時，請依照[本指引](site-recovery-failover.md)。

1.  移 tooAzure 入口網站，然後選取您的復原服務保存庫。
2.  按一下 hello SAP 應用程式所建立的復原計畫。
3.  按一下 [容錯移轉]。
4.  選取的復原點 toostart hello 容錯移轉程序。

## <a name="next-steps"></a>後續步驟
請參閱[本白皮書](http://aka.ms/asr-sap)，了解如何使用 Azure Site Recovery 為 SAP NetWeaver 部署建置災害復原解決方案。 hello 技術白皮書也會討論不同 SAP 架構的建議，列出在 Azure 上 SAP 支援的應用程式和 VM 類型並描述可能的災害復原方案的測試計劃。

深入了解如何使用 Site Recovery [複寫其他工作負載](site-recovery-workload.md)。

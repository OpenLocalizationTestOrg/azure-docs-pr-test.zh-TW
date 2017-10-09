---
title: "aaaWhat 工作負載可以使用 Azure Site Recovery 保護？"
description: "Azure Site Recovery 可協調 hello 複寫、 容錯移轉和復原的內部部署虛擬機器和實體伺服器 tooAzure 或 tooa 次要內部部署站台來保護您的工作負載和應用程式"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: 4953948f-26c0-4699-8fe7-59d3bfc1d3da
ms.service: site-recovery
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/08/2017
ms.author: raynew
ms.openlocfilehash: cab2e1ce3c2b7b2c5f899d957219f5c12eb5965c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-workloads-can-you-protect-with-azure-site-recovery"></a>Azure Site Recovery 可以保護哪些工作負載？
本文說明的工作負載和應用程式，您可以將複寫以 hello Azure Site Recovery 服務。

將任何註解或問題張貼在本文中，或在 hello hello 下方[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="overview"></a>概觀
組織需要業務續航力和災害復原 (BCDR) 策略 tookeep 工作負載以及資料安全且可在計劃性與非計劃性停機期間，並且儘速復原 tooregular 工作條件。

站台復原是一項 Azure 服務可提供 tooyour BCDR 策略。 使用站台復原，您可以部署應用程式感知的複寫 toohello 雲端或 tooa 次要站台。 無論您的應用程式是 Windows 或 Linux 為基礎，其執行於實體伺服器、 VMware 或 HYPER-V，您可以使用站台復原 tooorchestrate 複寫、 執行損毀修復測試，並執行容錯移轉和容錯回復。

Site Recovery 整合了 Microsoft 應用程式，包括 SharePoint、Exchange、Dynamics、SQL Server 和 Active Directory。 Microsoft 也與領導廠商密切合作，包括 Oracle、SAP、IBM 和 Red Hat。 您可以根據各應用程式自訂複寫解決方案。

## <a name="why-use-site-recovery-for-application-replication"></a>為何要使用 Site Recovery 進行應用程式複寫？
站台復原作為 tooapplication 層級的保護和復原，如下所示：

* 應用程式無從驗證，針對在受支援電腦上執行的任何工作負載提供複寫。
* 接近同步，與複寫 Rpo 為 30 秒 toomeet hello 需求最重要的商務營運應用程式。
* 適用於單一或多層式架構應用程式的應用程式一致性快照。
* 整合 SQL Server AlwaysOn，並與其他應用程式層級的複寫技術合作，包括 AD 複寫、SQL AlwaysOn、Exchange 資料庫可用性群組 (DAG) 和 Oracle 資料保護。
* 彈性的復原方案，可讓您 toorecover 整個應用程式堆疊，只要按一下，並包含 tooinclude 外部指令碼和手動動作 hello 計劃中。
* 進階 toosimplify Site Recovery 和 Azure 中的網路管理應用程式的網路需求，包括 hello 能力 tooreserve IP 位址設定負載平衡和整合搭配 Azure 流量管理員中，低 RTO 網路 switchovers。
* 豐富的自動化程式庫，提供已可用於生產環境的應用程式特定指令碼，這些指令碼可供下載並與復原方案整合。

## <a name="workload-summary"></a>工作負載摘要
Site Recovery 可複寫在支援的機器上執行的任何應用程式。 此外，我們已密切與產品小組 toocarry 出其他應用程式專屬測試。

| **工作負載** | **複寫 HYPER-V Vm tooa 次要站台** | **複寫 HYPER-V Vm tooAzure** | **複製 VMware Vm tooa 次要站台** | **複製 VMware Vm tooAzure** |
| --- | --- | --- | --- | --- |
| Active Directory、DNS |Y |Y |Y |Y |
| Web 應用程式 (IIS、SQL) |Y |Y |Y |Y |
| System Center Operations Manager |Y |Y |Y |Y |
| Sharepoint |Y |Y |Y |Y |
| SAP<br/><br/>非叢集的複寫 SAP 網站 tooAzure |Y (由 Microsoft 測試) |Y (由 Microsoft 測試) |Y (由 Microsoft 測試) |Y (由 Microsoft 測試) |
| Exchange (非 DAG) |Y |Y |Y |Y |
| 遠端桌面/VDI |Y |Y |Y |N/A |
| Linux (作業系統和應用程式) |Y (由 Microsoft 測試) |Y (由 Microsoft 測試) |Y (由 Microsoft 測試) |Y (由 Microsoft 測試) |
| Dynamics AX |Y |Y |Y |Y |
| Dynamics CRM |Y |敬請期待 |Y |敬請期待 |
| Oracle |Y (由 Microsoft 測試) |Y (由 Microsoft 測試) |Y (由 Microsoft 測試) |Y (由 Microsoft 測試) |
| Windows 檔案伺服器 |Y |Y |Y |Y |
| Citrix XenApp 和 XenDesktop |N/A |Y |N/A |Y |

## <a name="replicate-active-directory-and-dns"></a>複寫 Active Directory 和 DNS
Active Directory 和 DNS 基礎結構是不可或缺的 toomost 企業應用程式。 嚴重損壞修復期間，將需要 tooprotect 和復原這些基礎結構元件，然後再進行復原您的工作負載和應用程式。

您可以使用站台復原 toocreate 完整的自動化的災害復原方案的 Active Directory 和 DNS。 比方說，如果您想 toofail 透過 SharePoint 和 SAP，從主要 tooa 次要網站時，您可以設定復原方案容錯 Active Directory 第一次，並額外的應用程式專屬復原規劃 toofail 透過 hello 依賴作用中的其他應用程式目錄。

[深入了解](site-recovery-active-directory.md) 如何保護 Active Directory 和 DNS。

## <a name="protect-sql-server"></a>保護 SQL Server
SQL Server 針對內部部署資料中心內許多商務應用程式，提供資料服務的資料服務基礎。  站台復原可以對照 SQL Server HA/DR 技術，使用 SQL Server 的 tooprotect 多層式企業應用程式。 Site Recovery 提供：

* 針對 SQL Server 提供簡單且符合成本效益的災害復原解決方案。 複寫多個版本與版本的 SQL Server 的獨立伺服器和叢集、 tooAzure 或 tooa 次要站台。  
* SQL AlwaysOn 可用性群組容錯移轉、 toomanage 以及與 Azure Site Recovery 復原計劃的容錯回復與整合。
* 端對端復原計畫 hello 應用程式，包括 hello SQL Server 資料庫中的所有層。
* 藉由將 SQL Server「暴增」到 Azure 中較大的 IaaS 虛擬機器中，利用 Azure Site Recovery 調整 SQL Server 以因應尖峰負載。
* 簡單的 SQL Server 災害復原測試。 您可以執行測試容錯移轉 tooanalyze 資料並執行相容性檢查，而不會影響您的生產環境。

[深入了解](site-recovery-sql.md) 如何保護 SQL Server。

## <a name="protect-sharepoint"></a>保護 SharePoint
Azure Site Recovery 可協助保護 SharePoint 部署，如下所示：

* 排除 hello 需要和相關聯的基礎結構成本的災害復原的待命伺服器陣列。 使用站台復原 tooreplicate 整個伺服器陣列 （Web、 應用程式和資料庫層） tooAzure 或 tooa 次要站台。
* 簡化應用程式部署和管理作業。 部署更新 toohello 主要站台會自動複寫，並因此後就可以容錯移轉和復原的次要站台的伺服陣列。 也會減少 hello 管理複雜程度與成本相關聯的待命伺服器陣列保持在最新狀態。
* 藉由建立類似生產的複本隨選複本環境進行測試和偵錯，以簡化 SharePoint 應用程式開發和測試。
* 使用站台復原 toomigrate SharePoint 部署 tooAzure 簡化轉換 toohello 雲端。

[深入了解](site-recovery-sharepoint.md) 如何保護 SharePoint。

## <a name="protect-dynamics-ax"></a>保護 Dynamics AX
Azure Site Recovery 可協助保護您的 Dynamics AX ERP 解決方案，方法如下：

* 協調整個 Dynamics AX 環境 （Web 和 AOS 層、 資料庫層，SharePoint） 的複寫 tooAzure，或 tooa 次要站台。
* 簡化的 Dynamics AX 部署 toohello 雲端 (Azure) 的移轉。
* 藉由建立類似生產的複本隨選進行測試和偵錯，以簡化 Dynamics AX 應用程式開發和測試。

[深入了解](site-recovery-dynamicsax.md) 如何保護動態 Dynamic AX。

## <a name="protect-rds"></a>保護 RDS
遠端桌面服務 (RDS) 可啟用虛擬桌面基礎結構 (VDI)、 工作階段為基礎的桌面和應用程式，可讓使用者 toowork 任何位置。 使用 Azure Site Recovery，您可以：

* 受管理或未受管理的集區虛擬桌面 tooa 次要站台，以及遠端應用程式和工作階段 tooa 次要站台或 Azure 複寫。
* 以下是您可以複寫的項目︰

| **RDS** | **複寫 HYPER-V Vm tooa 次要站台** | **複寫 HYPER-V Vm tooAzure** | **複製 VMware Vm tooa 次要站台** | **複製 VMware Vm tooAzure** | **將實體伺服器 tooa 次要站台複寫** | **複寫 tooAzure 實體伺服器** |
| --- | --- | --- | --- | --- | --- | --- |
| **集區化虛擬桌面 (未受管理)** |是 |否 |是 |否 |是 |否 |
| **集區化虛擬桌面 (受管理但不含 UPD)** |是 |否 |是 |否 |是 |否 |
| **遠端應用程式和桌面工作階段 (不含 UPD)** |是 |是 |是 |是 |是 |是 |

[深入了解](https://gallery.technet.microsoft.com/Remote-Desktop-DR-Solution-bdf6ddcb) 如何保護 RDS。

## <a name="protect-exchange"></a>保護 Exchange
Site Recovery 協助保護 Exchange 的方式如下所示：

* 針對小型的 Exchange 部署，例如單一或獨立伺服器站台復原可以複寫和容錯移轉 tooAzure 或 tooa 次要站台。
* 對於大型部署，Site Recovery 會與 Exchange DAG 整合。
* Exchange Dag 會建議您在企業中的 Exchange 災害復原解決方案的 hello。  站台復原的復原計劃可以包括 Dag，tooorchestrate DAG 跨站台的容錯移轉。

[深入了解](https://gallery.technet.microsoft.com/Exchange-DR-Solution-using-11a7dcb6) 如何保護 Exchange。

## <a name="protect-sap"></a>保護 SAP
使用站台復原 tooprotect SAP 部署的選項，如下：

* 啟用 SAP NetWeaver 和非 NetWeaver 實際執行應用程式內部，藉由複寫元件 tooAzure 的保護。
* 啟用保護，藉由複寫元件 tooanother Azure 資料中心內執行 Azure 的 SAP NetWeaver 和非 NetWeaver 生產應用程式。
* 使用站台復原 toomigrate 您 SAP 部署 tooAzure 簡化雲端移轉。
* 藉由建立隨選生產複本來測試 SAP 應用程式，簡化 SAP 專案升級、測試和原型設計。

[深入了解](site-recovery-sap.md) 如何保護 SAP。

## <a name="protect-iis"></a>保護 IIS
使用站台復原 tooprotect IIS 部署，如下：

Azure Site Recovery 提供災害復原，藉由複寫您的環境 tooa 冷遠端站台或如 Microsoft Azure 公用雲端中的 hello 重要元件。 Hello hello web 伺服器與 hello 資料庫的虛擬機器正在複寫的 toohello 復原站台，因為沒有任何需求 toobackup 組態檔或憑證分開。 hello 應用程式對應，並透過整合到 hello 災害復原計畫的指令碼可以更新繫結相關的容錯移轉後已變更的環境變數。 虛擬機器只能在容錯移轉的 hello 事件中的 hello 復原站台上權數啟動。 不只如此，Azure Site Recovery 也可協助您協調 hello 結束 tooend 容錯移轉，藉由提供您 hello 下列功能：

-   排序 hello 關機和啟動虛擬機器中的 hello 各層。
-   後已啟動，請將指令碼 tooallow 更新應用程式相依性和繫結加入 hello 虛擬機器上。 hello 指令碼也可以使用的 tooupdate hello DNS 伺服器 toopoint toohello 復原站台。
-   藉由對應 hello 主要和復原網路配置 IP 位址 toovirtual 機器前容錯移轉，因此不需要 toobe 使用指令碼更新容錯移轉後。
-   Hello web 伺服器，因此減少混淆的可能性 hello 事件中的嚴重損壞的 hello 範圍上的多個 web 應用程式的一種單鍵容錯移轉的能力。
-   能力 tootest hello 復原計劃的 DR 向下切入的隔離環境中。

[深入了解](https://aka.ms/asr-iis) 如何保護 IIS web 伺服陣列。

## <a name="protect-citrix-xenapp-and-xendesktop"></a>保護 Citrix XenApp 和 XenDesktop
使用站台復原 tooprotect Citrix XenApp 和 XenDesktop 部署，如下：

* 啟用保護的 hello Citrix XenApp 和 XenDesktop 部署，藉由複寫不同的部署層上，包括 （AD DNS 伺服器，SQL 資料庫伺服器、 Citrix 傳遞控制站，StoreFront server，XenApp Master (VDA) Citrix XenApp 授權伺服器）tooAzure。
* 使用站台復原 toomigrate 您 Citrix XenApp 和 XenDesktop 部署 tooAzure，以簡化雲端移轉。
* 藉由建立類似生產的隨選複本來進行測試和偵錯，以簡化 Citrix XenApp/XenDesktop 測試。
* 此解決方案僅適用於 Windows Server 作業系統虛擬桌面，而不適用於用戶端虛擬桌面，因為尚未支援在 Azure 中進行用戶端虛擬桌面的授權。
[深入了解](https://azure.microsoft.com/pricing/licensing-faq/)如何在 Azure 中進行用戶端/伺服器桌面的授權。

[深入了解](site-recovery-citrix-xenapp-and-xendesktop.md)如何保護 Citrix XenApp 和 XenDesktop 部署。 另外，您可以參考 hello[白皮書 （英文) Citrix](https://aka.ms/citrix-xenapp-xendesktop-with-asr)詳述 hello 相同。

## <a name="next-steps"></a>後續步驟
[檢查必要條件](site-recovery-prereq.md)

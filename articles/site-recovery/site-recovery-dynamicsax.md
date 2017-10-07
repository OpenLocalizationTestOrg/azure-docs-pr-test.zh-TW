---
title: "使用 Azure Site Recovery 的多層式 Dynamics AX 部署 aaaReplicate |Microsoft 文件"
description: "本文說明如何 tooreplicate 及保護 Dynamics AX 使用 Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/24/2017
ms.author: asgang
ms.openlocfilehash: b974315ec50ab2ec43846b3d3f95c7de88b72fc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a>使用 Azure Site Recovery 複寫多層式 Dynamics AX 應用程式

## <a name="overview"></a>概觀


Microsoft Dynamics AX hello 熱門 ERP 方案之間的企業 toostandardized 程序的其中一個位置，管理資源和簡化相容性。 Hello 應用程式是商務關鍵 tooan 組織考量是確定非常重要 toobe，如果任何損毀時，應用程式應該啟動且正在執行中的最小時間。

現今，Microsoft Dynamics AX 並未提供任何現成的災害復原功能。 Microsoft Dynamics AX 包含許多伺服器元件，例如應用程式物件的伺服器、 Active Directory (AD)、 SQL 資料庫伺服器，SharePoint 伺服器，以手動方式是 Reporting Server 等 toomanage hello 嚴重損壞修復的每個元件不只若高度耗費資源，但也容易發生錯誤。

本文詳細說明有關如何使用 [Azure Site Recovery](site-recovery-overview.md) 為 Dynamics AX 應用程式建立災害復原解決方案。 也會探討使用單鍵復原方案、支援的組態和必要條件的計劃性/非計劃性/測試容錯移轉。
以 Azure Site Recovery 為基礎的災害復原解決方案已經過完整測試、認證並由 Microsoft Dynamics AX 建議。



## <a name="prerequisites"></a>必要條件

實作災害復原使用 Azure Site Recovery 的 Dynamics AX 應用程式需要 hello 之後完成的必要元件。

•   已設定內部部署 Dynamics AX 部署

•   已在 Microsoft Azure 訂用帳戶中建立 Azure Site Recovery 服務保存庫

• 如果 Azure 為您的復原網站 hello Azure 虛擬機器整備評估工具上執行的 Vm tooensure 它們相容的 Azure Vm 與 Azure Site Recovery Services


## <a name="site-recovery-support"></a>Site Recovery 支援

Hello 目的是要建立此發行項時，會使用與 Windows Server 2012 R2 Enterprise 上 Dynamics AX 2012R3 VMware 虛擬機器。 站台復原複寫與應用程式無關，hello 建議提供以下是預期的 toohold 以及下列案例。

### <a name="source-and-target"></a>來源與目標

**案例** | **tooa 次要站台** | **tooAzure**
--- | --- | ---
**Hyper-V** | 是 | 是
**VMware** | 是 | 是
**實體伺服器** | 是 | 是

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a>使用 Azure Site Recovery 啟用 Dynamics AX 應用程式的 DR
### <a name="protect-your-dynamics-ax-application"></a>保護 Dynamics AX 應用程式
每個元件的 hello Dynamics AX 需求 toobe 保護 tooenable hello 完整的應用程式的複寫和復原。 本節涵蓋︰

**1.Active Directory 的保護**

**2.SQL 層的保護**

**3.應用程式和 Web 層的保護**

**4.網路設定**

**5.復原方案**

### <a name="1-setup-ad-and-dns-replication"></a>1.安裝 AD 和 DNS 複寫

Active Directory 需要 Dynamics AX 應用程式 toofunction 的 hello DR 網站。 有兩個建議的選擇依據 hello 客戶的內部部署環境的 hello 複雜性。

**選項 1**

如果 hello 客戶都有少量應用程式和其整個的單一網域控制站在內部部署站台和將會容錯移轉 hello 整個站台在一起，則我們建議使用 ASR 複寫 tooreplicate hello DC 機器 toosecondary 站台 （適用於站台 tooSite 和站台 tooAzure）。

**選項 2**

如果 hello 客戶具有大量的應用程式和執行 Active Directory 樹系，而且將容錯移轉少數應用程式一次，則我們建議您設定 hello DR 網站上的其他網域控制站 (次要站台或 Azure 中)。

請參閱太[上提供可用的網域控制站在 DR 網站上的附屬指南](site-recovery-active-directory.md)。 對於本文件的其餘部分，我們會假設 DR 網站上有 DC 可用。

### <a name="2-setup-sql-server-replication"></a>2.設定 SQL Server 複寫
如需詳細指引技術 hello 建議保護選項，請參閱 toocompanion 指南[SQL 層](site-recovery-sql.md)。

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a>3.啟用 Dynamics AX 用戶端和 AOS VM 的保護
執行相關的 Azure Site Recovery 設定，根據 hello Vm 是否部署於[HYPER-V](site-recovery-hyper-v-site-to-azure.md)或在[VMware](site-recovery-vmware-to-azure.md)。

> [!TIP]
> 建議的損毀一致的頻率 tooconfigure 是 15 分鐘。
>

hello 快照下方會顯示 'VMware 站台 tooAzure' 保護案例中的 hello 的 Dynamics 元件 Vm 的保護狀態。
![受保護的項目](./media/site-recovery-dynamics-ax/protecteditems.png)

### <a name="4-configure-networking"></a>4.設定網路功能
設定 VM 計算和網路設定

Hello AX 用戶端和 AOS Vm，讓 hello VM 網路中取得附加的 toohello 正確 DR 網路容錯移轉之後，Azure Site Recovery 中設定網路設定。 請確定這些層的 hello DR 網路路由傳送 toohello SQL 層。

您可以選取在 hello hello VM 複寫項目 tooconfigure hello 網路設定，下列 hello 快照中所示。

* AOS 伺服器選取 hello 正確的可用性設定組。

* 如果您使用靜態 ip 位址，則指定您想 hello hello 中的虛擬機器 tootake hello IP**目標 IP**欄位![網路設定](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)



### <a name="5-creating-a-recovery-plan"></a>5.建立復原計劃

您可以在 Azure Site Recovery tooautomate hello 容錯移轉程序中建立的復原計劃。 Hello 復原計劃中加入應用程式層和 web 層。 排列這些資料行中不同的群組讓的 hello 前端應用程式層之前關閉。

1)  選取您的訂用帳戶中的 hello Azure Site Recovery 保存庫，並按一下 '復原計畫' 的磚。

2)  按一下 [+ 復原方案] 並指定名稱。

3)  選取 hello 'Source' 和 'Target'。 hello 目標可以是 Azure 或次要站台。 如果您選擇 Azure，您必須指定 hello 部署模型

![建立復原方案](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  選取 hello AOS 與用戶端 Vm toohello 復原計劃，然後按一下 ✓。
![建立復原方案](./media/site-recovery-dynamics-ax/selectvms.png)


![復原方案](./media/site-recovery-dynamics-ax/recoveryplan.png)

您可以藉由新增不同的步驟如下所述自訂 hello Dynamics AX 應用程式的復原計劃。 hello 快照集上方顯示 hello 完整的復原方案之後加入所有 hello 步驟。

*步驟：*

*1.SQL Server 容錯移轉步驟*

參照太['SQL Server DR 解決方案'](site-recovery-sql.md)附屬指南，如需復原步驟特定 tooSQL 伺服器詳細資料。

*2.容錯移轉群組 1： 容錯移轉 hello AOS Vm*

請確定選取的復原點 hello 做為可能 toohello 資料庫 PIT 關閉但不是會繼續。

*3.指令碼： 新增負載平衡器 (僅 E-A)*出現 tooadd 負載平衡器 tooit AOS VM 群組之後加入指令碼 （透過 Azure 自動化）。 您可以使用指令碼 toodo 這項工作。 發行項，請參閱[如何 tooadd 用於負載平衡器多層式應用程式 DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)

*4.容錯移轉群組 2： 容錯移轉 hello AX 用戶端 Vm。*
容錯移轉的 hello 復原方案一部分的 hello web 層 Vm。


### <a name="doing-a-test-failover"></a>執行測試容錯移轉

Too'AD DR 解決方案，請參閱 ' 與 'SQL Server DR 解決方案' 附屬指南考量特定 tooAD 和分別測試容錯移轉期間的 SQL server。

1.  移 tooAzure 入口網站，然後選取您的站台復原保存庫。
2.  按一下建立的 Dynamics AX hello 復原計劃。
3.  按一下 [測試容錯移轉]。
4.  選取 hello 虛擬網路 toostart hello 測試容錯移轉程序。
5.  一旦 hello 次要環境已啟動，您可以執行您的驗證。
6.  Hello 驗證完成後，您可以選取 '完成驗證'，並將清除 hello 測試容錯移轉環境。

請遵循[本指南](site-recovery-test-failover-to-azure.md)toodo 測試容錯移轉。

### <a name="doing-a-failover"></a>執行容錯移轉

1.  移 tooAzure 入口網站，然後選取您的站台復原保存庫。
2.  按一下建立的 Dynamics AX hello 復原計劃。
3.  按一下 [容錯移轉]，然後選取 [容錯移轉]。
4.  選取 hello 目標網路，然後按一下 ✓ toostart hello 容錯移轉程序。

當您在進行容錯移轉時，請依照[本指引](site-recovery-failover.md)。

### <a name="perform-a-failback"></a>執行容錯回復

Too'SQL 伺服器 DR 解決方案，請參閱 ' 考量特定 tooSQL 伺服器在容錯回復期間的附屬指南。

1.  移 tooAzure 入口網站，然後選取您的站台復原保存庫。
2.  按一下建立的 Dynamics AX hello 復原計劃。
3.  按一下 [容錯移轉]，然後選取 [容錯移轉]。
4.  按一下 [變更方向]。
5.  選取 hello 適當的選項為 VM 建立選項與資料同步處理
6.  按一下 ✓ toostart hello '容錯回復' 處理序。


當您在進行容錯回復時，請依照[本指引](site-recovery-failback-azure-to-vmware.md)。

##<a name="summary"></a>摘要
使用 Azure Site Recovery，您可以為 Dynamics AX 應用程式建立一個完整的自動化災害復原方案。 您可以從任何地方秒內起始 hello 容錯移轉在 hello 中斷的事件，並取得 hello 應用程式啟動並執行以分鐘為單位。

## <a name="next-steps"></a>後續步驟
讀取[可以保護哪些工作負載？](site-recovery-workload.md) toolearn 深入了解保護與 Azure Site Recovery 的企業工作負載。

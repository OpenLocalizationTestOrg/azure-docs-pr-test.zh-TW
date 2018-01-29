---
title: "關於 Azure Migrate | Microsoft Docs"
description: "提供 Azure Migrate 服務的概觀。"
author: rayne-wiselman
ms.service: azure-migrate
ms.topic: overview
ms.date: 01/08/2018
ms.author: raynew
ms.openlocfilehash: 0bd3d7a9961e7a095684262ae1031f5a3ac0c3fb
ms.sourcegitcommit: 9a8b9a24d67ba7b779fa34e67d7f2b45c941785e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="about-azure-migrate"></a>關於 Azure Migrate

Azure Migrate 服務會評估要移轉至 Azure 的內部部署工作負載。 此服務會評估移轉適用性和以效能為基礎的大小調整，並提供在 Azure 中執行內部部署機器的成本估計。 如果您打算進行隨即移轉，或在移轉的早期評估階段中，此服務很適合您。 評估之後，您可以使用 Azure Site Recovery 和 Azure 資料庫移轉等服務，將機器移轉至 Azure。

> [!NOTE]
> Azure Migrate 目前為預覽狀態並支援生產工作負載。

## <a name="why-use-azure-migrate"></a>為何使用 Azure Migrate？

Azure Migrate 可協助您：

- **評估 Azure 整備程度**：評估您的內部部署機器是否適合在 Azure 中執行。 
- **取得大小建議**：根據內部部署 VM 的效能歷程記錄，取得 Azure VM 的大小建議。 
- **預估每月成本**：取得在 Azure 中執行內部部署機器的估計成本。  
- **安心地移轉**：將內部部署機器的相依性視覺化，以建立您將一起評估和移轉的機器群組。 您可準確地檢視特定機器或群組中所有機器的相依性。

## <a name="current-limitations"></a>目前的限制

- 目前，您可以評估內部部署 VMware 虛擬機器 (VM) 以便移轉到 Azure VM。

> [!NOTE]
> Hyper-V 支援已在藍圖中，將儘速啟用。 在過渡時期，我們建議您使用 [Azure Site Recovery 部署規劃工具](http://aka.ms/asr-dp-hyperv-doc)來規劃 Hyper-V 工作負載的移轉。 

- 您可以在單一探索中探索多達 1000 個 VM，並在單一專案中探索多達 1500 個 VM。 此外，您還可以在單一評估中評估多達 400 個 VM。 如果您需要探索或評估更多數量，則可以增加探索或評估的數目。 [深入了解](how-to-scale-assessment.md)。
- 您要評估的 VM 必須由 vCenter Server (5.5、6.0 或 6.5 版) 管理。
- 您只能在「美國中西部」區域建立 Azure Migrate 專案。 不過，這不會影響您針對不同的目標 Azure 位置規劃移轉的能力。 移轉專案的位置只用於儲存在內部部署環境中發現的中繼資料。
- Azure Migrate 只支援將受控磁碟用於進行移轉評估。

## <a name="what-do-i-need-to-pay-for"></a>我需要支付多少費用？

不須額外費用即可使用 Azure Migrate。 但在公開預覽期間，使用相依性視覺效果功能會產生額外費用。 為了支援[相依性視覺效果](concepts-dependency-visualization.md)，Azure Migrate 預設會建立 Log Analytics 工作區。 如果您使用相依性視覺效果，或使用 Azure Migrate 外部的工作區，您就必須支付工作區使用費用。 [深入了解](https://azure.microsoft.com/en-us/pricing/details/insight-analytics/)費用。 當服務正式運作時，即可免費使用相依性視覺效果功能。


## <a name="whats-in-an-assessment"></a>評估包含什麼？

評估可協助您識別內部部署 VM 的 Azure 適用性，取得在 Azure 中執行 VM 的適當大小建議和成本估計。 評估是以下表中摘要說明的屬性為基礎。 您可以在 Azure Migrate 入口網站中修改這些屬性。 

**屬性** | **詳細資料**
--- | ---
**目標位置** | 要作為移轉目的地的 Azure 位置。 根據預設，目標位置會設定為美國西部 2。 
**儲存體備援** | Azure VM 會在移轉之後使用的儲存體類型。 LRS 是預設值。
**價格方案** | 評估會考慮您是否已註冊軟體保證，並且可以使用 [Azure Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/)。 它也會考慮應該提供的 Azure 供應項目，並允許您指定經由供應項目取得的特定訂用帳戶折扣 (%)。 
**定價層** | 您可以指定 Azure VM 的[定價層 (基本/標準)](../virtual-machines/windows/sizes-general.md)。 根據您是否在生產環境中，協助您移轉至合適的 Azure VM 系列。 預設會使用[標準](../virtual-machines/windows/sizes-general.md)層。
**效能歷程記錄** | 根據預設，Azure Migrate 會使用一個月的歷程記錄 (95% 百分位數值) 評估內部部署機器的效能。 您可以修改此設定。
**緩和因數** | Azure Migrate 會在評估期間考慮緩衝區 (緩和因數)。 此緩衝區適用於 VM 的機器使用量資料 (CPU、記憶體、磁碟和網路)。 緩和因數會考量各個問題，例如季節性使用量、簡短的效能歷程記錄，以及未來可能增加的使用量。<br/><br/> 例如，10 個核心且 20% 使用率的 VM 通常會造成 2 個核心的 VM。 不過，如果緩和因數為 2.0 x，則結果為 4 個核心的 VM。 預設緩和設定為 1.3x。


## <a name="how-does-azure-migrate-work"></a>Azure Migrate 如何運作？

1.  您可建立 Azure Migrate 專案。
2.  Azure Migrate 會使用稱為收集器設備的內部部署 VM，探索您的內部部署機器相關資訊。 若要建立設備，您可下載開放虛擬化設備 (.ova) 格式的安裝檔案，然後將它匯入為內部部署 vCenter Sever 上的 VM。
3.  您在 vCenter Server 中使用主控台連線來連線到 VM，在連線時為 VM 指定新密碼，然後在 VM 中執行收集器應用程式來開始探索。
4.  收集器會使用 VMware PowerCLI Cmdlet 來收集 VM 中繼資料。 探索是無代理程式的，而且不會在 VMware 主機或 VM 上安裝任何項目。 所收集的中繼資料包含 VM 資訊 (核心、記憶體、磁碟、磁碟大小和網路介面卡。 它也會收集 VM 的效能資料，包括 CPU 和記憶體使用量、磁碟 IOPS、磁碟輸送量 (MBps) 以及網路輸出 (MBps)。
5.  中繼資料會推送至 Azure Migrate 專案。 您可以在 Azure 入口網站中檢視它。
6.  基於評估目的，您會將探索到的 VM 集合成群組。 例如，您可將執行相同應用程式的 VM 群組在一起。 如需更精確的群組，您可以使用相依性視覺效果來檢視特定機器的相依性，或檢視群組中所有機器的相依性並調整群組。
7.  在群組形成後，您可建立群組的評估。 
8.  評估完成後，您可以在入口網站中進行檢視，或以 Excel 格式進行下載。



  ![Azure Planner 架構](./media/migration-planner-overview/overview-1.png)

## <a name="what-are-the-port-requirements"></a>連接埠需求為何？

下表摘要說明 Azure Migrate 通訊所需的連接埠。

|元件          |通訊對象     |所需的連接埠  |原因   |
|-------------------|------------------------|---------------|---------|
|收集器          |Azure Migrate 服務   |TCP 443        |收集器會透過 SSL 連接埠 443 連線至服務|
|收集器          |vCenter Server          |預設值 9443   | 根據預設，收集器會連線到連接埠 9443 上的 vCenter Server。 如果伺服器接聽不同的連接埠，則應該設定為收集器 VM 上的傳出連接埠。 |
|內部部署 VM     | Operations Management Suite (OMS) 工作區          |[TCP 443](../log-analytics/log-analytics-windows-agent.md) |MMA 代理程式會使用 TCP 443 來連線到 Log Analytics。 如果您正在使用相依性視覺效果功能，且正在安裝 Microsoft Monitoring Agent (MMA) 代理程式，您只需要此連接埠。 |


  
## <a name="what-happens-after-assessment"></a>評估後會發生什麼事？

在評估內部部署機器以便使用 Azure Migrate 服務移轉之後，您可以使用一些工具來執行移轉：

- **Azure Site Recovery**：您可以使用 Azure Site Recovery 來移轉至 Azure，如下所示：
  - 準備 Azure 資源，包括 Azure 訂用帳戶、Azure 虛擬網路和儲存體帳戶。
  - 準備內部部署 VMware 伺服器以便移轉。 您可確認 Site Recovery 的 VMware 支援需求、準備 VMware 伺服器以供探索，以及準備在您想要移轉的 VM 上安裝 Site Recovery 行動服務。 
  - 設定移轉。 您可設定復原服務保存庫、設定來源和目標移轉設定、設定複寫原則，以及啟用複寫。 您可以執行災害復原演練，以檢查 VM 移轉至 Azure 是否運作正常。
  - 執行容錯移轉以將內部部署機器移轉至 Azure。 
  - 在 Site Recovery 移轉教學課程中[深入了解](../site-recovery/tutorial-migrate-on-premises-to-azure.md)。

- **Azure 資料庫移轉**：如果您的內部部署機器正在執行 SQL Server、MySQL 或 Oracle 等資料庫，您可以使用 Azure 資料庫移轉服務將資料庫移轉到 Azure。 [深入了解](https://azure.microsoft.com/campaigns/database-migration/)。



## <a name="next-steps"></a>後續步驟 
[請遵循教學課程](tutorial-assessment-vmware.md)，以建立內部部署 VMware VM 的評估。
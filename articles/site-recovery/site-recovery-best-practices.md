---
title: "aaaAzure 站台復原的最佳作法 |Microsoft 文件"
description: "本文說明 Azure Site Recovery 部署的最佳做法"
services: site-recovery
documentationCenter: 
author: rayne-wiselman"
manager: cfreeman
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-support-matrix-to-azure
ms.openlocfilehash: 288df858a0e1c1f5ad96dbe8b9dd0dc69d8f56ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-ready-toodeploy-azure-site-recovery"></a>取得準備 toodeploy Azure Site Recovery

本文說明如何部署 Azure 站台復原的 tooprepare。

## <a name="protecting-hyper-v-virtual-machines"></a>保護 Hyper-V 虛擬機器

您有一些保護 Hyper-V 虛擬機器的部署選項。 您可以複寫在內部部署 Hyper-v Vm tooAzure 或 tooa 次要資料中心。 每個部署有不同的需求。

**需求** | **複寫 tooAzure （使用 VMM)** | **複寫 HYPER-V Vm tooAzure (無 VMM)** | **複寫 HYPER-V Vm toosecondary 網站 （VMM)** | **詳細資料**
---|---|---|---|---
**VMM** | 在 System Center 2012 R2 上執行的 VMM <br/><br/>至少一個 VMM 雲端，其中包含一或多個 VMM 主機群組。 | NA | VMM hello 主要和次要站台的伺服器上至少執行 System Center 2012 SP1 含最新的更新。 <br/><br/> 每個 VMM 伺服器上至少一個雲端。 雲端應有 hello HYPER-V 容量設定檔集合。<br/><br/> hello 來源雲端應該有至少一個 VMM 主機群組。 | 選用。 您不需要 System Center VMM 部署在順序 tooreplicate HYPER-V 虛擬機器 tooAzure toohave，但如果您這樣做需要 toomake 確定 hello VMM 伺服器已正確設定。 包括確定您執行 hello 正確的 VMM 版本，並已設定雲端。
**Hyper-V** | Hello 在內部部署站台執行 Windows Server 2012 R2 中的至少一部 HYPER-V 主機伺服器或更新版本 | 至少一部 HYPER-V 伺服器 hello 來源和目標站台在至少執行 Windows Server 2012 與 hello 最新的更新安裝，且連線 toohello 網際網路。<br/><br/> hello HYPER-V 伺服器必須位於 VMM 雲端中的主機群組。 | 至少一部 HYPER-V 伺服器 hello 來源和目標站台在至少執行 Windows Server 2012 與 hello 最新的更新安裝，且連線 toohello 網際網路。<br/><br/> hello HYPER-V 伺服器必須位於 VMM 雲端中的主機群組。 |
**虛擬機器** | Hello 來源 HYPER-V 主機伺服器上的至少一個 VM | Hello 來源 VMM 雲端中的 hello HYPER-V 主機伺服器上的至少一個 VM | Hello 來源 VMM 雲端中的 hello HYPER-V 主機伺服器上的至少一個 VM。 |  Vm 複寫 tooAzure 必須符合 Azure 的虛擬機器必要條件
**Azure 帳戶** | 您將需要 Azure 帳戶和訂用帳戶 toohello Site Recovery 服務。 | 您將需要 Azure 帳戶和訂用帳戶 toohello Site Recovery 服務。 | NA | 如果您沒有帳戶，請先免費試用。
**Azure 儲存體** | 您會需要已啟用異地複寫之 Azure 儲存體帳戶的訂用帳戶。 | 您會需要已啟用異地複寫之 Azure 儲存體帳戶的訂用帳戶。 | NA | hello 帳戶應該位於 hello 與 hello Azure Site Recovery 保存庫相同的區域並 hello 與相關聯相同訂用帳戶。
**網路功能** | 設定網路對應 tooensure 容錯移轉的所有機器都 hello 相同的 Azure 網路可以連接 tooeach 其他，無論它們是在復原計劃。 此外，如果網路閘道是設定在 hello 目標 Azure 網路，虛擬機器可以連接 tooother 在內部部署虛擬機器。 如果您未設定網路對應，則在 hello 可以連線相同復原計劃中容錯移轉的機器。 | NA |  <br/><br/>設定網路對應 tooensure 虛擬機器容錯移轉之後，就會連接的 tooappropriate 網路，而且複本虛擬機器以最佳方式放置在 HYPER-V 主機伺服器上。 如果您未設定網路對應，複寫的機器將容錯移轉之後無法連接的 tooany VM 網路。 |  tooset 與 VMM 的網路對應，您將需要 toomake 確定 VMM 的邏輯和 VM 網路已正確設定。
**提供者和代理程式** | 在部署期間您將 VMM 伺服器上安裝 hello Azure Site Recovery Provider。 在 VMM 雲端中 HYPER-V 伺服器上，您將安裝 hello Azure 復原服務代理程式。 | 在部署期間將會同時安裝 hello Azure Site Recovery Provider 與 hello Azure 復原服務代理程式 hello HYPER-V 主機伺服器或叢集上| 在部署期間您將 VMM 伺服器上安裝 hello Azure Site Recovery Provider。 在 VMM 雲端中 HYPER-V 伺服器上，您將安裝 hello Azure 復原服務代理程式。 | 提供者和代理程式連接 tooSite 復原 hello 透過網際網路使用加密的 HTTPS 連線。 您不需要 tooadd 防火牆例外狀況，或建立 hello 提供者連接的特定 proxy。
**網際網路連線** | Hello VMM 伺服器需要網際網路連線 | 只有 hello HYPER-V 主機伺服器需要網際網路連線 | 只有 VMM 伺服器才需要網際網路連線 | 虛擬機器不需要在其上安裝的任何項目，並不直接連接 toohello 網際網路。



## <a name="protect-vmware-virtual-machines-or-physical-servers"></a>保護 VMware 虛擬機器或實體伺服器

您有一些保護 VMware 虛擬機器或 Windows/Linux 實體伺服器的部署選項。 您可以將它們複寫 tooAzure 或 tooa 次要資料中心。 每個部署有不同的需求。

**需求** | **複製 VMware Vm/實體伺服器 tooAzure)** | * **複製 VMware Vm/實體伺服器 toosecondary 站台**  
---|---|---
**主要網站** | **處理序伺服器**：專用的 Windows 伺服器 (實體或虛擬) | **處理序伺服器**：專用的 Windows 伺服器 (實體或 VMware 虛擬機器<br/><br/>  
**次要內部部署網站** | NA | **組態伺服器**：專用的 Windows 伺服器 (實體或虛擬) <br/><br/> **主要目標伺服器**：專用伺服器 (實體或虛擬)。 使用 Windows tooprotect Windows 電腦或 Linux tooprotect Linux 設定。
**Azure** | **訂用帳戶**: hello Site Recovery 服務需要訂用帳戶。 <br/><br/> **儲存體帳戶**：您需要已啟用異地複寫的儲存體帳戶。 hello 帳戶應該位於 hello 與 hello Site Recovery 保存庫相同的區域並 hello 與相關聯相同訂用帳戶。 <br/><br/> **設定伺服器**： 您將需要 tooset hello 組態伺服器，作為 Azure VM <br/><br/> **主要目標伺服器**： 您將需要 tooset hello 主要目標伺服器，作為 Azure VM <br/><br/> 使用 Windows tooprotect Windows 電腦或 Linux tooprotect Linux 設定。<br/><br/> **Azure 虛擬網路**： 您將需要哪些 hello 設定伺服器與主要目標伺服器將會部署在 Azure 虛擬網路。 Hello 中應該有相同的訂用帳戶和區域，所以 hello Azure Site Recovery 保存庫 | NA  
**虛擬機器/實體伺服器** | 至少一部 VMware 虛擬機器或實體 Windows/Linux 伺服器。<br/><br/>在部署期間將 hello 行動服務安裝在每部電腦| 至少一個 VMware VM 或實體 Windows/Linux 伺服器。<br/><br/> 在部署期間 hello 整合代理程式被安裝在每部電腦上。




## <a name="azure-virtual-machine-requirements"></a>Azure 虛擬機器需求

您可以部署站台復原 tooreplicate 虛擬機器和實體伺服器執行任何 Azure 所支援的作業系統。 這包括大部分的 Windows 和 Linux 版本。 您需要 toomake 確定在內部部署虛擬機器的 tooprotect 符合 Azure 需求。


## <a name="optimizing-your-deployment"></a>最佳化您的部署

使用下列秘訣 toohelp 最佳化，並調整您的部署的 hello。

- **作業系統磁碟區大小**： 當您將複寫操作系統磁碟區的虛擬機器 tooAzure hello 必須是小於 1 TB。 如果您有更多的磁碟區比此您可以手動將它們移 tooa 不同的磁碟在開始部署之前。
- **資料磁碟大小**： 如果您要複寫的 tooAzure 您可以向上 too32 資料磁碟上虛擬機器，每個都有最大值為 1 TB。 您可以有效地複寫及容錯移轉最多 32 TB 的虛擬機器。
- **復原計劃限制**： 站台復原可以調整 toothousands 的虛擬機器。 復原方案會設計為應該一起進行容錯移轉使我們限制復原計劃 too50 中機器的 hello 數目的應用程式的模型。
- **Azure 服務限制**：每個 Azure 訂用帳戶均隨附一組對核心、雲端服務等的預設限制。我們建議您在您的訂用帳戶中執行測試容錯移轉 toovalidate hello 可用性的資源。 您可以透過 Azure 支援修改這些限制。
- **容量規劃**︰規劃大小調整和效能。
- 複寫頻寬：如果您的複寫頻寬不足，請注意：
    - **ExpressRoute**：Site Recovery 可搭配 Azure ExpressRoute 和 WAN 最佳化工具，例如 Riverbed。
    - **複寫流量**: Site Recovery 會使用執行使用只會將資料區塊的智慧初始複寫，且不 hello 整個 VHD。 只會在複寫進行期間複寫變更。
    - **網路流量**： 您可以控制用來複寫的設定 Windows QoS 原則，根據 hello 目的地 IP 位址和連接埠的網路流量。  此外，如果您要複寫 tooAzure 站台復原使用 hello Azure Backup agent。 則您可以設定該代理程式的節流。
- **RTO**： 如果您想要 toomeasure hello 復原時間目標 (RTO) 您可以使用 Site Recovery 預期我們建議您執行測試容錯移轉及檢視 hello 站台復原作業 tooanalyze 多少時間花 toocomplete hello 作業。 如果您要容錯移轉 tooAzure，hello 最佳 RTO，我們建議您將所有的手動動作自動化藉由整合與 Azure 自動化和復原計劃。
- **RPO**: Site Recovery 在何時將複寫 tooAzure 支援接近同步的復原點目標 (RPO)。 這是假設您的資料中心與 Azure 之間有足夠的頻寬。

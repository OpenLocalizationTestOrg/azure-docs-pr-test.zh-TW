---
title: "aaaWhat 是 Azure Site Recovery？ | Microsoft Docs"
description: "提供 hello Azure Site Recovery 服務的概觀，並摘要說明部署案例。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: e9b97b00-0c92-4970-ae92-5166a4d43b68
ms.service: site-recovery
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: da6755654b8036a03314ec836f014b64428d5518
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-site-recovery"></a>什麼是 Site Recovery？

歡迎使用 toohello Azure Site Recovery 服務 ！ 本文章提供 hello 服務的快速概觀。

## <a name="business-continuity-and-disaster-recovery-bcdr-with-azure-recovery-services"></a>Azure 復原服務提供的業務持續性和災害復原 (BCDR)

做為組織中，您需要 toofigure 出如何將 tookeep 安全，您的資料和應用程式/工作負載執行計劃和未規劃的中斷發生。

Azure 復原服務參與 tooyour BCDR 策略：

- **Site Recovery 服務**：Site Recovery 可在網站關閉時讓您的應用程式持續在 VM 上執行，並保持實體伺服器可用，協助確保業務持續性。 Site Recovery 會複寫，讓它們依然在次要位置中如果 hello 主要站台無法使用，在 Vm 和實體伺服器上執行的工作負載。 它會復原工作負載 toohello 主要站台時的設定而定，再次執行。
- **備份服務**： 颾魤 ㄛ hello [Azure Backup](https://docs.microsoft.com/azure/backup/)服務用來儲存您的資料安全且更容易修復備份 tooAzure。

Site Recovery 可以管理複寫：

- 在 Azure 區域間複寫 Azure VM。
- 內部部署虛擬機器和實體伺服器複寫 tooAzure 或 tooa 次要站台。


## <a name="what-does-site-recovery-provide"></a>Site Recovery 可以提供什麼功能？

**功能** | **詳細資料**
--- | ---
**部署簡單的 BCDR 解決方案** | 使用站台復原，您可以設定，並從單一位置 hello Azure 入口網站中管理複寫、 容錯移轉和容錯回復。
**複寫 Azure VM** | 您可以設定 BCDR 策略，即可在 Azure 區域間複寫 Azure VM。
**異地複寫內部部署 VM** | 您可以複寫在內部部署 Vm 或實體伺服器 tooAzure tooa 次要內部部署位置。 複寫 tooAzure 排除 hello 成本和複雜度維護次要資料中心。
**複寫任何工作負載** | 複寫在支援的 Azure VM、內部部署 Hyper-V VM、VMware VM 和 Windows/Linux 實體伺服器上執行的任何工作負載。
**保持資料彈性及安全** | Site Recovery 會協調複寫，且無須攔截應用程式資料。 複寫的資料的 Azure 儲存體中儲存與提供的 hello 恢復功能。 容錯移轉發生時，Azure Vm 會根據建立 hello 複寫資料。
**符合 RTO 和 RPO** | 將復原時間目標 (RTO) 和復原點目標 (RPO) 保持在組織的限制範圍內。 Site Recovery 為 Azure VM 和 VMware VM 提供了連續複寫功能，並為 Hyper-V 提供最低 30 秒的複寫頻率。 您可以藉由與 [Azure 流量管理員](https://azure.microsoft.com/blog/reduce-rto-by-using-azure-traffic-manager-with-azure-site-recovery/)整合，進一步縮減復原時間目標 (RTO)。
**透過容錯移轉讓應用程式保持一致** | 您可以使用與應用程式一致的快照集設定復原點。 與應用程式一致的快照集會擷取磁碟資料、記憶體中的所有資料和處理序中的所有交易。
**測試不中斷** | 您可以輕鬆地執行測試容錯移轉 toosupport 災害復原演練，而不會影響進行中的複寫。
**執行彈性容錯移轉** | 您可以執行計劃性容錯移轉，因為是預期中的中斷，所以不會遺失任何資料；也可以執行非計劃性容錯移轉，以在發生未預期的災害時將資料損失減到最少 (取決於複寫頻率)。 再次可用時，您可以輕鬆地容錯回復 tooyour 主要站台。
**建立復原計劃** | 您可以透過復原計劃，自訂及排序多部 VM 上多層應用程式的容錯移轉和復原。 您要將計劃內的機器分組，並新增指令碼和手動動作。 復原計劃可以與 Azure 自動化 Runbook 整合。
**與現有的 BCDR 技術整合** | Site Recovery 與其他 BCDR 技術整合。 例如，您可以使用站台復原 tooprotect hello SQL Server 後端企業工作負載，包括 SQL Server AlwaysOn、 toomanage hello 容錯移轉可用性群組的原生支援。
**整合與 hello 自動化程式庫** | 豐富的 Azure Automation 文件庫，提供已可用於生產環境，且可下載並已經與 Site Recovery 整合的應用程式特定指令碼。
**管理網路設定** | Site Recovery 與 Azure 整合，提供簡單的應用程式網路管理，包括保留 IP 位址、設定負載平衡器和整合 Azure 流量管理員以進行有效率的網路轉換。


## <a name="what-can-i-replicate"></a>我可以複寫哪些項目？

**支援** | **詳細資料**
--- | ---
**我可以複寫哪些項目？** | Azure 區域間的 Azure VM (預覽)<br/><br/>  在內部部署 VMware Vm，HYPER-V Vm （Windows 和 Linux） 的實體伺服器 tooAzure < b /<br/> 內部部署 VMware Vm，HYPER-V Vm 的實體伺服器 tooa 次要站台。 HYPER-V vm 複寫 tooa 次要站台才支援如果 System Center VMM 所管理 HYPER-V 主機。
**Site Recovery 支援哪些區域？** | [支援區域](https://azure.microsoft.com/regions/services/) |
**複寫的機器需要哪些作業系統？** | [Azure 虛擬機器需求](site-recovery-support-matrix-azure-to-azure.md#support-for-replicated-machine-os-versions)s<br></br>[VMware 虛擬機器需求](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)<br/><br/> 如果是 Hyper-V VM，支援 Azure 和 Hyper-V 支援的所有[客體 OS](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows)。<br/><br/> [實體伺服器需求](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)
**我需要哪些 VMware 伺服器/主機？** | VMware VM 可以位於[支援的 vSphere 主機/vCenter 伺服器](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers)上
**可以複寫哪些工作負載？** | 您可以複寫在支援的複寫機器上執行的所有工作負載。 此外，hello Site Recovery 小組已執行應用程式專屬測試[應用程式的數字](site-recovery-workload.md#workload-summary)。


## <a name="azure-portal-considerations"></a>Azure 入口網站的考量

* 站台復原可以部署在 hello [Azure 入口網站](https://portal.azure.com)。
* Hello Azure 傳統入口網站，您可以管理站台復原 hello 傳統服務管理模型。
- hello 傳統入口網站只能使用的 toomaintain 現有站台復原部署。 您無法建立新的保存庫 hello 傳統入口網站中。

## <a name="next-steps"></a>後續步驟
* 深入了解[工作負載支援](site-recovery-workload.md)
* 開始使用[區域之間的 Azure VM 複寫](site-recovery-azure-to-azure.md)， [VMware 複寫 tooAzure](vmware-walkthrough-overview.md)，或[HYPER-V 複寫 tooAzure](hyper-v-site-walkthrough-overview.md)。

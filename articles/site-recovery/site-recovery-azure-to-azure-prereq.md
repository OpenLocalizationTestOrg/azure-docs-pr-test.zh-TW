---
title: "使用 Azure Site Recovery 的複寫 tooAzure 的 aaaPrerequisites |Microsoft 文件"
description: "本文摘要說明使用 hello Azure Site Recovery 服務複寫 Vm 和實體機器 tooAzure 的必要條件。"
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/01/2017
ms.author: rajanaki
ms.openlocfilehash: c66cea8b097a872bae57e7b42e659e58c4b0b1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replicating-azure-virtual-machines-tooanother-region-by-using-azure-site-recovery"></a>用來複寫使用 Azure Site Recovery 的 Azure 虛擬機器 tooanother 區域的必要條件

> [!div class="op_single_selector"]
> * [從 Azure tooAzure 複寫](site-recovery-azure-to-azure-prereq.md)
> * [從內部部署 tooAzure 複寫](site-recovery-prereq.md)

hello Azure Site Recovery 服務作為 tooyour 業務續航力和災害復原 (BCDR) 策略可藉由協調：
* Azure 虛擬機器 tooanother Azure 區域資料複寫。
* 在內部部署實體伺服器和虛擬機器 tooAzure 或 tooa 次要資料中心複寫。 

當您的主要位置發生中斷時，您可以容錯移轉 tooa 次要位置 tookeep 應用程式和可用的工作負載。 當它傳回 toonormal 作業，您可以容錯回復 tooyour 主要位置。 如需有關 Site Recovery 的詳細資訊，請參閱[什麼是 Site Recovery？](site-recovery-overview.md)。

本文摘要說明 hello 必要條件需要的 toobegin 內部 tooAzure 從站台復原複寫。

張貼在 hello hello 文章底部的任何註解或詢問技術問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="azure-requirements"></a>Azure 需求

**需求** | **詳細資料**
--- | ---
**Azure 帳戶** | [Microsoft Azure](http://azure.microsoft.com/) 帳戶。<br/><br/> 您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。
**Site Recovery 服務** | 如需有關 Site Recovery 價格的詳細資訊，請參閱 [Site Recovery 價格](https://azure.microsoft.com/pricing/details/site-recovery/)。 我們建議您復原服務保存庫中建立 hello 目標 Azure 地區的 toouse 做為災害復原位置。 比方說，如果在美國東部、 執行您的來源 Vm，而且您希望 tooreplicate tooCentral 我們，我們建議您在美國中部建立 hello 保存庫。|
**Azure 容量** | Hello 目標 Azure 地區的 toouse 做為災害復原位置，您需要 toohave 足夠容量的虛擬機器、 儲存體帳戶和網路元件的訂用帳戶。 您可以連絡支援 tooadd 容量。
**儲存體指引** | 請確定您遵循 hello[儲存體指引](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks)針對您的來源 Azure 虛擬機器 tooavoid 任何效能問題。 如果您遵循 hello 預設設定，站台復原就會建立所需的 hello hello 來源設定為基礎的儲存體帳戶。 如果您自訂，並選取您自己的設定，請確定您遵循 hello[虛擬機器磁碟的延展性目標](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks)。
**網路服務指南** | 針對特定的 Url 或 IP 範圍，您需要從 Azure VM toowhitelist hello 的傳出連線。 如需詳細資訊，請參閱 toohello[網路複寫 Azure 虛擬機器的指引](site-recovery-azure-to-azure-networking-guidance.md)發行項。
**Azure VM** | 確認所有 hello 最新的根憑證都會出現在 hello Windows 或 Linux VM 上。 如果 hello 最新的根憑證不存在，hello VM 不能註冊的 tooSite 復原，因為 toosecurity 條件約束。

>[!NOTE]
>如需支援的特定設定的詳細資訊，請參閱 hello[支援矩陣](site-recovery-support-matrix-azure-to-azure.md)。

## <a name="next-steps"></a>後續步驟
- 深入了解[複寫 Azure 虛擬機器的網路指引](site-recovery-azure-to-azure-networking-guidance.md)。
- [複寫 Azure 虛擬機器](site-recovery-azure-to-azure.md)來開始保護您的工作負載。

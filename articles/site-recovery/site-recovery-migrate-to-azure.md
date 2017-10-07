---
title: "使用站台復原 aaaMigrate tooAzure |Microsoft 文件"
description: "本文提供移轉的 Vm 和 Azure Site recovery 的實體伺服器 tooAzure 的概觀"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/05/2017
ms.author: raynew
ms.openlocfilehash: 6e65deee337c5371d441812ddb820dc8bc233684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-tooazure-with-site-recovery"></a>移轉與 Site Recovery tooAzure

閱讀本文如需使用 移轉虛擬機器和實體伺服器 hello Azure Site Recovery 服務。

站台復原是達成 tooyour BCDR 策略，來協調複寫在內部部署實體伺服器和虛擬機器 toohello 雲端 (Azure)，或 tooa 次要資料中心的 Azure 服務。 當您的主要位置發生中斷時，您容錯移轉 toohello 次要位置 tookeep 應用程式和可用的工作負載。 當它傳回 toonormal 作業，您就會容錯回復 tooyour 主要位置。 深入了解 [什麼是 Site Recovery？](site-recovery-overview.md) 您也可以使用站台復原 toomigrate 您現有的內部工作負載 tooAzure tooexpedite 您的雲端之旅和可用性 hello Azure 提供的功能的陣列。

如需快速概觀 tooperform 移轉 toothis 視訊，請參閱。
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/ASRHowTo-Video2-Migrate-Virtual-Machines-to-Azure/player]

本文說明部署中 hello [Azure 入口網站](https://portal.azure.com)。 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)可以使用的 toomaintain 現有站台復原保存庫，但您無法建立新的保存庫。

張貼在 hello 這篇文章底部的任何註解。 在 hello 詢問技術問題[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="what-do-we-mean-by-migration"></a>移轉的意思為何？

您可以部署站台復原的複寫在內部部署 Vm 和實體伺服器、 tooAzure 或 tooa 次要站台。 複寫機器，它們從容錯移轉 hello 主要站台的中斷發生的而且它會復原完成時將它們容錯回復 toohello 主要站台。 在加法 toothis，您可以使用站台復原 toomigrate Vm 和實體伺服器 tooAzure，讓使用者可以存取它們做為 Azure Vm。 移轉需要複寫和容錯移轉從 hello 主要站台 tooAzure 和完成移轉筆勢。

## <a name="what-can-site-recovery-migrate"></a>Site Recovery 可以移轉什麼項目？

您可以：

- 將 Azure Vm 上的內部部署 HYPER-V Vm、 VMware Vm 與實體伺服器、 toorun 上執行的工作負載的移轉。 在此案例中，您也可以執行完整的複寫和容錯回復。
- 在 Azure 區域之間移轉 [Azure IaaS VM](site-recovery-migrate-azure-to-azure.md)。 此案例目前只支援移轉，亦即不支援容錯回復。
- 移轉[AWS Windows 執行個體](site-recovery-migrate-aws-to-azure.md)tooAzure IaaS Vm。 此案例目前只支援移轉，亦即不支援容錯回復。

## <a name="migrate-on-premises-vms-and-physical-servers"></a>移轉內部部署 VM 和實體伺服器

toomigrate 內部部署 HYPER-V Vm、 VMware Vm 和實體伺服器，您可以遵循幾乎相同步驟所使用的一般複寫的 hello。

1. 設定復原服務保存庫
2. 設定所需的 hello 管理伺服器 (VMware，VMM 中，HYPER-V-取決於您想要 toomigrate)、 將它們加入 toohello 保存庫，並指定複寫設定。
3. 啟用複寫，對 hello 機器想 toomigrate
4. Hello 初始移轉之後，執行一切正常地快速測試容錯移轉 tooensure。
5. 確認複寫環境有用之後，您需要根據您的案例[所支援的項目](site-recovery-failover.md)使用計劃性或非計劃性容錯移轉。 我們建議您儘可能使用規劃的容錯移轉。
6. 如需移轉，您不需要 toocommit 容錯移轉時，或刪除它。 相反地，您可以選取 hello**完成移轉**選項要為每一部機器 toomigrate。
     - 在**複寫的項目**，以滑鼠右鍵按一下 hello VM，然後按一下**完成移轉**。 按一下**確定**toocomplete。 您也可以監視中的 hello 完成移轉作業中追蹤在 hello VM 屬性中，進度**站台復原工作**。
     - hello**完成移轉**動作完成 hello 移轉程序、 移除 hello 機器的複寫和停止 hello 機器的 Site Recovery 計費。

![完成移轉](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

## <a name="migrate-between-azure-regions"></a>在不同的 Azure 地區之間移轉

您可以使用 Site Recovery 在區域之間移轉 Azure VM。 此案例只支援移轉。 換句話說，您可以複寫 hello Azure Vm，並容錯 tooanother 區域，但您無法進行容錯回復。 在此案例中，您將設定復原服務保存庫，部署在內部部署組態伺服器 toomanage 複寫，將它加入 toohello 保存庫，並指定複寫設定。 針對您想 toomigrate，而且執行快速的 hello 機器測試容錯移轉，您可以啟用複寫。 然後您可以執行規劃的容錯移轉以 hello**完成移轉**選項。

## <a name="migrate-aws-tooazure"></a>移轉 AWS tooAzure

您可以移轉 AWS 執行個體 tooAzure Vm。 此案例只支援移轉。 換句話說，您可以將複寫 hello AWS 執行個體，並容錯 tooAzure，但您無法進行容錯回復。 AWS 執行個體以處理 hello 相同實體伺服器進行移轉的方式。 您設定 復原服務保存庫、 部署在內部部署組態伺服器 toomanage 複寫、 將它加入 toohello 保存庫，和指定的複寫設定。 針對您想 toomigrate，而且執行快速的 hello 機器測試容錯移轉，您可以啟用複寫。 然後您可以執行規劃的容錯移轉以 hello**完成移轉**選項。




## <a name="next-steps"></a>後續步驟

- [移轉 VMware Vm tooAzure](site-recovery-vmware-to-azure.md)
- [在 VMM 雲端 tooAzure 移轉 HYPER-V Vm](site-recovery-vmm-to-azure.md)
- [移轉 HYPER-V Vm 沒有 VMM tooAzure](site-recovery-hyper-v-site-to-azure.md)
- [在 Azure 區域之間移轉 Azure VM](site-recovery-migrate-azure-to-azure.md)
- [移轉 AWS 執行個體 tooAzure](site-recovery-migrate-aws-to-azure.md)
- [準備移轉的機器 tooenable 複寫](site-recovery-azure-to-azure-after-migration.md)tooanother 嚴重損壞修復所需的區域。
- [複寫 Azure 虛擬機器](site-recovery-azure-to-azure.md)來開始保護您的工作負載。

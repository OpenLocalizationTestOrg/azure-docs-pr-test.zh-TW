---
title: "從 AWS tooAzure aaaMigrate Vm |Microsoft 文件"
description: "本文說明如何 toomigrate 虛擬機器正在執行中使用 Azure Site Recovery 的 Amazon Web Services (AWS) tooAzure。"
services: site-recovery
documentationcenter: 
author: bsiva
manager: jwhit
editor: 
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: c99b781ec9cca5b8f9a847d3fc48408062b120b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a>將在 Amazon Web Services (AWS) tooAzure 與 Azure Site Recovery 的虛擬機器移轉

本文說明如何 toomigrate AWS Windows 執行個體 tooAzure 虛擬機器以 hello [Azure Site Recovery](site-recovery-overview.md)服務。

移轉實際上就是從 AWS tooAzure 的容錯移轉。 您不能容錯回復機器 tooAWS，而且沒有任何進行中的複寫。 本文描述 hello hello Azure 入口網站中針對移轉的步驟，並為基礎的 hello 指示[複寫實體機器 tooAzure](site-recovery-vmware-to-azure.md)。

將任何註解或問題張貼在本文中，或在 hello hello 下方[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

## <a name="supported-operating-systems"></a>受支援的作業系統

使用的 toomigrate EC2 情況下執行任何 hello 下列作業系統時，可能是站台復原：

- Windows (僅 64 位元)
    - Windows Server 2008 R2 SP1+ (僅限 Citrix PV 驅動程式或 AWS PV 驅動程式。 **不支援執行 RedHat PV 驅動程式的執行個體**) Windows Server 2012 Windows Server 2012 R2
- Linux (僅 64 位元)
    - Red Hat Enterprise Linux 6.7 (只有 HVM 虛擬化執行個體)

## <a name="prerequisites"></a>必要條件

以下是您針對此部署所需要的項目︰

* **設定伺服器**： 執行 Windows Server 2012 R2 的 Amazon EC2 VM 部署為 hello 組態伺服器。 根據預設，hello （處理序伺服器和主要目標伺服器） 的其他 Azure Site Recovery 元件會安裝部署 hello 組態伺服器時。 本文描述 hello hello Azure 入口網站中針對移轉的步驟，並為基礎的 hello 指示[進一步了解](site-recovery-components.md)

* **EC2 執行個體**: hello 的 toomigrate Amazon EC2 虛擬機器執行個體。

## <a name="deployment-steps"></a>部署步驟

1. 建立復原服務保存庫。
2. hello 安全性群組 EC2 的執行個體應該有您想 toomigrate 和您計劃 toodeploy hello 組態伺服器的 hello 執行個體的 hello EC2 執行個體之間設定的規則 tooallow 通訊。

3. 在 hello 相同 Amazon 虛擬私人雲端與您 EC2 執行個體，部署 ASR 組態伺服器。 請參閱 hello VMware / 實體 tooAzure 組態伺服器部署需求的必要條件。

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  一旦設定伺服器是部署在 AWS，並註冊您的復原服務保存庫，您應該看到 hello 組態伺服器和處理序伺服器在 Site Recovery 基礎結構，如下所示：

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. 您已部署的 hello 組態伺服器之後 (它可能會為其佔用 too15 minustes tooappear)，驗證，它可以您想 toomigrate 通訊與 hello Vm。

6. [設定複寫設定](site-recovery-setup-replication-settings-vmware.md)。

7. 啟用複寫： hello 想 toomigrate Vm 為啟用複寫。 您可以探索使用 hello 私用 IP 位址，您可以從 hello EC2 主控台取得 hello EC2 執行個體。

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. 一旦 hello EC2 執行個體已受保護且 hello 複寫 tooAzure 已完成，[執行測試容錯移轉](site-recovery-test-failover-to-azure.md)toovalidate 在 Azure 中的應用程式的效能。

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. 從 AWS tooAzure 執行容錯移轉，為每個 VM。 （選擇性） 您可以建立復原計劃及執行容錯移轉時，toomigrate AWS tooAzure 從多部虛擬機器。 [深入了解](site-recovery-create-recovery-plans.md) 復原計劃。

10. 如需移轉，您不需要 toocommit 容錯移轉。 相反地，您可以選取 hello 完成移轉選項要為每一部機器 toomigrate。 hello 完成移轉動作完成 hello 移轉程序、 移除 hello 機器的複寫和停止計費 hello 機器的 Site Recovery。

    ![移轉](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a>後續步驟

- [準備移轉的機器 tooenable 複寫](site-recovery-azure-to-azure-after-migration.md)tooanother 嚴重損壞修復所需的區域。
- [複寫 Azure 虛擬機器](site-recovery-azure-to-azure.md)來開始保護您的工作負載。

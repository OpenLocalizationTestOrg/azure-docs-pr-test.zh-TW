---
title: "aaaInstall hello VMware tooAzure 複寫的行動服務 |Microsoft 文件"
description: "本文說明如何 tooinstall hello VMware tooAzure 複寫 hello Azure Site Recovery 服務的行動服務代理程式。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: d3b7bc9c4d84d13317e0b0b47adcf38e8c41d0bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-install-hello-mobility-service"></a>步驟 10： 安裝 hello 行動服務


本文說明如何 tooconfigure 來源和目標設定複寫時 VMware 虛擬機器 tooAzure，使用內部 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。

hello 行動服務擷取的電腦上的資料寫入，並將它們轉送 toohello 處理序伺服器。 它應該安裝在每部電腦上您想 tooreplicate tooAzure。

您可以安裝 hello 行動服務手動啟用複寫時，使用從 hello 站台復原處理序伺服器推入安裝，或是使用 System Center Configuration Manager 的工具。 如果您使用推入安裝，hello 服務已安裝在 hello VM 上，啟用複寫時。

在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="install-manually"></a>手動安裝

1. 檢查 hello[必要條件](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites)進行手動安裝。
2. 請遵循[這些指示](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)進行手動安裝使用 hello 入口網站。
3. 如果您偏好 tooinstall 從 hello 命令列，請遵循[這些指示](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)。

## <a name="install-from-hello-process-server"></a>從 hello 處理序伺服器安裝

如果您想 toopush hello 行動服務安裝從 hello 處理序伺服器，當您啟用 VM 的複寫時，您需要可供 hello 處理序伺服器 tooaccess hello VM 的帳戶。 hello 帳戶僅用於 hello 推入安裝。

1. 您應該[已建立一個帳戶](vmware-walkthrough-prepare-vmware.md)來供推入安裝使用。 然後，您會指定您想要讓 toouse，當您設定來源站台復原 」 部署期間的 hello 帳戶。
2. 然後依照[這些指示](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)如果想要在執行 Windows 或 Linux Vm 上的 toopush hello 行動服務。

## <a name="other-methods"></a>其他方法

深入了解[安裝 hello 行動服務使用 Configuration Manager](site-recovery-install-mobility-service-using-sccm.md)，或使用[Azure Automation DSC](site-recovery-automate-mobility-service-install.md)。

## <a name="next-steps"></a>後續步驟

跳過[步驟 11： 啟用複寫](vmware-walkthrough-enable-replication.md)

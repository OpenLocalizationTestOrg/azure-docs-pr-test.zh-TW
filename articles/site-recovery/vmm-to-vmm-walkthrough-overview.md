---
title: "aaaReplicate HYPER-V Vm tooa 次要 VMM 站台與 Azure Site Recovery |Microsoft 文件"
description: "用來複寫 HYPER-V Vm tooa 次要 VMM 站台使用 hello Azure 入口網站提供的概觀。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 476ca82a-8f5c-4498-9dcf-e1011d60ed59
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 90e44bfc2237dfa7646fb2b7b1e533a7f6d83c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a>將 HYPER-V 虛擬機器在 VMM 雲端 tooa 次要 VMM 站台複寫

> [!div class="op_single_selector"]
> * [Azure 入口網站](site-recovery-vmm-to-vmm.md)
> * [傳統入口網站](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - 資源管理員](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

本文概述的 hello 需要 tooreplicate 內部管理次要 VMM 位置 tooa，System Center Virtual Machine Manager (VMM) 雲端中 HYPER-V 虛擬機器 (Vm) 的步驟，使用[Azure Site Recovery](site-recovery-overview.md)hello Azure 入口網站中。

閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="step-1-review-hello-scenario-architecture"></a>步驟 1： 檢閱 hello 案例架構

您開始部署，檢閱 hello 案例架構，並確定您了解所有 hello 元件必須先 toodeploy。

跳過[步驟 1： 檢閱 hello 架構](vmm-to-vmm-walkthrough-architecture.md)。

## <a name="step-2-review-prerequisites-and-limitations"></a>步驟 2：檢閱必要條件和限制

請確定您已了解 hello 部署必要條件和限制。

**Azure 的必要條件**： 您需要 Microsoft Azure 訂用帳戶和 Azure 復原服務保存庫 tooorchestrate 和管理複寫。
**內部部署 VMM 伺服器和 Hyper-V 主機**：請確定 VMM 伺服器和 Hyper-V 主機符合 Site Recovery 部署的必要條件並已準備就緒。

跳過[步驟 2： 確認必要條件和限制](vmm-to-vmm-walkthrough-prerequisites.md)。

## <a name="step-3-plan-networking"></a>步驟 3：規劃網路服務

您需要 toodo 規劃，您可以設定網路對應，當您部署的 hello 案例時，VMM VM 網路間的 tooensure 部分網路。

跳過[步驟 3： 規劃網路](vmm-to-vmm-walkthrough-network.md)。


## <a name="step-4-prepare-vmm-and-hyper-v"></a>步驟 4：準備 VMM 和 Hyper-V

準備站台復原 」 部署的 hello VMM 伺服器和 HYPER-V 主機。

跳過[步驟 4： 準備內部部署伺服器](vmm-to-vmm-walkthrough-vmm-hyper-v.md)。

## <a name="step-5-set-up-a-vault"></a>步驟 5：設定保存庫

設定復原服務保存庫。 hello 保存庫包含組態設定，並且會協調複寫。

[步驟 5：設定保存庫](vmm-to-vmm-walkthrough-create-vault.md)。

## <a name="step-6-set-up-source-and-target-settings"></a>步驟 6：設定來源和目標設定

設定 hello 來源和目標複寫 VMM 位置。 新增 hello VMM 伺服器 toohello 保存庫，並下載 Site Recovery 元件的 hello 安裝檔案。 Hello VMM 伺服器上執行 Azure Site Recovery Provider 安裝程式。 安裝程式會在 hello VMM 伺服器上，安裝 hello 提供者，並登錄 hello 伺服器 hello 保存庫中。 您每個 HYPER-V 主機上安裝 hello Microsoft 復原服務代理程式。

跳過[步驟 6： 設定 hello 來源和目標設定](vmm-to-vmm-walkthrough-source-target.md)。

## <a name="step-7-configure-network-mapping"></a>步驟 7：設定網路對應

VMM 的 VM 網路對應 hello 來源和目標位置中。 容錯移轉之後，Vm 會在建立 hello 目標網路中的 hello 來源 HYPER-V 虛擬機器位於該對應 toohello 來源 VM 網路。

跳過[步驟 7： 設定網路對應](vmm-to-vmm-walkthrough-network-mapping.md)。


## <a name="step-8-set-up-a-replication-policy"></a>步驟 8：設定複寫原則

指定 VM 在 VMM 位置之間的複寫方式。

跳過[步驟 8： 設定複寫原則](vmm-to-vmm-walkthrough-replication.md)。


## <a name="step-9-enable-replication-for-vms"></a>步驟 9：啟用 VM 複寫

選取您想要 tooreplicate hello Vm。 啟用複寫觸發程序 hello 初始複寫 toohello 次要站台的 VM，後面接著進行中的差異複寫。

跳過[步驟 9： 啟用複寫](vmm-to-vmm-walkthrough-enable-replication.md)。


## <a name="step-10-run-a-test-failover"></a>步驟 10：執行測試容錯移轉

執行測試容錯移轉 toomake 確定一切如預期般運作。

跳過[步驟 10： 執行測試容錯移轉](vmm-to-vmm-walkthrough-test-failover.md)。

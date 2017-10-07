---
title: "aaaReplicate 在 VMM 中的 HYPER-V Vm 雲端與 Azure Site Recovery tooAzure |Microsoft 文件"
description: "提供用來複寫 VMM 雲端 tooAzure 使用 hello Azure Site Recovery 服務中的 HYPER-V Vm 的概觀"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: d6f729a49cc86ea07bebc4d7266fd7b58b3998f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a>複寫 HYPER-V 虛擬機器在 VMM 雲端 tooAzure hello Azure 入口網站中使用站台復原中
> [!div class="op_single_selector"]
> * [Azure 入口網站](site-recovery-vmm-to-azure.md)
> * [Azure 傳統型](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [PowerShell 傳統](site-recovery-deploy-with-powershell.md)


本文章提供概觀 hello 步驟需要 tooreplicate 內部部署 HYPER-V 虛擬機器 (Vm) 管理 System Center Virtual Machine Manager (VMM) 雲端 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md)服務hello Azure 入口網站。

閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="step-1-review-hello-scenario-architecture"></a>步驟 1： 檢閱 hello 案例架構

您開始部署，檢閱 hello 案例架構，並確定您了解所有 hello 元件必須先 toodeploy。

跳過[步驟 1： 檢閱 hello 架構](vmm-to-azure-walkthrough-architecture.md)

## <a name="step-2-review-prerequisites-and-limitations"></a>步驟 2：檢閱必要條件和限制

請確定您已了解 hello 部署必要條件和限制。

**Azure 必要條件**：您需要 Microsoft Azure 帳戶、Azure 網路及儲存體帳戶。
**內部部署 VMM 伺服器和 Hyper-V 主機**：請確定 VMM 伺服器和 Hyper-V 主機符合 Site Recovery 部署的必要條件並已準備就緒。
**複寫 Vm**： 核取您想要 tooreplicate Vm 符合 Azure 需求。

跳過[步驟 2： 確認必要條件和限制](vmm-to-azure-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>步驟 3：規劃容量

如果您進行完整部署，您會需要 toofigure 出您需要哪些複寫資源。 有幾個的工具可用 toohelp 這麼做。 如果您進行快速設定 tootest hello 環境，您可以略過此步驟。

跳過[步驟 3： 規劃容量](vmm-to-azure-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>步驟 4：規劃網路

您需要 toodo 某些網路規劃 tooensure，您可以設定網路對應，當您部署的 hello 案例中，Azure Vm 將會連接的 tooAzure 虛擬網路之後發生容錯移轉，以及它們要指派適當的 IP 位址。

跳過[步驟 4： 規劃的網路功能](vmm-to-azure-walkthrough-network.md)


## <a name="step-5-prepare-azure-resources"></a>步驟 5：準備 Azure 資源

設定 Azure 帳戶、網路和儲存體。 您可以在部署期間執行這項操作，但建議您在開始之前進行。

跳過[步驟 5： 準備 Azure](vmm-to-azure-walkthrough-prepare-azure.md)

## <a name="step-6-prepare-vmm-and-hyper-v"></a>步驟 6：準備 VMM 和 Hyper-V

準備站台復原 」 部署的 hello 在內部部署 VMM 伺服器和 HYPER-V 主機。

跳過[步驟 6： 準備內部部署伺服器](vmm-to-azure-walkthrough-vmm-hyper-v.md)

## <a name="step-7-set-up-a-vault"></a>步驟 7：設定保存庫

設定復原服務保存庫。 hello 保存庫包含組態設定，並且會協調複寫。

[步驟 7：設定保存庫](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>步驟 8：設定來源和目標設定

設定 hello 來源和目標複寫的位置。 新增 hello VMM 伺服器 toohello 保存庫，並下載 Site Recovery 元件的 hello 安裝檔案。 Hello VMM 伺服器上執行 Azure Site Recovery Provider 安裝程式。 安裝程式會在 hello VMM 伺服器上，安裝 hello 提供者，並登錄 hello 伺服器 hello 保存庫中。 您每個 HYPER-V 主機上安裝 hello Microsoft 復原服務代理程式。

跳過[步驟 8： 來源和目標設定](vmm-to-azure-walkthrough-source-target.md)

## <a name="step-9-configure-network-mapping"></a>步驟 9：設定網路對應

對應內部部署 VMM VM 網路 tooAzure 虛擬網路。 容錯移轉之後，Azure Vm 中建立 hello 對應 toohello 在內部部署的 VM 網路中的 hello 來源 HYPER-V 所在的 Azure 網路。

跳過[步驟 9： 設定網路對應](vmm-to-azure-walkthrough-network-mapping.md)


## <a name="step-10-set-up-a-replication-policy"></a>步驟 10：設定複寫原則

指定如何在內部部署 Vm 會複寫的 tooAzure。

跳過[步驟 10： 設定複寫原則](vmm-to-azure-walkthrough-replication.md)


## <a name="step-11-enable-replication-for-vms"></a>步驟 11：啟用 VM 複寫

選取您想要 tooreplicate hello Vm。 啟用複寫觸發程序 hello 初始複寫 tooAzure 的 VM，後面接著進行中的差異複寫。

跳過[步驟 11： 啟用複寫](vmm-to-azure-walkthrough-enable-replication.md)


## <a name="step-12-run-a-test-failover"></a>步驟 12：執行測試容錯移轉

執行測試容錯移轉 toomake 確定一切如預期般運作。

跳過[步驟 12： 執行測試容錯移轉](vmm-to-azure-walkthrough-test-failover.md)



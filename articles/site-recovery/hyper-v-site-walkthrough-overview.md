---
title: "使用 Azure Site Recovery aaaReplicate HYPER-V Vm tooAzure |Microsoft 文件"
description: "描述如何 tooorchestrate 複寫、 容錯移轉和復原的內部部署 Hyper-v-V Vm tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: efddd986-bc13-4a1d-932d-5484cdc7ad8d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: ab9cd14149ef32a416428d0f4327aa18b042e9c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure"></a>複寫 HYPER-V 虛擬機器 （無 VMM) tooAzure 

> [!div class="op_single_selector"]
> * [Azure 入口網站](site-recovery-hyper-v-site-to-azure.md)
> * [Azure 傳統型](site-recovery-hyper-v-site-to-azure-classic.md)
> * [PowerShell - 資源管理員](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

本文概述 hello 所需步驟 tooreplicate 在內部部署 HYPER-V 虛擬機器 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中。 在此部署中，Hyper-V VM 並非由 System Center Virtual Machine Manager (VMM) 所管理。


閱讀這篇文章之後, 張貼的任何註解底部 hello 或詢問技術問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="step-1-review-architecture-and-prerequisites"></a>步驟 1：檢閱架構和必要條件

在開始部署之前，檢閱 hello 案例架構，並確定您了解您需要 toodeploy 所有 hello 元件

跳過[步驟 1： 檢閱 hello 架構](hyper-v-site-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>步驟 2：檢閱必要條件

請確定您具備 hello 必要條件以便於部署的每個元件：

- **Azure 必要條件**：您需要 Microsoft Azure 帳戶、Azure 網路及儲存體帳戶。
- **內部部署 Hyper-V 必要條件**：請確定備妥 Hyper-V 主機可進行 Site Recovery 部署。
- **複寫 Vm**： 您想要 tooreplicate 需要 toocomply Azure 需求的 Vm。

跳過[步驟 2： 確認必要條件和限制](hyper-v-site-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>步驟 3：規劃容量

如果您進行完整部署需要 toofigure 出您需要哪些複寫資源。 有幾個的工具可用 toohelp 這麼做。 移 tooStep 2。 如果您進行快速設定 tootest hello 環境可以略過此步驟。

跳過[步驟 3： 規劃容量](hyper-v-site-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>步驟 4：規劃網路

您需要 toodo 規劃 tooensure Azure Vm 就會發生容錯移轉之後連接的 toonetworks 和確認他們已擁有 hello 正確 IP 位址，某些網路。

跳過[步驟 4： 規劃的網路功能](hyper-v-site-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>步驟 5：準備 Azure 資源

在開始之前，請先設定 Azure 網路和儲存體。 您可以在部署期間執行這項操作，但建議您在開始之前進行。

跳過[步驟 5： 準備 Azure](hyper-v-site-walkthrough-prepare-azure.md)


## <a name="step-6-prepare-hyper-v"></a>步驟 6：準備 Hyper-V

請確定 Hyper-V 伺服器符合 Site Recovery 部署需求。

跳過[步驟 6： 準備 HYPER-V](hyper-v-site-walkthrough-prepare-hyper-v.md)

## <a name="step-7-set-up-a-vault"></a>步驟 7：設定保存庫

您需要註冊復原服務保存庫 tooorchestrate tooset 和管理複寫。 當您設定 hello 保存庫時，指定您想要 tooreplicate，以及您希望 tooreplicate 它。

跳過[步驟 7： 建立保存庫](hyper-v-site-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>步驟 8：設定來源和目標設定

設定 hello 來源和目標使用，可用於複寫。 設定來源設定，包括新增 HYPER-V 主機 tooa HYPER-V 網站時，每個 HYPER-V 主機上，安裝 hello Site Recovery 提供者和復原服務代理程式和 hello 復原服務保存庫中註冊 hello 站台。

跳過[步驟 8: hello 來源和目標設定](hyper-v-site-walkthrough-source-target.md)

## <a name="step-9-set-up-a-replication-policy"></a>步驟 9：設定複寫原則

您設定原則 toospecify 複寫設定的 HYPER-V Vm hello 保存庫中。

跳過[步驟 9： 設定複寫原則](hyper-v-site-walkthrough-replication.md)


## <a name="step-10-enable-replication"></a>步驟 10：啟用複寫

您已備妥，複寫原則之後啟用之後，就會發生 hello VM 的初始複寫。

跳過[步驟 10： 啟用複寫](hyper-v-site-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>步驟 11：執行測試容錯移轉

初始複寫完成，並執行差異複寫之後，您可以執行測試容錯移轉 toomake 確定一切如預期運作。

跳過[步驟 11： 執行測試容錯移轉](hyper-v-site-walkthrough-test-failover.md)

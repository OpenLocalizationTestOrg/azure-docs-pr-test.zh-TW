---
title: "使用 Azure Site Recovery aaaReplicate VMware Vm tooAzure |Microsoft 文件"
description: "提供用來複寫 tooAzure VMware Vm 上執行工作負載的 hello 步驟的概觀"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 7104f67a3635b916048dcb61bca770c89f0c77fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-vms-tooazure-with-site-recovery"></a>複寫與站台復原的 VMware Vm tooAzure

本文概述 hello 步驟需要的 tooreplicate 在內部部署 VMware 虛擬機器 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。


![部署程序](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

**圖 1：部署程序摘要**

## <a name="step-1-review-architecture-and-prerequisites"></a>步驟 1：檢閱架構和必要條件

在開始部署之前，檢閱 hello 案例架構，並確定您了解您需要 toodeploy 所有 hello 元件

跳過[步驟 1： 檢閱 hello 架構](vmware-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>步驟 2：檢閱必要條件

請確定您具備 hello 必要條件以便於部署的每個元件：

- **Azure 必要條件**：您需要 Microsoft Azure 帳戶、Azure 網路及儲存體帳戶。
- **內部部署 Site Recovery 元件**：您需要有一部執行內部部署 Site Recovery 元件的機器。
- **在內部部署 VMware 必要條件**： 您需要 tooset 帳戶以便 VMware 伺服器和 Vm，可以存取站台復原。
- **複寫 Vm**: Vm tooreplicate 需要 toocomply Azure 需求，並安裝 hello 行動服務元件。

跳過[步驟 2： 檢閱必要條件和限制](vmware-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>步驟 3：規劃容量

如果您進行完整部署需要 toofigure 出您需要哪些複寫資源。 有幾個的工具可用 toohelp 這麼做。 移 tooStep 2。 如果您進行快速設定 tootest hello 環境可以略過此步驟。

跳過[步驟 3： 規劃容量](vmware-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>步驟 4：規劃網路

您需要 toodo 規劃 tooensure Azure Vm 就會發生容錯移轉之後連接的 toonetworks 和確認他們已擁有 hello 正確 IP 位址，某些網路。

跳過[步驟 4： 規劃的網路功能](vmware-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>步驟 5：準備 Azure 資源

在開始之前，請先設定 Azure 網路和儲存體。 您可以在部署期間執行這項操作，但建議您在開始之前進行。

跳過[步驟 5： 準備 Azure](vmware-walkthrough-prepare-azure.md)


## <a name="step-6-prepare-vmware"></a>步驟 6：準備 VMware

您需要 tooset 帳戶將用於站台復原：

- 存取 VMware 虛擬化伺服器 tooautomatically 偵測到 Vm。
- 存取 Vm tooinstall hello 行動服務。 每個的 VM，您想要 tooreplicate 必須擁有 hello 行動服務代理程式安裝之前，您可以啟用複寫功能。

跳過[步驟 6： 準備 VMware](vmware-walkthrough-prepare-vmware.md)

## <a name="step-7-set-up-a-vault"></a>步驟 7：設定保存庫

您需要註冊復原服務保存庫 tooorchestrate tooset 和管理複寫。 當您設定 hello 保存庫時，指定您想要 tooreplicate，以及您希望 tooreplicate 它。

跳過[步驟 7： 設定保存庫](vmware-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>步驟 8：設定來源和目標設定

設定 hello 來源和目標使用，可用於複寫。 來源設定的設定包含執行整合安裝 tooinstall hello 在內部部署站台復原元件。

跳過[步驟 8: hello 來源和目標設定](vmware-walkthrough-source-target.md)

## <a name="step-9-set-up-a-replication-policy"></a>步驟 9：設定複寫原則

您設定原則 toospecify 複寫設定 VMware vm hello 保存庫中。

跳過[步驟 9： 設定複寫原則](vmware-walkthrough-replication.md)

## <a name="step-10-install-hello-mobility-service"></a>步驟 10： 安裝 hello 行動服務

必須安裝行動服務的 hello 想在每個 VM 上 tooreplicate。 有幾個方式 tooset hello 與發送或提取安裝的服務。

跳過[步驟 10： 安裝 hello 行動服務](vmware-walkthrough-install-mobility.md)

## <a name="step-11-enable-replication"></a>步驟 11：啟用複寫

Hello 行動服務在 VM 上執行之後，您可以啟用複寫功能。 啟用之後，就會發生 hello VM 的初始複寫。

跳過[步驟 11： 啟用複寫](vmware-walkthrough-enable-replication.md)

## <a name="step-12-run-a-test-failover"></a>步驟 12：執行測試容錯移轉

初始複寫完成，並執行差異複寫之後，您可以執行測試容錯移轉 toomake 確定一切如預期運作。

跳過[步驟 12： 執行測試容錯移轉](vmware-walkthrough-test-failover.md)

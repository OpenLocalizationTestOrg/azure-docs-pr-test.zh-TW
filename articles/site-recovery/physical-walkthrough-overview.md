---
title: "aaaReplicate 實體內部部署伺服器與 Azure Site Recovery 的 tooAzure |Microsoft 文件"
description: "複寫在內部部署 Windows/Linux 實體伺服器 tooAzure 以 hello Azure Site Recovery 服務上執行工作負載提供 hello 步驟的概觀。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a>複寫與站台復原的實體伺服器 tooAzure

本文概述 hello 步驟需要的 tooreplicate 在內部部署 Windows/Linux 實體伺服器 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。


## <a name="step-1-review-architecture-and-prerequisites"></a>步驟 1：檢閱架構和必要條件

在開始部署之前，檢閱 hello 案例架構，並確定您了解所有您需要 tooset hello 部署的 hello 元件。

跳過[步驟 1： 檢閱 hello 架構](physical-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>步驟 2：檢閱必要條件

請確定您具備 hello 必要條件以便於部署的每個元件：

- **Azure 必要條件**：您需要 Microsoft Azure 帳戶、Azure 網路及儲存體帳戶。
- **內部部署 Site Recovery 元件**：您需要有一部執行內部部署 Site Recovery 元件的機器。
- **複寫機器**： 您想 tooreplicate 伺服器需要 toocomply 在內部部署與 Azure 需求。

跳過[步驟 2： 檢閱必要條件和限制](physical-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>步驟 3：規劃容量

如果您進行完整部署需要 toofigure 出您需要哪些複寫資源。 如果您進行快速設定 tootest hello 環境，您可以略過此步驟。

跳過[步驟 3： 規劃容量](physical-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>步驟 4：規劃網路

您需要 toodo 規劃 tooensure Azure Vm 就會發生容錯移轉之後連接的 toonetworks 和確認他們已擁有 hello 正確 IP 位址，某些網路。

跳過[步驟 4： 規劃的網路功能](physical-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>步驟 5：準備 Azure 資源

在開始之前，請先設定 Azure 網路和儲存體。 

跳過[步驟 5： 準備 Azure](physical-walkthrough-prepare-azure.md)


## <a name="step-6-set-up-a-vault"></a>步驟 6：設定保存庫

您可以設定 復原服務保存庫 tooorchestrate 和管理複寫。 當您設定 hello 保存庫時，指定您想要 tooreplicate，以及您希望 tooreplicate 它。

跳過[步驟 6： 設定保存庫](physical-walkthrough-create-vault.md)

## <a name="step-7-configure-source-and-target-settings"></a>步驟 7：設定來源和目標設定

設定 hello 來源和目標 (Azure) 的站台。 來源設定包含執行整合安裝 tooinstall hello 在內部部署站台復原元件。

跳過[步驟 7： 設定 hello 來源和目標](physical-walkthrough-source-target.md)

## <a name="step-8-set-up-a-replication-policy"></a>步驟 8：設定複寫原則

您設定原則 toospecify 如何實體伺服器應該將複寫。

跳過[步驟 8： 設定複寫原則](physical-walkthrough-replication.md)

## <a name="step-9-install-hello-mobility-service"></a>步驟 9： 安裝 hello 行動服務

必須安裝行動服務的 hello 想 tooreplicate 在每一部伺服器上。 有幾個方式 tooset hello 服務，與發送或提取的安裝。

跳過[步驟 9： 安裝 hello 行動服務](physical-walkthrough-install-mobility.md)

## <a name="step-10-enable-replication"></a>步驟 10：啟用複寫

Hello 行動服務正在伺服器上執行之後，您可以啟用複寫功能。 啟用之後，就會發生 hello VM 的初始複寫。

跳過[步驟 10： 啟用複寫](physical-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>步驟 11：執行測試容錯移轉

初始複寫完成，並執行差異複寫之後，您可以執行測試容錯移轉 toomake 確定一切如預期運作。

跳過[步驟 11： 執行測試容錯移轉](physical-walkthrough-test-failover.md)


---
title: "Azure 的區域之間的 Azure Vm aaaReplicate |Microsoft 文件 '"
description: "摘要說明 hello 步驟需要的 tooreplicate Azure Vm 與 hello Azure 入口網站中的 hello Azure Site Recovery 服務的 Azure 區域之間"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 6dd36239-4363-4538-bf80-a18e71b8ec67
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: f4ac386f040945131f8a10f02143437f4441e298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a>使用 Azure Site Recovery 在區域之間椱寫 Azure VM

>本文章提供 Azure 虛擬機器 (Vm) 在一個 Azure 區域 tooAzure Vm 位於不同的區域中的 hello 步驟需要 tooreplicate 的概觀。 

>[!NOTE]
>
> Azure VM 複寫目前為預覽狀態。

在這份文件或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="step-1-review-architecture"></a>步驟 1：檢閱架構

在開始部署之前，檢閱 hello 案例架構和您需要 toodeploy hello 元件。

跳過[步驟 1： 檢閱 hello 架構](azure-to-azure-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>步驟 2：檢閱必要條件

請檢查您擁有 hello Azure 位置，包括訂用帳戶、 虛擬網路、 儲存體帳戶和 VM 需求中的必要條件。

跳過[步驟 2： 確認必要條件和限制](azure-to-azure-walkthrough-prerequisites.md)


## <a name="step-3-plan-networking"></a>步驟 3：規劃網路服務

請檢查要 tooreplicate，以及從內部部署連線所設定的 Azure Vm 上的傳出連線已設定。

跳過[步驟 4： 規劃的網路功能](azure-to-azure-walkthrough-network.md)



## <a name="step-4-create-a-vault"></a>步驟 4：建立保存庫 

您需要註冊復原服務保存庫 tooorchestrate tooset 和管理複寫，並指定 hello 來源地區。

跳過[步驟 4： 建立保存庫](azure-to-azure-walkthrough-vault.md)


## <a name="step-5-enable-replication"></a>步驟 5：啟用複寫


tooenable 複寫，您設定目標位置設定，設定複寫原則，並選取您想 tooreplicate hello Azure Vm。 啟用之後，就會發生 hello VM 的初始複寫。

跳過[步驟 5： 啟用複寫](azure-to-azure-walkthrough-enable-replication.md)


## <a name="step-6-run-a-test-failover"></a>步驟 6：執行測試容錯移轉

初始複寫完成，並執行差異複寫之後，您可以執行測試容錯移轉 toomake 確定一切如預期運作。

跳過[步驟 6： 執行測試容錯移轉](azure-to-azure-walkthrough-test-failover.md)



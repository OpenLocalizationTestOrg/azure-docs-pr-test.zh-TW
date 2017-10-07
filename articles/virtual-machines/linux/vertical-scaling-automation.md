---
title: "aaaVertically 小數位數與 Azure 自動化的 Azure 虛擬機器 |Microsoft 文件"
description: "如何 toovertically 調整回應 toomonitoring 警示與 Azure 自動化中的 Linux 虛擬機器"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dcee199e-fa25-44d5-9b25-df564cee9b45
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: singhkay
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee4c1c33a588bd907d107f1828380a8afdaa725e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-azure-linux-virtual-machine-with-azure-automation"></a>使用 Azure 自動化來垂直調整 Azure Linux 虛擬機器
垂直延展是增加或減少回應 toohello 工作負載中電腦的 hello 資源 hello 程序。 在 Azure 中達成這點可以藉由變更 hello hello 虛擬機器大小。 這可協助在下列案例的 hello

* 如果未使用經常 hello 虛擬機器，可以調整 tooa 較小的大小 tooreduce 向您的每月成本
* 如果 hello 虛擬機器會看見尖峰負載，它可以是調整過大小的 tooa 較大的大小 tooincrease 其容量

這是與 hello 步驟 tooaccomplish 的 hello 大綱下方

1. 設定 Azure 自動化 tooaccess 虛擬機器
2. Hello 垂直延展的 Azure 自動化 runbook 匯入您的訂用帳戶
3. 加入 webhook tooyour runbook
4. 新增警示 tooyour 虛擬機器

> [!NOTE]
> 因為 hello hello 大小而第一個虛擬機器，它可以調整，以 hello 大小可能會有所限制到期的 hello toohello 可用性 hello 叢集中其他大小目前部署虛擬機器中。 在 hello 發行我們處理此情況下，只調整 VM 大小組下方 hello 內這篇文章中使用自動化 runbook。 這表示不突然將 tooStandard_G5 來擴充或縮小 tooBasic_A0 Standard_D1v2 虛擬機器。
> 
> | 成對的調整 VM 大小 |  |
> | --- | --- |
> | Basic_A0 |Basic_A4 |
> | Standard_A0 |Standard_A4 |
> | Standard_A5 |Standard_A7 |
> | Standard_A8 |Standard_A9 |
> | Standard_A10 |Standard_A11 |
> | 標準_D1 |標準_D4 |
> | 標準_D11 |標準_D14 |
> | Standard_DS1 |Standard_DS4 |
> | Standard_DS11 |Standard_DS14 |
> | Standard_D1v2 |Standard_D5v2 |
> | Standard_D11v2 |Standard_D14v2 |
> | Standard_G1 |Standard_G5 |
> | Standard_GS1 |Standard_GS5 |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a>設定 Azure 自動化 tooaccess 虛擬機器
您需要 toodo hello 第一件事是建立 Azure 自動化帳戶將裝載 hello runbook 使用 tooscale hello VM 規模調整集合執行個體。 最近 hello 自動化服務導入了 hello 「 執行身分帳戶 」 功能會自動執行 hello runbook 代表 hello 使用者很容易讓 hello 服務主體的設定。 閱讀更多關於此 hello 的下列文件中：

* [使用 Azure 執行身分帳戶驗證 Runbook](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>Hello 垂直延展的 Azure 自動化 runbook 匯入您的訂用帳戶
所需的垂直調整您的虛擬機器已經發行 hello Azure 自動化 Runbook 資源庫中的 hello runbook。 您將需要 tooimport 為您的訂用帳戶。 您可以了解如何藉由讀取 tooimport runbook hello 下列文章。

* [Azure 自動化的 Runbook 和模組資源庫](../../automation/automation-runbook-gallery.md)

需要 toobe 匯入的 hello runbook 所示 hello 圖

![匯入 Runbook](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a>加入 webhook tooyour runbook
您已匯入 hello runbook 之後您將需要 tooadd webhook toohello runbook，如此可藉由從虛擬機器警示。 為您的 Runbook 建立 webhook hello 詳細資料可以在這裡

* [Azure 自動化 Webhook](../../automation/automation-webhooks.md)

請確定您複製 hello webhook 之後才關閉 hello webhook 對話方塊，將會需要這個 hello 下一節。

## <a name="add-an-alert-tooyour-virtual-machine"></a>新增警示 tooyour 虛擬機器
1. 選取虛擬機器設定
2. 選取 [警示規則]
3. 選取 [加入警示]
4. 在選取度量 toofire hello 警示
5. 選取條件，當完成將導致 hello 警示 toofire
6. 選取在步驟 5 中的 hello 條件的臨界值。 toobe 完成
7. 在步驟 5 和 6 選取的期間透過哪一個 hello 監視服務會檢查 hello 條件和臨界值
8. 貼上您複製 hello 前一節的 hello webhook。

![新增警示 tooVirtual 機器 1](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![新增警示 tooVirtual 機器 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)


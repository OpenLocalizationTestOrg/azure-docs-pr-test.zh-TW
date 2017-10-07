---
title: "aaaSubscription 和適用於 Windows Vm 在 Azure 中的帳戶 |Microsoft 文件"
description: "深入了解 hello 金鑰設計和實作指導方針訂用帳戶和 Azure 上的帳戶。"
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 761fa847-78b0-4078-a33a-d95d198d1029
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f9dc712af559b04490be1dc721a9b9f7fe9ed88f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-windows-vms"></a>適用於 Windows VM 的 Azure 訂用帳戶和帳戶指導方針

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

本文著重在了解如何為您的環境與使用者基底的 tooapproach 訂用帳戶和帳戶管理成長。

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a>訂用帳戶和帳戶的實作指導方針
决策：

* 哪些設定訂用帳戶和帳戶您需要 toohost 您的 IT 工作負載或基礎結構？
* 如何關閉 hello 階層 toofit toobreak 組織嗎？

工作：

* 定義邏輯組織階層，您希望 toomanage 從訂用帳戶層級。
* toomatch 此邏輯的階層架構，定義所需的 hello 帳戶和訂用帳戶底下的每個帳戶。
* 建立 hello 組訂閱和使用您的命名慣例的帳戶。

## <a name="subscriptions-and-accounts"></a>訂用帳戶與帳戶
使用 Azure toowork，您需要一或多個 Azure 訂用帳戶。 虛擬機器 (VM) 或虛擬網路等資源存在於這些訂用帳戶中。

* 企業客戶通常會有 Enterprise 註冊，這是 hello hello 階層中的最上層資源相關聯的 tooone 或多個帳戶。
* 取用者，而不需要企業註冊的客戶 hello 最上層資源是 hello 帳戶。
* 訂用帳戶相關聯的 tooaccounts，而且可以有一或多個訂閱，每個帳戶。 Azure 帳單 hello 訂用帳戶層級資訊的記錄。

Toohello hello 帳戶/訂用帳戶的關聯性的兩個階層層級的限制，因為它不重要 tooalign hello 命名慣例的帳戶和訂用 toohello 計費的需求。 比方說，如果全域公司使用 Azure，他們可能會選擇每個區域，toohave 一個帳戶和訂閱管理在 hello 區域層級：

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

比方說，您可以使用下列結構的 hello:

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

如果區域決定 toohave 多個訂用帳戶相關聯的 tooa 特定群組，hello 命名慣例應該併入方式 tooencode hello hello 帳戶或 hello 訂用帳戶名稱的額外資料。 此組織允許 massaging 計費報表期間的計費資料 toogenerate hello 新階層的層級：

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

hello 組織可能看起來像下列範例中的 hello:

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

我們會透過可下載的檔案，針對單一帳戶或企業合約中的所有帳戶提供詳細的計費資訊。

## <a name="next-steps"></a>後續步驟
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]


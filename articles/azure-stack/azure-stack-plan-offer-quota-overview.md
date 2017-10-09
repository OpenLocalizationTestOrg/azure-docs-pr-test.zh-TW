---
title: "aaaAzure 堆疊計劃、 方案、 配額和訂用帳戶概觀 |Microsoft 文件"
description: "雲端操作員，我想的 toounderstand Azure 堆疊計劃、 提供項目、 配額和訂用帳戶。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 3dc92e5c-c004-49db-9a94-783f1f798b98
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/22/2017
ms.author: erikje
ms.openlocfilehash: 67f5bcfda221473b1f397668e2a3186b80d6f43c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="plan-offer-quota-and-subscription-overview"></a>方案、優惠、配頭和訂用帳戶概觀

Azure Stack 可讓您提供各式各樣的服務，例如虛擬機器、SQL Server 資料庫、SharePoint、Exchange，甚至 [Azure Marketplace 項目](azure-stack-marketplace-azure-items.md)。 身為雲端操作員，您可以使用方案、供應項目與配額，在 Azure Stack 中設定並提供這類服務。

供應項目包含一個或多個方案，而且每個方案包含一個或多個服務。 透過建立方案並將其組合成不同的供應項目，您可以控制
- 使用者可以存取的服務和資源
- 使用者可以使用這些資源的 hello 數量
- 哪些區域可以存取 toohello 資源

當您提供服務時，將遵循下列大致步驟：

1. 新增您要讓 toodeliver tooyour 使用者的服務。
2. 建立包含一個或多個服務的方案。 建立計畫時，您將會選取或建立 hello 計劃中定義的每個服務的 hello 資源限制的配額。
3. 建立包含一個或多個方案 (包含基本方案及選擇性的附加方案) 的供應項目。

建立 hello 供應項目之後，您的使用者可以訂閱 tooit tooaccess hello 服務及它所提供的資源。 使用者可以訂閱 tooas 許多提供他們想要。 hello 下列圖表顯示的使用者已訂閱 tootwo 優惠的簡單範例。 每個供應項目計劃或兩個，且每個計劃可讓他們存取 tooservices。

![](media/azure-stack-key-features/image4.png)

## <a name="plans"></a>方案

方案結合一或多項服務。 雲端操作員您[建立計劃](azure-stack-create-plan.md)toooffer tooyour 使用者。 接著，您的使用者訂閱 tooyour 優惠 toouse hello 計劃和它們所包含的服務。 在建立計畫時，您的配額，請確定 tooset、 定義基底的計劃，並考慮包括選擇性的附加元件計劃。

### <a name="quotas"></a>配額

管理您的雲端容量的 toohelp，選取或建立計劃中的每個服務的配額。 配額會定義使用者訂用帳戶可以佈建或取用 hello 上層資源限制。 例如，配額可能允許使用者 toocreate toofive 虛擬機器。 配額可以限制各種不同的資源，例如虛擬機器、RAM 和 CPU 限制。

配額可依地區設定。 例如，包含來自區域 A 計算服務的方案，其配額可能是兩部虛擬機器、4-GB RAM 與 10 個 CPU 核心。 在 hello Azure 堆疊開發套件，只有一個區域 (名為*本機*) 使用。

### <a name="base-plan"></a>基本方案

當建立提供項目，hello 服務系統管理員可以包含基底的計劃。 當使用者訂閱 toothat 供應項目，則預設會包含這些基底的計劃。 當使用者訂閱時，他們擁有存取 tooall hello 資源提供者指定的基底的計劃 （與 hello 對應的配額）。

### <a name="add-on-plans"></a>附加方案

您也可以在供應項目中包含選擇性的附加方案。 附加元件計劃不會包含的 hello 訂用帳戶中的預設值。 其他的計劃 （與配額） 可用的訂閱者可以加入 tootheir 訂用帳戶 的項目是附加元件計劃。 例如，您可以提供資源有限的試用版，基本方案與附加元件計劃與更多資源 toocustomers 決定 tooadopt hello 服務人員。

## <a name="offers"></a>優惠

提供項目是的一或多個計劃，好讓使用者可以訂閱 toothem 您建立的群組。 例如，產品 Alpha 可以包含方案 A (包含一組計算服務) 與方案 B (包含一組儲存體與網路服務)。 

當您[建立優惠](azure-stack-create-offer.md)，您必須包含至少一個基底的計劃，但您也可以建立使用者可以加入 tootheir 訂用帳戶的附加元件計劃。


## <a name="subscriptions"></a>訂用帳戶

訂用帳戶是使用者存取供應項目的方式。 如果您是在服務提供者雲端操作員，您的使用者 （租用戶） 會藉由訂閱 tooyour 優惠購買您的服務。 如果您是組織在雲端操作員，您的使用者 （員工） 可以訂閱 toohello 而不必付出您提供的服務。 使用者與供應項目的每個組合都是一個唯一的訂用帳戶。 因此，使用者可以擁有訂閱 toomultiple 提供項目，但每個訂閱適 tooonly 一個供應項目。 計劃、 提議，與配額套用 tooeach 唯一訂閱 – 訂用帳戶之間不共用它們。 使用者建立的每個資源都與一個訂用帳戶相關聯。


### <a name="default-provider-subscription"></a>預設的提供者訂用帳戶

當您部署的 hello Azure 堆疊開發套件時，會自動建立 hello 預設提供者訂用帳戶。 此訂用帳戶可使用的 toomanage Azure 堆疊、 部署進一步的資源提供者，及建立計劃與提供給使用者。 基於安全性和授權的原因，它不應該使用的 toorun 客戶工作負載和應用程式。 

## <a name="next-steps"></a>後續步驟

[建立方案](azure-stack-create-plan.md)

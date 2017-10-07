---
title: "aaaAzure Service Bus 常見問題集 (FAQ) |Microsoft 文件"
description: "回答一些有關 Azure 服務匯流排的常見問題。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: cc75786d-3448-4f79-9fec-eef56c0027ba
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 71fe9eac46647a3e4026dbcaf2196984dd4b6a44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-faq"></a>服務匯流排常見問題集
本文提供 Microsoft Azure 服務匯流排的一些常見問題解集。 您也可以造訪 hello [Azure 支援常見問題集](http://go.microsoft.com/fwlink/?LinkID=185083)一般 Azure 定價和支援資訊。

## <a name="general-questions-about-azure-service-bus"></a>關於 Azure 服務匯流排的一般問題
### <a name="what-is-azure-service-bus"></a>什麼是 Azure 服務匯流排？
[Azure 服務匯流排](service-bus-messaging-overview.md)是非同步傳訊雲端平台，可讓您 toosend 低耦合系統之間的資料。 Microsoft 提供此功能為服務時，這表示，您不需要 toohost 任一個順序 toouse 中硬體它。

### <a name="what-is-a-service-bus-namespace"></a>什麼是服務匯流排命名空間？
[命名空間](service-bus-create-namespace-portal.md)提供範圍容器，可在應用程式內定址服務匯流排資源。 建立一個必要 toouse Service Bus 並將會是其中一個 hello 中開始使用第一個步驟。

### <a name="what-is-an-azure-service-bus-queue"></a>什麼是 Azure 服務匯流排佇列？
[服務匯流排佇列](service-bus-queues-topics-subscriptions.md)是訊息儲存所在的實體。 您有多個應用程式或需要 toocommunicate 彼此的分散式應用程式的多個部分時，佇列會特別有用。 hello 佇列就類似 tooa 配送中心，也就是說，在接收或然後從該位置傳送多個產品 （訊息）。

### <a name="what-are-azure-service-bus-topics-and-subscriptions"></a>什麼是 Azure 服務匯流排主題和訂用帳戶？
主題可視覺化為佇列，而且在使用多個訂用帳戶時，主題會變成更豐富的訊息模型；基本上是一對多的通訊工具。 這個發行/訂閱模型 (或*pub/sub*) 可讓多個應用程式所接收該訊息會傳送具有多個訂用帳戶 toohave 訊息 tooa 主題的應用程式。

### <a name="what-is-a-partitioned-entity"></a>什麼是分割的實體？
傳統的佇列或主題由單一訊息代理程式處理並儲存在一個訊息存放區中。 [分割的佇列或主題](service-bus-partitioning.md)會由多個訊息代理程式處理，並儲存在多個訊息存放區。 這表示 hello 分割的佇列或主題的整體輸送量不再受限於單一訊息代理程式或訊息存放區的 hello 效能。 此外，即使訊息存放區暫時中斷也不會讓分割的佇列或主題無法使用。

請注意，使用分割實體時無法確保順序。 在 hello 事件中的資料分割，就無法使用，您仍然可以傳送和接收來自 hello 其他資料分割的訊息。

## <a name="best-practices"></a>最佳作法
### <a name="what-are-some-azure-service-bus-best-practices"></a>Azure 服務匯流排的最佳做法有哪些？
* [使用服務匯流排的效能改進的最佳做法][ Best practices for performance improvements using Service Bus] – 這篇文章描述 toooptimize 效能交換時的訊息。

### <a name="what-should-i-know-before-creating-entities"></a>建立實體前的須知事項為何？
下列屬性的佇列和主題的 hello 是不變。 在佈建實體時請將這一點納入考量，因為若要修改屬性，就必須建立新的替代實體。

* 大小
* 分割
* 工作階段
* 重複偵測
* 快速實體

## <a name="pricing"></a>價格
本節將回答一些常見問題集疑問 hello 服務匯流排定價結構。

hello[服務匯流排定價和計費](service-bus-pricing-billing.md)篇文章說明 hello 計費公尺，服務匯流排，而且服務匯流排定價選項的相關資訊，請參閱[服務匯流排定價詳細資料](https://azure.microsoft.com/pricing/details/service-bus/)。

您也可以造訪 hello [Azure 支援常見問題集](http://go.microsoft.com/fwlink/?LinkID=185083)一般 azure 定價資訊。 

### <a name="how-do-you-charge-for-service-bus"></a>服務匯流排的收費方式為何？
如需服務匯流排價格的完整資訊，請參閱[服務匯流排價格詳細資料][Pricing overview]。 此外 toohello 價格所述，您必須支付 hello 佈建您的應用程式的資料中心外部輸出的相關聯的資料傳輸。

### <a name="what-usage-of-service-bus-is-subject-toodata-transfer-what-is-not"></a>哪些 Service Bus 的使用會主旨 toodata 傳輸？ 何種不需？
指定的 Azure 區域內的任何資料傳輸都是免費提供，以及任何輸入的資料傳輸。 位於區域外部的資料傳輸是可以找到主旨 tooegress 費用[這裡](https://azure.microsoft.com/pricing/details/bandwidth/)。

### <a name="does-service-bus-charge-for-storage"></a>服務匯流排是否會收取儲存體費用？
不會，服務匯流排不會收取儲存體費用。 不過，沒有配額限制 hello 最大資料量可以保存每個佇列/主題。 請參閱 hello 下一個常見問題集。

## <a name="quotas"></a>配額

如需服務匯流排限制和配額的清單，請參閱 hello [Service Bus 配額概觀][Quotas overview]。

### <a name="does-service-bus-have-any-usage-quotas"></a>服務匯流排是否有任何使用量配額？
根據預設，對於所有雲端服務，Microsoft 會設定針對所有客戶的訂用帳戶計算的彙總每月使用量配額。 因為我們了解您的需求可能超過這些限制，請隨時連絡客戶服務部門，讓我們能夠了解您的需求並適當地調整這些限制。 服務匯流排的 hello 整體使用量配額是每個月的 5 億訊息。

我們都有保留 hello 右 toodisable 已超過其使用量配額是指定月份中的客戶帳戶，而我們將提供電子郵件通知，並採取任何動作之前請多嘗試 toocontact 客戶。 超過這些配額的客戶仍會負責超過 hello 配額的費用。

如同 Azure 上的其他服務，服務匯流排會強制執行一組特定的配額 tooensure 沒有資源使用公平。 您可以在 hello 找到這些配額的詳細[Service Bus 配額概觀][Quotas overview]。

## <a name="troubleshooting"></a>疑難排解
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-service-bus-apis-and-their-suggested-actions"></a>有哪些 Azure 服務匯流排 Api 以及其建議的動作所產生的 hello 例外狀況？
如需可能的服務匯流排例外狀況，請參閱[例外狀況概觀][Exceptions overview]。

### <a name="what-is-a-shared-access-signature-and-which-languages-support-generating-a-signature"></a>什麼是共用存取簽章，何種語言可支援產生簽章？
共用存取簽章是以 SHA-256 安全雜湊或 URI 為基礎的驗證機制。 如需有關資訊 toogenerate 自己節點、 PHP、 Java 和 C 中的簽章\#，請參閱 hello[共用存取簽章][ Shared Access Signatures]發行項。

## <a name="subscription-and-namespace-management"></a>訂用帳戶和命名空間管理
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a>我要如何移轉命名空間 tooanother Azure 訂用帳戶？

您可以移動命名空間從一個 Azure 訂用帳戶 tooanother，使用任一 hello [Azure 入口網站](https://portal.azure.com)或 PowerShell 命令。 在訂單 tooexecute hello 作業中，hello 命名空間必須已經使用。 執行 hello 命令 hello 使用者必須是系統管理員，在這兩個 hello 來源上的，與目標訂用帳戶。

#### <a name="portal"></a>入口網站

toouse hello Azure 入口網站 toomigrate Service Bus 命名空間 tooanother 訂閱 hello 遵循[這裡](../azure-resource-manager/resource-group-move-resources.md#use-portal)。 

#### <a name="powershell"></a>PowerShell

hello 以下 PowerShell 命令的順序會將命名空間從一個 Azure 訂用帳戶 tooanother。 tooexecute 這項作業，hello 命名空間必須已經是作用中，且執行 hello PowerShell 命令的 hello 使用者必須是這兩個 hello 來源與目標訂用帳戶的系統管理員。

```powershell
# Create a new resource group in target subscription
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move namespace from source subscription tootarget subscription
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="next-steps"></a>後續步驟
toolearn 有關 Service Bus 的詳細資訊，請參閱下列主題中的 hello。

* [Azure 服務匯流排進階簡介 (部落格文章)](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [Azure 服務匯流排進階簡介 (Channel9)](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [服務匯流排概觀](service-bus-messaging-overview.md)
* [Azure 服務匯流排架構概觀](service-bus-fundamentals-hybrid-solutions.md)
* [開始使用服務匯流排佇列](service-bus-dotnet-get-started-with-queues.md)

[Best practices for performance improvements using Service Bus]: service-bus-performance-improvements.md
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Quotas overview]: service-bus-quotas.md
[Exceptions overview]: service-bus-messaging-exceptions.md
[Shared Access Signatures]: service-bus-sas.md

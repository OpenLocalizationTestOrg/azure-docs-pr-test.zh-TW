---
title: "aaaPlans 和 Azure 排程器中的計費"
description: "Azure 排程器的計劃和計費"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 13a2be8c-dc14-46cc-ab7d-5075bfd4d724
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 051b8eeb1ea19678b3cef4db3237ebf04c8b0e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="plans-and-billing-in-azure-scheduler"></a>Azure 排程器的計劃和計費
## <a name="job-collection-plans"></a>工作集合計劃
工作集合是在 Azure 排程器中的 hello 計費實體。 工作集合包含許多工作，並分成三個計劃 (免費、標準和高階)，如下所述。

| **工作集合計劃** | **每個工作集合的工作數上限** | **最大週期** | **每個訂用帳戶的工作集合數上限** | **限制** |
|:--- |:--- |:--- |:--- |:--- |
| **免費** |每個工作集合 5 個工作 |每小時一次。 執行工作不得超過一個小時 |訂用帳戶允許 too1 免費工作集合 |無法使用 [HTTP 輸出授權物件](scheduler-outbound-authentication.md) |
| **標準** |每個工作集合 50 個工作 |每分鐘一次。 執行工作不得超過一分鐘 |訂用帳戶允許向上 too100 標準工作集合 |排程器的存取 toofull 功能集 |
| **P10 Premium** |每個工作集合 50 個工作 |每分鐘一次。 執行工作不得超過一分鐘 |訂用帳戶允許向上 too10，000 P10 進階工作集合。 如需詳細資訊，請<a href="mailto:wapteams@microsoft.com">與我們連絡</a>。 |排程器的存取 toofull 功能集 |
| **P20 Premium** |每個作業集合 1000 個工作 |每分鐘一次。 執行工作不得超過一分鐘 |訂用帳戶允許向上 too10，000 P20 進階工作集合。 如需詳細資訊，請<a href="mailto:wapteams@microsoft.com">與我們連絡</a>。 |排程器的存取 toofull 功能集 |

## <a name="upgrades-and-downgrades-of-job-collection-plans"></a>升級或降級工作集合計劃
您可以升級或降級工作集合方案隨時在 hello 免費、 標準和高階計劃間。 不過，降級時 tooa 免費工作集合，則可能會失敗 hello 降級其中一個 hello 下列原因：

* 免費工作集合已存在於 hello 訂用帳戶
* Hello 工作集合中的工作有更高的循環，高於允許的免費工作集合中的工作。 hello 免費工作集合中允許的最大循環會每小時一次
* Hello 工作集合中有 5 個以上的工作
* Hello 工作集合中的工作有會使用 HTTP 或 HTTPS 動作[HTTP 輸出的授權物件](scheduler-outbound-authentication.md)

## <a name="billing-and-azure-plans"></a>計費與 Azure 計劃
不會對免費工作集合的訂用帳戶計費。 如果您有 100 個以上的標準工作集合 （10 個標準計費單位），則更好的處理 toohave 所有 hello 高階計劃中將工作集合。

如果有一個標準作業集合和一個高階作業集合，則您會支付一個標準計費單位「和」一個高階計費單位。 hello tooeither standard 或 premium; 設定的作用中的作業集合的 hello 數目為基礎的排程器服務帳單hello 下兩節中進一步說明。

## <a name="standard-billable-units"></a>標準可計費單位
標準的可計費單位可以包括安裝 too10 標準工作集合。 每個工作集合 too50 作業有標準工作集合，因此一個標準的計費單位可讓訂閱 toohave too500 作業 – 向上 tooalmost 22 百萬個作業執行每個月。

如果有 1 到 10 個標準工作集合，則您將支付 1 個標準計費單位。 如果有 11 到 20 個標準工作集合，則您將支付 2 個標準計費單位。 如果有 21 到 30 個標準工作集合，則您將支付 3 個標準計費單位。

## <a name="p10-premium-billable-units"></a>P10 進階可計費單位
P10 premium 計費單位可以包括安裝 too10，000 P10 進階工作集合。 P10 進階工作集合有 too50 作業每個工作集合，因此一個 premium 計費單位可讓訂閱 toohave 向上 too500，000 工作 – 向上 tooalmost 22 10 億個工作執行每個月。

如果有 1 到 10,000 個進階工作集合，則您將支付 1 個 P10 進階計費單位。 如果有 10,001 到 20,000 個進階工作集合，則您將支付 2 個 P10 進階計費單位，依此類推。

因此，集合都具有 P10 高階工作 hello 相同的功能，因為 hello 標準工作集合但提供價格中斷，萬一您的應用程式需要大量的工作集合。

## <a name="p20-premium-billable-units"></a>P20 進階可計費單位
P20 premium 計費單位可以包括安裝 too5，000 P20 進階工作集合。 P20 進階工作集合有向上 too1，每個工作集合 000 作業，因此一個 premium 計費單位可讓訂閱 toohave 向上 too5 000 000 工作 – 向上 tooalmost 220 10 億個工作執行每個月。

P20 進階工作集合提供 hello P10 進階工作集合相同的功能，但也支援更大的數字工作，每個工作集合和更大的工作總數整體比 P10 premium 允許您 toohave 可調適性。

## <a name="billing-and-active-status"></a>計費和作用中狀態
除非您整個訂用帳戶靠近 toobilling 問題由於某些暫時停用狀態，會永遠啟用工作集合。 hello 只的工作集合不會計費方式 tooensure 是 tooeither 設 toohello*免費*計劃或 toodelete hello 工作集合。

雖然您可能會停用在單一作業中的工作集合內的所有作業，也不會變更 hello 工作集合的 hello 計費狀態 – hello 工作集合會*仍*計費。 同樣地，空白的工作集合會被視為作用中，並將計費。

## <a name="pricing"></a>價格
如需定價詳細資料，請參閱 [排程器定價](https://azure.microsoft.com/pricing/details/scheduler/)。

## <a name="see-also"></a>另請參閱
 [排程器是什麼？](scheduler-intro.md)

 [Azure 排程器概念、術語及實體階層](scheduler-concepts-terms.md)

 [開始在 hello Azure 入口網站中使用排程器](scheduler-get-started-portal.md)

 [Azure 排程器 REST API 參考](https://msdn.microsoft.com/library/mt629143)

 [Azure 排程器 PowerShell Cmdlet 參考](scheduler-powershell-reference.md)

 [Azure 排程器高可用性和可靠性](scheduler-high-availability-reliability.md)

 [Azure 排程器限制、預設值和錯誤碼](scheduler-limits-defaults-errors.md)

 [Azure 排程器輸出驗證](scheduler-outbound-authentication.md)


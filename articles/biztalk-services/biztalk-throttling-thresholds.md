---
title: "關於 BizTalk 服務的節流 aaaLearn |Microsoft 文件"
description: "了解 BizTalk 服務的節流閾值和產生的執行階段行為。 節流是以記憶體使用量和訊息數為依據。 MABS，WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: f6663cf2-cda4-4bac-855e-27d2ad5c4fa4
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 46c8806c3a1f4eeb793f721f849771e0ec155197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-throttling"></a>BizTalk 服務：節流

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Azure BizTalk 服務會實作兩個條件為基礎的服務節流： 記憶體使用量和 hello 同時處理的訊息數目。 本主題列出 hello 節流臨界值，並說明 hello 執行階段行為，當發生節流狀況。

## <a name="throttling-thresholds"></a>節流閾值
下表將列出 hello hello 節流的來源和臨界值：

|  | 說明 | 低閾值 | 高閾值 |
| --- | --- | --- | --- |
| 記憶體 |可用系統記憶體總計的 %/PageFileBytes。 <p><p>總計的可用 PageFileBytes 大約是 hello 系統的 2 倍 hello RAM。 |60% |70% |
| 訊息處理 |同時處理的訊息數目 |40 * 核心數目 |100 * 核心數目 |

當達到高的閾值時，Azure BizTalk 服務會啟動 toothrottle。 當達到 hello 低的閾值時，節流設定停駐點。 例如，服務使用 65% 系統記憶體。 在此情況下，不會不會節流 hello 服務。 服務開始使用 70% 系統記憶體。 在此情況下，hello 服務節流處理，並繼續 toothrottle 直到 hello 服務會使用 60%（下限臨界值） 的系統記憶體。

Azure BizTalk 服務會追蹤節流狀態 （一般狀態與節流狀態） 的 hello 與 hello 節流期間。

## <a name="runtime-behavior"></a>執行階段行為
Azure BizTalk 服務便會進入節流狀態，當 hello 會發生下列情況：

* 依每一角色執行個體來節流。 例如：<br/>
  RoleInstanceA 節流。 RoleInstanceB 未節流。 在此情況下，RoleInstanceB 中的訊息如預期般地處理。 RoleInstanceA 中的訊息都會被捨棄，並會因下列錯誤 hello:<br/><br/>
  **伺服器忙碌中。請再試一次。**<br/><br/>
* 所有提取來源不會輪詢或下載訊息。 例如：<br/>
  管線會從外部 FTP 來源提取訊息。 執行 hello 提取 hello 角色執行個體取得節流狀態。 在此情況下，hello 管線就會停止下載額外的訊息，直到 hello 角色執行個體停止節流。
* 回應會傳送 toohello 用戶端，因此 hello 用戶端可以再重新送出 hello 訊息。
* 您必須等到 hello 節流設定所解析。 具體來說，您必須等到達到 hello 低臨界值。

## <a name="important-notes"></a>重要事項
* 無法停用節流。
* 無法修改節流閾值。
* 節流的實作以全系統為範圍。
* hello Azure SQL Database 伺服器也有內建的節流。

## <a name="additional-azure-biztalk-services-topics"></a>其他 Azure BizTalk 服務主題
* [安裝 hello Azure BizTalk 服務 SDK](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [教學課程：Azure BizTalk 服務](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [開始使用我要如何 hello Azure BizTalk 服務 SDK](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Azure BizTalk 服務](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>另請參閱
* [BizTalk 服務：開發人員、基本、標準和高級版本圖表](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [BizTalk 服務：使用 Azure 傳統入口網站進行佈建](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [BizTalk 服務：佈建狀態圖](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [BizTalk 服務：儀表板、監視和調整索引標籤](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [BizTalk 服務：備份與還原](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [BizTalk 服務：簽發者名稱和簽發者金鑰](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>


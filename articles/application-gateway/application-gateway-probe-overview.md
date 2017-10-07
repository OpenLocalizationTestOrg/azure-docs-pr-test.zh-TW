---
title: "監視 Azure 應用程式閘道概觀 aaaHealth |Microsoft 文件"
description: "深入了解 hello 監視在 Azure 應用程式閘道的功能"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7eeba328-bb2d-4d3e-bdac-7552e7900b7f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 5091d80394a354ff849ce7ccee8cc9d2fd0456db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-health-monitoring-overview"></a>應用程式閘道健全狀況監視概觀

預設的 azure 應用程式閘道監視它的後端集區中的所有資源 hello 健全狀況，並自動移除任何從 hello 集區被視為狀況不良的資源。 應用程式閘道會繼續 toomonitor hello 狀況不良的執行個體，並將其加入回 toohello 狀況良好的後端集區，當它們變成可用，而且回應 toohealth 探查。 應用程式閘道會傳送 hello 健全狀況探查 hello 與 hello 後端 HTTP 設定中定義的相同連接埠。 此組態可確保該 hello 探查測試的 hello 相同連接埠，客戶就會使用 tooconnect toohello 後端。

![應用程式閘道探查範例][1]

在加法 toousing 預設健全狀況探查的監視，您也可以自訂 hello 健全狀況探查 toosuit 應用程式的需求。 本文會探討預設和自訂健全狀態探查。

> [!NOTE]
> 如果應用程式閘道子網路上沒有 NSG，應輸入流量的 hello 應用程式閘道子網路上開啟連接埠範圍 65503 65534。 這些連接埠不需要 hello 後端健全狀況 API toowork。

## <a name="default-health-probe"></a>預設的健全狀況探查

如果您沒有設定任何自訂探查組態，應用程式閘道就會自動設定預設健全狀況探查。 hello 監視行為的運作方式是進行 HTTP 要求 toohello IP 位址 hello 後端集區設定。 預設探查 hello 後端 http 設定設定為使用 HTTPS，如果 hello 探查使用 HTTPS 做為 hello 範例以及 tootest 健全狀況。

例如： 您設定連接埠 80 上的應用程式閘道 toouse 後端伺服器 A、 B 和 C tooreceive HTTP 網路流量。 hello 預設健全狀況監視測試 hello 三部伺服器處於狀況良好的 HTTP 回應每隔 30 秒。 狀況良好的 HTTP 回應具有 200 到 399 之間的 [狀態碼](https://msdn.microsoft.com/library/aa287675.aspx) 。

如果伺服器 A hello 預設探查檢查失敗，hello 應用程式閘道會從其後端集區中，移除它，網路流量停止傳送 toothis 伺服器。 hello 預設探查仍會繼續 toocheck 伺服器每隔 30 秒。 當伺服器的回應從預設健全狀況探查成功 tooone 要求時，它就會重新加入做為狀況良好的 toohello 後端集區和流量開始再次流動 toohello 伺服器。

### <a name="default-health-probe-settings"></a>預設的健全狀況探查設定

| 探查屬性 | 值 | 說明 |
| --- | --- | --- |
| 探查 URL |http://127.0.0.1:\<連接埠\>/ |URL 路徑 |
| 間隔 |30 |探查間隔 (秒) |
| 逾時 |30 |探查逾時 (秒) |
| 狀況不良臨界值 |3 |探查重試計數。 hello 連續探查失敗計數達到 hello 狀況不良閾值後，hello 後端伺服器標記為。 |

> [!NOTE]
> hello 連接埠是 hello 相同為 hello 後端 HTTP 設定連接埠。

hello 預設探查只會查看 http://127.0.0.1:\<連接埠\>toodetermine 健全狀況狀態。 如果您需要 tooconfigure hello 健全狀況探查 toogo tooa 自訂 URL，或修改其他任何設定，您必須使用自訂探查 hello 步驟中所述：

## <a name="custom-health-probe"></a>自訂的健全狀況探查

自訂探查可讓您 toohave 更細微的控制，透過 hello 健全狀況監視。 當使用自訂探查，則您可以設定 hello 探查間隔、 hello URL 和路徑 tootest，以及多少失敗的回應 tooaccept，再將標示為狀況不良的 hello 後端集區執行個體。

### <a name="custom-health-probe-settings"></a>自訂的健全狀況探查設定

hello 下表提供自訂的健全狀況探查的 hello 屬性定義。

| 探查屬性 | 說明 |
| --- | --- |
| 名稱 |Hello 探查的名稱。 這個名稱是使用的 toorefer toohello 探查後端 HTTP 設定中。 |
| 通訊協定 |使用 toosend hello 探查通訊協定。 hello 探查使用 hello hello 後端 HTTP 設定中所定義的通訊協定 |
| Host |主機名稱 toosend hello 探查。 只有當應用程式閘道上設定多站台時適用，否則請使用 '127.0.0.1'。 此值與 VM 主機名稱不同。 |
| Path |Hello 探查相對路徑。 hello 有效路徑的開頭 '/'。 |
| 間隔 |探查間隔 (秒)。 這個值是兩個連續探查 hello 時間間隔。 |
| 逾時 |探查逾時 (秒)。 如果這個逾時期限內未收到有效的回應，hello 探查被標示為失敗。  |
| 狀況不良臨界值 |探查重試計數。 hello 連續探查失敗計數達到 hello 狀況不良閾值後，hello 後端伺服器標記為。 |

> [!IMPORTANT]
> 如果應用程式閘道設定為單一站台，依預設 hello 主機名稱應指定為 '127.0.0.1'，除非否則在自訂探查設定。
> 參考自訂探查送出太\<通訊協定\>://\<主機\>:\<連接埠\>\<路徑\>。 hello 使用通訊埠會 hello hello 後端 HTTP 設定中所定義的相同連接埠。

## <a name="next-steps"></a>後續步驟
了解應用程式閘道健康狀態監控之後, 您可以設定[自訂健全狀況探查](application-gateway-create-probe-portal.md)hello Azure 入口網站中或[自訂健全狀況探查](application-gateway-create-probe-ps.md)使用 PowerShell 和 hello Azure 資源管理員部署模型。

[1]: ./media/application-gateway-probe-overview/appgatewayprobe.png

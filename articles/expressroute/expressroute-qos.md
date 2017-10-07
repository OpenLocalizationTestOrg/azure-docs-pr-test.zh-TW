---
title: "aaaQoS expressroute 的需求 |Microsoft 文件"
description: "此頁面提供用來設定和管理適用於 ExpressRoute 循環之 QoS 的詳細需求。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a>ExpressRoute QoS 需求
商務用 Skype 具有各種工作負載，其所要求的 QoS 處理方式各有差異。 如果您計劃 tooconsume 語音服務透過 ExpressRoute，您應遵守 toohello 底下所述的需求。

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> Toohello Microsoft 對等互連只套用 QoS 需求。 在 Azure 公用對等互連和 Azure 私人互連接收網路流量的 hello DSCP 值將會重設 too0。 
> 
> 

hello 下表提供用於商務用 Skype 的 DSCP 標示的清單。 請參閱太[管理商務用 Skype 的 QoS](https://technet.microsoft.com/library/gg405409.aspx)如需詳細資訊。

| **傳輸類別** | **處理方式 (DSCP 標示)** | **商務用 Skype 的工作負載** |
| --- | --- | --- |
| **語音** |EF (46) |Skype / Lync 語音 |
| **互動式** |AF41 (34) |影片、VBSS |
| AF21 (18) |APP 共用 | |
| **預設值** |AF11 (10) |檔案傳輸 |
| CS0 (0) |任何其他項目 | |

* 您應該分類 hello 工作負載，並將標示 hello 右 DSCP 值。 請遵循所提供的 hello 指引[這裡](https://technet.microsoft.com/library/gg405409.aspx)如何 tooset DSCP 標示您的網路中。
* 您應在網路中設定並支援多個 QoS 佇列。 語音必須是獨立類別，且收到 hello RFC 3246 中指定的 EF 處理方式。 
* 您可以決定 hello 佇列機制、 壅塞偵測原則和每個流量類別的頻寬配置。 但是，hello DSCP 標示 skype 以商業工作負載必須保留。 如果您使用 DSCP 標示，以上未列出例如 AF31 (26)，您必須重新撰寫此 DSCP 值 too0 傳送 hello 封包 tooMicrosoft 之前。 Microsoft 只會傳送 hello DSCP 值顯示在資料表上方的 hello 以標記的封包。 

## <a name="next-steps"></a>後續步驟
* 請參閱 toohello 需求[路由](expressroute-routing.md)和[NAT](expressroute-nat.md)。
* 請參閱 hello 下列連結 tooconfigure ExpressRoute 連線。
  
  * [建立 ExpressRoute 線路](expressroute-howto-circuit-classic.md)
  * [設定路由](expressroute-howto-routing-classic.md)
  * [連結的 VNet tooan ExpressRoute 電路](expressroute-howto-linkvnet-classic.md)


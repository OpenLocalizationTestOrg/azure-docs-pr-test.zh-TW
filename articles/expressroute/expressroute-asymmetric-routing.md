---
title: "aaaAsymmetric 路由 |Microsoft 文件"
description: "這篇文章會引導您客戶可能會面臨與具有多個連結 tooa 目的地網路中的非對稱路由 hello 問題。"
documentationcenter: na
services: expressroute
author: osamazia
manager: carmonm
editor: 
ms.assetid: a754bff9-95c9-44b5-9796-377fc21e8322
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: osamam
ms.openlocfilehash: 01a16242437a3674dcfe27b074911a829a6c1abd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="asymmetric-routing-with-multiple-network-paths"></a>非對稱式路由與多個網路路徑
本文說明如何在網路來源與目的地之間有多個路徑時，向前和回傳網路流量如何採取不同的路由。

它的重要 toounderstand 兩個概念 toounderstand 對稱路由。 其中一個是 hello 作用的多個網路路徑。 其他 hello 是裝置，例如防火牆後面，如何保留狀態。 這些裝置類型稱為具狀態裝置。 這兩項因素的組合建立網路流量由丟棄的可設定狀態的裝置 hello 可設定狀態的裝置未偵測到流量竟是 hello 裝置本身的案例。

## <a name="multiple-network-paths"></a>多個網路路徑
當企業網路有只有一個連結 toohello 其網際網路服務提供者，所有流量 tooand hello 網際網路從透過網際網路傳送 hello 相同的路徑。 通常，公司購買多個電路，做為重複的路徑，tooimprove 網路執行時間。 當發生這種情況時，有可能 hello 網路，toohello 網際網路，外部流量通過一個連結和 hello 傳回流量透過不同的連結。 這通常稱為非對稱式路由。 在非對稱路由，反向的網路流量會 hello 原始資料流程路徑不同。

![具有多個路徑的網路](./media/expressroute-asymmetric-routing/AsymmetricRouting3.png)

雖然它主要是發生在 hello 網際網路上，非對稱路由也適用於 tooother 組合多個路徑。 適用於，例如，tooan 網際網路路徑和私用的路徑，前往 toohello 相同的目的地，並移 toohello toomultiple 路徑相同的目的地。

Hello 方式，從來源 toodestination 沿著每個路由器計算最佳路徑 tooreach hello 目的地。 hello 最佳的可能路徑的路由器的決定根據兩個主要因素：

* 外部網路之間的路由是以「邊界閘道通訊協定」(BGP) 路由通訊協定為基礎。 BGP 公告接受從其他例項，並透過一系列的步驟 toodetermine hello 最佳路徑 toohello 預期目的執行它們。 它會儲存其路由表中的 hello 最佳路徑。
* hello 與路由相關聯的子網路遮罩長度會影響路由路徑。 如果路由器收到多個公告的 hello 相同的 IP 位址，但使用不同的子網路遮罩 hello 路由器慣用 hello 公告，較長的子網路遮罩因為它會被視為更特定的路由。

## <a name="stateful-devices"></a>具狀態裝置
路由器會基於路由目的查看 hello 封包的 IP 標頭。 某些裝置看起來更深入在 hello 封包。 這些裝置通常會查看 Layer4 (傳輸控制通訊協定 (TCP) 或使用者資料標通訊協定 (UDP))，或甚至是 Layer7 (應用程式層) 標頭。 這幾種裝置不是安全性裝置，就是頻寬最佳化裝置。 

防火牆是具狀態裝置的常見範例。 防火牆會允許或拒絕封包 toopass 透過其通訊協定，TCP/UDP 連接埠等 URL 標頭的各種欄位為基礎的介面。 此層級的封包檢查會將處理 hello 裝置上的負載過重。 tooimprove 效能 hello 防火牆會檢查 hello 流程的第一個封包。 如果允許 hello 封包 tooproceed，它會在其狀態資料表中保存 hello 流程資訊。 允許所有後續封包相關的 toothis 流程根據 hello 初始判斷。 是現有的流程一部分的封包可能抵達 hello 防火牆。 如果 hello 防火牆沒有先前的狀態相關的資訊，hello 防火牆會捨棄 hello 封包。

## <a name="asymmetric-routing-with-expressroute"></a>非對稱式路由與 ExpressRoute
當您透過 Azure ExpressRoute 連線 tooMicrosoft 時，您網路的變更如下：

* 您有多個連結 tooMicrosoft。 一個連結是現有的網際網路連線，而其他 hello 透過 ExpressRoute。 某些流量 tooMicrosoft 可能會通過 hello 網際網路，但回來透過 ExpressRoute，反之亦然。
* 您會透過 ExpressRoute 收到更多明確的 IP 位址。 因此，從您的網路 tooMicrosoft 透過 ExpressRoute 提供服務的流量，路由器一律最好 ExpressRoute。

toounderstand hello 影響這兩個變更網路，請考慮在某些情況。 例如，您必須只能有一個循環 toohello 網際網路和取用所有的 Microsoft 服務，透過網際網路 hello。 從您的網路來回 tooMicrosoft 周遊 hello 流量 hello 相同的網際網路連結和通過 hello 防火牆。 hello 防火牆記錄 hello 流程，因為它會看見 hello 第一個封包，並傳回因為 hello 狀態資料表中的 hello 流程有允許封包。

![非對稱式路由與 ExpressRoute](./media/expressroute-asymmetric-routing/AsymmetricRouting1.png)

然後，您會開啟 ExpressRoute，並透過 ExpressRoute 使用 Microsoft 所提供的服務。 其他 Microsoft 的服務會透過網際網路 hello 消耗。 您可以部署不同的防火牆在您已連接的 tooExpressRoute 的邊緣。 Microsoft 會透過 ExpressRoute 通告更特定的前置詞 tooyour 網路，針對特定的服務。 路由基礎結構會 ExpressRoute 選擇做為這些前置詞的 hello 慣用路徑。 如果您不會通知您的公用 IP 位址 tooMicrosoft 透過 ExpressRoute，Microsoft 會與您透過 hello 網際網路的公用 IP 位址進行通訊。 將流量從網路 tooMicrosoft 使用 ExpressRoute，並從 Microsoft 的反向流量使用 hello 網際網路。 當在 hello 邊緣 hello 防火牆看到它找不到在 hello 狀態資料表中的流程回應封包時，就會卸除 hello 返回流量。

如果您選擇 toouse hello ExpressRoute 以及 hello 網際網路，集區相同的網路位址轉譯 (NAT)，您會看到與 hello 用戶端類似的問題在網路上的私人 IP 位址。 要求的服務，例如 Windows Update 移透過 hello 網際網路，因為這些服務的 IP 位址不會透過 ExpressRoute 通告。 然而，hello 返回流量透過 ExpressRoute 會傳回。 如果 Microsoft 接收 IP 位址與 hello 相同子網路遮罩從 hello 網際網路和 ExpressRoute，它透過 hello 網際網路慣用 ExpressRoute。 如果防火牆或其他可設定狀態的裝置上您網路的邊緣和面對 ExpressRoute hello 流程沒有先前的資訊，就會卸除屬於 toothat 流程 hello 封包。

## <a name="asymmetric-routing-solutions"></a>非對稱式路由解決方案
您會有兩個主要選項 toosolve hello 的非對稱路由問題。 其中一個是透過路由，而其他 hello 是使用來源為基礎的 NAT (SNAT)。

### <a name="routing"></a>路由
確定您的公用 IP 位址公告的 tooappropriate 廣域網路 (WAN) 連結。 例如，如果您想要 toouse hello 網際網路驗證流量和 ExpressRoute 郵件流量，您應該透過 ExpressRoute 不通知您 Active Directory Federation Services (AD FS) 的公用 IP 位址。 同樣地，請務必不在內部 tooexpose hello 路由器的 AD FS 伺服器 tooIP 位址接收透過 ExpressRoute。 透過 ExpressRoute 接收路由是更特定的因此他們進行驗證的流量 tooMicrosoft 的 ExpressRoute hello 慣用的路徑。 這會導致非對稱式路由。

如果您想 toouse ExpressRoute 進行驗證，請確定您透過 ExpressRoute 沒有 NAT 廣告 AD FS 的公用 IP 位址 如此一來，來自 Microsoft 和進入 tooan 流量內部部署 AD FS 伺服器會透過 ExpressRoute。 因為它是透過網際網路 hello 的 hello 慣用的路由，從客戶 tooMicrosoft 返回流量就會使用 ExpressRoute。

### <a name="source-based-nat"></a>以來源為基礎的 NAT
解決非對稱式路由問題的另一種方式是使用 NAT。 比方說，您有不通告內部 Simple Mail Transfer Protocol (SMTP) 伺服器的 hello 公用 IP 位址透過 ExpressRoute 因為想 toouse hello 網際網路這種類型的通訊。 要求來自 Microsoft，然後到 tooyour 內部 SMTP 伺服器會周遊 hello 網際網路。 您 SNAT hello 連入要求 tooan 內部 IP 位址。 從 hello SMTP 伺服器的反向流量會傳送 toohello 邊緣防火牆 （它會使用 NAT） 而不是透過 ExpressRoute。 hello 返回流量會回到透過 hello 網際網路。

![以來源為基礎的 NAT 網路組態](./media/expressroute-asymmetric-routing/AsymmetricRouting2.png)

## <a name="asymmetric-routing-detection"></a>非對稱式路由偵測
追蹤路由是 hello 最佳方式 toomake 確定您的網路流量會周遊 hello 預期的路徑。 如果您預期流量從您的內部 SMTP 伺服器 tooMicrosoft tootake hello 網際網路的路徑，hello 預期追蹤路由取自 hello SMTP 伺服器 tooOffice 365。 hello 結果驗證流量確實離開您的網路朝 hello 網際網路，而不是 ExpressRoute。


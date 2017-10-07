---
title: "aaaNested Traffic Manager 設定檔 |Microsoft 文件"
description: "這篇文章說明 hello ' 巢狀設定檔 功能的 Azure 流量管理員"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f1b112c4-a3b1-496e-90eb-41e235a49609
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: e476d58a82ed94d12731156280c9665f980de0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="nested-traffic-manager-profiles"></a>巢狀流量管理員設定檔

Traffic Manager 會包含某個範圍的流量路由方法可讓您 toocontrol Traffic Manager 如何選擇哪一個端點應該從每位使用者接收流量。 如需詳細資訊，請參閱 [流量管理員流量路由方法](traffic-manager-routing-methods.md)。

每個「流量管理員」設定檔皆指定一個流量路由方法。 不過，有一些需要更複雜的流量路由比 hello 路由單一 Traffic Manager 設定檔所提供的案例。 您可以巢狀多個流量路由方法的 Traffic Manager 設定檔 toocombine hello 優點。 巢狀設定檔可讓您 toooverride hello 預設 Traffic Manager 行為 toosupport 較大和更複雜的應用程式部署。

hello 遵循範例說明如何 toouse 巢狀在各種情況中的 Traffic Manager 設定檔。

## <a name="example-1-combining-performance-and-weighted-traffic-routing"></a>範例 1︰結合「效能」和「加權」流量路由

假設您部署的應用程式在下列 Azure 區域的 hello： 美國西部，西歐、 東亞。 您可以使用 Traffic Manager 的 「 效能 」 流量路由方法 toodistribute 流量 toohello 區域最接近 toohello 使用者。

![單一流量管理員設定檔][4]

現在，假設您想要 tootest 更新 tooyour 服務然後再發送更廣泛。 您想 toouse hello 「 加權 」 流量路由方法 toodirect 一小部分的流量 tooyour 測試部署。 您在西歐設定 hello 測試部署，連同 hello 現有生產環境部署。

您無法在單一設定檔中結合「加權」和「效能」流量路由。 toosupport 此案例中，建立使用兩個 hello 西歐端點和 hello '加權' 流量路由方法的 Traffic Manager 設定檔。 接下來，您會加入此 'child' 設定檔為端點 toohello 'parent' 設定檔。 hello 父系設定檔仍會使用 hello 效能 」 流量路由方法和含有 hello 全域部署的其他端點。

hello 下列圖表說明此範例中：

![巢狀流量管理員設定檔][2]

在此組態中，透過 hello 父系設定檔導向流量將流量分散到區域通常。 在西歐，hello 巢狀設定檔會將流量 toohello 生產與測試端點根據 toohello 權重。

當 hello 父系設定檔使用 hello 「 效能 」 流量路由方法時，每個端點必須指派一個位置。 當您設定 hello 端點時，會指派 hello 位置。 選擇 hello Azure 地區最接近 tooyour 部署。 hello Azure 區域是 hello hello 網際網路延遲表格所支援的位置值。 如需詳細資訊，請參閱[流量管理員「效能」流量路由方法](traffic-manager-routing-methods.md#performance)。

## <a name="example-2-endpoint-monitoring-in-nested-profiles"></a>範例 2︰巢狀設定檔中的端點監視

Traffic Manager 會主動監視每個服務端點的 hello 健全的狀況。 如果端點為狀況不良，Traffic Manager 會指示使用者 tooalternative 端點 toopreserve hello 可用性的服務。 此端點監視和容錯移轉行為適用於 tooall 流量路由方法。 如需詳細資訊，請參閱 [流量管理員端點監視](traffic-manager-monitoring.md)。 巢狀設定檔的端點監視有不同的運作方式。 巢狀設定檔，請 hello 父系設定檔不會直接執行 hello 子系上的健康情況檢查。 相反地，hello hello 子項設定檔的端點健全狀況是使用的 toocalculate hello hello 子項設定檔的整體健全狀況。 此健全狀況資訊會 hello 巢狀設定檔的階層中往上傳播。 hello 父系設定檔會使用此彙總健全狀況 toodetermine 是否 toodirect 流量 toohello 子項設定檔。 請參閱 hello[常見問題集](traffic-manager-FAQs.md#traffic-manager-nested-profiles)的健全狀況監視的巢狀設定檔的完整詳細資料。

傳回 toohello 上例，假設在西歐 hello 生產環境部署就會失敗。 根據預設，hello 'child' 設定檔會指示所有流量 toohello 測試部署。 如果 hello 測試部署也會失敗，hello 父系設定檔會決定 hello 子系的設定檔應該不接收流量因為所有的子端點的狀況不良。 然後，hello 父系設定檔會將流量 toohello 其他區域。

![巢狀設定檔容錯移轉 (預設行為)][3]

您可能喜歡這種做法。 或者，您可能會考慮所有流量，如西歐現在都即將 toohello 測試部署，而不是有限的子集流量。 不論 hello hello 健全狀況測試部署，您會想 toofail toohello 透過其他區域在西歐 hello 生產環境部署失敗時。 tooenable 此容錯移轉，設定為 hello 父系設定檔中端點的 hello 子系的設定檔時，可以指定 hello 'MinChildEndpoints' 參數。 hello 參數會決定 hello hello 子項設定檔中可用的端點數目下限。 hello 預設值為 '1'。 此案例中，您可以設定 hello MinChildEndpoints 值 too2。 低於此閾值 hello 父系設定檔會認為 hello 整個子系設定檔 toobe 無法使用，並指示流量 toohello 其他端點。

hello 下圖說明這項設定：

![以 'MinChildEndpoints' = 2 進行容錯移轉的巢狀設定檔][4]

> [!NOTE]
> hello 'Priority' 流量路由方法會將所有流量 tooa 單一端點。 因此，如果子設定檔的 MinChildEndpoints 不是設為 '1'，則作用不大。

## <a name="example-3-prioritized-failover-regions-in-performance-traffic-routing"></a>範例 3︰設定「效能」流量路由中容錯移轉區域的優先順序

hello hello 「 效能 」 流量路由方法的預設行為是設計的 tooavoid 過度最接近端點接著載入 hello 和造成串聯的一連串的失敗。 當端點失敗時，會指示 toothat 端點是平均的所有流量都分散 toohello 其他端點的所有區域。

![搭配預設容錯移轉的「效能」流量路由][5]

不過，假設您偏好 hello 西歐流量容錯移轉 tooWest 我們，並只在兩個端點都無法使用時直接流量 tooother 區域。 您可以建立此解決方案使用 hello 'Priority' 流量路由方法的子系的設定檔。

![搭配優先性容錯移轉的「效能」流量路由][6]

Hello 西歐端點的優先順序高於 hello 美國西部端點，因為所有流量會在這兩個端點都在線上時都傳送 toohello 西歐端點。 如果西歐失敗，其流量會導向的 tooWest 美國。 巢狀的 hello 設定檔，流量西歐和美國西部失敗時，才會導向的 tooEast 亞洲。

您可以對所有區域重複此模式。 取代 hello 父系設定檔中的所有三個端點具有三個子項設定檔，每個提供優先順序的容錯移轉順序。

## <a name="example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-hello-same-region"></a>範例 4： 控制 「 效能 」 流量路由 hello 中的多個端點之間相同區域

假設 hello 「 效能 」 流量路由方法用在特定區域中有多個端點的設定檔。 根據預設，流量會導向 toothat 區域平均分散在該區域中所有可用的端點。

![「效能」流量路由區域內流量分配 (預設行為)][7]

我們不是在西歐新增多個端點，而是將這些端點封入個別的子設定檔中。 hello 子系的設定檔會成為 toohello 父 hello 西歐中唯一的端點。 hello hello 子項設定檔上的設定可以控制與西歐 hello 流量發佈啟用該區域內的優先權為基礎或加權的流量路由。

![搭配自訂區域內流量分配的「效能」流量路由][8]

## <a name="example-5-per-endpoint-monitoring-settings"></a>範例 5︰每個端點的監視設定

假設您使用 Traffic Manager toosmoothly 流量從傳統內部部署網站 tooa 新雲端架構版本移轉裝載於 Azure。 Hello 舊版的站台，您會想 toouse hello 首頁 URI toomonitor 站台健全狀況。 但如 hello 新雲端架構的版本，您要實作自訂監視的頁面 (路徑 ' / monitor.aspx')，其中包含額外的檢查。

![流量管理員端點監視 (預設行為)][9]

Traffic Manager 設定檔中的 hello 監視設定會套用 tooall 單一設定檔中的端點。 與巢狀設定檔，您可以使用不同的子系設定檔，每個站台 toodefine 不同監視設定。

![搭配每個設定的流量管理員端點監視][10]

## <a name="next-steps"></a>後續步驟

深入了解[流量管理員設定檔](traffic-manager-overview.md)

了解如何太[建立 Traffic Manager 設定檔](traffic-manager-create-profile.md)

<!--Image references-->
[1]: ./media/traffic-manager-nested-profiles/figure-1.png
[2]: ./media/traffic-manager-nested-profiles/figure-2.png
[3]: ./media/traffic-manager-nested-profiles/figure-3.png
[4]: ./media/traffic-manager-nested-profiles/figure-4.png
[5]: ./media/traffic-manager-nested-profiles/figure-5.png
[6]: ./media/traffic-manager-nested-profiles/figure-6.png
[7]: ./media/traffic-manager-nested-profiles/figure-7.png
[8]: ./media/traffic-manager-nested-profiles/figure-8.png
[9]: ./media/traffic-manager-nested-profiles/figure-9.png
[10]: ./media/traffic-manager-nested-profiles/figure-10.png

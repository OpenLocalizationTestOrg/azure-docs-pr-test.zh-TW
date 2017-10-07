---
title: "aaaPerformance 考量 Azure Traffic Manager |Microsoft 文件"
description: "了解效能 Traffic Manager 以及 tootest 效能，您的網站時使用流量管理員"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 3ba5dfa1-2922-43f1-9a23-d06969c4a516
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: fd4e6cb221a2ceee63ec57237ee90fd714e91db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performance-considerations-for-traffic-manager"></a>流量管理員的效能考量

此頁面說明使用流量管理員的效能考量。 請考慮下列案例中的 hello:

您必須在 hello Uswest 網站的執行個體和 EastAsia 區域。 其中一個 hello 執行個體失敗 hello 流量管理員探查 hello 健全狀況的檢查。 應用程式流量會導向的 toohello 狀況良好的區域。 預期此容錯移轉，但效能可能會產生根據 hello 流量現在旅行 tooa 遠方區域的 hello 延遲問題。

## <a name="performance-considerations-for-traffic-manager"></a>流量管理員的效能考量

hello 唯一效能的影響的流量管理員能在您的網站是 hello 初始 DNS 查閱。 該主機 hello trafficmanager.net 區域時，是由 hello Microsoft DNS 根伺服器處理 hello Traffic Manager 設定檔名稱的 DNS 要求。 Traffic Manager 會填入，且會定期更新，根據 hello Traffic Manager 原則及 hello 探查結果 hello Microsoft DNS 根伺服器。 因此即使在 hello 初始 DNS 查閱期間沒有 DNS 查詢傳送 tooTraffic 管理員。

Traffic Manager 由數個元件所組成： DNS 名稱伺服器、 API 服務、 hello 儲存層和監視服務的端點。 如果 Traffic Manager 服務元件失敗，則不會影響您的 Traffic Manager 設定檔相關聯的 hello DNS 名稱。 hello Microsoft DNS 伺服器中的 hello 記錄維持不變。 不過，端點監視和 DNS 更新不會發生。 因此，Traffic Manager 不是能 tooupdate DNS toopoint tooyour 容錯移轉站台您主要站台關閉而發生。

系統會快速解析 DNS 名稱並快取結果。 hello hello 初始 DNS 查閱速度取決於 hello 進行名稱解析的 DNS 伺服器 hello 用戶端使用。 一般而言，用戶端可以在大約 50 毫秒內完成 DNS 查閱。 DNS--存留時間 (TTL) 的 hello hello 持續時間內會快取 hello 查閱 hello 結果。 hello 預設 Traffic Manager 的 TTL 是 300 秒。

流量不會透過流量管理員流動。 Hello DNS 查閱完成之後，hello 用戶端有一個 IP 位址之網站的執行個體。 hello 用戶端會直接連接 toothat 位址，並透過 Traffic Manager 未通過。 hello 您選擇的 Traffic Manager 原則已在 hello DNS 效能上的沒有影響。 不過，效能路由方法會造成負面影響 hello 應用程式體驗。 比方說，如果您的原則重新導向流量從裝載於亞洲 North America tooan 執行個體，這些工作階段的 hello 網路延遲可能是效能問題。

## <a name="measuring-traffic-manager-performance"></a>測試流量管理員效能

有數個網站，您可以使用 toounderstand hello 效能與流量管理員設定檔的行為。 這些網站其中許多都是免費，但可能有限制。 某些網站提供付費的監視與報告增強功能。

在這些站台上的 hello 工具測量 DNS 延遲，並顯示 hello 解析 hello 世界各地的用戶端位置的 IP 位址。 這些工具大部分都不會快取 hello 的 DNS 結果。 因此，hello 工具顯示 hello 完整的 DNS 查閱每次執行測試。 當您測試自己的用戶端中時，您只會遇到 hello 完整 DNS 查閱的效能一次期間 hello TTL。

## <a name="sample-tools-toomeasure-dns-performance"></a>範例工具 toomeasure DNS 效能

* [SolveDNS](http://www.solvedns.com/dns-comparison/)

    SolveDNS 提供許多效能工具。 hello DNS 比較工具可以顯示您要花多久 tooresolve 您的 DNS 名稱，以及如何以比較 tooother DNS 服務提供者。

* [WebSitePulse](http://www.websitepulse.com/help/tools.php)

    WebSitePulse 其中一個 hello 最簡單工具。 輸入 hello URL toosee DNS 解析時間、 第一個位元組、 最後一個位元組和其他效能統計資料。 您可以從三個不同的測試位置中選擇。 在此範例中，您會看到 hello 第一次執行示範 DNS 查閱採用 0.204 秒。

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse.png)

    因為結果會快取，hello hello 第二個測試 hello 相同 Traffic Manager 端點 hello DNS 查閱會 0.002 秒。

    ![pulse2](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse2.png)

* [CA App Synthetic Monitor](https://asm.ca.com/en/checkit.php)

    此站台先前稱為 hello Watchmouse 檢查網站工具，顯示您的 DNS 解析 hello 同時時間從多個地理區域。 從數個地理位置中，輸入 hello URL toosee DNS 解析時間，連線時間，速度。 使用哪一種裝載的服務會傳回此測試 toosee hello 世界各地的不同位置。

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-watchmouse.png)

* [Pingdom](http://tools.pingdom.com/)

    這項工具提供網頁每個項目的效能統計資料。 hello 頁面分析 索引標籤會顯示 hello 花費的時間百分比上 DNS 查閱。

* [What's My DNS?](http://www.whatsmydns.net/)

    此站台從 20 個不同位置中沒有 DNS 查閱，並在地圖上顯示 hello 結果。

* [Dig Web Interface](http://www.digwebinterface.com)

    這個網站會顯示更詳細的 DNS 資訊，包括 CNAME 和 A 記錄。 請確定您在 [選項] 檢查 hello 'Colorize output' 和 '統計資料' 並選取 'All' Nameservers 底下。

## <a name="next-steps"></a>後續步驟

[關於流量管理員流量路由方法](traffic-manager-routing-methods.md)

[測試流量管理員設定](traffic-manager-testing-settings.md)

[流量管理員的相關作業 (REST API 參考)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Azure 流量管理員 Cmdlet](http://go.microsoft.com/fwlink/p/?LinkId=400769)


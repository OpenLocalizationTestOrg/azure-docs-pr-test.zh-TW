---
title: "Azure CDN 習慣 aaaAnalyze |Microsoft 文件"
description: "您可以檢視您的 CDN 使用下列報表 hello 習慣： 頻寬、 傳輸資料，叫用、 快取狀態、 快取點擊率、 IPV4/IPV6 傳送的資料。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 5a0d9018-8bdb-48ff-84df-23648ebcf763
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d27e6f60acaed66abb27d860c3a3e2e81c9f60cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-azure-cdn-usage-patterns"></a>分析 Azure CDN 使用模式

[!INCLUDE[cdn-verizon-only](../../includes/cdn-verizon-only.md)]

hello 指南會經歷 hello 步驟 tooview hello 核心報表透過 Verizon 設定檔的 hello 管理網站。 您也可以匯出核心分析資料 toostorage、 事件中心或 Verizon 和 Akamai 設定檔的記錄分析 (oms) [hello azure 入口網站透過](cdn-log-analysis.md)。

您可以檢視您的 CDN 使用 hello 遵循報表使用模式：

* 頻寬
* 傳輸的資料
* 點擊
* 快取狀態
* 快取點擊率
* 已轉送的 IPV4/IPV6 資料

## <a name="accessing-core-reports"></a>存取核心報告
1. 從 hello CDN 設定檔刀鋒視窗中，按一下 [hello**管理**] 按鈕。
   
    ![[CDN 設定檔] 刀鋒視窗的 [管理] 按鈕](./media/cdn-reports/cdn-manage-btn.png)
   
    hello CDN 管理入口網站隨即開啟。
2. 暫留在 hello**分析** 索引標籤，然後暫留在 hello**核心報告**彈出式視窗。  按一下想要的 hello hello 功能表中的報表。
   
    ![CDN 管理入口網站 - 核心報告功能表](./media/cdn-reports/cdn-core-reports.png)

## <a name="bandwidth"></a>頻寬
hello 頻寬 」 報表所組成的 HTTP 和 HTTPS 指出 hello 頻寬使用量，透過在特定時間週期圖表及資料表。 您可以跨所有 CDN 快顯或特定的快顯檢視 hello 頻寬使用量。 這可讓您 tooview hello 流量尖峰和發佈，CDN 快顯中 Mbps 之間。

* 從所有節點選取所有邊緣節點 toosee 流量，或從 hello 下拉式清單中選擇特定地區/節點。
* 選取日期範圍 tooview 資料此今天/週/本月等或輸入自訂的日期，然後按一下"go"toomake 確認已更新您的選擇。
* 您可以匯出和 hello，即可下載 hello 資料的 excel 工作表圖示位於 下一步太"go 的"。

hello 報表並更新每隔 5 分鐘。

![頻寬報告](./media/cdn-reports/cdn-bandwidth.png)

## <a name="data-transferred"></a>傳輸的資料
此報表包含指出的 HTTP 和 HTTPS 的 hello 流量使用方式，透過在特定時間週期的圖形和資料表格。 您可以跨所有 CDN 快顯或特定的快顯檢視 hello 流量使用方式。 這可讓您 tooview hello 流量尖峰和散發，透過 CDN 快顯以 gb 為單位。

* 從所有的便箋中選取所有邊緣節點 toosee 流量，或從 hello 下拉式清單中選擇特定地區/節點。
* 選取日期範圍 tooview 資料此今天/週/本月等或輸入自訂的日期，然後按一下"go"toomake 確認已更新您的選擇。
* 您可以匯出和 hello，即可下載 hello 資料的 excel 工作表圖示位於 下一步太"go 的"。

hello 報表並更新每隔 5 分鐘。

![傳輸的資料報告](./media/cdn-reports/cdn-data-transferred.png)

## <a name="hits-status-codes"></a>點擊 (狀態碼)
此報表說明 hello 發佈的要求狀態碼為您的內容。 內容的每個要求都會產生 HTTP 狀態碼。 hello 狀態碼說明邊緣快顯的 hello 要求的處理方式。 例如，2xx 狀態碼表示該 hello 成功處理要求 tooa 用戶端，而 4xx 狀態碼表示發生錯誤。 如需 HTTP 狀態碼的詳細資料，請參閱 [狀態碼](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)。

* 選取日期範圍 tooview 資料此今天/週/本月等或輸入自訂的日期，然後按一下"go"toomake 確認已更新您的選擇。
* 您可以匯出，而且按一下 hello 下載 hello 資料 excel 工作表位於接下來太"go 的"。

![點擊報告](./media/cdn-reports/cdn-hits.png)

## <a name="cache-statuses"></a>快取狀態
此報表說明 hello 發佈的快取命中和快取遺漏憑藉 「 用戶端要求。 Hello 最快的效能來自快取叫用，因為可以最佳化資料傳送速度降至最低的快取遺漏和過期的快取點擊率。 設定您指定 「 無快取 」 回應標頭的來源伺服器 tooavoid，避免在絕對必要，但快取查詢字串並避免非快取的回應碼，可能會降低快取遺漏。 過期的快取點擊可以避免藉由將資產的最大存留期，只要可能 toominimize hello 要求 toohello 原始伺服器的數目。

![快取狀態報告](./media/cdn-reports/cdn-cache-statuses.png)

### <a name="main-cache-statuses-include"></a>主要的快取狀態包括：
* TCP_HIT：從邊緣提供。 hello 物件已快取中，而且不超過最大期限。
* TCP_MISS：從來源提供。 hello 物件不在快取中，hello 回應後 tooorigin。
* TCP_EXPIRED _MISS：利用來源重新驗證之後從來源提供。 hello 物件已快取中，但已超過其最大存留期。 重新驗證與來源產生要取代原始的新回應 hello 快取物件。
* TCP_EXPIRED _HIT：利用來源重新驗證之後從邊緣提供。 hello 物件已快取中，但已超過其最大存留期。 Hello 來源伺服器重新驗證會導致不想要修改的 hello 快取物件。
* 選取日期範圍 tooview 資料此今天/週/本月等或輸入自訂的日期，然後按一下"go"toomake 確認已更新您的選擇。
* 您可以匯出和 hello，即可下載 hello 資料的 excel 工作表圖示位於 下一步太"go 的"。

### <a name="full-list-of-cache-statuses"></a>快取狀態的完整清單
* TCP_HIT-這個狀態報告時直接從 hello POP toohello 用戶端處理要求。 從快顯當 hello POP 最接近 toohello 用戶端上快取，並且具有有效的存留時間或 TTL 立即提供資產。 TTL 取決於下列回應標頭的 hello:
  
  * Cache-Control: s-maxage
  * Cache-Control: max-age
  * Expires
* TCP_MISS-這個狀態表示 hello 要求資產的快取的版本已找不到的 hello POP 最接近 toohello 用戶端上。 hello 資產將會從來源伺服器或原始保護盾伺服器要求。 如果 hello 原始伺服器或 hello 原始保護盾伺服器傳回資產，它會提供 toohello 用戶端和快取 hello 用戶端和 hello 邊緣伺服器。 否則，將會傳回非 200 狀態碼 (例如，403 禁止，404 找不到等)。
* TCP_EXPIRED _HIT-這個狀態報告目標 ttl 過期，例如當 hello 資產的最大存留期已到期，資產的要求已由提供直接從 hello POP toohello 用戶端時。
  
    過期的要求通常會導致重新驗證要求 toohello 原始伺服器。 為了讓 TCP_EXPIRED _HIT toooccur，hello 原始伺服器必須指出較新版的 hello 資產不存在。 這種情況通常會更新該資產的 Cache-Control 和 Expires 標頭。
* TCP_EXPIRED _MISS-這個狀態報告時從 hello POP toohello 用戶端提供較新版本已過期的快取資產。 快取資產 hello TTL 已經過期時，發生這種的情況 （例如過期保留時間上限） 和 hello 來源伺服器會傳回該資產的較新版本。 這個新版本的 hello 資產將會服務 toohello 用戶端，而不是 hello 快取版本。 此外，它將會快取 hello 邊緣伺服器與 hello 用戶端。
* CONFIG_NOCACHE-這個狀態表示客戶專屬的組態，在我們的邊緣快顯，導致無法快取的 hello 資產。
* NONE - 這個狀態指出快取內容的有效性檢查並未執行。
* TCP_ CLIENT_REFRESH _MISS-HTTP 用戶端 （例如瀏覽器） 強制執行從 hello 原始伺服器的邊緣 POP tooretrieve 過時資產的新版本時，此狀態的報告。
  
    根據預設，我們的伺服器可以防止 HTTP 用戶端在從 hello 原始伺服器強制我們的邊緣伺服器 tooretrieve hello 資產的新版本。
* TCP_ PARTIAL_HIT - 當位元組範圍要求導致部分快取資產的點擊時，就會傳回此狀態。 hello 要求立即從 hello POP toohello 用戶端提供的位元組範圍。
* 快取-資產的快取控制項和 Expires 標頭指出，它應該不會快取彈出或 hello HTTP 用戶端時，會報告此狀態。 這些類型的要求被由 hello 原始伺服器

## <a name="cache-hit-ratio"></a>快取點擊率
此報表指出 hello 直接從快取服務的快取要求百分比。

hello 報表會提供下列詳細資料的 hello:

* hello 要求上 hello POP 最接近 toohello 要求者已快取內容。
* 直接從 hello 網路邊緣的我們處理 hello 要求。
* hello 要求不需要重新驗證與 hello 原始伺服器。

hello 報表不包含：

* 拒絕由於 toocountry 篩選選項的要求。
* 資產的要求，其標頭指出他們不應該快取。 例如，Cache-Control: private、Cache-Control: no-cache 或 Pragma: no-cache 等標頭會防止資產被快取。
* 部分快取內容的位元組範圍要求。

hello 公式是: (TCP_ 點擊 / (TCP_ 叫用 + TCP_MISS)) * 100

* 選取日期範圍 tooview 資料此今天/週/本月等或輸入自訂的日期，然後按一下"go"toomake 確認已更新您的選擇。
* 您可以匯出和 hello，即可下載 hello 資料的 excel 工作表圖示位於 下一步太"go 的"。

![快取點擊率報告](./media/cdn-reports/cdn-cache-hit-ratio.png)

## <a name="ipv4ipv6-data-transferred"></a>已轉送的 IPV4/IPV6 資料
此報告會顯示 hello 流量使用分布在 IPV4 與 IPV6。

![已轉送的 IPV4/IPV6 資料](./media/cdn-reports/cdn-ipv4-ipv6.png)

* 選取此今天/週/本月份日期範圍 tooview 資料等，或輸入自訂的日期。
* 然後，按一下"go"toomake 確認已更新您的選擇。

## <a name="considerations"></a>考量
報表只能產生 hello 內最後一個 18 個月。


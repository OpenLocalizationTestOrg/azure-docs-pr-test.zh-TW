---
title: "aaaDashboard 監視器、 小數位數、 設定和 BizTalk 服務的混合式連線 |Microsoft 文件"
description: "深入了解 hello 控制項和監視效能 hello 傳統入口網站 索引標籤上的 BizTalk 服務： 儀表板、 監視器、 小數位數、 設定和混合式連線。 MABS，WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7a1815db-0de2-4274-8be0-198c1b077324
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c9fafdad20489571ee3849bbacd2c2b10933154f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="review-hello-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a>檢閱 hello 儀表板、 監視器、 小數位數、 設定和混合式連接索引標籤

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

建立 BizTalk 服務和部署您的應用程式之後，您可以變更某些 hello BizTalk 服務設定和監視 hello 應用程式效能。 

當您開啟 hello Azure 傳統入口網站時，系統會自動引導您前往 hello**所有項目** 索引標籤 tooview BizTalk 服務中，選取您的 BizTalk 服務中 hello**所有項目** 索引標籤或選取 hello **BIZTALK 服務**索引標籤上;，然後選取 BizTalk 服務名稱。

這會開啟新視窗以 hello 下列索引標籤。 本主題說明這些索引標籤。

## <a name="quickstart-quickstartquickstart"></a>快速入門 (![快速入門][Quickstart])
根據 hello BizTalk 服務版本，可能無法使用所有列出的選項。 

<table border="1">
    <tr>
        <td><strong>取得 hello 工具</strong></td>
        <td>下載 hello BizTalk 服務 SDK tooinstall hello Visual Studio 專案範本在內部部署開發電腦上。 這些範本會建立 hello <strong>BizTalk 服務</strong>(bridge) 和 hello <strong>BizTalk 服務成品</strong>部署的 tooyour BizTalk 服務的 （轉換） Visual Studio 專案。
        <br/><br/>
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">開始使用我該如何 hello Azure BizTalk 服務 SDK</a>和<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">安裝 hello Azure BizTalk 服務 SDK</a>清單 hello 步驟 tooget 啟動。
        </td>
    </tr>
    <tr>
        <td><strong>建立夥伴協議</strong></td>
        <td>開啟 hello Azure BizTalk 服務入口網站裝載於 Azure，讓您加入夥伴和建立 X12、 AS2 和 EDIFACT EDI 協議。
        <br/><br/>
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">設定元件的 BizTalk 服務入口網站上的 EDI 傳訊</a>清單 hello 步驟 tooget 啟動。
        </td>
    </tr>

<tr>
        <td><strong>深入了解 BizTalk 服務</strong></td>
        <td>移 toohello<a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">學習中心</a>toolearn 更多關於 Azure BizTalk 服務。</td>
</tr>
</table>


在底部 hello hello 工作列，您可以：

<table border="1">

<tr>
<td><strong>管理</strong>應用程式部署</td>
<td>開啟 hello Azure BizTalk 服務入口網站。 hello BizTalk 服務入口網站是 hello 進入 tooEDI 的設定，包括加入夥伴和建立 X12、 AS2 和 EDIFACT 協議。
<br/><br/>
這是與相同 hello<strong>建立夥伴協議</strong>上 hello<strong>快速入門</strong> 索引標籤。
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">設定元件的 BizTalk 服務入口網站上的 EDI 傳訊</a>hello BizTalk 服務入口網站上提供的詳細資訊。</td>
</tr>

<tr>
<td><strong>連接資訊</strong>的 hello 存取控制命名空間</td>
<td>當您選取的連接資訊時，然後 hello 存取控制命名空間、 預設簽發者，並且顯示預設索引鍵。 您可以複製這些值。
<br/><br/>
您也可以開啟 hello 存取控制入口網站。 <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">建立存取控制命名空間</a>hello 存取控制入口網站上提供的詳細資訊。</td>
</tr>

<tr>
<td><strong>同步索引鍵</strong>hello 儲存體帳戶中</td>
<td>當建立儲存體帳戶時，會自動建立主要金鑰和次要金鑰。 這些加密金鑰控制存取 tooyour 儲存體帳戶。 您的 BizTalk 服務會自動使用 hello 主索引鍵。 <strong>同步索引鍵</strong>啟用使用者 tooswitch hello 主索引鍵與 hello 次要索引鍵之間，而不會中斷 hello BizTalk 服務。
<br/><br/>
例如，您會想 hello BizTalk 服務 toouse hello 儲存體帳戶的新主索引鍵。 toodo 這樣：
<br/><br/>
<ol>
<li>選取 BizTalk 服務，再選取 [同步金鑰]<strong></strong>。 選取 hello 次要金鑰。 當您這樣做時，hello BizTalk 服務使用啟動 hello 次要金鑰。</li>
<li>在 hello Azure 傳統入口網站，選取儲存體帳戶並重新產生 hello 主索引鍵。 請記住，您的 BizTalk 服務使用 hello 次要金鑰。</li>
<li>選取 BizTalk 服務，再選取 [同步金鑰]<strong></strong>。 現在，選取 hello 主索引鍵。 這是新 hello 您重新產生的主索引鍵。</li>
<li>在 hello Azure 傳統入口網站，選取儲存體帳戶，然後重新產生次要金鑰 hello。</li>
</ol>
<br/>
此程序稱為「換用金鑰」。 hello 目的是 tooenable 使用者 tooswitch hello 主索引鍵與 hello 次要索引鍵之間，而不會中斷 hello BizTalk 服務。</td>
</tr>

<tr>
<td><strong>刪除</strong>應用程式</td>
<td>當您選取 刪除 BizTalk 服務和所有部署的項目 tooit 會移除。</td>
</tr>
</table>


## <a name="dashboard"></a>儀表板
根據 hello BizTalk 服務版本，可能無法使用所有列出的選項。 

當您選取 BizTalk 服務名稱時，則會顯示 hello 儀表板 索引標籤。 在 [儀表板] 裡，您可以：

##### <a name="usage-overview-shows-hello-number-of-used-hybrid-connections"></a>使用量概觀： 會顯示 hello 使用混合式連接的數目
以 gb 為單位，也會顯示 hello 資料使用量。 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a>度量圖：顯示固定的效能度量清單。
這些度量會提供有關 hello hello BizTalk 服務健全狀況的即時值。 您也可以選擇 hello**相對**或**絕對**值和 hello 時間範圍**間隔**的 hello 圖形中顯示的 hello 度量。 

如需這些效能度量的說明，請移至太[可用的度量](#Metrics)本主題中。

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a>快速瀏覽：列出 BizTalk 服務屬性
<table border="1">

<tr>
<td><strong>更新追蹤資料庫認證</strong></td>
<td>變更 hello 使用者名稱和密碼來 toolog hello 追蹤資料庫。</td>
</tr>
<tr>
<td><strong>更新 SSL 憑證</strong></td>
<td>可以更新 hello BizTalk 服務 toouse 不同的 SSL 憑證。 自我簽署的 SSL 憑證時，會自動建立您<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">建立 BizTalk 服務的 hello</a>。</td>
</tr>
<tr>
<td><strong>下載憑證</strong></td>
<td>您可以下載 BizTalk 服務 tooa 本機電腦所使用的 hello SSL 憑證。</td>
</tr>
<tr>
<td><strong>狀態</strong></td>
<td>顯示 hello BizTalk 服務的目前狀態。 請參閱 <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk 服務：服務狀態圖</a> (英文)。 </td>
</tr>
<tr>
<td><strong>服務 URL</strong></td>
<td>您的 BizTalk 服務的 hello URL。 這是為 hello hello 相同<strong>網域 URL</strong>輸入建立 BizTalk 服務時。</td>
</tr>
<tr>
<td><strong>公用虛擬 IP (VIP) 位址</strong></td>
<td>hello IP 位址指派 tooyour BizTalk 服務。 它用於所有的輸入端點，而且是 hello 輸出流量的來源位址。 此 IP 位址所屬 tooyour BizTalk 服務，只要它會建立。 如果您刪除 hello BizTalk 服務，hello IP 位址指派 tooanother BizTalk 服務。</td>
</tr>
<tr>
<td><strong>ACS 命名空間</strong></td>
<td>向 hello BizTalk 服務。</td>
</tr>
<tr>
<td><strong>版本</strong></td>
<td>列出版本建立 hello BizTalk 服務時所輸入的 hello。</td>
</tr>
<tr>
<td><strong>位置</strong></td>
<td>顯示 hello 主控 BizTalk 服務的地理區域。</td>
</tr>
<tr>
<td><strong>建立時間</strong></td>
<td>建立 BizTalk 服務顯示 hello 日期和時間 hello。</td>
</tr>
<tr>
<td><strong>追蹤資料庫</strong></td>
<td>儲存追蹤資料表，您的 BizTalk 服務所使用的 hello hello Azure SQL Database 名稱。 
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">需求說明</a>提供 hello 追蹤資料庫的詳細資訊。</td>
</tr>
<tr>
<td><strong>監視/封存儲存體</strong></td>
<td>儲存監視 BizTalk 服務的輸出 hello hello Azure 儲存體帳戶名稱。
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">需求說明</a>提供 hello 儲存體帳戶的詳細資訊。</td>
</tr>
<tr>
<td><strong>訂用帳戶名稱</strong></td>
<td>列出裝載您的 BizTalk 服務的 hello 訂用帳戶。 hello 訂閱控管存取 toohello Azure 傳統入口網站。</td>
</tr>
<tr>
<td><strong>訂用帳戶識別碼</strong></td>
<td>建立訂用帳戶時，會自動產生訂用帳戶識別碼。 當使用 REST Api，您可能需要 tooenter hello 訂用帳戶識別碼。</td>
</tr>
</table>

[BizTalk 服務： 佈建使用 Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=302280)清單 hello 步驟 toocreate BizTalk 服務。

##### <a name="manage-connection-information-sync-keys-and-delete-in-hello-task-bar"></a>管理連接資訊，同步金鑰及 hello 工作列中刪除：
<table border="1">

<tr>
<td><strong>管理</strong>應用程式部署</td>
<td>開啟 hello Azure BizTalk 服務入口網站。 hello BizTalk 服務入口網站是 hello 進入 tooEDI 的設定，包括加入夥伴和建立 X12、 AS2 和 EDIFACT 協議。
<br/><br/>
這是與相同 hello<strong>建立夥伴協議</strong>上 hello<strong>快速入門</strong> 索引標籤。
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">設定元件的 BizTalk 服務入口網站上的 EDI 傳訊</a>hello BizTalk 服務入口網站上提供的詳細資訊。</td>
</tr>
<tr>
<td><strong>連接資訊</strong>的 hello 存取控制命名空間</td>
<td>顯示 hello 存取控制命名空間、 預設簽發者和預設金鑰值。這可以複製。
<br/><br/>
您也可以開啟 hello 存取控制入口網站。 此存取控制入口網站是 hello 與 hello 左側的導覽窗格中使用 hello Active Directory 選項相同。
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">管理您的 ACS 命名空間</a>hello 存取控制入口網站上提供的詳細資訊。</td>
</tr>
<tr>
<td><strong>同步索引鍵</strong>hello 儲存體帳戶中</td>
<td>當建立儲存體帳戶時，會自動建立主要金鑰和次要金鑰。 這些加密金鑰控制存取 tooyour 儲存體帳戶。 您的 BizTalk 服務會自動使用 hello 主索引鍵。 <strong>同步索引鍵</strong>啟用使用者 tooswitch hello 主索引鍵與 hello 次要索引鍵之間，而不會中斷 hello BizTalk 服務。
<br/><br/>
例如，您會想 hello BizTalk 服務 toouse hello 儲存體帳戶的新主索引鍵。 toodo 這樣：
<br/><br/>
<ol>
<li>選取 BizTalk 服務，再選取 [同步金鑰]<strong></strong>。 選取 hello 次要金鑰。 當您這樣做時，hello BizTalk 服務使用啟動 hello 次要金鑰。</li>
<li>在 hello Azure 傳統入口網站，選取儲存體帳戶並重新產生 hello 主索引鍵。 請記住，您的 BizTalk 服務使用 hello 次要金鑰。</li>
<li>選取 BizTalk 服務，再選取 [同步金鑰]<strong></strong>。 現在，選取 hello 主索引鍵。 這是新 hello 您重新產生的主索引鍵。</li>
<li>在 hello Azure 傳統入口網站，選取儲存體帳戶，然後重新產生次要金鑰 hello。</li>
</ol>
<br/>
此程序稱為「換用金鑰」。 hello 目的是 tooenable 使用者 tooswitch hello 主索引鍵與 hello 次要索引鍵之間，而不會中斷 hello BizTalk 服務。</td>
</tr>

<tr>
<td><strong>刪除</strong>應用程式</td>
<td>您的 BizTalk 服務和所有部署的項目 tooit 被移除。</td>
</tr>
</table>


## <a name="monitor"></a>監視
不會套用 toohello 免費版本。

當您選取 BizTalk 服務名稱時，hello 監視 索引標籤使用，並顯示 hello 下列：

##### <a name="metric-graph-displays-hello-selected-performance-metrics"></a>顯示 hello 選取效能度量的度量的圖表：
這些度量會提供有關 hello hello BizTalk 服務健全狀況的即時值。 請選擇要顯示哪些效能度量。 一次最多同時顯示六個效能度量。 

您也可以選擇 hello**相對**或**絕對**值和 hello 時間範圍**間隔**的 hello 度量資訊會顯示。 

##### <a name="tooremove-or-display-metrics-in-hello-graph"></a>hello 圖形中 tooremove 或顯示度量：
1. 選取 hello**監視器** 索引標籤。
2. 選取**加入度量**hello 工作列中：  
   ![選取 [新增度量]][AddMetrics]
3. 請檢查您想要 toodisplay hello 效能度量。
4. 選取 hello 核取記號 tooreturn toohello**監視器** 索引標籤。
5. 選取該度量值 hello 圓形下一步 toohello 度量 toodisplay hello 圖形中。  
   
    例如，hello **CPU 使用量**度量呈現灰色，則其輸出不會顯示在 hello 圖形：  
   ![CPU 使用量度量呈現灰色][GrayedMetric]  
   
    選取 hello 灰色圓形 tooenable hello **CPU 使用量**度量 toodisplay hello 圖形中的其輸出：  
   ![CPU 使用量度量已啟用][EnabledMetric]
6. tooremove hello 顯示圖形與 hello 清單中，度量選取**刪除度量**hello 工作列中。 tooadd hello 度量後 toohello 清單中，選取**加入度量**在 hello 工作列上，核取 hello 度量，並選取 hello 核取記號 tooreturn toohello**監視器** 索引標籤。選取 hello 圓形 tooenable hello 度量呈現灰色。

## <a name="Metrics"></a>可用的度量
下列效能計數器度量的 hello 可用：

<table border="1">

<tr>
<td><strong>往返延遲</strong></td>
<td>顯示 hello 的平均使用時間 （毫秒） （毫秒） tooprocess 跨所有橋接器 hello BizTalk 服務所完全處理 hello 訊息之前收到來自 hello 時間 hello 訊息的訊息。 只會計算成功處理的訊息。<br/><br/>
Hello 下列事件發生時，會建立時間戳記：
<ul>
<li>訊息進入 hello 閘道</li>
<li>訊息是路由的 toohello 目的地</li>
<li>收到目的地回應</li>
<li>目的地通知傳送回應 toohello 閘道</li>
</ul>
<br/>
此標準會顯示 hello 結果 hello 下列計算：
<br/><br/>
[目的地通知傳送回應 toohello gateway]-[訊息進入 hello 閘道]</td>
</tr>
<tr>
<td><strong>來源失敗</strong></td>
<td>顯示 hello 總數失敗的訊息所 hello 提取從 hello 來源端點的訊息時，BizTalk 服務。</td>
</tr>
<tr>
<td><strong>CPU 使用率</strong></td>
<td>列出 hello 平均處理器時間百分比的所有角色執行個體。</td>
</tr>
<tr>
<td><strong>處理延遲</strong></td>
<td>顯示 hello 中跨所有橋接器，但不包括 hello 時間 hello BizTalk 服務的訊息目的地所花費的毫秒 (ms) tooprocess 所花費的平均時間。 只會計算成功處理的訊息。<br/><br/>
每個 hello 下列事件發生時，會建立時間戳記：

<ul>
<li>訊息進入 hello 閘道</li>
<li>訊息是路由的 toohello 目的地</li>
<li>收到目的地回應</li>
<li>目的地通知傳送回應 toohello 閘道</li>
</ul>
<br/>此標準會顯示 hello 結果 hello 下列計算：<br/><br/>
[目的地通知傳送回應 toohello gateway]-[訊息進入 hello 閘道]-[目的地未收到回應時] + [訊息是路由的 toohello 目的地]</td>
</tr>
<tr>
<td><strong>處理時失敗</strong></td>
<td>顯示 hello 總數無法在處理期間由跨所有 hello 橋接器 hello BizTalk 服務的時間間隔內的訊息。</td>
</tr>
<tr>
<td><strong>已傳送的訊息</strong></td>
<td>顯示 hello 跨所有橋接器 hello BizTalk 服務所傳送的時間間隔內的訊息總數。 此標準會在從管線所傳送的訊息到達 hello 路由目的地時累加。 此度量不表示已成功處理訊息。<br/><br/>
在要求-回覆案例中，當 hello 路由目的地傳送回條認可後 toohello 管線時，就會遞增 hello 度量。</td>
</tr>
<tr>
<td><strong>已接收的訊息</strong></td>
<td>顯示 hello 跨所有橋接器 hello BizTalk 服務的時間間隔內接收的訊息總數。 Hello 管線收到一封新郵件時，就會遞增此標準。</td>
</tr>
<tr>
<td><strong>處理中的訊息</strong></td>
<td>顯示 hello 目前正在處理的 hello BizTalk 服務的時間間隔內的訊息總數。</td>
</tr>
<tr>
<td><strong>已處理的訊息</strong></td>
<td>顯示 hello 順利處理的時間間隔內跨所有橋接器 hello BizTalk 服務的訊息總數。 訊息已成功收到 hello 管線 」 和 「 已成功路由的 toohello 目的地時，就會遞增此標準。</td>
</tr>
</table>


## <a name="scale"></a>調整
Hello 調整 索引標籤中，您可以加入或減去 hello BizTalk 服務所使用的單位數目。 依預設已設定一個單位。 額外的單位可以加入 tooscale BizTalk 服務。 當您增加 hello 標尺時，您正在提高輸送量。 資源的 hello 數量也會增加，包括已部署的橋接器、 合約、 LOB 連線和處理能力。 例如，您會增加 hello 小數位數，從 1 單位 too2 單位。 在此情況下，您可以部署雙 hello 橋接器、 double hello 協議，double hello LOB 連接數目，以及雙 hello 的處理能力。

有些 BizTalk 版本不提供調整選項。 在此情況下，只允許一個單位。 toodetermine 多少單位可以調整您的版本，參閱太[BizTalk 服務： 版本圖表](biztalk-editions-feature-chart.md)。

增加 hello 單位數目可能會影響定價。 如果您增加 hello 單位，則選取**儲存**會顯示訊息，告訴您計費會受到影響。 然後，您可以選擇在 toocontinue。 當您增加 hello 單位數目時，hello BizTalk 服務的狀態會從作用中 tooUpdating 變更。 在 hello 更新狀態，您的 BizTalk 服務會繼續 toorun。

[BizTalk 服務：版本圖表](biztalk-editions-feature-chart.md) 定義「單位」。

## <a name="configure"></a>設定
不適用 tooHybrid 連線。

Hello 備份狀態 tooNone] 或 [自動設定。 當設定 tooNone，備份會自動建立。 當設定 tooAutomatic，您可以設定 hello 備份位置、 hello 頻率 hello 備份，以及多久 tookeep hello 備份檔案。 

[BizTalk 服務： 備份和還原](biztalk-backup-restore.md)提供 hello 詳細資料。 

## <a name="HybridConnections"></a>混合式連線
混合式連接連接 Azure 應用程式，例如 Web 應用程式或行動應用程式在 Azure 應用程式服務中，使用靜態 TCP 連接埠，例如 SQL Server、 MySQL、 HTTP 的 Web Api 和最自訂的 Web 服務的 tooan 在內部部署資源。 BizTalk 服務的 hello Azure 傳統入口網站中管理混合式連接。

toocreate 混合式連線，在 Azure 應用程式服務，請參閱[存取內部部署混合式連線使用 Azure App Service 中的資源](../app-service-web/web-sites-hybrid-connection-get-started.md)。

toocreate 或管理在 Azure BizTalk 服務混合式連線，請參閱[混合式連線](integration-hybrid-connection-overview.md)。

## <a name="next"></a>下一步
既然您已熟悉 hello 不同索引標籤，您可以深入了解 hello Azure BizTalk 服務的功能：

* [BizTalk 服務：節流](biztalk-throttling-thresholds.md)  
* [BizTalk 服務：簽發者名稱和簽發者金鑰](biztalk-issuer-name-issuer-key.md)  
* [BizTalk 服務：備份與還原](biztalk-backup-restore.md)

## <a name="see-also"></a>另請參閱
* [混合式連線](integration-hybrid-connection-overview.md)  
* [BizTalk 服務：開發人員、基本、標準和高級版本圖表](biztalk-editions-feature-chart.md)  
* [BizTalk 服務：使用 Azure 傳統入口網站進行佈建](biztalk-provision-services.md)  
* [BizTalk 服務：BizTalk 服務狀態圖](biztalk-service-state-chart.md)  
* [開始使用我要如何 hello Azure BizTalk 服務 SDK](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png


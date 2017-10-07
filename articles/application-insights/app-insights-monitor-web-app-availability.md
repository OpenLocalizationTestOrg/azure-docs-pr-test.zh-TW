---
title: "aaaMonitor 可用性和回應的任何網站 |Microsoft 文件"
description: "在 Application Insights 中設定 Web 測試。 如果網站無法使用或回應緩慢，將收到警示。"
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 46dc13b4-eb2e-4142-a21c-94a156f760ee
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: bwren
ms.openlocfilehash: 4c5425c948770cc57a648ca50e217c75ac75fbd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-availability-and-responsiveness-of-any-web-site"></a>監視任何網站的可用性和回應性
您已部署您的 web 應用程式或網站 tooany 伺服器之後，您可以設定測試 toomonitor 其可用性和回應性。 [Azure 的 Application Insights](app-insights-overview.md)傳送 web 要求 tooyour 應用程式上定期從 hello 世界各地的點。 如果應用程式沒有回應或回應太慢，則會警告您。

您可以設定可用性測試的任何 HTTP 或 HTTPS 端點可從存取 hello 公用網際網路。 您不需要 tooadd 任何您要測試的 toohello 網站。 即使沒有 toobe 網站： 您可以測試您所仰賴的 REST API 服務。

可用性測試有兩種：

* [URL ping 測試](#create)： 您可以在 hello Azure 入口網站中建立簡單的測試。
* [多重步驟 web 測試](#multi-step-web-tests)： 您在 Visual Studio Enterprise 和上傳 toohello 入口網站中建立的。

您可以建立註冊 too25 可用性測試每個應用程式資源。

## <a name="create"></a>1.開啟可用性測試報告的資源

**如果您已經設定 Application Insights**您 web 應用程式中，開啟其 Application Insights 資源在 hello [Azure 入口網站](https://portal.azure.com)。

**或如果您想在新的資源中，報表 toosee**太註冊[Microsoft Azure](http://azure.com)，go toohello [Azure 入口網站](https://portal.azure.com)，並建立 Application Insights 資源。

![New > Application Insights](./media/app-insights-monitor-web-app-availability/11-new-app.png)

按一下**所有資源**hello 新資源的 tooopen hello 概觀刀鋒視窗。

## <a name="setup"></a>2.建立 URL Ping 測試
開啟 hello 可用性刀鋒視窗，並加入測試。

![填滿至少 hello 您網站的 URL](./media/app-insights-monitor-web-app-availability/13-availability.png)

* **hello URL**可以是任何網頁想 tootest，但是它必須從可見 hello 公用網際網路。 hello URL 可以包含查詢字串。 例如，您可以訓練一下您的資料庫。 如果 hello URL 解析 tooa 重新導向，我們追蹤它 too10 重新導向。
* **剖析相依要求**: hello 測試如果勾選此選項，要求映像、 指令碼、 樣式檔案及其他檔案 hello 受測的 web 網頁的一部分。 hello 記錄的回應時間包括 hello 所花費時間 tooget 這些檔案。 如果所有這些資源無法 hello hello 整個測試的逾時內已成功下載，hello 測試將會失敗。 

    如果未核取 hello 選項，hello 測試只會要求在您指定的 hello URL hello 檔案。
* **啟用重試**： 若勾選此選項，hello 測試失敗時，它會重試較短的間隔之後。 只有在連續三次重試失敗後，才會回報失敗。 接著會將後續的測試執行 hello 一般測試的頻率。 重試已暫時暫止，直到 hello 下一個成功為止。 此規則可個別套用在每個測試位置。 我們建議使用這個選項。 平均來說，大約 80% 失敗會在重試後消失。
* **測試頻率**： 設定頻率 hello 測試從每個測試位置執行。 頻率為 5 分鐘且有五個測試位置，則您的網站平均每一分鐘會執行測試。
* **測試位置**是 hello 會將我們的伺服器傳送 web 要求 tooyour URL 的位置。 請選擇多個位置，以便區分網站問題與網路問題。 您可以選取 too16 位置。
* **成功準則**：

    **測試逾時**： 減少此值 toobe，提醒回應變慢。 如果未在此期間內收到來自您的站台的 hello 回應 hello 測試被視為失敗。 如果您選取**剖析相依要求**、 然後所有 hello 影像、 樣式檔案、 指令碼和其他相依的資源必須已在此期間內收到。

    **HTTP 回應**: hello 傳回視為成功的狀態碼。 200 是表示已傳回標準的 web 網頁的 hello 程式碼。

    **內容比對**：字串，例如「歡迎！ 我們會測試每個回應中的區分大小寫完全相符。 必須是單純字串，不含萬用字元。 別忘了，如果您可能必須 tooupdate 頁面內容變更它。
* **警示**，根據預設，如果會傳送 tooyou 失敗會在三個位置超過五分鐘。 可能 toobe 網路問題，而不是問題與您的網站在同一個位置失敗。 但您可以變更 hello 閾值 toobe 更多或較不區分大小寫，而且您也可以變更 hello 電子郵件應該傳送至。

    您可以設定會在產生警示時呼叫的 [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。 (不過請注意，查詢參數目前不會當作屬性傳遞)。

### <a name="test-more-urls"></a>測試更多 URL
加入更多測試。 比方說，在加法 tootesting 首頁中，您可以確定您的資料庫藉由測試搜尋 hello URL 執行。


## <a name="monitor"></a>3.查看可用性測試結果

在幾分鐘之後, 按**重新整理**toosee 測試結果。 

![Hello 家用刀鋒視窗上的摘要結果](./media/app-insights-monitor-web-app-availability/14-availSummary-3.png)

hello scatterplot 顯示 hello 的範例中有診斷測試步驟的詳細資料的測試結果。 hello 測試引擎會儲存發生失敗的測試中的診斷詳細資料。 成功的測試，診斷詳細資料會儲存 hello 執行的子集。 將滑鼠停留在任何 hello 綠色/紅點 toosee hello 測試時間戳記、 測試持續期間、 位置和測試名稱。 按一下瀏覽 hello 散佈圖 toosee hello 詳細資料中的 hello 測試結果的任何點。  

選取特定測試的位置，或減少 hello 時間週期 toosee 取得更多結果周圍 hello 感興趣的時段。 搜尋總管 toosee 產生的所有執行中，或使用此資料的分析查詢 toorun 自訂報表。

在加法 toohello 未經處理的結果，有兩個可用性度量計量瀏覽器中： 

1. 已成功，跨所有測試執行的 hello 測試的可用性： 百分比。 
2. 測試持續期間︰所有測試執行中的平均測試持續期間。

您可以在 hello 測試名稱、 位置 tooanalyze 趨勢的特定測試和 （或） 位置套用篩選。

## <a name="edit"></a> 檢查和編輯測試

從 hello 摘要 頁面上，選取特定測試。 您可以在該頁面中看見其特定結果，並加以編輯或暫時將它停用。

![Edit or disable a web test](./media/app-insights-monitor-web-app-availability/19-availEdit-3.png)

您可能想 toodisable 可用性測試或與它們相關聯規則，而您會在服務上執行維護的 hello 警示。 

## <a name="failures"></a>如果您看到失敗
按一下一個紅點。

![按一下一個紅點](./media/app-insights-monitor-web-app-availability/open-instance-3.png)


從可用性測試結果，您可以：

* 檢查從伺服器收到 hello 回應。
* 開啟應用程式伺服器處理 hello 失敗的要求執行個體時傳送嗨遙測。
* 記錄問題或 Git 或 VSTS tootrack hello 問題中工作項目。 hello bug 會包含連結 toothis 事件。
* 開啟 Visual Studio 中的 hello web 測試結果。


*看起來正常，但回報為失敗？* 請檢查所有 hello 映像、 指令碼、 樣式表和 hello 頁面所載入的任何其他檔案。 如果其中任何失敗，hello 測試報告為失敗，即使 hello 主要 html 網頁載入 [確定]。

沒有相關項目？ 如果您已針對伺服器端應用程式設定 Application Insights，這可能是因為正在進行[取樣](app-insights-sampling.md)。 

## <a name="multi-step-web-tests"></a>多重步驟 Web 測試
您可以監視涉及一連串 URL 的案例。 例如，如果您要監視的銷售的網站，您可以測試，加入項目 toohello 購物車正常運作。

> [!NOTE] 
> 進行多步驟 Web 測試此會收取費用。 [價格方案](http://azure.microsoft.com/pricing/details/application-insights/)。
> 

toocreate multi-step 測試，您使用 Visual Studio Enterprise 中，記錄 hello 案例並再上傳記錄 tooApplication Insights hello。 Application Insights 重新 hello 案例中執行的間隔，並確認 hello 回應。

> [!NOTE]
> 您無法在測試中使用已編碼的函式或迴圈。 hello 測試必須完全包含在 hello.webtest 指令碼。 不過，您可以使用標準外掛程式。
>

#### <a name="1-record-a-scenario"></a>1.記錄案例
使用 Visual Studio Enterprise toorecord web 工作階段。

1. 建立 Web 效能測試專案。

    ![在 Visual Studio Enterprise 版本中，請從 hello Web 效能和負載測試範本建立專案。](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-create.png)

 * *沒看見 hello Web 效能和負載測試範本嗎？* - 關閉 Visual Studio Enterprise。 開啟**Visual Studio 安裝程式**toomodify Visual Studio 企業版安裝。 在 [個別元件] 之下，選取 [Web 效能和負載測試工具]。

2. 開啟 hello.webtest 檔案，並開始錄製。

    ![開啟 hello.webtest 檔案，然後按一下 [記錄]。](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-start.png)
3. 請勿 hello 想 toosimulate 測試中的使用者動作： 開啟您的網站，加入產品 toohello 車等等。 然後停止測試。

    ![hello web 測試錄製器執行 Internet Explorer 中。](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-record.png)

    不要讓案例太長。 以 100 個步驟和 2 分鐘為限。
4. 編輯 hello 測試：

   * 新增驗證 toocheck 收到 hello 文字和回應碼。
   * 移除任何多餘的互動。 您也可以移除相依要求的圖片或 tooad 或追蹤的網站。

     請記住您只能編輯 hello 測試指令碼-您無法加入自訂程式碼，或呼叫其他 web 測試。 不在 hello 測試中插入迴圈。 您可以使用標準 Web 測試的外掛程式。
5. Hello 測試在中執行 Visual Studio toomake 能運作。

    hello web 測試執行器會開啟網頁瀏覽器，並重複 hello 您所錄製的動作。 請確定運作如您所預期。

    ![在 Visual Studio 中，開啟 hello.webtest 檔案並按一下 [執行]。](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-run.png)

#### <a name="2-upload-hello-web-test-tooapplication-insights"></a>2.上傳 hello web 測試 tooApplication Insights
1. 在 hello Application Insights 入口網站建立 web 測試。

    ![在 hello web 測試刀鋒視窗中，選擇 [新增]。](./media/app-insights-monitor-web-app-availability/16-another-test.png)
2. 選取多重步驟的測試，並上傳 hello.webtest 檔案。

    ![選取 [多步驟 Web 測試]。](./media/app-insights-monitor-web-app-availability/appinsights-71webtestUpload.png)

    Hello 測試集的位置、 頻率及警示參數在 hello 相同方式如 ping 測試。

#### <a name="3-see-hello-results"></a>3.請參閱 hello 結果

檢視您的測試結果和任何失敗 hello 相同的方式為單一 url 測試。

此外，您可以下載 hello 測試結果 tooview Visual Studio 中。

#### <a name="too-many-failures"></a>太多失敗項目？

* 失敗的常見原因是該 hello 測試執行時間太長。 不可執行超過兩分鐘。

* 別忘了必須載入正確的頁面上的所有 hello 資源 hello 測試 toosucceed，包括指令碼、 樣式表、 影像和其他等等。

* hello web 測試必須完全包含在 hello.webtest 指令碼： 您無法在 hello 測試中使用自動程式化的函式。

### <a name="plugging-time-and-random-numbers-into-your-multi-step-test"></a>將時間和隨機數字插入多重步驟測試中
假設您要測試的工具會從外部來源取得與時間相關的資料 (例如股票)。 在錄製您的 web 測試時，有 toouse 特定時間，但您設定測試的 hello 參數，StartTime 和 EndTime。

![具有參數的 Web 測試。](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-parameters.png)

當執行 hello 測試時，您想要的 EndTime toobe hello 永遠存在時間，而 StartTime 應該是 15 分鐘前。

Web 測試外掛程式提供 hello 方式 toodo 參數化次數。

1. 針對您想要的每個變數參數值，各加入一個 Web 測試外掛程式。 在 hello web 測試 工具列，選擇 **加入 Web 測試外掛程式**。

    ![選擇 [加入 Web 測試外掛程式]，然後選取類型。](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugins.png)

    在此範例中，我們會使用兩個執行個體的日期時間外掛程式 hello。 一個執行個體設定為 "15 minutes ago"，另一個則設定為 "now"。
2. 開啟每個外掛程式的 hello 的屬性。 加以命名，並將它設定 toouse hello 目前的時間。 對其中一個，設定 [加入分鐘] = -15。

    ![設定 [名稱]、[使用目前時間] 和 [加入分鐘]。](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-parameters.png)
3. 在 hello web 測試參數，使用 {{外掛程式 name}} tooreference 外掛程式的名稱。

    ![Hello 測試參數中使用 {{外掛程式 name}}。](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-name.png)

現在，您可以上傳您的測試 toohello 入口網站。 在每個執行 hello 測試使用 hello 動態的值。

## <a name="dealing-with-sign-in"></a>處理登入
如果您的使用者登入 tooyour 應用程式，您會有不同的選項，來模擬登入，以便您可以測試背後 hello 登入頁面。 您使用的 hello 方法，取決於 hello hello 應用程式所提供的安全性類型。

在所有情況下，您應該只針對測試的 hello 目的應用程式中建立帳戶。 可能的話，請限制 hello 這個測試帳戶的權限，讓不可能發生的 hello web 測試會影響到實際的使用者。

### <a name="simple-username-and-password"></a>簡單的使用者名稱和密碼
錄製 web 中的 hello 一般方式。 先刪除 Cookie。

### <a name="saml-authentication"></a>SAML 驗證
使用適用於 web 測試的 hello SAML 外掛程式。

### <a name="client-secret"></a>用戶端密碼
如果應用程式的登入路由牽涉到用戶端密碼，請使用此路由。 Azure Active Directory (AAD) 是可提供用戶端密碼登入的服務範例。 AAD 時，在 hello 用戶端密碼為 hello 應用程式金鑰。

以下是使用應用程式金鑰之 Azure Web 應用程式的 Web 測試範例︰

![用戶端密碼範例](./media/app-insights-monitor-web-app-availability/110.png)

1. 從使用用戶端密鑰 (AppKey) 的 AAD 取得權杖。
2. 從回應中擷取持有人權杖。
3. 呼叫 hello 授權標頭中使用持有人權杖的 API。

請確定 hello web 測試，實際的用戶端-也就是說，在 AAD-有它自己的應用程式，並使用其 clientId + appkey。 測試您的服務也有自己的應用程式在 AAD 中： hello appID 此應用程式的 URI 會反映在 hello 「 資源 」 欄位中的 hello web 測試。

### <a name="open-authentication"></a>開放驗證
使用您的 Microsoft 或 Google 帳戶登入即是開放驗證的範例。 許多應用程式，使用 OAuth 提供 hello 用戶端密碼的替代方式，因此您第一種做法應該是 tooinvestigate 以排除這個可能性。

如果您的測試必須在使用 OAuth 登入，hello 一般方法是：

* 使用網頁瀏覽器、 hello 驗證網站和您的應用程式之間的 Fiddler tooexamine hello 流量之類的工具。
* 執行兩個或多個登入使用不同的電腦或瀏覽器，或在長時間間隔 (tooallow 語彙基元 tooexpire)。
* 藉由比較不同的工作階段，找出從 hello 驗證網站時，會傳遞 tooyour 應用程式伺服器在登入之後所傳遞的 hello 語彙基元。
* 使用 Visual Studio 記錄 Web 測試。
* 參數化 hello 語彙基元，hello 驗證器，從傳回 hello 語彙基元時，設定 hello 參數，並使用 hello 查詢 toohello 站台中。
  （visual Studio 嘗試 tooparameterize hello 測試，但不會正確地參數化 hello 語彙基元）。


## <a name="performance-tests"></a>效能測試
您可以在網站上執行負載測試。 像 hello 可用性測試，您可以從我們 hello 世界各地點傳送的簡單要求或多個步驟要求。 不同於可用性測試，許多要求傳送時會同時模擬多位使用者。

從 hello 概觀刀鋒視窗中，開啟**設定**，**效能測試**。 當您建立測試時，您獲邀參與 tooconnect tooor 建立 Visual Studio Team Services 帳戶。

Hello 測試完成時，便會顯示回應時間與成功率。


![效能測試](./media/app-insights-monitor-web-app-availability/perf-test.png)

> [!TIP]
> tooobserve hello 效果的效能測試中，使用[即時資料流](app-insights-live-stream.md)和[Profiler](app-insights-profiler.md)。
>

## <a name="automation"></a>自動化
* [使用 PowerShell 指令碼 tooset 可用性測試](app-insights-powershell.md#add-an-availability-test)自動。
* 設定會在產生警示時呼叫的 [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。

## <a name="qna"></a>有疑問嗎？ 有問題嗎？
* *可以從我的 Web 測試呼叫程式碼嗎？*

    否。 hello hello 測試步驟必須在 hello.webtest 檔案。 而且您不能呼叫其他 Web 測試或使用迴圈。 但是這裡有一些您會覺得有用的外掛程式。
* *是否支援 HTTPS？*

    我們支援 TLS 1.1 和 TLS 1.2。
* *「Web 測試」和「可用性測試」之間有任何差異嗎？*

    hello 兩個詞彙都可以參考交換使用。 可用性測試更泛型的詞彙，其中包含單一 URL ping hello 除了測試 toohello multi-step web 測試。
* *我希望 toouse 可用性測試我們內部執行伺服器上的防火牆後面。*

    有兩個可能的解決方案：
    
    * 設定您防火牆 toopermit 來自內送要求 hello [IP 位址的我們的測試代理程式](app-insights-ip-addresses.md)。
    * 撰寫您自己的程式碼 tooperiodically 測試您的內部伺服器。 Hello 程式碼做為背景處理序在伺服器上執行測試您的防火牆後面。 您的測試程序可以傳送其結果 tooApplication Insights 使用[TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) hello core SDK 封裝中的應用程式開發介面。 這需要您測試伺服器 toohave 傳出存取 toohello Application Insights 擷取的端點，但這是多較小的安全性風險比 hello 另一種可允許傳入要求。 hello 結果不會出現在 hello 可用性 web 測試的刀鋒視窗，但會顯示為可用性結果中分析、 搜尋和度量的總管。
* *上傳多步驟 Web 測試失敗*

    有 300 K 的大小限制。

    不支援迴圈。

    不支援參考 tooother web 測試。

    不支援資料來源。
* *多步驟測試未完成*

    每個測試有 100 個要求的限制。

    如果它執行時間長於兩分鐘的時間，停止 hello 測試。
* *如何使用用戶端憑證執行測試？*

    很抱歉，我們不支援此功能。


## <a name="next"></a>接續步驟
[搜尋診斷記錄][diagnostic]

[疑難排解][qna]

[Web 測試代理程式的 IP 位址](app-insights-ip-addresses.md)

<!--Link references-->

[azure-availability]: ../insights-create-web-tests.md
[diagnostic]: app-insights-diagnostic-search.md
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md

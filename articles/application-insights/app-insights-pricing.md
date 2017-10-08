---
title: "為 Azure Application Insights aaaManage 定價和資料磁碟區 |Microsoft 文件"
description: "在 Application Insights 中管理遙測量和監視成本。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: ebd0d843-4780-4ff3-bc68-932aa44185f6
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: bwren
ms.openlocfilehash: 4621c989cd467735aefc48ec9547fcbe1b1ae41b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-pricing-and-data-volume-in-application-insights"></a>管理 Application Insights 的價格和資料量


[Azure Application Insights][start] 的價格是根據每個應用程式的資料量而定。 在開發期間或小型應用程式的低使用量是可能 toobe 免費的因為有 1 GB 每月額度的遙測資料。

每個 Application Insights 資源的負責為個別的服務，並提供您的訂用帳戶 tooAzure toohello 帳單。

價格方案有兩個。 hello 預設計劃稱為 Basic。 您可以選擇 hello 企業計劃，其每日費用，但可讓某些特定功能時，例如[連續匯出](app-insights-export-telemetry.md)。

如果您有關於定價的運作方式 Application Insights 的問題，則可以免費 toopost 問題我們[論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=ApplicationInsights)。 

## <a name="hello-price-plans"></a>hello 價格計劃

請參閱 hello [Application Insights 定價頁面][ pricing]目前價格以您的貨幣。

### <a name="basic-plan"></a>基本方案

hello 基本方案是 hello 預設值，當建立新的 Application Insights 資源，以及對大多數客戶來說就夠了。

* 在 hello 基本計畫中，您需要付費資料磁碟區： 遙測 Application Insights 所接收的位元組數目。 資料磁碟區會以未壓縮的 hello JSON 資料封裝 Application Insights 從您的應用程式收到 hello 大小。
如[表格式資料匯入分析](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-import)，hello 資料磁碟區以如 hello 所傳送的檔案 tooApplication Insights 未壓縮的大小。  
* 因此您只是實驗或開發，如果您已經不太可能 toohave toopay，是免費的您每個應用程式的第一個 1 GB。
* [即時計量串流](app-insights-live-stream.md)資料不會計入價格用途。
* [連續匯出](app-insights-export-telemetry.md)hello 基本計劃中適用於每個 GB 的額外費用。

### <a name="enterprise-plan"></a>企業方案

* 在 hello 企業計劃，您的應用程式可以使用所有的 Application Insights 的 hello 功能。 [連續匯出](app-insights-export-telemetry.md)和 

[記錄分析連接器](https://go.microsoft.com/fwlink/?LinkId=833039&amp;clcid=0x409)hello 企業計劃中有任何額外的免費。
* 您必須支付每個節點的所有應用程式的遙測傳送 hello 企業計劃中。 
 * 「節點」是裝載應用程式的實體或虛擬伺服器機器，或是平台即服務 (PaaS) 角色執行個體。
 * 開發用電腦、用戶端瀏覽器、行動裝置不算節點。
 * 如果您的應用程式有數個會傳送遙測的元件，例如 Web 服務和後端背景工作，會將它們分開計算。
 * [即時計量資料流](app-insights-live-stream.md)資料不會針對價格目的進行計算。* 橫跨訂用帳戶，您的費用是針對每個節點，而不是每個應用程式。 如果您有五個傳送遙測 12 應用程式，然後 hello 收費適用於五個節點的節點。
* 雖然費用是按月報價，您的收費僅適用於一個節點從一個應用程式傳送遙測的任何小時。 hello 每小時費用是 hello 加上引號的月費 / 744 (hello 在 31 天的月份中的時數)。
* 每個節點 (資料粒度為小時) 偵測每日 200 MB 的資料量配置。 未使用的資料配置不會保存從一天 toohello 下一步。
 * 如果您選擇 hello 企業定價選項，每個訂用帳戶會取得每日允許 hello 傳送遙測 toohello Application Insights 資源，該訂用帳戶中的節點數目為依據的資料。 因此如果您有 5 個節點全天傳送資料時，您必須套用的 1 GB tooall hello Application Insights 資源集區的允許該訂用帳戶中。 如果傳送的其他節點的更多資料因為 hello 包含的資料共用的所有節點之間的某些節點，並不重要。 如果在給定日子，hello Application Insights 資源會收到超過隨附於此訂閱 hello 每日資料配置的資料，hello 每 GB overage 資料的費用。 
 * hello 每日資料允許使用的計算方式為 hello 數 hello 天 （使用 UTC） 中的每個節點傳送遙測除以 24 次 200 MB。 因此如果您有 4 個節點的 hello 15 期間 hello 天 24 小時傳送遙測，hello 包含資料，就是該日 ((4 x 15) / 24) x 200 MB = 500 MB。 針對資料超額部分的 hello 2.30 USD 每 GB 的價格，如果 hello 節點傳送 1 GB 資料的那一天的 hello 費用時，可能會 1.15 美元。
 * 請注意，hello 企業計劃的每日允許使用不會共用與應用程式，您已選擇 hello 基本選項，而且未使用的允許使用不能跨越每天。 
* 以下是判斷不同節點計數的一些範例︰
| 案例                               | 每日節點總數 |
|:---------------------------------------|:----------------:|
| 1 個應用程式使用 3 個 Azure App Service 執行個體和 1 個虛擬伺服器 | 4 |
| 這些應用程式在 hello 相同訂用帳戶，並在 hello 企業計劃，2 個 Vm 和 hello Application Insights 資源上執行的應用程式 3 | 2 | 
| 4 應用程式的應用程式 Insights 資源位於 hello 相同訂用帳戶。 在 16 小時的離峰時間裡每個應用程式執行 2 個執行個體，在 8 小時的尖峰時間裡執行 4 個執行個體。 | 13.33 | 
| 雲端服務有 1 個背景工作角色和 1 個 Web 角色，各執行 2 個執行個體 | 4 | 
| 5 個節的 Service Fabric 叢集執行 50 個微服務，每個微服務執行 3 個執行個體 | 5|

* hello 精確節點計數行為取決在其上使用 Application Insights SDK，您的應用程式。 
  * 在 SDK 版本 2.2 及更新版本，同時 hello Application Insights 和[Core SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights/)或[Web SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/)將報告做為節點的每個應用程式主機，例如 hello 實體伺服器和 VM 主機或 hello 的電腦名稱在雲端服務的 hello 案例中的執行個體名稱。  只有例外狀況為應用程式，只能使用 hello [.NET Core](https://dotnet.github.io/)和 hello Application Insights Core SDK 中的案例只有一個節點將因為 hello 主機名稱無法使用的所有主機的報告。 
  * 舊版的 hello SDK，hello [Web SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/)的行為就如同 hello 較新的 SDK 版本，不過 hello [Core SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights/)會報告只有一個節點，不論實際的應用程式主機的 hello 數目。 
  * 請注意，是否您的應用程式使用 hello SDK tooset roleInstance tooa 自訂值，依預設該相同的值將做為 toodetermine hello 次數的節點。 
  * 如果您使用新的 SDK 版本與執行的用戶端電腦或行動裝置應用程式，很可能 hello 計數的節點可能會傳回數字，這可能會非常大 （從 hello 大量用戶端電腦或行動裝置）。 

### <a name="multi-step-web-tests"></a>多重步驟 Web 測試

[多步驟 Web 測試](app-insights-monitor-web-app-availability.md#multi-step-web-tests)會有一項額外的費用。 這是指 tooweb 執行之測試的一系列動作。 

單一頁面的 ping 測試沒有另外的費用。 來自 ping 測試和多步驟測試的遙測，會與來自您應用程式的其他遙測一起計費。
 
## <a name="operations-management-suite-subscription-entitlement"></a>Operations Management Suite 訂用帳戶權利

做為[最近宣布](https://blogs.technet.microsoft.com/msoms/2017/05/19/azure-application-insights-enterprise-as-part-of-operations-management-suite-subscription/)，客戶購買 Microsoft Operations Management Suite E1 和 E2 會無法 tooget 應用程式 Insights 企業不需要額外成本的其他元件。 具體來說，每個單位的 Operations Management Suite E1 和 E2 包含 hello 企業計劃的 Application Insights 的權利 too1 節點。 如先前所述，Application Insights 中的每個節點會包含總 too200 MB 的內嵌每日 （不同於擷取記錄分析資料），不需額外成本的 90 天的資料保留的資料。 

> [!NOTE]
> tooensure 您取得此權限，您必須擁有您 hello 企業中的 Application Insights 資源定價計劃。 因此 hello 基本方案中的 Application Insights 資源不會知道有任何好處，只做為節點，適用於此權利。 請注意，此權限將不會顯示在 hello 估計成本 hello 功能 + 定價刀鋒視窗上顯示。 
>
 
## <a name="review-pricing-plans-and-estimate-costs"></a>檢閱定價方案和估計成本

Applicaition Insights 可讓您輕鬆 toounderstand hello 定價方案可用哪些 hello 成本可能會根據最近的使用模式。 先開啟 hello**功能 + 定價**刀鋒視窗中 hello hello Azure 入口網站中的 Application Insights 資源：

![選擇價格。](./media/app-insights-pricing/01-pricing.png)

**a.** 檢閱 hello 月份的資料量。 這包括所有的 hello 資料接收和保留 (之後任何[取樣](app-insights-sampling.md)從您的伺服器和用戶端應用程式，以及可用性測試。

**b.** 進行[多步驟 Web 測試](app-insights-monitor-web-app-availability.md#multi-step-web-tests)需另外收費。 （這不包括包含 hello 資料磁碟區費用的簡單可用性測試）。

**c.** 啟用 hello 企業計劃。

**d.** 按一下 透過 toodata 管理選項 tooview 的資料量 hello 上個月、 設定每日最或將擷取取樣。

應用程式 Insights 費用會加入 tooyour Azure 帳單。 您可以查看詳細資料的 Azure 上 hello 計費 > 一節的 hello Azure 入口網站，或在 hello 收費[Azure Billing Portal](https://account.windowsazure.com/Subscriptions)。 

![Hello 側邊功能表上，選擇計費。](./media/app-insights-pricing/02-billing.png)

## <a name="data-rate"></a>資料速率
有三種的方法在哪一個 hello 傳送資料的磁碟區會限制：

* **取樣：**可以使用這項機制的遙測資料從您伺服器和用戶端應用程式，使用的度量最小扭曲程度所傳送的 hello 減少。 這是 hello 有 tootune hello 少量資料的主要工具。 深入了解[取樣功能](app-insights-sampling.md)。 
* **每日最：**當這項建立 Application Insights 資源從 hello Azure 入口網站設定 too500 GB/天。 hello 預設，從 Visual Studio 中建立 Application Insights 資源時，為小 （只有 32.3 MB/日） 也就是預期唯一 toofaciliate 測試。 在此情況下它可能是該 hello 使用者將會引發 hello 每日最 hello 應用程式部署到實際執行環境之前。 hello 最大限度是 500 GB/天，除非您要求的高流量應用程式更高版本最大值。 小心時，使用每日最 hello，應該為您的意圖**從未 toohit hello 每日最**，因為您再將 hello 天 hello 其餘部分資料遺失，是無法 toomonitor 您的應用程式。 toochange 它使用 hello 每日磁碟區 cap 刀鋒視窗中，連結 hello 資料磁碟區管理刀鋒視窗 （請參閱下文）。 請注意，有些訂用帳戶類型的信用額度無法用於 Application Insights。 若 hello 訂用帳戶有消費限制、 每日 hello cap 刀鋒視窗中會有指示如何 tooremove 它，並啟用 hello 引發 32.3 MB/日超出每日 cap toobe。  
* **節流：**此限制 hello 資料速率 too32 k 事件每秒平均超過 1 分鐘。 


*如果我的應用程式超過 hello 節流速率會怎樣？*

* hello 磁碟區的應用程式傳送的資料來評估每隔一分鐘。 如果它超過平均值 hello 分鐘 hello 每秒的速率，hello 伺服器會拒絕某些要求。 hello SDK 緩衝處理 hello 資料，並再嘗試 tooresend，劇散佈幾分鐘的時間。 如果您的應用程式一致的方式傳送 hello 節流速率以上的資料，有些資料皆會予以捨棄。 （hello ASP.NET、 Java 和 JavaScript Sdk 再試一次以這種方式 tooresend; 其他 Sdk 可能只是節流的卸除資料）。當節流發生時，您會看到警告您這種情況已發生的通知。

如何知道應用程式正在傳送多少資料？

* 開啟 hello**資料磁碟區管理**刀鋒視窗 toosee hello 每日資料磁碟區圖表。 
* 或在 [計量瀏覽器] 中，新增新的圖表，然後選取 [資料點數量] 做為其計量。 切換群組，並依 [資料類型] 分組。

## <a name="tooreduce-your-data-rate"></a>tooreduce 資料速率
以下是一些您可以執行 tooreduce 資料量的事項：

* 使用 [取樣](app-insights-sampling.md)。 扭曲您的指標，而不干擾 hello 能力 toonavigate 中搜尋相關的項目之間，這項技術可減少資料的速率。 在伺服器應用程式，它會自動運作。
* [限制可報告的 Ajax 呼叫的 hello 數目](app-insights-javascript.md#detailed-configuration)中每個頁面檢視或關閉 Ajax 報告的參數。
* 藉由 [編輯 ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)來關閉您不需要的集合模組。例如，您可能會決定效能計數器或相依性資料是不必要的。
* 分割儲存遙測 tooseparate 檢測金鑰。 
* 預先彙總度量。 如果您已將呼叫 tooTrackMetric 放在您的應用程式，您可以使用可接受的 hello 平均計算和度量的批次的標準差 hello 多載來減少流量。 您也可以使用 [預先彙總套件](https://www.myget.org/gallery/applicationinsights-sdk-labs)。

## <a name="managing-hello-maximum-daily-data-volume"></a>管理 hello 最大每日資料磁碟區

您可以使用 hello 每日磁碟區 cap toolimit hello 收集資料，但如果符合 hello 端點時，將會導致從 hello 一天的 hello 其餘部分應用程式傳送的所有 telemetery 遺失。 它是**不建議您**toohave 您應用程式 toohit hello 每日最自您之後會變成無法 tootrack hello 健全狀況和效能的應用程式叫用。 

請改用[取樣](app-insights-sampling.md)tootune hello 資料磁碟區 toohello 層級，，然後使用 hello 每日最只當做 「 最後手段"意外傳送較高的磁碟區的 telemetery 啟動應用程式。 

toochange hello 每日最，hello 之應用程式 Insihgts 資源，[設定] 區段中的按一下**資料磁碟區管理**然後**每日最**。

![調整 每日遙測磁碟區最 hello](./media/app-insights-pricing/daily-cap.png) 

## <a name="sampling"></a>取樣
[取樣](app-insights-sampling.md)是減少時保有 hello 能力 toofind 相關事件在診斷的搜尋時遙測傳送 tooyour 應用程式，hello 速率的方法，而且仍保留正確的事件計數。 

取樣是 tooreduce 費用，並維持在每月配額內的有效方式。 hello 的採樣演算法會保留的遙測，相關項目，因此，比方說，當您使用搜尋時，您可以找到 hello 要求相關的 tooa 特定例外狀況。 hello 演算法也會保留正確的計數，讓您查看 hello 正確的值在總管 中計量要求率、 例外狀況率，以及其他目的計數。

取樣有數種形式。

* [自動調整取樣](app-insights-sampling.md)是 hello hello ASP.NET SDK，會自動調整 toohello 磁碟區的應用程式傳送遙測資料的預設值。 它操作自動在您的 web 應用程式中的 hello SDK 中，因此會降低 hello 遙測 hello 網路流量。 
* *擷取取樣*都是在其中從您的應用程式的遙測輸入 hello Application Insights 服務的 hello 點運作的替代方案。 它並不會影響的遙測資料從您的應用程式傳送的 hello 磁碟區，但它可減少 hello hello 服務所保留的磁碟區。 您可以使用瀏覽器和其他 Sdk 遙測資料所用完 tooreduce hello 配額。

取樣，tooset 擷取 hello 定價刀鋒視窗中設定 hello 控制項：

![從 hello 配額和定價刀鋒視窗中，按一下 hello 範例磚，然後選取取樣分數。](./media/app-insights-pricing/04.png)

> [!WARNING]
> hello 資料取樣 刀鋒視窗只會控制 hello 擷取取樣值。 它並不會反映套用 hello Application Insights SDK 在應用程式中的 hello 取樣率。 如果已經在 hello SDK 取樣 hello 傳入遙測，擷取取樣將不會套用。
> 

取樣率，不論它有已套用的位置，使用 toodiscover hello 實際[分析查詢](app-insights-analytics.md)如下：

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

在每個保留的記錄，`itemCount`指出 hello 原始記錄數目，它代表相等 too1 + hello 先前已捨棄的記錄數目。 


## <a name="automation"></a>自動化

您可以撰寫指令碼 tooset hello 價格計劃，使用 Azure 資源管理。 [了解作法](app-insights-powershell.md#price)。

## <a name="limits-summary"></a>限制摘要
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

## <a name="next-steps"></a>後續步驟

* [取樣](app-insights-sampling.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiproperties]: app-insights-api-custom-events-metrics.md#properties
[start]: app-insights-overview.md
[pricing]: http://azure.microsoft.com/pricing/details/application-insights/


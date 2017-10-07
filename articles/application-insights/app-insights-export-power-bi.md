---
title: "從 Application Insights aaaExport tooPower BI |Microsoft 文件"
description: "Analytics 查詢可以在 Power BI 中顯示。"
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a>從 Application Insights 提供 Power BI
[Power BI](http://www.powerbi.com/) 是一套商務分析工具，可協助您分析資料及分享見解。 每個裝置上都提供豐富的儀表板。 您可以結合許多來源的資料，包含來自 [Azure Application Insights](app-insights-overview.md) 的「分析」查詢。

有三種建議的方法，是要將 Application Insights 資料 tooPower BI 匯出。 您可以單獨或一起使用這些方法。

* [**Power BI 配接器**](#power-pi-adapter) - 從您的應用程式設定完整的遙測儀表板。 hello 組圖表預先定義的但您可以從任何其他來源加入您自己的查詢。
* [**匯出分析查詢**](#export-analytics-queries) -撰寫任何查詢，您想要使用分析，並將它匯出 tooPower BI。 您可以將此查詢和任何其他資料一起放在儀表板上。
* [**連續匯出和資料流分析**](app-insights-export-stream-analytics.md) -這項作業包括多個工作 tooset 組成。 如果您長時間希望 tookeep 資料時，就會很有用。 否則，hello 其他方法建議使用。

## <a name="power-bi-adapter"></a>Power BI 配接器
這個方法會為您建立完整的遙測儀表板。 hello 初始資料集預先定義的但您可以加入更多資料 tooit。

### <a name="get-hello-adapter"></a>取得 hello 配接器
1. 登入太[Power BI](https://app.powerbi.com/)。
2. 依序開啟 [取得資料]、[服務] 和 [Application Insights]
   
    ![取自 Application Insights 資料來源](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. 提供 Application Insights 資源 「 hello 」 詳細的資料。
   
    ![取自 Application Insights 資料來源](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. 等候一分鐘或兩個進行 hello 資料 toobe 匯入。
   
    ![Power BI 配接器](./media/app-insights-export-power-bi/010.png)

您可以編輯 hello 儀表板，與其他來源，以及分析查詢結合 hello Application Insights 圖表。 還有一個視覺效果資源庫，您可以從中取得更多圖表，且每個圖表都有您可以設定的參數。

Hello 初始匯入、 hello 儀表板及報表 hello 之後繼續執行每日 tooupdate。 您可以控制 hello hello 資料集上的重新整理排程。

## <a name="export-analytics-queries"></a>匯出 Analytics 查詢
此路由可讓您 toowrite 任何分析，您查詢，然後再匯出該 tooa Power BI 儀表板。 （您可以新增 toohello hello 配接器所建立的儀表板）。

### <a name="one-time-install-power-bi-desktop"></a>一次︰安裝 Power BI Desktop
tooimport Application Insights 查詢，並使用 hello 桌面版本的 Power BI。 但是，然後您可以將其發行 toohello web 或 tooyour Power BI 雲端工作區。 

安裝 [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/)。

### <a name="export-an-analytics-query"></a>匯出 Analytics 查詢
1. [開啟 Analytics 並撰寫查詢](app-insights-analytics-tour.md)。
2. 測試和精簡 hello 的查詢，直到您滿意 hello 結果。

   **請確定該回合正確在分析之前將它匯出的 hello 查詢。**
3. 在 hello**匯出**功能表上，選擇**Power BI (M)**。 儲存 hello 文字檔案。
   
    ![匯出 Power BI 查詢](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. 在 Power BI Desktop 選取**取得資料，空白查詢**然後在 hello 中查詢下方 編輯器 中，**檢視**選取**進階查詢編輯器**。

    貼上至匯出的 hello M 語言指令碼 hello 進階查詢編輯器。

    ![進階查詢編輯器](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. 您可能必須 tooprovide 認證 tooallow Power BI tooaccess Azure。 使用 「 組織帳戶 」 toosign 使用 Microsoft 帳戶。
   
    ![提供 Azure 認證 tooenable Power BI toorun Application Insights 查詢](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    （如果您需要 tooverify hello 認證時，使用 hello 資料來源設定 功能表命令在 hello 查詢編輯器中。 需要注意您使用 Azure，這可能會不同於您的認證，Power bi toospecify hello 認證）。
2. 選擇您的查詢的視覺效果，然後選取 hello 和欄位的 x 軸、 y 軸，切割維度。
   
    ![選取視覺效果](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. 發行報表 tooyour Power BI 雲端工作區。 您可以從該處將同步版本內嵌至其他網頁。
   
    ![選取視覺效果](./media/app-insights-export-power-bi/publish-power-bi.png)
4. 在時間間隔，以手動方式重新整理 hello 報表，或設定排定的重新整理 hello 選項 頁面上。

## <a name="troubleshooting"></a>疑難排解

### <a name="401-or-403-unauthorized"></a>401 或 403 未經授權 
如果您的重新整理權杖尚未更新，可能會發生這種情況。 您仍然可以存取這些步驟 tooensure 再試一次。 如果您沒有存取 refershing hello 認證無法運作，請開啟支援票證。

1. 登入 hello Azure 入口網站，並確定您可以存取 hello 資源
2. 嘗試 hello 儀表板的 toorefresh hello 認證

### <a name="502-bad-gateway"></a>502 錯誤的閘道
這通常是傳回太多資料的分析查詢所導致。 您應該嘗試使用較小的時間範圍或使用 hello[前](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago)或[startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek)僅限函式[專案](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator)hello 您需要的欄位。

如果降低 hello 來自 hello 分析查詢的資料集不符合您需求您應該考慮使用 hello [API](https://dev.applicationinsights.io/documentation/overview) toopull 較大的資料集。 以下是如何 tooconvert hello M 查詢匯出 toouse hello API 上的指示。

1. 建立 [API 金鑰](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)
2. 更新 hello Power BI 的 M 指令碼來取代分析從匯出的 hello ARM AI api 的 URL （請參閱下面的範例）
   * 將 **https://management.azure.com/subscriptions/...**
   * 取代為 **https://api.applicationinsights.io/beta/apps/...**
3. 最後，更新認證 toobasic，並使用您的 API 金鑰
  

**現有的指令碼**
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
**更新的指令碼**
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a>關於取樣
如果您的應用程式傳送大量資料，hello 調整取樣功能可能會運作，並傳送您遙測的百分比表示。 hello 也是如此，如果您已經手動設定取樣 hello SDK 或擷取。 [深入了解取樣。](app-insights-sampling.md)


## <a name="next-steps"></a>後續步驟
* [Power BI - 了解](http://www.powerbi.com/learning/)
* [Analytics 教學課程](app-insights-analytics-tour.md)


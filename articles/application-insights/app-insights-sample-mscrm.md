---
title: "aaaMicrosoft Dynamics CRM 和 Azure Application Insights |Microsoft 文件"
description: "使用 Application Insights 取得 Microsoft Dynamics CRM Online 遙測。 設定、取得資料、視覺化與匯出的逐步解說。"
services: application-insights
documentationcenter: 
author: mazharmicrosoft
manager: carmonm
ms.assetid: 04c66338-687e-49e5-9975-be935f98f156
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: bwren
ms.openlocfilehash: a39398060d6553fb18a26c101f085b7d87443636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a>逐步解說：使用 Application Insights 啟用Microsoft Dynamics CRM Online 遙測
本文章將示範如何從 tooget 遙測資料[Microsoft Dynamics CRM Online](https://www.dynamics.com/)使用[Azure Application Insights](https://azure.microsoft.com/services/application-insights/)。 我們將逐步 hello 加入 Application Insights 指令碼 tooyour 應用程式、 擷取資料和資料視覺效果的完整程序。

> [!NOTE]
> [瀏覽 hello 範例方案](https://dynamicsandappinsights.codeplex.com/)。
> 
> 

## <a name="add-application-insights-toonew-or-existing-crm-online-instance"></a>加入 Application Insights toonew 或現有的 CRM Online 執行個體
toomonitor 應用程式新增 Application Insights SDK tooyour 應用程式。 hello SDK 傳送遙測 toohello [Application Insights 入口網站](https://portal.azure.com)，其中您可以使用我們的功能強大的分析與診斷工具，或匯出 hello 資料 toostorage。

### <a name="create-an-application-insights-resource-in-azure"></a>在 Azure 中建立 Application Insights 資源
1. 取得 [Microsoft Azure 帳戶](http://azure.com/pricing)。 
2. 登入 hello [Azure 入口網站](https://portal.azure.com)並加入新的 Application Insights 資源。 這是處理與顯示您資料的位置。
   
    ![按一下 [+]、[開發人員服務]、[Application Insights]。](./media/app-insights-sample-mscrm/01.png)
   
    選擇 ASP.NET 做為 hello 應用程式類型。
3. 開啟 hello 開始使用 頁面，並開啟 「 監視及診斷用戶端 」。
   
    ![可在您網頁中進行插入的程式碼片段](./media/app-insights-sample-mscrm/03.png)

**保持開啟 hello 字碼頁**而您不要 hello 另一個瀏覽器視窗中的下一個步驟。 您將很快就需要 hello 程式碼。 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a>在 Microsoft Dynamics CRM 中建立 JavaScript Web 資源
1. 開啟您的 CRM Online 執行個體並使用系統管理員權限登入。
2. 開啟 [Microsoft Dynamics CRM 設定] 自訂項目，自訂 hello 系統
   
    ![Microsoft Dynamics CRM 設定](./media/app-insights-sample-mscrm/04.png)
   
    ![[設定] > [自訂]](./media/app-insights-sample-mscrm/05.png)

    ![自訂 hello 系統選項](./media/app-insights-sample-mscrm/06.png)

1. 建立 JavaScript 資源。
   
    ![新增 Web 資源對話方塊](./media/app-insights-sample-mscrm/07.png)
   
    指定它的名稱，選取**指令碼 (JScript)**和開啟 hello 文字編輯器。
   
    ![開啟的 hello 文字編輯器](./media/app-insights-sample-mscrm/08.png)
2. 從 Application Insights 複製 hello 程式碼。 複製時請確定 tooignore 指令碼標記。 請參閱以下螢幕擷取畫面：
   
    ![設定您的檢測金鑰](./media/app-insights-sample-mscrm/09.png)
   
    hello 程式碼包含 hello 識別您的 Application insights 資源的檢測金鑰。
3. 儲存並發佈。
   
    ![儲存並發佈](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a>檢測表單
1. 在 Microsoft CRM Online 中，開啟 hello 帳戶表單
   
    ![帳戶表單](./media/app-insights-sample-mscrm/11.png)
2. 開啟 hello 表單屬性
   
    ![表單屬性](./media/app-insights-sample-mscrm/12.png)
3. 新增 hello JavaScript 所建立的 web 資源
   
    ![[新增] 功能表](./media/app-insights-sample-mscrm/13.png)
   
    ![新增 hello web 資源](./media/app-insights-sample-mscrm/14.png)
4. 儲存並發佈您的表單自訂內容。

## <a name="metrics-captured"></a>擷取的度量
您現在已設定遙測擷取 hello 表單。 只要使用時，資料將傳送 tooyour Application Insights 資源。

以下是您會看到的 hello 資料的範例。

#### <a name="application-health"></a>應用程式健全狀況
![範例頁面載入時間](./media/app-insights-sample-mscrm/15.png)

![範例頁面檢視圖表](./media/app-insights-sample-mscrm/16.png)

瀏覽器例外狀況：

![瀏覽器例外狀況圖表](./media/app-insights-sample-mscrm/17.png)

按一下 hello 圖表 tooget 更多詳細資料：

![例外狀況清單](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a>使用量
![使用者數、工作階段數及頁面檢視數](./media/app-insights-sample-mscrm/19.png)

![工作階段圖表](./media/app-insights-sample-mscrm/20.png)

![瀏覽器版本](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a>瀏覽器
![頁面載入時間明細](./media/app-insights-sample-mscrm/22.png)

![依瀏覽器版本區分的工作階段計數](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a>地理位置
![依國家/地區區分的工作階段計數](./media/app-insights-sample-mscrm/24.png)

![依國家/地區區分的工作階段數和使用者數](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a>深入了解頁面檢視要求
![頁面檢視摘要](./media/app-insights-sample-mscrm/26.png)

![依頁面檢視事件進行搜尋](./media/app-insights-sample-mscrm/27.png)

![相似頁面檢視數](./media/app-insights-sample-mscrm/28.png)

![頁面檢視屬性](./media/app-insights-sample-mscrm/29.png)

![每個工作階段的頁面數](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a>範例程式碼
[瀏覽 hello 範例程式碼](https://dynamicsandappinsights.codeplex.com/)。

## <a name="power-bi"></a>Power BI
您可以執行甚至更深入分析，如果您[匯出 hello 資料 tooMicrosoft Power BI](app-insights-export-power-bi.md)。

## <a name="sample-microsoft-dynamics-crm-solution"></a>Microsoft Dynamics CRM 解決方案範例
[以下是在 Microsoft Dynamics CRM 中實作的 hello 範例方案](https://dynamicsandappinsights.codeplex.com/)。

## <a name="learn-more"></a>詳細資訊
* [什麼是 Application Insights？](app-insights-overview.md)
* [適用於網頁的 Application Insights](app-insights-javascript.md)
* [更多範例和逐步解說](app-insights-code-samples.md)

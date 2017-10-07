---
title: "aaaAutomate 與 Microsoft Flow 處理 Azure Application Insights"
description: "了解如何使用 Microsoft Flow tooquickly 使用 hello Application Insights 連接器來自動化重複程序。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: bwren
ms.openlocfilehash: b34488a6b8b8b0a6add960a67f1426cbbbc13552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automate-azure-application-insights-processes-with-hello-connector-for-microsoft-flow"></a>Microsoft flow 自動化 Azure Application Insights 處理程序與 hello 連接器

您發現自己重複 hello 相同的查詢上執行您的服務運作正常您遙測資料 toocheck 嗎？ 您尋找 tooautomate 這些查詢來尋找趨勢和異常及再建置您自己的工作流程周圍嗎？Microsoft flow hello Azure Application Insights 連接器 （預覽） 會針對這些用途是 hello 正確的工具。

有了此整合，您就能立即自動執行許多流程，而不需撰寫任何一行程式碼。 使用 Application Insights 動作建立流程之後，hello 流程會自動執行應用程式 Insights 分析查詢。 

您也可以新增額外的動作。 Microsoft Flow 提供數百個動作。 例如，您可以使用 Microsoft Flow tooautomatically 傳送電子郵件通知，或在 Visual Studio Team Services 中建立 bug。 您也可以使用其中一個 hello 許多[範本](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights)可用的 Microsoft flow hello 連接器。 這些範本會加快建立資料流程的 hello 程序。 

<!--hello Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a>建立 Application Insights 的流程

在本教學課程中，您將學習如何 toocreate 使用 hello 分析自動叢集演算法 toogroup 資料流程中的屬性 hello web 應用程式的資料。 hello 流量會透過電子郵件、 只在一個範例，告訴您可以使用 Microsoft Flow 及應用程式 Insights 分析一起自動傳送 hello 結果。 

### <a name="step-1-create-a-flow"></a>步驟 1：建立流程
1. 登入太[Microsoft Flow](http://flow.microsoft.com)，然後選取**我流動**。
2. 按一下 [從空白建立流程]。

### <a name="step-2-create-a-trigger-for-your-flow"></a>步驟 2：建立流程的觸發程序
1. 依序選取 [排程] 和 [排程 - 重複]。
2. 在 hello**頻率**方塊中，選取**天**，在 hello**間隔**方塊中，輸入**1**。

    ![Microsoft Flow 觸發程序對話方塊](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a>步驟 3：新增 Application Insights 動作
1. 按一下 新增步驟，然後按一下新增動作。
2. 搜尋 **Azure Application Insights**。
3. 按一下 [Azure Application Insights – 視覺化 Analytics 查詢預覽]。

    ![執行 Analytics 查詢視窗](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>步驟 4： 連接 tooan Application Insights 資源

toocomplete 此步驟中，您需要您為資源的應用程式識別碼和 API 金鑰。 您可以從取回 hello Azure 入口網站中 hello 下列圖表所示：

![在 hello Azure 入口網站應用程式識別碼](./media/app-insights-automate-with-flow/appid.png) 

- 提供您的連線，以及 hello 應用程式識別碼和 API 金鑰的名稱。

    ![Microsoft Flow 連線視窗](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>步驟 5： 指定 hello 分析查詢和圖表類型
這個範例查詢會選取 hello 最後一天中的 hello 失敗要求，並將它們與 hello 作業期間發生的例外狀況相互關聯。 分析相互關聯根據 hello operation_Id 識別項。 hello 查詢然後區段 hello 結果使用 hello autocluster 演算法。 

當您建立您自己的查詢時，確認它們會正常運作在分析中加入 tooyour 流程之前。

- 新增下列分析查詢的 hello，然後選取 hello HTML 表格的圖表類型。 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```
    
    ![Analytics 查詢設定畫面](./media/app-insights-automate-with-flow/flow4.png)

### <a name="step-6-configure-hello-flow-toosend-email"></a>步驟 6： 設定 hello 流程 toosend 電子郵件

1. 按一下 新增步驟，然後按一下新增動作。
2. 搜尋 **Office 365 Outlook**。
3. 按一下 [Office 365 Outlook – 傳送電子郵件]。

    ![Office 365 Outlook 選取視窗](./media/app-insights-automate-with-flow/flow2b.png)

4. 在 hello**傳送電子郵件**視窗中，執行下列 hello:

   a. 輸入 hello hello 收件者電子郵件地址。

   b. 輸入 hello 電子郵件的主旨。

   c. 按一下任何位置中的 hello**主體**方塊，然後 hello 動態內容功能表開啟在 hello 右、 上選取**主體**。

   d. 按一下 [顯示進階選項]。

    ![Office 365 Outlook 設定](./media/app-insights-automate-with-flow/flow5.png)

5. Hello 動態內容功能表上，hello 遵循：

    a. 選取 [附件名稱]。

    b.這是另一個 C# 主控台應用程式。 選取 [附件內容]。
    
    c. 在 hello**是 HTML**方塊中，選取**是**。

    ![Office 365 電子郵件設定畫面](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a>步驟 7：儲存並測試流程
- 在 hello**流程名稱**方塊中，加入您的流程的名稱，然後按一下**建立流程**。

    ![流程建立視窗](./media/app-insights-automate-with-flow/flow8.png)

您可以等候 hello 觸發程序 toorun 此動作，或者您可以立即藉由執行 hello 流程[依需求執行 hello 觸發程序](https://flow.microsoft.com/blog/run-now-and-six-more-services/)。

Hello 流程執行時，hello hello 的電子郵件清單中所指定的收件者會收到電子郵件訊息，看起來像下列 hello:

![範例電子郵件](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a>後續步驟

- 深入了解建立 [Analytics 查詢](app-insights-analytics-using.md)。
- 深入了解 [Microsoft Flow](https://ms.flow.microsoft.com)。



<!--Link references-->






---
title: "aaaAutomate 使用 Logic Apps 處理 Azure Application Insights。"
description: "了解如何您可以快速自動化重複程序加入 hello Application Insights 連接器 tooyour 邏輯應用程式。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a>使用 Logic Apps 自動執行 Application Insights 程序

您發現自己重複 hello 相同的查詢上執行您的遙測資料 toocheck 是否正常運作您的服務？ 您尋找 tooautomate 這些查詢來尋找趨勢和異常及再建置您自己的工作流程周圍嗎？Logic apps hello Azure Application Insights 連接器 （預覽） 是針對此用途的 hello 正確的工具。

有了此整合，您就能自動執行許多流程，而不需撰寫任何一行程式碼。 您可以建立邏輯應用程式以 hello Application Insights 連接器 tooquickly 任何 Application Insights 程序自動化。 

您也可以新增額外的動作。 Azure App Service hello Logic Apps 功能可讓您提供數百個動作。 例如，使用邏輯應用程式，您可以自動傳送電子郵件通知，或在 Visual Studio Team Services 中建立 Bug。 您也可以使用其中一個 hello 許多可用[範本](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates)toohelp 加速 hello 處理程序的建立應用程式邏輯。 

## <a name="create-a-logic-app-for-application-insights"></a>建立 Application Insights 的邏輯應用程式

在此教學課程中，您學會 toocreate 邏輯應用程式使用 hello 分析 autocluster 演算法 toogroup 屬性是如何在 web 應用程式的 hello 資料。 hello 流量會透過電子郵件、 一個範例，告訴您可以使用應用程式 Insights 分析和邏輯應用程式一起自動傳送 hello 結果。 

### <a name="step-1-create-a-logic-app"></a>步驟 1：建立邏輯應用程式
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello**新增**窗格中，選取**Web + 行動**，然後選取**邏輯應用程式**。

    ![新增邏輯應用程式視窗](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a>步驟 2：建立邏輯應用程式的觸發程序
1. 在 hello**邏輯應用程式的設計工具**視窗底下**一般的觸發程序的開頭**，選取**循環**。

    ![邏輯應用程式設計工具視窗](./media/automate-with-logic-apps/logicapp2.png)

2. 在 hello**頻率**方塊中，選取**天**，然後在 hello**間隔**方塊中，輸入**1**。

    ![邏輯應用程式設計工具 [參考] 視窗](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a>步驟 3：新增 Application Insights 動作
1. 按一下 新增步驟，然後按一下新增動作。

2. 在 [hello**選擇動作**搜尋] 方塊中，輸入**Azure Application Insights**。

3. 在 [動作] 之下，按一下 [Azure Application Insights – 視覺化 Analytics 查詢預覽]。

    ![邏輯應用程式設計工具的「選擇動作」視窗](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>步驟 4： 連接 tooan Application Insights 資源

toocomplete 此步驟中，您需要您為資源的應用程式識別碼和 API 金鑰。 您可以從取回 hello Azure 入口網站中 hello 下列圖表所示：

![在 hello Azure 入口網站應用程式識別碼](./media/automate-with-logic-apps/appid.png) 

提供您的連接、 hello 應用程式識別碼和 hello API 金鑰的名稱。

![邏輯應用程式設計工具連線視窗](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>步驟 5： 指定 hello 分析查詢和圖表類型
在下列範例的 hello，hello 查詢會選取 hello 最後一天中的 hello 失敗要求，並將它們與 hello 作業期間發生的例外狀況相互關聯。 分析相互關聯 hello 失敗的要求，根據 hello operation_Id 識別項。 hello 查詢然後區段 hello 結果使用 hello autocluster 演算法。 

當您建立您自己的查詢時，確認它們會正常運作在分析中加入 tooyour 流程之前。

1. 在 hello**查詢**方塊中，加入下列分析查詢的 hello: 

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

2. 在 hello**圖表類型**方塊中，選取**Html 表格**。

    ![Analytics 查詢設定畫面](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a>步驟 6： 設定 hello 邏輯應用程式 toosend 電子郵件

1. 按一下 [新增步驟]，然後選取 [新增動作]。

2. 在 [hello] 搜尋方塊中，輸入**Office 365 Outlook**。

3. 按一下 [Office 365 Outlook – 傳送電子郵件]。

    ![Office 365 Outlook 選項](./media/automate-with-logic-apps/flow2b.png)

4. 在 hello**傳送電子郵件**視窗中，執行下列 hello:

   a. 輸入 hello hello 收件者電子郵件地址。

   b. 輸入 hello 電子郵件的主旨。

   c. 按一下任何位置中的 hello**主體**方塊，然後 hello 動態內容功能表開啟在 hello 右、 上選取**主體**。

   d. 按一下 [顯示進階選項]。

      ![Office 365 Outlook 設定](./media/automate-with-logic-apps/flow5.png)

5. Hello 動態內容功能表上，hello 遵循：

    a. 選取 [附件名稱]。

    b.這是另一個 C# 主控台應用程式。 選取 [附件內容]。
    
    c. 在 hello**是 HTML**方塊中，選取**是**。

      ![Office 365 電子郵件設定畫面](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a>步驟 7：儲存並測試邏輯應用程式
* 按一下**儲存**toosave 您的變更。

您可以等候 hello 觸發程序 toorun hello 邏輯應用程式，或您可以立即執行 hello 邏輯應用程式，方法是選取**執行**。

![邏輯應用程式建立畫面](./media/automate-with-logic-apps/step7.png)

邏輯應用程式執行時，您指定 hello 電子郵件清單中的 hello 收件者會收到電子郵件，看起來像 hello 下列：

![邏輯應用程式電子郵件訊息](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a>後續步驟

- 深入了解建立 [Analytics 查詢](app-insights-analytics-using.md)。
- 深入了解 [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps)。



<!--Link references-->






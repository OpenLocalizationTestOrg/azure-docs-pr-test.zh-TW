---
title: "aaaCreate 您雲端應用程式和雲端服務-Azure 邏輯應用程式之間的第一個工作流程 |Microsoft 文件"
description: "在 Azure Logic Apps 中建立及執行工作流程，以自動執行系統整合和企業應用程式整合 (EAI) 案例的商務程序"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: "工作流程, 雲端應用程式, 雲端服務, 商務程序, 系統整合, 企業應用程式整合, EAI"
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a>建立您的第一個邏輯應用程式的雲端應用程式和雲端服務之間的工作流程 tooautomate 程序

不需撰寫任何程式碼，您可以在建立並執行工作流程時利用 [Azure Logic Apps](logic-apps-what-are-logic-apps.md)，更輕鬆快速地自動執行商務程序。 第一個範例顯示如何 toocreate 基本邏輯應用程式工作流程，以檢查 RSS 摘要，可在網站上的新內容。 當新項目出現在 hello 網站摘要中時，hello 邏輯應用程式會傳送電子郵件從 Outlook 或 Gmail 帳戶。

toocreate，以及執行邏輯應用程式，您會需要這些項目：

* Azure 訂用帳戶。 如果您沒有訂用帳戶，您可以[開始使用免費 Azure 帳戶](https://azure.microsoft.com/free/)。 否則，您可以[註冊隨用隨付訂用帳戶](https://azure.microsoft.com/pricing/purchase-options/)。

  您的 Azure 訂用帳戶用於邏輯應用程式使用量計費。 了解 Azure Logic Apps 的[使用量計量](../logic-apps/logic-apps-pricing.md)和[計價](https://azure.microsoft.com/pricing/details/logic-apps)方式。

此外，這個範例需要下列項目︰

* Outlook.com、Office 365 Outlook 或 Gmail 帳戶

    > [!TIP]
    > 如果您有個人 [Microsoft 帳戶](https://account.microsoft.com/account)，您便有 Outlook.com 帳戶。 否則，如果您有 Azure 工作或學校帳戶，您便有 **Office 365 Outlook** 帳戶。

* 連結 tooa 網站的 RSS 摘要。 這個範例會使用 hello [RSS 摘要中的最上層的劇本從 hello CNN.com 網站](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`

## <a name="add-a-trigger-that-starts-your-workflow"></a>新增可啟動工作流程的觸發程序

A [*觸發程序*](./logic-apps-what-are-logic-apps.md#logic-app-concepts)啟動邏輯的應用程式工作流程的事件，而邏輯應用程式所需的 hello 第一個項目。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com "Azure 入口網站")。

2. 從 hello 左窗格中，選擇 **新增** > **企業整合** > **邏輯應用程式**如下所示：

     ![Azure 入口網站, 新增, 企業整合, 邏輯應用程式](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > 您也可以選擇**新增**，然後在 [hello] 搜尋方塊中，輸入`logic app`，然後按 Enter。 然後選擇 [邏輯應用程式] > [建立]。

3. 為您的邏輯應用程式命名並選取您的 Azure 訂用帳戶。 現在建立或選取 Azure 資源群組，以協助您組織及管理相關的 Azure 資源。 最後，選取裝載應用程式邏輯的 hello 資料中心位置。 當您準備好時，選擇**Pin toodashboard**然後**建立**。

     ![邏輯應用程式詳細資料](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > 當您選取**Pin toodashboard**，邏輯應用程式部署之後，會出現在 hello Azure 儀表板，並會自動開啟。 邏輯應用程式不會出現在 hello 儀表板，在 hello**所有資源**磚中，選擇**更看到**，並選取邏輯應用程式。 或在 hello 左窗格中，選擇 **更多服務**。 在 [企業整合] 底下，選擇 [Logic Apps]，然後選取您的邏輯應用程式。

4. 當您第一次開啟 hello 的應用程式邏輯時，hello 邏輯應用程式的設計工具會顯示您可以使用啟動 tooget 範本。 暫時選擇 [空白邏輯應用程式]，以便從頭建置邏輯應用程式。

    hello 邏輯應用程式的設計工具隨即開啟並顯示可用的服務和*觸發程序*，您可以使用邏輯應用程式中。

5. 在 hello 搜尋方塊中，輸入`RSS`，然後選取 此觸發程序： **RSS-發行摘要項目時** 

    ![RSS 觸發程序](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. 輸入您想 tootrack hello 網站的 RSS 摘要 hello 連結。 

     您也可以變更 [頻率] 和 [間隔]。 
     這些設定會決定邏輯應用程式檢查新項目並傳回該時間範圍內找到之所有項目的頻率。

     針對此範例中，讓我們來檢查每一天的最上層的劇本張貼 toohello 可以使用網站。

     ![使用 RSS 摘要、頻率和間隔設定觸發程序](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. 儲存您目前的工作。 (在 hello 設計工具命令列上選擇 **儲存**。)

   ![儲存您的邏輯應用程式](media/logic-apps-create-a-logic-app/save-logic-app.png)

   當您儲存、 邏輯應用程式上線，但目前，邏輯應用程式只會檢查新的項目中的 hello 指定 RSS 摘要。 
   此範例中更有用的我們加入觸發程序後，執行邏輯應用程式的動作會引發 toomake。

## <a name="add-an-action-that-responds-tooyour-trigger"></a>加入回應 tooyour 觸發程序的動作

[動作](./logic-apps-what-are-logic-apps.md#logic-app-concepts)是邏輯應用程式工作流程所執行的工作。 新增觸發程序 tooyour 邏輯應用程式之後，您可以加入動作 tooperform 操作該觸發程序所產生的資料。 範例中，我們現在會加入新項目出現時傳送電子郵件中 hello 網站的 RSS 摘要的動作。

1. 在 hello 設計工具，在您的觸發程序中，選擇**新步驟** > **將動作加入**如下所示：

   ![新增動作](media/logic-apps-create-a-logic-app/add-new-action.png)

   hello 設計工具會顯示[可用的連接器](../connectors/apis-list.md)，因此觸發程序引發時，您可以選取動作 tooperform。

2. 根據您的電子郵件帳戶，請在 Outlook 或 Gmail 遵循 hello 步驟。

   * toosend 電子郵件從 Outlook 帳戶，在 hello 搜尋方塊中輸入`outlook`。 在 [服務] 之下，針對個人 Microsoft 帳戶選擇 [Outlook.com]，或針對 Azure 工作或學校帳戶選擇 [Office 365 Outlook]。 
   在 [動作] 之下，選取 [傳送電子郵件]。

       ![選取 Outlook「傳送電子郵件」動作](media/logic-apps-create-a-logic-app/actions.png)

   * toosend 電子郵件是來自您的 Gmail 帳戶，請在 [hello] 搜尋方塊中，輸入`gmail`。 
   在 [動作] 之下，選取 [傳送電子郵件]。

       ![選擇「Gmail - 傳送電子郵件」](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. 當系統提示您輸入認證時，hello 使用者名稱和密碼登入您的電子郵件帳戶。 

4. 提供此動作，像是 hello 目的地電子郵件地址，hello 詳細資料，並選擇 hello 資料 tooinclude hello 參數 hello 電子郵件，例如：

   ![電子郵件中的選取資料 tooinclude](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    因此如果您選擇 Outlook，邏輯應用程式可能如此範例所示︰

    ![已完成的邏輯應用程式](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  儲存您的變更。 (在 hello 設計工具命令列上選擇 **儲存**。)

6. 您現在可以手動執行邏輯應用程式進行測試。 在 hello 設計工具命令列上選擇 **執行**。 否則，您可以讓您檢查 hello 指定 RSS 摘要 hello 排程設定為基礎的邏輯應用程式。

   如果應用程式邏輯尋找新的項目，hello 邏輯應用程式會傳送電子郵件，其中包含您選取的資料。 
   如果找不到任何新的項目，應用程式邏輯會略過傳送電子郵件的 hello 動作。

7. toomonitor 和核取的執行邏輯應用程式，並觸發歷程記錄，在邏輯應用程式功能表上的選擇 **概觀**。

   ![監視及檢視邏輯應用程式執行和觸發歷程記錄](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > 如果找不到預期在 hello 命令列的 hello 資料再試一次選擇**重新整理**。

   toolearn 深入了解您的邏輯應用程式狀態或執行，並觸發歷程記錄或 toodiagnose 邏輯應用程式，請參閱[疑難排解應用程式邏輯](logic-apps-diagnosing-failures.md)。

      > [!NOTE]
      > 邏輯應用程式會繼續執行，直到您關閉應用程式為止。 現在，在邏輯應用程式功能表上的應用程式關閉 tooturn 選擇**概觀**。 在 hello 命令列上選擇 **停用**。

恭喜，您剛設定並執行第一個基本邏輯應用程式。 您也了解如何輕鬆地建立可自動執行程序的工作流程，並整合雲端應用程式和雲端服務 - 全都不需要程式碼。

## <a name="manage-your-logic-app"></a>管理邏輯應用程式

toomanage 應用程式，您可以執行工作，例如檢查 hello 狀態、 編輯、 檢視歷程記錄、 關閉或刪除邏輯應用程式。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com "Azure 入口網站")。

2. 在 hello 左窗格中，選擇 **更多服務**。 在 [企業整合] 底下選擇 [Logic Apps]。 選取您的邏輯應用程式。 

   在 hello 邏輯應用程式功能表中，您可以找到這些邏輯應用程式管理工作：

   |Task|步驟| 
   |:---|:---| 
   | 檢視應用程式的狀態、執行歷程記錄和一般資訊| 選擇 [概觀]。| 
   | 編輯應用程式 | 選擇 [邏輯應用程式設計工具]。 | 
   | 檢視應用程式的工作流程 JSON 定義 | 選擇 [邏輯應用程式程式碼檢視]。 | 
   | 檢視在邏輯應用程式上執行的作業 | 選擇 [活動記錄]。 | 
   | 檢視邏輯應用程式過去的版本 | 選擇 [版本]。 | 
   | 暫時關閉應用程式 | 選擇**概觀**，然後在 hello 命令列上選擇 **停用**。 | 
   | 刪除應用程式 | 選擇**概觀**，然後在 hello 命令列上選擇 **刪除**。 輸入邏輯應用程式的名稱，然後選擇 [刪除]。 | 

## <a name="get-help"></a>取得說明

tooask 問題回答的問題，以及了解哪些其他 Azure 邏輯應用程式使用者的行為，請瀏覽 hello [Azure 邏輯應用程式論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)。

toohelp 改善 Azure 邏輯應用程式和連接器、 票選或送出意見在 hello [Azure 邏輯應用程式使用者意見反應網站](http://aka.ms/logicapps-wish)。

## <a name="next-steps"></a>後續步驟

*  [新增條件並執行工作流程](../logic-apps/logic-apps-use-logic-app-features.md)
*    [邏輯應用程式範本](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [從 Azure Resource Manager 範本建立邏輯應用程式](../logic-apps/logic-apps-arm-provision.md)

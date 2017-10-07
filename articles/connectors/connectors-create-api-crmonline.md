---
title: "從 Azure 邏輯應用程式的 aaaConnect tooDynamics 365 （線上） |Microsoft 文件"
description: "建立邏輯管理 Dynamics 365 （線上） 的實體，透過 hello hello Dynamics 365 連接器所提供的 API 的應用程式工作流程"
services: logic-apps
cloud: Azure Stack
author: Mattp123
manager: anneta
documentationcenter: 
tags: connectors
ms.assetid: 0dc2abef-7d2c-4a2d-87ca-fad21367d135
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: matp; LADocs
ms.openlocfilehash: 183d7a6b8e5d2c0eecc70da0da3806e06c382df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toodynamics-365-from-logic-app-workflows"></a>邏輯應用程式工作流程從連接 tooDynamics 365

透過邏輯應用程式，您可以連接 tooDynamics 365 （線上），並建立實用的商務流程，建立記錄、 更新項目，或傳回的記錄清單。 與 hello Dynamics 365 連接器，您可以：

* 建置您的商務流程根據 hello 資料取自 Dynamics 365 （線上）。
* 使用取得回應，然後進行 hello 輸出適用於其他動作的動作。 舉例來說，當 Dynamics 365 (線上) 中有項目更新時，您可以利用 Office 365 來傳送電子郵件。

本主題說明您如何 toocreate 邏輯應用程式的工作中建立 Dynamics 365 Dynamics 365 在每次建立新的負責人時。

## <a name="prerequisites"></a>必要條件
* 一個 Azure 帳戶。
* Dynamics 365 (線上) 帳戶。

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a>每次在 Dynamics 365 中建立了新的潛在客戶時便建立工作

1.  [登入 tooAzure](https://portal.azure.com)。

2.  在 hello Azure 搜尋方塊中，輸入`Logic apps`，然後按 ENTER。

      ![尋找Logic Apps](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  在 [邏輯應用程式] 下，按一下 [新增]。

      ![LogicApp 新增](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  toocreate hello 邏輯應用程式，完成 hello**名稱**，**訂用帳戶**，**資源群組**，和**位置**欄位，然後再按一下  **建立**。

5.  選取 hello 新邏輯應用程式。 當您收到 hello**部署成功**通知，請按一下**重新整理**。

6.  在 [開發工具] 下，按一下 [邏輯應用程式設計工具]。 在 hello 範本清單中，按一下 **空白邏輯應用程式**。

7.  在 [hello] 搜尋方塊中，輸入`Dynamics 365`。 從 hello Dynamics 365 觸發程序清單中，選取**Dynamics 365 – 時建立的記錄**。

8.  如果您是在 tooDynamics 365 提示的 toosign，請立刻執行。

9.  在 hello 觸發程序的詳細資訊，請輸入下列資訊的 hello:

  * **組織名稱**。 選取您想要 hello 邏輯應用程式 toolisten hello Dynamics 365 執行個體。

  * **實體名稱**。 選取您想要 toolisten hello 實體。 此事件會做為觸發程序 toostart hello 邏輯應用程式。 
  在本逐步解說中，我們選取 [潛在客戶]。

  * **頻率想 toocheck 項目？** 這些值來設定頻率 hello 邏輯應用程式會檢查更新相關的 toohello 觸發程序。 更新每隔三分鐘 toocheck hello 預設設定。

    * **頻率**。 選取秒、分鐘、小時或天。

    * **間隔**。 輸入 hello 數秒、 分鐘、 小時或您想 toopass hello 下次檢查之前的天數。

      ![邏輯應用程式觸發程序的詳細資料](./media/connectors-create-api-crmonline/trigger-details.png)

10. 按一下 新增步驟，然後按一下新增動作。

11. 在 [hello] 搜尋方塊中，輸入`Dynamics 365`。 從 hello 動作清單中，選取**Dynamics 365 – 建立新的記錄**。

12. 輸入下列資訊的 hello:

    * **組織名稱**。 選取您想要 hello 流程 toocreate hello 記錄 hello Dynamics 365 執行個體。 
    請注意，這個執行個體並未 toobe hello 相同執行個體從觸發 hello 事件的位置。

    * **實體名稱**。 選取您想 toocreate 記錄 hello 事件觸發時 hello 實體。 
    在本逐步解說中，我們選取 [工作]。

13. 按一下 hello**主旨**出現方塊。 從 hello 動態內容清單隨即出現，您可以選取這些欄位：

    * **姓氏**。 選取此欄位插入 hello 姓氏的 hello hello hello 工作的主旨欄位時，會建立 hello 工作記錄。
    * **主題**。 選取 hello 負責人 hello hello 工作的主旨欄位至這個欄位插入 hello 主題欄位，當 hello 工作會建立記錄。 
    按一下**主題**tooadd 該 toohello**主旨**方塊。

      ![邏輯應用程式建立新記錄詳細資料](./media/connectors-create-api-crmonline/create-record-details.png)

14. Hello 邏輯應用程式的設計工具工具列上，按一下**儲存**。

    ![邏輯應用程式設計工具工具列儲存](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. toostart hello 邏輯應用程式中，按一下**執行**。

    ![邏輯應用程式設計工具工具列儲存](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. 現在，在 Dynamics 365 中建立銷售潛在客戶記錄，然後看看流程的運作！

## <a name="set-advanced-options-for-a-logic-app-step"></a>為邏輯應用程式步驟設定進階選項

如何 toofilter 資料在邏輯應用程式步驟中，按一下的 toospecify **Show advanced 選項**在該步驟，然後加入篩選或順序查詢。

例如，您可以使用篩選器查詢 tooget 唯一作用中帳戶，並依 hello 帳戶名稱。 tooperform 這項工作，輸入 hello OData 篩選器查詢`statuscode eq 1`，然後選取**帳戶名稱**從 hello 動態內容的清單。 詳細資訊︰[MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) 和 [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2)。

![邏輯應用程式進階選項](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a>使用進階選項時的最佳作法

當您將值 tooa 欄位時，您必須符合 hello 欄位類型，當您輸入的值，或從 hello 動態內容清單中選取值。

欄位類型  |如何 toouse  |其中 toofind  |名稱  |資料類型  
---------|---------|---------|---------|---------
文字欄位|文字欄位需要單行文字或屬於文字類型欄位的動態內容。 範例包括 hello 類別和子類別目錄欄位。|設定 > 自訂 > 自訂 hello 系統 > 實體 > 工作 > 欄位 |category |單行文字        
整數欄位 | 某些欄位需要整數或屬於整數類型欄位的動態內容。 範例包括 [完成百分比] 和 [持續時間]。 |設定 > 自訂 > 自訂 hello 系統 > 實體 > 工作 > 欄位 |percentcomplete |整數         
日期欄位 | 某些欄位需要以 mm/dd/yyyy 格式輸入的日期或屬於日期類型欄位的動態內容。 範例包括 [建立日期]、[開始日期]、[實際開始時間]、[上次保留時間]、[實際結束時間] 和 [到期日]。 | 設定 > 自訂 > 自訂 hello 系統 > 實體 > 工作 > 欄位 |createdon |日期和時間
同時需要記錄識別碼和查閱類型的欄位 |參考另一個實體記錄某些欄位需要 hello 記錄識別碼和 hello 查閱類型。 |設定 > 自訂 > 自訂 hello 系統 > 實體 > 帳戶 > 欄位  | accountid  | 主索引鍵

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a>同時需要記錄識別碼和查閱類型的其他欄位範例
展開 hello 前一個資料表上，以下是不處理 hello 動態內容清單中選取值的欄位的其他範例。 相反地，這些欄位需要這兩個的記錄識別碼和查閱型別中 PowerApps hello 欄位中輸入。  
* 擁有者和擁有者類型。 hello 擁有者 欄位必須是有效的使用者或小組記錄識別碼。 hello 擁有者型別必須是**systemusers**或**小組**。
* 客戶和客戶類型。 hello 客戶欄位必須是有效的帳戶，或連絡記錄識別碼。 hello 擁有者型別必須是**帳戶**或**連絡人**。
* 關於和關於類型。 hello 相關欄位必須是有效的記錄識別碼，例如帳戶或連絡記錄識別碼。 hello 有關類型必須是 hello 查閱類型 hello 記錄，例如**帳戶**或**連絡人**。

hello 下列工作建立動作範例會將對應將它加入有關 hello 工作的欄位 toohello toohello 記錄識別碼的帳戶記錄。

![流量記錄識別碼和類型帳戶](./media/connectors-create-api-crmonline/recordid-type-account.png)

此範例也會將指派的 hello 工作 tooa 特定使用者根據 hello 使用者的記錄識別碼。

![流量記錄識別碼和類型帳戶](./media/connectors-create-api-crmonline/recordid-type-user.png)

toofind 一筆記錄的識別碼，請參閱下列章節的 hello:*尋找 hello 記錄識別碼*

## <a name="find-hello-record-id"></a>尋找 hello 記錄識別碼

1. 開啟記錄，例如帳戶記錄。

2. Hello 動作在工具列上，按一下 **快顯**![彈出記錄](./media/connectors-create-api-crmonline/popout-record.png)。
或者，hello 動作 toocopy hello 完整的 URL 到預設電子郵件程式中，按一下工具列**電子郵件 連結**。

   hello %7b 和 %7 d hello URL 的字元編碼之間不會顯示 hello 記錄識別碼。

   ![流量記錄識別碼和類型帳戶](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a>疑難排解
tootroubleshoot 失敗的步驟，在邏輯應用程式中檢視的 hello 事件 hello 狀態詳細資料。

1. 在 Logic Apps 下，選取您的邏輯應用程式，然後按一下概觀。 

   hello 摘要區域中顯示，並提供 hello 邏輯應用程式中的 hello 執行狀態。 

   ![邏輯應用程式執行狀態](./media/connectors-create-api-crmonline/tshoot1.png)

2. tooview 執行任何失敗的詳細資訊按一下 hello 失敗事件。 tooexpand 失敗的步驟中，按一下該步驟。

   ![展開失敗的步驟](./media/connectors-create-api-crmonline/tshoot2.png)

   hello 步驟詳細資料會出現，並可協助您疑難排解 hello hello 失敗原因。

   ![失敗步驟的詳細資料](./media/connectors-create-api-crmonline/tshoot3.png)

如需針對邏輯應用程式進行疑難排解的詳細資訊，請參閱[診斷邏輯應用程式失敗](../logic-apps/logic-apps-diagnosing-failures.md)。

## <a name="connector-specific-details"></a>連接器特定的詳細資料

檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/crm/)。 

## <a name="next-steps"></a>後續步驟
瀏覽 hello 在邏輯應用程式中其他可用的連接器我們[Api 清單](apis-list.md)。

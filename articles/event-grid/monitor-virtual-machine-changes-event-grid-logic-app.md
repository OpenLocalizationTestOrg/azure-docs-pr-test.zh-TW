---
title: "aaaMonitor 變更的虛擬機器的 Azure 事件方格 & Logic Apps |Microsoft 文件"
description: "使用 Azure Event Grid 和 Logic Apps 來檢查虛擬機器 (VM) 的組態變更"
keywords: "logic apps, event grids, 虛擬機器, VM"
services: logic-apps
author: ecfan
manager: anneta
ms.assetid: 
ms.workload: logic-apps
ms.service: logic-apps
ms.topic: article
ms.date: 08/16/2017
ms.author: LADocs; estfan
ms.openlocfilehash: f0633e598be6e7880a310e6f8e64f6738cc692b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-changes-with-azure-event-grid-and-logic-apps"></a>使用 Azure Event Grid 和 Logic Apps 監視虛擬機器變更

當 Azure 資源或第三方資源發生特定事件時，您可以啟動自動化[邏輯應用程式工作流程](../logic-apps/logic-apps-what-are-logic-apps.md)。 這些資源可以發行這些事件 tooan [Azure 事件方格](../event-grid/overview.md)。 接著，hello 事件方格推播通知已佇列 webhook，這些事件 toosubscribers 或[事件中心](../event-hubs/event-hubs-what-is-event-hubs.md)為端點。 為訂閱者，邏輯應用程式可以等待 hello 事件方格中的這些事件，您撰寫任何程式碼不執行自動化的流程 tooperform 工作-之前。

例如，以下是 「 發行者 」 可以傳送 hello Azure 事件方格服務透過 toosubscribers 某些事件：

* 建立、讀取、更新或刪除資源。 例如，您可以監視可能會產生 Azure 訂用帳戶費用並會影響帳單的變更。 
* 從 Azure 訂用帳戶中新增或移除人員。
* 您的應用程式會執行特定動作。
* 新的訊息會出現在佇列中。

本教學課程中建立邏輯應用程式，監視變更 tooa 虛擬機器，並將傳送電子郵件有關這些變更。 當您建立邏輯應用程式與 Azure 資源的事件訂閱時，事件流程從事件方格 toohello 邏輯應用程式透過該資源。 hello 教學課程會引導您建立此邏輯應用程式：

![概觀 - 使用 Event Grid 和邏輯應用程式來監視虛擬機器](./media/monitor-virtual-machine-changes-event-grid-logic-app/monitor-virtual-machine-event-grid-logic-app-overview.png)

在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 建立可從 Event Grid 監視事件的邏輯應用程式。
> * 新增可特別檢查虛擬機器變更的條件。
> * 在虛擬機器變更時傳送電子郵件。

## <a name="prerequisites"></a>必要條件

* 來自 [Azure Logic Apps 所支援的任何電子郵件提供者](../connectors/apis-list.md)的電子郵件帳戶，例如 Office 365 Outlook、Outlook.com 或 Gmail，以傳送通知。 本教學課程是使用 Office 365 Outlook。

* [虛擬機器](https://azure.microsoft.com/services/virtual-machines)。 如果您尚未這樣做，請透過[建立 VM 教學課程](https://docs.microsoft.com/azure/virtual-machines/)來建立虛擬機器。 toomake hello 虛擬機器發行事件，您[不需要任何其他 toodo](../event-grid/overview.md)。

## <a name="create-a-logic-app-that-monitors-events-from-an-event-grid"></a>建立可從 Event Grid 監視事件的邏輯應用程式

首先，建立邏輯應用程式，並加入您的虛擬機器的 hello 資源群組會監視事件方格觸發程序。 

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。 

2. 從 hello 的左上角 hello 主要 Azure 功能表，選擇 **新增** > **企業整合** > **邏輯應用程式**。

   ![建立邏輯應用程式](./media/monitor-virtual-machine-changes-event-grid-logic-app/azure-portal-create-logic-app.png)

3. 建立邏輯應用程式指定 hello 下表中的 hello 設定：

   ![提供邏輯應用程式詳細資料](./media/monitor-virtual-machine-changes-event-grid-logic-app/create-logic-app-for-event-grid.png)

   | 設定 | 建議的值 | 說明 | 
   | ------- | --------------- | ----------- | 
   | **名稱** | {your-logic-app-name} | 提供唯一的邏輯應用程式名稱。 | 
   | **訂用帳戶** | {your-Azure-subscription} | 選取 hello 相同 Azure 訂用帳戶的所有服務在本教學課程。 | 
   | **資源群組** | {your-Azure-resource-group} | 選取 hello 本教學課程中的所有服務相同的 Azure 資源群組。 | 
   | **位置** | {your-Azure-region} | 選取 hello 本教學課程中的所有服務都有相同的區域。 | 
   | | | 

4. 當您準備好時，選取**Pin toodashboard**，然後選擇 **建立**。

   您現在已經為您的應用程式邏輯建立一項 Azure 資源。 
   Azure 會將您的邏輯應用程式部署之後，hello 邏輯應用程式的設計工具顯示您範本的一般模式讓您可以更快開始。

   > [!NOTE] 
   > 當您選取**Pin toodashboard**，應用程式邏輯會自動開啟邏輯應用程式的設計工具中。 不然，您可以手動尋找並開啟您的邏輯應用程式。

5. 立即選擇邏輯應用程式範本。 在 [範本] 之下，選擇 [空白邏輯應用程式]，以便從頭建置邏輯應用程式。

   ![選擇 [邏輯應用程式] 範本](./media/monitor-virtual-machine-changes-event-grid-logic-app/choose-logic-app-template.png)

   hello 邏輯應用程式的設計工具現在會顯示您[*連接器*](../connectors/apis-list.md)和[*觸發程序*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)邏輯應用程式，並也動作，您可以使用 toostart您可以新增觸發程序 tooperform 工作之後。 觸發程序是可建立邏輯應用程式執行個體並啟動邏輯應用程式工作流程的事件。 
   邏輯應用程式需要觸發程序為 hello 第一個項目。

6. Hello 搜尋方塊中，輸入 「 事件方格 」 做為您的篩選器。 選取此觸發程序：**Azure Event Grid - 在資源事件上**

   ![選取此觸發程序：「Azure Event Grid - 在資源事件上」](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger.png)

7. 出現提示時，登入與您的 Azure 認證 tooAzure 事件方格。

   ![利用您的 Azure 認證登入](./media/monitor-virtual-machine-changes-event-grid-logic-app/sign-in-event-grid.png)

   > [!NOTE]
   > 如果您已經登入個人 Microsoft 帳戶，例如@outlook.com或@hotmail.com，hello 事件方格觸發程序可能無法正確顯示。 因應措施，請選擇[連線與服務主體](/azure-resource-manager/resource-group-create-service-principal-portal.md)，或驗證 hello 與您 Azure 訂用帳戶，例如相關的 Azure Active Directory 的成員身分*使用者名稱*@emailoutlook.onmicrosoft.com.

8. 現在訂閱您 toopublisher 邏輯應用程式的事件。 提供您 hello 下表中所指定的事件訂閱 hello 詳細資料：

   ![提供事件訂閱的詳細資料](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details-generic.png)

   | 設定 | 建議的值 | 說明 | 
   | ------- | --------------- | ----------- | 
   | **訂用帳戶** | {virtual-machine-Azure-subscription} | 選取 hello 事件發行者的 Azure 訂用帳戶。 此教學課程中，選取 hello 虛擬機器的 Azure 訂用帳戶。 | 
   | **資源類型** | Microsoft.Resources.resourceGroups | 選取 hello 事件發行者的資源類型。 此教學課程中，選取 hello 指定的值，因此邏輯應用程式監視只資源群組。 | 
   | **資源名稱** | {virtual-machine-resource-group-name} | 選取 hello 發行者的資源名稱。 此教學課程中，選取 hello hello 資源群組名稱為虛擬機器。 | 
   | 針對選擇性設定，選擇 [顯示進階選項]。 | {see descriptions} | * **前置詞篩選條件**：在此教學課程中，將此設定保留空白。 hello 預設行為會比對所有的值。 不過，您可以指定前置詞字串作為篩選條件，例如，特定資源的路徑和參數。 <p>* **後置詞篩選條件**：在此教學課程中，將此設定保留空白。 hello 預設行為會比對所有的值。 不過，您可以指定前置詞字串作為篩選條件，例如，副檔名 (如果只想要特定檔案類型)。<p>* **訂用帳戶名稱**：提供事件訂用帳戶的唯一名稱。 |
   | | | 

   當您完成時，Event Grid 觸發程序可能如此範例所示︰
   
   ![範例 Event Grid 觸發程序詳細資料](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details.png)

9. 儲存您的邏輯應用程式。 Hello 設計工具工具列上，選擇**儲存**。 toocollapse 和隱藏動作的詳細資料，在邏輯應用程式，然後選擇 hello 動作的標題列。

   ![儲存您的邏輯應用程式](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save.png)

   當您儲存應用程式邏輯與事件方格的觸發程序時，Azure 會自動建立邏輯應用程式選取 tooyour 資源事件訂閱。 因此當 hello 資源發行事件 toohello 事件方格時，該事件方格自動推入 hello 事件 tooyour 邏輯應用程式。 此事件觸發程序邏輯應用程式，然後建立及執行您在下面的步驟中定義的 hello 工作流程執行個體。

邏輯應用程式現在是即時和會接聽 tooevents hello 事件方格中，但不會加入動作 toohello 工作流程之前執行任何動作。 

## <a name="add-a-condition-that-checks-for-virtual-machine-changes"></a>新增可檢查虛擬機器變更的條件

toorun 邏輯應用程式工作流程的特定事件發生時，才會加入條件來檢查虛擬機器的 「 寫入 」 作業。 此條件為 true 時，應用程式邏輯會將傳送您電子郵件傳送嗨更新虛擬機器的相關詳細資料。

1. 邏輯應用程式的設計工具，在 hello 事件方格觸發程序，在選擇**新步驟** > **加入條件**。

   ![新增條件 tooyour 邏輯應用程式](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-add-condition-step.png)

   hello 邏輯應用程式的設計工具加入了空白的條件 tooyour 工作流程，包括動作路徑 toofollow 根據是否 hello 條件為 true 或 false。

   ![空白條件](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-add-empty-condition.png)

2. 在 hello**條件**方塊中，選擇**在進階模式中編輯**。
輸入此運算式：

   `@equals(triggerBody()?['data']['operationName'], 'Microsoft.Compute/virtualMachines/write')`

   您的條件現在看起來就像下面這個範例︰

   ![空白條件](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-expression.png)

   這個運算式會檢查 hello 事件`body`如`data`物件在 hello`operationName`屬性為 hello`Microsoft.Compute/virtualMachines/write`作業。 
   深入了解 [Event Grid 事件結構描述](../event-grid/event-schema.md)。

3. tooprovide hello 條件的描述選擇 hello**省略符號**(**...**) 按鈕上 hello 條件 」 圖形，然後選擇**重新命名**。

   > [!NOTE] 
   > hello 稍後在本教學課程的範例也會提供描述 hello 邏輯應用程式工作流程中的步驟。

4. 現在選擇**在基本模式中編輯**以便 hello 運算式自動解決所示：

   ![邏輯應用程式條件](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-1.png)

5. 儲存您的邏輯應用程式。

## <a name="send-email-when-your-virtual-machine-changes"></a>在虛擬機器變更時傳送電子郵件

現在，加入[*動作*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)以便 hello 指定條件為 true 時，收到電子郵件。

1. 在 hello 條件**如果為 true**方塊中，選擇**將動作加入**。

   ![新增條件為 true 時的動作](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-2.png)

2. 在 hello 搜尋方塊中輸入"email"做為您的篩選器。 根據您的電子郵件提供者，尋找並選取 hello 比對的連接器。 然後選取您連接器的 hello 「 傳送電子郵件 」 動作。 例如： 

   * Azure 工作或學校帳戶，請選取 hello Office 365 Outlook 連接器。 
   * 個人的 Microsoft 帳戶中，選取 hello Outlook.com 連接器。 
   * Gmail 帳戶選取 hello Gmail 連接器。 

   我們 toocontinue 與 hello Office 365 Outlook 連接器。 
   如果您使用不同的提供者，步驟的 hello hello 相同，但您的 UI 可能會出現不同。 

   ![選取 [傳送電子郵件] 動作](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email.png)

3. 如果您還沒有為電子郵件提供者連接，登入 tooyour 電子郵件帳戶時詢問您進行驗證。

4. Hello hello 下表中所指定的電子郵件中提供詳細資料：

   ![空白的電子郵件動作](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-empty-email-action.png)

   > [!TIP]
   > 從您的工作流程中可用的欄位 tooselect 按一下編輯方塊中因此該 hello**動態內容**清單隨即開啟，或選擇**加入動態內容**。 取得更多的欄位，選擇 **看到更多**hello 清單中每個區段。 tooclose hello**動態內容**清單中，選擇**加入動態內容**。

   | 設定 | 建議的值 | 說明 | 
   | ------- | --------------- | ----------- | 
   | **To** | {recipient-email-address} |輸入 hello 收件者的電子郵件地址。 為了測試用途，您可以使用自己的電子郵件地址。 | 
   | **主旨** | 更新的資源：**主旨**| 輸入 hello 電子郵件主旨 hello 內容。 此教學課程中，輸入 hello 建議的文字和選取 hello 事件**主旨**欄位。 在這裡，您的電子郵件主旨包含 hello hello 更新資源 （虛擬機器） 的名稱。 | 
   | **內文** | 資源群組：**主題** <p>事件類型：**事件類型**<p>事件識別碼：**識別碼**<p>時間：**事件時間** | 輸入 hello 內容 hello 電子郵件內文。 此教學課程中，輸入 hello 建議的文字和選取 hello 事件**主題**，**事件類型**，**識別碼**，和**事件時間**欄位以便您的電子郵件包含 hello 資源群組名稱、 事件類型、 事件時間戳記，以及 hello 更新的事件識別碼。 <p>tooadd 空白行，在您的內容，請按 Shift + Enter。 | 
   | | | 

   > [!NOTE] 
   > 如果您選取的欄位，代表陣列，hello 設計工具會自動將加入**每個**參考 hello 陣列的 hello 動作的迴圈。 如此一來，應用程式邏輯會在每個陣列項目上執行該動作。

   現在，您的電子郵件動作看起來可能就像下面這個範例︰

   ![選取電子郵件中的輸出 tooinclude](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email-details.png)

   完成的邏輯應用程式可能如此範例所示︰

   ![完成的邏輯應用程式](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-completed.png)

5. 儲存您的邏輯應用程式。 toocollapse] 和 [隱藏每個動作的詳細資料，在邏輯應用程式，然後選擇 hello 動作的標題列。

   ![儲存您的邏輯應用程式](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save-completed.png)

   邏輯應用程式現在是即時的但是會等候變更 tooyour 虛擬機器執行的任何項目之前。 
   tootest 邏輯應用程式現在繼續 toohello 下一節。

## <a name="test-your-logic-app-workflow"></a>測試邏輯應用程式工作流程

1. 邏輯應用程式即將 hello toocheck 指定事件，請更新您的虛擬機器。 

   例如，您可以調整大小 hello Azure 入口網站中的虛擬機器或[調整您的 VM 使用 Azure PowerShell](../virtual-machines/windows/resize-vm.md)。 

   一會兒之後，您應可取得電子郵件。 例如：

   ![關於虛擬機器更新的電子郵件](./media/monitor-virtual-machine-changes-event-grid-logic-app/email.png)

2. tooreview hello 執行，並選擇邏輯應用程式，在邏輯應用程式功能表上的觸發程序記錄**概觀**。 tooview 詳細執行中，在該回合的選擇 hello 資料列。

   ![邏輯應用程式執行記錄](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history.png)

3. tooview hello 輸入和輸出的每個步驟中，展開您想 tooreview hello 步驟。 此資訊可協助您診斷和偵錯應用程式邏輯中的問題。
 
   ![邏輯應用程式執行記錄詳細資料](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history-details.png)

恭喜，您已建立並執行邏輯應用程式，該邏輯應用程式可透過 Event Grid 監視資源事件，以及在這些事件發生時監視電子郵件。 您也了解如何輕鬆地建立工作流程，以自動執行程序並整合系統與雲端服務。

## <a name="clean-up-resources"></a>清除資源

本教學課程使用會資源並執行會產生 Azure 訂用帳戶費用的動作。 因此當您完成時的 hello 教學課程和測試，請確定您停用或刪除，您不想 tooincur 費用的任何資源。

您可以停止執行，然後傳送電子郵件，而不刪除 hello 應用程式從應用程式邏輯。 在邏輯應用程式功能表上，選擇 [概觀]。 在 hello 工具列上選擇 **停用**。

![關閉應用程式邏輯](./media/monitor-virtual-machine-changes-event-grid-logic-app/turn-off-disable-logic-app.png)

## <a name="faq"></a>常見問題集

**問：**：我可以使用 Event Grid 和邏輯應用程式執行其他哪些虛擬機器監視工作？ </br>
**答**：您可以監視其他組態變更，例如：

* 虛擬機器取得角色型存取控制 (RBAC) 權限。
* Tooa 網路安全性群組 (NSG) 上的網路介面 (NIC) 時，會進行變更。
* 已新增或移除虛擬機器的磁碟。
* 公用 IP 位址指派 tooa 虛擬機器 nic。

## <a name="next-steps"></a>後續步驟

* [Event Grid 概觀](../event-grid/overview.md)
* [Event Grid 概念](../event-grid/concepts.md)
* [快速入門：使用 Event Grid 建立和路由傳送自訂事件](../event-grid/custom-event-quickstart.md)
* [Event Grid 事件結構描述](../event-grid/event-schema.md)
* [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md)
* [使用預先定義的範本來建立邏輯應用程式工作流程](../logic-apps/logic-apps-use-logic-app-templates.md)
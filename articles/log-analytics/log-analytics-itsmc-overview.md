---
title: "在 OMS 中的服務管理連接器 aaaIT |Microsoft 文件"
description: "使用 hello IT 服務管理連接器 toocentrally 監視和管理 hello ITSM 工作項目，在 OMS 中，以及快速解決任何問題。"
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a>使用 IT 服務管理連接器 (預覽) 將 ITSM 工作項目集中管理

![IT 服務管理連接器符號](./media/log-analytics-itsmc/itsmc-symbol.png)

您可以使用 OMS 記錄分析 toocentrally 監視器中的 hello IT 服務管理連接器 (ITSMC)，並管理工作項目到 ITSM 的產品/服務。

hello IT 服務管理連接器與 OMS 記錄分析整合，您的現有 IT 服務管理 (ITSM) 產品和服務。  hello 方案中有與 ITSM 產品/服務的雙向整合，它會提供在 hello OMS 使用者選項 toocreate 事件、 警示或 ITSM 方案中的事件。 hello 連接器也會匯入資料，例如事件、 以及 ITSM 方案變更要求，到 OMS 記錄分析。

利用 IT 服務管理連接器，您可以：

  - 將您組織內使用的 ITSM 產品/服務之工作項目集中監視及管理。
  - 從 OMS 警示及透過記錄搜尋，在 ITSM 中建立 ITSM 工作項目 (例如警示、事件、活動)。
  - 讀取 ITSM 解決方案的事件和變更要求，並與 Log Analytics 工作區中的相關記錄資料相互關聯。
  - 尋找任何非預期且不尋常的事件並解決問題，甚至之前 hello 使用者呼叫，並回報 toohello 技術服務人員。
  - 將工作項目資料匯入 Log Analytics，並建立關鍵效能指標 (KPI) 報告。  您可以使用這些報告來識別、評估和處理數個重要的項目，例如惡意程式碼評估。
  - 請檢視策劃儀表板，以獲得關於事件、變更要求及受影響系統的更深入見解。
  - 疑難排解更快建立相互關聯與 hello 記錄分析工作區中其他管理解決方案。


## <a name="prerequisites"></a>必要條件

tooimport hello ITSM 工作項目到 OMS 記錄分析，hello 解決方案需要 hello OMS 中的 hello IT 服務管理連接器與 hello IT SM 產品/服務從中匯入 hello 工作項目之間的連線。


## <a name="configuration"></a>組態

新增 hello IT 服務管理連接器方案 tooyour OMS 工作空間中，使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。

IT 服務管理連接器磚 hello 解決方案資源庫中所示：

![連接器圖格](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

之後成功時，您會看到 hello IT 服務管理連接器**OMS** > **設定** > **連接的來源。**

![ITSMC 已連線](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> 根據預設，hello IT 服務管理連接器重新整理一次中每隔 24 小時 hello 連接的資料。 toorefresh 連接的資料立即的任何編輯或範本更新您所做的按一下 hello 重新整理按鈕顯示 下一步 tooyour 連線。

 ![ITSMC 重新整理](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a>管理組件
此解決方案不需要任何管理組件。

## <a name="connected-sources"></a>連接的來源

hello 下列 ITSM 產品/服務支援 IT 服務管理連接器 hello:

- [System Center Service Manager (SCSM)](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [ServiceNow](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [Provance](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [Cherwell](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a>使用 hello 解決方案

一旦 ITSM 服務連線 hello OMS IT 服務管理連接器，hello 記錄分析服務會開始收集 hello 連接 ITSM 產品/服務的 hello 資料。

> [!NOTE]
> - IT 服務管理連接器解決方案所匯入的資料會出現在 Log Analytics 中，作為名為 **ServiceDesk_CL** 的事件。
- 事件會包含一個名為 **ServiceDeskWorkItemType_s** 的欄位。 這可以接受做為事件，其值或變更要求、 hello 根據工作項目資料包含在 hello **ServiceDesk_CL**事件。

## <a name="input-data"></a>輸入資料
工作項目從 hello ITSM 產品/服務匯入。

hello 下列資訊顯示 hello IT 服務管理連接器所收集資料的範例：

> [!NOTE]
> Hello 根據工作項目類型匯入到記錄分析**ServiceDesk_CL**包含下列欄位的 hello:

**工作項目︰****事件**  
ServiceDeskWorkItemType_s="Incident"

**欄位**

- ServiceDeskConnectionName
- 服務台識別碼
- State
- 急迫性
- 影響
- 優先順序
- 升級
- 建立者
- 解決者
- 關閉者
- 來源
- 指派對象
- 類別
- 課程名稱
- 說明
- 建立日期
- 關閉日期
- 解決日期
- 上次修改日期
- 電腦


**工作項目︰****變更要求**

ServiceDeskWorkItemType_s="ChangeRequest"

**欄位**
- ServiceDeskConnectionName
- 服務台識別碼
- 建立者
- 關閉者
- 來源
- 指派對象
- Title
- 類型
- 類別
- State
- 升級
- 衝突狀態
- 急迫性
- 優先順序
- 風險
- 影響
- 指派對象
- 建立日期
- 關閉日期
- 上次修改日期
- 要求日期
- 計劃開始日期
- 計劃結束日期
- 工作開始日期
- 工作結束日期
- 說明
- 電腦

## <a name="output-data-for-a-servicenow-incident"></a>ServiceNow 事件的輸出資料

| OMS 欄位 | ITSM 欄位 |
|:--- |:--- |
| ServiceDeskId_s| 數字 |
| IncidentState_s | State |
| Urgency_s |急迫性 |
| Impact_s |影響|
| Priority_s | 優先順序 |
| CreatedBy_s | 開啟者 |
| ResolvedBy_s | 解決者|
| ClosedBy_s  | 關閉者 |
| Source_s| 連絡人型別 |
| AssignedTo_s | 指派太 |
| Category_s | 類別 |
| Title_s|  簡短說明 |
| Description_s|  注意事項 |
| CreatedDate_t|  已開啟 |
| ClosedDate_t| 關閉|
| ResolvedDate_t|已解決|
| 電腦  | 設定項目 |

## <a name="output-data-for-a-servicenow-change-request"></a>ServiceNow 變更要求的輸出資料

| OMS 欄位 | ITSM 欄位 |
|:--- |:--- |
| ServiceDeskId_s| 數字 |
| CreatedBy_s | 要求者 |
| ClosedBy_s | 關閉者 |
| AssignedTo_s | 指派太 |
| Title_s|  簡短說明 |
| Type_s|  類型 |
| Category_s|  類別 |
| CRState_s|  State|
| Urgency_s|  急迫性 |
| Priority_s| 優先順序|
| Risk_s| 風險|
| Impact_s| 影響|
| RequestedDate_t  | 要求的日期 |
| ClosedDate_t | 關閉日期 |
| PlannedStartDate_t  |     計劃開始日期 |
| PlannedEndDate_t  |   計劃結束日期 |
| WorkStartDate_t  | 實際開始日期 |
| WorkEndDate_t | 實際結束日期|
| Description_s | 說明 |
| 電腦  | 設定項目 |

**ITSM 資料的範例 Log Analytics 畫面︰**

![Log Analytics 畫面](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a>IT 服務管理連接器 – 與其他 OMS 解決方案整合

IT 服務管理連接器，目前支援與 hello 服務對應解決方案整合。

服務對應會自動探索 hello Windows 上的應用程式元件和 Linux 系統和對應 hello 服務之間的通訊。 它可讓您 tooview 您的伺服器，當您將它們 – 互連提供重要服務的系統。 不需要進行任何設定，只要安裝了代理程式，服務對應就會顯示橫跨任何 TCP 連接架構的伺服器、處理程序和連接埠之間的連接。 詳細資訊︰[服務對應](../operations-management-suite/operations-management-suite-service-map.md)。

使用這項整合，您可以檢視 hello 下列範例所示，在 hello ITSM 方案中建立的 hello 服務支援項目：

![整合式解決方案 ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a>建立 OMS 警示的 ITSM 工作項目

Hello OMS 警示，您可以在 hello 連接 ITSM 來源中建立相關聯的工作項目。  toodo 程序後，使用 hello:

1. 從**記錄搜尋**視窗中，執行記錄搜尋查詢 tooview 資料。 查詢結果會 hello 來源工作項目。
2. 在**記錄搜尋**，按一下 **警示**tooopen hello**加入警示規則**頁面。

    ![Log Analytics 畫面](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. 在 hello**加入警示規則**視窗中，提供所需的 hello 詳細資料，如**名稱**，**嚴重性**，**搜尋查詢**，和**警示準則**（時間視窗度量的度量單位）。
4. 在 [ITSM 動作] 選取 [是]。
5. 選取您 ITSM 連線從 hello**選取連接**清單。
6. 提供所需的 hello 詳細資料。
7. 此警示，請選取 hello 的每個記錄項目不同的工作項目 toocreate**建立個別的工作項目，每個記錄項目**核取方塊。

    或

    將保留任意數目的記錄項目，這項警示之下此核取方塊未選取的 toocreate 只有一個工作項目。

7. 按一下 [儲存] 。

底下建立 hello OMS 警示**警示**。 hello 對應 ITSM 連線網路的工時 hello 指定的警示的條件符合時，會建立項目。

## <a name="create-itsm-work-items-from-oms-logs"></a>從 OMS 記錄建立 ITSM 工作項目

您可以使用 OMS 記錄搜尋，連接的 hello ITSM 來源中建立工作項目。 toodo 程序後，使用 hello:

1. 從**記錄搜尋**，搜尋所需的 hello 資料、 選取 hello 詳細資料，然後按一下**建立工作項目**。

    hello**建立 ITSM 工作項目** 視窗隨即出現：

    ![Log Analytics 畫面](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   新增下列詳細資料的 hello:

  - **工作項目標題**: hello 工作項目的標題。
  - **工作項目描述**: hello 新工作項目的描述。
  - **受影響電腦**: hello 找此記錄資料的電腦名稱。
  - **選取連接**: ITSM 連接您想在其中 toocreate 這個工作項目。
  - **工作項目**︰工作項目的類型。

3. 按一下 toouse 事件時，現有工作項目範本**是**下**hello 範本為基礎的產生工作項目**選項，然後再按一下**建立**。

    或者，

    按一下**否**您希望 tooprovide 您自訂的值。

4. 提供 hello 適當的值在 hello**連絡人類型**，**影響**，**急迫性**，**類別**，和**子類別目錄**文字方塊中，然後按一下**建立**。

hello 工作項目將會建立在 hello ITSM，您也可以在 OMS 中檢視。

## <a name="troubleshoot-itsm-connections-in-oms"></a>針對 OMS 中的 ITSM 連線進行疑難排解
1.  如果從已連接的來源 UI 的連線失敗，且您 hello**儲存連接時發生錯誤**訊息，請執行下列 hello:
 - 發生 ServiceNow、 Cherwell 和 Provance 連接，確保您正確輸入的 hello 使用者名稱/密碼與用戶端識別碼/用戶端密碼 hello 連線的每個。 如果 hello 錯誤持續發生，請檢查是否有足夠的權限在 hello 對應 ITSM 產品 toomake hello 的連接。
 - 發生 Service Manager，請確認 hello Web 應用程式部署成功建立混合式連接。 tooverify hello 連接已成功建立與 hello 內部的 Service Manager 電腦，請瀏覽 hello 文件以 hello 中所述的 hello Web 應用程式 URL[混合式連接](log-analytics-itsmc-connections.md#configure-the-hybrid-connection)。

2.  如果資料 servicenow 未取得 OMS 中同步處理，請確定該 hello ServiceNow 執行個體非睡眠中。 可能造成此結果一段時間中 hello ServiceNow 開發人員執行個體閒置時。 否則，報表 hello 問題。
3.  如果會取得從 OMS 來引發警示，但沒有取得 ITSM 產品在建立工作項目或設定項目不會進行建立/連結 toowork 項目或任何泛型資訊，請勿 hello 遵循：
 -  在 OMS 入口網站中的 IT 服務管理連接器解決方案可能是使用的 tooget 連接/工作項目/電腦等的摘要。按一下 hello hello 狀態刀鋒視窗中的錯誤訊息，瀏覽過**記錄搜尋**並檢視 hello 連接具有 hello 錯誤 hello 錯誤訊息中使用 hello 詳細資料。
 - 您可以直接檢視 hello 中的 hello/錯誤相關資訊**記錄搜尋**網頁的*類型 = ServiceDeskLog_CL*。

## <a name="troubleshoot-service-manager-web-app-deployment"></a>針對 Service Manager Web 應用程式部署進行疑難排解
1.  如果使用部署 web 應用程式的任何問題，請確定您有足夠的權限 hello 訂用帳戶中所述 toocreate/部署資源。
2.  如果**物件參考未設定物件的 tooinstance**執行 hello 時出現錯誤訊息[指令碼](log-analytics-itsmc-service-manager-script.md)請確認您輸入有效的值下,**使用者設定**> 一節。
3.  如果您無法 toocreate 服務匯流排轉送命名空間，請確定該 hello 需要 hello 訂用帳戶中註冊資源提供者。 如果未註冊，以手動方式建立從 hello Azure 入口網站。 您也可以建立它時[建立 hello 混合式連接](log-analytics-itsmc-connections.md#configure-the-hybrid-connection)從 hello Azure 入口網站。


## <a name="contact-us"></a>與我們連絡

對於任何查詢或 hello IT 服務管理連接器上的意見反應，請與我們連絡[ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com)。

## <a name="next-steps"></a>後續步驟
[新增 ITSM 產品/服務 tooIT Service Management Connector](log-analytics-itsmc-connections.md)。

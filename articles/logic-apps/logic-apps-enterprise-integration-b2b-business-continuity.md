---
title: "B2B 整合帳戶-Azure 邏輯應用程式的 aaaDisaster 復原 |Microsoft 文件"
description: "Logic Apps B2B 災害復原"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e86564a3c5a2607d22514936c606e2843cba0416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a>Logic Apps B2B 跨區域災害復原

B2B 工作負載涉及金錢交易，例如訂單和發票。 在發生損壞事件，它是關鍵商業層級 Sla 達成了協議與交易夥伴商務 tooquickly 復原 toomeet hello 項目。 本文示範如何 toobuild 業務持續性計劃 B2B 工作負載。 

* 災害復原整備 
* 在嚴重損壞事件期間容錯移轉 toosecondary 區域 
* 切換回 tooprimary 區域之後發生損壞事件

## <a name="disaster-recovery-readiness"></a>災害復原整備  

1. 指出次要區域並建立[整合帳戶](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md)hello 次要區域中。

2. 新增夥伴、 結構描述和合約的執行狀態的 hello 中需要複寫 toobe toosecondary 區域整合帳戶所需的 hello 訊息流程。

   > [!TIP]
   > 請確定沒有一致性 hello 整合帳戶成品的命名慣例在跨區域。 

3. hello 主要區域中，從執行狀態的 toopull hello hello 次要區域中建立邏輯應用程式。 

   這個邏輯應用程式應該有觸發程序和動作。 
   hello 觸發程序應該連接 tooprimary 區域整合帳戶，並 hello 動作應該 toosecondary 區域整合帳戶連接。 
   根據 hello 時間間隔，hello 觸發程序輪詢 hello 主要區域執行狀態資料表，並且會提取 hello 新的記錄，如果有的話。 hello 動作來更新這些 toosecondary 區域整合帳戶。 
   這是從主要區域 toosecondary 區域有助於 tooget 累加式的執行階段狀態。

4. 業務續航力 Logic Apps 整合帳戶被設計 toosupport B2B 通訊協定-X12、 AS2 和 EDIFACT 為基礎。 toofind 詳細步驟，選取 hello 各自的連結。

5. hello 建議太 toodeploy 次要區域中的所有主要區域資源。 

   主要區域的資源包括 Azure SQL Database 或 Azure Cosmos DB、 Azure 服務匯流排和 Azure 事件中心用於訊息、 Azure API 管理，以及 Azure App Service 中的 hello Azure 邏輯應用程式功能。   

6. 從建立連線的主要區域 tooa 次要區域。 主要區域中，從執行狀態的 toopull hello 次要區域中建立邏輯應用程式。 

   hello 邏輯應用程式應該有觸發程序和動作。 
   hello 觸發程序應該連接 tooa 主要區域整合帳戶。 
   hello 動作應該連接 tooa 次要區域整合帳戶。 
   根據 hello 時間間隔，hello 觸發程序輪詢 hello 主要區域執行狀態資料表，並且會提取 hello 新的記錄，如果有的話。 
   hello 動作來更新這些 tooa 次要區域整合帳戶。 
   此程序有助於 tooget 累加式的執行階段狀態從 hello 主要區域 toohello 次要區域。

業務續航力 Logic Apps 整合帳戶提供根據 hello B2B 通訊協定 X12、 AS2 和 EDIFACT 的支援。 如需使用 X12 和 AS2 的詳細步驟，請參閱本文中的 [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) 和 [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2)。

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a>在嚴重損壞事件期間容錯移轉 tooa 次要區域

Hello 主要地區未提供商務持續性資料流導向 toohello 次要區域在嚴重損壞事件。 次要區域可讓您商務 toorecover 函數快速 toomeet hello RPO/RTO 同意其夥伴。 它也會盡可能降低努力 toofail 透過從一個區域 tooanother 區域。 

同時複製的主要區域 tooa 次要區域中的控制編號沒有預期的延遲。 tooavoid 傳送產生的重複控制編號 toopartners 災害事件期間，hello 建議使用將 tooincrement hello 控制編號會在 hello 次要區域協議[PowerShell cmdlet](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery)。

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a>切換回 tooa 主要區域後發生損壞事件

toofall 後 tooa 主要區域時，請遵循下列步驟：

1. 停止接受來自夥伴 hello 次要區域中的訊息。  

2. 使用遞增 hello 主要區域的所有合約的 hello 產生控制編號[PowerShell cmdlet](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery)。  

3. 直接從 hello 次要區域 toohello 主要區域的流量。

4. 檢查建立 hello 提取從 hello 主要區域執行狀態的次要區域中的 hello 邏輯應用程式已啟用。

## <a name="x12"></a>X12 

EDI X12 文件的商務持續性是根據控制編號：

> [!TIP]
> 您也可以使用 hello [X12 快速啟動範本](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/)toocreate 邏輯應用程式。 建立主要和次要整合帳戶就是先決條件 toouse hello 範本。 hello 範本可協助 toocreate 兩個邏輯應用程式，一個用於接收的控制編號，另一個用於產生的控制編號。 Hello logic apps 連接 hello 觸發程序 toohello 主要整合帳戶與 hello 動作 toohello 次要整合帳戶中建立個別的觸發程序和動作。

**必要條件**

對於輸入訊息，tooenable 嚴重損壞修復 hello X12 協議的接收設定中，選取 hello 重複檢查設定。

![選取重複檢查設定](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. 在次要地區中建立[邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。    

2. 搜尋 **X12**，並選取 [X12 - 當控制編號修改時]。   

   ![搜尋 x12](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   hello 觸發程序會提示您 tooestablish 連線 tooan 整合帳戶。 
   hello 觸發程序應該連接 tooa 主要區域整合帳戶。

3. 輸入連線名稱，選取您*主要區域整合帳戶*從 hello 清單，並選擇**建立**。   

   ![主要區域整合帳戶名稱](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. hello **DateTime toostart 控制編號同步**設定是選擇性的。 hello**頻率**可以設定得**天**，**小時**，**分鐘**，或**第二個**間隔。   

   ![日期時間和頻率](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. 選取 [新增步驟] > [新增動作]。

   ![選取 [新增步驟]，然後選取 [新增動作]](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. 搜尋 **X12**，並選取 [X12 - 新增或更新控制編號]。   

   ![新增或更新控制編號](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. 選取 tooconnect 動作 tooa 次要區域整合帳戶，**變更連接** > **加入新的連接**hello 取得整合帳戶的清單。 輸入連線名稱，選取您*次要區域整合帳戶*從 hello 清單，並選擇**建立**。 

   ![次要地區整合帳戶名稱](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. 切換 tooraw 輸入 hello 右上角的圖示即可。

   ![切換 tooraw 輸入](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. 從 hello 動態內容選擇器中，選取主體，並儲存 hello 邏輯應用程式。

   ![動態內容欄位](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   根據 hello 時間間隔，hello 觸發程序會輪詢 hello 收到的主要區域控制編號的資料表，並會提取 hello 新記錄。 
   hello 動作來更新 hello 次要區域整合帳戶中的 hello 記錄。 
   如果有任何更新，hello 觸發程序狀態會顯示為**已略過**。   

   ![控制編號資料表](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

根據 hello 時間間隔，hello 累加式的執行階段狀態將會從複寫的主要區域 tooa 次要區域。 在 hello 主要區域無法時可用的直接流量 toohello 次要區域的業務持續性的嚴重損壞事件。 

## <a name="edifact"></a>EDIFACT 

EDI EDIFACT 文件的商務持續性是根據控制編號。

**必要條件**

tooenable 災害復原，對於輸入訊息，會選取 EDIFACT 協議的接收設定中的 hello 重複檢查設定。

![選取重複檢查設定](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. 在次要地區中建立[邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。    

2. 搜尋 **EDIFACT**，並選取 [EDIFACT - 當控制編號修改時]。

   ![搜尋 EDIFACT](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   hello 觸發程序會提示您 tooestablish 連線 tooan 整合帳戶。 
   hello 觸發程序應該連接 tooa 主要區域整合帳戶。 

3. 輸入連線名稱，選取您*主要區域整合帳戶*從 hello 清單，並選擇**建立**。    

   ![主要區域整合帳戶名稱](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. hello **DateTime toostart 控制編號同步**設定是選擇性的。 hello**頻率**可以設定得**天**，**小時**，**分鐘**，或**第二個**間隔。    

   ![日期時間和頻率](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. 選取 [新增步驟] > [新增動作]。    

   ![選取 [新增步驟]，然後選取 [新增動作]](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. 搜尋 **EDIFACT**，並選取 [EDIFACT - 新增或更新控制編號]。   

   ![新增或更新控制編號](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. 選取 tooconnect 動作 tooa 次要區域整合帳戶，**變更連接** > **加入新的連接**hello 取得整合帳戶的清單。 輸入連線名稱，選取您*次要區域整合帳戶*從 hello 清單，並選擇**建立**。

   ![次要地區整合帳戶名稱](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. 切換 tooraw 輸入 hello 右上角的圖示即可。

   ![切換 tooraw 輸入](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. 從 hello 動態內容選擇器中，選取主體，並儲存 hello 邏輯應用程式。   

   ![動態內容欄位](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   根據 hello 時間間隔，hello 觸發程序會輪詢 hello 收到的主要區域控制編號的資料表，並會提取 hello 新記錄。
   hello 動作來更新 hello 記錄 toohello 次要區域整合帳戶。 
   如果有任何更新，hello 觸發程序狀態會顯示為**已略過**。

   ![控制編號資料表](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

根據 hello 時間間隔，hello 累加式的執行階段狀態將會從複寫的主要區域 tooa 次要區域。 在 hello 主要區域無法時可用的直接流量 toohello 次要區域的業務持續性的嚴重損壞事件。 

## <a name="as2"></a>AS2 

業務持續性，使用 hello AS2 通訊協定的文件以 hello 訊息識別碼及 hello MIC 值。

> [!TIP]
> 您也可以使用 hello [AS2 快速入門範本](https://github.com/Azure/azure-quickstart-templates/pull/3302)toocreate 邏輯應用程式。 建立主要和次要整合帳戶就是先決條件 toouse hello 範本。 hello 範本可協助建立觸發程序和動作之邏輯應用程式。 hello 邏輯應用程式會從觸發程序 tooa 主要整合帳戶和動作 tooa 次要整合帳戶建立連接。

1. 建立[邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)hello 次要區域中。  

2. 搜尋 **AS2**，並選取 [AS2 - 建立 MIC 值時]。   

   ![搜尋 AS2](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   觸發程序會提示您 tooestablish 連線 tooan 整合帳戶。 
   hello 觸發程序應該連接 tooa 主要區域整合帳戶。 
   
3. 輸入連線名稱，選取您*主要區域整合帳戶*從 hello 清單，並選擇**建立**。

   ![主要區域整合帳戶名稱](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. hello **DateTime toostart MIC 值同步**設定是選擇性的。 hello**頻率**可以設定得**天**，**小時**，**分鐘**，或**第二個**間隔。   

   ![日期時間和頻率](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. 選取 [新增步驟] > [新增動作]。  

   ![選取 [新增步驟]，然後選取 [新增動作]](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. 搜尋 **AS2**，並選取 [AS2 - 新增或更新 MIC 內容]。  

   ![MIC 新增或更新](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. tooconnect 動作 tooa 次要整合帳戶 中，選取**變更連接** > **加入新的連接**hello 取得整合帳戶的清單。 輸入連線名稱，選取您*次要區域整合帳戶*從 hello 清單，並選擇**建立**。

   ![次要地區整合帳戶名稱](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. 切換 tooraw 輸入 hello 右上角的圖示即可。

   ![切換 tooraw 輸入](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. 從 hello 動態內容選擇器中，選取主體，並儲存 hello 邏輯應用程式。   

   ![動態內容](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   根據 hello 時間間隔，hello 觸發程序會輪詢 hello 主要區域 」 資料表，並會提取 hello 新記錄。 hello 動作來更新這些 toohello 次要區域整合帳戶。 
   如果有任何更新，hello 觸發程序狀態會顯示為**已略過**。  

   ![主要區域資料表](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

根據 hello 時間間隔，hello 累加式的執行階段狀態將會從複寫 hello 主要區域 toohello 次要區域。 在 hello 主要區域無法時可用的直接流量 toohello 次要區域的業務持續性的嚴重損壞事件。 

## <a name="next-steps"></a>後續步驟

[監視 B2B 訊息](logic-apps-monitor-b2b-message.md)


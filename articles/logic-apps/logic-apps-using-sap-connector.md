---
title: "aaaConnect tooan 內部 Azure 邏輯應用程式中的 SAP 系統 |Microsoft 文件"
description: "Tooan 在內部部署 SAP 系統連接與邏輯應用程式工作流程透過 hello 在內部部署資料閘道"
services: logic-apps
author: padmavc
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 594ec5fed337398bf931d396684630ee9f907d2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-on-premises-sap-system-from-logic-apps-with-hello-sap-connector"></a>從邏輯應用程式與 hello SAP 連接器連接 tooan 在內部部署 SAP 系統 

hello 在內部部署資料閘道可讓您 toomanage 資料，並安全地存取內部部署的資源。 本主題說明如何連接邏輯應用程式 tooan 在內部部署 SAP 系統。 在此範例中，邏輯應用程式會透過 HTTP 要求 IDOC，並將傳送 hello 回應傳回。    

> [!NOTE]
> 目前限制： 
> - 邏輯應用程式逾時，如果 hello 回應所需的所有步驟不 hello 內都完成[要求逾時限制](./logic-apps-limits-and-config.md)。 在此情況下，可能會封鎖要求。 
> - hello 檔案選擇器不會顯示所有的 hello 可用的欄位。 在此案例中，您可以手動新增路徑。

## <a name="prerequisites"></a>必要條件

- 安裝及最新設定 hello[在內部部署資料閘道](https://www.microsoft.com/download/details.aspx?id=53127)1.15.6150.1 版本或更新版本。 [如何 tooconnect toohello 內部部署資料閘道，在邏輯應用程式中](http://aka.ms/logicapps-gateway)清單 hello 步驟。 您可以繼續之前，必須安裝 hello 閘道在內部部署電腦上。

- 下載並安裝 hello 最新 SAP 用戶端程式庫上 hello 相同機器 hello 資料閘道的安裝位置。 使用任何下列 SAP 版本 hello: 
    - SAP 伺服器
        - 任何 SAP 伺服器的支援 hello.NET 連接器 (NCo) 3.0
 
    - SAP 用戶端
        - SAP.NET 連接器 (NCo) 3.0

## <a name="add-triggers-and-actions-for-connecting-tooyour-sap-system"></a>加入觸發程序和連接 tooyour SAP 系統的動作

hello SAP 連接器具有的動作，但未觸發程序。 因此，我們有 toouse 另一個觸發程序在 hello hello 工作流程的開頭。 

1. 加入 hello 要求/回應觸發程序，然後選取**新步驟**。

2. 選取**將動作加入**，然後輸入選取 hello SAP 連接器`SAP`hello [搜尋] 欄位中：    

     ![選取 SAP 應用程式伺服器或 SAP 訊息伺服器](media/logic-apps-using-sap-connector/sap-action.png)

3. 選取 [**SAP 應用程式伺服器**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server)或 [**SAP 訊息伺服器**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm)，這取決於您的 SAP 設定。 如果您沒有現有的連接，您必須提示的 toocreate 其中一個。

   1. 選取**連接透過內部部署資料閘道**，並輸入您的 SAP 系統的 hello 詳細資料：   

       ![加入連接字串 tooSAP](media/logic-apps-using-sap-connector/picture2.png)  

   2. 在下**閘道**、 選取現有的閘道或新的閘道 tooinstall、 選取**安裝閘道**。

        ![安裝新的閘道](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. 您輸入所有 hello 詳細資料之後，請選取**建立**。 
   邏輯應用程式設定，並測試 hello 連線，並確定 hello 連線正常運作。

4. 輸入 SAP 連線的名稱。

5. 現在可以使用 hello 不同 SAP 選項。 toofind IDOC 分類，則請從 hello 清單中選取。 或以手動方式輸入 hello 路徑中的和選取 hello HTTP 回應 hello**主體**欄位：

     ![SAP 動作](media/logic-apps-using-sap-connector/picture3.png)

6. 加入建立 hello 動作**HTTP 回應**。 hello 回應訊息應該從 hello SAP 輸出。

7. 儲存您的邏輯應用程式。 傳送 IDOC 透過 hello HTTP 觸發程序 URL 來測試它。 Hello 傳送 IDOC 之後, 等候 hello 回應 hello 邏輯應用程式：   

     > [!TIP]
     > 如何查看太[監視您的 Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md)。

既然 hello SAP 連接器加入 tooyour 邏輯應用程式，開始探索其他功能：

- BAPI
- RFC

## <a name="get-help"></a>取得說明

tooask 問題回答的問題，以及了解哪些其他 Azure 邏輯應用程式使用者的行為，請瀏覽 hello [Azure 邏輯應用程式論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)。

toohelp 改善 Azure 邏輯應用程式和連接器、 票選或送出意見在 hello [Azure 邏輯應用程式使用者意見反應網站](http://aka.ms/logicapps-wish)。

## <a name="next-steps"></a>後續步驟

- 深入了解如何 toovalidate、 轉換和其他 BizTalk 類似函式，在 hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md)。 
- [Tooon 內部部署資料連接](../logic-apps/logic-apps-gateway-connection.md)從邏輯應用程式

---
title: "Azure Cosmos DB 連接器 aaaPower BI 教學課程 |Microsoft 文件"
description: "使用此 Power BI 教學課程 tooimport JSON、 建立具洞察力的報表和視覺化資料使用 hello Azure Cosmos DB 和 Power BI 連接器。"
keywords: "power bi 教學課程，視覺化資料，power bi 連接器"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: cd1b7f70-ef99-40b7-ab1c-f5f3e97641f7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: mimig
ms.openlocfilehash: ca0bb8b76db8ef2ec936722b682af6a9488a3501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="power-bi-tutorial-for-azure-cosmos-db-visualize-data-using-hello-power-bi-connector"></a>Power BI Azure Cosmos DB 教學課程： 使用 hello Power BI 連接器的資料視覺化
[PowerBI.com](https://powerbi.microsoft.com/)是您可以在其中建立並與重要 tooyou 和貴組織的資料共用儀表板和報表的線上服務。  Power BI Desktop 是專用報表撰寫工具，可讓您從各種資料來源的 tooretrieve 資料、 合併和轉換 hello 資料、 建立功能強大的報表和視覺效果，然後發行 hello 報表 tooPower BI。  Hello 最新版本的 Power BI Desktop，您現在可以透過 hello Cosmos DB 連接器 tooyour Cosmos DB 帳戶連接 Power bi。   

在此 Power BI 教學課程中，我們逐步解說 hello 步驟 tooconnect tooa Cosmos DB 帳戶在 Power BI Desktop 中，瀏覽我們想要使用 hello 導覽器中，將 JSON 資料轉換成表格式格式使用 Power BI Desktop 查詢 tooextract hello 資料 tooa 集合編輯器中，建立和發行報表 tooPowerBI.com 和。

完成本教學課程中 Power BI 之後，您會無法 tooanswer hello 下列問題：  

* 如何使用 Power BI Desktop 以 Cosmos DB 中的資料建置報告？
* 如何在 Power BI Desktop tooa Cosmos DB 帳戶連接？
* 如何在 Power BI Desktop 中從集合擷取資料？
* 如何在 Power BI Desktop 中轉換巢狀 JSON 資料？
* 如何在 PowerBI.com 中發佈及共用我的報告？

> [!NOTE]
> Azure Cosmos DB 的 hello Power BI 連接器連接 tooPower BI Desktop 擷取和轉換的資料。 Power BI Desktop 中建立的報表然後可以是已發行的 tooPowerBI.com。您無法在 PowerBI.com 中直接擷取和轉換 Azure Cosmos DB 資料。 

## <a name="prerequisites"></a>必要條件
之前遵循此教學課程中 Power BI 中的 hello 指示，請確定您有存取 toohello 下列資源：

* [hello 最新版本的 Power BI Desktop](https://powerbi.microsoft.com/desktop)。
* 存取 tooour 示範帳戶或 Cosmos DB 帳戶中的資料。
  * 本教學課程中所顯示的 hello 火山資料擴展 hello 示範帳戶。 此示範帳戶未受限於任何 SLA，而是僅供示範之用。  保留： hello 右 toomake 修改 toothis 示範帳戶包括但不是限於、 終止 hello 變更 hello 索引鍵，限制存取，變更帳戶，並刪除 hello 資料，在任何時間，而不需要事先通知或原因。
    * URL：https://analytics.documents.azure.com
    * 唯讀金鑰：MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==
  * 或者，toocreate 您自己的帳戶，請參閱[建立使用 hello Azure 入口網站的 Azure Cosmos DB 資料庫帳戶](https://azure.microsoft.com/documentation/articles/create-account/)。 然後，會類似 toowhat tooget 範例火山資料在本教學課程中使用 （但不包含 hello GeoJSON 區塊），請參閱 hello [NOAA 網站](https://www.ngdc.noaa.gov/nndc/struts/form?t=102557&s=5&d=5)然後匯入使用 hello hello 資料[Azure Cosmos DB 的資料移轉工具](import-data.md)。

tooshare 您的報表在 PowerBI.com 中您必須在 PowerBI.com 中擁有帳戶。 深入了解 Power BI 免費和 Power BI Pro，toolearn 造訪[https://powerbi.microsoft.com/pricing](https://powerbi.microsoft.com/pricing)。

## <a name="lets-get-started"></a>現在就開始吧
在本教學課程中，我們假設您是 geologist，研究火山 hello 世界各地。  hello 火山資料會儲存在 Cosmos DB 帳戶且 hello JSON 文件看起來 hello 遵循範例文件。

    {
        "Volcano Name": "Rainier",
           "Country": "United States",
          "Region": "US-Washington",
          "Location": {
            "type": "Point",
            "coordinates": [
              -121.758,
              46.87
            ]
          },
          "Elevation": 4392,
          "Type": "Stratovolcano",
          "Status": "Dendrochronology",
          "Last Known Eruption": "Last known eruption from 1800-1899, inclusive"
    }

希望從 Cosmos DB hello tooretrieve hello 火山資料帳戶，並將類似下列報表 hello 互動式 Power BI 報表中的資料視覺化。

![完成本 hello Power BI 連接器使用的 Power BI 教學課程，您將會以 hello Power BI Desktop 火山報表無法 toovisualize 資料](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

準備好 toogive 為再試一次嗎？ 現在就開始吧。

1. 在您的工作站上執行 Power BI Desktop。
2. Power BI Desktop 啟動時，會顯示 [歡迎使用]  畫面。
   
    ![Power BI Desktop 歡迎使用畫面 - Power BI 連接器](./media/powerbi-visualize/power_bi_connector_welcome.png)
3. 您可以**取得資料**，請參閱**最近使用的來源**，或**開啟其他報表**直接從 hello * 褖畫惎*螢幕。  按一下 hello X 在 hello 右上角 tooclose 囉 」 畫面。 hello**報表**Power BI Desktop 的檢視會顯示。
   
    ![Power BI Desktop 報告檢視 - Power BI 連接器](./media/powerbi-visualize/power_bi_connector_pbireportview.png)
4. 選取 hello**首頁**功能區，然後按一下 **取得資料**。  hello**取得資料**視窗應該會出現。
5. 按一下 Azure、選取 Microsoft Azure DocumentDB (Beta)，然後按一下連接。 

    ![Power BI Desktop 取得資料 - Power BI 連接器](./media/powerbi-visualize/power_bi_connector_pbigetdata.png)   
6. 在 hello**預覽連接器**頁面上，按一下**繼續**。 hello **Microsoft Azure DocumentDB Connect**  視窗隨即出現。
7. 指定 hello Cosmos DB 帳戶端點的 URL，從 tooretrieve hello 資料如下所示，然後再按一下**確定**。 toouse 您自己的帳戶，您可以擷取來自 hello URI URL 方塊中 hello hello **[金鑰](manage-account.md#keys)** hello Azure 入口網站的刀鋒視窗。 toouse hello 示範帳戶中，輸入`https://analytics.documents.azure.com`hello url。 
   
    項目留 hello 資料庫名稱、 集合名稱和 SQL 陳述式時這些欄位為選擇性。  相反地，我們將使用 hello 導覽 tooselect hello 資料庫與集合 tooidentify hello 資料來自何處。
   
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 桌面連接視窗](./media/powerbi-visualize/power_bi_connector_pbiconnectwindow.png)
8. 如果您第一次連接 hello toothis 端點，系統會提示您 hello 帳戶金鑰。 為您自己的帳戶擷取 hello 金鑰 hello**主索引鍵**方塊中 hello **[唯讀金鑰](manage-account.md#keys)** hello Azure 入口網站的刀鋒視窗。 Hello 示範帳戶，hello 金鑰是`MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==`。 輸入 hello 適當的索引鍵，然後按一下**連接**。
   
    我們建議您在建立報表時使用 hello 唯讀金鑰。  如此可防止不必要的曝光的 hello 主要金鑰 toopotential 安全性風險。 hello 唯讀索引鍵是可從 hello[金鑰](manage-account.md#keys)刀鋒視窗中的 hello Azure 入口網站，或者您可以使用以上所提供的 hello 示範帳戶資訊。
   
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 帳戶金鑰](./media/powerbi-visualize/power_bi_connector_pbidocumentdbkey.png)
    
    > [!NOTE] 
    > 如果您收到錯誤指出 「 hello 指定的資料庫已找不到。 」 在這個步驟 hello 因應措施請參閱[Power BI 問題](https://community.powerbi.com/t5/Issues/Document-DB-Power-BI/idi-p/208200)。
    
9. 當 hello 帳戶順利連線時，hello**導覽**會出現。  hello**導覽**會顯示 hello 帳戶下的資料庫清單。
10. 按一下以展開其中 hello 資料 hello 報表，將來自，如果您使用 hello 示範帳戶，請選取 hello 資料庫上**volcanodb**。   
11. 現在，選取您將 hello 從中擷取資料的集合。 如果您使用 hello 示範帳戶，請選取**volcano1**。
    
    hello 預覽 窗格會顯示一份**記錄**項目。  一份文件會顯示為 Power BI 中的 [記錄]  類型。 同樣地，文件內的巢狀 JSON 區塊也是 [記錄] 。
    
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 瀏覽器視窗](./media/powerbi-visualize/power_bi_connector_pbinavigator.png)
12. 按一下**編輯**toolaunch hello 查詢編輯器中新的視窗 tootransform hello 資料。

## <a name="flattening-and-transforming-json-documents"></a>簡維化和轉換 JSON 文件
1. 切換 toohello Power BI 查詢編輯器 視窗，其中 hello**文件**hello 中間窗格內的資料行。
   ![Power BI Desktop 查詢編輯器](./media/powerbi-visualize/power_bi_connector_pbiqueryeditor.png)
2. 按一下 在 hello hello 右邊 hello expander**文件**資料行標頭。  hello 與欄位清單的內容功能表隨即出現。  選取您報表所需的例如 hello 欄位、 火山名稱、 國家/地區、 區域、 位置、 提高權限、 類型、 狀態和上次知道 Eruption，然後按一下**確定**。
   
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 展開文件](./media/powerbi-visualize/power_bi_connector_pbiqueryeditorexpander.png)
3. hello 中央窗格會顯示 hello 結果的預覽與選取的 hello 欄位。
   
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 壓平合併結果](./media/powerbi-visualize/power_bi_connector_pbiresultflatten.png)
4. 在本例中，hello Location 屬性是 GeoJSON 區塊文件中。  如您所見，[位置] 顯示為 Power BI Desktop 中的 [記錄]  類型。  
5. 按一下 hello expander 在 hello 位置資料行標頭 hello 右邊。  hello 的型別與座標欄位的內容功能表隨即出現。  讓我們選取 hello 座標欄位並按一下**確定**。
   
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 位置記錄](./media/powerbi-visualize/power_bi_connector_pbilocationrecord.png)
6. hello 中央窗格現在會顯示的資料行座標**清單**型別。  在 hello 開頭 hello 教學課程中所示，hello GeoJSON 資料在本教學課程是點型別的記錄 hello 座標陣列中的緯度與經度值。
   
    hello 座標 [0] 項目代表經度，而座標 [1] 表示緯度。
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 座標清單](./media/powerbi-visualize/power_bi_connector_pbiresultflattenlist.png)
7. tooflatten hello 座標的陣列，我們將建立**自訂資料行**呼叫 LatLong。  選取 hello**加入資料行**功能區，然後按一下 **新增自訂資料行**。  hello**新增自訂資料行**視窗應該會出現。
8. 提供 hello 新資料行，例如 LatLong 的名稱。
9. 接下來，指定 hello hello 新資料行的自訂公式。  範例中，我們將串連 hello 緯度與經度值以逗號分隔，如下所示使用下列公式的 hello: `Text.From([coordinates]{1})&","&Text.From([coordinates]{0})`。 按一下 [確定] 。
   
    如需資料分析運算式 (DAX) (包括 DAX 函數) 的詳細資訊，請瀏覽 [Power BI Desktop 中的 DAX 基礎](https://support.powerbi.com/knowledgebase/articles/554619-dax-basics-in-power-bi-desktop)。
   
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 新增自訂資料行](./media/powerbi-visualize/power_bi_connector_pbicustomlatlong.png)
10. 現在，hello 中央窗格會顯示 hello 新 LatLong 的資料行填入 hello 緯度和經度值以逗號分隔。
    
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 自訂 LatLong 資料行](./media/powerbi-visualize/power_bi_connector_pbicolumnlatlong.png)
    
    如果您收到錯誤 hello 新資料行中，確定 [查詢設定] 下的 hello 套用步驟符合下列圖的 hello:
    
    ![套用的步驟應該是來源、瀏覽、展開的文件、展開的 Document.Location、新增的自訂](./media/powerbi-visualize/power-bi-applied-steps.png)
    
    如果您的步驟不同，刪除 hello 額外的步驟，然後再試一次加入 hello 自訂資料行。 
11. 我們現在已經完成將簡維的 hello 資料成表格式格式。  您可以利用所有可用 hello tooshape 查詢編輯器中的 hello 功能，並轉換 Cosmos DB 中的資料。  如果您使用 hello 範例，hello 資料類型變更的提升權限太**整數**藉由變更 hello**資料型別**上 hello**首頁**功能區。
    
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 變更資料行類型](./media/powerbi-visualize/power_bi_connector_pbichangetype.png)
12. 按一下**關閉並套用**toosave hello 資料模型。
    
    ![Azure Cosmos DB Power BI 連接器的 Power BI 教學課程 - 關閉並套用](./media/powerbi-visualize/power_bi_connector_pbicloseapply.png)

<a id="build-the-reports"></a>
## <a name="build-hello-reports"></a>建立 hello 報表
Power BI Desktop 報表檢視是您可以啟動 toovisualize 資料建立報表的位置。  您可以建立報表的欄位拖放到 hello**報表**畫布。

![Power BI Desktop 報告檢視 - Power BI 連接器](./media/powerbi-visualize/power_bi_connector_pbireportview2.png)

在 hello 報表檢視中，您應該看到：

1. hello**欄位** 窗格中，這是您會看到的資料模型，您可以使用報表的欄位清單的位置。
2. hello**視覺效果**窗格。 一份報告可以包含一或多個視覺效果。  挑選適合您的需求，從 hello hello visual 類型**視覺效果**窗格。
3. hello**報表**畫布，這是您將在其中建立報表 hello 視覺效果。
4. hello**報表**頁面。 您可以在 Power BI Desktop 中心增多個報告頁面。

hello 下列範例示範建立簡單的互動式地圖檢視報表的 hello 基本步驟。

1. 範例中，我們將建立地圖檢視顯示每個火山 hello 位置。  在 hello**視覺效果** 窗格中，按一下 hello 上方螢幕擷取畫面中反白顯示 hello 地圖視覺效果類型。  您應該會看見 hello 地圖視覺效果類型繪製在 hello**報表**畫布。  hello**視覺效果**窗格也應該會顯示一組屬性相關 toohello 地圖視覺效果類型。
2. 現在，從拖放 hello LatLong 欄位 hello**欄位**窗格 toohello**位置**屬性**視覺效果**窗格。
3. 下一步，拖曳和卸除 hello 火山名稱欄位 toohello**圖例**屬性。  
4. 然後，拖曳和卸除 hello 提高權限欄位 toohello**大小**屬性。  
5. 您現在應該會看到 hello 視覺顯示一組指出 hello 位置的每個火山 hello 相互關聯的 hello 火山 toohello 提高權限的 hello 泡泡大小的泡泡地圖。
6. 現在您已建立基本報告。  您可以加入更多視覺效果，進一步自訂 hello 報表。  在我們的案例中，我們加入了火山類型交叉分析篩選器 toomake hello 報表互動。  
   
    ![Hello 最終 Power BI Desktop 報表 for Azure Cosmos DB hello Power BI 教學課程完成時的螢幕擷取畫面](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

## <a name="publish-and-share-your-report"></a>發佈和共用您的報告
tooshare 報表時，您必須在 PowerBI.com 中的帳戶。

1. 在 hello Power BI Desktop 中，按一下 hello**首頁**功能區。
2. 按一下 [發行] 。  PowerBI.com 帳戶，您將會是提示的 tooenter hello 使用者名稱和密碼。
3. Hello 認證經過驗證之後，一旦 hello 報表就會是您所選取的已發行的 tooyour 目的地。
4. 按一下**開啟 'PowerBITutorial.pbix' Power BI 中的**toosee 和共用您在 powerbi.com 內的報表。
   
    ![發行 tooPower BI 成功 ！ 在 Power BI 中開啟教學課程](./media/powerbi-visualize/power_bi_connector_open_in_powerbi.png)

## <a name="create-a-dashboard-in-powerbicom"></a>在 PowerBI.com 中建立儀表板
現在，您有一份報表可在 PowerBI.com 上共用。

當您發行報表從 Power BI Desktop tooPowerBI.com 時，它會產生**報表**和**資料集**PowerBI.com 租用戶中。 比方說，之後您將報表發行呼叫**PowerBITutorial** tooPowerBI.com，您會看到 PowerBITutorial 中這兩個 hello**報表**和**資料集**上一節PowerBI.com。

   ![新的報表和 PowerBI.com 中的資料集，hello 的螢幕擷取畫面](./media/powerbi-visualize/powerbi-reports-datasets.png)

toocreate 可共用的儀表板，按一下 hello**釘選即時頁面**PowerBI.com 報表上的按鈕。

   ![新的報表和 PowerBI.com 中的資料集，hello 的螢幕擷取畫面](./media/powerbi-visualize/power-bi-pin-live-tile.png)

然後依照中的 hello 指示[從報表將磚釘選](https://powerbi.microsoft.com/documentation/powerbi-service-pin-a-tile-to-a-dashboard-from-a-report/#pin-a-tile-from-a-report)toocreate 新儀表板。 

您也可以建立儀表板之前進行臨機操作修改 tooreport。 不過，建議您使用 Power BI Desktop tooperform hello 修改並重新發行 hello 報表 tooPowerBI.com。

## <a name="refresh-data-in-powerbicom"></a>重新整理 PowerBI.com 中的資料
有兩種方式 toorefresh 資料，隨選和排程。

針對臨機操作的重新整理，只要按一下 hello eclipses （...） 的 hello**資料集**，例如 PowerBITutorial。 您應該會看到包括 [立即重新整理] 在內的動作清單。 按一下**立即重新整理**toorefresh hello 資料。

![PowerBI.com 中立即重新整理的螢幕擷取畫面](./media/powerbi-visualize/power-bi-refresh-now.png)

排定的重新整理，請勿 hello 遵循。

1. 按一下**排程重新整理**hello 動作清單中。 

    ![排程重新整理在 PowerBI.com 中的 hello 的螢幕擷取畫面](./media/powerbi-visualize/power-bi-schedule-refresh.png)
2. 在 hello**設定**頁面上，展開**資料來源認證**。 
3. 按一下 [編輯認證] 。 
   
    hello 設定快顯視窗出現。 
4. 輸入 hello 金鑰 tooconnect toohello Cosmos DB 帳戶，該資料集，然後按一下 **登入**。 
5. 展開**排程重新整理**和您設定 hello 排程要 toorefresh hello 資料集。 
6. 按一下**套用**和您在設定 hello 排定的重新整理。

## <a name="next-steps"></a>後續步驟
* toolearn 深入了解 Power BI 中，請參閱[開始使用 Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/)。
* 深入了解 Cosmos DB toolearn 看到 hello [Azure Cosmos DB 文件登陸頁面](https://azure.microsoft.com/documentation/services/documentdb/)。


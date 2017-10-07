---
title: "aaaMonitor Azure Cosmos DB 要求和儲存體 |Microsoft 文件"
description: "了解如何 toomonitor Azure Cosmos DB 說明效能度量，例如要求和伺服器錯誤以及使用量度量，例如存放裝置耗用量。"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 4c6a2e6f-6e78-48e3-8dc6-f4498b235a9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: mimig
ms.openlocfilehash: aea029d10717236a573a080dab9d06d87f97f318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-cosmos-db-requests-usage-and-storage"></a>監視 Azure Cosmos DB 要求、使用量及儲存體
您可以監視您 Azure Cosmos DB 中的帳戶 hello [Azure 入口網站](https://portal.azure.com/)。 每一個 Azure Cosmos DB 帳戶都有效能計量 (例如要求和伺服器錯誤) 和使用量計量 (例如儲存體耗用量) 可供使用。

Hello 帳戶 刀鋒視窗，hello 新度量刀鋒視窗中，或在 Azure 監視器，可以檢閱度量。

## <a name="view-performance-metrics-on-hello-metrics-blade"></a>Hello 計量刀鋒視窗上檢視效能度量
1. 在 hello [Azure 入口網站](https://portal.azure.com/)，按一下 **更服務**，太捲動**資料庫**，按一下**Azure Cosmos DB**，然後按一下hello hello 名稱Azure 的 Cosmos DB 帳戶，您想要 tooview 效能度量。
2. 在 hello 資源功能表中，在**監視**，按一下 **度量**。

hello 計量刀鋒視窗隨即開啟，以及您可以選取 hello 集合 tooreview。 您可以檢閱可用性、 要求、 輸送量和儲存體度量，並比較 toohello Azure Cosmos DB Sla。

## <a name="view-performance-metrics-by-using-azure-monitoring"></a>使用 Azure 監視器檢視效能度量
1. 在 hello [Azure 入口網站](https://portal.azure.com/)，按一下 **監視器**hello Jumpbar 上。
2. 在 hello 資源功能表上，按一下 **度量**。
3. 在 hello**監視-度量**視窗中的，於 hello**資源群組**下拉式功能表，選取 hello 與您想要 toomonitor hello Azure Cosmos DB 帳戶相關聯的資源群組。 
4. 在 hello**資源**下拉式功能表、 選取 hello 資料庫帳戶 toomonitor。
5. 中的 hello 清單**可用的度量**，選取 hello 度量 toodisplay。 使用 hello CTRL 按鈕 toomulti select。 

    您的度量會顯示在 hello 中**繪製**視窗。 

## <a name="view-performance-metrics-on-hello-account-blade"></a>檢視效能度量 hello 帳戶 刀鋒視窗
1. 在 hello [Azure 入口網站](https://portal.azure.com/)，按一下 **更服務**，太捲動**資料庫**，按一下**Azure Cosmos DB**，然後按一下hello hello 名稱Azure 的 Cosmos DB 帳戶，您想要 tooview 效能度量。
2. hello**監視**透鏡會顯示下列預設圖格的 hello:
   
   * Hello 當天的要求總數。
   * 已使用儲存體。
   
   如果您的資料表會顯示**沒有可用的資料**和您認為您的資料庫中沒有資料，請參閱 hello[疑難排解](#troubleshooting)> 一節。
   
   ![會顯示 hello 要求以及 hello 存放裝置使用量 hello 監視功能濾鏡的螢幕擷取畫面](./media/monitor-accounts/documentdb-total-requests-and-usage.png)
3. 按一下 hello**要求**或**使用量配額**磚會開啟詳細**度量**刀鋒視窗。
4. hello**度量**刀鋒視窗會顯示有關您已選取的 hello 度量的詳細資料。  Hello hello 刀鋒視窗的頂端是要求的圖形繪製每小時、 並在下方會顯示要求已節流和總計的彙總值的資料表。  hello 計量刀鋒伺服器也會顯示 hello 清單已定義的篩選 toohello 度量 hello 目前計量刀鋒伺服器上所顯示的警示 （如此一來，如果您有許多的警示，您只看到 hello 這裡所呈現的相關項目）。   
   
   ![其中包括的 hello 計量刀鋒伺服器的螢幕擷取畫面節流處理要求](./media/monitor-accounts/documentdb-metric-blade.png)

## <a name="customize-performance-metric-views-in-hello-portal"></a>自訂 hello 入口網站中的效能計量檢視
1. toocustomize hello 度量顯示在特定圖中，按一下 hello 圖表 tooopen 在 hello**度量**刀鋒視窗中，然後再按一下**編輯圖表**。  
   ![使用反白顯示的編輯圖表的 hello 計量刀鋒伺服器控制項的螢幕擷取畫面](./media/monitor-accounts/madocdb3.png)
2. 在 hello**編輯圖表**刀鋒視窗中，有顯示 hello 圖表，以及其時間範圍中的選項 toomodify hello 度量。  
   ![Hello 編輯圖表 刀鋒視窗的螢幕擷取畫面](./media/monitor-accounts/madocdb4.png)
3. toochange hello 度量顯示在 hello 部分中，只需選取或清除 hello 可用的效能度量，，然後按一下**確定**在 hello hello 刀鋒視窗的底部。  
4. toochange hello 時間範圍中，選擇不同的範圍 (例如，**自訂**)，然後按一下 **[確定]**在 hello hello 刀鋒視窗的底部。  
   
   ![Hello 的時間範圍內屬於 hello 編輯圖表刀鋒視窗中顯示的螢幕擷取畫面如何 tooenter 自訂時間範圍內](./media/monitor-accounts/madocdb5.png)

## <a name="create-side-by-side-charts-in-hello-portal"></a>Hello 入口網站中建立的並排圖表
hello Azure 入口網站可讓您 toocreate 來並行度量圖表。  

1. 首先，以滑鼠右鍵按一下 hello 圖表 toocopy 再選取**自訂**。
   
   ![Hello 與 hello 反白顯示的自訂選項的要求總數圖表的螢幕擷取畫面](./media/monitor-accounts/madocdb6.png)
2. 按一下**複製**在 hello 功能表 toocopy hello 組件，然後按一下**完成自訂**。
   
   ![螢幕擷取畫面的 hello 與 hello 複製的要求總數圖表和完成反白顯示的自訂選項](./media/monitor-accounts/madocdb7.png)  

您現在可能會將此組件視為度量的一部分，自訂顯示 hello 組件中的 hello 度量和時間範圍。  如此一來，您可以看到兩個不同度量圖表-並存 hello 在相同的時間。  
    ![Hello 要求總數圖表的螢幕擷取畫面和 hello 過去小時圖表新要求的總數](./media/monitor-accounts/madocdb8.png)  

## <a name="set-up-alerts-in-hello-portal"></a>設定在 hello 入口網站中的警示
1. 在 hello [Azure 入口網站](https://portal.azure.com/)，按一下**更服務**，按一下**Azure Cosmos DB**，然後按一下您想其 toosetup hello Azure Cosmos DB 帳戶 hello 名稱效能度量的警示。
2. 在 hello 資源功能表上，按一下 **警示規則**tooopen hello 警示規則 刀鋒視窗。  
   ![選取部分的螢幕擷取畫面的 hello 警示規則](./media/monitor-accounts/madocdb10.5.png)
3. 在 hello**警示規則**刀鋒視窗中，按一下 **新增警示**。  
   ![Hello 警示規則刀鋒視窗中，強調顯示 hello 新增警示 按鈕的螢幕擷取畫面](./media/monitor-accounts/madocdb11.png)
4. 在 hello**加入警示規則**刀鋒視窗中，指定：
   
   * hello hello 您要設定的警示規則名稱。
   * Hello 新的警示規則的描述。
   * hello hello 警示規則的計量。
   * hello 條件、 臨界值，而且期間判斷 hello 警示就會啟動。 例如，伺服器錯誤 hello 過去 15 分鐘內透過計數大於 5。
   * 是否 hello 服務管理員和 coadministrators 會以電子郵件傳送嗨警示觸發時。
   * 警示通知的其他電子郵件地址。  
     ![Hello 新增警示規則刀鋒視窗的螢幕擷取畫面](./media/monitor-accounts/madocdb12.png)

## <a name="monitor-azure-cosmos-db-programatically"></a>以程式設計方式監視 Azure Cosmos DB
hello 帳戶 hello 入口網站中提供的層級度量，例如儲存體帳戶使用量和總計的要求，可透過 hello DocumentDB Api。 不過，您可以使用 hello DocumentDB Api 擷取 hello 集合層級的使用量資料。 tooretrieve 集合層級資料，請勿 hello 遵循：

* toouse hello REST API [hello 集合上執行 GET](https://msdn.microsoft.com/library/mt489073.aspx)。 hello 集合的 hello 配額和使用量資訊會以 hello 回應 hello x ms-資源配額和 x ms-資源使用量標頭中傳回。
* toouse hello.NET SDK 使用 hello [DocumentClient.ReadDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.readdocumentcollectionasync.aspx)方法，這個方法會傳回[ResourceResponse](https://msdn.microsoft.com/library/dn799209.aspx)所包含的數字的使用方式屬性，例如**CollectionSizeUsage**， **DatabaseUsage**， **DocumentUsage**，以及其他更多。

tooaccess 其他度量，使用 hello [Azure 監視 SDK](https://www.nuget.org/packages/Microsoft.Azure.Insights)。 您可以呼叫下列程式碼來擷取可用的度量定義：

    https://management.azure.com/subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metricDefinitions?api-version=2015-04-08

遵循格式查詢 tooretrieve 個別度量使用 hello:

    https://management.azure.com/subscriptions/{SubecriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metrics?api-version=2015-04-08&$filter=%28name.value%20eq%20%27Total%20Requests%27%29%20and%20timeGrain%20eq%20duration%27PT5M%27%20and%20startTime%20eq%202016-06-03T03%3A26%3A00.0000000Z%20and%20endTime%20eq%202016-06-10T03%3A26%3A00.0000000Z

如需詳細資訊，請參閱[透過 hello Azure 監視 REST API 擷取資源度量](https://blogs.msdn.microsoft.com/cloud_solution_architect/2016/02/23/retrieving-resource-metrics-via-the-azure-insights-api/)。 請注意，"Azure Inights" 已重新命名為「Azure 監視器」。  此部落格文章參考 toohello 舊名稱。

## <a name="troubleshooting"></a>疑難排解
如果您的監視並排顯示 hello**沒有可用的資料**訊息，以及您最近提出要求，或加入資料 toohello 資料庫，您可以編輯 hello 磚 tooreflect hello 最近的使用量。

### <a name="edit-a-tile-toorefresh-current-data"></a>編輯磚 toorefresh 目前資料
1. toocustomize hello 度量顯示在特定部分中，按一下 hello 圖表 tooopen hello**度量**刀鋒視窗中，然後再按一下**編輯圖表**。  
   ![使用反白顯示的編輯圖表的 hello 計量刀鋒伺服器控制項的螢幕擷取畫面](./media/monitor-accounts/madocdb3.png)
2. Hello 上**編輯圖表**刀鋒視窗中的，在 hello**時間範圍**區段中，按一下**過去一小時**，然後按一下**確定**。  
   ![Hello 與過去一小時，選取 [編輯圖表] 刀鋒視窗的螢幕擷取畫面](./media/monitor-accounts/documentdb-no-available-data-past-hour.png)
3. 您的圖格現在應該會重新整理，以顯示您目前的資料和使用量。  
   ![Hello 更新的螢幕擷取畫面過去小時磚的要求總數](./media/monitor-accounts/documentdb-no-available-data-fixed.png)

## <a name="next-steps"></a>後續步驟
toolearn 進一步了解 Azure Cosmos DB 容量計劃，請參閱 hello [Azure Cosmos DB 容量規劃計算機](https://www.documentdb.com/capacityplanner)。


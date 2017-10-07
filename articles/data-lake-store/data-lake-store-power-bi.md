---
title: "資料湖存放區中使用 Power BI 的 aaaAnalyze 資料 |Microsoft 文件"
description: "使用 Power BI tooanalyze 資料儲存在 Azure 資料湖存放區"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57d19d27-e135-49d9-a7ea-46c48ef4e3bd
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 6a1bfa80fd1b0dda59b7eaaae9ca1585ba42783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-in-data-lake-store-by-using-power-bi"></a>使用 Power BI 分析 Data Lake Store 中的資料
在本文中，您將學習如何 toouse Power BI Desktop tooanalyze 及視覺化儲存在 Azure 資料湖存放區中的資料。

## <a name="prerequisites"></a>必要條件
開始本教學課程之前，您必須擁有 hello 下列：

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure Data Lake Store 帳戶**。 請遵循指示 hello[開始使用 Azure 資料湖存放區使用 hello Azure 入口網站](data-lake-store-get-started-portal.md)。 本文假設您已經建立名為的 Data Lake Store 帳戶**mybidatalakestore**，並上傳範例資料檔 (**Drivers.txt**) tooit。 此範例檔案可從 [Azure Data Lake Git 儲存機制](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt)進行下載。
* **Power BI Desktop**。 您可以從 [Microsoft 下載中心](https://www.microsoft.com/en-us/download/details.aspx?id=45331)下載此項目。 

## <a name="create-a-report-in-power-bi-desktop"></a>在 Power BI Desktop 中建立報表
1. 在您的電腦上啟動 Power BI Desktop。
2. 從 hello**首頁**功能區中，按一下 **取得資料**，然後按一下更多。 在 hello**取得資料**對話方塊中，按一下  **Azure**，按一下**Azure Data Lake Store**，然後按一下**連接**。
   
    ![連接 tooData Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account.png "連接 tooData 湖存放區")
3. 如果您看到有關 hello 連接器處於開發階段的對話方塊，選擇 toocontinue。
4. 在 hello **Microsoft Azure Data Lake Store**對話方塊中，提供 hello URL tooyour Data Lake Store 帳戶，然後再按一下**確定**。
   
    ![Data Lake Store 的 URL](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "Data Lake Store 的 URL")
5. 在 hello 下一步 對話方塊中，按一下 **登入**toosign 到 Data Lake Store 帳戶。 您將會重新導向 tooyour 組織的登入頁面。 遵循 hello 提示 toosign hello 考量。
   
    ![登入 Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "登入 Data Lake Store")
6. 順利登入之後，請按一下 [連線] 。
   
    ![連接 tooData Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "連接 tooData 湖存放區")
7. hello 下一步 對話方塊會顯示 hello 檔案上傳 tooyour Data Lake Store 帳戶。 確認 hello 資訊，然後按一下**負載**。
   
    ![從 Data Lake Store 載入資料](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "從 Data Lake Store 載入資料")
8. Hello 資料已成功載入 Power BI 之後，您會看到下列 hello 中的欄位的 hello**欄位** 索引標籤。
   
    ![匯入的欄位](./media/data-lake-store-power-bi/imported-fields.png "匯入的欄位")
   
    不過，toovisualize 和分析 hello 資料，我們喜歡 hello 資料 toobe hello 下列欄位可用
   
    ![所需的欄位](./media/data-lake-store-power-bi/desired-fields.png "所需的欄位")
   
    在 hello 下一個步驟中，我們將會更新 hello 查詢 tooconvert hello 所要的格式中的 hello 匯入資料。
9. 從 hello**首頁**功能區中，按一下 **編輯查詢**。
   
    ![編輯查詢](./media/data-lake-store-power-bi/edit-queries.png "編輯查詢")
10. 在 hello 查詢編輯器中，在 hello**內容**資料行中，按一下 **二進位**。
    
    ![編輯查詢](./media/data-lake-store-power-bi/convert-query1.png "編輯查詢")
11. 您會看到檔案圖示，表示 hello **Drivers.txt**您上傳的檔案。 Hello 檔案上按一下滑鼠右鍵，然後按一下**CSV**。    
    
    ![編輯查詢](./media/data-lake-store-power-bi/convert-query2.png "編輯查詢")
12. 您應該會看到如下的輸出。 現在您可以使用 toocreate 視覺效果格式提供您的資料。
    
    ![編輯查詢](./media/data-lake-store-power-bi/convert-query3.png "編輯查詢")
13. 從 hello**首頁**功能區中，按一下 **關閉並套用**，然後按一下**關閉並套用**。
    
    ![編輯查詢](./media/data-lake-store-power-bi/load-edited-query.png "編輯查詢")
14. 一旦更新 hello 查詢時，hello**欄位**索引標籤會顯示 hello 可用視覺效果的新欄位。
    
    ![更新的欄位](./media/data-lake-store-power-bi/updated-query-fields.png "更新的欄位")
15. 讓我們建立圓形圖 toorepresent hello 驅動程式在給定的國家/地區的每個城市。 toodo，進行下列選取項目 hello。
    
    1. Hello 視覺效果 索引標籤中，按一下圓形圖的 hello 符號。
       
        ![建立圓形圖](./media/data-lake-store-power-bi/create-pie-chart.png "建立圓形圖")
    2. hello 資料行，我們會 toouse**資料行 4** （hello 縣 （市） 的名稱） 和**資料行 7** （hello 國家/地區的名稱）。 拖曳資料行，從**欄位**索引標籤太**視覺效果**索引標籤上，如下所示。
       
        ![建立視覺效果](./media/data-lake-store-power-bi/create-visualizations.png "建立視覺效果")
    3. hello 圓形圖現在應該類似如下所示的其中一個 hello 類似。
       
        ![圓形圖](./media/data-lake-store-power-bi/pie-chart.png "建立視覺效果")
16. 藉由從 hello 頁面層級篩選中選取特定國家/地區，您現在可以看到 hello hello 選取國家/地區的每個城市中的驅動程式數目。 例如，在 hello**視覺效果**索引標籤，下方**頁面層級篩選**，選取**巴西**。
    
    ![選取國家/地區](./media/data-lake-store-power-bi/select-country.png "選取國家/地區")
17. hello 圓形圖是巴西的 hello 城市中的自動更新的 toodisplay hello 驅動程式。
    
    ![國家/地區中的驅動程式](./media/data-lake-store-power-bi/driver-per-country.png "每個國家的驅動程式")
18. 從 hello**檔案**功能表上，按一下 **儲存**toosave hello 視覺效果，與 Power BI Desktop 檔案。

## <a name="publish-report-toopower-bi-service"></a>發行報表 tooPower BI 服務
Power BI Desktop 中建立 hello 視覺效果之後，您可以與其他人共用發佈 toohello Power BI 服務。 如需指示，請參閱 toodo[從 Power BI Desktop 發佈](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/)。

## <a name="see-also"></a>另請參閱
* [使用 Data Lake Analytics 分析 Data Lake Store 中的資料](../data-lake-analytics/data-lake-analytics-get-started-portal.md)


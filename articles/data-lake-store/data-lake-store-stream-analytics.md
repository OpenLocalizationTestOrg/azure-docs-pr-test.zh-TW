---
title: "資料湖存放區的資料流分析 aaaStream 資料 |Microsoft 文件"
description: "使用 Azure Stream Analytics toostream 資料至 Azure 資料湖存放區"
services: data-lake-store,stream-analytics
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 68c727d4807db0abe6efa90145d68c78902eb789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a>使用 Azure 串流分析將來自 Azure 儲存體 Blob 的資料串流處理至 Data Lake Store
在本文中，您將學習如何 toouse Azure 資料湖存放區做為 Azure 資料流分析工作的輸出。 本文將示範一個簡單的案例，可從 Azure 儲存體 blob （輸入） 讀取資料並寫入 hello data tooData Lake Store （輸出）。

> [!NOTE]
> 在這個階段中，建立及設定 Data Lake Store 的輸出資料流分析支援只能在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)。 因此，本教學課程中的某些部分會使用 hello Azure 傳統入口網站。
>
>

## <a name="prerequisites"></a>必要條件
開始本教學課程之前，您必須擁有 hello 下列：

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。

* **Azure 儲存體帳戶**。 您將使用此帳戶 tooinput 資料從 blob 容器的資料流分析工作。 此教學課程中，假設您有儲存體帳戶呼叫**storageforasa** hello 帳戶內的容器呼叫**storageforasacontainer**。 當您建立 hello 容器之後時上, 傳範例資料檔案 tooit。 
  
* **Azure Data Lake Store 帳戶**。 請遵循指示 hello[開始使用 Azure 資料湖存放區使用 hello Azure 入口網站](data-lake-store-get-started-portal.md)。 假設您有名為 **asadatalakestore** 的 Data Lake Store 帳戶。 

## <a name="create-a-stream-analytics-job"></a>建立串流分析作業
您可以從建立包含輸入來源和輸出目的地的串流分析作業開始。 本教學課程，hello 來源是 Azure blob 容器而且 hello 目的地資料湖存放區。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。

2. 從 hello 左窗格中，按一下 **串流分析工作**，然後按一下**新增**。

    ![建立串流分析作業](./media/data-lake-store-stream-analytics/create.job.png "建立串流分析作業")

    > [!NOTE]
    > 請確定您建立可在 hello 作業與 hello 儲存體帳戶，或相同的區域將會產生不同的區域之間移動資料的額外成本。
    >

## <a name="create-a-blob-input-for-hello-job"></a>建立 Blob 輸入 hello 工作

1. 開啟 hello 頁面 hello 資料流分析工作，從 hello 左窗格按一下 hello**輸入**索引標籤，然後再按一下**新增**。

    ![加入輸入的 tooyour 作業](./media/data-lake-store-stream-analytics/create.input.1.png "加入輸入的 tooyour 作業")

2. 在 hello**新輸入**刀鋒視窗中，提供下列值的 hello。

    ![加入輸入的 tooyour 作業](./media/data-lake-store-stream-analytics/create.input.2.png "加入輸入的 tooyour 作業")

    * 如**輸入別名**，輸入 hello 工作輸入唯一的名稱。
    * 在 [來源類型] 中，選取 [資料流]。
    * 在 [來源] 中，選取 [Blob 儲存體]。
    * 在 [訂用帳戶] 中，選取 [使用來自目前訂用帳戶的 Blob 儲存體]。
    * 如**儲存體帳戶**，選取您所建立的 hello 儲存體帳戶 hello 必要條件的一部分。 
    * 如**容器**，選取您在 hello hello 容器選取儲存體帳戶。
    * 在 [事件序列化格式] 中，選取 [CSV]。
    * 在 [分隔符號] 中，選取 [定位鍵]。
    * 在 [編碼] 中，選取 [UTF-8]。

    按一下 [建立] 。 hello 入口網站現在將 hello 輸入並測試 hello 連接 tooit。


## <a name="create-a-data-lake-store-output-for-hello-job"></a>建立 Data Lake Store hello 作業輸出

1. 開啟 hello 資料流分析工作的 hello 頁面中，按一下 hello**輸出**索引標籤，然後再按一下**新增**。

    ![加入輸出 tooyour 作業](./media/data-lake-store-stream-analytics/create.output.1.png "加入輸出 tooyour 作業")

2. 在 hello**新輸出**刀鋒視窗中，提供下列值的 hello。

    ![加入輸出 tooyour 作業](./media/data-lake-store-stream-analytics/create.output.2.png "加入輸出 tooyour 作業")

    * 如**輸出別名**，輸入 hello 作業輸出的唯一名稱。 這是用於查詢 toodirect hello 查詢輸出 toothis Data Lake Store 的易記名稱。
    * 在 [接收] 中，選取 [Data Lake Store]。
    * 您將會提示的 tooauthorize 存取 tooData Lake Store 帳戶。 按一下 [授權]。

3. 在 hello**新輸出**刀鋒視窗中，繼續 tooprovide hello 下列值。

    ![加入輸出 tooyour 作業](./media/data-lake-store-stream-analytics/create.output.3.png "加入輸出 tooyour 作業")

    * 如**帳戶名稱**，選取您已建立您想要傳送至 hello 作業輸出 toobe hello Data Lake Store 帳戶。
    * 如**路徑前置詞模式**，輸入檔案路徑使用 toowrite 內 hello 檔案指定 Data Lake Store 帳戶。
    * 如**日期格式**，如果您使用的日期語彙基元 hello 前置詞路徑中，您可以選取組織檔案的 hello 日期格式。
    * 如**時間格式**，如果您使用時間語彙基元 hello 前置詞的路徑中，指定組織檔案的 hello 時間格式。
    * 在 [事件序列化格式] 中，選取 [CSV]。
    * 在 [分隔符號] 中，選取 [定位鍵]。
    * 在 [編碼] 中，選取 [UTF-8]。
    
    按一下 [建立] 。 hello 入口網站現在將 hello 輸出，並測試 hello 連接 tooit。
    
## <a name="run-hello-stream-analytics-job"></a>執行 hello 資料流分析工作

1. toorun 資料流分析工作，您必須執行的查詢從 hello**查詢** 索引標籤。此教學課程中，您可以執行 hello 範例查詢來取代以 hello hello 預留位置工作輸入和輸出別名，hello 下列螢幕擷取畫面所示。

    ![執行查詢](./media/data-lake-store-stream-analytics/run.query.png "執行查詢")

2. 按一下**儲存**從 hello 囉 」 畫面頂端，然後從 hello**概觀**索引標籤上，按一下 **啟動**。 從 hello 對話方塊中，選取 **自訂時間**，然後設定 hello 目前日期和時間。

    ![設定作業時間](./media/data-lake-store-stream-analytics/run.query.2.png "設定作業時間")

    按一下**啟動**toostart hello 作業。 它可能會佔用 tooa 幾分鐘的時間 toostart hello 作業。

3. tootrigger hello toopick hello 的工作資料 hello blob 複製的範例資料檔案 toohello blob 容器。 您可以取得範例資料檔從 hello [Azure 資料湖 Git 儲存機制](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt)。 本教學課程，讓我們複製 hello 檔案**vehicle1_09142014.csv**。 您可以使用各種用戶端，例如[Azure 儲存體總管](http://storageexplorer.com/)，tooupload 資料 tooa blob 容器。

4. 從 hello**概觀**索引標籤，下方**監視**，請參閱 hello 資料處理的方式。

    ![監視作業](./media/data-lake-store-stream-analytics/run.query.3.png "監視作業")

5. 最後，您可以確認 hello 工作輸出資料均可在 hello Data Lake Store 帳戶。 

    ![確認輸出](./media/data-lake-store-stream-analytics/run.query.4.png "確認輸出")

    Hello 資料總管 窗格，請注意該 hello 輸出會寫入的 tooa 資料夾路徑，做為指定在 hello Data Lake Store 輸出設定 (`streamanalytics/job/output/{date}/{time}`)。  

## <a name="see-also"></a>另請參閱
* [建立 Data Lake Store 的 HDInsight 叢集 toouse](data-lake-store-hdinsight-hadoop-use-portal.md)

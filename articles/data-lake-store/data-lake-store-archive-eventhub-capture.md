---
title: "從事件中心至 Azure Data Lake Store aaaCapture 資料 |Microsoft 文件"
description: "使用 Azure Data Lake Store toocapture 資料，從事件中樞"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a>使用 Azure Data Lake Store toocapture 資料，從事件中樞

了解 Azure 事件中樞所收到 toouse Azure Data Lake Store toocapture 資料的方式。

## <a name="prerequisites"></a>必要條件

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。

* **Azure Data Lake Store 帳戶**。 如需有關指示 toocreate 一個，請參閱[開始使用 Azure Data Lake Store](data-lake-store-get-started-portal.md)。

*  **事件中樞命名空間**。 如需相關指示，請參閱[建立事件中樞命名空間](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace)。 請確定 hello Data Lake Store 帳戶和 hello 事件中樞命名空間位於 hello 相同的 Azure 訂用帳戶。


## <a name="assign-permissions-tooevent-hubs"></a>指派權限 tooEvent 集線器

在本節中，您可以建立 hello 帳戶內您要從事件中樞 toocapture hello 資料所在的資料夾。 您也指派權限 tooEvent 中心，讓它可以將資料寫入 Data Lake Store 帳戶。 

1. 開啟您想要從事件中樞 toocapture 資料，然後按一下其中 hello Data Lake Store 帳戶**資料總管**。

    ![Data Lake Store 資料總管](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store 資料總管")

2.  按一下**新資料夾**，然後輸入您要 toocapture hello 資料所在的資料夾的名稱。

    ![在 Data Lake Store 中建立新的資料夾](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "在 Data Lake Store 中建立新的資料夾")

3. 指派在 hello 根目錄的 hello 資料湖存放區的權限。 

    a. 按一下**資料總管**選取的 hello Data Lake Store 帳戶的 hello 根目錄，然後按一下**存取**。

    ![為 Data Lake Store 根目錄指派權限](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "為 Data Lake Store 根目錄指派權限")

    b. 在 [存取] 下，依序按一下 [新增] 和 [選取使用者或群組]，然後搜尋 `Microsoft.EventHubs`。 

    ![為 Data Lake Store 根目錄指派權限](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "為 Data Lake Store 根目錄指派權限")
    
    按一下 [選取] 。

    c. 在 [指派權限] 下，按一下 [選取權限]。 設定**權限**太**Execute**。 設定**加入**太**這個資料夾和所有子系**。 設定**加入做為**太**的存取權限項目和預設權限項目**。

    ![為 Data Lake Store 根目錄指派權限](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "為 Data Lake Store 根目錄指派權限")

    按一下 [確定] 。

4. 指派您要 toocapture 資料 Data Lake Store 帳戶的 hello 資料夾的權限。

    a. 按一下**資料總管**選取 hello Data Lake Store 帳戶中的 hello 資料夾，然後按**存取**。

    ![為 Data Lake Store 資料夾指派權限](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "為 Data Lake Store 資料夾指派權限")

    b. 在 [存取] 下，依序按一下 [新增] 和 [選取使用者或群組]，然後搜尋 `Microsoft.EventHubs`。 

    ![為 Data Lake Store 資料夾指派權限](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "為 Data Lake Store 資料夾指派權限")
    
    按一下 [選取] 。

    c. 在 [指派權限] 下，按一下 [選取權限]。 設定**權限**太**讀取、 寫入、**和**Execute**。 設定**加入**太**這個資料夾和所有子系**。 最後，設定**加入做為**太**的存取權限項目和預設權限項目**。

    ![為 Data Lake Store 資料夾指派權限](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "為 Data Lake Store 資料夾指派權限")
    
    按一下 [確定] 。 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a>設定事件中心 toocapture 資料 tooData 湖存放區

在本節中，您會在事件中樞命名空間內建立事件中樞。 您也可以設定 hello 事件中心 toocapture 資料 tooan Azure Data Lake Store 帳戶。 本節假設您已建立事件中樞命名空間。

2. 從 hello**概觀**窗格中的 hello 事件中樞命名空間中，按一下  **+ 事件中心**。

    ![建立事件中樞](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "建立事件中樞")

3. 提供的值 hello 如下 tooconfigure 事件中心 toocapture 資料 tooData 湖存放區。

    ![建立事件中樞](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "建立事件中樞")

    a. 提供 hello 事件中樞的名稱。
    
    b. 此教學課程中，設定**資料分割計數**和**訊息保留**toohello 預設值。
    
    c. 設定**擷取**太**上**。 設定 hello**時段**(頻率 toocapture) 和**視窗大小**(資料大小 toocapture)。 
    
    d. 如**擷取提供者**，選取**Azure Data Lake Store**和 hello 選取 hello 您稍早建立的資料湖存放區。 如**資料湖路徑**，輸入 hello hello hello Data Lake Store 帳戶中建立的資料夾名稱。 您只需要 tooprovide hello 相對路徑 toohello 資料夾。

    e. 保留 hello**範例擷取檔案名稱格式**toohello 預設值。 此選項可控制 hello 建立 hello 擷取資料夾下的資料夾結構。

    f. 按一下 [建立] 。

## <a name="test-hello-setup"></a>測試 hello 安裝程式

您現在可以傳送資料 toohello Azure 事件中心，以測試 hello 方案。 請遵循指示 hello[傳送事件 tooAzure 事件中心](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md)。 一旦您開始傳送嗨資料，您會看到 hello 資料反映資料湖存放區中，使用您指定的資料夾結構 hello 集。 比方說，您看到的資料夾結構，如下列螢幕擷取畫面，您的資料湖存放區中的 hello 中所示。

![Data Lake Store 中的事件中樞資料範例](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Data Lake Store 中的事件中樞資料範例")

> [!NOTE]
> 即使您沒有訊息傳送至事件中心，事件中心會寫入 hello Data Lake Store 帳戶只 hello 標頭的空檔案。 hello 檔案會寫入在 hello 相同建立 hello 事件中心時您所提供的時間間隔。
> 
>

## <a name="analyze-data-in-data-lake-store"></a>分析 Data Lake 存放區中的資料

資料湖存放區中 hello 資料之後，您可以執行分析作業 tooprocess 和無暇 hello 資料。 請參閱[USQL Avro 範例](https://github.com/Azure/usql/tree/master/Examples/AvroExamples)如何 toodo 此使用 Azure Data Lake Analytics。
  

## <a name="see-also"></a>另請參閱
* [保護 Data Lake Store 中的資料](data-lake-store-secure-data.md)
* [從 Azure 儲存體 Blob tooData 湖存放區複製資料](data-lake-store-copy-data-azure-storage-blob.md)

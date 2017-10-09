---
title: "aaaRegister 資料從 Azure 資料目錄中的資料湖存放區 |Microsoft 文件"
description: "在 Azure 資料目錄中註冊來自 Data Lake Store 的資料"
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3294d91e-a723-41b5-9eca-ace0ee408a4b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3e895b42cab4ba39d288950763312a243883cbdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-from-data-lake-store-in-azure-data-catalog"></a>在 Azure 資料目錄中註冊來自 Data Lake Store 的資料
在本文中，您將學習如何 toointegrate Azure 資料湖存放區與 Azure 資料目錄 toomake 您探索組織內的資料藉由整合以資料目錄。 如需編目資料的詳細資訊，請參閱 [Azure 資料目錄](../data-catalog/data-catalog-what-is-data-catalog.md)。 toounderstand 案例中，您可以使用資料目錄，請參閱[Azure 資料目錄的常見案例](../data-catalog/data-catalog-common-scenarios.md)。

## <a name="prerequisites"></a>必要條件
開始本教學課程之前，您必須擁有 hello 下列：

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **啟用您的 Azure 訂用帳戶** 以使用「Data Lake Store 公開預覽版」。 請參閱 [指示](data-lake-store-get-started-portal.md)。
* **Azure Data Lake Store 帳戶**。 請遵循指示 hello[開始使用 Azure 資料湖存放區使用 hello Azure 入口網站](data-lake-store-get-started-portal.md)。 在本教學課程中，讓我們建立名為 **datacatalogstore**的 Data Lake Store 帳戶。

    當您建立 hello 帳戶之後時上, 傳範例資料集 tooit。 本教學課程，讓我們上載 hello 底下的所有 hello.csv 檔案**AmbulanceData**資料夾中 hello [Azure 資料湖 Git 儲存機制](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/)。 您可以使用各種用戶端，例如[Azure 儲存體總管](http://storageexplorer.com/)，tooupload 資料 tooa blob 容器。
* **Azure 資料目錄**。 您的組織必須為組織建立 Azure 資料目錄。 每個組織只允許有一個目錄。

## <a name="register-data-lake-store-as-a-source-for-data-catalog"></a>註冊 Data Lake Store 做為資料目錄的來源

> [!VIDEO https://channel9.msdn.com/Series/AzureDataLake/ADCwithADL/player]

1. 跳過`https://azure.microsoft.com/services/data-catalog`，然後按一下**開始**。
2. 登入 hello Azure 資料目錄入口網站，並按一下**發行資料**。

    ![註冊資料來源](./media/data-lake-store-with-data-catalog/register-data-source.png "註冊資料來源")
3. 在 hello 下一個頁面上，按一下 **啟動應用程式**。 這會下載您的電腦上 hello 應用程式資訊清單檔案。 按兩下 hello 資訊清單檔案 toostart hello 應用程式。
4. 在 hello  褖畫惎 頁面上，按一下 **登入**，並輸入您的認證。

    ![歡迎使用畫面](./media/data-lake-store-with-data-catalog/welcome.screen.png "歡迎使用畫面")
5. 在 hello 選取資料來源 頁面上，選取  **Azure 資料湖**，然後按一下**下一步**。

    ![選取資料來源](./media/data-lake-store-with-data-catalog/select-source.png "選取資料來源")
6. 在 hello 下一個頁面上，提供 hello 想 tooregister 資料目錄中的 Data Lake Store 帳戶名稱。 保留 hello 做為預設值的其他選項，然後按**連接**。

    ![連接 toodata 來源](./media/data-lake-store-with-data-catalog/connect-to-source.png "連接 toodata 來源")
7. hello 下一頁可以分成下列區段的 hello。

    a. hello**伺服器階層**方塊都代表 hello Data Lake Store 帳戶的資料夾結構。 **$Root**代表 hello Data Lake Store 帳戶的根，和**AmbulanceData**代表 hello hello Data Lake Store 帳戶 hello 根目錄中建立資料夾。

    b. hello**可用物件**方塊會列出 hello 檔案和資料夾下 hello **AmbulanceData**資料夾。

    c. **物件 toobe 註冊方塊**清單 hello 您想 tooregister 在 Azure 資料目錄中的檔案和資料夾。

    ![檢視資料結構](./media/data-lake-store-with-data-catalog/view-data-structure.png "檢視資料結構")
8. 此教學課程中，您應該註冊所有 hello 檔案 hello 目錄中。 該作業，按一下 hello (![移動物件](./media/data-lake-store-with-data-catalog/move-objects.png "移動物件")) 所有 hello 按鈕 toomove 檔案太**註冊物件 toobe**方塊。

    因為 hello 資料將在整個組織的資料目錄中登錄，所以建議很接近 tooadd 一些可以在稍後使用的中繼資料 tooquickly 找出 hello 資料。 例如，您可以新增 hello 資料擁有者 （例如，一個人員會將 hello 資料上傳） 的電子郵件地址，或新增標記 tooidentify hello 資料。 hello 下列螢幕擷取畫面顯示標記，我們將新增 toohello 資料。

    ![檢視資料結構](./media/data-lake-store-with-data-catalog/view-selected-data-structure.png "檢視資料結構")

    按一下 [註冊] 。
9. hello 下列螢幕擷取畫面表示 hello 資料已經成功註冊 hello 資料目錄中。

    ![註冊完成](./media/data-lake-store-with-data-catalog/registration-complete.png "檢視資料結構")
10. 按一下**檢視入口網站**toogo 回 toohello 資料目錄入口網站，並確認，您現在可以存取 hello 註冊 hello 入口網站的資料。 toosearch hello 資料，您可以使用您註冊 hello 資料時所用的 hello 標記。

     ![搜尋目錄中的資料](./media/data-lake-store-with-data-catalog/search-data-in-catalog.png "搜尋目錄中的資料")
11. 您現在可以執行作業，像是新增註釋和文件 toohello 資料。 如需詳細資訊，請參閱下列連結查看 hello。

    * [註釋資料目錄中的資料來源](../data-catalog/data-catalog-how-to-annotate.md)
    * [記錄資料目錄中的資料來源](../data-catalog/data-catalog-how-to-documentation.md)

## <a name="see-also"></a>另請參閱
* [註釋資料目錄中的資料來源](../data-catalog/data-catalog-how-to-annotate.md)
* [記錄資料目錄中的資料來源](../data-catalog/data-catalog-how-to-documentation.md)
* [整合 Data Lake Store 與其他 Azure 服務](data-lake-store-integrate-with-other-services.md)

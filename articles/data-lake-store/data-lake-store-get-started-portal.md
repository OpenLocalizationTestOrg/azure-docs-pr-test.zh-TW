---
title: "使用 Azure 入口網站來開始使用 Data Lake Store | Microsoft Docs"
description: "使用 Azure 入口網站來建立 Data Lake Store 帳戶，並在 Data Lake Store 中執行基本作業"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: fea324d0-ad1a-4150-81f0-8682ddb4591c
ms.service: data-lake-store
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/09/2018
ms.author: nitinme
ms.openlocfilehash: 38a8792588e013a0105ea57b20b2560f0acf02e6
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/10/2018
---
# <a name="get-started-with-azure-data-lake-store-using-the-azure-portal"></a>使用 Azure 入口網站開始使用 Azure Data Lake Store
> [!div class="op_single_selector"]
> * [入口網站](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
>
> 

了解如何使用 Azure 入口網站建立 Azure Data Lake Store 帳戶並執行基本作業，例如建立資料夾、上傳和下載資料檔案、刪除您的帳戶等等。如需詳細資訊，請參閱 [Azure Data Lake Store 概觀](data-lake-store-overview.md)。

## <a name="prerequisites"></a>必要條件
開始進行本教學課程之前，您必須具備下列項目：

* **Azure 訂用帳戶**。 請參閱[取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="create-an-azure-data-lake-store-account"></a>建立 Azure Data Lake Store 帳戶

1. 登入新的 [Azure 入口網站](https://portal.azure.com)。
2. 按一下 [新增]，然後依序按一下 [資料 + 儲存體] 和 [Azure Data Lake Store]。 讀取 [Azure Data Lake Store] 刀鋒視窗中的資訊，然後按一下刀鋒視窗左上角的 [建立]。
3. 在 [新增 Data Lake Store] 刀鋒視窗中，提供如以下螢幕擷取畫面所示的值：
   
    ![建立新的 Azure Data Lake Store 帳戶](./media/data-lake-store-get-started-portal/ADL.Create.New.Account.png "建立新的 Azure Data Lake 帳戶")
   
   * **名稱**。 輸入 Data Lake Store 帳戶的唯一名稱。
   * **訂用帳戶**。 選取您想要建立新 Data Lake Store 帳戶所在的訂用帳戶。
   * **資源群組**。 選取現有的資源群組，或選取 [建立新的] 選項來建立一個。 資源群組是保留應用程式相關資源的容器。 如需詳細資訊，請參閱 [Azure 中的資源群組](../azure-resource-manager/resource-group-overview.md#resource-groups)。
   * **位置**：選取您要建立資料湖存放區帳戶的位置。
   * **加密設定**。 選項有三個：
     
     * **不啟用加密**。
     * **使用由 Auzre Data Lake 管理的金鑰**。  如果您要讓 Azure Data Lake Store 管理加密金鑰。
     * **使用來自您自己金鑰保存庫的金鑰**。 您可以選取現有的 Azure Key Vault，或建立新的 Key Vault。 若要使用 Key Vault 中的金鑰，您必須為 Azure Data Lake Store 帳戶指派用來存取 Azure Key Vault 的權限。 如需相關指示，請參閱[指派 Azure Key Vault 的權限](#assign-permissions-to-azure-key-vault)。
       
        ![Data Lake Store 加密](./media/data-lake-store-get-started-portal/adls-encryption-2.png "Data Lake Store 加密")
       
        按一下 [加密設定] 刀鋒視窗中的 [確定]。

        如需詳細資訊，請參閱[在 Azure Data Lake Store 中加密資料](./data-lake-store-encryption.md)。

4. 按一下頁面底部的 [新增] 。 如果您選擇將帳戶釘選到儀表板，您會回到儀表板，並且可以看到 Data Lake Store 帳戶的佈建進度。 一旦佈建 Data Lake Store 帳戶，帳戶刀鋒視窗就會出現。

### <a name="assign-permissions-to-azure-key-vault"></a>指派 Azure Key Vault 的權限
如果您使用 Azure 金鑰保存庫中的金鑰對 Data Lake Store 帳戶設定加密，您必須設定 Data Lake Store 帳戶和 Azure 金鑰保存庫帳戶之間的存取權。 請執行下列步驟來進行此作業。

1. 如果您使用 Azure 金鑰保存庫中的金鑰，Data Lake Store 帳戶的刀鋒視窗上方會顯示警告。 按一下警告以開啟 [加密]。
   
    ![Data Lake Store 加密](./media/data-lake-store-get-started-portal/adls-encryption-3.png "Data Lake Store 加密")
2. 刀鋒視窗中會顯示兩個用來設定存取權的選項。

    ![Data Lake Store 加密](./media/data-lake-store-get-started-portal/adls-encryption-4.png "Data Lake Store 加密")
   
   * 在第一個選項中，按一下 [授與權限] 以設定存取權。 只有當建立 Data Lake Store 帳戶的使用者也是 Azure 金鑰保存庫的系統管理員時，才會啟用第一個選項。
   * 另一個選項是執行刀鋒視窗上顯示的 PowerShell Cmdlet。 您必須是 Azure 金鑰保存庫的擁有者，或擁有對 Azure 金鑰保存庫授與權限的能力。 執行此 Cmdlet 之後，請返回刀鋒視窗，然後按一下 [啟用] 以設定存取權。

> [!NOTE]
> 您也可以使用 Azure Resource Manager 範本建立 Data Lake Store 帳戶。 您可從 [Azure 快速入門範本](https://azure.microsoft.com/resources/templates/?term=data+lake+store)存取這些範本︰
    - 未啟用資料加密：[部署 Azure Data Lake Store 帳戶 (未啟用資料加密)](https://azure.microsoft.com/resources/templates/101-data-lake-store-no-encryption/)。
    - 使用 Data Lake Store (已啟用資料加密)：[部署 Data Lake Store 帳戶 (已啟用加密) (Data Lake)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-adls/)。
    - 使用 Azure Key Vault (已啟用資料加密)：[部署 Data Lake Store 帳戶 (已啟用加密) (Key Vault)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-key-vault/)。
> 
> 



## <a name="createfolder"></a>在 Azure 資料湖存放區帳戶中建立資料夾
您可以在您的 Azure Data Lake Store 帳戶下建立資料夾，用於管理與存放資料。

1. 開啟您建立的 Data Lake Store 帳戶。 從左窗格按一下 [瀏覽]，按一下 [Data Lake Store]，然後從 [Data Lake Store] 刀鋒視窗中，按一下您要在其下建立資料夾的帳戶名稱。 如果您將帳戶釘選到開始面板，請按一下該帳戶磚。
2. 在您的 [Data Lake Store 帳戶] 刀鋒視窗中，按一下 [資料總管] 。
   
    ![在 Data Lake Store 帳戶中建立資料夾](./media/data-lake-store-get-started-portal/ADL.Create.Folder.png "在 Data Lake Store 帳戶中建立資料夾")
3. 在 [資料總管] 刀鋒視窗中，按一下 [新增資料夾]，輸入新資料夾的名稱，然後按一下 [確定]。
   
    ![在 Data Lake Store 帳戶中建立資料夾](./media/data-lake-store-get-started-portal/ADL.Folder.Name.png "在 Data Lake Store 帳戶中建立資料夾")
   
    新建立的資料夾會列在 [資料總管] 刀鋒視窗中。 您可以建立任何層級的巢狀資料夾。
   
    ![在 Data Lake 帳戶中建立資料夾](./media/data-lake-store-get-started-portal/ADL.New.Directory.png "在 Data Lake 帳戶中建立資料夾")

## <a name="uploaddata"></a>將資料上傳至 Azure Data Lake Store 帳戶
您可以直接在根層級將資料上傳至 Azure 資料湖存放區帳戶，或上傳至您在帳戶內建立的資料夾。 

1. 從 [資料總管] 刀鋒視窗中，按一下 [上傳]。 
2. 在 [上傳檔案] 刀鋒視窗中，導覽至您要上傳的檔案，然後按一下 [新增選取的檔案]。 您可以選取數個檔案加以上傳。

    ![上傳資料](./media/data-lake-store-get-started-portal/ADL.New.Upload.File.png "上傳資料")

如果您正在尋找一些可上傳的範例資料，您可以從 **Azure Data Lake Git 存放庫** 取得 [Ambulance Data](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)資料夾。

## <a name="properties"></a>儲存資料可用的動作
按一下檔案的省略符號圖示，在快顯功能表中，按一下您想要對資料執行的動作。

![資料屬性](./media/data-lake-store-get-started-portal/ADL.File.Properties.png "資料屬性") 

## <a name="secure-your-data"></a>保護您的資料
您可以在您的 Azure 資料湖存放區帳戶中使用 Azure Active Directory 和存取控制 (ACL) 保護儲存的資料。 如需如何執行此工作的指示，請參閱 [在 Azure 資料湖存放區中保護資料](data-lake-store-secure-data.md)。

## <a name="delete-azure-data-lake-store-account"></a>刪除 Azure 資料湖存放區帳戶
若要刪除 Azure 資料湖存放區帳戶，請從 [資料湖存放區] 刀鋒視窗按一下 [刪除] 。 為了確認此動作，將提示您輸入您要刪除的帳戶名稱。 輸入帳戶的名稱，然後按一下 [刪除] 。

![刪除 Data Lake 帳戶](./media/data-lake-store-get-started-portal/ADL.Delete.Account.png "刪除 Data Lake 帳戶")

## <a name="next-steps"></a>後續步驟
* [使用 Azure Data Lake Store 處理巨量資料需求](data-lake-store-data-scenarios.md) 
* [保護 Data Lake Store 中的資料](data-lake-store-secure-data.md)
* [搭配 Data Lake Store 使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [搭配資料湖存放區使用 Azure HDInsight](data-lake-store-hdinsight-hadoop-use-portal.md)


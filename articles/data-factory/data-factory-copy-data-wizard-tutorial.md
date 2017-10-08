---
title: "教學課程：使用複製精靈建立管線 | Microsoft Docs"
description: "在本教學課程中，您建立 Azure Data Factory 管線與複製活動使用 hello 複製精靈支援的 Data Factory"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 567b89e7a54c245c134cd0674690e6f3499b46d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a>教學課程：使用 Data Factory 複製精靈建立具有複製活動的管線
> [!div class="op_single_selector"]
> * [概觀和必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [複製精靈](data-factory-copy-data-wizard-tutorial.md)
> * [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager 範本](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)

本教學課程示範如何 toouse hello**複製精靈**toocopy 資料從 Azure blob 儲存體 tooan Azure SQL database。 

hello Azure Data Factory**複製精靈**可讓您 tooquickly 建立將資料從支援的來源資料存放區支援 tooa 目的地資料存放區複製在資料管線。 因此，我們建議當做第一個步驟 toocreate 範例管線使用 hello 精靈，為您的資料移動案例。 如需作為來源和目的地支援的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。  

本教學課程會示範如何 toocreate Azure data factory，啟動 hello 複製精靈 」，通過一連串的步驟 tooprovide 詳細資料的擷取/移動案例。 當您完成在 hello 精靈的步驟時，hello 精靈會自動建立管線複製活動 toocopy 資料從 Azure blob 儲存體 tooan Azure SQL database。 如需複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。

## <a name="prerequisites"></a>必要條件
完成 hello 中所列必要條件[教學課程概觀](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)發行項，然後再執行本教學課程。

## <a name="create-data-factory"></a>建立 Data Factory
在此步驟中，您使用 Azure 入口網站 toocreate 名為 Azure data factory hello **ADFTutorialDataFactory**。

1. 登入太[Azure 入口網站](https://portal.azure.com)。
2. 按一下**+ 新增**從 hello 左上角，按一下 **資料 + 分析**，然後按一下**Data Factory**。 
   
   ![新增->DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. 在 hello**新的 data factory**刀鋒視窗中：
   
   1. 輸入**ADFTutorialDataFactory** hello**名稱**。
       hello hello Azure data factory 的名稱必須是全域唯一的。 如果您收到 hello 錯誤： `Data factory name “ADFTutorialDataFactory” is not available`、 變更 hello hello data factory (例如，yournameADFTutorialDataFactoryYYYYMMDD) 名稱，然後再次嘗試重新建立。 請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。  
      
       ![Data Factory 名稱無法使用](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. 選取您的 Azure **訂用帳戶**。
   3. 資源群組，請執行步驟的 hello 其中一項： 
      
      - 選取**使用現有**tooselect 現有的資源群組。
      - 選取**建立新**tooenter 資源群組的名稱。
          
        部分 hello 步驟在本教學課程假設您使用 hello 名稱： **ADFTutorialResourceGroup** hello 資源群組。 toolearn 解資源群組，請參閱[資源使用您的 Azure 資源群組 toomanage](../azure-resource-manager/resource-group-overview.md)。
   4. 選取**位置**hello data factory。
   5. 選取**Pin toodashboard**在 hello hello 刀鋒視窗底部的核取方塊。  
   6. 按一下 [建立] 。
      
       ![新增 Data Factory 刀鋒視窗](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. Hello 建立完成之後，您會看到 hello **Data Factory**刀鋒視窗中 hello 下列影像所示：
   
   ![Data Factory 首頁](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a>啟動複製精靈
1. 在 hello Data Factory 刀鋒視窗中，按一下 **複製資料 [預覽]** toolaunch hello**複製精靈**。 
   
   > [!NOTE]
   > 如果您看到該 hello 網頁瀏覽器卡在 [授權]，停用/取消核取**封鎖第三方 cookie 和站台資料**在 hello 瀏覽器設定 （或） 保持啟用此設定，並建立的例外狀況**login.microsoftonline.com** ，然後再次嘗試重新啟動 hello 精靈。
2. 在 hello**屬性**頁面：
   
   1. 輸入 **CopyFromBlobToAzureSql** 做為 [工作名稱]
   2. 輸入 **說明** (選擇性)。
   3. 變更 hello**的開始日期時間**和 hello**結束日期時間**使 hello 結束日期設定 tootoday 且開始日期 toofive 天前。  
   4. 按一下 [下一步] 。  
      
      ![複製工具 - 屬性頁面](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. 在 hello**來源資料存放區**頁面上，按一下**Azure Blob 儲存體**磚。 您可以使用這個頁面 toospecify hello 來源資料存放區 hello 複製工作。 
   
    ![複製工具 - 來源資料儲存頁面](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. 在 hello**指定 hello Azure Blob 儲存體帳戶**頁面：
   
   1. 輸入 **AzureStorageLinkedService** 做為 [連結服務名稱]。
   2. 確認已針對 [帳戶選取方法] 選取 [從 Azure 訂用帳戶] 選項。
   3. 選取您的 Azure **訂用帳戶**。  
   4. 選取**Azure 儲存體帳戶**從 hello hello 選取訂用帳戶中可使用的清單中的 Azure 儲存體帳戶。 您也可以選擇 tooenter 儲存體帳戶設定手動選取**手動輸入**選項 hello**帳戶選取方法**，然後按一下**下一步**。 
      
      ![複製工具-指定 hello Azure Blob 儲存體帳戶](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. 在**選擇 hello 輸入的檔案或資料夾**頁面：
   
   1. 按兩下 **adftutorial** (資料夾)。
   2. 選取 **emp.txt**，然後按一下 [選擇]
      
      ![複製工具-選擇 hello 輸入的檔案或資料夾](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. 在 hello**選擇 hello 輸入的檔案或資料夾**頁面上，按一下**下一步**。 請勿選取 [二進位複本] 。 
   
    ![複製工具-選擇 hello 輸入的檔案或資料夾](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. 在 hello**檔案格式設定** 頁面上，您會看到 hello 分隔符號和是藉由剖析 hello 檔案的 自動偵測到的 hello 精靈的 hello 結構描述。 您也可以手動輸入 hello 分隔符號 hello 複製精靈 toostop 自動偵測或 toooverride。 按一下**下一步**在檢閱 hello 分隔符號和預覽資料。 
   
    ![複製工具 - 檔案格式設定](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. Hello 目的地資料存放區 頁面中，選取**Azure SQL Database**，然後按一下**下一步**。
   
    ![複製工具 - 選擇目的地存放區](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. 在**指定 hello Azure SQL database**頁面：
   
   1. 輸入**AzureSqlLinkedService** hello**連接名稱**欄位。
   2. 確認已針對 [伺服器 / 資料庫選取方法] 選取 [從 Azure 訂用帳戶] 選項。
   3. 選取您的 Azure **訂用帳戶**。  
   4. 選取 [伺服器名稱] 和 [資料庫]。
   5. 輸入 [使用者名稱] 和 [密碼]。
   6. 按一下 [下一步] 。  
      
      ![複製工具 - 指定 Azure SQL Database](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. 在 hello**資料表對應**頁面上，選取**emp** hello**目的地**欄位從 hello 下拉式清單中，按一下**向下箭號**（選擇性）toosee hello 結構描述和 toopreview hello 資料。
    
     ![複製工具 - 資料表對應](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. 在 hello**結構描述對應**頁面上，按一下**下一步**。
    
    ![複製工具 - 結構描述對應](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. 在 hello**效能設定**頁面上，按一下**下一步**。 
    
    ![複製工具 - 效能設定](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. 檢閱資訊在 hello**摘要**頁面，然後按一下**完成**。 hello 精靈會建立兩個連結的服務、 兩個資料集 （輸入與輸出），以及一個管線 （從啟動 hello 複製精靈 」 的位置） 的 hello data factory 中。 
    
    ![複製工具 - 效能設定](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a>啟動監視及管理應用程式
1. 在 hello**部署**頁面上，按一下 hello 連結： `Click here toomonitor copy pipeline`。
   
   ![複製工具 - 部署成功](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. hello 監視應用程式會啟動網頁瀏覽器中的個別索引標籤中。   
   
   ![監視應用程式](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. toosee hello 最新狀態的每小時的配量，按一下**重新整理**按鈕在 hello**活動 WINDOWS** hello 底部的清單。 您會看到五天之間 hello 管線的開始和結束時間的五個活動視窗。 hello 清單不會自動重新整理，因此您可能需要 tooclick 重新整理數次，才會看到 hello 就緒狀態中的所有 hello 活動視窗。 
4. Hello 清單中選取活動視窗。 Hello 中檢視詳細資料資訊，請參閱 hello**活動視窗總管**hello 右上。

    ![活動時段詳細資料](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    請注意，11、 12、 13、 14 和 15 hello 日期都為綠色，表示已經所產生 hello 每日輸出配量這些日期。 您也可以看到這個色彩編碼 hello 管線然後 hello hello 圖表檢視 中的輸出資料集。 在 hello 先前步驟中，請注意，兩個配量已產生，目前正在處理一個扇區，hello 其他兩個正在等候處理的 toobe （根據 hello 色彩編碼）。 

    如需使用此應用程式的詳細資訊，請參閱[使用監視應用程式來監視和管理管線](data-factory-monitor-manage-app.md)。

## <a name="next-steps"></a>後續步驟
在本教學課程中，您可使用 Azure Blob 儲存體作為來源資料存放區以及使用 Azure SQL Database 作為複製作業的目的地資料存放區。 hello 下表提供 hello 複製活動支援做為來源和目的地資料存放區的清單： 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

如需您在資料存放區的 hello 複製精靈中看到的欄位/屬性的詳細資訊，按一下 hello 連結 hello hello 資料表中的資料存放區。 

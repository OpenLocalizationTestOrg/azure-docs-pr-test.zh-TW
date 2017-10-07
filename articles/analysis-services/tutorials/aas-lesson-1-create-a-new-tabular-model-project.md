---
標題： aaa"Azure Analysis Services 教學課程第 1 課： 建立新的表格式模型專案 |Microsoft 文件"描述： 描述如何 toocreate 新 Azure Analysis Services 教學課程專案。 服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '

ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend
---
# <a name="lesson-1-create-a-tabular-model-project"></a>第 1 課：建立表格式模型專案

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

在這一課，您可以使用新的表格式模型專案的 SQL Server Data Tools (SSDT) toocreate hello 1400 相容性層級。 建立新的專案之後，您就可以開始新增資料和製作模型。 這一課也提供您簡單介紹 toohello 表格式模型撰寫環境在 SSDT 中。  
  
本課程的估計時間 toocomplete: **10 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型撰寫教學課程中的 hello 第 1 課。 這個課程 toocomplete，有數個需要 toohave 就地的先決條件。 詳細資訊，請參閱 toolearn [Azure Analysis Services-Adventure Works 教學課程](../tutorials/aas-adventure-works-tutorial.md)。  
  
## <a name="create-a-new-tabular-model-project"></a>建立新的表格式模型專案  
  
#### <a name="toocreate-a-new-tabular-model-project"></a>toocreate 新的表格式模型專案  
  
1.  在 SSDT 中，在 hello**檔案**功能表上，按一下 **新增** > **專案**。  
  
2.  在 hello**新專案**對話方塊方塊中，展開 **已安裝** > **Business Intelligence** > **Analysis Services**，然後按一下 **Analysis Services 表格式專案**。  
  
3.  在**名稱**，型別**AW Internet Sales**，然後指定 hello 專案檔案的位置。  
  
    根據預設，**方案名稱**hello 相同做為 hello 專案名稱; 不過，您可以輸入不同的方案名稱。  
  
4.  按一下 [確定] 。  
  
5.  在 hello**表格式模型設計師**對話方塊中，選取**整合式工作區**。  
  
    hello 表格式模型資料庫工作區中的主控件以 hello 相同的名稱，為 hello 專案在模型製作期間。 整合式工作區表示 SSDT 可以使用內建的執行個體，因而不 hello 需要 tooinstall 個別的 Analysis Services 伺服器執行個體，只是用於模型製作。
      
6.  在 [相容性等級] 中，選取 [SQL Server 2017 / Azure Analysis Services (1400)]。   
 
    ![aas 第 1 課 tmd](../tutorials/media/aas-lesson1-tmd.png)
      
    如果您沒有看到 SQL Server 2017 / Azure Analysis Services (1400) hello 相容性層級清單方塊中，您不使用 hello 最新版本的 SQL Server Data Tools。 tooget hello 最新版本，請參閱[安裝 SQL Server Data tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)。  
      
  
## <a name="understanding-hello-ssdt-tabular-model-authoring-environment"></a>了解 hello SSDT 表格式模型撰寫環境  
既然您已建立新的表格式模型專案，讓我們看一下 tooexplore hello 表格式模型撰寫環境在 SSDT 中。  
  
專案建立之後會在 SSDT 中開啟。 在右側中的 hello**表格式模型總管**，請參閱 < hello 物件的樹狀結構檢視模型中。 您還沒有匯入資料，因為 hello 資料夾是空的。 您可以以滑鼠右鍵按一下物件資料夾 tooperform 動作、 類似 toohello 功能表列。 當您逐步完成本教學課程，您會使用在模型專案中的 hello 表格式模型總管 toonavigate 不同物件。

![aas 第 1 課 tme](../tutorials/media/aas-lesson1-tme.png)

按一下 hello**方案總管 中** 索引標籤。在這裡，您可看到 **Model.bim** 檔案。 如果您沒有看見 hello 設計師視窗 toohello 左 （hello 空白視窗 hello Model.bim 索引標籤），在**方案總管 中**下**AW Internet Sales 專案**，按兩下 hello **Model.bim**檔案。 hello Model.bim 檔案包含您的模型專案的 hello 中繼資料。 

![aas 第 1 課 se](../tutorials/media/aas-lesson1-se.png)
  
按一下 [Model.bim]。 在 hello**屬性**視窗中，您會看到 hello 模型屬性，最重要的是 hello **DirectQuery 模式**屬性。 此屬性會指定是否在記憶體中模式 （關閉） 或是 DirectQuery 模式 （開啟） 部署 hello 模型。 本教學課程中，您會以 In-Memory 模式來製作和部署模型。

![aas 第 1 課屬性](../tutorials/media/aas-lesson1-properties.png)
  
當您建立模型專案時，某些模型屬性會設定自動根據資料模型化的設定可指定在 hello toohello**工具**功能表 >**選項** 對話方塊。 資料備份、 工作空間保留，與工作空間伺服器屬性會指定如何及在何處 hello 工作空間資料庫 （您的模型撰寫資料庫） 備份、 在記憶體中保留，以及建置。 稍後，如有必要，您可以變更這些設定，但現在，讓這些屬性保持不變即可。  

在 方案總管 中，以滑鼠右鍵按一下 AW 網際網路銷售 \(專案)，然後按一下屬性。 hello **AW Internet Sales 屬性頁** 對話方塊隨即出現。 稍後部署模型時，您會設定其中一些屬性。  
  
當您安裝 SSDT 時，數個新的功能表項目已加入 toohello Visual Studio 環境。 按一下 hello**模型**功能表。 從這裡，您可以匯入資料、 重新整理工作區中的資料、 瀏覽您在 Excel 中的模型、 建立檢視方塊和角色，選取 hello 模型檢視，以及設定計算選項。 按一下 hello**資料表**功能表。 從這裡，您可以建立和管理關聯性、指定日期資料表設定、建立分割區，以及編輯資料表屬性。 如果您按一下 hello**資料行**功能表上，您可以加入和刪除資料表中的資料行、 凍結資料行，以及指定排序次序。 SSDT 也會加入一些按鈕 toohello 列。 最有用是 hello 自動加總功能 toocreate 標準彙總的量值所選資料行。 其他工具列按鈕提供快速存取 toofrequently 用的功能和命令。  
  
探索 hello 對話方塊和位置的各種功能特定 tooauthoring 表格式模型的部分。 雖然某些項目尚無法使用中，您可以取得 hello 表格式模型撰寫環境的建議。  
  

## <a name="whats-next"></a>後續步驟
[第 2 課：取得資料](../tutorials/aas-lesson-2-get-data.md)。

  
  
  

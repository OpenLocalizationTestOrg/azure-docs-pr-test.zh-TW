---
標題： aaa"Azure Analysis Services 教學課程第 13 課： 部署 |Microsoft 文件"描述： 描述如何 toodeploy hello 教學課程專案 tooAzure Analysis Services。
服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '

ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 07/17/2017 ms.author: owend
---
# <a name="lesson-13-deploy"></a>第 13 課：部署

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

在這一課，您可以設定部署屬性;指定 Azure Analysis Services 伺服器 toodeploy tooand hello 模型的名稱。 然後，您可以部署在 hello 模型 toothat 執行個體。 部署模型之後，使用者可以使用報表用戶端應用程式連線 tooit。 詳細資訊，請參閱 toolearn[部署 tooAzure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy)。  
  
本課程的估計時間 toocomplete: **5 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，請依序完成。 在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 12 課： 在 Excel 中分析](../tutorials/aas-lesson-12-analyze-in-excel.md)。  

> [!IMPORTANT]  
> 您必須擁有[系統管理員權限](../analysis-services-server-admins.md)在 hello 遠端 Analysis Services 伺服器之 in-order toodeploy tooit。  

> [!IMPORTANT]  
> 如果您在內部部署 SQL Server 上安裝 hello AdventureWorksDW2014 範例資料庫，而且您要部署模型 tooan Azure Analysis Services 伺服器，[在內部部署資料閘道](../analysis-services-gateway.md)需要。
  
## <a name="deploy-hello-model"></a>部署 hello 模型  
  
#### <a name="tooconfigure-deployment-properties"></a>tooconfigure 部署屬性  

  
1.  在**方案總管 中**，以滑鼠右鍵按一下 hello **AW Internet Sales**專案，然後再按一下**屬性**。  
  
2.  在 hello **AW Internet Sales 屬性頁**對話方塊的 **部署伺服器**，在 hello**伺服器**屬性，輸入 hello 完整伺服器。  

    ![aas 第 13 課部署屬性](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  在 hello**資料庫**屬性中，輸入**Adventure Works Internet Sales**。  
  
4.  在 hello**模型名稱**屬性中，輸入**Adventure Works Internet Sales Model**。  
  
5.  驗證您的選取項目，然後按一下確定。  
  
#### <a name="toodeploy-hello-adventure-works-internet-sales"></a>toodeploy hello Adventure Works Internet Sales
  
1.  在**方案總管 中**，以滑鼠右鍵按一下 hello **AW Internet Sales**專案 >**建置**。  

2.  以滑鼠右鍵按一下 hello **AW Internet Sales**專案 >**部署**。

    當部署 tooAzure Analysis Services，您可能會提示的 tooenter 您的帳戶。 請輸入您的組織帳戶和密碼，例如 nancy@adventureworks.com。此帳戶必須在系統管理員在 hello 伺服器上。
  
    hello [部署] 對話方塊隨即出現，並顯示 hello hello 中繼資料的部署狀態和 hello 模型中每個資料表。  
    
    ![aas 第 13 課部署狀態](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. 當部署順利完成時，請繼續並按一下 [關閉]。  
  
## <a name="conclusion"></a>結論  
恭喜！ 您已完成製作和部署第一個 Analysis Services 表格式模型。 此教學課程已幫引導您完成建立表格式模型中的 hello 最常見工作。 既然部署 Adventure Works Internet Sales 模型之後，您可以使用 SQL Server Management Studio toomanage hello 模型;建立處理程序的指令碼和備份計劃。 使用者現在也可以連線 toohello 模型使用報表用戶端應用程式，例如 Microsoft Excel 或 Power BI。  

![aas 第 13 課 ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>後續步驟
[使用 Power BI Desktop 進行連線](../analysis-services-connect-pbi.md)   
[補充課程 - 動態安全性](../tutorials/aas-supplemental-lesson-dynamic-security.md)   
[補充課程 - 詳細資料列](../tutorials/aas-supplemental-lesson-detail-rows.md)   
[補充課程 - 不完全階層](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   

---
標題： aaa"Azure Analysis Services 教學課程的補充課程： 動態安全性 |Microsoft 文件"描述： 描述如何使用資料列的 toouse 動態安全性篩選 hello Azure Analysis Services 教學課程中。
服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '

ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="supplemental-lesson---dynamic-security"></a>補充課程 - 動態安全性

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

在此補充課程中，您可以建立其他角色來實作動態安全性。 動態安全性提供根據 hello 使用者名稱或登入識別碼 hello 使用者目前登入的資料列層級安全性。 
  
tooimplement 動態安全性，您可以加入包含這些使用者可以連接 toohello 模型並瀏覽模型物件和資料的 hello 使用者名稱的資料表 tooyour 模型。 您使用本教學課程所建立的 hello 模型是 Adventure Works; hello 內容中不過，toocomplete 這課程，您必須加入資料表，包含從您自己的網域使用者。 您不需要 hello 密碼的 hello 所加入的使用者名稱。 toocreate EmployeeSecurity 表格，從您自己的網域使用者的一小部分的範例與您使用 hello 貼上功能，貼上的 Excel 試算表的員工資料。 在真實世界案例中，包含使用者名稱的 hello 資料表一般會實際的資料庫中的資料表做為資料來源;例如，實際的 DimEmployee 資料表。  
  
tooimplement 動態安全性，您可以使用兩個 DAX 函數： [USERNAME 函數 (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f)和[LOOKUPVALUE 函數 (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab)。 套用於資料列篩選公式的這些函式，會以新的角色定義。 使用 hello LOOKUPVALUE 函數，hello 公式會指定 hello EmployeeSecurity 表中的值。 hello 公式然後將值 toohello USERNAME 函式，以指定 hello hello 登入的使用者的使用者名稱所屬 toothis 角色。 hello 使用者然後瀏覽 hello 角色的資料列篩選器所指定的資料。 在此案例中，您指定的銷售員工只能瀏覽網際網路 hello 各銷售領域都是成員的銷售資料。  
  
這些工作是唯一 toothis Adventure Works 表格式模型案例中，但不一定適用於 tooa 真實世界的實例會識別在這種情況。 每項工作包含描述 hello 目的 hello 工作的詳細資訊。  
  
本課程的估計時間 toocomplete: **30 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
此補充課程主題是表格式模型教學課程的一部分，請依序完成。 在執行前 hello 工作這個補充課程，您應該已完成所有先前的課程。  
  
## <a name="add-hello-dimsalesterritory-table-toohello-aw-internet-sales-tabular-model-project"></a>新增 hello DimSalesTerritory 資料表 toohello AW Internet Sales 表格式模型專案  
此 Adventure Works 案例 tooimplement 動態安全性，您必須加入兩個其他資料表 tooyour 模型。 您加入 DimSalesTerritory （做為銷售地區） 從 hello 第一個資料表 hello 相同 AdventureWorksDW 資料庫。 您稍後套用定義 hello 特定資料的資料列篩選器 toohello SalesTerritory 資料表 hello 登入的使用者可以瀏覽。  
  
#### <a name="tooadd-hello-dimsalesterritory-table"></a>tooadd hello DimSalesTerritory 資料表  
  
1.  在 表格式模型總管 > 資料來源 中，以滑鼠右鍵按一下您的連線，然後按一下匯入新資料表。  

    如果 hello 模擬認證 對話方塊出現，請輸入所使用的模擬認證 hello 第 2 課： 加入資料。
  
2.  在導覽中，選取 hello **DimSalesTerritory**資料表，然後按一下**確定**。    
  
3.  在 [查詢編輯器] 中，按一下 hello **DimSalesTerritory**查詢，然後再移除**[salesterritoryalternatekey]**資料行。  
  
7.  按一下 [匯入] 。  
  
    hello 新資料表加入 toohello 模型工作空間。 物件和資料從 hello 來源 DimSalesTerritory 資料表接著會匯入 AW Internet Sales 表格式模型中。  
  
9. 已成功匯入 hello 資料表之後，請按一下**關閉**。  

## <a name="add-a-table-with-user-name-data"></a>新增具有使用者名稱資料的資料表  
hello hello AdventureWorksDW 範例資料庫中的 DimEmployee 資料表包含來自 hello AdventureWorks 網域的使用者。 這些使用者名稱不存在於您自己的環境中。 您必須在您的模型中建立資料表，其中包含您組織中實際使用者 (至少三個) 的小型範例。 然後，您會加入這些使用者為成員 toohello 新角色。 您不需要 hello 密碼 hello 範例使用者名稱，但您需要實際的 Windows 使用者名稱從您自己的網域。  
  
#### <a name="tooadd-an-employeesecurity-table"></a>tooadd EmployeeSecurity 資料表  
  
1.  開啟 Microsoft Excel，並建立工作表。  
  
2.  複製 hello 下表，包括 hello 標頭資料列，並貼到 hello 工作表。  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  Hello 名字、 姓氏和 domain\username 取代 hello 名稱與您組織中的三個使用者的登入識別碼。 Put hello 在 hello 前兩個資料列，員工編號 1，顯示該使用者所屬銷售地區比 toomore 相同的使用者。 Hello EmployeeId 和 SalesTerritoryId 欄位保持不變。  
  
4.  儲存 hello 的工作表**SampleEmployee**。  
  
5.  Hello 工作表中選取所有 hello 資料格包含員工資料，包括 hello 標頭，然後以滑鼠右鍵按一下選取的 hello 資料，然後按一下**複製**。  
  
6.  在 SSDT 中，按一下 hello**編輯**功能表，然後再按一下**貼上**。  
  
    如果貼上呈現灰色時，按一下 hello 模型設計師視窗中的任何資料表中的任何資料行，並再試一次。  
  
7.  在 hello**貼上預覽**對話方塊中，於**資料表名稱**，型別**EmployeeSecurity**。  
  
8.  在**貼上資料 toobe**，確認 hello 資料包含所有 hello 使用者資料和 hello SampleEmployee 工作表中的標頭。  
  
9. 確認已核取 使用第一個資料列做為資料行標頭，然後按一下確定。  
  
    建立新的資料表，名為 EmployeeSecurity hello SampleEmployee 工作表複製的員工資料。  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>建立 FactInternetSales、DimGeography 和 DimSalesTerritory 資料表之間的關聯性  
hello FactInternetSales、 DimGeography 和 DimSalesTerritory 資料表全都包含常用的資料行，SalesTerritoryId。 hello DimSalesTerritory 資料表中的 hello SalesTerritoryId 資料行包含以每個銷售地區不同的識別碼值。  
  
#### <a name="toocreate-relationships-between-hello-factinternetsales-dimgeography-and-hello-dimsalesterritory-table"></a>toocreate hello FactInternetSales、 DimGeography，與 hello DimSalesTerritory 資料表之間的關聯性  
  
1.  在 圖表檢視中 hello **DimGeography**資料表，按一下並按住 hello **SalesTerritoryId**資料行，然後拖曳 hello 游標 toohello **SalesTerritoryId** hello 中的資料行**DimSalesTerritory**資料表，然後再放開。  
  
2.  在 hello **FactInternetSales**資料表，按一下並按住 hello **SalesTerritoryId**資料行，然後拖曳 hello 游標 toohello **SalesTerritoryId** hello中的資料行**DimSalesTerritory**資料表，然後再放開。  
  
    請注意 hello 此關聯性的作用中 屬性為 False，亦即非使用中。 hello FactInternetSales 資料表已經有另一個使用中關聯性。  
  
## <a name="hide-hello-employeesecurity-table-from-client-applications"></a>隱藏 hello EmployeeSecurity 資料表從用戶端應用程式  
在這個工作中，您隱藏 hello EmployeeSecurity 資料表，使其不會出現在用戶端應用程式欄位清單中。 請注意，隱藏資料表並不會保護它。 使用者仍可查詢 EmployeeSecurity 資料表資料，但前提是他們知道方式。 toosecure hello EmployeeSecurity 資料表資料，防止使用者能夠 tooquery 其中任何資料、 套用篩選，以在稍後的工作。  
  
#### <a name="toohide-hello-employeesecurity-table-from-client-applications"></a>從用戶端應用程式的 toohide hello EmployeeSecurity 資料表  
  
-   在 hello 模型設計師中，在圖表檢視中，以滑鼠右鍵按一下 hello**員工**資料表標題，然後再按一下**用戶端工具中隱藏**。  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>建立「銷售地區員工」使用者角色  
在此工作中，您會建立使用者角色。 這個角色包含定義 hello DimSalesTerritory 資料表的哪些資料列可見的 toousers 一個資料列篩選。 hello 篩選會套用在 hello 一對多關聯性方向 tooall 其他資料表相關的 tooDimSalesTerritory。 您也可以套用篩選器，可保護從任何使用者 hello 角色的成員可以查詢 hello 整個 EmployeeSecurity 資料表。  
  
> [!NOTE]  
> hello Sales Employees by Territory 角色，您在這一課中建立會限制成員 toobrowse （或查詢） 只的銷售資料所屬的 hello 銷售領域 toowhich。 如果您將使用者新增為成員 toohello Sales Employees by Territory 角色同時存在於中角色的成員建立時在[第 11 課： 建立角色](../tutorials/aas-lesson-11-create-roles.md)，取得權限的組合。 當使用者屬於多個角色、 hello 權限和每個角色定義的資料列篩選器會累計。 也就是說，hello 使用者擁有 hello 大於權限取決於 hello 角色組合。  
  
#### <a name="toocreate-a-sales-employees-by-territory-user-role"></a>toocreate Sales Employees by Territory 使用者角色  
  
1.  在 SSDT 中，按一下 hello**模型**功能表，然後再按一下**角色**。  
  
2.  在 [角色管理員] 中，按一下 [新增]。  
  
    新的角色將任何權限是以 hello 新增 toohello 清單。  
  
3.  按一下 hello 新角色，然後在 hello**名稱**資料行，hello 角色重新命名過**Sales Employees by Territory**。  
  
4.  在 hello**權限**資料行中，按一下 hello 下拉式清單中，然後選取 hello**讀取**權限。  
  
5.  按一下 hello**成員**索引標籤，然後再按一下**新增**。  
  
6.  在 hello**選取使用者或群組**對話方塊中，於**名為 tooselect Enter hello 物件**，輸入 hello 第一個範例的使用者名稱建立 hello EmployeeSecurity 資料表時，您使用。 按一下**檢查名稱**tooverify hello 使用者名稱有效，然後再按一下**確定**。  
  
    重複此步驟中，加入 hello 建立 hello EmployeeSecurity 資料表時，您使用其他範例使用者名稱。  
  
7.  按一下 hello**資料列篩選器** 索引標籤。  
  
8.  Hello **EmployeeSecurity**表格中的 hello **DAX 篩選**資料行中，下列公式的型別 hello:  
  
    ```
      =FALSE()  
    ```
  
    此公式會指定所有資料行解析 toohello false 布林條件。 Hello Sales Employees by Territory 使用者角色的成員可以查詢 hello EmployeeSecurity 資料表沒有資料行。  
  
9. Hello **DimSalesTerritory**資料表，下列公式的型別 hello:  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    此公式，hello LOOKUPVALUE 函數傳回所有 hello DimEmployeeSecurity [SalesTerritoryId] 資料行值，其中 hello EmployeeSecurity [LoginId] 是 hello 相同為 hello 目前登入 Windows 使用者名稱和 EmployeeSecurity [SalesTerritoryId] 是 hello 與 hello DimSalesTerritory [SalesTerritoryId] 相同。  
  
    hello 組 LOOKUPVALUE 所傳回的銷售領域識別碼則使用的 toorestrict hello 顯示 hello DimSalesTerritory 資料表的資料列。 只有其中 hello SalesTerritoryID hello 資料列是以 hello 組識別碼 hello LOOKUPVALUE 函數所傳回的資料列會顯示。  
  
10. 在 [角色管理員] 中，按一下 [確定]。  
  
## <a name="test-hello-sales-employees-by-territory-user-role"></a>測試 hello Sales Employees by Territory 使用者角色  
在這項工作，您可以使用在 excel 中的 hello 分析中的 hello Sales Employees by Territory 使用者角色的 SSDT tootest hello 效率。 您指定一個您要 toohello EmployeeSecurity 資料表加入 hello 使用者名稱和 hello 角色的成員。 建立 Excel 與 hello 模型之間的 hello 連接 hello 有效使用者名稱再使用這個使用者名稱。  
  
#### <a name="tootest-hello-sales-employees-by-territory-user-role"></a>tootest hello Sales Employees by Territory 使用者角色  
  
1.  在 SSDT 中，按一下 hello**模型**功能表，然後再按一下**在 Excel 中的進行分析**。  
  
2.  在 hello**在 Excel 中的進行分析**對話方塊中，於**指定 hello 使用者名稱或角色 toouse tooconnect toohello 模型**，選取**其他 Windows 使用者**，然後按一下 **瀏覽**。  
  
3.  在 hello**選取使用者或群組**對話方塊中，於**輸入 hello 物件名稱 tooselect**，輸入您在 hello EmployeeSecurity 資料表中，包含使用者名稱，然後按一下**檢查名稱**.  
  
4.  按一下**確定**tooclose hello**選取使用者或群組**對話方塊，然後按一下**確定**tooclose hello**在 Excel 中的進行分析** 對話方塊。  
  
    Excel 會開啟新的活頁簿。 將會自動建立樞紐分析表。 hello 樞紐分析表欄位清單包含最新的模型中可用的 hello 資料欄位。  
  
    請注意 hello EmployeeSecurity 資料表不是 hello 樞紐分析表欄位清單中可見的。 您於先前工作中在用戶端工具中隱藏此資料表。  
  
5.  在 hello**欄位**清單中， **∑ Internet Sales** （量值），選取 hello **InternetTotalSales**量值。 hello 量值輸入 hello**值**欄位。  
  
6.  選取 hello **SalesTerritoryId**資料行從 hello **DimSalesTerritory**資料表。 hello 資料行輸入 hello**資料列標籤**欄位。  
  
    請注意網際網路銷售數字只會出現 hello 一個區域 toowhich hello 有效使用者名稱使用所屬。 如果您選取另一個資料行，例如縣 （市） 從 hello DimGeography 資料表資料列標籤 欄位中，只有城市 hello 銷售領域 toowhich hello 有效使用者所屬會顯示。  
  
    此使用者無法瀏覽或查詢以外 hello 一個其所屬的領域的任何網際網路銷售資料。 這項限制是因為 hello hello Sales Employees by Territory 使用者角色中的 hello DimSalesTerritory 資料表定義的資料列篩選器可保護資料的所有資料與相關 tooother 銷售領域。  
  
## <a name="see-also"></a>另請參閱  
[USERNAME 函式 (DAX)](https://msdn.microsoft.com/library/hh230954.aspx)  
[LOOKUPVALUE 函式 (DAX)](https://msdn.microsoft.com/library/gg492170.aspx)  
[CUSTOMDATA 函式 (DAX)](https://msdn.microsoft.com/library/hh213140.aspx)  
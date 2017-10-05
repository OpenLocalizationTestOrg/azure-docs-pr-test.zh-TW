---
title: "Azure Analysis Services 教學課程補充課程︰動態安全性 | Microsoft Docs"
description: "說明如何在 Azure Analysis Services 教學課程中使用資料列篩選條件，進而使用動態安全性。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 4e97a558ae1a2601b5275a73164b483351f03857
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="supplemental-lesson---dynamic-security"></a><span data-ttu-id="56143-103">補充課程 - 動態安全性</span><span class="sxs-lookup"><span data-stu-id="56143-103">Supplemental lesson - Dynamic security</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="56143-104">在此補充課程中，您可以建立其他角色來實作動態安全性。</span><span class="sxs-lookup"><span data-stu-id="56143-104">In this supplemental lesson, you create an additional role that implements dynamic security.</span></span> <span data-ttu-id="56143-105">動態安全性會根據目前登入使用者的使用者名稱或登入識別碼來提供資料列層級安全性。</span><span class="sxs-lookup"><span data-stu-id="56143-105">Dynamic security provides row-level security based on the user name or login id of the user currently logged on.</span></span> 
  
<span data-ttu-id="56143-106">若要實作動態安全性，您可以將資料表新增至模型 (其中包含可連線至該模型及瀏覽模型物件和資料之使用者的使用者名稱)。</span><span class="sxs-lookup"><span data-stu-id="56143-106">To implement dynamic security, you add a table to your model containing the user names of those users that can connect to the model and browse model objects and data.</span></span> <span data-ttu-id="56143-107">您使用本教學課程建立的模型位於 Adventure Works 的環境中；不過，若要完成本課程，您必須新增包含您自有網域使用者的資料表。</span><span class="sxs-lookup"><span data-stu-id="56143-107">The model you create using this tutorial is in the context of Adventure Works; however, to complete this lesson, you must add a table containing users from your own domain.</span></span> <span data-ttu-id="56143-108">您不需要所新增使用者名稱的密碼。</span><span class="sxs-lookup"><span data-stu-id="56143-108">You do not need the passwords for the user names that are added.</span></span> <span data-ttu-id="56143-109">若要建立 EmployeeSecurity 資料表 (包含您自有網域中的少量使用者範例)，您可使用 [貼上] 功能中，貼上 Excel 試算表中的員工資料。</span><span class="sxs-lookup"><span data-stu-id="56143-109">To create an EmployeeSecurity table, with a small sample of users from your own domain, you use the Paste feature, pasting employee data from an Excel spreadsheet.</span></span> <span data-ttu-id="56143-110">在真實的案例中，包含使用者名稱的資料表通常會是實際資料庫中做為資料來源的資料表；例如，真實的 DimEmployee 資料表。</span><span class="sxs-lookup"><span data-stu-id="56143-110">In a real-world scenario, the table containing user names would typically be a table from an actual database as a data source; for example, a real DimEmployee table.</span></span>  
  
<span data-ttu-id="56143-111">若要實作動態安全性，您可以使用兩個 DAX 函式︰[USERNAME 函式 (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f) 和 [LOOKUPVALUE 函式 (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab)。</span><span class="sxs-lookup"><span data-stu-id="56143-111">To implement dynamic security, you use two DAX functions: [USERNAME Function (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f) and [LOOKUPVALUE Function (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab).</span></span> <span data-ttu-id="56143-112">套用於資料列篩選公式的這些函式，會以新的角色定義。</span><span class="sxs-lookup"><span data-stu-id="56143-112">These functions, applied in a row filter formula, are defined in a new role.</span></span> <span data-ttu-id="56143-113">使用 LOOKUPVALUE 函式，此公式會指定 EmployeeSecurity 資料表中的值。</span><span class="sxs-lookup"><span data-stu-id="56143-113">By using the LOOKUPVALUE function, the formula specifies a value from the EmployeeSecurity table.</span></span> <span data-ttu-id="56143-114">此公式接著將該值傳遞至 USERNAME 函式，其指定已登入使用者的使用者名稱屬於此角色。</span><span class="sxs-lookup"><span data-stu-id="56143-114">The formula then passes that value to the USERNAME function, which specifies the user name of the user logged on belongs to this role.</span></span> <span data-ttu-id="56143-115">使用者接著可以只瀏覽角色的資料列篩選條件所指定的資料。</span><span class="sxs-lookup"><span data-stu-id="56143-115">The user can then browse only data specified by the role’s row filters.</span></span> <span data-ttu-id="56143-116">在此案例中，您指定銷售員工只能瀏覽其所屬銷售地區的網際網路銷售資料。</span><span class="sxs-lookup"><span data-stu-id="56143-116">In this scenario, you specify that sales employees can only browse Internet sales data for the sales territories in which they are a member.</span></span>  
  
<span data-ttu-id="56143-117">這麼一來，便會識別此 Adventure Works 表格式模型案例獨有，但不一定適用於真實案例的工作。</span><span class="sxs-lookup"><span data-stu-id="56143-117">Those tasks that are unique to this Adventure Works tabular model scenario, but would not necessarily apply to a real-world scenario are identified as such.</span></span> <span data-ttu-id="56143-118">每個工作都包含描述工作目的的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="56143-118">Each task includes additional information describing the purpose of the task.</span></span>  
  
<span data-ttu-id="56143-119">這堂課的預估完成時間：**30 分鐘**</span><span class="sxs-lookup"><span data-stu-id="56143-119">Estimated time to complete this lesson: **30 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="56143-120">必要條件</span><span class="sxs-lookup"><span data-stu-id="56143-120">Prerequisites</span></span>  
<span data-ttu-id="56143-121">此補充課程主題是表格式模型教學課程的一部分，請依序完成。</span><span class="sxs-lookup"><span data-stu-id="56143-121">This supplemental lesson topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="56143-122">在此補充課程中執行工作之前，您必須已完成所有前面的課程。</span><span class="sxs-lookup"><span data-stu-id="56143-122">Before performing the tasks in this supplemental lesson, you should have completed all previous lessons.</span></span>  
  
## <a name="add-the-dimsalesterritory-table-to-the-aw-internet-sales-tabular-model-project"></a><span data-ttu-id="56143-123">將 DimSalesTerritory 資料表新增至 AW 網際網路銷售表格式模型專案</span><span class="sxs-lookup"><span data-stu-id="56143-123">Add the DimSalesTerritory table to the AW Internet Sales Tabular Model Project</span></span>  
<span data-ttu-id="56143-124">若要實作此 Adventure Works 案例的動態安全性，您必須將額外兩個資料表新增至您的模型。</span><span class="sxs-lookup"><span data-stu-id="56143-124">To implement dynamic security for this Adventure Works scenario, you must add two additional tables to your model.</span></span> <span data-ttu-id="56143-125">您新增的第一個資料表是來自相同 AdventureWorksDW 資料庫的 DimSalesTerritory (做為銷售地區)。</span><span class="sxs-lookup"><span data-stu-id="56143-125">The first table you add is DimSalesTerritory (as Sales Territory) from the same AdventureWorksDW database.</span></span> <span data-ttu-id="56143-126">您稍後會將資料列篩選條件套用到 SalesTerritory 資料表，以定義已登入使用者可以瀏覽的特定資料。</span><span class="sxs-lookup"><span data-stu-id="56143-126">You later apply a row filter to the SalesTerritory table that defines the particular data the logged on user can browse.</span></span>  
  
#### <a name="to-add-the-dimsalesterritory-table"></a><span data-ttu-id="56143-127">新增 DimSalesTerritory 資料表</span><span class="sxs-lookup"><span data-stu-id="56143-127">To add the DimSalesTerritory table</span></span>  
  
1.  <span data-ttu-id="56143-128">在 [表格式模型總管] > [資料來源] 中，以滑鼠右鍵按一下您的連線，然後按一下 [匯入新資料表]。</span><span class="sxs-lookup"><span data-stu-id="56143-128">In Tabular Model Explorer > **Data Sources**, right-click your connection, and then click **Import New Tables**.</span></span>  

    <span data-ttu-id="56143-129">如果出現 [模擬認證] 對話方塊，請輸入您在「第 2 課︰新增資料」中使用的模擬認證。</span><span class="sxs-lookup"><span data-stu-id="56143-129">If the Impersonation Credentials dialog box appears, type the impersonation credentials you used in Lesson 2: Add Data.</span></span>
  
2.  <span data-ttu-id="56143-130">在 [導覽器] 中，選取 [DimSalesTerritory] 資料表，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="56143-130">In Navigator, select the **DimSalesTerritory** table, and then click **OK**.</span></span>    
  
3.  <span data-ttu-id="56143-131">在 [查詢編輯器] 中，按一下 [DimSalesTerritory] 查詢，然後移除 [SalesTerritoryAlternateKey] 資料行。</span><span class="sxs-lookup"><span data-stu-id="56143-131">In Query Editor, click the **DimSalesTerritory** query, and then remove **SalesTerritoryAlternateKey** column.</span></span>  
  
7.  <span data-ttu-id="56143-132">按一下 [匯入] 。</span><span class="sxs-lookup"><span data-stu-id="56143-132">Click **Import**.</span></span>  
  
    <span data-ttu-id="56143-133">新資料表會新增至模型工作區。</span><span class="sxs-lookup"><span data-stu-id="56143-133">The new table is added to the model workspace.</span></span> <span data-ttu-id="56143-134">來源 DimSalesTerritory 資料表中的物件和資料則會匯入 AW 網際網路銷售表格式模型。</span><span class="sxs-lookup"><span data-stu-id="56143-134">Objects and data from the source DimSalesTerritory table are then imported into your AW Internet Sales Tabular Model.</span></span>  
  
9. <span data-ttu-id="56143-135">成功匯入資料表之後，請按一下 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="56143-135">After the table has been imported successfully, click **Close**.</span></span>  

## <a name="add-a-table-with-user-name-data"></a><span data-ttu-id="56143-136">新增具有使用者名稱資料的資料表</span><span class="sxs-lookup"><span data-stu-id="56143-136">Add a table with user name data</span></span>  
<span data-ttu-id="56143-137">AdventureWorksDW 範例資料庫中的 DimEmployee 資料表包含來自 AdventureWorks 網域的使用者。</span><span class="sxs-lookup"><span data-stu-id="56143-137">The DimEmployee table in the AdventureWorksDW sample database contains users from the AdventureWorks domain.</span></span> <span data-ttu-id="56143-138">這些使用者名稱不存在於您自己的環境中。</span><span class="sxs-lookup"><span data-stu-id="56143-138">Those user names do not exist in your own environment.</span></span> <span data-ttu-id="56143-139">您必須在您的模型中建立資料表，其中包含您組織中實際使用者 (至少三個) 的小型範例。</span><span class="sxs-lookup"><span data-stu-id="56143-139">You must create a table in your model that contains a small sample (at least three) of actual users from your organization.</span></span> <span data-ttu-id="56143-140">您接著會將這些使用者當作成員新增至新角色。</span><span class="sxs-lookup"><span data-stu-id="56143-140">You then add these users as members to the new role.</span></span> <span data-ttu-id="56143-141">您不需要範例使用者名稱的密碼，但您需要您自有網域中的實際 Windows 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="56143-141">You do not need the passwords for the sample user names, but you do need actual Windows user names from your own domain.</span></span>  
  
#### <a name="to-add-an-employeesecurity-table"></a><span data-ttu-id="56143-142">新增 EmployeeSecurity 資料表</span><span class="sxs-lookup"><span data-stu-id="56143-142">To add an EmployeeSecurity table</span></span>  
  
1.  <span data-ttu-id="56143-143">開啟 Microsoft Excel，並建立工作表。</span><span class="sxs-lookup"><span data-stu-id="56143-143">Open Microsoft Excel, creating a worksheet.</span></span>  
  
2.  <span data-ttu-id="56143-144">複製下列資料表 (包括標頭資料列)，然後將它貼到工作表中。</span><span class="sxs-lookup"><span data-stu-id="56143-144">Copy the following table, including the header row, and then paste it into the worksheet.</span></span>  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  <span data-ttu-id="56143-145">以您組織中三個使用者的名稱和登入識別碼，取代名字、姓氏和網域\使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="56143-145">Replace the first name, last name, and domain\username with the names and login ids of three users in your organization.</span></span> <span data-ttu-id="56143-146">將相同的使用者 (例如 EmployeeId 1) 放在前兩個資料列上，顯示此使用者屬於一個以上的銷售領域。</span><span class="sxs-lookup"><span data-stu-id="56143-146">Put the same user on the first two rows, for EmployeeId 1, showing this user belongs to more than one sales territory.</span></span> <span data-ttu-id="56143-147">讓 [EmployeeId] 和 [SalesTerritoryId] 欄位維持原樣。</span><span class="sxs-lookup"><span data-stu-id="56143-147">Leave the EmployeeId and SalesTerritoryId fields as they are.</span></span>  
  
4.  <span data-ttu-id="56143-148">將工作表儲存為 [SampleEmployee]。</span><span class="sxs-lookup"><span data-stu-id="56143-148">Save the worksheet as **SampleEmployee**.</span></span>  
  
5.  <span data-ttu-id="56143-149">在工作表中，選取具有員工資料的所有儲存格 (包括標頭)，然後以滑鼠右鍵按一下所選取的資料，然後按一下 [複製]。</span><span class="sxs-lookup"><span data-stu-id="56143-149">In the worksheet, select all the cells with employee data, including the headers, then right-click the selected data, and then click **Copy**.</span></span>  
  
6.  <span data-ttu-id="56143-150">在 SSDT 中，按一下 [編輯] 功能表，然後按一下 [貼上]。</span><span class="sxs-lookup"><span data-stu-id="56143-150">In SSDT, click the **Edit** menu, and then click **Paste**.</span></span>  
  
    <span data-ttu-id="56143-151">如果 [貼上] 呈現灰色，按一下模型設計工具視窗中任何資料表中的任何資料行，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="56143-151">If Paste is grayed out, click any column in any table in the model designer window, and try again.</span></span>  
  
7.  <span data-ttu-id="56143-152">在 [貼上預覽] 對話方塊的 [資料表名稱] 中，輸入 **EmployeeSecurity**。</span><span class="sxs-lookup"><span data-stu-id="56143-152">In the **Paste Preview** dialog box, in **Table Name**, type **EmployeeSecurity**.</span></span>  
  
8.  <span data-ttu-id="56143-153">在 [要貼上的資料] 中，確認資料包含 SampleEmployee 工作表中的所有使用者資料和標頭。</span><span class="sxs-lookup"><span data-stu-id="56143-153">In **Data to be pasted**, verify the data includes all the user data and headers from the SampleEmployee worksheet.</span></span>  
  
9. <span data-ttu-id="56143-154">確認已核取 [使用第一個資料列做為資料行標頭]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="56143-154">Verify **Use first row as column headers** is checked, and then click **Ok**.</span></span>  
  
    <span data-ttu-id="56143-155">隨即建立名為 EmployeeSecurity 的新資料表，其中包含從 SampleEmployee 工作表複製而來的員工資料。</span><span class="sxs-lookup"><span data-stu-id="56143-155">A new table named EmployeeSecurity with employee data copied from the SampleEmployee worksheet is created.</span></span>  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a><span data-ttu-id="56143-156">建立 FactInternetSales、DimGeography 和 DimSalesTerritory 資料表之間的關聯性</span><span class="sxs-lookup"><span data-stu-id="56143-156">Create relationships between FactInternetSales, DimGeography, and DimSalesTerritory table</span></span>  
<span data-ttu-id="56143-157">FactInternetSales、DimGeography 和 DimSalesTerritory 資料表全都包含常用的資料行 (SalesTerritoryId)。</span><span class="sxs-lookup"><span data-stu-id="56143-157">The FactInternetSales, DimGeography, and DimSalesTerritory table all contain a common column, SalesTerritoryId.</span></span> <span data-ttu-id="56143-158">DimSalesTerritory 資料表中的 SalesTerritoryId 資料行包含每個銷售地區內不同識別碼值的值。</span><span class="sxs-lookup"><span data-stu-id="56143-158">The SalesTerritoryId column in the DimSalesTerritory table contains values with a different Id for each sales territory.</span></span>  
  
#### <a name="to-create-relationships-between-the-factinternetsales-dimgeography-and-the-dimsalesterritory-table"></a><span data-ttu-id="56143-159">建立 FactInternetSales、DimGeography 和 DimSalesTerritory 資料表之間的關聯性</span><span class="sxs-lookup"><span data-stu-id="56143-159">To create relationships between the FactInternetSales, DimGeography, and the DimSalesTerritory table</span></span>  
  
1.  <span data-ttu-id="56143-160">在 [圖表檢視] 中，於 [DimGeography] 資料表中按一下並按住 [SalesTerritoryId] 資料行，然後將游標拖曳至 [DimSalesTerritory] 資料表中的 [SalesTerritoryId] 資料行，然後放開。</span><span class="sxs-lookup"><span data-stu-id="56143-160">In Diagram View, in the **DimGeography** table, click, and hold on the **SalesTerritoryId** column, then drag the cursor to the **SalesTerritoryId** column in the **DimSalesTerritory** table, and then release.</span></span>  
  
2.  <span data-ttu-id="56143-161">在 [FactInternetSales] 資料表中，按一下並按住 [SalesTerritoryId] 資料行，然後將游標拖曳至 [DimSalesTerritory] 資料表中的 [SalesTerritoryId] 資料行，然後放開。</span><span class="sxs-lookup"><span data-stu-id="56143-161">In the **FactInternetSales** table, click, and hold on the **SalesTerritoryId** column, then drag the cursor to the **SalesTerritoryId** column in the **DimSalesTerritory** table, and then release.</span></span>  
  
    <span data-ttu-id="56143-162">請注意，此關聯性的 [作用中] 屬性為 False，亦即非作用中。</span><span class="sxs-lookup"><span data-stu-id="56143-162">Notice the Active property for this relationship is False, meaning it's inactive.</span></span> <span data-ttu-id="56143-163">FactInternetSales 資料表已經有另一個作用中關聯性。</span><span class="sxs-lookup"><span data-stu-id="56143-163">The FactInternetSales table already has another active relationship.</span></span>  
  
## <a name="hide-the-employeesecurity-table-from-client-applications"></a><span data-ttu-id="56143-164">在用戶端應用程式中隱藏 EmployeeSecurity 資料表</span><span class="sxs-lookup"><span data-stu-id="56143-164">Hide the EmployeeSecurity Table from client applications</span></span>  
<span data-ttu-id="56143-165">在此工作中，您會隱藏 EmployeeSecurity 資料表，使其不會出現在用戶端應用程式的欄位清單中。</span><span class="sxs-lookup"><span data-stu-id="56143-165">In this task, you hide the EmployeeSecurity table, keeping it from appearing in a client application’s field list.</span></span> <span data-ttu-id="56143-166">請注意，隱藏資料表並不會保護它。</span><span class="sxs-lookup"><span data-stu-id="56143-166">Keep in mind that hiding a table does not secure it.</span></span> <span data-ttu-id="56143-167">使用者仍可查詢 EmployeeSecurity 資料表資料，但前提是他們知道方式。</span><span class="sxs-lookup"><span data-stu-id="56143-167">Users can still query EmployeeSecurity table data if they know how.</span></span> <span data-ttu-id="56143-168">若要保護 EmployeeSecurity 資料表資料，防止使用者查詢其中的任何資料，您可以在稍後的工作中套用篩選條件。</span><span class="sxs-lookup"><span data-stu-id="56143-168">To secure the EmployeeSecurity table data, preventing users from being able to query any of its data, you apply a filter in a later task.</span></span>  
  
#### <a name="to-hide-the-employeesecurity-table-from-client-applications"></a><span data-ttu-id="56143-169">在用戶端應用程式中隱藏 EmployeeSecurity 資料表</span><span class="sxs-lookup"><span data-stu-id="56143-169">To hide the EmployeeSecurity table from client applications</span></span>  
  
-   <span data-ttu-id="56143-170">在模型設計工具的 [圖表檢視] 中，以滑鼠右鍵按一下 [員工] 資料表標題，，然後按一下 [在用戶端工具中隱藏]。</span><span class="sxs-lookup"><span data-stu-id="56143-170">In the model designer, in Diagram View, right-click the **Employee** table heading, and then click **Hide from Client Tools**.</span></span>  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a><span data-ttu-id="56143-171">建立「銷售地區員工」使用者角色</span><span class="sxs-lookup"><span data-stu-id="56143-171">Create a Sales Employees by Territory user role</span></span>  
<span data-ttu-id="56143-172">在此工作中，您會建立使用者角色。</span><span class="sxs-lookup"><span data-stu-id="56143-172">In this task, you create a user role.</span></span> <span data-ttu-id="56143-173">此角色包含一個資料列篩選條件，以定義使用者可見的 DimSalesTerritory 資料表資料列。</span><span class="sxs-lookup"><span data-stu-id="56143-173">This role includes a row filter defining which rows of the DimSalesTerritory table are visible to users.</span></span> <span data-ttu-id="56143-174">此篩選條件接著會以一對多關聯性方向套用至 DimSalesTerritory 相關的所有其他資料表。</span><span class="sxs-lookup"><span data-stu-id="56143-174">The filter is then applied in the one-to-many relationship direction to all other tables related to DimSalesTerritory.</span></span> <span data-ttu-id="56143-175">您也可以套用一個篩選條件，以防止身為此角色成員的任何使用者查詢整個 EmployeeSecurity 資料表。</span><span class="sxs-lookup"><span data-stu-id="56143-175">You also apply a filter that secures the entire EmployeeSecurity table from being queryable by any user that is a member of the role.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="56143-176">您在這堂課中建立的「銷售地區員工」角色會限制成員只能瀏覽 (或查詢) 其所屬銷售地區的銷售資料。</span><span class="sxs-lookup"><span data-stu-id="56143-176">The Sales Employees by Territory role you create in this lesson restricts members to browse (or query) only sales data for the sales territory to which they belong.</span></span> <span data-ttu-id="56143-177">如果您將使用者新增為「銷售地區員工」角色的成員，而該使用者同時也是在[第 11 課︰建立角色](../tutorials/aas-lesson-11-create-roles.md)中建立之角色的成員，您會取得權限組合。</span><span class="sxs-lookup"><span data-stu-id="56143-177">If you add a user as a member to the Sales Employees by Territory role that also exists as a member in a role created in [Lesson 11: Create Roles](../tutorials/aas-lesson-11-create-roles.md), you get a combination of permissions.</span></span> <span data-ttu-id="56143-178">當使用者是多個角色的成員時，則針對每個角色定義的權限和資料列篩選條件會累計。</span><span class="sxs-lookup"><span data-stu-id="56143-178">When a user is a member of multiple roles, the permissions, and row filters defined for each role are cumulative.</span></span> <span data-ttu-id="56143-179">也就是說，使用者具有角色組合所決定的較高權限。</span><span class="sxs-lookup"><span data-stu-id="56143-179">That is, the user has the greater permissions determined by the combination of roles.</span></span>  
  
#### <a name="to-create-a-sales-employees-by-territory-user-role"></a><span data-ttu-id="56143-180">建立「銷售地區員工」使用者角色</span><span class="sxs-lookup"><span data-stu-id="56143-180">To create a Sales Employees by Territory user role</span></span>  
  
1.  <span data-ttu-id="56143-181">在 SSDT 中，按一下 [模型] 功能表，然後按一下 [角色]。</span><span class="sxs-lookup"><span data-stu-id="56143-181">In SSDT, click the **Model** menu, and then click **Roles**.</span></span>  
  
2.  <span data-ttu-id="56143-182">在 [角色管理員] 中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="56143-182">In **Role Manager**, click **New**.</span></span>  
  
    <span data-ttu-id="56143-183">清單中會新增 [無] 權限的新角色。</span><span class="sxs-lookup"><span data-stu-id="56143-183">A new role with the None permission is added to the list.</span></span>  
  
3.  <span data-ttu-id="56143-184">按一下新角色，然後在 [名稱] 資料行中，將角色重新命名為 [銷售地區員工]。</span><span class="sxs-lookup"><span data-stu-id="56143-184">Click the new role, and then in the **Name** column, rename the role to **Sales Employees by Territory**.</span></span>  
  
4.  <span data-ttu-id="56143-185">在 [權限] 資料行中，按一下下拉式清單，然後選取 [讀取] 權限。</span><span class="sxs-lookup"><span data-stu-id="56143-185">In the **Permissions** column, click the dropdown list, and then select the **Read** permission.</span></span>  
  
5.  <span data-ttu-id="56143-186">按一下 [成員] 索引標籤，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="56143-186">Click the **Members** tab, and then click **Add**.</span></span>  
  
6.  <span data-ttu-id="56143-187">在 [選取使用者或群組] 對話方塊的 [輸入要選取的物件名稱] 中，輸入您建立 EmployeeSecurity 資料表時使用的第一個範例使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="56143-187">In the **Select User or Group** dialog box, in **Enter the object named to select**, type the first sample user name you used when creating the EmployeeSecurity table.</span></span> <span data-ttu-id="56143-188">按一下 [檢查名稱] 來驗證使用者名稱是否有效，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="56143-188">Click **Check Names** to verify the user name is valid, and then click **Ok**.</span></span>  
  
    <span data-ttu-id="56143-189">重複此步驟，並新增您建立 EmployeeSecurity 資料表時使用的其他範例使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="56143-189">Repeat this step, adding the other sample user names you used when creating the EmployeeSecurity table.</span></span>  
  
7.  <span data-ttu-id="56143-190">按一下 [資料列篩選條件] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="56143-190">Click the **Row Filters** tab.</span></span>  
  
8.  <span data-ttu-id="56143-191">對於 **EmployeeSecurity** 資料表，在 [DAX 篩選條件] 資料行中，輸入下列公式︰</span><span class="sxs-lookup"><span data-stu-id="56143-191">For the **EmployeeSecurity** table, in the **DAX Filter** column, type the following formula:</span></span>  
  
    ```
      =FALSE()  
    ```
  
    <span data-ttu-id="56143-192">此公式指定所有資料行都會解析為 false 布林值條件。</span><span class="sxs-lookup"><span data-stu-id="56143-192">This formula specifies that all columns resolve to the false Boolean condition.</span></span> <span data-ttu-id="56143-193">「銷售地區員工」使用者角色的成員查詢無法查詢 EmployeeSecurity 資料表的任何資料行。</span><span class="sxs-lookup"><span data-stu-id="56143-193">No columns for the EmployeeSecurity table can be queried by a member of the Sales Employees by Territory user role.</span></span>  
  
9. <span data-ttu-id="56143-194">對於 **DimSalesTerritory** 資料表，輸入下列公式︰</span><span class="sxs-lookup"><span data-stu-id="56143-194">For the **DimSalesTerritory** table, type the following formula:</span></span>  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    <span data-ttu-id="56143-195">在此公式中，LOOKUPVALUE 函式會傳回 DimEmployeeSecurity[SalesTerritoryId] 資料行的所有值，其中 EmployeeSecurity[LoginId] 與目前已登入的 Windows 使用者名稱相同，而 EmployeeSecurity[SalesTerritoryId] 與 DimSalesTerritory[SalesTerritoryId] 相同。</span><span class="sxs-lookup"><span data-stu-id="56143-195">In this formula, the LOOKUPVALUE function returns all values for the DimEmployeeSecurity[SalesTerritoryId] column, where the EmployeeSecurity[LoginId] is the same as the current logged on Windows user name, and EmployeeSecurity[SalesTerritoryId] is the same as the DimSalesTerritory[SalesTerritoryId].</span></span>  
  
    <span data-ttu-id="56143-196">LOOKUPVALUE 所傳回的銷售地區 ID 集合會接著用來限制 DimSalesTerritory 資料表中顯示的資料列。</span><span class="sxs-lookup"><span data-stu-id="56143-196">The set of sales territory IDs returned by LOOKUPVALUE is then used to restrict the rows shown in the DimSalesTerritory table.</span></span> <span data-ttu-id="56143-197">只會顯示資料列的 SalesTerritoryID 在 LOOKUPVALUE 函式所傳回之 ID 集合中的資料列。</span><span class="sxs-lookup"><span data-stu-id="56143-197">Only rows where the SalesTerritoryID for the row is in the set of IDs returned by the LOOKUPVALUE function are displayed.</span></span>  
  
10. <span data-ttu-id="56143-198">在 [角色管理員] 中，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="56143-198">In Role Manager, click **Ok**.</span></span>  
  
## <a name="test-the-sales-employees-by-territory-user-role"></a><span data-ttu-id="56143-199">測試「銷售地區員工」使用者角色</span><span class="sxs-lookup"><span data-stu-id="56143-199">Test the Sales Employees by Territory User Role</span></span>  
<span data-ttu-id="56143-200">在此工作中，您會使用 SSDT 中的 [使用 Excel 分析] 功能來測試「銷售地區員工」使用者角色的功效。</span><span class="sxs-lookup"><span data-stu-id="56143-200">In this task, you use the Analyze in Excel feature in SSDT to test the efficacy of the Sales Employees by Territory user role.</span></span> <span data-ttu-id="56143-201">您可指定您新增到 EmployeeSecurity 資料表並成為角色成員的其中一個使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="56143-201">You specify one of the user names you added to the EmployeeSecurity table and as a member of the role.</span></span> <span data-ttu-id="56143-202">此使用者名稱接著會做為在 Excel 與模型之間建立之連線中的有效使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="56143-202">This user name is then used as the effective user name in the connection created between Excel and the model.</span></span>  
  
#### <a name="to-test-the-sales-employees-by-territory-user-role"></a><span data-ttu-id="56143-203">測試「銷售地區員工」使用者角色</span><span class="sxs-lookup"><span data-stu-id="56143-203">To test the Sales Employees by Territory user role</span></span>  
  
1.  <span data-ttu-id="56143-204">在 SSDT 中，按一下 [模型] 功能表，然後按一下 [使用 Excel 分析]。</span><span class="sxs-lookup"><span data-stu-id="56143-204">In SSDT, click the **Model** menu, and then click **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="56143-205">在 [使用 Excel 分析] 對話方塊的 [指定要用來連線至模型的使用者名稱或角色] 中，選取 [其他 Windows 使用者]，然後按一下 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="56143-205">In the **Analyze in Excel** dialog box, in **Specify the user name or role to use to connect to the model**, select **Other Windows User**, and then click **Browse**.</span></span>  
  
3.  <span data-ttu-id="56143-206">在 [選取使用者或群組] 對話方塊的 [輸入要選取的物件名稱] 中，輸入您包含在 EmployeeSecurity 資料表的使用者名稱，然後按一下 [檢查名稱]。</span><span class="sxs-lookup"><span data-stu-id="56143-206">In the **Select User or Group** dialog box, in **Enter the object name to select**, type a user name you included in the EmployeeSecurity table, and then click **Check Names**.</span></span>  
  
4.  <span data-ttu-id="56143-207">按一下 [確定] 以關閉 [選取使用者或群組] 對話方塊，然後按一下 [確定] 以關閉 [使用 Excel 分析] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="56143-207">Click **Ok** to close the **Select User or Group** dialog box, and then click **Ok** to close the **Analyze in Excel** dialog box.</span></span>  
  
    <span data-ttu-id="56143-208">Excel 會開啟新的活頁簿。</span><span class="sxs-lookup"><span data-stu-id="56143-208">Excel opens with a new workbook.</span></span> <span data-ttu-id="56143-209">將會自動建立樞紐分析表。</span><span class="sxs-lookup"><span data-stu-id="56143-209">A PivotTable is automatically created.</span></span> <span data-ttu-id="56143-210">樞紐分析表欄位清單包含您的新模型可用的大部分資料欄位。</span><span class="sxs-lookup"><span data-stu-id="56143-210">The PivotTable Fields list includes most of the data fields available in your new model.</span></span>  
  
    <span data-ttu-id="56143-211">請注意，樞紐分析表欄位清單不會顯示 EmployeeSecurity 資料表。</span><span class="sxs-lookup"><span data-stu-id="56143-211">Notice the EmployeeSecurity table is not visible in the PivotTable Fields list.</span></span> <span data-ttu-id="56143-212">您於先前工作中在用戶端工具中隱藏此資料表。</span><span class="sxs-lookup"><span data-stu-id="56143-212">You hid this table from client tools in a previous task.</span></span>  
  
5.  <span data-ttu-id="56143-213">在 **[欄位]** 清單的 **∑ 網際網路銷售** \(量值) 中，選取 **[InternetTotalSales]** 量值。</span><span class="sxs-lookup"><span data-stu-id="56143-213">In the **Fields** list, in **∑ Internet Sales** (measures), select the **InternetTotalSales** measure.</span></span> <span data-ttu-id="56143-214">此量值會輸入於 [值] 欄位中。</span><span class="sxs-lookup"><span data-stu-id="56143-214">The measure is entered into the **Values** fields.</span></span>  
  
6.  <span data-ttu-id="56143-215">從 **DimSalesTerritory** 資料表選取 **SalesTerritoryId** 資料行。</span><span class="sxs-lookup"><span data-stu-id="56143-215">Select the **SalesTerritoryId** column from the **DimSalesTerritory** table.</span></span> <span data-ttu-id="56143-216">此資料行會輸入於 [資料列標籤] 欄位中。</span><span class="sxs-lookup"><span data-stu-id="56143-216">The column is entered into the **Row Labels** fields.</span></span>  
  
    <span data-ttu-id="56143-217">請注意，只會針對您使用的有效使用者名稱所屬的區域顯示網際網路銷售數字。</span><span class="sxs-lookup"><span data-stu-id="56143-217">Notice Internet sales figures appear only for the one region to which the effective user name you used belongs.</span></span> <span data-ttu-id="56143-218">如果您選取另一個資料行 (例如，DimGeography 資料表中的 [城市]) 作為 [資料列標籤] 欄位，則只會顯示有效使用者所屬銷售地區中的城市。</span><span class="sxs-lookup"><span data-stu-id="56143-218">If you select another column, like City from the DimGeography table as Row Label field, only cities in the sales territory to which the effective user belongs are displayed.</span></span>  
  
    <span data-ttu-id="56143-219">此使用者無法瀏覽或查詢其所需地區以外的任何網際網路銷售資料。</span><span class="sxs-lookup"><span data-stu-id="56143-219">This user cannot browse or query any Internet sales data for territories other than the one they belong to.</span></span> <span data-ttu-id="56143-220">這項限制是因為以「銷售地區員工」使用者角色針對 DimSalesTerritory 資料表定義的資料列篩選條件，會保護其他銷售地區的所有相關資料。</span><span class="sxs-lookup"><span data-stu-id="56143-220">This restriction is because the row filter defined for the DimSalesTerritory table, in the Sales Employees by Territory user role, secures data for all data related to other sales territories.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="56143-221">另請參閱</span><span class="sxs-lookup"><span data-stu-id="56143-221">See Also</span></span>  
[<span data-ttu-id="56143-222">USERNAME 函式 (DAX)</span><span class="sxs-lookup"><span data-stu-id="56143-222">USERNAME Function (DAX)</span></span>](https://msdn.microsoft.com/library/hh230954.aspx)  
[<span data-ttu-id="56143-223">LOOKUPVALUE 函式 (DAX)</span><span class="sxs-lookup"><span data-stu-id="56143-223">LOOKUPVALUE Function (DAX)</span></span>](https://msdn.microsoft.com/library/gg492170.aspx)  
[<span data-ttu-id="56143-224">CUSTOMDATA 函式 (DAX)</span><span class="sxs-lookup"><span data-stu-id="56143-224">CUSTOMDATA Function (DAX)</span></span>](https://msdn.microsoft.com/library/hh213140.aspx)  
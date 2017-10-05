---
title: "將 Excel 連接到 SQL Database | Microsoft Docs"
description: "了解如何將 Microsoft Excel 連接到雲端的 Azure SQL Database。 將資料匯入 Excel 中進行報告和資料探索。"
services: sql-database
keywords: "連接到 sql, 將資料匯入 Excel"
documentationcenter: 
author: joseidz
manager: jhubbard
editor: 
ms.assetid: 906924bc-2707-48d3-bac6-397976a0409d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: jhubbard
ms.openlocfilehash: 97344d7c0be38b3092a3224074d486b5bb984176
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-excel-to-an-azure-sql-database-and-create-a-report"></a><span data-ttu-id="4d43c-105">將 Excel 連接到 Azure SQL Database 並建立報告</span><span class="sxs-lookup"><span data-stu-id="4d43c-105">Connect Excel to an Azure SQL database and create a report</span></span>

<span data-ttu-id="4d43c-106">將 Excel 連接到雲端的 SQL Database，以及匯入資料並根據資料庫中的值來建立資料表和圖表。</span><span class="sxs-lookup"><span data-stu-id="4d43c-106">Connect Excel to a SQL database in the cloud and import data and create tables and charts based on values in the database.</span></span> <span data-ttu-id="4d43c-107">在本教學課程中，您將設定 Excel 與資料庫資料表之間的連接、儲存可存放 Excel 資料和連接資訊的檔案，然後根據資料庫值建立樞紐分析圖。</span><span class="sxs-lookup"><span data-stu-id="4d43c-107">In this tutorial you will set up the connection between Excel and a database table, save the file that stores data and the connection information for Excel, and then create a pivot chart from the database values.</span></span>

<span data-ttu-id="4d43c-108">開始之前，Azure 中需要有 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="4d43c-108">You'll need a SQL database in Azure before you get started.</span></span> <span data-ttu-id="4d43c-109">如果您沒有，請參閱 [建立您的第一個 SQL Database](sql-database-get-started-portal.md) 以取得包含範例資料的資料庫，並執行幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="4d43c-109">If you don't have one, see [Create your first SQL database](sql-database-get-started-portal.md) to get a database with sample data up and running in a few minutes.</span></span> <span data-ttu-id="4d43c-110">在本文中，您會將該文章中的範例資料匯入 Excel 中，但是您可以依照類似的步驟並使用您自己的資料來執行。</span><span class="sxs-lookup"><span data-stu-id="4d43c-110">In this article, you'll import sample data into Excel from that article, but you can follow similar steps with your own data.</span></span>

<span data-ttu-id="4d43c-111">您也會需要 Excel。</span><span class="sxs-lookup"><span data-stu-id="4d43c-111">You'll also need a copy of Excel.</span></span> <span data-ttu-id="4d43c-112">本文使用 [Microsoft Excel 2016](https://products.office.com/)。</span><span class="sxs-lookup"><span data-stu-id="4d43c-112">This article uses [Microsoft Excel 2016](https://products.office.com/).</span></span>

## <a name="connect-excel-to-a-sql-database-and-create-an-odc-file"></a><span data-ttu-id="4d43c-113">將 Excel 連接到 SQL Database 並建立 odc 檔案</span><span class="sxs-lookup"><span data-stu-id="4d43c-113">Connect Excel to a SQL database and create an odc file</span></span>
1. <span data-ttu-id="4d43c-114">若要將 Excel 連接到 SQL Database，請開啟 Excel，然後建立新的活頁簿或開啟現有的 Excel 活頁簿。</span><span class="sxs-lookup"><span data-stu-id="4d43c-114">To connect Excel to SQL database, open Excel and then create a new workbook or open an existing Excel workbook.</span></span>
2. <span data-ttu-id="4d43c-115">在頁面頂端的功能表列中，依序按一下 [資料]、[從其他來源]，然後按一下 [從 SQL Server]。</span><span class="sxs-lookup"><span data-stu-id="4d43c-115">In the menu bar at the top of the page click **Data**, click **From Other Sources**, and then click **From SQL Server**.</span></span>
   
   ![選取資料來源：將 Excel 連接到 SQL Database。](./media/sql-database-connect-excel/excel_data_source.png)
   
   <span data-ttu-id="4d43c-117">資料連線精靈隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="4d43c-117">The Data Connection Wizard opens.</span></span>
3. <span data-ttu-id="4d43c-118">在 [連接到資料庫伺服器] 對話方塊中，以 <*servername*>**.database.windows.net** 格式，輸入您要連接的 SQL Database **伺服器名稱**。</span><span class="sxs-lookup"><span data-stu-id="4d43c-118">In the **Connect to Database Server** dialog box, type the SQL Database **Server name** you want to connect to in the form <*servername*>**.database.windows.net**.</span></span> <span data-ttu-id="4d43c-119">路如， **adworkserver.database.windows.net**。</span><span class="sxs-lookup"><span data-stu-id="4d43c-119">For example, **adworkserver.database.windows.net**.</span></span>
4. <span data-ttu-id="4d43c-120">在 [登入認證] 之下，按一下 [使用下列的使用者名稱和密碼]，輸入您在建立 SQL Database 時為它建立的 [使用者名稱] 和 [密碼]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="4d43c-120">Under **Log on credentials**, click **Use the following User Name and Password**, type the **User Name** and **Password** you set up for the SQL Database server when you created it, and then click **Next**.</span></span>
   
   ![輸入伺服器名稱和登入認證](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > <span data-ttu-id="4d43c-122">根據您的網路環境，您可能無法連接，而如果 SQL Database 伺服器不允許來自您的用戶端 IP 位址的流量，您可能會失去連接。</span><span class="sxs-lookup"><span data-stu-id="4d43c-122">Depending on your network environment, you may not be able to connect or you may lose the connection if the SQL Database server doesn't allow traffic from your client IP address.</span></span> <span data-ttu-id="4d43c-123">移至 [Azure 入口網站](https://portal.azure.com/)，按一下 SQL Server，按一下您的伺服器中，按一下設定下的防火牆並新增您的用戶端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4d43c-123">Go to the [Azure portal](https://portal.azure.com/), click SQL servers, click your server, click firewall under settings and add your client IP address.</span></span> <span data-ttu-id="4d43c-124">如需詳細資訊，請參閱 [如何設定防火牆設定](sql-database-configure-firewall-settings.md) 。</span><span class="sxs-lookup"><span data-stu-id="4d43c-124">See [How to configure firewall settings](sql-database-configure-firewall-settings.md) for details.</span></span>
   > 
   > 
5. <span data-ttu-id="4d43c-125">在 [選取資料庫和資料表] 對話方塊中，從清單中選取您要使用的資料庫，然後按一下您要使用的資料表或檢視 (我們選擇 **vGetAllCategories**)，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="4d43c-125">In the **Select Database and Table** dialog, select the database you want to work with from the list, and then click the tables or views you want to work with (we chose **vGetAllCategories**), and then click **Next**.</span></span>
   
    ![選取資料庫和資料表。](./media/sql-database-connect-excel/select-database-and-table.png)
   
    <span data-ttu-id="4d43c-127">[儲存資料連接檔案並完成]  對話方塊隨即開啟，請在其中提供 Excel 使用的 Office 資料庫連接 (*.odc) 檔案的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4d43c-127">The **Save Data Connection File and Finish** dialog box opens, where you provide information about the Office database connection (*.odc) file that Excel uses.</span></span> <span data-ttu-id="4d43c-128">您可以保留預設值，或自訂您的選取項目。</span><span class="sxs-lookup"><span data-stu-id="4d43c-128">You can leave the defaults or customize your selections.</span></span>
6. <span data-ttu-id="4d43c-129">您可以保留預設值，但請特別注意 [檔案名稱]  。</span><span class="sxs-lookup"><span data-stu-id="4d43c-129">You can leave the defaults, but note the **File Name** in particular.</span></span> <span data-ttu-id="4d43c-130">[描述]、[易記名稱] 和 [搜尋關鍵字] 可幫助您和其他使用者記住您要連接的項目並尋找連接。</span><span class="sxs-lookup"><span data-stu-id="4d43c-130">A **Description**, a **Friendly Name**, and **Search Keywords** help you and other users remember what you're connecting to and find the connection.</span></span> <span data-ttu-id="4d43c-131">如果您希望連接資訊儲存在 odc 檔案中，以便在連接時進行更新，請按一下 [永遠嘗試使用此檔案來重新整理資料]，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="4d43c-131">Click **Always attempt to use this file to refresh data** if you want connection information stored in the odc file so it can update when you connect to it, and then click **Finish**.</span></span>
   
    ![儲存 odc 檔案](./media/sql-database-connect-excel/save-odc-file.png)
   
    <span data-ttu-id="4d43c-133">[匯入資料]  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="4d43c-133">The **Import data** dialog box appears.</span></span>

## <a name="import-the-data-into-excel-and-create-a-pivot-chart"></a><span data-ttu-id="4d43c-134">將資料匯入 Excel 中並建立樞紐分析圖</span><span class="sxs-lookup"><span data-stu-id="4d43c-134">Import the data into Excel and create a pivot chart</span></span>
<span data-ttu-id="4d43c-135">您現已建立連接並建立含有資料與連接資訊的檔案，您可準備開始匯入資料。</span><span class="sxs-lookup"><span data-stu-id="4d43c-135">Now that you've established the connection and created the file with data and connection information, you're reading to import the data.</span></span>

1. <span data-ttu-id="4d43c-136">在 [匯入資料] 對話方塊中，按一下您要在工作表中呈現資料的選項，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="4d43c-136">In the **Import Data** dialog, click the option you want for presenting your data in the worksheet and then click **OK**.</span></span> <span data-ttu-id="4d43c-137">我們選擇 [樞紐分析圖]。</span><span class="sxs-lookup"><span data-stu-id="4d43c-137">We chose **PivotChart**.</span></span> <span data-ttu-id="4d43c-138">您也可以選擇建立**新工作表** 或**將此資料加入至資料模型**。</span><span class="sxs-lookup"><span data-stu-id="4d43c-138">You can also choose to create a **New worksheet** or to **Add this data to a Data Model**.</span></span> <span data-ttu-id="4d43c-139">如需資料模型的詳細資訊，請參閱[在 Excel 中建立資料模型](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B)。</span><span class="sxs-lookup"><span data-stu-id="4d43c-139">For more information on Data Models, see [Create a data model in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span></span> <span data-ttu-id="4d43c-140">按一下 [屬性] 以瀏覽您在上一個步驟中建立的 odc 檔案的相關資訊，並選擇用於重新整理資料的選項。</span><span class="sxs-lookup"><span data-stu-id="4d43c-140">Click **Properties** to explore information about the odc file you created in the previous step and to choose options for refreshing the data.</span></span>
   
    ![在 Excel 中選擇資料的格式](./media/sql-database-connect-excel/import-data.png)
   
    <span data-ttu-id="4d43c-142">工作表現在有空白的樞紐分析表和圖表。</span><span class="sxs-lookup"><span data-stu-id="4d43c-142">The worksheet now has an empty pivot table and chart.</span></span>
2. <span data-ttu-id="4d43c-143">在 [樞紐分析表欄位] 之下，選取所有您要檢視的欄位的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="4d43c-143">Under **PivotTable Fields**, select all the check-boxes for the fields you want to view.</span></span>
   
    ![設定資料庫報告。](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> <span data-ttu-id="4d43c-145">如果您要將其他 Excel 活頁簿和工作表連接到資料庫，請按一下 [資料]，按一下 [連接]，按一下 [新增]，從清單中選擇您所建立的連接，然後按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="4d43c-145">If you want to connect other Excel workbooks and worksheets to the database, click **Data**, click **Connections**, click **Add**, choose the connection you created from the list, and then click **Open**.</span></span>
> <span data-ttu-id="4d43c-146">![從另一個活頁簿開啟連接](./media/sql-database-connect-excel/open-from-another-workbook.png)</span><span class="sxs-lookup"><span data-stu-id="4d43c-146">![Open a connection from another workbook](./media/sql-database-connect-excel/open-from-another-workbook.png)</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4d43c-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4d43c-147">Next steps</span></span>
* <span data-ttu-id="4d43c-148">了解如何 [使用 SQL Server Management Studio 連接到 SQL Database](sql-database-connect-query-ssms.md) ，以便進行進階查詢和分析。</span><span class="sxs-lookup"><span data-stu-id="4d43c-148">Learn how to [Connect to SQL Database with SQL Server Management Studio](sql-database-connect-query-ssms.md) for advanced querying and analysis.</span></span>
* <span data-ttu-id="4d43c-149">了解 [彈性集區](sql-database-elastic-pool.md)的優點。</span><span class="sxs-lookup"><span data-stu-id="4d43c-149">Learn about the benefits of [elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="4d43c-150">了解如何 [建立 Web 應用程式以連接到後端的 SQL Database](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="4d43c-150">Learn how to [create a web application that connects to SQL Database on the back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span>


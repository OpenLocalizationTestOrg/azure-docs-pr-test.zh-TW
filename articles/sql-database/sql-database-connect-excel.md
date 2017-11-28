---
title: "aaaConnect Excel tooSQL 資料庫 |Microsoft 文件"
description: "了解如何 tooconnect Microsoft Excel tooAzure SQL 資料庫 hello 雲端中。 將資料匯入 Excel 中進行報告和資料探索。"
services: sql-database
keywords: "連接 excel toosql，匯入資料 tooexcel"
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
ms.openlocfilehash: 0048849432023145bd1009d45b6d9b64a9c7ac3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-tooan-azure-sql-database-and-create-a-report"></a><span data-ttu-id="29b7a-105">連接的 Excel tooan Azure SQL 資料庫，並建立報表</span><span class="sxs-lookup"><span data-stu-id="29b7a-105">Connect Excel tooan Azure SQL database and create a report</span></span>

<span data-ttu-id="29b7a-106">連接 hello 雲端中的 Excel tooa SQL database 匯入資料和建立資料表和圖表，根據 hello 資料庫中的值。</span><span class="sxs-lookup"><span data-stu-id="29b7a-106">Connect Excel tooa SQL database in hello cloud and import data and create tables and charts based on values in hello database.</span></span> <span data-ttu-id="29b7a-107">在本教學課程，您將設定 hello Excel 與資料庫資料表之間的連接，儲存 hello 檔案，其中會儲存適用於 Excel 的資料和 hello 連接資訊，然後建立樞紐分析圖 hello 資料庫值。</span><span class="sxs-lookup"><span data-stu-id="29b7a-107">In this tutorial you will set up hello connection between Excel and a database table, save hello file that stores data and hello connection information for Excel, and then create a pivot chart from hello database values.</span></span>

<span data-ttu-id="29b7a-108">開始之前，Azure 中需要有 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="29b7a-108">You'll need a SQL database in Azure before you get started.</span></span> <span data-ttu-id="29b7a-109">如果您沒有帳戶，請參閱[第一個 SQL 資料庫建立](sql-database-get-started-portal.md)tooget 啟動並執行幾分鐘的時間的範例資料的資料庫。</span><span class="sxs-lookup"><span data-stu-id="29b7a-109">If you don't have one, see [Create your first SQL database](sql-database-get-started-portal.md) tooget a database with sample data up and running in a few minutes.</span></span> <span data-ttu-id="29b7a-110">在本文中，您會將該文章中的範例資料匯入 Excel 中，但是您可以依照類似的步驟並使用您自己的資料來執行。</span><span class="sxs-lookup"><span data-stu-id="29b7a-110">In this article, you'll import sample data into Excel from that article, but you can follow similar steps with your own data.</span></span>

<span data-ttu-id="29b7a-111">您也會需要 Excel。</span><span class="sxs-lookup"><span data-stu-id="29b7a-111">You'll also need a copy of Excel.</span></span> <span data-ttu-id="29b7a-112">本文使用 [Microsoft Excel 2016](https://products.office.com/)。</span><span class="sxs-lookup"><span data-stu-id="29b7a-112">This article uses [Microsoft Excel 2016](https://products.office.com/).</span></span>

## <a name="connect-excel-tooa-sql-database-and-create-an-odc-file"></a><span data-ttu-id="29b7a-113">連接的 Excel tooa SQL 資料庫，並建立 odc 檔案</span><span class="sxs-lookup"><span data-stu-id="29b7a-113">Connect Excel tooa SQL database and create an odc file</span></span>
1. <span data-ttu-id="29b7a-114">tooconnect Excel tooSQL 資料庫中，開啟 Excel，然後再建立新的活頁簿或開啟現有的 Excel 活頁簿。</span><span class="sxs-lookup"><span data-stu-id="29b7a-114">tooconnect Excel tooSQL database, open Excel and then create a new workbook or open an existing Excel workbook.</span></span>
2. <span data-ttu-id="29b7a-115">Hello hello hello 頁頂端的功能表列中按一下**資料**，按一下 **從其他來源**，然後按一下**從 SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="29b7a-115">In hello menu bar at hello top of hello page click **Data**, click **From Other Sources**, and then click **From SQL Server**.</span></span>
   
   ![選取資料來源： 連接的 Excel tooSQL 資料庫。](./media/sql-database-connect-excel/excel_data_source.png)
   
   <span data-ttu-id="29b7a-117">hello 資料連線精靈 隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="29b7a-117">hello Data Connection Wizard opens.</span></span>
3. <span data-ttu-id="29b7a-118">在 hello**連接 tooDatabase 伺服器**對話方塊中，型別 hello SQL Database**伺服器名稱**想 tooconnect tooin hello 表單 <*servername* > **。.database.windows.net**。</span><span class="sxs-lookup"><span data-stu-id="29b7a-118">In hello **Connect tooDatabase Server** dialog box, type hello SQL Database **Server name** you want tooconnect tooin hello form <*servername*>**.database.windows.net**.</span></span> <span data-ttu-id="29b7a-119">路如， **adworkserver.database.windows.net**。</span><span class="sxs-lookup"><span data-stu-id="29b7a-119">For example, **adworkserver.database.windows.net**.</span></span>
4. <span data-ttu-id="29b7a-120">下**登入認證**，按一下**下列使用者名稱和密碼使用 hello**，型別 hello**使用者名**和**密碼**設定的當您建立 hello SQL Database 伺服器，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="29b7a-120">Under **Log on credentials**, click **Use hello following User Name and Password**, type hello **User Name** and **Password** you set up for hello SQL Database server when you created it, and then click **Next**.</span></span>
   
   ![輸入 hello 伺服器名稱和登入認證](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > <span data-ttu-id="29b7a-122">根據您的網路環境，您可能不是能 tooconnect，或如果 hello SQL Database 伺服器不允許從您的用戶端 IP 位址的流量，您可能會遺失 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="29b7a-122">Depending on your network environment, you may not be able tooconnect or you may lose hello connection if hello SQL Database server doesn't allow traffic from your client IP address.</span></span> <span data-ttu-id="29b7a-123">移 toohello [Azure 入口網站](https://portal.azure.com/)、 按一下 SQL server]，按一下您的伺服器、 按一下 [設定] 下的防火牆，加入您的用戶端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="29b7a-123">Go toohello [Azure portal](https://portal.azure.com/), click SQL servers, click your server, click firewall under settings and add your client IP address.</span></span> <span data-ttu-id="29b7a-124">請參閱[tooconfigure 防火牆設定的方式](sql-database-configure-firewall-settings.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="29b7a-124">See [How tooconfigure firewall settings](sql-database-configure-firewall-settings.md) for details.</span></span>
   > 
   > 
5. <span data-ttu-id="29b7a-125">在 hello**選取資料庫和資料表**對話方塊中，選取 hello 資料庫，您想要從 hello 清單與 toowork，然後按一下hello 資料表或檢視您想要與 toowork (我們選擇**vGetAllCategories**)，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="29b7a-125">In hello **Select Database and Table** dialog, select hello database you want toowork with from hello list, and then click hello tables or views you want toowork with (we chose **vGetAllCategories**), and then click **Next**.</span></span>
   
    ![選取資料庫和資料表。](./media/sql-database-connect-excel/select-database-and-table.png)
   
    <span data-ttu-id="29b7a-127">hello**儲存資料連線檔案和完成**對話方塊隨即開啟，您用來提供 hello Office 資料庫連線 (query) 檔案，Excel 會使用的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="29b7a-127">hello **Save Data Connection File and Finish** dialog box opens, where you provide information about hello Office database connection (*.odc) file that Excel uses.</span></span> <span data-ttu-id="29b7a-128">您可以保留 hello 預設值，或自訂您的選擇。</span><span class="sxs-lookup"><span data-stu-id="29b7a-128">You can leave hello defaults or customize your selections.</span></span>
6. <span data-ttu-id="29b7a-129">您可以保留 hello 的預設值，但請注意 hello**檔案名稱**特別。</span><span class="sxs-lookup"><span data-stu-id="29b7a-129">You can leave hello defaults, but note hello **File Name** in particular.</span></span> <span data-ttu-id="29b7a-130">A**描述**、**易記名稱**，和**搜尋關鍵字**幫助您和您要連線的其他使用者記住 tooand 找不到 hello 連接。</span><span class="sxs-lookup"><span data-stu-id="29b7a-130">A **Description**, a **Friendly Name**, and **Search Keywords** help you and other users remember what you're connecting tooand find hello connection.</span></span> <span data-ttu-id="29b7a-131">按一下**永遠嘗試 toouse 這個檔案 toorefresh 資料**如果您想連接資訊儲存在 hello odc 檔案，所以當您連接 tooit，然後按一下它可以更新**完成**。</span><span class="sxs-lookup"><span data-stu-id="29b7a-131">Click **Always attempt toouse this file toorefresh data** if you want connection information stored in hello odc file so it can update when you connect tooit, and then click **Finish**.</span></span>
   
    ![儲存 odc 檔案](./media/sql-database-connect-excel/save-odc-file.png)
   
    <span data-ttu-id="29b7a-133">hello**匯入資料** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="29b7a-133">hello **Import data** dialog box appears.</span></span>

## <a name="import-hello-data-into-excel-and-create-a-pivot-chart"></a><span data-ttu-id="29b7a-134">Hello 資料匯入 Excel，並建立樞紐分析圖</span><span class="sxs-lookup"><span data-stu-id="29b7a-134">Import hello data into Excel and create a pivot chart</span></span>
<span data-ttu-id="29b7a-135">現在，您已建立 hello 連接及資料與連接資訊建立的 hello 檔案，您所閱讀 tooimport hello 資料。</span><span class="sxs-lookup"><span data-stu-id="29b7a-135">Now that you've established hello connection and created hello file with data and connection information, you're reading tooimport hello data.</span></span>

1. <span data-ttu-id="29b7a-136">在 [hello**匯入資料**] 對話方塊中，按一下您想要您的資料呈現 hello 工作表中的 hello 選項，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="29b7a-136">In hello **Import Data** dialog, click hello option you want for presenting your data in hello worksheet and then click **OK**.</span></span> <span data-ttu-id="29b7a-137">我們選擇 [樞紐分析圖]。</span><span class="sxs-lookup"><span data-stu-id="29b7a-137">We chose **PivotChart**.</span></span> <span data-ttu-id="29b7a-138">您也可以選擇 toocreate**新工作表**或太**加入此資料 tooa 資料模型**。</span><span class="sxs-lookup"><span data-stu-id="29b7a-138">You can also choose toocreate a **New worksheet** or too**Add this data tooa Data Model**.</span></span> <span data-ttu-id="29b7a-139">如需資料模型的詳細資訊，請參閱[在 Excel 中建立資料模型](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B)。</span><span class="sxs-lookup"><span data-stu-id="29b7a-139">For more information on Data Models, see [Create a data model in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span></span> <span data-ttu-id="29b7a-140">按一下**屬性**tooexplore hello 先前步驟和 toochoose 選項重新整理 hello 資料中建立 hello odc 檔案的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="29b7a-140">Click **Properties** tooexplore information about hello odc file you created in hello previous step and toochoose options for refreshing hello data.</span></span>
   
    ![選擇在 Excel 中的 hello 資料格式](./media/sql-database-connect-excel/import-data.png)
   
    <span data-ttu-id="29b7a-142">空白的樞紐分析表和圖表，現在有 hello 工作表。</span><span class="sxs-lookup"><span data-stu-id="29b7a-142">hello worksheet now has an empty pivot table and chart.</span></span>
2. <span data-ttu-id="29b7a-143">在下**樞紐分析表欄位**，所有 hello 的核取方塊選取 hello 想 tooview 欄位。</span><span class="sxs-lookup"><span data-stu-id="29b7a-143">Under **PivotTable Fields**, select all hello check-boxes for hello fields you want tooview.</span></span>
   
    ![設定資料庫報告。](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> <span data-ttu-id="29b7a-145">如果您想 tooconnect 其他 Excel 活頁簿和工作表 toohello 資料庫時，按一下**資料**，按一下 **連線**，按一下 **新增**，選擇您所建立的 hello 連接從 hello 清單，然後按一下**開啟**。</span><span class="sxs-lookup"><span data-stu-id="29b7a-145">If you want tooconnect other Excel workbooks and worksheets toohello database, click **Data**, click **Connections**, click **Add**, choose hello connection you created from hello list, and then click **Open**.</span></span>
> <span data-ttu-id="29b7a-146">![從另一個活頁簿開啟連接](./media/sql-database-connect-excel/open-from-another-workbook.png)</span><span class="sxs-lookup"><span data-stu-id="29b7a-146">![Open a connection from another workbook](./media/sql-database-connect-excel/open-from-another-workbook.png)</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="29b7a-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="29b7a-147">Next steps</span></span>
* <span data-ttu-id="29b7a-148">了解如何太[tooSQL 資料庫連接使用 SQL Server Management Studio](sql-database-connect-query-ssms.md)的進階 查詢和分析。</span><span class="sxs-lookup"><span data-stu-id="29b7a-148">Learn how too[Connect tooSQL Database with SQL Server Management Studio](sql-database-connect-query-ssms.md) for advanced querying and analysis.</span></span>
* <span data-ttu-id="29b7a-149">深入了解 hello 優點[彈性集區](sql-database-elastic-pool.md)。</span><span class="sxs-lookup"><span data-stu-id="29b7a-149">Learn about hello benefits of [elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="29b7a-150">了解如何太[建立 web 應用程式連接 tooSQL 資料庫 hello 後端上的](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="29b7a-150">Learn how too[create a web application that connects tooSQL Database on hello back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span>


---
title: "移轉：資料倉儲移轉公用程式 | Microsoft Docs"
description: "移轉至 SQL 資料倉儲。"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 4d7ad981-ef31-4513-b337-50bdc4709c09
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 2466e823c448ada4dc7bc5769b1b7f10bbb5dc7d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="data-warehouse-migration-utility-preview"></a><span data-ttu-id="40e85-103">資料倉儲移轉公用程式 (預覽)</span><span class="sxs-lookup"><span data-stu-id="40e85-103">Data Warehouse Migration Utility (Preview)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="40e85-104">[下載移轉公用程式][Download Migration Utility]</span><span class="sxs-lookup"><span data-stu-id="40e85-104">[Download Migration Utility][Download Migration Utility]</span></span>
> 
> 

<span data-ttu-id="40e85-105">資料倉儲移轉公用程式是一種工具，專門用來將結構描述和資料從 SQL Server 和 Azure SQL Database 移轉至 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="40e85-105">The Data Warehouse Migration Utility is a tool designed to migrate schema and data from SQL Server and Azure SQL Database to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="40e85-106">在結構描述移轉的過程中，此工具會在來源與目的地之間自動對應相應的結構描述。</span><span class="sxs-lookup"><span data-stu-id="40e85-106">During schema migration, the tool automatically maps the corresponding schema from source to destination.</span></span> <span data-ttu-id="40e85-107">結構描述完成移轉後，工具提供以自動產生的指令碼移動資料的選項。</span><span class="sxs-lookup"><span data-stu-id="40e85-107">After the schema has been migrated, the tools provides the option to move data with automatically generated scripts.</span></span>

<span data-ttu-id="40e85-108">除了結構描述和資料移轉之外，此工具還能讓您選擇產生相容性報告，以摘要的形式列出目標和來源執行個體之間可能會妨礙移轉作業的不相容問題。</span><span class="sxs-lookup"><span data-stu-id="40e85-108">In addition to schema and data migration, this tool gives you the option to generate compatibility reports which summarize incompatibilities between the target and source instances which would prevent streamlined migration.</span></span>

## <a name="get-started"></a><span data-ttu-id="40e85-109">開始使用</span><span class="sxs-lookup"><span data-stu-id="40e85-109">Get started</span></span>
<span data-ttu-id="40e85-110">安裝的先決條件是，您必須使用 BCP 命令列公用程式來執行移轉指令碼和 Office，才能檢視相容性報告。</span><span class="sxs-lookup"><span data-stu-id="40e85-110">As a prerequisite for installation, you will need the BCP command-line utility to run migration scripts and Office to view the compatibility report.</span></span> <span data-ttu-id="40e85-111">啟動所下載的可執行檔之後，系統會提示您接受標準 EULA，才能繼續安裝此工具。</span><span class="sxs-lookup"><span data-stu-id="40e85-111">After launching the executable that is downloaded you will be prompted to accept a standard EULA before the tool will be installed.</span></span>

<span data-ttu-id="40e85-112">此外，若要執行移轉公用程式，您在想要移轉的資料庫上需要有下列其中一個權限：CREATE DATABASE、ALTER ANY DATABASE 或 VIEW ANY DEFINITION。</span><span class="sxs-lookup"><span data-stu-id="40e85-112">In addition, to run the Migration Utiliy, you will need the one following permissions on the database that you are looking to migrate: CREATE DATABASE, ALTER ANY DATABASE or VIEW ANY DEFINITION.</span></span>

### <a name="launching-the-tool-and-connecting"></a><span data-ttu-id="40e85-113">啟動工具並進行連接</span><span class="sxs-lookup"><span data-stu-id="40e85-113">Launching the tool and connecting</span></span>
<span data-ttu-id="40e85-114">透過按一下於安裝後出現的桌面圖示來啟動工具。</span><span class="sxs-lookup"><span data-stu-id="40e85-114">Launch the tool by clicking on the desktop icon which appears post install.</span></span> <span data-ttu-id="40e85-115">開啟此工具時，畫面會顯示初始連接頁面，提示您選擇移轉工具的來源和目的地。</span><span class="sxs-lookup"><span data-stu-id="40e85-115">Upon opening the tool, you will be prompted with an initial connection page where you can choose your source and destination for the migration tool.</span></span> <span data-ttu-id="40e85-116">目前，此工具支援 SQL Server 和 Azure SQL Database 做為來源，SQL 資料倉儲做為目的地。</span><span class="sxs-lookup"><span data-stu-id="40e85-116">At this time, we support SQL Server and Azure SQL Database as sources and SQL Data Warehouse as a destination.</span></span> <span data-ttu-id="40e85-117">選取這些項目之後，工具會要求您填寫伺服器名稱並執行驗證程序，然後按一下 [連接]，以連接至您的來源伺服器。</span><span class="sxs-lookup"><span data-stu-id="40e85-117">After selecting this you will be asked to connect to your source server by filling in server name and authenticating and then clicking ‘Connect’.</span></span>

<span data-ttu-id="40e85-118">完成驗證後，工具會顯示已連接伺服器中現有的資料庫清單。</span><span class="sxs-lookup"><span data-stu-id="40e85-118">After authenticating, the tool will show a list of databases that are present in the server which you are connected to.</span></span> <span data-ttu-id="40e85-119">您可以選取想要移轉的資料庫，然後按一下 [移轉選取項目]，開始移轉程序。</span><span class="sxs-lookup"><span data-stu-id="40e85-119">You can begin the migration by selecting a database that you would like to migrate and then clicking on ‘Migrate selected’.</span></span>

## <a name="migration-report"></a><span data-ttu-id="40e85-120">移轉報告</span><span class="sxs-lookup"><span data-stu-id="40e85-120">Migration report</span></span>
<span data-ttu-id="40e85-121">在工具中選取 [檢查資料庫相容性] 會產生一份報告，針對您已要求移轉的資料庫，摘要說明所有的物件不相容問題。</span><span class="sxs-lookup"><span data-stu-id="40e85-121">Selecting ‘Check Database Compatibility’ in the tool will generate a report summarizing all object incompatibilities in the database you requested to migrate.</span></span> <span data-ttu-id="40e85-122">未列在 SQL 資料倉儲中的部分 SQL Server 功能清單，可以在我們的[移轉文件][migration documentation]中找到。</span><span class="sxs-lookup"><span data-stu-id="40e85-122">A broader list of some of the SQL Server functionality that is not present in SQL Data Warehouse can be found in our [migration documentation][migration documentation].</span></span> <span data-ttu-id="40e85-123">報告產生後，您可以在 Excel 中儲存並開啟該報告。</span><span class="sxs-lookup"><span data-stu-id="40e85-123">After the report is generated you will be able to save and open the report in Excel.</span></span>

<span data-ttu-id="40e85-124">請注意，產生移轉結構描述時，大部分識別為「物件」的問題將會經過調整，以便立即移轉該資料。</span><span class="sxs-lookup"><span data-stu-id="40e85-124">Please note that when generating the migration schema, most issues identified as ‘Object’ will be adjusted in order to allow immediate migration of that data.</span></span> <span data-ttu-id="40e85-125">請檢閱變更的項目，確保您對所有調整項皆感到滿意後，再套用結構描述。</span><span class="sxs-lookup"><span data-stu-id="40e85-125">Please review the changes to ensure you do not want to make additional adjustments before applying the schema.</span></span>

## <a name="migrate-schema"></a><span data-ttu-id="40e85-126">移轉結構描述</span><span class="sxs-lookup"><span data-stu-id="40e85-126">Migrate schema</span></span>
<span data-ttu-id="40e85-127">連接後，選取 [移轉結構描述] 會產生所選資料表的結構描述移轉指令碼。</span><span class="sxs-lookup"><span data-stu-id="40e85-127">After connecting, selecting ‘Migrate Schema’ will generate a schema migration script for the selected tables.</span></span> <span data-ttu-id="40e85-128">此指令碼可連接資料表結構、將不相容的資料類型對應至較為相容的表單，且若使用者在移轉設定中指定的話，也將一併建立安全性認證和結構描述。</span><span class="sxs-lookup"><span data-stu-id="40e85-128">This script ports the structure of the table, maps incompatible data types to more compatible forms, and creates security credentials and schema if this is indicated by the user in the migration settings.</span></span> <span data-ttu-id="40e85-129">您可對鎖定的 SQL 資料倉儲執行個體執行此程式碼，或將它儲存至檔案、複製到剪貼簿，甚或以內嵌的方式編輯，再採取進一步的動作。</span><span class="sxs-lookup"><span data-stu-id="40e85-129">This code can be run against the targeted SQL Data Warehouse instance, saved to a file, copied to your clipboard, or even edited in-line before taking further action.</span></span>  

<span data-ttu-id="40e85-130">如前所述，移轉結構描述時，請仔細檢閱工具所做的移轉變更，以確定您已完全了解這些變更內容。</span><span class="sxs-lookup"><span data-stu-id="40e85-130">As noted above, when migrating schema review the migration changes that the tool has made in order to ensure that that you fully understand them.</span></span>  

## <a name="migrate-data"></a><span data-ttu-id="40e85-131">移轉資料</span><span class="sxs-lookup"><span data-stu-id="40e85-131">Migrate data</span></span>
<span data-ttu-id="40e85-132">按一下 [移轉資料] 選項，您就可以產生 BCP 指令碼，它會先將資料移至伺服器上的一般檔案，接著再直接移進您的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="40e85-132">By clicking the ‘Migrate Data’ option you can generate BCP scripts that will move your data first to flat files on your server, and then directly into your SQL Data Warehouse.</span></span> <span data-ttu-id="40e85-133">因為並沒有內建重試功能，且網路連線中斷可能會導致失敗，我們建議您在移動少量資料的情況下使用此程序。</span><span class="sxs-lookup"><span data-stu-id="40e85-133">We recommend this process for moving small amounts of data and, as retries are not built-in and failures may occur if there is a loss of the network connection.</span></span> <span data-ttu-id="40e85-134">若要執行此程序，您必須先安裝 BCP 命令列公用程式，且必須事先建立資料的結構描述。</span><span class="sxs-lookup"><span data-stu-id="40e85-134">In order to run this, you will need to have the BCP command-line utility installed and the schema for the data must already have been created.</span></span>

<span data-ttu-id="40e85-135">填妥上述參數之後，您只需要按一下 [執行移轉]，系統就會在您指定的位置產生兩個封裝。</span><span class="sxs-lookup"><span data-stu-id="40e85-135">After you have filled out the parameters above you simply need to click run migration and a set of two packages will be generated to your specified location.</span></span> <span data-ttu-id="40e85-136">執行匯出檔案，以將移轉來源的資料匯出至一般檔案，接著執行匯入檔案，將資料匯入 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="40e85-136">Run the export file in order to export data from your migration source into flat files, and run the import file in order to import your data into SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40e85-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="40e85-137">Next steps</span></span>
<span data-ttu-id="40e85-138">現在您已成功移轉部分資料，請繼續了解如何[開發][develop]。</span><span class="sxs-lookup"><span data-stu-id="40e85-138">Now that you've migrated some data, check out how to [develop][develop].</span></span>

<!--Image references-->

<!--Article references-->
[migration documentation]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md

<!--Other Web references--> 
[Download Migration Utility]: https://migrhoststorage.blob.core.windows.net/sqldwsample/DataWarehouseMigrationUtility.zip

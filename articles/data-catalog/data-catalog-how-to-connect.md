---
title: "如何連接到資料來源 | Microsoft Docs"
description: "操作說明文章著重在說明如何連接到使用 Azure 資料目錄找到的資料來源。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 4e6b27a5-cf75-4012-b88c-333c1fe638e8
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: fd687bb74a22b0483225c509171edaa67f1c49d4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-connect-to-data-sources"></a><span data-ttu-id="bb5df-103">如何連接到資料來源</span><span class="sxs-lookup"><span data-stu-id="bb5df-103">How to connect to data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="bb5df-104">簡介</span><span class="sxs-lookup"><span data-stu-id="bb5df-104">Introduction</span></span>
<span data-ttu-id="bb5df-105"> 是全面管理的雲端服務，可作為企業資料來源的註冊系統和探索系統。</span><span class="sxs-lookup"><span data-stu-id="bb5df-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="bb5df-106">換句話說，[Azure 資料目錄]  的重點在於協助人們探索、了解，以及使用資料來源，並可協助組織從現有的資料獲得更多價值。</span><span class="sxs-lookup"><span data-stu-id="bb5df-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations to get more value from their existing data.</span></span> <span data-ttu-id="bb5df-107">這個背景的重點就在於使用資料，也就是使用者探索資料來源並了解其用途，然後連接到資料來源將使用其資料。</span><span class="sxs-lookup"><span data-stu-id="bb5df-107">A key aspect of this scenario is using the data – once a user discovers a data source and understands its purpose, the next step is to connect to the data source to put its data to use.</span></span>

## <a name="data-source-locations"></a><span data-ttu-id="bb5df-108">資料來源位置</span><span class="sxs-lookup"><span data-stu-id="bb5df-108">Data source locations</span></span>
<span data-ttu-id="bb5df-109">資料來源在註冊期間， **Azure 資料目錄** 會收到有關資料來源的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="bb5df-109">During data source registration, **Azure Data Catalog** receives metadata about the data source.</span></span> <span data-ttu-id="bb5df-110">此中繼資料包含資料來源位置的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="bb5df-110">This metadata includes the details of the data source’s location.</span></span> <span data-ttu-id="bb5df-111">位置的詳細資料會因資料來源而異，但永遠會包含連接所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="bb5df-111">The details of the location will vary from data source to data source, but it will always contain the information needed to connect.</span></span> <span data-ttu-id="bb5df-112">例如，SQL Server 資料表的位置包含伺服器名稱、資料庫名稱、結構描述名稱和資料表名稱，而 SQL Server Reporting Services 報表的位置包含伺服器名稱和報表的路徑。</span><span class="sxs-lookup"><span data-stu-id="bb5df-112">For example, the location for a SQL Server table includes the server name, database name, schema name, and table name, while the location for a SQL Server Reporting Services report includes the server name and the path to the report.</span></span> <span data-ttu-id="bb5df-113">其他資料來源類型的位置，則會反映結構與來源系統的功能。</span><span class="sxs-lookup"><span data-stu-id="bb5df-113">Other data source types will have locations that reflect the structure and capabilities of the source system.</span></span>

## <a name="integrated-client-tools"></a><span data-ttu-id="bb5df-114">整合式用戶端工具</span><span class="sxs-lookup"><span data-stu-id="bb5df-114">Integrated client tools</span></span>
<span data-ttu-id="bb5df-115">若要連接到資料來源，最簡單的方式就是使用 [開啟於...]</span><span class="sxs-lookup"><span data-stu-id="bb5df-115">The simplest way to connect to a data source is to use the “Open in…”</span></span> <span data-ttu-id="bb5df-116">功能表 (位於 **Azure 資料目錄**入口網站)。</span><span class="sxs-lookup"><span data-stu-id="bb5df-116">menu in the **Azure Data Catalog** portal.</span></span> <span data-ttu-id="bb5df-117">這個功能表會顯示一份選項清單，可供您連接到所選取的資料資產。</span><span class="sxs-lookup"><span data-stu-id="bb5df-117">This menu displays a list of options for connecting to the selected data asset.</span></span>
<span data-ttu-id="bb5df-118">使用預設的並排顯示檢視時，此功能表位於每個磚上。</span><span class="sxs-lookup"><span data-stu-id="bb5df-118">When using the default tile view, this menu is available on the each tile.</span></span>

 ![從資料資產磚以 Excel 開啟 SQL Server 資料表](./media/data-catalog-how-to-connect/data-catalog-how-to-connect1.png)

<span data-ttu-id="bb5df-120">使用清單檢視時，此功能表位於入口網站視窗頂端的搜尋列中。</span><span class="sxs-lookup"><span data-stu-id="bb5df-120">When using the list view, the menu is available in the search bar at the top of the portal window.</span></span>

 ![從搜尋列以報告管理員開啟 SQL Server Reporting Services 報表](./media/data-catalog-how-to-connect/data-catalog-how-to-connect2.png)

## <a name="supported-client-applications"></a><span data-ttu-id="bb5df-122">支援的用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="bb5df-122">Supported Client Applications</span></span>
<span data-ttu-id="bb5df-123">在 Azure 資料目錄入口網站中</span><span class="sxs-lookup"><span data-stu-id="bb5df-123">When using the “Open in…”</span></span> <span data-ttu-id="bb5df-124">對資料來源使用 [開啟於...] 功能表時，用戶端電腦上必須已安裝正確的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="bb5df-124">menu for data sources in the Azure Data Catalog portal, the correct client application must be installed on the client computer.</span></span>

| <span data-ttu-id="bb5df-125">在應用程式中開啟</span><span class="sxs-lookup"><span data-stu-id="bb5df-125">Open in application</span></span> | <span data-ttu-id="bb5df-126">副檔名/通訊協定</span><span class="sxs-lookup"><span data-stu-id="bb5df-126">File extension / protocol</span></span> | <span data-ttu-id="bb5df-127">支援的應用程式版本</span><span class="sxs-lookup"><span data-stu-id="bb5df-127">Supported application versions</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bb5df-128">Excel</span><span class="sxs-lookup"><span data-stu-id="bb5df-128">Excel</span></span> |<span data-ttu-id="bb5df-129">.odc</span><span class="sxs-lookup"><span data-stu-id="bb5df-129">.odc</span></span> |<span data-ttu-id="bb5df-130">Excel 2010 或更新版本</span><span class="sxs-lookup"><span data-stu-id="bb5df-130">Excel 2010 or later</span></span> |
| <span data-ttu-id="bb5df-131">Excel (前 1000 個)</span><span class="sxs-lookup"><span data-stu-id="bb5df-131">Excel (Top 1000)</span></span> |<span data-ttu-id="bb5df-132">.odc</span><span class="sxs-lookup"><span data-stu-id="bb5df-132">.odc</span></span> |<span data-ttu-id="bb5df-133">Excel 2010 或更新版本</span><span class="sxs-lookup"><span data-stu-id="bb5df-133">Excel 2010 or later</span></span> |
| <span data-ttu-id="bb5df-134">Power Query</span><span class="sxs-lookup"><span data-stu-id="bb5df-134">Power Query</span></span> |<span data-ttu-id="bb5df-135">.xlsx</span><span class="sxs-lookup"><span data-stu-id="bb5df-135">.xlsx</span></span> |<span data-ttu-id="bb5df-136">安裝了 Power Query for Excel 增益集的 Excel 2016、Excel 2010 或 Excel 2013</span><span class="sxs-lookup"><span data-stu-id="bb5df-136">Excel 2016 or Excel 2010 or Excel 2013 with the Power Query for Excel add-in installed</span></span> |
| <span data-ttu-id="bb5df-137">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="bb5df-137">Power BI Desktop</span></span> |<span data-ttu-id="bb5df-138">.pbix</span><span class="sxs-lookup"><span data-stu-id="bb5df-138">.pbix</span></span> |<span data-ttu-id="bb5df-139">Power BI Desktop 2016 年 7 月或更新版本</span><span class="sxs-lookup"><span data-stu-id="bb5df-139">Power BI Desktop July 2016 or later</span></span> |
| <span data-ttu-id="bb5df-140">SQL Server Data Tools</span><span class="sxs-lookup"><span data-stu-id="bb5df-140">SQL Server Data Tools</span></span> |<span data-ttu-id="bb5df-141">vsweb://</span><span class="sxs-lookup"><span data-stu-id="bb5df-141">vsweb://</span></span> |<span data-ttu-id="bb5df-142">安裝了 SQL Server 工具的 Visual Studio 2013 Update 4 或更新版本</span><span class="sxs-lookup"><span data-stu-id="bb5df-142">Visual Studio 2013 Update 4 or later with SQL Server tooling installed</span></span> |
| <span data-ttu-id="bb5df-143">報表管理員</span><span class="sxs-lookup"><span data-stu-id="bb5df-143">Report Manager</span></span> |<span data-ttu-id="bb5df-144">http://</span><span class="sxs-lookup"><span data-stu-id="bb5df-144">http://</span></span> |<span data-ttu-id="bb5df-145">請參閱 [SQL Server Reporting Services 的瀏覽器需求](https://technet.microsoft.com/en-us/library/ms156511.aspx)</span><span class="sxs-lookup"><span data-stu-id="bb5df-145">See [browser requirements for SQL Server Reporting Services](https://technet.microsoft.com/en-us/library/ms156511.aspx)</span></span> |

## <a name="your-data-your-tools"></a><span data-ttu-id="bb5df-146">您的資料與工具</span><span class="sxs-lookup"><span data-stu-id="bb5df-146">Your data, your tools</span></span>
<span data-ttu-id="bb5df-147">功能表中可用的選項取決於目前選取的資料資產的類型。</span><span class="sxs-lookup"><span data-stu-id="bb5df-147">The options available in the menu will depend on the type of data asset currently selected.</span></span> <span data-ttu-id="bb5df-148">當然，並非所有可能的工具都將包含於 [開啟於...]</span><span class="sxs-lookup"><span data-stu-id="bb5df-148">Of course, not all possible tools will be included in the “Open in…”</span></span> <span data-ttu-id="bb5df-149">功能表中，但仍能使用任何用戶端工具輕鬆連接至資料來源。</span><span class="sxs-lookup"><span data-stu-id="bb5df-149">menu, but it is still easy to connect to the data source using any client tool.</span></span> <span data-ttu-id="bb5df-150">在 **Azure 資料目錄**入口網站中選取資料資產時，完整的位置會顯示於屬性窗格中。</span><span class="sxs-lookup"><span data-stu-id="bb5df-150">When a data asset is selected in the **Azure Data Catalog** portal, the complete location is displayed in the properties pane.</span></span>

 ![SQL Server 資料表的連接資訊](./media/data-catalog-how-to-connect/data-catalog-how-to-connect3.png)

<span data-ttu-id="bb5df-152">連接資訊的詳細資料會因資料來源的類型而異，但是入口網站中所包含的資訊提供您所需的一切，讓您可以使用任何用戶端工具連接到資料來源。</span><span class="sxs-lookup"><span data-stu-id="bb5df-152">The connection information details will differ from data source type to data source type, but the information included in the portal will give you everything you need to connect to the data source in any client tool.</span></span> <span data-ttu-id="bb5df-153">使用者可以複製他們使用 **Azure 資料目錄**所找到之資料來源的連接詳細資料，讓他們能夠使用他們選擇的工具來處理資料。</span><span class="sxs-lookup"><span data-stu-id="bb5df-153">Users can copy the connection details for the data sources that they have discovered using **Azure Data Catalog**, enabling them to work with the data in their tool of choice.</span></span>

## <a name="connecting-and-data-source-permissions"></a><span data-ttu-id="bb5df-154">連接和資料來源的權限</span><span class="sxs-lookup"><span data-stu-id="bb5df-154">Connecting and data source permissions</span></span>
<span data-ttu-id="bb5df-155">雖然 **Azure 資料目錄** 可讓資料來源變成可探索，資料本身的存取權仍受到資料來源擁有者或系統管理員的控制。</span><span class="sxs-lookup"><span data-stu-id="bb5df-155">Although **Azure Data Catalog** makes data sources discoverable, access to the data itself remains under the control of the data source owner or administrator.</span></span> <span data-ttu-id="bb5df-156">在 **Azure 資料目錄** 中探索資料來源，並不會提供使用者任何權限以存取資料來源本身。</span><span class="sxs-lookup"><span data-stu-id="bb5df-156">Discovering a data source in **Azure Data Catalog** does not give a user any permissions to access the data source itself.</span></span>

<span data-ttu-id="bb5df-157">若要讓使用者更輕鬆地探索資料來源，但不要有存取其資料的權限，使用者可以在加註資料來源時於 [要求存取] 屬性中提供資訊。</span><span class="sxs-lookup"><span data-stu-id="bb5df-157">To make it easier for users who discover a data source but do not have permission to access its data, users can provide information in the Request Access property when annotating a data source.</span></span> <span data-ttu-id="bb5df-158">這裡所提供的資訊會和入口網站中的資料來源位置資訊一起呈現，包括連結的程序或取得資料來源存取權的聯絡點。</span><span class="sxs-lookup"><span data-stu-id="bb5df-158">Information provided here – including links to the process or point of contact for gaining data source access – is presented alongside the data source location information in the portal.</span></span>

 ![具有所提供之要求存取指示的連接資訊](./media/data-catalog-how-to-connect/data-catalog-how-to-connect4.png)

## <a name="summary"></a><span data-ttu-id="bb5df-160">摘要</span><span class="sxs-lookup"><span data-stu-id="bb5df-160">Summary</span></span>
<span data-ttu-id="bb5df-161">使用 **Azure 資料目錄**註冊資料來源，即可藉由將資料來源的結構性和描述性中繼資料複製到目錄服務內，使其變成可探索的資料。</span><span class="sxs-lookup"><span data-stu-id="bb5df-161">Registering a data source with **Azure Data Catalog** makes that data discoverable by copying structural and descriptive metadata from the data source into the Catalog service.</span></span> <span data-ttu-id="bb5df-162">資料來源一經註冊且變成可探索之後，使用者就能從 **Azure 資料目錄**入口網站的 [開啟於...]</span><span class="sxs-lookup"><span data-stu-id="bb5df-162">Once a data source has been registered, and discovered, users can connect to the data source from the **Azure Data Catalog** portal “Open in…””</span></span> <span data-ttu-id="bb5df-163">功能表，或使用他們選擇的資料工具，連接到資料來源。</span><span class="sxs-lookup"><span data-stu-id="bb5df-163">menu or using their data tools of choice.</span></span>

## <a name="see-also"></a><span data-ttu-id="bb5df-164">另請參閱</span><span class="sxs-lookup"><span data-stu-id="bb5df-164">See also</span></span>
* <span data-ttu-id="bb5df-165">[開始使用 Azure 資料目錄](data-catalog-get-started.md) 教學課程，取得如何連線至資料來源的逐步詳細資料。</span><span class="sxs-lookup"><span data-stu-id="bb5df-165">[Get Started with Azure Data Catalog](data-catalog-get-started.md) tutorial for step-by-step details about how to connect to data sources.</span></span>

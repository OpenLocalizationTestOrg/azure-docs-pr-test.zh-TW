---
title: "搭配使用 Power BI 與 SQL 資料倉儲 | Microsoft Docs"
description: "搭配使用 Power BI 與 Azure SQL 資料倉儲以便開發解決方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 4b7609fc5d6ce7bf0e3bd3ebf6d8f52e93a40a75
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a><span data-ttu-id="7e850-103">搭配使用 Power BI 與 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="7e850-103">Use Power BI with SQL Data Warehouse</span></span>
<span data-ttu-id="7e850-104">在 Azure SQL Database 中，SQL Data Warehouse Direct Connect 可讓使用者充分利用功能強大的邏輯下推，以及 Power BI 的分析功能。</span><span class="sxs-lookup"><span data-stu-id="7e850-104">As with Azure SQL Database, SQL Data Warehouse Direct Connect allows user to leverage powerful logical pushdown alongside the analytical capabilities of Power BI.</span></span>  <span data-ttu-id="7e850-105">透過 Direct Connect，查詢會在您瀏覽資料時即時傳送回到您的 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="7e850-105">With Direct Connect, queries are sent back to your Azure SQL Data Warehouse in real time as you explore the data.</span></span>  <span data-ttu-id="7e850-106">這項與 SQL 資料倉儲結合的功能，可讓使用者在數分鐘內針對數 TB 的資料建立動態報表。</span><span class="sxs-lookup"><span data-stu-id="7e850-106">This, combined with the scale of SQL Data Warehouse, enables users to create dynamic reports in minutes against terabytes of data.</span></span>  <span data-ttu-id="7e850-107">此外，引入 [在 Power BI 中開啟] 按鈕可讓使用者直接將 Power BI 連接到其 SQL 資料倉儲，而不需從其他 Azure 部分收集資訊。</span><span class="sxs-lookup"><span data-stu-id="7e850-107">In addition, the introduction of the Open in Power BI button allows users to directly connect Power BI to their SQL Data Warehouse without collecting information from other parts of Azure.</span></span>

<span data-ttu-id="7e850-108">使用 Direct Connect 時，請注意：</span><span class="sxs-lookup"><span data-stu-id="7e850-108">When using Direct Connect please note:</span></span>

* <span data-ttu-id="7e850-109">在連接時指定完整的伺服器名稱 (請參閱以下內容以取得詳細資料)</span><span class="sxs-lookup"><span data-stu-id="7e850-109">Specify the fully qualified server name when connecting (see below for more details)</span></span>
* <span data-ttu-id="7e850-110">確定資料庫的防火牆規則都設定為 [允許存取 Azure 服務]。</span><span class="sxs-lookup"><span data-stu-id="7e850-110">Ensure firewall rules for the database are configured to "Allow access to Azure services".</span></span>
* <span data-ttu-id="7e850-111">每個動作 (例如選取資料行或新增篩選器) 會直接查詢資料倉儲</span><span class="sxs-lookup"><span data-stu-id="7e850-111">Every action such as selecting a column or adding a filter will  directly query the data warehouse</span></span>
* <span data-ttu-id="7e850-112">大約每隔 15 分鐘重新整理一次動態磚 (重新整理不需要排程)</span><span class="sxs-lookup"><span data-stu-id="7e850-112">Tiles are refreshed approximately every 15 minutes (refresh does not need to be scheduled)</span></span>
* <span data-ttu-id="7e850-113">問答集不適用於 Direct Connect 資料集</span><span class="sxs-lookup"><span data-stu-id="7e850-113">Q&A is not available for Direct Connect datasets</span></span>
* <span data-ttu-id="7e850-114">不會自動挑選結構描述變更</span><span class="sxs-lookup"><span data-stu-id="7e850-114">Schema changes are not picked up automatically</span></span>
* <span data-ttu-id="7e850-115">所有「直接連接」查詢都將在 2 分鐘後逾時</span><span class="sxs-lookup"><span data-stu-id="7e850-115">All Direct Connect queries will time out after 2 minutes</span></span>

<span data-ttu-id="7e850-116">隨著我們持續改善使用體驗，這些限制和助益事項可能會改變。</span><span class="sxs-lookup"><span data-stu-id="7e850-116">These restrictions and notes may change as we continue to improve the experiences.</span></span> <span data-ttu-id="7e850-117">連接的步驟如下詳述。</span><span class="sxs-lookup"><span data-stu-id="7e850-117">The steps to connect are detailed below.</span></span>  

## <a name="using-the-open-in-power-bi-button"></a><span data-ttu-id="7e850-118">使用 [在 Power BI 中開啟] 按鈕</span><span class="sxs-lookup"><span data-stu-id="7e850-118">Using the ‘Open in Power BI’ button</span></span>
<span data-ttu-id="7e850-119">使用 [在 Power BI 中開啟] 按鈕，是在 SQL 資料倉儲與 Power BI 之間移動的最簡單方式。</span><span class="sxs-lookup"><span data-stu-id="7e850-119">The easiest way to move between your SQL Data Warehouse and Power BI is with the Open in Power BI button.</span></span> <span data-ttu-id="7e850-120">此按鈕可讓您順暢地開始在 Power BI 中建立新的儀表板。</span><span class="sxs-lookup"><span data-stu-id="7e850-120">This button allows you to seamlessly begin creating new dashboards in Power BI.</span></span>  

1. <span data-ttu-id="7e850-121">若要開始進行，請瀏覽至 Azure 傳統入口網站中的 SQL 資料倉儲執行個體。</span><span class="sxs-lookup"><span data-stu-id="7e850-121">To get started navigate to your SQL Data Warehouse instance in the Azure Classic Portal.</span></span>
2. <span data-ttu-id="7e850-122">按一下 [在 Power BI 中開啟] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7e850-122">Click the 'Open in Power BI' button.</span></span>
3. <span data-ttu-id="7e850-123">如果我們無法直接將您登入，或者您沒有 Power BI 帳戶，您必須登入。</span><span class="sxs-lookup"><span data-stu-id="7e850-123">If we are not able to sign you in directly, or if you do not have a Power BI account, you will need to sign-in.</span></span>  
4. <span data-ttu-id="7e850-124">您會被導向到 SQL 資料倉儲連線頁面，其中預先填入您的 SQL 資料倉儲中的資訊。</span><span class="sxs-lookup"><span data-stu-id="7e850-124">You will be directed to the SQL Data Warehouse connection page, with the information from your SQL Data Warehouse pre-populated.</span></span>
5. <span data-ttu-id="7e850-125">輸入您的認證後，您將會完全連線到您的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="7e850-125">After entering your credentials you will be fully connected to your SQL Data Warehouse.</span></span>

## <a name="connecting-through-the-power-bi-portal"></a><span data-ttu-id="7e850-126">透過 Power BI 入口網站連接</span><span class="sxs-lookup"><span data-stu-id="7e850-126">Connecting through the Power BI portal</span></span>
<span data-ttu-id="7e850-127">除了使用 [在 Power BI 中開啟] 按鈕，使用者也可以透過 Power BI 入口網站連接至其 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="7e850-127">In addition to using the Open in Power BI button, users can also connect to their SQL Data Warehouse through the Power BI Portal.</span></span>

1. <span data-ttu-id="7e850-128">在導覽窗格的底部按一下 [取得資料]。</span><span class="sxs-lookup"><span data-stu-id="7e850-128">Click 'Get Data' at the bottom of the navigation pane.</span></span>
2. <span data-ttu-id="7e850-129">選取 [資料庫]。</span><span class="sxs-lookup"><span data-stu-id="7e850-129">Select 'Databases'.</span></span>
3. <span data-ttu-id="7e850-130">一旦進入了 [資料庫] 頁面，請選取 [Azure SQL 資料倉儲]，然後按一下 [連線]。</span><span class="sxs-lookup"><span data-stu-id="7e850-130">Once on the Databases page, select 'Azure SQL Data Warehouse' and then click 'Connect'.</span></span>
4. <span data-ttu-id="7e850-131">輸入必要的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="7e850-131">Enter the necessary connection information.</span></span>  <span data-ttu-id="7e850-132">在「Azure 入口網站」中可以找到您的伺服器名稱和資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="7e850-132">Your server name and database name can be found in the Azure Portal.</span></span>
5. <span data-ttu-id="7e850-133">會將您導向回到 Power BI 的主頁面，在您的連接已建立後，[資料集] 底下新的項目會出現，並具有執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="7e850-133">You will be directed back to the main page of Power BI and after your connection is made a new entry under 'Datasets' will appear with the name of your instance.</span></span>  
6. <span data-ttu-id="7e850-134">您可以按一下新資料集，以瀏覽您資料庫中的所有資料表和檢視。</span><span class="sxs-lookup"><span data-stu-id="7e850-134">You can click on the new dataset to explore all of the tables and views in your database.</span></span> <span data-ttu-id="7e850-135">選取資料行會將查詢送回來源，並以動態方式建立視覺效果。</span><span class="sxs-lookup"><span data-stu-id="7e850-135">Selecting a column will send a query back to the source, dynamically creating your visual.</span></span> <span data-ttu-id="7e850-136">這些視覺效果可儲存在新的報表中，並釘選回您的儀表板。</span><span class="sxs-lookup"><span data-stu-id="7e850-136">These visuals can be saved in a new report and pinned back to your dashboard.</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->

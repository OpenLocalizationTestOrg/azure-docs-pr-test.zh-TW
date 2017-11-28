---
title: "SQL 資料倉儲與 Power BI aaaUse |Microsoft 文件"
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
ms.openlocfilehash: a3a347493d07af6824a561567f05894cfe3c0471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a><span data-ttu-id="1cff9-103">搭配使用 Power BI 與 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="1cff9-103">Use Power BI with SQL Data Warehouse</span></span>
<span data-ttu-id="1cff9-104">如同 Azure SQL Database，SQL 資料倉儲直接連線可讓使用者 tooleverage 強大邏輯下推連同 hello 的 Power BI 的分析功能。</span><span class="sxs-lookup"><span data-stu-id="1cff9-104">As with Azure SQL Database, SQL Data Warehouse Direct Connect allows user tooleverage powerful logical pushdown alongside hello analytical capabilities of Power BI.</span></span>  <span data-ttu-id="1cff9-105">使用直接連接，查詢會傳送後 tooyour Azure SQL 資料倉儲即時當您瀏覽 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="1cff9-105">With Direct Connect, queries are sent back tooyour Azure SQL Data Warehouse in real time as you explore hello data.</span></span>  <span data-ttu-id="1cff9-106">此特性加 hello 小數位數 SQL 資料倉儲，可讓使用者 toocreate 動態報表以分鐘為單位依據數 tb 的資料。</span><span class="sxs-lookup"><span data-stu-id="1cff9-106">This, combined with hello scale of SQL Data Warehouse, enables users toocreate dynamic reports in minutes against terabytes of data.</span></span>  <span data-ttu-id="1cff9-107">此外，hello hello 開啟 Power BI 按鈕中導入可讓使用者 toodirectly 連接 Power BI tootheir SQL 資料倉儲，而不會收集 Azure 的其他部分的資訊。</span><span class="sxs-lookup"><span data-stu-id="1cff9-107">In addition, hello introduction of hello Open in Power BI button allows users toodirectly connect Power BI tootheir SQL Data Warehouse without collecting information from other parts of Azure.</span></span>

<span data-ttu-id="1cff9-108">使用 Direct Connect 時，請注意：</span><span class="sxs-lookup"><span data-stu-id="1cff9-108">When using Direct Connect please note:</span></span>

* <span data-ttu-id="1cff9-109">連接 （請參閱以下以取得詳細資料） 時，指定 hello 完整的伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="1cff9-109">Specify hello fully qualified server name when connecting (see below for more details)</span></span>
* <span data-ttu-id="1cff9-110">確定防火牆規則的 hello 資料庫設定太 「 允許存取 tooAzure 服務 」。</span><span class="sxs-lookup"><span data-stu-id="1cff9-110">Ensure firewall rules for hello database are configured too"Allow access tooAzure services".</span></span>
* <span data-ttu-id="1cff9-111">選取資料行或加入篩選等每一個動作，都會直接查詢 hello 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="1cff9-111">Every action such as selecting a column or adding a filter will  directly query hello data warehouse</span></span>
* <span data-ttu-id="1cff9-112">磚重新整理大約每隔 15 分鐘 （重新整理不需要 toobe 排程）</span><span class="sxs-lookup"><span data-stu-id="1cff9-112">Tiles are refreshed approximately every 15 minutes (refresh does not need toobe scheduled)</span></span>
* <span data-ttu-id="1cff9-113">問答集不適用於 Direct Connect 資料集</span><span class="sxs-lookup"><span data-stu-id="1cff9-113">Q&A is not available for Direct Connect datasets</span></span>
* <span data-ttu-id="1cff9-114">不會自動挑選結構描述變更</span><span class="sxs-lookup"><span data-stu-id="1cff9-114">Schema changes are not picked up automatically</span></span>
* <span data-ttu-id="1cff9-115">所有「直接連接」查詢都將在 2 分鐘後逾時</span><span class="sxs-lookup"><span data-stu-id="1cff9-115">All Direct Connect queries will time out after 2 minutes</span></span>

<span data-ttu-id="1cff9-116">這些限制和備註可能會隨著我們持續 tooimprove hello 體驗變更。</span><span class="sxs-lookup"><span data-stu-id="1cff9-116">These restrictions and notes may change as we continue tooimprove hello experiences.</span></span> <span data-ttu-id="1cff9-117">hello 步驟 tooconnect 如下所述。</span><span class="sxs-lookup"><span data-stu-id="1cff9-117">hello steps tooconnect are detailed below.</span></span>  

## <a name="using-hello-open-in-power-bi-button"></a><span data-ttu-id="1cff9-118">使用 hello 'Power BI 中開啟 按鈕</span><span class="sxs-lookup"><span data-stu-id="1cff9-118">Using hello ‘Open in Power BI’ button</span></span>
<span data-ttu-id="1cff9-119">您的 SQL 資料倉儲與 Power BI 之間 hello 最簡單方式 toomove 是以 hello 開啟中 Power BI 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1cff9-119">hello easiest way toomove between your SQL Data Warehouse and Power BI is with hello Open in Power BI button.</span></span> <span data-ttu-id="1cff9-120">這個按鈕可讓您 tooseamlessly 開始在 Power BI 中建立新的儀表板。</span><span class="sxs-lookup"><span data-stu-id="1cff9-120">This button allows you tooseamlessly begin creating new dashboards in Power BI.</span></span>  

1. <span data-ttu-id="1cff9-121">啟動 tooget 瀏覽 tooyour hello Azure 傳統入口網站中的 SQL 資料倉儲執行個體。</span><span class="sxs-lookup"><span data-stu-id="1cff9-121">tooget started navigate tooyour SQL Data Warehouse instance in hello Azure Classic Portal.</span></span>
2. <span data-ttu-id="1cff9-122">按一下 hello 'Power BI 中開啟 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1cff9-122">Click hello 'Open in Power BI' button.</span></span>
3. <span data-ttu-id="1cff9-123">如果我們不能 toosign 您在直接管理，或如果您沒有 Power BI 帳戶，您必須 toosign 中。</span><span class="sxs-lookup"><span data-stu-id="1cff9-123">If we are not able toosign you in directly, or if you do not have a Power BI account, you will need toosign-in.</span></span>  
4. <span data-ttu-id="1cff9-124">會將您導向 toohello SQL 資料倉儲連接頁面，您的 SQL 資料倉儲中的 hello 資訊預先填入。</span><span class="sxs-lookup"><span data-stu-id="1cff9-124">You will be directed toohello SQL Data Warehouse connection page, with hello information from your SQL Data Warehouse pre-populated.</span></span>
5. <span data-ttu-id="1cff9-125">輸入您的認證之後，您會完全連接的 tooyour SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="1cff9-125">After entering your credentials you will be fully connected tooyour SQL Data Warehouse.</span></span>

## <a name="connecting-through-hello-power-bi-portal"></a><span data-ttu-id="1cff9-126">透過 hello Power BI 入口網站連接</span><span class="sxs-lookup"><span data-stu-id="1cff9-126">Connecting through hello Power BI portal</span></span>
<span data-ttu-id="1cff9-127">加法 toousing hello 開啟 Power BI 按鈕中，使用者可以也 tootheir SQL 資料倉儲連線透過 hello Power BI 入口網站。</span><span class="sxs-lookup"><span data-stu-id="1cff9-127">In addition toousing hello Open in Power BI button, users can also connect tootheir SQL Data Warehouse through hello Power BI Portal.</span></span>

1. <span data-ttu-id="1cff9-128">按一下 在 hello hello 瀏覽窗格底部的 「 取得資料 」。</span><span class="sxs-lookup"><span data-stu-id="1cff9-128">Click 'Get Data' at hello bottom of hello navigation pane.</span></span>
2. <span data-ttu-id="1cff9-129">選取 [資料庫]。</span><span class="sxs-lookup"><span data-stu-id="1cff9-129">Select 'Databases'.</span></span>
3. <span data-ttu-id="1cff9-130">一次在 hello 資料庫頁面上，選取 [Azure SQL 資料倉儲 '，然後按一下連線]。</span><span class="sxs-lookup"><span data-stu-id="1cff9-130">Once on hello Databases page, select 'Azure SQL Data Warehouse' and then click 'Connect'.</span></span>
4. <span data-ttu-id="1cff9-131">輸入 hello 必要的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="1cff9-131">Enter hello necessary connection information.</span></span>  <span data-ttu-id="1cff9-132">Hello Azure 入口網站中可以找到您的伺服器名稱和資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="1cff9-132">Your server name and database name can be found in hello Azure Portal.</span></span>
5. <span data-ttu-id="1cff9-133">您將會導向回到 Power bi 和您的連線建立新的項目底下 '資料集' 之後 toohello 主頁面會顯示 hello 執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="1cff9-133">You will be directed back toohello main page of Power BI and after your connection is made a new entry under 'Datasets' will appear with hello name of your instance.</span></span>  
6. <span data-ttu-id="1cff9-134">您可以按一下新資料集 tooexplore hello hello 資料表和檢視您的資料庫中的所有。</span><span class="sxs-lookup"><span data-stu-id="1cff9-134">You can click on hello new dataset tooexplore all of hello tables and views in your database.</span></span> <span data-ttu-id="1cff9-135">選取資料行，將會傳送查詢後 toohello 來源，以動態方式建立視覺效果。</span><span class="sxs-lookup"><span data-stu-id="1cff9-135">Selecting a column will send a query back toohello source, dynamically creating your visual.</span></span> <span data-ttu-id="1cff9-136">這些視覺效果可儲存為新的報表，並釘選回 tooyour 儀表板。</span><span class="sxs-lookup"><span data-stu-id="1cff9-136">These visuals can be saved in a new report and pinned back tooyour dashboard.</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->

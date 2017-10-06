---
title: "aaaSQL 伺服器資料科學逐步解說使用 R、 Python 和 T-SQL |Microsoft 文件"
description: "逐步解說 hello 的範例將使用 R、 Python 和 T-SQL 中 SQL Server toodo 的預測分析。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: 009354304da6cd02c4fd3cf948b7fa7d488cc4e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-data-science-walkthroughs-using-r-python-and-t-sql"></a><span data-ttu-id="66ef9-103">使用 R、Python 和 T-SQL 的 SQL Server 資料科學逐步解說</span><span class="sxs-lookup"><span data-stu-id="66ef9-103">SQL Server data science walkthroughs using R, Python and T-SQL</span></span>

<span data-ttu-id="66ef9-104">這些逐步解說會使用 SQL Server、 SQL Server R Services 和 SQL Server Python Services toodo 預測分析。</span><span class="sxs-lookup"><span data-stu-id="66ef9-104">These walkthroughs use SQL Server, SQL Server R Services, and SQL Server Python Services toodo predictive analytics.</span></span> <span data-ttu-id="66ef9-105">R 和 Python 程式碼會部署在預存程序中。</span><span class="sxs-lookup"><span data-stu-id="66ef9-105">R and Python code is deployed in stored procedures.</span></span> <span data-ttu-id="66ef9-106">它們遵循下列 hello hello 小組資料科學程序中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="66ef9-106">They follow hello steps outlined in hello Team Data Science Process.</span></span> <span data-ttu-id="66ef9-107">如需 hello 小組資料科學程序的概觀，請參閱[資料科學程序](data-science-process-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="66ef9-107">For an overview of hello Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> 

<span data-ttu-id="66ef9-108">執行 hello 資料科學的小組流程的其他資料科學逐步解說會依照 hello**平台**它們使用：</span><span class="sxs-lookup"><span data-stu-id="66ef9-108">Additional data science walkthroughs that execute hello Team Data Science Process are grouped by hello **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-python-and-sql-queries-with-sql-server"></a><span data-ttu-id="66ef9-109">使用 Python 和 SQL 查詢搭配 SQL Server 來預測計程車小費</span><span class="sxs-lookup"><span data-stu-id="66ef9-109">Predict taxi tips using Python and SQL queries with SQL Server</span></span> 

<span data-ttu-id="66ef9-110">hello[使用 SQL Server](machine-learning-data-science-process-sql-walkthrough.md)逐步解說將示範如何建置和部署的機器學習分類和迴歸模型使用 SQL Server 和公開可用 NYC 計程車行程及價位資料集。</span><span class="sxs-lookup"><span data-stu-id="66ef9-110">hello [Use SQL Server](machine-learning-data-science-process-sql-walkthrough.md) walkthrough shows how you build and deploy machine learning classification and regression models using SQL Server and a publicly available NYC taxi trip and fare dataset.</span></span>


## <a name="predict-taxi-tips-using-microsoft-r-with-sql-server"></a><span data-ttu-id="66ef9-111">使用 Microsoft R 搭配 SQL Server 來預測計程車小費</span><span class="sxs-lookup"><span data-stu-id="66ef9-111">Predict taxi tips using Microsoft R with SQL Server</span></span> 

<span data-ttu-id="66ef9-112">hello[使用 SQL Server R Services](https://msdn.microsoft.com/library/mt612857.aspx)逐步解說提供的 R 程式碼中，SQL Server 資料，資料科學家和自訂的 SQL 函數 toobuild 和部署 R 模型 tooSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="66ef9-112">hello [Use SQL Server R Services](https://msdn.microsoft.com/library/mt612857.aspx) walkthrough provides data scientists with a combination of R code, SQL Server data, and custom SQL functions toobuild and deploy an R model tooSQL Server.</span></span> <span data-ttu-id="66ef9-113">hello 逐步解說是設計的 toointroduce R 開發人員導覽服務 （資料庫）。</span><span class="sxs-lookup"><span data-stu-id="66ef9-113">hello walkthrough is designed toointroduce R developers tooR Services (In-Database).</span></span>


## <a name="predict-taxi-tips-using-r-from-t-sql-or-stored-procedures-with-sql-server"></a><span data-ttu-id="66ef9-114">使用 T-SQL 或預存程序中的 R 搭配 SQL Server 來預測計程車小費</span><span class="sxs-lookup"><span data-stu-id="66ef9-114">Predict taxi tips using R from T-SQL or stored procedures with SQL Server</span></span>

<span data-ttu-id="66ef9-115">hello [R 和 SQL Server 的資料科學逐步解說](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/walkthrough-data-science-end-to-end-walkthrough)建置 TRANSACT-SQL 的進階的分析解決方案的體驗會提供 SQL 程式設計人員使用 SQL Server R Services toooperationalize R 解決方案。</span><span class="sxs-lookup"><span data-stu-id="66ef9-115">hello [Data science walkthrough for R and SQL Server](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/walkthrough-data-science-end-to-end-walkthrough) provides SQL programmers with experience building an advanced analytics solution with Transact-SQL using SQL Server R Services toooperationalize an R solution.</span></span> 


## <a name="predict-taxi-tips-using-python-in-sql-server-stored-procedures"></a><span data-ttu-id="66ef9-116">使用 SQL Server 預存程序中的 Python 來預測計程車小費</span><span class="sxs-lookup"><span data-stu-id="66ef9-116">Predict taxi tips using Python in SQL Server stored procedures</span></span>

<span data-ttu-id="66ef9-117">hello[使用 T-SQL 與 SQL Server Python Services](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers)逐步解說提供 SQL 程式設計者建立的機器學習中 SQL Server 方案的體驗。</span><span class="sxs-lookup"><span data-stu-id="66ef9-117">hello [Use T-SQL with SQL Server Python Services](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers) walkthrough provides SQL programmers with experience building a machine learning solution in SQL Server.</span></span> <span data-ttu-id="66ef9-118">它會示範如何 tooincorporate Python 加 Python 程式碼 toostored 程序的應用程式。</span><span class="sxs-lookup"><span data-stu-id="66ef9-118">It demonstrates how tooincorporate Python into an application by adding Python code toostored procedures.</span></span>


## <a name="next-steps"></a><span data-ttu-id="66ef9-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="66ef9-119">Next steps</span></span>

<span data-ttu-id="66ef9-120">Hello 主要元件組成 hello 資料科學的小組流程的討論，請參閱[小組資料科學程序概觀](data-science-process-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="66ef9-120">For a discussion of hello key components that comprise hello Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="66ef9-121">如需您可以使用 toostructure hello 小組資料科學程序生命週期的討論資料科學專案，請參閱[小組資料科學程序生命週期](data-science-process-lifecycle.md)。</span><span class="sxs-lookup"><span data-stu-id="66ef9-121">For a discussion of hello Team Data Science Process lifecycle that you can use toostructure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="66ef9-122">hello 生命週期概述 hello 步驟，從開始 toofinish 專案通常會遵循在執行時。</span><span class="sxs-lookup"><span data-stu-id="66ef9-122">hello lifecycle outlines hello steps, from start toofinish, that projects usually follow when they are executed.</span></span> 

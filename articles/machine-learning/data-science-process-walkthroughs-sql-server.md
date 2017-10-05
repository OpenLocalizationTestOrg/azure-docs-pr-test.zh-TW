---
title: "使用 R、Python 和 T-SQL 的 SQL Server 資料科學逐步解說 | Microsoft Docs"
description: "舉例逐步解說如何使用 SQL Server 中的 R、Python 和 T-SQL 來執行預測性分析。"
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
ms.openlocfilehash: 333fd4ee6dcdcbfd347d6b5e8cb900474f6ec8cc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="sql-server-data-science-walkthroughs-using-r-python-and-t-sql"></a><span data-ttu-id="7456b-103">使用 R、Python 和 T-SQL 的 SQL Server 資料科學逐步解說</span><span class="sxs-lookup"><span data-stu-id="7456b-103">SQL Server data science walkthroughs using R, Python and T-SQL</span></span>

<span data-ttu-id="7456b-104">這些逐步解說會使用 SQL Server、SQL Server R Services 和 SQL Server Python Services 來執行預測性分析。</span><span class="sxs-lookup"><span data-stu-id="7456b-104">These walkthroughs use SQL Server, SQL Server R Services, and SQL Server Python Services to do predictive analytics.</span></span> <span data-ttu-id="7456b-105">R 和 Python 程式碼會部署在預存程序中。</span><span class="sxs-lookup"><span data-stu-id="7456b-105">R and Python code is deployed in stored procedures.</span></span> <span data-ttu-id="7456b-106">其遵循 Team Data Science Process 中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="7456b-106">They follow the steps outlined in the Team Data Science Process.</span></span> <span data-ttu-id="7456b-107">如需 Team Data Science Process 的概觀，請參閱 [Data Science Process](data-science-process-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7456b-107">For an overview of the Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> 

<span data-ttu-id="7456b-108">執行 Team Data Science Process 的其他資料科學逐步解說是依據它們使用的**平台**來歸納整理：</span><span class="sxs-lookup"><span data-stu-id="7456b-108">Additional data science walkthroughs that execute the Team Data Science Process are grouped by the **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-python-and-sql-queries-with-sql-server"></a><span data-ttu-id="7456b-109">使用 Python 和 SQL 查詢搭配 SQL Server 來預測計程車小費</span><span class="sxs-lookup"><span data-stu-id="7456b-109">Predict taxi tips using Python and SQL queries with SQL Server</span></span> 

<span data-ttu-id="7456b-110">[使用 SQL Server](machine-learning-data-science-process-sql-walkthrough.md) 逐步解說會示範如何使用 SQL Server，針對公開使用的 NYC 計程車車程和車資資料集建置和部署機器學習服務的分類和迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="7456b-110">The [Use SQL Server](machine-learning-data-science-process-sql-walkthrough.md) walkthrough shows how you build and deploy machine learning classification and regression models using SQL Server and a publicly available NYC taxi trip and fare dataset.</span></span>


## <a name="predict-taxi-tips-using-microsoft-r-with-sql-server"></a><span data-ttu-id="7456b-111">使用 Microsoft R 搭配 SQL Server 來預測計程車小費</span><span class="sxs-lookup"><span data-stu-id="7456b-111">Predict taxi tips using Microsoft R with SQL Server</span></span> 

<span data-ttu-id="7456b-112">[使用 SQL Server R Services](https://msdn.microsoft.com/library/mt612857.aspx) 逐步解說會對資料科學家提供 R 程式碼、SQL Server 資料和自訂 SQL 函式的組合，以在 SQL Server 建置和部署 R 模型。</span><span class="sxs-lookup"><span data-stu-id="7456b-112">The [Use SQL Server R Services](https://msdn.microsoft.com/library/mt612857.aspx) walkthrough provides data scientists with a combination of R code, SQL Server data, and custom SQL functions to build and deploy an R model to SQL Server.</span></span> <span data-ttu-id="7456b-113">此逐步解說是為了向 R 開發人員介紹 R Services (資料庫內) 所設計。</span><span class="sxs-lookup"><span data-stu-id="7456b-113">The walkthrough is designed to introduce R developers to R Services (In-Database).</span></span>


## <a name="predict-taxi-tips-using-r-from-t-sql-or-stored-procedures-with-sql-server"></a><span data-ttu-id="7456b-114">使用 T-SQL 或預存程序中的 R 搭配 SQL Server 來預測計程車小費</span><span class="sxs-lookup"><span data-stu-id="7456b-114">Predict taxi tips using R from T-SQL or stored procedures with SQL Server</span></span>

<span data-ttu-id="7456b-115">[Data science walkthrough for R and SQL Server](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/walkthrough-data-science-end-to-end-walkthrough) (適用於 R 和 SQL Server 的資料科學逐步解說) 會對 SQL 程式設計人員提供使用 SQL Server R Services 來建置搭配 Transact-SQL 的進階分析解決方案的體驗，以操作 R 解決方案。</span><span class="sxs-lookup"><span data-stu-id="7456b-115">The [Data science walkthrough for R and SQL Server](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/walkthrough-data-science-end-to-end-walkthrough) provides SQL programmers with experience building an advanced analytics solution with Transact-SQL using SQL Server R Services to operationalize an R solution.</span></span> 


## <a name="predict-taxi-tips-using-python-in-sql-server-stored-procedures"></a><span data-ttu-id="7456b-116">使用 SQL Server 預存程序中的 Python 來預測計程車小費</span><span class="sxs-lookup"><span data-stu-id="7456b-116">Predict taxi tips using Python in SQL Server stored procedures</span></span>

<span data-ttu-id="7456b-117">[使用 T-SQL 與 SQL Server Python Services](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers) 逐步解說可向 SQL 程式設計師提供在 SQL Server 中建置機器學習解決方案的經驗。</span><span class="sxs-lookup"><span data-stu-id="7456b-117">The [Use T-SQL with SQL Server Python Services](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers) walkthrough provides SQL programmers with experience building a machine learning solution in SQL Server.</span></span> <span data-ttu-id="7456b-118">該逐步解說會說明如何透過將 Python 程式碼新增至預存程序，來將 Python 合併到應用程式中。</span><span class="sxs-lookup"><span data-stu-id="7456b-118">It demonstrates how to incorporate Python into an application by adding Python code to stored procedures.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7456b-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7456b-119">Next steps</span></span>

<span data-ttu-id="7456b-120">如需組成 Team Data Science Process 之主要元件的討論，請參閱 [Team Data Science Process 概觀](data-science-process-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7456b-120">For a discussion of the key components that comprise the Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="7456b-121">如需您可以用來結構化資料科學專案之 Team Data Science Process 生命週期的討論，請參閱 [Team Data Science Process 生命週期](data-science-process-lifecycle.md)。</span><span class="sxs-lookup"><span data-stu-id="7456b-121">For a discussion of the Team Data Science Process lifecycle that you can use to structure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="7456b-122">生命週期會概述專案在執行時通常會遵循之從開始到完成的步驟。</span><span class="sxs-lookup"><span data-stu-id="7456b-122">The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed.</span></span> 
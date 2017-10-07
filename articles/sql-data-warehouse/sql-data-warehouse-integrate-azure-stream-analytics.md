---
title: "SQL 資料倉儲與 Azure Stream Analytics aaaUse |Microsoft 文件"
description: "搭配使用 Azure 串流分析與 SQL 資料倉儲以便開發解決方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1278197a6764864124fd92fc672de00b83ec343f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a><span data-ttu-id="a7968-103">搭配使用 Azure 串流分析與 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="a7968-103">Use Azure Stream Analytics with SQL Data Warehouse</span></span>
<span data-ttu-id="a7968-104">Azure Stream Analytics 是完全受管理的服務，透過 hello 雲端中的資料流提供低延遲、 高可用性、 可擴充的複雜事件處理。</span><span class="sxs-lookup"><span data-stu-id="a7968-104">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="a7968-105">您可以藉由讀取了解 hello 基本概念[簡介 tooAzure Stream Analytics][Introduction tooAzure Stream Analytics]。</span><span class="sxs-lookup"><span data-stu-id="a7968-105">You can learn hello basics by reading [Introduction tooAzure Stream Analytics][Introduction tooAzure Stream Analytics].</span></span> <span data-ttu-id="a7968-106">您接著可以學 toocreate 依照資料流分析的端對端解決方案如何 hello[開始使用 Azure Stream Analytics] [ Get started using Azure Stream Analytics]教學課程。</span><span class="sxs-lookup"><span data-stu-id="a7968-106">You can then learn how toocreate an end-to-end solution with Stream Analytics by following hello [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>

<span data-ttu-id="a7968-107">在本文中，您將學習如何 toouse Azure SQL 資料倉儲資料庫做為您的資料流分析工作的輸出來源。</span><span class="sxs-lookup"><span data-stu-id="a7968-107">In this article, you will learn how toouse your Azure SQL Data Warehouse database as an output sink for your Steam Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7968-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="a7968-108">Prerequisites</span></span>
<span data-ttu-id="a7968-109">首先，執行透過下列步驟在 hello hello[開始使用 Azure Stream Analytics] [ Get started using Azure Stream Analytics]教學課程。</span><span class="sxs-lookup"><span data-stu-id="a7968-109">First, run through hello following steps in hello [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>  

1. <span data-ttu-id="a7968-110">建立事件中樞輸入</span><span class="sxs-lookup"><span data-stu-id="a7968-110">Create an Event Hub input</span></span>
2. <span data-ttu-id="a7968-111">設定並啟動事件產生器應用程式</span><span class="sxs-lookup"><span data-stu-id="a7968-111">Configure and start event generator application</span></span>
3. <span data-ttu-id="a7968-112">佈建資料流分析工作</span><span class="sxs-lookup"><span data-stu-id="a7968-112">Provision a Stream Analytics job</span></span>
4. <span data-ttu-id="a7968-113">指定工作輸入和查詢</span><span class="sxs-lookup"><span data-stu-id="a7968-113">Specify job input and query</span></span>

<span data-ttu-id="a7968-114">接著，建立 Azure SQL 資料倉儲資料庫</span><span class="sxs-lookup"><span data-stu-id="a7968-114">Then, create an Azure SQL Data Warehouse database</span></span>

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a><span data-ttu-id="a7968-115">指定工作輸出：Azure SQL 資料倉儲資料庫</span><span class="sxs-lookup"><span data-stu-id="a7968-115">Specify job output: Azure SQL Data Warehouse database</span></span>
### <a name="step-1"></a><span data-ttu-id="a7968-116">步驟 1</span><span class="sxs-lookup"><span data-stu-id="a7968-116">Step 1</span></span>
<span data-ttu-id="a7968-117">在資料流分析工作按一下**輸出**hello 頁面上，然後再按一下 hello 由上至下**加入輸出**。</span><span class="sxs-lookup"><span data-stu-id="a7968-117">In your Stream Analytics job click **OUTPUT** from hello top of hello page, and then click **ADD OUTPUT**.</span></span>

### <a name="step-2"></a><span data-ttu-id="a7968-118">步驟 2</span><span class="sxs-lookup"><span data-stu-id="a7968-118">Step 2</span></span>
<span data-ttu-id="a7968-119">選取 SQL Database，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a7968-119">Select SQL Database and click next.</span></span>

![][add-output]

### <a name="step-3"></a><span data-ttu-id="a7968-120">步驟 3</span><span class="sxs-lookup"><span data-stu-id="a7968-120">Step 3</span></span>
<span data-ttu-id="a7968-121">輸入下列值 hello 下一個頁面上的 hello:</span><span class="sxs-lookup"><span data-stu-id="a7968-121">Enter hello following values on hello next page:</span></span>

* <span data-ttu-id="a7968-122">*輸出別名*：輸入此工作輸出的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="a7968-122">*Output Alias*: Enter a friendly name for this job output.</span></span>
* <span data-ttu-id="a7968-123">訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="a7968-123">*Subscription*:</span></span>
  * <span data-ttu-id="a7968-124">如果您的 SQL 資料倉儲資料庫在 hello 相同訂用帳戶 hello 資料流分析工作，從目前的訂用帳戶中選取 使用 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="a7968-124">If your SQL Data Warehouse database is in hello same subscription as hello Stream Analytics job, select Use SQL Database from Current Subscription.</span></span>
  * <span data-ttu-id="a7968-125">如果您的資料庫是在不同的訂用帳戶中，請選取 [使用其他訂用帳戶的 SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="a7968-125">If your database is in a different subscription, select Use SQL Database from Another Subscription.</span></span>
* <span data-ttu-id="a7968-126">*資料庫*： 指定 hello 目的地資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="a7968-126">*Database*: Specify hello name of a destination database.</span></span>
* <span data-ttu-id="a7968-127">*伺服器名稱*： 指定 hello hello 您剛才指定的資料庫伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="a7968-127">*Server Name*: Specify hello server name for hello database you just specified.</span></span> <span data-ttu-id="a7968-128">您可以使用 hello Azure 傳統入口網站 toofind 這個。</span><span class="sxs-lookup"><span data-stu-id="a7968-128">You can use hello Azure Classic Portal toofind this.</span></span>

![][server-name]

* <span data-ttu-id="a7968-129">*使用者名稱*： 指定 hello 擁有 hello 資料庫的寫入權限的帳戶使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="a7968-129">*User Name*: Specify hello user name of an account that has write permissions for hello database.</span></span>
* <span data-ttu-id="a7968-130">*密碼*： 提供 hello hello 密碼指定使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a7968-130">*Password*: Provide hello password for hello specified user account.</span></span>
* <span data-ttu-id="a7968-131">*資料表*： 指定 hello 資料庫中的 hello hello 目標資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="a7968-131">*Table*: Specify hello name of hello target table in hello database.</span></span>

![][add-database]

### <a name="step-4"></a><span data-ttu-id="a7968-132">步驟 4</span><span class="sxs-lookup"><span data-stu-id="a7968-132">Step 4</span></span>
<span data-ttu-id="a7968-133">此工作輸出和 tooverify 資料流分析可以成功連線 toohello 資料庫，請按一下 hello 核取按鈕 tooadd。</span><span class="sxs-lookup"><span data-stu-id="a7968-133">Click hello check button tooadd this job output and tooverify that Stream Analytics can successfully connect toohello database.</span></span>

![][test-connection]

<span data-ttu-id="a7968-134">Hello 連線 toohello 資料庫成功時，您會看到在 hello hello 入口網站底部的通知。</span><span class="sxs-lookup"><span data-stu-id="a7968-134">When hello connection toohello database succeeds, you will see a notification at hello bottom of hello portal.</span></span> <span data-ttu-id="a7968-135">在 hello 底部 tootest hello 連線 toohello 資料庫，您可以按一下測試連接。</span><span class="sxs-lookup"><span data-stu-id="a7968-135">You can click Test Connection at hello bottom tootest hello connection toohello database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7968-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a7968-136">Next steps</span></span>
<span data-ttu-id="a7968-137">如需整合概觀，請參閱 [SQL 資料倉儲整合概觀][SQL Data Warehouse integration overview]。</span><span class="sxs-lookup"><span data-stu-id="a7968-137">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>

<span data-ttu-id="a7968-138">如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀][SQL Data Warehouse development overview]。</span><span class="sxs-lookup"><span data-stu-id="a7968-138">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction tooAzure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/

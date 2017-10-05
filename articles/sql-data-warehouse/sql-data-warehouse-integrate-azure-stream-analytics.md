---
title: "搭配使用 Azure 串流分析與 SQL 資料倉儲 | Microsoft Docs"
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
ms.openlocfilehash: 14783f0464764a11d7f03a5db1c2d63728a4cb50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a><span data-ttu-id="099b0-103">搭配使用 Azure 串流分析與 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="099b0-103">Use Azure Stream Analytics with SQL Data Warehouse</span></span>
<span data-ttu-id="099b0-104">Azure 串流分析是完全受管理的服務，可用來對雲端中的串流資料進行低延遲、高可用性、可延展的複雜事件處理。</span><span class="sxs-lookup"><span data-stu-id="099b0-104">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable complex event processing over streaming data in the cloud.</span></span> <span data-ttu-id="099b0-105">如需基本概念，請參閱 [Azure 串流分析簡介][Introduction to Azure Stream Analytics]。</span><span class="sxs-lookup"><span data-stu-id="099b0-105">You can learn the basics by reading [Introduction to Azure Stream Analytics][Introduction to Azure Stream Analytics].</span></span> <span data-ttu-id="099b0-106">您可以接著依照[開始使用 Azure 串流分析][Get started using Azure Stream Analytics]教學課程，了解如何使用串流分析建立端對端解決方案。</span><span class="sxs-lookup"><span data-stu-id="099b0-106">You can then learn how to create an end-to-end solution with Stream Analytics by following the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>

<span data-ttu-id="099b0-107">在本文中，您將學習如何使用 Azure SQL 資料倉儲資料庫做為串流分析工作的輸出接收器。</span><span class="sxs-lookup"><span data-stu-id="099b0-107">In this article, you will learn how to use your Azure SQL Data Warehouse database as an output sink for your Steam Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="099b0-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="099b0-108">Prerequisites</span></span>
<span data-ttu-id="099b0-109">首先，執行[開始使用 Azure 串流分析][Get started using Azure Stream Analytics]教學課程中的下列步驟。</span><span class="sxs-lookup"><span data-stu-id="099b0-109">First, run through the following steps in the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>  

1. <span data-ttu-id="099b0-110">建立事件中樞輸入</span><span class="sxs-lookup"><span data-stu-id="099b0-110">Create an Event Hub input</span></span>
2. <span data-ttu-id="099b0-111">設定並啟動事件產生器應用程式</span><span class="sxs-lookup"><span data-stu-id="099b0-111">Configure and start event generator application</span></span>
3. <span data-ttu-id="099b0-112">佈建資料流分析工作</span><span class="sxs-lookup"><span data-stu-id="099b0-112">Provision a Stream Analytics job</span></span>
4. <span data-ttu-id="099b0-113">指定工作輸入和查詢</span><span class="sxs-lookup"><span data-stu-id="099b0-113">Specify job input and query</span></span>

<span data-ttu-id="099b0-114">接著，建立 Azure SQL 資料倉儲資料庫</span><span class="sxs-lookup"><span data-stu-id="099b0-114">Then, create an Azure SQL Data Warehouse database</span></span>

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a><span data-ttu-id="099b0-115">指定工作輸出：Azure SQL 資料倉儲資料庫</span><span class="sxs-lookup"><span data-stu-id="099b0-115">Specify job output: Azure SQL Data Warehouse database</span></span>
### <a name="step-1"></a><span data-ttu-id="099b0-116">步驟 1</span><span class="sxs-lookup"><span data-stu-id="099b0-116">Step 1</span></span>
<span data-ttu-id="099b0-117">在串流分析工作中，按一下頁面上方的 [輸出]，然後按一下 [新增輸出]。</span><span class="sxs-lookup"><span data-stu-id="099b0-117">In your Stream Analytics job click **OUTPUT** from the top of the page, and then click **ADD OUTPUT**.</span></span>

### <a name="step-2"></a><span data-ttu-id="099b0-118">步驟 2</span><span class="sxs-lookup"><span data-stu-id="099b0-118">Step 2</span></span>
<span data-ttu-id="099b0-119">選取 SQL Database，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="099b0-119">Select SQL Database and click next.</span></span>

![][add-output]

### <a name="step-3"></a><span data-ttu-id="099b0-120">步驟 3</span><span class="sxs-lookup"><span data-stu-id="099b0-120">Step 3</span></span>
<span data-ttu-id="099b0-121">在下一頁輸入下列值：</span><span class="sxs-lookup"><span data-stu-id="099b0-121">Enter the following values on the next page:</span></span>

* <span data-ttu-id="099b0-122">*輸出別名*：輸入此工作輸出的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="099b0-122">*Output Alias*: Enter a friendly name for this job output.</span></span>
* <span data-ttu-id="099b0-123">訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="099b0-123">*Subscription*:</span></span>
  * <span data-ttu-id="099b0-124">如果 SQL 資料倉儲資料庫是在與此資料流分析工作相同的訂用帳戶中，則請選取 [使用目前訂用帳戶的 SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="099b0-124">If your SQL Data Warehouse database is in the same subscription as the Stream Analytics job, select Use SQL Database from Current Subscription.</span></span>
  * <span data-ttu-id="099b0-125">如果您的資料庫是在不同的訂用帳戶中，請選取 [使用其他訂用帳戶的 SQL Database]。</span><span class="sxs-lookup"><span data-stu-id="099b0-125">If your database is in a different subscription, select Use SQL Database from Another Subscription.</span></span>
* <span data-ttu-id="099b0-126">資料庫：指定目的地資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="099b0-126">*Database*: Specify the name of a destination database.</span></span>
* <span data-ttu-id="099b0-127">伺服器名稱：為您剛指定的資料庫指定伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="099b0-127">*Server Name*: Specify the server name for the database you just specified.</span></span> <span data-ttu-id="099b0-128">您可以使用 Azure 傳統入口網站進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="099b0-128">You can use the Azure Classic Portal to find this.</span></span>

![][server-name]

* <span data-ttu-id="099b0-129">使用者名稱：指定具有資料庫寫入權限的帳戶的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="099b0-129">*User Name*: Specify the user name of an account that has write permissions for the database.</span></span>
* <span data-ttu-id="099b0-130">密碼：提供指定之使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="099b0-130">*Password*: Provide the password for the specified user account.</span></span>
* <span data-ttu-id="099b0-131">資料表：指定資料庫中目標資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="099b0-131">*Table*: Specify the name of the target table in the database.</span></span>

![][add-database]

### <a name="step-4"></a><span data-ttu-id="099b0-132">步驟 4</span><span class="sxs-lookup"><span data-stu-id="099b0-132">Step 4</span></span>
<span data-ttu-id="099b0-133">按一下核取按鈕以新增此工作輸出，並確認串流分析可成功連接到資料庫。</span><span class="sxs-lookup"><span data-stu-id="099b0-133">Click the check button to add this job output and to verify that Stream Analytics can successfully connect to the database.</span></span>

![][test-connection]

<span data-ttu-id="099b0-134">成功連接到資料庫時，您將會在入口網站的底部看到通知。</span><span class="sxs-lookup"><span data-stu-id="099b0-134">When the connection to the database succeeds, you will see a notification at the bottom of the portal.</span></span> <span data-ttu-id="099b0-135">您可以按一下底部的 [測試連線]，以測試資料庫的連線。</span><span class="sxs-lookup"><span data-stu-id="099b0-135">You can click Test Connection at the bottom to test the connection to the database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="099b0-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="099b0-136">Next steps</span></span>
<span data-ttu-id="099b0-137">如需整合概觀，請參閱 [SQL 資料倉儲整合概觀][SQL Data Warehouse integration overview]。</span><span class="sxs-lookup"><span data-stu-id="099b0-137">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>

<span data-ttu-id="099b0-138">如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀][SQL Data Warehouse development overview]。</span><span class="sxs-lookup"><span data-stu-id="099b0-138">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction to Azure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/

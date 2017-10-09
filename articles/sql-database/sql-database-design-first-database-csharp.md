---
title: "aaaDesign 第一個 Azure SQL database-C# |Microsoft 文件"
description: "瞭解 toodesign 第一個 Azure SQL database，並以 C# 程式使用 ADO.NET 連接 tooit。"
services: sql-database
documentationcenter: 
author: MightyPen
manager: craigg-msft
editor: CarlRabeler
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 07/31/2017
ms.author: genemi;carlrab
ms.openlocfilehash: 8161de24bff1ec2fa307efa93adab2bd1b761fd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a><span data-ttu-id="6ce68-103">設計 Azure SQL Database 並連接 C&#x23; 和 ADO.NET</span><span class="sxs-lookup"><span data-stu-id="6ce68-103">Design an Azure SQL database and connect with C&#x23; and ADO.NET</span></span>

<span data-ttu-id="6ce68-104">Azure SQL Database 是關聯式資料庫做為-的中的服務 (DBaaS) hello Microsoft 雲端 ("Azure")。</span><span class="sxs-lookup"><span data-stu-id="6ce68-104">Azure SQL Database is a relational database-as-a service (DBaaS) in hello Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="6ce68-105">在本教學課程中，您會學習如何 toouse hello Azure 入口網站和 ADO.NET 與 Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="6ce68-105">In this tutorial, you learn how toouse hello Azure portal and ADO.NET with Visual Studio to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="6ce68-106">Hello Azure 入口網站中建立資料庫</span><span class="sxs-lookup"><span data-stu-id="6ce68-106">Create a database in hello Azure portal</span></span>
> * <span data-ttu-id="6ce68-107">設定在 hello Azure 入口網站中的伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="6ce68-107">Set up a server-level firewall rule in hello Azure portal</span></span>
> * <span data-ttu-id="6ce68-108">連接 toohello 資料庫與 ADO.NET 和 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6ce68-108">Connect toohello database with ADO.NET and Visual Studio</span></span>
> * <span data-ttu-id="6ce68-109">使用 ADO.NET 建立資料表</span><span class="sxs-lookup"><span data-stu-id="6ce68-109">Create tables with ADO.NET</span></span>
> * <span data-ttu-id="6ce68-110">使用 ADO.NET 插入、更新和刪除資料</span><span class="sxs-lookup"><span data-stu-id="6ce68-110">Insert, update, and delete data with ADO.NET</span></span> 
> * <span data-ttu-id="6ce68-111">使用 ADO.NET 查詢資料</span><span class="sxs-lookup"><span data-stu-id="6ce68-111">Query data ADO.NET</span></span>

<span data-ttu-id="6ce68-112">如果您沒有 Azure 訂用帳戶，請在開始之前先[建立免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="6ce68-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ce68-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="6ce68-113">Prerequisites</span></span>

<span data-ttu-id="6ce68-114">安裝 [Visual Studio Community 2017、Visual Studio Professional 2017 或 Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="6ce68-114">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

<!-- hello following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- hello following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a><span data-ttu-id="6ce68-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ce68-115">Next steps</span></span>

<span data-ttu-id="6ce68-116">在本教學課程中，您已了解基本的資料庫工作，例如建立資料庫和資料表、 載入和查詢資料，以及還原 hello 資料庫 tooa 前一個點的時間。</span><span class="sxs-lookup"><span data-stu-id="6ce68-116">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore hello database tooa previous point in time.</span></span> <span data-ttu-id="6ce68-117">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="6ce68-117">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="6ce68-118">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="6ce68-118">Create a database</span></span>
> * <span data-ttu-id="6ce68-119">設定防火牆規則</span><span class="sxs-lookup"><span data-stu-id="6ce68-119">Set up a firewall rule</span></span>
> * <span data-ttu-id="6ce68-120">連接與 toohello 資料庫[Visual Studio 和 C#](sql-database-connect-query-dotnet-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="6ce68-120">Connect toohello database with [Visual Studio and C#](sql-database-connect-query-dotnet-visual-studio.md)</span></span>
> * <span data-ttu-id="6ce68-121">建立資料表</span><span class="sxs-lookup"><span data-stu-id="6ce68-121">Create tables</span></span>
> * <span data-ttu-id="6ce68-122">插入、更新和刪除資料</span><span class="sxs-lookup"><span data-stu-id="6ce68-122">Insert, update, and delete data</span></span>
> * <span data-ttu-id="6ce68-123">查詢資料</span><span class="sxs-lookup"><span data-stu-id="6ce68-123">Query data</span></span>

<span data-ttu-id="6ce68-124">前進 toohello 下一個教學課程的 toolearn 有關移轉您的資料。</span><span class="sxs-lookup"><span data-stu-id="6ce68-124">Advance toohello next tutorial toolearn about migrating your data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="6ce68-125">移轉您的 SQL Server 資料庫 tooAzure SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="6ce68-125">Migrate your SQL Server database tooAzure SQL Database</span></span>](sql-database-migrate-your-sql-server-database.md)


---
title: "設計您的第一個 Azure SQL Database - C# | Microsoft Docs"
description: "了解如何設計您的第一個 Azure SQL Database，並透過 C# 程式使用 ADO.NET 來與它連接。"
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
ms.openlocfilehash: d9731cf5399cce6f103129ccda521f2867bd8da6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a><span data-ttu-id="ac833-103">設計 Azure SQL Database 並連接 C&#x23; 和 ADO.NET</span><span class="sxs-lookup"><span data-stu-id="ac833-103">Design an Azure SQL database and connect with C&#x23; and ADO.NET</span></span>

<span data-ttu-id="ac833-104">Azure SQL Database 是 Microsoft 雲端 ("Azure") 中的關聯式資料庫即服務 (DBaaS)。</span><span class="sxs-lookup"><span data-stu-id="ac833-104">Azure SQL Database is a relational database-as-a service (DBaaS) in the Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="ac833-105">在本教學課程裡，您將了解如何搭配使用 Visual Studio 與 Azure 入口網站和 ADO.NET 執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="ac833-105">In this tutorial, you learn how to use the Azure portal and ADO.NET with Visual Studio to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="ac833-106">在 Azure 入口網站中建立資料庫</span><span class="sxs-lookup"><span data-stu-id="ac833-106">Create a database in the Azure portal</span></span>
> * <span data-ttu-id="ac833-107">在 Azure 入口網站中設定伺服器層級的防火牆規則</span><span class="sxs-lookup"><span data-stu-id="ac833-107">Set up a server-level firewall rule in the Azure portal</span></span>
> * <span data-ttu-id="ac833-108">使用 ADO.NET 和 Visual Studio 連線到資料庫</span><span class="sxs-lookup"><span data-stu-id="ac833-108">Connect to the database with ADO.NET and Visual Studio</span></span>
> * <span data-ttu-id="ac833-109">使用 ADO.NET 建立資料表</span><span class="sxs-lookup"><span data-stu-id="ac833-109">Create tables with ADO.NET</span></span>
> * <span data-ttu-id="ac833-110">使用 ADO.NET 插入、更新和刪除資料</span><span class="sxs-lookup"><span data-stu-id="ac833-110">Insert, update, and delete data with ADO.NET</span></span> 
> * <span data-ttu-id="ac833-111">使用 ADO.NET 查詢資料</span><span class="sxs-lookup"><span data-stu-id="ac833-111">Query data ADO.NET</span></span>

<span data-ttu-id="ac833-112">如果您沒有 Azure 訂用帳戶，請在開始之前先[建立免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="ac833-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac833-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="ac833-113">Prerequisites</span></span>

<span data-ttu-id="ac833-114">安裝 [Visual Studio Community 2017、Visual Studio Professional 2017 或 Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="ac833-114">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

<!-- The following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- The following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a><span data-ttu-id="ac833-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ac833-115">Next steps</span></span>

<span data-ttu-id="ac833-116">在本教學課程中，您已了解基本的資料庫工作，例如建立資料庫和資料表、載入和查詢資料，以及將資料庫還原至先前的時間點。</span><span class="sxs-lookup"><span data-stu-id="ac833-116">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore the database to a previous point in time.</span></span> <span data-ttu-id="ac833-117">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="ac833-117">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="ac833-118">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="ac833-118">Create a database</span></span>
> * <span data-ttu-id="ac833-119">設定防火牆規則</span><span class="sxs-lookup"><span data-stu-id="ac833-119">Set up a firewall rule</span></span>
> * <span data-ttu-id="ac833-120">使用 [Visual Studio 和 C#](sql-database-connect-query-dotnet-visual-studio.md) 連線到資料庫</span><span class="sxs-lookup"><span data-stu-id="ac833-120">Connect to the database with [Visual Studio and C#](sql-database-connect-query-dotnet-visual-studio.md)</span></span>
> * <span data-ttu-id="ac833-121">建立資料表</span><span class="sxs-lookup"><span data-stu-id="ac833-121">Create tables</span></span>
> * <span data-ttu-id="ac833-122">插入、更新和刪除資料</span><span class="sxs-lookup"><span data-stu-id="ac833-122">Insert, update, and delete data</span></span>
> * <span data-ttu-id="ac833-123">查詢資料</span><span class="sxs-lookup"><span data-stu-id="ac833-123">Query data</span></span>

<span data-ttu-id="ac833-124">請前進到下一個教學課程，以了解如何移轉資料。</span><span class="sxs-lookup"><span data-stu-id="ac833-124">Advance to the next tutorial to learn about migrating your data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="ac833-125">將 SQL Server Database 移轉至 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="ac833-125">Migrate your SQL Server database to Azure SQL Database</span></span>](sql-database-migrate-your-sql-server-database.md)


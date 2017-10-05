---
title: "連線到 Azure SQL 資料倉儲 | Microsoft Docs"
description: "如何尋找您的伺服器名稱和 Azure SQL 資料倉儲的連接字串"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: e52872ca-ae74-4e25-9c56-d49c85c8d0f0
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 72c2b404e66611da421eca0dc30aa71e18c6d120
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-azure-sql-data-warehouse"></a><span data-ttu-id="4d5fa-103">連接到 Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="4d5fa-103">Connect to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="4d5fa-104">本文可協助您第一次連接到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="4d5fa-104">This article helps you get connected to SQL Data Warehouse for the first time.</span></span>

## <a name="find-your-server-name"></a><span data-ttu-id="4d5fa-105">尋找您的伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="4d5fa-105">Find your server name</span></span>
<span data-ttu-id="4d5fa-106">連接到 SQL 資料倉儲的第一個步驟是了解如何尋找您的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="4d5fa-106">The first step to connecting to SQL Data Warehouse is knowing how to find your server name.</span></span>  <span data-ttu-id="4d5fa-107">例如，下列範例中的伺服器名稱是 sample.database.windows.net。</span><span class="sxs-lookup"><span data-stu-id="4d5fa-107">For example, the server name in the following example is sample.database.windows.net.</span></span> <span data-ttu-id="4d5fa-108">若要尋找完整的伺服器名稱：</span><span class="sxs-lookup"><span data-stu-id="4d5fa-108">To find the fully qualified server name:</span></span>

1. <span data-ttu-id="4d5fa-109">移至 [Azure 入口網站][Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="4d5fa-109">Go to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="4d5fa-110">按一下 [SQL Database] </span><span class="sxs-lookup"><span data-stu-id="4d5fa-110">Click on **SQL databases**</span></span> 
3. <span data-ttu-id="4d5fa-111">按一下您想連接的資料庫。</span><span class="sxs-lookup"><span data-stu-id="4d5fa-111">Click on the database you want to connect to.</span></span>
4. <span data-ttu-id="4d5fa-112">找出完整的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="4d5fa-112">Locate the full server name.</span></span>
   
    ![完整伺服器名稱][1]

## <a name="supported-drivers-and-connection-strings"></a><span data-ttu-id="4d5fa-114">支援的驅動程式和連接字串</span><span class="sxs-lookup"><span data-stu-id="4d5fa-114">Supported drivers and connection strings</span></span>
<span data-ttu-id="4d5fa-115">Azure SQL 資料倉儲支援 [ADO.NET][ADO.NET]、[ODBC][ODBC]、[PHP][PHP] 和 [JDBC][JDBC]。</span><span class="sxs-lookup"><span data-stu-id="4d5fa-115">Azure SQL Data Warehouse supports [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP], and [JDBC][JDBC].</span></span> <span data-ttu-id="4d5fa-116">按一下上述其中一個驅動程式，以尋找最新版本和文件。</span><span class="sxs-lookup"><span data-stu-id="4d5fa-116">Click on one of the preceding drivers to find the latest version and documentation.</span></span> <span data-ttu-id="4d5fa-117">若要從 Azure 入口網站自動為您使用的驅動程式產生連接字串，您可以按一下前述範例中的 [顯示資料庫連接字串]  。</span><span class="sxs-lookup"><span data-stu-id="4d5fa-117">To automatically generate the connection string for the driver that you are using from the Azure portal, you can click on the **Show database connection strings** from the preceding example.</span></span>  <span data-ttu-id="4d5fa-118">下列一些範例顯示每個驅動程式的連接字串。</span><span class="sxs-lookup"><span data-stu-id="4d5fa-118">Following are also some examples of what a connection string looks like for each driver.</span></span>

> [!NOTE]
> <span data-ttu-id="4d5fa-119">請考慮將連線逾時設定為 300 秒，以便在短時間無法使用時能夠維持連線。</span><span class="sxs-lookup"><span data-stu-id="4d5fa-119">Consider setting the connection timeout to 300 seconds to allow your connection to survive short periods of unavailability.</span></span>
> 
> 

### <a name="adonet-connection-string-example"></a><span data-ttu-id="4d5fa-120">ADO.NET 連接字串範例</span><span class="sxs-lookup"><span data-stu-id="4d5fa-120">ADO.NET connection string example</span></span>
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

### <a name="odbc-connection-string-example"></a><span data-ttu-id="4d5fa-121">ODBC 連接字串範例</span><span class="sxs-lookup"><span data-stu-id="4d5fa-121">ODBC connection string example</span></span>
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

### <a name="php-connection-string-example"></a><span data-ttu-id="4d5fa-122">PHP 連接字串範例</span><span class="sxs-lookup"><span data-stu-id="4d5fa-122">PHP connection string example</span></span>
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting to SQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

### <a name="jdbc-connection-string-example"></a><span data-ttu-id="4d5fa-123">JDBC 連接字串範例</span><span class="sxs-lookup"><span data-stu-id="4d5fa-123">JDBC connection string example</span></span>
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

## <a name="connection-settings"></a><span data-ttu-id="4d5fa-124">連線設定</span><span class="sxs-lookup"><span data-stu-id="4d5fa-124">Connection settings</span></span>
<span data-ttu-id="4d5fa-125">SQL 資料倉儲會在連線和物件建立期間將一些設定標準化。</span><span class="sxs-lookup"><span data-stu-id="4d5fa-125">SQL Data Warehouse standardizes some settings during connection and object creation.</span></span> <span data-ttu-id="4d5fa-126">這些設定不能覆寫，其中包括︰</span><span class="sxs-lookup"><span data-stu-id="4d5fa-126">These settings cannot be overridden and include:</span></span>

| <span data-ttu-id="4d5fa-127">資料庫設定</span><span class="sxs-lookup"><span data-stu-id="4d5fa-127">Database Setting</span></span> | <span data-ttu-id="4d5fa-128">值</span><span class="sxs-lookup"><span data-stu-id="4d5fa-128">Value</span></span> |
|:--- |:--- |
| <span data-ttu-id="4d5fa-129">[ANSI_NULLS][ANSI_NULLS]</span><span class="sxs-lookup"><span data-stu-id="4d5fa-129">[ANSI_NULLS][ANSI_NULLS]</span></span> |<span data-ttu-id="4d5fa-130">開啟</span><span class="sxs-lookup"><span data-stu-id="4d5fa-130">ON</span></span> |
| <span data-ttu-id="4d5fa-131">[QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS]</span><span class="sxs-lookup"><span data-stu-id="4d5fa-131">[QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS]</span></span> |<span data-ttu-id="4d5fa-132">開啟</span><span class="sxs-lookup"><span data-stu-id="4d5fa-132">ON</span></span> |
| <span data-ttu-id="4d5fa-133">[DATEFORMAT][DATEFORMAT]</span><span class="sxs-lookup"><span data-stu-id="4d5fa-133">[DATEFORMAT][DATEFORMAT]</span></span> |<span data-ttu-id="4d5fa-134">mdy</span><span class="sxs-lookup"><span data-stu-id="4d5fa-134">mdy</span></span> |
| <span data-ttu-id="4d5fa-135">[DATEFIRST][DATEFIRST]</span><span class="sxs-lookup"><span data-stu-id="4d5fa-135">[DATEFIRST][DATEFIRST]</span></span> |<span data-ttu-id="4d5fa-136">7</span><span class="sxs-lookup"><span data-stu-id="4d5fa-136">7</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4d5fa-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4d5fa-137">Next steps</span></span>
<span data-ttu-id="4d5fa-138">若要使用 Visual Studio 連線及查詢，請參閱 [使用 Visual Studio 查詢][Query with Visual Studio]。</span><span class="sxs-lookup"><span data-stu-id="4d5fa-138">To connect and query with Visual Studio, see [Query with Visual Studio][Query with Visual Studio].</span></span> <span data-ttu-id="4d5fa-139">若要深入了解驗證選項，請參閱 [適用於 Azure SQL 資料倉儲的驗證][Authentication to Azure SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="4d5fa-139">To learn more about authentication options, see [Authentication to Azure SQL Data Warehouse][Authentication to Azure SQL Data Warehouse].</span></span>

<!--Articles-->
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[Authentication to Azure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[ADO.NET]: https://msdn.microsoft.com/library/e80y5yhx(v=vs.110).aspx
[ODBC]: https://msdn.microsoft.com/library/jj730314.aspx
[PHP]: https://msdn.microsoft.com/library/cc296172.aspx?f=255&MSPPError=-2147217396
[JDBC]: https://msdn.microsoft.com/library/mt484311(v=sql.110).aspx
[ANSI_NULLS]: https://msdn.microsoft.com/library/ms188048.aspx
[QUOTED_IDENTIFIERS]: https://msdn.microsoft.com/library/ms174393.aspx
[DATEFORMAT]: https://msdn.microsoft.com/library/ms189491.aspx
[DATEFIRST]: https://msdn.microsoft.com/library/ms181598.aspx

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->
[1]: media/sql-data-warehouse-connect-overview/get-server-name.png



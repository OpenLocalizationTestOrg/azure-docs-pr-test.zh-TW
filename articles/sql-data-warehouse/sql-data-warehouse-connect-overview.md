---
title: "aaaConnect tooAzure SQL 資料倉儲 |Microsoft 文件"
description: "如何 toofind hello 伺服器名稱和連接字串，您 tooAzure SQL 資料倉儲"
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
ms.openlocfilehash: f15e098026afb7c5efbbbfaf62b681e8cd7936bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-sql-data-warehouse"></a><span data-ttu-id="6b1de-103">連接 tooAzure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="6b1de-103">Connect tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="6b1de-104">這篇文章可協助您取得資料倉儲的連接的 tooSQL hello 第一次。</span><span class="sxs-lookup"><span data-stu-id="6b1de-104">This article helps you get connected tooSQL Data Warehouse for hello first time.</span></span>

## <a name="find-your-server-name"></a><span data-ttu-id="6b1de-105">尋找您的伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="6b1de-105">Find your server name</span></span>
<span data-ttu-id="6b1de-106">hello 知道資料倉儲的第一個步驟 tooconnecting tooSQL 如何 toofind 您的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="6b1de-106">hello first step tooconnecting tooSQL Data Warehouse is knowing how toofind your server name.</span></span>  <span data-ttu-id="6b1de-107">比方說，在下列範例中的 hello hello 伺服器名稱是 sample.database.windows.net。</span><span class="sxs-lookup"><span data-stu-id="6b1de-107">For example, hello server name in hello following example is sample.database.windows.net.</span></span> <span data-ttu-id="6b1de-108">toofind hello 完整的伺服器名稱：</span><span class="sxs-lookup"><span data-stu-id="6b1de-108">toofind hello fully qualified server name:</span></span>

1. <span data-ttu-id="6b1de-109">移 toohello [Azure 入口網站][Azure portal]。</span><span class="sxs-lookup"><span data-stu-id="6b1de-109">Go toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="6b1de-110">按一下 [SQL Database] </span><span class="sxs-lookup"><span data-stu-id="6b1de-110">Click on **SQL databases**</span></span> 
3. <span data-ttu-id="6b1de-111">按一下您想要 tooconnect hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b1de-111">Click on hello database you want tooconnect to.</span></span>
4. <span data-ttu-id="6b1de-112">找出 hello 完整的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="6b1de-112">Locate hello full server name.</span></span>
   
    ![完整伺服器名稱][1]

## <a name="supported-drivers-and-connection-strings"></a><span data-ttu-id="6b1de-114">支援的驅動程式和連接字串</span><span class="sxs-lookup"><span data-stu-id="6b1de-114">Supported drivers and connection strings</span></span>
<span data-ttu-id="6b1de-115">Azure SQL 資料倉儲支援 [ADO.NET][ADO.NET]、[ODBC][ODBC]、[PHP][PHP] 和 [JDBC][JDBC]。</span><span class="sxs-lookup"><span data-stu-id="6b1de-115">Azure SQL Data Warehouse supports [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP], and [JDBC][JDBC].</span></span> <span data-ttu-id="6b1de-116">按一下其中一個 hello 上述驅動程式 toofind hello 最新版本，且文件。</span><span class="sxs-lookup"><span data-stu-id="6b1de-116">Click on one of hello preceding drivers toofind hello latest version and documentation.</span></span> <span data-ttu-id="6b1de-117">tooautomatically 產生 hello hello 驅動程式所使用的連接字串從 hello Azure 入口網站中，您可以按一下 hello**顯示資料庫的連接字串**從前面範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="6b1de-117">tooautomatically generate hello connection string for hello driver that you are using from hello Azure portal, you can click on hello **Show database connection strings** from hello preceding example.</span></span>  <span data-ttu-id="6b1de-118">下列一些範例顯示每個驅動程式的連接字串。</span><span class="sxs-lookup"><span data-stu-id="6b1de-118">Following are also some examples of what a connection string looks like for each driver.</span></span>

> [!NOTE]
> <span data-ttu-id="6b1de-119">請考慮設定 hello 連接逾時 too300 秒 tooallow 連接 toosurvive 短期間無法使用。</span><span class="sxs-lookup"><span data-stu-id="6b1de-119">Consider setting hello connection timeout too300 seconds tooallow your connection toosurvive short periods of unavailability.</span></span>
> 
> 

### <a name="adonet-connection-string-example"></a><span data-ttu-id="6b1de-120">ADO.NET 連接字串範例</span><span class="sxs-lookup"><span data-stu-id="6b1de-120">ADO.NET connection string example</span></span>
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

### <a name="odbc-connection-string-example"></a><span data-ttu-id="6b1de-121">ODBC 連接字串範例</span><span class="sxs-lookup"><span data-stu-id="6b1de-121">ODBC connection string example</span></span>
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

### <a name="php-connection-string-example"></a><span data-ttu-id="6b1de-122">PHP 連接字串範例</span><span class="sxs-lookup"><span data-stu-id="6b1de-122">PHP connection string example</span></span>
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting tooSQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

### <a name="jdbc-connection-string-example"></a><span data-ttu-id="6b1de-123">JDBC 連接字串範例</span><span class="sxs-lookup"><span data-stu-id="6b1de-123">JDBC connection string example</span></span>
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

## <a name="connection-settings"></a><span data-ttu-id="6b1de-124">連線設定</span><span class="sxs-lookup"><span data-stu-id="6b1de-124">Connection settings</span></span>
<span data-ttu-id="6b1de-125">SQL 資料倉儲會在連線和物件建立期間將一些設定標準化。</span><span class="sxs-lookup"><span data-stu-id="6b1de-125">SQL Data Warehouse standardizes some settings during connection and object creation.</span></span> <span data-ttu-id="6b1de-126">這些設定不能覆寫，其中包括︰</span><span class="sxs-lookup"><span data-stu-id="6b1de-126">These settings cannot be overridden and include:</span></span>

| <span data-ttu-id="6b1de-127">資料庫設定</span><span class="sxs-lookup"><span data-stu-id="6b1de-127">Database Setting</span></span> | <span data-ttu-id="6b1de-128">值</span><span class="sxs-lookup"><span data-stu-id="6b1de-128">Value</span></span> |
|:--- |:--- |
| <span data-ttu-id="6b1de-129">[ANSI_NULLS][ANSI_NULLS]</span><span class="sxs-lookup"><span data-stu-id="6b1de-129">[ANSI_NULLS][ANSI_NULLS]</span></span> |<span data-ttu-id="6b1de-130">開啟</span><span class="sxs-lookup"><span data-stu-id="6b1de-130">ON</span></span> |
| <span data-ttu-id="6b1de-131">[QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS]</span><span class="sxs-lookup"><span data-stu-id="6b1de-131">[QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS]</span></span> |<span data-ttu-id="6b1de-132">開啟</span><span class="sxs-lookup"><span data-stu-id="6b1de-132">ON</span></span> |
| <span data-ttu-id="6b1de-133">[DATEFORMAT][DATEFORMAT]</span><span class="sxs-lookup"><span data-stu-id="6b1de-133">[DATEFORMAT][DATEFORMAT]</span></span> |<span data-ttu-id="6b1de-134">mdy</span><span class="sxs-lookup"><span data-stu-id="6b1de-134">mdy</span></span> |
| <span data-ttu-id="6b1de-135">[DATEFIRST][DATEFIRST]</span><span class="sxs-lookup"><span data-stu-id="6b1de-135">[DATEFIRST][DATEFIRST]</span></span> |<span data-ttu-id="6b1de-136">7</span><span class="sxs-lookup"><span data-stu-id="6b1de-136">7</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6b1de-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6b1de-137">Next steps</span></span>
<span data-ttu-id="6b1de-138">tooconnect 及查詢使用 Visual Studio，請參閱[Visual Studio 中的查詢][Query with Visual Studio]。</span><span class="sxs-lookup"><span data-stu-id="6b1de-138">tooconnect and query with Visual Studio, see [Query with Visual Studio][Query with Visual Studio].</span></span> <span data-ttu-id="6b1de-139">toolearn 進一步了解驗證選項，請參閱[驗證 tooAzure SQL 資料倉儲][Authentication tooAzure SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="6b1de-139">toolearn more about authentication options, see [Authentication tooAzure SQL Data Warehouse][Authentication tooAzure SQL Data Warehouse].</span></span>

<!--Articles-->
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[Authentication tooAzure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md

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



---
title: "aaaConnect tooSQL 資料庫使用 C 和 c + + |Microsoft 文件"
description: "使用 hello 範例此快速入門 toobuild 中的程式碼與 c + + 的現代應用程式，並使用 Azure SQL Database hello 定域機組中功能強大關聯式資料庫支援的。"
services: sql-database
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: 
ms.assetid: 07d9e0b1-3234-4f17-a252-a7559160a9db
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 03/06/2017
ms.author: edmacauley
ms.openlocfilehash: 9b581424c91bfdd93deb6914212629519a011d8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-database-using-c-and-c"></a><span data-ttu-id="b7c1a-103">連接 tooSQL 資料庫使用 C 和 c + +</span><span class="sxs-lookup"><span data-stu-id="b7c1a-103">Connect tooSQL Database using C and C++</span></span>
<span data-ttu-id="b7c1a-104">這篇文章的目標是 C 和 c + + 開發人員嘗試 tooconnect tooAzure SQL DB。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-104">This post is aimed at C and C++ developers trying tooconnect tooAzure SQL DB.</span></span> <span data-ttu-id="b7c1a-105">它會分成區段讓您可以跳最佳擷取您感興趣的 toohello > 一節。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-105">It is broken down into sections so you can jump toohello section that best captures your interest.</span></span> 

## <a name="prerequisites-for-hello-cc-tutorial"></a><span data-ttu-id="b7c1a-106">Hello C/c + + 教學課程的必要條件</span><span class="sxs-lookup"><span data-stu-id="b7c1a-106">Prerequisites for hello C/C++ tutorial</span></span>
<span data-ttu-id="b7c1a-107">請確定您擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="b7c1a-107">Make sure you have hello following items:</span></span>

* <span data-ttu-id="b7c1a-108">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-108">An active Azure account.</span></span> <span data-ttu-id="b7c1a-109">如果您沒有帳戶，您可以註冊 [免費 Azure 試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-109">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b7c1a-110">[Visual Studio](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-110">[Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="b7c1a-111">您必須安裝 hello c + + 語言元件 toobuild 並執行此範例。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-111">You must install hello C++ language components toobuild and run this sample.</span></span>
* <span data-ttu-id="b7c1a-112">[Visual Studio Linux 開發](https://visualstudiogallery.msdn.microsoft.com/725025cf-7067-45c2-8d01-1e0fd359ae6e)。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-112">[Visual Studio Linux Development](https://visualstudiogallery.msdn.microsoft.com/725025cf-7067-45c2-8d01-1e0fd359ae6e).</span></span> <span data-ttu-id="b7c1a-113">如果您正在開發 Linux 上，您也必須安裝 hello Visual Studio Linux 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-113">If you are developing on Linux, you must also install hello Visual Studio Linux extension.</span></span> 

## <span data-ttu-id="b7c1a-114"><a id="AzureSQL"></a>虛擬機器上的 Azure SQL Database 和 SQL Server</span><span class="sxs-lookup"><span data-stu-id="b7c1a-114"><a id="AzureSQL"></a>Azure SQL Database and SQL Server on virtual machines</span></span>
<span data-ttu-id="b7c1a-115">Azure SQL 建置在 Microsoft SQL Server，且是設計的 tooprovide 高可用性、 高效能和可擴充的服務。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-115">Azure SQL is built on Microsoft SQL Server and is designed tooprovide a high-availability, performant, and scalable service.</span></span> <span data-ttu-id="b7c1a-116">有許多優點 toousing SQL Azure 透過您專屬的資料庫，在內部部署上執行。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-116">There are many benefits toousing SQL Azure over your proprietary database running on premises.</span></span> <span data-ttu-id="b7c1a-117">使用 SQL Azure 不具有 tooinstall、 設定、 維護或管理您的資料庫，但只 hello 內容和資料庫的 hello 結構。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-117">With SQL Azure you don’t have tooinstall, set up, maintain, or manage your database but only hello content and hello structure of your database.</span></span> <span data-ttu-id="b7c1a-118">我們所擔心像容錯和冗餘等資料庫的一般項目皆已內建。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-118">Typical things that we worry about with databases like fault tolerance and redundancy are all built in.</span></span> 

<span data-ttu-id="b7c1a-119">Azure 目前有兩個裝載 SQL Server 工作負載的選項︰Azure SQL Database (資料庫即服務) 和虛擬機器 (VM) 上的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-119">Azure currently has two options for hosting SQL server workloads: Azure SQL database, database as a service and SQL server on Virtual Machines (VM).</span></span> <span data-ttu-id="b7c1a-120">不同之處在於 Azure SQL database 是您的新雲端型應用程式 tootake 利用 hello 節省成本的最佳選擇，並提供雲端服務的效能最佳化，我們不會收到到這兩個 hello 差異的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-120">We will not get into detail about hello differences between these two except that Azure SQL database is your best bet for new cloud-based applications tootake advantage of hello cost savings and performance optimization that cloud services provide.</span></span> <span data-ttu-id="b7c1a-121">如果您考慮移轉或擴充您內部部署應用程式 toohello 雲端，Azure 虛擬機器上的 SQL server 可能運作較合適。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-121">If you are considering migrating or extending your on-premises applications toohello cloud, SQL server on Azure virtual machine might work out better for you.</span></span> <span data-ttu-id="b7c1a-122">tookeep 事項簡單這個發行項，讓我們來建立 Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-122">tookeep things simple for this article, let's create an Azure SQL database.</span></span> 

## <span data-ttu-id="b7c1a-123"><a id="ODBC"></a>資料存取技術︰ODBC 和 OLE DB</span><span class="sxs-lookup"><span data-stu-id="b7c1a-123"><a id="ODBC"></a>Data access technologies: ODBC and OLE DB</span></span>
<span data-ttu-id="b7c1a-124">連接 tooAzure SQL 資料庫並無不同，目前有兩種方式 tooconnect toodatabases: ODBC （開放式資料庫連接） 和 OLE DB （物件連結與內嵌的資料庫）。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-124">Connecting tooAzure SQL DB is no different and currently there are two ways tooconnect toodatabases: ODBC (Open Database connectivity) and OLE DB (Object Linking and Embedding database).</span></span> <span data-ttu-id="b7c1a-125">近年來，Microsoft 已配合 [ODBC 進行原生關聯式資料存取](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-125">In recent years, Microsoft has aligned with [ODBC for native relational data access](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/).</span></span> <span data-ttu-id="b7c1a-126">ODBC 相當簡單，而且也比 OLE DB 更快速。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-126">ODBC is relatively simple, and also much faster than OLE DB.</span></span> <span data-ttu-id="b7c1a-127">hello 唯一必須注意的是 ODBC 會使用舊的 C 樣式 API。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-127">hello only caveat here is that ODBC does use an old C-style API.</span></span> 

## <span data-ttu-id="b7c1a-128"><a id="Create"></a>步驟 1：建立 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="b7c1a-128"><a id="Create"></a>Step 1:  Creating your Azure SQL Database</span></span>
<span data-ttu-id="b7c1a-129">請參閱 hello[快速入門頁面](sql-database-get-started-portal.md)toolearn 如何 toocreate 範例資料庫。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-129">See hello [getting started page](sql-database-get-started-portal.md) toolearn how toocreate a sample database.</span></span>  <span data-ttu-id="b7c1a-130">或者，您可以依照這[段簡短的兩分鐘影片](https://azure.microsoft.com/documentation/videos/azure-sql-database-create-dbs-in-seconds/)toocreate Azure SQL 資料庫使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-130">Alternatively, you can follow this [short two-minute video](https://azure.microsoft.com/documentation/videos/azure-sql-database-create-dbs-in-seconds/) toocreate an Azure SQL database using hello Azure portal.</span></span>

## <span data-ttu-id="b7c1a-131"><a id="ConnectionString"></a>步驟 2：取得連接字串</span><span class="sxs-lookup"><span data-stu-id="b7c1a-131"><a id="ConnectionString"></a>Step 2:  Get connection string</span></span>
<span data-ttu-id="b7c1a-132">您的 Azure SQL database 佈建之後，您需要 toocarry 出 hello 遵循步驟 toodetermine 連接資訊，並加入您的防火牆存取的用戶端 IP。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-132">After your Azure SQL database has been provisioned, you need toocarry out hello following steps toodetermine connection information and add your client IP for firewall access.</span></span> 

<span data-ttu-id="b7c1a-133">在[Azure 入口網站](https://portal.azure.com/)，經過 tooyour Azure SQL 資料庫的 ODBC 連接字串 hello**顯示資料庫的連接字串**列為 hello 概觀區段，為您的資料庫的組件：</span><span class="sxs-lookup"><span data-stu-id="b7c1a-133">In [Azure portal](https://portal.azure.com/), go tooyour Azure SQL database ODBC connection string by using hello **Show database connection strings** listed as a part of hello overview section for your database:</span></span> 

![ODBCConnectionString](./media/sql-database-develop-cplusplus-simple/azureportal.png)

![ODBCConnectionStringProps](./media/sql-database-develop-cplusplus-simple/dbconnection.png)

<span data-ttu-id="b7c1a-136">複製 hello hello 內容**ODBC (包括 Node.js) [SQL 驗證]**字串。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-136">Copy hello contents of hello **ODBC (Includes Node.js) [SQL authentication]** string.</span></span> <span data-ttu-id="b7c1a-137">我們會使用這個字串稍後 tooconnect 從我們的 c + + ODBC 命令列解譯器。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-137">We use this string later tooconnect from our C++ ODBC command-line interpreter.</span></span> <span data-ttu-id="b7c1a-138">這個字串提供詳細資料，例如 hello 驅動程式、 伺服器和其他資料庫的連接參數。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-138">This string provides details such as hello driver, server, and other database connection parameters.</span></span> 

## <span data-ttu-id="b7c1a-139"><a id="Firewall"></a>步驟 3： 加入您的 IP toohello 防火牆</span><span class="sxs-lookup"><span data-stu-id="b7c1a-139"><a id="Firewall"></a>Step 3:  Add your IP toohello firewall</span></span>
<span data-ttu-id="b7c1a-140">至 toohello 資料庫伺服器的防火牆 > 一節，並新增您[用戶端 IP toohello 防火牆使用這些步驟](sql-database-configure-firewall-settings.md)toomake 確定我們可以建立成功的連線：</span><span class="sxs-lookup"><span data-stu-id="b7c1a-140">Go toohello firewall section for your Database server and add your [client IP toohello firewall using these steps](sql-database-configure-firewall-settings.md) toomake sure we can establish a successful connection:</span></span> 

![AddyourIPWindow](./media/sql-database-develop-cplusplus-simple/ip.png)

<span data-ttu-id="b7c1a-142">此時，您已設定您的 Azure SQL DB 並準備好 tooconnect 從您的 c + + 程式碼。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-142">At this point, you have configured your Azure SQL DB and are ready tooconnect from your C++ code.</span></span> 

## <span data-ttu-id="b7c1a-143"><a id="Windows"></a>步驟 4：從 Windows C/C++ 應用程式連接</span><span class="sxs-lookup"><span data-stu-id="b7c1a-143"><a id="Windows"></a>Step 4: Connecting from a Windows C/C++ application</span></span>
<span data-ttu-id="b7c1a-144">您可以輕鬆地連接 tooyour[使用這個範例在 Windows 上使用 ODBC 的 Azure SQL DB](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29)與 Visual Studio 來建置。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-144">You can easily connect tooyour [Azure SQL DB using ODBC on Windows using this sample](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29) that builds with Visual Studio.</span></span> <span data-ttu-id="b7c1a-145">hello 範例會實作 ODBC 命令列解譯器可使用的 tooconnect tooour Azure SQL DB。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-145">hello sample implements an ODBC command-line interpreter that can be used tooconnect tooour Azure SQL DB.</span></span> <span data-ttu-id="b7c1a-146">這個範例會採用資料庫來源名稱 (DSN) 檔案做為命令列引數，或是 hello 我們稍早從 hello Azure 入口網站複製的詳細資訊的連接字串。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-146">This sample takes either a Database source name file (DSN) file as a command-line argument or hello verbose connection string that we copied earlier from hello Azure portal.</span></span> <span data-ttu-id="b7c1a-147">顯示 hello 這個專案的屬性頁面，並貼上 hello 連接字串，做為命令引數，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b7c1a-147">Bring up hello property page for this project and paste hello connection string as a command argument as shown here:</span></span> 

![DSN Propsfile](./media/sql-database-develop-cplusplus-simple/props.png)

<span data-ttu-id="b7c1a-149">請確定您提供您的資料庫 hello 正確的驗證詳細資料為該資料庫連接字串的一部分。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-149">Make sure you provide hello right authentication details for your database as a part of that database connection string.</span></span> 

<span data-ttu-id="b7c1a-150">啟動 hello 應用程式 toobuild 它。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-150">Launch hello application toobuild it.</span></span> <span data-ttu-id="b7c1a-151">您應該會看到下列驗證成功的連線 視窗的 hello。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-151">You should see hello following window validating a successful connection.</span></span> <span data-ttu-id="b7c1a-152">您甚至可以執行一些基本的 SQL 命令，例如**建立資料表**toovalidate 資料庫連線：</span><span class="sxs-lookup"><span data-stu-id="b7c1a-152">You can even run some basic SQL commands like **create table** toovalidate your database connectivity:</span></span>

![SQL 命令](./media/sql-database-develop-cplusplus-simple/sqlcommands.png)

<span data-ttu-id="b7c1a-154">或者，您可以建立使用 hello 精靈所不提供的任何命令引數時，會啟動的 DSN 檔案。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-154">Alternatively, you could create a DSN file using hello wizard that is launched when no command arguments are provided.</span></span> <span data-ttu-id="b7c1a-155">我們建議您也試用此選項。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-155">We recommend that you try this option as well.</span></span> <span data-ttu-id="b7c1a-156">您可以使用此 DSN 檔案進行自動化及保護您的驗證設定︰</span><span class="sxs-lookup"><span data-stu-id="b7c1a-156">You can use this DSN file for automation and protecting your authentication settings:</span></span> 

![建立 DSN 檔案](./media/sql-database-develop-cplusplus-simple/datasource.png)

<span data-ttu-id="b7c1a-158">恭喜！</span><span class="sxs-lookup"><span data-stu-id="b7c1a-158">Congratulations!</span></span> <span data-ttu-id="b7c1a-159">您現在已成功連接 tooAzure SQL Windows 上使用 c + + 和 ODBC。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-159">You have now successfully connected tooAzure SQL using C++ and ODBC on Windows.</span></span> <span data-ttu-id="b7c1a-160">您可以繼續讀取 toodo hello 相同 Linux 平台。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-160">You can continue reading toodo hello same for Linux platform as well.</span></span> 

## <span data-ttu-id="b7c1a-161"><a id="Linux"></a>步驟 5：從 Linux C/C++ 應用程式連接</span><span class="sxs-lookup"><span data-stu-id="b7c1a-161"><a id="Linux"></a>Step 5: Connecting from a Linux C/C++ application</span></span>
<span data-ttu-id="b7c1a-162">如果您沒收到 hello 新聞，但 Visual Studio 現在可讓您 toodevelop c + + Linux 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-162">In case you haven’t heard hello news yet, Visual Studio now allows you toodevelop C++ Linux application as well.</span></span> <span data-ttu-id="b7c1a-163">您可以閱讀 hello 這個新案例[對 Linux 開發的 Visual c + +](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/)部落格。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-163">You can read about this new scenario in hello [Visual C++ for Linux Development](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/) blog.</span></span> <span data-ttu-id="b7c1a-164">適用於 Linux toobuild，您需要在執行 Linux distro 遠端電腦。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-164">toobuild for Linux, you need a remote machine where your Linux distro is running.</span></span> <span data-ttu-id="b7c1a-165">如果您沒有帳戶，可以使用 [Linux Azure 虛擬機器](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)快速設定一個。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-165">If you don’t have one available, you can set one up quickly using [Linux Azure Virtual machines](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="b7c1a-166">針對本教學課程，讓我們假設您已設定 Ubuntu 16.04 Linux 散發套件。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-166">For this tutorial, let us assume that you have an Ubuntu 16.04 Linux distribution set up.</span></span> <span data-ttu-id="b7c1a-167">此處 hello 步驟應該也套用 tooUbuntu 15.10、 Red Hat 6 和 Red Hat 7。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-167">hello steps here should also apply tooUbuntu 15.10, Red Hat 6, and Red Hat 7.</span></span> 

<span data-ttu-id="b7c1a-168">hello 下列步驟安裝您 distro SQL 和 ODBC 所需的 hello 程式庫：</span><span class="sxs-lookup"><span data-stu-id="b7c1a-168">hello following steps install hello libraries needed for SQL and ODBC for your distro:</span></span>

    sudo su
    sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/mssql-ubuntu-test/ xenial main" > /etc/apt/sources.list.d/mssqlpreview.list'
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    apt-get update
    apt-get install msodbcsql
    apt-get install unixodbc-dev-utf16 #this step is optional but recommended*

<span data-ttu-id="b7c1a-169">啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-169">Launch Visual Studio.</span></span> <span data-ttu-id="b7c1a-170">在 工具-> 選項-> 跨平台-> 連接管理員，加入連接 tooyour Linux 方塊：</span><span class="sxs-lookup"><span data-stu-id="b7c1a-170">Under Tools -> Options -> Cross Platform -> Connection Manager, add a connection tooyour Linux box:</span></span> 

![工具選項](./media/sql-database-develop-cplusplus-simple/tools.png)

<span data-ttu-id="b7c1a-172">在建立透過 SSH 的連線之後，建立一個空白專案 (Linux) 範本︰</span><span class="sxs-lookup"><span data-stu-id="b7c1a-172">After connection over SSH is established, create an Empty project (Linux) template:</span></span> 

![新增專案範本](./media/sql-database-develop-cplusplus-simple/template.png)

<span data-ttu-id="b7c1a-174">接著，您可以新增[ C 原始程式檔，並取代為此內容](https://github.com/Microsoft/VCSamples/blob/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29/odbcconnector/odbcconnector.c)。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-174">You can then add a [new C source file and replace it with this content](https://github.com/Microsoft/VCSamples/blob/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29/odbcconnector/odbcconnector.c).</span></span> <span data-ttu-id="b7c1a-175">使用 ODBC Api SQLAllocHandle hello、 SQLSetConnectAttr 和 SQLDriverConnect，您也應該能夠 tooinitialize 並建立連接 tooyour 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-175">Using hello ODBC APIs SQLAllocHandle, SQLSetConnectAttr, and SQLDriverConnect, you should be able tooinitialize and establish a connection tooyour database.</span></span> <span data-ttu-id="b7c1a-176">如有 hello Windows ODBC 範例中，您需要 tooreplace hello SQLDriverConnect 呼叫 hello 詳細資料從您先前複製從 hello Azure 入口網站的資料庫連接字串參數。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-176">Like with hello Windows ODBC sample, you need tooreplace hello SQLDriverConnect call with hello details from your database connection string parameters copied from hello Azure portal previously.</span></span> 

     retcode = SQLDriverConnect(
        hdbc, NULL, "Driver=ODBC Driver 13 for SQL"
                    "Server;Server=<yourserver>;Uid=<yourusername>;Pwd=<"
                    "yourpassword>;database=<yourdatabase>",
        SQL_NTS, outstr, sizeof(outstr), &outstrlen, SQL_DRIVER_NOPROMPT);

<span data-ttu-id="b7c1a-177">編譯後 tooadd hello 最後一件事 toodo **odbc**做為程式庫相依性：</span><span class="sxs-lookup"><span data-stu-id="b7c1a-177">hello last thing toodo before compiling is tooadd **odbc** as a library dependency:</span></span> 

![新增 ODBC 做為輸入程式庫](./media/sql-database-develop-cplusplus-simple/lib.png)

<span data-ttu-id="b7c1a-179">toolaunch 應用程式從 hello hello Linux 主控台開啟**偵錯**功能表：</span><span class="sxs-lookup"><span data-stu-id="b7c1a-179">toolaunch your application, bring up hello Linux Console from hello **Debug** menu:</span></span> 

![Linux 主控台](./media/sql-database-develop-cplusplus-simple/linuxconsole.png)

<span data-ttu-id="b7c1a-181">如果您連線成功，您現在應該會看到 hello hello Linux 主控台以列印目前的資料庫名稱：</span><span class="sxs-lookup"><span data-stu-id="b7c1a-181">If your connection was successful, you should now see hello current database name printed in hello Linux Console:</span></span> 

![Linux 主控台視窗輸出](./media/sql-database-develop-cplusplus-simple/linuxconsolewindow.png)

<span data-ttu-id="b7c1a-183">恭喜！</span><span class="sxs-lookup"><span data-stu-id="b7c1a-183">Congratulations!</span></span> <span data-ttu-id="b7c1a-184">您已順利完成 hello 教學課程，可以現在連線 tooyour Azure SQL DB 從 c + + Windows 和 Linux 平台上。</span><span class="sxs-lookup"><span data-stu-id="b7c1a-184">You have successfully completed hello tutorial and can now connect tooyour Azure SQL DB from C++ on Windows and Linux platforms.</span></span>

## <span data-ttu-id="b7c1a-185"><a id="GetSolution"></a>取得 hello 完成 C/c + + 教學課程解決方案</span><span class="sxs-lookup"><span data-stu-id="b7c1a-185"><a id="GetSolution"></a>Get hello complete C/C++ tutorial solution</span></span>
<span data-ttu-id="b7c1a-186">您可以找到 hello GetStarted 方案，其中包含所有在 github 上的這篇文章中的 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="b7c1a-186">You can find hello GetStarted solution that contains all hello samples in this article at github:</span></span>

* <span data-ttu-id="b7c1a-187">[ODBC c + + Windows 範例](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29)，下載 hello Windows c + + ODBC 範例 tooconnect tooAzure SQL</span><span class="sxs-lookup"><span data-stu-id="b7c1a-187">[ODBC C++ Windows sample](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29), Download hello Windows C++ ODBC Sample tooconnect tooAzure SQL</span></span>
* <span data-ttu-id="b7c1a-188">[ODBC c + + Linux 範例](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29)，下載 hello Linux c + + ODBC 範例 tooconnect tooAzure SQL</span><span class="sxs-lookup"><span data-stu-id="b7c1a-188">[ODBC C++ Linux sample](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29), Download hello Linux C++ ODBC Sample tooconnect tooAzure SQL</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7c1a-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b7c1a-189">Next steps</span></span>
* <span data-ttu-id="b7c1a-190">檢閱 hello [SQL Database 開發概觀](sql-database-develop-overview.md)</span><span class="sxs-lookup"><span data-stu-id="b7c1a-190">Review hello [SQL Database Development Overview](sql-database-develop-overview.md)</span></span>
* <span data-ttu-id="b7c1a-191">更多有關 hello [ODBC 應用程式開發介面參考](https://docs.microsoft.com/sql/odbc/reference/syntax/odbc-api-reference/)</span><span class="sxs-lookup"><span data-stu-id="b7c1a-191">More information on hello [ODBC API Reference](https://docs.microsoft.com/sql/odbc/reference/syntax/odbc-api-reference/)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b7c1a-192">其他資源</span><span class="sxs-lookup"><span data-stu-id="b7c1a-192">Additional resources</span></span>
* [<span data-ttu-id="b7c1a-193">多租用戶 SaaS 應用程式與 Azure SQL Database 的設計模式</span><span class="sxs-lookup"><span data-stu-id="b7c1a-193">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* <span data-ttu-id="b7c1a-194">瀏覽所有 hello [SQL Database 的功能](https://azure.microsoft.com/services/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="b7c1a-194">Explore all hello [capabilities of SQL Database](https://azure.microsoft.com/services/sql-database/)</span></span>


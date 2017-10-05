---
title: "使用 C 和 C++ 連接到 SQL Database | Microsoft Docs"
description: "使用這個快速入門中的範例程式碼建置現代應用程式，這個應用程式使用 C++，並受到具有 Azure SQL Database 的雲端中之強大關聯式資料庫的支援。"
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
ms.openlocfilehash: ee7398304b7ba864eff17eb6e7d7c3777f4a9fe6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-sql-database-using-c-and-c"></a><span data-ttu-id="496ec-103">使用 C 和 C++ 連接到 SQL Database</span><span class="sxs-lookup"><span data-stu-id="496ec-103">Connect to SQL Database using C and C++</span></span>
<span data-ttu-id="496ec-104">這篇文章是以嘗試連接到 Azure SQL DB 的 C 和 C++ 開發人員為目標。</span><span class="sxs-lookup"><span data-stu-id="496ec-104">This post is aimed at C and C++ developers trying to connect to Azure SQL DB.</span></span> <span data-ttu-id="496ec-105">它會分成區段，讓您可以跳到您最感興趣的區段。</span><span class="sxs-lookup"><span data-stu-id="496ec-105">It is broken down into sections so you can jump to the section that best captures your interest.</span></span> 

## <a name="prerequisites-for-the-cc-tutorial"></a><span data-ttu-id="496ec-106">C/C++ 教學課程的必要條件</span><span class="sxs-lookup"><span data-stu-id="496ec-106">Prerequisites for the C/C++ tutorial</span></span>
<span data-ttu-id="496ec-107">請確定您具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="496ec-107">Make sure you have the following items:</span></span>

* <span data-ttu-id="496ec-108">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="496ec-108">An active Azure account.</span></span> <span data-ttu-id="496ec-109">如果您沒有帳戶，您可以註冊 [免費 Azure 試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="496ec-109">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="496ec-110">[Visual Studio](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="496ec-110">[Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="496ec-111">您必須安裝 C++ 語言元件以建置並執行此範例。</span><span class="sxs-lookup"><span data-stu-id="496ec-111">You must install the C++ language components to build and run this sample.</span></span>
* <span data-ttu-id="496ec-112">[Visual Studio Linux 開發](https://visualstudiogallery.msdn.microsoft.com/725025cf-7067-45c2-8d01-1e0fd359ae6e)。</span><span class="sxs-lookup"><span data-stu-id="496ec-112">[Visual Studio Linux Development](https://visualstudiogallery.msdn.microsoft.com/725025cf-7067-45c2-8d01-1e0fd359ae6e).</span></span> <span data-ttu-id="496ec-113">如果您要在 Linux 上進行開發，必須也安裝 Visual Studio Linux 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="496ec-113">If you are developing on Linux, you must also install the Visual Studio Linux extension.</span></span> 

## <span data-ttu-id="496ec-114"><a id="AzureSQL"></a>虛擬機器上的 Azure SQL Database 和 SQL Server</span><span class="sxs-lookup"><span data-stu-id="496ec-114"><a id="AzureSQL"></a>Azure SQL Database and SQL Server on virtual machines</span></span>
<span data-ttu-id="496ec-115">Azure SQL 建置在 Microsoft SQL Server 上，旨在提供高可用性、高效能以及可調整的服務。</span><span class="sxs-lookup"><span data-stu-id="496ec-115">Azure SQL is built on Microsoft SQL Server and is designed to provide a high-availability, performant, and scalable service.</span></span> <span data-ttu-id="496ec-116">透過內部部署上所執行的專屬資料庫來使用 SQL Azure 有許多好處。</span><span class="sxs-lookup"><span data-stu-id="496ec-116">There are many benefits to using SQL Azure over your proprietary database running on premises.</span></span> <span data-ttu-id="496ec-117">使用 SQL Azure，您無需安裝、設定、維護或管理您的資料庫，只需要資料庫的內容和結構。</span><span class="sxs-lookup"><span data-stu-id="496ec-117">With SQL Azure you don’t have to install, set up, maintain, or manage your database but only the content and the structure of your database.</span></span> <span data-ttu-id="496ec-118">我們所擔心像容錯和冗餘等資料庫的一般項目皆已內建。</span><span class="sxs-lookup"><span data-stu-id="496ec-118">Typical things that we worry about with databases like fault tolerance and redundancy are all built in.</span></span> 

<span data-ttu-id="496ec-119">Azure 目前有兩個裝載 SQL Server 工作負載的選項︰Azure SQL Database (資料庫即服務) 和虛擬機器 (VM) 上的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="496ec-119">Azure currently has two options for hosting SQL server workloads: Azure SQL database, database as a service and SQL server on Virtual Machines (VM).</span></span> <span data-ttu-id="496ec-120">我們不會詳細說明這兩個之間的差異，除非 Azure SQL Database 是您新雲端應用程式，可充分節省成本的最佳選擇，且雲端服務可提供的效能最佳化。</span><span class="sxs-lookup"><span data-stu-id="496ec-120">We will not get into detail about the differences between these two except that Azure SQL database is your best bet for new cloud-based applications to take advantage of the cost savings and performance optimization that cloud services provide.</span></span> <span data-ttu-id="496ec-121">如果您考慮將您的內部應用程式移轉或擴充至雲端，Azure 虛擬機器上的 SQL Server 可能較合適您。</span><span class="sxs-lookup"><span data-stu-id="496ec-121">If you are considering migrating or extending your on-premises applications to the cloud, SQL server on Azure virtual machine might work out better for you.</span></span> <span data-ttu-id="496ec-122">若要將本文簡化，讓我們建立 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="496ec-122">To keep things simple for this article, let's create an Azure SQL database.</span></span> 

## <span data-ttu-id="496ec-123"><a id="ODBC"></a>資料存取技術︰ODBC 和 OLE DB</span><span class="sxs-lookup"><span data-stu-id="496ec-123"><a id="ODBC"></a>Data access technologies: ODBC and OLE DB</span></span>
<span data-ttu-id="496ec-124">連接到 Azure SQL 資料庫並無不同，目前有兩種方式可連接到資料庫︰ODBC (開放式資料庫連接) 和 OLE DB (物件連結與嵌入資料庫)。</span><span class="sxs-lookup"><span data-stu-id="496ec-124">Connecting to Azure SQL DB is no different and currently there are two ways to connect to databases: ODBC (Open Database connectivity) and OLE DB (Object Linking and Embedding database).</span></span> <span data-ttu-id="496ec-125">近年來，Microsoft 已配合 [ODBC 進行原生關聯式資料存取](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)。</span><span class="sxs-lookup"><span data-stu-id="496ec-125">In recent years, Microsoft has aligned with [ODBC for native relational data access](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/).</span></span> <span data-ttu-id="496ec-126">ODBC 相當簡單，而且也比 OLE DB 更快速。</span><span class="sxs-lookup"><span data-stu-id="496ec-126">ODBC is relatively simple, and also much faster than OLE DB.</span></span> <span data-ttu-id="496ec-127">唯一必須注意的是 ODBC 會使用舊的 C 樣式 API。</span><span class="sxs-lookup"><span data-stu-id="496ec-127">The only caveat here is that ODBC does use an old C-style API.</span></span> 

## <span data-ttu-id="496ec-128"><a id="Create"></a>步驟 1：建立 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="496ec-128"><a id="Create"></a>Step 1:  Creating your Azure SQL Database</span></span>
<span data-ttu-id="496ec-129">請參閱 [快速入門頁面](sql-database-get-started-portal.md) ，以了解如何建立範例資料庫。</span><span class="sxs-lookup"><span data-stu-id="496ec-129">See the [getting started page](sql-database-get-started-portal.md) to learn how to create a sample database.</span></span>  <span data-ttu-id="496ec-130">或者，您可以依照此[兩分鐘短片](https://azure.microsoft.com/documentation/videos/azure-sql-database-create-dbs-in-seconds/)使用 Azure 入口網站建立 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="496ec-130">Alternatively, you can follow this [short two-minute video](https://azure.microsoft.com/documentation/videos/azure-sql-database-create-dbs-in-seconds/) to create an Azure SQL database using the Azure portal.</span></span>

## <span data-ttu-id="496ec-131"><a id="ConnectionString"></a>步驟 2：取得連接字串</span><span class="sxs-lookup"><span data-stu-id="496ec-131"><a id="ConnectionString"></a>Step 2:  Get connection string</span></span>
<span data-ttu-id="496ec-132">在您佈建 Azure SQL Database 之後，需要執行下列步驟來判斷連接資訊，並新增您防火牆存取的用戶端 IP。</span><span class="sxs-lookup"><span data-stu-id="496ec-132">After your Azure SQL database has been provisioned, you need to carry out the following steps to determine connection information and add your client IP for firewall access.</span></span> 

<span data-ttu-id="496ec-133">在 [Azure 入口網站](https://portal.azure.com/)中，請移至 Azure SQL Database ODBC 連接字串，方法為使用列於您資料庫概觀區段的**顯示資料庫連接字串**︰</span><span class="sxs-lookup"><span data-stu-id="496ec-133">In [Azure portal](https://portal.azure.com/), go to your Azure SQL database ODBC connection string by using the **Show database connection strings** listed as a part of the overview section for your database:</span></span> 

![ODBCConnectionString](./media/sql-database-develop-cplusplus-simple/azureportal.png)

![ODBCConnectionStringProps](./media/sql-database-develop-cplusplus-simple/dbconnection.png)

<span data-ttu-id="496ec-136">複製 **ODBC (包含 Node.js) [SQL 驗證]** 字串的內容。</span><span class="sxs-lookup"><span data-stu-id="496ec-136">Copy the contents of the **ODBC (Includes Node.js) [SQL authentication]** string.</span></span> <span data-ttu-id="496ec-137">我們稍後要使用此字串從我們的 C++ ODBC 命令列轉譯器進行連接。</span><span class="sxs-lookup"><span data-stu-id="496ec-137">We use this string later to connect from our C++ ODBC command-line interpreter.</span></span> <span data-ttu-id="496ec-138">此字串會提供詳細資料，例如驅動程式、伺服器和其他資料庫連接參數。</span><span class="sxs-lookup"><span data-stu-id="496ec-138">This string provides details such as the driver, server, and other database connection parameters.</span></span> 

## <span data-ttu-id="496ec-139"><a id="Firewall"></a>步驟 3︰將您的 IP 新增至防火牆</span><span class="sxs-lookup"><span data-stu-id="496ec-139"><a id="Firewall"></a>Step 3:  Add your IP to the firewall</span></span>
<span data-ttu-id="496ec-140">請移至您資料庫伺服器的防火牆區段，並使用下列步驟將您的[用戶端 IP 新增至防火牆](sql-database-configure-firewall-settings.md)，藉此確定我們可以建立成功的連線︰</span><span class="sxs-lookup"><span data-stu-id="496ec-140">Go to the firewall section for your Database server and add your [client IP to the firewall using these steps](sql-database-configure-firewall-settings.md) to make sure we can establish a successful connection:</span></span> 

![AddyourIPWindow](./media/sql-database-develop-cplusplus-simple/ip.png)

<span data-ttu-id="496ec-142">此時，您已設定您的 Azure SQL DB 並準備好要從您的 C++ 程式碼連線。</span><span class="sxs-lookup"><span data-stu-id="496ec-142">At this point, you have configured your Azure SQL DB and are ready to connect from your C++ code.</span></span> 

## <span data-ttu-id="496ec-143"><a id="Windows"></a>步驟 4：從 Windows C/C++ 應用程式連接</span><span class="sxs-lookup"><span data-stu-id="496ec-143"><a id="Windows"></a>Step 4: Connecting from a Windows C/C++ application</span></span>
<span data-ttu-id="496ec-144">您可以在 Windows 上使用 ODBC 輕鬆地連接到您的 [Azure SQL DB，藉由使用這個以 Visual Studio 建置的範例](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29)。</span><span class="sxs-lookup"><span data-stu-id="496ec-144">You can easily connect to your [Azure SQL DB using ODBC on Windows using this sample](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29) that builds with Visual Studio.</span></span> <span data-ttu-id="496ec-145">此範例會實作 ODBC 命令列轉譯器，可用於連接到我們的 Azure SQL DB。</span><span class="sxs-lookup"><span data-stu-id="496ec-145">The sample implements an ODBC command-line interpreter that can be used to connect to our Azure SQL DB.</span></span> <span data-ttu-id="496ec-146">這個範例會採用資料庫來源名稱 (DSN) 檔案做為命令列引數，或是我們稍早從 Azure 入口網站複製的詳細資訊連接字串。</span><span class="sxs-lookup"><span data-stu-id="496ec-146">This sample takes either a Database source name file (DSN) file as a command-line argument or the verbose connection string that we copied earlier from the Azure portal.</span></span> <span data-ttu-id="496ec-147">開啟此專案的屬性頁，然後貼上連接字串做為命令引數，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="496ec-147">Bring up the property page for this project and paste the connection string as a command argument as shown here:</span></span> 

![DSN Propsfile](./media/sql-database-develop-cplusplus-simple/props.png)

<span data-ttu-id="496ec-149">請確定您提供的資料庫驗證詳細資料是的正確，做為該資料庫連接字串的一部分。</span><span class="sxs-lookup"><span data-stu-id="496ec-149">Make sure you provide the right authentication details for your database as a part of that database connection string.</span></span> 

<span data-ttu-id="496ec-150">啟動應用程式來建置它。</span><span class="sxs-lookup"><span data-stu-id="496ec-150">Launch the application to build it.</span></span> <span data-ttu-id="496ec-151">您應該會看到下列驗證成功連線的視窗。</span><span class="sxs-lookup"><span data-stu-id="496ec-151">You should see the following window validating a successful connection.</span></span> <span data-ttu-id="496ec-152">您甚至可以執行一些基本的 SQL 命令，例如**建立資料表**來驗證您的資料庫連線︰</span><span class="sxs-lookup"><span data-stu-id="496ec-152">You can even run some basic SQL commands like **create table** to validate your database connectivity:</span></span>

![SQL 命令](./media/sql-database-develop-cplusplus-simple/sqlcommands.png)

<span data-ttu-id="496ec-154">或者，您可以使用當未提供任何命令列引數時會啟動的精靈來建立 DSN 檔案。</span><span class="sxs-lookup"><span data-stu-id="496ec-154">Alternatively, you could create a DSN file using the wizard that is launched when no command arguments are provided.</span></span> <span data-ttu-id="496ec-155">我們建議您也試用此選項。</span><span class="sxs-lookup"><span data-stu-id="496ec-155">We recommend that you try this option as well.</span></span> <span data-ttu-id="496ec-156">您可以使用此 DSN 檔案進行自動化及保護您的驗證設定︰</span><span class="sxs-lookup"><span data-stu-id="496ec-156">You can use this DSN file for automation and protecting your authentication settings:</span></span> 

![建立 DSN 檔案](./media/sql-database-develop-cplusplus-simple/datasource.png)

<span data-ttu-id="496ec-158">恭喜！</span><span class="sxs-lookup"><span data-stu-id="496ec-158">Congratulations!</span></span> <span data-ttu-id="496ec-159">您現在已在 Windows 上使用 C++ 和 ODBC 成功連接至 Azure SQL。</span><span class="sxs-lookup"><span data-stu-id="496ec-159">You have now successfully connected to Azure SQL using C++ and ODBC on Windows.</span></span> <span data-ttu-id="496ec-160">您可以繼續閱讀，針對 Linux 平台上執行相同的作業。</span><span class="sxs-lookup"><span data-stu-id="496ec-160">You can continue reading to do the same for Linux platform as well.</span></span> 

## <span data-ttu-id="496ec-161"><a id="Linux"></a>步驟 5：從 Linux C/C++ 應用程式連接</span><span class="sxs-lookup"><span data-stu-id="496ec-161"><a id="Linux"></a>Step 5: Connecting from a Linux C/C++ application</span></span>
<span data-ttu-id="496ec-162">如果您還沒聽過新聞，那麼 Visual Studio 現在也可讓您開發 C++ Linux 應用程式。</span><span class="sxs-lookup"><span data-stu-id="496ec-162">In case you haven’t heard the news yet, Visual Studio now allows you to develop C++ Linux application as well.</span></span> <span data-ttu-id="496ec-163">您可以在 [Linux 開發的 Visual C++](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/) 部落格中閱讀這個新的案例。</span><span class="sxs-lookup"><span data-stu-id="496ec-163">You can read about this new scenario in the [Visual C++ for Linux Development](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/) blog.</span></span> <span data-ttu-id="496ec-164">若要針對 Linux 建置，您需要正在執行您 Linux 散發版本的遠端電腦。</span><span class="sxs-lookup"><span data-stu-id="496ec-164">To build for Linux, you need a remote machine where your Linux distro is running.</span></span> <span data-ttu-id="496ec-165">如果您沒有帳戶，可以使用 [Linux Azure 虛擬機器](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)快速設定一個。</span><span class="sxs-lookup"><span data-stu-id="496ec-165">If you don’t have one available, you can set one up quickly using [Linux Azure Virtual machines](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="496ec-166">針對本教學課程，讓我們假設您已設定 Ubuntu 16.04 Linux 散發套件。</span><span class="sxs-lookup"><span data-stu-id="496ec-166">For this tutorial, let us assume that you have an Ubuntu 16.04 Linux distribution set up.</span></span> <span data-ttu-id="496ec-167">以下步驟應該也適用於 Ubuntu 15.10、Red Hat 6 和 Red Hat 7。</span><span class="sxs-lookup"><span data-stu-id="496ec-167">The steps here should also apply to Ubuntu 15.10, Red Hat 6, and Red Hat 7.</span></span> 

<span data-ttu-id="496ec-168">下列步驟會安裝適用於您散發的 SQL 和 ODBC 所需的程式庫︰</span><span class="sxs-lookup"><span data-stu-id="496ec-168">The following steps install the libraries needed for SQL and ODBC for your distro:</span></span>

    sudo su
    sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/mssql-ubuntu-test/ xenial main" > /etc/apt/sources.list.d/mssqlpreview.list'
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    apt-get update
    apt-get install msodbcsql
    apt-get install unixodbc-dev-utf16 #this step is optional but recommended*

<span data-ttu-id="496ec-169">啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="496ec-169">Launch Visual Studio.</span></span> <span data-ttu-id="496ec-170">在 [工具] -> [選項] -> [跨平台] -> [連線管理員] 下，將連線新增至 Linux 方塊︰</span><span class="sxs-lookup"><span data-stu-id="496ec-170">Under Tools -> Options -> Cross Platform -> Connection Manager, add a connection to your Linux box:</span></span> 

![工具選項](./media/sql-database-develop-cplusplus-simple/tools.png)

<span data-ttu-id="496ec-172">在建立透過 SSH 的連線之後，建立一個空白專案 (Linux) 範本︰</span><span class="sxs-lookup"><span data-stu-id="496ec-172">After connection over SSH is established, create an Empty project (Linux) template:</span></span> 

![新增專案範本](./media/sql-database-develop-cplusplus-simple/template.png)

<span data-ttu-id="496ec-174">接著，您可以新增[ C 原始程式檔，並取代為此內容](https://github.com/Microsoft/VCSamples/blob/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29/odbcconnector/odbcconnector.c)。</span><span class="sxs-lookup"><span data-stu-id="496ec-174">You can then add a [new C source file and replace it with this content](https://github.com/Microsoft/VCSamples/blob/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29/odbcconnector/odbcconnector.c).</span></span> <span data-ttu-id="496ec-175">使用 ODBC API SQLAllocHandle、SQLSetConnectAttr 和 SQLDriverConnect，您應該能夠初始化並建立您資料庫的連接。</span><span class="sxs-lookup"><span data-stu-id="496ec-175">Using the ODBC APIs SQLAllocHandle, SQLSetConnectAttr, and SQLDriverConnect, you should be able to initialize and establish a connection to your database.</span></span> <span data-ttu-id="496ec-176">像是利用 Windows ODBC 範例，您需要將 SQLDriverConnect 呼叫取代為您先前從 Azure 入口網站複製的資料庫連接字串參數的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="496ec-176">Like with the Windows ODBC sample, you need to replace the SQLDriverConnect call with the details from your database connection string parameters copied from the Azure portal previously.</span></span> 

     retcode = SQLDriverConnect(
        hdbc, NULL, "Driver=ODBC Driver 13 for SQL"
                    "Server;Server=<yourserver>;Uid=<yourusername>;Pwd=<"
                    "yourpassword>;database=<yourdatabase>",
        SQL_NTS, outstr, sizeof(outstr), &outstrlen, SQL_DRIVER_NOPROMPT);

<span data-ttu-id="496ec-177">在編譯之前最後一件要做的事是新增 **odbc** 做為程式庫相依性︰</span><span class="sxs-lookup"><span data-stu-id="496ec-177">The last thing to do before compiling is to add **odbc** as a library dependency:</span></span> 

![新增 ODBC 做為輸入程式庫](./media/sql-database-develop-cplusplus-simple/lib.png)

<span data-ttu-id="496ec-179">若要啟動您的應用程式，從**偵錯**功能表開啟 Linux 主控台︰</span><span class="sxs-lookup"><span data-stu-id="496ec-179">To launch your application, bring up the Linux Console from the **Debug** menu:</span></span> 

![Linux 主控台](./media/sql-database-develop-cplusplus-simple/linuxconsole.png)

<span data-ttu-id="496ec-181">如果您的連線成功，現在應該會看到在 Linux 主控台列印的目前資料庫名稱︰</span><span class="sxs-lookup"><span data-stu-id="496ec-181">If your connection was successful, you should now see the current database name printed in the Linux Console:</span></span> 

![Linux 主控台視窗輸出](./media/sql-database-develop-cplusplus-simple/linuxconsolewindow.png)

<span data-ttu-id="496ec-183">恭喜！</span><span class="sxs-lookup"><span data-stu-id="496ec-183">Congratulations!</span></span> <span data-ttu-id="496ec-184">您已順利完成本教學課程，現在可以在 Windows 和 Linux 平台上從 C++ 連線到您的 Azure SQL DB。</span><span class="sxs-lookup"><span data-stu-id="496ec-184">You have successfully completed the tutorial and can now connect to your Azure SQL DB from C++ on Windows and Linux platforms.</span></span>

## <span data-ttu-id="496ec-185"><a id="GetSolution"></a>取得完整的 C/C++ 教學課程方案</span><span class="sxs-lookup"><span data-stu-id="496ec-185"><a id="GetSolution"></a>Get the complete C/C++ tutorial solution</span></span>
<span data-ttu-id="496ec-186">您可以在 GitHub 中找到包含本文中所有範例的 GetStarted 方案：</span><span class="sxs-lookup"><span data-stu-id="496ec-186">You can find the GetStarted solution that contains all the samples in this article at github:</span></span>

* <span data-ttu-id="496ec-187">[ODBC C++ Windows 範例](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29)，下載 Windows C++ ODBC 範例以連接到 Azure SQL</span><span class="sxs-lookup"><span data-stu-id="496ec-187">[ODBC C++ Windows sample](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29), Download the Windows C++ ODBC Sample to connect to Azure SQL</span></span>
* <span data-ttu-id="496ec-188">[ 範例](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29)，下載 Linux C++ ODBC 範例以連接到 Azure SQL</span><span class="sxs-lookup"><span data-stu-id="496ec-188">[ODBC C++ Linux sample](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29), Download the Linux C++ ODBC Sample to connect to Azure SQL</span></span>

## <a name="next-steps"></a><span data-ttu-id="496ec-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="496ec-189">Next steps</span></span>
* <span data-ttu-id="496ec-190">檢閱 [SQL Database 開發概觀](sql-database-develop-overview.md)</span><span class="sxs-lookup"><span data-stu-id="496ec-190">Review the [SQL Database Development Overview](sql-database-develop-overview.md)</span></span>
* <span data-ttu-id="496ec-191">更多 [ODBC API 參考](https://docs.microsoft.com/sql/odbc/reference/syntax/odbc-api-reference/)的相關資訊</span><span class="sxs-lookup"><span data-stu-id="496ec-191">More information on the [ODBC API Reference](https://docs.microsoft.com/sql/odbc/reference/syntax/odbc-api-reference/)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="496ec-192">其他資源</span><span class="sxs-lookup"><span data-stu-id="496ec-192">Additional resources</span></span>
* [<span data-ttu-id="496ec-193">多租用戶 SaaS 應用程式與 Azure SQL Database 的設計模式</span><span class="sxs-lookup"><span data-stu-id="496ec-193">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* <span data-ttu-id="496ec-194">瀏覽所有 [SQL Database 的能力](https://azure.microsoft.com/services/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="496ec-194">Explore all the [capabilities of SQL Database](https://azure.microsoft.com/services/sql-database/)</span></span>


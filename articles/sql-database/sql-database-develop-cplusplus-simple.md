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
# <a name="connect-toosql-database-using-c-and-c"></a>連接 tooSQL 資料庫使用 C 和 c + +
這篇文章的目標是 C 和 c + + 開發人員嘗試 tooconnect tooAzure SQL DB。 它會分成區段讓您可以跳最佳擷取您感興趣的 toohello > 一節。 

## <a name="prerequisites-for-hello-cc-tutorial"></a>Hello C/c + + 教學課程的必要條件
請確定您擁有 hello 下列項目：

* 使用中的 Azure 帳戶。 如果您沒有帳戶，您可以註冊 [免費 Azure 試用](https://azure.microsoft.com/pricing/free-trial/)。
* [Visual Studio](https://www.visualstudio.com/downloads/)。 您必須安裝 hello c + + 語言元件 toobuild 並執行此範例。
* [Visual Studio Linux 開發](https://visualstudiogallery.msdn.microsoft.com/725025cf-7067-45c2-8d01-1e0fd359ae6e)。 如果您正在開發 Linux 上，您也必須安裝 hello Visual Studio Linux 擴充功能。 

## <a id="AzureSQL"></a>虛擬機器上的 Azure SQL Database 和 SQL Server
Azure SQL 建置在 Microsoft SQL Server，且是設計的 tooprovide 高可用性、 高效能和可擴充的服務。 有許多優點 toousing SQL Azure 透過您專屬的資料庫，在內部部署上執行。 使用 SQL Azure 不具有 tooinstall、 設定、 維護或管理您的資料庫，但只 hello 內容和資料庫的 hello 結構。 我們所擔心像容錯和冗餘等資料庫的一般項目皆已內建。 

Azure 目前有兩個裝載 SQL Server 工作負載的選項︰Azure SQL Database (資料庫即服務) 和虛擬機器 (VM) 上的 SQL Server。 不同之處在於 Azure SQL database 是您的新雲端型應用程式 tootake 利用 hello 節省成本的最佳選擇，並提供雲端服務的效能最佳化，我們不會收到到這兩個 hello 差異的詳細資料。 如果您考慮移轉或擴充您內部部署應用程式 toohello 雲端，Azure 虛擬機器上的 SQL server 可能運作較合適。 tookeep 事項簡單這個發行項，讓我們來建立 Azure SQL database。 

## <a id="ODBC"></a>資料存取技術︰ODBC 和 OLE DB
連接 tooAzure SQL 資料庫並無不同，目前有兩種方式 tooconnect toodatabases: ODBC （開放式資料庫連接） 和 OLE DB （物件連結與內嵌的資料庫）。 近年來，Microsoft 已配合 [ODBC 進行原生關聯式資料存取](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)。 ODBC 相當簡單，而且也比 OLE DB 更快速。 hello 唯一必須注意的是 ODBC 會使用舊的 C 樣式 API。 

## <a id="Create"></a>步驟 1：建立 Azure SQL Database
請參閱 hello[快速入門頁面](sql-database-get-started-portal.md)toolearn 如何 toocreate 範例資料庫。  或者，您可以依照這[段簡短的兩分鐘影片](https://azure.microsoft.com/documentation/videos/azure-sql-database-create-dbs-in-seconds/)toocreate Azure SQL 資料庫使用 hello Azure 入口網站。

## <a id="ConnectionString"></a>步驟 2：取得連接字串
您的 Azure SQL database 佈建之後，您需要 toocarry 出 hello 遵循步驟 toodetermine 連接資訊，並加入您的防火牆存取的用戶端 IP。 

在[Azure 入口網站](https://portal.azure.com/)，經過 tooyour Azure SQL 資料庫的 ODBC 連接字串 hello**顯示資料庫的連接字串**列為 hello 概觀區段，為您的資料庫的組件： 

![ODBCConnectionString](./media/sql-database-develop-cplusplus-simple/azureportal.png)

![ODBCConnectionStringProps](./media/sql-database-develop-cplusplus-simple/dbconnection.png)

複製 hello hello 內容**ODBC (包括 Node.js) [SQL 驗證]**字串。 我們會使用這個字串稍後 tooconnect 從我們的 c + + ODBC 命令列解譯器。 這個字串提供詳細資料，例如 hello 驅動程式、 伺服器和其他資料庫的連接參數。 

## <a id="Firewall"></a>步驟 3： 加入您的 IP toohello 防火牆
至 toohello 資料庫伺服器的防火牆 > 一節，並新增您[用戶端 IP toohello 防火牆使用這些步驟](sql-database-configure-firewall-settings.md)toomake 確定我們可以建立成功的連線： 

![AddyourIPWindow](./media/sql-database-develop-cplusplus-simple/ip.png)

此時，您已設定您的 Azure SQL DB 並準備好 tooconnect 從您的 c + + 程式碼。 

## <a id="Windows"></a>步驟 4：從 Windows C/C++ 應用程式連接
您可以輕鬆地連接 tooyour[使用這個範例在 Windows 上使用 ODBC 的 Azure SQL DB](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29)與 Visual Studio 來建置。 hello 範例會實作 ODBC 命令列解譯器可使用的 tooconnect tooour Azure SQL DB。 這個範例會採用資料庫來源名稱 (DSN) 檔案做為命令列引數，或是 hello 我們稍早從 hello Azure 入口網站複製的詳細資訊的連接字串。 顯示 hello 這個專案的屬性頁面，並貼上 hello 連接字串，做為命令引數，如下所示： 

![DSN Propsfile](./media/sql-database-develop-cplusplus-simple/props.png)

請確定您提供您的資料庫 hello 正確的驗證詳細資料為該資料庫連接字串的一部分。 

啟動 hello 應用程式 toobuild 它。 您應該會看到下列驗證成功的連線 視窗的 hello。 您甚至可以執行一些基本的 SQL 命令，例如**建立資料表**toovalidate 資料庫連線：

![SQL 命令](./media/sql-database-develop-cplusplus-simple/sqlcommands.png)

或者，您可以建立使用 hello 精靈所不提供的任何命令引數時，會啟動的 DSN 檔案。 我們建議您也試用此選項。 您可以使用此 DSN 檔案進行自動化及保護您的驗證設定︰ 

![建立 DSN 檔案](./media/sql-database-develop-cplusplus-simple/datasource.png)

恭喜！ 您現在已成功連接 tooAzure SQL Windows 上使用 c + + 和 ODBC。 您可以繼續讀取 toodo hello 相同 Linux 平台。 

## <a id="Linux"></a>步驟 5：從 Linux C/C++ 應用程式連接
如果您沒收到 hello 新聞，但 Visual Studio 現在可讓您 toodevelop c + + Linux 應用程式。 您可以閱讀 hello 這個新案例[對 Linux 開發的 Visual c + +](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/)部落格。 適用於 Linux toobuild，您需要在執行 Linux distro 遠端電腦。 如果您沒有帳戶，可以使用 [Linux Azure 虛擬機器](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)快速設定一個。 

針對本教學課程，讓我們假設您已設定 Ubuntu 16.04 Linux 散發套件。 此處 hello 步驟應該也套用 tooUbuntu 15.10、 Red Hat 6 和 Red Hat 7。 

hello 下列步驟安裝您 distro SQL 和 ODBC 所需的 hello 程式庫：

    sudo su
    sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/mssql-ubuntu-test/ xenial main" > /etc/apt/sources.list.d/mssqlpreview.list'
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    apt-get update
    apt-get install msodbcsql
    apt-get install unixodbc-dev-utf16 #this step is optional but recommended*

啟動 Visual Studio。 在 工具-> 選項-> 跨平台-> 連接管理員，加入連接 tooyour Linux 方塊： 

![工具選項](./media/sql-database-develop-cplusplus-simple/tools.png)

在建立透過 SSH 的連線之後，建立一個空白專案 (Linux) 範本︰ 

![新增專案範本](./media/sql-database-develop-cplusplus-simple/template.png)

接著，您可以新增[ C 原始程式檔，並取代為此內容](https://github.com/Microsoft/VCSamples/blob/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29/odbcconnector/odbcconnector.c)。 使用 ODBC Api SQLAllocHandle hello、 SQLSetConnectAttr 和 SQLDriverConnect，您也應該能夠 tooinitialize 並建立連接 tooyour 資料庫。 如有 hello Windows ODBC 範例中，您需要 tooreplace hello SQLDriverConnect 呼叫 hello 詳細資料從您先前複製從 hello Azure 入口網站的資料庫連接字串參數。 

     retcode = SQLDriverConnect(
        hdbc, NULL, "Driver=ODBC Driver 13 for SQL"
                    "Server;Server=<yourserver>;Uid=<yourusername>;Pwd=<"
                    "yourpassword>;database=<yourdatabase>",
        SQL_NTS, outstr, sizeof(outstr), &outstrlen, SQL_DRIVER_NOPROMPT);

編譯後 tooadd hello 最後一件事 toodo **odbc**做為程式庫相依性： 

![新增 ODBC 做為輸入程式庫](./media/sql-database-develop-cplusplus-simple/lib.png)

toolaunch 應用程式從 hello hello Linux 主控台開啟**偵錯**功能表： 

![Linux 主控台](./media/sql-database-develop-cplusplus-simple/linuxconsole.png)

如果您連線成功，您現在應該會看到 hello hello Linux 主控台以列印目前的資料庫名稱： 

![Linux 主控台視窗輸出](./media/sql-database-develop-cplusplus-simple/linuxconsolewindow.png)

恭喜！ 您已順利完成 hello 教學課程，可以現在連線 tooyour Azure SQL DB 從 c + + Windows 和 Linux 平台上。

## <a id="GetSolution"></a>取得 hello 完成 C/c + + 教學課程解決方案
您可以找到 hello GetStarted 方案，其中包含所有在 github 上的這篇文章中的 hello 範例：

* [ODBC c + + Windows 範例](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29)，下載 hello Windows c + + ODBC 範例 tooconnect tooAzure SQL
* [ODBC c + + Linux 範例](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29)，下載 hello Linux c + + ODBC 範例 tooconnect tooAzure SQL

## <a name="next-steps"></a>後續步驟
* 檢閱 hello [SQL Database 開發概觀](sql-database-develop-overview.md)
* 更多有關 hello [ODBC 應用程式開發介面參考](https://docs.microsoft.com/sql/odbc/reference/syntax/odbc-api-reference/)

## <a name="additional-resources"></a>其他資源
* [多租用戶 SaaS 應用程式與 Azure SQL Database 的設計模式](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* 瀏覽所有 hello [SQL Database 的功能](https://azure.microsoft.com/services/sql-database/)


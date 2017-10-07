---
title: "用於使用 Go MySQL 連接 tooAzure 資料庫 |Microsoft 文件"
description: "本快速入門會提供數個移至程式碼範例，您可以使用 tooconnect 和查詢資料從 Azure 資料庫的 MySQL。"
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: go
ms.topic: hero-article
ms.date: 07/18/2017
ms.openlocfilehash: e8067b807ee729e04850c5325f476806bcd54983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-go-language-tooconnect-and-query-data"></a><span data-ttu-id="9d7cb-103">Azure 資料庫的 MySQL： 使用 Go 語言 tooconnect 和查詢資料</span><span class="sxs-lookup"><span data-stu-id="9d7cb-103">Azure Database for MySQL: Use Go language tooconnect and query data</span></span>
<span data-ttu-id="9d7cb-104">本快速入門示範如何使用 MySQL tooconnect tooan Azure 資料庫程式碼撰寫的 hello[移](https://golang.org/)從 Windows、 Ubuntu Linux 和 Apple macOS 平台的語言。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using code written in hello [Go](https://golang.org/) language from Windows, Ubuntu Linux, and Apple macOS platforms.</span></span> <span data-ttu-id="9d7cb-105">它會顯示 toouse SQL 陳述式 tooquery，如何插入、 更新和刪除 hello 資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="9d7cb-106">本文假設您熟悉開發使用 Go，但是，您就可以與 MySQL 的 Azure 資料庫的新 tooworking。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-106">This article assumes you are familiar with development using Go, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d7cb-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="9d7cb-107">Prerequisites</span></span>
<span data-ttu-id="9d7cb-108">本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：</span><span class="sxs-lookup"><span data-stu-id="9d7cb-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="9d7cb-109">使用 Azure 入口網站建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="9d7cb-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="9d7cb-110">使用 Azure CLI 建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="9d7cb-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-go-and-mysql-connector"></a><span data-ttu-id="9d7cb-111">安裝 Go 與 MySQL 連接器</span><span class="sxs-lookup"><span data-stu-id="9d7cb-111">Install Go and MySQL connector</span></span>
<span data-ttu-id="9d7cb-112">安裝[移](https://golang.org/doc/install)和 hello [go sql-驅動程式的 MySQL](https://github.com/go-sql-driver/mysql#installation)自己電腦上。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-112">Install [Go](https://golang.org/doc/install) and hello [go-sql-driver for MySQL](https://github.com/go-sql-driver/mysql#installation) on your own machine.</span></span> <span data-ttu-id="9d7cb-113">根據您的平台，請依照下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="9d7cb-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="9d7cb-114">Windows</span><span class="sxs-lookup"><span data-stu-id="9d7cb-114">Windows</span></span>
1. <span data-ttu-id="9d7cb-115">[下載](https://golang.org/dl/)並安裝 Microsoft windows 根據 toohello Go[安裝指示](https://golang.org/doc/install)。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according toohello [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="9d7cb-116">啟動 hello 從 hello [開始] 功能表的命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-116">Launch hello command prompt from hello start menu.</span></span>
3. <span data-ttu-id="9d7cb-117">為您的專案產生資料夾，例如</span><span class="sxs-lookup"><span data-stu-id="9d7cb-117">Make a folder for your project such.</span></span> <span data-ttu-id="9d7cb-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`.</span></span>
4. <span data-ttu-id="9d7cb-119">將目錄變更至 hello 專案資料夾中，例如`cd %USERPROFILE%\go\src\mysqlgo`。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-119">Change directory into hello project folder, such as `cd %USERPROFILE%\go\src\mysqlgo`.</span></span>
5. <span data-ttu-id="9d7cb-120">設定 GOPATH toopoint toohello 原始程式碼目錄的 hello 環境變數。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-120">Set hello environment variable for GOPATH toopoint toohello source code directory.</span></span> <span data-ttu-id="9d7cb-121">`set GOPATH=%USERPROFILE%\go`。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="9d7cb-122">安裝 hello [go sql-驅動程式的 mysql](https://github.com/go-sql-driver/mysql#installation)執行 hello`go get github.com/go-sql-driver/mysql`命令。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-122">Install hello [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running hello `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="9d7cb-123">在 [摘要] 安裝到]，然後 hello 命令提示字元中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="9d7cb-123">In summary, install Go, then run these commands in hello command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\mysqlgo
   cd %USERPROFILE%\go\src\mysqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/go-sql-driver/mysql
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="9d7cb-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="9d7cb-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="9d7cb-125">啟動 hello Bash 殼層。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-125">Launch hello Bash shell.</span></span> 
2. <span data-ttu-id="9d7cb-126">執行 `sudo apt-get install golang-go` 以安裝 Go。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="9d7cb-127">在主目錄中為您的專案產生資料夾，例如 `mkdir -p ~/go/src/mysqlgo/`。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="9d7cb-128">將目錄變更至 hello 資料夾中，例如`cd ~/go/src/mysqlgo/`。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-128">Change directory into hello folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="9d7cb-129">設定 hello GOPATH 環境變數 toopoint tooa 有效的來源目錄，例如您目前的首頁目錄移資料夾。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-129">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="9d7cb-130">在 [hello bash 殼層中，執行`export GOPATH=~/go`tooadd hello 走向 hello GOPATH hello 目前的殼層工作階段目錄。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-130">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="9d7cb-131">安裝 hello [go sql-驅動程式的 mysql](https://github.com/go-sql-driver/mysql#installation)執行 hello`go get github.com/go-sql-driver/mysql`命令。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-131">Install hello [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running hello `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="9d7cb-132">總而言之，就是執行下列 bash 命令：</span><span class="sxs-lookup"><span data-stu-id="9d7cb-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

### <a name="apple-macos"></a><span data-ttu-id="9d7cb-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="9d7cb-133">Apple macOS</span></span>
1. <span data-ttu-id="9d7cb-134">下載並安裝到根據 toohello[安裝指示](https://golang.org/doc/install)比對您的平台。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-134">Download and install Go according toohello [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="9d7cb-135">啟動 hello Bash 殼層。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-135">Launch hello Bash shell.</span></span> 
3. <span data-ttu-id="9d7cb-136">在主目錄中為您的專案產生資料夾，例如 `mkdir -p ~/go/src/mysqlgo/`。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="9d7cb-137">將目錄變更至 hello 資料夾中，例如`cd ~/go/src/mysqlgo/`。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-137">Change directory into hello folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="9d7cb-138">設定 hello GOPATH 環境變數 toopoint tooa 有效的來源目錄，例如您目前的首頁目錄移資料夾。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-138">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="9d7cb-139">在 [hello bash 殼層中，執行`export GOPATH=~/go`tooadd hello 走向 hello GOPATH hello 目前的殼層工作階段目錄。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-139">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="9d7cb-140">安裝 hello [go sql-驅動程式的 mysql](https://github.com/go-sql-driver/mysql#installation)執行 hello`go get github.com/go-sql-driver/mysql`命令。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-140">Install hello [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running hello `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="9d7cb-141">總而言之，就是安裝 Go，然後執行下列 bash 命令：</span><span class="sxs-lookup"><span data-stu-id="9d7cb-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

## <a name="get-connection-information"></a><span data-ttu-id="9d7cb-142">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="9d7cb-142">Get connection information</span></span>
<span data-ttu-id="9d7cb-143">取得 MySQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-143">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="9d7cb-144">您需要 hello 完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-144">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="9d7cb-145">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-145">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9d7cb-146">在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，並搜尋您有 creased，例如 hello 伺服器**myserver4demo**。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-146">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="9d7cb-147">按一下伺服器名稱，hello **myserver4demo**。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-147">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="9d7cb-148">選取 hello 伺服器**屬性**頁面。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-148">Select hello server's **Properties** page.</span></span> <span data-ttu-id="9d7cb-149">請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-149">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="9d7cb-150">![Azure Database for MySQL - 伺服器管理員登入](./media/connect-go/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="9d7cb-150">![Azure Database for MySQL - Server Admin Login](./media/connect-go/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="9d7cb-151">如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀**頁面 tooview hello 伺服器系統管理員登入名稱，並視需要重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-151">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>
   

## <a name="build-and-run-go-code"></a><span data-ttu-id="9d7cb-152">建置並執行 Go 程式碼</span><span class="sxs-lookup"><span data-stu-id="9d7cb-152">Build and run Go code</span></span> 
1. <span data-ttu-id="9d7cb-153">toowrite Golang 程式碼，您可以使用簡單的文字編輯器，例如 [記事本] 在 Windows 中， [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5)或[Nano](https://www.nano-editor.org/) Ubuntu 或在 macOS TextEdit 中。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-153">toowrite Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="9d7cb-154">如果想要使用更豐富的互動式開發環境 (IDE)，您可以選擇 Jetbrains 的 [Gogland](https://www.jetbrains.com/go/)、Microsoft 的 [Visual Studio Code](https://code.visualstudio.com/)，或 [Atom](https://atom.io/)。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-154">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="9d7cb-155">Hello 移至從 hello 區段下方的程式碼貼入文字檔案，並儲存到專案資料夾中副檔名\*.go，例如 Windows 路徑`%USERPROFILE%\go\src\mysqlgo\createtable.go`或 Linux 路徑`~/go/src/mysqlgo/createtable.go`。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-155">Paste hello Go code from hello sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\mysqlgo\createtable.go` or Linux path `~/go/src/mysqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="9d7cb-156">找出 hello `HOST`， `DATABASE`， `USER`，和`PASSWORD`hello 程式碼，並以您自己的值取代 hello 範例值中的常數。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-156">Locate hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in hello code, and replace hello example values with your own values.</span></span> 
4. <span data-ttu-id="9d7cb-157">啟動 hello 命令提示字元，或被殼層。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-157">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="9d7cb-158">將目錄切換到專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-158">Change directory into your project folder.</span></span> <span data-ttu-id="9d7cb-159">例如，在 Windows 上為 `cd %USERPROFILE%\go\src\mysqlgo\`。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-159">For example, on Windows `cd %USERPROFILE%\go\src\mysqlgo\`.</span></span> <span data-ttu-id="9d7cb-160">在 Linux 上為 `cd ~/go/src/mysqlgo/`。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-160">On Linux `cd ~/go/src/mysqlgo/`.</span></span>  <span data-ttu-id="9d7cb-161">部分所述的 hello IDE 編輯器提供偵錯和執行階段功能而不需要殼層命令。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-161">Some of hello IDE editors mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="9d7cb-162">輸入 hello 命令執行 hello 程式碼`go run createtable.go`toocompile hello 應用程式，並執行它。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-162">Run hello code by typing hello command `go run createtable.go` toocompile hello application and run it.</span></span> 
6. <span data-ttu-id="9d7cb-163">或者，toobuild hello 碼轉換為原生應用程式， `go build createtable.go`，然後啟動`createtable.exe`toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-163">Alternatively, toobuild hello code into a native application, `go build createtable.go`, then launch `createtable.exe` toorun hello application.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="9d7cb-164">連線、建立資料表及插入資料</span><span class="sxs-lookup"><span data-stu-id="9d7cb-164">Connect, create table, and insert data</span></span>
<span data-ttu-id="9d7cb-165">使用 hello 下列程式碼 tooconnect toohello 伺服器、 建立資料表，以及載入 hello 資料使用**插入**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-165">Use hello following code tooconnect toohello server, create a table, and load hello data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="9d7cb-166">hello 程式碼匯入三個封裝： hello [sql 封裝](https://golang.org/pkg/database/sql/)，hello [mysql 移 sql 驅動程式](https://github.com/go-sql-driver/mysql#installation)為 hello 與 hello Azure 資料庫的 MySQL 驅動程式 toocommunicate [fmt 封裝](https://golang.org/pkg/fmt/)列印的輸入和輸出 hello 命令列上的。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-166">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="9d7cb-167">hello 程式碼呼叫方法[sql。Open （)](http://go-database-sql.org/accessing.html) tooconnect tooAzure MySQL 和使用方法檢查 hello 連接資料庫的[db。Ping()](https://golang.org/pkg/database/sql/#DB.Ping)。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-167">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="9d7cb-168">A[資料庫控制代碼](https://golang.org/pkg/database/sql/#DB)會完全使用，保留 hello hello 的資料庫伺服器的連接集區。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-168">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="9d7cb-169">hello 程式碼呼叫 hello [exec （)](https://golang.org/pkg/database/sql/#DB.Exec)方法多次 toorun 數個 DDL 命令。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-169">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times toorun several DDL commands.</span></span> <span data-ttu-id="9d7cb-170">hello 程式碼也會使用 hello [Prepare()](http://go-database-sql.org/prepared.html)和 exec （) toorun 備妥的陳述式使用不同的參數 tooinsert 三個資料列。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-170">hello code also uses hello [Prepare()](http://go-database-sql.org/prepared.html) and Exec() toorun prepared statements with different parameters tooinsert three rows.</span></span> <span data-ttu-id="9d7cb-171">每次自訂 checkError() 方法是使用的 toocheck 如果發生錯誤，而驚慌 tooexit。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-171">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="9d7cb-172">取代 hello `host`， `database`， `user`，和`password`常數以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-172">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed).")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table.")

    // Insert some data into table.
    sqlStatement, err := db.Prepare("INSERT INTO inventory (name, quantity) VALUES (?, ?);")
    res, err := sqlStatement.Exec("banana", 150)
    checkError(err)
    rowCount, err := res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("orange", 154)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("apple", 100)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}

```

## <a name="read-data"></a><span data-ttu-id="9d7cb-173">讀取資料</span><span class="sxs-lookup"><span data-stu-id="9d7cb-173">Read data</span></span>
<span data-ttu-id="9d7cb-174">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**選取**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-174">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="9d7cb-175">hello 程式碼匯入三個封裝： hello [sql 封裝](https://golang.org/pkg/database/sql/)，hello [mysql 移 sql 驅動程式](https://github.com/go-sql-driver/mysql#installation)為 hello 與 hello Azure 資料庫的 MySQL 驅動程式 toocommunicate [fmt 封裝](https://golang.org/pkg/fmt/)列印的輸入和輸出 hello 命令列上的。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-175">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="9d7cb-176">hello 程式碼呼叫方法[sql。Open （)](http://go-database-sql.org/accessing.html) tooconnect tooAzure MySQL 和使用方法檢查 hello 連接資料庫的[db。Ping()](https://golang.org/pkg/database/sql/#DB.Ping)。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-176">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="9d7cb-177">A[資料庫控制代碼](https://golang.org/pkg/database/sql/#DB)會完全使用，保留 hello hello 的資料庫伺服器的連接集區。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="9d7cb-178">hello 程式碼呼叫 hello [query （)](https://golang.org/pkg/database/sql/#DB.Query)方法 toorun hello select 命令。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-178">hello code calls hello [Query()](https://golang.org/pkg/database/sql/#DB.Query) method toorun hello select command.</span></span> <span data-ttu-id="9d7cb-179">然後它會執行[next （)](https://golang.org/pkg/database/sql/#Rows.Next) tooiterate 透過 hello 結果集和[Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) tooparse hello 資料行值儲存到變數中的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-179">Then it runs [Next()](https://golang.org/pkg/database/sql/#Rows.Next) tooiterate through hello result set and [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) tooparse hello column values, saving hello value into variables.</span></span> <span data-ttu-id="9d7cb-180">每次自訂 checkError() 方法是使用的 toocheck 如果發生錯誤，而驚慌 tooexit。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-180">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="9d7cb-181">取代 hello `host`， `database`， `user`，和`password`常數以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-181">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Variables for printing column data when scanned.
    var (
        id       int
        name     string
        quantity int
    )

    // Read some data from hello table.
    rows, err := db.Query("SELECT id, name, quantity from inventory;")
    checkError(err)
    defer rows.Close()
    fmt.Println("Reading data:")
    for rows.Next() {
        err := rows.Scan(&id, &name, &quantity)
        checkError(err)
        fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
    }
    err = rows.Err()
    checkError(err)
    fmt.Println("Done.")
}
```

## <a name="update-data"></a><span data-ttu-id="9d7cb-182">更新資料</span><span class="sxs-lookup"><span data-stu-id="9d7cb-182">Update data</span></span>
<span data-ttu-id="9d7cb-183">使用 hello 下列程式碼 tooconnect 並更新 hello 資料使用**更新**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-183">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="9d7cb-184">hello 程式碼匯入三個封裝： hello [sql 封裝](https://golang.org/pkg/database/sql/)，hello [mysql 移 sql 驅動程式](https://github.com/go-sql-driver/mysql#installation)為 hello 與 hello Azure 資料庫的 MySQL 驅動程式 toocommunicate [fmt 封裝](https://golang.org/pkg/fmt/)列印的輸入和輸出 hello 命令列上的。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-184">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="9d7cb-185">hello 程式碼呼叫方法[sql。Open （)](http://go-database-sql.org/accessing.html) tooconnect tooAzure MySQL 和使用方法檢查 hello 連接資料庫的[db。Ping()](https://golang.org/pkg/database/sql/#DB.Ping)。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-185">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="9d7cb-186">A[資料庫控制代碼](https://golang.org/pkg/database/sql/#DB)會完全使用，保留 hello hello 的資料庫伺服器的連接集區。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="9d7cb-187">hello 程式碼呼叫 hello [exec （)](https://golang.org/pkg/database/sql/#DB.Exec)方法 toorun hello 更新命令。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-187">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello update command.</span></span> <span data-ttu-id="9d7cb-188">每次自訂 checkError() 方法是使用的 toocheck 如果發生錯誤，而驚慌 tooexit。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-188">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="9d7cb-189">取代 hello `host`， `database`， `user`，和`password`常數以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-189">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Modify some data in table.
    rows, err := db.Exec("UPDATE inventory SET quantity = ? WHERE name = ?", 200, "banana")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="delete-data"></a><span data-ttu-id="9d7cb-190">刪除資料</span><span class="sxs-lookup"><span data-stu-id="9d7cb-190">Delete data</span></span>
<span data-ttu-id="9d7cb-191">使用 hello 下列程式碼 tooconnect 並移除資料使用**刪除**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-191">Use hello following code tooconnect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="9d7cb-192">hello 程式碼匯入三個封裝： hello [sql 封裝](https://golang.org/pkg/database/sql/)，hello [mysql 移 sql 驅動程式](https://github.com/go-sql-driver/mysql#installation)為 hello 與 hello Azure 資料庫的 MySQL 驅動程式 toocommunicate [fmt 封裝](https://golang.org/pkg/fmt/)列印的輸入和輸出 hello 命令列上的。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-192">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="9d7cb-193">hello 程式碼呼叫方法[sql。Open （)](http://go-database-sql.org/accessing.html) tooconnect tooAzure MySQL 和使用方法檢查 hello 連接資料庫的[db。Ping()](https://golang.org/pkg/database/sql/#DB.Ping)。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-193">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="9d7cb-194">A[資料庫控制代碼](https://golang.org/pkg/database/sql/#DB)會完全使用，保留 hello hello 的資料庫伺服器的連接集區。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="9d7cb-195">hello 程式碼呼叫 hello [exec （)](https://golang.org/pkg/database/sql/#DB.Exec)方法 toorun hello 的 delete 命令。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-195">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello delete command.</span></span> <span data-ttu-id="9d7cb-196">每次自訂 checkError() 方法是使用的 toocheck 如果發生錯誤，而驚慌 tooexit。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-196">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="9d7cb-197">取代 hello `host`， `database`， `user`，和`password`常數以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="9d7cb-197">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Modify some data in table.
    rows, err := db.Exec("DELETE FROM inventory WHERE name = ?", "orange")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="next-steps"></a><span data-ttu-id="9d7cb-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9d7cb-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="9d7cb-199">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="9d7cb-199">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)

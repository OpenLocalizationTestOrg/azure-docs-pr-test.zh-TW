---
title: "使用 Go 語言連線至 Azure Database for PostgreSQL | Microsoft Docs"
description: "本快速入門提供 Go 程式設計語言範例，您可用於從 Azure Database for PostgreSQL 連線及查詢資料。"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: go
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: a7555464879826c5e4f55929d23163b002664e81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-go-language-to-connect-and-query-data"></a><span data-ttu-id="fb70b-103">Azure Database for PostgreSQL︰使用 Go 語言連線及查詢資料</span><span class="sxs-lookup"><span data-stu-id="fb70b-103">Azure Database for PostgreSQL: Use Go language to connect and query data</span></span>
<span data-ttu-id="fb70b-104">本快速入門示範如何使用以 [Go](https://golang.org/) 語言 (golang) 撰寫的程式碼來連線到 Azure Database for PostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="fb70b-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using code written in the [Go](https://golang.org/) language (golang).</span></span> <span data-ttu-id="fb70b-105">它會顯示如何使用 SQL 陳述式來查詢、插入、更新和刪除資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="fb70b-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="fb70b-106">本文假設您已熟悉使用 Go 進行開發，但不熟悉 Azure Database for PostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="fb70b-106">This article assumes you are familiar with development using Go, but that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb70b-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="fb70b-107">Prerequisites</span></span>
<span data-ttu-id="fb70b-108">本快速入門使用在以下任一指南中建立的資源作為起點︰</span><span class="sxs-lookup"><span data-stu-id="fb70b-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="fb70b-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="fb70b-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="fb70b-110">建立 DB - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fb70b-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a><span data-ttu-id="fb70b-111">安裝 Go 和 pq 連接器</span><span class="sxs-lookup"><span data-stu-id="fb70b-111">Install Go and pq connector</span></span>
<span data-ttu-id="fb70b-112">在您自己的機器上安裝 [Go](https://golang.org/doc/install) 和 [Pure Go Postgres 驅動程式 (pq)](https://github.com/lib/pq)。</span><span class="sxs-lookup"><span data-stu-id="fb70b-112">Install [Go](https://golang.org/doc/install) and the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) on your own machine.</span></span> <span data-ttu-id="fb70b-113">根據您的平台，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fb70b-113">Depending on your platform, follow the steps:</span></span>

### <a name="windows"></a><span data-ttu-id="fb70b-114">Windows</span><span class="sxs-lookup"><span data-stu-id="fb70b-114">Windows</span></span>
1. <span data-ttu-id="fb70b-115">根據[安裝指示](https://golang.org/doc/install)，[下載](https://golang.org/dl/)並安裝 Go for Microsoft Windows。</span><span class="sxs-lookup"><span data-stu-id="fb70b-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according to the [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="fb70b-116">從 [開始] 功能表啟動命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="fb70b-116">Launch the command prompt from the start menu.</span></span>
3. <span data-ttu-id="fb70b-117">為您的專案產生資料夾，例如</span><span class="sxs-lookup"><span data-stu-id="fb70b-117">Make a folder for your project such.</span></span> <span data-ttu-id="fb70b-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`。</span><span class="sxs-lookup"><span data-stu-id="fb70b-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span></span>
4. <span data-ttu-id="fb70b-119">將目錄切換到專案資料夾，例如 `cd %USERPROFILE%\go\src\postgresqlgo`。</span><span class="sxs-lookup"><span data-stu-id="fb70b-119">Change directory into the project folder, such as `cd %USERPROFILE%\go\src\postgresqlgo`.</span></span>
5. <span data-ttu-id="fb70b-120">將 GOPATH 環境變數設定為指向來源程式碼目錄。</span><span class="sxs-lookup"><span data-stu-id="fb70b-120">Set the environment variable for GOPATH to point to the source code directory.</span></span> <span data-ttu-id="fb70b-121">`set GOPATH=%USERPROFILE%\go`。</span><span class="sxs-lookup"><span data-stu-id="fb70b-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="fb70b-122">執行 `go get github.com/lib/pq` 命令來安裝 [Pure Go Postgres 驅動程式 (pq)](https://github.com/lib/pq)。</span><span class="sxs-lookup"><span data-stu-id="fb70b-122">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="fb70b-123">總而言之，就是安裝 Go，然後在命令提示字元中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="fb70b-123">In summary, install Go, then run these commands in the command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="fb70b-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="fb70b-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="fb70b-125">啟動 Bash 殼層。</span><span class="sxs-lookup"><span data-stu-id="fb70b-125">Launch the Bash shell.</span></span> 
2. <span data-ttu-id="fb70b-126">執行 `sudo apt-get install golang-go` 以安裝 Go。</span><span class="sxs-lookup"><span data-stu-id="fb70b-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="fb70b-127">在主目錄中為您的專案產生資料夾，例如 `mkdir -p ~/go/src/postgresqlgo/`。</span><span class="sxs-lookup"><span data-stu-id="fb70b-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="fb70b-128">將目錄切換到此資料夾，例如 `cd ~/go/src/postgresqlgo/`。</span><span class="sxs-lookup"><span data-stu-id="fb70b-128">Change directory into the folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="fb70b-129">將 GOPATH 環境變數設定為指向有效的來源目錄，例如目前主目錄的 go 資料夾。</span><span class="sxs-lookup"><span data-stu-id="fb70b-129">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="fb70b-130">在 Bash 殼層，執行 `export GOPATH=~/go` 以將 go 目錄新增為目前殼層工作階段的 GOPATH。</span><span class="sxs-lookup"><span data-stu-id="fb70b-130">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="fb70b-131">執行 `go get github.com/lib/pq` 命令來安裝 [Pure Go Postgres 驅動程式 (pq)](https://github.com/lib/pq)。</span><span class="sxs-lookup"><span data-stu-id="fb70b-131">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="fb70b-132">總而言之，就是執行下列 bash 命令：</span><span class="sxs-lookup"><span data-stu-id="fb70b-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a><span data-ttu-id="fb70b-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="fb70b-133">Apple macOS</span></span>
1. <span data-ttu-id="fb70b-134">根據符合您平台的[安裝指示](https://golang.org/doc/install)，下載並安裝 Go。</span><span class="sxs-lookup"><span data-stu-id="fb70b-134">Download and install Go according to the [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="fb70b-135">啟動 Bash 殼層。</span><span class="sxs-lookup"><span data-stu-id="fb70b-135">Launch the Bash shell.</span></span> 
3. <span data-ttu-id="fb70b-136">在主目錄中為您的專案產生資料夾，例如 `mkdir -p ~/go/src/postgresqlgo/`。</span><span class="sxs-lookup"><span data-stu-id="fb70b-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="fb70b-137">將目錄切換到此資料夾，例如 `cd ~/go/src/postgresqlgo/`。</span><span class="sxs-lookup"><span data-stu-id="fb70b-137">Change directory into the folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="fb70b-138">將 GOPATH 環境變數設定為指向有效的來源目錄，例如目前主目錄的 go 資料夾。</span><span class="sxs-lookup"><span data-stu-id="fb70b-138">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="fb70b-139">在 Bash 殼層，執行 `export GOPATH=~/go` 以將 go 目錄新增為目前殼層工作階段的 GOPATH。</span><span class="sxs-lookup"><span data-stu-id="fb70b-139">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="fb70b-140">執行 `go get github.com/lib/pq` 命令來安裝 [Pure Go Postgres 驅動程式 (pq)](https://github.com/lib/pq)。</span><span class="sxs-lookup"><span data-stu-id="fb70b-140">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="fb70b-141">總而言之，就是安裝 Go，然後執行下列 bash 命令：</span><span class="sxs-lookup"><span data-stu-id="fb70b-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a><span data-ttu-id="fb70b-142">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="fb70b-142">Get connection information</span></span>
<span data-ttu-id="fb70b-143">取得連線到 Azure Database for PostgreSQL 所需的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="fb70b-143">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="fb70b-144">您需要完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="fb70b-144">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="fb70b-145">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="fb70b-145">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fb70b-146">從 Azure 入口網站的左側功能表中，按一下 [所有資源]，然後搜尋您所建立的伺服器，例如 **mypgserver-20170401**。</span><span class="sxs-lookup"><span data-stu-id="fb70b-146">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="fb70b-147">按一下伺服器名稱 [mypgserver-20170401]。</span><span class="sxs-lookup"><span data-stu-id="fb70b-147">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="fb70b-148">選取伺服器的 [概觀] 頁面。</span><span class="sxs-lookup"><span data-stu-id="fb70b-148">Select the server's **Overview** page.</span></span> <span data-ttu-id="fb70b-149">記下 [伺服器名稱] 和 [伺服器管理員登入名稱]。</span><span class="sxs-lookup"><span data-stu-id="fb70b-149">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="fb70b-150">![Azure Database for PostgreSQL - 伺服器管理員登入](./media/connect-go/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="fb70b-150">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-go/1-connection-string.png)</span></span>
5. <span data-ttu-id="fb70b-151">如果您忘記伺服器登入資訊，請瀏覽至 [概觀] 頁面，然後檢視伺服器管理員登入名稱。</span><span class="sxs-lookup"><span data-stu-id="fb70b-151">If you forget your server login information, navigate to the **Overview** page, and view the Server admin login name.</span></span> <span data-ttu-id="fb70b-152">如有必要，請重設密碼。</span><span class="sxs-lookup"><span data-stu-id="fb70b-152">If necessary, reset the password.</span></span>

## <a name="build-and-run-go-code"></a><span data-ttu-id="fb70b-153">建置並執行 Go 程式碼</span><span class="sxs-lookup"><span data-stu-id="fb70b-153">Build and run Go code</span></span> 
1. <span data-ttu-id="fb70b-154">若要撰寫 Golang 程式碼，您可以使用簡單的文字編輯器，例如 Microsoft Windows 的記事本、Ubuntu 的 [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) 或 [Nano](https://www.nano-editor.org/)，或 macOS 的 TextEdit。</span><span class="sxs-lookup"><span data-stu-id="fb70b-154">To write Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="fb70b-155">如果想要使用更豐富的互動式開發環境 (IDE)，您可以選擇 Jetbrains 的 [Gogland](https://www.jetbrains.com/go/)、Microsoft 的 [Visual Studio Code](https://code.visualstudio.com/)，或 [Atom](https://atom.io/)。</span><span class="sxs-lookup"><span data-stu-id="fb70b-155">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="fb70b-156">將下列幾節的 Golang 程式碼貼到文字檔中，並加上副檔名 \*.go 來儲存到專案資料夾，例如 Windows 路徑 `%USERPROFILE%\go\src\postgresqlgo\createtable.go` 或 Linux 路徑 `~/go/src/postgresqlgo/createtable.go`。</span><span class="sxs-lookup"><span data-stu-id="fb70b-156">Paste the Golang code from the sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\postgresqlgo\createtable.go` or Linux path `~/go/src/postgresqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="fb70b-157">在程式碼中找出 `HOST`、`DATABASE`、`USER` 和 `PASSWORD` 常數，然後將範例值換成您自己的值。</span><span class="sxs-lookup"><span data-stu-id="fb70b-157">Locate the `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in the code, and replace the example values with your own values.</span></span>  
4. <span data-ttu-id="fb70b-158">啟動命令提示字元或 bash 殼層。</span><span class="sxs-lookup"><span data-stu-id="fb70b-158">Launch the command prompt or bash shell.</span></span> <span data-ttu-id="fb70b-159">將目錄切換到專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="fb70b-159">Change directory into your project folder.</span></span> <span data-ttu-id="fb70b-160">例如，在 Windows 上為 `cd %USERPROFILE%\go\src\postgresqlgo\`。</span><span class="sxs-lookup"><span data-stu-id="fb70b-160">For example, on Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span></span> <span data-ttu-id="fb70b-161">在 Linux 上執行 `cd ~/go/src/postgresqlgo/`。</span><span class="sxs-lookup"><span data-stu-id="fb70b-161">On Linux `cd ~/go/src/postgresqlgo/`.</span></span> <span data-ttu-id="fb70b-162">提及的部分 IDE 環境提供偵錯和執行階段功能，並不需要殼層命令。</span><span class="sxs-lookup"><span data-stu-id="fb70b-162">Some of the IDE environments mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="fb70b-163">輸入命令 `go run createtable.go` 來編譯應用程式並加以執行，以執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="fb70b-163">Run the code by typing the command `go run createtable.go` to compile the application and run it.</span></span> 
6. <span data-ttu-id="fb70b-164">或者，若要將程式碼建置到原生應用程式，請執行 `go build createtable.go`，然後啟動 `createtable.exe` 來執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="fb70b-164">Alternatively, to build the code into a native application, `go build createtable.go`, then launch `createtable.exe` to run the application.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="fb70b-165">連線及建立資料表</span><span class="sxs-lookup"><span data-stu-id="fb70b-165">Connect and create a table</span></span>
<span data-ttu-id="fb70b-166">使用下列程式碼搭配 **CREATE TABLE** SQL 陳述式 (後面接著 **INSERT INTO** SQL 陳述式) 來連線和建立資料表，進而將資料列新增至資料表中。</span><span class="sxs-lookup"><span data-stu-id="fb70b-166">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="fb70b-167">程式碼會匯入三個套件：[sql 套件](https://golang.org/pkg/database/sql/)、[pq 套件](http://godoc.org/github.com/lib/pq)作為驅動程式來與 Postgres 伺服器通訊，以及 [fmt 套件](https://golang.org/pkg/fmt/) (適用於命令列上列印的輸入和輸出)。</span><span class="sxs-lookup"><span data-stu-id="fb70b-167">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="fb70b-168">程式碼會呼叫 [sql.Open()](http://godoc.org/github.com/lib/pq#Open) 方法來連線到Azure Database for PostgreSQL，用於連線到 Azure 資料庫，並使用 [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping) 方法檢查連線。</span><span class="sxs-lookup"><span data-stu-id="fb70b-168">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="fb70b-169">[資料庫控制代碼](https://golang.org/pkg/database/sql/#DB)會到處使用，並保留資料庫伺服器的連線集區。</span><span class="sxs-lookup"><span data-stu-id="fb70b-169">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="fb70b-170">程式碼會呼叫 [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) 方法數次以執行數個 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="fb70b-170">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times to run several SQL commands.</span></span> <span data-ttu-id="fb70b-171">每次自訂 checkError() 方法檢查是否發生錯誤，而如果發生錯誤，則會驚慌結束。</span><span class="sxs-lookup"><span data-stu-id="fb70b-171">Each time a custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="fb70b-172">以您自己的值取代 `HOST`、`DATABASE`、`USER` 和 `PASSWORD` 參數。</span><span class="sxs-lookup"><span data-stu-id="fb70b-172">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed)")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table")

    // Insert some data into table.
    sql_statement := "INSERT INTO inventory (name, quantity) VALUES ($1, $2);"
    _, err = db.Exec(sql_statement, "banana", 150)
    checkError(err)
    _, err = db.Exec(sql_statement, "orange", 154)
    checkError(err)
    _, err = db.Exec(sql_statement, "apple", 100)
    checkError(err)
    fmt.Println("Inserted 3 rows of data")
}
```

## <a name="read-data"></a><span data-ttu-id="fb70b-173">讀取資料</span><span class="sxs-lookup"><span data-stu-id="fb70b-173">Read data</span></span>
<span data-ttu-id="fb70b-174">使用下列程式碼搭配 **SELECT** SQL 陳述式來連線和讀取資料。</span><span class="sxs-lookup"><span data-stu-id="fb70b-174">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="fb70b-175">程式碼會匯入三個套件：[sql 套件](https://golang.org/pkg/database/sql/)、[pq 套件](http://godoc.org/github.com/lib/pq)作為驅動程式來與 Postgres 伺服器通訊，以及 [fmt 套件](https://golang.org/pkg/fmt/) (適用於命令列上列印的輸入和輸出)。</span><span class="sxs-lookup"><span data-stu-id="fb70b-175">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="fb70b-176">程式碼會呼叫 [sql.Open()](http://godoc.org/github.com/lib/pq#Open) 方法來連線到Azure Database for PostgreSQL，用於連線到 Azure 資料庫，並使用 [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping) 方法檢查連線。</span><span class="sxs-lookup"><span data-stu-id="fb70b-176">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="fb70b-177">[資料庫控制代碼](https://golang.org/pkg/database/sql/#DB)會到處使用，並保留資料庫伺服器的連線集區。</span><span class="sxs-lookup"><span data-stu-id="fb70b-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="fb70b-178">呼叫 [db.Query()](https://golang.org/pkg/database/sql/#DB.Query) 方法可執行 select 查詢，而結果產生的資料列會保留在類型為 [rows](https://golang.org/pkg/database/sql/#Rows) 的變數中。</span><span class="sxs-lookup"><span data-stu-id="fb70b-178">The select query is run by calling method [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), and the resulting rows is kept in a variable of type [rows](https://golang.org/pkg/database/sql/#Rows).</span></span> <span data-ttu-id="fb70b-179">程式碼會使用 [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) 方法讀取目前資料列中的資料行資料值，並使用 [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) 迭代器對資料列執行迴圈，直到再也沒有資料列存在為止。</span><span class="sxs-lookup"><span data-stu-id="fb70b-179">The code reads the column data values in the current row using method [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) and loops over the rows using the iterator [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) until no more rows exist.</span></span> <span data-ttu-id="fb70b-180">每個資料列的資料行值都會列印到主控台。每次自訂 checkError() 方法檢查是否發生錯誤，而如果發生錯誤，則會驚慌結束。</span><span class="sxs-lookup"><span data-stu-id="fb70b-180">Each row's column values are printed to the console out. Each time a custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="fb70b-181">以您自己的值取代 `HOST`、`DATABASE`、`USER` 和 `PASSWORD` 參數。</span><span class="sxs-lookup"><span data-stu-id="fb70b-181">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database")

    // Read rows from table.
    var id int
    var name string
    var quantity int

    sql_statement := "SELECT * from inventory;"
    rows, err := db.Query(sql_statement)
    checkError(err)

    for rows.Next() {
        switch err := rows.Scan(&id, &name, &quantity); err {
        case sql.ErrNoRows:
            fmt.Println("No rows were returned")
        case nil:
            fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
        default:
            checkError(err)
        }
    }
}
```

## <a name="update-data"></a><span data-ttu-id="fb70b-182">更新資料</span><span class="sxs-lookup"><span data-stu-id="fb70b-182">Update data</span></span>
<span data-ttu-id="fb70b-183">使用下列程式碼搭配 **UPDATE** SQL 陳述式來連線和更新資料。</span><span class="sxs-lookup"><span data-stu-id="fb70b-183">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="fb70b-184">程式碼會匯入三個套件：[sql 套件](https://golang.org/pkg/database/sql/)、[pq 套件](http://godoc.org/github.com/lib/pq)作為驅動程式來與 Postgres 伺服器通訊，以及 [fmt 套件](https://golang.org/pkg/fmt/) (適用於命令列上列印的輸入和輸出)。</span><span class="sxs-lookup"><span data-stu-id="fb70b-184">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="fb70b-185">程式碼會呼叫 [sql.Open()](http://godoc.org/github.com/lib/pq#Open) 方法來連線到Azure Database for PostgreSQL，用於連線到 Azure 資料庫，並使用 [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping) 方法檢查連線。</span><span class="sxs-lookup"><span data-stu-id="fb70b-185">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="fb70b-186">[資料庫控制代碼](https://golang.org/pkg/database/sql/#DB)會到處使用，並保留資料庫伺服器的連線集區。</span><span class="sxs-lookup"><span data-stu-id="fb70b-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="fb70b-187">程式碼會呼叫 [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) 方法來執行可更新資料表的 SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="fb70b-187">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the SQL statement that updates the table.</span></span> <span data-ttu-id="fb70b-188">自訂 checkError() 方法可檢查是否發生錯誤，而如果發生錯誤，則會驚慌結束。</span><span class="sxs-lookup"><span data-stu-id="fb70b-188">A custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="fb70b-189">以您自己的值取代 `HOST`、`DATABASE`、`USER` 和 `PASSWORD` 參數。</span><span class="sxs-lookup"><span data-stu-id="fb70b-189">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database")

    // Modify some data in table.
    sql_statement := "UPDATE inventory SET quantity = $2 WHERE name = $1;"
    _, err = db.Exec(sql_statement, "banana", 200)
    checkError(err)
    fmt.Println("Updated 1 row of data")
}
```

## <a name="delete-data"></a><span data-ttu-id="fb70b-190">刪除資料</span><span class="sxs-lookup"><span data-stu-id="fb70b-190">Delete data</span></span>
<span data-ttu-id="fb70b-191">使用下列程式碼搭配 **DELETE** SQL 陳述式來連線和讀取資料。</span><span class="sxs-lookup"><span data-stu-id="fb70b-191">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="fb70b-192">程式碼會匯入三個套件：[sql 套件](https://golang.org/pkg/database/sql/)、[pq 套件](http://godoc.org/github.com/lib/pq)作為驅動程式來與 Postgres 伺服器通訊，以及 [fmt 套件](https://golang.org/pkg/fmt/) (適用於命令列上列印的輸入和輸出)。</span><span class="sxs-lookup"><span data-stu-id="fb70b-192">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="fb70b-193">程式碼會呼叫 [sql.Open()](http://godoc.org/github.com/lib/pq#Open) 方法來連線到Azure Database for PostgreSQL，用於連線到 Azure 資料庫，並使用 [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping) 方法檢查連線。</span><span class="sxs-lookup"><span data-stu-id="fb70b-193">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="fb70b-194">[資料庫控制代碼](https://golang.org/pkg/database/sql/#DB)會到處使用，並保留資料庫伺服器的連線集區。</span><span class="sxs-lookup"><span data-stu-id="fb70b-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="fb70b-195">程式碼會呼叫 [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) 方法來執行可更新資料表的 SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="fb70b-195">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the SQL statement that updates the table.</span></span> <span data-ttu-id="fb70b-196">自訂 checkError() 方法可檢查是否發生錯誤，而如果發生錯誤，則會驚慌結束。</span><span class="sxs-lookup"><span data-stu-id="fb70b-196">A custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="fb70b-197">以您自己的值取代 `HOST`、`DATABASE`、`USER` 和 `PASSWORD` 參數。</span><span class="sxs-lookup"><span data-stu-id="fb70b-197">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database")

    // Delete some data from table.
    sql_statement := "DELETE FROM inventory WHERE name = $1;"
    _, err = db.Exec(sql_statement, "orange")
    checkError(err)
    fmt.Println("Deleted 1 row of data")
}
```

## <a name="next-steps"></a><span data-ttu-id="fb70b-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fb70b-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="fb70b-199">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="fb70b-199">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)

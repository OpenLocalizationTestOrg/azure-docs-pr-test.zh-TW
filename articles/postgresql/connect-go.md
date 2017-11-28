---
title: "aaaConnect tooAzure 使用 Go 語言 PostgreSQL 資料庫 |Microsoft 文件"
description: "本快速入門提供 Go 程式設計語言範例，您可以使用 tooconnect 和 PostgreSQL 查詢從 Azure 資料庫的資料。"
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
ms.openlocfilehash: aa3c93da03116b8fcb54557494dccfad558e5f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-go-language-tooconnect-and-query-data"></a><span data-ttu-id="15dd9-103">Azure PostgreSQL 資料庫： 使用 Go 語言 tooconnect 和查詢資料</span><span class="sxs-lookup"><span data-stu-id="15dd9-103">Azure Database for PostgreSQL: Use Go language tooconnect and query data</span></span>
<span data-ttu-id="15dd9-104">本快速入門示範如何使用 PostgreSQL tooconnect tooan Azure 資料庫程式碼撰寫的 hello[移](https://golang.org/)語言 (golang)。</span><span class="sxs-lookup"><span data-stu-id="15dd9-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using code written in hello [Go](https://golang.org/) language (golang).</span></span> <span data-ttu-id="15dd9-105">它會顯示 toouse SQL 陳述式 tooquery，如何插入、 更新和刪除 hello 資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="15dd9-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="15dd9-106">本文假設您熟悉開發使用 Go，但是，您就可以新增 tooworking Azure PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="15dd9-106">This article assumes you are familiar with development using Go, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15dd9-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="15dd9-107">Prerequisites</span></span>
<span data-ttu-id="15dd9-108">本快速入門會使用 hello 資源建立在其中一個這些指南做為起點：</span><span class="sxs-lookup"><span data-stu-id="15dd9-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="15dd9-109">建立 DB - 入口網站</span><span class="sxs-lookup"><span data-stu-id="15dd9-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="15dd9-110">建立 DB - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="15dd9-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a><span data-ttu-id="15dd9-111">安裝 Go 和 pq 連接器</span><span class="sxs-lookup"><span data-stu-id="15dd9-111">Install Go and pq connector</span></span>
<span data-ttu-id="15dd9-112">安裝[移](https://golang.org/doc/install)和 hello[純移 Postgres 驅動程式 (pq)](https://github.com/lib/pq)自己電腦上。</span><span class="sxs-lookup"><span data-stu-id="15dd9-112">Install [Go](https://golang.org/doc/install) and hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) on your own machine.</span></span> <span data-ttu-id="15dd9-113">根據您的平台，請依照下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="15dd9-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="15dd9-114">Windows</span><span class="sxs-lookup"><span data-stu-id="15dd9-114">Windows</span></span>
1. <span data-ttu-id="15dd9-115">[下載](https://golang.org/dl/)並安裝 Microsoft windows 根據 toohello Go[安裝指示](https://golang.org/doc/install)。</span><span class="sxs-lookup"><span data-stu-id="15dd9-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according toohello [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="15dd9-116">啟動 hello 從 hello [開始] 功能表的命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="15dd9-116">Launch hello command prompt from hello start menu.</span></span>
3. <span data-ttu-id="15dd9-117">為您的專案產生資料夾，例如</span><span class="sxs-lookup"><span data-stu-id="15dd9-117">Make a folder for your project such.</span></span> <span data-ttu-id="15dd9-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`。</span><span class="sxs-lookup"><span data-stu-id="15dd9-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span></span>
4. <span data-ttu-id="15dd9-119">將目錄變更至 hello 專案資料夾中，例如`cd %USERPROFILE%\go\src\postgresqlgo`。</span><span class="sxs-lookup"><span data-stu-id="15dd9-119">Change directory into hello project folder, such as `cd %USERPROFILE%\go\src\postgresqlgo`.</span></span>
5. <span data-ttu-id="15dd9-120">設定 GOPATH toopoint toohello 原始程式碼目錄的 hello 環境變數。</span><span class="sxs-lookup"><span data-stu-id="15dd9-120">Set hello environment variable for GOPATH toopoint toohello source code directory.</span></span> <span data-ttu-id="15dd9-121">`set GOPATH=%USERPROFILE%\go`。</span><span class="sxs-lookup"><span data-stu-id="15dd9-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="15dd9-122">安裝 hello[純移 Postgres 驅動程式 (pq)](https://github.com/lib/pq)執行 hello`go get github.com/lib/pq`命令。</span><span class="sxs-lookup"><span data-stu-id="15dd9-122">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="15dd9-123">在 摘要 安裝到，然後 hello 命令提示字元中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="15dd9-123">In summary, install Go, then run these commands in hello command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="15dd9-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="15dd9-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="15dd9-125">啟動 hello Bash 殼層。</span><span class="sxs-lookup"><span data-stu-id="15dd9-125">Launch hello Bash shell.</span></span> 
2. <span data-ttu-id="15dd9-126">執行 `sudo apt-get install golang-go` 以安裝 Go。</span><span class="sxs-lookup"><span data-stu-id="15dd9-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="15dd9-127">在主目錄中為您的專案產生資料夾，例如 `mkdir -p ~/go/src/postgresqlgo/`。</span><span class="sxs-lookup"><span data-stu-id="15dd9-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="15dd9-128">將目錄變更至 hello 資料夾中，例如`cd ~/go/src/postgresqlgo/`。</span><span class="sxs-lookup"><span data-stu-id="15dd9-128">Change directory into hello folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="15dd9-129">設定 hello GOPATH 環境變數 toopoint tooa 有效的來源目錄，例如您目前的首頁目錄移資料夾。</span><span class="sxs-lookup"><span data-stu-id="15dd9-129">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="15dd9-130">在 hello bash 殼層中，執行`export GOPATH=~/go`tooadd hello 走向 hello GOPATH hello 目前的殼層工作階段目錄。</span><span class="sxs-lookup"><span data-stu-id="15dd9-130">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="15dd9-131">安裝 hello[純移 Postgres 驅動程式 (pq)](https://github.com/lib/pq)執行 hello`go get github.com/lib/pq`命令。</span><span class="sxs-lookup"><span data-stu-id="15dd9-131">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="15dd9-132">總而言之，就是執行下列 bash 命令：</span><span class="sxs-lookup"><span data-stu-id="15dd9-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a><span data-ttu-id="15dd9-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="15dd9-133">Apple macOS</span></span>
1. <span data-ttu-id="15dd9-134">下載並安裝到根據 toohello[安裝指示](https://golang.org/doc/install)比對您的平台。</span><span class="sxs-lookup"><span data-stu-id="15dd9-134">Download and install Go according toohello [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="15dd9-135">啟動 hello Bash 殼層。</span><span class="sxs-lookup"><span data-stu-id="15dd9-135">Launch hello Bash shell.</span></span> 
3. <span data-ttu-id="15dd9-136">在主目錄中為您的專案產生資料夾，例如 `mkdir -p ~/go/src/postgresqlgo/`。</span><span class="sxs-lookup"><span data-stu-id="15dd9-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="15dd9-137">將目錄變更至 hello 資料夾中，例如`cd ~/go/src/postgresqlgo/`。</span><span class="sxs-lookup"><span data-stu-id="15dd9-137">Change directory into hello folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="15dd9-138">設定 hello GOPATH 環境變數 toopoint tooa 有效的來源目錄，例如您目前的首頁目錄移資料夾。</span><span class="sxs-lookup"><span data-stu-id="15dd9-138">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="15dd9-139">在 hello bash 殼層中，執行`export GOPATH=~/go`tooadd hello 走向 hello GOPATH hello 目前的殼層工作階段目錄。</span><span class="sxs-lookup"><span data-stu-id="15dd9-139">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="15dd9-140">安裝 hello[純移 Postgres 驅動程式 (pq)](https://github.com/lib/pq)執行 hello`go get github.com/lib/pq`命令。</span><span class="sxs-lookup"><span data-stu-id="15dd9-140">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="15dd9-141">總而言之，就是安裝 Go，然後執行下列 bash 命令：</span><span class="sxs-lookup"><span data-stu-id="15dd9-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a><span data-ttu-id="15dd9-142">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="15dd9-142">Get connection information</span></span>
<span data-ttu-id="15dd9-143">取得 PostgreSQL hello 連線所需的資訊 tooconnect toohello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="15dd9-143">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="15dd9-144">您需要 hello 完整的伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="15dd9-144">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="15dd9-145">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="15dd9-145">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="15dd9-146">在 Azure 入口網站中的 hello 左側功能表中按一下**所有資源**，並搜尋您已經建立，例如 hello 伺服器**mypgserver 20170401**。</span><span class="sxs-lookup"><span data-stu-id="15dd9-146">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="15dd9-147">按一下伺服器名稱，hello **mypgserver 20170401**。</span><span class="sxs-lookup"><span data-stu-id="15dd9-147">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="15dd9-148">選取 hello 伺服器**概觀**頁面。</span><span class="sxs-lookup"><span data-stu-id="15dd9-148">Select hello server's **Overview** page.</span></span> <span data-ttu-id="15dd9-149">請記下 hello**伺服器名稱**和**伺服器系統管理員登入名稱**。</span><span class="sxs-lookup"><span data-stu-id="15dd9-149">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="15dd9-150">![Azure Database for PostgreSQL - 伺服器管理員登入](./media/connect-go/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="15dd9-150">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-go/1-connection-string.png)</span></span>
5. <span data-ttu-id="15dd9-151">如果您忘記您的伺服器登入資訊，請瀏覽 toohello**概觀** 頁面上，並檢視 hello 伺服器系統管理員登入名稱。</span><span class="sxs-lookup"><span data-stu-id="15dd9-151">If you forget your server login information, navigate toohello **Overview** page, and view hello Server admin login name.</span></span> <span data-ttu-id="15dd9-152">如有需要，重設 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="15dd9-152">If necessary, reset hello password.</span></span>

## <a name="build-and-run-go-code"></a><span data-ttu-id="15dd9-153">建置並執行 Go 程式碼</span><span class="sxs-lookup"><span data-stu-id="15dd9-153">Build and run Go code</span></span> 
1. <span data-ttu-id="15dd9-154">toowrite Golang 程式碼，您可以使用簡單的文字編輯器，例如 [記事本] 在 Windows 中， [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5)或[Nano](https://www.nano-editor.org/) Ubuntu 或在 macOS TextEdit 中。</span><span class="sxs-lookup"><span data-stu-id="15dd9-154">toowrite Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="15dd9-155">如果想要使用更豐富的互動式開發環境 (IDE)，您可以選擇 Jetbrains 的 [Gogland](https://www.jetbrains.com/go/)、Microsoft 的 [Visual Studio Code](https://code.visualstudio.com/)，或 [Atom](https://atom.io/)。</span><span class="sxs-lookup"><span data-stu-id="15dd9-155">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="15dd9-156">從下方的 hello 區段的 hello Golang 程式碼貼入文字檔案，並儲存到專案資料夾中副檔名\*.go，例如 Windows 路徑`%USERPROFILE%\go\src\postgresqlgo\createtable.go`或 Linux 路徑`~/go/src/postgresqlgo/createtable.go`。</span><span class="sxs-lookup"><span data-stu-id="15dd9-156">Paste hello Golang code from hello sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\postgresqlgo\createtable.go` or Linux path `~/go/src/postgresqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="15dd9-157">找出 hello `HOST`， `DATABASE`， `USER`，和`PASSWORD`hello 程式碼，並以您自己的值取代 hello 範例值中的常數。</span><span class="sxs-lookup"><span data-stu-id="15dd9-157">Locate hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in hello code, and replace hello example values with your own values.</span></span>  
4. <span data-ttu-id="15dd9-158">啟動 hello 命令提示字元，或被殼層。</span><span class="sxs-lookup"><span data-stu-id="15dd9-158">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="15dd9-159">將目錄切換到專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="15dd9-159">Change directory into your project folder.</span></span> <span data-ttu-id="15dd9-160">例如，在 Windows 上為 `cd %USERPROFILE%\go\src\postgresqlgo\`。</span><span class="sxs-lookup"><span data-stu-id="15dd9-160">For example, on Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span></span> <span data-ttu-id="15dd9-161">在 Linux 上為 `cd ~/go/src/postgresqlgo/`。</span><span class="sxs-lookup"><span data-stu-id="15dd9-161">On Linux `cd ~/go/src/postgresqlgo/`.</span></span> <span data-ttu-id="15dd9-162">部分所述的 hello IDE 環境提供偵錯和執行階段功能而不需要殼層命令。</span><span class="sxs-lookup"><span data-stu-id="15dd9-162">Some of hello IDE environments mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="15dd9-163">輸入 hello 命令執行 hello 程式碼`go run createtable.go`toocompile hello 應用程式，並執行它。</span><span class="sxs-lookup"><span data-stu-id="15dd9-163">Run hello code by typing hello command `go run createtable.go` toocompile hello application and run it.</span></span> 
6. <span data-ttu-id="15dd9-164">或者，toobuild hello 碼轉換為原生應用程式， `go build createtable.go`，然後啟動`createtable.exe`toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="15dd9-164">Alternatively, toobuild hello code into a native application, `go build createtable.go`, then launch `createtable.exe` toorun hello application.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="15dd9-165">連線及建立資料表</span><span class="sxs-lookup"><span data-stu-id="15dd9-165">Connect and create a table</span></span>
<span data-ttu-id="15dd9-166">使用 hello 下列程式碼 tooconnect 並建立資料表，使用**CREATE TABLE** SQL 陳述式，後面接著**INSERT INTO** hello 資料表的 SQL 陳述式 tooadd 資料列。</span><span class="sxs-lookup"><span data-stu-id="15dd9-166">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="15dd9-167">hello 程式碼匯入三個封裝： hello [sql 封裝](https://golang.org/pkg/database/sql/)，hello [pq 封裝](http://godoc.org/github.com/lib/pq)為 hello hello Postgres 伺服器，與驅動程式 toocommunicate [fmt 封裝](https://golang.org/pkg/fmt/)列印輸入和輸出 hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="15dd9-167">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="15dd9-168">hello 程式碼呼叫方法[sql。Open （)](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure PostgreSQL 和使用方法檢查 hello 連接資料庫的[db。Ping()](https://golang.org/pkg/database/sql/#DB.Ping)。</span><span class="sxs-lookup"><span data-stu-id="15dd9-168">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="15dd9-169">A[資料庫控制代碼](https://golang.org/pkg/database/sql/#DB)會完全使用，保留 hello hello 的資料庫伺服器的連接集區。</span><span class="sxs-lookup"><span data-stu-id="15dd9-169">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="15dd9-170">hello 程式碼呼叫 hello [exec （)](https://golang.org/pkg/database/sql/#DB.Exec)方法多次 toorun 數個 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="15dd9-170">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times toorun several SQL commands.</span></span> <span data-ttu-id="15dd9-171">每次自訂 checkError() 方法 toocheck，如果發生錯誤，且驚慌 tooexit，如果發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="15dd9-171">Each time a custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="15dd9-172">取代 hello `HOST`， `DATABASE`， `USER`，和`PASSWORD`參數以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="15dd9-172">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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
    fmt.Println("Successfully created connection toodatabase")

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

## <a name="read-data"></a><span data-ttu-id="15dd9-173">讀取資料</span><span class="sxs-lookup"><span data-stu-id="15dd9-173">Read data</span></span>
<span data-ttu-id="15dd9-174">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**選取**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="15dd9-174">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="15dd9-175">hello 程式碼匯入三個封裝： hello [sql 封裝](https://golang.org/pkg/database/sql/)，hello [pq 封裝](http://godoc.org/github.com/lib/pq)為 hello hello Postgres 伺服器，與驅動程式 toocommunicate [fmt 封裝](https://golang.org/pkg/fmt/)列印輸入和輸出 hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="15dd9-175">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="15dd9-176">hello 程式碼呼叫方法[sql。Open （)](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure PostgreSQL 和使用方法檢查 hello 連接資料庫的[db。Ping()](https://golang.org/pkg/database/sql/#DB.Ping)。</span><span class="sxs-lookup"><span data-stu-id="15dd9-176">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="15dd9-177">A[資料庫控制代碼](https://golang.org/pkg/database/sql/#DB)會完全使用，保留 hello hello 的資料庫伺服器的連接集區。</span><span class="sxs-lookup"><span data-stu-id="15dd9-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="15dd9-178">呼叫方法來執行 hello select 查詢[db。Query （)](https://golang.org/pkg/database/sql/#DB.Query)，並且 hello 產生的資料列會保留在類型的變數[列](https://golang.org/pkg/database/sql/#Rows)。</span><span class="sxs-lookup"><span data-stu-id="15dd9-178">hello select query is run by calling method [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), and hello resulting rows is kept in a variable of type [rows](https://golang.org/pkg/database/sql/#Rows).</span></span> <span data-ttu-id="15dd9-179">hello 程式碼會讀取使用方法 hello 目前資料列中的 hello 資料行資料值[資料列。Scan()](https://golang.org/pkg/database/sql/#Rows.Scan)和 hello 資料列使用 hello 迭代器，透過迴圈[資料列。Next （)](https://golang.org/pkg/database/sql/#Rows.Next)直到沒有其他資料列存在。</span><span class="sxs-lookup"><span data-stu-id="15dd9-179">hello code reads hello column data values in hello current row using method [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) and loops over hello rows using hello iterator [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) until no more rows exist.</span></span> <span data-ttu-id="15dd9-180">每個資料列的資料行值為出列印的 toohello 主控台。每次自訂 checkError() 方法 toocheck，如果發生錯誤，且驚慌 tooexit，如果發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="15dd9-180">Each row's column values are printed toohello console out. Each time a custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="15dd9-181">取代 hello `HOST`， `DATABASE`， `USER`，和`PASSWORD`參數以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="15dd9-181">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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
    fmt.Println("Successfully created connection toodatabase")

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

## <a name="update-data"></a><span data-ttu-id="15dd9-182">更新資料</span><span class="sxs-lookup"><span data-stu-id="15dd9-182">Update data</span></span>
<span data-ttu-id="15dd9-183">使用 hello 下列程式碼 tooconnect 並更新 hello 資料使用**更新**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="15dd9-183">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="15dd9-184">hello 程式碼匯入三個封裝： hello [sql 封裝](https://golang.org/pkg/database/sql/)，hello [pq 封裝](http://godoc.org/github.com/lib/pq)為 hello hello Postgres 伺服器，與驅動程式 toocommunicate [fmt 封裝](https://golang.org/pkg/fmt/)列印輸入和輸出 hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="15dd9-184">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="15dd9-185">hello 程式碼呼叫方法[sql。Open （)](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure PostgreSQL 和使用方法檢查 hello 連接資料庫的[db。Ping()](https://golang.org/pkg/database/sql/#DB.Ping)。</span><span class="sxs-lookup"><span data-stu-id="15dd9-185">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="15dd9-186">A[資料庫控制代碼](https://golang.org/pkg/database/sql/#DB)會完全使用，保留 hello hello 的資料庫伺服器的連接集區。</span><span class="sxs-lookup"><span data-stu-id="15dd9-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="15dd9-187">hello 程式碼呼叫 hello [exec （)](https://golang.org/pkg/database/sql/#DB.Exec)方法 toorun hello 更新 hello 資料表的 SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="15dd9-187">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello SQL statement that updates hello table.</span></span> <span data-ttu-id="15dd9-188">自訂 checkError() 方法 toocheck 如果發生錯誤，而驚慌 tooexit 錯誤時，就會發生。</span><span class="sxs-lookup"><span data-stu-id="15dd9-188">A custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="15dd9-189">取代 hello `HOST`， `DATABASE`， `USER`，和`PASSWORD`參數以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="15dd9-189">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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
    fmt.Println("Successfully created connection toodatabase")

    // Modify some data in table.
    sql_statement := "UPDATE inventory SET quantity = $2 WHERE name = $1;"
    _, err = db.Exec(sql_statement, "banana", 200)
    checkError(err)
    fmt.Println("Updated 1 row of data")
}
```

## <a name="delete-data"></a><span data-ttu-id="15dd9-190">刪除資料</span><span class="sxs-lookup"><span data-stu-id="15dd9-190">Delete data</span></span>
<span data-ttu-id="15dd9-191">使用 hello 下列程式碼 tooconnect 並讀取 hello 資料使用**刪除**SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="15dd9-191">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="15dd9-192">hello 程式碼匯入三個封裝： hello [sql 封裝](https://golang.org/pkg/database/sql/)，hello [pq 封裝](http://godoc.org/github.com/lib/pq)為 hello hello Postgres 伺服器，與驅動程式 toocommunicate [fmt 封裝](https://golang.org/pkg/fmt/)列印輸入和輸出 hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="15dd9-192">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="15dd9-193">hello 程式碼呼叫方法[sql。Open （)](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure PostgreSQL 和使用方法檢查 hello 連接資料庫的[db。Ping()](https://golang.org/pkg/database/sql/#DB.Ping)。</span><span class="sxs-lookup"><span data-stu-id="15dd9-193">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="15dd9-194">A[資料庫控制代碼](https://golang.org/pkg/database/sql/#DB)會完全使用，保留 hello hello 的資料庫伺服器的連接集區。</span><span class="sxs-lookup"><span data-stu-id="15dd9-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="15dd9-195">hello 程式碼呼叫 hello [exec （)](https://golang.org/pkg/database/sql/#DB.Exec)方法 toorun hello 更新 hello 資料表的 SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="15dd9-195">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello SQL statement that updates hello table.</span></span> <span data-ttu-id="15dd9-196">自訂 checkError() 方法 toocheck 如果發生錯誤，而驚慌 tooexit 錯誤時，就會發生。</span><span class="sxs-lookup"><span data-stu-id="15dd9-196">A custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="15dd9-197">取代 hello `HOST`， `DATABASE`， `USER`，和`PASSWORD`參數以您自己的值。</span><span class="sxs-lookup"><span data-stu-id="15dd9-197">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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
    fmt.Println("Successfully created connection toodatabase")

    // Delete some data from table.
    sql_statement := "DELETE FROM inventory WHERE name = $1;"
    _, err = db.Exec(sql_statement, "orange")
    checkError(err)
    fmt.Println("Deleted 1 row of data")
}
```

## <a name="next-steps"></a><span data-ttu-id="15dd9-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="15dd9-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="15dd9-199">使用匯出和匯入來移轉資料庫</span><span class="sxs-lookup"><span data-stu-id="15dd9-199">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)

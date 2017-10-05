---
title: "在 Azure 中建置 Docker Python 和 PostgreSQL Web 應用程式 | Microsoft Docs"
description: "了解如何取得在 Azure 中運作的 Docker Python 應用程式，並連線至 PostgreSQL 資料庫。"
services: app-service\web
documentationcenter: python
author: berndverst
manager: erikre
editor: 
ms.assetid: 2bada123-ef18-44e5-be71-e16323b20466
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: tutorial
ms.date: 05/03/2017
ms.author: beverst
ms.custom: mvc
ms.openlocfilehash: e70f85a1eb4a6e1a81e0ca4fae228ca97deca6fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a><span data-ttu-id="97307-103">在 Azure 中建置 Docker Python 和 PostgreSQL Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="97307-103">Build a Docker Python and PostgreSQL web app in Azure</span></span>

<span data-ttu-id="97307-104">Azure Web Apps 提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="97307-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="97307-105">本教學課程會示範如何在 Azure 中建立基本的 Docker Python Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="97307-105">This tutorial shows how to create a basic Docker Python web app in Azure.</span></span> <span data-ttu-id="97307-106">您會將此應用程式連線至 PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="97307-106">You'll connect this app to a PostgreSQL database.</span></span> <span data-ttu-id="97307-107">完成之後，您在 [Azure App Service Web Apps](app-service-web-overview.md) 上就會有 Docker 容器內執行的 Python Flask 應用程式。</span><span class="sxs-lookup"><span data-stu-id="97307-107">When you're done, you'll have a Python Flask application running within a Docker container on [Azure App Service Web Apps](app-service-web-overview.md).</span></span>

![Azure App Service 中的 Docker Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

<span data-ttu-id="97307-109">您可以在 Mac OS 上依照下列步驟進行。</span><span class="sxs-lookup"><span data-stu-id="97307-109">You can follow the steps below on macOS.</span></span> <span data-ttu-id="97307-110">Linux 和 Windows 指示在大部分情況下都相同，本教學課程對差異不加詳述。</span><span class="sxs-lookup"><span data-stu-id="97307-110">Linux and Windows instructions are the same in most cases, but the differences are not detailed in this tutorial.</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="97307-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="97307-111">Prerequisites</span></span>

<span data-ttu-id="97307-112">若要完成本教學課程：</span><span class="sxs-lookup"><span data-stu-id="97307-112">To complete this tutorial:</span></span>

1. [<span data-ttu-id="97307-113">安裝 Git</span><span class="sxs-lookup"><span data-stu-id="97307-113">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="97307-114">安裝 Python</span><span class="sxs-lookup"><span data-stu-id="97307-114">Install Python</span></span>](https://www.python.org/downloads/)
1. [<span data-ttu-id="97307-115">安裝及執行 PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="97307-115">Install and run PostgreSQL</span></span>](https://www.postgresql.org/download/)
1. [<span data-ttu-id="97307-116">安裝 Docker Community 版本</span><span class="sxs-lookup"><span data-stu-id="97307-116">Install Docker Community Edition</span></span>](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="97307-117">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="97307-117">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="97307-118">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="97307-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="97307-119">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="97307-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-postgresql-installation-and-create-a-database"></a><span data-ttu-id="97307-120">測試本機 PostgreSQL 安裝並建立資料庫</span><span class="sxs-lookup"><span data-stu-id="97307-120">Test local PostgreSQL installation and create a database</span></span>

<span data-ttu-id="97307-121">開啟終端機視窗，然後執行 `psql postgres` 來連線至本機 PostgreSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="97307-121">Open the terminal window and run `psql postgres` to connect to your local PostgreSQL server.</span></span>

```bash
psql postgres
```

<span data-ttu-id="97307-122">如果連線成功，則您的 PostgreSQL 資料庫就已在執行中。</span><span class="sxs-lookup"><span data-stu-id="97307-122">If your connection is successful, your PostgreSQL database is running.</span></span> <span data-ttu-id="97307-123">如果沒有，請確定您的本機 PostgresQL 資料庫已遵循[下載 - PostgresQL 核心散發](https://www.postgresql.org/download/)中的步驟來啟動。</span><span class="sxs-lookup"><span data-stu-id="97307-123">If not, make sure that your local PostgresQL database is started by following the steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span></span>

<span data-ttu-id="97307-124">建立名為 eventregistration 的資料庫，並且設定名為 manager、密碼為 supersecretpass 的個別資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="97307-124">Create a database called *eventregistration* and set up a separate database user named *manager* with password *supersecretpass*.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration TO manager;
```
<span data-ttu-id="97307-125">輸入 \q 來結束 PostgreSQL 用戶端。</span><span class="sxs-lookup"><span data-stu-id="97307-125">Type *\q* to exit the PostgreSQL client.</span></span> 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a><span data-ttu-id="97307-126">建立本機 Python Flask 應用程式</span><span class="sxs-lookup"><span data-stu-id="97307-126">Create local Python Flask application</span></span>

<span data-ttu-id="97307-127">在此步驟中，您要設定本機 Python Flask 專案。</span><span class="sxs-lookup"><span data-stu-id="97307-127">In this step, you set up the local Python Flask project.</span></span>

### <a name="clone-the-sample-application"></a><span data-ttu-id="97307-128">複製範例應用程式</span><span class="sxs-lookup"><span data-stu-id="97307-128">Clone the sample application</span></span>

<span data-ttu-id="97307-129">開啟終端機視窗，然後 `CD` 至工作目錄。</span><span class="sxs-lookup"><span data-stu-id="97307-129">Open the terminal window, and `CD` to a working directory.</span></span>  

<span data-ttu-id="97307-130">執行下列命令來複製範例存放庫，然後前往 0.1-initialapp 版本。</span><span class="sxs-lookup"><span data-stu-id="97307-130">Run the following commands to clone the sample repository and go to the *0.1-initialapp* release.</span></span>

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

<span data-ttu-id="97307-131">此範例存放庫包含 [Flask](http://flask.pocoo.org/) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="97307-131">This sample repository contains a [Flask](http://flask.pocoo.org/) application.</span></span> 

### <a name="run-the-application"></a><span data-ttu-id="97307-132">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="97307-132">Run the application</span></span>

> [!NOTE] 
> <span data-ttu-id="97307-133">在稍後步驟中簡化這個程序，方法是建立可與生產環境資料庫搭配使用的 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="97307-133">In a later step you simplify this process by building a Docker container to use with the production database.</span></span>

<span data-ttu-id="97307-134">安裝必要的封裝，然後啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="97307-134">Install the required packages and start the application.</span></span>

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="97307-135">當應用程式完全載入時，您會看到類似下列的訊息：</span><span class="sxs-lookup"><span data-stu-id="97307-135">When the app is fully loaded, you see something similar to the following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="97307-136">在瀏覽器中，瀏覽至 http://127.0.0.1:5000 。</span><span class="sxs-lookup"><span data-stu-id="97307-136">Navigate to http://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="97307-137">按一下 [註冊!]</span><span class="sxs-lookup"><span data-stu-id="97307-137">Click **Register!**</span></span> <span data-ttu-id="97307-138">並且建立測試使用者。</span><span class="sxs-lookup"><span data-stu-id="97307-138">and create a test user.</span></span>

![在本機執行的 Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

<span data-ttu-id="97307-140">Flask 範例應用程式會將使用者資料儲存於資料庫中。</span><span class="sxs-lookup"><span data-stu-id="97307-140">The Flask sample application stores user data in the database.</span></span> <span data-ttu-id="97307-141">如果您成功註冊使用者，您的應用程式會將資料寫入本機 PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="97307-141">If you are successful at registering a user, your app is writing data to the local PostgreSQL database.</span></span>

<span data-ttu-id="97307-142">如需隨時停止 Flask 伺服器，請在終端機上輸入 Ctrl+C。</span><span class="sxs-lookup"><span data-stu-id="97307-142">To stop the Flask server at anytime, type Ctrl+C in the terminal.</span></span> 

## <a name="create-a-production-postgresql-database"></a><span data-ttu-id="97307-143">建立生產環境 PostgreSQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="97307-143">Create a production PostgreSQL database</span></span>

<span data-ttu-id="97307-144">在此步驟中，您要在 Azure 中建立 PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="97307-144">In this step, you create a PostgreSQL database in Azure.</span></span> <span data-ttu-id="97307-145">當您的應用程式部署至 Azure 時，它會使用此雲端資料庫。</span><span class="sxs-lookup"><span data-stu-id="97307-145">When your app is deployed to Azure, it will use this cloud database.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="97307-146">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="97307-146">Log in to Azure</span></span>

<span data-ttu-id="97307-147">您即將使用 Azure CLI 2.0，來建立在 Azure App Service 中裝載 Python 應用程式所需的資源。</span><span class="sxs-lookup"><span data-stu-id="97307-147">You are now going to use the Azure CLI 2.0 to create the resources needed to host your Python application in Azure App Service.</span></span>  <span data-ttu-id="97307-148">使用 [az login](/cli/azure/#login) 命令登入 Azure 訂用帳戶並遵循畫面上的指示。</span><span class="sxs-lookup"><span data-stu-id="97307-148">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="97307-149">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="97307-149">Create a resource group</span></span>

<span data-ttu-id="97307-150">使用 [az group create](../azure-resource-manager/resource-group-overview.md) 來建立[資源群組](/cli/azure/group#create)。</span><span class="sxs-lookup"><span data-stu-id="97307-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#create).</span></span> 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="97307-151">下列範例會在美國西部區域中建立一個資源群組：</span><span class="sxs-lookup"><span data-stu-id="97307-151">The following example creates a resource group in the West US region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

<span data-ttu-id="97307-152">使用 [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI 命令以列出可用的位置。</span><span class="sxs-lookup"><span data-stu-id="97307-152">Use the [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command to list available locations.</span></span>

### <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="97307-153">建立適用於 PostgreSQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="97307-153">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="97307-154">使用 [az postgres server create](/cli/azure/documentdb#create) 命令來建立 PostgreSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="97307-154">Create a PostgreSQL server with the [az postgres server create](/cli/azure/documentdb#create) command.</span></span>

<span data-ttu-id="97307-155">在下列命令中，使用唯一的伺服器名稱取代 \<postgresql_name> 預留位置，以及用使用者名稱取代 \<admin_username> 預留位置。</span><span class="sxs-lookup"><span data-stu-id="97307-155">In the following command, substitute a unique server name for the *\<postgresql_name>* placeholder and a user name for the *\<admin_username>* placeholder.</span></span> <span data-ttu-id="97307-156">這個伺服器名稱會用來作為 PostgreSQL 端點 (`https://<postgresql_name>.postgres.database.azure.com`) 的一部分，所以在 Azure 的所有伺服器中必須是唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="97307-156">The server name is used as part of your PostgreSQL endpoint (`https://<postgresql_name>.postgres.database.azure.com`), so the name needs to be unique across all servers in Azure.</span></span> <span data-ttu-id="97307-157">使用者名稱是用於初始資料庫管理使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="97307-157">The user name is for the initial database admin user account.</span></span> <span data-ttu-id="97307-158">系統會提示您選取此使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="97307-158">You are prompted to pick a password for this user.</span></span>

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

<span data-ttu-id="97307-159">建立適用於 PostgreSQL 的 Azure 資料庫伺服器後，Azure CLI 會顯示類似下列範例的資訊：</span><span class="sxs-lookup"><span data-stu-id="97307-159">When the Azure Database for PostgreSQL server is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "administratorLogin": "<my_admin_username>",
  "fullyQualifiedDomainName": "<postgresql_name>.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>",
  "location": "westus",
  "name": "<postgresql_name>",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": 100,
    "family": null,
    "name": "PGSQLS3M100",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

### <a name="create-a-firewall-rule-for-the-azure-database-for-postgresql-server"></a><span data-ttu-id="97307-160">建立適用於 PostgreSQL 的 Azure 資料庫伺服器防火牆規則</span><span class="sxs-lookup"><span data-stu-id="97307-160">Create a firewall rule for the Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="97307-161">執行下列 Azure CLI 命令，允許從所有 IP 位址存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="97307-161">Run the following Azure CLI command to allow access to the database from all IP addresses.</span></span>

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

<span data-ttu-id="97307-162">Azure CLI 確認防火牆規則建立，具有類似下列範例的輸出：</span><span class="sxs-lookup"><span data-stu-id="97307-162">The Azure CLI confirms the firewall rule creation with output similar to the following example:</span></span>

```json
{
  "endIpAddress": "255.255.255.255",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>/firewallRules/AllowAllIPs",
  "name": "AllowAllIPs",
  "resourceGroup": "myResourceGroup",
  "startIpAddress": "0.0.0.0",
  "type": "Microsoft.DBforPostgreSQL/servers/firewallRules"
}
```

## <a name="connect-your-python-flask-application-to-the-database"></a><span data-ttu-id="97307-163">將 Python Flask 應用程式連線至資料庫</span><span class="sxs-lookup"><span data-stu-id="97307-163">Connect your Python Flask application to the database</span></span>

<span data-ttu-id="97307-164">在此步驟中，您要將 Python Flask 範例應用程式連線至適用於您所建立之適用於 PostgreSQL 的 Azure 資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="97307-164">In this step, you connect your Python Flask sample application to the Azure Database for PostgreSQL server you created.</span></span>

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a><span data-ttu-id="97307-165">建立空的資料庫並設定新的資料庫應用程式使用者</span><span class="sxs-lookup"><span data-stu-id="97307-165">Create an empty database and set up a new database application user</span></span>

<span data-ttu-id="97307-166">建立資料庫使用者，並僅提供單一資料庫的存取權。</span><span class="sxs-lookup"><span data-stu-id="97307-166">Create a database user with access to a single database only.</span></span> <span data-ttu-id="97307-167">您將會使用這些認證以避免將伺服器的完整存取權給予應用程式。</span><span class="sxs-lookup"><span data-stu-id="97307-167">You'll use these credentials to avoid giving the application full access to the server.</span></span>

<span data-ttu-id="97307-168">連線至資料庫 (系統會提示您輸入管理員密碼)。</span><span class="sxs-lookup"><span data-stu-id="97307-168">Connect to the database (you're prompted for your admin password).</span></span>

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

<span data-ttu-id="97307-169">從 PostgreSQL CLI 建立資料庫和使用者。</span><span class="sxs-lookup"><span data-stu-id="97307-169">Create the database and user from the PostgreSQL CLI.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration TO manager;
```

<span data-ttu-id="97307-170">輸入 \q 來結束 PostgreSQL 用戶端。</span><span class="sxs-lookup"><span data-stu-id="97307-170">Type *\q* to exit the PostgreSQL client.</span></span>

### <a name="test-the-application-locally-against-the-azure-postgresql-database"></a><span data-ttu-id="97307-171">針對 Azure PostgreSQL 資料庫本機測試應用程式</span><span class="sxs-lookup"><span data-stu-id="97307-171">Test the application locally against the Azure PostgreSQL database</span></span> 

<span data-ttu-id="97307-172">現在回到複製的 Github 存放庫 app 資料夾，您只要更新資料庫環境變數，就可以執行 Python Flask 應用程式。</span><span class="sxs-lookup"><span data-stu-id="97307-172">Going back now to the *app* folder of the cloned Github repository, you can run the Python Flask application by updating the database environment variables.</span></span>

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="97307-173">當應用程式完全載入時，您會看到類似下列的訊息：</span><span class="sxs-lookup"><span data-stu-id="97307-173">When the app is fully loaded, you see something similar to the following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="97307-174">在瀏覽器中，瀏覽至 http://127.0.0.1:5000 。</span><span class="sxs-lookup"><span data-stu-id="97307-174">Navigate to http://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="97307-175">按一下 [註冊!]</span><span class="sxs-lookup"><span data-stu-id="97307-175">Click **Register!**</span></span> <span data-ttu-id="97307-176">並且建立測試註冊。</span><span class="sxs-lookup"><span data-stu-id="97307-176">and create a test registration.</span></span> <span data-ttu-id="97307-177">現在您要將資料寫入 Azure 中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="97307-177">You are now writing data to the database in Azure.</span></span>

![在本機執行的 Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-the-application-from-a-docker-container"></a><span data-ttu-id="97307-179">從 Docker 容器執行應用程式</span><span class="sxs-lookup"><span data-stu-id="97307-179">Running the application from a Docker Container</span></span>

<span data-ttu-id="97307-180">建置 Docker 容器映像。</span><span class="sxs-lookup"><span data-stu-id="97307-180">Build the Docker container image.</span></span>

```bash
cd ..
docker build -t flask-postgresql-sample .
```

<span data-ttu-id="97307-181">Docker 會顯示已成功建立容器的確認。</span><span class="sxs-lookup"><span data-stu-id="97307-181">Docker displays a confirmation that it successfully created the container.</span></span>

```bash
Successfully built 7548f983a36b
```

<span data-ttu-id="97307-182">將資料庫環境變數新增至環境變數檔案 db.env。</span><span class="sxs-lookup"><span data-stu-id="97307-182">Add database environment variables to an environment variable file *db.env*.</span></span> <span data-ttu-id="97307-183">應用程式會連線至 Azure 中的 PostgreSQL 生產環境資料庫。</span><span class="sxs-lookup"><span data-stu-id="97307-183">The app will connect to the PostgreSQL production database in Azure.</span></span>

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

<span data-ttu-id="97307-184">從 Docker 容器內執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="97307-184">Run the app from within the Docker container.</span></span> <span data-ttu-id="97307-185">下列命令會指定環境變數檔案，並將預設 Flask 連接埠 5000 對應至本機連接埠 5000。</span><span class="sxs-lookup"><span data-stu-id="97307-185">The following command specifies the environment variable file and maps the default Flask port 5000 to local port 5000.</span></span>

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

<span data-ttu-id="97307-186">輸出類似您稍早所見的範例。</span><span class="sxs-lookup"><span data-stu-id="97307-186">The output is similar to what you saw earlier.</span></span> <span data-ttu-id="97307-187">不過，不再需要執行初始資料庫移轉，因此會予以略過。</span><span class="sxs-lookup"><span data-stu-id="97307-187">However, the initial database migration no longer needs to be performed and therefore is skipped.</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="97307-188">資料庫已包含您先前建立的註冊。</span><span class="sxs-lookup"><span data-stu-id="97307-188">The database already contains the registration you created previously.</span></span>

![以 Docker 容器為基礎在本機執行的 Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-the-docker-container-to-a-container-registry"></a><span data-ttu-id="97307-190">將 Docker 容器上傳至容器登錄</span><span class="sxs-lookup"><span data-stu-id="97307-190">Upload the Docker container to a container registry</span></span>

<span data-ttu-id="97307-191">在此步驟中，將 Docker 容器上傳至容器登錄。</span><span class="sxs-lookup"><span data-stu-id="97307-191">In this step, you upload the Docker container to a container registry.</span></span> <span data-ttu-id="97307-192">您將會使用 Azure Container Registry，但是您也可以使用 Docker Hub 等其他熱門的項目。</span><span class="sxs-lookup"><span data-stu-id="97307-192">You'll use Azure Container Registry, but you could also use other popular ones such as Docker Hub.</span></span>

### <a name="create-an-azure-container-registry"></a><span data-ttu-id="97307-193">建立 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="97307-193">Create an Azure Container Registry</span></span>

<span data-ttu-id="97307-194">在下列命令中，建立容器登錄，將 \<registry_name> 取代為您選擇的唯一 Azure Container Registry 名稱。</span><span class="sxs-lookup"><span data-stu-id="97307-194">In the following command to create a container registry replace *\<registry_name>* with a unique Azure container registry name of your choice.</span></span>

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

<span data-ttu-id="97307-195">輸出</span><span class="sxs-lookup"><span data-stu-id="97307-195">Output</span></span>
```json
{
  "adminUserEnabled": false,
  "creationDate": "2017-05-04T08:50:55.635688+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/<registry_name>",
  "location": "westus",
  "loginServer": "<registry_name>.azurecr.io",
  "name": "<registry_name>",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "<registry_name>01234"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

### <a name="retrieve-the-registry-credentials-for-pushing-and-pulling-docker-images"></a><span data-ttu-id="97307-196">擷取用來推送及提取 Docker 映像的登錄認證</span><span class="sxs-lookup"><span data-stu-id="97307-196">Retrieve the registry credentials for pushing and pulling Docker images</span></span>

<span data-ttu-id="97307-197">若要顯示登錄認證，請先啟用管理員模式。</span><span class="sxs-lookup"><span data-stu-id="97307-197">To show registry credentials, enable admin mode first.</span></span>

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

<span data-ttu-id="97307-198">您會看到兩個密碼。</span><span class="sxs-lookup"><span data-stu-id="97307-198">You see two passwords.</span></span> <span data-ttu-id="97307-199">請記下使用者名稱和第一個密碼。</span><span class="sxs-lookup"><span data-stu-id="97307-199">Make note of the user name and the first password.</span></span>

```json
{
  "passwords": [
    {
      "name": "password",
      "value": "<registry_password>"
    },
    {
      "name": "password2",
      "value": "<registry_password2>"
    }
  ],
  "username": "<registry_name>"
}
```

### <a name="upload-your-docker-container-to-azure-container-registry"></a><span data-ttu-id="97307-200">將 Docker 容器上傳至 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="97307-200">Upload your Docker container to Azure Container Registry</span></span>

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-the-docker-python-flask-application-to-azure"></a><span data-ttu-id="97307-201">將 Docker Python Flask 應用程式部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="97307-201">Deploy the Docker Python Flask application to Azure</span></span>

<span data-ttu-id="97307-202">在此步驟中，您可以將以 Docker 容器為基礎的 Python Flask 應用程式部署至 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="97307-202">In this step, you deploy your Docker container-based Python Flask application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="97307-203">建立應用程式服務方案</span><span class="sxs-lookup"><span data-stu-id="97307-203">Create an App Service plan</span></span>

<span data-ttu-id="97307-204">使用 [az appservice plan create](/cli/azure/appservice/plan#create) 命令來建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="97307-204">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="97307-205">下列範例會使用 S1 定價層，建立名為 myAppServicePlan 之以 Linux 為基礎的 App Service 方案：</span><span class="sxs-lookup"><span data-stu-id="97307-205">The following example creates a Linux-based App Service plan named *myAppServicePlan* using the S1 pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="97307-206">建立 App Service 方案後，Azure CLI 會顯示類似下列範例的資訊：</span><span class="sxs-lookup"><span data-stu-id="97307-206">When the App Service plan is created, the Azure CLI shows information similar to the following example:</span></span>

```json 
{
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West US",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "linux",
  "location": "West US",
  "maximumNumberOfWorkers": 10,
  "name": "myAppServicePlan",
  "numberOfSites": 0,
  "perSiteScaling": false,
  "provisioningState": "Succeeded",
  "reserved": true,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capabilities": null,
    "capacity": 1,
    "family": "S",
    "locations": null,
    "name": "S1",
    "size": "S1",
    "skuCapacity": null,
    "tier": "Standard"
  },
  "status": "Ready",
  "subscription": "00000000-0000-0000-0000-000000000000",
  "tags": null,
  "targetWorkerCount": 0,
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
}
``` 

### <a name="create-a-web-app"></a><span data-ttu-id="97307-207">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="97307-207">Create a web app</span></span>

<span data-ttu-id="97307-208">使用 [az webapp create](/cli/azure/webapp#create) 命令，在 myAppServicePlan App Service 方案中建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="97307-208">Create a web app in the *myAppServicePlan* App Service plan with the [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="97307-209">Web 應用程式會為您提供裝載空間來部署程式碼，以及提供 URL 讓您能夠檢視已部署的應用程式。</span><span class="sxs-lookup"><span data-stu-id="97307-209">The web app gives you a hosting space to deploy your code and provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="97307-210">用來建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="97307-210">Use  to create the web app.</span></span> 

<span data-ttu-id="97307-211">在下列命令中，將 \<app_name> 預留位置取代為唯一的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="97307-211">In the following command, replace the *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="97307-212">這個名稱是 Web 應用程式預設 URL 的一部分，因此，這個名稱在 Azure App Service 的所有應用程式中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="97307-212">This name is part of the default URL for the web app, so the name needs to be unique across all apps in Azure App Service.</span></span> 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="97307-213">建立 Web 應用程式後，Azure CLI 會顯示類似下列範例的資訊：</span><span class="sxs-lookup"><span data-stu-id="97307-213">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-the-database-environment-variables"></a><span data-ttu-id="97307-214">設定資料庫環境變數</span><span class="sxs-lookup"><span data-stu-id="97307-214">Configure the database environment variables</span></span>

<span data-ttu-id="97307-215">稍早在本教學課程中，您定義了環境變數來連線至 PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="97307-215">Earlier in the tutorial, you defined environment variables to connect to your PostgreSQL database.</span></span>

<span data-ttu-id="97307-216">在 App Service 中，您可以使用 [az webapp config appsettings set](/cli/azure/webapp/config#set) 命令將環境變數設定為「應用程式設定」。</span><span class="sxs-lookup"><span data-stu-id="97307-216">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings set](/cli/azure/webapp/config#set) command.</span></span> 

<span data-ttu-id="97307-217">下列範例會指定資料庫連線詳細資料作為應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="97307-217">The following example specifies the database connection details as app settings.</span></span> <span data-ttu-id="97307-218">它也會使用 PORT 變數，將 Docker 容器上的連接埠 5000 對應至接收連接埠 80 上的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="97307-218">It also uses the *PORT* variable to map PORT 5000 from your Docker Container to receive HTTP traffic on PORT 80.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a><span data-ttu-id="97307-219">設定 Docker 容器部署</span><span class="sxs-lookup"><span data-stu-id="97307-219">Configure Docker container deployment</span></span> 

<span data-ttu-id="97307-220">AppService 會自動下載及執行 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="97307-220">AppService can automatically download and run a Docker container.</span></span>

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

<span data-ttu-id="97307-221">每當您更新 Docker 容器或變更設定時，重新啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="97307-221">Whenever you update the Docker container or change the settings, restart the app.</span></span> <span data-ttu-id="97307-222">重新啟動可確保套用所有設定，以及從登錄提取最新容器。</span><span class="sxs-lookup"><span data-stu-id="97307-222">Restarting ensures that all settings are applied and the latest container is pulled from the registry.</span></span>

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="97307-223">瀏覽至 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="97307-223">Browse to the Azure web app</span></span> 

<span data-ttu-id="97307-224">使用 Web 瀏覽器，瀏覽至已部署的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="97307-224">Browse to the deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> <span data-ttu-id="97307-225">Web 應用程式載入的時間較久，因為在容器設定變更之後，必須下載及啟動容器。</span><span class="sxs-lookup"><span data-stu-id="97307-225">The web app takes longer to load because the container has to be downloaded and started after the container configuration is changed.</span></span>

<span data-ttu-id="97307-226">您會看到先前已註冊的來賓，儲存至上一個步驟中的 Azure 生產環境資料庫。</span><span class="sxs-lookup"><span data-stu-id="97307-226">You see previously registered guests that were saved to the Azure production database in the previous step.</span></span>

![以 Docker 容器為基礎在本機執行的 Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

<span data-ttu-id="97307-228">**恭喜！**</span><span class="sxs-lookup"><span data-stu-id="97307-228">**Congratulations!**</span></span> <span data-ttu-id="97307-229">您要在 Azure App Service 中執行以 Docker 容器為基礎的 Python Flask 應用程式。</span><span class="sxs-lookup"><span data-stu-id="97307-229">You're running a Docker container-based Python Flask app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="97307-230">更新資料模型並重新部署</span><span class="sxs-lookup"><span data-stu-id="97307-230">Update data model and redeploy</span></span>

<span data-ttu-id="97307-231">在此步驟中，您會更新來賓模式，將出席者的人數新增至每個事件註冊。</span><span class="sxs-lookup"><span data-stu-id="97307-231">In this step, you add the number of attendees to each event registration by updating the Guest model.</span></span>

<span data-ttu-id="97307-232">請使用下列 git 命令查看 0.2-migration 版本：</span><span class="sxs-lookup"><span data-stu-id="97307-232">Check out the *0.2-migration* release with the following git command:</span></span>

```bash
git checkout tags/0.2-migration
```

<span data-ttu-id="97307-233">此版本已對檢視、控制器及模型進行必要變更。</span><span class="sxs-lookup"><span data-stu-id="97307-233">This release already made the necessary changes to views, controllers, and model.</span></span> <span data-ttu-id="97307-234">它也會包含透過 alembic (`flask db migrate`) 產生的資料庫移轉。</span><span class="sxs-lookup"><span data-stu-id="97307-234">It also includes a database migration generated via *alembic* (`flask db migrate`).</span></span> <span data-ttu-id="97307-235">您可以看到透過下列 git 命令所進行的所有變更：</span><span class="sxs-lookup"><span data-stu-id="97307-235">You can see all changes made via the following git command:</span></span>

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="97307-236">本機測試您的變更</span><span class="sxs-lookup"><span data-stu-id="97307-236">Test your changes locally</span></span>

<span data-ttu-id="97307-237">透過執行 Flask 伺服器，可執行下列命令在本機測試您的變更。</span><span class="sxs-lookup"><span data-stu-id="97307-237">Run the following commands to test your changes locally by running the flask server.</span></span>

<span data-ttu-id="97307-238">Mac / Linux：</span><span class="sxs-lookup"><span data-stu-id="97307-238">Mac / Linux:</span></span>
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="97307-239">在瀏覽器中瀏覽至 http://127.0.0.1:5000 可檢視變更。</span><span class="sxs-lookup"><span data-stu-id="97307-239">Navigate to http://127.0.0.1:5000 in your browser to view the changes.</span></span> <span data-ttu-id="97307-240">建立測試註冊。</span><span class="sxs-lookup"><span data-stu-id="97307-240">Create a test registration.</span></span>

![以 Docker 容器為基礎在本機執行的 Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-to-azure"></a><span data-ttu-id="97307-242">將變更發佈至 Azure</span><span class="sxs-lookup"><span data-stu-id="97307-242">Publish changes to Azure</span></span>

<span data-ttu-id="97307-243">建立新的 Docker 映像、將其推送至容器登錄，並重新啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="97307-243">Build the new docker image, push it to the container registry, and restart the app.</span></span>

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

<span data-ttu-id="97307-244">瀏覽至 Azure Web 應用程式，然後再次嘗試執行新功能。</span><span class="sxs-lookup"><span data-stu-id="97307-244">Navigate to your Azure web app and try out the new functionality again.</span></span> <span data-ttu-id="97307-245">建立另一個事件註冊。</span><span class="sxs-lookup"><span data-stu-id="97307-245">Create another event registration.</span></span>

```bash 
http://<app_name>.azurewebsites.net 
```

![Azure App Service 中的 Docker Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="97307-247">管理您的 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="97307-247">Manage your Azure web app</span></span>

<span data-ttu-id="97307-248">請移至 [Azure 入口網站](https://portal.azure.com)，以查看您所建立的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="97307-248">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span>

<span data-ttu-id="97307-249">按一下左側功能表中的 [應用程式服務]，然後按一下 Azure Web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="97307-249">From the left menu, click **App Services**, then click the name of your Azure web app.</span></span>

![入口網站瀏覽至 Azure Web 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

<span data-ttu-id="97307-251">根據預設，入口網站會顯示 Web 應用程式的 [概觀] 分頁。</span><span class="sxs-lookup"><span data-stu-id="97307-251">By default, the portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="97307-252">此頁面可讓您檢視應用程式的執行方式。</span><span class="sxs-lookup"><span data-stu-id="97307-252">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="97307-253">您也可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。</span><span class="sxs-lookup"><span data-stu-id="97307-253">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="97307-254">分頁左側的索引標籤會顯示您可開啟的各種設定分頁。</span><span class="sxs-lookup"><span data-stu-id="97307-254">The tabs on the left side of the page show the different configuration pages you can open.</span></span>

![Azure 入口網站中的 App Service 頁面](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a><span data-ttu-id="97307-256">後續步驟</span><span class="sxs-lookup"><span data-stu-id="97307-256">Next steps</span></span>

<span data-ttu-id="97307-257">前往下一個教學課程，了解如何將自訂的 DNS 名稱對應至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="97307-257">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="97307-258">將現有的自訂 DNS 名稱對應至 Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="97307-258">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)

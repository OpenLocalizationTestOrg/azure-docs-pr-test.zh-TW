---
title: "aaaBuild Docker Python 和 PostgreSQL web 應用程式在 Azure 中 |Microsoft 文件"
description: "深入了解如何 tooget Docker Python 應用程式使用 Azure，以連接 tooa PostgreSQL 資料庫。"
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
ms.openlocfilehash: e594ef9ec8c04ef2bf725e5f998691f3fb8cf815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a><span data-ttu-id="ac563-103">在 Azure 中建置 Docker Python 和 PostgreSQL Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ac563-103">Build a Docker Python and PostgreSQL web app in Azure</span></span>

<span data-ttu-id="ac563-104">Azure Web Apps 提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="ac563-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="ac563-105">本教學課程會示範如何 toocreate 基本的 Docker Python web 應用程式在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="ac563-105">This tutorial shows how toocreate a basic Docker Python web app in Azure.</span></span> <span data-ttu-id="ac563-106">您要連接此應用程式 tooa PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ac563-106">You'll connect this app tooa PostgreSQL database.</span></span> <span data-ttu-id="ac563-107">完成之後，您在 [Azure App Service Web Apps](app-service-web-overview.md) 上就會有 Docker 容器內執行的 Python Flask 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac563-107">When you're done, you'll have a Python Flask application running within a Docker container on [Azure App Service Web Apps](app-service-web-overview.md).</span></span>

![Azure App Service 中的 Docker Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

<span data-ttu-id="ac563-109">您可以依照下列步驟來 hello macOS 上。</span><span class="sxs-lookup"><span data-stu-id="ac563-109">You can follow hello steps below on macOS.</span></span> <span data-ttu-id="ac563-110">Linux 和 Windows 的指示是在大部分情況下，hello 相同但 hello 差異不詳述於本教學課程。</span><span class="sxs-lookup"><span data-stu-id="ac563-110">Linux and Windows instructions are hello same in most cases, but hello differences are not detailed in this tutorial.</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="ac563-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="ac563-111">Prerequisites</span></span>

<span data-ttu-id="ac563-112">toocomplete 本教學課程：</span><span class="sxs-lookup"><span data-stu-id="ac563-112">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="ac563-113">安裝 Git</span><span class="sxs-lookup"><span data-stu-id="ac563-113">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="ac563-114">安裝 Python</span><span class="sxs-lookup"><span data-stu-id="ac563-114">Install Python</span></span>](https://www.python.org/downloads/)
1. [<span data-ttu-id="ac563-115">安裝及執行 PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ac563-115">Install and run PostgreSQL</span></span>](https://www.postgresql.org/download/)
1. [<span data-ttu-id="ac563-116">安裝 Docker Community 版本</span><span class="sxs-lookup"><span data-stu-id="ac563-116">Install Docker Community Edition</span></span>](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ac563-117">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ac563-117">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ac563-118">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="ac563-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ac563-119">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="ac563-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-postgresql-installation-and-create-a-database"></a><span data-ttu-id="ac563-120">測試本機 PostgreSQL 安裝並建立資料庫</span><span class="sxs-lookup"><span data-stu-id="ac563-120">Test local PostgreSQL installation and create a database</span></span>

<span data-ttu-id="ac563-121">開啟 hello 終端機視窗，然後執行`psql postgres`tooconnect tooyour 本機 PostgreSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ac563-121">Open hello terminal window and run `psql postgres` tooconnect tooyour local PostgreSQL server.</span></span>

```bash
psql postgres
```

<span data-ttu-id="ac563-122">如果連線成功，則您的 PostgreSQL 資料庫就已在執行中。</span><span class="sxs-lookup"><span data-stu-id="ac563-122">If your connection is successful, your PostgreSQL database is running.</span></span> <span data-ttu-id="ac563-123">如果沒有，請確定您的本機 PostgresQL 資料庫已啟動在 hello 步驟[下載-PostgreSQL 核心發佈](https://www.postgresql.org/download/)。</span><span class="sxs-lookup"><span data-stu-id="ac563-123">If not, make sure that your local PostgresQL database is started by following hello steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span></span>

<span data-ttu-id="ac563-124">建立名為 eventregistration 的資料庫，並且設定名為 manager、密碼為 supersecretpass 的個別資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="ac563-124">Create a database called *eventregistration* and set up a separate database user named *manager* with password *supersecretpass*.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```
<span data-ttu-id="ac563-125">型別*\q* tooexit hello PostgreSQL 用戶端。</span><span class="sxs-lookup"><span data-stu-id="ac563-125">Type *\q* tooexit hello PostgreSQL client.</span></span> 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a><span data-ttu-id="ac563-126">建立本機 Python Flask 應用程式</span><span class="sxs-lookup"><span data-stu-id="ac563-126">Create local Python Flask application</span></span>

<span data-ttu-id="ac563-127">在此步驟中，您會將設定 hello 本機 Python 酒瓶專案。</span><span class="sxs-lookup"><span data-stu-id="ac563-127">In this step, you set up hello local Python Flask project.</span></span>

### <a name="clone-hello-sample-application"></a><span data-ttu-id="ac563-128">複製 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="ac563-128">Clone hello sample application</span></span>

<span data-ttu-id="ac563-129">開啟 hello 終端機視窗，和`CD`tooa 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="ac563-129">Open hello terminal window, and `CD` tooa working directory.</span></span>  

<span data-ttu-id="ac563-130">Hello 執行的下列命令 tooclone hello 範例儲存機制，然後移至 toohello *0.1 initialapp*版本。</span><span class="sxs-lookup"><span data-stu-id="ac563-130">Run hello following commands tooclone hello sample repository and go toohello *0.1-initialapp* release.</span></span>

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

<span data-ttu-id="ac563-131">此範例存放庫包含 [Flask](http://flask.pocoo.org/) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac563-131">This sample repository contains a [Flask](http://flask.pocoo.org/) application.</span></span> 

### <a name="run-hello-application"></a><span data-ttu-id="ac563-132">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="ac563-132">Run hello application</span></span>

> [!NOTE] 
> <span data-ttu-id="ac563-133">在稍後步驟中您會藉由建置 Docker 容器 toouse 與 hello 生產資料庫簡化這個程序。</span><span class="sxs-lookup"><span data-stu-id="ac563-133">In a later step you simplify this process by building a Docker container toouse with hello production database.</span></span>

<span data-ttu-id="ac563-134">安裝所需的 hello 封裝並啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac563-134">Install hello required packages and start hello application.</span></span>

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="ac563-135">完全載入 hello 應用程式時，您會看到下列訊息類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="ac563-135">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="ac563-136">瀏覽 toohttp://127.0.0.1:5000 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="ac563-136">Navigate toohttp://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="ac563-137">按一下 [註冊!]</span><span class="sxs-lookup"><span data-stu-id="ac563-137">Click **Register!**</span></span> <span data-ttu-id="ac563-138">並且建立測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ac563-138">and create a test user.</span></span>

![在本機執行的 Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

<span data-ttu-id="ac563-140">hello 酒瓶範例應用程式會將使用者資料儲存在 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ac563-140">hello Flask sample application stores user data in hello database.</span></span> <span data-ttu-id="ac563-141">如果您成功註冊使用者時，您的應用程式會撰寫資料 toohello 本機 PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ac563-141">If you are successful at registering a user, your app is writing data toohello local PostgreSQL database.</span></span>

<span data-ttu-id="ac563-142">在任何時候、 toostop hello 酒瓶伺服器 hello 終端機中，輸入 Ctrl + C。</span><span class="sxs-lookup"><span data-stu-id="ac563-142">toostop hello Flask server at anytime, type Ctrl+C in hello terminal.</span></span> 

## <a name="create-a-production-postgresql-database"></a><span data-ttu-id="ac563-143">建立生產環境 PostgreSQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="ac563-143">Create a production PostgreSQL database</span></span>

<span data-ttu-id="ac563-144">在此步驟中，您要在 Azure 中建立 PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ac563-144">In this step, you create a PostgreSQL database in Azure.</span></span> <span data-ttu-id="ac563-145">已部署的 tooAzure 您的應用程式時，它會使用此雲端的資料庫。</span><span class="sxs-lookup"><span data-stu-id="ac563-145">When your app is deployed tooAzure, it will use this cloud database.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="ac563-146">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="ac563-146">Log in tooAzure</span></span>

<span data-ttu-id="ac563-147">您正在進行 toouse hello Azure CLI 2.0 toocreate hello 資源所需 toohost Python 應用程式在 Azure App Service 中。</span><span class="sxs-lookup"><span data-stu-id="ac563-147">You are now going toouse hello Azure CLI 2.0 toocreate hello resources needed toohost your Python application in Azure App Service.</span></span>  <span data-ttu-id="ac563-148">登入 Azure 訂用帳戶以 hello tooyour [az 登入](/cli/azure/#login)命令，並遵循螢幕上指示 hello。</span><span class="sxs-lookup"><span data-stu-id="ac563-148">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="ac563-149">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="ac563-149">Create a resource group</span></span>

<span data-ttu-id="ac563-150">建立[資源群組](../azure-resource-manager/resource-group-overview.md)以 hello [az 群組建立](/cli/azure/group#create)。</span><span class="sxs-lookup"><span data-stu-id="ac563-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create).</span></span> 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="ac563-151">hello 下列範例會建立資源群組 hello 美國西部區域中：</span><span class="sxs-lookup"><span data-stu-id="ac563-151">hello following example creates a resource group in hello West US region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

<span data-ttu-id="ac563-152">使用 hello [az appservice 列出位置](/cli/azure/appservice#list-locations)Azure CLI 命令 toolist 可用的位置。</span><span class="sxs-lookup"><span data-stu-id="ac563-152">Use hello [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command toolist available locations.</span></span>

### <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="ac563-153">建立適用於 PostgreSQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="ac563-153">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="ac563-154">建立以 hello PostgreSQL 伺服器[az postgres 伺服器建立](/cli/azure/documentdb#create)命令。</span><span class="sxs-lookup"><span data-stu-id="ac563-154">Create a PostgreSQL server with hello [az postgres server create](/cli/azure/documentdb#create) command.</span></span>

<span data-ttu-id="ac563-155">在 hello 下列命令，以取代 hello 的唯一的伺服器名稱 *\<postgresql_name >*預留位置和 hello 的使用者名稱 *\<admin_username >*預留位置.</span><span class="sxs-lookup"><span data-stu-id="ac563-155">In hello following command, substitute a unique server name for hello *\<postgresql_name>* placeholder and a user name for hello *\<admin_username>* placeholder.</span></span> <span data-ttu-id="ac563-156">hello 的伺服器名稱會做為 PostgreSQL 端點的一部分 (`https://<postgresql_name>.postgres.database.azure.com`)，因此 hello 名稱需要 toobe 唯一在 Azure 中的所有伺服器。</span><span class="sxs-lookup"><span data-stu-id="ac563-156">hello server name is used as part of your PostgreSQL endpoint (`https://<postgresql_name>.postgres.database.azure.com`), so hello name needs toobe unique across all servers in Azure.</span></span> <span data-ttu-id="ac563-157">hello 使用者名稱為 hello 初始資料庫管理員使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="ac563-157">hello user name is for hello initial database admin user account.</span></span> <span data-ttu-id="ac563-158">您必須提示的 toopick 這位使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="ac563-158">You are prompted toopick a password for this user.</span></span>

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

<span data-ttu-id="ac563-159">PostgreSQL 伺服器 hello Azure 資料庫建立時，hello Azure CLI 顯示資訊的類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="ac563-159">When hello Azure Database for PostgreSQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-firewall-rule-for-hello-azure-database-for-postgresql-server"></a><span data-ttu-id="ac563-160">建立 PostgreSQL 伺服器 hello Azure 資料庫的防火牆規則</span><span class="sxs-lookup"><span data-stu-id="ac563-160">Create a firewall rule for hello Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="ac563-161">執行的所有 IP 位址中的下列 Azure CLI 命令 tooallow access toohello 資料庫 hello。</span><span class="sxs-lookup"><span data-stu-id="ac563-161">Run hello following Azure CLI command tooallow access toohello database from all IP addresses.</span></span>

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

<span data-ttu-id="ac563-162">hello Azure CLI 使用下列範例的輸出類似 toohello 確認 hello 防火牆規則的建立：</span><span class="sxs-lookup"><span data-stu-id="ac563-162">hello Azure CLI confirms hello firewall rule creation with output similar toohello following example:</span></span>

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

## <a name="connect-your-python-flask-application-toohello-database"></a><span data-ttu-id="ac563-163">連接您的 Python 酒瓶應用程式 toohello 資料庫</span><span class="sxs-lookup"><span data-stu-id="ac563-163">Connect your Python Flask application toohello database</span></span>

<span data-ttu-id="ac563-164">在此步驟中，您可以連接您所建立的 PostgreSQL 伺服器您 Python 酒瓶範例應用程式 toohello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ac563-164">In this step, you connect your Python Flask sample application toohello Azure Database for PostgreSQL server you created.</span></span>

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a><span data-ttu-id="ac563-165">建立空的資料庫並設定新的資料庫應用程式使用者</span><span class="sxs-lookup"><span data-stu-id="ac563-165">Create an empty database and set up a new database application user</span></span>

<span data-ttu-id="ac563-166">存取 tooa 單一資料庫只能建立資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="ac563-166">Create a database user with access tooa single database only.</span></span> <span data-ttu-id="ac563-167">您將使用這些認證 tooavoid，給予 hello 應用程式的完整存取 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ac563-167">You'll use these credentials tooavoid giving hello application full access toohello server.</span></span>

<span data-ttu-id="ac563-168">連接 toohello 資料庫 （系統提示您輸入系統管理員密碼）。</span><span class="sxs-lookup"><span data-stu-id="ac563-168">Connect toohello database (you're prompted for your admin password).</span></span>

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

<span data-ttu-id="ac563-169">從 PostgreSQL CLI hello 建立 hello 資料庫和使用者。</span><span class="sxs-lookup"><span data-stu-id="ac563-169">Create hello database and user from hello PostgreSQL CLI.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```

<span data-ttu-id="ac563-170">型別*\q* tooexit hello PostgreSQL 用戶端。</span><span class="sxs-lookup"><span data-stu-id="ac563-170">Type *\q* tooexit hello PostgreSQL client.</span></span>

### <a name="test-hello-application-locally-against-hello-azure-postgresql-database"></a><span data-ttu-id="ac563-171">測試本機 hello hello Azure PostgreSQL 資料庫應用程式</span><span class="sxs-lookup"><span data-stu-id="ac563-171">Test hello application locally against hello Azure PostgreSQL database</span></span> 

<span data-ttu-id="ac563-172">返回現在 toohello*應用程式*hello 資料夾複製 Github 儲存機制，您可以藉由更新 hello 資料庫環境變數執行 hello Python 酒瓶應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac563-172">Going back now toohello *app* folder of hello cloned Github repository, you can run hello Python Flask application by updating hello database environment variables.</span></span>

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="ac563-173">完全載入 hello 應用程式時，您會看到下列訊息類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="ac563-173">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="ac563-174">瀏覽 toohttp://127.0.0.1:5000 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="ac563-174">Navigate toohttp://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="ac563-175">按一下 [註冊!]</span><span class="sxs-lookup"><span data-stu-id="ac563-175">Click **Register!**</span></span> <span data-ttu-id="ac563-176">並且建立測試註冊。</span><span class="sxs-lookup"><span data-stu-id="ac563-176">and create a test registration.</span></span> <span data-ttu-id="ac563-177">您現在要在 Azure 中，撰寫資料 toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ac563-177">You are now writing data toohello database in Azure.</span></span>

![在本機執行的 Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-hello-application-from-a-docker-container"></a><span data-ttu-id="ac563-179">執行 Docker 容器中的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="ac563-179">Running hello application from a Docker Container</span></span>

<span data-ttu-id="ac563-180">建置 hello Docker 容器映像。</span><span class="sxs-lookup"><span data-stu-id="ac563-180">Build hello Docker container image.</span></span>

```bash
cd ..
docker build -t flask-postgresql-sample .
```

<span data-ttu-id="ac563-181">Docker 顯示確認訊息已成功建立 it hello 容器。</span><span class="sxs-lookup"><span data-stu-id="ac563-181">Docker displays a confirmation that it successfully created hello container.</span></span>

```bash
Successfully built 7548f983a36b
```

<span data-ttu-id="ac563-182">新增資料庫環境變數 tooan 環境變數檔*db.env*。</span><span class="sxs-lookup"><span data-stu-id="ac563-182">Add database environment variables tooan environment variable file *db.env*.</span></span> <span data-ttu-id="ac563-183">hello 應用程式會連接 toohello PostgreSQL 生產資料庫，在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="ac563-183">hello app will connect toohello PostgreSQL production database in Azure.</span></span>

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

<span data-ttu-id="ac563-184">執行從 hello Docker 容器中的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac563-184">Run hello app from within hello Docker container.</span></span> <span data-ttu-id="ac563-185">hello 下列命令會指定 hello 環境變數的檔案並將對應 hello 預設酒瓶連接埠 5000 toolocal port 5000。</span><span class="sxs-lookup"><span data-stu-id="ac563-185">hello following command specifies hello environment variable file and maps hello default Flask port 5000 toolocal port 5000.</span></span>

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

<span data-ttu-id="ac563-186">hello 輸出是您稍早所看到的類似 toowhat。</span><span class="sxs-lookup"><span data-stu-id="ac563-186">hello output is similar toowhat you saw earlier.</span></span> <span data-ttu-id="ac563-187">不過，hello 初始資料庫移轉不需要再 toobe 執行，因此已略過。</span><span class="sxs-lookup"><span data-stu-id="ac563-187">However, hello initial database migration no longer needs toobe performed and therefore is skipped.</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="ac563-188">hello 資料庫已經包含您先前建立的 hello 註冊。</span><span class="sxs-lookup"><span data-stu-id="ac563-188">hello database already contains hello registration you created previously.</span></span>

![以 Docker 容器為基礎在本機執行的 Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-hello-docker-container-tooa-container-registry"></a><span data-ttu-id="ac563-190">上傳 hello Docker 容器 tooa 容器登錄中</span><span class="sxs-lookup"><span data-stu-id="ac563-190">Upload hello Docker container tooa container registry</span></span>

<span data-ttu-id="ac563-191">在此步驟中，您上傳 hello Docker 容器 tooa 容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="ac563-191">In this step, you upload hello Docker container tooa container registry.</span></span> <span data-ttu-id="ac563-192">您將會使用 Azure Container Registry，但是您也可以使用 Docker Hub 等其他熱門的項目。</span><span class="sxs-lookup"><span data-stu-id="ac563-192">You'll use Azure Container Registry, but you could also use other popular ones such as Docker Hub.</span></span>

### <a name="create-an-azure-container-registry"></a><span data-ttu-id="ac563-193">建立 Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="ac563-193">Create an Azure Container Registry</span></span>

<span data-ttu-id="ac563-194">在下列命令 toocreate 容器登錄中的 hello 取代 *\<registry_name >*與您所選擇的 Azure 容器登錄名稱。</span><span class="sxs-lookup"><span data-stu-id="ac563-194">In hello following command toocreate a container registry replace *\<registry_name>* with a unique Azure container registry name of your choice.</span></span>

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

<span data-ttu-id="ac563-195">輸出</span><span class="sxs-lookup"><span data-stu-id="ac563-195">Output</span></span>
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

### <a name="retrieve-hello-registry-credentials-for-pushing-and-pulling-docker-images"></a><span data-ttu-id="ac563-196">擷取推送及提取的 Docker 映像的 hello 登錄憑證</span><span class="sxs-lookup"><span data-stu-id="ac563-196">Retrieve hello registry credentials for pushing and pulling Docker images</span></span>

<span data-ttu-id="ac563-197">tooshow 登錄認證，可先讓系統管理員模式。</span><span class="sxs-lookup"><span data-stu-id="ac563-197">tooshow registry credentials, enable admin mode first.</span></span>

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

<span data-ttu-id="ac563-198">您會看到兩個密碼。</span><span class="sxs-lookup"><span data-stu-id="ac563-198">You see two passwords.</span></span> <span data-ttu-id="ac563-199">請記下 hello 使用者名稱和 hello 第一個密碼。</span><span class="sxs-lookup"><span data-stu-id="ac563-199">Make note of hello user name and hello first password.</span></span>

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

### <a name="upload-your-docker-container-tooazure-container-registry"></a><span data-ttu-id="ac563-200">上傳您的 Docker 容器 tooAzure 容器登錄中</span><span class="sxs-lookup"><span data-stu-id="ac563-200">Upload your Docker container tooAzure Container Registry</span></span>

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-hello-docker-python-flask-application-tooazure"></a><span data-ttu-id="ac563-201">部署 hello Docker Python 酒瓶應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="ac563-201">Deploy hello Docker Python Flask application tooAzure</span></span>

<span data-ttu-id="ac563-202">在此步驟中，您可以部署您 Docker 容器基礎 Python 酒瓶應用程式 tooAzure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="ac563-202">In this step, you deploy your Docker container-based Python Flask application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="ac563-203">建立應用程式服務方案</span><span class="sxs-lookup"><span data-stu-id="ac563-203">Create an App Service plan</span></span>

<span data-ttu-id="ac563-204">建立應用程式服務方案以 hello [az 應用程式服務方案建立](/cli/azure/appservice/plan#create)命令。</span><span class="sxs-lookup"><span data-stu-id="ac563-204">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="ac563-205">hello 下列範例會建立名為 Linux 為基礎的應用程式服務方案*myAppServicePlan*使用 hello S1 定價層：</span><span class="sxs-lookup"><span data-stu-id="ac563-205">hello following example creates a Linux-based App Service plan named *myAppServicePlan* using hello S1 pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="ac563-206">建立 hello 應用程式服務方案時，hello Azure CLI 顯示資訊的類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="ac563-206">When hello App Service plan is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-web-app"></a><span data-ttu-id="ac563-207">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ac563-207">Create a web app</span></span>

<span data-ttu-id="ac563-208">建立 web 應用程式在 hello *myAppServicePlan*應用程式服務方案以 hello [az webapp 建立](/cli/azure/webapp#create)命令。</span><span class="sxs-lookup"><span data-stu-id="ac563-208">Create a web app in hello *myAppServicePlan* App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="ac563-209">hello web 應用程式可讓您裝載空間 toodeploy 您的程式碼和為您提供 URL tooview hello 部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac563-209">hello web app gives you a hosting space toodeploy your code and provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="ac563-210">使用 toocreate hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac563-210">Use  toocreate hello web app.</span></span> 

<span data-ttu-id="ac563-211">在 hello 下列命令，將取代 hello  *\<app_name >*具有唯一的應用程式名稱的預留位置。</span><span class="sxs-lookup"><span data-stu-id="ac563-211">In hello following command, replace hello *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="ac563-212">這個名稱是 hello hello web 應用程式，預設 URL 的一部分，因此 hello 名稱需要 toobe 唯一跨 Azure App Service 中的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac563-212">This name is part of hello default URL for hello web app, so hello name needs toobe unique across all apps in Azure App Service.</span></span> 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="ac563-213">Hello web 應用程式建立後，hello Azure CLI 顯示資訊的類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="ac563-213">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-hello-database-environment-variables"></a><span data-ttu-id="ac563-214">設定 hello 資料庫環境變數</span><span class="sxs-lookup"><span data-stu-id="ac563-214">Configure hello database environment variables</span></span>

<span data-ttu-id="ac563-215">稍早在 hello 教學課程中，您可以定義環境變數 tooconnect tooyour PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ac563-215">Earlier in hello tutorial, you defined environment variables tooconnect tooyour PostgreSQL database.</span></span>

<span data-ttu-id="ac563-216">在應用程式服務中，您設定環境變數為_應用程式設定_使用 hello [az webapp config appsettings 組](/cli/azure/webapp/config#set)命令。</span><span class="sxs-lookup"><span data-stu-id="ac563-216">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config#set) command.</span></span> 

<span data-ttu-id="ac563-217">hello 下列範例指定 hello 資料庫連接詳細資料為應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="ac563-217">hello following example specifies hello database connection details as app settings.</span></span> <span data-ttu-id="ac563-218">它也會使用 hello*連接埠*變數 toomap PORT 5000 從您在連接埠 80 上的 Docker 容器 tooreceive HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="ac563-218">It also uses hello *PORT* variable toomap PORT 5000 from your Docker Container tooreceive HTTP traffic on PORT 80.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a><span data-ttu-id="ac563-219">設定 Docker 容器部署</span><span class="sxs-lookup"><span data-stu-id="ac563-219">Configure Docker container deployment</span></span> 

<span data-ttu-id="ac563-220">AppService 會自動下載及執行 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="ac563-220">AppService can automatically download and run a Docker container.</span></span>

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

<span data-ttu-id="ac563-221">每當您更新 hello Docker 容器，或變更 hello 設定，重新啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac563-221">Whenever you update hello Docker container or change hello settings, restart hello app.</span></span> <span data-ttu-id="ac563-222">重新啟動，可確保套用所有的設定，以及從 hello 登錄提取 hello 最新的容器。</span><span class="sxs-lookup"><span data-stu-id="ac563-222">Restarting ensures that all settings are applied and hello latest container is pulled from hello registry.</span></span>

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="ac563-223">瀏覽 toohello Azure web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ac563-223">Browse toohello Azure web app</span></span> 

<span data-ttu-id="ac563-224">瀏覽使用網頁瀏覽器 toohello 部署 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac563-224">Browse toohello deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> <span data-ttu-id="ac563-225">hello web 應用程式需要較長的 tooload 因為 hello 容器具有 toobe 下載及啟動 hello 容器組態變更之後。</span><span class="sxs-lookup"><span data-stu-id="ac563-225">hello web app takes longer tooload because hello container has toobe downloaded and started after hello container configuration is changed.</span></span>

<span data-ttu-id="ac563-226">您會看到先前註冊的來賓 hello 上一個步驟中儲存 toohello Azure 生產資料庫。</span><span class="sxs-lookup"><span data-stu-id="ac563-226">You see previously registered guests that were saved toohello Azure production database in hello previous step.</span></span>

![以 Docker 容器為基礎在本機執行的 Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

<span data-ttu-id="ac563-228">**恭喜！**</span><span class="sxs-lookup"><span data-stu-id="ac563-228">**Congratulations!**</span></span> <span data-ttu-id="ac563-229">您要在 Azure App Service 中執行以 Docker 容器為基礎的 Python Flask 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac563-229">You're running a Docker container-based Python Flask app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="ac563-230">更新資料模型並重新部署</span><span class="sxs-lookup"><span data-stu-id="ac563-230">Update data model and redeploy</span></span>

<span data-ttu-id="ac563-231">在此步驟中，您可以加入 hello 數目出席者 tooeach 事件註冊藉由更新 hello 客體模型。</span><span class="sxs-lookup"><span data-stu-id="ac563-231">In this step, you add hello number of attendees tooeach event registration by updating hello Guest model.</span></span>

<span data-ttu-id="ac563-232">簽出 hello *0.2 移轉*版本與 hello 下列 git 命令：</span><span class="sxs-lookup"><span data-stu-id="ac563-232">Check out hello *0.2-migration* release with hello following git command:</span></span>

```bash
git checkout tags/0.2-migration
```

<span data-ttu-id="ac563-233">此版本中已經完成 hello 必要的變更 tooviews、 控制站，以及模型。</span><span class="sxs-lookup"><span data-stu-id="ac563-233">This release already made hello necessary changes tooviews, controllers, and model.</span></span> <span data-ttu-id="ac563-234">它也會包含透過 alembic (`flask db migrate`) 產生的資料庫移轉。</span><span class="sxs-lookup"><span data-stu-id="ac563-234">It also includes a database migration generated via *alembic* (`flask db migrate`).</span></span> <span data-ttu-id="ac563-235">您可以看到所有透過 hello 下列 git 命令進行的變更：</span><span class="sxs-lookup"><span data-stu-id="ac563-235">You can see all changes made via hello following git command:</span></span>

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="ac563-236">本機測試您的變更</span><span class="sxs-lookup"><span data-stu-id="ac563-236">Test your changes locally</span></span>

<span data-ttu-id="ac563-237">下列命令 tootest hello 您的變更在本機執行所執行的 hello 酒瓶伺服器。</span><span class="sxs-lookup"><span data-stu-id="ac563-237">Run hello following commands tootest your changes locally by running hello flask server.</span></span>

<span data-ttu-id="ac563-238">Mac / Linux：</span><span class="sxs-lookup"><span data-stu-id="ac563-238">Mac / Linux:</span></span>
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="ac563-239">瀏覽在您的瀏覽器 tooview hello 變更 toohttp://127.0.0.1:5000。</span><span class="sxs-lookup"><span data-stu-id="ac563-239">Navigate toohttp://127.0.0.1:5000 in your browser tooview hello changes.</span></span> <span data-ttu-id="ac563-240">建立測試註冊。</span><span class="sxs-lookup"><span data-stu-id="ac563-240">Create a test registration.</span></span>

![以 Docker 容器為基礎在本機執行的 Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-tooazure"></a><span data-ttu-id="ac563-242">發行變更 tooAzure</span><span class="sxs-lookup"><span data-stu-id="ac563-242">Publish changes tooAzure</span></span>

<span data-ttu-id="ac563-243">建置 hello 新的 docker 映像，直接將其推 toohello 容器登錄中，然後重新啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac563-243">Build hello new docker image, push it toohello container registry, and restart hello app.</span></span>

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

<span data-ttu-id="ac563-244">瀏覽 tooyour Azure web 應用程式，然後再試 hello 新功能。</span><span class="sxs-lookup"><span data-stu-id="ac563-244">Navigate tooyour Azure web app and try out hello new functionality again.</span></span> <span data-ttu-id="ac563-245">建立另一個事件註冊。</span><span class="sxs-lookup"><span data-stu-id="ac563-245">Create another event registration.</span></span>

```bash 
http://<app_name>.azurewebsites.net 
```

![Azure App Service 中的 Docker Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="ac563-247">管理您的 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ac563-247">Manage your Azure web app</span></span>

<span data-ttu-id="ac563-248">移 toohello [Azure 入口網站](https://portal.azure.com)toosee hello web 應用程式所建立。</span><span class="sxs-lookup"><span data-stu-id="ac563-248">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span>

<span data-ttu-id="ac563-249">從 hello 左窗格中，按一下 **應用程式服務**，然後按一下 hello Azure web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="ac563-249">From hello left menu, click **App Services**, then click hello name of your Azure web app.</span></span>

![入口網站瀏覽 tooAzure web 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

<span data-ttu-id="ac563-251">根據預設，hello 入口網站會顯示 web 應用程式的**概觀**頁面。</span><span class="sxs-lookup"><span data-stu-id="ac563-251">By default, hello portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="ac563-252">此頁面可讓您檢視應用程式的執行方式。</span><span class="sxs-lookup"><span data-stu-id="ac563-252">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="ac563-253">您也可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。</span><span class="sxs-lookup"><span data-stu-id="ac563-253">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="ac563-254">在左邊 hello 頁面 hello hello 索引標籤會顯示 hello 不同的組態頁面，您可以開啟。</span><span class="sxs-lookup"><span data-stu-id="ac563-254">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span>

![Azure 入口網站中的 App Service 頁面](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a><span data-ttu-id="ac563-256">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ac563-256">Next steps</span></span>

<span data-ttu-id="ac563-257">前進 toohello 下一個教學課程 toolearn toomap 自訂的 DNS 名稱 tooyour web 應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="ac563-257">Advance toohello next tutorial toolearn how toomap a custom DNS name tooyour web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="ac563-258">將現有自訂 DNS 名稱 tooAzure Web 應用程式的對應</span><span class="sxs-lookup"><span data-stu-id="ac563-258">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)

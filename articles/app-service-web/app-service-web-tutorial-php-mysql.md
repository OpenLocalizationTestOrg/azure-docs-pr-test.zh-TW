---
title: "aaaBuild PHP 和 MySQL web 應用程式在 Azure 中 |Microsoft 文件"
description: "深入了解如何 tooget Azure ad 中運作的 PHP 應用程式，以連接 tooa MySQL 資料庫在 Azure 中。"
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 14feb4f3-5095-496e-9a40-690e1414bd73
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 07/21/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3c050b30e2e2c80d011bed989cd5f8cecac35d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a><span data-ttu-id="42287-103">在 Azure 中建置 PHP 和 MySQL Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="42287-103">Build a PHP and MySQL web app in Azure</span></span>

<span data-ttu-id="42287-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="42287-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="42287-105">本教學課程會示範如何 toocreate PHP web 應用程式在 Azure 中的，並將它連接 tooa MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="42287-105">This tutorial shows how toocreate a PHP web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="42287-106">完成後，您將有一個在 Azure App Service Web Apps 上執行的 [Laravel](https://laravel.com/) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="42287-106">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on Azure App Service Web Apps.</span></span>

![在 Azure App Service 中執行的 PHP 應用程式](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="42287-108">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="42287-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="42287-109">在 Azure 中建立 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="42287-109">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="42287-110">連接 PHP 應用程式 tooMySQL</span><span class="sxs-lookup"><span data-stu-id="42287-110">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="42287-111">部署 hello 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="42287-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="42287-112">更新 hello 資料模型，部署 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="42287-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="42287-113">來自 Azure 的串流診斷記錄</span><span class="sxs-lookup"><span data-stu-id="42287-113">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="42287-114">管理 hello hello Azure 入口網站中的應用程式</span><span class="sxs-lookup"><span data-stu-id="42287-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42287-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="42287-115">Prerequisites</span></span>

<span data-ttu-id="42287-116">toocomplete 本教學課程：</span><span class="sxs-lookup"><span data-stu-id="42287-116">toocomplete this tutorial:</span></span>

* [<span data-ttu-id="42287-117">安裝 Git</span><span class="sxs-lookup"><span data-stu-id="42287-117">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="42287-118">安裝 PHP 5.6.4 或更新版本</span><span class="sxs-lookup"><span data-stu-id="42287-118">Install PHP 5.6.4 or above</span></span>](http://php.net/downloads.php)
* [<span data-ttu-id="42287-119">安裝編輯器</span><span class="sxs-lookup"><span data-stu-id="42287-119">Install Composer</span></span>](https://getcomposer.org/doc/00-intro.md)
* <span data-ttu-id="42287-120">啟用下列 PHP 延伸模組 Laravel 需求 hello: OpenSSL、 PDO MySQL、 Mbstring、 Tokenizer、 XML</span><span class="sxs-lookup"><span data-stu-id="42287-120">Enable hello following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span></span>
* [<span data-ttu-id="42287-121">下載並啟動 MySQL</span><span class="sxs-lookup"><span data-stu-id="42287-121">Install and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a><span data-ttu-id="42287-122">準備本機 MySQL</span><span class="sxs-lookup"><span data-stu-id="42287-122">Prepare local MySQL</span></span>

<span data-ttu-id="42287-123">在此步驟中，您可以在本機 MySQL 伺服器中建立資料庫，供您在本教學課程中使用。</span><span class="sxs-lookup"><span data-stu-id="42287-123">In this step, you create a database in your local MySQL server for your use in this tutorial.</span></span>

### <a name="connect-toolocal-mysql-server"></a><span data-ttu-id="42287-124">Toolocal MySQL 伺服器連接</span><span class="sxs-lookup"><span data-stu-id="42287-124">Connect toolocal MySQL server</span></span>

<span data-ttu-id="42287-125">在終端機視窗中，連接 tooyour 本機 MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="42287-125">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="42287-126">您可以使用這個終端機視窗 toorun hello 的所有命令，在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="42287-126">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="42287-127">如果系統提示您輸入密碼，輸入 hello 密碼 hello`root`帳戶。</span><span class="sxs-lookup"><span data-stu-id="42287-127">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="42287-128">如果您不記得您的根帳號密碼，請參閱[MySQL： 如何 tooReset hello 根密碼](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html)。</span><span class="sxs-lookup"><span data-stu-id="42287-128">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="42287-129">如果您的命令執行成功，表示您的 MySQL 伺服器正在執行。</span><span class="sxs-lookup"><span data-stu-id="42287-129">If your command runs successfully, then your MySQL server is running.</span></span> <span data-ttu-id="42287-130">如果沒有，請確定您的本機 MySQL 伺服器已啟動由下列 hello [MySQL 安裝後步驟](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html)。</span><span class="sxs-lookup"><span data-stu-id="42287-130">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database-locally"></a><span data-ttu-id="42287-131">在本機建立資料庫</span><span class="sxs-lookup"><span data-stu-id="42287-131">Create a database locally</span></span>

<span data-ttu-id="42287-132">在 hello`mysql`提示字元中，建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="42287-132">At hello `mysql` prompt, create a database.</span></span>

```sql 
CREATE DATABASE sampledb;
```

<span data-ttu-id="42287-133">輸入 `quit` 即可結束您的伺服器連線。</span><span class="sxs-lookup"><span data-stu-id="42287-133">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a><span data-ttu-id="42287-134">在本機建立 PHP 應用程式</span><span class="sxs-lookup"><span data-stu-id="42287-134">Create a PHP app locally</span></span>
<span data-ttu-id="42287-135">在此步驟中，您會取得 Laravel 範例應用程式、設定其資料庫連線，並在本機執行。</span><span class="sxs-lookup"><span data-stu-id="42287-135">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="42287-136">複製 hello 範例</span><span class="sxs-lookup"><span data-stu-id="42287-136">Clone hello sample</span></span>

<span data-ttu-id="42287-137">在 hello 終端機視窗， `cd` tooa 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="42287-137">In hello terminal window, `cd` tooa working directory.</span></span>

<span data-ttu-id="42287-138">執行下列命令 tooclone hello 範例儲存機制的 hello。</span><span class="sxs-lookup"><span data-stu-id="42287-138">Run hello following command tooclone hello sample repository.</span></span>

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

<span data-ttu-id="42287-139">`cd`tooyour 複製的目錄。</span><span class="sxs-lookup"><span data-stu-id="42287-139">`cd` tooyour cloned directory.</span></span>
<span data-ttu-id="42287-140">安裝所需的 hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="42287-140">Install hello required packages.</span></span>

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a><span data-ttu-id="42287-141">設定 MySQL 連線</span><span class="sxs-lookup"><span data-stu-id="42287-141">Configure MySQL connection</span></span>

<span data-ttu-id="42287-142">Hello 儲存機制在根目錄中，建立名為*.env*。</span><span class="sxs-lookup"><span data-stu-id="42287-142">In hello repository root, create a file named *.env*.</span></span> <span data-ttu-id="42287-143">下列變數到 hello 複製 hello *.env*檔案。</span><span class="sxs-lookup"><span data-stu-id="42287-143">Copy hello following variables into hello *.env* file.</span></span> <span data-ttu-id="42287-144">取代 hello  _&lt;root_password >_預留位置 hello MySQL root 使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="42287-144">Replace hello _&lt;root_password>_ placeholder with hello MySQL root user's password.</span></span>

```
APP_ENV=local
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=sampledb
DB_USERNAME=root
DB_PASSWORD=<root_password>
```

<span data-ttu-id="42287-145">如需有關如何 Laravel 使用 hello 詳細_.env_檔案，請參閱[Laravel 環境組態](https://laravel.com/docs/5.4/configuration#environment-configuration)。</span><span class="sxs-lookup"><span data-stu-id="42287-145">For information on how Laravel uses hello _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span></span>

### <a name="run-hello-sample-locally"></a><span data-ttu-id="42287-146">在本機執行 hello 範例</span><span class="sxs-lookup"><span data-stu-id="42287-146">Run hello sample locally</span></span>

<span data-ttu-id="42287-147">執行[Laravel 資料庫移轉](https://laravel.com/docs/5.4/migrations)toocreate hello 資料表 hello 應用程式的需求。</span><span class="sxs-lookup"><span data-stu-id="42287-147">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) toocreate hello tables hello application needs.</span></span> <span data-ttu-id="42287-148">哪些資料表在中建立 hello 移轉，查看 hello toosee_資料庫/移轉_hello Git 儲存機制的目錄。</span><span class="sxs-lookup"><span data-stu-id="42287-148">toosee which tables are created in hello migrations, look in hello _database/migrations_ directory in hello Git repository.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="42287-149">產生新的 Laravel 應用程式金鑰。</span><span class="sxs-lookup"><span data-stu-id="42287-149">Generate a new Laravel application key.</span></span>

```bash
php artisan key:generate
```

<span data-ttu-id="42287-150">執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="42287-150">Run hello application.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="42287-151">瀏覽過`http://localhost:8000`瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="42287-151">Navigate too`http://localhost:8000` in a browser.</span></span> <span data-ttu-id="42287-152">Hello 頁面中新增一些工作。</span><span class="sxs-lookup"><span data-stu-id="42287-152">Add a few tasks in hello page.</span></span>

![PHP 順利連線 tooMySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="42287-154">輸入 toostop PHP `Ctrl + C` hello 終端機中。</span><span class="sxs-lookup"><span data-stu-id="42287-154">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a><span data-ttu-id="42287-155">在 Azure 中建立 MySQL</span><span class="sxs-lookup"><span data-stu-id="42287-155">Create MySQL in Azure</span></span>

<span data-ttu-id="42287-156">在此步驟中，您會在[適用於 MySQL 的 Azure 資料庫 (預覽)](/azure/mysql) 中建立 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="42287-156">In this step, you create a MySQL database in [Azure Database for MySQL (Preview)](/azure/mysql).</span></span> <span data-ttu-id="42287-157">稍後，您可以設定 hello PHP 應用程式 tooconnect toothis 資料庫。</span><span class="sxs-lookup"><span data-stu-id="42287-157">Later, you configure hello PHP application tooconnect toothis database.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="42287-158">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="42287-158">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a><span data-ttu-id="42287-159">建立 MySQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="42287-159">Create a MySQL server</span></span>

<span data-ttu-id="42287-160">Azure 資料庫中建立伺服器的 MySQL （預覽） 以 hello [az mysql 伺服器建立](/cli/azure/mysql/server#create)命令。</span><span class="sxs-lookup"><span data-stu-id="42287-160">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>

<span data-ttu-id="42287-161">在 hello 下列命令，以取代 MySQL 伺服器名稱，您會看到 hello  _&lt;mysql_server_name >_預留位置 (有效的字元是`a-z`， `0-9`，和`-`)。</span><span class="sxs-lookup"><span data-stu-id="42287-161">In hello following command, substitute your MySQL server name where you see hello _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="42287-162">這個名稱是 hello MySQL 伺服器的主機名稱的一部分 (`<mysql_server_name>.database.windows.net`)，它需要 toobe 全域唯一。</span><span class="sxs-lookup"><span data-stu-id="42287-162">This name is part of hello MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs toobe globally unique.</span></span>

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

<span data-ttu-id="42287-163">建立 hello MySQL 伺服器時，hello Azure CLI 顯示資訊的類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="42287-163">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "administratorLogin": "adminuser",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<mysql_server_name>.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>",
  "location": "northeurope",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  ...
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="42287-164">設定伺服器防火牆</span><span class="sxs-lookup"><span data-stu-id="42287-164">Configure server firewall</span></span>

<span data-ttu-id="42287-165">建立防火牆規則的 MySQL 伺服器 tooallow 用戶端連接使用 hello [az mysql 伺服器防火牆規則建立](/cli/azure/mysql/server/firewall-rule#create)命令。</span><span class="sxs-lookup"><span data-stu-id="42287-165">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span>

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="42287-166">Azure 資料庫的 MySQL （預覽） 目前並不會限制連線只 tooAzure 服務。</span><span class="sxs-lookup"><span data-stu-id="42287-166">Azure Database for MySQL (Preview) doesn't currently limit connections only tooAzure services.</span></span> <span data-ttu-id="42287-167">在 Azure 中的 IP 位址動態指派，它是較佳的 tooenable 所有 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="42287-167">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses.</span></span> <span data-ttu-id="42287-168">hello 服務處於預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="42287-168">hello service is in preview.</span></span> <span data-ttu-id="42287-169">我們正在規劃更好的方法來保護您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="42287-169">Better methods for securing your database are planned.</span></span>
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a><span data-ttu-id="42287-170">Tooproduction MySQL 伺服器本機連接</span><span class="sxs-lookup"><span data-stu-id="42287-170">Connect tooproduction MySQL server locally</span></span>

<span data-ttu-id="42287-171">在 hello 終端機視窗中，連接在 Azure 中的 toohello MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="42287-171">In hello terminal window, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="42287-172">使用您先前指定的 hello 值 _&lt;mysql_server_name >_。</span><span class="sxs-lookup"><span data-stu-id="42287-172">Use hello value you specified previously for _&lt;mysql_server_name>_.</span></span>

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

<span data-ttu-id="42287-173">當提示您輸入密碼，請使用_$tr0ngPa$ w0rd ！_，這是您指定當您建立 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="42287-173">When prompted for a password, use _$tr0ngPa$w0rd!_, which you specified when you created hello database.</span></span>

### <a name="create-a-production-database"></a><span data-ttu-id="42287-174">建立生產環境資料庫</span><span class="sxs-lookup"><span data-stu-id="42287-174">Create a production database</span></span>

<span data-ttu-id="42287-175">在 hello`mysql`提示字元中，建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="42287-175">At hello `mysql` prompt, create a database.</span></span>

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="42287-176">建立具有權限的使用者</span><span class="sxs-lookup"><span data-stu-id="42287-176">Create a user with permissions</span></span>

<span data-ttu-id="42287-177">建立資料庫使用者，稱為_phpappuser_並給予其所有特殊權限在 hello`sampledb`資料庫。</span><span class="sxs-lookup"><span data-stu-id="42287-177">Create a database user called _phpappuser_ and give it all privileges in hello `sampledb` database.</span></span>

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

<span data-ttu-id="42287-178">結束輸入 hello 伺服器連接`quit`。</span><span class="sxs-lookup"><span data-stu-id="42287-178">Exit hello server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a><span data-ttu-id="42287-179">連接應用程式 tooAzure MySQL</span><span class="sxs-lookup"><span data-stu-id="42287-179">Connect app tooAzure MySQL</span></span>

<span data-ttu-id="42287-180">在此步驟中，您可以連接 hello PHP 應用程式 toohello MySQL 資料庫您 Azure 資料庫中建立的 MySQL （預覽）。</span><span class="sxs-lookup"><span data-stu-id="42287-180">In this step, you connect hello PHP application toohello MySQL database you created in Azure Database for MySQL (Preview).</span></span>

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="42287-181">設定 hello 資料庫連接</span><span class="sxs-lookup"><span data-stu-id="42287-181">Configure hello database connection</span></span>

<span data-ttu-id="42287-182">在 hello 儲存機制根目錄中，建立_。 env.production_下列變數到其中的檔案，並複製 hello。</span><span class="sxs-lookup"><span data-stu-id="42287-182">In hello repository root, create an _.env.production_ file and copy hello following variables into it.</span></span> <span data-ttu-id="42287-183">取代 hello 預留位置 _&lt;mysql_server_name >_。</span><span class="sxs-lookup"><span data-stu-id="42287-183">Replace hello placeholder _&lt;mysql_server_name>_.</span></span>

```
APP_ENV=production
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=<mysql_server_name>.database.windows.net
DB_DATABASE=sampledb
DB_USERNAME=phpappuser@<mysql_server_name>
DB_PASSWORD=MySQLAzure2017
MYSQL_SSL=true
```

<span data-ttu-id="42287-184">儲存 hello 的變更。</span><span class="sxs-lookup"><span data-stu-id="42287-184">Save hello changes.</span></span>

> [!TIP]
> <span data-ttu-id="42287-185">您的 MySQL 連接資訊，此檔案已經排除 hello Git 儲存機制的 toosecure (請參閱_.gitignore_ hello 儲存機制的根目錄中)。</span><span class="sxs-lookup"><span data-stu-id="42287-185">toosecure your MySQL connection information, this file is already excluded from hello Git repository (See _.gitignore_ in hello repository root).</span></span> <span data-ttu-id="42287-186">更新版本中，您會學習如何在應用程式服務 tooconnect tooyour tooconfigure 環境變數資料庫 Azure Database 中的 MySQL （預覽）。</span><span class="sxs-lookup"><span data-stu-id="42287-186">Later, you learn how tooconfigure environment variables in App Service tooconnect tooyour database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="42287-187">環境變數使用，您不需要 hello *.env* App Service 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="42287-187">With environment variables, you don't need hello *.env* file in App Service.</span></span>
>

### <a name="configure-ssl-certificate"></a><span data-ttu-id="42287-188">設定 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="42287-188">Configure SSL certificate</span></span>

<span data-ttu-id="42287-189">根據預設，用於 MySQL 的 Azure 資料庫會強制用戶端使用 SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="42287-189">By default, Azure Database for MySQL enforces SSL connections from clients.</span></span> <span data-ttu-id="42287-190">在 Azure 中的 tooconnect tooyour MySQL 資料庫，您必須使用_.pem_ SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="42287-190">tooconnect tooyour MySQL database in Azure, you must use a _.pem_ SSL certificate.</span></span>

<span data-ttu-id="42287-191">開啟_config/database.php_和新增 hello _sslmode_和_選項_參數太`connections.mysql`hello 下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="42287-191">Open _config/database.php_ and add hello _sslmode_ and _options_ parameters too`connections.mysql`, as shown in hello following code.</span></span>

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

<span data-ttu-id="42287-192">toolearn 如何 toogenerate 這_certificate.pem_，請參閱[設定 SSL 連接，您的應用程式 toosecurely 所連接的 MySQL tooAzure 資料庫](../mysql/howto-configure-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="42287-192">toolearn how toogenerate this _certificate.pem_, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](../mysql/howto-configure-ssl.md).</span></span>

> [!TIP]
> <span data-ttu-id="42287-193">hello 路徑_/ssl/certificate.pem_點 tooan 現有_certificate.pem_ hello Git 儲存機制中的檔案。</span><span class="sxs-lookup"><span data-stu-id="42287-193">hello path _/ssl/certificate.pem_ points tooan existing _certificate.pem_ file in hello Git repository.</span></span> <span data-ttu-id="42287-194">本教學課程為了方便起見提供這個檔案。</span><span class="sxs-lookup"><span data-stu-id="42287-194">This file is provided for convenience in this tutorial.</span></span> <span data-ttu-id="42287-195">實際的最佳做法是您不應該認可您的 _.pem_ 憑證進入原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="42287-195">For best practice, you should not commit your _.pem_ certificates into source control.</span></span> 
>

### <a name="test-hello-application-locally"></a><span data-ttu-id="42287-196">在本機測試 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="42287-196">Test hello application locally</span></span>

<span data-ttu-id="42287-197">執行 Laravel 資料庫移轉，而_。 env.production_為 hello MySQL （預覽） 環境內的檔案 toocreate hello 表格中 Azure 資料庫的 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="42287-197">Run Laravel database migrations with _.env.production_ as hello environment file toocreate hello tables in your MySQL database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="42287-198">請記住， _。 env.production_已在 Azure 中的 hello 連線資訊 tooyour MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="42287-198">Remember that _.env.production_ has hello connection information tooyour MySQL database in Azure.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="42287-199">_.env.production_ 沒有有效的應用程式金鑰。</span><span class="sxs-lookup"><span data-stu-id="42287-199">_.env.production_ doesn't have a valid application key yet.</span></span> <span data-ttu-id="42287-200">產生一個新的 hello 終端機中。</span><span class="sxs-lookup"><span data-stu-id="42287-200">Generate a new one for it in hello terminal.</span></span>

```bash
php artisan key:generate --env=production --force
```

<span data-ttu-id="42287-201">執行與 hello 範例應用程式_。 env.production_為 hello 環境檔案。</span><span class="sxs-lookup"><span data-stu-id="42287-201">Run hello sample application with _.env.production_ as hello environment file.</span></span>

```bash
php artisan serve --env=production
```

<span data-ttu-id="42287-202">瀏覽過`http://localhost:8000`。</span><span class="sxs-lookup"><span data-stu-id="42287-202">Navigate too`http://localhost:8000`.</span></span> <span data-ttu-id="42287-203">如果 hello 頁面載入無錯誤，hello PHP 應用程式正在連接 Azure toohello MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="42287-203">If hello page loads without errors, hello PHP application is connecting toohello MySQL database in Azure.</span></span>

<span data-ttu-id="42287-204">Hello 頁面中新增一些工作。</span><span class="sxs-lookup"><span data-stu-id="42287-204">Add a few tasks in hello page.</span></span>

![PHP 連接成功 tooAzure 資料庫的 MySQL （預覽）](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="42287-206">輸入 toostop PHP `Ctrl + C` hello 終端機中。</span><span class="sxs-lookup"><span data-stu-id="42287-206">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="commit-your-changes"></a><span data-ttu-id="42287-207">認可變更</span><span class="sxs-lookup"><span data-stu-id="42287-207">Commit your changes</span></span>

<span data-ttu-id="42287-208">Git 命令 toocommit 執行 hello 下列變更：</span><span class="sxs-lookup"><span data-stu-id="42287-208">Run hello following Git commands toocommit your changes:</span></span>

```bash
git add .
git commit -m "database.php updates"
```

<span data-ttu-id="42287-209">您的應用程式是部署的準備 toobe。</span><span class="sxs-lookup"><span data-stu-id="42287-209">Your app is ready toobe deployed.</span></span>

## <a name="deploy-tooazure"></a><span data-ttu-id="42287-210">部署 tooAzure</span><span class="sxs-lookup"><span data-stu-id="42287-210">Deploy tooAzure</span></span>

<span data-ttu-id="42287-211">在此步驟中，您可以部署 hello MySQL 連接 PHP 應用程式 tooAzure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="42287-211">In this step, you deploy hello MySQL-connected PHP application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="42287-212">建立應用程式服務方案</span><span class="sxs-lookup"><span data-stu-id="42287-212">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="42287-213">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="42287-213">Create a web app</span></span>

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a><span data-ttu-id="42287-214">Set hello PHP 版本</span><span class="sxs-lookup"><span data-stu-id="42287-214">Set hello PHP version</span></span>

<span data-ttu-id="42287-215">Hello 應用程式的設定 hello PHP 版本需要使用 hello [az webapp 組態集](/cli/azure/webapp/config#set)命令。</span><span class="sxs-lookup"><span data-stu-id="42287-215">Set hello PHP version that hello application requires by using hello [az webapp config set](/cli/azure/webapp/config#set) command.</span></span>

<span data-ttu-id="42287-216">hello 下列命令設定 hello PHP 版本 too_7.0_。</span><span class="sxs-lookup"><span data-stu-id="42287-216">hello following command sets hello PHP version too_7.0_.</span></span>

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a><span data-ttu-id="42287-217">設定資料庫設定</span><span class="sxs-lookup"><span data-stu-id="42287-217">Configure database settings</span></span>

<span data-ttu-id="42287-218">如先前，您可以連接 tooyour Azure MySQL 資料庫應用程式服務中使用環境變數。</span><span class="sxs-lookup"><span data-stu-id="42287-218">As pointed out previously, you can connect tooyour Azure MySQL database using environment variables in App Service.</span></span>

<span data-ttu-id="42287-219">在應用程式服務中，您設定環境變數為_應用程式設定_使用 hello [az webapp config appsettings 組](/cli/azure/webapp/config/appsettings#set)命令。</span><span class="sxs-lookup"><span data-stu-id="42287-219">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span>

<span data-ttu-id="42287-220">hello 下列命令會設定 hello 應用程式設定`DB_HOST`， `DB_DATABASE`， `DB_USERNAME`，和`DB_PASSWORD`。</span><span class="sxs-lookup"><span data-stu-id="42287-220">hello following command configures hello app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span></span> <span data-ttu-id="42287-221">Hello 預留位置取代 _&lt;appname >_和 _&lt;mysql_server_name >_。</span><span class="sxs-lookup"><span data-stu-id="42287-221">Replace hello placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

<span data-ttu-id="42287-222">您可以使用 hello PHP [getenv](http://www.php.net/manual/function.getenv.php)方法 tooaccess hello 設定。</span><span class="sxs-lookup"><span data-stu-id="42287-222">You can use hello PHP [getenv](http://www.php.net/manual/function.getenv.php) method tooaccess hello settings.</span></span> <span data-ttu-id="42287-223">hello Laravel 程式碼會使用[env](https://laravel.com/docs/5.4/helpers#method-env)包裝函式透過 hello PHP `getenv`。</span><span class="sxs-lookup"><span data-stu-id="42287-223">hello Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over hello PHP `getenv`.</span></span> <span data-ttu-id="42287-224">例如，hello MySQL 組態中的_config/database.php_看起來像下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="42287-224">For example, hello MySQL configuration in _config/database.php_ looks like hello following code:</span></span>

```php
'mysql' => [
    'driver'    => 'mysql',
    'host'      => env('DB_HOST', 'localhost'),
    'database'  => env('DB_DATABASE', 'forge'),
    'username'  => env('DB_USERNAME', 'forge'),
    'password'  => env('DB_PASSWORD', ''),
    ...
],
```

### <a name="configure-laravel-environment-variables"></a><span data-ttu-id="42287-225">設定 Laravel 環境變數</span><span class="sxs-lookup"><span data-stu-id="42287-225">Configure Laravel environment variables</span></span>

<span data-ttu-id="42287-226">Laravel 在 App Service 中需要應用程式金鑰。</span><span class="sxs-lookup"><span data-stu-id="42287-226">Laravel needs an application key in App Service.</span></span> <span data-ttu-id="42287-227">您可以使用應用程式設定加以設定。</span><span class="sxs-lookup"><span data-stu-id="42287-227">You can configure it with app settings.</span></span>

<span data-ttu-id="42287-228">使用`php artisan`toogenerate 新的應用程式金鑰，而不儲存 too_.env_。</span><span class="sxs-lookup"><span data-stu-id="42287-228">Use `php artisan` toogenerate a new application key without saving it too_.env_.</span></span>

```bash
php artisan key:generate --show
```

<span data-ttu-id="42287-229">設定 hello 應用程式中索引鍵 hello App Service web 應用程式使用 hello [az webapp config appsettings 組](/cli/azure/webapp/config/appsettings#set)命令。</span><span class="sxs-lookup"><span data-stu-id="42287-229">Set hello application key in hello App Service web app by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span> <span data-ttu-id="42287-230">Hello 預留位置取代 _&lt;appname >_和 _&lt;outputofphpartisankey： 產生 >_。</span><span class="sxs-lookup"><span data-stu-id="42287-230">Replace hello placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

<span data-ttu-id="42287-231">`APP_DEBUG="true"`會告知 Laravel tooreturn 偵錯資訊 hello 部署 web 應用程式時遇到錯誤。</span><span class="sxs-lookup"><span data-stu-id="42287-231">`APP_DEBUG="true"` tells Laravel tooreturn debugging information when hello deployed web app encounters errors.</span></span> <span data-ttu-id="42287-232">當執行生產應用程式，將它設定太`false`，這是更安全。</span><span class="sxs-lookup"><span data-stu-id="42287-232">When running a production application, set it too`false`, which is more secure.</span></span>

### <a name="set-hello-virtual-application-path"></a><span data-ttu-id="42287-233">設定 hello 虛擬應用程式路徑</span><span class="sxs-lookup"><span data-stu-id="42287-233">Set hello virtual application path</span></span>

<span data-ttu-id="42287-234">設定 hello hello web 應用程式的虛擬應用程式路徑。</span><span class="sxs-lookup"><span data-stu-id="42287-234">Set hello virtual application path for hello web app.</span></span> <span data-ttu-id="42287-235">這個步驟是必要的因為 hello [Laravel 應用程式生命週期](https://laravel.com/docs/5.4/lifecycle)一開始會處於 hello_公用_目錄而不是 hello 應用程式的根目錄。</span><span class="sxs-lookup"><span data-stu-id="42287-235">This step is required because hello [Laravel application lifecycle](https://laravel.com/docs/5.4/lifecycle) begins in hello _public_ directory instead of hello application's root directory.</span></span> <span data-ttu-id="42287-236">在 hello 根目錄開始其生命週期其他 PHP 架構可以運作而不需要手動設定的 hello 虛擬應用程式路徑。</span><span class="sxs-lookup"><span data-stu-id="42287-236">Other PHP frameworks whose lifecycle start in hello root directory can work without manual configuration of hello virtual application path.</span></span>

<span data-ttu-id="42287-237">設定 hello 虛擬應用程式路徑使用 hello [az 資源更新](/cli/azure/resource#update)命令。</span><span class="sxs-lookup"><span data-stu-id="42287-237">Set hello virtual application path by using hello [az resource update](/cli/azure/resource#update) command.</span></span> <span data-ttu-id="42287-238">取代 hello  _&lt;appname >_預留位置。</span><span class="sxs-lookup"><span data-stu-id="42287-238">Replace hello _&lt;appname>_ placeholder.</span></span>

```azurecli-interactive
az resource update \
    --name web \
    --resource-group myResourceGroup \
    --namespace Microsoft.Web \
    --resource-type config \
    --parent sites/<app_name> \
    --set properties.virtualApplications[0].physicalPath="site\wwwroot\public" \
    --api-version 2015-06-01
```

<span data-ttu-id="42287-239">根據預設，Azure 應用程式服務點 hello 根虛擬應用程式路徑 (_/_) hello toohello 根目錄部署應用程式檔案 (_sites\wwwroot_)。</span><span class="sxs-lookup"><span data-stu-id="42287-239">By default, Azure App Service points hello root virtual application path (_/_) toohello root directory of hello deployed application files (_sites\wwwroot_).</span></span>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="42287-240">設定部署使用者</span><span class="sxs-lookup"><span data-stu-id="42287-240">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a><span data-ttu-id="42287-241">設定本機 Git 部署</span><span class="sxs-lookup"><span data-stu-id="42287-241">Configure local Git deployment</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a><span data-ttu-id="42287-242">從 Git 推送 tooAzure</span><span class="sxs-lookup"><span data-stu-id="42287-242">Push tooAzure from Git</span></span>

<span data-ttu-id="42287-243">新增 Azure 遠端 tooyour 本機 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="42287-243">Add an Azure remote tooyour local Git repository.</span></span>

```bash
git remote add azure <paste_copied_url_here>
```

<span data-ttu-id="42287-244">推送 toohello Azure 遠端 toodeploy hello PHP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="42287-244">Push toohello Azure remote toodeploy hello PHP application.</span></span> <span data-ttu-id="42287-245">系統會提示您稍早提供一部分 hello hello 部署使用者建立的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="42287-245">You are prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span>

```bash
git push azure master
```

<span data-ttu-id="42287-246">在部署期間，Azure App Service 會與 Git 溝通其進度。</span><span class="sxs-lookup"><span data-stu-id="42287-246">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 3, done.
Delta compression using up too8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 291 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'a5e076db9c'.
remote: Running custom deployment command...
remote: Running deployment command...
...
< Output has been truncated for readability >
```

> [!NOTE]
> <span data-ttu-id="42287-247">您可能會注意到 hello 部署程序會安裝[編輯器](https://getcomposer.org/)hello 結尾的封裝。</span><span class="sxs-lookup"><span data-stu-id="42287-247">You may notice that hello deployment process installs [Composer](https://getcomposer.org/) packages at hello end.</span></span> <span data-ttu-id="42287-248">應用程式服務不會執行這些自動化增加了在預設部署期間，因此這個範例儲存機制有三個額外的檔案其根目錄 tooenable 它：</span><span class="sxs-lookup"><span data-stu-id="42287-248">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory tooenable it:</span></span>
>
> - <span data-ttu-id="42287-249">`.deployment`-此檔案會告知應用程式服務 toorun `bash deploy.sh` hello 自訂部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="42287-249">`.deployment` - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
> - <span data-ttu-id="42287-250">`deploy.sh`-hello 自訂部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="42287-250">`deploy.sh` - hello custom deployment script.</span></span> <span data-ttu-id="42287-251">如果您檢閱 hello 檔案時，您會看到應用程式會執行`php composer.phar install`之後`npm install`。</span><span class="sxs-lookup"><span data-stu-id="42287-251">If you review hello file, you will see that it runs `php composer.phar install` after `npm install`.</span></span>
> - <span data-ttu-id="42287-252">`composer.phar`-hello 編輯器封裝管理員。</span><span class="sxs-lookup"><span data-stu-id="42287-252">`composer.phar` - hello Composer package manager.</span></span>
>
> <span data-ttu-id="42287-253">您可以使用此方法 tooadd 任何步驟 tooyour Git 架構部署 tooApp 服務。</span><span class="sxs-lookup"><span data-stu-id="42287-253">You can use this approach tooadd any step tooyour Git-based deployment tooApp Service.</span></span> <span data-ttu-id="42287-254">如需相關資訊，請參閱[自訂部署指令碼](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script)。</span><span class="sxs-lookup"><span data-stu-id="42287-254">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span></span>
>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="42287-255">瀏覽 toohello Azure web 應用程式</span><span class="sxs-lookup"><span data-stu-id="42287-255">Browse toohello Azure web app</span></span>

<span data-ttu-id="42287-256">瀏覽過`http://<app_name>.azurewebsites.net`並加入一些工作 toohello 清單。</span><span class="sxs-lookup"><span data-stu-id="42287-256">Browse too`http://<app_name>.azurewebsites.net` and add a few tasks toohello list.</span></span>

![在 Azure App Service 中執行的 PHP 應用程式](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

<span data-ttu-id="42287-258">恭喜，您正在 Azure App Service 中執行資料驅動的 PHP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="42287-258">Congratulations, you're running a data-driven PHP app in Azure App Service.</span></span>

## <a name="update-model-locally-and-redeploy"></a><span data-ttu-id="42287-259">在本機更新模型並重新部署</span><span class="sxs-lookup"><span data-stu-id="42287-259">Update model locally and redeploy</span></span>

<span data-ttu-id="42287-260">在此步驟中，您可以進行簡單的變更 toohello`task`資料模型和 hello webapp，，然後將發行 hello 更新 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="42287-260">In this step, you make a simple change toohello `task` data model and hello webapp, and then publish hello update tooAzure.</span></span>

<span data-ttu-id="42287-261">Hello 工作案例中，您會修改 hello 應用程式，使您可以將工作標示為完成。</span><span class="sxs-lookup"><span data-stu-id="42287-261">For hello tasks scenario, you modify hello application so that you can mark a task as complete.</span></span>

### <a name="add-a-column"></a><span data-ttu-id="42287-262">新增資料行</span><span class="sxs-lookup"><span data-stu-id="42287-262">Add a column</span></span>

<span data-ttu-id="42287-263">在終端機 hello，瀏覽 toohello hello Git 儲存機制的根目錄。</span><span class="sxs-lookup"><span data-stu-id="42287-263">In hello terminal, navigate toohello root of hello Git repository.</span></span>

<span data-ttu-id="42287-264">產生新的資料庫移轉 hello`tasks`資料表：</span><span class="sxs-lookup"><span data-stu-id="42287-264">Generate a new database migration for hello `tasks` table:</span></span>

```bash
php artisan make:migration add_complete_column --table=tasks
```

<span data-ttu-id="42287-265">此命令會顯示 hello 所產生的 hello 移轉檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="42287-265">This command shows you hello name of hello migration file that's generated.</span></span> <span data-ttu-id="42287-266">在 _database/migrations_ 中找到這個檔案並開啟它。</span><span class="sxs-lookup"><span data-stu-id="42287-266">Find this file in _database/migrations_ and open it.</span></span>

<span data-ttu-id="42287-267">取代 hello`up`方法，以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="42287-267">Replace hello `up` method with hello following code:</span></span>

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

<span data-ttu-id="42287-268">hello 上述程式碼的布林資料行會在新增 hello`tasks`資料表稱為`complete`。</span><span class="sxs-lookup"><span data-stu-id="42287-268">hello preceding code adds a boolean column in hello `tasks` table called `complete`.</span></span>

<span data-ttu-id="42287-269">取代 hello`down`方法，以下列程式碼執行 hello 復原動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="42287-269">Replace hello `down` method with hello following code for hello rollback action:</span></span>

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

<span data-ttu-id="42287-270">在終端機 hello 執行 Laravel 資料庫移轉 toomake hello 變更 hello 本機資料庫中。</span><span class="sxs-lookup"><span data-stu-id="42287-270">In hello terminal, run Laravel database migrations toomake hello change in hello local database.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="42287-271">根據 hello [Laravel 命名慣例](https://laravel.com/docs/5.4/eloquent#defining-models)，hello 模型`Task`(請參閱_app/Task.php_) 對應 toohello`tasks`預設資料表。</span><span class="sxs-lookup"><span data-stu-id="42287-271">Based on hello [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), hello model `Task` (see _app/Task.php_) maps toohello `tasks` table by default.</span></span>

### <a name="update-application-logic"></a><span data-ttu-id="42287-272">更新應用程式邏輯</span><span class="sxs-lookup"><span data-stu-id="42287-272">Update application logic</span></span>

<span data-ttu-id="42287-273">開啟 hello *routes/web.php*檔案。</span><span class="sxs-lookup"><span data-stu-id="42287-273">Open hello *routes/web.php* file.</span></span> <span data-ttu-id="42287-274">hello 應用程式定義的路由和商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="42287-274">hello application defines its routes and business logic here.</span></span>

<span data-ttu-id="42287-275">在 hello hello 檔案結尾，加入路由以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="42287-275">At hello end of hello file, add a route with hello following code:</span></span>

```php
/**
 * Toggle Task completeness
 */
Route::post('/task/{id}', function ($id) {
    error_log('INFO: post /task/'.$id);
    $task = Task::findOrFail($id);

    $task->complete = !$task->complete;
    $task->save();

    return redirect('/');
});
```

<span data-ttu-id="42287-276">hello 上述程式碼就可以簡單更新 toohello 資料模型切換 hello 值`complete`。</span><span class="sxs-lookup"><span data-stu-id="42287-276">hello preceding code makes a simple update toohello data model by toggling hello value of `complete`.</span></span>

### <a name="update-hello-view"></a><span data-ttu-id="42287-277">更新 hello 檢視</span><span class="sxs-lookup"><span data-stu-id="42287-277">Update hello view</span></span>

<span data-ttu-id="42287-278">開啟 hello *resources/views/tasks.blade.php*檔案。</span><span class="sxs-lookup"><span data-stu-id="42287-278">Open hello *resources/views/tasks.blade.php* file.</span></span> <span data-ttu-id="42287-279">尋找 hello`<tr>`開頭標記，並將它取代為：</span><span class="sxs-lookup"><span data-stu-id="42287-279">Find hello `<tr>` opening tag and replace it with:</span></span>

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

<span data-ttu-id="42287-280">上述程式碼變更 hello 根據 hello 工作是否已完成的資料列色彩 hello。</span><span class="sxs-lookup"><span data-stu-id="42287-280">hello preceding code changes hello row color depending on whether hello task is complete.</span></span>

<span data-ttu-id="42287-281">在 hello 下一行中，您會有下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="42287-281">In hello next line, you have hello following code:</span></span>

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

<span data-ttu-id="42287-282">Hello 整行取代成下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="42287-282">Replace hello entire line with hello following code:</span></span>

```html
<td>
    <form action="{{ url('task/'.$task->id) }}" method="POST">
        {{ csrf_field() }}

        <button type="submit" class="btn btn-xs">
            <i class="fa {{$task->complete ? 'fa-check-square-o' : 'fa-square-o'}}"></i>
        </button>
        {{ $task->name }}
    </form>
</td>
```

<span data-ttu-id="42287-283">hello 上述程式碼中加入參考先前定義的 hello 路由的 hello 送出按鈕。</span><span class="sxs-lookup"><span data-stu-id="42287-283">hello preceding code adds hello submit button that references hello route that you defined earlier.</span></span>

### <a name="test-hello-changes-locally"></a><span data-ttu-id="42287-284">在本機測試 hello 變更</span><span class="sxs-lookup"><span data-stu-id="42287-284">Test hello changes locally</span></span>

<span data-ttu-id="42287-285">Hello 根目錄中的 hello Git 儲存機制，從執行 hello 程式開發伺服器。</span><span class="sxs-lookup"><span data-stu-id="42287-285">From hello root directory of hello Git repository, run hello development server.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="42287-286">toosee hello 工作狀態變更，瀏覽過`http://localhost:8000`和選取 hello 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="42287-286">toosee hello task status change, navigate too`http://localhost:8000` and select hello checkbox.</span></span>

![加入核取方塊 tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

<span data-ttu-id="42287-288">輸入 toostop PHP `Ctrl + C` hello 終端機中。</span><span class="sxs-lookup"><span data-stu-id="42287-288">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="publish-changes-tooazure"></a><span data-ttu-id="42287-289">發行變更 tooAzure</span><span class="sxs-lookup"><span data-stu-id="42287-289">Publish changes tooAzure</span></span>

<span data-ttu-id="42287-290">在終端機 hello 執行 Laravel 資料庫移轉與 hello 生產連接字串 toomake hello 變更 hello Azure 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="42287-290">In hello terminal, run Laravel database migrations with hello production connection string toomake hello change in hello Azure database.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="42287-291">認可 Git 中的所有 hello 變更，並接著推送 hello 程式碼變更 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="42287-291">Commit all hello changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

<span data-ttu-id="42287-292">一次 hello`git push`已完成，請瀏覽 toohello Azure web 應用程式和測試 hello 新功能。</span><span class="sxs-lookup"><span data-stu-id="42287-292">Once hello `git push` is complete, navigate toohello Azure web app and test hello new functionality.</span></span>

![發行 tooAzure 模型與資料庫的變更。](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="42287-294">如果您加入的任何工作時，它們會保留在 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="42287-294">If you added any tasks, they are retained in hello database.</span></span> <span data-ttu-id="42287-295">更新 toohello 資料結構描述可讓現有的資料保持不變。</span><span class="sxs-lookup"><span data-stu-id="42287-295">Updates toohello data schema leave existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="42287-296">資料流診斷記錄</span><span class="sxs-lookup"><span data-stu-id="42287-296">Stream diagnostic logs</span></span>

<span data-ttu-id="42287-297">Hello PHP 應用程式執行時 Azure App Service 中，您可以取得 hello 主控台記錄檔傳送的 tooyour 終端機。</span><span class="sxs-lookup"><span data-stu-id="42287-297">While hello PHP application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="42287-298">這樣一來，您可以取得 hello 相同的診斷訊息 toohelp 您偵錯應用程式錯誤。</span><span class="sxs-lookup"><span data-stu-id="42287-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="42287-299">資料流中，使用 hello toostart 記錄[az webapp 記錄結尾](/cli/azure/webapp/log#tail)命令。</span><span class="sxs-lookup"><span data-stu-id="42287-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

<span data-ttu-id="42287-300">記錄檔資料流啟動之後，重新整理 hello Azure web 應用程式在 hello 瀏覽器 tooget 某些網路流量。</span><span class="sxs-lookup"><span data-stu-id="42287-300">Once log streaming has started, refresh hello Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="42287-301">您現在可以看到主控台記錄檔傳送的 toohello 終端機。</span><span class="sxs-lookup"><span data-stu-id="42287-301">You can now see console logs piped toohello terminal.</span></span> <span data-ttu-id="42287-302">如果您沒有立即看到主控台記錄，請在 30 秒後再查看。</span><span class="sxs-lookup"><span data-stu-id="42287-302">If you don't see console logs immediately, check again in 30 seconds.</span></span>

<span data-ttu-id="42287-303">在任何時候、 資料流 toostop 記錄類型`Ctrl` + `C`。</span><span class="sxs-lookup"><span data-stu-id="42287-303">toostop log streaming at anytime, type `Ctrl`+`C`.</span></span>

> [!TIP]
> <span data-ttu-id="42287-304">PHP 應用程式可以使用 hello 標準[error_log()](http://php.net/manual/function.error-log.php) toooutput toohello 主控台。</span><span class="sxs-lookup"><span data-stu-id="42287-304">A PHP application can use hello standard [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello console.</span></span> <span data-ttu-id="42287-305">hello 範例應用程式使用這個方法在_app/Http/routes.php_。</span><span class="sxs-lookup"><span data-stu-id="42287-305">hello sample application uses this approach in _app/Http/routes.php_.</span></span>
>
> <span data-ttu-id="42287-306">一種 web 架構，為[Laravel 使用 Monolog](https://laravel.com/docs/5.4/errors)為 hello 記錄提供者。</span><span class="sxs-lookup"><span data-stu-id="42287-306">As a web framework, [Laravel uses Monolog](https://laravel.com/docs/5.4/errors) as hello logging provider.</span></span> <span data-ttu-id="42287-307">toosee 如何 tooget Monolog toooutput 訊息 toohello 主控台中，請參閱[PHP： 如何 toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out)。</span><span class="sxs-lookup"><span data-stu-id="42287-307">toosee how tooget Monolog toooutput messages toohello console, see [PHP: How toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span></span>
>
>

## <a name="manage-hello-azure-web-app"></a><span data-ttu-id="42287-308">管理 hello Azure web 應用程式</span><span class="sxs-lookup"><span data-stu-id="42287-308">Manage hello Azure web app</span></span>

<span data-ttu-id="42287-309">移 toohello [Azure 入口網站](https://portal.azure.com)toomanage hello web 應用程式所建立。</span><span class="sxs-lookup"><span data-stu-id="42287-309">Go toohello [Azure portal](https://portal.azure.com) toomanage hello web app you created.</span></span>

<span data-ttu-id="42287-310">從 hello 左窗格中，按一下 **應用程式服務**，然後按一下hello Azure web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="42287-310">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![入口網站瀏覽 tooAzure web 應用程式](./media/app-service-web-tutorial-php-mysql/access-portal.png)

<span data-ttu-id="42287-312">您會看到 Web 應用程式的 [概觀] 頁面。</span><span class="sxs-lookup"><span data-stu-id="42287-312">You see your web app's Overview page.</span></span> <span data-ttu-id="42287-313">您可以在這裡執行基本管理工作，像是停止、啟動、重新啟動、瀏覽、刪除。</span><span class="sxs-lookup"><span data-stu-id="42287-313">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span></span>

<span data-ttu-id="42287-314">hello 左側的功能表會提供如何設定您的應用程式頁面。</span><span class="sxs-lookup"><span data-stu-id="42287-314">hello left menu provides pages for configuring your app.</span></span>

![Azure 入口網站中的 App Service 頁面](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="42287-316">後續步驟</span><span class="sxs-lookup"><span data-stu-id="42287-316">Next steps</span></span>

<span data-ttu-id="42287-317">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="42287-317">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="42287-318">在 Azure 中建立 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="42287-318">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="42287-319">連接 PHP 應用程式 tooMySQL</span><span class="sxs-lookup"><span data-stu-id="42287-319">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="42287-320">部署 hello 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="42287-320">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="42287-321">更新 hello 資料模型，部署 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="42287-321">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="42287-322">來自 Azure 的串流診斷記錄</span><span class="sxs-lookup"><span data-stu-id="42287-322">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="42287-323">管理 hello hello Azure 入口網站中的應用程式</span><span class="sxs-lookup"><span data-stu-id="42287-323">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="42287-324">前進 toohello 下一個教學課程 toolearn toomap 自訂的 DNS 名稱 tooa web 應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="42287-324">Advance toohello next tutorial toolearn how toomap a custom DNS name tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="42287-325">將現有自訂 DNS 名稱 tooAzure Web 應用程式的對應</span><span class="sxs-lookup"><span data-stu-id="42287-325">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)

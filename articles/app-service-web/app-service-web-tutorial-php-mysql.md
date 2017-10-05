---
title: "在 Azure 中建置 PHP 和 MySQL Web 應用程式 | Microsoft Docs"
description: "了解如何取得在 Azure 中運作的 PHP 應用程式，並連線至 Azure 中的 MySQL 資料庫。"
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
ms.openlocfilehash: 6e8d8962180f7534b0b9074f03ecc8ea431ae1a4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a><span data-ttu-id="297a7-103">在 Azure 中建置 PHP 和 MySQL Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="297a7-103">Build a PHP and MySQL web app in Azure</span></span>

<span data-ttu-id="297a7-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="297a7-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="297a7-105">本教學課程示範如何在 Azure 中建立 PHP Web 應用程式，並將它連線到 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="297a7-105">This tutorial shows how to create a PHP web app in Azure and connect it to a MySQL database.</span></span> <span data-ttu-id="297a7-106">完成後，您將有一個在 Azure App Service Web Apps 上執行的 [Laravel](https://laravel.com/) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="297a7-106">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on Azure App Service Web Apps.</span></span>

![在 Azure App Service 中執行的 PHP 應用程式](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="297a7-108">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="297a7-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="297a7-109">在 Azure 中建立 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="297a7-109">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="297a7-110">將 PHP 應用程式連線至 MySQL</span><span class="sxs-lookup"><span data-stu-id="297a7-110">Connect a PHP app to MySQL</span></span>
> * <span data-ttu-id="297a7-111">將應用程式部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="297a7-111">Deploy the app to Azure</span></span>
> * <span data-ttu-id="297a7-112">將資料模型更新並將應用程式重新部署</span><span class="sxs-lookup"><span data-stu-id="297a7-112">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="297a7-113">來自 Azure 的串流診斷記錄</span><span class="sxs-lookup"><span data-stu-id="297a7-113">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="297a7-114">在 Azure 入口網站中管理應用程式</span><span class="sxs-lookup"><span data-stu-id="297a7-114">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="297a7-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="297a7-115">Prerequisites</span></span>

<span data-ttu-id="297a7-116">若要完成本教學課程：</span><span class="sxs-lookup"><span data-stu-id="297a7-116">To complete this tutorial:</span></span>

* [<span data-ttu-id="297a7-117">安裝 Git</span><span class="sxs-lookup"><span data-stu-id="297a7-117">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="297a7-118">安裝 PHP 5.6.4 或更新版本</span><span class="sxs-lookup"><span data-stu-id="297a7-118">Install PHP 5.6.4 or above</span></span>](http://php.net/downloads.php)
* [<span data-ttu-id="297a7-119">安裝編輯器</span><span class="sxs-lookup"><span data-stu-id="297a7-119">Install Composer</span></span>](https://getcomposer.org/doc/00-intro.md)
* <span data-ttu-id="297a7-120">啟用下列 PHP 擴充功能 Laravel 需求︰OpenSSL、PDO-MySQL、Mbstring、Tokenizer、XML</span><span class="sxs-lookup"><span data-stu-id="297a7-120">Enable the following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span></span>
* [<span data-ttu-id="297a7-121">下載並啟動 MySQL</span><span class="sxs-lookup"><span data-stu-id="297a7-121">Install and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a><span data-ttu-id="297a7-122">準備本機 MySQL</span><span class="sxs-lookup"><span data-stu-id="297a7-122">Prepare local MySQL</span></span>

<span data-ttu-id="297a7-123">在此步驟中，您可以在本機 MySQL 伺服器中建立資料庫，供您在本教學課程中使用。</span><span class="sxs-lookup"><span data-stu-id="297a7-123">In this step, you create a database in your local MySQL server for your use in this tutorial.</span></span>

### <a name="connect-to-local-mysql-server"></a><span data-ttu-id="297a7-124">連線至本機 MySQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="297a7-124">Connect to local MySQL server</span></span>

<span data-ttu-id="297a7-125">在終端機視窗中，連線到您的本機 MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="297a7-125">In a terminal window, connect to your local MySQL server.</span></span> <span data-ttu-id="297a7-126">您可使用這個終端機視窗來執行本教學課程中的所有命令。</span><span class="sxs-lookup"><span data-stu-id="297a7-126">You can use this terminal window to run all the commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="297a7-127">如果系統提示您輸入密碼，請輸入 `root` 帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="297a7-127">If you're prompted for a password, enter the password for the `root` account.</span></span> <span data-ttu-id="297a7-128">如果您不記得根帳戶密碼，請參閱 [MySQL︰如何重設根密碼](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html)。</span><span class="sxs-lookup"><span data-stu-id="297a7-128">If you don't remember your root account password, see [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="297a7-129">如果您的命令執行成功，表示您的 MySQL 伺服器正在執行。</span><span class="sxs-lookup"><span data-stu-id="297a7-129">If your command runs successfully, then your MySQL server is running.</span></span> <span data-ttu-id="297a7-130">如果沒有，請遵循 [MySQL 後續安裝步驟](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html)，確定您已啟動本機 MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="297a7-130">If not, make sure that your local MySQL server is started by following the [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database-locally"></a><span data-ttu-id="297a7-131">在本機建立資料庫</span><span class="sxs-lookup"><span data-stu-id="297a7-131">Create a database locally</span></span>

<span data-ttu-id="297a7-132">在 `mysql` 提示中，建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="297a7-132">At the `mysql` prompt, create a database.</span></span>

```sql 
CREATE DATABASE sampledb;
```

<span data-ttu-id="297a7-133">輸入 `quit` 即可結束您的伺服器連線。</span><span class="sxs-lookup"><span data-stu-id="297a7-133">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a><span data-ttu-id="297a7-134">在本機建立 PHP 應用程式</span><span class="sxs-lookup"><span data-stu-id="297a7-134">Create a PHP app locally</span></span>
<span data-ttu-id="297a7-135">在此步驟中，您會取得 Laravel 範例應用程式、設定其資料庫連線，並在本機執行。</span><span class="sxs-lookup"><span data-stu-id="297a7-135">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span></span> 

### <a name="clone-the-sample"></a><span data-ttu-id="297a7-136">複製範例</span><span class="sxs-lookup"><span data-stu-id="297a7-136">Clone the sample</span></span>

<span data-ttu-id="297a7-137">在終端機視窗中，使用 `cd` 移至工作目錄。</span><span class="sxs-lookup"><span data-stu-id="297a7-137">In the terminal window, `cd` to a working directory.</span></span>

<span data-ttu-id="297a7-138">執行下列命令來複製範例存放庫。</span><span class="sxs-lookup"><span data-stu-id="297a7-138">Run the following command to clone the sample repository.</span></span>

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

<span data-ttu-id="297a7-139">使用 `cd` 移至您複製的目錄。</span><span class="sxs-lookup"><span data-stu-id="297a7-139">`cd` to your cloned directory.</span></span>
<span data-ttu-id="297a7-140">安裝必要的套件。</span><span class="sxs-lookup"><span data-stu-id="297a7-140">Install the required packages.</span></span>

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a><span data-ttu-id="297a7-141">設定 MySQL 連線</span><span class="sxs-lookup"><span data-stu-id="297a7-141">Configure MySQL connection</span></span>

<span data-ttu-id="297a7-142">在存放庫的根目錄中，建立名為 *.env* 的檔案。</span><span class="sxs-lookup"><span data-stu-id="297a7-142">In the repository root, create a file named *.env*.</span></span> <span data-ttu-id="297a7-143">將下列變數複製到 *.env* 檔案。</span><span class="sxs-lookup"><span data-stu-id="297a7-143">Copy the following variables into the *.env* file.</span></span> <span data-ttu-id="297a7-144">將 _&lt;root_password>_ 預留位置取代為 MySQL 根使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="297a7-144">Replace the _&lt;root_password>_ placeholder with the MySQL root user's password.</span></span>

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

<span data-ttu-id="297a7-145">如需有關 Laravel 如何使用 _.env_ 檔案的資訊，請參閱 [Laravel 環境設定](https://laravel.com/docs/5.4/configuration#environment-configuration)。</span><span class="sxs-lookup"><span data-stu-id="297a7-145">For information on how Laravel uses the _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span></span>

### <a name="run-the-sample-locally"></a><span data-ttu-id="297a7-146">在本機執行範例</span><span class="sxs-lookup"><span data-stu-id="297a7-146">Run the sample locally</span></span>

<span data-ttu-id="297a7-147">執行 [Laravel 資料庫移轉](https://laravel.com/docs/5.4/migrations)來建立應用程式所需的資料表。</span><span class="sxs-lookup"><span data-stu-id="297a7-147">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) to create the tables the application needs.</span></span> <span data-ttu-id="297a7-148">若要查看移轉中會建立哪些資料表，請參閱 Git 存放庫中的 _database/migrations_ 目錄。</span><span class="sxs-lookup"><span data-stu-id="297a7-148">To see which tables are created in the migrations, look in the _database/migrations_ directory in the Git repository.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="297a7-149">產生新的 Laravel 應用程式金鑰。</span><span class="sxs-lookup"><span data-stu-id="297a7-149">Generate a new Laravel application key.</span></span>

```bash
php artisan key:generate
```

<span data-ttu-id="297a7-150">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="297a7-150">Run the application.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="297a7-151">在瀏覽器中，瀏覽至 `http://localhost:8000`。</span><span class="sxs-lookup"><span data-stu-id="297a7-151">Navigate to `http://localhost:8000` in a browser.</span></span> <span data-ttu-id="297a7-152">在頁面中新增幾項工作。</span><span class="sxs-lookup"><span data-stu-id="297a7-152">Add a few tasks in the page.</span></span>

![PHP 成功連線至 MySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="297a7-154">若要停止 PHP，請在終端機中輸入 `Ctrl + C`。</span><span class="sxs-lookup"><span data-stu-id="297a7-154">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a><span data-ttu-id="297a7-155">在 Azure 中建立 MySQL</span><span class="sxs-lookup"><span data-stu-id="297a7-155">Create MySQL in Azure</span></span>

<span data-ttu-id="297a7-156">在此步驟中，您會在[適用於 MySQL 的 Azure 資料庫 (預覽)](/azure/mysql) 中建立 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="297a7-156">In this step, you create a MySQL database in [Azure Database for MySQL (Preview)](/azure/mysql).</span></span> <span data-ttu-id="297a7-157">稍後，您要將 PHP 應用程式設定為連線至此資料庫。</span><span class="sxs-lookup"><span data-stu-id="297a7-157">Later, you configure the PHP application to connect to this database.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="297a7-158">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="297a7-158">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a><span data-ttu-id="297a7-159">建立 MySQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="297a7-159">Create a MySQL server</span></span>

<span data-ttu-id="297a7-160">使用 [az mysql server create](/cli/azure/mysql/server#create) 命令，在適用於 MySQL 的 Azure 資料庫 (預覽) 中建立伺服器。</span><span class="sxs-lookup"><span data-stu-id="297a7-160">Create a server in Azure Database for MySQL (Preview) with the [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>

<span data-ttu-id="297a7-161">在下列命令中，在您看見 _&lt;mysql_server_name>_ 預留位置的地方，取代成您自己的 MySQL 伺服器名稱 (有效字元有 `a-z`、`0-9`、`-`)。</span><span class="sxs-lookup"><span data-stu-id="297a7-161">In the following command, substitute your MySQL server name where you see the _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="297a7-162">這個名稱是 MySQL 伺服器主機名稱 (`<mysql_server_name>.database.windows.net`) 的一部分，必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="297a7-162">This name is part of the MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs to be globally unique.</span></span>

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

<span data-ttu-id="297a7-163">建立 MySQL 伺服器後，Azure CLI 會顯示類似下列範例的資訊：</span><span class="sxs-lookup"><span data-stu-id="297a7-163">When the MySQL server is created, the Azure CLI shows information similar to the following example:</span></span>

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

### <a name="configure-server-firewall"></a><span data-ttu-id="297a7-164">設定伺服器防火牆</span><span class="sxs-lookup"><span data-stu-id="297a7-164">Configure server firewall</span></span>

<span data-ttu-id="297a7-165">使用 [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) 命令，建立 MySQL 伺服器的防火牆規則來允許用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="297a7-165">Create a firewall rule for your MySQL server to allow client connections by using the [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span>

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="297a7-166">適用於 MySQL 的 Azure 資料庫 (預覽) 目前沒有限制只能連線至 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="297a7-166">Azure Database for MySQL (Preview) doesn't currently limit connections only to Azure services.</span></span> <span data-ttu-id="297a7-167">由於 Azure 中的 IP 位址為動態指派，最好是啟用所有的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="297a7-167">As IP addresses in Azure are dynamically assigned, it is better to enable all IP addresses.</span></span> <span data-ttu-id="297a7-168">此服務為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="297a7-168">The service is in preview.</span></span> <span data-ttu-id="297a7-169">我們正在規劃更好的方法來保護您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="297a7-169">Better methods for securing your database are planned.</span></span>
>
>

### <a name="connect-to-production-mysql-server-locally"></a><span data-ttu-id="297a7-170">在本機連線到生產環境 MySQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="297a7-170">Connect to production MySQL server locally</span></span>

<span data-ttu-id="297a7-171">在終端機視窗中，連線至 Azure 中的 MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="297a7-171">In the terminal window, connect to the MySQL server in Azure.</span></span> <span data-ttu-id="297a7-172">使用您先前為 _&lt;mysql_server_name>_ 指定的值。</span><span class="sxs-lookup"><span data-stu-id="297a7-172">Use the value you specified previously for _&lt;mysql_server_name>_.</span></span>

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

<span data-ttu-id="297a7-173">當系統提示您輸入密碼，使用您建立資料庫時指定的 _$tr0ngPa$w0rd!_。</span><span class="sxs-lookup"><span data-stu-id="297a7-173">When prompted for a password, use _$tr0ngPa$w0rd!_, which you specified when you created the database.</span></span>

### <a name="create-a-production-database"></a><span data-ttu-id="297a7-174">建立生產環境資料庫</span><span class="sxs-lookup"><span data-stu-id="297a7-174">Create a production database</span></span>

<span data-ttu-id="297a7-175">在 `mysql` 提示中，建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="297a7-175">At the `mysql` prompt, create a database.</span></span>

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="297a7-176">建立具有權限的使用者</span><span class="sxs-lookup"><span data-stu-id="297a7-176">Create a user with permissions</span></span>

<span data-ttu-id="297a7-177">建立名為 _phpappuser_ 的資料庫使用者，並將 `sampledb` 資料庫中所有的權限授權給它。</span><span class="sxs-lookup"><span data-stu-id="297a7-177">Create a database user called _phpappuser_ and give it all privileges in the `sampledb` database.</span></span>

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* TO 'phpappuser';
```

<span data-ttu-id="297a7-178">輸入 `quit` 結束伺服器連線。</span><span class="sxs-lookup"><span data-stu-id="297a7-178">Exit the server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="connect-app-to-azure-mysql"></a><span data-ttu-id="297a7-179">將應用程式連線至 Azure MySQL</span><span class="sxs-lookup"><span data-stu-id="297a7-179">Connect app to Azure MySQL</span></span>

<span data-ttu-id="297a7-180">在此步驟中，您要將 PHP 應用程式連線至您在適用於 MySQL 的 Azure 資料庫 (預覽) 中建立的 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="297a7-180">In this step, you connect the PHP application to the MySQL database you created in Azure Database for MySQL (Preview).</span></span>

<a name="devconfig"></a>

### <a name="configure-the-database-connection"></a><span data-ttu-id="297a7-181">設定資料庫連接</span><span class="sxs-lookup"><span data-stu-id="297a7-181">Configure the database connection</span></span>

<span data-ttu-id="297a7-182">在存放庫根目錄中，建立 _.env.production_ 檔案，並將下列變數複製到檔案中。</span><span class="sxs-lookup"><span data-stu-id="297a7-182">In the repository root, create an _.env.production_ file and copy the following variables into it.</span></span> <span data-ttu-id="297a7-183">取代預留位置 _&lt;mysql_server_name>_。</span><span class="sxs-lookup"><span data-stu-id="297a7-183">Replace the placeholder _&lt;mysql_server_name>_.</span></span>

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

<span data-ttu-id="297a7-184">儲存變更。</span><span class="sxs-lookup"><span data-stu-id="297a7-184">Save the changes.</span></span>

> [!TIP]
> <span data-ttu-id="297a7-185">為了保護您的 MySQL 連接資訊，Git 存放庫中已經排除此檔案 (請看_.gitignore_ 存放庫的根目錄)。</span><span class="sxs-lookup"><span data-stu-id="297a7-185">To secure your MySQL connection information, this file is already excluded from the Git repository (See _.gitignore_ in the repository root).</span></span> <span data-ttu-id="297a7-186">稍後，您將了解如何設定 App Service 中的環境變數，來連線至適用於 MySQL 的 Azure 資料庫 (預覽)。</span><span class="sxs-lookup"><span data-stu-id="297a7-186">Later, you learn how to configure environment variables in App Service to connect to your database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="297a7-187">使用環境變數，您在 App Service 中就不需要 *.env* 檔案。</span><span class="sxs-lookup"><span data-stu-id="297a7-187">With environment variables, you don't need the *.env* file in App Service.</span></span>
>

### <a name="configure-ssl-certificate"></a><span data-ttu-id="297a7-188">設定 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="297a7-188">Configure SSL certificate</span></span>

<span data-ttu-id="297a7-189">根據預設，用於 MySQL 的 Azure 資料庫會強制用戶端使用 SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="297a7-189">By default, Azure Database for MySQL enforces SSL connections from clients.</span></span> <span data-ttu-id="297a7-190">若要連線到您在 Azure 中的 MySQL 資料庫，您必須使用 _.pem_ SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="297a7-190">To connect to your MySQL database in Azure, you must use a _.pem_ SSL certificate.</span></span>

<span data-ttu-id="297a7-191">開啟 _config/database.php_，在 `connections.mysql` 中新增 _sslmode_ 和 _options_ 參數，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="297a7-191">Open _config/database.php_ and add the _sslmode_ and _options_ parameters to `connections.mysql`, as shown in the following code.</span></span>

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

<span data-ttu-id="297a7-192">若要了解如何產生此 _certificate.pem_，請參閱[在您的應用程式中設定 SSL 連線能力，以安全地連線至適用於 MySQL 的 Azure 資料庫](../mysql/howto-configure-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="297a7-192">To learn how to generate this _certificate.pem_, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](../mysql/howto-configure-ssl.md).</span></span>

> [!TIP]
> <span data-ttu-id="297a7-193">_/ssl/certificate.pem_ 路徑指向 Git 存放庫中現有的 _certificate.pem_ 檔案。</span><span class="sxs-lookup"><span data-stu-id="297a7-193">The path _/ssl/certificate.pem_ points to an existing _certificate.pem_ file in the Git repository.</span></span> <span data-ttu-id="297a7-194">本教學課程為了方便起見提供這個檔案。</span><span class="sxs-lookup"><span data-stu-id="297a7-194">This file is provided for convenience in this tutorial.</span></span> <span data-ttu-id="297a7-195">實際的最佳做法是您不應該認可您的 _.pem_ 憑證進入原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="297a7-195">For best practice, you should not commit your _.pem_ certificates into source control.</span></span> 
>

### <a name="test-the-application-locally"></a><span data-ttu-id="297a7-196">在本機測試應用程式</span><span class="sxs-lookup"><span data-stu-id="297a7-196">Test the application locally</span></span>

<span data-ttu-id="297a7-197">使用 _.env.production_ 作為環境檔案來執行 Laravel 資料庫移轉，可在適用於 MySQL 的 Azure 資料庫 (預覽) 中建立資料表。</span><span class="sxs-lookup"><span data-stu-id="297a7-197">Run Laravel database migrations with _.env.production_ as the environment file to create the tables in your MySQL database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="297a7-198">請記住，_.env.production_ 中有連線至您在 Azure 中的 MySQL 資料庫的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="297a7-198">Remember that _.env.production_ has the connection information to your MySQL database in Azure.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="297a7-199">_.env.production_ 沒有有效的應用程式金鑰。</span><span class="sxs-lookup"><span data-stu-id="297a7-199">_.env.production_ doesn't have a valid application key yet.</span></span> <span data-ttu-id="297a7-200">在終端機中為它產生一個新的。</span><span class="sxs-lookup"><span data-stu-id="297a7-200">Generate a new one for it in the terminal.</span></span>

```bash
php artisan key:generate --env=production --force
```

<span data-ttu-id="297a7-201">使用 _.env.production_ 作為環境檔案來執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="297a7-201">Run the sample application with _.env.production_ as the environment file.</span></span>

```bash
php artisan serve --env=production
```

<span data-ttu-id="297a7-202">瀏覽至 `http://localhost:8000`。</span><span class="sxs-lookup"><span data-stu-id="297a7-202">Navigate to `http://localhost:8000`.</span></span> <span data-ttu-id="297a7-203">如果頁面載入無誤，PHP 應用程式就會連線至 Azure 中的 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="297a7-203">If the page loads without errors, the PHP application is connecting to the MySQL database in Azure.</span></span>

<span data-ttu-id="297a7-204">在頁面中新增幾項工作。</span><span class="sxs-lookup"><span data-stu-id="297a7-204">Add a few tasks in the page.</span></span>

![PHP 順利連線至適用於 MySQL 的 Azure 資料庫 (預覽)](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="297a7-206">若要停止 PHP，請在終端機中輸入 `Ctrl + C`。</span><span class="sxs-lookup"><span data-stu-id="297a7-206">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

### <a name="commit-your-changes"></a><span data-ttu-id="297a7-207">認可變更</span><span class="sxs-lookup"><span data-stu-id="297a7-207">Commit your changes</span></span>

<span data-ttu-id="297a7-208">執行下列的 Git 命令認可您的變更：</span><span class="sxs-lookup"><span data-stu-id="297a7-208">Run the following Git commands to commit your changes:</span></span>

```bash
git add .
git commit -m "database.php updates"
```

<span data-ttu-id="297a7-209">您的應用程式已準備好進行部署。</span><span class="sxs-lookup"><span data-stu-id="297a7-209">Your app is ready to be deployed.</span></span>

## <a name="deploy-to-azure"></a><span data-ttu-id="297a7-210">部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="297a7-210">Deploy to Azure</span></span>

<span data-ttu-id="297a7-211">在此步驟中，您要將已與 MySQL 連線的 PHP 應用程式部署至 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="297a7-211">In this step, you deploy the MySQL-connected PHP application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="297a7-212">建立應用程式服務方案</span><span class="sxs-lookup"><span data-stu-id="297a7-212">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="297a7-213">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="297a7-213">Create a web app</span></span>

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-the-php-version"></a><span data-ttu-id="297a7-214">設定 PHP 版本</span><span class="sxs-lookup"><span data-stu-id="297a7-214">Set the PHP version</span></span>

<span data-ttu-id="297a7-215">使用 [az webapp config set](/cli/azure/webapp/config#set) 命令設定應用程式所需的 PHP 版本。</span><span class="sxs-lookup"><span data-stu-id="297a7-215">Set the PHP version that the application requires by using the [az webapp config set](/cli/azure/webapp/config#set) command.</span></span>

<span data-ttu-id="297a7-216">下列命令會將 PHP 版本設定為 _7.0_。</span><span class="sxs-lookup"><span data-stu-id="297a7-216">The following command sets the PHP version to _7.0_.</span></span>

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a><span data-ttu-id="297a7-217">設定資料庫設定</span><span class="sxs-lookup"><span data-stu-id="297a7-217">Configure database settings</span></span>

<span data-ttu-id="297a7-218">如先前所指出，您可以使用 App Service 中的環境變數，連線至 Azure MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="297a7-218">As pointed out previously, you can connect to your Azure MySQL database using environment variables in App Service.</span></span>

<span data-ttu-id="297a7-219">在 App Service 中，您可以使用 [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) 命令將環境變數設定為「應用程式設定」。</span><span class="sxs-lookup"><span data-stu-id="297a7-219">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span>

<span data-ttu-id="297a7-220">下列命令會設定 `DB_HOST`、`DB_DATABASE`、`DB_USERNAME`、`DB_PASSWORD` 應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="297a7-220">The following command configures the app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span></span> <span data-ttu-id="297a7-221">取代預留位置 _&lt;appname>_ 和 _&lt;mysql_server_name>_。</span><span class="sxs-lookup"><span data-stu-id="297a7-221">Replace the placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

<span data-ttu-id="297a7-222">您可以使用 PHP [getenv](http://www.php.net/manual/function.getenv.php) 方法來存取這些設定。</span><span class="sxs-lookup"><span data-stu-id="297a7-222">You can use the PHP [getenv](http://www.php.net/manual/function.getenv.php) method to access the settings.</span></span> <span data-ttu-id="297a7-223">Laravel 程式碼會透過 PHP `getenv` 使用 [env](https://laravel.com/docs/5.4/helpers#method-env) 包裝函式。</span><span class="sxs-lookup"><span data-stu-id="297a7-223">the Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over the PHP `getenv`.</span></span> <span data-ttu-id="297a7-224">例如，在 _config/database.php_ 中的 MySQL 設定看起來像這樣︰</span><span class="sxs-lookup"><span data-stu-id="297a7-224">For example, the MySQL configuration in _config/database.php_ looks like the following code:</span></span>

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

### <a name="configure-laravel-environment-variables"></a><span data-ttu-id="297a7-225">設定 Laravel 環境變數</span><span class="sxs-lookup"><span data-stu-id="297a7-225">Configure Laravel environment variables</span></span>

<span data-ttu-id="297a7-226">Laravel 在 App Service 中需要應用程式金鑰。</span><span class="sxs-lookup"><span data-stu-id="297a7-226">Laravel needs an application key in App Service.</span></span> <span data-ttu-id="297a7-227">您可以使用應用程式設定加以設定。</span><span class="sxs-lookup"><span data-stu-id="297a7-227">You can configure it with app settings.</span></span>

<span data-ttu-id="297a7-228">使用 `php artisan` 產生新的應用程式金鑰，而不將它儲存為 _.env_。</span><span class="sxs-lookup"><span data-stu-id="297a7-228">Use `php artisan` to generate a new application key without saving it to _.env_.</span></span>

```bash
php artisan key:generate --show
```

<span data-ttu-id="297a7-229">使用 [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) 命令來設定 App Service Web 應用程式中的應用程式金鑰。</span><span class="sxs-lookup"><span data-stu-id="297a7-229">Set the application key in the App Service web app by using the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span> <span data-ttu-id="297a7-230">取代 _&lt;appname>_ 和 _&lt;outputofphpartisankey:generate>_ 預留位置。</span><span class="sxs-lookup"><span data-stu-id="297a7-230">Replace the placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

<span data-ttu-id="297a7-231">當部署的 Web 應用程式遇到錯誤，`APP_DEBUG="true"` 會告訴 Laravel 傳回偵錯資訊。</span><span class="sxs-lookup"><span data-stu-id="297a7-231">`APP_DEBUG="true"` tells Laravel to return debugging information when the deployed web app encounters errors.</span></span> <span data-ttu-id="297a7-232">執行生產環境應用程式時，將它設為 `false` 會更安全。</span><span class="sxs-lookup"><span data-stu-id="297a7-232">When running a production application, set it to `false`, which is more secure.</span></span>

### <a name="set-the-virtual-application-path"></a><span data-ttu-id="297a7-233">設定虛擬應用程式路徑</span><span class="sxs-lookup"><span data-stu-id="297a7-233">Set the virtual application path</span></span>

<span data-ttu-id="297a7-234">設定 Web 應用程式的虛擬應用程式路徑。</span><span class="sxs-lookup"><span data-stu-id="297a7-234">Set the virtual application path for the web app.</span></span> <span data-ttu-id="297a7-235">需要執行此步驟，是因為 [Laravel 應用程式生命週期](https://laravel.com/docs/5.4/lifecycle)是在「公用」目錄中啟動，而不是在應用程式的根目錄。</span><span class="sxs-lookup"><span data-stu-id="297a7-235">This step is required because the [Laravel application lifecycle](https://laravel.com/docs/5.4/lifecycle) begins in the _public_ directory instead of the application's root directory.</span></span> <span data-ttu-id="297a7-236">在根目錄中啟動生命週期的其他 PHP 架構，不需要手動設定虛擬應用程式路徑即可運作。</span><span class="sxs-lookup"><span data-stu-id="297a7-236">Other PHP frameworks whose lifecycle start in the root directory can work without manual configuration of the virtual application path.</span></span>

<span data-ttu-id="297a7-237">使用 [az resource update](/cli/azure/resource#update) 命令設定虛擬應用程式的路徑。</span><span class="sxs-lookup"><span data-stu-id="297a7-237">Set the virtual application path by using the [az resource update](/cli/azure/resource#update) command.</span></span> <span data-ttu-id="297a7-238">取代 _&lt;appname>_ 預留位置。</span><span class="sxs-lookup"><span data-stu-id="297a7-238">Replace the _&lt;appname>_ placeholder.</span></span>

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

<span data-ttu-id="297a7-239">依預設，Azure App Service 會將根虛擬應用程式路徑 (_/_) 指向已部署應用程式檔案的根目錄 (_sites\wwwroot_)。</span><span class="sxs-lookup"><span data-stu-id="297a7-239">By default, Azure App Service points the root virtual application path (_/_) to the root directory of the deployed application files (_sites\wwwroot_).</span></span>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="297a7-240">設定部署使用者</span><span class="sxs-lookup"><span data-stu-id="297a7-240">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a><span data-ttu-id="297a7-241">設定本機 Git 部署</span><span class="sxs-lookup"><span data-stu-id="297a7-241">Configure local Git deployment</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-to-azure-from-git"></a><span data-ttu-id="297a7-242">從 Git 推送至 Azure</span><span class="sxs-lookup"><span data-stu-id="297a7-242">Push to Azure from Git</span></span>

<span data-ttu-id="297a7-243">將 Azure 遠端新增至本機 Git 存放庫。</span><span class="sxs-lookup"><span data-stu-id="297a7-243">Add an Azure remote to your local Git repository.</span></span>

```bash
git remote add azure <paste_copied_url_here>
```

<span data-ttu-id="297a7-244">推送至 Azure 遠端以部署 PHP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="297a7-244">Push to the Azure remote to deploy the PHP application.</span></span> <span data-ttu-id="297a7-245">建立部署使用者時，系統會提示您輸入稍早提供的密碼。</span><span class="sxs-lookup"><span data-stu-id="297a7-245">You are prompted for the password you supplied earlier as part of the creation of the deployment user.</span></span>

```bash
git push azure master
```

<span data-ttu-id="297a7-246">在部署期間，Azure App Service 會與 Git 溝通其進度。</span><span class="sxs-lookup"><span data-stu-id="297a7-246">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 3, done.
Delta compression using up to 8 threads.
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
> <span data-ttu-id="297a7-247">您可能會注意到，部署程序會在結尾安裝 [Composer](https://getcomposer.org/) 套件。</span><span class="sxs-lookup"><span data-stu-id="297a7-247">You may notice that the deployment process installs [Composer](https://getcomposer.org/) packages at the end.</span></span> <span data-ttu-id="297a7-248">App Service 不會在預設部署期間執行這些自動化，因此，這個範例存放庫在其根目錄中有三個其他檔案可啟用它：</span><span class="sxs-lookup"><span data-stu-id="297a7-248">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory to enable it:</span></span>
>
> - <span data-ttu-id="297a7-249">`.deployment` - 此檔案會告訴 App Service，執行 `bash deploy.sh` 以做為自訂部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="297a7-249">`.deployment` - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span></span>
> - <span data-ttu-id="297a7-250">`deploy.sh` - 自訂部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="297a7-250">`deploy.sh` - The custom deployment script.</span></span> <span data-ttu-id="297a7-251">如果您檢閱檔案，您將看到它會在 `npm install` 之後執行 `php composer.phar install`。</span><span class="sxs-lookup"><span data-stu-id="297a7-251">If you review the file, you will see that it runs `php composer.phar install` after `npm install`.</span></span>
> - <span data-ttu-id="297a7-252">`composer.phar` - Composer 套件管理員。</span><span class="sxs-lookup"><span data-stu-id="297a7-252">`composer.phar` - The Composer package manager.</span></span>
>
> <span data-ttu-id="297a7-253">您可以使用這種方法，將您任何以 Git 為基礎的部署步驟新增至 App Service。</span><span class="sxs-lookup"><span data-stu-id="297a7-253">You can use this approach to add any step to your Git-based deployment to App Service.</span></span> <span data-ttu-id="297a7-254">如需相關資訊，請參閱[自訂部署指令碼](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script)。</span><span class="sxs-lookup"><span data-stu-id="297a7-254">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span></span>
>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="297a7-255">瀏覽至 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="297a7-255">Browse to the Azure web app</span></span>

<span data-ttu-id="297a7-256">瀏覽至 `http://<app_name>.azurewebsites.net` 並將幾項工作新增至清單。</span><span class="sxs-lookup"><span data-stu-id="297a7-256">Browse to `http://<app_name>.azurewebsites.net` and add a few tasks to the list.</span></span>

![在 Azure App Service 中執行的 PHP 應用程式](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

<span data-ttu-id="297a7-258">恭喜，您正在 Azure App Service 中執行資料驅動的 PHP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="297a7-258">Congratulations, you're running a data-driven PHP app in Azure App Service.</span></span>

## <a name="update-model-locally-and-redeploy"></a><span data-ttu-id="297a7-259">在本機更新模型並重新部署</span><span class="sxs-lookup"><span data-stu-id="297a7-259">Update model locally and redeploy</span></span>

<span data-ttu-id="297a7-260">在此步驟中，您會簡單變更 `task` 資料模型和 webapp，然後將更新發行至 Azure。</span><span class="sxs-lookup"><span data-stu-id="297a7-260">In this step, you make a simple change to the `task` data model and the webapp, and then publish the update to Azure.</span></span>

<span data-ttu-id="297a7-261">在此工作案例中，您將修改應用程式，讓您可以將工作標示為完成。</span><span class="sxs-lookup"><span data-stu-id="297a7-261">For the tasks scenario, you modify the application so that you can mark a task as complete.</span></span>

### <a name="add-a-column"></a><span data-ttu-id="297a7-262">新增資料行</span><span class="sxs-lookup"><span data-stu-id="297a7-262">Add a column</span></span>

<span data-ttu-id="297a7-263">在終端機中，瀏覽至 Git 存放庫的根目錄。</span><span class="sxs-lookup"><span data-stu-id="297a7-263">In the terminal, navigate to the root of the Git repository.</span></span>

<span data-ttu-id="297a7-264">為 `tasks` 資料表產生新的資料庫移轉：</span><span class="sxs-lookup"><span data-stu-id="297a7-264">Generate a new database migration for the `tasks` table:</span></span>

```bash
php artisan make:migration add_complete_column --table=tasks
```

<span data-ttu-id="297a7-265">此命令會顯示所產生的移轉檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="297a7-265">This command shows you the name of the migration file that's generated.</span></span> <span data-ttu-id="297a7-266">在 _database/migrations_ 中找到這個檔案並開啟它。</span><span class="sxs-lookup"><span data-stu-id="297a7-266">Find this file in _database/migrations_ and open it.</span></span>

<span data-ttu-id="297a7-267">以下列程式碼取代 `up` 方法：</span><span class="sxs-lookup"><span data-stu-id="297a7-267">Replace the `up` method with the following code:</span></span>

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

<span data-ttu-id="297a7-268">上方的程式碼會在名為 `complete` 的 `tasks` 資料表中新增布林值資料行。</span><span class="sxs-lookup"><span data-stu-id="297a7-268">The preceding code adds a boolean column in the `tasks` table called `complete`.</span></span>

<span data-ttu-id="297a7-269">將 `down` 方法取代為下列程式碼以進行復原動作︰</span><span class="sxs-lookup"><span data-stu-id="297a7-269">Replace the `down` method with the following code for the rollback action:</span></span>

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

<span data-ttu-id="297a7-270">在終端機中，執行 Laravel 資料庫移轉，以在本機資料庫中進行變更。</span><span class="sxs-lookup"><span data-stu-id="297a7-270">In the terminal, run Laravel database migrations to make the change in the local database.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="297a7-271">根據 [Laravel 命名慣例](https://laravel.com/docs/5.4/eloquent#defining-models)，依預設 `Task` 模型 (請看 app/Task.php) 會對應至 `tasks` 資料表。</span><span class="sxs-lookup"><span data-stu-id="297a7-271">Based on the [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), the model `Task` (see _app/Task.php_) maps to the `tasks` table by default.</span></span>

### <a name="update-application-logic"></a><span data-ttu-id="297a7-272">更新應用程式邏輯</span><span class="sxs-lookup"><span data-stu-id="297a7-272">Update application logic</span></span>

<span data-ttu-id="297a7-273">開啟 *routes/web.php* 檔案。</span><span class="sxs-lookup"><span data-stu-id="297a7-273">Open the *routes/web.php* file.</span></span> <span data-ttu-id="297a7-274">應用程式會在這裡定義其路由和商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="297a7-274">The application defines its routes and business logic here.</span></span>

<span data-ttu-id="297a7-275">在檔案的結尾，使用下列程式碼新增路由︰</span><span class="sxs-lookup"><span data-stu-id="297a7-275">At the end of the file, add a route with the following code:</span></span>

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

<span data-ttu-id="297a7-276">上方的程式碼會切換 `complete` 的值，對資料模型進行簡單的更新。</span><span class="sxs-lookup"><span data-stu-id="297a7-276">The preceding code makes a simple update to the data model by toggling the value of `complete`.</span></span>

### <a name="update-the-view"></a><span data-ttu-id="297a7-277">更新檢視</span><span class="sxs-lookup"><span data-stu-id="297a7-277">Update the view</span></span>

<span data-ttu-id="297a7-278">開啟 *resources/views/tasks.blade.php* 檔案。</span><span class="sxs-lookup"><span data-stu-id="297a7-278">Open the *resources/views/tasks.blade.php* file.</span></span> <span data-ttu-id="297a7-279">尋找 `<tr>` 開頭標記，並將它取代為︰</span><span class="sxs-lookup"><span data-stu-id="297a7-279">Find the `<tr>` opening tag and replace it with:</span></span>

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

<span data-ttu-id="297a7-280">上方的程式碼會視工作是否完成來變更資料列色彩。</span><span class="sxs-lookup"><span data-stu-id="297a7-280">The preceding code changes the row color depending on whether the task is complete.</span></span>

<span data-ttu-id="297a7-281">在下一行中，您會有下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="297a7-281">In the next line, you have the following code:</span></span>

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

<span data-ttu-id="297a7-282">將這一整行取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="297a7-282">Replace the entire line with the following code:</span></span>

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

<span data-ttu-id="297a7-283">上方的程式碼新增的提交按鈕會參考您稍早定義的路由。</span><span class="sxs-lookup"><span data-stu-id="297a7-283">The preceding code adds the submit button that references the route that you defined earlier.</span></span>

### <a name="test-the-changes-locally"></a><span data-ttu-id="297a7-284">本機測試變更</span><span class="sxs-lookup"><span data-stu-id="297a7-284">Test the changes locally</span></span>

<span data-ttu-id="297a7-285">從 Git 存放庫的根目錄，執行程式開發伺服器。</span><span class="sxs-lookup"><span data-stu-id="297a7-285">From the root directory of the Git repository, run the development server.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="297a7-286">若要查看工作狀態的變更，瀏覽至 `http://localhost:8000`，然後選取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="297a7-286">To see the task status change, navigate to `http://localhost:8000` and select the checkbox.</span></span>

![已將核取方塊新增至工作](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

<span data-ttu-id="297a7-288">若要停止 PHP，請在終端機中輸入 `Ctrl + C`。</span><span class="sxs-lookup"><span data-stu-id="297a7-288">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

### <a name="publish-changes-to-azure"></a><span data-ttu-id="297a7-289">將變更發佈至 Azure</span><span class="sxs-lookup"><span data-stu-id="297a7-289">Publish changes to Azure</span></span>

<span data-ttu-id="297a7-290">在終端機中，使用生產環境連接字串執行 Laravel 資料庫移轉，以在 Azure 資料庫中進行變更。</span><span class="sxs-lookup"><span data-stu-id="297a7-290">In the terminal, run Laravel database migrations with the production connection string to make the change in the Azure database.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="297a7-291">在 Git 中認可所有變更，然後將程式碼變更推送至 Azure。</span><span class="sxs-lookup"><span data-stu-id="297a7-291">Commit all the changes in Git, and then push the code changes to Azure.</span></span>

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

<span data-ttu-id="297a7-292">完成 `git push` 之後，瀏覽至 Azure Web 應用程式，然後測試新功能。</span><span class="sxs-lookup"><span data-stu-id="297a7-292">Once the `git push` is complete, navigate to the Azure web app and test the new functionality.</span></span>

![發佈至 Azure 的模型和資料庫變更](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="297a7-294">如果您新增任何工作，它們會保留在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="297a7-294">If you added any tasks, they are retained in the database.</span></span> <span data-ttu-id="297a7-295">對資料結構描述進行的更新，現有資料會原封不動。</span><span class="sxs-lookup"><span data-stu-id="297a7-295">Updates to the data schema leave existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="297a7-296">資料流診斷記錄</span><span class="sxs-lookup"><span data-stu-id="297a7-296">Stream diagnostic logs</span></span>

<span data-ttu-id="297a7-297">當 PHP 應用程式在 Azure App Service 中執行時，您可以使用管線將主控台記錄傳送至終端機。</span><span class="sxs-lookup"><span data-stu-id="297a7-297">While the PHP application runs in Azure App Service, you can get the console logs piped to your terminal.</span></span> <span data-ttu-id="297a7-298">這樣一來，您就能取得相同的診斷訊息，以協助您偵錯應用程式錯誤。</span><span class="sxs-lookup"><span data-stu-id="297a7-298">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="297a7-299">請使用 [az webapp log tail](/cli/azure/webapp/log#tail) 命令開始記錄資料流。</span><span class="sxs-lookup"><span data-stu-id="297a7-299">To start log streaming, use the [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

<span data-ttu-id="297a7-300">開始記錄資料流之後，重新整理瀏覽器中的 Azure Web 應用程式，以取得部分 Web 流量。</span><span class="sxs-lookup"><span data-stu-id="297a7-300">Once log streaming has started, refresh the Azure web app in the browser to get some web traffic.</span></span> <span data-ttu-id="297a7-301">您現在會看到使用管線傳送到終端機的主控台記錄。</span><span class="sxs-lookup"><span data-stu-id="297a7-301">You can now see console logs piped to the terminal.</span></span> <span data-ttu-id="297a7-302">如果您沒有立即看到主控台記錄，請在 30 秒後再查看。</span><span class="sxs-lookup"><span data-stu-id="297a7-302">If you don't see console logs immediately, check again in 30 seconds.</span></span>

<span data-ttu-id="297a7-303">若要隨時停止記錄資料流，輸入 `Ctrl`+`C`。</span><span class="sxs-lookup"><span data-stu-id="297a7-303">To stop log streaming at anytime, type `Ctrl`+`C`.</span></span>

> [!TIP]
> <span data-ttu-id="297a7-304">PHP 應用程式可以使用標準 [error_log()](http://php.net/manual/function.error-log.php) 輸出到主控台。</span><span class="sxs-lookup"><span data-stu-id="297a7-304">A PHP application can use the standard [error_log()](http://php.net/manual/function.error-log.php) to output to the console.</span></span> <span data-ttu-id="297a7-305">範例應用程式會在 _app/Http/routes.php_ 中使用這種方法。</span><span class="sxs-lookup"><span data-stu-id="297a7-305">The sample application uses this approach in _app/Http/routes.php_.</span></span>
>
> <span data-ttu-id="297a7-306">如同 web 架構，[Laravel 會使用 Monolog](https://laravel.com/docs/5.4/errors) 作為記錄提供者。</span><span class="sxs-lookup"><span data-stu-id="297a7-306">As a web framework, [Laravel uses Monolog](https://laravel.com/docs/5.4/errors) as the logging provider.</span></span> <span data-ttu-id="297a7-307">若要了解如何使 Monolog 將訊息輸出至主控台，請參閱 [PHP︰如何使用 Monolog 記錄至主控台 (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out)。</span><span class="sxs-lookup"><span data-stu-id="297a7-307">To see how to get Monolog to output messages to the console, see [PHP: How to use monolog to log to console (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span></span>
>
>

## <a name="manage-the-azure-web-app"></a><span data-ttu-id="297a7-308">管理 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="297a7-308">Manage the Azure web app</span></span>

<span data-ttu-id="297a7-309">請移至 [Azure 入口網站](https://portal.azure.com)，以管理您所建立的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="297a7-309">Go to the [Azure portal](https://portal.azure.com) to manage the web app you created.</span></span>

<span data-ttu-id="297a7-310">按一下左側功能表中的 [應用程式服務]，然後按一下 Azure Web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="297a7-310">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![入口網站瀏覽至 Azure Web 應用程式](./media/app-service-web-tutorial-php-mysql/access-portal.png)

<span data-ttu-id="297a7-312">您會看到 Web 應用程式的 [概觀] 頁面。</span><span class="sxs-lookup"><span data-stu-id="297a7-312">You see your web app's Overview page.</span></span> <span data-ttu-id="297a7-313">您可以在這裡執行基本管理工作，像是停止、啟動、重新啟動、瀏覽、刪除。</span><span class="sxs-lookup"><span data-stu-id="297a7-313">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span></span>

<span data-ttu-id="297a7-314">左側功能表提供的頁面可用來設定您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="297a7-314">The left menu provides pages for configuring your app.</span></span>

![Azure 入口網站中的 App Service 頁面](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="297a7-316">後續步驟</span><span class="sxs-lookup"><span data-stu-id="297a7-316">Next steps</span></span>

<span data-ttu-id="297a7-317">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="297a7-317">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="297a7-318">在 Azure 中建立 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="297a7-318">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="297a7-319">將 PHP 應用程式連線至 MySQL</span><span class="sxs-lookup"><span data-stu-id="297a7-319">Connect a PHP app to MySQL</span></span>
> * <span data-ttu-id="297a7-320">將應用程式部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="297a7-320">Deploy the app to Azure</span></span>
> * <span data-ttu-id="297a7-321">將資料模型更新並將應用程式重新部署</span><span class="sxs-lookup"><span data-stu-id="297a7-321">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="297a7-322">來自 Azure 的串流診斷記錄</span><span class="sxs-lookup"><span data-stu-id="297a7-322">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="297a7-323">在 Azure 入口網站中管理應用程式</span><span class="sxs-lookup"><span data-stu-id="297a7-323">Manage the app in the Azure portal</span></span>

<span data-ttu-id="297a7-324">前往下一個教學課程，了解如何將自訂的 DNS 名稱對應至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="297a7-324">Advance to the next tutorial to learn how to map a custom DNS name to a web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="297a7-325">將現有的自訂 DNS 名稱對應至 Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="297a7-325">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)

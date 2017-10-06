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
# <a name="build-a-php-and-mysql-web-app-in-azure"></a>在 Azure 中建置 PHP 和 MySQL Web 應用程式

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 提供可高度擴充、自我修復的 Web 主機服務。 本教學課程會示範如何 toocreate PHP web 應用程式在 Azure 中的，並將它連接 tooa MySQL 資料庫。 完成後，您將有一個在 Azure App Service Web Apps 上執行的 [Laravel](https://laravel.com/) 應用程式。

![在 Azure App Service 中執行的 PHP 應用程式](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 在 Azure 中建立 MySQL 資料庫
> * 連接 PHP 應用程式 tooMySQL
> * 部署 hello 應用程式 tooAzure
> * 更新 hello 資料模型，部署 hello 應用程式
> * 來自 Azure 的串流診斷記錄
> * 管理 hello hello Azure 入口網站中的應用程式

## <a name="prerequisites"></a>必要條件

toocomplete 本教學課程：

* [安裝 Git](https://git-scm.com/)
* [安裝 PHP 5.6.4 或更新版本](http://php.net/downloads.php)
* [安裝編輯器](https://getcomposer.org/doc/00-intro.md)
* 啟用下列 PHP 延伸模組 Laravel 需求 hello: OpenSSL、 PDO MySQL、 Mbstring、 Tokenizer、 XML
* [下載並啟動 MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a>準備本機 MySQL

在此步驟中，您可以在本機 MySQL 伺服器中建立資料庫，供您在本教學課程中使用。

### <a name="connect-toolocal-mysql-server"></a>Toolocal MySQL 伺服器連接

在終端機視窗中，連接 tooyour 本機 MySQL 伺服器。 您可以使用這個終端機視窗 toorun hello 的所有命令，在本教學課程。

```bash
mysql -u root -p
```

如果系統提示您輸入密碼，輸入 hello 密碼 hello`root`帳戶。 如果您不記得您的根帳號密碼，請參閱[MySQL： 如何 tooReset hello 根密碼](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html)。

如果您的命令執行成功，表示您的 MySQL 伺服器正在執行。 如果沒有，請確定您的本機 MySQL 伺服器已啟動由下列 hello [MySQL 安裝後步驟](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html)。

### <a name="create-a-database-locally"></a>在本機建立資料庫

在 hello`mysql`提示字元中，建立資料庫。

```sql 
CREATE DATABASE sampledb;
```

輸入 `quit` 即可結束您的伺服器連線。

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a>在本機建立 PHP 應用程式
在此步驟中，您會取得 Laravel 範例應用程式、設定其資料庫連線，並在本機執行。 

### <a name="clone-hello-sample"></a>複製 hello 範例

在 hello 終端機視窗， `cd` tooa 工作目錄。

執行下列命令 tooclone hello 範例儲存機制的 hello。

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

`cd`tooyour 複製的目錄。
安裝所需的 hello 封裝。

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a>設定 MySQL 連線

Hello 儲存機制在根目錄中，建立名為*.env*。 下列變數到 hello 複製 hello *.env*檔案。 取代 hello  _&lt;root_password >_預留位置 hello MySQL root 使用者的密碼。

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

如需有關如何 Laravel 使用 hello 詳細_.env_檔案，請參閱[Laravel 環境組態](https://laravel.com/docs/5.4/configuration#environment-configuration)。

### <a name="run-hello-sample-locally"></a>在本機執行 hello 範例

執行[Laravel 資料庫移轉](https://laravel.com/docs/5.4/migrations)toocreate hello 資料表 hello 應用程式的需求。 哪些資料表在中建立 hello 移轉，查看 hello toosee_資料庫/移轉_hello Git 儲存機制的目錄。

```bash
php artisan migrate
```

產生新的 Laravel 應用程式金鑰。

```bash
php artisan key:generate
```

執行 hello 應用程式。

```bash
php artisan serve
```

瀏覽過`http://localhost:8000`瀏覽器中。 Hello 頁面中新增一些工作。

![PHP 順利連線 tooMySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

輸入 toostop PHP `Ctrl + C` hello 終端機中。

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a>在 Azure 中建立 MySQL

在此步驟中，您會在[適用於 MySQL 的 Azure 資料庫 (預覽)](/azure/mysql) 中建立 MySQL 資料庫。 稍後，您可以設定 hello PHP 應用程式 tooconnect toothis 資料庫。

### <a name="create-a-resource-group"></a>建立資源群組

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a>建立 MySQL 伺服器

Azure 資料庫中建立伺服器的 MySQL （預覽） 以 hello [az mysql 伺服器建立](/cli/azure/mysql/server#create)命令。

在 hello 下列命令，以取代 MySQL 伺服器名稱，您會看到 hello  _&lt;mysql_server_name >_預留位置 (有效的字元是`a-z`， `0-9`，和`-`)。 這個名稱是 hello MySQL 伺服器的主機名稱的一部分 (`<mysql_server_name>.database.windows.net`)，它需要 toobe 全域唯一。

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

建立 hello MySQL 伺服器時，hello Azure CLI 顯示資訊的類似 toohello 下列範例：

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

### <a name="configure-server-firewall"></a>設定伺服器防火牆

建立防火牆規則的 MySQL 伺服器 tooallow 用戶端連接使用 hello [az mysql 伺服器防火牆規則建立](/cli/azure/mysql/server/firewall-rule#create)命令。

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> Azure 資料庫的 MySQL （預覽） 目前並不會限制連線只 tooAzure 服務。 在 Azure 中的 IP 位址動態指派，它是較佳的 tooenable 所有 IP 位址。 hello 服務處於預覽狀態。 我們正在規劃更好的方法來保護您的資料庫。
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a>Tooproduction MySQL 伺服器本機連接

在 hello 終端機視窗中，連接在 Azure 中的 toohello MySQL 伺服器。 使用您先前指定的 hello 值 _&lt;mysql_server_name >_。

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

當提示您輸入密碼，請使用_$tr0ngPa$ w0rd ！_，這是您指定當您建立 hello 資料庫。

### <a name="create-a-production-database"></a>建立生產環境資料庫

在 hello`mysql`提示字元中，建立資料庫。

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a>建立具有權限的使用者

建立資料庫使用者，稱為_phpappuser_並給予其所有特殊權限在 hello`sampledb`資料庫。

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

結束輸入 hello 伺服器連接`quit`。

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a>連接應用程式 tooAzure MySQL

在此步驟中，您可以連接 hello PHP 應用程式 toohello MySQL 資料庫您 Azure 資料庫中建立的 MySQL （預覽）。

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a>設定 hello 資料庫連接

在 hello 儲存機制根目錄中，建立_。 env.production_下列變數到其中的檔案，並複製 hello。 取代 hello 預留位置 _&lt;mysql_server_name >_。

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

儲存 hello 的變更。

> [!TIP]
> 您的 MySQL 連接資訊，此檔案已經排除 hello Git 儲存機制的 toosecure (請參閱_.gitignore_ hello 儲存機制的根目錄中)。 更新版本中，您會學習如何在應用程式服務 tooconnect tooyour tooconfigure 環境變數資料庫 Azure Database 中的 MySQL （預覽）。 環境變數使用，您不需要 hello *.env* App Service 中的檔案。
>

### <a name="configure-ssl-certificate"></a>設定 SSL 憑證

根據預設，用於 MySQL 的 Azure 資料庫會強制用戶端使用 SSL 連線。 在 Azure 中的 tooconnect tooyour MySQL 資料庫，您必須使用_.pem_ SSL 憑證。

開啟_config/database.php_和新增 hello _sslmode_和_選項_參數太`connections.mysql`hello 下列程式碼所示。

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

toolearn 如何 toogenerate 這_certificate.pem_，請參閱[設定 SSL 連接，您的應用程式 toosecurely 所連接的 MySQL tooAzure 資料庫](../mysql/howto-configure-ssl.md)。

> [!TIP]
> hello 路徑_/ssl/certificate.pem_點 tooan 現有_certificate.pem_ hello Git 儲存機制中的檔案。 本教學課程為了方便起見提供這個檔案。 實際的最佳做法是您不應該認可您的 _.pem_ 憑證進入原始檔控制。 
>

### <a name="test-hello-application-locally"></a>在本機測試 hello 應用程式

執行 Laravel 資料庫移轉，而_。 env.production_為 hello MySQL （預覽） 環境內的檔案 toocreate hello 表格中 Azure 資料庫的 MySQL 資料庫。 請記住， _。 env.production_已在 Azure 中的 hello 連線資訊 tooyour MySQL 資料庫。

```bash
php artisan migrate --env=production --force
```

_.env.production_ 沒有有效的應用程式金鑰。 產生一個新的 hello 終端機中。

```bash
php artisan key:generate --env=production --force
```

執行與 hello 範例應用程式_。 env.production_為 hello 環境檔案。

```bash
php artisan serve --env=production
```

瀏覽過`http://localhost:8000`。 如果 hello 頁面載入無錯誤，hello PHP 應用程式正在連接 Azure toohello MySQL 資料庫。

Hello 頁面中新增一些工作。

![PHP 連接成功 tooAzure 資料庫的 MySQL （預覽）](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

輸入 toostop PHP `Ctrl + C` hello 終端機中。

### <a name="commit-your-changes"></a>認可變更

Git 命令 toocommit 執行 hello 下列變更：

```bash
git add .
git commit -m "database.php updates"
```

您的應用程式是部署的準備 toobe。

## <a name="deploy-tooazure"></a>部署 tooAzure

在此步驟中，您可以部署 hello MySQL 連接 PHP 應用程式 tooAzure 應用程式服務。

### <a name="create-an-app-service-plan"></a>建立應用程式服務方案

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a>建立 Web 應用程式

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a>Set hello PHP 版本

Hello 應用程式的設定 hello PHP 版本需要使用 hello [az webapp 組態集](/cli/azure/webapp/config#set)命令。

hello 下列命令設定 hello PHP 版本 too_7.0_。

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a>設定資料庫設定

如先前，您可以連接 tooyour Azure MySQL 資料庫應用程式服務中使用環境變數。

在應用程式服務中，您設定環境變數為_應用程式設定_使用 hello [az webapp config appsettings 組](/cli/azure/webapp/config/appsettings#set)命令。

hello 下列命令會設定 hello 應用程式設定`DB_HOST`， `DB_DATABASE`， `DB_USERNAME`，和`DB_PASSWORD`。 Hello 預留位置取代 _&lt;appname >_和 _&lt;mysql_server_name >_。

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

您可以使用 hello PHP [getenv](http://www.php.net/manual/function.getenv.php)方法 tooaccess hello 設定。 hello Laravel 程式碼會使用[env](https://laravel.com/docs/5.4/helpers#method-env)包裝函式透過 hello PHP `getenv`。 例如，hello MySQL 組態中的_config/database.php_看起來像下列程式碼的 hello:

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

### <a name="configure-laravel-environment-variables"></a>設定 Laravel 環境變數

Laravel 在 App Service 中需要應用程式金鑰。 您可以使用應用程式設定加以設定。

使用`php artisan`toogenerate 新的應用程式金鑰，而不儲存 too_.env_。

```bash
php artisan key:generate --show
```

設定 hello 應用程式中索引鍵 hello App Service web 應用程式使用 hello [az webapp config appsettings 組](/cli/azure/webapp/config/appsettings#set)命令。 Hello 預留位置取代 _&lt;appname >_和 _&lt;outputofphpartisankey： 產生 >_。

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

`APP_DEBUG="true"`會告知 Laravel tooreturn 偵錯資訊 hello 部署 web 應用程式時遇到錯誤。 當執行生產應用程式，將它設定太`false`，這是更安全。

### <a name="set-hello-virtual-application-path"></a>設定 hello 虛擬應用程式路徑

設定 hello hello web 應用程式的虛擬應用程式路徑。 這個步驟是必要的因為 hello [Laravel 應用程式生命週期](https://laravel.com/docs/5.4/lifecycle)一開始會處於 hello_公用_目錄而不是 hello 應用程式的根目錄。 在 hello 根目錄開始其生命週期其他 PHP 架構可以運作而不需要手動設定的 hello 虛擬應用程式路徑。

設定 hello 虛擬應用程式路徑使用 hello [az 資源更新](/cli/azure/resource#update)命令。 取代 hello  _&lt;appname >_預留位置。

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

根據預設，Azure 應用程式服務點 hello 根虛擬應用程式路徑 (_/_) hello toohello 根目錄部署應用程式檔案 (_sites\wwwroot_)。

### <a name="configure-a-deployment-user"></a>設定部署使用者

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a>設定本機 Git 部署

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a>從 Git 推送 tooAzure

新增 Azure 遠端 tooyour 本機 Git 儲存機制。

```bash
git remote add azure <paste_copied_url_here>
```

推送 toohello Azure 遠端 toodeploy hello PHP 應用程式。 系統會提示您稍早提供一部分 hello hello 部署使用者建立的 hello 密碼。

```bash
git push azure master
```

在部署期間，Azure App Service 會與 Git 溝通其進度。

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
> 您可能會注意到 hello 部署程序會安裝[編輯器](https://getcomposer.org/)hello 結尾的封裝。 應用程式服務不會執行這些自動化增加了在預設部署期間，因此這個範例儲存機制有三個額外的檔案其根目錄 tooenable 它：
>
> - `.deployment`-此檔案會告知應用程式服務 toorun `bash deploy.sh` hello 自訂部署指令碼。
> - `deploy.sh`-hello 自訂部署指令碼。 如果您檢閱 hello 檔案時，您會看到應用程式會執行`php composer.phar install`之後`npm install`。
> - `composer.phar`-hello 編輯器封裝管理員。
>
> 您可以使用此方法 tooadd 任何步驟 tooyour Git 架構部署 tooApp 服務。 如需相關資訊，請參閱[自訂部署指令碼](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script)。
>

### <a name="browse-toohello-azure-web-app"></a>瀏覽 toohello Azure web 應用程式

瀏覽過`http://<app_name>.azurewebsites.net`並加入一些工作 toohello 清單。

![在 Azure App Service 中執行的 PHP 應用程式](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

恭喜，您正在 Azure App Service 中執行資料驅動的 PHP 應用程式。

## <a name="update-model-locally-and-redeploy"></a>在本機更新模型並重新部署

在此步驟中，您可以進行簡單的變更 toohello`task`資料模型和 hello webapp，，然後將發行 hello 更新 tooAzure。

Hello 工作案例中，您會修改 hello 應用程式，使您可以將工作標示為完成。

### <a name="add-a-column"></a>新增資料行

在終端機 hello，瀏覽 toohello hello Git 儲存機制的根目錄。

產生新的資料庫移轉 hello`tasks`資料表：

```bash
php artisan make:migration add_complete_column --table=tasks
```

此命令會顯示 hello 所產生的 hello 移轉檔案的名稱。 在 _database/migrations_ 中找到這個檔案並開啟它。

取代 hello`up`方法，以下列程式碼的 hello:

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

hello 上述程式碼的布林資料行會在新增 hello`tasks`資料表稱為`complete`。

取代 hello`down`方法，以下列程式碼執行 hello 復原動作的 hello:

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

在終端機 hello 執行 Laravel 資料庫移轉 toomake hello 變更 hello 本機資料庫中。

```bash
php artisan migrate
```

根據 hello [Laravel 命名慣例](https://laravel.com/docs/5.4/eloquent#defining-models)，hello 模型`Task`(請參閱_app/Task.php_) 對應 toohello`tasks`預設資料表。

### <a name="update-application-logic"></a>更新應用程式邏輯

開啟 hello *routes/web.php*檔案。 hello 應用程式定義的路由和商務邏輯。

在 hello hello 檔案結尾，加入路由以下列程式碼的 hello:

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

hello 上述程式碼就可以簡單更新 toohello 資料模型切換 hello 值`complete`。

### <a name="update-hello-view"></a>更新 hello 檢視

開啟 hello *resources/views/tasks.blade.php*檔案。 尋找 hello`<tr>`開頭標記，並將它取代為：

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

上述程式碼變更 hello 根據 hello 工作是否已完成的資料列色彩 hello。

在 hello 下一行中，您會有下列程式碼的 hello:

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

Hello 整行取代成下列程式碼的 hello:

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

hello 上述程式碼中加入參考先前定義的 hello 路由的 hello 送出按鈕。

### <a name="test-hello-changes-locally"></a>在本機測試 hello 變更

Hello 根目錄中的 hello Git 儲存機制，從執行 hello 程式開發伺服器。

```bash
php artisan serve
```

toosee hello 工作狀態變更，瀏覽過`http://localhost:8000`和選取 hello 核取方塊。

![加入核取方塊 tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

輸入 toostop PHP `Ctrl + C` hello 終端機中。

### <a name="publish-changes-tooazure"></a>發行變更 tooAzure

在終端機 hello 執行 Laravel 資料庫移轉與 hello 生產連接字串 toomake hello 變更 hello Azure 資料庫中。

```bash
php artisan migrate --env=production --force
```

認可 Git 中的所有 hello 變更，並接著推送 hello 程式碼變更 tooAzure。

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

一次 hello`git push`已完成，請瀏覽 toohello Azure web 應用程式和測試 hello 新功能。

![發行 tooAzure 模型與資料庫的變更。](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

如果您加入的任何工作時，它們會保留在 hello 資料庫。 更新 toohello 資料結構描述可讓現有的資料保持不變。

## <a name="stream-diagnostic-logs"></a>資料流診斷記錄

Hello PHP 應用程式執行時 Azure App Service 中，您可以取得 hello 主控台記錄檔傳送的 tooyour 終端機。 這樣一來，您可以取得 hello 相同的診斷訊息 toohelp 您偵錯應用程式錯誤。

資料流中，使用 hello toostart 記錄[az webapp 記錄結尾](/cli/azure/webapp/log#tail)命令。

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

記錄檔資料流啟動之後，重新整理 hello Azure web 應用程式在 hello 瀏覽器 tooget 某些網路流量。 您現在可以看到主控台記錄檔傳送的 toohello 終端機。 如果您沒有立即看到主控台記錄，請在 30 秒後再查看。

在任何時候、 資料流 toostop 記錄類型`Ctrl` + `C`。

> [!TIP]
> PHP 應用程式可以使用 hello 標準[error_log()](http://php.net/manual/function.error-log.php) toooutput toohello 主控台。 hello 範例應用程式使用這個方法在_app/Http/routes.php_。
>
> 一種 web 架構，為[Laravel 使用 Monolog](https://laravel.com/docs/5.4/errors)為 hello 記錄提供者。 toosee 如何 tooget Monolog toooutput 訊息 toohello 主控台中，請參閱[PHP： 如何 toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out)。
>
>

## <a name="manage-hello-azure-web-app"></a>管理 hello Azure web 應用程式

移 toohello [Azure 入口網站](https://portal.azure.com)toomanage hello web 應用程式所建立。

從 hello 左窗格中，按一下 **應用程式服務**，然後按一下hello Azure web 應用程式名稱。

![入口網站瀏覽 tooAzure web 應用程式](./media/app-service-web-tutorial-php-mysql/access-portal.png)

您會看到 Web 應用程式的 [概觀] 頁面。 您可以在這裡執行基本管理工作，像是停止、啟動、重新啟動、瀏覽、刪除。

hello 左側的功能表會提供如何設定您的應用程式頁面。

![Azure 入口網站中的 App Service 頁面](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 在 Azure 中建立 MySQL 資料庫
> * 連接 PHP 應用程式 tooMySQL
> * 部署 hello 應用程式 tooAzure
> * 更新 hello 資料模型，部署 hello 應用程式
> * 來自 Azure 的串流診斷記錄
> * 管理 hello hello Azure 入口網站中的應用程式

前進 toohello 下一個教學課程 toolearn toomap 自訂的 DNS 名稱 tooa web 應用程式的方式。

> [!div class="nextstepaction"]
> [將現有自訂 DNS 名稱 tooAzure Web 應用程式的對應](app-service-web-tutorial-custom-domain.md)

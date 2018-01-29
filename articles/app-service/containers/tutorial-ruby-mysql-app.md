---
title: "在 Linux 上建置的 Ruby 和 MySQL web 應用程式設定 Azure App Service 中 |Microsoft 文件"
description: "了解如何取得 Azure ad 中運作，並連接到 Azure 中的 MySQL 資料庫的 Ruby 應用程式。"
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: cfowler
ms.service: app-service-web
ms.workload: web
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 12/21/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 03b2b4e8f8827a08e1414512d848bd5bed48d674
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/04/2018
---
# <a name="build-a-ruby-and-mysql-web-app-in-azure-app-service-on-linux"></a>在 Linux 上建置的 Ruby 和 MySQL web 應用程式設定 Azure App Service 中

[Linux 上的 App Service](app-service-linux-intro.md) 使用 Linux 作業系統提供可高度擴充、自我修復的 Web 主機服務。 本教學課程會示範如何建立拼音 web 應用程式，並連接到 MySQL 資料庫。 當您完成時，則必須[拼音滑軌上](http://rubyonrails.org/)Linux 上的應用程式服務上執行的應用程式。

![Ruby 上滑軌 Azure App Service 中執行的應用程式](./media/tutorial-ruby-mysql-app/complete-checkbox-published.png)

在本教學課程中，您了解如何：

> [!div class="checklist"]
> * 在 Azure 中建立 MySQL 資料庫
> * Ruby 上滑軌應用程式連接到 MySQL
> * 將應用程式部署至 Azure
> * 將資料模型更新並將應用程式重新部署
> * 來自 Azure 的串流診斷記錄
> * 在 Azure 入口網站中管理應用程式

## <a name="prerequisites"></a>必要條件

若要完成本教學課程：

* [安裝 Git](https://git-scm.com/)
* [安裝 Ruby 2.3](https://www.ruby-lang.org/documentation/installation/)
* [安裝在機殼 5.1 Ruby](http://guides.rubyonrails.org/v5.1/getting_started.html)
* [下載並啟動 MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a>準備本機 MySQL

在此步驟中，您可以在本機 MySQL 伺服器中建立資料庫，供您在本教學課程中使用。

### <a name="connect-to-local-mysql-server"></a>連線至本機 MySQL 伺服器

在終端機視窗中，連線到您的本機 MySQL 伺服器。 您可使用這個終端機視窗來執行本教學課程中的所有命令。

```bash
mysql -u root -p
```

如果系統提示您輸入密碼，請輸入 `root` 帳戶的密碼。 如果您不記得根帳戶密碼，請參閱 [MySQL︰如何重設根密碼](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html)。

如果您的命令執行成功，表示您的 MySQL 伺服器正在執行。 如果沒有，請遵循 [MySQL 後續安裝步驟](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html)，確定您已啟動本機 MySQL 伺服器。

輸入 `quit` 即可結束您的伺服器連線。

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-ruby-on-rails-app-locally"></a>在滑軌應用程式在本機上建立 Ruby
在此步驟中，您可以取得 Ruby 滑軌範例應用程式上、 設定其資料庫連線，和在本機執行。 

### <a name="clone-the-sample"></a>複製範例

在終端機視窗中，使用 `cd` 移至工作目錄。

執行下列命令來複製範例存放庫。

```bash
git clone https://github.com/Azure-Samples/rubyrails-tasks.git
```

使用 `cd` 移至您複製的目錄。 安裝必要的套件。

```bash
cd rubyrails-tasks
bundle install --path vendor/bundle
```

### <a name="configure-mysql-connection"></a>設定 MySQL 連線

在儲存機制中，開啟_config/database.yml_並提供本機 MySQL 根使用者名稱和密碼 （行 13）。 如果您已安裝 MySQL 使用這類工具[Homebrew](https://brew.sh/)，然後在檔案中的認證已設定為預設值 (也就是`root`和空的密碼)。

```txt
default: &default
  adapter: mysql2
  encoding: utf8
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: root
  password:
  socket: /tmp/mysql.sock
```

### <a name="run-the-sample-locally"></a>在本機執行範例

執行[滑軌移轉](http://guides.rubyonrails.org/active_record_migrations.html#running-migrations)建立資料表的應用程式需要。 若要查看哪些資料表會建立在移轉，請查看_db/移轉_目錄中的 Git 儲存機制。

```bash
rake db:create
rake db:migrate
```

執行應用程式。

```bash
rails server
```

在瀏覽器中，瀏覽至 `http://localhost:3000`。 在頁面中新增幾項工作。

![Ruby 滑軌上的已成功連接到 MySQL](./media/tutorial-ruby-mysql-app/mysql-connect-success.png)

若要停止滑軌伺服器，請輸入`Ctrl + C`終端機中。

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a>在 Azure 中建立 MySQL

在此步驟中，您會在[適用於 MySQL 的 Azure 資料庫 (預覽)](/azure/mysql) 中建立 MySQL 資料庫。 稍後，您可以設定拼音滑軌應用程式連接到此資料庫上。

### <a name="create-a-resource-group"></a>建立資源群組

[!INCLUDE [Create resource group](../../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a>建立 MySQL 伺服器

使用 [az mysql server create](/cli/azure/mysql/server?view=azure-cli-latest#az_mysql_server_create) 命令，在適用於 MySQL 的 Azure 資料庫 (預覽) 中建立伺服器。

在下列命令中，在您看見 _&lt;mysql_server_name>_ 預留位置的地方，取代成您自己的 MySQL 伺服器名稱 (有效字元有 `a-z`、`0-9`、`-`)。 這個名稱是 MySQL 伺服器主機名稱 (`<mysql_server_name>.mysql.database.azure.com`) 的一部分，必須是全域唯一的。

```azurecli-interactive
az mysql server create --name <mysql_server_name> --resource-group myResourceGroup --location "North Europe" --admin-user adminuser --admin-password My5up3r$tr0ngPa$w0rd!
```

建立 MySQL 伺服器後，Azure CLI 會顯示類似下列範例的資訊：

```json
{
  "administratorLogin": "adminuser",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<mysql_server_name>.database.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>",
  "location": "northeurope",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  ...
}
```

### <a name="configure-server-firewall"></a>設定伺服器防火牆

使用 [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule?view=azure-cli-latest#az_mysql_server_firewall_rule_create) 命令，建立 MySQL 伺服器的防火牆規則來允許用戶端連線。

```azurecli-interactive
az mysql server firewall-rule create --name allIPs --server <mysql_server_name> --resource-group myResourceGroup --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> 適用於 MySQL 的 Azure 資料庫 (預覽) 目前沒有限制只能連線至 Azure 服務。 由於 Azure 中的 IP 位址為動態指派，最好是啟用所有的 IP 位址。 此服務為預覽狀態。 我們正在規劃更好的方法來保護您的資料庫。
>

### <a name="connect-to-production-mysql-server-locally"></a>在本機連線到生產環境 MySQL 伺服器

在終端機視窗中，連線至 Azure 中的 MySQL 伺服器。 使用您先前為 _&lt;mysql_server_name>_ 指定的值。

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

當提示您輸入密碼，請使用_My5up3r$ tr0ngPa$ w0rd ！_，這是您指定當您建立的資料庫伺服器。

### <a name="create-a-production-database"></a>建立生產環境資料庫

在 `mysql` 提示中，建立資料庫。

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a>建立具有權限的使用者

建立資料庫使用者，稱為_railsappuser_並為它提供所有特殊權限`sampledb`資料庫。

```sql
CREATE USER 'railsappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* TO 'railsappuser';
```

輸入 `quit` 結束伺服器連線。

```sql
quit
```

## <a name="connect-app-to-azure-mysql"></a>將應用程式連線至 Azure MySQL

在此步驟中，您可以連接拼音滑軌您 Azure 資料庫中 MySQL （預覽） 建立的 MySQL 資料庫應用程式。

<a name="devconfig"></a>

### <a name="configure-the-database-connection"></a>設定資料庫連接

在儲存機制中，開啟_config/database.yml_。 在檔案最下方，取代下列程式碼中的實際執行環境變數。 如 _&lt;mysql_server_name >_預留位置，請使用您建立的 MySQL 伺服器的名稱。

```txt
production:
  <<: *default
  host: <%= ENV['DB_HOST'] %>
  port: 3306
  database: <%= ENV['DB_DATABASE'] %>
  username: <%= ENV['DB_USERNAME'] %>
  password: <%= ENV['DB_PASSWORD'] %>
  sslca: ssl/BaltimoreCyberTrustRoot.crt.pem
```

儲存變更。

> [!NOTE]
> `sslca`會加入，而且點的現有_.pem_範例儲存機制中的檔案。 根據預設，用於 MySQL 的 Azure 資料庫會強制用戶端使用 SSL 連線。 這`.pem`憑證是您要如何進行 SSL 連線 Azure 資料庫的 MySQL。 如需詳細資訊，請參閱[在您的應用程式中設定 SSL 連線能力，以安全地連線至適用於 MySQL 的 Azure 資料庫](../../mysql/howto-configure-ssl.md)。
>

### <a name="test-the-application-locally"></a>在本機測試應用程式

在本機的終端機中，設定下列環境變數：

```bash
export DB_HOST=<mysql_server_name>.mysql.database.azure.com
export DB_DATABASE=sampledb 
export DB_USERNAME=railsappuser@<mysql_server_name>
export DB_PASSWORD=MySQLAzure2017
```

執行滑軌資料庫移轉與您剛才設定您在 Azure 資料庫的 MySQL 資料庫中建立資料表，用於 MySQL （預覽） 的實際值。 

```bash
rake db:migrate RAILS_ENV=production
```

在實際執行環境中執行時，滑軌應用程式必須先行編譯的資產。 產生的必要的資產，使用下列命令：

```bash
rake assets:precompile
```

滑軌生產環境也會使用密碼來管理安全性。 產生密碼金鑰。

```bash
rails secret
```

將滑軌實際執行環境所使用的個別變數的祕密金鑰。 為了方便起見，您可以使用相同的索引鍵的兩個變數。

```bash
export RAILS_MASTER_KEY=<output_of_rails_secret>
export SECRET_KEY_BASE=<output_of_rails_secret>
```

啟用滑軌生產環境支援 JavaScript 和 CSS 的檔案。

```bash
export RAILS_SERVE_STATIC_FILES=true
```

在生產環境中執行範例應用程式。

```bash
rails server -e production
```

瀏覽至 `http://localhost:3000`。 如果頁面載入無錯誤，滑軌應用程式上的 Ruby 正在連接至 Azure 中的 MySQL 資料庫。

在頁面中新增幾項工作。

![Ruby 搭配滑軌安裝在成功連接至 Azure 資料庫的 MySQL （預覽）](./media/tutorial-ruby-mysql-app/azure-mysql-connect-success.png)

若要停止滑軌伺服器，請輸入`Ctrl + C`終端機中。

### <a name="commit-your-changes"></a>認可變更

執行下列的 Git 命令認可您的變更：

```bash
git add .
git commit -m "database.yml updates"
```

您的應用程式已準備好進行部署。

## <a name="deploy-to-azure"></a>部署至 Azure

在此步驟中，您部署至 Azure App Service 的 MySQL 連接滑軌應用程式。

### <a name="configure-a-deployment-user"></a>設定部署使用者

[!INCLUDE [Configure deployment user](../../../includes/configure-deployment-user-no-h.md)]

### <a name="create-an-app-service-plan"></a>建立應用程式服務方案

[!INCLUDE [Create app service plan no h](../../../includes/app-service-web-create-app-service-plan-linux-no-h.md)]

### <a name="create-a-web-app"></a>建立 Web 應用程式

在 Cloud Shell 中，使用 [az webapp create](/cli/azure/webapp?view=azure-cli-latest#az_webapp_create) 命令，在 `myAppServicePlan` App Service 方案中建立 Web 應用程式。 

在下列範,了中，使用全域唯一的應用程式名稱 (有效的字元為 `a-z`、`0-9` 和 `-`) 取代 `<app_name>`。 執行階段設定為`RUBY|2.3`，會將部署[預設拼音影像](https://hub.docker.com/r/appsvc/ruby/)。 若要查看所有支援的執行階段，請執行 [az webapp list-runtimes](/cli/azure/webapp?view=azure-cli-latest#az_webapp_list_runtimes)。 

```azurecli-interactive
az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app_name> --runtime "RUBY|2.3" --deployment-local-git
```

建立 Web 應用程式後，Azure CLI 會顯示類似下列範例的輸出：

```json
Local git is configured with url of 'https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git'
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "deploymentLocalGitUrl": "https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git",
  "enabled": true,
  < JSON data removed for brevity. >
}
```

您已建立空的新 Web 應用程式，其中已啟用 Git 部署。

> [!NOTE]
> Git 遠端的 URL 會顯示在 `deploymentLocalGitUrl` 屬性中，其格式為 `https://<username>@<app_name>.scm.azurewebsites.net/<app_name>.git`。 儲存此 URL，稍後您將會用到此資訊。
>

### <a name="configure-database-settings"></a>設定資料庫設定

在應用程式服務中，您設定環境變數為_應用程式設定_使用[az webapp config appsettings 組](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az_webapp_config_appsettings_set)雲端殼層命令。

下列雲端殼層命令會設定應用程式設定`DB_HOST`， `DB_DATABASE`， `DB_USERNAME`，和`DB_PASSWORD`。 取代預留位置 _&lt;appname>_ 和 _&lt;mysql_server_name>_。

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DB_HOST="<mysql_server_name>.mysql.database.azure.com" DB_DATABASE="sampledb" DB_USERNAME="railsappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017"
```

### <a name="configure-rails-environment-variables"></a>設定滑軌環境變數

在本機終端機中，產生新的秘密金鑰，在 Azure 中滑軌實際執行環境。

```bash
rails secret
```

設定滑軌實際執行環境所需的變數。

在下列雲端殼層命令中，將兩個 _&lt;output_of_rails_secret >_預留位置取代您在本機的終端機中產生新的秘密金鑰。

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings RAILS_MASTER_KEY="<output_of_rails_secret>" SECRET_KEY_BASE="<output_of_rails_secret>" RAILS_SERVE_STATIC_FILES="true" ASSETS_PRECOMPILE="true"
```

`ASSETS_PRECOMPILE="true"`會告知預設拼音先行編譯在各 Git 部署資產的容器。

### <a name="push-to-azure-from-git"></a>從 Git 推送至 Azure

在本機的終端機中，將 Azure 的遠端加入您的本機 Git 儲存機制。

```bash
git remote add azure <paste_copied_url_here>
```

推入至 Azure 遠端部署 Ruby 滑軌應用程式上。 建立部署使用者時，系統會提示您輸入稍早提供的密碼。

```bash
git push azure master
```

在部署期間，Azure App Service 會與 Git 溝通其進度。

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

### <a name="browse-to-the-azure-web-app"></a>瀏覽至 Azure Web 應用程式

瀏覽至 `http://<app_name>.azurewebsites.net` 並將幾項工作新增至清單。

![Ruby 上滑軌 Azure App Service 中執行的應用程式](./media/tutorial-ruby-mysql-app/ruby-mysql-in-azure.png)

恭喜，您執行資料驅動的 Ruby 滑軌 Azure App Service 中的應用程式上。

## <a name="update-model-locally-and-redeploy"></a>在本機更新模型並重新部署

在此步驟中，您會簡單變更 `task` 資料模型和 webapp，然後將更新發行至 Azure。

在此工作案例中，您將修改應用程式，讓您可以將工作標示為完成。

### <a name="add-a-column"></a>新增資料行

在終端機中，瀏覽至 Git 存放庫的根目錄。

產生新的移轉，將布林資料行呼叫`Done`至`Tasks`資料表：

```bash
rails generate migration add_Done_to_Tasks Done:boolean
```

此命令會產生新的移轉檔案中_db/移轉_目錄。


在終端機中，執行滑軌資料庫移轉至本機資料庫中進行變更。

```bash
rake db:migrate
```

### <a name="update-application-logic"></a>更新應用程式邏輯

開啟*app/controllers/tasks_controller.rb*檔案。 在檔案結尾，找到下列行：

```rb
params.require(:task).permit(:Description)
```

修改為包含新此行`Done`參數。

```rb
params.require(:task).permit(:Description, :Done)
```

### <a name="update-the-views"></a>更新檢視

開啟*app/views/tasks/_form.html.erb*檔案，也就是編輯表單。

找到行`<%=f.error_span(:Description) %>`並插入下列程式碼正下方：

```erb
<%= f.label :Done, :class => 'control-label col-lg-2' %>
<div class="col-lg-10">
  <%= f.check_box :Done, :class => 'form-control' %>
</div>
```

開啟*app/views/tasks/show.html.erb*檔案，這是單一資料錄檢視頁面。 

找到行`<dd><%= @task.Description %></dd>`並插入下列程式碼正下方：

```erb
  <dt><strong><%= model_class.human_attribute_name(:Done) %>:</strong></dt>
  <dd><%= check_box "task", "Done", {:checked => @task.Done, :disabled => true}%></dd>
```

開啟*app/views/tasks/index.html.erb*是所有記錄的索引頁面的檔案。

找到行`<th><%= model_class.human_attribute_name(:Description) %></th>`並插入下列程式碼正下方：

```erb
<th><%= model_class.human_attribute_name(:Done) %></th>
```

在相同的檔案中，尋找行`<td><%= task.Description %></td>`並插入下列程式碼正下方：

```erb
<td><%= check_box "task", "Done", {:checked => task.Done, :disabled => true} %></td>
```

### <a name="test-the-changes-locally"></a>本機測試變更

在本機的終端機中，執行滑軌伺服器。

```bash
rails server
```

若要查看工作狀態變更，請瀏覽至`http://localhost:3000`以及新增或編輯項目。

![已將核取方塊新增至工作](./media/tutorial-ruby-mysql-app/complete-checkbox.png)

若要停止滑軌伺服器，請輸入`Ctrl + C`終端機中。

### <a name="publish-changes-to-azure"></a>將變更發佈至 Azure

在終端機中，執行滑軌資料庫移轉至 Azure 的資料庫中進行變更的實際執行環境。

```bash
rake db:migrate RAILS_ENV=production
```

在 Git 中認可所有變更，然後將程式碼變更推送至 Azure。

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

完成 `git push` 之後，瀏覽至 Azure Web 應用程式，然後測試新功能。

![發佈至 Azure 的模型和資料庫變更](media/tutorial-ruby-mysql-app/complete-checkbox-published.png)

如果您新增任何工作，它們會保留在資料庫中。 對資料結構描述進行的更新，現有資料會原封不動。

## <a name="manage-the-azure-web-app"></a>管理 Azure Web 應用程式

請移至 [Azure 入口網站](https://portal.azure.com)，以管理您所建立的 Web 應用程式。

按一下左側功能表中的 [應用程式服務]，然後按一下 Azure Web 應用程式的名稱。

![入口網站瀏覽至 Azure Web 應用程式](./media/tutorial-php-mysql-app/access-portal.png)

您會看到 Web 應用程式的 [概觀] 頁面。 您可以在這裡執行基本管理工作，像是停止、啟動、重新啟動、瀏覽、刪除。

左側功能表提供的頁面可用來設定您的應用程式。

![Azure 入口網站中的 App Service 頁面](./media/tutorial-php-mysql-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 在 Azure 中建立 MySQL 資料庫
> * Ruby 上滑軌應用程式連接到 MySQL
> * 將應用程式部署至 Azure
> * 將資料模型更新並將應用程式重新部署
> * 來自 Azure 的串流診斷記錄
> * 在 Azure 入口網站中管理應用程式

前往下一個教學課程，了解如何將自訂的 DNS 名稱對應至 Web 應用程式。

> [!div class="nextstepaction"]
> [將現有的自訂 DNS 名稱對應至 Azure Web Apps](../app-service-web-tutorial-custom-domain.md)

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
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a>在 Azure 中建置 Docker Python 和 PostgreSQL Web 應用程式

Azure Web Apps 提供可高度擴充、自我修復的 Web 主機服務。 本教學課程會示範如何 toocreate 基本的 Docker Python web 應用程式在 Azure 中。 您要連接此應用程式 tooa PostgreSQL 資料庫。 完成之後，您在 [Azure App Service Web Apps](app-service-web-overview.md) 上就會有 Docker 容器內執行的 Python Flask 應用程式。

![Azure App Service 中的 Docker Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

您可以依照下列步驟來 hello macOS 上。 Linux 和 Windows 的指示是在大部分情況下，hello 相同但 hello 差異不詳述於本教學課程。
 
## <a name="prerequisites"></a>必要條件

toocomplete 本教學課程：

1. [安裝 Git](https://git-scm.com/)
1. [安裝 Python](https://www.python.org/downloads/)
1. [安裝及執行 PostgreSQL](https://www.postgresql.org/download/)
1. [安裝 Docker Community 版本](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="test-local-postgresql-installation-and-create-a-database"></a>測試本機 PostgreSQL 安裝並建立資料庫

開啟 hello 終端機視窗，然後執行`psql postgres`tooconnect tooyour 本機 PostgreSQL 伺服器。

```bash
psql postgres
```

如果連線成功，則您的 PostgreSQL 資料庫就已在執行中。 如果沒有，請確定您的本機 PostgresQL 資料庫已啟動在 hello 步驟[下載-PostgreSQL 核心發佈](https://www.postgresql.org/download/)。

建立名為 eventregistration 的資料庫，並且設定名為 manager、密碼為 supersecretpass 的個別資料庫使用者。

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```
型別*\q* tooexit hello PostgreSQL 用戶端。 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a>建立本機 Python Flask 應用程式

在此步驟中，您會將設定 hello 本機 Python 酒瓶專案。

### <a name="clone-hello-sample-application"></a>複製 hello 範例應用程式

開啟 hello 終端機視窗，和`CD`tooa 工作目錄。  

Hello 執行的下列命令 tooclone hello 範例儲存機制，然後移至 toohello *0.1 initialapp*版本。

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

此範例存放庫包含 [Flask](http://flask.pocoo.org/) 應用程式。 

### <a name="run-hello-application"></a>執行 hello 應用程式

> [!NOTE] 
> 在稍後步驟中您會藉由建置 Docker 容器 toouse 與 hello 生產資料庫簡化這個程序。

安裝所需的 hello 封裝並啟動 hello 應用程式。

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

完全載入 hello 應用程式時，您會看到下列訊息類似 toohello:

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

瀏覽 toohttp://127.0.0.1:5000 瀏覽器中。 按一下 [註冊!] 並且建立測試使用者。

![在本機執行的 Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

hello 酒瓶範例應用程式會將使用者資料儲存在 hello 資料庫。 如果您成功註冊使用者時，您的應用程式會撰寫資料 toohello 本機 PostgreSQL 資料庫。

在任何時候、 toostop hello 酒瓶伺服器 hello 終端機中，輸入 Ctrl + C。 

## <a name="create-a-production-postgresql-database"></a>建立生產環境 PostgreSQL 資料庫

在此步驟中，您要在 Azure 中建立 PostgreSQL 資料庫。 已部署的 tooAzure 您的應用程式時，它會使用此雲端的資料庫。

### <a name="log-in-tooazure"></a>登入 tooAzure

您正在進行 toouse hello Azure CLI 2.0 toocreate hello 資源所需 toohost Python 應用程式在 Azure App Service 中。  登入 Azure 訂用帳戶以 hello tooyour [az 登入](/cli/azure/#login)命令，並遵循螢幕上指示 hello。 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a>建立資源群組

建立[資源群組](../azure-resource-manager/resource-group-overview.md)以 hello [az 群組建立](/cli/azure/group#create)。 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

hello 下列範例會建立資源群組 hello 美國西部區域中：

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

使用 hello [az appservice 列出位置](/cli/azure/appservice#list-locations)Azure CLI 命令 toolist 可用的位置。

### <a name="create-an-azure-database-for-postgresql-server"></a>建立適用於 PostgreSQL 的 Azure 資料庫伺服器

建立以 hello PostgreSQL 伺服器[az postgres 伺服器建立](/cli/azure/documentdb#create)命令。

在 hello 下列命令，以取代 hello 的唯一的伺服器名稱 *\<postgresql_name >*預留位置和 hello 的使用者名稱 *\<admin_username >*預留位置. hello 的伺服器名稱會做為 PostgreSQL 端點的一部分 (`https://<postgresql_name>.postgres.database.azure.com`)，因此 hello 名稱需要 toobe 唯一在 Azure 中的所有伺服器。 hello 使用者名稱為 hello 初始資料庫管理員使用者帳戶。 您必須提示的 toopick 這位使用者的密碼。

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

PostgreSQL 伺服器 hello Azure 資料庫建立時，hello Azure CLI 顯示資訊的類似 toohello 下列範例：

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

### <a name="create-a-firewall-rule-for-hello-azure-database-for-postgresql-server"></a>建立 PostgreSQL 伺服器 hello Azure 資料庫的防火牆規則

執行的所有 IP 位址中的下列 Azure CLI 命令 tooallow access toohello 資料庫 hello。

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

hello Azure CLI 使用下列範例的輸出類似 toohello 確認 hello 防火牆規則的建立：

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

## <a name="connect-your-python-flask-application-toohello-database"></a>連接您的 Python 酒瓶應用程式 toohello 資料庫

在此步驟中，您可以連接您所建立的 PostgreSQL 伺服器您 Python 酒瓶範例應用程式 toohello Azure 資料庫。

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a>建立空的資料庫並設定新的資料庫應用程式使用者

存取 tooa 單一資料庫只能建立資料庫使用者。 您將使用這些認證 tooavoid，給予 hello 應用程式的完整存取 toohello 伺服器。

連接 toohello 資料庫 （系統提示您輸入系統管理員密碼）。

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

從 PostgreSQL CLI hello 建立 hello 資料庫和使用者。

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```

型別*\q* tooexit hello PostgreSQL 用戶端。

### <a name="test-hello-application-locally-against-hello-azure-postgresql-database"></a>測試本機 hello hello Azure PostgreSQL 資料庫應用程式 

返回現在 toohello*應用程式*hello 資料夾複製 Github 儲存機制，您可以藉由更新 hello 資料庫環境變數執行 hello Python 酒瓶應用程式。

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

完全載入 hello 應用程式時，您會看到下列訊息類似 toohello:

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

瀏覽 toohttp://127.0.0.1:5000 瀏覽器中。 按一下 [註冊!] 並且建立測試註冊。 您現在要在 Azure 中，撰寫資料 toohello 資料庫。

![在本機執行的 Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-hello-application-from-a-docker-container"></a>執行 Docker 容器中的 hello 應用程式

建置 hello Docker 容器映像。

```bash
cd ..
docker build -t flask-postgresql-sample .
```

Docker 顯示確認訊息已成功建立 it hello 容器。

```bash
Successfully built 7548f983a36b
```

新增資料庫環境變數 tooan 環境變數檔*db.env*。 hello 應用程式會連接 toohello PostgreSQL 生產資料庫，在 Azure 中。

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

執行從 hello Docker 容器中的 hello 應用程式。 hello 下列命令會指定 hello 環境變數的檔案並將對應 hello 預設酒瓶連接埠 5000 toolocal port 5000。

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

hello 輸出是您稍早所看到的類似 toowhat。 不過，hello 初始資料庫移轉不需要再 toobe 執行，因此已略過。

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C tooquit)
```

hello 資料庫已經包含您先前建立的 hello 註冊。

![以 Docker 容器為基礎在本機執行的 Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-hello-docker-container-tooa-container-registry"></a>上傳 hello Docker 容器 tooa 容器登錄中

在此步驟中，您上傳 hello Docker 容器 tooa 容器登錄中。 您將會使用 Azure Container Registry，但是您也可以使用 Docker Hub 等其他熱門的項目。

### <a name="create-an-azure-container-registry"></a>建立 Azure Container Registry

在下列命令 toocreate 容器登錄中的 hello 取代 *\<registry_name >*與您所選擇的 Azure 容器登錄名稱。

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

輸出
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

### <a name="retrieve-hello-registry-credentials-for-pushing-and-pulling-docker-images"></a>擷取推送及提取的 Docker 映像的 hello 登錄憑證

tooshow 登錄認證，可先讓系統管理員模式。

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

您會看到兩個密碼。 請記下 hello 使用者名稱和 hello 第一個密碼。

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

### <a name="upload-your-docker-container-tooazure-container-registry"></a>上傳您的 Docker 容器 tooAzure 容器登錄中

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-hello-docker-python-flask-application-tooazure"></a>部署 hello Docker Python 酒瓶應用程式 tooAzure

在此步驟中，您可以部署您 Docker 容器基礎 Python 酒瓶應用程式 tooAzure 應用程式服務。

### <a name="create-an-app-service-plan"></a>建立應用程式服務方案

建立應用程式服務方案以 hello [az 應用程式服務方案建立](/cli/azure/appservice/plan#create)命令。 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

hello 下列範例會建立名為 Linux 為基礎的應用程式服務方案*myAppServicePlan*使用 hello S1 定價層：

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

建立 hello 應用程式服務方案時，hello Azure CLI 顯示資訊的類似 toohello 下列範例：

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

### <a name="create-a-web-app"></a>建立 Web 應用程式

建立 web 應用程式在 hello *myAppServicePlan*應用程式服務方案以 hello [az webapp 建立](/cli/azure/webapp#create)命令。 

hello web 應用程式可讓您裝載空間 toodeploy 您的程式碼和為您提供 URL tooview hello 部署應用程式。 使用 toocreate hello web 應用程式。 

在 hello 下列命令，將取代 hello  *\<app_name >*具有唯一的應用程式名稱的預留位置。 這個名稱是 hello hello web 應用程式，預設 URL 的一部分，因此 hello 名稱需要 toobe 唯一跨 Azure App Service 中的所有應用程式。 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Hello web 應用程式建立後，hello Azure CLI 顯示資訊的類似 toohello 下列範例： 

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

### <a name="configure-hello-database-environment-variables"></a>設定 hello 資料庫環境變數

稍早在 hello 教學課程中，您可以定義環境變數 tooconnect tooyour PostgreSQL 資料庫。

在應用程式服務中，您設定環境變數為_應用程式設定_使用 hello [az webapp config appsettings 組](/cli/azure/webapp/config#set)命令。 

hello 下列範例指定 hello 資料庫連接詳細資料為應用程式設定。 它也會使用 hello*連接埠*變數 toomap PORT 5000 從您在連接埠 80 上的 Docker 容器 tooreceive HTTP 流量。

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a>設定 Docker 容器部署 

AppService 會自動下載及執行 Docker 容器。

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

每當您更新 hello Docker 容器，或變更 hello 設定，重新啟動 hello 應用程式。 重新啟動，可確保套用所有的設定，以及從 hello 登錄提取 hello 最新的容器。

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-toohello-azure-web-app"></a>瀏覽 toohello Azure web 應用程式 

瀏覽使用網頁瀏覽器 toohello 部署 web 應用程式。 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> hello web 應用程式需要較長的 tooload 因為 hello 容器具有 toobe 下載及啟動 hello 容器組態變更之後。

您會看到先前註冊的來賓 hello 上一個步驟中儲存 toohello Azure 生產資料庫。

![以 Docker 容器為基礎在本機執行的 Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

**恭喜！** 您要在 Azure App Service 中執行以 Docker 容器為基礎的 Python Flask 應用程式。

## <a name="update-data-model-and-redeploy"></a>更新資料模型並重新部署

在此步驟中，您可以加入 hello 數目出席者 tooeach 事件註冊藉由更新 hello 客體模型。

簽出 hello *0.2 移轉*版本與 hello 下列 git 命令：

```bash
git checkout tags/0.2-migration
```

此版本中已經完成 hello 必要的變更 tooviews、 控制站，以及模型。 它也會包含透過 alembic (`flask db migrate`) 產生的資料庫移轉。 您可以看到所有透過 hello 下列 git 命令進行的變更：

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a>本機測試您的變更

下列命令 tootest hello 您的變更在本機執行所執行的 hello 酒瓶伺服器。

Mac / Linux：
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

瀏覽在您的瀏覽器 tooview hello 變更 toohttp://127.0.0.1:5000。 建立測試註冊。

![以 Docker 容器為基礎在本機執行的 Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-tooazure"></a>發行變更 tooAzure

建置 hello 新的 docker 映像，直接將其推 toohello 容器登錄中，然後重新啟動 hello 應用程式。

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

瀏覽 tooyour Azure web 應用程式，然後再試 hello 新功能。 建立另一個事件註冊。

```bash 
http://<app_name>.azurewebsites.net 
```

![Azure App Service 中的 Docker Python Flask 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a>管理您的 Azure Web 應用程式

移 toohello [Azure 入口網站](https://portal.azure.com)toosee hello web 應用程式所建立。

從 hello 左窗格中，按一下 **應用程式服務**，然後按一下 hello Azure web 應用程式名稱。

![入口網站瀏覽 tooAzure web 應用程式](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

根據預設，hello 入口網站會顯示 web 應用程式的**概觀**頁面。 此頁面可讓您檢視應用程式的執行方式。 您也可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。 在左邊 hello 頁面 hello hello 索引標籤會顯示 hello 不同的組態頁面，您可以開啟。

![Azure 入口網站中的 App Service 頁面](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a>後續步驟

前進 toohello 下一個教學課程 toolearn toomap 自訂的 DNS 名稱 tooyour web 應用程式的方式。

> [!div class="nextstepaction"] 
> [將現有自訂 DNS 名稱 tooAzure Web 應用程式的對應](app-service-web-tutorial-custom-domain.md)

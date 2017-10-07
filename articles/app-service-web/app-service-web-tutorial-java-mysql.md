---
title: "aaaBuild Java 和 MySQL web 應用程式在 Azure 中"
description: "深入了解如何 tooget Java 應用程式連接 Azure 應用程式服務中使用的 toohello Azure MySQL 資料庫服務。"
services: app-service\web
documentationcenter: Java
author: bbenz
manager: jeffsand
editor: jasonwhowell
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: tutorial
ms.date: 05/22/2017
ms.author: bbenz
ms.custom: mvc
ms.openlocfilehash: 0820ee9c2b7bf8fcaa22287c27a7ab848a1c4927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a>在 Azure 中建置 Java 和 MySQL Web 應用程式

本教學課程會示範如何 toocreate Java web 應用程式在 Azure 中的，並將它連接 tooa MySQL 資料庫。 當您完成後，在 [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 中執行的 [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) 會有一個儲存資料的 [Spring Boot](https://projects.spring.io/spring-boot/)應用程式。

![在 Azure Appservice 中執行的 Java 應用程式](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 在 Azure 中建立 MySQL 資料庫
> * 連接範例應用程式 toohello 資料庫
> * 部署 hello 應用程式 tooAzure
> * 更新和重新部署 hello 應用程式
> * 來自 Azure 的串流診斷記錄
> * 監視 hello hello Azure 入口網站中的應用程式


## <a name="prerequisites"></a>必要條件

1. [下載並安裝 Git](https://git-scm.com/)
1. [下載並安裝 Java 7 JDK hello 或更新版本](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [下載、安裝並啟動 MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="prepare-local-mysql"></a>準備本機 MySQL 

在此步驟中，您建立本機 MySQL 伺服器的使用中的資料庫測試 hello 應用程式中本機電腦上。

### <a name="connect-toomysql-server"></a>TooMySQL 伺服器連接

在終端機視窗中，連接 tooyour 本機 MySQL 伺服器。 您可以使用這個終端機視窗 toorun hello 的所有命令，在本教學課程。

```bash
mysql -u root -p
```

如果系統提示您輸入密碼，輸入 hello 密碼 hello`root`帳戶。 如果您不記得您的根帳號密碼，請參閱[MySQL： 如何 tooReset hello 根密碼](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html)。

如果您的命令執行成功，表示您的 MySQL 伺服器已經在執行中。 如果沒有，請確定您的本機 MySQL 伺服器已啟動由下列 hello [MySQL 安裝後步驟](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html)。

### <a name="create-a-database"></a>建立資料庫 

在 hello`mysql`提示字元中，建立資料庫和資料表的 hello 待辦項目。

```sql
CREATE DATABASE tododb;
```

輸入 `quit` 即可結束您的伺服器連線。

```sql
quit
```

## <a name="create-and-run-hello-sample-app"></a>建立和執行 hello 範例應用程式 

在此步驟中，您可以複製範例 Spring 開機應用程式、 設定它 toouse hello 本機 MySQL 資料庫，和您的電腦上執行。 

### <a name="clone-hello-sample"></a>複製 hello 範例

在 hello 終端機視窗，瀏覽 tooa 工作目錄和複製 hello 範例儲存機制。 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-hello-app-toouse-hello-mysql-database"></a>設定 hello 應用程式 toouse hello MySQL 資料庫

更新 hello`spring.datasource.password`和值*spring-boot-mysql-todo/src/main/resources/application.properties* hello 與相同的根密碼使用 tooopen hello MySQL 提示：

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-hello-sample"></a>建置並執行 hello 範例

建置和執行使用 hello Maven 包裝函式包含在 hello 儲存機制中的 hello 範例：

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

開啟您的瀏覽器 toohttp://localhost:8080 toosee hello 範例中的動作。 當您新增工作 toohello 清單中，使用下列 SQL 命令中 hello MySQL 提示 tooview hello 資料儲存在 MySQL hello。

```SQL
use testdb;
select * from todo_item;
```

停止 hello 應用程式，請按`Ctrl` + `C` hello 終端機中。 

## <a name="create-an-azure-mysql-database"></a>建立 Azure MySQL 資料庫

在此步驟中，您會建立[Azure 資料庫的 MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md)執行個體使用 hello [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli)。 您設定 hello 範例應用程式 toouse 這個資料庫稍後在 hello 教學課程。

在終端機視窗 toocreate hello 資源使用 hello Azure CLI 2.0 需要 toohost Java 應用程式在 Azure 應用程式服務。 登入 Azure 訂用帳戶以 hello tooyour [az 登入](/cli/azure/#login)命令，並遵循螢幕上指示 hello。 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a>建立資源群組

建立[資源群組](../azure-resource-manager/resource-group-overview.md)以 hello [az 群組建立](/cli/azure/group#create)命令。 Azure 資源群組是一個邏輯容器，可在其中部署與管理例如 Web 應用程式、資料庫和儲存體帳戶等相關資源。 

hello 下列範例會建立資源群組 hello 北歐區域中：

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

toosee hello 可能的值可用於`--location`，使用 hello [az appservice 列出位置](/cli/azure/appservice#list-locations)命令。

### <a name="create-a-mysql-server"></a>建立 MySQL 伺服器

Azure 資料庫中建立伺服器的 MySQL （預覽） 以 hello [az mysql 伺服器建立](/cli/azure/mysql/server#create)命令。    
取代您自己唯一 MySQL 伺服器的名稱，您會看到 hello`<mysql_server_name>`預留位置。 這個名稱是 MySQL 伺服器的主機名稱的一部分`<mysql_server_name>.mysql.database.azure.com`，所以它需要 toobe 全域唯一。 另外，請將 `<admin_user>` 和 `<admin_password>` 替代成您自己的值。

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

建立 hello MySQL 伺服器時，hello Azure CLI 顯示資訊的類似 toohello 下列範例：

```json
{
  "administratorLogin": "admin_user",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mysql_server_name.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/mysql_server_name",
  "location": "northeurope",
  "name": "mysql_server_name",
  "resourceGroup": "mysqlJavaResourceGroup",
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-server-firewall"></a>設定伺服器防火牆

建立防火牆規則的 MySQL 伺服器 tooallow 用戶端連接使用 hello [az mysql 伺服器防火牆規則建立](/cli/azure/mysql/server/firewall-rule#create)命令。 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> 適用於 MySQL 的 Azure 資料庫 (預覽) 目前尚未自動啟用來自 Azure 服務的連線。 在 Azure 中的 IP 位址動態指派，它是較佳的 tooenable 所有 IP 位址現在。 因為 hello 服務會繼續其預覽，將會啟用更好的方法，來保護您的資料庫。

## <a name="configure-hello-azure-mysql-database"></a>設定 hello Azure MySQL 資料庫

在 hello 終端機視窗，在您的電腦上，連接在 Azure 中的 toohello MySQL 伺服器。 使用您先前指定的 hello 值`<admin_user>`和`<mysql_server_name>`。

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a>建立資料庫 

在 hello`mysql`提示字元中，建立資料庫和資料表的 hello 待辦項目。

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a>建立具有權限的使用者

建立資料庫使用者，將它所有的權限在 hello`tododb`資料庫。 Hello 預留位置取代`<Javaapp_user>`和`<Javaapp_password>`以您自己唯一的應用程式的名稱。

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* too'<Javaapp_user>';
```

輸入 `quit` 即可結束您的伺服器連線。

```sql
quit
```

## <a name="deploy-hello-sample-tooazure-app-service"></a>部署 hello 範例 tooAzure 應用程式服務

建立 Azure App Service 方案以 hello**免費**定價層使用 hello [az 應用程式服務方案建立](/cli/azure/appservice/plan#create)CLI 命令。 hello 應用程式服務方案會定義 hello 使用的實體資源 toohost 您的應用程式。 指派 tooan 應用程式服務方案的所有應用程式共用這些資源，讓您 toosave 成本裝載多個應用程式時。 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

準備 hello 計劃時，Azure CLI 顯示類似的 hello 輸出 toohello 下列範例：

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a>建立 Azure Web 應用程式

 使用 hello [az webapp 建立](/cli/azure/appservice/web#create)CLI 命令 toocreate web 應用程式定義在 hello`myAppServicePlan`應用程式服務方案。 hello web 應用程式定義您的應用程式提供 URL tooaccess，並設定數個選項 toodeploy 程式碼 tooAzure。 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

替代 hello`<app_name>`預留位置自己唯一的應用程式的名稱。 這個唯一名稱是 hello hello web 應用程式的預設網域名稱的一部分，因此 hello 名稱需要 toobe 唯一跨 Azure 中的所有應用程式。 公開 tooyour 使用者之前，您可以將自訂網域名稱項目 toohello web 應用程式的對應。

Hello web 應用程式定義就緒時，hello Azure CLI 顯示資訊的類似 toohello 下列範例： 

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

### <a name="configure-java"></a>設定 Java 

設定您的應用程式需要具有 hello 的 hello Java 執行階段組態[az appservice web 組態更新](/cli/azure/appservice/web/config#update)命令。

hello 下列命令會設定 hello web 應用程式 toorun 上最近的 Java 8 JDK 和[Apache Tomcat](http://tomcat.apache.org/) 8.0。

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-hello-app-toouse-hello-azure-sql-database"></a>設定 hello 應用程式 toouse hello Azure SQL database

在執行之前 hello 範例應用程式，設定 hello web 應用程式 toouse hello Azure MySQL 資料庫上您在 Azure 中建立的應用程式設定。 這些屬性會公開的 toohello web 應用程式做為環境變數，並覆寫 hello hello application.properties 內 hello 封裝的 web 應用程式中設定的值。 

設定使用的應用程式設定[az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) hello CLI 中：

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL="jdbc:mysql://<mysql_server_name>.mysql.database.azure.com:3306/tododb?verifyServerCertificate=true&useSSL=true&requireSSL=false" \
    --resource-group myResourceGroup \
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_USERNAME=Javaapp_user@mysql_server_name  \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL=Javaapp_password \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

### <a name="get-ftp-deployment-credentials"></a>取得 FTP 部署認證 
您可以部署應用程式 tooAzure 應用程式服務，以各種方式，包括 FTP、 本機 Git、 GitHub、 Visual Studio Team Services 和 BitBucket。 例如，FTP toodeploy hello。在您本機電腦 tooAzure 應用程式服務上建置的 WAR 檔案。

toodetermine 以及認證中的 ftp 命令 toohello Web 應用程式，使用沿著 toopass [az appservice web 清單-發行-設定檔的部署](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles)命令： 

```azurecli-interactive
az webapp deployment list-publishing-profiles \ 
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" \ 
    --output json
```

```JSON
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-069.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "app_name\\$app_name"
  }
]
```

### <a name="upload-hello-app-using-ftp"></a>使用 FTP 的 hello 應用程式上傳

使用您喜愛的 FTP 工具 toodeploy hello。WAR 檔案 toohello */site/wwwroot/webapps*取自 hello hello 伺服器位址上的資料夾`URL`hello 先前命令中的欄位。 移除 hello 現有預設 （根） 的應用程式目錄，並取代現有 ROOT.war hello 與 hello。內建的 hello hello 教學課程中先前的 WAR 檔案。

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected toowaws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-hello-web-app"></a>測試 hello web 應用程式

瀏覽過`http://<app_name>.azurewebsites.net/`並加入一些工作 toohello 清單。 

![在 Azure Appservice 中執行的 Java 應用程式](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

**恭喜！** 您正在 Azure App Service 中執行資料驅動的 Java 應用程式。

## <a name="update-hello-app-and-redeploy"></a>更新 hello 應用程式後再重新部署

更新 hello 應用程式 tooinclude 額外的資料行中的哪些日期 hello 項目建立 hello todo 清單。 Spring 開機會隨著 hello 資料模型變更為您更新 hello 資料庫結構描述處理而不會變更現有的資料庫記錄。

1. 在您的本機系統上開啟*src/main/java/com/example/fabrikam/TodoItem.java*並加入 hello 下列匯入 toohello 類別：   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. 新增`String`屬性`timeCreated`太*src/main/java/com/example/fabrikam/TodoItem.java*，初始化在物件建立時間戳記。 加入新的 hello 的 getter/setter`timeCreated`您正在編輯這個檔案的屬性。

    ```java
    private String name;
    private boolean complete;
    private String timeCreated;
    ...

    public TodoItem(String category, String name) {
       this.category = category;
       this.name = name;
       this.complete = false;
       this.timeCreated = new SimpleDateFormat("MMMM dd, YYYY").format(Calendar.getInstance().getTime());
    }
    ...
    public void setTimeCreated(String timeCreated) {
       this.timeCreated = timeCreated;
    }

    public String getTimeCreated() {
        return timeCreated;
    }
    ```

3. 更新*src/main/java/com/example/fabrikam/TodoDemoController.java* hello 中的第一行`updateTodo`方法 tooset hello 時間戳記：

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. 新增 hello Thymeleaf 範本中的 hello 新欄位的支援。 更新*src/main/resources/templates/index.html*具有代表 hello 時間戳記，每個資料表資料列中的 hello 時間戳記，新欄位 toodisplay hello 值的新資料表標頭。

    ```html
    <th>Name</th>
    <th>Category</th>
    <th>Time Created</th>
    <th>Complete</th>
    ...
    <td th:text="${item.category}">item_category</td><input type="hidden" th:field="*{todoList[__${i.index}__].category}"/>
    <td th:text="${item.timeCreated}">item_time_created</td><input type="hidden" th:field="*{todoList[__${i.index}__].timeCreated}"/>
    <td><input type="checkbox" th:checked="${item.complete} == true" th:field="*{todoList[__${i.index}__].complete}"/></td>
    ```

5. 重建 hello 應用程式：

    ```bash
    mvnw clean package 
    ```

6. FTP hello 更新。WAR 之前，移除現有的 hello*站台/wwwroot/webapps/ROOT*目錄和*ROOT.war*，然後上傳更新的 hello。為 ROOT.war WAR 檔案。 

當您重新整理 hello 應用程式，**建立時間**資料行現在會顯示。 當您新增新的工作時，hello 應用程式將會自動填入 hello 時間戳記。 您現有的工作會保留不變，而且使用 hello 應用程式，即使 hello 基礎資料模型已變更。 

![搭配新資料行的 Java 應用程式更新](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a>資料流診斷記錄 

雖然 Azure App Service 中，執行您的 Java 應用程式，您可以取得 hello 主控台記錄檔經由管道輸出直接 tooyour 終端機。 這樣一來，您可以取得 hello 相同的診斷訊息 toohelp 您偵錯應用程式錯誤。

資料流中，使用 hello toostart 記錄[az webapp 記錄結尾](/cli/azure/appservice/web/log#tail)命令。

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a>管理您的 Azure Web 應用程式

移 toohello Azure 入口網站 toosee hello web 應用程式所建立。

toodo，登入太[https://portal.azure.com](https://portal.azure.com)。

從 hello 左窗格中，按一下  **App Service**，然後按一下 hello Azure web 應用程式名稱。

![入口網站瀏覽 tooAzure web 應用程式](./media/app-service-web-tutorial-java-mysql/access-portal.png)

根據預設，您的 web 應用程式 刀鋒視窗會顯示 hello**概觀**頁面。 此頁面可讓您檢視應用程式的執行方式。 您也可以在這裡執行像是停止、啟動、重新啟動及刪除等管理工作。 hello hello 左邊算起的 hello 刀鋒視窗上的索引標籤會顯示 hello 不同的組態頁面，您可以開啟。

![Azure 入口網站中的 App Service 刀鋒視窗](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

在 [hello] 刀鋒視窗中的這些索引標籤會顯示 hello 許多很棒的功能，您可以加入 tooyour web 應用程式。 下列清單中的 hello 可讓您幾個 hello 可能性：
* 對應自訂 DNS 名稱
* 繫結自訂 SSL 憑證
* 設定連續部署
* 相應增加和相應放大
* 新增使用者驗證

## <a name="clean-up-resources"></a>清除資源

如果您不需要這些資源進行其他教學課程 (請參閱[後續步驟](#next))，您可以執行下列命令的 hello 刪除： 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a>後續步驟

> [!div class="checklist"]
> * 在 Azure 中建立 MySQL 資料庫
> * 連接範例 Java 應用程式 toohello MySQL
> * 部署 hello 應用程式 tooAzure
> * 更新和重新部署 hello 應用程式
> * 來自 Azure 的串流診斷記錄
> * 管理 hello hello Azure 入口網站中的應用程式

前進 toohello 下一個教學課程 toolearn toomap 自訂 DNS toohello 的應用程式的命名。

> [!div class="nextstepaction"] 
> [將現有自訂 DNS 名稱 tooAzure Web 應用程式的對應](app-service-web-tutorial-custom-domain.md)

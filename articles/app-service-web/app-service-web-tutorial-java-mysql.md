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
# <a name="build-a-java-and-mysql-web-app-in-azure"></a><span data-ttu-id="d469c-103">在 Azure 中建置 Java 和 MySQL Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d469c-103">Build a Java and MySQL web app in Azure</span></span>

<span data-ttu-id="d469c-104">本教學課程會示範如何 toocreate Java web 應用程式在 Azure 中的，並將它連接 tooa MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d469c-104">This tutorial shows you how toocreate a Java web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="d469c-105">當您完成後，在 [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 中執行的 [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) 會有一個儲存資料的 [Spring Boot](https://projects.spring.io/spring-boot/)應用程式。</span><span class="sxs-lookup"><span data-stu-id="d469c-105">When you are finished, you will have a [Spring Boot](https://projects.spring.io/spring-boot/) application storing data in [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) running on [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span></span>

![在 Azure Appservice 中執行的 Java 應用程式](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="d469c-107">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="d469c-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d469c-108">在 Azure 中建立 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="d469c-108">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="d469c-109">連接範例應用程式 toohello 資料庫</span><span class="sxs-lookup"><span data-stu-id="d469c-109">Connect a sample app toohello database</span></span>
> * <span data-ttu-id="d469c-110">部署 hello 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="d469c-110">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="d469c-111">更新和重新部署 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="d469c-111">Update and redeploy hello app</span></span>
> * <span data-ttu-id="d469c-112">來自 Azure 的串流診斷記錄</span><span class="sxs-lookup"><span data-stu-id="d469c-112">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="d469c-113">監視 hello hello Azure 入口網站中的應用程式</span><span class="sxs-lookup"><span data-stu-id="d469c-113">Monitor hello app in hello Azure portal</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d469c-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="d469c-114">Prerequisites</span></span>

1. [<span data-ttu-id="d469c-115">下載並安裝 Git</span><span class="sxs-lookup"><span data-stu-id="d469c-115">Download and install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="d469c-116">下載並安裝 Java 7 JDK hello 或更新版本</span><span class="sxs-lookup"><span data-stu-id="d469c-116">Download and install hello Java 7 JDK or above</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [<span data-ttu-id="d469c-117">下載、安裝並啟動 MySQL</span><span class="sxs-lookup"><span data-stu-id="d469c-117">Download, install, and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d469c-118">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d469c-118">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d469c-119">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="d469c-119">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d469c-120">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="d469c-120">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-local-mysql"></a><span data-ttu-id="d469c-121">準備本機 MySQL</span><span class="sxs-lookup"><span data-stu-id="d469c-121">Prepare local MySQL</span></span> 

<span data-ttu-id="d469c-122">在此步驟中，您建立本機 MySQL 伺服器的使用中的資料庫測試 hello 應用程式中本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="d469c-122">In this step, you create a database in a local MySQL server for use in testing hello app locally on your machine.</span></span>

### <a name="connect-toomysql-server"></a><span data-ttu-id="d469c-123">TooMySQL 伺服器連接</span><span class="sxs-lookup"><span data-stu-id="d469c-123">Connect tooMySQL server</span></span>

<span data-ttu-id="d469c-124">在終端機視窗中，連接 tooyour 本機 MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d469c-124">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="d469c-125">您可以使用這個終端機視窗 toorun hello 的所有命令，在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="d469c-125">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="d469c-126">如果系統提示您輸入密碼，輸入 hello 密碼 hello`root`帳戶。</span><span class="sxs-lookup"><span data-stu-id="d469c-126">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="d469c-127">如果您不記得您的根帳號密碼，請參閱[MySQL： 如何 tooReset hello 根密碼](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html)。</span><span class="sxs-lookup"><span data-stu-id="d469c-127">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="d469c-128">如果您的命令執行成功，表示您的 MySQL 伺服器已經在執行中。</span><span class="sxs-lookup"><span data-stu-id="d469c-128">If your command runs successfully, then your MySQL server is already running.</span></span> <span data-ttu-id="d469c-129">如果沒有，請確定您的本機 MySQL 伺服器已啟動由下列 hello [MySQL 安裝後步驟](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html)。</span><span class="sxs-lookup"><span data-stu-id="d469c-129">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database"></a><span data-ttu-id="d469c-130">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="d469c-130">Create a database</span></span> 

<span data-ttu-id="d469c-131">在 hello`mysql`提示字元中，建立資料庫和資料表的 hello 待辦項目。</span><span class="sxs-lookup"><span data-stu-id="d469c-131">In hello `mysql` prompt, create a database and a table for hello to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

<span data-ttu-id="d469c-132">輸入 `quit` 即可結束您的伺服器連線。</span><span class="sxs-lookup"><span data-stu-id="d469c-132">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="create-and-run-hello-sample-app"></a><span data-ttu-id="d469c-133">建立和執行 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="d469c-133">Create and run hello sample app</span></span> 

<span data-ttu-id="d469c-134">在此步驟中，您可以複製範例 Spring 開機應用程式、 設定它 toouse hello 本機 MySQL 資料庫，和您的電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="d469c-134">In this step, you clone sample Spring boot app, configure it toouse hello local MySQL database, and run it on your computer.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="d469c-135">複製 hello 範例</span><span class="sxs-lookup"><span data-stu-id="d469c-135">Clone hello sample</span></span>

<span data-ttu-id="d469c-136">在 hello 終端機視窗，瀏覽 tooa 工作目錄和複製 hello 範例儲存機制。</span><span class="sxs-lookup"><span data-stu-id="d469c-136">In hello terminal window, navigate tooa working directory and clone hello sample repository.</span></span> 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-hello-app-toouse-hello-mysql-database"></a><span data-ttu-id="d469c-137">設定 hello 應用程式 toouse hello MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="d469c-137">Configure hello app toouse hello MySQL database</span></span>

<span data-ttu-id="d469c-138">更新 hello`spring.datasource.password`和值*spring-boot-mysql-todo/src/main/resources/application.properties* hello 與相同的根密碼使用 tooopen hello MySQL 提示：</span><span class="sxs-lookup"><span data-stu-id="d469c-138">Update hello `spring.datasource.password` and  value in *spring-boot-mysql-todo/src/main/resources/application.properties* with hello same root password used tooopen hello MySQL prompt:</span></span>

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-hello-sample"></a><span data-ttu-id="d469c-139">建置並執行 hello 範例</span><span class="sxs-lookup"><span data-stu-id="d469c-139">Build and run hello sample</span></span>

<span data-ttu-id="d469c-140">建置和執行使用 hello Maven 包裝函式包含在 hello 儲存機制中的 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="d469c-140">Build and run hello sample using hello Maven wrapper included in hello repo:</span></span>

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

<span data-ttu-id="d469c-141">開啟您的瀏覽器 toohttp://localhost:8080 toosee hello 範例中的動作。</span><span class="sxs-lookup"><span data-stu-id="d469c-141">Open your browser toohttp://localhost:8080 toosee in hello sample in action.</span></span> <span data-ttu-id="d469c-142">當您新增工作 toohello 清單中，使用下列 SQL 命令中 hello MySQL 提示 tooview hello 資料儲存在 MySQL hello。</span><span class="sxs-lookup"><span data-stu-id="d469c-142">As you add tasks toohello list,  use hello following SQL commands in hello MySQL prompt tooview hello data stored in MySQL.</span></span>

```SQL
use testdb;
select * from todo_item;
```

<span data-ttu-id="d469c-143">停止 hello 應用程式，請按`Ctrl` + `C` hello 終端機中。</span><span class="sxs-lookup"><span data-stu-id="d469c-143">Stop hello application by hitting `Ctrl`+`C` in hello terminal.</span></span> 

## <a name="create-an-azure-mysql-database"></a><span data-ttu-id="d469c-144">建立 Azure MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="d469c-144">Create an Azure MySQL database</span></span>

<span data-ttu-id="d469c-145">在此步驟中，您會建立[Azure 資料庫的 MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md)執行個體使用 hello [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="d469c-145">In this step, you create an [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance using hello [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="d469c-146">您設定 hello 範例應用程式 toouse 這個資料庫稍後在 hello 教學課程。</span><span class="sxs-lookup"><span data-stu-id="d469c-146">You configure hello sample application toouse this database later on in hello tutorial.</span></span>

<span data-ttu-id="d469c-147">在終端機視窗 toocreate hello 資源使用 hello Azure CLI 2.0 需要 toohost Java 應用程式在 Azure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="d469c-147">Use hello Azure CLI 2.0 in a terminal window toocreate hello resources needed toohost your Java application in Azure appservice.</span></span> <span data-ttu-id="d469c-148">登入 Azure 訂用帳戶以 hello tooyour [az 登入](/cli/azure/#login)命令，並遵循螢幕上指示 hello。</span><span class="sxs-lookup"><span data-stu-id="d469c-148">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="d469c-149">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="d469c-149">Create a resource group</span></span>

<span data-ttu-id="d469c-150">建立[資源群組](../azure-resource-manager/resource-group-overview.md)以 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="d469c-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d469c-151">Azure 資源群組是一個邏輯容器，可在其中部署與管理例如 Web 應用程式、資料庫和儲存體帳戶等相關資源。</span><span class="sxs-lookup"><span data-stu-id="d469c-151">An Azure resource group is a logical container where related resources like web apps, databases, and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="d469c-152">hello 下列範例會建立資源群組 hello 北歐區域中：</span><span class="sxs-lookup"><span data-stu-id="d469c-152">hello following example creates a resource group in hello North Europe region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

<span data-ttu-id="d469c-153">toosee hello 可能的值可用於`--location`，使用 hello [az appservice 列出位置](/cli/azure/appservice#list-locations)命令。</span><span class="sxs-lookup"><span data-stu-id="d469c-153">toosee hello possible values you can use for `--location`, use hello [az appservice list-locations](/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-a-mysql-server"></a><span data-ttu-id="d469c-154">建立 MySQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="d469c-154">Create a MySQL server</span></span>

<span data-ttu-id="d469c-155">Azure 資料庫中建立伺服器的 MySQL （預覽） 以 hello [az mysql 伺服器建立](/cli/azure/mysql/server#create)命令。</span><span class="sxs-lookup"><span data-stu-id="d469c-155">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>    
<span data-ttu-id="d469c-156">取代您自己唯一 MySQL 伺服器的名稱，您會看到 hello`<mysql_server_name>`預留位置。</span><span class="sxs-lookup"><span data-stu-id="d469c-156">Substitute your own unique MySQL server name where you see hello `<mysql_server_name>` placeholder.</span></span> <span data-ttu-id="d469c-157">這個名稱是 MySQL 伺服器的主機名稱的一部分`<mysql_server_name>.mysql.database.azure.com`，所以它需要 toobe 全域唯一。</span><span class="sxs-lookup"><span data-stu-id="d469c-157">This name is part of your MySQL server's hostname, `<mysql_server_name>.mysql.database.azure.com`, so it needs toobe globally unique.</span></span> <span data-ttu-id="d469c-158">另外，請將 `<admin_user>` 和 `<admin_password>` 替代成您自己的值。</span><span class="sxs-lookup"><span data-stu-id="d469c-158">Also substitute `<admin_user>` and `<admin_password>` with your own values.</span></span>

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

<span data-ttu-id="d469c-159">建立 hello MySQL 伺服器時，hello Azure CLI 顯示資訊的類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="d469c-159">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="configure-server-firewall"></a><span data-ttu-id="d469c-160">設定伺服器防火牆</span><span class="sxs-lookup"><span data-stu-id="d469c-160">Configure server firewall</span></span>

<span data-ttu-id="d469c-161">建立防火牆規則的 MySQL 伺服器 tooallow 用戶端連接使用 hello [az mysql 伺服器防火牆規則建立](/cli/azure/mysql/server/firewall-rule#create)命令。</span><span class="sxs-lookup"><span data-stu-id="d469c-161">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="d469c-162">適用於 MySQL 的 Azure 資料庫 (預覽) 目前尚未自動啟用來自 Azure 服務的連線。</span><span class="sxs-lookup"><span data-stu-id="d469c-162">Azure Database for MySQL (Preview) does not currently automatically enable connections from Azure services.</span></span> <span data-ttu-id="d469c-163">在 Azure 中的 IP 位址動態指派，它是較佳的 tooenable 所有 IP 位址現在。</span><span class="sxs-lookup"><span data-stu-id="d469c-163">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses for now.</span></span> <span data-ttu-id="d469c-164">因為 hello 服務會繼續其預覽，將會啟用更好的方法，來保護您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d469c-164">As hello service continues its preview, better methods for securing your database will be enabled.</span></span>

## <a name="configure-hello-azure-mysql-database"></a><span data-ttu-id="d469c-165">設定 hello Azure MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="d469c-165">Configure hello Azure MySQL database</span></span>

<span data-ttu-id="d469c-166">在 hello 終端機視窗，在您的電腦上，連接在 Azure 中的 toohello MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d469c-166">In hello terminal window on your computer, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="d469c-167">使用您先前指定的 hello 值`<admin_user>`和`<mysql_server_name>`。</span><span class="sxs-lookup"><span data-stu-id="d469c-167">Use hello value you specified previously for `<admin_user>` and `<mysql_server_name>`.</span></span>

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a><span data-ttu-id="d469c-168">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="d469c-168">Create a database</span></span> 

<span data-ttu-id="d469c-169">在 hello`mysql`提示字元中，建立資料庫和資料表的 hello 待辦項目。</span><span class="sxs-lookup"><span data-stu-id="d469c-169">In hello `mysql` prompt, create a database and a table for hello to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="d469c-170">建立具有權限的使用者</span><span class="sxs-lookup"><span data-stu-id="d469c-170">Create a user with permissions</span></span>

<span data-ttu-id="d469c-171">建立資料庫使用者，將它所有的權限在 hello`tododb`資料庫。</span><span class="sxs-lookup"><span data-stu-id="d469c-171">Create a database user and give it all privileges in hello `tododb` database.</span></span> <span data-ttu-id="d469c-172">Hello 預留位置取代`<Javaapp_user>`和`<Javaapp_password>`以您自己唯一的應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="d469c-172">Replace hello placeholders `<Javaapp_user>` and `<Javaapp_password>` with your own unique app name.</span></span>

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* too'<Javaapp_user>';
```

<span data-ttu-id="d469c-173">輸入 `quit` 即可結束您的伺服器連線。</span><span class="sxs-lookup"><span data-stu-id="d469c-173">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="deploy-hello-sample-tooazure-app-service"></a><span data-ttu-id="d469c-174">部署 hello 範例 tooAzure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="d469c-174">Deploy hello sample tooAzure App Service</span></span>

<span data-ttu-id="d469c-175">建立 Azure App Service 方案以 hello**免費**定價層使用 hello [az 應用程式服務方案建立](/cli/azure/appservice/plan#create)CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="d469c-175">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="d469c-176">hello 應用程式服務方案會定義 hello 使用的實體資源 toohost 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d469c-176">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="d469c-177">指派 tooan 應用程式服務方案的所有應用程式共用這些資源，讓您 toosave 成本裝載多個應用程式時。</span><span class="sxs-lookup"><span data-stu-id="d469c-177">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="d469c-178">準備 hello 計劃時，Azure CLI 顯示類似的 hello 輸出 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="d469c-178">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="d469c-179">建立 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d469c-179">Create an Azure Web app</span></span>

 <span data-ttu-id="d469c-180">使用 hello [az webapp 建立](/cli/azure/appservice/web#create)CLI 命令 toocreate web 應用程式定義在 hello`myAppServicePlan`應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="d469c-180">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="d469c-181">hello web 應用程式定義您的應用程式提供 URL tooaccess，並設定數個選項 toodeploy 程式碼 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="d469c-181">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="d469c-182">替代 hello`<app_name>`預留位置自己唯一的應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="d469c-182">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="d469c-183">這個唯一名稱是 hello hello web 應用程式的預設網域名稱的一部分，因此 hello 名稱需要 toobe 唯一跨 Azure 中的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="d469c-183">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="d469c-184">公開 tooyour 使用者之前，您可以將自訂網域名稱項目 toohello web 應用程式的對應。</span><span class="sxs-lookup"><span data-stu-id="d469c-184">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="d469c-185">Hello web 應用程式定義就緒時，hello Azure CLI 顯示資訊的類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="d469c-185">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="d469c-186">設定 Java</span><span class="sxs-lookup"><span data-stu-id="d469c-186">Configure Java</span></span> 

<span data-ttu-id="d469c-187">設定您的應用程式需要具有 hello 的 hello Java 執行階段組態[az appservice web 組態更新](/cli/azure/appservice/web/config#update)命令。</span><span class="sxs-lookup"><span data-stu-id="d469c-187">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="d469c-188">hello 下列命令會設定 hello web 應用程式 toorun 上最近的 Java 8 JDK 和[Apache Tomcat](http://tomcat.apache.org/) 8.0。</span><span class="sxs-lookup"><span data-stu-id="d469c-188">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-hello-app-toouse-hello-azure-sql-database"></a><span data-ttu-id="d469c-189">設定 hello 應用程式 toouse hello Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="d469c-189">Configure hello app toouse hello Azure SQL database</span></span>

<span data-ttu-id="d469c-190">在執行之前 hello 範例應用程式，設定 hello web 應用程式 toouse hello Azure MySQL 資料庫上您在 Azure 中建立的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="d469c-190">Before running hello sample app, set application settings on hello web app toouse hello Azure MySQL database you created in Azure.</span></span> <span data-ttu-id="d469c-191">這些屬性會公開的 toohello web 應用程式做為環境變數，並覆寫 hello hello application.properties 內 hello 封裝的 web 應用程式中設定的值。</span><span class="sxs-lookup"><span data-stu-id="d469c-191">These properties are exposed toohello web application as environment variables and override hello values set in hello application.properties inside hello packaged web app.</span></span> 

<span data-ttu-id="d469c-192">設定使用的應用程式設定[az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) hello CLI 中：</span><span class="sxs-lookup"><span data-stu-id="d469c-192">Set application settings using [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in hello CLI:</span></span>

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

### <a name="get-ftp-deployment-credentials"></a><span data-ttu-id="d469c-193">取得 FTP 部署認證</span><span class="sxs-lookup"><span data-stu-id="d469c-193">Get FTP deployment credentials</span></span> 
<span data-ttu-id="d469c-194">您可以部署應用程式 tooAzure 應用程式服務，以各種方式，包括 FTP、 本機 Git、 GitHub、 Visual Studio Team Services 和 BitBucket。</span><span class="sxs-lookup"><span data-stu-id="d469c-194">You can deploy your application tooAzure appservice in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="d469c-195">例如，FTP toodeploy hello。在您本機電腦 tooAzure 應用程式服務上建置的 WAR 檔案。</span><span class="sxs-lookup"><span data-stu-id="d469c-195">For this example, FTP toodeploy hello .WAR file built previously on your local machine tooAzure App Service.</span></span>

<span data-ttu-id="d469c-196">toodetermine 以及認證中的 ftp 命令 toohello Web 應用程式，使用沿著 toopass [az appservice web 清單-發行-設定檔的部署](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles)命令：</span><span class="sxs-lookup"><span data-stu-id="d469c-196">toodetermine what credentials toopass along in an ftp command toohello Web App, Use [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) command:</span></span> 

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

### <a name="upload-hello-app-using-ftp"></a><span data-ttu-id="d469c-197">使用 FTP 的 hello 應用程式上傳</span><span class="sxs-lookup"><span data-stu-id="d469c-197">Upload hello app using FTP</span></span>

<span data-ttu-id="d469c-198">使用您喜愛的 FTP 工具 toodeploy hello。WAR 檔案 toohello */site/wwwroot/webapps*取自 hello hello 伺服器位址上的資料夾`URL`hello 先前命令中的欄位。</span><span class="sxs-lookup"><span data-stu-id="d469c-198">Use your favorite FTP tool toodeploy hello .WAR file toohello */site/wwwroot/webapps* folder on hello server address taken from hello `URL` field in hello previous command.</span></span> <span data-ttu-id="d469c-199">移除 hello 現有預設 （根） 的應用程式目錄，並取代現有 ROOT.war hello 與 hello。內建的 hello hello 教學課程中先前的 WAR 檔案。</span><span class="sxs-lookup"><span data-stu-id="d469c-199">Remove hello existing default (ROOT) application directory and replace hello existing ROOT.war with hello .WAR file built in hello earlier in hello tutorial.</span></span>

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

### <a name="test-hello-web-app"></a><span data-ttu-id="d469c-200">測試 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d469c-200">Test hello web app</span></span>

<span data-ttu-id="d469c-201">瀏覽過`http://<app_name>.azurewebsites.net/`並加入一些工作 toohello 清單。</span><span class="sxs-lookup"><span data-stu-id="d469c-201">Browse too`http://<app_name>.azurewebsites.net/` and add a few tasks toohello list.</span></span> 

![在 Azure Appservice 中執行的 Java 應用程式](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="d469c-203">**恭喜！**</span><span class="sxs-lookup"><span data-stu-id="d469c-203">**Congratulations!**</span></span> <span data-ttu-id="d469c-204">您正在 Azure App Service 中執行資料驅動的 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d469c-204">You're running a data-driven Java app in Azure App Service.</span></span>

## <a name="update-hello-app-and-redeploy"></a><span data-ttu-id="d469c-205">更新 hello 應用程式後再重新部署</span><span class="sxs-lookup"><span data-stu-id="d469c-205">Update hello app and redeploy</span></span>

<span data-ttu-id="d469c-206">更新 hello 應用程式 tooinclude 額外的資料行中的哪些日期 hello 項目建立 hello todo 清單。</span><span class="sxs-lookup"><span data-stu-id="d469c-206">Update hello application tooinclude an additional column in hello todo list for what day hello item was created.</span></span> <span data-ttu-id="d469c-207">Spring 開機會隨著 hello 資料模型變更為您更新 hello 資料庫結構描述處理而不會變更現有的資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="d469c-207">Spring Boot handles updating hello database schema for you as hello data model changes without altering your existing database records.</span></span>

1. <span data-ttu-id="d469c-208">在您的本機系統上開啟*src/main/java/com/example/fabrikam/TodoItem.java*並加入 hello 下列匯入 toohello 類別：</span><span class="sxs-lookup"><span data-stu-id="d469c-208">On your local system, open up *src/main/java/com/example/fabrikam/TodoItem.java* and add hello following imports toohello class:</span></span>   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. <span data-ttu-id="d469c-209">新增`String`屬性`timeCreated`太*src/main/java/com/example/fabrikam/TodoItem.java*，初始化在物件建立時間戳記。</span><span class="sxs-lookup"><span data-stu-id="d469c-209">Add a `String` property `timeCreated` too*src/main/java/com/example/fabrikam/TodoItem.java*, initializing it with a timestamp at object creation.</span></span> <span data-ttu-id="d469c-210">加入新的 hello 的 getter/setter`timeCreated`您正在編輯這個檔案的屬性。</span><span class="sxs-lookup"><span data-stu-id="d469c-210">Add getters/setters for hello new `timeCreated` property while you are editing this file.</span></span>

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

3. <span data-ttu-id="d469c-211">更新*src/main/java/com/example/fabrikam/TodoDemoController.java* hello 中的第一行`updateTodo`方法 tooset hello 時間戳記：</span><span class="sxs-lookup"><span data-stu-id="d469c-211">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* with a line in hello `updateTodo` method tooset hello timestamp:</span></span>

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. <span data-ttu-id="d469c-212">新增 hello Thymeleaf 範本中的 hello 新欄位的支援。</span><span class="sxs-lookup"><span data-stu-id="d469c-212">Add support for hello new field in hello Thymeleaf template.</span></span> <span data-ttu-id="d469c-213">更新*src/main/resources/templates/index.html*具有代表 hello 時間戳記，每個資料表資料列中的 hello 時間戳記，新欄位 toodisplay hello 值的新資料表標頭。</span><span class="sxs-lookup"><span data-stu-id="d469c-213">Update *src/main/resources/templates/index.html* with a new table header for hello timestamp, and a new field toodisplay hello value of hello timestamp in each table data row.</span></span>

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

5. <span data-ttu-id="d469c-214">重建 hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="d469c-214">Rebuild hello application:</span></span>

    ```bash
    mvnw clean package 
    ```

6. <span data-ttu-id="d469c-215">FTP hello 更新。WAR 之前，移除現有的 hello*站台/wwwroot/webapps/ROOT*目錄和*ROOT.war*，然後上傳更新的 hello。為 ROOT.war WAR 檔案。</span><span class="sxs-lookup"><span data-stu-id="d469c-215">FTP hello updated .WAR as before, removing hello existing *site/wwwroot/webapps/ROOT* directory and *ROOT.war*, then uploading hello updated .WAR file as ROOT.war.</span></span> 

<span data-ttu-id="d469c-216">當您重新整理 hello 應用程式，**建立時間**資料行現在會顯示。</span><span class="sxs-lookup"><span data-stu-id="d469c-216">When you refresh hello app, a **Time Created** column is now visible.</span></span> <span data-ttu-id="d469c-217">當您新增新的工作時，hello 應用程式將會自動填入 hello 時間戳記。</span><span class="sxs-lookup"><span data-stu-id="d469c-217">When you add a new task, hello app will populate hello timestamp automatically.</span></span> <span data-ttu-id="d469c-218">您現有的工作會保留不變，而且使用 hello 應用程式，即使 hello 基礎資料模型已變更。</span><span class="sxs-lookup"><span data-stu-id="d469c-218">Your existing tasks remain unchanged and work with hello app even though hello underlying data model has changed.</span></span> 

![搭配新資料行的 Java 應用程式更新](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a><span data-ttu-id="d469c-220">資料流診斷記錄</span><span class="sxs-lookup"><span data-stu-id="d469c-220">Stream diagnostic logs</span></span> 

<span data-ttu-id="d469c-221">雖然 Azure App Service 中，執行您的 Java 應用程式，您可以取得 hello 主控台記錄檔經由管道輸出直接 tooyour 終端機。</span><span class="sxs-lookup"><span data-stu-id="d469c-221">While your Java application runs in Azure App Service, you can get hello console logs piped directly tooyour terminal.</span></span> <span data-ttu-id="d469c-222">這樣一來，您可以取得 hello 相同的診斷訊息 toohelp 您偵錯應用程式錯誤。</span><span class="sxs-lookup"><span data-stu-id="d469c-222">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="d469c-223">資料流中，使用 hello toostart 記錄[az webapp 記錄結尾](/cli/azure/appservice/web/log#tail)命令。</span><span class="sxs-lookup"><span data-stu-id="d469c-223">toostart log streaming, use hello [az webapp log tail](/cli/azure/appservice/web/log#tail) command.</span></span>

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="d469c-224">管理您的 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d469c-224">Manage your Azure web app</span></span>

<span data-ttu-id="d469c-225">移 toohello Azure 入口網站 toosee hello web 應用程式所建立。</span><span class="sxs-lookup"><span data-stu-id="d469c-225">Go toohello Azure portal toosee hello web app you created.</span></span>

<span data-ttu-id="d469c-226">toodo，登入太[https://portal.azure.com](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d469c-226">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="d469c-227">從 hello 左窗格中，按一下  **App Service**，然後按一下 hello Azure web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="d469c-227">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![入口網站瀏覽 tooAzure web 應用程式](./media/app-service-web-tutorial-java-mysql/access-portal.png)

<span data-ttu-id="d469c-229">根據預設，您的 web 應用程式 刀鋒視窗會顯示 hello**概觀**頁面。</span><span class="sxs-lookup"><span data-stu-id="d469c-229">By default, your web app's blade shows hello **Overview** page.</span></span> <span data-ttu-id="d469c-230">此頁面可讓您檢視應用程式的執行方式。</span><span class="sxs-lookup"><span data-stu-id="d469c-230">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="d469c-231">您也可以在這裡執行像是停止、啟動、重新啟動及刪除等管理工作。</span><span class="sxs-lookup"><span data-stu-id="d469c-231">Here, you can also perform management tasks like stop, start, restart, and delete.</span></span> <span data-ttu-id="d469c-232">hello hello 左邊算起的 hello 刀鋒視窗上的索引標籤會顯示 hello 不同的組態頁面，您可以開啟。</span><span class="sxs-lookup"><span data-stu-id="d469c-232">hello tabs on hello left side of hello blade show hello different configuration pages you can open.</span></span>

![Azure 入口網站中的 App Service 刀鋒視窗](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

<span data-ttu-id="d469c-234">在 [hello] 刀鋒視窗中的這些索引標籤會顯示 hello 許多很棒的功能，您可以加入 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d469c-234">These tabs in hello blade show hello many great features you can add tooyour web app.</span></span> <span data-ttu-id="d469c-235">下列清單中的 hello 可讓您幾個 hello 可能性：</span><span class="sxs-lookup"><span data-stu-id="d469c-235">hello following list gives you just a few of hello possibilities:</span></span>
* <span data-ttu-id="d469c-236">對應自訂 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="d469c-236">Map a custom DNS name</span></span>
* <span data-ttu-id="d469c-237">繫結自訂 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="d469c-237">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="d469c-238">設定連續部署</span><span class="sxs-lookup"><span data-stu-id="d469c-238">Configure continuous deployment</span></span>
* <span data-ttu-id="d469c-239">相應增加和相應放大</span><span class="sxs-lookup"><span data-stu-id="d469c-239">Scale up and out</span></span>
* <span data-ttu-id="d469c-240">新增使用者驗證</span><span class="sxs-lookup"><span data-stu-id="d469c-240">Add user authentication</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="d469c-241">清除資源</span><span class="sxs-lookup"><span data-stu-id="d469c-241">Clean up resources</span></span>

<span data-ttu-id="d469c-242">如果您不需要這些資源進行其他教學課程 (請參閱[後續步驟](#next))，您可以執行下列命令的 hello 刪除：</span><span class="sxs-lookup"><span data-stu-id="d469c-242">If you don't need these resources for another tutorial (see [Next steps](#next)), you can delete them by running hello following command:</span></span> 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="d469c-243">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d469c-243">Next steps</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d469c-244">在 Azure 中建立 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="d469c-244">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="d469c-245">連接範例 Java 應用程式 toohello MySQL</span><span class="sxs-lookup"><span data-stu-id="d469c-245">Connect a sample Java app toohello MySQL</span></span>
> * <span data-ttu-id="d469c-246">部署 hello 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="d469c-246">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="d469c-247">更新和重新部署 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="d469c-247">Update and redeploy hello app</span></span>
> * <span data-ttu-id="d469c-248">來自 Azure 的串流診斷記錄</span><span class="sxs-lookup"><span data-stu-id="d469c-248">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="d469c-249">管理 hello hello Azure 入口網站中的應用程式</span><span class="sxs-lookup"><span data-stu-id="d469c-249">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="d469c-250">前進 toohello 下一個教學課程 toolearn toomap 自訂 DNS toohello 的應用程式的命名。</span><span class="sxs-lookup"><span data-stu-id="d469c-250">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="d469c-251">將現有自訂 DNS 名稱 tooAzure Web 應用程式的對應</span><span class="sxs-lookup"><span data-stu-id="d469c-251">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)

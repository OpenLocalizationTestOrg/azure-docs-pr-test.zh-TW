---
title: "在 Azure 中建置 Java 和 MySQL Web 應用程式"
description: "了解如何取得連線至在 Azure Appservice 中運作的 Azure MySQL 資料庫服務之 Java 應用程式。"
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
ms.openlocfilehash: eb2d59939c4e4486bb14bb143a4a18f9bc1478e1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a><span data-ttu-id="4215e-103">在 Azure 中建置 Java 和 MySQL Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4215e-103">Build a Java and MySQL web app in Azure</span></span>

<span data-ttu-id="4215e-104">本教學課程示範如何在 Azure 中建立 Java Web 應用程式，並將它連線到 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4215e-104">This tutorial shows you how to create a Java web app in Azure and connect it to a MySQL database.</span></span> <span data-ttu-id="4215e-105">當您完成後，在 [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 中執行的 [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) 會有一個儲存資料的 [Spring Boot](https://projects.spring.io/spring-boot/)應用程式。</span><span class="sxs-lookup"><span data-stu-id="4215e-105">When you are finished, you will have a [Spring Boot](https://projects.spring.io/spring-boot/) application storing data in [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) running on [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span></span>

![在 Azure Appservice 中執行的 Java 應用程式](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="4215e-107">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="4215e-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4215e-108">在 Azure 中建立 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="4215e-108">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="4215e-109">將範例應用程式連線至資料庫</span><span class="sxs-lookup"><span data-stu-id="4215e-109">Connect a sample app to the database</span></span>
> * <span data-ttu-id="4215e-110">將應用程式部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="4215e-110">Deploy the app to Azure</span></span>
> * <span data-ttu-id="4215e-111">更新和重新部署應用程式</span><span class="sxs-lookup"><span data-stu-id="4215e-111">Update and redeploy the app</span></span>
> * <span data-ttu-id="4215e-112">來自 Azure 的串流診斷記錄</span><span class="sxs-lookup"><span data-stu-id="4215e-112">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="4215e-113">在 Azure 入口網站中監視應用程式</span><span class="sxs-lookup"><span data-stu-id="4215e-113">Monitor the app in the Azure portal</span></span>


## <a name="prerequisites"></a><span data-ttu-id="4215e-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="4215e-114">Prerequisites</span></span>

1. [<span data-ttu-id="4215e-115">下載並安裝 Git</span><span class="sxs-lookup"><span data-stu-id="4215e-115">Download and install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="4215e-116">下載並安裝 Java 7 JDK 或更高版本</span><span class="sxs-lookup"><span data-stu-id="4215e-116">Download and install the Java 7 JDK or above</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [<span data-ttu-id="4215e-117">下載、安裝並啟動 MySQL</span><span class="sxs-lookup"><span data-stu-id="4215e-117">Download, install, and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4215e-118">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="4215e-118">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4215e-119">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="4215e-119">Run `az --version` to find the version.</span></span> <span data-ttu-id="4215e-120">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="4215e-120">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-local-mysql"></a><span data-ttu-id="4215e-121">準備本機 MySQL</span><span class="sxs-lookup"><span data-stu-id="4215e-121">Prepare local MySQL</span></span> 

<span data-ttu-id="4215e-122">在此步驟中，您可以在本機 MySQL 伺服器中建立資料庫，供您在本機電腦上測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="4215e-122">In this step, you create a database in a local MySQL server for use in testing the app locally on your machine.</span></span>

### <a name="connect-to-mysql-server"></a><span data-ttu-id="4215e-123">連線至 MySQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="4215e-123">Connect to MySQL server</span></span>

<span data-ttu-id="4215e-124">在終端機視窗中，連線到您的本機 MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4215e-124">In a terminal window, connect to your local MySQL server.</span></span> <span data-ttu-id="4215e-125">您可使用這個終端機視窗來執行本教學課程中的所有命令。</span><span class="sxs-lookup"><span data-stu-id="4215e-125">You can use this terminal window to run all the commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="4215e-126">如果系統提示您輸入密碼，請輸入 `root` 帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="4215e-126">If you're prompted for a password, enter the password for the `root` account.</span></span> <span data-ttu-id="4215e-127">如果您不記得根帳戶密碼，請參閱 [MySQL︰如何重設根密碼](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html)。</span><span class="sxs-lookup"><span data-stu-id="4215e-127">If you don't remember your root account password, see [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="4215e-128">如果您的命令執行成功，表示您的 MySQL 伺服器已經在執行中。</span><span class="sxs-lookup"><span data-stu-id="4215e-128">If your command runs successfully, then your MySQL server is already running.</span></span> <span data-ttu-id="4215e-129">如果沒有，請遵循 [MySQL 後續安裝步驟](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html)，確定您已啟動本機 MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4215e-129">If not, make sure that your local MySQL server is started by following the [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database"></a><span data-ttu-id="4215e-130">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="4215e-130">Create a database</span></span> 

<span data-ttu-id="4215e-131">在 `mysql` 提示中，建立待辦事項的資料庫和資料表。</span><span class="sxs-lookup"><span data-stu-id="4215e-131">In the `mysql` prompt, create a database and a table for the to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

<span data-ttu-id="4215e-132">輸入 `quit` 即可結束您的伺服器連線。</span><span class="sxs-lookup"><span data-stu-id="4215e-132">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="create-and-run-the-sample-app"></a><span data-ttu-id="4215e-133">建立和執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="4215e-133">Create and run the sample app</span></span> 

<span data-ttu-id="4215e-134">在此步驟中，您可以複製範例 Spring Boot 應用程式、將它設定為使用本機 MySQL 資料庫，並在您的電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="4215e-134">In this step, you clone sample Spring boot app, configure it to use the local MySQL database, and run it on your computer.</span></span> 

### <a name="clone-the-sample"></a><span data-ttu-id="4215e-135">複製範例</span><span class="sxs-lookup"><span data-stu-id="4215e-135">Clone the sample</span></span>

<span data-ttu-id="4215e-136">在終端機視窗中，瀏覽到工作目錄並複製範例存放庫。</span><span class="sxs-lookup"><span data-stu-id="4215e-136">In the terminal window, navigate to a working directory and clone the sample repository.</span></span> 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-the-app-to-use-the-mysql-database"></a><span data-ttu-id="4215e-137">將應用程式設定為使用 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="4215e-137">Configure the app to use the MySQL database</span></span>

<span data-ttu-id="4215e-138">更新 `spring.datasource.password` 以及 *spring-boot-mysql-todo/src/main/resources/application.properties* 中的值，以用來開啟 MySQL 命令提示字元相同的根密碼加以取代：</span><span class="sxs-lookup"><span data-stu-id="4215e-138">Update the `spring.datasource.password` and  value in *spring-boot-mysql-todo/src/main/resources/application.properties* with the same root password used to open the MySQL prompt:</span></span>

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-the-sample"></a><span data-ttu-id="4215e-139">建置並執行範例</span><span class="sxs-lookup"><span data-stu-id="4215e-139">Build and run the sample</span></span>

<span data-ttu-id="4215e-140">使用存放庫中包含的 Maven 包裝函式建置並執行範例：</span><span class="sxs-lookup"><span data-stu-id="4215e-140">Build and run the sample using the Maven wrapper included in the repo:</span></span>

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

<span data-ttu-id="4215e-141">開啟瀏覽器至 http://localhost:8080 ，查看範例如何運作。</span><span class="sxs-lookup"><span data-stu-id="4215e-141">Open your browser to http://localhost:8080 to see in the sample in action.</span></span> <span data-ttu-id="4215e-142">在清單中新增工作時，請使用 MySQL 命令提示字元中的下列 SQL 命令，以檢視 MySQL 中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="4215e-142">As you add tasks to the list,  use the following SQL commands in the MySQL prompt to view the data stored in MySQL.</span></span>

```SQL
use testdb;
select * from todo_item;
```

<span data-ttu-id="4215e-143">按下終端機中的 `Ctrl`+`C` 以停止應用程式。</span><span class="sxs-lookup"><span data-stu-id="4215e-143">Stop the application by hitting `Ctrl`+`C` in the terminal.</span></span> 

## <a name="create-an-azure-mysql-database"></a><span data-ttu-id="4215e-144">建立 Azure MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="4215e-144">Create an Azure MySQL database</span></span>

<span data-ttu-id="4215e-145">在此步驟中，您會使用 [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) 建立 [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) 執行個體。</span><span class="sxs-lookup"><span data-stu-id="4215e-145">In this step, you create an [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance using the [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="4215e-146">也會設定範例應用程式，以便稍後可以在教學課程中使用此資料庫。</span><span class="sxs-lookup"><span data-stu-id="4215e-146">You configure the sample application to use this database later on in the tutorial.</span></span>

<span data-ttu-id="4215e-147">在終端機視窗中使用 Azure CLI 2.0，來建立在 Azure Appservice 中裝載 Java 應用程式所需的資源。</span><span class="sxs-lookup"><span data-stu-id="4215e-147">Use the Azure CLI 2.0 in a terminal window to create the resources needed to host your Java application in Azure appservice.</span></span> <span data-ttu-id="4215e-148">使用 [az login](/cli/azure/#login) 命令登入 Azure 訂用帳戶並遵循畫面上的指示。</span><span class="sxs-lookup"><span data-stu-id="4215e-148">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="4215e-149">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="4215e-149">Create a resource group</span></span>

<span data-ttu-id="4215e-150">使用 [az group create](/cli/azure/group#create) 命令來建立[資源群組](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4215e-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="4215e-151">Azure 資源群組是一個邏輯容器，可在其中部署與管理例如 Web 應用程式、資料庫和儲存體帳戶等相關資源。</span><span class="sxs-lookup"><span data-stu-id="4215e-151">An Azure resource group is a logical container where related resources like web apps, databases, and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="4215e-152">下列範例會在北歐區域中建立一個資源群組：</span><span class="sxs-lookup"><span data-stu-id="4215e-152">The following example creates a resource group in the North Europe region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

<span data-ttu-id="4215e-153">若要查看可用於 `--location` 的可能值，請使用 [az appservice list-locations](/cli/azure/appservice#list-locations) 命令。</span><span class="sxs-lookup"><span data-stu-id="4215e-153">To see the possible values you can use for `--location`, use the [az appservice list-locations](/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-a-mysql-server"></a><span data-ttu-id="4215e-154">建立 MySQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="4215e-154">Create a MySQL server</span></span>

<span data-ttu-id="4215e-155">使用 [az mysql server create](/cli/azure/mysql/server#create) 命令，在適用於 MySQL 的 Azure 資料庫 (預覽) 中建立伺服器。</span><span class="sxs-lookup"><span data-stu-id="4215e-155">Create a server in Azure Database for MySQL (Preview) with the [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>    
<span data-ttu-id="4215e-156">在您看見 `<mysql_server_name>` 預留位置的地方，替代成您自己的唯一 MySQL 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="4215e-156">Substitute your own unique MySQL server name where you see the `<mysql_server_name>` placeholder.</span></span> <span data-ttu-id="4215e-157">這個名稱是 MySQL 伺服器主機名稱 `<mysql_server_name>.mysql.database.azure.com` 的一部分，因此它必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="4215e-157">This name is part of your MySQL server's hostname, `<mysql_server_name>.mysql.database.azure.com`, so it needs to be globally unique.</span></span> <span data-ttu-id="4215e-158">另外，請將 `<admin_user>` 和 `<admin_password>` 替代成您自己的值。</span><span class="sxs-lookup"><span data-stu-id="4215e-158">Also substitute `<admin_user>` and `<admin_password>` with your own values.</span></span>

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

<span data-ttu-id="4215e-159">建立 MySQL 伺服器後，Azure CLI 會顯示類似下列範例的資訊：</span><span class="sxs-lookup"><span data-stu-id="4215e-159">When the MySQL server is created, the Azure CLI shows information similar to the following example:</span></span>

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

### <a name="configure-server-firewall"></a><span data-ttu-id="4215e-160">設定伺服器防火牆</span><span class="sxs-lookup"><span data-stu-id="4215e-160">Configure server firewall</span></span>

<span data-ttu-id="4215e-161">使用 [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) 命令，建立 MySQL 伺服器的防火牆規則來允許用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="4215e-161">Create a firewall rule for your MySQL server to allow client connections by using the [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="4215e-162">適用於 MySQL 的 Azure 資料庫 (預覽) 目前尚未自動啟用來自 Azure 服務的連線。</span><span class="sxs-lookup"><span data-stu-id="4215e-162">Azure Database for MySQL (Preview) does not currently automatically enable connections from Azure services.</span></span> <span data-ttu-id="4215e-163">隨著您將 Azure 中的 IP 位址進行動態指派，目前最好是啟用所有的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4215e-163">As IP addresses in Azure are dynamically assigned, it is better to enable all IP addresses for now.</span></span> <span data-ttu-id="4215e-164">因為服務仍為預覽中，很快就會透過更好的方法，來保護您的資料庫安全。</span><span class="sxs-lookup"><span data-stu-id="4215e-164">As the service continues its preview, better methods for securing your database will be enabled.</span></span>

## <a name="configure-the-azure-mysql-database"></a><span data-ttu-id="4215e-165">設定 Azure MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="4215e-165">Configure the Azure MySQL database</span></span>

<span data-ttu-id="4215e-166">在電腦的終端機視窗中，連線至 Azure 中的 MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4215e-166">In the terminal window on your computer, connect to the MySQL server in Azure.</span></span> <span data-ttu-id="4215e-167">針對 `<admin_user>` 和 `<mysql_server_name>`，使用您先前指定的值。</span><span class="sxs-lookup"><span data-stu-id="4215e-167">Use the value you specified previously for `<admin_user>` and `<mysql_server_name>`.</span></span>

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a><span data-ttu-id="4215e-168">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="4215e-168">Create a database</span></span> 

<span data-ttu-id="4215e-169">在 `mysql` 提示中，建立待辦事項的資料庫和資料表。</span><span class="sxs-lookup"><span data-stu-id="4215e-169">In the `mysql` prompt, create a database and a table for the to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="4215e-170">建立具有權限的使用者</span><span class="sxs-lookup"><span data-stu-id="4215e-170">Create a user with permissions</span></span>

<span data-ttu-id="4215e-171">建立資料庫使用者，並將 `tododb` 資料庫中所有的權限授權給它。</span><span class="sxs-lookup"><span data-stu-id="4215e-171">Create a database user and give it all privileges in the `tododb` database.</span></span> <span data-ttu-id="4215e-172">將 `<Javaapp_user>` 和 `<Javaapp_password>` 預留位置取代您自己的唯一應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="4215e-172">Replace the placeholders `<Javaapp_user>` and `<Javaapp_password>` with your own unique app name.</span></span>

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* TO '<Javaapp_user>';
```

<span data-ttu-id="4215e-173">輸入 `quit` 即可結束您的伺服器連線。</span><span class="sxs-lookup"><span data-stu-id="4215e-173">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="deploy-the-sample-to-azure-app-service"></a><span data-ttu-id="4215e-174">將範例部署到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4215e-174">Deploy the sample to Azure App Service</span></span>

<span data-ttu-id="4215e-175">使用 [az appservice plan create](/cli/azure/appservice/plan#create) CLI 命令，建立搭配**免費**定價層的 Azure App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="4215e-175">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="4215e-176">Appservice 方案會定義用來託管應用程式的實體資源。</span><span class="sxs-lookup"><span data-stu-id="4215e-176">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="4215e-177">所有指派給 Appservice 方案的應用程式都會共用這些資源，從而讓您節省託管多個應用程式的成本。</span><span class="sxs-lookup"><span data-stu-id="4215e-177">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="4215e-178">方案準備妥當時，Azure CLI 會顯示類似下列範例的輸出：</span><span class="sxs-lookup"><span data-stu-id="4215e-178">When the plan is ready, the Azure CLI shows similar output to the following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="4215e-179">建立 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4215e-179">Create an Azure Web app</span></span>

 <span data-ttu-id="4215e-180">使用 [az webapp create](/cli/azure/appservice/web#create) CLI 命令，在 `myAppServicePlan` App Service 方案中建立 Web 應用程式定義。</span><span class="sxs-lookup"><span data-stu-id="4215e-180">Use the [az webapp create](/cli/azure/appservice/web#create) CLI command to create a web app definition in the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="4215e-181">Web 應用程式定義會提供一個 URL 以存取您的應用程式，並設定數個選項將您的程式碼部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="4215e-181">The web app definition provides a URL to access your application with and configures several options to deploy your code to Azure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="4215e-182">使用您自己的唯一應用程式名稱來取代 `<app_name>` 預留位置。</span><span class="sxs-lookup"><span data-stu-id="4215e-182">Substitute the `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="4215e-183">這個唯一名稱會是 Web 應用程式預設網域名稱的一部分，因此，這個名稱在 Azure 的所有應用程式中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="4215e-183">This unique name is part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="4215e-184">您可以先將自訂的網域名稱項目對應至 Web 應用程式，再將它公開給使用者。</span><span class="sxs-lookup"><span data-stu-id="4215e-184">You can map a custom domain name entry to the web app before you expose it to your users.</span></span>

<span data-ttu-id="4215e-185">Web 應用程式定義備妥之後，Azure CLI 會顯示類似下列範例的資訊：</span><span class="sxs-lookup"><span data-stu-id="4215e-185">When the web app definition is ready, the Azure CLI shows information similar to the following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="4215e-186">設定 Java</span><span class="sxs-lookup"><span data-stu-id="4215e-186">Configure Java</span></span> 

<span data-ttu-id="4215e-187">使用 [az appservice web config update](/cli/azure/appservice/web/config#update) 命令來設定您的應用程式需要的 Java 執行階段組態。</span><span class="sxs-lookup"><span data-stu-id="4215e-187">Set up the Java runtime configuration that your app needs with the  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="4215e-188">下列命令會將 Web 應用程式設定為在最新的 Java 8 JDK 和 [Apache Tomcat](http://tomcat.apache.org/) 8.0 上執行。</span><span class="sxs-lookup"><span data-stu-id="4215e-188">The following command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-the-app-to-use-the-azure-sql-database"></a><span data-ttu-id="4215e-189">將應用程式設定為使用 Azure SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="4215e-189">Configure the app to use the Azure SQL database</span></span>

<span data-ttu-id="4215e-190">請先將 Web 應用程式上的應用程式設定設為使用在 Azure 中建立的 Azure MySQL 資料庫，再執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="4215e-190">Before running the sample app, set application settings on the web app to use the Azure MySQL database you created in Azure.</span></span> <span data-ttu-id="4215e-191">這些屬性會公開至 Web 應用程式作為環境變數，並覆寫已封裝之 Web 應用程式中 application.properties 所設定的值。</span><span class="sxs-lookup"><span data-stu-id="4215e-191">These properties are exposed to the web application as environment variables and override the values set in the application.properties inside the packaged web app.</span></span> 

<span data-ttu-id="4215e-192">使用 CLI 中的 [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) 來設定應用程式設定：</span><span class="sxs-lookup"><span data-stu-id="4215e-192">Set application settings using [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in the CLI:</span></span>

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

### <a name="get-ftp-deployment-credentials"></a><span data-ttu-id="4215e-193">取得 FTP 部署認證</span><span class="sxs-lookup"><span data-stu-id="4215e-193">Get FTP deployment credentials</span></span> 
<span data-ttu-id="4215e-194">您可以使用各種方式來將應用程式部署至 Azure Appservice，包括 FTP、本機 Git、GitHub、Visual Studio Team Services 和 BitBucket。</span><span class="sxs-lookup"><span data-stu-id="4215e-194">You can deploy your application to Azure appservice in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="4215e-195">在此範例中，使用 FTP 將先前在您本機電腦上建置的 .WAR 檔案部署至 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="4215e-195">For this example, FTP to deploy the .WAR file built previously on your local machine to Azure App Service.</span></span>

<span data-ttu-id="4215e-196">若要判斷要在 ftp 命令中將哪些認證傳遞至 Web 應用程式，請使用 [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) 命令︰</span><span class="sxs-lookup"><span data-stu-id="4215e-196">To determine what credentials to pass along in an ftp command to the Web App, Use [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) command:</span></span> 

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

### <a name="upload-the-app-using-ftp"></a><span data-ttu-id="4215e-197">使用 FTP 上傳應用程式</span><span class="sxs-lookup"><span data-stu-id="4215e-197">Upload the app using FTP</span></span>

<span data-ttu-id="4215e-198">使用您喜愛的 FTP 工具將 .WAR 檔案部署至 */site/wwwroot/webapps* 資料夾；，該資料夾位於先前命令中 `URL` 欄位的伺服器位址上。</span><span class="sxs-lookup"><span data-stu-id="4215e-198">Use your favorite FTP tool to deploy the .WAR file to the */site/wwwroot/webapps* folder on the server address taken from the `URL` field in the previous command.</span></span> <span data-ttu-id="4215e-199">移除現有的預設 (ROOT) 應用程式目錄，並以先前在教學課程中建置的 .WAR 檔案取代現有的 ROOT.war。</span><span class="sxs-lookup"><span data-stu-id="4215e-199">Remove the existing default (ROOT) application directory and replace the existing ROOT.war with the .WAR file built in the earlier in the tutorial.</span></span>

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected to waws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-the-web-app"></a><span data-ttu-id="4215e-200">測試 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4215e-200">Test the web app</span></span>

<span data-ttu-id="4215e-201">瀏覽至 `http://<app_name>.azurewebsites.net/` 並將幾項工作新增至清單。</span><span class="sxs-lookup"><span data-stu-id="4215e-201">Browse to `http://<app_name>.azurewebsites.net/` and add a few tasks to the list.</span></span> 

![在 Azure Appservice 中執行的 Java 應用程式](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="4215e-203">**恭喜！**</span><span class="sxs-lookup"><span data-stu-id="4215e-203">**Congratulations!**</span></span> <span data-ttu-id="4215e-204">您正在 Azure App Service 中執行資料驅動的 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4215e-204">You're running a data-driven Java app in Azure App Service.</span></span>

## <a name="update-the-app-and-redeploy"></a><span data-ttu-id="4215e-205">更新應用程式並重新部署</span><span class="sxs-lookup"><span data-stu-id="4215e-205">Update the app and redeploy</span></span>

<span data-ttu-id="4215e-206">更新應用程式，以在待辦事項清單中包含額外的資料行，用來記錄項目的建立日期。</span><span class="sxs-lookup"><span data-stu-id="4215e-206">Update the application to include an additional column in the todo list for what day the item was created.</span></span> <span data-ttu-id="4215e-207">Spring Boot 會在資料模型變更時為您更新資料庫結構描述，無需更改您現有的資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="4215e-207">Spring Boot handles updating the database schema for you as the data model changes without altering your existing database records.</span></span>

1. <span data-ttu-id="4215e-208">在您的本機系統中，開啟 *src/main/java/com/example/fabrikam/TodoItem.java* 並在類別中新增下列匯入項目：</span><span class="sxs-lookup"><span data-stu-id="4215e-208">On your local system, open up *src/main/java/com/example/fabrikam/TodoItem.java* and add the following imports to the class:</span></span>   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. <span data-ttu-id="4215e-209">在 *src/main/java/com/example/fabrikam/TodoItem.java* 中新增 `String` 屬性 `timeCreated`，並以建立物件時使用的時間戳記加以起始。</span><span class="sxs-lookup"><span data-stu-id="4215e-209">Add a `String` property `timeCreated` to *src/main/java/com/example/fabrikam/TodoItem.java*, initializing it with a timestamp at object creation.</span></span> <span data-ttu-id="4215e-210">在編輯此檔案時，為新的 `timeCreated` 屬性新增 getter/setter。</span><span class="sxs-lookup"><span data-stu-id="4215e-210">Add getters/setters for the new `timeCreated` property while you are editing this file.</span></span>

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

3. <span data-ttu-id="4215e-211">以 `updateTodo` 方法中的一行更新 *src/main/java/com/example/fabrikam/TodoDemoController.java*，以設定時間戳記：</span><span class="sxs-lookup"><span data-stu-id="4215e-211">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* with a line in the `updateTodo` method to set the timestamp:</span></span>

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. <span data-ttu-id="4215e-212">在Thymeleaf 範本中加入新欄位的支援。</span><span class="sxs-lookup"><span data-stu-id="4215e-212">Add support for the new field in the Thymeleaf template.</span></span> <span data-ttu-id="4215e-213">以適用於時間戳記的新資料表標頭來更新 *src/main/resources/templates/index.html*，並以新欄位來顯示每個資料表資料列中的時間戳記值。</span><span class="sxs-lookup"><span data-stu-id="4215e-213">Update *src/main/resources/templates/index.html* with a new table header for the timestamp, and a new field to display the value of the timestamp in each table data row.</span></span>

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

5. <span data-ttu-id="4215e-214">重新建置應用程式：</span><span class="sxs-lookup"><span data-stu-id="4215e-214">Rebuild the application:</span></span>

    ```bash
    mvnw clean package 
    ```

6. <span data-ttu-id="4215e-215">一如往常透過 FTP 處理已更新的 .WAR、移除現有的 *site/wwwroot/webapps/ROOT* 目錄和 *ROOT.war*，接著上傳更新的 .WAR 檔案以取代 ROOT.war。</span><span class="sxs-lookup"><span data-stu-id="4215e-215">FTP the updated .WAR as before, removing the existing *site/wwwroot/webapps/ROOT* directory and *ROOT.war*, then uploading the updated .WAR file as ROOT.war.</span></span> 

<span data-ttu-id="4215e-216">當您重新整理應用程式時，會看到**建立時間**的資料行。</span><span class="sxs-lookup"><span data-stu-id="4215e-216">When you refresh the app, a **Time Created** column is now visible.</span></span> <span data-ttu-id="4215e-217">當您新增工作時，應用程式會自動植入時間戳記。</span><span class="sxs-lookup"><span data-stu-id="4215e-217">When you add a new task, the app will populate the timestamp automatically.</span></span> <span data-ttu-id="4215e-218">您現有的工作會維持不變，即使基礎資料模型已變更，仍可搭配使用該應用程式。</span><span class="sxs-lookup"><span data-stu-id="4215e-218">Your existing tasks remain unchanged and work with the app even though the underlying data model has changed.</span></span> 

![搭配新資料行的 Java 應用程式更新](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a><span data-ttu-id="4215e-220">資料流診斷記錄</span><span class="sxs-lookup"><span data-stu-id="4215e-220">Stream diagnostic logs</span></span> 

<span data-ttu-id="4215e-221">在 Azure App Service 中執行您的 Java 應用程式時，可以將主控台記錄直接傳送至終端機。</span><span class="sxs-lookup"><span data-stu-id="4215e-221">While your Java application runs in Azure App Service, you can get the console logs piped directly to your terminal.</span></span> <span data-ttu-id="4215e-222">這樣一來，您就能取得相同的診斷訊息，以協助您偵錯應用程式錯誤。</span><span class="sxs-lookup"><span data-stu-id="4215e-222">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="4215e-223">請使用 [az webapp log tail](/cli/azure/appservice/web/log#tail) 命令開始記錄資料流。</span><span class="sxs-lookup"><span data-stu-id="4215e-223">To start log streaming, use the [az webapp log tail](/cli/azure/appservice/web/log#tail) command.</span></span>

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="4215e-224">管理您的 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4215e-224">Manage your Azure web app</span></span>

<span data-ttu-id="4215e-225">請移至 Azure 入口網站，以查看您所建立的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4215e-225">Go to the Azure portal to see the web app you created.</span></span>

<span data-ttu-id="4215e-226">若要這麼做，請登入 [https://portal.azure.com](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="4215e-226">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="4215e-227">按一下左側功能表中的 [App Service]，然後按一下 Azure Web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="4215e-227">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![入口網站瀏覽至 Azure Web 應用程式](./media/app-service-web-tutorial-java-mysql/access-portal.png)

<span data-ttu-id="4215e-229">根據預設，Web 應用程式的刀鋒視窗會顯示 [概觀] 頁面。</span><span class="sxs-lookup"><span data-stu-id="4215e-229">By default, your web app's blade shows the **Overview** page.</span></span> <span data-ttu-id="4215e-230">此頁面可讓您檢視應用程式的執行方式。</span><span class="sxs-lookup"><span data-stu-id="4215e-230">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="4215e-231">您也可以在這裡執行像是停止、啟動、重新啟動及刪除等管理工作。</span><span class="sxs-lookup"><span data-stu-id="4215e-231">Here, you can also perform management tasks like stop, start, restart, and delete.</span></span> <span data-ttu-id="4215e-232">刀鋒視窗左側的索引標籤會顯示您可開啟的各種設定頁面。</span><span class="sxs-lookup"><span data-stu-id="4215e-232">The tabs on the left side of the blade show the different configuration pages you can open.</span></span>

![Azure 入口網站中的 App Service 刀鋒視窗](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

<span data-ttu-id="4215e-234">刀鋒視窗中的索引標籤會顯示您可以新增至 Web 應用程式的許多強大功能。</span><span class="sxs-lookup"><span data-stu-id="4215e-234">These tabs in the blade show the many great features you can add to your web app.</span></span> <span data-ttu-id="4215e-235">下表提供幾個可能性︰</span><span class="sxs-lookup"><span data-stu-id="4215e-235">The following list gives you just a few of the possibilities:</span></span>
* <span data-ttu-id="4215e-236">對應自訂 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="4215e-236">Map a custom DNS name</span></span>
* <span data-ttu-id="4215e-237">繫結自訂 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="4215e-237">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="4215e-238">設定連續部署</span><span class="sxs-lookup"><span data-stu-id="4215e-238">Configure continuous deployment</span></span>
* <span data-ttu-id="4215e-239">相應增加和相應放大</span><span class="sxs-lookup"><span data-stu-id="4215e-239">Scale up and out</span></span>
* <span data-ttu-id="4215e-240">新增使用者驗證</span><span class="sxs-lookup"><span data-stu-id="4215e-240">Add user authentication</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="4215e-241">清除資源</span><span class="sxs-lookup"><span data-stu-id="4215e-241">Clean up resources</span></span>

<span data-ttu-id="4215e-242">如果您不需要這些資源來進行其他教學課程 (請參閱[後續步驟](#next))，您可以執行下列命令來將這些資源刪除︰</span><span class="sxs-lookup"><span data-stu-id="4215e-242">If you don't need these resources for another tutorial (see [Next steps](#next)), you can delete them by running the following command:</span></span> 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="4215e-243">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4215e-243">Next steps</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4215e-244">在 Azure 中建立 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="4215e-244">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="4215e-245">將範例 Java 應用程式連線至 MySQL</span><span class="sxs-lookup"><span data-stu-id="4215e-245">Connect a sample Java app to the MySQL</span></span>
> * <span data-ttu-id="4215e-246">將應用程式部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="4215e-246">Deploy the app to Azure</span></span>
> * <span data-ttu-id="4215e-247">更新和重新部署應用程式</span><span class="sxs-lookup"><span data-stu-id="4215e-247">Update and redeploy the app</span></span>
> * <span data-ttu-id="4215e-248">來自 Azure 的串流診斷記錄</span><span class="sxs-lookup"><span data-stu-id="4215e-248">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="4215e-249">在 Azure 入口網站中管理應用程式</span><span class="sxs-lookup"><span data-stu-id="4215e-249">Manage the app in the Azure portal</span></span>

<span data-ttu-id="4215e-250">前往下一個教學課程，了解如何將自訂的 DNS 名稱對應至該應用程式。</span><span class="sxs-lookup"><span data-stu-id="4215e-250">Advance to the next tutorial to learn how to map a custom DNS name to the app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="4215e-251">將現有的自訂 DNS 名稱對應至 Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="4215e-251">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
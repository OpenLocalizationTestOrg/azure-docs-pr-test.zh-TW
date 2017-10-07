---
title: "aaaDeploy tooAzure 使用 Jenkins 外掛程式的應用程式服務 |Microsoft 文件"
description: "了解如何 toouse Azure 應用程式服務 Jenkins 外掛程式 toodeploy Java web 應用程式 tooAzure Jenkins 中"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 7/24/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 080be7277555ce7d688dccdf38eef309e7a7b194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-plugin"></a>部署使用 Jenkins 外掛程式 tooAzure 應用程式服務 
toodeploy Java web 應用程式 tooAzure，您可以使用 Azure CLI 中[Jenkins 管線](/azure/jenkins/execute-cli-jenkins-pipeline)或者您可以使用的 hello [Azure 應用程式服務 Jenkins 外掛程式](https://plugins.jenkins.io/azure-app-service)。 在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 設定 Jenkins toodeploy tooAzure 透過 FTP 的應用程式服務 
> * 設定透過 Docker 的 Linux 上的 Jenkins toodeploy tooAzure 應用程式服務 

## <a name="create-and-configure-jenkins-instance"></a>建立及設定 Jenkins 執行個體
如果您還沒有 Jenkins 主要，以 hello 開頭[方案範本](install-jenkins-solution-template.md)，其中包括 JDK8 和下列必要的外掛程式 hello:

* [Jenkins Git 用戶端外掛程式](https://plugins.jenkins.io/git-client) v.2.4.6 
* [Docker Commons 外掛程式](https://plugins.jenkins.io/docker-commons) v.1.4.0
* [Azure 認證](https://plugins.jenkins.io/azure-credentials) v.1.2
* [Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1

您可以使用 hello (比方說，C#、 PHP、 Java 和 node.js 等等） 支援的所有語言 Azure App Service 中的應用程式服務外掛程式 toodeploy Web 應用程式。 在此教學課程中，我們會使用 hello 範例 Java 應用程式，[簡單的 Java Web 應用程式的 Azure](https://github.com/azure-devops/javawebappsample)。 toofork hello 儲存機制 tooyour 擁有 GitHub 帳戶，請按一下 hello**分岔**hello 右上角中的按鈕。  

Java JDK 和 Maven 不需要建置 hello Java 專案。 請確定您將安裝 hello 元件在 hello Jenkins master 或 hello VM 代理程式中，如果您使用另一個用於連續整合。 

tooinstall，登入使用 SSH toohello Jenkins 執行個體，然後執行下列命令的 hello:

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

針對部署 tooApp Linux 上的服務，您也需要 tooinstall Docker hello Jenkins master 或用於建置 hello VM 代理程式上。 Toothis 文章 tooinstall Docker，請參閱： https://docs.docker.com/engine/installation/linux/ubuntu/。

## <a name="add-azure-service-principal-toojenkins-credential"></a>加入 Azure 服務主體 tooJenkins 認證

Azure 服務主體是所需的 toodeploy tooAzure。 

<ol>
<li>使用[Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json)或[Azure 入口網站](/azure/azure-resource-manager/resource-group-create-service-principal-portal)toocreate Azure 服務主體</li>
<li>在 hello Jenkins 儀表板內，按一下**認證-> 系統->** 。 按一下 [Global credentials(unrestricted)] \(全域認證 (不受限)\)。</li>
<li>按一下**新增認證**tooadd 填寫 hello 訂用帳戶 ID、 用戶端識別碼、 用戶端密碼和 OAuth 2.0 權杖端點的 Microsoft Azure 服務主體。 請提供要在後續步驟中使用的識別碼 (**mySp**)。</li>
</ol>

## <a name="azure-app-service-plugin"></a>Azure App Service 外掛程式

Azure App Service 外掛程式 v1.0 支援以連續部署 tooAzure Web 應用程式透過：

* Git 和 FTP
* 適用於 Linux 上 Web 應用程式的 Docker

## <a name="configure-jenkins-toodeploy-web-app-through-ftp-using-hello-jenkins-dashboard"></a>設定 Jenkins toodeploy 透過 FTP 使用 hello Jenkins 儀表板的 Web 應用程式

toodeploy 您專案 tooAzure Web 應用程式，您可以上傳您的組建成品 （例如，在 Java 中.war 檔案） 使用 Git 或 FTP。

之前設定 Jenkins hello 工作，您需要 Azure App Service 方案和 Web 應用程式執行 hello Java 應用程式。


1. 建立 Azure App Service 方案以 hello**免費**定價層使用 hello [az 應用程式服務方案建立](/cli/azure/appservice/plan#create)CLI 命令。 hello 應用程式服務方案會定義 hello 使用的實體資源 toohost 您的應用程式。 指派 tooan 應用程式服務方案的所有應用程式共用這些資源，讓您 toosave 成本裝載多個應用程式時。
2. 建立 Web 應用程式。 可以是使用 hello [Azure 入口網站](/azure/app-service-web/web-sites-configure)或使用 hello 下列 Az CLI 命令：
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. 請確定您設定您的應用程式需要的 hello Java 執行階段組態。 下列 Azure CLI 命令的 hello 設定 hello web 應用程式 toorun 上最近的 Java 8 JDK 和[Apache Tomcat](http://tomcat.apache.org/) 8.0。
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-hello-jenkins-job"></a>設定 hello Jenkins 工作


1. 在 Jenkins 儀表板中建立新的**自由樣式**專案
2. 設定**原始程式碼管理**toouse 本機分岔[簡單的 Java Web 應用程式的 Azure](https://github.com/azure-devops/javawebappsample)藉由提供 hello**儲存機制 URL**。 例如：http://github.com/&lt;yourID>/javawebappsample。
3. 加入使用 Maven 建置步驟 toobuild hello 專案。 新增**執行殼層**即可達到此目的。 例如，我們需要額外的步驟 toorename hello *.war 中的檔案目標資料夾 tooROOT.war。   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. 選取 [發行 Azure Web 應用程式] 來新增建置後動作。
5. 供應、"mySp 」、 儲存在上一個步驟中的 hello Azure 服務主體。
6. 在**應用程式組態**區段中，選擇您的訂用帳戶中的 hello 資源群組和 web 應用程式。 hello 外掛程式會自動偵測 hello Web 應用程式是否為 Windows 或 Linux。 Windows Web 應用程式中，會顯示 hello 選項 「 發行檔案 」。
7. 填滿 hello 檔案中，您想 toodeploy （例如 war 封裝如果您使用 Java。）[來源目錄] 和 [目標目錄] 是選擇性欄位。 hello 參數可讓您 toospecify 來源和目標資料夾上傳檔案時。 Azure 上的 Java Web 應用程式會在 Tomcat 伺服器中執行。 因此，您會將 war 套件上傳到 webapps 資料夾。 這個範例中，將設定**來源目錄**太 「 目標 」 和 「 webapps 」 提供的**目標目錄**。
8. 如果您想 toodeploy tooa 插槽生產以外，您也可以設定**插槽**名稱。
9. 儲存 hello 專案並建置該檔案。 組建完成時，您的 web 應用程式是部署的 tooAzure。

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a>使用 Jenkins 管線來透過 FTP 部署 Web 應用程式

hello 外掛程式是管線已備妥。 您可以參考 tooa hello GitHub 儲存機制中的範例。

1. 在 GitHub Web UI 中，開啟 **Jenkinsfile_ftp_plugin** 檔案。 分別按一下 hello 鉛筆圖示 tooedit 這個檔案 tooupdate hello 資源群組與上一行 11 和 12 的 web 應用程式的名稱。    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. 變更您 Jenkins 執行個體中的行 14 tooupdate 認證識別碼。    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a>建立 Jenkins 管線

1. 在網頁瀏覽器中開啟 Jenkins，按一下 [New Item] \(新增項目\)。
2. 提供 hello 工作的名稱，並選取**管線**。 按一下 [確定] 。
3. 按一下 hello**管線**索引標籤旁邊。
4. 針對 [Definition] \(定義\)，選取 [Pipeline script from SCM] \(來自 SCM 的管線指令碼\)。
5. 針對 [SCM]，選取 [Git]。 輸入您分岔的儲存機制的 hello GitHub URL: https:&lt;您分岔的儲存機制 >.git
6. 更新**指令碼路徑**太"Jenkinsfile_ftp_plugin"
7. 按一下**儲存**與 hello 執行的工作。

## <a name="configure-jenkins-toodeploy-web-app-on-linux-through-docker"></a>設定透過 Docker 的 Linux 上的 Jenkins toodeploy Web 應用程式

除了透過 Git/FTP，Linux 上的 Web 應用程式還支援使用 Docker 來進行部署。 使用 Docker toodeploy 需要 tooprovide 將 docker 映像封裝為 web 應用程式與服務執行階段的 Dockerfile。 然後 hello 外掛程式建置 hello 映像、 將其發送 tooa docker 登錄和部署 hello 映像 tooyour web 應用程式。

Linux 上的 Web 應用程式也支援 Git 和 FTP 等傳統方式，但這些方式只適用於內建語言 (.NET Core、Node.js、PHP 和 Ruby)。 至於其他語言，您需要 toopackage 應用程式程式碼和服務執行階段一起到 docker 映像和使用 docker toodeploy。

之前設定 Jenkins hello 工作，您必須在 Linux 上的 Azure 應用程式服務。 容器登錄中也需要的 toostore 並管理私人 Docker 容器映像。 您可以使用 DockerHub；我們會在此範例中使用 Azure Container Registry。

* 您可以依照 hello 步驟[這裡](/azure/app-service-web/app-service-linux-how-to-create-web-app)toocreate Linux 上的 Web 應用程式 
* Azure 容器登錄中是受管理 [Docker 登錄] (https://docs.docker.com/registry/) 為基礎的服務 hello 開放原始碼 Docker 登錄 2.0。 請遵循 [這裡] hello 步驟 （/ azure/container-registry/container-registry-get-started-azure-cli） 的詳細指引 toodo 讓。 您也可以使用 DockerHub。

### <a name="toodeploy-using-docker"></a>使用 docker toodeploy:

1. 在 Jenkins 儀表板中建立新的自由樣式專案。
2. 設定**原始程式碼管理**toouse 本機分岔[簡單的 Java Web 應用程式的 Azure](https://github.com/azure-devops/javawebappsample)藉由提供 hello**儲存機制 URL**。 例如：http://github.com/&lt;yourid>/javawebappsample。
加入使用 Maven 建置步驟 toobuild hello 專案。 這樣做將**執行殼層**並加入下列行中的 hello**命令**:    
```bash
mvn clean package
```

3. 選取 [發行 Azure Web 應用程式] 來新增建置後動作。
4. 提供， **mySp**，做為 Azure 認證的上一個步驟中儲存的 hello Azure 服務主體。
5. 在**應用程式組態**區段中，選擇您的訂用帳戶中的 hello 資源群組和 Linux 的 web 應用程式。
6. 選擇透過 Docker 來發行。
7. 填寫 **Dockerfile** 路徑。 您可以保留 hello 預設 「 / Dockerfile 」 的**Docker 登錄 URL**、 https:// hello 格式提供&lt;myRegistry >。 azurecr.io，如果您使用 Azure 容器登錄中。 如果您使用 DockerHub，請讓它保持空白。
8. 如**登錄認證**，新增 hello Azure 容器登錄中的 hello 認證。 您可以藉由執行下列 Azure CLI 命令的 hello 取得 hello 使用者識別碼和密碼。 hello 第一個命令會啟用 hello 系統管理員帳戶。    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. docker 映像名稱和標記中的 hello**進階**是選擇性的索引標籤。 根據預設，可取得的映像名稱從 hello 映像從 $BUILD_NUMBER 產生您在 Azure 入口網站 （在 Docker 容器設定。） hello 標記中設定的名稱。 請確定您指定其中一個 Azure 入口網站中的 hello 映像名稱，或提供的值**Docker 映像**中**進階** 索引標籤。在此範例中，請在 Docker 映像 中提供「&lt;yourRegistry>.azurecr.io/calculator」，並讓 Docker 映像標記 保持空白。
10. 請注意，如果您使用內建的 Docker 映像設定，部署將會失敗。 請確定您變更 docker 設定 toouse 自訂映像中的 Azure 入口網站上的 Docker 容器設定。 內建影像，請使用檔案上傳方法 toodeploy。
11. 類似的 toofile 上傳方法，您可以選擇生產環境以外的不同位置。
12. 儲存並建置 hello 專案。 您會看到您的容器映像推入 tooyour 登錄和 web 應用程式部署。

### <a name="deploy-tooweb-app-on-linux-through-docker-using-jenkins-pipeline"></a>部署 tooWeb 透過使用 Jenkins 管線的 Docker 的 Linux 上的應用程式

1. 在 GitHub Web UI 中，開啟 **Jenkinsfile_container_plugin** 檔案。 分別按一下 hello 鉛筆圖示 tooedit 這個檔案 tooupdate hello 資源群組與上一行 11 和 12 的 web 應用程式的名稱。    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. 變更線條 13 tooyour 容器登錄伺服器    
```java
def registryServer = '<registryURL>'
```    

3. 變更您 Jenkins 執行個體中的行 16 tooupdate 認證識別碼    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a>建立 Jenkins 管線    

1. 在網頁瀏覽器中開啟 Jenkins，按一下 [New Item] \(新增項目\)。
2. 提供 hello 工作的名稱，並選取**管線**。 按一下 [確定] 。
3. 按一下 hello**管線**索引標籤旁邊。
4. 針對 [Definition] \(定義\)，選取 [Pipeline script from SCM] \(來自 SCM 的管線指令碼\)。
5. 針對 [SCM]，選取 [Git]。
6. 輸入您分岔的儲存機制的 hello GitHub URL: https:&lt;您分岔的儲存機制 >.git</li>
第 7 更新**指令碼路徑**太"Jenkinsfile_container_plugin"
8. 按一下**儲存**與 hello 執行的工作。

## <a name="verify-your-web-app"></a>確認您的 Web 應用程式

1. 已成功部署 tooverify hello WAR 檔案 tooyour web 應用程式。 請開啟網頁瀏覽器。
2. 移 toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping 您會看到：    
     Web 應用程式的 歡迎使用 tooJava!!! 此應用程式已更新！
   Sun Jun 17 16:39:10 UTC 2017
3. 移 toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > （& s) y =&lt;y > (替代&lt;x > 和&lt;y > 使用的任何數字) tooget hello 總和的 x 和 y        
    ![計算機：加法](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a>Linux 上的 App Service

* tooverify，在 Azure CLI 執行：

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    您會收到 hello 下列結果：
    
    ```
    [
    "calculator"
    ]
    ```
    
    移 toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping。 您會看到 hello 訊息： 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    移 toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > （& s) y =&lt;y > (替代&lt;x > 和&lt;y > 使用的任何數字) tooget hello 總和的 x 和 y
    
## <a name="next-steps"></a>後續步驟

在本教學課程中，您可以使用 hello Azure App Service 外掛程式 toodeploy tooAzure。

您已了解如何︰

> [!div class="checklist"]
> * 設定 Jenkins toodeploy 透過 FTP 的 Azure 應用程式服務 
> * 設定透過 Docker 的 Linux 上的 Jenkins toodeploy tooAzure 應用程式服務 

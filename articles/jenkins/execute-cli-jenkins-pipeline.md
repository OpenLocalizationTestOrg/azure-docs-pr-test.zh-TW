---
title: "aaaExecute hello Azure CLI jenkins |Microsoft 文件"
description: "了解如何 toouse Azure CLI toodeploy Java web 應用程式 tooAzure Jenkins 管線中"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: jenkins
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 4bd1e12e6de1f010453ff51c835f84e7361962f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a>部署應用程式服務與 Jenkins tooAzure 和 hello Azure CLI
toodeploy Java web 應用程式 tooAzure，您可以使用 Azure CLI 中[Jenkins 管線](https://jenkins.io/doc/book/pipeline/)。 在本教學課程中，您會在 Azure VM 上建立 CI/CD 管線，包括如何︰

> [!div class="checklist"]
> * 建立 Jenkins VM
> * 設定 Jenkins
> * 在 Azure 中建立 Web 應用程式
> * 準備 GitHub 存放庫
> * 建立 Jenkins 管線
> * 執行 hello 管線，並確認 hello web 應用程式

本教學課程需要 hello Azure CLI 版本 2.0.4 或更新版本。 toofind hello 版本，執行`az --version`。 如果您需要 tooupgrade，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a>建立及設定 Jenkins 執行個體
如果您還沒有 Jenkins 主要，以 hello 開頭[方案範本](install-jenkins-solution-template.md)，其中包含所需的 hello [Azure 認證](https://plugins.jenkins.io/azure-credentials)預設的外掛程式。 

hello Azure 認證外掛程式可讓您 toostore Microsoft Azure 服務主體認證 Jenkins 中。 在 1.2 版中，我們會加入 hello 支援，因此該 Jenkins 管線可以取得 hello Azure 認證。 

請確定您擁有的版本是 1.2 或更新版本：
* 在 hello Jenkins 儀表板內，按一下**管理 Jenkins-> 外掛程式管理員->** 並搜尋**Azure 認證**。 
* 如果 hello 版本早於 1.2，更新 hello 外掛程式。

也需要 Java JDK 和 Maven hello Jenkins master 中。 tooinstall，登入使用 SSH tooJenkins master，然後執行下列命令的 hello:
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a>加入 Azure 服務主體 tooJenkins 認證

Azure 的認證是需要的 tooexecute Azure CLI。

* 在 hello Jenkins 儀表板內，按一下**認證-> 系統->** 。 按一下 [Global credentials(unrestricted)] \(全域認證 (不受限)\)。
* 按一下**新增認證**tooadd [Microsoft Azure 服務主體](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json)填寫 hello 訂用帳戶 ID、 用戶端識別碼、 用戶端密碼和 OAuth 2.0 權杖端點。 請提供一個要在後續步驟中使用的識別碼。

![新增認證](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a>建立 hello Java web 應用程式部署的 Azure 應用程式服務

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

## <a name="prepare-a-github-repository"></a>準備 GitHub 存放庫
開啟 hello[簡單的 Java Web 應用程式的 Azure](https://github.com/azure-devops/javawebappsample)儲存機制。 toofork hello 儲存機制 tooyour 擁有 GitHub 帳戶，請按一下 hello**分岔**hello 右上角中的按鈕。

* 在 GitHub Web UI 中，開啟 **Jenkinsfile** 檔案。 分別按一下 hello 鉛筆圖示 tooedit 此檔案 tooupdate hello 資源群組和 20 和 21 行上的 web 應用程式的名稱。

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* 變更您 Jenkins 執行個體中的行 23 tooupdate 認證識別碼

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a>建立 Jenkins 管線
在網頁瀏覽器中開啟 Jenkins，按一下 [New Item] \(新增項目\)。 

* 提供 hello 工作的名稱，並選取**管線**。 按一下 [確定] 。
* 按一下 hello**管線**索引標籤旁邊。 
* 針對 [Definition] \(定義\)，選取 [Pipeline script from SCM] \(來自 SCM 的管線指令碼\)。
* 針對 [SCM]，選取 [Git]。
* 輸入您分岔的儲存機制的 hello GitHub URL: https:\<您分岔的儲存機制\>.git
* 按一下 [儲存] 

## <a name="test-your-pipeline"></a>測試您的管線
* 前往您所建立的 toohello 管線中，按一下**現在建置**
* 幾分鐘後，應該會成功建置，而且您可以移 toohello 組建，並按一下**主控台輸出**toosee hello 詳細資料

## <a name="verify-your-web-app"></a>確認您的 Web 應用程式
已成功部署 tooverify hello WAR 檔案 tooyour web 應用程式。 請開啟網頁瀏覽器：

* 移 toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping  
您會看見：

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* 移 toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > （& s) y =&lt;y > (替代&lt;x > 和&lt;y > 使用的任何數字) tooget hello 總和的 x 和 y

![計算機：加法](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a>部署 tooAzure Linux 上的 Web 應用程式
您現在知道如何在您 Jenkins Azure CLI toouse 管線，您可以修改 hello 指令碼 toodeploy tooan on Linux 的 Azure Web 應用程式。

Web 應用程式，在 Linux 上支援不同的方式 toodo hello 部署，也就是 toouse Docker。 toodeploy，您需要 tooprovide 將 Docker 映像封裝為 web 應用程式與服務執行階段的 Dockerfile。 hello 外掛程式將再建置 hello 映像，直接將其推 tooa Docker 登錄和部署 hello 映像 tooyour web 應用程式。

* 請依照下列步驟 hello[這裡](/azure/app-service-web/app-service-linux-how-to-create-web-app)toocreate 在 Linux 上執行的 Azure Web 應用程式。
* Jenkins 執行個體上安裝 Docker，在這個 hello 指示[文章](https://docs.docker.com/engine/installation/linux/ubuntu/)。
* 在 hello Azure 入口網站中建立容器登錄中，使用 hello 步驟[這裡](/azure/container-registry/container-registry-get-started-azure-cli)。
* 在 hello 相同[簡單的 Java Web 應用程式的 Azure](https://github.com/azure-devops/javawebappsample)分叉時，儲存機制編輯 hello **Jenkinsfile2**檔案：
    * 行 18-21，分別更新的資源群組、 web 應用程式，以及 ACR toohello 名稱。 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * 第 24 行、 更新\<azsrvprincipal\> tooyour 認證識別碼
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* 因為您未部署在 Windows 中，這個時間，使用 tooAzure web 應用程式時，建立新的 Jenkins 管線**Jenkinsfile2**改為。
* 執行您的新作業。
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
在本教學課程中，您可以設定簽出 hello 原始碼 GitHub 儲存機制中的 Jenkins 管線。 執行 Maven toobuild war 檔案，然後使用 Azure CLI toodeploy tooAzure 應用程式服務。 您已了解如何︰

> [!div class="checklist"]
> * 建立 Jenkins VM
> * 設定 Jenkins
> * 在 Azure 中建立 Web 應用程式
> * 準備 GitHub 存放庫
> * 建立 Jenkins 管線
> * 執行 hello 管線，並確認 hello web 應用程式

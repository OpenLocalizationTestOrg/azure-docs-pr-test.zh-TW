---
title: "aaaDeploy 上 Azure 容器服務中 Kubernetes Spring 開機應用程式 |Microsoft 文件"
description: "本教學課程將逐步引導您透過 hello 步驟 toodeploy Spring 開機應用程式在 Kubernetes 叢集中在 Microsoft Azure 上。"
services: container-service
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 2bf9df459f874a1f478f43cdd29992d86c370837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-hello-azure-container-service"></a>Spring 開機應用程式部署上 Kubernetes 叢集在 hello Azure 容器服務

hello  **[Spring 架構]**是熱門的開放原始碼架構，可協助建立 web、 行動裝置版及 API 應用程式的 Java 開發人員。 本教學課程使用範例應用程式使用建立[Spring 開機]，慣例導向的方式使用 Spring tooget 快速入門。

**[Kubernetes]** 和 **[Docker]**  hello 部署、 調整及管理的應用程式執行的是協助開發人員的開放原始碼解決方案自動化在容器中。

本教學課程會逐步引導您雖然結合這些兩個常用、 開放原始碼技術，toodevelop 和部署 Spring 開機應用程式 tooMicrosoft Azure。 更具體來說，您使用 *[Spring 開機]*應用程式開發 *[Kubernetes]* 容器部署和 hello[Azure 容器服務 (ACS)] toohost 您的應用程式。

### <a name="prerequisites"></a>必要條件

* Azure 訂用帳戶；如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益]或註冊[免費的 Azure 帳戶]。
* hello [Azure 命令列介面 (CLI)]。
* 最新的 [Java 開發工具組 (JDK)]。
* Apache 的 [Maven] 建置工具 (第 3 版)。
* [Git] 用戶端。
* [Docker] 用戶端。

> [!NOTE]
>
> Toohello 本教學課程的虛擬化需求，因為您無法依照本文中的 hello 步驟執行虛擬機器;啟用虛擬化功能，您必須使用實體電腦。
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a>Docker 快速入門的 web 應用程式上建立 hello Spring 開機

hello 步驟會逐步引導您建置 Spring 開機 web 應用程式，並在本機加以測試。

1. 開啟命令提示字元，並建立本機目錄 toohold，您的應用程式，以及變更 toothat 目錄;例如：
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- 或 --
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. 複製 hello[上開始使用 Docker Spring 開機]到 hello 目錄中的範例專案。
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. 變更目錄已完成的 toohello 專案。
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. 使用 Maven toobuild 和執行的 hello 範例應用程式。
   ```
   mvn package spring-boot:run
   ```

1. 測試 hello web 應用程式瀏覽 toohttp://localhost:8080，或與 hello 下列`curl`命令：
   ```
   curl http://localhost:8080
   ```

1. 您應該會看到下列訊息顯示 hello: **Hello Docker World**

   ![在本機瀏覽範例應用程式][SB01]

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a>建立 Azure 容器登錄中使用 Azure CLI hello

1. 開啟命令提示字元。

1. Azure 帳戶登入 tooyour 中：
   ```azurecli
   az login
   ```

1. 本教學課程中所使用的 Azure 資源建立 hello 的資源群組。
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. Hello 資源群組中建立私人 Azure 容器登錄中。 hello 教學課程將為 Docker 映像 toothis 登錄在稍後步驟中，推入 hello 範例應用程式。 以登錄的唯一名稱取代 `wingtiptoysregistry`。
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-toohello-container-registry"></a>推送您的應用程式 toohello 容器登錄中

1. 瀏覽 toohello Maven 安裝的設定目錄 (預設 ~/.m2/ 或 C:\Users\username\.m2) 並開啟 hello *settings.xml*使用文字編輯器的檔案。

1. 擷取 hello Azure CLI hello 容器登錄中您的密碼。
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. 加入您 Azure 容器登錄 id 和密碼 tooa 新`<server>`中 hello 集合*settings.xml*檔案。
hello`id`和`username`hello hello 登錄名稱。 使用 hello `password` hello 前一個命令 （不含引號） 的值。

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. 瀏覽 toohello 完成 Spring 開機應用程式的專案目錄 (例如，"*C:\SpringBoot\gs-spring-boot-docker\complete*「 或 」*/users/robert/SpringBoot/gs-spring-boot-docker /完成*")，並開啟 hello *pom.xml*使用文字編輯器的檔案。

1. 更新 hello`<properties>`中 hello 集合*pom.xml* Azure 容器登錄檔案具有 hello 登入伺服器的值。

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. 更新 hello`<plugins>`中 hello 集合*pom.xml*檔案，因此，hello`<plugin>`包含 hello 登入伺服器位址和登錄名稱 Azure 容器登錄。

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. 瀏覽 toohello 完成 Spring 開機應用程式的專案目錄，然後執行下列命令 toobuild hello Docker 容器和推播 hello 映像 toohello 登錄 hello:

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  您可能會收到錯誤訊息，Maven 推播通知 hello 映像 tooAzure 時會 hello 以下的類似 tooone:
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> 如果您收到這個錯誤，請登入 tooAzure 從 hello Docker 命令列。
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> 然後推送您的容器：
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-hello-azure-cli"></a>使用 Azure CLI hello ACS 上建立 Kubernetes 叢集

1. 在 Azure Container Service 中建立 Kubernetes 叢集。 hello 下列命令會建立*kubernetes*叢集中 hello *wingtiptoys kubernetes*資源群組，以及*wingtiptoys containerservice*為 hello 叢集名稱，和*wingtiptoys kubernetes* hello DNS 前置詞為：
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   此命令可能需要一些時間 toocomplete。

1. 安裝`kubectl`使用 hello Azure CLI。 Linux 使用者與此命令時可能有 tooprefix`sudo`因為它太部署 hello Kubernetes CLI`/usr/local/bin`。
   ```azurecli
   az acs kubernetes install-cli
   ```

1. 下載 hello 叢集組態資訊，因此您可以從 hello Kubernetes web 介面來管理您的叢集和`kubectl`。 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-hello-image-tooyour-kubernetes-cluster"></a>部署 hello 映像 tooyour Kubernetes 叢集

本教學課程部署 hello 的應用程式使用`kubectl`，然後允許您 tooexplore hello 部署透過 hello Kubernetes web 介面。

### <a name="deploy-with-hello-kubernetes-web-interface"></a>部署與 hello Kubernetes web 介面

1. 開啟命令提示字元。

1. 在預設瀏覽器中開啟 hello 組態網站 Kubernetes 叢集：
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. Hello Kubernetes 組態網站開啟時瀏覽器中，按一下 hello 連結太**容器化應用程式部署**:

   ![Kubernetes 設定網站][KB01]

1. 當 hello**容器化應用程式部署**會顯示頁面，指定下列選項的 hello:

   a. 選取 [Specify app details below] (指定以下的應用程式詳細資料)。

   b. 輸入您的 Spring 開機應用程式名稱，以 hello**應用程式名稱**; 例如:"*gs spring 開機-docker*"。

   c. 從您登入伺服器和容器映像輸入稍早 hello**容器映像**; 例如:"*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"。

   d. 選擇**外部**hello**服務**。

   e. 指定您的外部和內部連接埠在 hello**連接埠**和**目標連接埠**文字方塊。

   ![Kubernetes 設定網站][KB02]


1. 按一下**部署**toodeploy hello 容器。

   ![部署容器][KB05]

1. 應用程式一經部署，您就會看到 [服務] 底下列出您的 Spring Boot 應用程式。

   ![Kubernetes 服務][KB06]

1. 如果您按一下 hello 連結**外部端點**，您可以看到您在 Azure 上執行的 Spring 開機應用程式。

   ![Kubernetes 服務][KB07]

   ![在 Azure 上瀏覽範例應用程式][SB02]


### <a name="deploy-with-kubectl"></a>使用 kubectl 部署

1. 開啟命令提示字元。

1. 在 hello Kubernetes 叢集中執行您的容器，使用 hello`kubectl run`命令。 可讓您的應用程式中 Kubernetes 的服務名稱和 hello 完整的映像名稱。 例如：
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   在這個命令中：

   * hello 容器名稱`gs-spring-boot-docker`指定 hello 之後立即`run`命令

   * hello`--image`參數會指定 hello 結合登入伺服器，做為映像名稱`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`

1. 公開外部使用 hello Kubernetes 叢集`kubectl expose`命令。 指定服務名稱、 hello 公開 TCP 使用連接埠 tooaccess hello 應用程式和您的應用程式所接聽的 hello 內部目標連接埠。 例如：
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   在這個命令中：

   * hello 容器名稱`gs-spring-boot-docker`指定 hello 之後立即`expose deployment`命令

   * hello`--type`參數指定該 hello 叢集會使用負載平衡器

   * hello`--port`參數會指定 hello 公開 TCP 連接埠 80。 您存取在此連接埠的 hello 應用程式。

   * hello`--target-port`參數會指定 hello 內部 TCP 連接埠 8080。 hello 負載平衡器會將轉送要求 tooyour 應用程式在此連接埠。

1. Hello 應用程式部署之後 toohello 叢集中，查詢 hello 外部 IP 位址，並在網頁瀏覽器中開啟它：

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![在 Azure 上瀏覽範例應用程式][SB02]


## <a name="next-steps"></a>後續步驟

如需在 Azure 上使用 Spring 開機的詳細資訊，請參閱下列文章 hello:

* [部署 Spring 開機應用程式 toohello Azure App Service](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [部署在 Linux 上 hello Azure 容器服務中的 Spring 開機應用程式](container-service-deploy-spring-boot-app-on-linux.md)

如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]和 hello [Java 工具的 Visual Studio Team Services]。

Docker 範例專案在 hello Spring 開機的相關資訊，請參閱[上開始使用 Docker Spring 開機]。

hello 下列連結提供有關建立 Spring 開機應用程式的其他資訊：

* 如需有關如何建立簡單的 Spring 開機應用程式的詳細資訊，請參閱 < 在 https://start.spring.io/ hello Spring Initializr。

hello 下列連結提供有關搭配 Azure 使用 Kubernetes 的其他資訊：

* [在 Container Service 中開始使用 Kubernetes 叢集](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [使用 hello Kubernetes web UI，使用 Azure 容器服務](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

使用 Kubernetes 命令列介面的詳細資訊位於 hello **kubectl**使用者指南 》，網址<https://kubernetes.io/docs/user-guide/kubectl/>。

hello Kubernetes 網站有幾篇文章會討論使用私人登錄中的映像：

* [設定 Pod 的服務帳戶]
* [命名空間]
* [從私用登錄提取映像]

針對如何 toouse 自訂的 Docker 映像與 Azure 的其他範例，請參閱[on Linux 的 Azure Web 應用程式中使用自訂的 Docker 映像]。

<!-- URL List -->

[Azure 命令列介面 (CLI)]: /cli/azure/overview
[Azure 容器服務 (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[on Linux 的 Azure Web 應用程式中使用自訂的 Docker 映像]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[免費的 Azure 帳戶]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java 開發工具組 (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java 工具的 Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[MSDN 訂戶權益]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring 開機]: http://projects.spring.io/spring-boot/
[上開始使用 Docker Spring 開機]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring 架構]: https://spring.io/
[設定 Pod 的服務帳戶]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[命名空間]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[從私用登錄提取映像]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR04.png

[KB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB01.png
[KB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB02.png
[KB03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB03.png
[KB04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB04.png
[KB05]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB05.png
[KB06]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB06.png
[KB07]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB07.png

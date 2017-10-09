---
title: "aaaContinuous 建置和 Azure Service Fabric Linux Java 應用程式使用 Jenkins 的整合 |Microsoft 文件"
description: "使用 Jenkins 連續建置和整合 Linux Java 應用程式"
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 15da2cb8c759233219369ea889550da93748129f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-jenkins-toobuild-and-deploy-your-linux-java-application"></a>使用 Jenkins toobuild 及部署 Linux Java 應用程式
Jenkins 是連續整合和部署應用程式的熱門工具。 以下是如何 toobuild 和部署 Azure Service Fabric 應用程式使用 Jenkins。

## <a name="general-prerequisites"></a>一般先決條件
- 在本機安裝 Git。 您可以安裝來自 hello 適當 Git 版本[hello Git 下載頁面](https://git-scm.com/downloads)，根據您的作業系統。 如果您是新 tooGit，深入了解從 hello [Git 文件](https://git-scm.com/docs)。
- 擁有 hello 服務網狀架構 Jenkins 外掛程式很方便。 您可以從 [Service Fabric 下載](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi)進行下載。

## <a name="set-up-jenkins-inside-a-service-fabric-cluster"></a>在 Service Fabric 叢集內設定 Jenkins

您可以在 Service Fabric 叢集內部或外部設定 Jenkins。 hello 面各節顯示 tooset 如何當它在使用 Azure 儲存體叢集內帳戶 toosave hello hello 容器執行個體狀態。

### <a name="prerequisites"></a>必要條件
1. 讓 Service Fabric Linux 叢集準備就緒。 Service Fabric 叢集已經從 hello Azure 入口網站建立具有已安裝 Docker。 如果您在本機執行 hello 叢集，請檢查使用 hello 命令是否已安裝 Docker ``docker info``。 如果未安裝，安裝據以使用下列命令 hello:

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```
2. 已使用下列步驟的 hello hello 叢集上部署的 hello Service Fabric 容器應用程式：

  ```sh
git clone https://github.com/Azure-Samples/service-fabric-java-getting-started.git
cd service-fabric-java-getting-started/Services/JenkinsDocker/
```

3. 您需要 hello 連接選項的詳細資料的 hello Azure 儲存體檔案共用，您想要 toopersist hello hello Jenkins 容器執行個體狀態。 如果您使用 hello hello Microsoft Azure 入口網站相同，請在步驟 hello，-建立 Azure 儲存體帳戶，例如``sfjenkinsstorage1``。 在該儲存體帳戶底下建立一個「檔案共用」(例如 ``sfjenkins``)。 按一下**連接**針對 hello 檔案共用，注意 hello 值就會顯示在**連接從 Linux**，假設這看起來會類似如下-
```sh
sudo mount -t cifs //sfjenkinsstorage1.file.core.windows.net/sfjenkins [mount point] -o vers=3.0,username=sfjenkinsstorage1,password=<storage_key>,dir_mode=0777,file_mode=0777
```

4. 更新在 hello hello 預留位置值```setupentrypoint.sh```與對應的 azure 儲存體詳細資料的指令碼。
```sh
vi JenkinsSF/JenkinsOnSF/Code/setupentrypoint.sh
```
取代``[REMOTE_FILE_SHARE_LOCATION]``hello 值``//sfjenkinsstorage1.file.core.windows.net/sfjenkins``hello hello 輸出連接上面的 3 點中。
取代``[FILE_SHARE_CONNECT_OPTIONS_STRING]``hello 值``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777``從上面的 3 點。

5. Toohello 叢集連線，並安裝 hello 容器應用程式。
```azurecli
sfctl cluster select --endpoint http://PublicIPorFQDN:19080   # cluster connect command
bash Scripts/install.sh
```
這在 hello 叢集上，安裝 Jenkins 容器，您可以監視使用 hello Service Fabric 總管。

### <a name="steps"></a>步驟
1. 從您的瀏覽器，移過``http://PublicIPorFQDN:8081``。 它提供了在 hello 初始管理所需密碼 toosign hello 路徑。 您可以繼續 toouse Jenkins 身為系統管理員使用者。 或者，您可以建立並之後 hello 初始管理帳戶登入時變更 hello 使用者。

   > [!NOTE]
   > 請在建立 hello 叢集時，確認要 hello 8081 的連接埠指定為 hello 應用程式端點連接埠。
   >

2. 使用取得 hello 容器執行個體識別碼``docker ps -a``。
3. 安全殼層 (SSH) 登入 toohello 容器內，並貼上您所顯示 hello Jenkins 入口網站的 hello 路徑。 例如，如果它在 hello 入口網站中顯示 hello 路徑`PATH_TO_INITIAL_ADMIN_PASSWORD`，執行下列 hello:

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash   # This takes you inside Docker shell
  cat PATH_TO_INITIAL_ADMIN_PASSWORD
  ```

4. 使用 hello 步驟中所述，設定 GitHub toowork jenkins，[產生新的 SSH 金鑰，並將它加入 toohello SSH 代理程式](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)。
    * 使用 hello GitHub toogenerate hello SSH 金鑰和 tooadd hello SSH 金鑰 toohello 裝載您的儲存機制的 GitHub 帳戶所提供的指示。
    * 執行 hello 上述連結 hello Jenkins Docker 命令介面中 （且不在主機上） 中所述的 hello 命令。
    * toosign 中 toohello Jenkins 殼層，從您的主機使用 hello 下列命令：

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
  ```

## <a name="set-up-jenkins-outside-a-service-fabric-cluster"></a>在 Service Fabric 叢集外設定 Jenkins

您可以在 Service Fabric 叢集內部或外部設定 Jenkins。 hello 下列各節顯示如何 tooset 它在叢集外。

### <a name="prerequisites"></a>必要條件
您必須已安裝 Docker toohave。 hello，下列命令可以是使用的 tooinstall Docker hello 終端機的：

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```

現在，當您執行``docker info``在 hello 終端機，您應該會看到 hello 輸出中的 hello Docker 服務正在執行。

### <a name="steps"></a>步驟
  1. 提取 hello 服務網狀架構 Jenkins 容器映像：``docker pull raunakpandya/jenkins:v1``
  2. 執行 hello 容器映像：``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``
  3. 取得 hello 識別碼 hello 容器映像執行個體。 您可以列出所有與 hello 命令的 hello Docker 容器``docker ps –a``
  4. Toohello Jenkins 入口網站使用的登入 hello 下列步驟：

    * ```sh
    docker exec [first-four-digits-of-container-ID] cat /var/jenkins_home/secrets/initialAdminPassword
    ```
    如果容器識別碼是 2d24a73b5964，請使用 2d24。
    * 此密碼是必要的登入入口網站，也就是 toohello Jenkins 儀表板``http://<HOST-IP>:8080``
    * 您登入的 hello 第一次之後，您可以建立您自己的使用者帳戶，並使用該以備將來使用，或者您可以繼續 toouse hello 系統管理員帳戶。 建立使用者之後，您需要與 toocontinue。
  5. 使用 hello 步驟中所述，設定 GitHub toowork jenkins，[產生新的 SSH 金鑰，並將它加入 toohello SSH 代理程式](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)。
        * 使用 hello GitHub toogenerate hello SSH 金鑰和 tooadd hello SSH 金鑰 toohello 裝載 hello 儲存機制的 GitHub 帳戶所提供的指示。
        * 執行 hello 上述連結 hello Jenkins Docker 命令介面中 （且不在主機上） 中所述的 hello 命令。
      * toosign 中 toohello Jenkins 殼層，從您的主機使用 hello 下列命令：

      ```sh
      docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
      ```

請確定該 hello 叢集或其中 hello Jenkins 容器映像裝載具有公開 IP 的機器。 這可讓從 GitHub hello Jenkins 執行個體 tooreceive 通知。

## <a name="install-hello-service-fabric-jenkins-plug-in-from-hello-portal"></a>從 hello 入口網站安裝 hello 服務網狀架構 Jenkins 外掛程式

1. 跳過``http://PublicIPorFQDN:8081``
2. 從 hello Jenkins 儀表板中，選取**管理 Jenkins** > **管理外掛程式** > **進階**。
在這裡，您可以上傳外掛程式。 選取**選擇檔案**，然後選取 hello **serviceFabric.hpi**必要條件下您下載的檔案。 當您選取**上傳**，Jenkins 會自動安裝外掛程式的 hello。 在系統要求時允許重新啟動。

## <a name="create-and-configure-a-jenkins-job"></a>建立及設定 Jenkins 作業

1. 從儀表板建立**新項目**。
2. 輸入項目名稱 (例如，**MyJob**)。 選取 [自由樣式專案]，然後按一下 [確定]。
3. 移 hello 作業] 頁面上，然後按一下 [**設定**。

   a. 在 hello 一般區段中，在**GitHub 專案**，指定您的 GitHub 專案 URL。 此 URL 主機 hello 服務網狀架構 Java 應用程式想要以 hello Jenkins 連續整合 toointegrate，(CI/CD) 進行持續部署流程 (例如， ``https://github.com/sayantancs/SFJenkins``)。

   b. 在 hello**原始程式碼管理**區段中，選取**Git**。 指定裝載您要以 hello Jenkins CI/CD 流程 toointegrate hello 服務網狀架構 Java 應用程式的 hello 儲存機制 URL (例如， ``https://github.com/sayantancs/SFJenkins.git``)。 此外，您可以在此處指定的分支 toobuild (例如， **/master**)。
4. 設定您*GitHub* （其中主控 hello 儲存機制），以便能夠 tootalk tooJenkins。 使用下列步驟的 hello:

   a. 移至 tooyour GitHub 儲存機制頁面。 跳過**設定** > **整合和服務**。

   b. 選取**加入服務**，型別**Jenkins**，並選取 hello **Jenkins GitHub 外掛程式**。

   c. 輸入您的 Jenkins webhook URL (根據預設，它應該是 ``http://<PublicIPorFQDN>:8081/github-webhook/``)。 按一下 [新增/更新服務]。

   d. 測試事件會傳送 tooyour Jenkins 執行個體。 您應該查看在 GitHub 中的 hello webhook 綠色的核取，並建置專案。

   e. 在 hello**組建觸發程序**區段中，選取哪一個建置您想要的選項。 例如，您想 tootrigger 組建，每當發生某些發送 toohello 儲存機制時。 因此，您選取 [GITScm 輪詢的 GitHub 攔截觸發程序]。 (此選項之前，呼叫**建置時變更推入 tooGitHub**。)

   f. 在 hello**建立區段**，從 hello 下拉式清單**加入建置步驟**，選取 hello 選項**叫用 Gradle 指令碼**。 在出現 hello widget 中，指定 hello 路徑太**根建置指令碼**應用程式。 它會拾取 build.gradle hello 路徑指定，從，並據此運作。 如果您建立專案，名為``MyActor``（使用 hello Eclipse 外掛程式或 Yeoman 產生器），hello 根組建指令碼應包含``${WORKSPACE}/MyActor``。 請參閱下列的這好像範例的螢幕擷取畫面的 hello:

    ![Service Fabric Jenkins 建置動作][build-step]

   g. 從 hello**建置後動作**下拉式清單中，選取**部署 Service Fabric 專案**。 您需要在這裡 tooprovide 叢集將部署的 hello Jenkins 已編譯之 Service Fabric 應用程式的詳細資料。 您也可以提供使用 toodeploy hello 應用程式的其他應用程式詳細資料。 請參閱下列的這好像範例的螢幕擷取畫面的 hello:

    ![Service Fabric Jenkins 建置動作][post-build-step]

   > [!NOTE]
   > 如果您使用 Service Fabric toodeploy hello Jenkins 容器映像，可能是與 hello 一個裝載 hello Jenkins 容器應用程式，相同 hello 叢集中。
   >

## <a name="next-steps"></a>後續步驟
現在已設定 GitHub 和 Jenkins。 請考慮進行一些樣本，以變更您``MyActor``在 hello 儲存機制範例中，專案 https://github.com/sayantancs/SFJenkins。 推送變更 tooa 遠端``master``分支 （或您已設定 toowork 與任何分支）。 這會觸發 hello Jenkins 作業， ``MyJob``，在您的設定。 從 GitHub 提取 hello 變更、 建立它們，和部署您在建置後動作中指定的 hello 應用程式 toohello 叢集端點。  

  <!-- Images -->
  [build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/build-step.png
  [post-build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/post-build-step.png

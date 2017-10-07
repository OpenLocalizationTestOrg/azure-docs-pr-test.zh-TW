---
title: "aaaCI/CD 與 Azure 容器服務引擎廣域模式 |Microsoft 文件"
description: "Docker Swarm 模式、 Azure 容器登錄中，而且 Visual Studio Team Services toodeliver 持續多容器.NET Core 應用程式搭配使用 Azure 容器服務引擎"
services: container-service
documentationcenter: " "
author: diegomrtnzg
manager: esterdnb
tags: acs, azure-container-service, acs-engine
keywords: "Docker, 容器, 微服務, Swarm, Azure, Visual Studio Team Services, DevOps, ACS 引擎"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 040522c452f7ea0ce3c92f2fe57b1c141b97e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a>完整的 CI/CD 管線 toodeploy 多容器上的應用程式與 ACS 引擎使用 Visual Studio Team Services 的 Docker Swarm 模式 Azure 容器服務

*這篇文章根據[完整的 CI CD 管線 toodeploy 多容器上的應用程式與使用 Visual Studio Team Services 的 Docker Swarm Azure 容器服務](container-service-docker-swarm-setup-ci-cd.md)文件*

Screen 鍵，其中一個 hello 最大的挑戰時開發 hello 雲端的現代應用程式可以 toodeliver 這些應用程式持續。 在本文中，您會學習如何 tooimplement 完整連續整合和部署 (CI/CD) 管線使用： 
* 使用 Docker Swarm 模式的 Azure Container Service 引擎
* Azure Container Registry
* Visual Studio Team Services

本文是以一個使用 ASP.NET Core 開發的簡單應用程式 (可在 [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux) 上取得) 為依據。 hello 應用程式由四個不同的服務所組成： 三個 web 應用程式開發介面和一個 web 前端：

![MyShop 範例應用程式](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

hello 目標是 toodeliver 持續在 Docker Swarm 模式叢集中，使用 Visual Studio Team Services 的這個應用程式。 hello 下列圖這個連續的傳送管線的詳細資料：

![MyShop 範例應用程式](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

以下是 hello 步驟的簡短說明：

1. 程式碼變更都會認可的 toohello 原始程式碼儲存機制 （此處 GitHub） 
2. GitHub 觸發 Visual Studio Team Services 中的組建 
3. Visual Studio Team Services 取得 hello 的 hello 來源的最新版本，並建置撰寫 hello 應用程式的所有 hello 映像 
4. Visual Studio Team Services 推播通知使用 hello Azure 容器登錄服務所建立的每個映像 tooa Docker 登錄 
5. Visual Studio Team Services 觸發新版本 
6. hello 版本執行 hello Azure 容器服務叢集主機節點上使用 SSH 一些命令 
7. Hello 叢集上的 docker Swarm 模式會提取 hello hello 映像的最新版本 
8. hello hello 應用程式被部署新版使用 Docker 堆疊 

## <a name="prerequisites"></a>必要條件

開始之前本教學課程，您需要 toocomplete hello 下列工作：

- [使用 ACS 引擎在 Azure Container Service 中建立 Swarm 模式叢集](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [連接與 Azure 容器服務中的 hello 群集叢集](../container-service-connect.md)
- [建立 Azure 容器登錄](../../container-registry/container-registry-get-started-portal.md)
- [建立 Visual Studio Team Services 帳戶以及 Team 專案 (英文)](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [分岔 hello GitHub 儲存機制 tooyour GitHub 帳戶](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> 在 Azure 容器服務中的 hello Docker Swarm orchestrator 會使用舊版獨立群集。 目前，hello 整合[群集模式](https://docs.docker.com/engine/swarm/)（Docker 1.12 （含） 以上） 不是在 Azure 容器服務中的支援的 orchestrator。 基於這個理由，我們使用[ACS 引擎](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md)，社群貢獻[快速入門範本](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/)，或在 hello Docker 方案[Azure Marketplace](https://azuremarketplace.microsoft.com)。
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>步驟 1：設定 Visual Studio Team Services 帳戶 

在本節中，您會設定您的 Visual Studio Team Services 帳戶。 tooconfigure VSTS 服務端點，在 Visual Studio Team Services 專案中，按一下 hello**設定**hello 工具列上，然後選取圖示**服務**。

![開啟服務端點](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a>連接 Visual Studio Team Services 與 Azure 帳戶

設定 VSTS 專案與 Azure 帳戶之間的連線。

1. Hello 左側，按一下 **新的服務端點** > **Azure Resource Manager**。
2. tooauthorize VSTS toowork 與 Azure 帳戶，選取您**訂用帳戶**按一下**確定**。

    ![Visual Studio Team Services - 授權 Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a>將 Visual Studio Team Services 與 GitHub 連線

設定您的 VSTS 專案與 GitHub 帳戶之間的連線。

1. Hello 左側，按一下 **新的服務端點** > **GitHub**。
2. 按一下與您的 GitHub 帳戶 tooauthorize VSTS toowork**授權**遵循 hello hello 開啟的視窗中的程序。

    ![Visual Studio Team Services - 授權 GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-tooyour-azure-container-service-cluster"></a>VSTS tooyour Azure 容器服務叢集連線

hello hello CI/CD 管線之前的最後一個步驟是 tooconfigure 外部連接 tooyour Docker Swarm Azure 中的叢集。 

1. Hello Docker Swarm 叢集中，將端點的型別加入**SSH**。 然後輸入 hello SSH 連接資訊的群集叢集 （主要節點）。

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

所有的 hello 組態是立即完成。 在 hello 下一個步驟中，您可以建立組建和部署 hello 應用程式 toohello Docker Swarm 叢集 hello CI/CD 管線。 

## <a name="step-2-create-hello-build-definition"></a>步驟 2： 建立 hello 組建定義

在此步驟中，設定 VSTS 專案的組建定義和定義 hello 組建工作流程的容器映像

### <a name="initial-definition-setup"></a>初始定義設定

1. toocreate 組建定義中，連接 Visual Studio Team Services 專案，然後按一下的 tooyour**建置和發行**。 在 hello**組建定義**區段中，按一下**+ 新增**。 

    ![Visual Studio Team Services - 新增組建定義](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. 選取 hello**清空處理序**。

    ![Visual Studio Team Services - 新增空白的組建定義](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. 然後，按一下 hello**變數**索引標籤，然後建立兩個新的變數： **RegistryURL**和**AgentURL**。 貼上您登錄與叢集代理程式的 DNS hello 值。

    ![Visual Studio Team Services - 組建變數設定](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. 在 [hello**組建定義**頁面上，開啟 hello**觸發程序**索引標籤，然後設定與您建立在 hello prerequisites] 中的 hello MyShop 專案 hello 分岔 hello 組建 toouse 連續整合。 接著，選取 [批次變更]。 請確定您選取*docker linux*為 hello**分支規格**。

    ![Visual Studio Team Services - 組建存放庫組態](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. 最後，按一下 hello**選項**索引標籤，設定 hello 預設代理程式佇列太**裝載的 Linux 預覽**。

    ![Visual Studio Team Services - 主機代理程式設定](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-hello-build-workflow"></a>定義 hello 組建工作流程
hello 接下來的步驟定義 hello 組建工作流程。 首先，您需要 tooconfigure hello 來源 hello 程式碼。 toodo 它，選取**GitHub**和您**儲存機制**和**分支**(docker linux)。

![Visual Studio Team Services - 設定程式碼來源](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

有五個容器映像 toobuild hello *MyShop*應用程式。 每個映像的建立使用 Dockerfile 位於 hello 專案資料夾中的 hello:

* ProductsApi
* Proxy
* RatingsApi
* RecommandationsApi
* ShopFront

您需要每個映像的兩個 Docker 步驟、 一個 toobuild hello 影像和 hello Azure 容器登錄中的一個 toopush hello 映像。 

1. 按一下 tooadd hello 組建工作流程中的步驟**+ 加入建置步驟**選取**Docker**。

    ![Visual Studio Team Services - 新增建置步驟](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. 每個映像，設定一個步驟，來使用 hello`docker build`命令。

    ![Visual Studio Team Services - Docker 建置](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    Hello 建置作業中，選取您的 Azure 容器登錄 hello**建置的映像**動作和 hello 定義每個映像的 Dockerfile。 設定 hello**工作目錄**hello Dockerfile 根目錄中，定義 hello**映像名稱**，然後選取**包含最新的標籤**。
    
    hello 映像名稱具有 toobe 格式如下： ```$(RegistryURL)/[NAME]:$(Build.BuildId)```。 取代**[NAME]** hello 映像名稱：
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. 每個映像，設定 第二個步驟使用 hello`docker push`命令。

    ![Visual Studio Team Services - Docker 推送](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    Hello 推入作業中，選取您的 Azure 容器登錄 hello**推入映像**動作中，輸入 hello**映像名稱**hello 上一個步驟並選取內建**包含最新的標籤**.

4. 之後您設定 hello 組建和 push hello 五個映像的每個步驟，加入三個步驟詳細 hello 組建工作流程。

   ![Visual Studio Team Services - 新增命令列工作](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. 使用 bash 指令碼 tooreplace hello 的命令列工作*RegistryURL* hello RegistryURL 變數 hello docker compose.yml 檔案中的項目。 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services - 使用登錄 URL 更新 Compose 檔案](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. 使用 bash 指令碼 tooreplace hello 的命令列工作*AgentURL* hello AgentURL 變數 hello docker compose.yml 檔案中的項目。
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. 卸除 hello 工作更新組建成品撰寫檔案，所以用於 hello 版本。 請參閱下列詳細資料螢幕的 hello。

         ![Visual Studio Team Services - 發佈構件](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services - 發佈 Compose 檔案](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. 按一下**儲存，並佇列**tootest 組建定義。

   ![Visual Studio Team Services - 儲存並排入佇列](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services - 新增佇列](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. 如果 hello**建置**是否正確，您有 toosee 這個畫面：

  ![Visual Studio Team Services - 建置成功](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-hello-release-definition"></a>步驟 3： 建立 hello 發行定義

Visual Studio Team Services 可讓您太[的環境中管理發行](https://www.visualstudio.com/team-services/release-management/)。 您可以啟用連續部署 toomake 確定您的應用程式部署在不同環境 （例如開發、 測試、 生產階段前及生產），以平滑的方式。 您可以建立代表 Azure Container Service Docker Swarm 模式叢集的環境。

![Visual Studio Team Services 的版本 tooACS](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>初始發行設定

1. toocreate 發行定義中，按一下**版本** > **+ 版本**

2. tooconfigure hello 成品來源，按一下**成品** > **連結成品來源**。 在這裡，連結此新發行定義 toohello 組建在 hello 上一個步驟中所定義。 在這之後，hello docker compose.yml 檔案位於 hello 發行程序。

    ![Visual Studio Team Services - 發行構件](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. tooconfigure hello 釋放觸發程序，按一下 **觸發程序**選取**連續部署**。 Hello hello 組觸發程序相同的成品來源。 此設定可確保 hello 組建已成功完成時，會啟動新的版本。

    ![Visual Studio Team Services - 發行觸發程序](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. tooconfigure hello 發行變數，按一下**變數**選取**+ 變數**toocreate 三個新的變數與 hello hello 登錄資訊： **docker.username**，**docker.password**，和**docker.registry**。 貼上您登錄與叢集代理程式的 DNS hello 值。

    ![Visual Studio Team Services - 組建存放庫組態](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > 顯示 hello 上一個畫面中，按一下 hello**鎖定**docker.password 中的核取方塊。 這項設定是很重要的 toorestrict hello 密碼。
    >

### <a name="define-hello-release-workflow"></a>定義 hello 發行工作流程

hello 發行工作流程是由您加入的兩個工作所組成。

1. 設定工作 toosecurely 複製 hello 撰寫檔案 tooa*部署*hello Docker Swarm 主要節點上，使用您先前設定的 hello SSH 連線的資料夾。 請參閱下列詳細資料螢幕的 hello。
    
    來源資料夾：```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```

    ![Visual Studio Team Services - 發行 SCP](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. 設定第二個工作 tooexecute bash 指令 toorun`docker`和`docker stack deploy`hello 主要節點上的命令。 請參閱下列詳細資料螢幕的 hello。

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services - 發行 Bash](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    hello hello 主機上執行的命令會使用 hello Docker CLI 和 hello Docker Compose CLI toodo hello 下列工作：

    - 登入 toohello Azure 容器登錄中 (它會使用三個 hello 中所定義的組建變數**變數** 索引標籤)
    - 定義 hello **DOCKER_HOST**變數 toowork 與 hello 群集端點 (: 2375年)
    - 瀏覽 toohello*部署*hello 前面安全複製工作所建立，並包含 hello docker compose.yml 檔案的資料夾 
    - 執行`docker stack deploy`提取 hello 新映像，並建立 hello 容器的命令。

    >[!IMPORTANT]
    > 如下所示 hello 上一個畫面，讓 hello**失敗 STDERR 上**未核取核取方塊。 此設定可讓我們 toocomplete hello 發行程序，因為太`docker-compose`會列印數診斷訊息，例如容器會停止中或正在刪除，hello 標準錯誤輸出上。 如果您檢查 hello 核取方塊時，Visual Studio Team Services 報告錯誤時發生 hello 版本中，即使一切順利。
    >
3. 儲存這個新的發行定義。

## <a name="step-4-test-hello-cicd-pipeline"></a>步驟 4： 測試 hello CI/CD 管線

既然您以 hello 組態完成之後，它是這個新的時間 tootest CI/CD 管線。 hello tooupdate hello 來源的程式碼和 commit hello 是最簡單方式 tootest 變更為您的 GitHub 儲存機制。 幾秒後就是您推送 hello 程式碼中，您會看到新的組建，在 Visual Studio Team Services 中執行。 順利完成後，會觸發新的版本，並部署 hello hello hello Azure 容器服務的叢集上的應用程式的新版本。

## <a name="next-steps"></a>後續步驟

* 如需使用 Visual Studio Team Services 的 CI/CD 的詳細資訊，請參閱 hello [VSTS 建置概觀](https://www.visualstudio.com/docs/build/overview)。
* 如需 ACS 引擎的詳細資訊，請參閱 hello [ACS 引擎 GitHub 儲存機制](https://github.com/Azure/acs-engine)。
* 如需有關 Docker Swarm 模式的詳細資訊，請參閱 hello [Docker Swarm 模式概觀](https://docs.docker.com/engine/swarm/)。

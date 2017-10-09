---
title: "aaaCI/CD 群集與 Azure 容器服務 |Microsoft 文件"
description: "Docker Swarm、 Azure 容器登錄中，而且 Visual Studio Team Services toodeliver 持續多容器.NET Core 應用程式搭配使用 Azure 容器服務"
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: "Docker, Containers, Micro-services, Swarm, Azure, Visual Studio Team Services, DevOps, 容器, 微型服務"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 35348800aa620469fb62ab3e5a02b33834359446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a>完整的 CI/CD 管線 toodeploy 多容器上的應用程式與使用 Visual Studio Team Services 的 Docker Swarm Azure 容器服務

其中一個 hello 最大的挑戰時開發 hello 雲端的現代應用程式可以 toodeliver 這些應用程式持續。 在本文中，您會了解 tooimplement 完整連續整合和部署 (CI/CD) 管線 Docker Swarm、 與 Azure 容器登錄中，Visual Studio Team Services 中使用 Azure 容器服務的建置，以及發行管理。

本文是以一個使用 ASP.NET Core 開發的簡單應用程式 (可在 [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs) 上取得) 為依據。 hello 應用程式由四個不同的服務所組成： 三個 web 應用程式開發介面和一個 web 前端：

![MyShop 範例應用程式](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

hello 目標是 toodeliver 持續在 Docker Swarm 叢集中，使用 Visual Studio Team Services 的這個應用程式。 hello 下列圖這個連續的傳送管線的詳細資料：

![MyShop 範例應用程式](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

以下是 hello 步驟的簡短說明：

1. 程式碼變更都會認可的 toohello 原始程式碼儲存機制 （此處 GitHub） 
2. GitHub 觸發 Visual Studio Team Services 中的組建 
3. Visual Studio Team Services 取得 hello 的 hello 來源的最新版本，並建置撰寫 hello 應用程式的所有 hello 映像 
4. Visual Studio Team Services 推播通知使用 hello Azure 容器登錄服務所建立的每個映像 tooa Docker 登錄 
5. Visual Studio Team Services 觸發新版本 
6. hello 版本執行 hello Azure 容器服務叢集主機節點上使用 SSH 一些命令 
7. Hello 叢集提取 hello 最新版本的 hello 映像上的 docker 群集 
8. 使用 Docker Compose 部署 hello 新版 hello 應用程式 

## <a name="prerequisites"></a>必要條件

開始之前本教學課程，您需要 toocomplete hello 下列工作：

- [在 Azure 容器服務中建立 Swarm 叢集](container-service-deployment.md)
- [連接與 Azure 容器服務中的 hello 群集叢集](../container-service-connect.md)
- [建立 Azure 容器登錄](../../container-registry/container-registry-get-started-portal.md)
- [建立 Visual Studio Team Services 帳戶以及 Team 專案 (英文)](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [分岔 hello GitHub 儲存機制 tooyour GitHub 帳戶](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

您也需要已經安裝 Docker 的 Ubuntu (14.04 or 16.04) 機器。 使用這部電腦是由 Visual Studio Team Services 在 hello 期間建立及發佈程序。 其中一種方式 toocreate 這台電腦是 toouse hello 映像可在 hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/)。 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>步驟 1：設定 Visual Studio Team Services 帳戶 

在本節中，您會設定您的 Visual Studio Team Services 帳戶。

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a>設定 Visual Studio Team Services Linux 組件代理程式

toocreate Docker 映像並推送建置到 Visual Studio Team Services 從 Azure 容器登錄這些映像，您會需要 tooregister Linux 代理程式。 安裝選項如下：

* [在 Linux 上部署代理程式 (英文)](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [使用 Docker toorun hello VSTS 代理程式](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-hello-docker-integration-vsts-extension"></a>安裝 hello Docker 整合 VSTS 擴充功能

Microsoft 提供 VSTS 延伸 toowork 使用 Docker 在組建中的，並釋放處理程序。 這個延伸可用於 hello [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker)。 按一下**安裝**tooadd 此延伸模組 tooyour VSTS 帳戶：

![安裝 hello Docker 整合](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

系統會要求您使用您的認證 tooconnect tooyour VSTS 帳戶。 

### <a name="connect-visual-studio-team-services-and-github"></a>將 Visual Studio Team Services 與 GitHub 連線

設定您的 VSTS 專案與 GitHub 帳戶之間的連線。

1. 在 Visual Studio Team Services 專案中，按一下 hello**設定**hello 工具列上，然後選取圖示**服務**。

    ![Visual Studio Team Services - 外部連線](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. Hello 左側，按一下 **新的服務端點** > **GitHub**。

    ![Visual Studio Team Services - GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. 按一下與您的 GitHub 帳戶 tooauthorize VSTS toowork**授權**遵循 hello hello 開啟的視窗中的程序。

    ![Visual Studio Team Services - 授權 GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-tooyour-azure-container-registry-and-azure-container-service-cluster"></a>連接 Azure 容器登錄中 VSTS tooyour 和 Azure 容器服務的叢集

hello hello CI/CD 管線之前的最後一個步驟是 tooconfigure 外部連接 tooyour 容器登錄中和在 Azure 中您 Docker Swarm 的叢集。 

1. 在 hello**服務**設定您的 Visual Studio Team Services 專案，加入服務端點的型別**Docker 登錄**。 

2. 在 hello 快顯視窗開啟，輸入 hello URL 和 Azure 容器登錄 hello 認證。

    ![Visual Studio Team Services - Docker 登錄](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. Hello Docker Swarm 叢集中，將端點的型別加入**SSH**。 然後輸入 hello SSH 連接資訊的群集叢集。

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

所有的 hello 組態是立即完成。 在 hello 下一個步驟中，您可以建立組建和部署 hello 應用程式 toohello Docker Swarm 叢集 hello CI/CD 管線。 

## <a name="step-2-create-hello-build-definition"></a>步驟 2： 建立 hello 組建定義

在此步驟中，您需要設定組建 definitionfor VSTS 專案並 hello 組建工作流程定義您的容器映像

### <a name="initial-definition-setup"></a>初始定義設定

1. toocreate 組建定義中，連接 Visual Studio Team Services 專案，然後按一下的 tooyour**建置和發行**。 

2. 在 hello**組建定義**區段中，按一下**+ 新增**。 選取 hello**空**範本。

    ![Visual Studio Team Services - 新增組建定義](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. 設定新組建的 hello 與 GitHub 儲存機制來源，核取**連續整合**，和您用來註冊您的 Linux 代理程式選取 hello 代理程式佇列。 按一下**建立**toocreate hello 組建定義。

    ![Visual Studio Team Services - 建立組建定義](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. 在 hello**組建定義**頁面上，第一次開啟 hello**儲存機制**索引標籤，設定 hello 組建 toouse hello 分岔 hello MyShop 專案在 hello 必要條件中所建立。 請確定您選取*acs 文件*為 hello**預設分支**。

    ![Visual Studio Team Services - 組建存放庫組態](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. 在 hello**觸發程序**索引標籤上，設定 hello 組建 toobe 每次認可之後觸發。 選取 [持續整合] 和 [批次變更]。

    ![Visual Studio Team Services - 組建觸發組態](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-hello-build-workflow"></a>定義 hello 組建工作流程
hello 接下來的步驟定義 hello 組建工作流程。 有五個容器映像 toobuild hello *MyShop*應用程式。 每個映像的建立使用 Dockerfile 位於 hello 專案資料夾中的 hello:

* ProductsApi
* Proxy
* RatingsApi
* RecommandationsApi
* ShopFront

您需要每個映像 tooadd 兩個 Docker 步驟、 一個 toobuild hello 影像和 hello Azure 容器登錄中的一個 toopush hello 映像。 

1. 按一下 tooadd hello 組建工作流程中的步驟**+ 加入建置步驟**選取**Docker**。

    ![Visual Studio Team Services - 新增建置步驟](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. 每個映像，設定一個步驟，來使用 hello`docker build`命令。

    ![Visual Studio Team Services - Docker 建置](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    Hello 建置作業中，選取您的 Azure 容器登錄 hello**建置的映像**動作和 hello 定義每個映像的 Dockerfile。 設定 hello**建置內容**hello Dockerfile 為根目錄，並定義 hello**映像名稱**。 
    
    如下所示 hello 前面螢幕，hello 映像名稱開頭 hello Azure 容器登錄的 URI。 （您也可以使用組建變數 tooparameterize hello 標記 hello 映像，例如在此範例中的 hello 組建識別項）。

3. 每個映像，設定 第二個步驟使用 hello`docker push`命令。

    ![Visual Studio Team Services - Docker 推送](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    Hello 推入作業中，選取您的 Azure 容器登錄 hello**推入映像**動作，然後輸入 hello**映像名稱**hello 上一個步驟中內建。

4. 之後您設定 hello 組建和 push hello 五個映像的每個步驟，加入兩個步驟，在 hello 組建工作流程。

    a. 使用 bash 指令碼 tooreplace hello 的命令列工作*BuildNumber* hello 目前 hello docker compose.yml 檔案中的項目建立的識別碼。請參閱下列詳細資料螢幕的 hello。

    ![Visual Studio Team Services - 更新 Compose 檔案](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    b. 卸除 hello 工作更新組建成品撰寫檔案，所以用於 hello 版本。 請參閱下列詳細資料螢幕的 hello。

    ![Visual Studio Team Services - 發佈 Compose 檔案](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. 按一下 [儲存] 並命名您的組建定義。

## <a name="step-3-create-hello-release-definition"></a>步驟 3： 建立 hello 發行定義

Visual Studio Team Services 可讓您太[的環境中管理發行](https://www.visualstudio.com/team-services/release-management/)。 您可以啟用連續部署 toomake 確定您的應用程式部署在不同環境 （例如開發、 測試、 生產階段前及生產），以平滑的方式。 您可以建立代表 Azure Container Service Docker Swarm 叢集的新環境。

![Visual Studio Team Services 的版本 tooACS](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>初始發行設定

1. toocreate 發行定義中，按一下**版本** > **+ 版本**

2. tooconfigure hello 成品來源，按一下**成品** > **連結成品來源**。 在這裡，連結此新發行定義 toohello 組建在 hello 上一個步驟中所定義。 如此一來，hello docker compose.yml 檔案可在 hello 發行程序。

    ![Visual Studio Team Services - 發行構件](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. tooconfigure hello 釋放觸發程序，按一下 **觸發程序**選取**連續部署**。 Hello hello 組觸發程序相同的成品來源。 此設定可確保新的版本會在 hello 建置成功完成時立即啟動。

    ![Visual Studio Team Services - 發行觸發程序](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-hello-release-workflow"></a>定義 hello 發行工作流程

hello 發行工作流程是由您加入的兩個工作所組成。

1. 設定工作 toosecurely 複製 hello 撰寫檔案 tooa*部署*hello Docker Swarm 主要節點上，使用您先前設定的 hello SSH 連線的資料夾。 請參閱下列詳細資料螢幕的 hello。

    ![Visual Studio Team Services - 發行 SCP](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. 設定第二個工作 tooexecute bash 指令 toorun`docker`和`docker-compose`hello 主要節點上的命令。 請參閱下列詳細資料螢幕的 hello。

    ![Visual Studio Team Services - 發行 Bash](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    hello hello 主要使用 hello Docker CLI 和 hello Docker Compose CLI toodo hello 下列工作上執行的命令：

    - 登入 toohello Azure 容器登錄中 (它會使用三個 hello 中所定義的組建 variab'les**變數** 索引標籤)
    - 定義 hello **DOCKER_HOST**變數 toowork 與 hello 群集端點 (: 2375年)
    - 瀏覽 toohello*部署*hello 前面安全複製工作所建立，並包含 hello docker compose.yml 檔案的資料夾 
    - 執行`docker-compose`提取 hello 新映像的命令停止 hello 服務、 移除 hello 服務，以及建立 hello 容器。

    >[!IMPORTANT]
    > Hello 前面螢幕上所示，將保留 hello**失敗 STDERR 上**未核取核取方塊。 這是重要設定，因為`docker-compose`會列印數診斷訊息，例如容器會停止中或正在刪除，hello 標準錯誤輸出上。 如果您檢查 hello 核取方塊時，Visual Studio Team Services 報告錯誤時發生 hello 版本中，即使一切順利。
    >
3. 儲存這個新的發行定義。


>[!NOTE]
>此部署包含一些停機時間，因為我們會停止 hello 舊服務並執行新的 hello。 它是可能 tooavoid 這執行藍綠色部署。
>

## <a name="step-4-test-hello-cicd-pipeline"></a>步驟 4. 測試 hello CI/CD 管線

既然您以 hello 組態完成之後，它是這個新的時間 tootest CI/CD 管線。 hello tooupdate hello 來源的程式碼和 commit hello 是最簡單方式 tootest 變更為您的 GitHub 儲存機制。 幾秒後就是您推送 hello 程式碼中，您會看到新的組建，在 Visual Studio Team Services 中執行。 順利完成後，新的版本會將觸發，因此將會部署 hello hello hello Azure 容器服務的叢集上的應用程式的新版本。

## <a name="next-steps"></a>後續步驟

* 如需使用 Visual Studio Team Services 的 CI/CD 的詳細資訊，請參閱 hello [VSTS 建置概觀](https://www.visualstudio.com/docs/build/overview)。

---
title: "aaaCreate jenkins Azure 中開發管線 |Microsoft 文件"
description: "了解如何 toocreate Jenkins 虛擬機器中的每個程式碼從 GitHub 提取認可，並建立新的 Docker 容器 toorun Azure 應用程式"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c079e3c9186c9da0a3e51e1823215779c565e0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a>如何 toocreate Jenkins、 GitHub、 與 Docker 的 Azure 中 Linux VM 上開發基礎結構
tooautomate hello 組建和測試階段的應用程式開發，您可以使用持續整合和部署 (CI/CD) 管線。 在本教學課程中，您會在 Azure VM 上建立 CI/CD 管線，包括如何︰

> [!div class="checklist"]
> * 建立 Jenkins VM
> * 安裝並設定 Jenkins
> * 建立 GitHub 與 Jenkins 之間的 webhook 整合
> * 從 GitHub 認可建立並觸發 Jenkins 組建作業
> * 建立應用程式的 Docker 映像
> * 確認 GitHub 已認可組建的新 Docker 映像，並更新了執行中的應用程式


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="create-jenkins-instance"></a>建立 Jenkins 執行個體
在上一個教學課程中[如何 toocustomize Linux 虛擬機器第一次開機](tutorial-automate-vm-deployment.md)，您學到如何使用雲端 init tooautomate VM 自訂。 本教學課程會使用雲端 init 檔案 tooinstall Jenkins 和 Docker VM 上。 

您目前的殼層中建立名為*雲端 init.txt*和 hello 貼上下列組態。 例如，在 hello 雲端 Shell 不在您本機電腦上建立 hello 檔案。 輸入`sensible-editor cloud-init-jenkins.txt`toocreate hello 檔案，並查看一份可用的編輯器。 請確定已正確複製該 hello 整個雲端初始化檔案，特別是 hello 第一行：

```yaml
#cloud-config
package_upgrade: true
write_files:
  - path: /etc/systemd/system/docker.service.d/docker.conf
    content: |
      [Service]
        ExecStart=
        ExecStart=/usr/bin/dockerd
  - path: /etc/docker/daemon.json
    content: |
      {
        "hosts": ["fd://","tcp://127.0.0.1:2375"]
      }
runcmd:
  - wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
  - sh -c 'echo deb http://pkg.jenkins-ci.org/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
  - apt-get update && apt-get install jenkins -y
  - curl -sSL https://get.docker.com/ | sh
  - usermod -aG docker azureuser
  - usermod -aG docker jenkins
  - service jenkins restart
```

建立 VM 之前，請先使用 [az group create](/cli/azure/group#create) 來建立資源群組。 hello 下列範例會建立名為的資源群組*myResourceGroupJenkins*在 hello *eastus*位置：

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

現在，使用 [az vm create](/cli/azure/vm#create) 建立 VM。 使用 hello`--custom-data`參數 toopass 雲端 init 組態檔中的。 提供完整路徑，hello 太*雲端-init-jenkins.txt*如果 hello 檔案儲存目前的工作目錄之外。

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

花幾分鐘，讓 hello VM toobe 建立及設定。

tooallow web 流量 tooreach 您的 VM 使用[az vm 開啟通訊埠](/cli/azure/vm#open-port)tooopen 連接埠*8080* Jenkins 流量和連接埠*1337年*hello Node.js 應用程式所使用的 toorun 範例應用程式：

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a>設定 Jenkins
tooaccess 您 Jenkins 執行個體，取得您的 VM hello 公用 IP 位址：

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

基於安全性目的，您需要 tooenter hello 初始管理密碼儲存在您 VM toostart hello Jenkins 安裝上的文字檔案。 使用 hello 在上一個步驟 tooSSH tooyour hello VM 中取得公用 IP 位址：

```bash
ssh azureuser@<publicIps>
```

檢視 hello`initialAdminPassword`您 Jenkins 安裝，並將它複製：

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

如果還沒有 hello 檔案，等候幾分鐘，雲端 init toocomplete hello Jenkins 和 Docker 安裝。

現在開啟網頁瀏覽器並移過`http://<publicIps>:8080`。 完成初始 Jenkins 設定 hello，如下所示：

- 輸入 hello *initialAdminPassword*取自 hello 上一個步驟中的 hello VM。
- 按一下**選取外掛程式 tooinstall**
- 搜尋*GitHub* hello hello 頂端的文字方塊中，選取 hello *GitHub 外掛程式*，然後按一下 **安裝**
- toocreate Jenkins 使用者帳戶，填寫所需的 hello 形式。 從安全性觀點來看，您應該建立第一個 Jenkins 使用者，而不是為 hello 預設管理員帳戶繼續進行。
- 完成後，按一下 [開始使用 Jenkins]


## <a name="create-github-webhook"></a>建立 GitHub webhook
tooconfigure hello 整合與 GitHub，開啟 hello [Node.js Hello World 範例應用程式](https://github.com/Azure-Samples/nodejs-docs-hello-world)從 hello Azure 範例儲存機制。 toofork hello 儲存機制 tooyour 擁有 GitHub 帳戶，請按一下 hello**分岔**hello 右上角中的按鈕。

建立 webhook 內所建立的 hello 分岔：

- 按一下**設定**，然後選取**整合與服務**左側為 hello。
- 按一下 [新增服務]，在篩選方塊中輸入 Jenkins。
- 選取 [Jenkins (GitHub 外掛程式)]
- Hello **Jenkins 連接 URL**，輸入`http://<publicIps>:8080/github-webhook/`。 請確定您包含結尾的 hello /
- 按一下 [新增服務]。

![新增 GitHub webhook tooyour 分叉儲存機制](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a>建立 Jenkins 作業
toohave Jenkins 回應 tooan 事件在 GitHub 中認可的程式碼，例如建立 Jenkins 作業。 

在您 Jenkins 的網站，按一下**建立新的作業**hello 首頁上：

- 輸入 HelloWorld 作為作業名稱。 選擇 [自由樣式專案]，然後選取 [確定]。
- 在 hello**一般**區段中，選取**GitHub**專案，並輸入您分岔的儲存機制的 URL，例如*https://github.com/iainfoulds/nodejs-docs-hello-world*
- 在 hello**來源的程式碼管理**區段中，選取**Git**，輸入您分岔的儲存機制*.git* URL，例如*https://github.com/iainfoulds/nodejs-docs-hello-world.git*
- 在 hello**組建觸發程序**區段中，選取**GitHub 勾點觸發程序進行輪詢 GITscm**。
- 在 hello**建置**區段中，選擇**加入建置步驟**。 選取**執行殼層**，然後輸入`echo "Testing"`toocommand 視窗中。
- 按一下**儲存**在 hello hello 工作 視窗的底部。


## <a name="test-github-integration"></a>測試 GitHub 整合
tootest hello GitHub 的整合 jenkins，認可您的 「 分叉 」 中的變更。 

GitHub 中備份 web UI，選取您分岔的儲存機制，然後按一下hello **index.js**檔案。 按一下 hello 鉛筆圖示 tooedit 這個檔案就會讀取第 6 行：

```nodejs
response.end("Hello World!");
```

toocommit 您的變更，按一下 hello**認可變更**hello 底部的按鈕。

Jenkins，在新的組建會開始在 hello**建置記錄**hello 左下角的 [工作] 頁面的區段。 按一下 hello 組建編號] 連結並選取 [**主控台輸出**hello 左側的大小。 您可以檢視您的程式碼取自 GitHub 和 hello 建置動作輸出 hello 訊息當成 Jenkins hello 步驟`Testing`toohello 主控台。 每次認可時就在 GitHub 中 hello webhook 向外連 tooJenkins 並觸發新的組建，以這種方式。


## <a name="define-docker-build-image"></a>定義 Docker 組建映像
toosee hello Node.js 應用程式執行您的 GitHub 認可中的 架構可讓您建立 Docker 映像 toorun hello 應用程式。 hello 映像的建立從 Dockerfile，定義如何 tooconfigure hello 執行 hello 應用程式的容器。 

從 hello SSH 連線 tooyour VM，變更 toohello Jenkins 工作區目錄名為您在上一個步驟中建立的 hello 工作之後。 在我們的範例中命名為 HelloWorld。

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

此工作區的目錄中建立的檔案`sudo sensible-editor Dockerfile`和 hello 貼上下列內容。 請確定該 hello 整個 Dockerfile 會正確複製，特別是 hello 第一行：

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

此 Dockerfile 使用使用 Alpine Linux hello 基底 Node.js 映像，hello Hello World 應用程式的公開連接埠 1337年上，執行，然後複製 hello 應用程式檔案，並將它初始化。


## <a name="create-jenkins-build-rules"></a>建立 Jenkins 組建規則
在上一個步驟中，您可以建立基本的 Jenkins 組建規則輸出訊息 toohello 主控台。 可讓我們 Dockerfile 建立 hello 建置步驟 toouse 和執行 hello 應用程式。

回到您 Jenkins 執行個體中，選取您在上一個步驟中建立的 hello 作業。 按一下**設定**hello 左手邊及捲動 toohello**建置**> 一節：

- 移除現有的 `echo "Test"` 組建步驟。 按一下紅色跨 hello 右上角的 hello 現有的建置步驟方塊上的 hello。
- 按一下 [新增組件步驟]，然後選取 [執行殼層]。
- 在 hello**命令**方塊中，輸入 hello 遵循 Docker 命令，然後選取**儲存**:

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

hello Docker 建置步驟會建立映像和它以 hello Jenkins 組建編號，因此您可以維護映像的歷程記錄的標記。 任何現有的容器執行 hello 應用程式會停止，然後移除。 開始使用 hello 映像，並執行 Node.js 應用程式根據 hello GitHub 中的最新認可，則新的容器。


## <a name="test-your-pipeline"></a>測試您的管線
toosee hello 整個管線在動作中，編輯 hello *index.js*再次檔案分岔的 GitHub 儲存機制中，按一下**認可變更**。 Jenkins 根據 hello webhook GitHub 中，啟動新的工作。 它需要幾秒鐘 toocreate hello Docker 映像並啟動新的容器中的應用程式。

如有需要請再次取得 VM 的 hello 公用 IP 位址：

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

開啟網路瀏覽器，輸入 `http://<publicIps>:1337`。 Node.js 應用程式會顯示，而且會反映出 hello GitHub 分支中的最新認可，如下所示：

![執行 Node.js 應用程式](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

現在讓另一個編輯 toohello *index.js*在 GitHub 和 commit hello 變更的檔案。 等候數秒鐘，讓 hello 作業 toocomplete 中 Jenkins，然後再重新整理您網頁瀏覽器 toosee hello 更新的版本，如下所示的新容器中執行的應用程式：

![在另一次 GitHub 認可後執行 Node.js 應用程式](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a>後續步驟
在本教學課程中，您可以在每個程式碼認可設定 GitHub toorun Jenkins 組建工作，然後再部署 Docker 容器 tootest 您的應用程式。 您已了解如何︰

> [!div class="checklist"]
> * 建立 Jenkins VM
> * 安裝並設定 Jenkins
> * 建立 GitHub 與 Jenkins 之間的 webhook 整合
> * 從 GitHub 認可建立並觸發 Jenkins 組建作業
> * 建立應用程式的 Docker 映像
> * 確認 GitHub 已認可組建的新 Docker 映像，並更新了執行中的應用程式

進一步瞭解前進 toohello 下一個教學課程 toolearn toointegrate Jenkins 與 Visual Studio Team Services。

> [!div class="nextstepaction"]
> [使用 Jenkins 和 Team Services 部署應用程式](tutorial-build-deploy-jenkins.md)
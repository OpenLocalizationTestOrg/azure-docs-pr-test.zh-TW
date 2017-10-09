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
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a><span data-ttu-id="a8619-103">如何 toocreate Jenkins、 GitHub、 與 Docker 的 Azure 中 Linux VM 上開發基礎結構</span><span class="sxs-lookup"><span data-stu-id="a8619-103">How toocreate a development infrastructure on a Linux VM in Azure with Jenkins, GitHub, and Docker</span></span>
<span data-ttu-id="a8619-104">tooautomate hello 組建和測試階段的應用程式開發，您可以使用持續整合和部署 (CI/CD) 管線。</span><span class="sxs-lookup"><span data-stu-id="a8619-104">tooautomate hello build and test phase of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="a8619-105">在本教學課程中，您會在 Azure VM 上建立 CI/CD 管線，包括如何︰</span><span class="sxs-lookup"><span data-stu-id="a8619-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a8619-106">建立 Jenkins VM</span><span class="sxs-lookup"><span data-stu-id="a8619-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="a8619-107">安裝並設定 Jenkins</span><span class="sxs-lookup"><span data-stu-id="a8619-107">Install and configure Jenkins</span></span>
> * <span data-ttu-id="a8619-108">建立 GitHub 與 Jenkins 之間的 webhook 整合</span><span class="sxs-lookup"><span data-stu-id="a8619-108">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="a8619-109">從 GitHub 認可建立並觸發 Jenkins 組建作業</span><span class="sxs-lookup"><span data-stu-id="a8619-109">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="a8619-110">建立應用程式的 Docker 映像</span><span class="sxs-lookup"><span data-stu-id="a8619-110">Create a Docker image for your app</span></span>
> * <span data-ttu-id="a8619-111">確認 GitHub 已認可組建的新 Docker 映像，並更新了執行中的應用程式</span><span class="sxs-lookup"><span data-stu-id="a8619-111">Verify GitHub commits build new Docker image and updates running app</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a8619-112">如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a8619-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a8619-113">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="a8619-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a8619-114">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="a8619-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-jenkins-instance"></a><span data-ttu-id="a8619-115">建立 Jenkins 執行個體</span><span class="sxs-lookup"><span data-stu-id="a8619-115">Create Jenkins instance</span></span>
<span data-ttu-id="a8619-116">在上一個教學課程中[如何 toocustomize Linux 虛擬機器第一次開機](tutorial-automate-vm-deployment.md)，您學到如何使用雲端 init tooautomate VM 自訂。</span><span class="sxs-lookup"><span data-stu-id="a8619-116">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="a8619-117">本教學課程會使用雲端 init 檔案 tooinstall Jenkins 和 Docker VM 上。</span><span class="sxs-lookup"><span data-stu-id="a8619-117">This tutorial uses a cloud-init file tooinstall Jenkins and Docker on a VM.</span></span> 

<span data-ttu-id="a8619-118">您目前的殼層中建立名為*雲端 init.txt*和 hello 貼上下列組態。</span><span class="sxs-lookup"><span data-stu-id="a8619-118">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="a8619-119">例如，在 hello 雲端 Shell 不在您本機電腦上建立 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="a8619-119">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="a8619-120">輸入`sensible-editor cloud-init-jenkins.txt`toocreate hello 檔案，並查看一份可用的編輯器。</span><span class="sxs-lookup"><span data-stu-id="a8619-120">Enter `sensible-editor cloud-init-jenkins.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="a8619-121">請確定已正確複製該 hello 整個雲端初始化檔案，特別是 hello 第一行：</span><span class="sxs-lookup"><span data-stu-id="a8619-121">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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

<span data-ttu-id="a8619-122">建立 VM 之前，請先使用 [az group create](/cli/azure/group#create) 來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="a8619-122">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="a8619-123">hello 下列範例會建立名為的資源群組*myResourceGroupJenkins*在 hello *eastus*位置：</span><span class="sxs-lookup"><span data-stu-id="a8619-123">hello following example creates a resource group named *myResourceGroupJenkins* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

<span data-ttu-id="a8619-124">現在，使用 [az vm create](/cli/azure/vm#create) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="a8619-124">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="a8619-125">使用 hello`--custom-data`參數 toopass 雲端 init 組態檔中的。</span><span class="sxs-lookup"><span data-stu-id="a8619-125">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="a8619-126">提供完整路徑，hello 太*雲端-init-jenkins.txt*如果 hello 檔案儲存目前的工作目錄之外。</span><span class="sxs-lookup"><span data-stu-id="a8619-126">Provide hello full path too*cloud-init-jenkins.txt* if you saved hello file outside of your present working directory.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

<span data-ttu-id="a8619-127">花幾分鐘，讓 hello VM toobe 建立及設定。</span><span class="sxs-lookup"><span data-stu-id="a8619-127">It takes a few minutes for hello VM toobe created and configured.</span></span>

<span data-ttu-id="a8619-128">tooallow web 流量 tooreach 您的 VM 使用[az vm 開啟通訊埠](/cli/azure/vm#open-port)tooopen 連接埠*8080* Jenkins 流量和連接埠*1337年*hello Node.js 應用程式所使用的 toorun 範例應用程式：</span><span class="sxs-lookup"><span data-stu-id="a8619-128">tooallow web traffic tooreach your VM, use [az vm open-port](/cli/azure/vm#open-port) tooopen port *8080* for Jenkins traffic and port *1337* for hello Node.js app that is used toorun a sample app:</span></span>

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a><span data-ttu-id="a8619-129">設定 Jenkins</span><span class="sxs-lookup"><span data-stu-id="a8619-129">Configure Jenkins</span></span>
<span data-ttu-id="a8619-130">tooaccess 您 Jenkins 執行個體，取得您的 VM hello 公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="a8619-130">tooaccess your Jenkins instance, obtain hello public IP address of your VM:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="a8619-131">基於安全性目的，您需要 tooenter hello 初始管理密碼儲存在您 VM toostart hello Jenkins 安裝上的文字檔案。</span><span class="sxs-lookup"><span data-stu-id="a8619-131">For security purposes, you need tooenter hello initial admin password that is stored in a text file on your VM toostart hello Jenkins install.</span></span> <span data-ttu-id="a8619-132">使用 hello 在上一個步驟 tooSSH tooyour hello VM 中取得公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="a8619-132">Use hello public IP address obtained in hello previous step tooSSH tooyour VM:</span></span>

```bash
ssh azureuser@<publicIps>
```

<span data-ttu-id="a8619-133">檢視 hello`initialAdminPassword`您 Jenkins 安裝，並將它複製：</span><span class="sxs-lookup"><span data-stu-id="a8619-133">View hello `initialAdminPassword` for your Jenkins install and copy it:</span></span>

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<span data-ttu-id="a8619-134">如果還沒有 hello 檔案，等候幾分鐘，雲端 init toocomplete hello Jenkins 和 Docker 安裝。</span><span class="sxs-lookup"><span data-stu-id="a8619-134">If hello file isn't available yet, wait a couple more minutes for cloud-init toocomplete hello Jenkins and Docker install.</span></span>

<span data-ttu-id="a8619-135">現在開啟網頁瀏覽器並移過`http://<publicIps>:8080`。</span><span class="sxs-lookup"><span data-stu-id="a8619-135">Now open a web browser and go too`http://<publicIps>:8080`.</span></span> <span data-ttu-id="a8619-136">完成初始 Jenkins 設定 hello，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a8619-136">Complete hello initial Jenkins setup as follows:</span></span>

- <span data-ttu-id="a8619-137">輸入 hello *initialAdminPassword*取自 hello 上一個步驟中的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="a8619-137">Enter hello *initialAdminPassword* obtained from hello VM in hello previous step.</span></span>
- <span data-ttu-id="a8619-138">按一下**選取外掛程式 tooinstall**</span><span class="sxs-lookup"><span data-stu-id="a8619-138">Click **Select plugins tooinstall**</span></span>
- <span data-ttu-id="a8619-139">搜尋*GitHub* hello hello 頂端的文字方塊中，選取 hello *GitHub 外掛程式*，然後按一下 **安裝**</span><span class="sxs-lookup"><span data-stu-id="a8619-139">Search for *GitHub* in hello text box across hello top, select hello *GitHub plugin*, then click **Install**</span></span>
- <span data-ttu-id="a8619-140">toocreate Jenkins 使用者帳戶，填寫所需的 hello 形式。</span><span class="sxs-lookup"><span data-stu-id="a8619-140">toocreate a Jenkins user account, fill out hello form as desired.</span></span> <span data-ttu-id="a8619-141">從安全性觀點來看，您應該建立第一個 Jenkins 使用者，而不是為 hello 預設管理員帳戶繼續進行。</span><span class="sxs-lookup"><span data-stu-id="a8619-141">From a security perspective, you should create this first Jenkins user rather than continuing as hello default admin account.</span></span>
- <span data-ttu-id="a8619-142">完成後，按一下 [開始使用 Jenkins]</span><span class="sxs-lookup"><span data-stu-id="a8619-142">When finished, click **Start using Jenkins**</span></span>


## <a name="create-github-webhook"></a><span data-ttu-id="a8619-143">建立 GitHub webhook</span><span class="sxs-lookup"><span data-stu-id="a8619-143">Create GitHub webhook</span></span>
<span data-ttu-id="a8619-144">tooconfigure hello 整合與 GitHub，開啟 hello [Node.js Hello World 範例應用程式](https://github.com/Azure-Samples/nodejs-docs-hello-world)從 hello Azure 範例儲存機制。</span><span class="sxs-lookup"><span data-stu-id="a8619-144">tooconfigure hello integration with GitHub, open hello [Node.js Hello World sample app](https://github.com/Azure-Samples/nodejs-docs-hello-world) from hello Azure samples repo.</span></span> <span data-ttu-id="a8619-145">toofork hello 儲存機制 tooyour 擁有 GitHub 帳戶，請按一下 hello**分岔**hello 右上角中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a8619-145">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

<span data-ttu-id="a8619-146">建立 webhook 內所建立的 hello 分岔：</span><span class="sxs-lookup"><span data-stu-id="a8619-146">Create a webhook inside hello fork you created:</span></span>

- <span data-ttu-id="a8619-147">按一下**設定**，然後選取**整合與服務**左側為 hello。</span><span class="sxs-lookup"><span data-stu-id="a8619-147">Click **Settings**, then select **Integrations & services** on hello left-hand side.</span></span>
- <span data-ttu-id="a8619-148">按一下 [新增服務]，在篩選方塊中輸入 Jenkins。</span><span class="sxs-lookup"><span data-stu-id="a8619-148">Click **Add service**, then enter *Jenkins* in filter box.</span></span>
- <span data-ttu-id="a8619-149">選取 [Jenkins (GitHub 外掛程式)]</span><span class="sxs-lookup"><span data-stu-id="a8619-149">Select *Jenkins (GitHub plugin)*</span></span>
- <span data-ttu-id="a8619-150">Hello **Jenkins 連接 URL**，輸入`http://<publicIps>:8080/github-webhook/`。</span><span class="sxs-lookup"><span data-stu-id="a8619-150">For hello **Jenkins hook URL**, enter `http://<publicIps>:8080/github-webhook/`.</span></span> <span data-ttu-id="a8619-151">請確定您包含結尾的 hello /</span><span class="sxs-lookup"><span data-stu-id="a8619-151">Make sure you include hello trailing /</span></span>
- <span data-ttu-id="a8619-152">按一下 [新增服務]。</span><span class="sxs-lookup"><span data-stu-id="a8619-152">Click **Add service**</span></span>

![新增 GitHub webhook tooyour 分叉儲存機制](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a><span data-ttu-id="a8619-154">建立 Jenkins 作業</span><span class="sxs-lookup"><span data-stu-id="a8619-154">Create Jenkins job</span></span>
<span data-ttu-id="a8619-155">toohave Jenkins 回應 tooan 事件在 GitHub 中認可的程式碼，例如建立 Jenkins 作業。</span><span class="sxs-lookup"><span data-stu-id="a8619-155">toohave Jenkins respond tooan event in GitHub such as committing code, create a Jenkins job.</span></span> 

<span data-ttu-id="a8619-156">在您 Jenkins 的網站，按一下**建立新的作業**hello 首頁上：</span><span class="sxs-lookup"><span data-stu-id="a8619-156">In your Jenkins website, click **Create new jobs** from hello home page:</span></span>

- <span data-ttu-id="a8619-157">輸入 HelloWorld 作為作業名稱。</span><span class="sxs-lookup"><span data-stu-id="a8619-157">Enter *HelloWorld* as job name.</span></span> <span data-ttu-id="a8619-158">選擇 [自由樣式專案]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a8619-158">Choose **Freestyle project**, then select **OK**.</span></span>
- <span data-ttu-id="a8619-159">在 hello**一般**區段中，選取**GitHub**專案，並輸入您分岔的儲存機制的 URL，例如*https://github.com/iainfoulds/nodejs-docs-hello-world*</span><span class="sxs-lookup"><span data-stu-id="a8619-159">Under hello **General** section, select **GitHub** project and enter your forked repo URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world*</span></span>
- <span data-ttu-id="a8619-160">在 hello**來源的程式碼管理**區段中，選取**Git**，輸入您分岔的儲存機制*.git* URL，例如*https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span><span class="sxs-lookup"><span data-stu-id="a8619-160">Under hello **Source code management** section, select **Git**, enter your forked repo *.git* URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span></span>
- <span data-ttu-id="a8619-161">在 hello**組建觸發程序**區段中，選取**GitHub 勾點觸發程序進行輪詢 GITscm**。</span><span class="sxs-lookup"><span data-stu-id="a8619-161">Under hello **Build Triggers** section, select **GitHub hook trigger for GITscm polling**.</span></span>
- <span data-ttu-id="a8619-162">在 hello**建置**區段中，選擇**加入建置步驟**。</span><span class="sxs-lookup"><span data-stu-id="a8619-162">Under hello **Build** section, choose **Add build step**.</span></span> <span data-ttu-id="a8619-163">選取**執行殼層**，然後輸入`echo "Testing"`toocommand 視窗中。</span><span class="sxs-lookup"><span data-stu-id="a8619-163">Select **Execute shell**, then enter `echo "Testing"` in toocommand window.</span></span>
- <span data-ttu-id="a8619-164">按一下**儲存**在 hello hello 工作 視窗的底部。</span><span class="sxs-lookup"><span data-stu-id="a8619-164">Click **Save** at hello bottom of hello jobs window.</span></span>


## <a name="test-github-integration"></a><span data-ttu-id="a8619-165">測試 GitHub 整合</span><span class="sxs-lookup"><span data-stu-id="a8619-165">Test GitHub integration</span></span>
<span data-ttu-id="a8619-166">tootest hello GitHub 的整合 jenkins，認可您的 「 分叉 」 中的變更。</span><span class="sxs-lookup"><span data-stu-id="a8619-166">tootest hello GitHub integration with Jenkins, commit a change in your fork.</span></span> 

<span data-ttu-id="a8619-167">GitHub 中備份 web UI，選取您分岔的儲存機制，然後按一下hello **index.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="a8619-167">Back in GitHub web UI, select your forked repo, and then click hello **index.js** file.</span></span> <span data-ttu-id="a8619-168">按一下 hello 鉛筆圖示 tooedit 這個檔案就會讀取第 6 行：</span><span class="sxs-lookup"><span data-stu-id="a8619-168">Click hello pencil icon tooedit this file so line 6 reads:</span></span>

```nodejs
response.end("Hello World!");
```

<span data-ttu-id="a8619-169">toocommit 您的變更，按一下 hello**認可變更**hello 底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a8619-169">toocommit your changes, click hello **Commit changes** button at hello bottom.</span></span>

<span data-ttu-id="a8619-170">Jenkins，在新的組建會開始在 hello**建置記錄**hello 左下角的 [工作] 頁面的區段。</span><span class="sxs-lookup"><span data-stu-id="a8619-170">In Jenkins, a new build starts under hello **Build history** section of hello bottom left-hand corner of your job page.</span></span> <span data-ttu-id="a8619-171">按一下 hello 組建編號] 連結並選取 [**主控台輸出**hello 左側的大小。</span><span class="sxs-lookup"><span data-stu-id="a8619-171">Click hello build number link and select **Console output** on hello left-hand size.</span></span> <span data-ttu-id="a8619-172">您可以檢視您的程式碼取自 GitHub 和 hello 建置動作輸出 hello 訊息當成 Jenkins hello 步驟`Testing`toohello 主控台。</span><span class="sxs-lookup"><span data-stu-id="a8619-172">You can view hello steps Jenkins takes as your code is pulled from GitHub and hello build action outputs hello message `Testing` toohello console.</span></span> <span data-ttu-id="a8619-173">每次認可時就在 GitHub 中 hello webhook 向外連 tooJenkins 並觸發新的組建，以這種方式。</span><span class="sxs-lookup"><span data-stu-id="a8619-173">Each time a commit is made in GitHub, hello webhook reaches out tooJenkins and trigger a new build in this way.</span></span>


## <a name="define-docker-build-image"></a><span data-ttu-id="a8619-174">定義 Docker 組建映像</span><span class="sxs-lookup"><span data-stu-id="a8619-174">Define Docker build image</span></span>
<span data-ttu-id="a8619-175">toosee hello Node.js 應用程式執行您的 GitHub 認可中的 架構可讓您建立 Docker 映像 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a8619-175">toosee hello Node.js app running based on your GitHub commits, lets build a Docker image toorun hello app.</span></span> <span data-ttu-id="a8619-176">hello 映像的建立從 Dockerfile，定義如何 tooconfigure hello 執行 hello 應用程式的容器。</span><span class="sxs-lookup"><span data-stu-id="a8619-176">hello image is built from a Dockerfile that defines how tooconfigure hello container that runs hello app.</span></span> 

<span data-ttu-id="a8619-177">從 hello SSH 連線 tooyour VM，變更 toohello Jenkins 工作區目錄名為您在上一個步驟中建立的 hello 工作之後。</span><span class="sxs-lookup"><span data-stu-id="a8619-177">From hello SSH connection tooyour VM, change toohello Jenkins workspace directory named after hello job you created in a previous step.</span></span> <span data-ttu-id="a8619-178">在我們的範例中命名為 HelloWorld。</span><span class="sxs-lookup"><span data-stu-id="a8619-178">In our example, that was named *HelloWorld*.</span></span>

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

<span data-ttu-id="a8619-179">此工作區的目錄中建立的檔案`sudo sensible-editor Dockerfile`和 hello 貼上下列內容。</span><span class="sxs-lookup"><span data-stu-id="a8619-179">Create a file with in this workspace directory with `sudo sensible-editor Dockerfile` and paste hello following contents.</span></span> <span data-ttu-id="a8619-180">請確定該 hello 整個 Dockerfile 會正確複製，特別是 hello 第一行：</span><span class="sxs-lookup"><span data-stu-id="a8619-180">Make sure that hello whole Dockerfile is copied correctly, especially hello first line:</span></span>

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

<span data-ttu-id="a8619-181">此 Dockerfile 使用使用 Alpine Linux hello 基底 Node.js 映像，hello Hello World 應用程式的公開連接埠 1337年上，執行，然後複製 hello 應用程式檔案，並將它初始化。</span><span class="sxs-lookup"><span data-stu-id="a8619-181">This Dockerfile uses hello base Node.js image using Alpine Linux, exposes port 1337 that hello Hello World app runs on, then copies hello app files and initializes it.</span></span>


## <a name="create-jenkins-build-rules"></a><span data-ttu-id="a8619-182">建立 Jenkins 組建規則</span><span class="sxs-lookup"><span data-stu-id="a8619-182">Create Jenkins build rules</span></span>
<span data-ttu-id="a8619-183">在上一個步驟中，您可以建立基本的 Jenkins 組建規則輸出訊息 toohello 主控台。</span><span class="sxs-lookup"><span data-stu-id="a8619-183">In a previous step, you created a basic Jenkins build rule that output a message toohello console.</span></span> <span data-ttu-id="a8619-184">可讓我們 Dockerfile 建立 hello 建置步驟 toouse 和執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a8619-184">Lets create hello build step toouse our Dockerfile and run hello app.</span></span>

<span data-ttu-id="a8619-185">回到您 Jenkins 執行個體中，選取您在上一個步驟中建立的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="a8619-185">Back in your Jenkins instance, select hello job you created in a previous step.</span></span> <span data-ttu-id="a8619-186">按一下**設定**hello 左手邊及捲動 toohello**建置**> 一節：</span><span class="sxs-lookup"><span data-stu-id="a8619-186">Click **Configure** on hello left-hand side and scroll down toohello **Build** section:</span></span>

- <span data-ttu-id="a8619-187">移除現有的 `echo "Test"` 組建步驟。</span><span class="sxs-lookup"><span data-stu-id="a8619-187">Remove your existing `echo "Test"` build step.</span></span> <span data-ttu-id="a8619-188">按一下紅色跨 hello 右上角的 hello 現有的建置步驟方塊上的 hello。</span><span class="sxs-lookup"><span data-stu-id="a8619-188">Click hello red cross on hello top right-hand corner of hello existing build step box.</span></span>
- <span data-ttu-id="a8619-189">按一下 [新增組件步驟]，然後選取 [執行殼層]。</span><span class="sxs-lookup"><span data-stu-id="a8619-189">Click **Add build step**, then select **Execute shell**</span></span>
- <span data-ttu-id="a8619-190">在 hello**命令**方塊中，輸入 hello 遵循 Docker 命令，然後選取**儲存**:</span><span class="sxs-lookup"><span data-stu-id="a8619-190">In hello **Command** box, enter hello following Docker commands, then select **Save**:</span></span>

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

<span data-ttu-id="a8619-191">hello Docker 建置步驟會建立映像和它以 hello Jenkins 組建編號，因此您可以維護映像的歷程記錄的標記。</span><span class="sxs-lookup"><span data-stu-id="a8619-191">hello Docker build steps create an image and tag it with hello Jenkins build number so you can maintain a history of images.</span></span> <span data-ttu-id="a8619-192">任何現有的容器執行 hello 應用程式會停止，然後移除。</span><span class="sxs-lookup"><span data-stu-id="a8619-192">Any existing containers running hello app are stopped and then removed.</span></span> <span data-ttu-id="a8619-193">開始使用 hello 映像，並執行 Node.js 應用程式根據 hello GitHub 中的最新認可，則新的容器。</span><span class="sxs-lookup"><span data-stu-id="a8619-193">A new container is then started using hello image and runs your Node.js app based on hello latest commits in GitHub.</span></span>


## <a name="test-your-pipeline"></a><span data-ttu-id="a8619-194">測試您的管線</span><span class="sxs-lookup"><span data-stu-id="a8619-194">Test your pipeline</span></span>
<span data-ttu-id="a8619-195">toosee hello 整個管線在動作中，編輯 hello *index.js*再次檔案分岔的 GitHub 儲存機制中，按一下**認可變更**。</span><span class="sxs-lookup"><span data-stu-id="a8619-195">toosee hello whole pipeline in action, edit hello *index.js* file in your forked GitHub repo again and click **Commit change**.</span></span> <span data-ttu-id="a8619-196">Jenkins 根據 hello webhook GitHub 中，啟動新的工作。</span><span class="sxs-lookup"><span data-stu-id="a8619-196">A new job starts in Jenkins based on hello webhook for GitHub.</span></span> <span data-ttu-id="a8619-197">它需要幾秒鐘 toocreate hello Docker 映像並啟動新的容器中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a8619-197">It takes a few seconds toocreate hello Docker image and start your app in a new container.</span></span>

<span data-ttu-id="a8619-198">如有需要請再次取得 VM 的 hello 公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="a8619-198">If needed, obtain hello public IP address of your VM again:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="a8619-199">開啟網路瀏覽器，輸入 `http://<publicIps>:1337`。</span><span class="sxs-lookup"><span data-stu-id="a8619-199">Open a web browser and enter `http://<publicIps>:1337`.</span></span> <span data-ttu-id="a8619-200">Node.js 應用程式會顯示，而且會反映出 hello GitHub 分支中的最新認可，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a8619-200">Your Node.js app is displayed and reflects hello latest commits in your GitHub fork as follows:</span></span>

![執行 Node.js 應用程式](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

<span data-ttu-id="a8619-202">現在讓另一個編輯 toohello *index.js*在 GitHub 和 commit hello 變更的檔案。</span><span class="sxs-lookup"><span data-stu-id="a8619-202">Now make another edit toohello *index.js* file in GitHub and commit hello change.</span></span> <span data-ttu-id="a8619-203">等候數秒鐘，讓 hello 作業 toocomplete 中 Jenkins，然後再重新整理您網頁瀏覽器 toosee hello 更新的版本，如下所示的新容器中執行的應用程式：</span><span class="sxs-lookup"><span data-stu-id="a8619-203">Wait a few seconds for hello job toocomplete in Jenkins, then refresh your web browser toosee hello updated version of your app running in a new container as follows:</span></span>

![在另一次 GitHub 認可後執行 Node.js 應用程式](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a><span data-ttu-id="a8619-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a8619-205">Next steps</span></span>
<span data-ttu-id="a8619-206">在本教學課程中，您可以在每個程式碼認可設定 GitHub toorun Jenkins 組建工作，然後再部署 Docker 容器 tootest 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a8619-206">In this tutorial, you configured GitHub toorun a Jenkins build job on each code commit and then deploy a Docker container tootest your app.</span></span> <span data-ttu-id="a8619-207">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="a8619-207">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a8619-208">建立 Jenkins VM</span><span class="sxs-lookup"><span data-stu-id="a8619-208">Create a Jenkins VM</span></span>
> * <span data-ttu-id="a8619-209">安裝並設定 Jenkins</span><span class="sxs-lookup"><span data-stu-id="a8619-209">Install and configure Jenkins</span></span>
> * <span data-ttu-id="a8619-210">建立 GitHub 與 Jenkins 之間的 webhook 整合</span><span class="sxs-lookup"><span data-stu-id="a8619-210">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="a8619-211">從 GitHub 認可建立並觸發 Jenkins 組建作業</span><span class="sxs-lookup"><span data-stu-id="a8619-211">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="a8619-212">建立應用程式的 Docker 映像</span><span class="sxs-lookup"><span data-stu-id="a8619-212">Create a Docker image for your app</span></span>
> * <span data-ttu-id="a8619-213">確認 GitHub 已認可組建的新 Docker 映像，並更新了執行中的應用程式</span><span class="sxs-lookup"><span data-stu-id="a8619-213">Verify GitHub commits build new Docker image and updates running app</span></span>

<span data-ttu-id="a8619-214">進一步瞭解前進 toohello 下一個教學課程 toolearn toointegrate Jenkins 與 Visual Studio Team Services。</span><span class="sxs-lookup"><span data-stu-id="a8619-214">Advance toohello next tutorial toolearn more about how toointegrate Jenkins with Visual Studio Team Services.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a8619-215">使用 Jenkins 和 Team Services 部署應用程式</span><span class="sxs-lookup"><span data-stu-id="a8619-215">Deploy apps with Jenkins and Team Services</span></span>](tutorial-build-deploy-jenkins.md)
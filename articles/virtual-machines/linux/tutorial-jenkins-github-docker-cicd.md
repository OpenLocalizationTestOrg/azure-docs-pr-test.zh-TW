---
title: "在 Azure 中使用 Jenkins 建立開發管線 | Microsoft Docs"
description: "了解如何在 Azure 中建立 Jenkins 虛擬機器，用於在每次程式碼認可時從 GitHub 提取資料，並建立新的 Docker 容器來執行應用程式"
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
ms.openlocfilehash: d9849b5e061dd7f2ae0744a3522dc2eb1fb37035
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a><span data-ttu-id="0a7d0-103">如何在 Azure 中的 Linux VM 上以 Jenkins、GitHub 及 Docker 建立開發基礎結構</span><span class="sxs-lookup"><span data-stu-id="0a7d0-103">How to create a development infrastructure on a Linux VM in Azure with Jenkins, GitHub, and Docker</span></span>
<span data-ttu-id="0a7d0-104">若要將應用程式開發的組建和測試階段自動化，可以使用持續整合和部署 (CI/CD) 管線。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-104">To automate the build and test phase of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="0a7d0-105">在本教學課程中，您會在 Azure VM 上建立 CI/CD 管線，包括如何︰</span><span class="sxs-lookup"><span data-stu-id="0a7d0-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0a7d0-106">建立 Jenkins VM</span><span class="sxs-lookup"><span data-stu-id="0a7d0-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="0a7d0-107">安裝並設定 Jenkins</span><span class="sxs-lookup"><span data-stu-id="0a7d0-107">Install and configure Jenkins</span></span>
> * <span data-ttu-id="0a7d0-108">建立 GitHub 與 Jenkins 之間的 webhook 整合</span><span class="sxs-lookup"><span data-stu-id="0a7d0-108">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="0a7d0-109">從 GitHub 認可建立並觸發 Jenkins 組建作業</span><span class="sxs-lookup"><span data-stu-id="0a7d0-109">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="0a7d0-110">建立應用程式的 Docker 映像</span><span class="sxs-lookup"><span data-stu-id="0a7d0-110">Create a Docker image for your app</span></span>
> * <span data-ttu-id="0a7d0-111">確認 GitHub 已認可組建的新 Docker 映像，並更新了執行中的應用程式</span><span class="sxs-lookup"><span data-stu-id="0a7d0-111">Verify GitHub commits build new Docker image and updates running app</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0a7d0-112">如果您選擇在本機安裝和使用 CLI，本教學課程會要求您執行 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="0a7d0-113">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="0a7d0-114">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-jenkins-instance"></a><span data-ttu-id="0a7d0-115">建立 Jenkins 執行個體</span><span class="sxs-lookup"><span data-stu-id="0a7d0-115">Create Jenkins instance</span></span>
<span data-ttu-id="0a7d0-116">在[如何在首次開機時自訂 Linux 虛擬機器](tutorial-automate-vm-deployment.md)的先前教學課程中，您已了解如何使用 cloud-init 自動進行 VM 自訂。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-116">In a previous tutorial on [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with cloud-init.</span></span> <span data-ttu-id="0a7d0-117">本教學課程使用 cloud-init 檔案在 VM 上安裝 Jenkins 和 Docker。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-117">This tutorial uses a cloud-init file to install Jenkins and Docker on a VM.</span></span> 

<span data-ttu-id="0a7d0-118">您目前的殼層中，建立名為 cloud-init.txt 的檔案，並貼上下列組態。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-118">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="0a7d0-119">例如，在 Cloud Shell 中建立不在本機電腦上的檔案。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-119">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="0a7d0-120">輸入 `sensible-editor cloud-init-jenkins.txt` 可建立檔案，並查看可用的編輯器清單。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-120">Enter `sensible-editor cloud-init-jenkins.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="0a7d0-121">請確定已正確複製整個 cloud-init 檔案，特別是第一行：</span><span class="sxs-lookup"><span data-stu-id="0a7d0-121">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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

<span data-ttu-id="0a7d0-122">建立 VM 之前，請先使用 [az group create](/cli/azure/group#create) 來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-122">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="0a7d0-123">下列範例會在 eastus 位置建立名為 myResourceGroupJenkins 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-123">The following example creates a resource group named *myResourceGroupJenkins* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

<span data-ttu-id="0a7d0-124">現在，使用 [az vm create](/cli/azure/vm#create) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-124">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="0a7d0-125">使用 `--custom-data` 參數以傳入 cloud-init 組態檔。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-125">Use the `--custom-data` parameter to pass in your cloud-init config file.</span></span> <span data-ttu-id="0a7d0-126">如果您將檔案儲存於目前工作目錄之外的位置，請提供 cloud-init-jenkins.txt 的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-126">Provide the full path to *cloud-init-jenkins.txt* if you saved the file outside of your present working directory.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

<span data-ttu-id="0a7d0-127">系統需要花幾分鐘的時間來建立及設定 VM。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-127">It takes a few minutes for the VM to be created and configured.</span></span>

<span data-ttu-id="0a7d0-128">為了允許網路流量連線到您的 VM，使用 [az vm open-port](/cli/azure/vm#open-port) 開啟連接埠 8080 (用於 Jenkins 流量) 和連接埠 1337 (用於 Node.js 應用程式，此應用程式用來執行範例應用程式)︰</span><span class="sxs-lookup"><span data-stu-id="0a7d0-128">To allow web traffic to reach your VM, use [az vm open-port](/cli/azure/vm#open-port) to open port *8080* for Jenkins traffic and port *1337* for the Node.js app that is used to run a sample app:</span></span>

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a><span data-ttu-id="0a7d0-129">設定 Jenkins</span><span class="sxs-lookup"><span data-stu-id="0a7d0-129">Configure Jenkins</span></span>
<span data-ttu-id="0a7d0-130">若要存取您的 Jenkins 執行個體，取得您的 VM 的公用 IP 位址︰</span><span class="sxs-lookup"><span data-stu-id="0a7d0-130">To access your Jenkins instance, obtain the public IP address of your VM:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="0a7d0-131">基於安全考量，您必須輸入初始的系統管理員密碼 (儲存在您的 VM 上的文字檔案中)，才能啟動 Jenkins 安裝。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-131">For security purposes, you need to enter the initial admin password that is stored in a text file on your VM to start the Jenkins install.</span></span> <span data-ttu-id="0a7d0-132">使用上一個步驟取得的公用 IP 位址，透過 SSH 連線至您的 VM：</span><span class="sxs-lookup"><span data-stu-id="0a7d0-132">Use the public IP address obtained in the previous step to SSH to your VM:</span></span>

```bash
ssh azureuser@<publicIps>
```

<span data-ttu-id="0a7d0-133">檢視 Jenkins 安裝的 `initialAdminPassword`，並複製它︰</span><span class="sxs-lookup"><span data-stu-id="0a7d0-133">View the `initialAdminPassword` for your Jenkins install and copy it:</span></span>

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<span data-ttu-id="0a7d0-134">如果檔案尚無法使用，請等待數分鐘，讓 cloud-init 完成 Jenkins 和 Docker 安裝。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-134">If the file isn't available yet, wait a couple more minutes for cloud-init to complete the Jenkins and Docker install.</span></span>

<span data-ttu-id="0a7d0-135">現在開啟瀏覽器，前往 `http://<publicIps>:8080`。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-135">Now open a web browser and go to `http://<publicIps>:8080`.</span></span> <span data-ttu-id="0a7d0-136">完成初始 Jenkins 設定，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="0a7d0-136">Complete the initial Jenkins setup as follows:</span></span>

- <span data-ttu-id="0a7d0-137">輸入上一個步驟從 VM 取得的 initialAdminPassword。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-137">Enter the *initialAdminPassword* obtained from the VM in the previous step.</span></span>
- <span data-ttu-id="0a7d0-138">按一下 [選取要安裝的外掛程式]</span><span class="sxs-lookup"><span data-stu-id="0a7d0-138">Click **Select plugins to install**</span></span>
- <span data-ttu-id="0a7d0-139">在頂端的文字方塊中搜尋 GitHub，選取 GitHub 外掛程式，然後按一下 [安裝]</span><span class="sxs-lookup"><span data-stu-id="0a7d0-139">Search for *GitHub* in the text box across the top, select the *GitHub plugin*, then click **Install**</span></span>
- <span data-ttu-id="0a7d0-140">若要建立 Jenkins 使用者帳戶，依所需填寫表單。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-140">To create a Jenkins user account, fill out the form as desired.</span></span> <span data-ttu-id="0a7d0-141">從安全性角度來看，您應該建立第一個 Jenkins 使用者，而不是繼續使用預設管理帳戶。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-141">From a security perspective, you should create this first Jenkins user rather than continuing as the default admin account.</span></span>
- <span data-ttu-id="0a7d0-142">完成後，按一下 [開始使用 Jenkins]</span><span class="sxs-lookup"><span data-stu-id="0a7d0-142">When finished, click **Start using Jenkins**</span></span>


## <a name="create-github-webhook"></a><span data-ttu-id="0a7d0-143">建立 GitHub webhook</span><span class="sxs-lookup"><span data-stu-id="0a7d0-143">Create GitHub webhook</span></span>
<span data-ttu-id="0a7d0-144">若要設定與 GitHub 整合，開啟 Azure 範例存放庫中的 [Node.js Hello World 範例應用程式](https://github.com/Azure-Samples/nodejs-docs-hello-world)。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-144">To configure the integration with GitHub, open the [Node.js Hello World sample app](https://github.com/Azure-Samples/nodejs-docs-hello-world) from the Azure samples repo.</span></span> <span data-ttu-id="0a7d0-145">為了將存放庫分支至您自己的 GitHub 帳戶，按一下右上角的 [分支] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-145">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>

<span data-ttu-id="0a7d0-146">在您建立的分支內建立 webhook︰</span><span class="sxs-lookup"><span data-stu-id="0a7d0-146">Create a webhook inside the fork you created:</span></span>

- <span data-ttu-id="0a7d0-147">按一下 [設定]，然後選取左手邊的 [整合與服務]。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-147">Click **Settings**, then select **Integrations & services** on the left-hand side.</span></span>
- <span data-ttu-id="0a7d0-148">按一下 [新增服務]，在篩選方塊中輸入 Jenkins。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-148">Click **Add service**, then enter *Jenkins* in filter box.</span></span>
- <span data-ttu-id="0a7d0-149">選取 [Jenkins (GitHub 外掛程式)]</span><span class="sxs-lookup"><span data-stu-id="0a7d0-149">Select *Jenkins (GitHub plugin)*</span></span>
- <span data-ttu-id="0a7d0-150">在 [Jenkins 勾點 URL] 輸入 `http://<publicIps>:8080/github-webhook/`。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-150">For the **Jenkins hook URL**, enter `http://<publicIps>:8080/github-webhook/`.</span></span> <span data-ttu-id="0a7d0-151">別漏掉最後的斜線 (/)。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-151">Make sure you include the trailing /</span></span>
- <span data-ttu-id="0a7d0-152">按一下 [新增服務]。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-152">Click **Add service**</span></span>

![將 GitHub webhook 新增至您的分支存放庫](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a><span data-ttu-id="0a7d0-154">建立 Jenkins 作業</span><span class="sxs-lookup"><span data-stu-id="0a7d0-154">Create Jenkins job</span></span>
<span data-ttu-id="0a7d0-155">為了讓 Jenkins 回應 GitHub 中的事件，例如認可程式碼，請建立 Jenkins 作業。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-155">To have Jenkins respond to an event in GitHub such as committing code, create a Jenkins job.</span></span> 

<span data-ttu-id="0a7d0-156">在您的 Jenkins 網站中，按一下首頁中的 [建立新作業]︰</span><span class="sxs-lookup"><span data-stu-id="0a7d0-156">In your Jenkins website, click **Create new jobs** from the home page:</span></span>

- <span data-ttu-id="0a7d0-157">輸入 HelloWorld 作為作業名稱。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-157">Enter *HelloWorld* as job name.</span></span> <span data-ttu-id="0a7d0-158">選擇 [自由樣式專案]，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-158">Choose **Freestyle project**, then select **OK**.</span></span>
- <span data-ttu-id="0a7d0-159">在 [一般] 區段中，選取 [GitHub] 專案，然後輸入您的分支存放庫 URL，例如 *https://github.com/iainfoulds/nodejs-docs-hello-world*</span><span class="sxs-lookup"><span data-stu-id="0a7d0-159">Under the **General** section, select **GitHub** project and enter your forked repo URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world*</span></span>
- <span data-ttu-id="0a7d0-160">在 [原始碼管理] 區段中，選取 [Git]，輸入您的分支存放庫 .git URL，例如 *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span><span class="sxs-lookup"><span data-stu-id="0a7d0-160">Under the **Source code management** section, select **Git**, enter your forked repo *.git* URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span></span>
- <span data-ttu-id="0a7d0-161">在 [組建觸發程序] 下，選取 [GITScm 輪詢的 GitHub 勾點觸發程序]。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-161">Under the **Build Triggers** section, select **GitHub hook trigger for GITscm polling**.</span></span>
- <span data-ttu-id="0a7d0-162">在 [組建] 區段中，選擇 [新增組建步驟]。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-162">Under the **Build** section, choose **Add build step**.</span></span> <span data-ttu-id="0a7d0-163">選取 [執行殼層]，然後在命令視窗中輸入 `echo "Testing"`。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-163">Select **Execute shell**, then enter `echo "Testing"` in to command window.</span></span>
- <span data-ttu-id="0a7d0-164">按一下作業視窗底部的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-164">Click **Save** at the bottom of the jobs window.</span></span>


## <a name="test-github-integration"></a><span data-ttu-id="0a7d0-165">測試 GitHub 整合</span><span class="sxs-lookup"><span data-stu-id="0a7d0-165">Test GitHub integration</span></span>
<span data-ttu-id="0a7d0-166">若要測試 GitHub 與 Jenkins 的整合，請認可您分支中的變更。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-166">To test the GitHub integration with Jenkins, commit a change in your fork.</span></span> 

<span data-ttu-id="0a7d0-167">回到 GitHub 的網路介面，選取您的分支存放庫，然後按一下 index.js 檔案。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-167">Back in GitHub web UI, select your forked repo, and then click the **index.js** file.</span></span> <span data-ttu-id="0a7d0-168">按一下鉛筆圖示以編輯此檔案，將第 6 行改為︰</span><span class="sxs-lookup"><span data-stu-id="0a7d0-168">Click the pencil icon to edit this file so line 6 reads:</span></span>

```nodejs
response.end("Hello World!");
```

<span data-ttu-id="0a7d0-169">若要認可變更，按一下底部的 [認可變更] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-169">To commit your changes, click the **Commit changes** button at the bottom.</span></span>

<span data-ttu-id="0a7d0-170">在 Jenkins 在作業頁面左下角的 [組建歷程記錄] 區段中會啟動新的組建。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-170">In Jenkins, a new build starts under the **Build history** section of the bottom left-hand corner of your job page.</span></span> <span data-ttu-id="0a7d0-171">按一下組建編號的連結，選取左側大小的 [主控台輸出]。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-171">Click the build number link and select **Console output** on the left-hand size.</span></span> <span data-ttu-id="0a7d0-172">在從 GitHub 提取您的程式碼時，您可以檢視 Jenkins 進行的步驟，組建動作會將 `Testing` 訊息輸出到主控台。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-172">You can view the steps Jenkins takes as your code is pulled from GitHub and the build action outputs the message `Testing` to the console.</span></span> <span data-ttu-id="0a7d0-173">每次在 GitHub 中認可，webhook 就會連線到 Jenkins，以這種方式觸發新的組建。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-173">Each time a commit is made in GitHub, the webhook reaches out to Jenkins and trigger a new build in this way.</span></span>


## <a name="define-docker-build-image"></a><span data-ttu-id="0a7d0-174">定義 Docker 組建映像</span><span class="sxs-lookup"><span data-stu-id="0a7d0-174">Define Docker build image</span></span>
<span data-ttu-id="0a7d0-175">為了查看因應您的 GitHub 認可而執行的 Node.js 應用程式，可以組建一個 Docker 映像來執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-175">To see the Node.js app running based on your GitHub commits, lets build a Docker image to run the app.</span></span> <span data-ttu-id="0a7d0-176">映像是從 Dockerfile 建立，此檔案定義如何設定執行應用程式的容器。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-176">The image is built from a Dockerfile that defines how to configure the container that runs the app.</span></span> 

<span data-ttu-id="0a7d0-177">在您的虛擬機器的 SSH 連線中，切換至以上一個步驟建立之作業為名的 Jenkins 工作區目錄。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-177">From the SSH connection to your VM, change to the Jenkins workspace directory named after the job you created in a previous step.</span></span> <span data-ttu-id="0a7d0-178">在我們的範例中命名為 HelloWorld。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-178">In our example, that was named *HelloWorld*.</span></span>

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

<span data-ttu-id="0a7d0-179">使用 `sudo sensible-editor Dockerfile` 在這個工作區目錄中建立檔案，並貼上下列內容。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-179">Create a file with in this workspace directory with `sudo sensible-editor Dockerfile` and paste the following contents.</span></span> <span data-ttu-id="0a7d0-180">請確定已正確複製整個 Docker 檔案，特別是第一行：</span><span class="sxs-lookup"><span data-stu-id="0a7d0-180">Make sure that the whole Dockerfile is copied correctly, especially the first line:</span></span>

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

<span data-ttu-id="0a7d0-181">這個 Dockerfile 會使用基本 Node.js 映像 (此映像使用 Alpine Linux)，公開Hello World 應用程式執行的連接埠 1337，然後複製應用程式檔案並將它初始化。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-181">This Dockerfile uses the base Node.js image using Alpine Linux, exposes port 1337 that the Hello World app runs on, then copies the app files and initializes it.</span></span>


## <a name="create-jenkins-build-rules"></a><span data-ttu-id="0a7d0-182">建立 Jenkins 組建規則</span><span class="sxs-lookup"><span data-stu-id="0a7d0-182">Create Jenkins build rules</span></span>
<span data-ttu-id="0a7d0-183">您已在上一個步驟中建立基本 Jenkins 組建規則，將訊息輸出至主控台。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-183">In a previous step, you created a basic Jenkins build rule that output a message to the console.</span></span> <span data-ttu-id="0a7d0-184">現在要建立組建步驟來使用我們的 Dockerfile 並執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-184">Lets create the build step to use our Dockerfile and run the app.</span></span>

<span data-ttu-id="0a7d0-185">回到您的 Jenkins 執行個體，選取在上一個步驟建立的作業。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-185">Back in your Jenkins instance, select the job you created in a previous step.</span></span> <span data-ttu-id="0a7d0-186">按一下左手邊的 [設定]，向下捲動至 [組建] 區段︰</span><span class="sxs-lookup"><span data-stu-id="0a7d0-186">Click **Configure** on the left-hand side and scroll down to the **Build** section:</span></span>

- <span data-ttu-id="0a7d0-187">移除現有的 `echo "Test"` 組建步驟。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-187">Remove your existing `echo "Test"` build step.</span></span> <span data-ttu-id="0a7d0-188">按一下現有組建步驟方塊右上角的紅色叉叉。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-188">Click the red cross on the top right-hand corner of the existing build step box.</span></span>
- <span data-ttu-id="0a7d0-189">按一下 [新增組件步驟]，然後選取 [執行殼層]。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-189">Click **Add build step**, then select **Execute shell**</span></span>
- <span data-ttu-id="0a7d0-190">在 [命令] 方塊中輸入下列 Docker 命令，然後選取 [儲存]：</span><span class="sxs-lookup"><span data-stu-id="0a7d0-190">In the **Command** box, enter the following Docker commands, then select **Save**:</span></span>

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

<span data-ttu-id="0a7d0-191">Docker 組建步驟會建立映像，並標記 Jenkins 組建編號，讓您可以維護映像的歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-191">The Docker build steps create an image and tag it with the Jenkins build number so you can maintain a history of images.</span></span> <span data-ttu-id="0a7d0-192">系統會停止任何執行應用程式的現有容器，並加以移除。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-192">Any existing containers running the app are stopped and then removed.</span></span> <span data-ttu-id="0a7d0-193">然後會使用映像啟動新的容器將，並根據 GitHub 中最新的認可執行您的 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-193">A new container is then started using the image and runs your Node.js app based on the latest commits in GitHub.</span></span>


## <a name="test-your-pipeline"></a><span data-ttu-id="0a7d0-194">測試您的管線</span><span class="sxs-lookup"><span data-stu-id="0a7d0-194">Test your pipeline</span></span>
<span data-ttu-id="0a7d0-195">若要查看作用中的整個管線，再次編輯您的分支 GitHub 存放庫中的 index.js 檔案，然後按一下 [認可變更]。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-195">To see the whole pipeline in action, edit the *index.js* file in your forked GitHub repo again and click **Commit change**.</span></span> <span data-ttu-id="0a7d0-196">在 Jenkins 中會依據 GitHub 的 webhook啟動新的作業。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-196">A new job starts in Jenkins based on the webhook for GitHub.</span></span> <span data-ttu-id="0a7d0-197">系統約需要幾秒鐘來建立 Docker 映像並在新容器中啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-197">It takes a few seconds to create the Docker image and start your app in a new container.</span></span>

<span data-ttu-id="0a7d0-198">如有需要，再次取得您的 VM 公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="0a7d0-198">If needed, obtain the public IP address of your VM again:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="0a7d0-199">開啟網路瀏覽器，輸入 `http://<publicIps>:1337`。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-199">Open a web browser and enter `http://<publicIps>:1337`.</span></span> <span data-ttu-id="0a7d0-200">您的 Node.js 應用程式會顯示，而且會反映您的 GitHub 分支中最新的認可，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="0a7d0-200">Your Node.js app is displayed and reflects the latest commits in your GitHub fork as follows:</span></span>

![執行 Node.js 應用程式](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

<span data-ttu-id="0a7d0-202">現在，對 GitHub 中的 index.js 檔案進行另一次編輯，並認可變更。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-202">Now make another edit to the *index.js* file in GitHub and commit the change.</span></span> <span data-ttu-id="0a7d0-203">稍等幾秒鐘讓 Jenkins 中的作業完成，然後重新整理網路瀏覽器以查看在新容器中執行之應用程式的更新版本，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="0a7d0-203">Wait a few seconds for the job to complete in Jenkins, then refresh your web browser to see the updated version of your app running in a new container as follows:</span></span>

![在另一次 GitHub 認可後執行 Node.js 應用程式](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a><span data-ttu-id="0a7d0-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0a7d0-205">Next steps</span></span>
<span data-ttu-id="0a7d0-206">在本教學課程中，您設定 GitHub 在每次程式碼認可時執行 Jenkins 組建作業，然後部署 Docker 容器來測試您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-206">In this tutorial, you configured GitHub to run a Jenkins build job on each code commit and then deploy a Docker container to test your app.</span></span> <span data-ttu-id="0a7d0-207">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="0a7d0-207">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0a7d0-208">建立 Jenkins VM</span><span class="sxs-lookup"><span data-stu-id="0a7d0-208">Create a Jenkins VM</span></span>
> * <span data-ttu-id="0a7d0-209">安裝並設定 Jenkins</span><span class="sxs-lookup"><span data-stu-id="0a7d0-209">Install and configure Jenkins</span></span>
> * <span data-ttu-id="0a7d0-210">建立 GitHub 與 Jenkins 之間的 webhook 整合</span><span class="sxs-lookup"><span data-stu-id="0a7d0-210">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="0a7d0-211">從 GitHub 認可建立並觸發 Jenkins 組建作業</span><span class="sxs-lookup"><span data-stu-id="0a7d0-211">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="0a7d0-212">建立應用程式的 Docker 映像</span><span class="sxs-lookup"><span data-stu-id="0a7d0-212">Create a Docker image for your app</span></span>
> * <span data-ttu-id="0a7d0-213">確認 GitHub 已認可組建的新 Docker 映像，並更新了執行中的應用程式</span><span class="sxs-lookup"><span data-stu-id="0a7d0-213">Verify GitHub commits build new Docker image and updates running app</span></span>

<span data-ttu-id="0a7d0-214">前進到下一個教學課程，以深入了解如何整合 Jenkins 與 Visual Studio Team Services。</span><span class="sxs-lookup"><span data-stu-id="0a7d0-214">Advance to the next tutorial to learn more about how to integrate Jenkins with Visual Studio Team Services.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0a7d0-215">使用 Jenkins 和 Team Services 部署應用程式</span><span class="sxs-lookup"><span data-stu-id="0a7d0-215">Deploy apps with Jenkins and Team Services</span></span>](tutorial-build-deploy-jenkins.md)
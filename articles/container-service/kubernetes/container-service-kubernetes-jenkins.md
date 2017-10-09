---
title: "aaaJenkins CI/CD 與 Azure 容器服務中 Kubernetes |Microsoft 文件"
description: "Tooautomate CI/CD Jenkins toodeploy 然後升級上 Kubernetes Azure 容器服務中的容器化應用程式的處理方式"
services: container-service
documentationcenter: 
author: chzbrgr71
manager: johny
editor: 
tags: acs, azure-container-service, jenkins
keywords: "Docker, 容器, Kubernetes, Azure, Jenkins"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: briar
ms.custom: mvc
ms.openlocfilehash: e00e13bf06619bed73e82878777e55458ea3dd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a><span data-ttu-id="ff173-104">Jenkins 與 Azure Container Service 和 Kubernetes 整合</span><span class="sxs-lookup"><span data-stu-id="ff173-104">Jenkins integration with Azure Container Service and Kubernetes</span></span> 
<span data-ttu-id="ff173-105">在本教學課程中，我們逐步 hello 程序 tooset 多容器應用程式的連續整合到 Azure 容器服務 Kubernetes 使用 hello Jenkins 平台。</span><span class="sxs-lookup"><span data-stu-id="ff173-105">In this tutorial, we walk through hello process tooset up continuous integration of a multi-container application into Azure Container Service Kubernetes using hello Jenkins platform.</span></span> <span data-ttu-id="ff173-106">hello 工作流程更新中 Docker Hub hello 容器映像，及升級 hello Kubernetes pod 使用部署的首度發行。</span><span class="sxs-lookup"><span data-stu-id="ff173-106">hello workflow updates hello container image in Docker Hub and upgrades hello Kubernetes pods using a deployment rollout.</span></span> 

## <a name="high-level-process"></a><span data-ttu-id="ff173-107">高階程序</span><span class="sxs-lookup"><span data-stu-id="ff173-107">High level process</span></span>
<span data-ttu-id="ff173-108">此文件中詳述的 hello 基本步驟如下：</span><span class="sxs-lookup"><span data-stu-id="ff173-108">hello basic steps detailed in this article are:</span></span> 
- <span data-ttu-id="ff173-109">在 Container Service 中安裝 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="ff173-109">Install a Kubernetes cluster in Container Service</span></span>
- <span data-ttu-id="ff173-110">Jenkins 安裝和設定存取 tooContainer 服務</span><span class="sxs-lookup"><span data-stu-id="ff173-110">Set up Jenkins and configure access tooContainer Service</span></span>
- <span data-ttu-id="ff173-111">建立 Jenkins 工作流程</span><span class="sxs-lookup"><span data-stu-id="ff173-111">Create a Jenkins workflow</span></span>
- <span data-ttu-id="ff173-112">測試 hello CI/CD 程序結束 tooend</span><span class="sxs-lookup"><span data-stu-id="ff173-112">Test hello CI/CD process end tooend</span></span>

## <a name="install-a-kubernetes-cluster"></a><span data-ttu-id="ff173-113">安裝 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="ff173-113">Install a Kubernetes cluster</span></span>
    
<span data-ttu-id="ff173-114">部署使用下列步驟的 hello Azure 容器服務中的 hello Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="ff173-114">Deploy hello Kubernetes cluster in Azure Container Service using hello following steps.</span></span> <span data-ttu-id="ff173-115">完整文件位於[這裡](container-service-kubernetes-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="ff173-115">Full documentation is located [here](container-service-kubernetes-walkthrough.md).</span></span>

### <a name="step-1-create-a-resource-group"></a><span data-ttu-id="ff173-116">步驟 1：建立資源群組</span><span class="sxs-lookup"><span data-stu-id="ff173-116">Step 1: Create a resource group</span></span>
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-hello-cluster"></a><span data-ttu-id="ff173-117">步驟 2： 部署的 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="ff173-117">Step 2: Deploy hello cluster</span></span>
> [!NOTE]
> <span data-ttu-id="ff173-118">hello 以下步驟需要本機的 SSH 公開金鑰機碼，並儲存在 hello ~/.ssh 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="ff173-118">hello following steps require a local SSH public key stored in hello ~/.ssh folder.</span></span>
>

```azurecli
RESOURCE_GROUP=my-resource-group
DNS_PREFIX=some-unique-value
CLUSTER_NAME=any-acs-cluster-name

az acs create \
--orchestrator-type=kubernetes \
--resource-group $RESOURCE_GROUP \
--name=$CLUSTER_NAME \
--dns-prefix=$DNS_PREFIX \
--ssh-key-value ~/.ssh/id_rsa.pub \
--admin-username=azureuser \
--master-count=1 \
--agent-count=5 \
--agent-vm-size=Standard_D1_v2
```

## <a name="set-up-jenkins-and-configure-access-toocontainer-service"></a><span data-ttu-id="ff173-119">Jenkins 安裝和設定存取 tooContainer 服務</span><span class="sxs-lookup"><span data-stu-id="ff173-119">Set up Jenkins and configure access tooContainer Service</span></span>

### <a name="step-1-install-jenkins"></a><span data-ttu-id="ff173-120">步驟 1：安裝 Jenkins</span><span class="sxs-lookup"><span data-stu-id="ff173-120">Step 1: Install Jenkins</span></span>
1. <span data-ttu-id="ff173-121">使用 Ubuntu 16.04 LTS 建立 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="ff173-121">Create an Azure VM with Ubuntu 16.04 LTS.</span></span>  <span data-ttu-id="ff173-122">因為 hello 稍後會引導您將需要 tooconnect toothis VM 使用撞在本機電腦，設定 hello '驗證類型' too'SSH 公開金鑰 ' 和貼上 hello SSH 公開金鑰存放在本機 ~/.ssh 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="ff173-122">Since later in hello steps you will need tooconnect toothis VM using bash on your local machine, set hello 'Authentication type' too'SSH public key' and paste hello SSH public key that is stored locally in your ~/.ssh folder.</span></span>  <span data-ttu-id="ff173-123">此外，請注意，指定由於這個使用者名稱會為所需的 tooview hello Jenkins 儀表板以及連接 toohello Jenkins VM 在稍後步驟中的 hello '使用者名稱'。</span><span class="sxs-lookup"><span data-stu-id="ff173-123">Also, take note of hello 'User name' that you specify since this user name will be needed tooview hello Jenkins dashboard and for connecting toohello Jenkins VM in later steps.</span></span>
2. <span data-ttu-id="ff173-124">透過這些[指示](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu)安裝 Jenkins。</span><span class="sxs-lookup"><span data-stu-id="ff173-124">Install Jenkins via these [instructions](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span></span> <span data-ttu-id="ff173-125">更詳細的教學課程在 [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04)。</span><span class="sxs-lookup"><span data-stu-id="ff173-125">A more detailed tutorial is at [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span></span>
3. <span data-ttu-id="ff173-126">tooview hello Jenkins 儀表板，在本機電腦上的，藉由新增輸入的規則允許存取 tooport 8080 更新 hello Azure 網路安全性群組 tooallow 連接埠 8080。</span><span class="sxs-lookup"><span data-stu-id="ff173-126">tooview hello Jenkins dashboard on your local machine, update hello Azure network security group tooallow port 8080 by adding an inbound rule that allows access tooport 8080.</span></span>  <span data-ttu-id="ff173-127">或者，您將需要設定連接埠轉送，方法是執行此命令：`ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span><span class="sxs-lookup"><span data-stu-id="ff173-127">Alternatively, you may setup port forwarding by running this command: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span></span>
4. <span data-ttu-id="ff173-128">Tooyour Jenkins 伺服器使用 hello 瀏覽器瀏覽 toohello 公用 IP 連接 (http:// < your_jenkins_public_ip >: 8080) 和解除鎖定 hello hello 的 Jenkins 儀表板與 hello 初始管理密碼的第一次。</span><span class="sxs-lookup"><span data-stu-id="ff173-128">Connect tooyour Jenkins server using hello browser by navigating toohello public IP (http://<your_jenkins_public_ip>:8080) and unlock hello Jenkins dashboard for hello first time with hello initial admin password.</span></span>  <span data-ttu-id="ff173-129">hello 系統管理員密碼會儲存在 /var/lib/jenkins/secrets/initialAdminPassword hello Jenkins VM 上。</span><span class="sxs-lookup"><span data-stu-id="ff173-129">hello admin password is stored at /var/lib/jenkins/secrets/initialAdminPassword on hello Jenkins VM.</span></span>  <span data-ttu-id="ff173-130">此密碼是到 tooSSH 輕鬆 tooget hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`。</span><span class="sxs-lookup"><span data-stu-id="ff173-130">An easy way tooget this password is tooSSH into hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="ff173-131">接下來，請執行：`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`。</span><span class="sxs-lookup"><span data-stu-id="ff173-131">Next, run: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span></span>
5. <span data-ttu-id="ff173-132">透過這些的 hello Jenkins 機器上安裝 Docker[指示](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts)。</span><span class="sxs-lookup"><span data-stu-id="ff173-132">Install Docker on hello Jenkins machine via these [instructions](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span></span> <span data-ttu-id="ff173-133">這可讓 Docker 命令 toobe Jenkins 作業中執行。</span><span class="sxs-lookup"><span data-stu-id="ff173-133">This allows for Docker commands toobe run in Jenkins jobs.</span></span>
6. <span data-ttu-id="ff173-134">設定 Docker 權限 tooallow Jenkins tooaccess hello Docker 端點。</span><span class="sxs-lookup"><span data-stu-id="ff173-134">Configure Docker permissions tooallow Jenkins tooaccess hello Docker endpoint.</span></span>

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. <span data-ttu-id="ff173-135">在 Jenkins 上安裝 `kubectl` CLI。</span><span class="sxs-lookup"><span data-stu-id="ff173-135">Install `kubectl` CLI on Jenkins.</span></span> <span data-ttu-id="ff173-136">更多詳細資料位於[安裝和設定 kubectl](https://kubernetes.io/docs/tasks/kubectl/install/)。</span><span class="sxs-lookup"><span data-stu-id="ff173-136">More details are at [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>  <span data-ttu-id="ff173-137">Jenkins 作業將會使用 'kubectl' toomanage 和部署 toohello Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="ff173-137">Jenkins jobs will use 'kubectl' toomanage and deploy toohello Kubernetes cluster.</span></span>

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-toohello-kubernetes-cluster"></a><span data-ttu-id="ff173-138">步驟 2： 設定存取 toohello Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="ff173-138">Step 2: Set up access toohello Kubernetes cluster</span></span>

> [!NOTE]
> <span data-ttu-id="ff173-139">有多個方法 tooaccomplishing hello 下列步驟。</span><span class="sxs-lookup"><span data-stu-id="ff173-139">There are multiple approaches tooaccomplishing hello following steps.</span></span> <span data-ttu-id="ff173-140">使用 hello 做為您的最簡單的方法。</span><span class="sxs-lookup"><span data-stu-id="ff173-140">Use hello approach that is easiest for you.</span></span>
>

1. <span data-ttu-id="ff173-141">複製 hello`kubectl`組態檔案 toohello Jenkins 機器，所以 Jenkins 工作需要存取 toohello Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="ff173-141">Copy hello `kubectl` config file toohello Jenkins machine so that Jenkins jobs have access toohello Kubernetes cluster.</span></span> <span data-ttu-id="ff173-142">這些指示假設您比 hello Jenkins VM 使用 bash 從不同的電腦和本機 SSH 公開金鑰，會儲存在 hello 機器 ~/.ssh 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ff173-142">These instructions assume that you are using bash from a different machine than hello Jenkins VM and that a local SSH public key is stored in hello machine's ~/.ssh folder.</span></span>

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. <span data-ttu-id="ff173-143">驗證從 Jenkins 該 hello Kubernetes 叢集可供存取。</span><span class="sxs-lookup"><span data-stu-id="ff173-143">Validate from Jenkins that hello Kubernetes cluster is accessible.</span></span>  <span data-ttu-id="ff173-144">toodo hello Jenkins VM 到此，SSH: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`。</span><span class="sxs-lookup"><span data-stu-id="ff173-144">toodo this, SSH into hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="ff173-145">接下來，確認 Jenkins 可以成功連線 tooyour 叢集： `kubectl cluster-info`。</span><span class="sxs-lookup"><span data-stu-id="ff173-145">Next, verify Jenkins can successfully connect tooyour cluster: `kubectl cluster-info`.</span></span>
    

## <a name="create-a-jenkins-workflow"></a><span data-ttu-id="ff173-146">建立 Jenkins 工作流程</span><span class="sxs-lookup"><span data-stu-id="ff173-146">Create a Jenkins workflow</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ff173-147">必要條件</span><span class="sxs-lookup"><span data-stu-id="ff173-147">Prerequisites</span></span>

- <span data-ttu-id="ff173-148">程式碼儲存機制的 GitHub 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ff173-148">GitHub account for code repo.</span></span>
- <span data-ttu-id="ff173-149">Docker 中樞帳戶 toostore 和更新映像。</span><span class="sxs-lookup"><span data-stu-id="ff173-149">Docker Hub account toostore and update images.</span></span>
- <span data-ttu-id="ff173-150">可以重新建立及更新的容器化應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff173-150">Containerized application that can be rebuilt and updated.</span></span> <span data-ttu-id="ff173-151">您可以使用這個以 Golang 撰寫的範例容器應用程式：https://github.com/chzbrgr71/go-web</span><span class="sxs-lookup"><span data-stu-id="ff173-151">You can use this sample container app written in Golang: https://github.com/chzbrgr71/go-web</span></span> 

> [!NOTE]
> <span data-ttu-id="ff173-152">hello 執行下列步驟必須在您自己的 GitHub 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ff173-152">hello following steps must be performed in your own GitHub account.</span></span> <span data-ttu-id="ff173-153">您可用 tooclone hello 上述儲存機制，但您必須使用您自己的帳戶 tooconfigure hello webhook 並 Jenkins 存取。</span><span class="sxs-lookup"><span data-stu-id="ff173-153">Feel free tooclone hello above repo, but you must use your own account tooconfigure hello webhooks and Jenkins access.</span></span>
>

### <a name="step-1-deploy-initial-v1-of-application"></a><span data-ttu-id="ff173-154">步驟 1︰部署應用程式的初始 v1</span><span class="sxs-lookup"><span data-stu-id="ff173-154">Step 1: Deploy initial v1 of application</span></span>
1. <span data-ttu-id="ff173-155">以下列命令的 hello 建置 hello 應用程式從 hello 開發人員電腦。</span><span class="sxs-lookup"><span data-stu-id="ff173-155">Build hello app from hello developer machine with hello following commands.</span></span> <span data-ttu-id="ff173-156">以您自己取代 `myrepo`。</span><span class="sxs-lookup"><span data-stu-id="ff173-156">Replace `myrepo` with your own.</span></span>
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. <span data-ttu-id="ff173-157">映像 tooDocker 中樞發送。</span><span class="sxs-lookup"><span data-stu-id="ff173-157">Push image tooDocker Hub.</span></span>

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. <span data-ttu-id="ff173-158">部署 toohello Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="ff173-158">Deploy toohello Kubernetes cluster.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="ff173-159">編輯 hello`go-web.yaml`檔案 tooupdate，您的容器映像和儲存機制。</span><span class="sxs-lookup"><span data-stu-id="ff173-159">Edit hello `go-web.yaml` file tooupdate your container image and repo.</span></span>
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a><span data-ttu-id="ff173-160">步驟 2︰設定 Jenkins 系統</span><span class="sxs-lookup"><span data-stu-id="ff173-160">Step 2: Configure Jenkins system</span></span>
1. <span data-ttu-id="ff173-161">按一下 [管理 Jenkins] > [設定系統]。</span><span class="sxs-lookup"><span data-stu-id="ff173-161">Click **Manage Jenkins** > **Configure System**.</span></span>
2. <span data-ttu-id="ff173-162">在 [GitHub] 下，選取 [新增 GitHub Server]。</span><span class="sxs-lookup"><span data-stu-id="ff173-162">Under **GitHub**, select **Add GitHub Server**.</span></span>
3. <span data-ttu-id="ff173-163">保留 **API URL** 為預設值。</span><span class="sxs-lookup"><span data-stu-id="ff173-163">Leave **API URL** as default.</span></span>
4. <span data-ttu-id="ff173-164">在 [認證] 下，使用 [密碼文字] 新增 Jenkins 認證。</span><span class="sxs-lookup"><span data-stu-id="ff173-164">Under **Credentials**, add a Jenkins credential using **Secret text**.</span></span> <span data-ttu-id="ff173-165">我們建議使用在您 GitHub 使用者帳戶設定中設定的 GitHub 個人存取權杖。</span><span class="sxs-lookup"><span data-stu-id="ff173-165">We recommend using GitHub personal access tokens, which are configured in your GitHub user account settings.</span></span> <span data-ttu-id="ff173-166">更多與此相關的詳細資料在[這裡。](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span><span class="sxs-lookup"><span data-stu-id="ff173-166">More details on this [here.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span></span>
5. <span data-ttu-id="ff173-167">按一下**測試連接**tooensure 正確設定。</span><span class="sxs-lookup"><span data-stu-id="ff173-167">Click **Test connection** tooensure this is configured correctly.</span></span>
6. <span data-ttu-id="ff173-168">在 [全域屬性] 下，新增環境變數 `DOCKER_HUB`，並提供您 Docker 中樞的密碼。</span><span class="sxs-lookup"><span data-stu-id="ff173-168">Under **Global Properties**, add an environment variable `DOCKER_HUB` and provide your Docker Hub password.</span></span> <span data-ttu-id="ff173-169">(這在此示範中非常有用，但實際執行案例需要更安全的方法)。</span><span class="sxs-lookup"><span data-stu-id="ff173-169">(This is useful in this demo, but a production scenario would require a more secure approach.)</span></span>
7. <span data-ttu-id="ff173-170">儲存。</span><span class="sxs-lookup"><span data-stu-id="ff173-170">Save.</span></span>

![Jenkins GitHub 存取](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-hello-jenkins-workflow"></a><span data-ttu-id="ff173-172">步驟 3： 建立 hello Jenkins 工作流程</span><span class="sxs-lookup"><span data-stu-id="ff173-172">Step 3: Create hello Jenkins workflow</span></span>
1. <span data-ttu-id="ff173-173">建立 Jenkins 項目。</span><span class="sxs-lookup"><span data-stu-id="ff173-173">Create a Jenkins item.</span></span>
2. <span data-ttu-id="ff173-174">提供名稱 (例如，「go-web」)，然後選取 **Freestyle 專案**。</span><span class="sxs-lookup"><span data-stu-id="ff173-174">Provide a name (for example, "go-web") and select **Freestyle Project**.</span></span> 
3. <span data-ttu-id="ff173-175">請檢查**GitHub 專案**並提供 hello URL tooyour GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="ff173-175">Check **GitHub project** and provide hello URL tooyour GitHub repo.</span></span>
4. <span data-ttu-id="ff173-176">在**原始程式碼管理**，提供 hello GitHub 儲存機制 URL 和認證。</span><span class="sxs-lookup"><span data-stu-id="ff173-176">In **Source Code Management**, provide hello GitHub repo URL and credentials.</span></span> 
5. <span data-ttu-id="ff173-177">新增**建置步驟**型別的**執行殼層**和使用 hello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="ff173-177">Add a **Build Step** of type **Execute shell** and use hello following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. <span data-ttu-id="ff173-178">加入另一個**建置步驟**型別的**執行殼層**和使用 hello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="ff173-178">Add another **Build Step** of type **Execute shell** and use hello following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Jenkins 建置步驟](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. <span data-ttu-id="ff173-180">儲存 hello Jenkins 項目和測試與**現在建置**。</span><span class="sxs-lookup"><span data-stu-id="ff173-180">Save hello Jenkins item and test with **Build Now**.</span></span>

### <a name="step-4-connect-github-webhook"></a><span data-ttu-id="ff173-181">步驟 4︰連線 GitHub webhook</span><span class="sxs-lookup"><span data-stu-id="ff173-181">Step 4: Connect GitHub webhook</span></span>
1. <span data-ttu-id="ff173-182">在您建立 hello Jenkins 項目，按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="ff173-182">In hello Jenkins item you created, click **Configure**.</span></span>
2. <span data-ttu-id="ff173-183">在 [建置觸發程序] 下，選取 [GITScm 輪詢的 GitHub 攔截觸發程序] 和 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="ff173-183">Under **Build Triggers**, select **GitHub hook trigger for GITScm polling** and **Save**.</span></span> <span data-ttu-id="ff173-184">這會自動設定 hello GitHub webhook。</span><span class="sxs-lookup"><span data-stu-id="ff173-184">This automatically configures hello GitHub webhook.</span></span>
3. <span data-ttu-id="ff173-185">在您 go-web 的 GitHub 儲存機制中，按一下 [設定 > Webhook]。</span><span class="sxs-lookup"><span data-stu-id="ff173-185">In your GitHub repo for go-web, click **Settings > Webhooks**.</span></span>
4. <span data-ttu-id="ff173-186">請確認該 hello Jenkins webhook URL 已成功新增。</span><span class="sxs-lookup"><span data-stu-id="ff173-186">Verify that hello Jenkins webhook URL was added successfully.</span></span> <span data-ttu-id="ff173-187">"github webhook"結尾應該 hello URL。</span><span class="sxs-lookup"><span data-stu-id="ff173-187">hello URL should end in "github-webhook".</span></span>

![Jenkins webhook 組態](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-hello-cicd-process-end-tooend"></a><span data-ttu-id="ff173-189">測試 hello CI/CD 程序結束 tooend</span><span class="sxs-lookup"><span data-stu-id="ff173-189">Test hello CI/CD process end tooend</span></span>

1. <span data-ttu-id="ff173-190">更新與 hello GitHub 儲存機制的 hello 儲存機制並發送/同步處理的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ff173-190">Update code for hello repo and push/synch with hello GitHub repository.</span></span>
2. <span data-ttu-id="ff173-191">從 hello Jenkins 主控台中，檢查 hello**建置記錄**和驗證該 hello 作業已執行。</span><span class="sxs-lookup"><span data-stu-id="ff173-191">From hello Jenkins console, check hello **Build History** and validate that hello job has run.</span></span> <span data-ttu-id="ff173-192">檢視主控台輸出 toosee 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ff173-192">View console output toosee details.</span></span>
3. <span data-ttu-id="ff173-193">從 Kubernetes，檢視詳細資料的 hello 升級部署：</span><span class="sxs-lookup"><span data-stu-id="ff173-193">From Kubernetes, view details of hello upgraded deployment:</span></span>

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a><span data-ttu-id="ff173-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ff173-194">Next steps</span></span>

- <span data-ttu-id="ff173-195">部署 Azure 容器登錄，並將影像儲存在安全的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="ff173-195">Deploy Azure Container Registry and store images in a secure repository.</span></span> <span data-ttu-id="ff173-196">請參閱[使用 Azure 容器登錄](https://docs.microsoft.com/azure/container-registry)。</span><span class="sxs-lookup"><span data-stu-id="ff173-196">See [Azure Container Registry docs](https://docs.microsoft.com/azure/container-registry).</span></span>
- <span data-ttu-id="ff173-197">建置的更複雜工作流程，其包含在 Jenkins 中的並存部署和自動化測試。</span><span class="sxs-lookup"><span data-stu-id="ff173-197">Build a more complex workflow that includes side-by-side deployment and automated tests in Jenkins.</span></span>
- <span data-ttu-id="ff173-198">如需 CI/CD 與 Jenkins 和 Kubernetes 的詳細資訊，請參閱 hello [Jenkins 部落格](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/)。</span><span class="sxs-lookup"><span data-stu-id="ff173-198">For more information about CI/CD with Jenkins and Kubernetes, see hello [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span></span>

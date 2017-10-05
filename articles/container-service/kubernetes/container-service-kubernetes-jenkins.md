---
title: "Jenkins CI/CD 在 Azure Container Service 中使用 Kubernetes | Microsoft Docs"
description: "如何使用 Jenkins 自動化 CI/CD 程序以在 Azure Container Service 中部署和升級 Kubernetes 上的容器化應用程式"
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
ms.openlocfilehash: 2078d0694fc4dd6e83ecd2792588b4254980cd78
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a><span data-ttu-id="25189-104">Jenkins 與 Azure Container Service 和 Kubernetes 整合</span><span class="sxs-lookup"><span data-stu-id="25189-104">Jenkins integration with Azure Container Service and Kubernetes</span></span> 
<span data-ttu-id="25189-105">在本教學課程中，我們逐步解說使用 Jenkins 平台將多容器應用程式的連續整合設定至 Azure Container Service Kubernetes 的程序。</span><span class="sxs-lookup"><span data-stu-id="25189-105">In this tutorial, we walk through the process to set up continuous integration of a multi-container application into Azure Container Service Kubernetes using the Jenkins platform.</span></span> <span data-ttu-id="25189-106">工作流程會更新 Docker 中樞內的容器映像，並使用部署導入升級 Kubernetes Pod。</span><span class="sxs-lookup"><span data-stu-id="25189-106">The workflow updates the container image in Docker Hub and upgrades the Kubernetes pods using a deployment rollout.</span></span> 

## <a name="high-level-process"></a><span data-ttu-id="25189-107">高階程序</span><span class="sxs-lookup"><span data-stu-id="25189-107">High level process</span></span>
<span data-ttu-id="25189-108">本文章中的基本步驟如下︰</span><span class="sxs-lookup"><span data-stu-id="25189-108">The basic steps detailed in this article are:</span></span> 
- <span data-ttu-id="25189-109">在 Container Service 中安裝 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="25189-109">Install a Kubernetes cluster in Container Service</span></span>
- <span data-ttu-id="25189-110">設定 Jenkins 和容器服務的存取權</span><span class="sxs-lookup"><span data-stu-id="25189-110">Set up Jenkins and configure access to Container Service</span></span>
- <span data-ttu-id="25189-111">建立 Jenkins 工作流程</span><span class="sxs-lookup"><span data-stu-id="25189-111">Create a Jenkins workflow</span></span>
- <span data-ttu-id="25189-112">端對端測試 CI/CD 程序</span><span class="sxs-lookup"><span data-stu-id="25189-112">Test the CI/CD process end to end</span></span>

## <a name="install-a-kubernetes-cluster"></a><span data-ttu-id="25189-113">安裝 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="25189-113">Install a Kubernetes cluster</span></span>
    
<span data-ttu-id="25189-114">使用下列步驟部署 Azure Container Service 中的 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="25189-114">Deploy the Kubernetes cluster in Azure Container Service using the following steps.</span></span> <span data-ttu-id="25189-115">完整文件位於[這裡](container-service-kubernetes-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="25189-115">Full documentation is located [here](container-service-kubernetes-walkthrough.md).</span></span>

### <a name="step-1-create-a-resource-group"></a><span data-ttu-id="25189-116">步驟 1：建立資源群組</span><span class="sxs-lookup"><span data-stu-id="25189-116">Step 1: Create a resource group</span></span>
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-the-cluster"></a><span data-ttu-id="25189-117">步驟 2︰部署叢集</span><span class="sxs-lookup"><span data-stu-id="25189-117">Step 2: Deploy the cluster</span></span>
> [!NOTE]
> <span data-ttu-id="25189-118">下列步驟需要本機 SSH 公用金鑰儲存在 ~/.ssh 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="25189-118">The following steps require a local SSH public key stored in the ~/.ssh folder.</span></span>
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

## <a name="set-up-jenkins-and-configure-access-to-container-service"></a><span data-ttu-id="25189-119">設定 Jenkins 和容器服務的存取權</span><span class="sxs-lookup"><span data-stu-id="25189-119">Set up Jenkins and configure access to Container Service</span></span>

### <a name="step-1-install-jenkins"></a><span data-ttu-id="25189-120">步驟 1：安裝 Jenkins</span><span class="sxs-lookup"><span data-stu-id="25189-120">Step 1: Install Jenkins</span></span>
1. <span data-ttu-id="25189-121">使用 Ubuntu 16.04 LTS 建立 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="25189-121">Create an Azure VM with Ubuntu 16.04 LTS.</span></span>  <span data-ttu-id="25189-122">因為在稍後的步驟中，您必須使用本機電腦上的 Bash 連線到這個 VM，請將「驗證類型」設定為「SSH 公開金鑰」，並貼上本機儲存在 ~/.ssh 資料夾中的 SSH 公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="25189-122">Since later in the steps you will need to connect to this VM using bash on your local machine, set the 'Authentication type' to 'SSH public key' and paste the SSH public key that is stored locally in your ~/.ssh folder.</span></span>  <span data-ttu-id="25189-123">此外，記下您指定的「使用者名稱」，因為在稍後步驟中，將需要這個使用者名稱才能檢視 Jenkins 儀表板以及連線到 Jenkins VM。</span><span class="sxs-lookup"><span data-stu-id="25189-123">Also, take note of the 'User name' that you specify since this user name will be needed to view the Jenkins dashboard and for connecting to the Jenkins VM in later steps.</span></span>
2. <span data-ttu-id="25189-124">透過這些[指示](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu)安裝 Jenkins。</span><span class="sxs-lookup"><span data-stu-id="25189-124">Install Jenkins via these [instructions](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span></span> <span data-ttu-id="25189-125">更詳細的教學課程在 [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04)。</span><span class="sxs-lookup"><span data-stu-id="25189-125">A more detailed tutorial is at [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span></span>
3. <span data-ttu-id="25189-126">若要在本機電腦上檢視 Jenkins 儀表板，可新增允許存取連接埠 8080 的輸入規則，從而更新可允許連接埠 8080 的 Azure 網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="25189-126">To view the Jenkins dashboard on your local machine, update the Azure network security group to allow port 8080 by adding an inbound rule that allows access to port 8080.</span></span>  <span data-ttu-id="25189-127">或者，您將需要設定連接埠轉送，方法是執行此命令：`ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span><span class="sxs-lookup"><span data-stu-id="25189-127">Alternatively, you may setup port forwarding by running this command: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span></span>
4. <span data-ttu-id="25189-128">使用瀏覽器連線到您的 Jenkins 伺服器，方法是瀏覽至公用 IP (http://<your_jenkins_public_ip>:8080)，並在第一次使用時，使用初始管理密碼將 Jenkins 儀表板解除鎖定。</span><span class="sxs-lookup"><span data-stu-id="25189-128">Connect to your Jenkins server using the browser by navigating to the public IP (http://<your_jenkins_public_ip>:8080) and unlock the Jenkins dashboard for the first time with the initial admin password.</span></span>  <span data-ttu-id="25189-129">管理密碼會儲存在 Jenkins VM 上的 /var/lib/jenkins/secrets/initialAdminPassword。</span><span class="sxs-lookup"><span data-stu-id="25189-129">The admin password is stored at /var/lib/jenkins/secrets/initialAdminPassword on the Jenkins VM.</span></span>  <span data-ttu-id="25189-130">取得此密碼的簡單方法是 SSH 至 Jenkins VM 中：`ssh <your_jenkins_user>@<your_jenkins_public_ip>`。</span><span class="sxs-lookup"><span data-stu-id="25189-130">An easy way to get this password is to SSH into the Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="25189-131">接下來，請執行：`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`。</span><span class="sxs-lookup"><span data-stu-id="25189-131">Next, run: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span></span>
5. <span data-ttu-id="25189-132">透過這些[指示](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts)在 Jenkins 機器上安裝 Docker。</span><span class="sxs-lookup"><span data-stu-id="25189-132">Install Docker on the Jenkins machine via these [instructions](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span></span> <span data-ttu-id="25189-133">這可讓 Docker 命令在 Jenkins 工作中執行。</span><span class="sxs-lookup"><span data-stu-id="25189-133">This allows for Docker commands to be run in Jenkins jobs.</span></span>
6. <span data-ttu-id="25189-134">設定 Docker 權限以允許 Jenkins 存取 Docker 端點。</span><span class="sxs-lookup"><span data-stu-id="25189-134">Configure Docker permissions to allow Jenkins to access the Docker endpoint.</span></span>

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. <span data-ttu-id="25189-135">在 Jenkins 上安裝 `kubectl` CLI。</span><span class="sxs-lookup"><span data-stu-id="25189-135">Install `kubectl` CLI on Jenkins.</span></span> <span data-ttu-id="25189-136">更多詳細資料位於[安裝和設定 kubectl](https://kubernetes.io/docs/tasks/kubectl/install/)。</span><span class="sxs-lookup"><span data-stu-id="25189-136">More details are at [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>  <span data-ttu-id="25189-137">Jenkins 作業將使用 'kubectl' 來管理及部署至 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="25189-137">Jenkins jobs will use 'kubectl' to manage and deploy to the Kubernetes cluster.</span></span>

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-to-the-kubernetes-cluster"></a><span data-ttu-id="25189-138">步驟 2︰設定 Kubernetes 叢集的存取權</span><span class="sxs-lookup"><span data-stu-id="25189-138">Step 2: Set up access to the Kubernetes cluster</span></span>

> [!NOTE]
> <span data-ttu-id="25189-139">有多個方式可以完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="25189-139">There are multiple approaches to accomplishing the following steps.</span></span> <span data-ttu-id="25189-140">使用對您最簡單的方法。</span><span class="sxs-lookup"><span data-stu-id="25189-140">Use the approach that is easiest for you.</span></span>
>

1. <span data-ttu-id="25189-141">將 `kubectl` 組態檔複製到 Jenkins 電腦，讓 Jenkins 作業能夠存取 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="25189-141">Copy the `kubectl` config file to the Jenkins machine so that Jenkins jobs have access to the Kubernetes cluster.</span></span> <span data-ttu-id="25189-142">這些指示假設您是從 Jenkins VM 以外的電腦使用 Bash，且本機 SSH 公開金鑰是儲存在電腦的 ~/.ssh 資料夾。</span><span class="sxs-lookup"><span data-stu-id="25189-142">These instructions assume that you are using bash from a different machine than the Jenkins VM and that a local SSH public key is stored in the machine's ~/.ssh folder.</span></span>

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. <span data-ttu-id="25189-143">從 Jenkins 驗證 Kubernetes 叢集可存取。</span><span class="sxs-lookup"><span data-stu-id="25189-143">Validate from Jenkins that the Kubernetes cluster is accessible.</span></span>  <span data-ttu-id="25189-144">若要這樣做，請 SSH 至 Jenkins VM 中：`ssh <your_jenkins_user>@<your_jenkins_public_ip>`。</span><span class="sxs-lookup"><span data-stu-id="25189-144">To do this, SSH into the Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="25189-145">接下來，請確認 Jenkins 可以成功連線到您的叢集：`kubectl cluster-info`。</span><span class="sxs-lookup"><span data-stu-id="25189-145">Next, verify Jenkins can successfully connect to your cluster: `kubectl cluster-info`.</span></span>
    

## <a name="create-a-jenkins-workflow"></a><span data-ttu-id="25189-146">建立 Jenkins 工作流程</span><span class="sxs-lookup"><span data-stu-id="25189-146">Create a Jenkins workflow</span></span>

### <a name="prerequisites"></a><span data-ttu-id="25189-147">必要條件</span><span class="sxs-lookup"><span data-stu-id="25189-147">Prerequisites</span></span>

- <span data-ttu-id="25189-148">程式碼儲存機制的 GitHub 帳戶。</span><span class="sxs-lookup"><span data-stu-id="25189-148">GitHub account for code repo.</span></span>
- <span data-ttu-id="25189-149">用來儲存和更新映像的 Docker 中樞帳戶。</span><span class="sxs-lookup"><span data-stu-id="25189-149">Docker Hub account to store and update images.</span></span>
- <span data-ttu-id="25189-150">可以重新建立及更新的容器化應用程式。</span><span class="sxs-lookup"><span data-stu-id="25189-150">Containerized application that can be rebuilt and updated.</span></span> <span data-ttu-id="25189-151">您可以使用這個以 Golang 撰寫的範例容器應用程式：https://github.com/chzbrgr71/go-web</span><span class="sxs-lookup"><span data-stu-id="25189-151">You can use this sample container app written in Golang: https://github.com/chzbrgr71/go-web</span></span> 

> [!NOTE]
> <span data-ttu-id="25189-152">必須在您自己的 GitHub 帳戶中執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="25189-152">The following steps must be performed in your own GitHub account.</span></span> <span data-ttu-id="25189-153">隨意複製上述的儲存機制，但您必須使用自己的帳戶來設定 webhook 和 Jenkins 存取。</span><span class="sxs-lookup"><span data-stu-id="25189-153">Feel free to clone the above repo, but you must use your own account to configure the webhooks and Jenkins access.</span></span>
>

### <a name="step-1-deploy-initial-v1-of-application"></a><span data-ttu-id="25189-154">步驟 1︰部署應用程式的初始 v1</span><span class="sxs-lookup"><span data-stu-id="25189-154">Step 1: Deploy initial v1 of application</span></span>
1. <span data-ttu-id="25189-155">使用下列命令從開發人員機器建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="25189-155">Build the app from the developer machine with the following commands.</span></span> <span data-ttu-id="25189-156">以您自己取代 `myrepo`。</span><span class="sxs-lookup"><span data-stu-id="25189-156">Replace `myrepo` with your own.</span></span>
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. <span data-ttu-id="25189-157">將映像推送至 Docker 中樞。</span><span class="sxs-lookup"><span data-stu-id="25189-157">Push image to Docker Hub.</span></span>

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. <span data-ttu-id="25189-158">部署 Kubernetes 叢集。</span><span class="sxs-lookup"><span data-stu-id="25189-158">Deploy to the Kubernetes cluster.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="25189-159">編輯 `go-web.yaml` 檔案以更新容器映像和儲存機制。</span><span class="sxs-lookup"><span data-stu-id="25189-159">Edit the `go-web.yaml` file to update your container image and repo.</span></span>
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a><span data-ttu-id="25189-160">步驟 2︰設定 Jenkins 系統</span><span class="sxs-lookup"><span data-stu-id="25189-160">Step 2: Configure Jenkins system</span></span>
1. <span data-ttu-id="25189-161">按一下 [管理 Jenkins] > [設定系統]。</span><span class="sxs-lookup"><span data-stu-id="25189-161">Click **Manage Jenkins** > **Configure System**.</span></span>
2. <span data-ttu-id="25189-162">在 [GitHub] 下，選取 [新增 GitHub Server]。</span><span class="sxs-lookup"><span data-stu-id="25189-162">Under **GitHub**, select **Add GitHub Server**.</span></span>
3. <span data-ttu-id="25189-163">保留 **API URL** 為預設值。</span><span class="sxs-lookup"><span data-stu-id="25189-163">Leave **API URL** as default.</span></span>
4. <span data-ttu-id="25189-164">在 [認證] 下，使用 [密碼文字] 新增 Jenkins 認證。</span><span class="sxs-lookup"><span data-stu-id="25189-164">Under **Credentials**, add a Jenkins credential using **Secret text**.</span></span> <span data-ttu-id="25189-165">我們建議使用在您 GitHub 使用者帳戶設定中設定的 GitHub 個人存取權杖。</span><span class="sxs-lookup"><span data-stu-id="25189-165">We recommend using GitHub personal access tokens, which are configured in your GitHub user account settings.</span></span> <span data-ttu-id="25189-166">更多與此相關的詳細資料在[這裡。](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span><span class="sxs-lookup"><span data-stu-id="25189-166">More details on this [here.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span></span>
5. <span data-ttu-id="25189-167">按一下 [測試連接] 以確保正確設定。</span><span class="sxs-lookup"><span data-stu-id="25189-167">Click **Test connection** to ensure this is configured correctly.</span></span>
6. <span data-ttu-id="25189-168">在 [全域屬性] 下，新增環境變數 `DOCKER_HUB`，並提供您 Docker 中樞的密碼。</span><span class="sxs-lookup"><span data-stu-id="25189-168">Under **Global Properties**, add an environment variable `DOCKER_HUB` and provide your Docker Hub password.</span></span> <span data-ttu-id="25189-169">(這在此示範中非常有用，但實際執行案例需要更安全的方法)。</span><span class="sxs-lookup"><span data-stu-id="25189-169">(This is useful in this demo, but a production scenario would require a more secure approach.)</span></span>
7. <span data-ttu-id="25189-170">儲存。</span><span class="sxs-lookup"><span data-stu-id="25189-170">Save.</span></span>

![Jenkins GitHub 存取](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-the-jenkins-workflow"></a><span data-ttu-id="25189-172">步驟 3︰建立 Jenkins 工作流程</span><span class="sxs-lookup"><span data-stu-id="25189-172">Step 3: Create the Jenkins workflow</span></span>
1. <span data-ttu-id="25189-173">建立 Jenkins 項目。</span><span class="sxs-lookup"><span data-stu-id="25189-173">Create a Jenkins item.</span></span>
2. <span data-ttu-id="25189-174">提供名稱 (例如，「go-web」)，然後選取 **Freestyle 專案**。</span><span class="sxs-lookup"><span data-stu-id="25189-174">Provide a name (for example, "go-web") and select **Freestyle Project**.</span></span> 
3. <span data-ttu-id="25189-175">檢查 **GitHub 專案**，並提供您 GitHub 儲存機制的 URL。</span><span class="sxs-lookup"><span data-stu-id="25189-175">Check **GitHub project** and provide the URL to your GitHub repo.</span></span>
4. <span data-ttu-id="25189-176">在**原始程式碼管理**中，提供 GitHub 儲存機制 URL 和認證。</span><span class="sxs-lookup"><span data-stu-id="25189-176">In **Source Code Management**, provide the GitHub repo URL and credentials.</span></span> 
5. <span data-ttu-id="25189-177">新增 [執行殼層] 類型的 [建置步驟]，並使用下列文字︰</span><span class="sxs-lookup"><span data-stu-id="25189-177">Add a **Build Step** of type **Execute shell** and use the following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. <span data-ttu-id="25189-178">新增另一個 [執行殼層] 類型的 [建置步驟]，並使用下列文字︰</span><span class="sxs-lookup"><span data-stu-id="25189-178">Add another **Build Step** of type **Execute shell** and use the following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Jenkins 建置步驟](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. <span data-ttu-id="25189-180">儲存 Jenkins 項目並以 [立即建置] 測試。</span><span class="sxs-lookup"><span data-stu-id="25189-180">Save the Jenkins item and test with **Build Now**.</span></span>

### <a name="step-4-connect-github-webhook"></a><span data-ttu-id="25189-181">步驟 4︰連線 GitHub webhook</span><span class="sxs-lookup"><span data-stu-id="25189-181">Step 4: Connect GitHub webhook</span></span>
1. <span data-ttu-id="25189-182">在您建立的 Jenkins 項目中，按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="25189-182">In the Jenkins item you created, click **Configure**.</span></span>
2. <span data-ttu-id="25189-183">在 [建置觸發程序] 下，選取 [GITScm 輪詢的 GitHub 攔截觸發程序] 和 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="25189-183">Under **Build Triggers**, select **GitHub hook trigger for GITScm polling** and **Save**.</span></span> <span data-ttu-id="25189-184">這會自動設定 GitHub webhook。</span><span class="sxs-lookup"><span data-stu-id="25189-184">This automatically configures the GitHub webhook.</span></span>
3. <span data-ttu-id="25189-185">在您 go-web 的 GitHub 儲存機制中，按一下 [設定 > Webhook]。</span><span class="sxs-lookup"><span data-stu-id="25189-185">In your GitHub repo for go-web, click **Settings > Webhooks**.</span></span>
4. <span data-ttu-id="25189-186">請確認已成功新增 Jenkins webhook URL。</span><span class="sxs-lookup"><span data-stu-id="25189-186">Verify that the Jenkins webhook URL was added successfully.</span></span> <span data-ttu-id="25189-187">URL 應該以「github-webhook」結束。</span><span class="sxs-lookup"><span data-stu-id="25189-187">The URL should end in "github-webhook".</span></span>

![Jenkins webhook 組態](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-the-cicd-process-end-to-end"></a><span data-ttu-id="25189-189">端對端測試 CI/CD 程序</span><span class="sxs-lookup"><span data-stu-id="25189-189">Test the CI/CD process end to end</span></span>

1. <span data-ttu-id="25189-190">更新儲存機制的程式碼並使用 GitHub 儲存機制推入/同步處理。</span><span class="sxs-lookup"><span data-stu-id="25189-190">Update code for the repo and push/synch with the GitHub repository.</span></span>
2. <span data-ttu-id="25189-191">從 Jenkins 主控台中，檢查**建置記錄**並驗證作業已執行。</span><span class="sxs-lookup"><span data-stu-id="25189-191">From the Jenkins console, check the **Build History** and validate that the job has run.</span></span> <span data-ttu-id="25189-192">檢視主控台輸出以查看詳細資料。</span><span class="sxs-lookup"><span data-stu-id="25189-192">View console output to see details.</span></span>
3. <span data-ttu-id="25189-193">從 Kubernetes，檢視已升級部署的詳細資訊︰</span><span class="sxs-lookup"><span data-stu-id="25189-193">From Kubernetes, view details of the upgraded deployment:</span></span>

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a><span data-ttu-id="25189-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="25189-194">Next steps</span></span>

- <span data-ttu-id="25189-195">部署 Azure 容器登錄，並將影像儲存在安全的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="25189-195">Deploy Azure Container Registry and store images in a secure repository.</span></span> <span data-ttu-id="25189-196">請參閱[使用 Azure 容器登錄](https://docs.microsoft.com/azure/container-registry)。</span><span class="sxs-lookup"><span data-stu-id="25189-196">See [Azure Container Registry docs](https://docs.microsoft.com/azure/container-registry).</span></span>
- <span data-ttu-id="25189-197">建置的更複雜工作流程，其包含在 Jenkins 中的並存部署和自動化測試。</span><span class="sxs-lookup"><span data-stu-id="25189-197">Build a more complex workflow that includes side-by-side deployment and automated tests in Jenkins.</span></span>
- <span data-ttu-id="25189-198">如需關於 CI/CD 與 Jenkins 和 Kubernetes 的詳細資訊，請參閱 [Jenkins 部落格](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/)。</span><span class="sxs-lookup"><span data-stu-id="25189-198">For more information about CI/CD with Jenkins and Kubernetes, see the [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span></span>

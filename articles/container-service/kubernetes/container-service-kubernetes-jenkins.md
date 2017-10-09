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
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a>Jenkins 與 Azure Container Service 和 Kubernetes 整合 
在本教學課程中，我們逐步 hello 程序 tooset 多容器應用程式的連續整合到 Azure 容器服務 Kubernetes 使用 hello Jenkins 平台。 hello 工作流程更新中 Docker Hub hello 容器映像，及升級 hello Kubernetes pod 使用部署的首度發行。 

## <a name="high-level-process"></a>高階程序
此文件中詳述的 hello 基本步驟如下： 
- 在 Container Service 中安裝 Kubernetes 叢集
- Jenkins 安裝和設定存取 tooContainer 服務
- 建立 Jenkins 工作流程
- 測試 hello CI/CD 程序結束 tooend

## <a name="install-a-kubernetes-cluster"></a>安裝 Kubernetes 叢集
    
部署使用下列步驟的 hello Azure 容器服務中的 hello Kubernetes 叢集。 完整文件位於[這裡](container-service-kubernetes-walkthrough.md)。

### <a name="step-1-create-a-resource-group"></a>步驟 1：建立資源群組
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-hello-cluster"></a>步驟 2： 部署的 hello 叢集
> [!NOTE]
> hello 以下步驟需要本機的 SSH 公開金鑰機碼，並儲存在 hello ~/.ssh 資料夾中。
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

## <a name="set-up-jenkins-and-configure-access-toocontainer-service"></a>Jenkins 安裝和設定存取 tooContainer 服務

### <a name="step-1-install-jenkins"></a>步驟 1：安裝 Jenkins
1. 使用 Ubuntu 16.04 LTS 建立 Azure VM。  因為 hello 稍後會引導您將需要 tooconnect toothis VM 使用撞在本機電腦，設定 hello '驗證類型' too'SSH 公開金鑰 ' 和貼上 hello SSH 公開金鑰存放在本機 ~/.ssh 資料夾中。  此外，請注意，指定由於這個使用者名稱會為所需的 tooview hello Jenkins 儀表板以及連接 toohello Jenkins VM 在稍後步驟中的 hello '使用者名稱'。
2. 透過這些[指示](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu)安裝 Jenkins。 更詳細的教學課程在 [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04)。
3. tooview hello Jenkins 儀表板，在本機電腦上的，藉由新增輸入的規則允許存取 tooport 8080 更新 hello Azure 網路安全性群組 tooallow 連接埠 8080。  或者，您將需要設定連接埠轉送，方法是執行此命令：`ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`
4. Tooyour Jenkins 伺服器使用 hello 瀏覽器瀏覽 toohello 公用 IP 連接 (http:// < your_jenkins_public_ip >: 8080) 和解除鎖定 hello hello 的 Jenkins 儀表板與 hello 初始管理密碼的第一次。  hello 系統管理員密碼會儲存在 /var/lib/jenkins/secrets/initialAdminPassword hello Jenkins VM 上。  此密碼是到 tooSSH 輕鬆 tooget hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`。  接下來，請執行：`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`。
5. 透過這些的 hello Jenkins 機器上安裝 Docker[指示](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts)。 這可讓 Docker 命令 toobe Jenkins 作業中執行。
6. 設定 Docker 權限 tooallow Jenkins tooaccess hello Docker 端點。

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. 在 Jenkins 上安裝 `kubectl` CLI。 更多詳細資料位於[安裝和設定 kubectl](https://kubernetes.io/docs/tasks/kubectl/install/)。  Jenkins 作業將會使用 'kubectl' toomanage 和部署 toohello Kubernetes 叢集。

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-toohello-kubernetes-cluster"></a>步驟 2： 設定存取 toohello Kubernetes 叢集

> [!NOTE]
> 有多個方法 tooaccomplishing hello 下列步驟。 使用 hello 做為您的最簡單的方法。
>

1. 複製 hello`kubectl`組態檔案 toohello Jenkins 機器，所以 Jenkins 工作需要存取 toohello Kubernetes 叢集。 這些指示假設您比 hello Jenkins VM 使用 bash 從不同的電腦和本機 SSH 公開金鑰，會儲存在 hello 機器 ~/.ssh 資料夾。

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. 驗證從 Jenkins 該 hello Kubernetes 叢集可供存取。  toodo hello Jenkins VM 到此，SSH: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`。  接下來，確認 Jenkins 可以成功連線 tooyour 叢集： `kubectl cluster-info`。
    

## <a name="create-a-jenkins-workflow"></a>建立 Jenkins 工作流程

### <a name="prerequisites"></a>必要條件

- 程式碼儲存機制的 GitHub 帳戶。
- Docker 中樞帳戶 toostore 和更新映像。
- 可以重新建立及更新的容器化應用程式。 您可以使用這個以 Golang 撰寫的範例容器應用程式：https://github.com/chzbrgr71/go-web 

> [!NOTE]
> hello 執行下列步驟必須在您自己的 GitHub 帳戶。 您可用 tooclone hello 上述儲存機制，但您必須使用您自己的帳戶 tooconfigure hello webhook 並 Jenkins 存取。
>

### <a name="step-1-deploy-initial-v1-of-application"></a>步驟 1︰部署應用程式的初始 v1
1. 以下列命令的 hello 建置 hello 應用程式從 hello 開發人員電腦。 以您自己取代 `myrepo`。
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. 映像 tooDocker 中樞發送。

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. 部署 toohello Kubernetes 叢集。
    
    > [!NOTE] 
    > 編輯 hello`go-web.yaml`檔案 tooupdate，您的容器映像和儲存機制。
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a>步驟 2︰設定 Jenkins 系統
1. 按一下 [管理 Jenkins] > [設定系統]。
2. 在 [GitHub] 下，選取 [新增 GitHub Server]。
3. 保留 **API URL** 為預設值。
4. 在 [認證] 下，使用 [密碼文字] 新增 Jenkins 認證。 我們建議使用在您 GitHub 使用者帳戶設定中設定的 GitHub 個人存取權杖。 更多與此相關的詳細資料在[這裡。](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)
5. 按一下**測試連接**tooensure 正確設定。
6. 在 [全域屬性] 下，新增環境變數 `DOCKER_HUB`，並提供您 Docker 中樞的密碼。 (這在此示範中非常有用，但實際執行案例需要更安全的方法)。
7. 儲存。

![Jenkins GitHub 存取](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-hello-jenkins-workflow"></a>步驟 3： 建立 hello Jenkins 工作流程
1. 建立 Jenkins 項目。
2. 提供名稱 (例如，「go-web」)，然後選取 **Freestyle 專案**。 
3. 請檢查**GitHub 專案**並提供 hello URL tooyour GitHub 儲存機制。
4. 在**原始程式碼管理**，提供 hello GitHub 儲存機制 URL 和認證。 
5. 新增**建置步驟**型別的**執行殼層**和使用 hello 下列文字：

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. 加入另一個**建置步驟**型別的**執行殼層**和使用 hello 下列文字：

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Jenkins 建置步驟](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. 儲存 hello Jenkins 項目和測試與**現在建置**。

### <a name="step-4-connect-github-webhook"></a>步驟 4︰連線 GitHub webhook
1. 在您建立 hello Jenkins 項目，按一下**設定**。
2. 在 [建置觸發程序] 下，選取 [GITScm 輪詢的 GitHub 攔截觸發程序] 和 [儲存]。 這會自動設定 hello GitHub webhook。
3. 在您 go-web 的 GitHub 儲存機制中，按一下 [設定 > Webhook]。
4. 請確認該 hello Jenkins webhook URL 已成功新增。 "github webhook"結尾應該 hello URL。

![Jenkins webhook 組態](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-hello-cicd-process-end-tooend"></a>測試 hello CI/CD 程序結束 tooend

1. 更新與 hello GitHub 儲存機制的 hello 儲存機制並發送/同步處理的程式碼。
2. 從 hello Jenkins 主控台中，檢查 hello**建置記錄**和驗證該 hello 作業已執行。 檢視主控台輸出 toosee 詳細資料。
3. 從 Kubernetes，檢視詳細資料的 hello 升級部署：

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a>後續步驟

- 部署 Azure 容器登錄，並將影像儲存在安全的儲存機制。 請參閱[使用 Azure 容器登錄](https://docs.microsoft.com/azure/container-registry)。
- 建置的更複雜工作流程，其包含在 Jenkins 中的並存部署和自動化測試。
- 如需 CI/CD 與 Jenkins 和 Kubernetes 的詳細資訊，請參閱 hello [Jenkins 部落格](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/)。

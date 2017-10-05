---
title: "使用 Jenkins 連續建置和整合 Azure Service Fabric Linux Java 應用程式 | Microsoft Docs"
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
ms.openlocfilehash: d9372407540d903acca5b1639a2d9ceb0bf3c571
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-jenkins-to-build-and-deploy-your-linux-java-application"></a><span data-ttu-id="3fd80-103">使用 Jenkins 建置和部署您的 Linux Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="3fd80-103">Use Jenkins to build and deploy your Linux Java application</span></span>
<span data-ttu-id="3fd80-104">Jenkins 是連續整合和部署應用程式的熱門工具。</span><span class="sxs-lookup"><span data-stu-id="3fd80-104">Jenkins is a popular tool for continuous integration and deployment of your apps.</span></span> <span data-ttu-id="3fd80-105">以下是使用 Jenkins 建置和部署 Azure Service Fabric 應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="3fd80-105">Here's how to build and deploy your Azure Service Fabric application by using Jenkins.</span></span>

## <a name="general-prerequisites"></a><span data-ttu-id="3fd80-106">一般先決條件</span><span class="sxs-lookup"><span data-stu-id="3fd80-106">General prerequisites</span></span>
- <span data-ttu-id="3fd80-107">在本機安裝 Git。</span><span class="sxs-lookup"><span data-stu-id="3fd80-107">Have Git installed locally.</span></span> <span data-ttu-id="3fd80-108">您可以根據您的作業系統，從 [Git 下載頁面](https://git-scm.com/downloads)安裝適當的 Git 版本。</span><span class="sxs-lookup"><span data-stu-id="3fd80-108">You can install the appropriate Git version from [the Git downloads page](https://git-scm.com/downloads), based on your operating system.</span></span> <span data-ttu-id="3fd80-109">如果您不熟悉 Git，請從 [Git 文件](https://git-scm.com/docs)深入了解。</span><span class="sxs-lookup"><span data-stu-id="3fd80-109">If you are new to Git, learn more about it from the [Git documentation](https://git-scm.com/docs).</span></span>
- <span data-ttu-id="3fd80-110">備妥 Service Fabric Jenkins 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="3fd80-110">Have the Service Fabric Jenkins plug-in handy.</span></span> <span data-ttu-id="3fd80-111">您可以從 [Service Fabric 下載](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi)進行下載。</span><span class="sxs-lookup"><span data-stu-id="3fd80-111">You can download it from [Service Fabric downloads](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi).</span></span>

## <a name="set-up-jenkins-inside-a-service-fabric-cluster"></a><span data-ttu-id="3fd80-112">在 Service Fabric 叢集內設定 Jenkins</span><span class="sxs-lookup"><span data-stu-id="3fd80-112">Set up Jenkins inside a Service Fabric cluster</span></span>

<span data-ttu-id="3fd80-113">您可以在 Service Fabric 叢集內部或外部設定 Jenkins。</span><span class="sxs-lookup"><span data-stu-id="3fd80-113">You can set up Jenkins either inside or outside a Service Fabric cluster.</span></span> <span data-ttu-id="3fd80-114">下列小節說明如何在叢集內設定它，同時又使用 Azure 儲存體帳戶來儲存容器執行個體的狀態。</span><span class="sxs-lookup"><span data-stu-id="3fd80-114">The following sections show how to set it up inside a cluster while using an Azure storage account to save the state of the container instance.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3fd80-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="3fd80-115">Prerequisites</span></span>
1. <span data-ttu-id="3fd80-116">讓 Service Fabric Linux 叢集準備就緒。</span><span class="sxs-lookup"><span data-stu-id="3fd80-116">Have a Service Fabric Linux cluster ready.</span></span> <span data-ttu-id="3fd80-117">從 Azure 入口網站建立的 Service Fabric 叢集已安裝 Docker。</span><span class="sxs-lookup"><span data-stu-id="3fd80-117">A Service Fabric cluster created from the Azure portal already has Docker installed.</span></span> <span data-ttu-id="3fd80-118">如果您在本機執行叢集，請使用命令 ``docker info``來檢查是否已安裝 Docker。</span><span class="sxs-lookup"><span data-stu-id="3fd80-118">If you are running the cluster locally, check if Docker is installed by using the command ``docker info``.</span></span> <span data-ttu-id="3fd80-119">如果未安裝，使用下列命令據以安裝︰</span><span class="sxs-lookup"><span data-stu-id="3fd80-119">If it is not installed, install it accordingly by using the following commands:</span></span>

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```
2. <span data-ttu-id="3fd80-120">使用下列步驟將 Service Fabric 容器應用程式部署至叢集：</span><span class="sxs-lookup"><span data-stu-id="3fd80-120">Have the Service Fabric container application deployed on the cluster, by using the following steps:</span></span>

  ```sh
git clone https://github.com/Azure-Samples/service-fabric-java-getting-started.git
cd service-fabric-java-getting-started/Services/JenkinsDocker/
```

3. <span data-ttu-id="3fd80-121">您需要 Azure 儲存體檔案共用的連線選項詳細資料，這是您要保存 Jenkins 容器執行個體狀態的位置。</span><span class="sxs-lookup"><span data-stu-id="3fd80-121">You need the connect option details of the Azure storage file-share, where you want to persist the state of the Jenkins container instance.</span></span> <span data-ttu-id="3fd80-122">如果您使用 Microsoft Azure 入口網站來進行相同的操作，請依照步驟來建立 Azure 儲存體帳戶 (例如 ``sfjenkinsstorage1``)。</span><span class="sxs-lookup"><span data-stu-id="3fd80-122">If you are using the Microsoft Azure portal for the same, please follow the steps - Create an Azure storage account, say ``sfjenkinsstorage1``.</span></span> <span data-ttu-id="3fd80-123">在該儲存體帳戶底下建立一個「檔案共用」(例如 ``sfjenkins``)。</span><span class="sxs-lookup"><span data-stu-id="3fd80-123">Create a **File Share** under that storage account, say ``sfjenkins``.</span></span> <span data-ttu-id="3fd80-124">針對該檔案共用按一下 [連接]，並記下 [正在從 Linux 連線] 底下顯示的值，例如這會看起來如下：</span><span class="sxs-lookup"><span data-stu-id="3fd80-124">Click on **Connect** for the file-share and note the values it displays under **Connecting from Linux**, say this would look like as follows -</span></span>
```sh
sudo mount -t cifs //sfjenkinsstorage1.file.core.windows.net/sfjenkins [mount point] -o vers=3.0,username=sfjenkinsstorage1,password=<storage_key>,dir_mode=0777,file_mode=0777
```

4. <span data-ttu-id="3fd80-125">將 ```setupentrypoint.sh``` 指令碼中的預留位置值更新成對應的 Azure 儲存體詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3fd80-125">Update the placeholder values in the ```setupentrypoint.sh``` script with corresponding azure-storage details.</span></span>
```sh
vi JenkinsSF/JenkinsOnSF/Code/setupentrypoint.sh
```
<span data-ttu-id="3fd80-126">以來自上述第 3 點中連線輸出的 ``//sfjenkinsstorage1.file.core.windows.net/sfjenkins`` 值取代 ``[REMOTE_FILE_SHARE_LOCATION]``。</span><span class="sxs-lookup"><span data-stu-id="3fd80-126">Replace ``[REMOTE_FILE_SHARE_LOCATION]`` with the value ``//sfjenkinsstorage1.file.core.windows.net/sfjenkins`` from the output of the connect in point 3 above.</span></span>
<span data-ttu-id="3fd80-127">以來自上述第 3 點的 ``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777`` 值取代 ``[FILE_SHARE_CONNECT_OPTIONS_STRING]``。</span><span class="sxs-lookup"><span data-stu-id="3fd80-127">Replace ``[FILE_SHARE_CONNECT_OPTIONS_STRING]`` with the value ``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777`` from point 3 above.</span></span>

5. <span data-ttu-id="3fd80-128">連線至叢集並安裝容器應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fd80-128">Connect to the cluster and install the container application.</span></span>
```azurecli
sfctl cluster select --endpoint http://PublicIPorFQDN:19080   # cluster connect command
bash Scripts/install.sh
```
<span data-ttu-id="3fd80-129">這會在叢集上安裝 Jenkins 容器，您可以使用 Service Fabric Explorer 加以監視。</span><span class="sxs-lookup"><span data-stu-id="3fd80-129">This installs a Jenkins container on the cluster, and can be monitored by using the Service Fabric Explorer.</span></span>

### <a name="steps"></a><span data-ttu-id="3fd80-130">步驟</span><span class="sxs-lookup"><span data-stu-id="3fd80-130">Steps</span></span>
1. <span data-ttu-id="3fd80-131">從瀏覽器中，前往 ``http://PublicIPorFQDN:8081``。</span><span class="sxs-lookup"><span data-stu-id="3fd80-131">From your browser, go to ``http://PublicIPorFQDN:8081``.</span></span> <span data-ttu-id="3fd80-132">它會提供登入所需之初始管理密碼的路徑。</span><span class="sxs-lookup"><span data-stu-id="3fd80-132">It provides the path of the initial admin password required to sign in.</span></span> <span data-ttu-id="3fd80-133">您可以繼續使用 Jenkins 做為管理員使用者。</span><span class="sxs-lookup"><span data-stu-id="3fd80-133">You can continue to use Jenkins as an admin user.</span></span> <span data-ttu-id="3fd80-134">或者您可以在使用初始管理帳戶登入之後建立及變更使用者。</span><span class="sxs-lookup"><span data-stu-id="3fd80-134">Or you can create and change the user, after you sign in with the initial admin account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3fd80-135">建立叢集時，請確定 8081 連接埠指定為應用程式端點連接埠。</span><span class="sxs-lookup"><span data-stu-id="3fd80-135">Ensure that the 8081 port is specified as the application endpoint port while you are creating the cluster.</span></span>
   >

2. <span data-ttu-id="3fd80-136">使用 ``docker ps -a`` 取得容器執行個體識別碼。</span><span class="sxs-lookup"><span data-stu-id="3fd80-136">Get the container instance ID by using ``docker ps -a``.</span></span>
3. <span data-ttu-id="3fd80-137">以 Secure Shell (SSH) 登入容器，並貼上您在 Jenkins 入口網站中看到的路徑。</span><span class="sxs-lookup"><span data-stu-id="3fd80-137">Secure Shell (SSH) sign in to the container, and paste the path you were shown on the Jenkins portal.</span></span> <span data-ttu-id="3fd80-138">例如，如果在入口網站中它顯示路徑 `PATH_TO_INITIAL_ADMIN_PASSWORD`，執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="3fd80-138">For example, if in the portal it shows the path `PATH_TO_INITIAL_ADMIN_PASSWORD`, run the following:</span></span>

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash   # This takes you inside Docker shell
  cat PATH_TO_INITIAL_ADMIN_PASSWORD
  ```

4. <span data-ttu-id="3fd80-139">設定 GitHub 以 Jenkins，方法為使用[產生新的 SSH 金鑰，並將它新增至 SSH 代理程式](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)中提到的步驟。</span><span class="sxs-lookup"><span data-stu-id="3fd80-139">Set up GitHub to work with Jenkins, by using the steps mentioned in [Generating a new SSH key and adding it to the SSH agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).</span></span>
    * <span data-ttu-id="3fd80-140">使用 GitHub 所提供的指示產生 SSH 金鑰，並將 SSH 金鑰新增至裝載存放庫的 GitHub 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fd80-140">Use the instructions provided by GitHub to generate the SSH key, and to add the SSH key to the GitHub account that is hosting your repository.</span></span>
    * <span data-ttu-id="3fd80-141">在 Jenkins Docker 殼層 (而非在主機上) 執行上述連結內所提到的命令。</span><span class="sxs-lookup"><span data-stu-id="3fd80-141">Run the commands mentioned in the preceding link in the Jenkins Docker shell (and not on your host).</span></span>
    * <span data-ttu-id="3fd80-142">若要從主機登入 Jenkins 殼層，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="3fd80-142">To sign in to the Jenkins shell from your host, use the following command:</span></span>

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
  ```

## <a name="set-up-jenkins-outside-a-service-fabric-cluster"></a><span data-ttu-id="3fd80-143">在 Service Fabric 叢集外設定 Jenkins</span><span class="sxs-lookup"><span data-stu-id="3fd80-143">Set up Jenkins outside a Service Fabric cluster</span></span>

<span data-ttu-id="3fd80-144">您可以在 Service Fabric 叢集內部或外部設定 Jenkins。</span><span class="sxs-lookup"><span data-stu-id="3fd80-144">You can set up Jenkins either inside or outside of a Service Fabric cluster.</span></span> <span data-ttu-id="3fd80-145">下列各節顯示如何在叢集外設定。</span><span class="sxs-lookup"><span data-stu-id="3fd80-145">The following sections show how to set it up outside a cluster.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3fd80-146">必要條件</span><span class="sxs-lookup"><span data-stu-id="3fd80-146">Prerequisites</span></span>
<span data-ttu-id="3fd80-147">您必須安裝 Docker。</span><span class="sxs-lookup"><span data-stu-id="3fd80-147">You need to have Docker installed.</span></span> <span data-ttu-id="3fd80-148">使用下列命令可從終端機安裝 Docker︰</span><span class="sxs-lookup"><span data-stu-id="3fd80-148">The following commands can be used to install Docker from the terminal:</span></span>

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```

<span data-ttu-id="3fd80-149">現在，當您在終端機執行 ``docker info``，您應該會在輸出中看到 Docker 服務正在執行。</span><span class="sxs-lookup"><span data-stu-id="3fd80-149">Now when you run ``docker info`` in the terminal, you should see in the output that the Docker service is running.</span></span>

### <a name="steps"></a><span data-ttu-id="3fd80-150">步驟</span><span class="sxs-lookup"><span data-stu-id="3fd80-150">Steps</span></span>
  1. <span data-ttu-id="3fd80-151">提取 Service Fabric Jenkins 容器映像︰``docker pull raunakpandya/jenkins:v1``</span><span class="sxs-lookup"><span data-stu-id="3fd80-151">Pull the Service Fabric Jenkins container image: ``docker pull raunakpandya/jenkins:v1``</span></span>
  2. <span data-ttu-id="3fd80-152">執行容器映像︰``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``</span><span class="sxs-lookup"><span data-stu-id="3fd80-152">Run the container image: ``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``</span></span>
  3. <span data-ttu-id="3fd80-153">取得容器映像執行個體的識別碼。</span><span class="sxs-lookup"><span data-stu-id="3fd80-153">Get the ID of the container image instance.</span></span> <span data-ttu-id="3fd80-154">您可以使用命令 ``docker ps –a`` 列出所有 Docker 容器</span><span class="sxs-lookup"><span data-stu-id="3fd80-154">You can list all the Docker containers with the command ``docker ps –a``</span></span>
  4. <span data-ttu-id="3fd80-155">使用下列步驟登入 Jenkins 入口網站︰</span><span class="sxs-lookup"><span data-stu-id="3fd80-155">Sign in to the Jenkins portal by using the following steps:</span></span>

    * ```sh
    docker exec [first-four-digits-of-container-ID] cat /var/jenkins_home/secrets/initialAdminPassword
    ```
    <span data-ttu-id="3fd80-156">如果容器識別碼是 2d24a73b5964，請使用 2d24。</span><span class="sxs-lookup"><span data-stu-id="3fd80-156">If container ID is 2d24a73b5964, use 2d24.</span></span>
    * <span data-ttu-id="3fd80-157">從入口網站 (``http://<HOST-IP>:8080``) 登入 Jenkins 儀表板需要此密碼</span><span class="sxs-lookup"><span data-stu-id="3fd80-157">This password is required for signing in to the Jenkins dashboard from portal, which is ``http://<HOST-IP>:8080``</span></span>
    * <span data-ttu-id="3fd80-158">第一次登入之後，您可以建立您自己的使用者帳戶，並針對未來目的使用該帳戶，或者您可以繼續使用系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fd80-158">After you sign in for the first time, you can create your own user account and use that for future purposes, or you can continue to use the administrator account.</span></span> <span data-ttu-id="3fd80-159">您建立使用者之後，需要繼續使用。</span><span class="sxs-lookup"><span data-stu-id="3fd80-159">After you create a user, you need to continue with that.</span></span>
  5. <span data-ttu-id="3fd80-160">設定 GitHub 以 Jenkins，方法為使用[產生新的 SSH 金鑰，並將它新增至 SSH 代理程式](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)中提到的步驟。</span><span class="sxs-lookup"><span data-stu-id="3fd80-160">Set up GitHub to work with Jenkins, by using the steps mentioned in [Generating a new SSH key and adding it to the SSH agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).</span></span>
        * <span data-ttu-id="3fd80-161">使用 GitHub 所提供的指示產生 SSH 金鑰，並將 SSH 金鑰新增至裝載存放庫的 GitHub 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fd80-161">Use the instructions provided by GitHub to generate the SSH key, and to add the SSH key to the GitHub account that is hosting the repository.</span></span>
        * <span data-ttu-id="3fd80-162">在 Jenkins Docker 殼層 (而非在主機上) 執行上述連結內所提到的命令。</span><span class="sxs-lookup"><span data-stu-id="3fd80-162">Run the commands mentioned in the preceding link in the Jenkins Docker shell (and not on your host).</span></span>
      * <span data-ttu-id="3fd80-163">若要從主機登入 Jenkins 殼層，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="3fd80-163">To sign in to the Jenkins shell from your host, use the following commands:</span></span>

      ```sh
      docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
      ```

<span data-ttu-id="3fd80-164">請確定 Jenkins 容器映像所裝載的叢集或電腦具有公開 IP。</span><span class="sxs-lookup"><span data-stu-id="3fd80-164">Ensure that the cluster or machine where the Jenkins container image is hosted has a public-facing IP.</span></span> <span data-ttu-id="3fd80-165">這可讓 Jenkins 執行個體接收來自 GitHub 的通知。</span><span class="sxs-lookup"><span data-stu-id="3fd80-165">This enables the Jenkins instance to receive notifications from GitHub.</span></span>

## <a name="install-the-service-fabric-jenkins-plug-in-from-the-portal"></a><span data-ttu-id="3fd80-166">從入口網站安裝 Service Fabric Jenkins 外掛程式</span><span class="sxs-lookup"><span data-stu-id="3fd80-166">Install the Service Fabric Jenkins plug-in from the portal</span></span>

1. <span data-ttu-id="3fd80-167">移至 ``http://PublicIPorFQDN:8081``。</span><span class="sxs-lookup"><span data-stu-id="3fd80-167">Go to ``http://PublicIPorFQDN:8081``</span></span>
2. <span data-ttu-id="3fd80-168">從 Jenkins 儀表板中，選取 [管理 Jenkins] > [管理外掛程式] > [進階]。</span><span class="sxs-lookup"><span data-stu-id="3fd80-168">From the Jenkins dashboard, select **Manage Jenkins** > **Manage Plugins** > **Advanced**.</span></span>
<span data-ttu-id="3fd80-169">在這裡，您可以上傳外掛程式。</span><span class="sxs-lookup"><span data-stu-id="3fd80-169">Here, you can upload a plug-in.</span></span> <span data-ttu-id="3fd80-170">選取 [選擇檔案]，然後選取 **serviceFabric.hpi** 檔案，您已在「必要條件」下載該檔案。</span><span class="sxs-lookup"><span data-stu-id="3fd80-170">Select **Choose file**, and then select the **serviceFabric.hpi** file, which you downloaded under prerequisites.</span></span> <span data-ttu-id="3fd80-171">當您選取 [上傳] 時，Jenkins 會自動安裝外掛程式。</span><span class="sxs-lookup"><span data-stu-id="3fd80-171">When you select **Upload**, Jenkins automatically installs the plug-in.</span></span> <span data-ttu-id="3fd80-172">在系統要求時允許重新啟動。</span><span class="sxs-lookup"><span data-stu-id="3fd80-172">Allow a restart if requested.</span></span>

## <a name="create-and-configure-a-jenkins-job"></a><span data-ttu-id="3fd80-173">建立及設定 Jenkins 作業</span><span class="sxs-lookup"><span data-stu-id="3fd80-173">Create and configure a Jenkins job</span></span>

1. <span data-ttu-id="3fd80-174">從儀表板建立**新項目**。</span><span class="sxs-lookup"><span data-stu-id="3fd80-174">Create a **new item** from dashboard.</span></span>
2. <span data-ttu-id="3fd80-175">輸入項目名稱 (例如，**MyJob**)。</span><span class="sxs-lookup"><span data-stu-id="3fd80-175">Enter an item name (for example, **MyJob**).</span></span> <span data-ttu-id="3fd80-176">選取 [自由樣式專案]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="3fd80-176">Select **free-style project**, and click **OK**.</span></span>
3. <span data-ttu-id="3fd80-177">前往 [作業] 頁面，並按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="3fd80-177">Go the job page, and click **Configure**.</span></span>

   <span data-ttu-id="3fd80-178">a.</span><span class="sxs-lookup"><span data-stu-id="3fd80-178">a.</span></span> <span data-ttu-id="3fd80-179">在 [GitHub 專案] 下的 [一般] 區段中，指定您的 GitHub 專案 URL。</span><span class="sxs-lookup"><span data-stu-id="3fd80-179">In the general section, under **GitHub project**, specify your GitHub project URL.</span></span> <span data-ttu-id="3fd80-180">此 URL 會裝載您想要與 Jenkins 連續整合、連續部署 (CI/CD) 流程整合的 Service Fabric Java 應用程式 (例如，``https://github.com/sayantancs/SFJenkins``)。</span><span class="sxs-lookup"><span data-stu-id="3fd80-180">This URL hosts the Service Fabric Java application that you want to integrate with the Jenkins continuous integration, continuous deployment (CI/CD) flow (for example, ``https://github.com/sayantancs/SFJenkins``).</span></span>

   <span data-ttu-id="3fd80-181">b.</span><span class="sxs-lookup"><span data-stu-id="3fd80-181">b.</span></span> <span data-ttu-id="3fd80-182">在 [原始程式碼管理] 區段底下，選取 [Git]。</span><span class="sxs-lookup"><span data-stu-id="3fd80-182">Under the **Source Code Management** section, select **Git**.</span></span> <span data-ttu-id="3fd80-183">指定存放庫 URL，它會裝載您想要與 Jenkins CI/CD 流程整合的 Service Fabric Java 應用程式 (例如，``https://github.com/sayantancs/SFJenkins.git``)。</span><span class="sxs-lookup"><span data-stu-id="3fd80-183">Specify the repository URL that hosts the Service Fabric Java application that you want to integrate with the Jenkins CI/CD flow (for example, ``https://github.com/sayantancs/SFJenkins.git``).</span></span> <span data-ttu-id="3fd80-184">您也可以在這裡指定要建置哪些分支 (例如，**/master**)。</span><span class="sxs-lookup"><span data-stu-id="3fd80-184">Also, you can specify here which branch to build (for example, **/master**).</span></span>
4. <span data-ttu-id="3fd80-185">設定您的 *GitHub* (裝載存放庫者)，讓它能夠與 Jenkins 溝通。</span><span class="sxs-lookup"><span data-stu-id="3fd80-185">Configure your *GitHub* (which is hosting the repository) so that it is able to talk to Jenkins.</span></span> <span data-ttu-id="3fd80-186">請使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3fd80-186">Use the following steps:</span></span>

   <span data-ttu-id="3fd80-187">a.</span><span class="sxs-lookup"><span data-stu-id="3fd80-187">a.</span></span> <span data-ttu-id="3fd80-188">移至您的 GitHub 儲存機制頁面。</span><span class="sxs-lookup"><span data-stu-id="3fd80-188">Go to your GitHub repository page.</span></span> <span data-ttu-id="3fd80-189">移至 [設定] > [整合和服務]。</span><span class="sxs-lookup"><span data-stu-id="3fd80-189">Go to **Settings** > **Integrations and Services**.</span></span>

   <span data-ttu-id="3fd80-190">b.</span><span class="sxs-lookup"><span data-stu-id="3fd80-190">b.</span></span> <span data-ttu-id="3fd80-191">選取 [新增服務]、輸入 **Jenkins**，然後選取 [Jenkins-Github 外掛程式]。</span><span class="sxs-lookup"><span data-stu-id="3fd80-191">Select **Add Service**, type **Jenkins**, and select the **Jenkins-GitHub plugin**.</span></span>

   <span data-ttu-id="3fd80-192">c.</span><span class="sxs-lookup"><span data-stu-id="3fd80-192">c.</span></span> <span data-ttu-id="3fd80-193">輸入您的 Jenkins webhook URL (根據預設，它應該是 ``http://<PublicIPorFQDN>:8081/github-webhook/``)。</span><span class="sxs-lookup"><span data-stu-id="3fd80-193">Enter your Jenkins webhook URL (by default, it should be ``http://<PublicIPorFQDN>:8081/github-webhook/``).</span></span> <span data-ttu-id="3fd80-194">按一下 [新增/更新服務]。</span><span class="sxs-lookup"><span data-stu-id="3fd80-194">Click **add/update service**.</span></span>

   <span data-ttu-id="3fd80-195">d.</span><span class="sxs-lookup"><span data-stu-id="3fd80-195">d.</span></span> <span data-ttu-id="3fd80-196">隨即會將測試事件傳送至您的 Jenkins 執行個體。</span><span class="sxs-lookup"><span data-stu-id="3fd80-196">A test event is sent to your Jenkins instance.</span></span> <span data-ttu-id="3fd80-197">您應該會在 GitHub 中看到 webhook 所做的綠色勾號，而且您的專案將會建置。</span><span class="sxs-lookup"><span data-stu-id="3fd80-197">You should see a green check by the webhook in GitHub, and your project will build.</span></span>

   <span data-ttu-id="3fd80-198">e.</span><span class="sxs-lookup"><span data-stu-id="3fd80-198">e.</span></span> <span data-ttu-id="3fd80-199">在 [組建觸發程序] 區段下，選取您想要的建置選項。</span><span class="sxs-lookup"><span data-stu-id="3fd80-199">Under the **Build Triggers** section, select which build option you want.</span></span> <span data-ttu-id="3fd80-200">針對此範例，您要每當發生某些推送至存放庫時觸發組建。</span><span class="sxs-lookup"><span data-stu-id="3fd80-200">For this example, you want to trigger a build whenever some push to the repository happens.</span></span> <span data-ttu-id="3fd80-201">因此，您選取 [GITScm 輪詢的 GitHub 攔截觸發程序]。</span><span class="sxs-lookup"><span data-stu-id="3fd80-201">So you select **GitHub hook trigger for GITScm polling**.</span></span> <span data-ttu-id="3fd80-202">(在先前，此選項稱為**當變更推送至 GitHub 時建置**。)</span><span class="sxs-lookup"><span data-stu-id="3fd80-202">(Previously, this option was called **Build when a change is pushed to GitHub**.)</span></span>

   <span data-ttu-id="3fd80-203">f.</span><span class="sxs-lookup"><span data-stu-id="3fd80-203">f.</span></span> <span data-ttu-id="3fd80-204">在 [建置] 區段底下，從下拉式清單 [新增建置步驟]，選取 [叫用 Gradle 指令碼] 選項。</span><span class="sxs-lookup"><span data-stu-id="3fd80-204">Under the **Build section**, from the drop-down **Add build step**, select the option **Invoke Gradle Script**.</span></span> <span data-ttu-id="3fd80-205">在隨附的 Widget 中，針對您的應用程式指定 [根建置指令碼] 的路徑。</span><span class="sxs-lookup"><span data-stu-id="3fd80-205">In the widget that comes, specify the path to **Root build script** for your application.</span></span> <span data-ttu-id="3fd80-206">它會從指定的路徑挑選 build.gradle，並據以運作。</span><span class="sxs-lookup"><span data-stu-id="3fd80-206">It picks up build.gradle from the path specified, and works accordingly.</span></span> <span data-ttu-id="3fd80-207">如果您建立名為 ``MyActor`` 的專案 (使用 Eclipse 外掛程式或 Yeoman 產生器)，則根建置指令碼應該包含 ``${WORKSPACE}/MyActor``。</span><span class="sxs-lookup"><span data-stu-id="3fd80-207">If you create a project named ``MyActor`` (using the Eclipse plug-in or Yeoman generator), the root build script should contain ``${WORKSPACE}/MyActor``.</span></span> <span data-ttu-id="3fd80-208">請參閱下列螢幕擷取畫面，查看像這樣的範例︰</span><span class="sxs-lookup"><span data-stu-id="3fd80-208">See the following screenshot for an example of what this looks like:</span></span>

    ![Service Fabric Jenkins 建置動作][build-step]

   <span data-ttu-id="3fd80-210">g.</span><span class="sxs-lookup"><span data-stu-id="3fd80-210">g.</span></span> <span data-ttu-id="3fd80-211">從 [建置後動作] 下拉式清單，選取 [部署 Service Fabric 專案]。</span><span class="sxs-lookup"><span data-stu-id="3fd80-211">From the **Post-Build Actions** drop-down, select **Deploy Service Fabric Project**.</span></span> <span data-ttu-id="3fd80-212">這裡您必須提供叢集詳細資料，當中會部署 Jenkins 編譯 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fd80-212">Here you need to provide cluster details where the Jenkins compiled Service Fabric application would be deployed.</span></span> <span data-ttu-id="3fd80-213">您也可以提供用來部署應用程式的其他應用程式詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3fd80-213">You can also provide additional application details used to deploy the application.</span></span> <span data-ttu-id="3fd80-214">請參閱下列螢幕擷取畫面，查看像這樣的範例︰</span><span class="sxs-lookup"><span data-stu-id="3fd80-214">See the following screenshot for an example of what this looks like:</span></span>

    ![Service Fabric Jenkins 建置動作][post-build-step]

   > [!NOTE]
   > <span data-ttu-id="3fd80-216">如果您使用 Service Fabric 來部署 Jenkins 容器映像，這裡的叢集可能與裝載 Jenkins 容器應用程式的叢集相同。</span><span class="sxs-lookup"><span data-stu-id="3fd80-216">The cluster here could be same as the one hosting the Jenkins container application, in case you are using Service Fabric to deploy the Jenkins container image.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="3fd80-217">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3fd80-217">Next steps</span></span>
<span data-ttu-id="3fd80-218">現在已設定 GitHub 和 Jenkins。</span><span class="sxs-lookup"><span data-stu-id="3fd80-218">GitHub and Jenkins are now configured.</span></span> <span data-ttu-id="3fd80-219">請考慮在存放庫範例 https://github.com/sayantancs/SFJenkins 的 ``MyActor`` 專案中進行一些範例變更。</span><span class="sxs-lookup"><span data-stu-id="3fd80-219">Consider making some sample change in your ``MyActor`` project in the repository example, https://github.com/sayantancs/SFJenkins.</span></span> <span data-ttu-id="3fd80-220">將您的變更推送至遠端 ``master`` 分支 (或任何您已設定要使用的分支)。</span><span class="sxs-lookup"><span data-stu-id="3fd80-220">Push your changes to a remote ``master`` branch (or any branch that you have configured to work with).</span></span> <span data-ttu-id="3fd80-221">這會觸發您設定的 Jenkins 作業 ``MyJob``。</span><span class="sxs-lookup"><span data-stu-id="3fd80-221">This triggers the Jenkins job, ``MyJob``, that you configured.</span></span> <span data-ttu-id="3fd80-222">它會從 GitHub 擷取變更、建置它們並且將應用程式部署至您在建置後動作中指定的叢集端點。</span><span class="sxs-lookup"><span data-stu-id="3fd80-222">It fetches the changes from GitHub, builds them, and deploys the application to the cluster endpoint you specified in post-build actions.</span></span>  

  <!-- Images -->
  [build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/build-step.png
  [post-build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/post-build-step.png

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
# <a name="use-jenkins-toobuild-and-deploy-your-linux-java-application"></a><span data-ttu-id="c7055-103">使用 Jenkins toobuild 及部署 Linux Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="c7055-103">Use Jenkins toobuild and deploy your Linux Java application</span></span>
<span data-ttu-id="c7055-104">Jenkins 是連續整合和部署應用程式的熱門工具。</span><span class="sxs-lookup"><span data-stu-id="c7055-104">Jenkins is a popular tool for continuous integration and deployment of your apps.</span></span> <span data-ttu-id="c7055-105">以下是如何 toobuild 和部署 Azure Service Fabric 應用程式使用 Jenkins。</span><span class="sxs-lookup"><span data-stu-id="c7055-105">Here's how toobuild and deploy your Azure Service Fabric application by using Jenkins.</span></span>

## <a name="general-prerequisites"></a><span data-ttu-id="c7055-106">一般先決條件</span><span class="sxs-lookup"><span data-stu-id="c7055-106">General prerequisites</span></span>
- <span data-ttu-id="c7055-107">在本機安裝 Git。</span><span class="sxs-lookup"><span data-stu-id="c7055-107">Have Git installed locally.</span></span> <span data-ttu-id="c7055-108">您可以安裝來自 hello 適當 Git 版本[hello Git 下載頁面](https://git-scm.com/downloads)，根據您的作業系統。</span><span class="sxs-lookup"><span data-stu-id="c7055-108">You can install hello appropriate Git version from [hello Git downloads page](https://git-scm.com/downloads), based on your operating system.</span></span> <span data-ttu-id="c7055-109">如果您是新 tooGit，深入了解從 hello [Git 文件](https://git-scm.com/docs)。</span><span class="sxs-lookup"><span data-stu-id="c7055-109">If you are new tooGit, learn more about it from hello [Git documentation](https://git-scm.com/docs).</span></span>
- <span data-ttu-id="c7055-110">擁有 hello 服務網狀架構 Jenkins 外掛程式很方便。</span><span class="sxs-lookup"><span data-stu-id="c7055-110">Have hello Service Fabric Jenkins plug-in handy.</span></span> <span data-ttu-id="c7055-111">您可以從 [Service Fabric 下載](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi)進行下載。</span><span class="sxs-lookup"><span data-stu-id="c7055-111">You can download it from [Service Fabric downloads](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi).</span></span>

## <a name="set-up-jenkins-inside-a-service-fabric-cluster"></a><span data-ttu-id="c7055-112">在 Service Fabric 叢集內設定 Jenkins</span><span class="sxs-lookup"><span data-stu-id="c7055-112">Set up Jenkins inside a Service Fabric cluster</span></span>

<span data-ttu-id="c7055-113">您可以在 Service Fabric 叢集內部或外部設定 Jenkins。</span><span class="sxs-lookup"><span data-stu-id="c7055-113">You can set up Jenkins either inside or outside a Service Fabric cluster.</span></span> <span data-ttu-id="c7055-114">hello 面各節顯示 tooset 如何當它在使用 Azure 儲存體叢集內帳戶 toosave hello hello 容器執行個體狀態。</span><span class="sxs-lookup"><span data-stu-id="c7055-114">hello following sections show how tooset it up inside a cluster while using an Azure storage account toosave hello state of hello container instance.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c7055-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="c7055-115">Prerequisites</span></span>
1. <span data-ttu-id="c7055-116">讓 Service Fabric Linux 叢集準備就緒。</span><span class="sxs-lookup"><span data-stu-id="c7055-116">Have a Service Fabric Linux cluster ready.</span></span> <span data-ttu-id="c7055-117">Service Fabric 叢集已經從 hello Azure 入口網站建立具有已安裝 Docker。</span><span class="sxs-lookup"><span data-stu-id="c7055-117">A Service Fabric cluster created from hello Azure portal already has Docker installed.</span></span> <span data-ttu-id="c7055-118">如果您在本機執行 hello 叢集，請檢查使用 hello 命令是否已安裝 Docker ``docker info``。</span><span class="sxs-lookup"><span data-stu-id="c7055-118">If you are running hello cluster locally, check if Docker is installed by using hello command ``docker info``.</span></span> <span data-ttu-id="c7055-119">如果未安裝，安裝據以使用下列命令 hello:</span><span class="sxs-lookup"><span data-stu-id="c7055-119">If it is not installed, install it accordingly by using hello following commands:</span></span>

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```
2. <span data-ttu-id="c7055-120">已使用下列步驟的 hello hello 叢集上部署的 hello Service Fabric 容器應用程式：</span><span class="sxs-lookup"><span data-stu-id="c7055-120">Have hello Service Fabric container application deployed on hello cluster, by using hello following steps:</span></span>

  ```sh
git clone https://github.com/Azure-Samples/service-fabric-java-getting-started.git
cd service-fabric-java-getting-started/Services/JenkinsDocker/
```

3. <span data-ttu-id="c7055-121">您需要 hello 連接選項的詳細資料的 hello Azure 儲存體檔案共用，您想要 toopersist hello hello Jenkins 容器執行個體狀態。</span><span class="sxs-lookup"><span data-stu-id="c7055-121">You need hello connect option details of hello Azure storage file-share, where you want toopersist hello state of hello Jenkins container instance.</span></span> <span data-ttu-id="c7055-122">如果您使用 hello hello Microsoft Azure 入口網站相同，請在步驟 hello，-建立 Azure 儲存體帳戶，例如``sfjenkinsstorage1``。</span><span class="sxs-lookup"><span data-stu-id="c7055-122">If you are using hello Microsoft Azure portal for hello same, please follow hello steps - Create an Azure storage account, say ``sfjenkinsstorage1``.</span></span> <span data-ttu-id="c7055-123">在該儲存體帳戶底下建立一個「檔案共用」(例如 ``sfjenkins``)。</span><span class="sxs-lookup"><span data-stu-id="c7055-123">Create a **File Share** under that storage account, say ``sfjenkins``.</span></span> <span data-ttu-id="c7055-124">按一下**連接**針對 hello 檔案共用，注意 hello 值就會顯示在**連接從 Linux**，假設這看起來會類似如下-</span><span class="sxs-lookup"><span data-stu-id="c7055-124">Click on **Connect** for hello file-share and note hello values it displays under **Connecting from Linux**, say this would look like as follows -</span></span>
```sh
sudo mount -t cifs //sfjenkinsstorage1.file.core.windows.net/sfjenkins [mount point] -o vers=3.0,username=sfjenkinsstorage1,password=<storage_key>,dir_mode=0777,file_mode=0777
```

4. <span data-ttu-id="c7055-125">更新在 hello hello 預留位置值```setupentrypoint.sh```與對應的 azure 儲存體詳細資料的指令碼。</span><span class="sxs-lookup"><span data-stu-id="c7055-125">Update hello placeholder values in hello ```setupentrypoint.sh``` script with corresponding azure-storage details.</span></span>
```sh
vi JenkinsSF/JenkinsOnSF/Code/setupentrypoint.sh
```
<span data-ttu-id="c7055-126">取代``[REMOTE_FILE_SHARE_LOCATION]``hello 值``//sfjenkinsstorage1.file.core.windows.net/sfjenkins``hello hello 輸出連接上面的 3 點中。</span><span class="sxs-lookup"><span data-stu-id="c7055-126">Replace ``[REMOTE_FILE_SHARE_LOCATION]`` with hello value ``//sfjenkinsstorage1.file.core.windows.net/sfjenkins`` from hello output of hello connect in point 3 above.</span></span>
<span data-ttu-id="c7055-127">取代``[FILE_SHARE_CONNECT_OPTIONS_STRING]``hello 值``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777``從上面的 3 點。</span><span class="sxs-lookup"><span data-stu-id="c7055-127">Replace ``[FILE_SHARE_CONNECT_OPTIONS_STRING]`` with hello value ``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777`` from point 3 above.</span></span>

5. <span data-ttu-id="c7055-128">Toohello 叢集連線，並安裝 hello 容器應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7055-128">Connect toohello cluster and install hello container application.</span></span>
```azurecli
sfctl cluster select --endpoint http://PublicIPorFQDN:19080   # cluster connect command
bash Scripts/install.sh
```
<span data-ttu-id="c7055-129">這在 hello 叢集上，安裝 Jenkins 容器，您可以監視使用 hello Service Fabric 總管。</span><span class="sxs-lookup"><span data-stu-id="c7055-129">This installs a Jenkins container on hello cluster, and can be monitored by using hello Service Fabric Explorer.</span></span>

### <a name="steps"></a><span data-ttu-id="c7055-130">步驟</span><span class="sxs-lookup"><span data-stu-id="c7055-130">Steps</span></span>
1. <span data-ttu-id="c7055-131">從您的瀏覽器，移過``http://PublicIPorFQDN:8081``。</span><span class="sxs-lookup"><span data-stu-id="c7055-131">From your browser, go too``http://PublicIPorFQDN:8081``.</span></span> <span data-ttu-id="c7055-132">它提供了在 hello 初始管理所需密碼 toosign hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="c7055-132">It provides hello path of hello initial admin password required toosign in.</span></span> <span data-ttu-id="c7055-133">您可以繼續 toouse Jenkins 身為系統管理員使用者。</span><span class="sxs-lookup"><span data-stu-id="c7055-133">You can continue toouse Jenkins as an admin user.</span></span> <span data-ttu-id="c7055-134">或者，您可以建立並之後 hello 初始管理帳戶登入時變更 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="c7055-134">Or you can create and change hello user, after you sign in with hello initial admin account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c7055-135">請在建立 hello 叢集時，確認要 hello 8081 的連接埠指定為 hello 應用程式端點連接埠。</span><span class="sxs-lookup"><span data-stu-id="c7055-135">Ensure that hello 8081 port is specified as hello application endpoint port while you are creating hello cluster.</span></span>
   >

2. <span data-ttu-id="c7055-136">使用取得 hello 容器執行個體識別碼``docker ps -a``。</span><span class="sxs-lookup"><span data-stu-id="c7055-136">Get hello container instance ID by using ``docker ps -a``.</span></span>
3. <span data-ttu-id="c7055-137">安全殼層 (SSH) 登入 toohello 容器內，並貼上您所顯示 hello Jenkins 入口網站的 hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="c7055-137">Secure Shell (SSH) sign in toohello container, and paste hello path you were shown on hello Jenkins portal.</span></span> <span data-ttu-id="c7055-138">例如，如果它在 hello 入口網站中顯示 hello 路徑`PATH_TO_INITIAL_ADMIN_PASSWORD`，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="c7055-138">For example, if in hello portal it shows hello path `PATH_TO_INITIAL_ADMIN_PASSWORD`, run hello following:</span></span>

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash   # This takes you inside Docker shell
  cat PATH_TO_INITIAL_ADMIN_PASSWORD
  ```

4. <span data-ttu-id="c7055-139">使用 hello 步驟中所述，設定 GitHub toowork jenkins，[產生新的 SSH 金鑰，並將它加入 toohello SSH 代理程式](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)。</span><span class="sxs-lookup"><span data-stu-id="c7055-139">Set up GitHub toowork with Jenkins, by using hello steps mentioned in [Generating a new SSH key and adding it toohello SSH agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).</span></span>
    * <span data-ttu-id="c7055-140">使用 hello GitHub toogenerate hello SSH 金鑰和 tooadd hello SSH 金鑰 toohello 裝載您的儲存機制的 GitHub 帳戶所提供的指示。</span><span class="sxs-lookup"><span data-stu-id="c7055-140">Use hello instructions provided by GitHub toogenerate hello SSH key, and tooadd hello SSH key toohello GitHub account that is hosting your repository.</span></span>
    * <span data-ttu-id="c7055-141">執行 hello 上述連結 hello Jenkins Docker 命令介面中 （且不在主機上） 中所述的 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="c7055-141">Run hello commands mentioned in hello preceding link in hello Jenkins Docker shell (and not on your host).</span></span>
    * <span data-ttu-id="c7055-142">toosign 中 toohello Jenkins 殼層，從您的主機使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="c7055-142">toosign in toohello Jenkins shell from your host, use hello following command:</span></span>

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
  ```

## <a name="set-up-jenkins-outside-a-service-fabric-cluster"></a><span data-ttu-id="c7055-143">在 Service Fabric 叢集外設定 Jenkins</span><span class="sxs-lookup"><span data-stu-id="c7055-143">Set up Jenkins outside a Service Fabric cluster</span></span>

<span data-ttu-id="c7055-144">您可以在 Service Fabric 叢集內部或外部設定 Jenkins。</span><span class="sxs-lookup"><span data-stu-id="c7055-144">You can set up Jenkins either inside or outside of a Service Fabric cluster.</span></span> <span data-ttu-id="c7055-145">hello 下列各節顯示如何 tooset 它在叢集外。</span><span class="sxs-lookup"><span data-stu-id="c7055-145">hello following sections show how tooset it up outside a cluster.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c7055-146">必要條件</span><span class="sxs-lookup"><span data-stu-id="c7055-146">Prerequisites</span></span>
<span data-ttu-id="c7055-147">您必須已安裝 Docker toohave。</span><span class="sxs-lookup"><span data-stu-id="c7055-147">You need toohave Docker installed.</span></span> <span data-ttu-id="c7055-148">hello，下列命令可以是使用的 tooinstall Docker hello 終端機的：</span><span class="sxs-lookup"><span data-stu-id="c7055-148">hello following commands can be used tooinstall Docker from hello terminal:</span></span>

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```

<span data-ttu-id="c7055-149">現在，當您執行``docker info``在 hello 終端機，您應該會看到 hello 輸出中的 hello Docker 服務正在執行。</span><span class="sxs-lookup"><span data-stu-id="c7055-149">Now when you run ``docker info`` in hello terminal, you should see in hello output that hello Docker service is running.</span></span>

### <a name="steps"></a><span data-ttu-id="c7055-150">步驟</span><span class="sxs-lookup"><span data-stu-id="c7055-150">Steps</span></span>
  1. <span data-ttu-id="c7055-151">提取 hello 服務網狀架構 Jenkins 容器映像：``docker pull raunakpandya/jenkins:v1``</span><span class="sxs-lookup"><span data-stu-id="c7055-151">Pull hello Service Fabric Jenkins container image: ``docker pull raunakpandya/jenkins:v1``</span></span>
  2. <span data-ttu-id="c7055-152">執行 hello 容器映像：``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``</span><span class="sxs-lookup"><span data-stu-id="c7055-152">Run hello container image: ``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``</span></span>
  3. <span data-ttu-id="c7055-153">取得 hello 識別碼 hello 容器映像執行個體。</span><span class="sxs-lookup"><span data-stu-id="c7055-153">Get hello ID of hello container image instance.</span></span> <span data-ttu-id="c7055-154">您可以列出所有與 hello 命令的 hello Docker 容器``docker ps –a``</span><span class="sxs-lookup"><span data-stu-id="c7055-154">You can list all hello Docker containers with hello command ``docker ps –a``</span></span>
  4. <span data-ttu-id="c7055-155">Toohello Jenkins 入口網站使用的登入 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c7055-155">Sign in toohello Jenkins portal by using hello following steps:</span></span>

    * ```sh
    docker exec [first-four-digits-of-container-ID] cat /var/jenkins_home/secrets/initialAdminPassword
    ```
    <span data-ttu-id="c7055-156">如果容器識別碼是 2d24a73b5964，請使用 2d24。</span><span class="sxs-lookup"><span data-stu-id="c7055-156">If container ID is 2d24a73b5964, use 2d24.</span></span>
    * <span data-ttu-id="c7055-157">此密碼是必要的登入入口網站，也就是 toohello Jenkins 儀表板``http://<HOST-IP>:8080``</span><span class="sxs-lookup"><span data-stu-id="c7055-157">This password is required for signing in toohello Jenkins dashboard from portal, which is ``http://<HOST-IP>:8080``</span></span>
    * <span data-ttu-id="c7055-158">您登入的 hello 第一次之後，您可以建立您自己的使用者帳戶，並使用該以備將來使用，或者您可以繼續 toouse hello 系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="c7055-158">After you sign in for hello first time, you can create your own user account and use that for future purposes, or you can continue toouse hello administrator account.</span></span> <span data-ttu-id="c7055-159">建立使用者之後，您需要與 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="c7055-159">After you create a user, you need toocontinue with that.</span></span>
  5. <span data-ttu-id="c7055-160">使用 hello 步驟中所述，設定 GitHub toowork jenkins，[產生新的 SSH 金鑰，並將它加入 toohello SSH 代理程式](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)。</span><span class="sxs-lookup"><span data-stu-id="c7055-160">Set up GitHub toowork with Jenkins, by using hello steps mentioned in [Generating a new SSH key and adding it toohello SSH agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).</span></span>
        * <span data-ttu-id="c7055-161">使用 hello GitHub toogenerate hello SSH 金鑰和 tooadd hello SSH 金鑰 toohello 裝載 hello 儲存機制的 GitHub 帳戶所提供的指示。</span><span class="sxs-lookup"><span data-stu-id="c7055-161">Use hello instructions provided by GitHub toogenerate hello SSH key, and tooadd hello SSH key toohello GitHub account that is hosting hello repository.</span></span>
        * <span data-ttu-id="c7055-162">執行 hello 上述連結 hello Jenkins Docker 命令介面中 （且不在主機上） 中所述的 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="c7055-162">Run hello commands mentioned in hello preceding link in hello Jenkins Docker shell (and not on your host).</span></span>
      * <span data-ttu-id="c7055-163">toosign 中 toohello Jenkins 殼層，從您的主機使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="c7055-163">toosign in toohello Jenkins shell from your host, use hello following commands:</span></span>

      ```sh
      docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
      ```

<span data-ttu-id="c7055-164">請確定該 hello 叢集或其中 hello Jenkins 容器映像裝載具有公開 IP 的機器。</span><span class="sxs-lookup"><span data-stu-id="c7055-164">Ensure that hello cluster or machine where hello Jenkins container image is hosted has a public-facing IP.</span></span> <span data-ttu-id="c7055-165">這可讓從 GitHub hello Jenkins 執行個體 tooreceive 通知。</span><span class="sxs-lookup"><span data-stu-id="c7055-165">This enables hello Jenkins instance tooreceive notifications from GitHub.</span></span>

## <a name="install-hello-service-fabric-jenkins-plug-in-from-hello-portal"></a><span data-ttu-id="c7055-166">從 hello 入口網站安裝 hello 服務網狀架構 Jenkins 外掛程式</span><span class="sxs-lookup"><span data-stu-id="c7055-166">Install hello Service Fabric Jenkins plug-in from hello portal</span></span>

1. <span data-ttu-id="c7055-167">跳過``http://PublicIPorFQDN:8081``</span><span class="sxs-lookup"><span data-stu-id="c7055-167">Go too``http://PublicIPorFQDN:8081``</span></span>
2. <span data-ttu-id="c7055-168">從 hello Jenkins 儀表板中，選取**管理 Jenkins** > **管理外掛程式** > **進階**。</span><span class="sxs-lookup"><span data-stu-id="c7055-168">From hello Jenkins dashboard, select **Manage Jenkins** > **Manage Plugins** > **Advanced**.</span></span>
<span data-ttu-id="c7055-169">在這裡，您可以上傳外掛程式。</span><span class="sxs-lookup"><span data-stu-id="c7055-169">Here, you can upload a plug-in.</span></span> <span data-ttu-id="c7055-170">選取**選擇檔案**，然後選取 hello **serviceFabric.hpi**必要條件下您下載的檔案。</span><span class="sxs-lookup"><span data-stu-id="c7055-170">Select **Choose file**, and then select hello **serviceFabric.hpi** file, which you downloaded under prerequisites.</span></span> <span data-ttu-id="c7055-171">當您選取**上傳**，Jenkins 會自動安裝外掛程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="c7055-171">When you select **Upload**, Jenkins automatically installs hello plug-in.</span></span> <span data-ttu-id="c7055-172">在系統要求時允許重新啟動。</span><span class="sxs-lookup"><span data-stu-id="c7055-172">Allow a restart if requested.</span></span>

## <a name="create-and-configure-a-jenkins-job"></a><span data-ttu-id="c7055-173">建立及設定 Jenkins 作業</span><span class="sxs-lookup"><span data-stu-id="c7055-173">Create and configure a Jenkins job</span></span>

1. <span data-ttu-id="c7055-174">從儀表板建立**新項目**。</span><span class="sxs-lookup"><span data-stu-id="c7055-174">Create a **new item** from dashboard.</span></span>
2. <span data-ttu-id="c7055-175">輸入項目名稱 (例如，**MyJob**)。</span><span class="sxs-lookup"><span data-stu-id="c7055-175">Enter an item name (for example, **MyJob**).</span></span> <span data-ttu-id="c7055-176">選取 [自由樣式專案]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c7055-176">Select **free-style project**, and click **OK**.</span></span>
3. <span data-ttu-id="c7055-177">移 hello 作業] 頁面上，然後按一下 [**設定**。</span><span class="sxs-lookup"><span data-stu-id="c7055-177">Go hello job page, and click **Configure**.</span></span>

   <span data-ttu-id="c7055-178">a.</span><span class="sxs-lookup"><span data-stu-id="c7055-178">a.</span></span> <span data-ttu-id="c7055-179">在 hello 一般區段中，在**GitHub 專案**，指定您的 GitHub 專案 URL。</span><span class="sxs-lookup"><span data-stu-id="c7055-179">In hello general section, under **GitHub project**, specify your GitHub project URL.</span></span> <span data-ttu-id="c7055-180">此 URL 主機 hello 服務網狀架構 Java 應用程式想要以 hello Jenkins 連續整合 toointegrate，(CI/CD) 進行持續部署流程 (例如， ``https://github.com/sayantancs/SFJenkins``)。</span><span class="sxs-lookup"><span data-stu-id="c7055-180">This URL hosts hello Service Fabric Java application that you want toointegrate with hello Jenkins continuous integration, continuous deployment (CI/CD) flow (for example, ``https://github.com/sayantancs/SFJenkins``).</span></span>

   <span data-ttu-id="c7055-181">b.</span><span class="sxs-lookup"><span data-stu-id="c7055-181">b.</span></span> <span data-ttu-id="c7055-182">在 hello**原始程式碼管理**區段中，選取**Git**。</span><span class="sxs-lookup"><span data-stu-id="c7055-182">Under hello **Source Code Management** section, select **Git**.</span></span> <span data-ttu-id="c7055-183">指定裝載您要以 hello Jenkins CI/CD 流程 toointegrate hello 服務網狀架構 Java 應用程式的 hello 儲存機制 URL (例如， ``https://github.com/sayantancs/SFJenkins.git``)。</span><span class="sxs-lookup"><span data-stu-id="c7055-183">Specify hello repository URL that hosts hello Service Fabric Java application that you want toointegrate with hello Jenkins CI/CD flow (for example, ``https://github.com/sayantancs/SFJenkins.git``).</span></span> <span data-ttu-id="c7055-184">此外，您可以在此處指定的分支 toobuild (例如， **/master**)。</span><span class="sxs-lookup"><span data-stu-id="c7055-184">Also, you can specify here which branch toobuild (for example, **/master**).</span></span>
4. <span data-ttu-id="c7055-185">設定您*GitHub* （其中主控 hello 儲存機制），以便能夠 tootalk tooJenkins。</span><span class="sxs-lookup"><span data-stu-id="c7055-185">Configure your *GitHub* (which is hosting hello repository) so that it is able tootalk tooJenkins.</span></span> <span data-ttu-id="c7055-186">使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c7055-186">Use hello following steps:</span></span>

   <span data-ttu-id="c7055-187">a.</span><span class="sxs-lookup"><span data-stu-id="c7055-187">a.</span></span> <span data-ttu-id="c7055-188">移至 tooyour GitHub 儲存機制頁面。</span><span class="sxs-lookup"><span data-stu-id="c7055-188">Go tooyour GitHub repository page.</span></span> <span data-ttu-id="c7055-189">跳過**設定** > **整合和服務**。</span><span class="sxs-lookup"><span data-stu-id="c7055-189">Go too**Settings** > **Integrations and Services**.</span></span>

   <span data-ttu-id="c7055-190">b.</span><span class="sxs-lookup"><span data-stu-id="c7055-190">b.</span></span> <span data-ttu-id="c7055-191">選取**加入服務**，型別**Jenkins**，並選取 hello **Jenkins GitHub 外掛程式**。</span><span class="sxs-lookup"><span data-stu-id="c7055-191">Select **Add Service**, type **Jenkins**, and select hello **Jenkins-GitHub plugin**.</span></span>

   <span data-ttu-id="c7055-192">c.</span><span class="sxs-lookup"><span data-stu-id="c7055-192">c.</span></span> <span data-ttu-id="c7055-193">輸入您的 Jenkins webhook URL (根據預設，它應該是 ``http://<PublicIPorFQDN>:8081/github-webhook/``)。</span><span class="sxs-lookup"><span data-stu-id="c7055-193">Enter your Jenkins webhook URL (by default, it should be ``http://<PublicIPorFQDN>:8081/github-webhook/``).</span></span> <span data-ttu-id="c7055-194">按一下 [新增/更新服務]。</span><span class="sxs-lookup"><span data-stu-id="c7055-194">Click **add/update service**.</span></span>

   <span data-ttu-id="c7055-195">d.</span><span class="sxs-lookup"><span data-stu-id="c7055-195">d.</span></span> <span data-ttu-id="c7055-196">測試事件會傳送 tooyour Jenkins 執行個體。</span><span class="sxs-lookup"><span data-stu-id="c7055-196">A test event is sent tooyour Jenkins instance.</span></span> <span data-ttu-id="c7055-197">您應該查看在 GitHub 中的 hello webhook 綠色的核取，並建置專案。</span><span class="sxs-lookup"><span data-stu-id="c7055-197">You should see a green check by hello webhook in GitHub, and your project will build.</span></span>

   <span data-ttu-id="c7055-198">e.</span><span class="sxs-lookup"><span data-stu-id="c7055-198">e.</span></span> <span data-ttu-id="c7055-199">在 hello**組建觸發程序**區段中，選取哪一個建置您想要的選項。</span><span class="sxs-lookup"><span data-stu-id="c7055-199">Under hello **Build Triggers** section, select which build option you want.</span></span> <span data-ttu-id="c7055-200">例如，您想 tootrigger 組建，每當發生某些發送 toohello 儲存機制時。</span><span class="sxs-lookup"><span data-stu-id="c7055-200">For this example, you want tootrigger a build whenever some push toohello repository happens.</span></span> <span data-ttu-id="c7055-201">因此，您選取 [GITScm 輪詢的 GitHub 攔截觸發程序]。</span><span class="sxs-lookup"><span data-stu-id="c7055-201">So you select **GitHub hook trigger for GITScm polling**.</span></span> <span data-ttu-id="c7055-202">(此選項之前，呼叫**建置時變更推入 tooGitHub**。)</span><span class="sxs-lookup"><span data-stu-id="c7055-202">(Previously, this option was called **Build when a change is pushed tooGitHub**.)</span></span>

   <span data-ttu-id="c7055-203">f.</span><span class="sxs-lookup"><span data-stu-id="c7055-203">f.</span></span> <span data-ttu-id="c7055-204">在 hello**建立區段**，從 hello 下拉式清單**加入建置步驟**，選取 hello 選項**叫用 Gradle 指令碼**。</span><span class="sxs-lookup"><span data-stu-id="c7055-204">Under hello **Build section**, from hello drop-down **Add build step**, select hello option **Invoke Gradle Script**.</span></span> <span data-ttu-id="c7055-205">在出現 hello widget 中，指定 hello 路徑太**根建置指令碼**應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7055-205">In hello widget that comes, specify hello path too**Root build script** for your application.</span></span> <span data-ttu-id="c7055-206">它會拾取 build.gradle hello 路徑指定，從，並據此運作。</span><span class="sxs-lookup"><span data-stu-id="c7055-206">It picks up build.gradle from hello path specified, and works accordingly.</span></span> <span data-ttu-id="c7055-207">如果您建立專案，名為``MyActor``（使用 hello Eclipse 外掛程式或 Yeoman 產生器），hello 根組建指令碼應包含``${WORKSPACE}/MyActor``。</span><span class="sxs-lookup"><span data-stu-id="c7055-207">If you create a project named ``MyActor`` (using hello Eclipse plug-in or Yeoman generator), hello root build script should contain ``${WORKSPACE}/MyActor``.</span></span> <span data-ttu-id="c7055-208">請參閱下列的這好像範例的螢幕擷取畫面的 hello:</span><span class="sxs-lookup"><span data-stu-id="c7055-208">See hello following screenshot for an example of what this looks like:</span></span>

    ![Service Fabric Jenkins 建置動作][build-step]

   <span data-ttu-id="c7055-210">g.</span><span class="sxs-lookup"><span data-stu-id="c7055-210">g.</span></span> <span data-ttu-id="c7055-211">從 hello**建置後動作**下拉式清單中，選取**部署 Service Fabric 專案**。</span><span class="sxs-lookup"><span data-stu-id="c7055-211">From hello **Post-Build Actions** drop-down, select **Deploy Service Fabric Project**.</span></span> <span data-ttu-id="c7055-212">您需要在這裡 tooprovide 叢集將部署的 hello Jenkins 已編譯之 Service Fabric 應用程式的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c7055-212">Here you need tooprovide cluster details where hello Jenkins compiled Service Fabric application would be deployed.</span></span> <span data-ttu-id="c7055-213">您也可以提供使用 toodeploy hello 應用程式的其他應用程式詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c7055-213">You can also provide additional application details used toodeploy hello application.</span></span> <span data-ttu-id="c7055-214">請參閱下列的這好像範例的螢幕擷取畫面的 hello:</span><span class="sxs-lookup"><span data-stu-id="c7055-214">See hello following screenshot for an example of what this looks like:</span></span>

    ![Service Fabric Jenkins 建置動作][post-build-step]

   > [!NOTE]
   > <span data-ttu-id="c7055-216">如果您使用 Service Fabric toodeploy hello Jenkins 容器映像，可能是與 hello 一個裝載 hello Jenkins 容器應用程式，相同 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="c7055-216">hello cluster here could be same as hello one hosting hello Jenkins container application, in case you are using Service Fabric toodeploy hello Jenkins container image.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="c7055-217">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c7055-217">Next steps</span></span>
<span data-ttu-id="c7055-218">現在已設定 GitHub 和 Jenkins。</span><span class="sxs-lookup"><span data-stu-id="c7055-218">GitHub and Jenkins are now configured.</span></span> <span data-ttu-id="c7055-219">請考慮進行一些樣本，以變更您``MyActor``在 hello 儲存機制範例中，專案 https://github.com/sayantancs/SFJenkins。</span><span class="sxs-lookup"><span data-stu-id="c7055-219">Consider making some sample change in your ``MyActor`` project in hello repository example, https://github.com/sayantancs/SFJenkins.</span></span> <span data-ttu-id="c7055-220">推送變更 tooa 遠端``master``分支 （或您已設定 toowork 與任何分支）。</span><span class="sxs-lookup"><span data-stu-id="c7055-220">Push your changes tooa remote ``master`` branch (or any branch that you have configured toowork with).</span></span> <span data-ttu-id="c7055-221">這會觸發 hello Jenkins 作業， ``MyJob``，在您的設定。</span><span class="sxs-lookup"><span data-stu-id="c7055-221">This triggers hello Jenkins job, ``MyJob``, that you configured.</span></span> <span data-ttu-id="c7055-222">從 GitHub 提取 hello 變更、 建立它們，和部署您在建置後動作中指定的 hello 應用程式 toohello 叢集端點。</span><span class="sxs-lookup"><span data-stu-id="c7055-222">It fetches hello changes from GitHub, builds them, and deploys hello application toohello cluster endpoint you specified in post-build actions.</span></span>  

  <!-- Images -->
  [build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/build-step.png
  [post-build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/post-build-step.png

---
title: "aaaPublish Docker 容器使用 hello Azure Toolkit for IntelliJ |Microsoft 文件"
description: "深入了解如何為 Docker 容器使用的 Azure web 應用程式 tooMicrosoft toopublish hello Azure Toolkit IntelliJ。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: bee94cb269ea707ae7ad55232e23e915aec48c34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="4c977-103">使用 IntelliJ hello Azure Toolkit Docker 容器發行 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4c977-103">Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="4c977-104">Docker 容器是常見的 Web 應用程式部署方法。</span><span class="sxs-lookup"><span data-stu-id="4c977-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="4c977-105">藉由使用 Docker 容器，開發人員可以將合併所有的專案檔和成單一封裝的部署 tooa 伺服器的相依性。</span><span class="sxs-lookup"><span data-stu-id="4c977-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="4c977-106">hello Azure Toolkit for IntelliJ Java 開發人員簡化此程序，藉由新增*發佈為 Docker 容器*部署 tooMicrosoft Azure 的功能。</span><span class="sxs-lookup"><span data-stu-id="4c977-106">hello Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="4c977-107">本文將告訴您透過 hello 步驟需要 toopublish 應用程式 tooAzure 做為 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="4c977-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="4c977-108">Docker 的詳細資訊位於 hello [Docker 網站]。</span><span class="sxs-lookup"><span data-stu-id="4c977-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="4c977-109">使用 Docker 容器發行您的 web 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="4c977-109">Publish your web app tooAzure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="4c977-110">toopublish 您 web 應用程式中，您必須建立可供部署的成品。</span><span class="sxs-lookup"><span data-stu-id="4c977-110">toopublish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="4c977-111">toolearn 詳細資訊，請參閱 hello[建立成品的其他資訊](#artifacts)> 一節。</span><span class="sxs-lookup"><span data-stu-id="4c977-111">toolearn more, see hello [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="4c977-112">您至少一次完成 hello 部署精靈 之後，大部分的設定會使用預設執行 hello 精靈時。</span><span class="sxs-lookup"><span data-stu-id="4c977-112">After you have completed hello deployment wizard at least once, most of your settings are used as defaults when you run hello wizard again.</span></span>
>

1. <span data-ttu-id="4c977-113">在 IntelliJ 中開啟 web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="4c977-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="4c977-114">toostart hello**發佈為 Docker 容器**精靈 中，執行 hello 下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="4c977-114">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="4c977-115">在 hello**專案**工具視窗，以滑鼠右鍵按一下您的專案，按一下  **Azure**，然後按一下**發佈為 Docker 容器**:</span><span class="sxs-lookup"><span data-stu-id="4c977-115">In hello **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![hello 發佈為 Docker 容器命令][PUB01]

   * <span data-ttu-id="4c977-117">Hello IntelliJ 工具列上，按一下 hello**發佈群組**按鈕，然後再按一下**發佈為 Docker 容器**:</span><span class="sxs-lookup"><span data-stu-id="4c977-117">On hello IntelliJ toolbar, click hello **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="4c977-118">![hello 發佈為 Docker 容器命令][PUB02]</span><span class="sxs-lookup"><span data-stu-id="4c977-118">![hello Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="4c977-119">hello**在 Azure 上部署 Docker 容器**精靈 隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="4c977-119">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![hello Azure 精靈上部署 Docker 容器][PUB03]

3. <span data-ttu-id="4c977-121">在 hello**輸入映像名稱選取 hello 成品路徑，請檢查使用 Docker 主機 toobe**視窗中，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="4c977-121">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span> 

   <span data-ttu-id="4c977-122">a.</span><span class="sxs-lookup"><span data-stu-id="4c977-122">a.</span></span> <span data-ttu-id="4c977-123">在 hello **Docker 映像名稱**方塊中，輸入您的 Docker 主機的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="4c977-123">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="4c977-124">（hello 精靈會自動建立一個名稱，但您可以修改它）。</span><span class="sxs-lookup"><span data-stu-id="4c977-124">(hello wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="4c977-125">b.</span><span class="sxs-lookup"><span data-stu-id="4c977-125">b.</span></span> <span data-ttu-id="4c977-126">hello**主機**區域會顯示您已經建立任何 Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="4c977-126">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="4c977-127">執行 hello 下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="4c977-127">Do either of hello following:</span></span> 
      * <span data-ttu-id="4c977-128">如果您有現有的 Docker 主機，您可以部署您的 web 應用程式 tooit。</span><span class="sxs-lookup"><span data-stu-id="4c977-128">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
      * <span data-ttu-id="4c977-129">toocreate Docker 主機時，按一下 hello 綠色加號 (**+**)。</span><span class="sxs-lookup"><span data-stu-id="4c977-129">toocreate a Docker host, click hello green plus sign (**+**).</span></span>  
       <span data-ttu-id="4c977-130">hello**建立 Docker 主機**對話方塊隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="4c977-130">hello **Create Docker Host** dialog box opens.</span></span> 

      ![[在 Azure 上部署 Docker 容器] 精靈][PUB04a]

4. <span data-ttu-id="4c977-132">在 hello **hello 新虛擬機器設定**視窗中，提供 hello 下列 Docker 主機的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4c977-132">In hello **Configure hello new virtual machine** window, provide hello following information about your Docker host.</span></span> <span data-ttu-id="4c977-133">（hello 精靈會自動產生大部分的 hello 資訊，但您可以修改任何其中）。</span><span class="sxs-lookup"><span data-stu-id="4c977-133">(hello wizard automatically generates most of hello information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="4c977-134">a.</span><span class="sxs-lookup"><span data-stu-id="4c977-134">a.</span></span> <span data-ttu-id="4c977-135">在 hello**名稱**方塊中，輸入 hello Docker 主機的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="4c977-135">In hello **Name** box, enter a unique name for hello Docker host.</span></span> <span data-ttu-id="4c977-136">（它是不 hello 與 hello 您稍早指定的 Docker 映像名稱相同）。</span><span class="sxs-lookup"><span data-stu-id="4c977-136">(It is not hello same as hello Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="4c977-137">b.</span><span class="sxs-lookup"><span data-stu-id="4c977-137">b.</span></span> <span data-ttu-id="4c977-138">在 hello**訂用帳戶**方塊中，輸入 hello 您為您的主機使用的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4c977-138">In hello **Subscription** box, enter hello Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="4c977-139">c.</span><span class="sxs-lookup"><span data-stu-id="4c977-139">c.</span></span> <span data-ttu-id="4c977-140">在 hello**區域**方塊中，輸入您的主機所在的 hello 地理區域。</span><span class="sxs-lookup"><span data-stu-id="4c977-140">In hello **Region** box, enter hello geographical region where your host is located.</span></span>
      
   <span data-ttu-id="4c977-141">d.</span><span class="sxs-lookup"><span data-stu-id="4c977-141">d.</span></span> <span data-ttu-id="4c977-142">在 hello **OS 和大小**索引標籤上，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="4c977-142">On hello **OS and Size** tab, do hello following:</span></span>      
      * <span data-ttu-id="4c977-143">**主機作業系統**: hello 虛擬機器，其中包含您的主機輸入 hello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="4c977-143">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="4c977-144">**大小**： 輸入您的主機 hello 虛擬機器大小。</span><span class="sxs-lookup"><span data-stu-id="4c977-144">**Size**: Enter hello virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="4c977-145">e.</span><span class="sxs-lookup"><span data-stu-id="4c977-145">e.</span></span> <span data-ttu-id="4c977-146">在 hello**資源群組**索引標籤上，選取其中一個 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="4c977-146">On hello **Resource Group** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="4c977-147">**新的資源群組**︰為主機建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="4c977-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="4c977-148">**現有的資源群組**︰指定 Azure 帳戶中的現有資源群組。</span><span class="sxs-lookup"><span data-stu-id="4c977-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="4c977-149">f.</span><span class="sxs-lookup"><span data-stu-id="4c977-149">f.</span></span> <span data-ttu-id="4c977-150">在 hello**網路**索引標籤上，選取其中一個 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="4c977-150">On hello **Network** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="4c977-151">**新的虛擬網路**︰為主機建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4c977-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="4c977-152">**現有的虛擬網路**︰指定 Azure 帳戶中的現有虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4c977-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="4c977-153">g.</span><span class="sxs-lookup"><span data-stu-id="4c977-153">g.</span></span> <span data-ttu-id="4c977-154">在 hello**儲存體**索引標籤上，選取其中一個 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="4c977-154">On hello **Storage** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="4c977-155">**新的儲存體帳戶**︰為主機建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4c977-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="4c977-156">**現有的儲存體帳戶**︰指定 Azure 帳戶中的現有儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4c977-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="4c977-157">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="4c977-157">Click **Next**.</span></span>  
     <span data-ttu-id="4c977-158">hello**設定記錄檔中的認證和連接埠設定**視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="4c977-158">hello **Configure log in credentials and port settings** window opens.</span></span>

      ![hello 設定登入認證和連接埠設定 視窗][PUB05]

6. <span data-ttu-id="4c977-160">選取其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="4c977-160">Select one of hello following options:</span></span>

      * <span data-ttu-id="4c977-161">**從 Azure Key Vault 匯入認證**︰指定先前儲存的一組認證，這些認證儲存在 Azure 訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="4c977-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="4c977-162">無法自動存取其他帳戶或服務主體共用 hello 訂用帳戶的 Azure 金鑰保存庫用來建立特定帳戶或服務主體。</span><span class="sxs-lookup"><span data-stu-id="4c977-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="4c977-163">tooallow 另一個帳戶或服務主體 toouse hello 金鑰保存庫，您必須使用 hello Azure 入口網站 tooadd hello 帳戶或服務主體。</span><span class="sxs-lookup"><span data-stu-id="4c977-163">tooallow another account or service principal toouse hello key vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

      * <span data-ttu-id="4c977-164">**新的登入認證**︰建立一組新的登入認證。</span><span class="sxs-lookup"><span data-stu-id="4c977-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="4c977-165">如果您選取此選項時，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="4c977-165">If you select this option, do hello following:</span></span>

        <span data-ttu-id="4c977-166">a.</span><span class="sxs-lookup"><span data-stu-id="4c977-166">a.</span></span> <span data-ttu-id="4c977-167">在 hello **VM 認證**索引標籤上，提供下列資訊 hello 虛擬機器的登入認證您的 Docker 主機 hello: * **Username**: hello 使用者名稱輸入虛擬機器登入認證。</span><span class="sxs-lookup"><span data-stu-id="4c977-167">On hello **VM Credentials** tab, provide hello following information for hello virtual-machine login credentials of your Docker host: * **Username**: Enter hello username for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="4c977-168">* **密碼**和**確認**: hello 密碼輸入您的虛擬機器的登入認證。</span><span class="sxs-lookup"><span data-stu-id="4c977-168">* **Password** and **Confirm**: Enter hello password for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="4c977-169">* **SSH**： 輸入 hello 安全殼層 (SSH) 設定為您的 Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="4c977-169">* **SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="4c977-170">您可以選取其中一個 hello 下列選項: ***無**： 指定您的虛擬機器不允許 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="4c977-170">You can select one of hello following options: * **None**: Specifies that your virtual machine does not allow SSH connections.</span></span>
                <span data-ttu-id="4c977-171">* **自動產生**： 會自動建立必要設定 hello 透過 SSH 的連接。</span><span class="sxs-lookup"><span data-stu-id="4c977-171">* **Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
                <span data-ttu-id="4c977-172">* **從目錄匯入**： 可讓您 toospecify 包含一組先前儲存的 SSH 設定的目錄。</span><span class="sxs-lookup"><span data-stu-id="4c977-172">* **Import from directory**: Allows you toospecify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="4c977-173">hello 目錄必須包含下列兩個檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="4c977-173">hello directory must contain hello following two files:</span></span>
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        <span data-ttu-id="4c977-174">b.</span><span class="sxs-lookup"><span data-stu-id="4c977-174">b.</span></span> <span data-ttu-id="4c977-175">在 hello **Docker Daemon 存取**索引標籤上，提供下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="4c977-175">On hello **Docker Daemon Access** tab, provide hello following information:</span></span>

          ![建立 Docker 主機][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. <span data-ttu-id="4c977-177">您輸入 hello 所需的資訊之後，請按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="4c977-177">After you have entered hello required information, click **Finish**.</span></span>  
    <span data-ttu-id="4c977-178">hello**在 Azure 上部署 Docker 容器**精靈隨即再度出現。</span><span class="sxs-lookup"><span data-stu-id="4c977-178">hello **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![[在 Azure 上部署 Docker 容器] 精靈][PUB07]

8. <span data-ttu-id="4c977-180">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="4c977-180">Click **Next**.</span></span>  
    <span data-ttu-id="4c977-181">hello**設定建立 hello Docker 容器 toobe**視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="4c977-181">hello **Configure hello Docker container toobe created** window opens.</span></span>

   ![hello 設定 hello Docker 容器 toobe 建立視窗][PUB08]

9. <span data-ttu-id="4c977-183">在 hello**設定建立 hello Docker 容器 toobe**視窗中，提供下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="4c977-183">In hello **Configure hello Docker container toobe created** window, provide hello following information:</span></span> 

   <span data-ttu-id="4c977-184">a.</span><span class="sxs-lookup"><span data-stu-id="4c977-184">a.</span></span> <span data-ttu-id="4c977-185">在 hello **Docker 容器名稱**方塊中，輸入您的 Docker 容器的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="4c977-185">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="4c977-186">b.</span><span class="sxs-lookup"><span data-stu-id="4c977-186">b.</span></span> <span data-ttu-id="4c977-187">選擇其中一個 hello 遵循 Docker 映像：</span><span class="sxs-lookup"><span data-stu-id="4c977-187">Choose one of hello following Docker images:</span></span> 

      * <span data-ttu-id="4c977-188">**預先定義的 Docker 映像**︰指定 Azure 中的既存 Docker 映像。</span><span class="sxs-lookup"><span data-stu-id="4c977-188">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="4c977-189">包含數個映像的 Docker 映像，在此方塊中的 hello 清單已使用 Azure Toolkit 該 hello 設定 toopatch，使您的成品會自動進行部署。</span><span class="sxs-lookup"><span data-stu-id="4c977-189">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="4c977-190">**自訂 Dockerfile**︰指定本機電腦中先前儲存的 Dockerfile。</span><span class="sxs-lookup"><span data-stu-id="4c977-190">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="4c977-191">這是開發人員希望 toodeploy 自己 Dockerfile 的更進階的功能。</span><span class="sxs-lookup"><span data-stu-id="4c977-191">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="4c977-192">不過，是由使用其 Dockerfile 已正確建置此選項 tooensure toodevelopers。</span><span class="sxs-lookup"><span data-stu-id="4c977-192">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="4c977-193">Hello Azure 工具組不會驗證自訂 Dockerfile 中的 hello 內容，因為如果 hello Dockerfile 有問題 hello 部署可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="4c977-193">Because hello Azure Toolkit does not validate hello content in a custom Dockerfile, hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="4c977-194">此外，由於 hello Azure Toolkit 預期 hello 自訂 Dockerfile toocontain web 應用程式成品，它會嘗試 tooopen HTTP 連接。</span><span class="sxs-lookup"><span data-stu-id="4c977-194">In addition, because hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, it attempts tooopen an HTTP connection.</span></span> <span data-ttu-id="4c977-195">如果開發人員發佈不同類型的構件，他們可能會在部署後收到無關緊要的錯誤。</span><span class="sxs-lookup"><span data-stu-id="4c977-195">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="4c977-196">c.</span><span class="sxs-lookup"><span data-stu-id="4c977-196">c.</span></span> <span data-ttu-id="4c977-197">在 hello**連接埠設定**方塊中，輸入 hello 唯一的 TCP 連接埠繫結的 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="4c977-197">In hello **Port settings** box, enter hello unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="4c977-198">您已完成 hello 先前步驟之後，請按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="4c977-198">After you have completed hello preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="4c977-199">hello Azure Toolkit 開始部署您的 Docker 容器中的 web 應用程式 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="4c977-199">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> <span data-ttu-id="4c977-200">除非您已設定部署在 hello 背景 IntelliJ toobe**部署 tooAzure**進度列顯示。</span><span class="sxs-lookup"><span data-stu-id="4c977-200">Unless you have configured IntelliJ toobe deployed in hello background, a **Deploying tooAzure** progress bar appears.</span></span> 

![hello 部署進度列][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="4c977-202">建立構件的其他資訊</span><span class="sxs-lookup"><span data-stu-id="4c977-202">Additional information about creating artifacts</span></span>

<span data-ttu-id="4c977-203">toocreate 可供部署的成品，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="4c977-203">toocreate a deployment-ready artifact, do hello following:</span></span>

1. <span data-ttu-id="4c977-204">在 IntelliJ 中開啟 web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="4c977-204">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="4c977-205">依序按一下 [檔案] 及 [專案結構]。</span><span class="sxs-lookup"><span data-stu-id="4c977-205">Click **File**, and then click **Project Structure**.</span></span>

   ![hello 專案結構命令][ART01]

3. <span data-ttu-id="4c977-207">tooadd 的成品，按一下 hello 綠色加號 (**+**)，然後按一下 **Web 應用程式： 封存**。</span><span class="sxs-lookup"><span data-stu-id="4c977-207">tooadd an artifact, click hello green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![hello 「 Web 應用程式:: 封存 」 命令][ART02]

4. <span data-ttu-id="4c977-209">在 hello**名稱**方塊中，輸入您的成品名稱 (不包括 hello *.war*延伸模組)，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="4c977-209">In hello **Name** box, enter a name for your artifact (do not include hello *.war* extension), and then click **OK**.</span></span>

   ![hello 成品名稱 方塊][ART03]

<span data-ttu-id="4c977-211">如需在 IntelliJ 中建立成品的詳細資訊，請參閱[設定成品]hello JetBrains 網站上。</span><span class="sxs-lookup"><span data-stu-id="4c977-211">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on hello JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c977-212">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4c977-212">Next steps</span></span>
<span data-ttu-id="4c977-213">針對 Java Ide hello Azure 工具套件的相關資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="4c977-213">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="4c977-214">[適用於 Eclipse 的 Azure 工具組]</span><span class="sxs-lookup"><span data-stu-id="4c977-214">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="4c977-215">[在 hello Azure Toolkit for Eclipse 中最新消息]</span><span class="sxs-lookup"><span data-stu-id="4c977-215">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="4c977-216">[安裝 Azure Toolkit for Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="4c977-216">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="4c977-217">[登入指示 hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4c977-217">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="4c977-218">[在 Eclipse 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="4c977-218">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="4c977-219">[Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="4c977-219">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="4c977-220">[在 hello Azure Toolkit for IntelliJ 最新消息]</span><span class="sxs-lookup"><span data-stu-id="4c977-220">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="4c977-221">[安裝 hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="4c977-221">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="4c977-222">[登入的指示 hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="4c977-222">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="4c977-223">[在 IntelliJ 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="4c977-223">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="4c977-224">如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心]和 hello [Java 工具的 Visual Studio Team Services]。</span><span class="sxs-lookup"><span data-stu-id="4c977-224">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="4c977-225">如需對 Docker 的其他資源，請參閱 hello 官方[Docker 網站]。</span><span class="sxs-lookup"><span data-stu-id="4c977-225">For additional resources for Docker, see hello official [Docker website].</span></span>

<!-- URL List -->

[適用於 Eclipse 的 Azure 工具組]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md
[在 Eclipse 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[在 IntelliJ 中建立 Azure Hello World Web 應用程式]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[安裝 Azure Toolkit for Eclipse hello]: ./azure-toolkit-for-eclipse-installation.md
[安裝 hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[登入指示 hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[登入的指示 hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[在 hello Azure Toolkit for Eclipse 中最新消息]: ./azure-toolkit-for-eclipse-whats-new.md
[在 hello Azure Toolkit for IntelliJ 最新消息]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java 開發人員中心]: https://azure.microsoft.com/develop/java/
[Java 工具的 Visual Studio Team Services]: https://java.visualstudio.com/

[Docker 網站]: https://www.docker.com/
[設定成品]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png

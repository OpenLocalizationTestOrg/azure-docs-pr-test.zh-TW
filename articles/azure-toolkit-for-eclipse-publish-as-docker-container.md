---
title: "使用 Docker 容器 aaaPublish hello Azure Toolkit for Eclipse |Microsoft 文件"
description: "深入了解如何為 Docker 容器使用的 Azure web 應用程式 tooMicrosoft toopublish hello Azure Toolkit for Eclipse。"
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
ms.openlocfilehash: 53ec3a7f7a171691024e03622fd48d6f1e257b50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="c9cc2-103">Docker 容器發行 web 應用程式使用 hello Azure Toolkit for Eclipse</span><span class="sxs-lookup"><span data-stu-id="c9cc2-103">Publish a web app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="c9cc2-104">Docker 容器是常見的 Web 應用程式部署方法。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="c9cc2-105">藉由使用 Docker 容器，開發人員可以將合併所有的專案檔和成單一封裝的部署 tooa 伺服器的相依性。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="c9cc2-106">hello Azure Toolkit for Eclipse 的 Java 開發人員簡化此程序，藉由新增*發佈為 Docker 容器*部署 tooMicrosoft Azure 的功能。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-106">hello Azure Toolkit for Eclipse simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="c9cc2-107">本文將告訴您透過 hello 步驟需要 toopublish 應用程式 tooAzure 做為 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
> <span data-ttu-id="c9cc2-108">Docker 的詳細資訊位於 hello [Docker 網站]。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="c9cc2-109">使用 Docker 容器發行您的 web 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="c9cc2-109">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="c9cc2-110">在 Eclipse 中開啟 web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-110">Open your web app project in Eclipse.</span></span>

2. <span data-ttu-id="c9cc2-111">toostart hello**發佈為 Docker 容器**精靈 中，執行 hello 下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="c9cc2-111">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="c9cc2-112">在 hello**導覽**檢視，以滑鼠右鍵按一下您的專案，請按一下**Azure**，然後按一下**發佈為 Docker 容器**。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-112">In hello **Navigator** view, right-click your project, click **Azure**, and then click **Publish as Docker Container**.</span></span>

      ![導覽器檢視 [發佈作為 Docker 容器] 命令][PUB01]

   * <span data-ttu-id="c9cc2-114">Hello Eclipse 工具列上，按一下 hello**發行**按鈕，然後再按一下**發佈為 Docker 容器**。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-114">On hello Eclipse toolbar, click hello **Publish** button, and then click **Publish as Docker Container**.</span></span>

      ![Eclipse 工具列 [發佈作為 Docker 容器] 命令][PUB02]
      
    <span data-ttu-id="c9cc2-116">hello**在 Azure 上部署 Docker 容器**精靈 隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-116">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

    ![hello Azure 精靈上部署 Docker 容器][PUB03]

3. <span data-ttu-id="c9cc2-118">在 hello**輸入映像名稱選取 hello 成品路徑，請檢查使用 Docker 主機 toobe**視窗中，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="c9cc2-118">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span>

    <span data-ttu-id="c9cc2-119">a.</span><span class="sxs-lookup"><span data-stu-id="c9cc2-119">a.</span></span> <span data-ttu-id="c9cc2-120">在 hello **Docker 映像名稱**方塊中，輸入您的 Docker 主機的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-120">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="c9cc2-121">（hello 精靈會自動建立一個名稱，但您可以修改它）。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-121">(hello wizard automatically creates a name, but you can modify it.)</span></span>

    <span data-ttu-id="c9cc2-122">b.</span><span class="sxs-lookup"><span data-stu-id="c9cc2-122">b.</span></span> <span data-ttu-id="c9cc2-123">hello**主機**區域會顯示您已經建立任何 Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-123">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="c9cc2-124">執行 hello 下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="c9cc2-124">Do either of hello following:</span></span>

    * <span data-ttu-id="c9cc2-125">如果您有現有的 Docker 主機，您可以部署您的 web 應用程式 tooit。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-125">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
    * <span data-ttu-id="c9cc2-126">按一下 新的 Docker 主機，toocreate**新增**。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-126">toocreate a new Docker host, click **Add**.</span></span>  
      
    <span data-ttu-id="c9cc2-127">hello**建立 Docker 主機**對話方塊隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-127">hello **Create Docker Host** dialog box opens.</span></span>

    ![[在 Azure 上部署 Docker 容器] 精靈][PUB04a]

4. <span data-ttu-id="c9cc2-129">在 hello **hello 新虛擬機器設定**視窗中，指定下列選項，為您的 Docker 主機 hello。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-129">In hello **Configure hello new virtual machine** window, specify hello following options for your Docker host.</span></span> <span data-ttu-id="c9cc2-130">（hello 精靈會自動產生大部分的 hello 選項，但您可以修改任何其中）。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-130">(hello wizard automatically generates most of hello options for you, but you can modify any of them.)</span></span>

   <span data-ttu-id="c9cc2-131">a.</span><span class="sxs-lookup"><span data-stu-id="c9cc2-131">a.</span></span> <span data-ttu-id="c9cc2-132">**名稱**： 輸入 hello Docker 主機的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-132">**Name**: Enter a unique name for hello Docker host.</span></span> <span data-ttu-id="c9cc2-133">（它是不 hello 與 hello 您稍早指定的 Docker 映像名稱相同）。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-133">(It is not hello same as hello Docker image name that you specified earlier.)</span></span>

   <span data-ttu-id="c9cc2-134">b.</span><span class="sxs-lookup"><span data-stu-id="c9cc2-134">b.</span></span> <span data-ttu-id="c9cc2-135">**訂用帳戶**： 輸入 hello 您為您的主機使用的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-135">**Subscription**: Enter hello Azure subscription that you use for your host.</span></span>

   <span data-ttu-id="c9cc2-136">c.</span><span class="sxs-lookup"><span data-stu-id="c9cc2-136">c.</span></span> <span data-ttu-id="c9cc2-137">**區域**： 輸入 hello 主機所在的地理區域。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-137">**Region**: Enter hello geographical region where your host is located.</span></span>

   <span data-ttu-id="c9cc2-138">d.</span><span class="sxs-lookup"><span data-stu-id="c9cc2-138">d.</span></span> <span data-ttu-id="c9cc2-139">在 [hello**主機作業系統和大小**] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="c9cc2-139">On hello **Host OS and Size** tab:</span></span>
     * <span data-ttu-id="c9cc2-140">**主機作業系統**: hello 虛擬機器，其中包含您的主機輸入 hello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-140">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span>
     * <span data-ttu-id="c9cc2-141">**大小**： 輸入您的主機 hello 虛擬機器大小。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-141">**Size**: Enter hello virtual-machine size for your host.</span></span>

   <span data-ttu-id="c9cc2-142">e.</span><span class="sxs-lookup"><span data-stu-id="c9cc2-142">e.</span></span> <span data-ttu-id="c9cc2-143">在 [hello**資源群組**] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="c9cc2-143">On hello **Resource Group** tab:</span></span>
     * <span data-ttu-id="c9cc2-144">**新的資源群組**︰為主機建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-144">**New resource group**: Create a new resource group for your host.</span></span>
     * <span data-ttu-id="c9cc2-145">**現有的資源群組**︰輸入 Azure 帳戶中的現有資源群組。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-145">**Existing resource group**: Enter an existing resource group from your Azure account.</span></span>

   <span data-ttu-id="c9cc2-146">f.</span><span class="sxs-lookup"><span data-stu-id="c9cc2-146">f.</span></span> <span data-ttu-id="c9cc2-147">在 [hello**網路**] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="c9cc2-147">On hello **Network** tab:</span></span>
     * <span data-ttu-id="c9cc2-148">**新的虛擬網路**︰為主機建立新的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-148">**New virtual network**: Create a new virtual network for your host.</span></span>
     * <span data-ttu-id="c9cc2-149">**現有的虛擬網路**︰輸入 Azure 帳戶中的現有虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-149">**Existing virtual network**: Enter an existing virtual network from your Azure account.</span></span>

   <span data-ttu-id="c9cc2-150">g.</span><span class="sxs-lookup"><span data-stu-id="c9cc2-150">g.</span></span> <span data-ttu-id="c9cc2-151">在 [hello**儲存體**] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="c9cc2-151">On hello **Storage** tab:</span></span>
     * <span data-ttu-id="c9cc2-152">**新的儲存體帳戶**︰為主機建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-152">**New storage account**: Create a new storage account for your host.</span></span>
     * <span data-ttu-id="c9cc2-153">**現有的儲存體帳戶**︰輸入 Azure 帳戶中的現有儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-153">**Existing storage account**: Enter an existing storage account from your Azure account.</span></span>

5. <span data-ttu-id="c9cc2-154">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-154">Click **Next**.</span></span>

6. <span data-ttu-id="c9cc2-155">在 [hello**設定記錄檔中的認證和連接埠設定**] 視窗中，選取其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="c9cc2-155">In hello **Configure log in credentials and port settings** window, select one of hello following options:</span></span>

    * <span data-ttu-id="c9cc2-156">**從 Azure Key Vault 匯入認證**︰指定先前儲存在 Azure 訂用帳戶中的一組認證。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-156">**Import credentials from Azure Key Vault**: Specifies a previously saved set of credentials that are stored in your Azure subscription.</span></span>

      >[!NOTE]
      ><span data-ttu-id="c9cc2-157">無法自動存取其他帳戶或服務主體共用 hello 訂用帳戶的 Azure 金鑰保存庫用來建立特定帳戶或服務主體。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-157">An Azure Key Vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="c9cc2-158">tooallow 另一個帳戶或服務主體 toouse hello 金鑰保存庫，您必須使用 hello Azure 入口網站 tooadd hello 帳戶或服務主體。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-158">tooallow another account or service principal toouse hello Key Vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

    * <span data-ttu-id="c9cc2-159">**新的登入認證**︰建立一組新的登入認證。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-159">**New log in credentials**: Creates a new set of login credentials.</span></span> <span data-ttu-id="c9cc2-160">如果您選取此選項時，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="c9cc2-160">If you select this option, do hello following:</span></span>
    
      * <span data-ttu-id="c9cc2-161">在 hello **VM 認證**索引標籤上，選擇 hello 下列其中一種 hello 的 Docker 主機的虛擬機器登入認證的選項：</span><span class="sxs-lookup"><span data-stu-id="c9cc2-161">On hello **VM Credentials** tab, choose one of hello following options for hello virtual-machine login credentials of your Docker host:</span></span>

          * <span data-ttu-id="c9cc2-162">**使用者名稱**： 輸入您的虛擬機器的登入認證 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-162">**Username**: Enter hello username for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="c9cc2-163">**密碼**和**確認**: hello 密碼輸入您的虛擬機器的登入認證。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-163">**Password** and **Confirm**: Enter hello password for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="c9cc2-164">**SSH**： 輸入 hello 安全殼層 (SSH) 設定為您的 Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-164">**SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="c9cc2-165">您可以選擇下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="c9cc2-165">You can choose from hello following options:</span></span>
            * <span data-ttu-id="c9cc2-166">**無**︰指定虛擬機器將不允許 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-166">**None**: Specifies that your virtual machine will not allow SSH connections.</span></span>
            * <span data-ttu-id="c9cc2-167">**自動產生**： 會自動建立必要設定 hello 透過 SSH 的連接。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-167">**Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
            * <span data-ttu-id="c9cc2-168">**從目錄匯入**︰指定內含一組先前儲存之 SSH 設定的目錄。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-168">**Import from directory**: Specifies a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="c9cc2-169">hello 目錄必須包含下列兩個檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="c9cc2-169">hello directory must contain hello following two files:</span></span>
                * <span data-ttu-id="c9cc2-170">*id_rsa*： 包含 hello RSA 識別使用者。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-170">*id_rsa*: Contains hello RSA identification for a user.</span></span>
                * <span data-ttu-id="c9cc2-171">*id_rsa.pub*: hello RSA 公開金鑰是用來驗證。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-171">*id_rsa.pub*: Contains hello RSA public key that is used for authentication.</span></span>
        
        ![建立 Docker 主機][PUB05]

      * <span data-ttu-id="c9cc2-173">在 hello **Docker Daemon 認證**索引標籤上，指定下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="c9cc2-173">On hello **Docker Daemon Credentials** tab, specify hello following options:</span></span>

          * <span data-ttu-id="c9cc2-174">**Docker 精靈通訊埠**： 輸入您的 Docker 主機 hello 唯一的 TCP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-174">**Docker Daemon port**: Enter hello unique TCP port for your Docker host.</span></span>
          * <span data-ttu-id="c9cc2-175">**TLS 安全性**： 輸入您的 Docker 主機的 hello 傳輸層安全性設定。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-175">**TLS Security**: Enter hello Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="c9cc2-176">您可以選擇下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="c9cc2-176">You can choose from hello following options:</span></span>
            * <span data-ttu-id="c9cc2-177">**無**︰指定虛擬機器將不允許 TLS 連線。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-177">**None**: Specifies that your virtual machine will not allow TLS connections.</span></span>
            * <span data-ttu-id="c9cc2-178">**自動產生**： 會自動建立必要設定 hello 透過 TLS 連線。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-178">**Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.</span></span>
            * <span data-ttu-id="c9cc2-179">**從目錄匯入**︰指定內含一組先前儲存之 TLS 設定的目錄。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-179">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="c9cc2-180">更具體來說，hello 目錄必須包含下列六個檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="c9cc2-180">More specifically, hello directory must contain hello following six files:</span></span>
                * <span data-ttu-id="c9cc2-181">*ca.pem*和*ca key.pem*： 包含 hello 憑證和公開金鑰 hello TLS 憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-181">*ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.</span></span>
                * <span data-ttu-id="c9cc2-182">*cert.pem*和*key.pem*： 包含 hello 用戶端憑證和公開金鑰用於 TLS 驗證。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-182">*cert.pem* and *key.pem*: Contain hello client certificate and public key that is used for TLS authentication.</span></span>
                * <span data-ttu-id="c9cc2-183">*server.pem*和*伺服器 key.pem*： 包含 hello 伺服器憑證和公開金鑰 hello 主機。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-183">*server.pem* and *server-key.pem*: Contain hello server certificate and public key for hello host.</span></span>

        ![建立 Docker 主機][PUB06]

7. <span data-ttu-id="c9cc2-185">輸入所有 hello 上述資訊之後，請按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-185">After you have entered all of hello preceding information, click **Finish**.</span></span>

8. <span data-ttu-id="c9cc2-186">在 hello**在 Azure 上部署 Docker 容器**精靈 中，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-186">In hello **Deploy Docker Container on Azure** wizard, click **Next**.</span></span>

   ![hello Azure 精靈上部署 Docker 容器][PUB07]

9. <span data-ttu-id="c9cc2-188">在 hello**設定建立 hello Docker 容器 toobe**視窗中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="c9cc2-188">In hello **Configure hello Docker container toobe created** window, do hello following:</span></span>

   <span data-ttu-id="c9cc2-189">a.</span><span class="sxs-lookup"><span data-stu-id="c9cc2-189">a.</span></span> <span data-ttu-id="c9cc2-190">在 hello **Docker 容器名稱**方塊中，輸入您的 Docker 容器的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-190">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="c9cc2-191">b.</span><span class="sxs-lookup"><span data-stu-id="c9cc2-191">b.</span></span> <span data-ttu-id="c9cc2-192">選擇其中一個 hello 遵循 Docker 映像：</span><span class="sxs-lookup"><span data-stu-id="c9cc2-192">Choose one of hello following Docker images:</span></span>
     * <span data-ttu-id="c9cc2-193">**預先定義的 Docker 映像**︰指定 Azure 中的既存 Docker 映像。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-193">**Predefined Docker image**: Specifies a pre-existing Docker image from Azure.</span></span>

       >[!NOTE]
       ><span data-ttu-id="c9cc2-194">包含數個映像的 Docker 映像，在此方塊中的 hello 清單已使用 Azure Toolkit 該 hello 設定 toopatch，使您的成品會自動進行部署。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-194">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span>

     * <span data-ttu-id="c9cc2-195">**自訂 Dockerfile**︰指定本機電腦中先前儲存的 Dockerfile。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-195">**Custom Dockerfile**: Specifies a previously saved Dockerfile from your local computer.</span></span>

       >[!NOTE]
       ><span data-ttu-id="c9cc2-196">這是開發人員希望 toodeploy 自己 Dockerfile 的更進階的功能。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-196">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="c9cc2-197">不過，是由使用其 Dockerfile 已正確建置此選項 tooensure toodevelopers。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-197">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="c9cc2-198">hello Azure Toolkit 不會驗證 hello 內容中自訂 Dockerfile 中，因此如果 hello Dockerfile 有問題，hello 部署可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-198">hello Azure Toolkit does not validate hello content in a custom Dockerfile, so hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="c9cc2-199">此外，hello Azure Toolkit 預期自訂 Dockerfile toocontain hello 的 web 應用程式成品，並會 tooopen HTTP 連接。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-199">In addition, hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, and it will attempt tooopen an HTTP connection.</span></span> <span data-ttu-id="c9cc2-200">如果開發人員發佈不同類型的構件，他們可能會在部署後收到無關緊要的錯誤。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-200">If developers publish a different type of artifact, they may receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="c9cc2-201">c.</span><span class="sxs-lookup"><span data-stu-id="c9cc2-201">c.</span></span> <span data-ttu-id="c9cc2-202">**連接埠設定**： 輸入 hello 唯一的 TCP 連接埠繫結的 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-202">**Port settings**: Enter hello unique TCP port binding for your Docker container.</span></span>

     ![hello 設定 hello Docker 容器 toobe 建立視窗][PUB08]

10. <span data-ttu-id="c9cc2-204">您已完成所有 hello 先前步驟之後，請按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-204">After you have completed all of hello preceding steps, click **Finish**.</span></span>

<span data-ttu-id="c9cc2-205">hello Azure Toolkit 開始部署您的 Docker 容器中的 web 應用程式 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-205">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c9cc2-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c9cc2-206">Next steps</span></span>
<span data-ttu-id="c9cc2-207">針對 Java Ide hello Azure 工具套件的相關資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="c9cc2-207">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="c9cc2-208">[適用於 Eclipse 的 Azure 工具組]</span><span class="sxs-lookup"><span data-stu-id="c9cc2-208">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c9cc2-209">[在 hello Azure Toolkit for Eclipse 中最新消息]</span><span class="sxs-lookup"><span data-stu-id="c9cc2-209">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c9cc2-210">[安裝 Azure Toolkit for Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="c9cc2-210">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c9cc2-211">[登入指示 hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c9cc2-211">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c9cc2-212">[在 Eclipse 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="c9cc2-212">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="c9cc2-213">[Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c9cc2-213">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c9cc2-214">[在 hello Azure Toolkit for IntelliJ 最新消息]</span><span class="sxs-lookup"><span data-stu-id="c9cc2-214">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c9cc2-215">[安裝 hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c9cc2-215">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c9cc2-216">[登入的指示 hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c9cc2-216">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c9cc2-217">[在 IntelliJ 中建立 Azure Hello World Web 應用程式]</span><span class="sxs-lookup"><span data-stu-id="c9cc2-217">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="c9cc2-218">如需有關使用 Azure 搭配 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心]和[適用於 Visual Studio Team Services 的 Java 工具]。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-218">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="c9cc2-219">如需對 Docker 的其他資源，請參閱 hello 官方[Docker 網站]。</span><span class="sxs-lookup"><span data-stu-id="c9cc2-219">For additional resources for Docker, see hello official [Docker website].</span></span>

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
[適用於 Visual Studio Team Services 的 Java 工具]: https://java.visualstudio.com/

[Docker 網站]: https://www.docker.com/

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png
---
title: "aaaUsing 適用於 Linux 的 Docker VM 擴充功能 |Microsoft 文件"
description: "描述 Docker 和 hello Azure 虛擬機器擴充功能，以及 toocreate docker 主機使用的 Azure 虛擬機器 hello Azure CLI 傳統部署模型中的方式。"
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 19cf64e8-f92c-43ad-a120-8976cd9102ac
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/27/2016
ms.author: rasquill
ms.openlocfilehash: 9d455b63c48b0c1b6f14862e072f899a73b46153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a><span data-ttu-id="062d1-103">使用 hello Azure 傳統入口網站中的 hello Docker VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="062d1-103">Using hello Docker VM Extension with hello Azure classic portal</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="062d1-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="062d1-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="062d1-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="062d1-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="062d1-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="062d1-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="062d1-107">[Docker](https://www.docker.com/)是 hello 的其中一個最普遍使用的虛擬化方法[Linux 容器](http://en.wikipedia.org/wiki/LXC)而不是虛擬機器做為隔離資料，並在共用資源上運算的方式。</span><span class="sxs-lookup"><span data-stu-id="062d1-107">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="062d1-108">您可以使用由管理的 hello Docker VM 擴充功能[Azure Linux 代理程式]toocreate 裝載任何數目的容器應用程式在 Azure 上的 Docker VM。</span><span class="sxs-lookup"><span data-stu-id="062d1-108">You can use hello Docker VM extension managed by [Azure Linux Agent] toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="062d1-109">本主題描述如何從 Docker VM 的 toocreate hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="062d1-109">This topic describes how toocreate a Docker VM from hello Azure classic portal.</span></span> <span data-ttu-id="062d1-110">如何 toocreate Docker VM 在 hello 命令列，請參閱的 toosee [toouse hello Azure 命令列介面 (Azure CLI) 從 hello Docker VM 擴充功能的方式]。</span><span class="sxs-lookup"><span data-stu-id="062d1-110">toosee how toocreate a Docker VM at hello command line, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)].</span></span> <span data-ttu-id="062d1-111">toosee 高層級容器和 lamdba 的優點的討論，請參閱 「 hello [Docker 高的層級抄寫](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard)。</span><span class="sxs-lookup"><span data-stu-id="062d1-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a><span data-ttu-id="062d1-112">從 hello 映像庫中建立新的 VM</span><span class="sxs-lookup"><span data-stu-id="062d1-112">Create a new VM from hello Image Gallery</span></span>
<span data-ttu-id="062d1-113">hello 第一個步驟之前，必須從 Linux 映像支援 Docker VM 擴充功能，使用做為範例伺服器映像和 Ubuntu 14.04 桌面的 Ubuntu 14.04 LTS 從 hello 映像庫映像，做為用戶端 hello Azure VM。</span><span class="sxs-lookup"><span data-stu-id="062d1-113">hello first step requires an Azure VM from a Linux image that supports hello Docker VM Extension, using an Ubuntu 14.04 LTS image from hello Image Gallery as an example server image and Ubuntu 14.04 Desktop as a client.</span></span> <span data-ttu-id="062d1-114">在 hello 入口網站中，按一下  **+ 新增**在 hello 底部往左角 toocreate 新的 VM 執行個體，並選取從可用的 hello 選項或 hello Ubuntu 14.04 LTS 映像完成映像庫，如下所示。</span><span class="sxs-lookup"><span data-stu-id="062d1-114">In hello portal, click **+ New** in hello bottom left corner toocreate a new VM instance and select an Ubuntu 14.04 LTS image from hello selections available or from hello complete Image Gallery, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="062d1-115">目前，只有 Ubuntu 14.04 LTS 映像以上 2014 年 7 月支援 hello Docker VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="062d1-115">Currently, only Ubuntu 14.04 LTS images more recent than July 2014 support hello Docker VM Extension.</span></span>
> 
> 

![Create a new Ubuntu Image](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a><span data-ttu-id="062d1-117">建立 Docker 憑證</span><span class="sxs-lookup"><span data-stu-id="062d1-117">Create Docker Certificates</span></span>
<span data-ttu-id="062d1-118">Hello 之後建立 VM，確定已安裝 Docker 用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="062d1-118">After hello VM has been created, ensure that Docker is installed on your client computer.</span></span> <span data-ttu-id="062d1-119">(如需詳細資訊，請參閱 [Docker 安裝指示](https://docs.docker.com/installation/#installation)。)</span><span class="sxs-lookup"><span data-stu-id="062d1-119">(For details, see [Docker installation instructions](https://docs.docker.com/installation/#installation).)</span></span>

<span data-ttu-id="062d1-120">建立 hello 太根據 Docker 通訊的憑證與金鑰檔案[執行 Docker https]並將它們放在 hello  **`~/.docker`** 目錄用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="062d1-120">Create hello certificate and key files for Docker communication according too[Running Docker with https] and place them in hello **`~/.docker`** directory on your client computer.</span></span>

> [!NOTE]
> <span data-ttu-id="062d1-121">hello 入口網站中的 hello Docker VM 擴充功能目前需要是以 base64 編碼的認證。</span><span class="sxs-lookup"><span data-stu-id="062d1-121">hello Docker VM Extension in hello portal currently requires credentials that are base64 encoded.</span></span>
> 
> 

<span data-ttu-id="062d1-122">在 hello 命令列使用 **`base64`** 或另一個編碼 tool toocreate base64 編碼主題的最愛。</span><span class="sxs-lookup"><span data-stu-id="062d1-122">At hello command line, use **`base64`** or another favorite encoding tool toocreate base64-encoded topics.</span></span> <span data-ttu-id="062d1-123">執行此動作有一組簡單的憑證與金鑰檔案，可能看起來類似 toothis:</span><span class="sxs-lookup"><span data-stu-id="062d1-123">Doing this with a simple set of certificate and key files might look similar toothis:</span></span>

```
 ~/.docker$ ls
 ca-key.pem  ca.pem  cert.pem  key.pem  server-cert.pem  server-key.pem
 ~/.docker$ base64 ca.pem > ca64.pem
 ~/.docker$ base64 server-cert.pem > server-cert64.pem
 ~/.docker$ base64 server-key.pem > server-key64.pem
 ~/.docker$ ls
 ca64.pem    ca.pem    key.pem            server-cert.pem   server-key.pem
 ca-key.pem  cert.pem  server-cert64.pem  server-key64.pem
```

## <a name="add-hello-docker-vm-extension"></a><span data-ttu-id="062d1-124">新增 hello Docker VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="062d1-124">Add hello Docker VM Extension</span></span>
<span data-ttu-id="062d1-125">tooadd hello Docker VM 擴充功能，找出您所建立的 hello VM 執行個體，並向下捲動太**延伸**按一下 toobring VM 延伸模組，如下所示。</span><span class="sxs-lookup"><span data-stu-id="062d1-125">tooadd hello Docker VM Extension, locate hello VM instance you created and scroll down too**Extensions** and click it toobring up VM Extensions, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="062d1-126">Hello 預覽入口網站中支援這項功能： https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="062d1-126">This functionality is supported in hello preview portal only: https://portal.azure.com/</span></span>
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a><span data-ttu-id="062d1-127">新增擴充程式</span><span class="sxs-lookup"><span data-stu-id="062d1-127">Add an Extension</span></span>
<span data-ttu-id="062d1-128">按一下 hello **+ 加**toodisplay hello 可能可以新增 toothis VM 的 VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="062d1-128">Click hello **+ Add** toodisplay hello possible VM Extensions you can add toothis VM.</span></span>

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a><span data-ttu-id="062d1-129">選取 hello Docker VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="062d1-129">Select hello Docker VM Extension</span></span>
<span data-ttu-id="062d1-130">選擇 hello Docker VM 擴充功能，這會顯示 hello Docker 描述和重要的連結，然後再按一下**建立**在 hello 底部 toobegin hello 安裝程序。</span><span class="sxs-lookup"><span data-stu-id="062d1-130">Choose hello Docker VM Extension, which brings up hello Docker description and important links, and then click **Create** at hello bottom toobegin hello installation procedure.</span></span>

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a><span data-ttu-id="062d1-131">新增憑證和金鑰檔案：</span><span class="sxs-lookup"><span data-stu-id="062d1-131">Add your Certificate and Key Files:</span></span>
<span data-ttu-id="062d1-132">Hello 表單在欄位中，輸入 hello base64 編碼的版本您的 CA 憑證，您的伺服器憑證，而您的伺服器金鑰，hello 下列圖片所示。</span><span class="sxs-lookup"><span data-stu-id="062d1-132">In hello form fields, enter hello base64-encoded versions of your CA Certificate, your Server Certificate, and your Server Key, as shown in hello following graphic.</span></span>

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> <span data-ttu-id="062d1-133">請注意，（如同在上述映像的 hello) hello 2376 預設會填入。</span><span class="sxs-lookup"><span data-stu-id="062d1-133">Note that (as in hello preceding image) hello 2376 is filled in by default.</span></span> <span data-ttu-id="062d1-134">您可以輸入任何端點，但是 hello 下一個步驟將會比對端點的 hello 向上 tooopen。</span><span class="sxs-lookup"><span data-stu-id="062d1-134">You can enter any endpoint here, but hello next step will be tooopen up hello matching endpoint.</span></span> <span data-ttu-id="062d1-135">如果您變更 hello 預設值，請確定 tooopen 向上 hello 比對 hello 下一個步驟中的端點。</span><span class="sxs-lookup"><span data-stu-id="062d1-135">If you change hello default, make sure tooopen up hello matching endpoint in hello next step.</span></span>
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a><span data-ttu-id="062d1-136">新增 hello Docker 通訊端點</span><span class="sxs-lookup"><span data-stu-id="062d1-136">Add hello Docker Communication Endpoint</span></span>
<span data-ttu-id="062d1-137">當您檢視您已建立 hello 資源群組，選取與您的 VM 的網路安全性群組相關聯的 hello，然後按一下**輸入安全性規則**tooview hello 規則如下所示。</span><span class="sxs-lookup"><span data-stu-id="062d1-137">When viewing hello resource group you've created, select hello Network Security Group associated with your VM, and click **Inbound Security Rules** tooview hello rules as shown here.</span></span>

![](media/portal-use-docker/AddingEndpoint.png)

<span data-ttu-id="062d1-138">按一下**+ 加**tooadd 另一個規則，並在 hello 預設情況下，輸入 hello 端點的名稱 (在此範例中， **Docker**)，和 2376年 ' 目的地連接埠範圍 '。</span><span class="sxs-lookup"><span data-stu-id="062d1-138">Click **+ Add** tooadd another rule, and in hello default case, enter a name for hello endpoint (in this example, **Docker**), and 2376 'Destination Port Range'.</span></span> <span data-ttu-id="062d1-139">設定 hello 通訊協定值顯示**TCP**，然後按一下**確定**toocreate hello 規則。</span><span class="sxs-lookup"><span data-stu-id="062d1-139">Set hello protocol value showing **TCP**, and Click **OK** toocreate hello rule.</span></span>

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a><span data-ttu-id="062d1-140">測試 Docker 用戶端和 Azure Docker 主機</span><span class="sxs-lookup"><span data-stu-id="062d1-140">Test your Docker Client and Azure Docker Host</span></span>
<span data-ttu-id="062d1-141">找出並複製 VM 的網域，而且在 hello 命令列的用戶端電腦，類型的 hello 名稱`docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (其中*dockerextension*取代為 hello子網域的 VM）。</span><span class="sxs-lookup"><span data-stu-id="062d1-141">Locate and copy hello name of your VM's domain, and at hello command line of your client computer, type `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` (where *dockerextension* is replaced by hello subdomain for your VM).</span></span>

<span data-ttu-id="062d1-142">hello 結果應該會出現類似 toothis:</span><span class="sxs-lookup"><span data-stu-id="062d1-142">hello result should appear similar toothis:</span></span>

```
$ docker --tls -H tcp://dockerextension.cloudapp.net:2376 info
Containers: 0
Images: 0
Storage Driver: devicemapper
 Pool Name: docker-8:1-131214-pool
 Pool Blocksize: 65.54 kB
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 305.7 MB
 Data Space Total: 107.4 GB
 Metadata Space Used: 729.1 kB
 Metadata Space Total: 2.147 GB
 Library Version: 1.02.82-git (2013-10-04)
Execution Driver: native-0.2
Kernel Version: 3.13.0-36-generic
WARNING: No swap limit support
```

<span data-ttu-id="062d1-143">一旦您完成上述步驟 hello，現在有完全正常運作的 Docker 主機，在 Azure VM 中，設定執行 toobe 連接 tooremotely 從其他用戶端。</span><span class="sxs-lookup"><span data-stu-id="062d1-143">Once you complete hello above steps, you now have a fully functional Docker host running on an Azure VM, configured toobe connected tooremotely from other clients.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="062d1-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="062d1-144">Next steps</span></span>
<span data-ttu-id="062d1-145">您已準備好 toogo toohello [Docker 使用者指南]並使用您的 Docker VM。</span><span class="sxs-lookup"><span data-stu-id="062d1-145">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="062d1-146">如果您想 tooautomate 建立 Azure Vm 上的 Docker 主機，透過命令列介面時，請參閱[toouse hello Azure 命令列介面 (Azure CLI) 從 hello Docker VM 擴充功能的方式]</span><span class="sxs-lookup"><span data-stu-id="062d1-146">If you want tooautomate creating Docker hosts on Azure VMs through command line interface, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)]</span></span>

<!--Anchors-->
[Create a new VM from hello Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add hello Docker VM Extension]:#adddockerextension
[Test Docker Client and Azure Docker Host]:#testclientandserver
[Next steps]:#next-steps

<!--Image references-->
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[6]:./media/markdown-template-for-new-articles/pretty49.png
[7]:./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[toouse hello Azure 命令列介面 (Azure CLI) 從 hello Docker VM 擴充功能的方式]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/
[Azure Linux 代理程式]:../agent-user-guide.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md

[執行 Docker https]:http://docs.docker.com/articles/https/
[Docker 使用者指南]:https://docs.docker.com/userguide/

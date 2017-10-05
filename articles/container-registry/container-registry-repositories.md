---
title: "Azure 容器登錄存放庫 | Microsoft Docs"
description: "如何使用 Docker 映像的 Azure 容器登錄存放庫"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 06b809c31cecef1714f60d04657eb74c611be8cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="fe52c-103">Azure 容器登錄存放庫</span><span class="sxs-lookup"><span data-stu-id="fe52c-103">Azure container registry repositories</span></span>

<span data-ttu-id="fe52c-104">Azure 容器登錄可讓您將容器映像儲存在存放庫中。</span><span class="sxs-lookup"><span data-stu-id="fe52c-104">Azure container registry allows you to store container images in repositories.</span></span> <span data-ttu-id="fe52c-105">透過將映像儲存在存放庫中，您可以在隔離的環境中擁有映像 (或映像的版本) 的群組。</span><span class="sxs-lookup"><span data-stu-id="fe52c-105">By storing images in repositories, you can have groups of images (or version of images) in isolated environments.</span></span> <span data-ttu-id="fe52c-106">當您將映像推送到您的登錄時，可以指定這些存放庫。</span><span class="sxs-lookup"><span data-stu-id="fe52c-106">You can specify these repositories when you push images to your registry.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="fe52c-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="fe52c-107">Prerequisites</span></span>
* <span data-ttu-id="fe52c-108">**Azure 容器登錄庫** - 在 Azure 訂用帳戶中建立容器登錄庫。</span><span class="sxs-lookup"><span data-stu-id="fe52c-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="fe52c-109">例如，使用 [Azure 入口網站](container-registry-get-started-portal.md)或 [Azure CLI 2.0](container-registry-get-started-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="fe52c-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="fe52c-110">**Docker CLI** - 若要將您的本機電腦設定為 Docker 主機並存取 Docker CLI 命令，安裝 [Docker 引擎](https://docs.docker.com/engine/installation/)。</span><span class="sxs-lookup"><span data-stu-id="fe52c-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>
* <span data-ttu-id="fe52c-111">**提取映像** - 從公用 Docker Hub 登錄提取映像、標記映像，並將其推送到您的登錄。</span><span class="sxs-lookup"><span data-stu-id="fe52c-111">**Pull an image** - Pull an image from the public Docker Hub registry, tag it, and push it to your registry.</span></span> <span data-ttu-id="fe52c-112">如需如何推送和提取映像的指示，請參閱[推送 Docker 映像到 Azure 私人登錄](container-registry-get-started-docker-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="fe52c-112">For guidance on how push and pull images, see [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md).</span></span>


## <a name="viewing-repositories-in-the-portal"></a><span data-ttu-id="fe52c-113">在入口網站中檢視存放庫</span><span class="sxs-lookup"><span data-stu-id="fe52c-113">Viewing repositories in the Portal</span></span>

<span data-ttu-id="fe52c-114">一旦您將映像推送到容器登錄，即可在 Azure 入口網站中看到裝載映像的存放庫清單。</span><span class="sxs-lookup"><span data-stu-id="fe52c-114">Once you have pushed images to your container registry, you can see a list of the repositories hosting the images in the Azure portal.</span></span>

<span data-ttu-id="fe52c-115">如果您遵循[推送 Docker 映像到 Azure 私人登錄](container-registry-get-started-docker-cli.md)一文中的步驟，您的容器登錄中現在應該有 Nginx 映像。</span><span class="sxs-lookup"><span data-stu-id="fe52c-115">If you followed the steps in the [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md) article, you should now have a Nginx image in your container registry.</span></span> <span data-ttu-id="fe52c-116">依指示所述，您應該已為該映像指定命名空間。</span><span class="sxs-lookup"><span data-stu-id="fe52c-116">As part of the instructions, you should have specified a namespace for the image.</span></span> <span data-ttu-id="fe52c-117">在下列範例中，命令將 NGinx 映像推送到 "samples" 存放庫︰</span><span class="sxs-lookup"><span data-stu-id="fe52c-117">In the example below, the command pushes the NGinx image to the "samples" repository:</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```
 <span data-ttu-id="fe52c-118">Azure 容器登錄庫支援多層級的儲存機制命名空間。</span><span class="sxs-lookup"><span data-stu-id="fe52c-118">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="fe52c-119">這項功能可讓您將與特定應用程式相關的映像集合為群組，或將特定開發或作業團隊的應用程式集合為群組。</span><span class="sxs-lookup"><span data-stu-id="fe52c-119">This feature enables you to group collections of images related to a specific app, or a collection of apps to specific development or operational teams.</span></span> <span data-ttu-id="fe52c-120">若要深入了解容器登錄中的存放庫，請參閱 [Azure 中的私人 Docker 容器登錄](container-registry-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="fe52c-120">To read more about repositories in container registries, see [Private Docker container registries in Azure](container-registry-intro.md).</span></span>

<span data-ttu-id="fe52c-121">檢視容器登錄存放庫：</span><span class="sxs-lookup"><span data-stu-id="fe52c-121">To view the container registry repositories:</span></span>

1. <span data-ttu-id="fe52c-122">登入 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="fe52c-122">Log in to the Azure portal</span></span>
2. <span data-ttu-id="fe52c-123">在 [Azure 容器登錄 (Azure Container Registry)] 刀鋒視窗中，選取您想要檢查的登錄</span><span class="sxs-lookup"><span data-stu-id="fe52c-123">On the **Azure Container Registry** blade, select the registry you wish to inspect</span></span>
3. <span data-ttu-id="fe52c-124">在登錄刀鋒視窗中，按一下 [儲存機制 (Repositories)] 以查看所有儲存機制和其映像的清單</span><span class="sxs-lookup"><span data-stu-id="fe52c-124">In the registry blade, click **Repositories** to see a list of all the repositories and their images</span></span>
4. <span data-ttu-id="fe52c-125">(選擇性) 選取特定的映像以查看標記</span><span class="sxs-lookup"><span data-stu-id="fe52c-125">(Optional) Select a specific image to see tags</span></span>

![入口網站中的存放庫](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a><span data-ttu-id="fe52c-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fe52c-127">Next steps</span></span>
<span data-ttu-id="fe52c-128">現在您瞭解基本概念了，可以開始使用您的登錄庫！</span><span class="sxs-lookup"><span data-stu-id="fe52c-128">Now that you know the basics, you are ready to start using your registry!</span></span> <span data-ttu-id="fe52c-129">例如，開始將容器映像部署到 [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) 叢集。</span><span class="sxs-lookup"><span data-stu-id="fe52c-129">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>

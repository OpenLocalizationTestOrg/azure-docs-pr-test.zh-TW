---
title: "Azure 容器登錄 aaaAuthenticate |Microsoft 文件"
description: "如何使用 Azure Active Directory tooan Azure 容器登錄中的 toolog 服務主體或系統管理員帳戶"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 128a937a-766a-415b-b9fc-35a6c2f27417
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a0b0462e8432b2567689debca322e2426baa7fa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="ab046-103">向私用 Docker 容器登錄進行驗證</span><span class="sxs-lookup"><span data-stu-id="ab046-103">Authenticate with a private Docker container registry</span></span>
<span data-ttu-id="ab046-104">toowork 與 Azure 容器登錄中的容器映像，您使用登入 hello`docker login`命令。</span><span class="sxs-lookup"><span data-stu-id="ab046-104">toowork with container images in an Azure container registry, you log in using hello `docker login` command.</span></span> <span data-ttu-id="ab046-105">您可以使用 **[Azure Active Directory 服務主體](../active-directory/active-directory-application-objects.md)**或登錄庫特定的**管理帳戶**登入。</span><span class="sxs-lookup"><span data-stu-id="ab046-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span></span> <span data-ttu-id="ab046-106">本文提供關於這些身分識別的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ab046-106">This article provides more detail about these identities.</span></span>



## <a name="service-principal"></a><span data-ttu-id="ab046-107">服務主體</span><span class="sxs-lookup"><span data-stu-id="ab046-107">Service principal</span></span>

<span data-ttu-id="ab046-108">您可以[指派服務主體](container-registry-get-started-azure-cli.md#assign-a-service-principal)tooyour 登錄並使用基本的 Docker 驗證。</span><span class="sxs-lookup"><span data-stu-id="ab046-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour registry and use it for basic Docker authentication.</span></span> <span data-ttu-id="ab046-109">在大部分情況下，建議使用服務主體。</span><span class="sxs-lookup"><span data-stu-id="ab046-109">Using a service principal is recommended for most scenarios.</span></span> <span data-ttu-id="ab046-110">提供 hello 應用程式識別碼和密碼 hello 服務主體 toohello`docker login`命令時，hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="ab046-110">Provide hello app ID and password of hello service principal toohello `docker login` command, as shown in hello following example:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="ab046-111">登入之後，Docker 會快取 hello 認證，因此您不需要 tooremember hello 應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="ab046-111">Once logged in, Docker caches hello credentials, so you don't need tooremember hello app ID.</span></span>

> [!TIP]
> <span data-ttu-id="ab046-112">如果您想，您可以執行重新產生服務主體的 hello 密碼 hello`az ad sp reset-credentials`命令。</span><span class="sxs-lookup"><span data-stu-id="ab046-112">If you want, you can regenerate hello password of a service principal by running hello `az ad sp reset-credentials` command.</span></span>
>


<span data-ttu-id="ab046-113">服務主體允許[角色型存取](../active-directory/role-based-access-control-configure.md)tooa 登錄。</span><span class="sxs-lookup"><span data-stu-id="ab046-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) tooa registry.</span></span> <span data-ttu-id="ab046-114">可用的角色如下：</span><span class="sxs-lookup"><span data-stu-id="ab046-114">Available roles are:</span></span>
  * <span data-ttu-id="ab046-115">讀取者 (僅擁有提取存取權限)。</span><span class="sxs-lookup"><span data-stu-id="ab046-115">Reader (pull only access).</span></span>
  * <span data-ttu-id="ab046-116">投稿人 (提取和推送)。</span><span class="sxs-lookup"><span data-stu-id="ab046-116">Contributor (pull and push).</span></span>
  * <span data-ttu-id="ab046-117">擁有者 （提取、 推送及指派角色 tooother 使用者）。</span><span class="sxs-lookup"><span data-stu-id="ab046-117">Owner (pull, push, and assign roles tooother users).</span></span>

<span data-ttu-id="ab046-118">Azure Container Registry 無法進行匿名存取。</span><span class="sxs-lookup"><span data-stu-id="ab046-118">Anonymous access is not available on Azure Container Registries.</span></span> <span data-ttu-id="ab046-119">您可以使用[Docker 中樞](https://docs.docker.com/docker-hub/)存取公用映像。</span><span class="sxs-lookup"><span data-stu-id="ab046-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

<span data-ttu-id="ab046-120">您可以指派多個服務主體 tooa 登錄中，可讓您 toodefine 不同的使用者或應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="ab046-120">You can assign multiple service principals tooa registry, which allows you toodefine access for different users or applications.</span></span> <span data-ttu-id="ab046-121">服務主體也可讓開發人員或 DevOps 案例，例如 hello 遵循範例中的 「 遠端控制 」 連線 tooa 登錄：</span><span class="sxs-lookup"><span data-stu-id="ab046-121">Service principals also enable "headless" connectivity tooa registry in developer or DevOps scenarios such as hello following examples:</span></span>

  * <span data-ttu-id="ab046-122">容器包括 DC/OS、 Docker Swarm 和 Kubernetes 登錄 tooorchestration 系統的部署。</span><span class="sxs-lookup"><span data-stu-id="ab046-122">Container deployments from a registry tooorchestration systems including DC/OS, Docker Swarm and Kubernetes.</span></span> <span data-ttu-id="ab046-123">您可以也提取容器登錄 toorelated Azure 服務例如[容器服務](../container-service/index.yml)， [App Service](../app-service/index.md)，[批次](../batch/index.md)， [Service Fabric](/azure/service-fabric/)，和其他人。</span><span class="sxs-lookup"><span data-stu-id="ab046-123">You can also pull container registries toorelated Azure services such as [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), and others.</span></span>

  * <span data-ttu-id="ab046-124">連續整合及部署解決方案 （例如 Visual Studio Team Services 或 Jenkins） 會建立容器映像，並將其推送 tooa 登錄。</span><span class="sxs-lookup"><span data-stu-id="ab046-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them tooa registry.</span></span>





## <a name="admin-account"></a><span data-ttu-id="ab046-125">管理帳戶</span><span class="sxs-lookup"><span data-stu-id="ab046-125">Admin account</span></span>
<span data-ttu-id="ab046-126">您建立的每個登錄，都會自動建立一個管理帳戶。</span><span class="sxs-lookup"><span data-stu-id="ab046-126">With each registry you create, an admin account gets created automatically.</span></span> <span data-ttu-id="ab046-127">Hello 帳戶預設為停用，但您可以啟用它，並管理 hello 認證，例如透過 hello[入口網站](container-registry-get-started-portal.md#manage-registry-settings)或使用 hello [Azure CLI 2.0 命令](container-registry-get-started-azure-cli.md#manage-admin-credentials)。</span><span class="sxs-lookup"><span data-stu-id="ab046-127">By default hello account is disabled, but you can enable it and manage hello credentials, for example through hello [portal](container-registry-get-started-portal.md#manage-registry-settings) or using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span></span> <span data-ttu-id="ab046-128">每個管理帳戶會提供兩個可以重新產生的密碼。</span><span class="sxs-lookup"><span data-stu-id="ab046-128">Each admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="ab046-129">hello 兩個密碼可讓您 toomaintain 連線 toohello 登錄使用一個密碼，當您重新產生 hello 其他密碼。</span><span class="sxs-lookup"><span data-stu-id="ab046-129">hello two passwords allow you toomaintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="ab046-130">如果啟用 hello 帳戶時，您可以傳遞 hello 使用者名稱和其中一個密碼 toohello`docker login`命令的基本驗證 toohello 登錄。</span><span class="sxs-lookup"><span data-stu-id="ab046-130">If hello account is enabled, you can pass hello user name and either password toohello `docker login` command for basic authentication toohello registry.</span></span> <span data-ttu-id="ab046-131">例如：</span><span class="sxs-lookup"><span data-stu-id="ab046-131">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> <span data-ttu-id="ab046-132">hello 系統管理員帳戶可供單一使用者 tooaccess hello 登錄，主要是基於測試目的。</span><span class="sxs-lookup"><span data-stu-id="ab046-132">hello admin account is designed for a single user tooaccess hello registry, mainly for test purposes.</span></span> <span data-ttu-id="ab046-133">不建議其他使用者之間 tooshare hello 系統管理員帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="ab046-133">It is not recommended tooshare hello admin account credentials among other users.</span></span> <span data-ttu-id="ab046-134">所有使用者都顯示為單一使用者 toohello 登錄。</span><span class="sxs-lookup"><span data-stu-id="ab046-134">All users appear as a single user toohello registry.</span></span> <span data-ttu-id="ab046-135">變更或停用此帳戶會停用登錄的全部使用者都使用 hello 認證的存取權。</span><span class="sxs-lookup"><span data-stu-id="ab046-135">Changing or disabling this account disables registry access for all users who use hello credentials.</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="ab046-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ab046-136">Next steps</span></span>
* <span data-ttu-id="ab046-137">[推入第一個映像使用 Docker CLI hello](container-registry-get-started-docker-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="ab046-137">[Push your first image using hello Docker CLI](container-registry-get-started-docker-cli.md).</span></span>
* <span data-ttu-id="ab046-138">如需驗證在 hello 容器登錄中預覽的詳細資訊，請參閱 hello[部落格文章](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/)。</span><span class="sxs-lookup"><span data-stu-id="ab046-138">For more information about authentication in hello Container Registry preview, see hello [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span></span>

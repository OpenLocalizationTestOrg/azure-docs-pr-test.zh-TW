---
title: "向 Azure 容器登錄庫驗證 | Microsoft Docs"
description: "如何使用 Azure Active Directory 服務主體或管理員帳戶登入 Azure 容器登錄庫"
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
ms.openlocfilehash: aa2a6bf3d7d9ec22020036851fc0f2bca37e31bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="2b860-103">向私用 Docker 容器登錄進行驗證</span><span class="sxs-lookup"><span data-stu-id="2b860-103">Authenticate with a private Docker container registry</span></span>
<span data-ttu-id="2b860-104">若要使用 Azure 容器登錄庫中的容器映像，請使用 `docker login` 命令登入。</span><span class="sxs-lookup"><span data-stu-id="2b860-104">To work with container images in an Azure container registry, you log in using the `docker login` command.</span></span> <span data-ttu-id="2b860-105">您可以使用 **[Azure Active Directory 服務主體](../active-directory/active-directory-application-objects.md)**或登錄庫特定的**管理帳戶**登入。</span><span class="sxs-lookup"><span data-stu-id="2b860-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span></span> <span data-ttu-id="2b860-106">本文提供關於這些身分識別的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2b860-106">This article provides more detail about these identities.</span></span>



## <a name="service-principal"></a><span data-ttu-id="2b860-107">服務主體</span><span class="sxs-lookup"><span data-stu-id="2b860-107">Service principal</span></span>

<span data-ttu-id="2b860-108">您可以[指派服務主體](container-registry-get-started-azure-cli.md#assign-a-service-principal)到登錄庫，並使用於基本 Docker 驗證。</span><span class="sxs-lookup"><span data-stu-id="2b860-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) to your registry and use it for basic Docker authentication.</span></span> <span data-ttu-id="2b860-109">在大部分情況下，建議使用服務主體。</span><span class="sxs-lookup"><span data-stu-id="2b860-109">Using a service principal is recommended for most scenarios.</span></span> <span data-ttu-id="2b860-110">將服務主體的應用程式識別碼和密碼提供給 `docker login` 命令，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="2b860-110">Provide the app ID and password of the service principal to the `docker login` command, as shown in the following example:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="2b860-111">登入後，Docker 會快取認證，因此您不需要記憶應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="2b860-111">Once logged in, Docker caches the credentials, so you don't need to remember the app ID.</span></span>

> [!TIP]
> <span data-ttu-id="2b860-112">如果您想，您可以執行 `az ad sp reset-credentials` 命令以重新產生服務主體的密碼。</span><span class="sxs-lookup"><span data-stu-id="2b860-112">If you want, you can regenerate the password of a service principal by running the `az ad sp reset-credentials` command.</span></span>
>


<span data-ttu-id="2b860-113">服務主體允許登錄庫的[角色型存取](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="2b860-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) to a registry.</span></span> <span data-ttu-id="2b860-114">可用的角色如下：</span><span class="sxs-lookup"><span data-stu-id="2b860-114">Available roles are:</span></span>
  * <span data-ttu-id="2b860-115">讀取者 (僅擁有提取存取權限)。</span><span class="sxs-lookup"><span data-stu-id="2b860-115">Reader (pull only access).</span></span>
  * <span data-ttu-id="2b860-116">投稿人 (提取和推送)。</span><span class="sxs-lookup"><span data-stu-id="2b860-116">Contributor (pull and push).</span></span>
  * <span data-ttu-id="2b860-117">擁有者 (提取、推送及並指派角色給其他使用者)。</span><span class="sxs-lookup"><span data-stu-id="2b860-117">Owner (pull, push, and assign roles to other users).</span></span>

<span data-ttu-id="2b860-118">Azure Container Registry 無法進行匿名存取。</span><span class="sxs-lookup"><span data-stu-id="2b860-118">Anonymous access is not available on Azure Container Registries.</span></span> <span data-ttu-id="2b860-119">您可以使用[Docker 中樞](https://docs.docker.com/docker-hub/)存取公用映像。</span><span class="sxs-lookup"><span data-stu-id="2b860-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

<span data-ttu-id="2b860-120">您可以指派多個服務主體到登錄庫，就能為不同的使用者或應用程式定義存取權。</span><span class="sxs-lookup"><span data-stu-id="2b860-120">You can assign multiple service principals to a registry, which allows you to define access for different users or applications.</span></span> <span data-ttu-id="2b860-121">在如下的開發人員或 DevOps 案例中，服務主體也會啟用與登錄庫的「無周邊」連線：</span><span class="sxs-lookup"><span data-stu-id="2b860-121">Service principals also enable "headless" connectivity to a registry in developer or DevOps scenarios such as the following examples:</span></span>

  * <span data-ttu-id="2b860-122">從登錄庫到協調流程系統的容器部署，包括 DC/OS、Docker Swarm 和 Kubernetes。</span><span class="sxs-lookup"><span data-stu-id="2b860-122">Container deployments from a registry to orchestration systems including DC/OS, Docker Swarm and Kubernetes.</span></span> <span data-ttu-id="2b860-123">您也可以將容器登錄庫提取到相關的 Azure 服務 (例如 [Container Service](../container-service/index.yml)、[App Service](../app-service/index.md)、[Batch](../batch/index.md) 及 [Service Fabric](/azure/service-fabric/) 等)。</span><span class="sxs-lookup"><span data-stu-id="2b860-123">You can also pull container registries to related Azure services such as [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), and others.</span></span>

  * <span data-ttu-id="2b860-124">建立容器映像，並將其推送到登錄庫的連續整合和部署解決方案 (例如 Visual Studio Team Services 或 Jenkins)。</span><span class="sxs-lookup"><span data-stu-id="2b860-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them to a registry.</span></span>





## <a name="admin-account"></a><span data-ttu-id="2b860-125">管理帳戶</span><span class="sxs-lookup"><span data-stu-id="2b860-125">Admin account</span></span>
<span data-ttu-id="2b860-126">您建立的每個登錄，都會自動建立一個管理帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b860-126">With each registry you create, an admin account gets created automatically.</span></span> <span data-ttu-id="2b860-127">此帳戶預設為停用，但您可以啟用它以管理認證，例如透過[入口網站](container-registry-get-started-portal.md#manage-registry-settings)或使用 [Azure CLI 2.0 命令](container-registry-get-started-azure-cli.md#manage-admin-credentials)。</span><span class="sxs-lookup"><span data-stu-id="2b860-127">By default the account is disabled, but you can enable it and manage the credentials, for example through the [portal](container-registry-get-started-portal.md#manage-registry-settings) or using the [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span></span> <span data-ttu-id="2b860-128">每個管理帳戶會提供兩個可以重新產生的密碼。</span><span class="sxs-lookup"><span data-stu-id="2b860-128">Each admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="2b860-129">這兩個密碼讓您在重新產生其他密碼時，可以使用其中一個密碼來維持對登錄的連線。</span><span class="sxs-lookup"><span data-stu-id="2b860-129">The two passwords allow you to maintain connections to the registry by using one password while you regenerate the other password.</span></span> <span data-ttu-id="2b860-130">如果已啟用此帳戶，您可以傳送使用者名稱和密碼到 `docker login` 命令，向登錄庫進行基本驗證。</span><span class="sxs-lookup"><span data-stu-id="2b860-130">If the account is enabled, you can pass the user name and either password to the `docker login` command for basic authentication to the registry.</span></span> <span data-ttu-id="2b860-131">例如：</span><span class="sxs-lookup"><span data-stu-id="2b860-131">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> <span data-ttu-id="2b860-132">管理帳戶是專為單一使用者存取登錄庫而設計，主要用於測試。</span><span class="sxs-lookup"><span data-stu-id="2b860-132">The admin account is designed for a single user to access the registry, mainly for test purposes.</span></span> <span data-ttu-id="2b860-133">不建議和其他使用者共用管理帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="2b860-133">It is not recommended to share the admin account credentials among other users.</span></span> <span data-ttu-id="2b860-134">對登錄庫而言，所有使用者都會顯示為單一使用者。</span><span class="sxs-lookup"><span data-stu-id="2b860-134">All users appear as a single user to the registry.</span></span> <span data-ttu-id="2b860-135">變更或停用此帳戶，會停用使用該認證之所有使用者的登錄庫存取權。</span><span class="sxs-lookup"><span data-stu-id="2b860-135">Changing or disabling this account disables registry access for all users who use the credentials.</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="2b860-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2b860-136">Next steps</span></span>
* <span data-ttu-id="2b860-137">[使用 Docker CLI 推送您的第一個映像](container-registry-get-started-docker-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="2b860-137">[Push your first image using the Docker CLI](container-registry-get-started-docker-cli.md).</span></span>
* <span data-ttu-id="2b860-138">如需容器登錄庫預覽中的驗證詳細資訊，請參閱[部落格文章](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/)。</span><span class="sxs-lookup"><span data-stu-id="2b860-138">For more information about authentication in the Container Registry preview, see the [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span></span>

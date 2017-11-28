---
title: "aaaCreate 的私用 Docker 登錄-而 Azure 入口網站 |Microsoft 文件"
description: "開始建立及管理私人 Docker 容器登錄以 hello Azure 入口網站"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40f3ce44fea26e5fbeca865c9da6df55c2df9511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-portal"></a><span data-ttu-id="ca3bd-103">建立私用 Docker 容器登錄中使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ca3bd-103">Create a private Docker container registry using hello Azure portal</span></span>
<span data-ttu-id="ca3bd-104">使用 Azure 入口網站 toocreate 容器登錄中的 hello 和管理其設定。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-104">Use hello Azure portal toocreate a container registry and manage its settings.</span></span> <span data-ttu-id="ca3bd-105">您也可以建立及管理使用 hello 容器登錄[Azure CLI 2.0 命令](container-registry-get-started-azure-cli.md)， [Azure PowerShell](container-registry-get-started-powershell.md)或以程式設計方式使用容器登錄中的 hello [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="ca3bd-105">You can also create and manage container registries using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>

<span data-ttu-id="ca3bd-106">背景和概念，請參閱[hello 概觀](container-registry-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-106">For background and concepts, see [hello overview](container-registry-intro.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="ca3bd-107">建立容器登錄庫</span><span class="sxs-lookup"><span data-stu-id="ca3bd-107">Create a container registry</span></span>
1. <span data-ttu-id="ca3bd-108">在 hello [Azure 入口網站](https://portal.azure.com)，按一下  **+ 新增**。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-108">In hello [Azure portal](https://portal.azure.com), click **+ New**.</span></span>
2. <span data-ttu-id="ca3bd-109">搜尋 hello marketplace 中的**Azure 容器登錄**。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-109">Search hello marketplace for **Azure container registry**.</span></span>
3. <span data-ttu-id="ca3bd-110">選取 [Azure 容器登錄]，其發佈者為 **Microsoft**。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-110">Select **Azure Container Registry**, with publisher **Microsoft**.</span></span>
    <span data-ttu-id="ca3bd-111">![Azure Marketplace 中的容器登錄庫服務](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span><span class="sxs-lookup"><span data-stu-id="ca3bd-111">![Container Registry service in Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)</span></span>
4. <span data-ttu-id="ca3bd-112">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-112">Click **Create**.</span></span> <span data-ttu-id="ca3bd-113">hello **Azure 容器登錄中**刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-113">hello **Azure Container Registry** blade appears.</span></span>

    ![容器登錄庫設定](./media/container-registry-get-started-portal/container-registry-settings.png)
5. <span data-ttu-id="ca3bd-115">在 hello **Azure 容器登錄中**刀鋒視窗中，輸入下列資訊的 hello。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-115">In hello **Azure Container Registry** blade, enter hello following information.</span></span> <span data-ttu-id="ca3bd-116">完成後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-116">Click **Create** when you are done.</span></span>

    <span data-ttu-id="ca3bd-117">a.</span><span class="sxs-lookup"><span data-stu-id="ca3bd-117">a.</span></span> <span data-ttu-id="ca3bd-118">**登錄名稱**：指定登錄的全域唯一最上層網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-118">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="ca3bd-119">在此範例中，是 hello 登錄名稱*myRegistry01*，但以取代您自己的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-119">In this example, hello registry name is *myRegistry01*, but substitute a unique name of your own.</span></span> <span data-ttu-id="ca3bd-120">hello 名稱只能包含字母和數字。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-120">hello name can contain only letters and numbers.</span></span>

    <span data-ttu-id="ca3bd-121">b.</span><span class="sxs-lookup"><span data-stu-id="ca3bd-121">b.</span></span> <span data-ttu-id="ca3bd-122">**資源群組**： 選取現有[資源群組](../azure-resource-manager/resource-group-overview.md#resource-groups)或新的型別 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-122">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span>

    <span data-ttu-id="ca3bd-123">c.</span><span class="sxs-lookup"><span data-stu-id="ca3bd-123">c.</span></span> <span data-ttu-id="ca3bd-124">**位置**： 選取 hello 服務所在的 Azure 資料中心位置[可用](https://azure.microsoft.com/regions/services/)，例如**美國中南部**。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-124">**Location**: Select an Azure datacenter location where hello service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="ca3bd-125">d.</span><span class="sxs-lookup"><span data-stu-id="ca3bd-125">d.</span></span> <span data-ttu-id="ca3bd-126">**系統管理使用者**： 如果您想，讓系統管理員使用者 tooaccess hello 登錄。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-126">**Admin user**: If you want, enable an admin user tooaccess hello registry.</span></span> <span data-ttu-id="ca3bd-127">您可以變更此設定建立 hello 登錄之後。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-127">You can change this setting after creating hello registry.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="ca3bd-128">此外 tooproviding 存取透過系統管理使用者帳戶、 容器登錄支援 Azure Active Directory 服務主體所支援的驗證。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-128">In addition tooproviding access through an admin user account, container registries support authentication backed by Azure Active Directory service principals.</span></span> <span data-ttu-id="ca3bd-129">如需詳細資訊和考量事項，請參閱[驗證容器登錄庫](container-registry-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-129">For more information and considerations, see [Authenticate with a container registry](container-registry-authentication.md).</span></span>
      >

    <span data-ttu-id="ca3bd-130">e.</span><span class="sxs-lookup"><span data-stu-id="ca3bd-130">e.</span></span> <span data-ttu-id="ca3bd-131">**儲存體帳戶**： 使用 hello 預設設定 toocreate[儲存體帳戶](../storage/common/storage-introduction.md)，或在 hello 中選取現有的儲存體帳戶相同的位置。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-131">**Storage account**: Use hello default setting toocreate a [storage account](../storage/common/storage-introduction.md), or select an existing storage account in hello same location.</span></span> <span data-ttu-id="ca3bd-132">目前不支援進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-132">Currently Premium Storage is not supported.</span></span>

## <a name="manage-registry-settings"></a><span data-ttu-id="ca3bd-133">管理登錄庫設定</span><span class="sxs-lookup"><span data-stu-id="ca3bd-133">Manage registry settings</span></span>
<span data-ttu-id="ca3bd-134">在建立之後 hello 登錄，尋找 hello 登錄設定開始 hello**容器登錄**hello 入口網站中的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-134">After creating hello registry, find hello registry settings by starting at hello **Container Registries** blade in hello portal.</span></span> <span data-ttu-id="ca3bd-135">例如，您可能需要 tooyour 登錄中的 hello 設定 toolog 或您可能會想 tooenable 或是停用 hello 系統管理使用者。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-135">For example, you might need hello settings toolog in tooyour registry, or you might want tooenable or disable hello admin user.</span></span>

1. <span data-ttu-id="ca3bd-136">在 hello**容器登錄**刀鋒視窗中，按一下您的登錄 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-136">On hello **Container Registries** blade, click hello name of your registry.</span></span>

    ![容器登錄庫刀鋒視窗](./media/container-registry-get-started-portal/container-registry-blade.png)
2. <span data-ttu-id="ca3bd-138">toomanage 存取設定，請按一下**便捷鍵**。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-138">toomanage access settings, click **Access key**.</span></span>

    ![容器登錄庫的存取權](./media/container-registry-get-started-portal/container-registry-access.png)
3. <span data-ttu-id="ca3bd-140">請注意下列設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="ca3bd-140">Note hello following settings:</span></span>

   * <span data-ttu-id="ca3bd-141">**登入伺服器**-您可以使用 toolog toohello 登錄中的 hello 完整限定的名稱。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-141">**Login server** - hello fully qualified name you use toolog in toohello registry.</span></span> <span data-ttu-id="ca3bd-142">在此範例中為 `myregistry01.azurecr.io`。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-142">In this example, it is `myregistry01.azurecr.io`.</span></span>
   * <span data-ttu-id="ca3bd-143">**系統管理使用者**-切換 tooenable 或停用 hello 登錄系統管理使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-143">**Admin user** - Toggle tooenable or disable hello registry's admin user account.</span></span>
   * <span data-ttu-id="ca3bd-144">**使用者名稱**和**密碼**-hello hello 系統管理員使用者帳戶的認證 （如果啟用） 您可以使用 toolog toohello 登錄中。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-144">**Username** and **Password** - hello credentials of hello admin user account (if enabled) you can use toolog in toohello registry.</span></span> <span data-ttu-id="ca3bd-145">您可以選擇性地重新產生 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-145">You can optionally regenerate hello passwords.</span></span> <span data-ttu-id="ca3bd-146">如此您就可以維護連接 toohello 登錄使用一組密碼，當您重新產生 hello 其他密碼，會建立兩個密碼。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-146">Two passwords are created so that you can maintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="ca3bd-147">相反地，請參閱與服務主體 tooauthenticate[與私用 Docker 容器登錄中的 Authenticate](container-registry-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="ca3bd-147">tooauthenticate with a service principal instead, see [Authenticate with a private Docker container registry](container-registry-authentication.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca3bd-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ca3bd-148">Next steps</span></span>
* [<span data-ttu-id="ca3bd-149">推入第一個映像使用 Docker CLI hello</span><span class="sxs-lookup"><span data-stu-id="ca3bd-149">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)

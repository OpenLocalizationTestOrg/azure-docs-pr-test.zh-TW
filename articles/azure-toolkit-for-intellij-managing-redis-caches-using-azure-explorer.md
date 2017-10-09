---
title: "IntelliJ aaaManaging Redis 快取使用 hello Azure 總管 |Microsoft 文件"
description: "了解如何 toomanage 您的 Azure redis 快取使用 IntelliJ hello Azure 總管。"
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
ms.date: 06/14/2017
ms.author: robmcm
ms.openlocfilehash: 76ba37a2a35c26d0045e17003181108992eb957d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-redis-caches-using-hello-azure-explorer-for-intellij"></a><span data-ttu-id="07673-103">管理用於 IntelliJ hello Azure 總管的 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="07673-103">Managing Redis Caches using hello Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="07673-104">hello Azure 總管 中，這是 hello Azure Toolkit for IntelliJ 的一部分，提供方便使用解決方案的 Java 開發人員管理 redis 快取內從其 Azure 帳戶中的 hello IntelliJ IDE。</span><span class="sxs-lookup"><span data-stu-id="07673-104">hello Azure Explorer, which is part of hello Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing redis caches in their Azure account from inside hello IntelliJ IDE.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-intellij"></a><span data-ttu-id="07673-105">使用 IntelliJ 建立 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="07673-105">Create a Redis Cache by using IntelliJ</span></span>

<span data-ttu-id="07673-106">hello 步驟引導您完成 hello 步驟 toocreate 使用 hello Azure 總管的 redis 快取。</span><span class="sxs-lookup"><span data-stu-id="07673-106">hello following steps walk you through hello steps toocreate a redis cache using hello Azure Explorer.</span></span>

1. <span data-ttu-id="07673-107">使用中 hello hello 步驟的 Azure 帳戶登入 tooyour[符號中的 hello Azure Toolkit for IntelliJ 指示]發行項。</span><span class="sxs-lookup"><span data-stu-id="07673-107">Sign in tooyour Azure account using hello steps in hello [Sign In Instructions for hello Azure Toolkit for IntelliJ] article.</span></span>

1. <span data-ttu-id="07673-108">在 hello **Azure 總管**工具視窗中，展開 hello **Azure**  節點，以滑鼠右鍵按一下**Redis 快取**，然後按一下**建立 Redis 快取**。</span><span class="sxs-lookup"><span data-stu-id="07673-108">In hello **Azure Explorer** tool window, expand hello **Azure** node, right-click **Redis Caches**, and then click **Create Redis Cache**.</span></span>

   ![建立 Redis 快取功能表][CR01]

1. <span data-ttu-id="07673-110">當 hello**新增 Redis 快取**出現對話方塊，請指定下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="07673-110">When hello **New Redis Cache** dialog box appears, specify hello following options:</span></span>

   ![建立新的 Redis 快取對話方塊][CR02]

   <span data-ttu-id="07673-112">a.</span><span class="sxs-lookup"><span data-stu-id="07673-112">a.</span></span> <span data-ttu-id="07673-113">**DNS 名稱**： 指定 hello 新 redis 快取，前面加上太 hello DNS 子網域 」。 redis.cache.windows.net"; 例如： *wingtiptoys.redis.cache.windows.net*。</span><span class="sxs-lookup"><span data-stu-id="07673-113">**DNS Name**: Specifies hello DNS subdomain for hello new redis cache, which are prepended too".redis.cache.windows.net"; for example: *wingtiptoys.redis.cache.windows.net*.</span></span>

   <span data-ttu-id="07673-114">b.</span><span class="sxs-lookup"><span data-stu-id="07673-114">b.</span></span> <span data-ttu-id="07673-115">**訂用帳戶**： 指定 hello 想 toouse hello 新 redis 快取的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="07673-115">**Subscription**: Specifies hello Azure subscription you want toouse for hello new redis cache.</span></span>

   <span data-ttu-id="07673-116">c.</span><span class="sxs-lookup"><span data-stu-id="07673-116">c.</span></span> <span data-ttu-id="07673-117">**資源群組**： 指定 hello redis 快取的資源群組，您需要的下列選項的 hello toochoose 其中一個：</span><span class="sxs-lookup"><span data-stu-id="07673-117">**Resource Group**: Specifies hello resource group for your redis cache; you need toochoose one of hello following options:</span></span>
      * <span data-ttu-id="07673-118">**建立新**： 指定您想 toocreate 新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="07673-118">**Create New**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="07673-119">**使用現有**︰指定您將從與您 Azure 帳戶相關聯的資源群組清單中進行選擇。</span><span class="sxs-lookup"><span data-stu-id="07673-119">**Use Existing**: Specifies that you will choose from a list of resource groups associated with your Azure account.</span></span>

   <span data-ttu-id="07673-120">d.</span><span class="sxs-lookup"><span data-stu-id="07673-120">d.</span></span> <span data-ttu-id="07673-121">**位置**： 指定 hello 位置建立 redis 快取的位置; 例如，*美國西部*。</span><span class="sxs-lookup"><span data-stu-id="07673-121">**Location**: Specifies hello location where your redis cache is created; for example, *West US*.</span></span>

   <span data-ttu-id="07673-122">e.</span><span class="sxs-lookup"><span data-stu-id="07673-122">e.</span></span> <span data-ttu-id="07673-123">**定價層**： 指定您的 redis 快取會使用哪一個定價層，此設定會決定用戶端連線的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="07673-123">**Pricing Tier**: Specifies which pricing tier your redis cache uses; this setting determines hello number of client connections.</span></span> <span data-ttu-id="07673-124">(如需詳細資訊，請參閱 [Redis 快取定價]。)</span><span class="sxs-lookup"><span data-stu-id="07673-124">(For more information, see [Redis Cache Pricing].)</span></span>

   <span data-ttu-id="07673-125">f.</span><span class="sxs-lookup"><span data-stu-id="07673-125">f.</span></span> <span data-ttu-id="07673-126">**非 SSL 連接埠**：指定 Redis 快取是否可允許非 SSL 連線；預設只允許 SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="07673-126">**Non-SSL port**: Specifies whether your redis cache allows non-SSL connections; by default, only SSL connections are allowed.</span></span>

1. <span data-ttu-id="07673-127">指定所有的 Redis 快取設定後，請按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="07673-127">When you have specified all your redis cache settings, click **OK**.</span></span>

<span data-ttu-id="07673-128">建立 redis 快取之後，它就會顯示在 hello Azure 總管。</span><span class="sxs-lookup"><span data-stu-id="07673-128">After your redis cache has been created, it will be displayed in hello Azure Explorer.</span></span>

   ![Azure Explorer 中的 Redis 快取][CR03]

> [!NOTE]
>
> <span data-ttu-id="07673-130">如需有關設定您的 Azure redis 快取設定，請參閱[如何 tooconfigure Azure Redis 快取]。</span><span class="sxs-lookup"><span data-stu-id="07673-130">For more information about configuring your Azure redis cache settings, see [How tooconfigure Azure Redis Cache].</span></span>
>

## <a name="display-hello-properties-for-your-redis-cache-in-intellij"></a><span data-ttu-id="07673-131">Redis 快取中 IntelliJ 顯示 hello 屬性</span><span class="sxs-lookup"><span data-stu-id="07673-131">Display hello properties for your Redis Cache in IntelliJ</span></span>

1. <span data-ttu-id="07673-132">在 hello Azure 總管，以滑鼠右鍵按一下您的 redis 快取，按一下 **顯示屬性**。</span><span class="sxs-lookup"><span data-stu-id="07673-132">In hello Azure Explorer, right-click your redis cache and click **Show properties**.</span></span>

   ![Azure 總管內容功能表 toodisplay 屬性 redis 快取][SP01]

1. <span data-ttu-id="07673-134">hello Azure 總管會顯示 hello redis 快取的屬性。</span><span class="sxs-lookup"><span data-stu-id="07673-134">hello Azure Explorer displays hello properties for your redis cache.</span></span>

   ![Redis 快取屬性][SP02]

## <a name="delete-your-redis-cache-by-using-intellij"></a><span data-ttu-id="07673-136">使用 IntelliJ 刪除 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="07673-136">Delete your Redis Cache by using IntelliJ</span></span>

1. <span data-ttu-id="07673-137">在 hello Azure 總管，以滑鼠右鍵按一下您的 redis 快取，按一下 **刪除**。</span><span class="sxs-lookup"><span data-stu-id="07673-137">In hello Azure Explorer, right-click your redis cache and click **Delete**.</span></span>

   ![Azure 總管內容功能表 toodelete redis 快取][DE01]

1. <span data-ttu-id="07673-139">按一下**是**時提示 toodelete redis 快取。</span><span class="sxs-lookup"><span data-stu-id="07673-139">Click **Yes** when prompted toodelete your redis cache.</span></span>

   ![刪除 Redis 快取提示][DE02]

## <a name="next-steps"></a><span data-ttu-id="07673-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="07673-141">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="07673-142">如需 Azure redis 快取、 組態設定和定價的詳細資訊，請參閱下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="07673-142">For more information about Azure redis caches, configuration settings and pricing, see hello following links:</span></span>

* <span data-ttu-id="07673-143">[Azure Redis 快取]</span><span class="sxs-lookup"><span data-stu-id="07673-143">[Azure Redis Cache]</span></span>
* <span data-ttu-id="07673-144">[Redis 快取文件]</span><span class="sxs-lookup"><span data-stu-id="07673-144">[Redis Cache Documentation]</span></span>
* <span data-ttu-id="07673-145">[Redis 快取定價]</span><span class="sxs-lookup"><span data-stu-id="07673-145">[Redis Cache Pricing]</span></span>
* <span data-ttu-id="07673-146">[如何 tooconfigure Azure Redis 快取]</span><span class="sxs-lookup"><span data-stu-id="07673-146">[How tooconfigure Azure Redis Cache]</span></span>

<!-- URL List -->

[Redis 快取定價]: https://azure.microsoft.com/pricing/details/cache/
[Azure Redis 快取]: https://azure.microsoft.com/services/cache/
[Redis 快取文件]: ./redis-cache/index.md
[如何 tooconfigure Azure Redis 快取]: ./redis-cache/cache-configure.md
[符號中的 hello Azure Toolkit for IntelliJ 指示]: ./azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE02.png

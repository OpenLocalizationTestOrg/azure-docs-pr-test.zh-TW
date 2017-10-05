---
title: "更新 Azure RemoteApp 服務 | Microsoft Docs"
description: "了解如何更新 Azure RemoteApp 收藏"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 454d78445d6092aec9eaa383e4c50cf15195848c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a><span data-ttu-id="121ac-103">更新 Azure RemoteApp 中的收藏</span><span class="sxs-lookup"><span data-stu-id="121ac-103">Update a collection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="121ac-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="121ac-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="121ac-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="121ac-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="121ac-106">無可避免地，總會有一次，您需要更新 Azure RemoteApp 收藏中的應用程式或映像。</span><span class="sxs-lookup"><span data-stu-id="121ac-106">There will come a time, inevitably, when you need to update the apps or image in your Azure RemoteApp collection.</span></span> <span data-ttu-id="121ac-107">如果您是使用 Azure RemoteApp 訂用帳戶隨附的其中一個映像，則在雲端或混合式收藏中，任何和所有的更新都是由 Azure RemoteApp 本身處理，因此您可以放手不管。</span><span class="sxs-lookup"><span data-stu-id="121ac-107">If you are using one of the images included with your Azure RemoteApp subscription, in either a cloud or hybrid collection, any and all updates are handled by Azure RemoteApp itself, so you can rest easy.</span></span>

<span data-ttu-id="121ac-108">不過，如果您是使用自訂映像 (從頭建立的映像，或是修改其中一個我們的映像所建立的映像)，則您需負責維護映像和應用程式。</span><span class="sxs-lookup"><span data-stu-id="121ac-108">However, if you are using a custom image (either that you built from scratch or that you created by modifying one of our images), you are in charge of maintaining the image and apps.</span></span> <span data-ttu-id="121ac-109">如果您需要更新映像或其內的任何應用程式，則需要建立映像的新的已更新版本，然後使用這個新的已更新映像取代集合中的現有映像。</span><span class="sxs-lookup"><span data-stu-id="121ac-109">If you need to update your image or any of the apps inside it, you need to create a new, updated version of the image, and then replace the existing image in your collection with this new updated image.</span></span>

<span data-ttu-id="121ac-110">因此，您該如何更新您的收藏？</span><span class="sxs-lookup"><span data-stu-id="121ac-110">So, how do you go about updating your collection?</span></span> <span data-ttu-id="121ac-111">相當簡單：</span><span class="sxs-lookup"><span data-stu-id="121ac-111">It's fairly straightforward:</span></span>

1. <span data-ttu-id="121ac-112">更新您在收藏中使用的映像。</span><span class="sxs-lookup"><span data-stu-id="121ac-112">Update the image that you used in your collection.</span></span> <span data-ttu-id="121ac-113">套用所需的任何修補程式或更新，然後將它儲存成新的名稱。</span><span class="sxs-lookup"><span data-stu-id="121ac-113">Apply any patches or updates needed, and then save it with a new name.</span></span>
2. <span data-ttu-id="121ac-114">將該映像[上傳](remoteapp-uploadimage.md)或[匯入](remoteapp-image-on-azurevm.md)至 RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="121ac-114">[Upload](remoteapp-uploadimage.md) or [import](remoteapp-image-on-azurevm.md) that image to RemoteApp.</span></span>
3. <span data-ttu-id="121ac-115">現在，在 [收藏] 頁面上，按一下 [ **更新**]。</span><span class="sxs-lookup"><span data-stu-id="121ac-115">Now, on the collection page, click **Update**.</span></span>
4. <span data-ttu-id="121ac-116">從 [ **範本映像** ] 清單中選擇新的映像。</span><span class="sxs-lookup"><span data-stu-id="121ac-116">Choose the new image from the **Template Image** list.</span></span>
5. <span data-ttu-id="121ac-117">以下是麻煩的部分 - 您必須決定如何處理任何目前正在使用收藏中應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="121ac-117">Here's the tricky part - you need to decide how to deal with any users that are currently using an app in the collection.</span></span> <span data-ttu-id="121ac-118">您有下列選擇：</span><span class="sxs-lookup"><span data-stu-id="121ac-118">You have the following choices:</span></span>
   
   * <span data-ttu-id="121ac-119">**更新後給與使用者 60 分鐘**。</span><span class="sxs-lookup"><span data-stu-id="121ac-119">**Give users 60 minutes after the update**.</span></span> <span data-ttu-id="121ac-120">一完成更新，Azure RemoteApp 就會顯示訊息給任何作用中使用者，告訴他們儲存工作並登出，然後重新登入。</span><span class="sxs-lookup"><span data-stu-id="121ac-120">As soon as the update is finished, Azure RemoteApp will display a message to any active users telling them to save their work and log off and log back in.</span></span> <span data-ttu-id="121ac-121">60 分鐘之後，任何未登出的作用中使用者將自動登出。</span><span class="sxs-lookup"><span data-stu-id="121ac-121">After 60 minutes, any active users who have not logged off will be automatically logged off.</span></span> <span data-ttu-id="121ac-122">使用者可以立即重新登入。</span><span class="sxs-lookup"><span data-stu-id="121ac-122">Users can immediately log back on.</span></span>
   * <span data-ttu-id="121ac-123">**立即登出使用者**。</span><span class="sxs-lookup"><span data-stu-id="121ac-123">**Sign users out immediately**.</span></span> <span data-ttu-id="121ac-124">一完成更新，就會自動登出所有使用者，而且沒有任何警告。</span><span class="sxs-lookup"><span data-stu-id="121ac-124">As soon as the update is finished, log off all users automatically without any warning.</span></span> <span data-ttu-id="121ac-125">如果您選擇此選項，使用者可能會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="121ac-125">If you choose this option, users might lose data.</span></span> <span data-ttu-id="121ac-126">不過，它們可以立即重新連接至應用程式。</span><span class="sxs-lookup"><span data-stu-id="121ac-126">However, they can reconnect to the app immediately.</span></span>
6. <span data-ttu-id="121ac-127">按一下核取記號以啟動更新。</span><span class="sxs-lookup"><span data-stu-id="121ac-127">Click the check mark to start the update.</span></span>


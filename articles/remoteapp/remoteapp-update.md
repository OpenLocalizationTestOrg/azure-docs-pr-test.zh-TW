---
title: "aaaUpdate 您 Azure RemoteApp 集合 |Microsoft 文件"
description: "深入了解如何 tooupdate 您 Azure RemoteApp 集合"
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
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a><span data-ttu-id="f8b5d-103">更新 Azure RemoteApp 中的收藏</span><span class="sxs-lookup"><span data-stu-id="f8b5d-103">Update a collection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f8b5d-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f8b5d-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f8b5d-106">會有時間，無可避免地，當您需要 tooupdate hello 應用程式或映像在您的 Azure RemoteApp 集合。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-106">There will come a time, inevitably, when you need tooupdate hello apps or image in your Azure RemoteApp collection.</span></span> <span data-ttu-id="f8b5d-107">如果您使用其中一個包含與您 Azure RemoteApp 訂用帳戶的雲端或混合式集合中的 hello 映像所有更新是由 Azure RemoteApp 本身，都處理，因此您可以輕鬆將。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-107">If you are using one of hello images included with your Azure RemoteApp subscription, in either a cloud or hybrid collection, any and all updates are handled by Azure RemoteApp itself, so you can rest easy.</span></span>

<span data-ttu-id="f8b5d-108">不過，如果您使用自訂映像 （內建從頭或您所建立的修改其中一個我們映像），您必須負責維護 hello 映像和應用程式。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-108">However, if you are using a custom image (either that you built from scratch or that you created by modifying one of our images), you are in charge of maintaining hello image and apps.</span></span> <span data-ttu-id="f8b5d-109">如果您的映像，或任何的內文中的 hello 應用程式，您會需要 tooupdate，您需要 toocreate hello 映像，然後按一下 取代 hello 現有映像的新更新版本的新更新映像集合中。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-109">If you need tooupdate your image or any of hello apps inside it, you need toocreate a new, updated version of hello image, and then replace hello existing image in your collection with this new updated image.</span></span>

<span data-ttu-id="f8b5d-110">因此，您該如何更新您的收藏？</span><span class="sxs-lookup"><span data-stu-id="f8b5d-110">So, how do you go about updating your collection?</span></span> <span data-ttu-id="f8b5d-111">相當簡單：</span><span class="sxs-lookup"><span data-stu-id="f8b5d-111">It's fairly straightforward:</span></span>

1. <span data-ttu-id="f8b5d-112">更新您使用您的集合中的 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-112">Update hello image that you used in your collection.</span></span> <span data-ttu-id="f8b5d-113">套用所需的任何修補程式或更新，然後將它儲存成新的名稱。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-113">Apply any patches or updates needed, and then save it with a new name.</span></span>
2. <span data-ttu-id="f8b5d-114">[上傳](remoteapp-uploadimage.md)或[匯入](remoteapp-image-on-azurevm.md)該映像 tooRemoteApp。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-114">[Upload](remoteapp-uploadimage.md) or [import](remoteapp-image-on-azurevm.md) that image tooRemoteApp.</span></span>
3. <span data-ttu-id="f8b5d-115">現在，在 hello 集合頁面上，按一下**更新**。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-115">Now, on hello collection page, click **Update**.</span></span>
4. <span data-ttu-id="f8b5d-116">選擇 hello 新映像從 hello**範本映像**清單。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-116">Choose hello new image from hello **Template Image** list.</span></span>
5. <span data-ttu-id="f8b5d-117">以下是 hello 麻煩的部分-您需要如何 toodecide toodeal 與 hello 集合中目前正在使用應用程式的任何使用者。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-117">Here's hello tricky part - you need toodecide how toodeal with any users that are currently using an app in hello collection.</span></span> <span data-ttu-id="f8b5d-118">您有下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="f8b5d-118">You have hello following choices:</span></span>
   
   * <span data-ttu-id="f8b5d-119">**提供 hello 更新後的 60 分鐘給使用者**。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-119">**Give users 60 minutes after hello update**.</span></span> <span data-ttu-id="f8b5d-120">Hello 更新完成，因為 Azure RemoteApp 會顯示訊息 tooany 作用中的使用者告知的 toosave 其工作和記錄檔關閉並重新登入。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-120">As soon as hello update is finished, Azure RemoteApp will display a message tooany active users telling them toosave their work and log off and log back in.</span></span> <span data-ttu-id="f8b5d-121">60 分鐘之後，任何未登出的作用中使用者將自動登出。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-121">After 60 minutes, any active users who have not logged off will be automatically logged off.</span></span> <span data-ttu-id="f8b5d-122">使用者可以立即重新登入。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-122">Users can immediately log back on.</span></span>
   * <span data-ttu-id="f8b5d-123">**立即登出使用者**。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-123">**Sign users out immediately**.</span></span> <span data-ttu-id="f8b5d-124">Hello 更新完成，如登出所有使用者自動而不發出警告。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-124">As soon as hello update is finished, log off all users automatically without any warning.</span></span> <span data-ttu-id="f8b5d-125">如果您選擇此選項，使用者可能會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-125">If you choose this option, users might lose data.</span></span> <span data-ttu-id="f8b5d-126">不過，它們可以重新連線 toohello 應用程式立即。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-126">However, they can reconnect toohello app immediately.</span></span>
6. <span data-ttu-id="f8b5d-127">按一下 hello 核取記號 toostart hello 更新。</span><span class="sxs-lookup"><span data-stu-id="f8b5d-127">Click hello check mark toostart hello update.</span></span>


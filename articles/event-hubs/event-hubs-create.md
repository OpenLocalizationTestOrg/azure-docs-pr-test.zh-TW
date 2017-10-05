---
title: "建立 Azure 事件中樞 | Microsoft Docs"
description: "使用 Azure 入口網站來建立「Azure 事件中樞」命名空間和事件中樞"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: sethm
ms.openlocfilehash: 816bf1426704d3391550e80c0700f1b011683a94
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-the-azure-portal"></a><span data-ttu-id="b1aa9-103">使用 Azure 入口網站來建立事件中樞命名空間和事件中樞</span><span class="sxs-lookup"><span data-stu-id="b1aa9-103">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="b1aa9-104">建立事件中樞命名空間</span><span class="sxs-lookup"><span data-stu-id="b1aa9-104">Create an Event Hubs namespace</span></span>
1. <span data-ttu-id="b1aa9-105">登入 [Azure 入口網站][Azure portal]，然後按一下畫面左上方的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b1aa9-105">Log on to the [Azure portal][Azure portal], and click **New** at the top left of the screen.</span></span>
1. <span data-ttu-id="b1aa9-106">按一下 [物聯網]，然後按一下 [事件中樞]。</span><span class="sxs-lookup"><span data-stu-id="b1aa9-106">Click **Internet of Things**, and then click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. <span data-ttu-id="b1aa9-107">在 [建立命名空間]  刀鋒視窗中，輸入命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="b1aa9-107">In the **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="b1aa9-108">系統會立即檢查此名稱是否可用。</span><span class="sxs-lookup"><span data-stu-id="b1aa9-108">The system immediately checks to see if the name is available.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. <span data-ttu-id="b1aa9-109">確定命名空間名稱可用之後，請選擇定價層 ([基本] 或 [標準])。</span><span class="sxs-lookup"><span data-stu-id="b1aa9-109">After making sure the namespace name is available, choose the pricing tier (Basic or Standard).</span></span> <span data-ttu-id="b1aa9-110">此外，選擇要在其中建立資源的 Azure 訂用帳戶、資源群組和位置。</span><span class="sxs-lookup"><span data-stu-id="b1aa9-110">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span></span> 
1. <span data-ttu-id="b1aa9-111">按一下 [建立]  來建立命名空間。</span><span class="sxs-lookup"><span data-stu-id="b1aa9-111">Click **Create** to create the namespace.</span></span> <span data-ttu-id="b1aa9-112">您可能必須等候幾分鐘，讓系統完整佈建資源。</span><span class="sxs-lookup"><span data-stu-id="b1aa9-112">You may have to wait a few minutes for the system to fully provision the resources.</span></span>
2. <span data-ttu-id="b1aa9-113">在入口網站的命名空間清單中，按一下新建立的命名空間。</span><span class="sxs-lookup"><span data-stu-id="b1aa9-113">In the portal list of namespaces, click the newly created namespace.</span></span>
2. <span data-ttu-id="b1aa9-114">按一下 [共用存取原則]，然後按一下 [RootManageSharedAccessKey]。</span><span class="sxs-lookup"><span data-stu-id="b1aa9-114">Click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. <span data-ttu-id="b1aa9-115">按一下複製按鈕，將 **RootManageSharedAccessKey** 連接字串複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="b1aa9-115">Click the copy button to copy the **RootManageSharedAccessKey** connection string to the clipboard.</span></span> <span data-ttu-id="b1aa9-116">將這個連接字串儲存在暫存位置，例如 [記事本]，供以日後使用。</span><span class="sxs-lookup"><span data-stu-id="b1aa9-116">Save this connection string in a temporary location, such as Notepad, to use later.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a><span data-ttu-id="b1aa9-117">建立事件中心</span><span class="sxs-lookup"><span data-stu-id="b1aa9-117">Create an event hub</span></span>

1. <span data-ttu-id="b1aa9-118">在事件中樞命名空間清單中，按一下新建立的命名空間。</span><span class="sxs-lookup"><span data-stu-id="b1aa9-118">In the Event Hubs namespace list, click the newly created namespace.</span></span>      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. <span data-ttu-id="b1aa9-119">在命名空間刀鋒視窗中，按一下 [事件中樞] 。</span><span class="sxs-lookup"><span data-stu-id="b1aa9-119">In the namespace blade, click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. <span data-ttu-id="b1aa9-120">在刀鋒視窗頂端，按一下 [新增事件中樞] 。</span><span class="sxs-lookup"><span data-stu-id="b1aa9-120">At the top of the blade, click **Add Event Hub**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. <span data-ttu-id="b1aa9-121">輸入您的事件中樞名稱，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="b1aa9-121">Type a name for your event hub, then click **Create**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub5.png)

<span data-ttu-id="b1aa9-122">現已建立事件中樞，您已具有傳送及接收事件所需的連接字串。</span><span class="sxs-lookup"><span data-stu-id="b1aa9-122">Your event hub is now created, and you have the connection strings you need to send and receive events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1aa9-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b1aa9-123">Next steps</span></span>
<span data-ttu-id="b1aa9-124">若要深入了解事件中樞，請造訪下列連結：</span><span class="sxs-lookup"><span data-stu-id="b1aa9-124">To learn more about Event Hubs, visit these links:</span></span>

* [<span data-ttu-id="b1aa9-125">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="b1aa9-125">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="b1aa9-126">事件中樞 API 概觀</span><span class="sxs-lookup"><span data-stu-id="b1aa9-126">Event Hubs API overview</span></span>](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/
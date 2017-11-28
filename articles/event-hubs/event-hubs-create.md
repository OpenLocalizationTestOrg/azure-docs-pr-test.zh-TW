---
title: "aaaCreate Azure 事件中心 |Microsoft 文件"
description: "建立 Azure 事件中樞命名空間和事件中心使用 hello Azure 入口網站"
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
ms.openlocfilehash: 9a8b7711e2ca7d112e24be19353d43c365ff6935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-hello-azure-portal"></a><span data-ttu-id="ee0ef-103">建立事件中樞命名空間和事件中心使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ee0ef-103">Create an Event Hubs namespace and an event hub using hello Azure portal</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="ee0ef-104">建立事件中樞命名空間</span><span class="sxs-lookup"><span data-stu-id="ee0ef-104">Create an Event Hubs namespace</span></span>
1. <span data-ttu-id="ee0ef-105">登入 toohello [Azure 入口網站][Azure portal]，然後按一下**新增**hello 在左上方的囉 」 畫面。</span><span class="sxs-lookup"><span data-stu-id="ee0ef-105">Log on toohello [Azure portal][Azure portal], and click **New** at hello top left of hello screen.</span></span>
1. <span data-ttu-id="ee0ef-106">按一下 物聯網，然後按一下事件中樞。</span><span class="sxs-lookup"><span data-stu-id="ee0ef-106">Click **Internet of Things**, and then click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. <span data-ttu-id="ee0ef-107">在 hello**建立命名空間**刀鋒視窗中，輸入命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="ee0ef-107">In hello **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="ee0ef-108">hello 系統立即檢查 toosee hello 名稱是否可用。</span><span class="sxs-lookup"><span data-stu-id="ee0ef-108">hello system immediately checks toosee if hello name is available.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. <span data-ttu-id="ee0ef-109">提供讓確定 hello 命名空間名稱之後，選擇 hello 定價層 （基本或標準）。</span><span class="sxs-lookup"><span data-stu-id="ee0ef-109">After making sure hello namespace name is available, choose hello pricing tier (Basic or Standard).</span></span> <span data-ttu-id="ee0ef-110">而且請 toocreate hello 資源選擇 Azure 訂用帳戶、 資源群組和位置。</span><span class="sxs-lookup"><span data-stu-id="ee0ef-110">Also, choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> 
1. <span data-ttu-id="ee0ef-111">按一下**建立**toocreate hello 命名空間。</span><span class="sxs-lookup"><span data-stu-id="ee0ef-111">Click **Create** toocreate hello namespace.</span></span> <span data-ttu-id="ee0ef-112">您可能需要幾分鐘，讓 hello 系統 toofully 佈建 hello 資源 toowait。</span><span class="sxs-lookup"><span data-stu-id="ee0ef-112">You may have toowait a few minutes for hello system toofully provision hello resources.</span></span>
2. <span data-ttu-id="ee0ef-113">在 hello 入口網站清單的命名空間中，按一下新建立的命名空間的 hello。</span><span class="sxs-lookup"><span data-stu-id="ee0ef-113">In hello portal list of namespaces, click hello newly created namespace.</span></span>
2. <span data-ttu-id="ee0ef-114">按一下 共用存取原則，然後按一下RootManageSharedAccessKey。</span><span class="sxs-lookup"><span data-stu-id="ee0ef-114">Click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. <span data-ttu-id="ee0ef-115">按一下 hello 複製按鈕 toocopy hello **RootManageSharedAccessKey**連接字串 toohello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="ee0ef-115">Click hello copy button toocopy hello **RootManageSharedAccessKey** connection string toohello clipboard.</span></span> <span data-ttu-id="ee0ef-116">將這個連接字串儲存在暫存位置，例如 [記事本]，稍後 toouse。</span><span class="sxs-lookup"><span data-stu-id="ee0ef-116">Save this connection string in a temporary location, such as Notepad, toouse later.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a><span data-ttu-id="ee0ef-117">建立事件中心</span><span class="sxs-lookup"><span data-stu-id="ee0ef-117">Create an event hub</span></span>

1. <span data-ttu-id="ee0ef-118">在 hello 事件中樞命名空間清單中，按一下新建立的 hello 命名空間。</span><span class="sxs-lookup"><span data-stu-id="ee0ef-118">In hello Event Hubs namespace list, click hello newly created namespace.</span></span>      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. <span data-ttu-id="ee0ef-119">在 hello 命名空間刀鋒視窗中，按一下 **事件中心**。</span><span class="sxs-lookup"><span data-stu-id="ee0ef-119">In hello namespace blade, click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. <span data-ttu-id="ee0ef-120">在 hello hello 刀鋒視窗頂端，按一下**新增事件中樞**。</span><span class="sxs-lookup"><span data-stu-id="ee0ef-120">At hello top of hello blade, click **Add Event Hub**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. <span data-ttu-id="ee0ef-121">輸入您的事件中樞名稱，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="ee0ef-121">Type a name for your event hub, then click **Create**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub5.png)

<span data-ttu-id="ee0ef-122">現在建立事件中樞，和您擁有 hello 連接字串，您需要 toosend 與接收事件。</span><span class="sxs-lookup"><span data-stu-id="ee0ef-122">Your event hub is now created, and you have hello connection strings you need toosend and receive events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee0ef-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ee0ef-123">Next steps</span></span>
<span data-ttu-id="ee0ef-124">toolearn 有關事件中心的詳細資訊，請前往下列連結：</span><span class="sxs-lookup"><span data-stu-id="ee0ef-124">toolearn more about Event Hubs, visit these links:</span></span>

* [<span data-ttu-id="ee0ef-125">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="ee0ef-125">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="ee0ef-126">事件中樞 API 概觀</span><span class="sxs-lookup"><span data-stu-id="ee0ef-126">Event Hubs API overview</span></span>](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/
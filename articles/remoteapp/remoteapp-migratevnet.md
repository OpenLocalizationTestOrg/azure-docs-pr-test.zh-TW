---
title: "如何從 RemoteApp VNET 移轉至 Azure VNET | Microsoft Docs"
description: "了解如何從 RemoteApp VNET 移轉至 Azure VNET"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 10b5f4844a38fe97852dee8634e8cf54f1a23a1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-migrate-a-hybrid-collection-from-a-remoteapp-vnet-to-an-azure-vnet"></a><span data-ttu-id="b75a4-103">如何將混合式集合從 RemoteApp VNET 移轉至 Azure VNET</span><span class="sxs-lookup"><span data-stu-id="b75a4-103">How to migrate a hybrid collection from a RemoteApp VNET to an Azure VNET</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b75a4-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="b75a4-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="b75a4-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="b75a4-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="b75a4-106">好消息！</span><span class="sxs-lookup"><span data-stu-id="b75a4-106">Good news!</span></span> <span data-ttu-id="b75a4-107">我們已讓您將混合式 RemoteApp 集合直接部署到現有 Azure 虛擬網路 (VNET)，而未建立 RemoteApp 特定 VNET。</span><span class="sxs-lookup"><span data-stu-id="b75a4-107">We have enabled you to deploy hybrid RemoteApp collections directly into your existing Azure virtual networks (VNETs) instead of creating RemoteApp-specific VNETs.</span></span> <span data-ttu-id="b75a4-108">這可讓您利用最新的 VNET 功能 (如 ExpressRoute)，並將部署至該 VNET 之其他 Azure 服務和虛擬機器的直接網路存取權提供給混合式集合 </span><span class="sxs-lookup"><span data-stu-id="b75a4-108">This lets you take advantage of the latest VNET features (like ExpressRoute) and give your hybrid collections direct network access to other Azure services and virtual machines deployed to that VNET.</span></span>  <span data-ttu-id="b75a4-109">(這與 VNET 對 VNET 組態相較之下，可讓您擁有更佳的效能和更簡單的設定)。</span><span class="sxs-lookup"><span data-stu-id="b75a4-109">(This gets you better performance and easier setup than VNET-to-VNET configurations).</span></span>

<span data-ttu-id="b75a4-110">假設，您已經建立稱為「OriginalCollection」的混合式 RemoteApp 集合與稱為「RemoteAppVNET」的 RemoteApp VNET。</span><span class="sxs-lookup"><span data-stu-id="b75a4-110">Let’s say that you’ve already created a hybrid RemoteApp collection called *OriginalCollection* with a RemoteApp VNET called *RemoteAppVNET*.</span></span> <span data-ttu-id="b75a4-111">以下是將它移轉至稱為 *AzureVNET*之新 Azure VNET 的步驟。</span><span class="sxs-lookup"><span data-stu-id="b75a4-111">Here are the steps to migrate it to a new Azure VNET called *AzureVNET*.</span></span>

1. <span data-ttu-id="b75a4-112">在[管理入口網站](http://manage.windowsazure.com/)的 [網路] 索引標籤上，使用與用於 RemoteAppVNET 相同的位置、DNS 組態和位址空間 (針對至少其中一個 AzureVNET 子網路) 建立稱為 AzureVNET 的 VNET。</span><span class="sxs-lookup"><span data-stu-id="b75a4-112">On the **Networks** tab in the [management portal](http://manage.windowsazure.com/), create a VNET called *AzureVNET*, using the same location, DNS configuration, and address space (for at least one of the *AzureVNET* subnets) as you used for *RemoteAppVNET*.</span></span>
2. <span data-ttu-id="b75a4-113">設定 AzureVNET 裝載或透過網路連接到 OriginalCollection 加入網域的 Active Directory 部署。</span><span class="sxs-lookup"><span data-stu-id="b75a4-113">Configure *AzureVNET* to either host or have network connectivity to the Active Directory deployment that *OriginalCollection* is domain joined to.</span></span>
3. <span data-ttu-id="b75a4-114">在 [RemoteApp] 索引標籤上，建立稱為「新集合」的新 RemoteApp 集合 </span><span class="sxs-lookup"><span data-stu-id="b75a4-114">On the **RemoteApps** tab, create a new RemoteApp collection called *New Collection*.</span></span> <span data-ttu-id="b75a4-115">(使用 [使用 VNET 建立] 選項，而不是 [快速建立])。</span><span class="sxs-lookup"><span data-stu-id="b75a4-115">(Use the **Create with VNET** option, not **Quick Create**.)</span></span>
4. <span data-ttu-id="b75a4-116">設定要部署到 AzureVNET 中子網路的 NewCollection。</span><span class="sxs-lookup"><span data-stu-id="b75a4-116">Configure *NewCollection* to be deployed to a subnet in *AzureVNET*.</span></span>
5. <span data-ttu-id="b75a4-117">設定 NewCollection 使用與您用於 OriginalCollection 相同的映像和網域加入資訊。</span><span class="sxs-lookup"><span data-stu-id="b75a4-117">Configure *NewCollection* to use the same image and domain join information as you used for *OriginalCollection*.</span></span>
6. <span data-ttu-id="b75a4-118">在幾個小時後， *NewCollection* 會顯示在集合清單中，且狀態為 [作用中]。</span><span class="sxs-lookup"><span data-stu-id="b75a4-118">After a few hours, *NewCollection* will show up in your collection list with an Active state.</span></span>

<span data-ttu-id="b75a4-119">現在，如果您不需要將任何使用者資訊從原始集合移轉到新的集合，請接著執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b75a4-119">Now, if you DON’T need to migrate any user information from the original collection to the new collection, do these steps next:</span></span>

1. <span data-ttu-id="b75a4-120">刪除 *OriginalCollection*。</span><span class="sxs-lookup"><span data-stu-id="b75a4-120">Delete *OriginalCollection*.</span></span>
2. <span data-ttu-id="b75a4-121">刪除 *RemoteAppVNET*。</span><span class="sxs-lookup"><span data-stu-id="b75a4-121">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="b75a4-122">大功告成！</span><span class="sxs-lookup"><span data-stu-id="b75a4-122">And, you’re done!</span></span>

<span data-ttu-id="b75a4-123">或者，如果您需要將使用者資訊從原始集合移轉到新的集合，請接著執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b75a4-123">Alternately, if you DO need to migrate user information from the original collection to the new collection, do these steps next:</span></span>

1. <span data-ttu-id="b75a4-124">使用 Azure 訂用帳戶識別碼、原始集合名稱以及新集合名稱，將電子郵件傳送給 [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) ，並要求他們移轉您的使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="b75a4-124">Send an email to [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) with your Azure subscription ID, the name of your original collection, and the name of your new collection, and ask them to migrate your user information.</span></span>
2. <span data-ttu-id="b75a4-125">在 2 個工作日內，RemoteApp 小組會將使用者存取清單以及所有使用者文件和使用者設定從原始集合移至新的集合。</span><span class="sxs-lookup"><span data-stu-id="b75a4-125">Within 2 business days the RemoteApp team will move the user access list and all user documents and user settings from the original collection to the new collection.</span></span>
3. <span data-ttu-id="b75a4-126">刪除 *OriginalCollection*。</span><span class="sxs-lookup"><span data-stu-id="b75a4-126">Delete *OriginalCollection*.</span></span>
4. <span data-ttu-id="b75a4-127">刪除 *RemoteAppVNET*。</span><span class="sxs-lookup"><span data-stu-id="b75a4-127">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="b75a4-128">現在，大功告成！</span><span class="sxs-lookup"><span data-stu-id="b75a4-128">And now, you’re done!</span></span>

<span data-ttu-id="b75a4-129">如果您有任何疑問或需要特殊協助，請將電子郵件寄到 [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help)的 RemoteApp VNET。</span><span class="sxs-lookup"><span data-stu-id="b75a4-129">If you have any questions or need special assistance, please email [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span></span>


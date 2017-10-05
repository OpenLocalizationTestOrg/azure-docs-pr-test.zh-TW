---
title: "機密資料絕不儲存在 Azure remoteapp 的自訂映像上 | Microsoft Docs"
description: "深入了解在 Azure RemoteApp 自訂映像中儲存資料的指導方針"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 5a19903b-15f9-49d9-9bc1-ae80f2671aa1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 75d5415d33324d957617426e75909a6c6c58b1f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="5593d-103">機密資料絕不要儲存在自訂映像上</span><span class="sxs-lookup"><span data-stu-id="5593d-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5593d-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="5593d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="5593d-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="5593d-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="5593d-106">當您將自己的應用程式裝載在 Azure RemoteApp 中時，第一個步驟就是建立自訂映像。</span><span class="sxs-lookup"><span data-stu-id="5593d-106">When you host your own application in Azure RemoteApp, the first step is to create a custom image.</span></span> <span data-ttu-id="5593d-107">我們會使用這個自訂映像建立 VM 執行個體，向您的使用者提供應用程式。</span><span class="sxs-lookup"><span data-stu-id="5593d-107">We use that custom image to create VM instances that serve your apps to your users.</span></span> <span data-ttu-id="5593d-108">自訂映像應該只包含應用程式，絕對不要包含可能遺失的機密資料，例如 SQL 資料庫、人事檔案，或像是 QuickBooks 公司檔案的特殊資料檔案。</span><span class="sxs-lookup"><span data-stu-id="5593d-108">The custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="5593d-109">所有的機密資料都應位於 Azure RemoteApp 外部的檔案伺服器上，可以是另一個 Azure VM，或在 SQL Azure 中。</span><span class="sxs-lookup"><span data-stu-id="5593d-109">All sensitive data should reside external to Azure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="5593d-110">映像應該只裝載連接到資料來源及顯示資料的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5593d-110">The image should just host the application that connects to the data source and presents the data.</span></span> <span data-ttu-id="5593d-111">如需詳細資訊，請參閱 [Azure RemoteApp 映像需求](remoteapp-imagereqs.md) 。</span><span class="sxs-lookup"><span data-stu-id="5593d-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="5593d-112">若要了解不該儲存機密資料的原因，您需要了解 Azure RemoteApp 的運作方式。</span><span class="sxs-lookup"><span data-stu-id="5593d-112">To understand why you should not store sensitive data, you need to understand how Azure RemoteApp works.</span></span> <span data-ttu-id="5593d-113">當建立或更新集合時，幕後會建立多個映像的複製品或複本。</span><span class="sxs-lookup"><span data-stu-id="5593d-113">When a collection is created or updated, behind the scenes multiple clones or copies of the image are created.</span></span> <span data-ttu-id="5593d-114">所有這些 VM 執行個體都是和自訂映像完全一致的確切複本，當使用者啟動應用程式時，他們就會連接到這些 VM 執行個體的其中之一。</span><span class="sxs-lookup"><span data-stu-id="5593d-114">All these VM instances are exact replicas of the custom image; when users launch applications they are connected to one of these VM instances.</span></span> <span data-ttu-id="5593d-115">但是相同的執行個體沒有任何保證，也不應該有什麼影響，因為它們是非永續性的。</span><span class="sxs-lookup"><span data-stu-id="5593d-115">But the same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="5593d-116">裝載應用程式的 VM 執行個體是非永續性的，可以損毀或刪除，例如，在集合更新期間。</span><span class="sxs-lookup"><span data-stu-id="5593d-116">The VM instances hosting the applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="5593d-117">集合一經佈建且使用者開始連接到 VM，使用者資料就是永續性且受保護的，因為它會儲存在 VHD 的個別儲存體中，我們稱之為[使用者設定檔磁碟 (UPD)](remoteapp-upd.md)，這是 c:\users\<使用者設定檔> 中的使用者設定檔。</span><span class="sxs-lookup"><span data-stu-id="5593d-117">Once the collection is provisioned and users start connecting to the VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is the user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="5593d-118">當應用程式啟動時，就會掛載 UPD，作業系統會視同本機使用者設定檔處理。</span><span class="sxs-lookup"><span data-stu-id="5593d-118">When an application starts, the UPD is mounted and treated just like a local user profile by the operating system.</span></span> <span data-ttu-id="5593d-119">深入了解 [Azure RemoteApp 如何儲存使用者資料和設定](remoteapp-upd.md)。</span><span class="sxs-lookup"><span data-stu-id="5593d-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="5593d-120">不該在映像的資料範例︰</span><span class="sxs-lookup"><span data-stu-id="5593d-120">Example data that should not reside in the image:</span></span>

* <span data-ttu-id="5593d-121">供使用者存取的共用資料</span><span class="sxs-lookup"><span data-stu-id="5593d-121">Shared data for users to access</span></span>
* <span data-ttu-id="5593d-122">SQL DB 或 QuickBooks DB</span><span class="sxs-lookup"><span data-stu-id="5593d-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="5593d-123">D:\ 中的所有資料</span><span class="sxs-lookup"><span data-stu-id="5593d-123">Any data in D:\\</span></span>

<span data-ttu-id="5593d-124">可以位在預設設定檔，要複製到每個使用者 UPD 的範例資料︰</span><span class="sxs-lookup"><span data-stu-id="5593d-124">Example data that can reside in the default profile to be copied into every users’ UPD:</span></span>

* <span data-ttu-id="5593d-125">每個使用者的組態檔</span><span class="sxs-lookup"><span data-stu-id="5593d-125">Configuration files per user</span></span>
* <span data-ttu-id="5593d-126">使用者需要保留在 UPD 中的指令碼</span><span class="sxs-lookup"><span data-stu-id="5593d-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="5593d-127">重點︰</span><span class="sxs-lookup"><span data-stu-id="5593d-127">Key points:</span></span>

* <span data-ttu-id="5593d-128">建立自訂映像時，可能遺失的機密資料絕不儲存在映像上。</span><span class="sxs-lookup"><span data-stu-id="5593d-128">Never store sensitive data that can be lost on the image when creating a custom image.</span></span>
* <span data-ttu-id="5593d-129">機密資料應該一律放在雲端的個別檔案伺服器、個別 Azure VM 上，一律是在 Azure RemoteApp 中裝載應用程式的 VM 執行個體外部。</span><span class="sxs-lookup"><span data-stu-id="5593d-129">Sensitive data should always reside on a separate file server, separate Azure VM, on the cloud, and always external to the VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="5593d-130">使用者資料儲存和保存在使用者設定檔磁碟 (UPD)</span><span class="sxs-lookup"><span data-stu-id="5593d-130">User data is saved and persists in the user profile disk (UPD)</span></span>


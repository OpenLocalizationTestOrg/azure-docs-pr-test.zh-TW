---
title: "aaaNever 存放區上的機密資料的 Azure RemoteApp 的自訂映像 |Microsoft 文件"
description: "深入了解 hello 指導方針，將資料儲存在 Azure RemoteApp 中的自訂映像"
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
ms.openlocfilehash: 86a0fea218f8826d6d25f50d3c4c36e368e26fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="f7d78-103">機密資料絕不要儲存在自訂映像上</span><span class="sxs-lookup"><span data-stu-id="f7d78-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f7d78-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="f7d78-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f7d78-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f7d78-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f7d78-106">裝載自己在 Azure RemoteApp 中的應用程式時，hello 第一個步驟是 toocreate 自訂映像。</span><span class="sxs-lookup"><span data-stu-id="f7d78-106">When you host your own application in Azure RemoteApp, hello first step is toocreate a custom image.</span></span> <span data-ttu-id="f7d78-107">我們使用 tooyour 使用者提供您的應用程式的自訂映像 toocreate VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="f7d78-107">We use that custom image toocreate VM instances that serve your apps tooyour users.</span></span> <span data-ttu-id="f7d78-108">僅限應用程式和從未機密資料，可能會遺失，例如 SQL 資料庫、 人員檔案或特殊的資料檔案，像是 QuickBooks 公司檔案，應該包含 hello 自訂映像。</span><span class="sxs-lookup"><span data-stu-id="f7d78-108">hello custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="f7d78-109">所有的機密資料應該位於外部 tooAzure RemoteApp 的檔案伺服器上，另一個 Azure VM，或 SQL Azure 中。</span><span class="sxs-lookup"><span data-stu-id="f7d78-109">All sensitive data should reside external tooAzure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="f7d78-110">hello 映像應該只主機 hello 應用程式，可連接 toohello 資料來源，並顯示 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="f7d78-110">hello image should just host hello application that connects toohello data source and presents hello data.</span></span> <span data-ttu-id="f7d78-111">如需詳細資訊，請參閱 [Azure RemoteApp 映像需求](remoteapp-imagereqs.md) 。</span><span class="sxs-lookup"><span data-stu-id="f7d78-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="f7d78-112">toounderstand 為什麼您不應儲存敏感性資料，您需要的 toounderstand Azure RemoteApp 的運作方式。</span><span class="sxs-lookup"><span data-stu-id="f7d78-112">toounderstand why you should not store sensitive data, you need toounderstand how Azure RemoteApp works.</span></span> <span data-ttu-id="f7d78-113">建立或更新集合，hello 幕後多個複製品或 hello 映像的複本會建立。</span><span class="sxs-lookup"><span data-stu-id="f7d78-113">When a collection is created or updated, behind hello scenes multiple clones or copies of hello image are created.</span></span> <span data-ttu-id="f7d78-114">所有這些 VM 執行個體都完全 hello 自訂映像; 的複本當使用者啟動應用程式會連接的 tooone 個 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="f7d78-114">All these VM instances are exact replicas of hello custom image; when users launch applications they are connected tooone of these VM instances.</span></span> <span data-ttu-id="f7d78-115">但 hello 相同的執行個體並不一定都應該不重要，因為它們是在非持續性。</span><span class="sxs-lookup"><span data-stu-id="f7d78-115">But hello same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="f7d78-116">hello VM 執行個體 hello 的裝載應用程式為非持續性，可能會損毀或刪除基礎，例如，在集合更新時。</span><span class="sxs-lookup"><span data-stu-id="f7d78-116">hello VM instances hosting hello applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="f7d78-117">一旦 hello 集合已佈建，且使用者開始連接 toohello Vm，使用者資料的持續性和保護，因為它會儲存在個別的存放裝置內的 VHD，我們會呼叫[使用者設定檔磁碟 (UPD)](remoteapp-upd.md)，這是 hello 使用者設定檔在 c:\users\<userprofile >。</span><span class="sxs-lookup"><span data-stu-id="f7d78-117">Once hello collection is provisioned and users start connecting toohello VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is hello user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="f7d78-118">當應用程式啟動時，hello UPD 會掛接並被視為本機使用者設定檔依 hello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="f7d78-118">When an application starts, hello UPD is mounted and treated just like a local user profile by hello operating system.</span></span> <span data-ttu-id="f7d78-119">深入了解 [Azure RemoteApp 如何儲存使用者資料和設定](remoteapp-upd.md)。</span><span class="sxs-lookup"><span data-stu-id="f7d78-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="f7d78-120">不應該位於 hello 映像中的範例資料：</span><span class="sxs-lookup"><span data-stu-id="f7d78-120">Example data that should not reside in hello image:</span></span>

* <span data-ttu-id="f7d78-121">共用的資料的使用者 tooaccess</span><span class="sxs-lookup"><span data-stu-id="f7d78-121">Shared data for users tooaccess</span></span>
* <span data-ttu-id="f7d78-122">SQL DB 或 QuickBooks DB</span><span class="sxs-lookup"><span data-stu-id="f7d78-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="f7d78-123">D:\ 中的所有資料</span><span class="sxs-lookup"><span data-stu-id="f7d78-123">Any data in D:\\</span></span>

<span data-ttu-id="f7d78-124">範例資料複製到每個使用者的 UPD hello 預設設定檔 toobe 可以位於：</span><span class="sxs-lookup"><span data-stu-id="f7d78-124">Example data that can reside in hello default profile toobe copied into every users’ UPD:</span></span>

* <span data-ttu-id="f7d78-125">每個使用者的組態檔</span><span class="sxs-lookup"><span data-stu-id="f7d78-125">Configuration files per user</span></span>
* <span data-ttu-id="f7d78-126">使用者需要保留在 UPD 中的指令碼</span><span class="sxs-lookup"><span data-stu-id="f7d78-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="f7d78-127">重點︰</span><span class="sxs-lookup"><span data-stu-id="f7d78-127">Key points:</span></span>

* <span data-ttu-id="f7d78-128">絕對不要儲存機密資料，可能會建立自訂映像時遺失 hello 映像上。</span><span class="sxs-lookup"><span data-stu-id="f7d78-128">Never store sensitive data that can be lost on hello image when creating a custom image.</span></span>
* <span data-ttu-id="f7d78-129">機密資料永遠應該位於個別的檔案伺服器上，個別 Azure VM，hello 雲端和裝載在 Azure RemoteApp 中的應用程式永遠外部 toohello VM 執行個體上。</span><span class="sxs-lookup"><span data-stu-id="f7d78-129">Sensitive data should always reside on a separate file server, separate Azure VM, on hello cloud, and always external toohello VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="f7d78-130">使用者資料儲存和保存在 hello 使用者設定檔磁碟 (UPD)</span><span class="sxs-lookup"><span data-stu-id="f7d78-130">User data is saved and persists in hello user profile disk (UPD)</span></span>


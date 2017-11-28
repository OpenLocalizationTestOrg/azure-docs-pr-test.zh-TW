---
title: "aaaManage StorSimple 磁碟區容器上 hello StorSimple 8000 系列裝置 |Microsoft 文件"
description: "說明如何使用 hello StorSimple 裝置管理員服務磁碟區容器頁面 tooadd、 修改或刪除磁碟區容器。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="1e0d2-103">使用 hello StorSimple 裝置管理員服務 toomanage StorSimple 磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="1e0d2-103">Use hello StorSimple Device Manager service toomanage StorSimple volume containers</span></span>

## <a name="overview"></a><span data-ttu-id="1e0d2-104">概觀</span><span class="sxs-lookup"><span data-stu-id="1e0d2-104">Overview</span></span>
<span data-ttu-id="1e0d2-105">本教學課程將說明 toouse hello StorSimple 裝置管理員服務 toocreate 並管理 StorSimple 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="1e0d2-106">Microsoft Azure StorSimple 裝置中的磁碟區容器包含一個或多個可共用儲存體帳戶、加密和頻寬耗用量設定的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="1e0d2-107">一個裝置可以有多個磁碟區容器，供其所有磁碟區使用。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="1e0d2-108">磁碟區容器具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e0d2-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="1e0d2-109">**磁碟區**– hello 分層或固定在本機 hello 磁碟區容器內包含的 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> 
* <span data-ttu-id="1e0d2-110">**加密** – 可以為每個磁碟區容器定義的加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-110">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="1e0d2-111">此金鑰用來加密從您的 StorSimple 裝置 toohello 雲端傳送 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-111">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="1e0d2-112">軍事等級 aes-256 位元金鑰可搭配 hello 使用者輸入的金鑰。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-112">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="1e0d2-113">toosecure 您的資料，我們建議您一律啟用雲端儲存體加密。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-113">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="1e0d2-114">**儲存體帳戶**– hello 使用的 toostore hello 資料的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-114">**Storage account** – hello Azure storage account that is used toostore hello data.</span></span> <span data-ttu-id="1e0d2-115">所有位於磁碟區容器中的 hello 磁碟區共用這個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-115">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="1e0d2-116">您可以從現有的清單，請選擇儲存體帳戶，或建立新的帳戶，當您建立 hello 磁碟區容器，然後指定該帳戶的 hello 存取認證。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-116">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="1e0d2-117">**雲端頻寬**– hello hello 裝置所傳送嗨裝置中的 hello 資料 toohello 雲端時所使用的頻寬。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-117">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="1e0d2-118">當您建立此容器時，可以指定一個介於 1 Mbps 到 1000 Mbps 之間的值，以強制執行頻寬控制。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-118">You can enforce a bandwidth control by specifying a value between 1 Mbps and 1,000 Mbps when you create this container.</span></span> <span data-ttu-id="1e0d2-119">如果您想 hello 裝置 tooconsume 所有可用的頻寬，請將此欄位太**Unlimited**。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-119">If you want hello device tooconsume all available bandwidth, set this field too**Unlimited**.</span></span> <span data-ttu-id="1e0d2-120">您也可以建立和套用頻寬範本 tooallocate 頻寬排程為基礎。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-120">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

<span data-ttu-id="1e0d2-121">hello 下列程序說明如何 toouse hello StorSimple**磁碟區容器**刀鋒視窗 toocomplete hello 下列常見作業：</span><span class="sxs-lookup"><span data-stu-id="1e0d2-121">hello following procedures explain how toouse hello StorSimple **Volume containers** blade toocomplete hello following common operations:</span></span>

* <span data-ttu-id="1e0d2-122">新增磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="1e0d2-122">Add a volume container</span></span>
* <span data-ttu-id="1e0d2-123">修改磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="1e0d2-123">Modify a volume container</span></span>
* <span data-ttu-id="1e0d2-124">刪除磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="1e0d2-124">Delete a volume container</span></span>

## <a name="add-a-volume-container"></a><span data-ttu-id="1e0d2-125">新增磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="1e0d2-125">Add a volume container</span></span>
<span data-ttu-id="1e0d2-126">執行下列步驟 tooadd 磁碟區容器的 hello。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-126">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="1e0d2-127">修改磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="1e0d2-127">Modify a volume container</span></span>
<span data-ttu-id="1e0d2-128">執行下列步驟 toomodify 磁碟區容器的 hello。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-128">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="1e0d2-129">刪除磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="1e0d2-129">Delete a volume container</span></span>
<span data-ttu-id="1e0d2-130">磁碟區容器內具有磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-130">A volume container has volumes within it.</span></span> <span data-ttu-id="1e0d2-131">先刪除所有包含在它的 hello 磁碟區時，才可以刪除它。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-131">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="1e0d2-132">執行下列步驟 toodelete 磁碟區容器的 hello。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-132">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="1e0d2-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1e0d2-133">Next steps</span></span>
* <span data-ttu-id="1e0d2-134">深入了解 [管理 StorSimple 磁碟區](storsimple-8000-manage-volumes-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-134">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span> 
* <span data-ttu-id="1e0d2-135">深入了解[使用您的 StorSimple 裝置 hello StorSimple 裝置管理員服務 tooadminister](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="1e0d2-135">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>


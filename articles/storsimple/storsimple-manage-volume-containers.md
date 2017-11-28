---
title: "aaaManage StorSimple 磁碟區容器 |Microsoft 文件"
description: "說明如何使用 hello StorSimple Manager 服務磁碟區容器頁面 tooadd、 修改或刪除磁碟區容器。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 1c64ce75-1fd3-4d3b-9304-d4dc0fc2b069
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 9b29536e0072306e53ac92bacca78a13d932c2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="dbb65-103">使用 hello StorSimple Manager 服務 toomanage StorSimple 磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="dbb65-103">Use hello StorSimple Manager service toomanage StorSimple volume containers</span></span>
## <a name="overview"></a><span data-ttu-id="dbb65-104">概觀</span><span class="sxs-lookup"><span data-stu-id="dbb65-104">Overview</span></span>
<span data-ttu-id="dbb65-105">本教學課程將說明 toouse hello StorSimple Manager 服務 toocreate 並管理 StorSimple 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="dbb65-105">This tutorial explains how toouse hello StorSimple Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="dbb65-106">Microsoft Azure StorSimple 裝置中的磁碟區容器包含一個或多個可共用儲存體帳戶、加密和頻寬耗用量設定的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dbb65-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="dbb65-107">一個裝置可以有多個磁碟區容器，供其所有磁碟區使用。</span><span class="sxs-lookup"><span data-stu-id="dbb65-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="dbb65-108">磁碟區容器具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="dbb65-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="dbb65-109">**磁碟區**– hello 分層或固定在本機 hello 磁碟區容器內包含的 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dbb65-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> <span data-ttu-id="dbb65-110">磁碟區容器可包含 too256 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dbb65-110">A volume container may contain up too256 StorSimple volumes.</span></span>
* <span data-ttu-id="dbb65-111">**加密** – 可以為每個磁碟區容器定義的加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="dbb65-111">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="dbb65-112">此金鑰用來加密從您的 StorSimple 裝置 toohello 雲端傳送 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="dbb65-112">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="dbb65-113">軍事等級 aes-256 位元金鑰可搭配 hello 使用者輸入的金鑰。</span><span class="sxs-lookup"><span data-stu-id="dbb65-113">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="dbb65-114">toosecure 您的資料，我們建議您一律啟用雲端儲存體加密。</span><span class="sxs-lookup"><span data-stu-id="dbb65-114">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="dbb65-115">**儲存體帳戶**– hello 是連結的 tooyour 雲端儲存體服務提供者的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="dbb65-115">**Storage account** – hello storage account that is linked tooyour cloud storage service provider.</span></span> <span data-ttu-id="dbb65-116">所有位於磁碟區容器中的 hello 磁碟區共用這個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="dbb65-116">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="dbb65-117">您可以從現有的清單，請選擇儲存體帳戶，或建立新的帳戶，當您建立 hello 磁碟區容器，然後指定該帳戶的 hello 存取認證。</span><span class="sxs-lookup"><span data-stu-id="dbb65-117">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="dbb65-118">**雲端頻寬**– hello hello 裝置所傳送嗨裝置中的 hello 資料 toohello 雲端時所使用的頻寬。</span><span class="sxs-lookup"><span data-stu-id="dbb65-118">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="dbb65-119">當您定義此容器時，可以指定一個介於 1 與 1000 Mbps 之間的值，以強制執行頻寬控制。</span><span class="sxs-lookup"><span data-stu-id="dbb65-119">You can enforce a bandwidth control by specifying a value between 1 and 1000 Mbps when you define this container.</span></span> <span data-ttu-id="dbb65-120">如果您想要 hello 裝置 tooconsume 所有可用的頻寬，設定此欄位 tooUnlimited。</span><span class="sxs-lookup"><span data-stu-id="dbb65-120">If you want hello device tooconsume all available bandwidth, set this field tooUnlimited.</span></span> <span data-ttu-id="dbb65-121">您也可以建立和套用頻寬範本 tooallocate 頻寬排程為基礎。</span><span class="sxs-lookup"><span data-stu-id="dbb65-121">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

![磁碟區容器頁面](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

<span data-ttu-id="dbb65-123">此下列的程序說明如何 toouse hello StorSimple**磁碟區容器**頁面 toocomplete hello 下列常見作業：</span><span class="sxs-lookup"><span data-stu-id="dbb65-123">This following procedures explain how toouse hello StorSimple **Volume containers** page toocomplete hello following common operations:</span></span>

* <span data-ttu-id="dbb65-124">新增磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="dbb65-124">Add a volume container</span></span> 
* <span data-ttu-id="dbb65-125">修改磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="dbb65-125">Modify a volume container</span></span> 
* <span data-ttu-id="dbb65-126">刪除磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="dbb65-126">Delete a volume container</span></span> 

## <a name="add-a-volume-container"></a><span data-ttu-id="dbb65-127">新增磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="dbb65-127">Add a volume container</span></span>
<span data-ttu-id="dbb65-128">執行下列步驟 tooadd 磁碟區容器的 hello。</span><span class="sxs-lookup"><span data-stu-id="dbb65-128">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="dbb65-129">修改磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="dbb65-129">Modify a volume container</span></span>
<span data-ttu-id="dbb65-130">執行下列步驟 toomodify 磁碟區容器的 hello。</span><span class="sxs-lookup"><span data-stu-id="dbb65-130">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="dbb65-131">刪除磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="dbb65-131">Delete a volume container</span></span>
<span data-ttu-id="dbb65-132">磁碟區容器內具有磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dbb65-132">A volume container has volumes within it.</span></span> <span data-ttu-id="dbb65-133">先刪除所有包含在它的 hello 磁碟區時，才可以刪除它。</span><span class="sxs-lookup"><span data-stu-id="dbb65-133">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="dbb65-134">執行下列步驟 toodelete 磁碟區容器的 hello。</span><span class="sxs-lookup"><span data-stu-id="dbb65-134">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="dbb65-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dbb65-135">Next steps</span></span>
* <span data-ttu-id="dbb65-136">深入了解 [管理 StorSimple 磁碟區](storsimple-manage-volumes.md)。</span><span class="sxs-lookup"><span data-stu-id="dbb65-136">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span> 
* <span data-ttu-id="dbb65-137">深入了解[使用您的 StorSimple 裝置 hello StorSimple Manager 服務 tooadminister](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="dbb65-137">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>


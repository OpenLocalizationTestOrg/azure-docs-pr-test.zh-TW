---
title: "管理 StorSimple 磁碟區容器 | Microsoft Docs"
description: "說明如何使用 StorSimple Manager 服務磁碟區容器頁面新增、修改或刪除磁碟區容器。"
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
ms.openlocfilehash: bb55a7a4bff0fd4319de6f6ce958686ad8a4142b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-storsimple-volume-containers"></a><span data-ttu-id="218c9-103">使用 StorSimple Manager 服務管理 StorSimple 磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="218c9-103">Use the StorSimple Manager service to manage StorSimple volume containers</span></span>
## <a name="overview"></a><span data-ttu-id="218c9-104">概觀</span><span class="sxs-lookup"><span data-stu-id="218c9-104">Overview</span></span>
<span data-ttu-id="218c9-105">本教學課程說明如何使用 StorSimple Manager 服務建立和管理 StorSimple 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="218c9-105">This tutorial explains how to use the StorSimple Manager service to create and manage StorSimple volume containers.</span></span>

<span data-ttu-id="218c9-106">Microsoft Azure StorSimple 裝置中的磁碟區容器包含一個或多個可共用儲存體帳戶、加密和頻寬耗用量設定的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="218c9-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="218c9-107">一個裝置可以有多個磁碟區容器，供其所有磁碟區使用。</span><span class="sxs-lookup"><span data-stu-id="218c9-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="218c9-108">磁碟區容器具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="218c9-108">A volume container has the following attributes:</span></span>

* <span data-ttu-id="218c9-109">**磁碟區** – 磁碟區容器內所包含的分層 StorSimple 磁碟區或固定在本機的 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="218c9-109">**Volumes** – The tiered or locally pinned StorSimple volumes that are contained within the volume container.</span></span> <span data-ttu-id="218c9-110">一個磁碟區容器可以包含最多 256 個 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="218c9-110">A volume container may contain up to 256 StorSimple volumes.</span></span>
* <span data-ttu-id="218c9-111">**加密** – 可以為每個磁碟區容器定義的加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="218c9-111">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="218c9-112">此金鑰用於加密自 StorSimple 裝置傳送至雲端的資料。</span><span class="sxs-lookup"><span data-stu-id="218c9-112">This key is used for encrypting the data that is sent from your StorSimple device to the cloud.</span></span> <span data-ttu-id="218c9-113">軍事級的 AES-256 位元金鑰是搭配使用者輸入的金鑰使用。</span><span class="sxs-lookup"><span data-stu-id="218c9-113">A military-grade AES-256 bit key is used with the user-entered key.</span></span> <span data-ttu-id="218c9-114">為保護您的資料，建議您務必啟用雲端儲存體加密。</span><span class="sxs-lookup"><span data-stu-id="218c9-114">To secure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="218c9-115">**儲存體帳戶** – 連結至雲端儲存體服務提供者的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="218c9-115">**Storage account** – The storage account that is linked to your cloud storage service provider.</span></span> <span data-ttu-id="218c9-116">位於磁碟區容器中的所有磁碟區都會共用這個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="218c9-116">All the volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="218c9-117">當您建立磁碟區容器，然後指定該帳戶的存取認證時，可以從現有的清單中選擇一個儲存體帳戶，或建立新的帳戶。</span><span class="sxs-lookup"><span data-stu-id="218c9-117">You can choose a storage account from an existing list, or create a new account when you create the volume container and then specify the access credentials for that account.</span></span>
* <span data-ttu-id="218c9-118">**雲端頻寬** – 當資料從裝置傳送至雲端時裝置所耗用的頻寬。</span><span class="sxs-lookup"><span data-stu-id="218c9-118">**Cloud bandwidth** – The bandwidth consumed by the device when the data from the device is being sent to the cloud.</span></span> <span data-ttu-id="218c9-119">當您定義此容器時，可以指定一個介於 1 與 1000 Mbps 之間的值，以強制執行頻寬控制。</span><span class="sxs-lookup"><span data-stu-id="218c9-119">You can enforce a bandwidth control by specifying a value between 1 and 1000 Mbps when you define this container.</span></span> <span data-ttu-id="218c9-120">如果您希望裝置耗用所有可用的頻寬，將此欄位設定為 [無限制]。</span><span class="sxs-lookup"><span data-stu-id="218c9-120">If you want the device to consume all available bandwidth, set this field to Unlimited.</span></span> <span data-ttu-id="218c9-121">您也可以建立並套用頻寬範本，以便根據排程配置頻寬。</span><span class="sxs-lookup"><span data-stu-id="218c9-121">You can also create and apply a bandwidth template to allocate bandwidth based on schedule.</span></span>

![磁碟區容器頁面](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

<span data-ttu-id="218c9-123">以下程序說明如何使用 StorSimple 的 [磁碟區容器]  頁面，完成下列常見的作業：</span><span class="sxs-lookup"><span data-stu-id="218c9-123">This following procedures explain how to use the StorSimple **Volume containers** page to complete the following common operations:</span></span>

* <span data-ttu-id="218c9-124">新增磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="218c9-124">Add a volume container</span></span> 
* <span data-ttu-id="218c9-125">修改磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="218c9-125">Modify a volume container</span></span> 
* <span data-ttu-id="218c9-126">刪除磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="218c9-126">Delete a volume container</span></span> 

## <a name="add-a-volume-container"></a><span data-ttu-id="218c9-127">新增磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="218c9-127">Add a volume container</span></span>
<span data-ttu-id="218c9-128">執行下列步驟來新增磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="218c9-128">Perform the following steps to add a volume container.</span></span>

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="218c9-129">修改磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="218c9-129">Modify a volume container</span></span>
<span data-ttu-id="218c9-130">執行下列步驟來修改磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="218c9-130">Perform the following steps to modify a volume container.</span></span>

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="218c9-131">刪除磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="218c9-131">Delete a volume container</span></span>
<span data-ttu-id="218c9-132">磁碟區容器內具有磁碟區。</span><span class="sxs-lookup"><span data-stu-id="218c9-132">A volume container has volumes within it.</span></span> <span data-ttu-id="218c9-133">只有在先刪除磁碟區容器內包含的所有磁碟區之後，才可以刪除該磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="218c9-133">It can be deleted only if all the volumes contained in it are first deleted.</span></span> <span data-ttu-id="218c9-134">執行下列步驟來刪除磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="218c9-134">Perform the following steps to delete a volume container.</span></span>

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="218c9-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="218c9-135">Next steps</span></span>
* <span data-ttu-id="218c9-136">深入了解 [管理 StorSimple 磁碟區](storsimple-manage-volumes.md)。</span><span class="sxs-lookup"><span data-stu-id="218c9-136">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span> 
* <span data-ttu-id="218c9-137">深入了解 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="218c9-137">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>


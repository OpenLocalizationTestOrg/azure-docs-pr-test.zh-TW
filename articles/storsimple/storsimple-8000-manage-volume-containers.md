---
title: "管理 StorSimple 8000 系列裝置上的 StorSimple 磁碟區容器 | Microsoft Docs"
description: "說明如何使用 StorSimple 裝置管理員服務磁碟區容器頁面新增、修改或刪除磁碟區容器。"
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
ms.openlocfilehash: 0f8e00d6d07224f56625482f339e612e68914be2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-storsimple-volume-containers"></a><span data-ttu-id="03693-103">使用 StorSimple 裝置管理員服務管理 StorSimple 磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="03693-103">Use the StorSimple Device Manager service to manage StorSimple volume containers</span></span>

## <a name="overview"></a><span data-ttu-id="03693-104">概觀</span><span class="sxs-lookup"><span data-stu-id="03693-104">Overview</span></span>
<span data-ttu-id="03693-105">本教學課程說明如何使用 StorSimple 裝置管理員服務建立和管理 StorSimple 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="03693-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage StorSimple volume containers.</span></span>

<span data-ttu-id="03693-106">Microsoft Azure StorSimple 裝置中的磁碟區容器包含一個或多個可共用儲存體帳戶、加密和頻寬耗用量設定的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="03693-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="03693-107">一個裝置可以有多個磁碟區容器，供其所有磁碟區使用。</span><span class="sxs-lookup"><span data-stu-id="03693-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="03693-108">磁碟區容器具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="03693-108">A volume container has the following attributes:</span></span>

* <span data-ttu-id="03693-109">**磁碟區** – 磁碟區容器內所包含的分層 StorSimple 磁碟區或固定在本機的 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="03693-109">**Volumes** – The tiered or locally pinned StorSimple volumes that are contained within the volume container.</span></span> 
* <span data-ttu-id="03693-110">**加密** – 可以為每個磁碟區容器定義的加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="03693-110">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="03693-111">此金鑰用於加密自 StorSimple 裝置傳送至雲端的資料。</span><span class="sxs-lookup"><span data-stu-id="03693-111">This key is used for encrypting the data that is sent from your StorSimple device to the cloud.</span></span> <span data-ttu-id="03693-112">軍事級的 AES-256 位元金鑰是搭配使用者輸入的金鑰使用。</span><span class="sxs-lookup"><span data-stu-id="03693-112">A military-grade AES-256 bit key is used with the user-entered key.</span></span> <span data-ttu-id="03693-113">為保護您的資料，建議您務必啟用雲端儲存體加密。</span><span class="sxs-lookup"><span data-stu-id="03693-113">To secure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="03693-114">**儲存體帳戶** – Azure 儲存體帳戶用於儲存資料。</span><span class="sxs-lookup"><span data-stu-id="03693-114">**Storage account** – The Azure storage account that is used to store the data.</span></span> <span data-ttu-id="03693-115">位於磁碟區容器中的所有磁碟區都會共用這個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="03693-115">All the volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="03693-116">當您建立磁碟區容器，然後指定該帳戶的存取認證時，可以從現有的清單中選擇一個儲存體帳戶，或建立新的帳戶。</span><span class="sxs-lookup"><span data-stu-id="03693-116">You can choose a storage account from an existing list, or create a new account when you create the volume container and then specify the access credentials for that account.</span></span>
* <span data-ttu-id="03693-117">**雲端頻寬** – 當資料從裝置傳送至雲端時裝置所耗用的頻寬。</span><span class="sxs-lookup"><span data-stu-id="03693-117">**Cloud bandwidth** – The bandwidth consumed by the device when the data from the device is being sent to the cloud.</span></span> <span data-ttu-id="03693-118">當您建立此容器時，可以指定一個介於 1 Mbps 到 1000 Mbps 之間的值，以強制執行頻寬控制。</span><span class="sxs-lookup"><span data-stu-id="03693-118">You can enforce a bandwidth control by specifying a value between 1 Mbps and 1,000 Mbps when you create this container.</span></span> <span data-ttu-id="03693-119">如果您希望裝置耗用所有可用的頻寬，將此欄位設定為 [無限制]。</span><span class="sxs-lookup"><span data-stu-id="03693-119">If you want the device to consume all available bandwidth, set this field to **Unlimited**.</span></span> <span data-ttu-id="03693-120">您也可以建立並套用頻寬範本，以便根據排程配置頻寬。</span><span class="sxs-lookup"><span data-stu-id="03693-120">You can also create and apply a bandwidth template to allocate bandwidth based on schedule.</span></span>

<span data-ttu-id="03693-121">以下程序說明如何使用 StorSimple 的 [磁碟區容器] 刀鋒視窗，完成下列常見的作業：</span><span class="sxs-lookup"><span data-stu-id="03693-121">The following procedures explain how to use the StorSimple **Volume containers** blade to complete the following common operations:</span></span>

* <span data-ttu-id="03693-122">新增磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="03693-122">Add a volume container</span></span>
* <span data-ttu-id="03693-123">修改磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="03693-123">Modify a volume container</span></span>
* <span data-ttu-id="03693-124">刪除磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="03693-124">Delete a volume container</span></span>

## <a name="add-a-volume-container"></a><span data-ttu-id="03693-125">新增磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="03693-125">Add a volume container</span></span>
<span data-ttu-id="03693-126">執行下列步驟來新增磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="03693-126">Perform the following steps to add a volume container.</span></span>

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="03693-127">修改磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="03693-127">Modify a volume container</span></span>
<span data-ttu-id="03693-128">執行下列步驟來修改磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="03693-128">Perform the following steps to modify a volume container.</span></span>

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="03693-129">刪除磁碟區容器</span><span class="sxs-lookup"><span data-stu-id="03693-129">Delete a volume container</span></span>
<span data-ttu-id="03693-130">磁碟區容器內具有磁碟區。</span><span class="sxs-lookup"><span data-stu-id="03693-130">A volume container has volumes within it.</span></span> <span data-ttu-id="03693-131">只有在先刪除磁碟區容器內包含的所有磁碟區之後，才可以刪除該磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="03693-131">It can be deleted only if all the volumes contained in it are first deleted.</span></span> <span data-ttu-id="03693-132">執行下列步驟來刪除磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="03693-132">Perform the following steps to delete a volume container.</span></span>

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="03693-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="03693-133">Next steps</span></span>
* <span data-ttu-id="03693-134">深入了解 [管理 StorSimple 磁碟區](storsimple-8000-manage-volumes-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="03693-134">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span> 
* <span data-ttu-id="03693-135">深入了解[使用 StorSimple 裝置管理員服務管理 StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="03693-135">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>


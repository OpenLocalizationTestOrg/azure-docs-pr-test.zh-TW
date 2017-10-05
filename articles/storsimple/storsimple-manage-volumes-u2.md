---
title: "管理 StorSimple 磁碟區 (U2) | Microsoft Docs"
description: "說明如何加入、修改及監視 StorSimple 磁碟區，以及如何在必要時使其離線。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 57896932-0aa5-4805-970c-d13403ae7551
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 10/28/2016
ms.author: alkohli
ms.openlocfilehash: a61c57cd74a0df8363648dd8df40e433b0e6489d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-volumes-update-2"></a><span data-ttu-id="b6d68-103">使用 StorSimple Manager 服務來管理磁碟區 (Update 2)</span><span class="sxs-lookup"><span data-stu-id="b6d68-103">Use the StorSimple Manager service to manage volumes (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a><span data-ttu-id="b6d68-104">Overview</span><span class="sxs-lookup"><span data-stu-id="b6d68-104">Overview</span></span>
<span data-ttu-id="b6d68-105">本教學課程說明如何使用 StorSimple Manager 服務來建立和管理已安裝 Update 2 的 StorSimple 裝置與 StorSimple 虛擬裝置上的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-105">This tutorial explains how to use the StorSimple Manager service to create and manage volumes on the StorSimple device and StorSimple virtual device with Update 2 installed.</span></span>

<span data-ttu-id="b6d68-106">StorSimple Manager 服務是 Azure 傳統入口網站中的擴充功能，可讓您透過單一 Web 介面管理 StorSimple 解決方案。</span><span class="sxs-lookup"><span data-stu-id="b6d68-106">The StorSimple Manager service is an extension in the Azure classic portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="b6d68-107">除了管理磁碟區，您可以使用 StorSimple Manager 服務來建立和管理 StorSimple 服務、檢視和管理裝置、檢視警示，以及檢視和管理備份原則與備份類別目錄。</span><span class="sxs-lookup"><span data-stu-id="b6d68-107">In addition to managing volumes, you can use the StorSimple Manager service to create and manage StorSimple services, view and manage devices, view alerts, and view and manage backup policies and the backup catalog.</span></span>

## <a name="volume-types"></a><span data-ttu-id="b6d68-108">磁碟區類型</span><span class="sxs-lookup"><span data-stu-id="b6d68-108">Volume types</span></span>
<span data-ttu-id="b6d68-109">StorSimple 磁碟區可以是：</span><span class="sxs-lookup"><span data-stu-id="b6d68-109">StorSimple volumes can be:</span></span>

* <span data-ttu-id="b6d68-110">**固定在本機的磁碟區**：這些磁碟區中的資料隨時都會保留在本機 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="b6d68-110">**Locally pinned volumes**: Data in these volumes remains on the local StorSimple device at all times.</span></span>
* <span data-ttu-id="b6d68-111">**分層磁碟區**：這些磁碟區中的資料可以溢出至雲端。</span><span class="sxs-lookup"><span data-stu-id="b6d68-111">**Tiered volumes**: Data in these volumes can spill to the cloud.</span></span>

<span data-ttu-id="b6d68-112">封存的磁碟區是一種分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-112">An archival volume is a type of tiered volume.</span></span> <span data-ttu-id="b6d68-113">用於封存磁碟區的較大重複資料刪除區塊大小，可讓裝置將資料的較大區段傳輸至雲端。</span><span class="sxs-lookup"><span data-stu-id="b6d68-113">The larger deduplication chunk size used for archival volumes allows the device to transfer larger segments of data to the cloud.</span></span> 

<span data-ttu-id="b6d68-114">如果有需要，您可以將磁碟區類型從本機變更為分層或從分層變更為本機。</span><span class="sxs-lookup"><span data-stu-id="b6d68-114">If necessary, you can change the volume type from local to tiered or from tiered to local.</span></span> <span data-ttu-id="b6d68-115">如需詳細資訊，請移至 [變更磁碟區類型](#change-the-volume-type)。</span><span class="sxs-lookup"><span data-stu-id="b6d68-115">For more information, go to [Change the volume type](#change-the-volume-type).</span></span>

### <a name="locally-pinned-volumes"></a><span data-ttu-id="b6d68-116">固定在本機的磁碟區</span><span class="sxs-lookup"><span data-stu-id="b6d68-116">Locally pinned volumes</span></span>
<span data-ttu-id="b6d68-117">固定在本機的磁碟區是完整佈建的磁碟區，不會將資料分層至雲端，因此可以確保主要資料在本機當中，獨立於雲端連線之外。</span><span class="sxs-lookup"><span data-stu-id="b6d68-117">Locally pinned volumes are fully provisioned volumes that do not tier data to the cloud, thereby ensuring local guarantees for primary data, independent of cloud connectivity.</span></span> <span data-ttu-id="b6d68-118">固定在本機的磁碟區的資料不會進行重複資料刪除和壓縮，但是，固定在本機的磁碟區的快照會進行重複資料刪除。</span><span class="sxs-lookup"><span data-stu-id="b6d68-118">Data on locally pinned volumes is not deduplicated and compressed; however, snapshots of locally pinned volumes are deduplicated.</span></span> 

<span data-ttu-id="b6d68-119">固定在本機的磁碟區是完整佈建，因此，當您建立它們時，必須在裝置上有足夠的空間。</span><span class="sxs-lookup"><span data-stu-id="b6d68-119">Locally pinned volumes are fully provisioned; therefore, you must have sufficient space on your device when you create them.</span></span> <span data-ttu-id="b6d68-120">您可以在 StorSimple 8100 裝置上佈建大小高達 8 TB 且固定在本機的磁碟區，以及在 8600 裝置上佈建大小高達 20 TB 且固定在本機的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-120">You can provision locally pinned volumes up to a maximum size of 8 TB on the StorSimple 8100 device and 20 TB on the 8600 device.</span></span> <span data-ttu-id="b6d68-121">StorSimple 會為快照、中繼資料和資料處理在裝置上保留剩餘的本機空間。</span><span class="sxs-lookup"><span data-stu-id="b6d68-121">StorSimple reserves the remaining local space on the device for snapshots, metadata, and data processing.</span></span> <span data-ttu-id="b6d68-122">您可以將固定在本機的磁碟區大小增加到可用的最大空間，但是建立之後就不能減少磁碟區的大小。</span><span class="sxs-lookup"><span data-stu-id="b6d68-122">You can increase the size of a locally pinned volume to the maximum space available, but you cannot decrease the size of a volume once created.</span></span>

<span data-ttu-id="b6d68-123">當您建立固定在本機的磁碟區時，建立分層磁碟區的可用空間會減少。</span><span class="sxs-lookup"><span data-stu-id="b6d68-123">When you create a locally pinned volume, the available space for creation of tiered volumes is reduced.</span></span> <span data-ttu-id="b6d68-124">反之亦然：如果您有現有的分層磁碟區，可用於建立固定在本機的磁碟區的空間將會低於上述的最大限制。</span><span class="sxs-lookup"><span data-stu-id="b6d68-124">The reverse is also true: if you have existing tiered volumes, the space available for creating locally pinned volumes will be lower than the maximum limits stated above.</span></span> <span data-ttu-id="b6d68-125">如需有關本機磁碟區的詳細資訊，請參閱 [固定在本機的磁碟區常見問題集](storsimple-local-volume-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="b6d68-125">For more information on local volumes, refer to the [frequently asked questions on locally pinned volumes](storsimple-local-volume-faq.md).</span></span>   

### <a name="tiered-volumes"></a><span data-ttu-id="b6d68-126">分層磁碟區</span><span class="sxs-lookup"><span data-stu-id="b6d68-126">Tiered volumes</span></span>
<span data-ttu-id="b6d68-127">分層磁碟區是精簡佈建磁碟區，經常存取裝置上本機的資料，而較少使用的資料會自動分層至雲端。</span><span class="sxs-lookup"><span data-stu-id="b6d68-127">Tiered volumes are thinly provisioned volumes in which the frequently accessed data stays local on the device and less frequently used data is automatically tiered to the cloud.</span></span> <span data-ttu-id="b6d68-128">精簡佈建是一種虛擬化技術，精簡佈建中的可用儲存體會顯示超過實體資源。</span><span class="sxs-lookup"><span data-stu-id="b6d68-128">Thin provisioning is a virtualization technology in which available storage appears to exceed physical resources.</span></span> <span data-ttu-id="b6d68-129">與其預先保留足夠的儲存空間，StorSimple 會使用精簡佈建來配置剛好符合目前需求的足夠空間。</span><span class="sxs-lookup"><span data-stu-id="b6d68-129">Instead of reserving sufficient storage in advance, StorSimple uses thin provisioning to allocate just enough space to meet current requirements.</span></span> <span data-ttu-id="b6d68-130">雲端儲存體的彈性本質正好支援這種方法，因為 StorSimple 可以增加或減少雲端儲存體以符合不斷變更的需求。</span><span class="sxs-lookup"><span data-stu-id="b6d68-130">The elastic nature of cloud storage facilitates this approach because StorSimple can increase or decrease cloud storage to meet changing demands.</span></span>

<span data-ttu-id="b6d68-131">如果您針對封存資料使用分層磁碟區，選取 [使用此磁碟區存放不常存取的封存資料]  核取方塊會將您磁碟區的重複資料刪除區塊大小變更為 512 KB。</span><span class="sxs-lookup"><span data-stu-id="b6d68-131">If you are using the tiered volume for archival data, selecting the **Use this volume for less frequently accessed archival data** check box changes the deduplication chunk size for your volume to 512 KB.</span></span> <span data-ttu-id="b6d68-132">如果未核取此選項，對應的分層磁碟區會使用 64 KB 的區塊大小。</span><span class="sxs-lookup"><span data-stu-id="b6d68-132">If you do not select this option, the corresponding tiered volume will use a chunk size of 64 KB.</span></span> <span data-ttu-id="b6d68-133">較大的重複資料刪除區塊大小可讓裝置加速傳送大型封存資料到雲端。</span><span class="sxs-lookup"><span data-stu-id="b6d68-133">A larger deduplication chunk size allows the device to expedite the transfer of large archival data to the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="b6d68-134">使用 StorSimple Update 2 前版本所建立的封存磁碟區將會匯入為分層，且選取封存核取方塊。</span><span class="sxs-lookup"><span data-stu-id="b6d68-134">Archival volumes created with a pre-Update 2 version of StorSimple will be imported as tiered with the archival check box selected.</span></span>
> 
> 

### <a name="provisioned-capacity"></a><span data-ttu-id="b6d68-135">佈建的容量</span><span class="sxs-lookup"><span data-stu-id="b6d68-135">Provisioned capacity</span></span>
<span data-ttu-id="b6d68-136">請參閱下表以取得每個裝置與磁碟區類型的最大佈建容量。</span><span class="sxs-lookup"><span data-stu-id="b6d68-136">Refer to the following table for maximum provisioned capacity for each device and volume type.</span></span> <span data-ttu-id="b6d68-137">(請注意，固定在本機的磁碟區無法在虛擬裝置上使用。)</span><span class="sxs-lookup"><span data-stu-id="b6d68-137">(Note that locally pinned volumes are not available on a virtual device.)</span></span>

|  | <span data-ttu-id="b6d68-138">最大的分層磁碟區大小</span><span class="sxs-lookup"><span data-stu-id="b6d68-138">Maximum tiered volume size</span></span> | <span data-ttu-id="b6d68-139">最大的固定在本機的磁碟區大小</span><span class="sxs-lookup"><span data-stu-id="b6d68-139">Maximum locally pinned volume size</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b6d68-140">**實體裝置**</span><span class="sxs-lookup"><span data-stu-id="b6d68-140">**Physical devices**</span></span> | | |
| <span data-ttu-id="b6d68-141">8100</span><span class="sxs-lookup"><span data-stu-id="b6d68-141">8100</span></span> |<span data-ttu-id="b6d68-142">64 TB</span><span class="sxs-lookup"><span data-stu-id="b6d68-142">64 TB</span></span> |<span data-ttu-id="b6d68-143">8 TB</span><span class="sxs-lookup"><span data-stu-id="b6d68-143">8 TB</span></span> |
| <span data-ttu-id="b6d68-144">8600</span><span class="sxs-lookup"><span data-stu-id="b6d68-144">8600</span></span> |<span data-ttu-id="b6d68-145">64 TB</span><span class="sxs-lookup"><span data-stu-id="b6d68-145">64 TB</span></span> |<span data-ttu-id="b6d68-146">20 TB</span><span class="sxs-lookup"><span data-stu-id="b6d68-146">20 TB</span></span> |
| <span data-ttu-id="b6d68-147">**虛擬裝置**</span><span class="sxs-lookup"><span data-stu-id="b6d68-147">**Virtual devices**</span></span> | | |
| <span data-ttu-id="b6d68-148">8010</span><span class="sxs-lookup"><span data-stu-id="b6d68-148">8010</span></span> |<span data-ttu-id="b6d68-149">30 TB</span><span class="sxs-lookup"><span data-stu-id="b6d68-149">30 TB</span></span> |<span data-ttu-id="b6d68-150">N/A</span><span class="sxs-lookup"><span data-stu-id="b6d68-150">N/A</span></span> |
| <span data-ttu-id="b6d68-151">8020</span><span class="sxs-lookup"><span data-stu-id="b6d68-151">8020</span></span> |<span data-ttu-id="b6d68-152">64 TB</span><span class="sxs-lookup"><span data-stu-id="b6d68-152">64 TB</span></span> |<span data-ttu-id="b6d68-153">N/A</span><span class="sxs-lookup"><span data-stu-id="b6d68-153">N/A</span></span> |

## <a name="the-volumes-page"></a><span data-ttu-id="b6d68-154">[磁碟區] 頁面</span><span class="sxs-lookup"><span data-stu-id="b6d68-154">The Volumes page</span></span>
<span data-ttu-id="b6d68-155">您為啟動器 (伺服器) 佈建在 Microsoft Azure StorSimple 裝置的存放磁碟區，可以在 [磁碟區]  頁面管理 。</span><span class="sxs-lookup"><span data-stu-id="b6d68-155">The **Volumes** page allows you to manage the storage volumes that are provisioned on the Microsoft Azure StorSimple device for your initiators (servers).</span></span> <span data-ttu-id="b6d68-156">它會顯示 StorSimple 裝置上的磁碟區清單。</span><span class="sxs-lookup"><span data-stu-id="b6d68-156">It displays the list of volumes on your StorSimple device.</span></span>

 ![磁碟區頁面](./media/storsimple-manage-volumes-u2/VolumePage.png)

<span data-ttu-id="b6d68-158">磁碟區是由一系列屬性所組成：</span><span class="sxs-lookup"><span data-stu-id="b6d68-158">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="b6d68-159">**磁碟區名稱** – 必須是唯一且有助於識別磁碟區的描述性名稱。</span><span class="sxs-lookup"><span data-stu-id="b6d68-159">**Volume Name** – A descriptive name that must be unique and helps identify the volume.</span></span> <span data-ttu-id="b6d68-160">這個名稱也可在您篩選特定磁碟區時用於監視報告。</span><span class="sxs-lookup"><span data-stu-id="b6d68-160">This name is also used in monitoring reports when you filter on a specific volume.</span></span>
* <span data-ttu-id="b6d68-161">**狀態** – 可為連線或離線。</span><span class="sxs-lookup"><span data-stu-id="b6d68-161">**Status** – Can be online or offline.</span></span> <span data-ttu-id="b6d68-162">如果是離線的磁碟區，允許存取使用它的啟動器 (伺服器) 會看不到該磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-162">If a volume is offline, it is not visible to initiators (servers) that are allowed access to use the volume.</span></span>
* <span data-ttu-id="b6d68-163">**容量** – 指定啟動器 (伺服器) 可以儲存的總資料量。</span><span class="sxs-lookup"><span data-stu-id="b6d68-163">**Capacity** – specifies the total amount of data that can be stored by the initiator (server).</span></span> <span data-ttu-id="b6d68-164">固定在本機的磁碟區是完整佈建，而且位於 StorSimple 裝置上。</span><span class="sxs-lookup"><span data-stu-id="b6d68-164">Locally-pinned volumes are fully provisioned and reside on the StorSimple device.</span></span> <span data-ttu-id="b6d68-165">分層磁碟區是精簡佈建，而且資料會進行重複資料刪除。</span><span class="sxs-lookup"><span data-stu-id="b6d68-165">Tiered volumes are thinly provisioned and the data is deduplicated.</span></span> <span data-ttu-id="b6d68-166">使用精簡佈建磁碟區，您的裝置不會根據設定的磁碟區容量，在內部或在雲端預先配置實體儲存體容量。</span><span class="sxs-lookup"><span data-stu-id="b6d68-166">With thinly provisioned volumes, your device doesn’t pre-allocate physical storage capacity internally or on the cloud according to configured volume capacity.</span></span> <span data-ttu-id="b6d68-167">磁碟區容量會依需求來配置和耗用。</span><span class="sxs-lookup"><span data-stu-id="b6d68-167">The volume capacity is allocated and consumed on demand.</span></span>
* <span data-ttu-id="b6d68-168">**類型** – 指出磁碟區為「分層」(預設值) 或「固定在本機」。</span><span class="sxs-lookup"><span data-stu-id="b6d68-168">**Type** – Indicates whether the volume is **Tiered** (the default) or **Locally pinned**.</span></span>
* <span data-ttu-id="b6d68-169">**備份** – 指出磁碟區是否有預設的備份原則。</span><span class="sxs-lookup"><span data-stu-id="b6d68-169">**Backup** – Indicates whether a default backup policy exists for the volume.</span></span>
* <span data-ttu-id="b6d68-170">**存取** – 指定允許存取此磁碟區的啟動器 (伺服器)。</span><span class="sxs-lookup"><span data-stu-id="b6d68-170">**Access** – Specifies the initiators (servers) that are allowed access to this volume.</span></span> <span data-ttu-id="b6d68-171">啟動器不是與磁碟區相關聯的存取控制記錄 (ACR) 成員，就看不到磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-171">Initiators that are not members of access control record (ACR) that is associated with the volume will not see the volume.</span></span>
* <span data-ttu-id="b6d68-172">**監視** – 指定是否正在監視磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-172">**Monitoring** – Specifies whether or not a volume is being monitored.</span></span> <span data-ttu-id="b6d68-173">預設會在建立磁碟區時啟用監視。</span><span class="sxs-lookup"><span data-stu-id="b6d68-173">A volume will have monitoring enabled by default when it is created.</span></span> <span data-ttu-id="b6d68-174">不過，磁碟區複製會停用監視。</span><span class="sxs-lookup"><span data-stu-id="b6d68-174">Monitoring will, however, be disabled for a volume clone.</span></span> <span data-ttu-id="b6d68-175">若要啟用監視磁碟區，請依照 [監視磁碟區](#monitor-a-volume)中的指示執行。</span><span class="sxs-lookup"><span data-stu-id="b6d68-175">To enable monitoring for a volume, follow the instructions in [Monitor a volume](#monitor-a-volume).</span></span> 

<span data-ttu-id="b6d68-176">使用本教學課程中的指示以執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="b6d68-176">Use the instructions in this tutorial to perform the following tasks:</span></span>

* <span data-ttu-id="b6d68-177">新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="b6d68-177">Add a volume</span></span> 
* <span data-ttu-id="b6d68-178">修改磁碟區</span><span class="sxs-lookup"><span data-stu-id="b6d68-178">Modify a volume</span></span> 
* <span data-ttu-id="b6d68-179">變更磁碟區類型</span><span class="sxs-lookup"><span data-stu-id="b6d68-179">Change the volume type</span></span>
* <span data-ttu-id="b6d68-180">刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="b6d68-180">Delete a volume</span></span> 
* <span data-ttu-id="b6d68-181">使磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="b6d68-181">Take a volume offline</span></span> 
* <span data-ttu-id="b6d68-182">監視磁碟區</span><span class="sxs-lookup"><span data-stu-id="b6d68-182">Monitor a volume</span></span> 

## <a name="add-a-volume"></a><span data-ttu-id="b6d68-183">新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="b6d68-183">Add a volume</span></span>
<span data-ttu-id="b6d68-184">您已在部署 StorSimple 方案期間 [建立磁碟區](storsimple-deployment-walkthrough-u2.md#step-6-create-a-volume) 。</span><span class="sxs-lookup"><span data-stu-id="b6d68-184">You [created a volume](storsimple-deployment-walkthrough-u2.md#step-6-create-a-volume) during deployment of your StorSimple solution.</span></span> <span data-ttu-id="b6d68-185">新增磁碟區會是類似的程序。</span><span class="sxs-lookup"><span data-stu-id="b6d68-185">Adding a volume is a similar procedure.</span></span>

#### <a name="to-add-a-volume"></a><span data-ttu-id="b6d68-186">若要新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="b6d68-186">To add a volume</span></span>
1. <span data-ttu-id="b6d68-187">在 [裝置] 頁面中，選取並按兩下裝置，然後按一下 [磁碟區容器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b6d68-187">On the **Devices** page, select the device, double-click it, and then click the **Volume Containers** tab.</span></span>
2. <span data-ttu-id="b6d68-188">從清單中選取磁碟區容器，然後按兩下它以存取與該容器相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-188">Select a volume container from the list and double-click it to access the volumes associated with the container.</span></span>
3. <span data-ttu-id="b6d68-189">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="b6d68-189">Click **Add** at the bottom of the page.</span></span> <span data-ttu-id="b6d68-190">[新增磁碟區精靈] 隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="b6d68-190">The Add a volume wizard starts.</span></span>
   
     ![加入磁碟區精靈基本設定](./media/storsimple-manage-volumes-u2/TieredVolEx.png)
4. <span data-ttu-id="b6d68-192">在 [新增磁碟區精靈] 的 [基本設定] 下，執行列動作：</span><span class="sxs-lookup"><span data-stu-id="b6d68-192">In the Add a volume wizard, under **Basic Settings**, do the following:</span></span>
   
   1. <span data-ttu-id="b6d68-193">輸入磁碟區的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="b6d68-193">Supply a **Name** for your volume.</span></span>
   2. <span data-ttu-id="b6d68-194">從下拉式清單中選取 [使用類型]。</span><span class="sxs-lookup"><span data-stu-id="b6d68-194">Select a **Usage Type** from the drop-down list.</span></span> <span data-ttu-id="b6d68-195">對於需要資料在任何時間都可於裝置本機使用的工作負載，選取 [固定在本機]。</span><span class="sxs-lookup"><span data-stu-id="b6d68-195">For workloads that require data to be available locally on the device at all times, select **Locally Pinned**.</span></span> <span data-ttu-id="b6d68-196">對於所有其他資料類型，選取 [分層]。</span><span class="sxs-lookup"><span data-stu-id="b6d68-196">For all other types of data, select **Tiered**.</span></span> <span data-ttu-id="b6d68-197">(預設值是 [分層]。)</span><span class="sxs-lookup"><span data-stu-id="b6d68-197">(**Tiered** is the default.)</span></span>
   3. <span data-ttu-id="b6d68-198">如果您在步驟 2 中選取 [分層]，您可以選取 [使用此磁碟區存放不常存取的封存資料] 核取方塊以設定封存磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-198">If you selected **Tiered** in step 2, you can select the **Use this volume for less frequently accessed archival data** check box to configure an archival volume.</span></span>
   4. <span data-ttu-id="b6d68-199">為磁碟區輸入 [佈建的容量]  \(GB 或 TB)。</span><span class="sxs-lookup"><span data-stu-id="b6d68-199">Enter the **Provisioned Capacity** for your volume in GB or TB.</span></span> <span data-ttu-id="b6d68-200">請參閱 [佈建的容量](#provisioned-capacity) 以取得每個裝置與磁碟區類型的最大大小。</span><span class="sxs-lookup"><span data-stu-id="b6d68-200">See [Provisioned capacity](#provisioned-capacity) for maximum sizes for each device and volume type.</span></span> <span data-ttu-id="b6d68-201">查看 [可用容量]  來判斷您的裝置實際上有多少儲存體可用。</span><span class="sxs-lookup"><span data-stu-id="b6d68-201">Look at the **Available Capacity** to determine how much storage is actually available on your device.</span></span>
5. <span data-ttu-id="b6d68-202">按一下箭頭圖示 </span><span class="sxs-lookup"><span data-stu-id="b6d68-202">Click the arrow icon</span></span>![箭號圖示](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png)<span data-ttu-id="b6d68-204">。</span><span class="sxs-lookup"><span data-stu-id="b6d68-204">.</span></span> <span data-ttu-id="b6d68-205">如果您要設定固定在本機的磁碟區，您會看到下列訊息。</span><span class="sxs-lookup"><span data-stu-id="b6d68-205">If you are configuring a locally pinned volume, you will see the following message.</span></span>
   
    ![變更磁碟區類型訊息](./media/storsimple-manage-volumes-u2/LocalVolEx.png)
6. <span data-ttu-id="b6d68-207">再按一下箭頭圖示![箭頭圖示](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png)，前往 [其他設定] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b6d68-207">Click the arrow icon ![Arrow icon](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png)again to go to the **Additional Settings** page.</span></span>
   
    ![加入磁碟區精靈其他設定](./media/storsimple-manage-volumes-u2/AddVolume2.png)<br>
7. <span data-ttu-id="b6d68-209">在 [其他設定] 下，加入新的存取控制記錄 (ACR)：</span><span class="sxs-lookup"><span data-stu-id="b6d68-209">Under **Additional Settings**, add a new access control record (ACR):</span></span>
   
   1. <span data-ttu-id="b6d68-210">在下拉式清單中選取存取控制記錄 (ACR)。</span><span class="sxs-lookup"><span data-stu-id="b6d68-210">Select an access control record (ACR) from the drop-down list.</span></span> <span data-ttu-id="b6d68-211">或者，您可以加入新的 ACR。</span><span class="sxs-lookup"><span data-stu-id="b6d68-211">Alternatively, you can add a new ACR.</span></span> <span data-ttu-id="b6d68-212">ACR 會藉由比對主機與記錄中列出的 IQN 來決定哪些主機可以存取磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-212">ACRs determine which hosts can access your volumes by matching the host IQN with that listed in the record.</span></span> <span data-ttu-id="b6d68-213">如果您尚未指定 ACR，您會看到下列訊息。</span><span class="sxs-lookup"><span data-stu-id="b6d68-213">If you do not specify an ACR, you will see the following message.</span></span>
      
        ![指定 ACR](./media/storsimple-manage-volumes-u2/SpecifyACR.png)
   2. <span data-ttu-id="b6d68-215">建議選取 [啟用此磁碟區的預設備份]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="b6d68-215">We recommend that you select the **Enable a default backup for this volume** checkbox.</span></span>
   3. <span data-ttu-id="b6d68-216">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="b6d68-216">Click the check icon</span></span> ![核取圖示](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png) <span data-ttu-id="b6d68-218">，以利用指定的設定來建立磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-218">to create the volume with the specified settings.</span></span>

<span data-ttu-id="b6d68-219">新的磁碟區現在已備妥可供使用。</span><span class="sxs-lookup"><span data-stu-id="b6d68-219">Your new volume is now ready to use.</span></span>

> [!NOTE]
> <span data-ttu-id="b6d68-220">如果您建立固定在本機的磁碟區，然後立即建立另一個固定在本機的磁碟區，磁碟區建立作業會依序執行。</span><span class="sxs-lookup"><span data-stu-id="b6d68-220">If you create a locally pinned volume and then create another locally pinned volume immediately afterwards, the volume creation jobs run sequentially.</span></span> <span data-ttu-id="b6d68-221">必須先完成第一個磁碟區建立作業，才能開始下一個磁碟區建立作業。</span><span class="sxs-lookup"><span data-stu-id="b6d68-221">The first volume creation job must finish before the next volume creation job can begin.</span></span>
> 
> 

## <a name="modify-a-volume"></a><span data-ttu-id="b6d68-222">修改磁碟區</span><span class="sxs-lookup"><span data-stu-id="b6d68-222">Modify a volume</span></span>
<span data-ttu-id="b6d68-223">當您需要擴充磁碟區，或變更存取該磁碟區的主機時，請修改磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-223">Modify a volume when you need to expand it or change the hosts that access the volume.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="b6d68-224">如果您修改裝置上的磁碟區大小，也必須變更主機上的磁碟區大小。</span><span class="sxs-lookup"><span data-stu-id="b6d68-224">If you modify the volume size on the device, the volume size needs to be changed on the host as well.</span></span> 
> * <span data-ttu-id="b6d68-225">此處所述的主機端步驟適用於 Windows Server 2012 (2012R2)。</span><span class="sxs-lookup"><span data-stu-id="b6d68-225">The host-side steps described here are for Windows Server 2012 (2012R2).</span></span> <span data-ttu-id="b6d68-226">Linux 或其他主機作業系統的程序會有所不同。</span><span class="sxs-lookup"><span data-stu-id="b6d68-226">Procedures for Linux or other host operating systems will be different.</span></span> <span data-ttu-id="b6d68-227">如果要在執行其他作業系統的主機上修改磁碟區，請參考主機作業系統的指示。</span><span class="sxs-lookup"><span data-stu-id="b6d68-227">Refer to your host operating system instructions when modifying the volume on a host running another operating system.</span></span> 
> 
> 

#### <a name="to-modify-a-volume"></a><span data-ttu-id="b6d68-228">若要修改磁碟區</span><span class="sxs-lookup"><span data-stu-id="b6d68-228">To modify a volume</span></span>
1. <span data-ttu-id="b6d68-229">在 [裝置] 頁面中，選取並按兩下裝置，然後按一下 [磁碟區容器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b6d68-229">On the **Devices** page, select the device, double-click it, and then click the **Volume Containers** tab.</span></span>
2. <span data-ttu-id="b6d68-230">從清單中選取磁碟區容器，然後按兩下它以檢視與該容器相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-230">Select a volume container from the list and double-click it to view the volumes associated with the container.</span></span>
3. <span data-ttu-id="b6d68-231">選取磁碟區，然後按一下頁面底部的 [修改] 。</span><span class="sxs-lookup"><span data-stu-id="b6d68-231">Select a volume, and at the bottom of the page, click **Modify**.</span></span> <span data-ttu-id="b6d68-232">[修改磁碟區精靈] 隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="b6d68-232">The Modify volume wizard starts.</span></span>
4. <span data-ttu-id="b6d68-233">在 [修改磁碟區精靈] 的 [基本設定] 下，您可以執行列動作：</span><span class="sxs-lookup"><span data-stu-id="b6d68-233">In the Modify volume wizard, under **Basic Settings**, you can do the following:</span></span>
   
   * <span data-ttu-id="b6d68-234">編輯 [名稱] 。</span><span class="sxs-lookup"><span data-stu-id="b6d68-234">Edit the **Name**.</span></span>
   * <span data-ttu-id="b6d68-235">將 [使用類型]  從固定在本機轉換為分層，或從分層轉換為固定在本機 (如需詳細資訊，請參閱 [變更磁碟區類型](#change-the-volume-type) )。</span><span class="sxs-lookup"><span data-stu-id="b6d68-235">Convert the **Usage Type** from locally pinned to tiered or from tiered to locally pinned (see [Change the volume type](#change-the-volume-type) for more information).</span></span>
   * <span data-ttu-id="b6d68-236">增加 [佈建的容量] 。</span><span class="sxs-lookup"><span data-stu-id="b6d68-236">Increase the **Provisioned Capacity**.</span></span> <span data-ttu-id="b6d68-237">[佈建的容量]  只能增加。</span><span class="sxs-lookup"><span data-stu-id="b6d68-237">The **Provisioned Capacity** can only be increased.</span></span> <span data-ttu-id="b6d68-238">您無法在磁碟區建立後予以壓縮。</span><span class="sxs-lookup"><span data-stu-id="b6d68-238">You cannot shrink a volume after it is created.</span></span>
5. <span data-ttu-id="b6d68-239">在 [其他設定] 下，若是磁碟區已離線，您可以修改 ACR。</span><span class="sxs-lookup"><span data-stu-id="b6d68-239">Under **Additional Settings**, you can modify the ACR, provided that the volume is offline.</span></span> <span data-ttu-id="b6d68-240">如果磁碟區已連線，您必須先讓它離線。</span><span class="sxs-lookup"><span data-stu-id="b6d68-240">If the volume is online, you will need to take it offline first.</span></span> <span data-ttu-id="b6d68-241">修改 ACR 之前，請參閱 [使磁碟區離線](#take-a-volume-offline) 中的步驟。</span><span class="sxs-lookup"><span data-stu-id="b6d68-241">Refer to the steps in [Take a volume offline](#take-a-volume-offline) prior to modifying the ACR.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b6d68-242">您無法變更磁碟區的 [啟用預設備份] 選項。</span><span class="sxs-lookup"><span data-stu-id="b6d68-242">You cannot change the **Enable a default backup** option for the volume.</span></span>
   > 
   > 
6. <span data-ttu-id="b6d68-243">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="b6d68-243">Save your changes by clicking the check icon</span></span> ![核取圖示](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png)<span data-ttu-id="b6d68-245">。</span><span class="sxs-lookup"><span data-stu-id="b6d68-245">.</span></span> <span data-ttu-id="b6d68-246">Azure 傳統入口網站將會顯示更新磁碟區訊息。</span><span class="sxs-lookup"><span data-stu-id="b6d68-246">The Azure classic portal will display an updating volume message.</span></span> <span data-ttu-id="b6d68-247">如果磁碟區已成功更新，即會顯示成功訊息。</span><span class="sxs-lookup"><span data-stu-id="b6d68-247">It will display a success message when the volume has been successfully updated.</span></span>
7. <span data-ttu-id="b6d68-248">如果您要延伸磁碟區，請在 Windows 主機電腦上完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b6d68-248">If you are expanding a volume, complete the following steps on your Windows host computer:</span></span>
   
   1. <span data-ttu-id="b6d68-249">移至 [電腦管理]  ->[磁碟管理]。</span><span class="sxs-lookup"><span data-stu-id="b6d68-249">Go to **Computer Management** ->**Disk Management**.</span></span>
   2. <span data-ttu-id="b6d68-250">以滑鼠右鍵按一下 [磁碟管理]，並選取 [重新掃描磁碟]。</span><span class="sxs-lookup"><span data-stu-id="b6d68-250">Right-click **Disk Management** and select **Rescan Disks**.</span></span>
   3. <span data-ttu-id="b6d68-251">在磁碟清單中，選取您已更新的磁碟區，按一下滑鼠右鍵，然後選取 [延伸磁碟區] 。</span><span class="sxs-lookup"><span data-stu-id="b6d68-251">In the list of disks, select the volume that you updated, right-click, and then select **Extend Volume**.</span></span> <span data-ttu-id="b6d68-252">[延伸磁碟區精靈] 隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="b6d68-252">The Extend Volume wizard starts.</span></span> <span data-ttu-id="b6d68-253">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="b6d68-253">Click **Next**.</span></span>
   4. <span data-ttu-id="b6d68-254">使用預設值完成精靈。</span><span class="sxs-lookup"><span data-stu-id="b6d68-254">Complete the wizard, accepting the default values.</span></span> <span data-ttu-id="b6d68-255">完成精靈後，磁碟區應該會顯示增加的大小。</span><span class="sxs-lookup"><span data-stu-id="b6d68-255">After the wizard is finished, the volume should show the increased size.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="b6d68-256">如果您擴充固定在本機的磁碟區，然後立即擴充另一個固定在本機的磁碟區，磁碟區擴充作業會依序執行。</span><span class="sxs-lookup"><span data-stu-id="b6d68-256">If you expand a locally pinned volume and then expand another locally pinned volume immediately afterwards, the volume expansion jobs run sequentially.</span></span> <span data-ttu-id="b6d68-257">必須先完成第一個磁碟區擴充作業，才能開始下一個磁碟區擴充作業。</span><span class="sxs-lookup"><span data-stu-id="b6d68-257">The first volume expansion job must finish before the next volume expansion job can begin.</span></span>
      > 
      > 

<span data-ttu-id="b6d68-258">![提供的影片](./media/storsimple-manage-volumes-u2/Video_icon.png) **提供的影片**</span><span class="sxs-lookup"><span data-stu-id="b6d68-258">![Video available](./media/storsimple-manage-volumes-u2/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="b6d68-259">若要觀看影片示範如何擴充磁碟區，請按一下 [這裡](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/)。</span><span class="sxs-lookup"><span data-stu-id="b6d68-259">To watch a video that demonstrates how to expand a volume, click [here](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/).</span></span>

## <a name="change-the-volume-type"></a><span data-ttu-id="b6d68-260">變更磁碟區類型</span><span class="sxs-lookup"><span data-stu-id="b6d68-260">Change the volume type</span></span>
<span data-ttu-id="b6d68-261">您可以將磁碟區類型從分層變更為固定在本機或從固定在本機變更為分層。</span><span class="sxs-lookup"><span data-stu-id="b6d68-261">You can change the volume type from tiered to locally pinned or from locally pinned to tiered.</span></span> <span data-ttu-id="b6d68-262">不過，這種轉換不應該經常發生。</span><span class="sxs-lookup"><span data-stu-id="b6d68-262">However, this conversion should not be a frequent occurrence.</span></span> <span data-ttu-id="b6d68-263">將磁碟區從分層轉換為固定在本機的部分原因為：</span><span class="sxs-lookup"><span data-stu-id="b6d68-263">Some reasons for converting a volume from tiered to locally pinned are:</span></span>

* <span data-ttu-id="b6d68-264">關於資料可用性和效能的本機保證</span><span class="sxs-lookup"><span data-stu-id="b6d68-264">Local guarantees regarding data availability and performance</span></span>
* <span data-ttu-id="b6d68-265">消除雲端延遲和雲端連線問題。</span><span class="sxs-lookup"><span data-stu-id="b6d68-265">Elimination of cloud latencies and cloud connectivity issues.</span></span>

<span data-ttu-id="b6d68-266">通常，這些磁碟區是您想要經常存取的小的現有磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-266">Typically, these are small existing volumes that you want to access frequently.</span></span> <span data-ttu-id="b6d68-267">當固定在本機的磁碟區建立時，它就會完整佈建。</span><span class="sxs-lookup"><span data-stu-id="b6d68-267">A locally pinned volume is fully provisioned when it is created.</span></span> <span data-ttu-id="b6d68-268">如果您要將分層磁碟區轉換為固定在本機的磁碟區，StorSimple 會先確認您在裝置上有足夠的空間，再開始轉換。</span><span class="sxs-lookup"><span data-stu-id="b6d68-268">If you are converting a tiered volume to a locally pinned volume, StorSimple verifies that you have sufficient space on your device before it starts the conversion.</span></span> <span data-ttu-id="b6d68-269">如果您沒有足夠的空間，您會收到錯誤，且作業將會取消。</span><span class="sxs-lookup"><span data-stu-id="b6d68-269">If you have insufficient space, you will receive an error and the operation will be canceled.</span></span> 

> [!NOTE]
> <span data-ttu-id="b6d68-270">在您開始從分層轉換為固定在本機之前，請確定您為其他工作負載考量空間需求。</span><span class="sxs-lookup"><span data-stu-id="b6d68-270">Before you begin a conversion from tiered to locally pinned, make sure that you consider the space requirements of your other workloads.</span></span> 
> 
> 

<span data-ttu-id="b6d68-271">如果您需要額外空間來佈建其他磁碟區，您可能想要將固定在本機的磁碟區變更為分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-271">You might want to change a locally pinned volume to a tiered volume if you need additional space to provision other volumes.</span></span> <span data-ttu-id="b6d68-272">當您將固定在本機的磁碟區轉換為分層時，裝置上的可用容量會隨著釋放的容量大小增加。</span><span class="sxs-lookup"><span data-stu-id="b6d68-272">When you convert the locally pinned volume to tiered, the available capacity on the device increases by the size of the released capacity.</span></span> <span data-ttu-id="b6d68-273">如果連線問題讓磁碟區無法從本機類型轉換為分層類型，本機磁碟區會展示分層磁碟區的屬性，直到完成轉換為止。</span><span class="sxs-lookup"><span data-stu-id="b6d68-273">If connectivity issues prevent the conversion of a volume from the local type to the tiered type, the local volume will exhibit properties of a tiered volume until the conversion is completed.</span></span> <span data-ttu-id="b6d68-274">這是因為可能有部分資料溢出到雲端。</span><span class="sxs-lookup"><span data-stu-id="b6d68-274">This is because some data might have spilled to the cloud.</span></span> <span data-ttu-id="b6d68-275">此溢出的資料將繼續佔用裝置上的本機空間，無法釋放，直到重新啟動並完成作業。</span><span class="sxs-lookup"><span data-stu-id="b6d68-275">This spilled data will continue to occupy local space on the device that cannot be freed until the operation is restarted and completed.</span></span>

> [!NOTE]
> <span data-ttu-id="b6d68-276">轉換磁碟區可能需要一些時間，且您在啟動之後無法取消轉換。</span><span class="sxs-lookup"><span data-stu-id="b6d68-276">Converting a volume can take some time and you cannot cancel a conversion after it starts.</span></span> <span data-ttu-id="b6d68-277">磁碟區在轉換時仍然保持連線，您可以建立備份，但是您無法在轉換正在進行時擴充或還原磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-277">The volume remains online during the conversion, and you can take backups, but you cannot expand or restore the volume while the conversion is taking place.</span></span>  
> 
> 

<span data-ttu-id="b6d68-278">從階層式轉換成固定在本機的磁碟區，可能會對裝置效能產生負面影響。</span><span class="sxs-lookup"><span data-stu-id="b6d68-278">Conversion from a tiered to a locally pinned volume can adversely affect device performance.</span></span> <span data-ttu-id="b6d68-279">此外，下列因素可能會增加完成轉換所需的時間：</span><span class="sxs-lookup"><span data-stu-id="b6d68-279">Additionally, the following factors might increase the time it takes to complete the conversion:</span></span>

* <span data-ttu-id="b6d68-280">頻寬不足。</span><span class="sxs-lookup"><span data-stu-id="b6d68-280">There is insufficient bandwidth.</span></span>
* <span data-ttu-id="b6d68-281">沒有最新備份。</span><span class="sxs-lookup"><span data-stu-id="b6d68-281">There is no current backup.</span></span>

<span data-ttu-id="b6d68-282">若要將這些因素可能造成的影響降到最低：</span><span class="sxs-lookup"><span data-stu-id="b6d68-282">To minimize the effects that these factors may have:</span></span>

* <span data-ttu-id="b6d68-283">請檢閱頻寬節流設定原則，並確認有專用的 40 Mbps 頻寬。</span><span class="sxs-lookup"><span data-stu-id="b6d68-283">Review your bandwidth throttling policies and make sure that a dedicated 40 Mbps bandwidth is available.</span></span>
* <span data-ttu-id="b6d68-284">將轉換排在離峰時間。</span><span class="sxs-lookup"><span data-stu-id="b6d68-284">Schedule the conversion for off-peak hours.</span></span>
* <span data-ttu-id="b6d68-285">在開始轉換之前，請先建立雲端快照。</span><span class="sxs-lookup"><span data-stu-id="b6d68-285">Take a cloud snapshot before you start the conversion.</span></span>

<span data-ttu-id="b6d68-286">如果您要轉換多個磁碟區 (支援不同的工作負載)，您應該設定磁碟區轉換的優先權，讓優先權較高的磁碟區先行轉換。</span><span class="sxs-lookup"><span data-stu-id="b6d68-286">If you are converting multiple volumes (supporting different workloads), then you should prioritize the volume conversion so that higher priority volumes are converted first.</span></span> <span data-ttu-id="b6d68-287">例如，您應該先轉換裝載虛擬機器 (VM) 的磁碟區，或具有 SQL 工作負載的磁碟區，然後才轉換檔案共用工作負載的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-287">For example, you should convert volumes that host virtual machines (VMs) or volumes with SQL workloads before you convert volumes with file share workloads.</span></span>

#### <a name="to-change-the-volume-type"></a><span data-ttu-id="b6d68-288">變更磁碟區類型</span><span class="sxs-lookup"><span data-stu-id="b6d68-288">To change the volume type</span></span>
1. <span data-ttu-id="b6d68-289">在 [裝置] 頁面中，選取並按兩下裝置，然後按一下 [磁碟區容器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b6d68-289">On the **Devices** page, select the device, double-click it, and then click the **Volume Containers** tab.</span></span>
2. <span data-ttu-id="b6d68-290">從清單中選取磁碟區容器，然後按兩下它以檢視與該容器相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-290">Select a volume container from the list and double-click it to view the volumes associated with the container.</span></span>
3. <span data-ttu-id="b6d68-291">選取磁碟區，然後按一下頁面底部的 [修改] 。</span><span class="sxs-lookup"><span data-stu-id="b6d68-291">Select a volume, and at the bottom of the page, click **Modify**.</span></span> <span data-ttu-id="b6d68-292">[修改磁碟區精靈] 隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="b6d68-292">The Modify volume wizard starts.</span></span>
4. <span data-ttu-id="b6d68-293">在 [基本設定] 頁面上，從 [使用類型] 下拉式清單選取新的類型，以變更使用類型。</span><span class="sxs-lookup"><span data-stu-id="b6d68-293">On the **Basic Settings** page, change the usage type by selecting the new type from the **Usage Type** drop-down list.</span></span>
   
   * <span data-ttu-id="b6d68-294">如果您將類型變更為 [固定在本機] ，StorSimple 會檢查是否有足夠的容量。</span><span class="sxs-lookup"><span data-stu-id="b6d68-294">If you are changing the type to **Locally pinned**, StorSimple will check to see if there is sufficient capacity.</span></span>
   * <span data-ttu-id="b6d68-295">如果您將類型變更為 [分層]，且此磁碟區將會用於封存資料，請選取 [使用此磁碟區存放不常存取的封存資料] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="b6d68-295">If you are changing the type to **Tiered** and this volume will be used for archival data, select the **Use this volume for less frequently accessed archival data** check box.</span></span>
     
       ![封存核取方塊](./media/storsimple-manage-volumes-u2/ModifyTieredVolEx.png)
5. <span data-ttu-id="b6d68-297">按一下箭頭圖示![箭頭圖示](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png)，前往 [其他設定] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b6d68-297">Click the arrow icon ![Arrow icon](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png) to go to the **Additional Settings** page.</span></span> <span data-ttu-id="b6d68-298">如果您要設定固定在本機的磁碟區，將會顯示下列訊息。</span><span class="sxs-lookup"><span data-stu-id="b6d68-298">If you are configuring a locally pinned volume, the following message appears.</span></span>
   
    ![變更磁碟區類型訊息](./media/storsimple-manage-volumes-u2/ModifyLocalVolEx.png)
6. <span data-ttu-id="b6d68-300">按一下箭頭圖示 </span><span class="sxs-lookup"><span data-stu-id="b6d68-300">Click the arrow icon</span></span> ![箭號圖示](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png) <span data-ttu-id="b6d68-302">以繼續。</span><span class="sxs-lookup"><span data-stu-id="b6d68-302">again to continue.</span></span>
7. <span data-ttu-id="b6d68-303">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="b6d68-303">Click the check icon</span></span> ![核取圖示](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png) <span data-ttu-id="b6d68-305">以開始轉換程序。</span><span class="sxs-lookup"><span data-stu-id="b6d68-305">to start the conversion process.</span></span> <span data-ttu-id="b6d68-306">Azure 入口網站將會顯示更新磁碟區訊息。</span><span class="sxs-lookup"><span data-stu-id="b6d68-306">The Azure portal will display an updating volume message.</span></span> <span data-ttu-id="b6d68-307">如果磁碟區已成功更新，即會顯示成功訊息。</span><span class="sxs-lookup"><span data-stu-id="b6d68-307">It will display a success message when the volume has been successfully updated.</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="b6d68-308">使磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="b6d68-308">Take a volume offline</span></span>
<span data-ttu-id="b6d68-309">您想要修改或刪除磁碟區時，可能需要先使其離線。</span><span class="sxs-lookup"><span data-stu-id="b6d68-309">You may need to take a volume offline when you are planning to modify it or delete it.</span></span> <span data-ttu-id="b6d68-310">當磁碟區離線時，即無法進行讀寫存取。</span><span class="sxs-lookup"><span data-stu-id="b6d68-310">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="b6d68-311">您必須使主機與裝置上的磁碟區同時離線。</span><span class="sxs-lookup"><span data-stu-id="b6d68-311">You will need to take the volume offline on the host as well as on the device.</span></span> 

#### <a name="to-take-a-volume-offline"></a><span data-ttu-id="b6d68-312">若要使磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="b6d68-312">To take a volume offline</span></span>
1. <span data-ttu-id="b6d68-313">請確定有問題的磁碟區不在使用中後，再使其離線。</span><span class="sxs-lookup"><span data-stu-id="b6d68-313">Make sure that the volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="b6d68-314">先使主機上的磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="b6d68-314">Take the volume offline on the host first.</span></span> <span data-ttu-id="b6d68-315">這樣做可以排除任何會造成磁碟區上資料損毀的潛在風險。</span><span class="sxs-lookup"><span data-stu-id="b6d68-315">This eliminates any potential risk of data corruption on the volume.</span></span> <span data-ttu-id="b6d68-316">如需特定步驟，請參閱主機作業系統的指示。</span><span class="sxs-lookup"><span data-stu-id="b6d68-316">For specific steps, refer to the instructions for your host operating system.</span></span>
3. <span data-ttu-id="b6d68-317">在主機離線之後，請執行下列步驟以使裝置上的磁碟區離線：</span><span class="sxs-lookup"><span data-stu-id="b6d68-317">After the host is offline, take the volume on the device offline by performing the following steps:</span></span>
   
   1. <span data-ttu-id="b6d68-318">在 [裝置] 頁面中，選取並按兩下裝置，然後按一下 [磁碟區容器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b6d68-318">On the **Devices** page, select the device, double-click it, and then click the **Volume Containers** tab.</span></span> <span data-ttu-id="b6d68-319">[磁碟區容器]  索引標籤會以表格列出與裝置相關聯的所有磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="b6d68-319">The **Volume Containers** tab lists in a tabular format all the volume containers that are associated with the device.</span></span>
   2. <span data-ttu-id="b6d68-320">選取並按一下磁碟區容器，以清單顯示該容器內的所有磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-320">Select a volume container and click it to display the list of all the volumes within the container.</span></span>
   3. <span data-ttu-id="b6d68-321">選取磁碟區，然後按一下 [離線] 。</span><span class="sxs-lookup"><span data-stu-id="b6d68-321">Select a volume and click **Take offline**.</span></span>
   4. <span data-ttu-id="b6d68-322">系統提示您進行確認時，按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="b6d68-322">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="b6d68-323">磁碟區現在應已離線。</span><span class="sxs-lookup"><span data-stu-id="b6d68-323">The volume should now be offline.</span></span>
      
      <span data-ttu-id="b6d68-324">磁碟區離線之後，[上線]  選項就會變成可用。</span><span class="sxs-lookup"><span data-stu-id="b6d68-324">After a volume is offline, the **Bring Online** option becomes available.</span></span>

> [!NOTE]
> <span data-ttu-id="b6d68-325">[離線] 命令會將要求傳送到裝置，以使磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="b6d68-325">The **Take Offline** command sends a request to the device to take the volume offline.</span></span> <span data-ttu-id="b6d68-326">如果主機仍在使用該磁碟區，這會導致連線中斷，但是使磁碟區離線不會失敗。</span><span class="sxs-lookup"><span data-stu-id="b6d68-326">If hosts are still using the volume, this results in broken connections, but taking the volume offline will not fail.</span></span> 
> 
> 

## <a name="delete-a-volume"></a><span data-ttu-id="b6d68-327">刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="b6d68-327">Delete a volume</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b6d68-328">只有當磁碟區離線時，您才能予以刪除。</span><span class="sxs-lookup"><span data-stu-id="b6d68-328">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="b6d68-329">請完成下列步驟來刪除磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-329">Complete the following steps to delete a volume.</span></span>

#### <a name="to-delete-a-volume"></a><span data-ttu-id="b6d68-330">若要刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="b6d68-330">To delete a volume</span></span>
1. <span data-ttu-id="b6d68-331">在 [裝置] 頁面中，選取並按兩下裝置，然後按一下 [磁碟區容器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b6d68-331">On the **Devices** page, select the device, double-click it, and then click the **Volume Containers** tab.</span></span>
2. <span data-ttu-id="b6d68-332">選取含有您想要刪除之磁碟區的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="b6d68-332">Select the volume container that has the volume you want to delete.</span></span> <span data-ttu-id="b6d68-333">按一下該磁碟區容器，即可存取 [磁碟區]  頁面。</span><span class="sxs-lookup"><span data-stu-id="b6d68-333">Click the volume container to access the **Volumes** page.</span></span>
3. <span data-ttu-id="b6d68-334">與這個容器相關聯的所有磁碟區會以表格顯示。</span><span class="sxs-lookup"><span data-stu-id="b6d68-334">All the volumes associated with this container are displayed in a tabular format.</span></span> <span data-ttu-id="b6d68-335">檢查您想要刪除之磁碟區的狀態。</span><span class="sxs-lookup"><span data-stu-id="b6d68-335">Check the status of the volume you want to delete.</span></span> <span data-ttu-id="b6d68-336">如果您想要刪除的磁碟區未離線，請先使其離線，請依照 [使磁碟區離線](#take-a-volume-offline)中的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="b6d68-336">If the volume you want to delete is not offline, take it offline first, following the steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="b6d68-337">在磁碟區離線之後，按一下頁面底部的 [刪除]  。</span><span class="sxs-lookup"><span data-stu-id="b6d68-337">After the volume is offline, click **Delete** at the bottom of the page.</span></span>
5. <span data-ttu-id="b6d68-338">系統提示您進行確認時，按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="b6d68-338">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="b6d68-339">現已刪除磁碟區，而 [磁碟區]  頁面會顯示容器內已更新的磁碟區清單。</span><span class="sxs-lookup"><span data-stu-id="b6d68-339">The volume will now be deleted and the **Volumes** page will show the updated list of volumes within the container.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b6d68-340">如果您刪除固定在本機的磁碟區，新的磁碟區的可用空間可能不會立即更新。</span><span class="sxs-lookup"><span data-stu-id="b6d68-340">If you delete a locally pinned volume, the space available for new volumes may not be updated immediately.</span></span> <span data-ttu-id="b6d68-341">StorSimple Manager 服務會定期更新本機可用空間。</span><span class="sxs-lookup"><span data-stu-id="b6d68-341">The StorSimple Manager Service updates the local space available periodically.</span></span> <span data-ttu-id="b6d68-342">建議您等候幾分鐘，然後再嘗試建立新的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-342">We suggest you wait for a few minutes before you try to create the new volume.</span></span><br> <span data-ttu-id="b6d68-343">此外，如果您刪除固定在本機的磁碟區，然後立即刪除另一個固定在本機的磁碟區，磁碟區刪除作業會依序執行。</span><span class="sxs-lookup"><span data-stu-id="b6d68-343">Additionally, if you delete a locally pinned volume and then delete another locally pinned volume immediately afterwards, the volume deletion jobs run sequentially.</span></span> <span data-ttu-id="b6d68-344">必須先完成第一個磁碟區刪除作業，才能開始下一個磁碟區刪除作業。</span><span class="sxs-lookup"><span data-stu-id="b6d68-344">The first volume deletion job must finish before the next volume deletion job can begin.</span></span>
   > 
   > 

## <a name="monitor-a-volume"></a><span data-ttu-id="b6d68-345">監視磁碟區</span><span class="sxs-lookup"><span data-stu-id="b6d68-345">Monitor a volume</span></span>
<span data-ttu-id="b6d68-346">監視磁碟區可讓您為磁碟區收集 I/O 相關的統計資料。</span><span class="sxs-lookup"><span data-stu-id="b6d68-346">Volume monitoring allows you to collect I/O-related statistics for a volume.</span></span> <span data-ttu-id="b6d68-347">根據預設，您建立的前 32 個磁碟區會啟用監視。</span><span class="sxs-lookup"><span data-stu-id="b6d68-347">Monitoring is enabled by default for the first 32 volumes that you create.</span></span> <span data-ttu-id="b6d68-348">預設會停用監視其他磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-348">Monitoring of additional volumes is disabled by default.</span></span> <span data-ttu-id="b6d68-349">預設也會停用監視複製的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-349">Monitoring of cloned volumes is also disabled by default.</span></span>

<span data-ttu-id="b6d68-350">請執行下列步驟來啟用或停用監視磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-350">Perform the following steps to enable or disable monitoring for a volume.</span></span>

#### <a name="to-enable-or-disable-volume-monitoring"></a><span data-ttu-id="b6d68-351">若要啟用或停用監視磁碟區</span><span class="sxs-lookup"><span data-stu-id="b6d68-351">To enable or disable volume monitoring</span></span>
1. <span data-ttu-id="b6d68-352">在 [裝置] 頁面中，選取並按兩下裝置，然後按一下 [磁碟區容器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b6d68-352">On the **Devices** page, select the device, double-click it, and then click the **Volume Containers** tab.</span></span>
2. <span data-ttu-id="b6d68-353">選取磁碟區所在的磁碟區容器，然後按一下該磁碟區容器來存取 [磁碟區]  頁面。</span><span class="sxs-lookup"><span data-stu-id="b6d68-353">Select the volume container in which the volume resides, and then click the volume container to access the **Volumes** page.</span></span>
3. <span data-ttu-id="b6d68-354">以表格顯示所列出與這個容器相關聯的所有磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b6d68-354">All the volumes associated with this container are listed in the tabular display.</span></span> <span data-ttu-id="b6d68-355">按一下並選取磁碟區或磁碟區複製。</span><span class="sxs-lookup"><span data-stu-id="b6d68-355">Click and select the volume or volume clone.</span></span>
4. <span data-ttu-id="b6d68-356">按一下頁面底部的 [修改] 。</span><span class="sxs-lookup"><span data-stu-id="b6d68-356">At the bottom of the page, click **Modify**.</span></span>
5. <span data-ttu-id="b6d68-357">在 [修改磁碟區精靈] 的 [基本設定] 下，從 [監視] 下拉式清單中選取 [啟用] 或 [停用]。</span><span class="sxs-lookup"><span data-stu-id="b6d68-357">In the Modify Volume wizard, under **Basic Settings**, select **Enable** or **Disable** from the **Monitoring** drop-down list.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6d68-358">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b6d68-358">Next steps</span></span>
* <span data-ttu-id="b6d68-359">了解如何 [複製 StorSimple 磁碟區](storsimple-clone-volume.md)。</span><span class="sxs-lookup"><span data-stu-id="b6d68-359">Learn how to [clone a StorSimple volume](storsimple-clone-volume.md).</span></span>
* <span data-ttu-id="b6d68-360">了解如何 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="b6d68-360">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>


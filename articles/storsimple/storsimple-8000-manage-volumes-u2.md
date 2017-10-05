---
title: "管理 StorSimple 磁碟區 (Update 3) | Microsoft Docs"
description: "說明如何加入、修改及監視 StorSimple 磁碟區，以及如何在必要時使其離線。"
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
ms.workload: NA
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 09f4de79ab9b0cdfafd10c7c7c29b0f8e6304f14
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-volumes-update-3-or-later"></a><span data-ttu-id="ec9df-103">使用 StorSimple 裝置管理員服務來管理磁碟區 (Update 3 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="ec9df-103">Use the StorSimple Device Manager service to manage volumes (Update 3 or later)</span></span>

## <a name="overview"></a><span data-ttu-id="ec9df-104">概觀</span><span class="sxs-lookup"><span data-stu-id="ec9df-104">Overview</span></span>

<span data-ttu-id="ec9df-105">本教學課程說明如何使用 StorSimple 裝置管理員服務來建立和管理執行 Update 3 和更新版本之 StorSimple 8000 系列裝置上的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage volumes on the StorSimple 8000 series devices running Update 3 and later.</span></span>

<span data-ttu-id="ec9df-106">StorSimple 裝置管理員服務是 Azure 入口網站中的一項擴充，可讓您從單一 Web 介面來管理 StorSimple 解決方案。</span><span class="sxs-lookup"><span data-stu-id="ec9df-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="ec9df-107">您可以使用 Azure 入口網站來管理所有裝置上的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-107">Use the Azure portal to manage volumes on all your devices.</span></span> <span data-ttu-id="ec9df-108">您也可以建立和管理 StorSimple 服務、管理裝置、備份原則，以及備份類別目錄，並檢視警示。</span><span class="sxs-lookup"><span data-stu-id="ec9df-108">You can also create and manage StorSimple services, manage devices, backup policies, and backup catalog, and view alerts.</span></span>

## <a name="volume-types"></a><span data-ttu-id="ec9df-109">磁碟區類型</span><span class="sxs-lookup"><span data-stu-id="ec9df-109">Volume types</span></span>

<span data-ttu-id="ec9df-110">StorSimple 磁碟區可以是：</span><span class="sxs-lookup"><span data-stu-id="ec9df-110">StorSimple volumes can be:</span></span>

* <span data-ttu-id="ec9df-111">**固定在本機的磁碟區**：這些磁碟區中的資料隨時都會保留在本機 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="ec9df-111">**Locally pinned volumes**: Data in these volumes remains on the local StorSimple device at all times.</span></span>
* <span data-ttu-id="ec9df-112">**分層磁碟區**：這些磁碟區中的資料可以溢出至雲端。</span><span class="sxs-lookup"><span data-stu-id="ec9df-112">**Tiered volumes**: Data in these volumes can spill to the cloud.</span></span>

<span data-ttu-id="ec9df-113">封存的磁碟區是一種分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-113">An archival volume is a type of tiered volume.</span></span> <span data-ttu-id="ec9df-114">用於封存磁碟區的較大重複資料刪除區塊大小，可讓裝置將資料的較大區段傳輸至雲端。</span><span class="sxs-lookup"><span data-stu-id="ec9df-114">The larger deduplication chunk size used for archival volumes allows the device to transfer larger segments of data to the cloud.</span></span>

<span data-ttu-id="ec9df-115">如果有需要，您可以將磁碟區類型從本機變更為分層或從分層變更為本機。</span><span class="sxs-lookup"><span data-stu-id="ec9df-115">If necessary, you can change the volume type from local to tiered or from tiered to local.</span></span> <span data-ttu-id="ec9df-116">如需詳細資訊，請移至 [變更磁碟區類型](#change-the-volume-type)。</span><span class="sxs-lookup"><span data-stu-id="ec9df-116">For more information, go to [Change the volume type](#change-the-volume-type).</span></span>

### <a name="locally-pinned-volumes"></a><span data-ttu-id="ec9df-117">固定在本機的磁碟區</span><span class="sxs-lookup"><span data-stu-id="ec9df-117">Locally pinned volumes</span></span>

<span data-ttu-id="ec9df-118">固定在本機的磁碟區是完整佈建的磁碟區，不會將資料分層至雲端，因此可以確保主要資料在本機當中，獨立於雲端連線之外。</span><span class="sxs-lookup"><span data-stu-id="ec9df-118">Locally pinned volumes are fully provisioned volumes that do not tier data to the cloud, thereby ensuring local guarantees for primary data, independent of cloud connectivity.</span></span> <span data-ttu-id="ec9df-119">固定在本機的磁碟區的資料不會進行重複資料刪除和壓縮，但是，固定在本機的磁碟區的快照會進行重複資料刪除。</span><span class="sxs-lookup"><span data-stu-id="ec9df-119">Data on locally pinned volumes is not deduplicated and compressed; however, snapshots of locally pinned volumes are deduplicated.</span></span> 

<span data-ttu-id="ec9df-120">固定在本機的磁碟區是完整佈建，因此，當您建立它們時，必須在裝置上有足夠的空間。</span><span class="sxs-lookup"><span data-stu-id="ec9df-120">Locally pinned volumes are fully provisioned; therefore, you must have sufficient space on your device when you create them.</span></span> <span data-ttu-id="ec9df-121">您可以在 StorSimple 8100 裝置上佈建大小高達 8 TB 且固定在本機的磁碟區，以及在 8600 裝置上佈建大小高達 20 TB 且固定在本機的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-121">You can provision locally pinned volumes up to a maximum size of 8 TB on the StorSimple 8100 device and 20 TB on the 8600 device.</span></span> <span data-ttu-id="ec9df-122">StorSimple 會為快照、中繼資料和資料處理在裝置上保留剩餘的本機空間。</span><span class="sxs-lookup"><span data-stu-id="ec9df-122">StorSimple reserves the remaining local space on the device for snapshots, metadata, and data processing.</span></span> <span data-ttu-id="ec9df-123">您可以將固定在本機的磁碟區大小增加到可用的最大空間，但是建立之後就不能減少磁碟區的大小。</span><span class="sxs-lookup"><span data-stu-id="ec9df-123">You can increase the size of a locally pinned volume to the maximum space available, but you cannot decrease the size of a volume once created.</span></span>

<span data-ttu-id="ec9df-124">當您建立固定在本機的磁碟區時，建立分層磁碟區的可用空間會減少。</span><span class="sxs-lookup"><span data-stu-id="ec9df-124">When you create a locally pinned volume, the available space for creation of tiered volumes is reduced.</span></span> <span data-ttu-id="ec9df-125">反之亦然：如果您有現有的分層磁碟區，可用於建立固定在本機的磁碟區的空間將會低於上述的最大限制。</span><span class="sxs-lookup"><span data-stu-id="ec9df-125">The reverse is also true: if you have existing tiered volumes, the space available for creating locally pinned volumes will be lower than the maximum limits stated above.</span></span> <span data-ttu-id="ec9df-126">如需有關本機磁碟區的詳細資訊，請參閱 [固定在本機的磁碟區常見問題集](storsimple-8000-local-volume-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="ec9df-126">For more information on local volumes, refer to the [frequently asked questions on locally pinned volumes](storsimple-8000-local-volume-faq.md).</span></span>

### <a name="tiered-volumes"></a><span data-ttu-id="ec9df-127">分層磁碟區</span><span class="sxs-lookup"><span data-stu-id="ec9df-127">Tiered volumes</span></span>

<span data-ttu-id="ec9df-128">分層磁碟區是精簡佈建磁碟區，經常存取裝置上本機的資料，而較少使用的資料會自動分層至雲端。</span><span class="sxs-lookup"><span data-stu-id="ec9df-128">Tiered volumes are thinly provisioned volumes in which the frequently accessed data stays local on the device and less frequently used data is automatically tiered to the cloud.</span></span> <span data-ttu-id="ec9df-129">精簡佈建是一種虛擬化技術，精簡佈建中的可用儲存體會顯示超過實體資源。</span><span class="sxs-lookup"><span data-stu-id="ec9df-129">Thin provisioning is a virtualization technology in which available storage appears to exceed physical resources.</span></span> <span data-ttu-id="ec9df-130">與其預先保留足夠的儲存空間，StorSimple 會使用精簡佈建來配置剛好符合目前需求的足夠空間。</span><span class="sxs-lookup"><span data-stu-id="ec9df-130">Instead of reserving sufficient storage in advance, StorSimple uses thin provisioning to allocate just enough space to meet current requirements.</span></span> <span data-ttu-id="ec9df-131">雲端儲存體的彈性本質正好支援這種方法，因為 StorSimple 可以增加或減少雲端儲存體以符合不斷變更的需求。</span><span class="sxs-lookup"><span data-stu-id="ec9df-131">The elastic nature of cloud storage facilitates this approach because StorSimple can increase or decrease cloud storage to meet changing demands.</span></span>

<span data-ttu-id="ec9df-132">如果您針對封存資料使用分層磁碟區，請選取 [使用此磁碟區存放不常存取的封存資料] 核取方塊，以將您磁碟區的重複資料刪除區塊大小變更為 512 KB。</span><span class="sxs-lookup"><span data-stu-id="ec9df-132">If you are using the tiered volume for archival data, select the **Use this volume for less frequently accessed archival data** check box to change the deduplication chunk size for your volume to 512 KB.</span></span> <span data-ttu-id="ec9df-133">如果未核取此選項，對應的分層磁碟區會使用 64 KB 的區塊大小。</span><span class="sxs-lookup"><span data-stu-id="ec9df-133">If you do not select this option, the corresponding tiered volume will use a chunk size of 64 KB.</span></span> <span data-ttu-id="ec9df-134">較大的重複資料刪除區塊大小可讓裝置加速傳送大型封存資料到雲端。</span><span class="sxs-lookup"><span data-stu-id="ec9df-134">A larger deduplication chunk size allows the device to expedite the transfer of large archival data to the cloud.</span></span>


### <a name="provisioned-capacity"></a><span data-ttu-id="ec9df-135">佈建的容量</span><span class="sxs-lookup"><span data-stu-id="ec9df-135">Provisioned capacity</span></span>

<span data-ttu-id="ec9df-136">請參閱下表以取得每個裝置與磁碟區類型的最大佈建容量。</span><span class="sxs-lookup"><span data-stu-id="ec9df-136">Refer to the following table for maximum provisioned capacity for each device and volume type.</span></span> <span data-ttu-id="ec9df-137">(請注意，固定在本機的磁碟區無法在虛擬裝置上使用。)</span><span class="sxs-lookup"><span data-stu-id="ec9df-137">(Note that locally pinned volumes are not available on a virtual device.)</span></span>

|  | <span data-ttu-id="ec9df-138">最大的分層磁碟區大小</span><span class="sxs-lookup"><span data-stu-id="ec9df-138">Maximum tiered volume size</span></span> | <span data-ttu-id="ec9df-139">最大的固定在本機的磁碟區大小</span><span class="sxs-lookup"><span data-stu-id="ec9df-139">Maximum locally pinned volume size</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ec9df-140">**實體裝置**</span><span class="sxs-lookup"><span data-stu-id="ec9df-140">**Physical devices**</span></span> | | |
| <span data-ttu-id="ec9df-141">8100</span><span class="sxs-lookup"><span data-stu-id="ec9df-141">8100</span></span> |<span data-ttu-id="ec9df-142">64 TB</span><span class="sxs-lookup"><span data-stu-id="ec9df-142">64 TB</span></span> |<span data-ttu-id="ec9df-143">8 TB</span><span class="sxs-lookup"><span data-stu-id="ec9df-143">8 TB</span></span> |
| <span data-ttu-id="ec9df-144">8600</span><span class="sxs-lookup"><span data-stu-id="ec9df-144">8600</span></span> |<span data-ttu-id="ec9df-145">64 TB</span><span class="sxs-lookup"><span data-stu-id="ec9df-145">64 TB</span></span> |<span data-ttu-id="ec9df-146">20 TB</span><span class="sxs-lookup"><span data-stu-id="ec9df-146">20 TB</span></span> |
| <span data-ttu-id="ec9df-147">**虛擬裝置**</span><span class="sxs-lookup"><span data-stu-id="ec9df-147">**Virtual devices**</span></span> | | |
| <span data-ttu-id="ec9df-148">8010</span><span class="sxs-lookup"><span data-stu-id="ec9df-148">8010</span></span> |<span data-ttu-id="ec9df-149">30 TB</span><span class="sxs-lookup"><span data-stu-id="ec9df-149">30 TB</span></span> |<span data-ttu-id="ec9df-150">N/A</span><span class="sxs-lookup"><span data-stu-id="ec9df-150">N/A</span></span> |
| <span data-ttu-id="ec9df-151">8020</span><span class="sxs-lookup"><span data-stu-id="ec9df-151">8020</span></span> |<span data-ttu-id="ec9df-152">64 TB</span><span class="sxs-lookup"><span data-stu-id="ec9df-152">64 TB</span></span> |<span data-ttu-id="ec9df-153">N/A</span><span class="sxs-lookup"><span data-stu-id="ec9df-153">N/A</span></span> |

## <a name="the-volumes-blade"></a><span data-ttu-id="ec9df-154">[磁碟區] 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="ec9df-154">The volumes blade</span></span>

<span data-ttu-id="ec9df-155">[磁碟區] 刀鋒視窗可讓您管理為啟動器 (伺服器) 佈建在 Microsoft Azure StorSimple 裝置的存放磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-155">The **Volumes** blade allows you to manage the storage volumes that are provisioned on the Microsoft Azure StorSimple device for your initiators (servers).</span></span> <span data-ttu-id="ec9df-156">該視窗會顯示連接至服務之 StorSimple 裝置上的磁碟區清單。</span><span class="sxs-lookup"><span data-stu-id="ec9df-156">It displays the list of volumes on the StorSimple devices connected to your service.</span></span>

 ![磁碟區頁面](./media/storsimple-8000-manage-volumes-u2/volumeslist.png)

<span data-ttu-id="ec9df-158">磁碟區是由一系列屬性所組成：</span><span class="sxs-lookup"><span data-stu-id="ec9df-158">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="ec9df-159">**磁碟區名稱** – 必須是唯一且有助於識別磁碟區的描述性名稱。</span><span class="sxs-lookup"><span data-stu-id="ec9df-159">**Volume Name** – A descriptive name that must be unique and helps identify the volume.</span></span> <span data-ttu-id="ec9df-160">這個名稱也可在您篩選特定磁碟區時用於監視報告。</span><span class="sxs-lookup"><span data-stu-id="ec9df-160">This name is also used in monitoring reports when you filter on a specific volume.</span></span> <span data-ttu-id="ec9df-161">磁碟區一旦建立，便無法重新命名。</span><span class="sxs-lookup"><span data-stu-id="ec9df-161">Once the volume is created, it cannot be renamed.</span></span>
* <span data-ttu-id="ec9df-162">**狀態** – 可為連線或離線。</span><span class="sxs-lookup"><span data-stu-id="ec9df-162">**Status** – Can be online or offline.</span></span> <span data-ttu-id="ec9df-163">如果是離線的磁碟區，允許存取使用它的啟動器 (伺服器) 會看不到該磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-163">If a volume is offline, it is not visible to initiators (servers) that are allowed access to use the volume.</span></span>
* <span data-ttu-id="ec9df-164">**容量** – 指定啟動器 (伺服器) 可以儲存的總資料量。</span><span class="sxs-lookup"><span data-stu-id="ec9df-164">**Capacity** – specifies the total amount of data that can be stored by the initiator (server).</span></span> <span data-ttu-id="ec9df-165">固定在本機的磁碟區是完整佈建，而且位於 StorSimple 裝置上。</span><span class="sxs-lookup"><span data-stu-id="ec9df-165">Locally-pinned volumes are fully provisioned and reside on the StorSimple device.</span></span> <span data-ttu-id="ec9df-166">分層磁碟區是精簡佈建，而且資料會進行重複資料刪除。</span><span class="sxs-lookup"><span data-stu-id="ec9df-166">Tiered volumes are thinly provisioned and the data is deduplicated.</span></span> <span data-ttu-id="ec9df-167">使用精簡佈建磁碟區，您的裝置不會根據設定的磁碟區容量，在內部或在雲端預先配置實體儲存體容量。</span><span class="sxs-lookup"><span data-stu-id="ec9df-167">With thinly provisioned volumes, your device doesn’t pre-allocate physical storage capacity internally or on the cloud according to configured volume capacity.</span></span> <span data-ttu-id="ec9df-168">磁碟區容量會依需求來配置和耗用。</span><span class="sxs-lookup"><span data-stu-id="ec9df-168">The volume capacity is allocated and consumed on demand.</span></span>
* <span data-ttu-id="ec9df-169">**類型** – 指出磁碟區為「分層」(預設值) 或「固定在本機」。</span><span class="sxs-lookup"><span data-stu-id="ec9df-169">**Type** – Indicates whether the volume is **Tiered** (the default) or **Locally pinned**.</span></span>

<span data-ttu-id="ec9df-170">使用本教學課程中的指示以執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="ec9df-170">Use the instructions in this tutorial to perform the following tasks:</span></span>

* <span data-ttu-id="ec9df-171">新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="ec9df-171">Add a volume</span></span> 
* <span data-ttu-id="ec9df-172">修改磁碟區</span><span class="sxs-lookup"><span data-stu-id="ec9df-172">Modify a volume</span></span> 
* <span data-ttu-id="ec9df-173">變更磁碟區類型</span><span class="sxs-lookup"><span data-stu-id="ec9df-173">Change the volume type</span></span>
* <span data-ttu-id="ec9df-174">刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="ec9df-174">Delete a volume</span></span> 
* <span data-ttu-id="ec9df-175">使磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="ec9df-175">Take a volume offline</span></span> 
* <span data-ttu-id="ec9df-176">監視磁碟區</span><span class="sxs-lookup"><span data-stu-id="ec9df-176">Monitor a volume</span></span> 

## <a name="add-a-volume"></a><span data-ttu-id="ec9df-177">新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="ec9df-177">Add a volume</span></span>

<span data-ttu-id="ec9df-178">您已在部署 StorSimple 8000 系列裝置期間[建立磁碟區](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume)。</span><span class="sxs-lookup"><span data-stu-id="ec9df-178">You [created a volume](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume) during deployment of your StorSimple 8000 series device.</span></span> <span data-ttu-id="ec9df-179">新增磁碟區會是類似的程序。</span><span class="sxs-lookup"><span data-stu-id="ec9df-179">Adding a volume is a similar procedure.</span></span>

#### <a name="to-add-a-volume"></a><span data-ttu-id="ec9df-180">若要新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="ec9df-180">To add a volume</span></span>

1. <span data-ttu-id="ec9df-181">從 [裝置] 刀鋒視窗的表格式裝置清單中，選取您的裝置。</span><span class="sxs-lookup"><span data-stu-id="ec9df-181">From the tabular listing of the devices in the **Devices** blade, select your device.</span></span> <span data-ttu-id="ec9df-182">按一下 [+ 新增磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-182">Click **+ Add volume**.</span></span>

    ![新增磁碟區](./media/storsimple-8000-manage-volumes-u2/step5createvol1.png)

2. <span data-ttu-id="ec9df-184">在 [新增磁碟區] 刀鋒視窗中︰</span><span class="sxs-lookup"><span data-stu-id="ec9df-184">In the **Add a volume** blade:</span></span>
   
    1. <span data-ttu-id="ec9df-185">您目前的裝置會自動填入 [選取裝置] 欄位。</span><span class="sxs-lookup"><span data-stu-id="ec9df-185">The **Select device** field is automatically populated with your current device.</span></span>

    2. <span data-ttu-id="ec9df-186">從下拉式清單中，選取您需要新增磁碟區的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="ec9df-186">From the drop-down list, select the volume container where you need to add a volume.</span></span>

    3.  <span data-ttu-id="ec9df-187">輸入磁碟區的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="ec9df-187">Type a **Name** for your volume.</span></span> <span data-ttu-id="ec9df-188">一旦建立磁碟區，則無法重新命名磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-188">Once the volume is created, you cannot rename the volume.</span></span>

    4. <span data-ttu-id="ec9df-189">在下拉式清單中，為磁碟區選取 [類型]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-189">On the drop-down list, select the **Type** for your volume.</span></span> <span data-ttu-id="ec9df-190">需要本機保證、低延遲，以及高效能的工作負載，請選取 [固定在本機]  磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-190">For workloads that require local guarantees, low latencies, and higher performance, select a **Locally pinned** volume.</span></span> <span data-ttu-id="ec9df-191">針對所有其他資料，請選取 [分層]  磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-191">For all other data, select a **Tiered** volume.</span></span> <span data-ttu-id="ec9df-192">如果您將此磁碟區用於封存資料，請核取 [將此磁碟區用於較不常存取的封存資料] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="ec9df-192">If you are using this volume for archival data, check **Use this volume for less frequently accessed archival data**.</span></span>
      
       <span data-ttu-id="ec9df-193">分層磁碟區已精簡佈建，而且可以快速地建立。</span><span class="sxs-lookup"><span data-stu-id="ec9df-193">A tiered volume is thinly provisioned and can be created quickly.</span></span> <span data-ttu-id="ec9df-194">針對以封存資料為目標的分層磁碟區，選取 [使用此磁碟區存放不常存取的封存資料]  會將您磁碟區的重複資料刪除區塊大小變更為 512 KB。</span><span class="sxs-lookup"><span data-stu-id="ec9df-194">Selecting **Use this volume for less frequently accessed archival data** for tiered volume targeted for archival data changes the deduplication chunk size for your volume to 512 KB.</span></span> <span data-ttu-id="ec9df-195">如果未核取此欄位，對應的分層磁碟區會使用 64 KB 的區塊大小。</span><span class="sxs-lookup"><span data-stu-id="ec9df-195">If this field is not checked, the corresponding tiered volume uses a chunk size of 64 KB.</span></span> <span data-ttu-id="ec9df-196">較大的重複資料刪除區塊大小可讓裝置加速傳送大型封存資料到雲端。</span><span class="sxs-lookup"><span data-stu-id="ec9df-196">A larger deduplication chunk size allows the device to expedite the transfer of large archival data to the cloud.</span></span>
       
       <span data-ttu-id="ec9df-197">固定在本機之磁碟區會大量佈建，並確保磁碟區上的主要資料會保留在本機裝置，而不會散至雲端。</span><span class="sxs-lookup"><span data-stu-id="ec9df-197">A locally pinned volume is thickly provisioned and ensures that the primary data on the volume stays local to the device and does not spill to the cloud.</span></span>  <span data-ttu-id="ec9df-198">如果您建立固定在本機之磁碟區，裝置便會檢查本機層上的可用空間，以佈建要求大小的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-198">If you create a locally pinned volume, the device checks for available space on the local tiers to provision the volume of the requested size.</span></span> <span data-ttu-id="ec9df-199">建立固定在本機之磁碟區的作業可能牽涉從裝置溢出資料至雲端，且建立磁碟區所花費的時間可能會很長。</span><span class="sxs-lookup"><span data-stu-id="ec9df-199">The operation of creating a locally pinned volume may involve spilling existing data from the device to the cloud and the time taken to create the volume may be long.</span></span> <span data-ttu-id="ec9df-200">總時間取決於已佈建的磁碟區大小、可用的網路頻寬和您裝置上的資料。</span><span class="sxs-lookup"><span data-stu-id="ec9df-200">The total time depends on the size of the provisioned volume, available network bandwidth, and the data on your device.</span></span>

    5. <span data-ttu-id="ec9df-201">為磁碟區指定 [佈建的容量]  。</span><span class="sxs-lookup"><span data-stu-id="ec9df-201">Specify the **Provisioned Capacity** for your volume.</span></span> <span data-ttu-id="ec9df-202">請記下根據選取的磁碟區類型的可用容量。</span><span class="sxs-lookup"><span data-stu-id="ec9df-202">Make a note of the capacity that is available based on the volume type selected.</span></span> <span data-ttu-id="ec9df-203">指定的磁碟區大小不得超過可用的空間。</span><span class="sxs-lookup"><span data-stu-id="ec9df-203">The specified volume size must not exceed the available space.</span></span>
      
       <span data-ttu-id="ec9df-204">您可以在 8100 裝置上佈建最多 8.5 TB 且固定在本機的磁碟區，或者最多 200 TB 的分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-204">You can provision locally pinned volumes up to 8.5 TB or tiered volumes up to 200 TB on the 8100 device.</span></span> <span data-ttu-id="ec9df-205">在較大的 8600 裝置上，您可以佈建最多 22.5 TB 的本機固定磁碟區，或者最多 500 TB 的階層式磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-205">On the larger 8600 device, you can provision locally pinned volumes up to 22.5 TB or tiered volumes up to 500 TB.</span></span> <span data-ttu-id="ec9df-206">因為需要本機裝置上的空間來裝載分層磁碟區的工作集，建立固定到本機磁碟區會影響佈建分層磁碟區的可用空間。</span><span class="sxs-lookup"><span data-stu-id="ec9df-206">As local space on the device is required to host the working set of tiered volumes, creation of locally pinned volumes impacts the space available for provisioning tiered volumes.</span></span> <span data-ttu-id="ec9df-207">因此，如果您建立固定在本機的磁碟區，建立分層磁碟區的可用空間就會縮小。</span><span class="sxs-lookup"><span data-stu-id="ec9df-207">Therefore, if you create a locally pinned volume, space available for creation of tiered volumes is reduced.</span></span> <span data-ttu-id="ec9df-208">同樣地，如果建立分層磁碟區，建立固定在本機的磁碟區的可用空間就會縮小。</span><span class="sxs-lookup"><span data-stu-id="ec9df-208">Similarly, if a tiered volume is created, the available space for creation of locally pinned volumes is reduced.</span></span>
      
       <span data-ttu-id="ec9df-209">如果您在 8100 裝置上佈建 8.5 TB (允許的大小上限) 且固定在本機的磁碟區，則您會用盡裝置上所有可用的本機空間。</span><span class="sxs-lookup"><span data-stu-id="ec9df-209">If you provision a locally pinned volume of 8.5 TB (maximum allowable size) on your 8100 device, then you have exhausted all the local space available on the device.</span></span> <span data-ttu-id="ec9df-210">從那時起，您就無法建立任何分層磁碟區，因為裝置上已沒有任何本機空間，可用來裝載分層磁碟區的工作集。</span><span class="sxs-lookup"><span data-stu-id="ec9df-210">You can't create any tiered volume from that point onwards as there is no local space on the device to host the working set of the tiered volume.</span></span> <span data-ttu-id="ec9df-211">現有的分層磁碟區也會影響可用的空間。</span><span class="sxs-lookup"><span data-stu-id="ec9df-211">Existing tiered volumes also affect the space available.</span></span> <span data-ttu-id="ec9df-212">例如，如果您的 8100 裝置已經有大約 106 TB 的分層磁碟區，則固定在本機的磁碟區僅只有 4 TB 的可用空間。</span><span class="sxs-lookup"><span data-stu-id="ec9df-212">For example, if you have an 8100 device that already has tiered volumes of roughly 106 TB, only 4 TB of space is available for locally pinned volumes.</span></span>

    6. <span data-ttu-id="ec9df-213">在 [已連線的主機] 欄位中，按一下箭號。</span><span class="sxs-lookup"><span data-stu-id="ec9df-213">In the **Connected hosts** field, click the arrow.</span></span> 

        ![已連線的主機](./media/storsimple-8000-manage-volumes-u2/step5createvol2.png)

    7. <span data-ttu-id="ec9df-215">在 [已連線的主機] 刀鋒視窗中，選擇現有的 ACR 或新的 ACR。</span><span class="sxs-lookup"><span data-stu-id="ec9df-215">In the **Connected hosts** blade, choose an existing ACR or add a new ACR.</span></span> <span data-ttu-id="ec9df-216">如果您選擇新的 ACR，請提供 ACR 的 [名稱]，並提供 Windows 主機的 [iSCSI 限定名稱]\(IQN)。</span><span class="sxs-lookup"><span data-stu-id="ec9df-216">If you choose a new ACR, then supply a **Name** for your ACR, provide the **iSCSI Qualified Name** (IQN) of your Windows host.</span></span> <span data-ttu-id="ec9df-217">如果沒有 IQN，請移至 [取得 Windows Server 主機的 IQN] [](#get-the-iqn-of-a-windows-server-host)。</span><span class="sxs-lookup"><span data-stu-id="ec9df-217">If you don't have the IQN, go to [Get the IQN of a Windows Server host](#get-the-iqn-of-a-windows-server-host).</span></span> <span data-ttu-id="ec9df-218">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ec9df-218">Click **Create**.</span></span> <span data-ttu-id="ec9df-219">使用指定的設定來建立磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-219">A volume is created with the specified settings.</span></span>

        ![Click Create](./media/storsimple-8000-manage-volumes-u2/step5createvol3.png)

<span data-ttu-id="ec9df-221">新的磁碟區現在已備妥可供使用。</span><span class="sxs-lookup"><span data-stu-id="ec9df-221">Your new volume is now ready to use.</span></span>

> [!NOTE]
> <span data-ttu-id="ec9df-222">如果您建立固定在本機的磁碟區，然後立即建立另一個固定在本機的磁碟區，磁碟區建立作業會依序執行。</span><span class="sxs-lookup"><span data-stu-id="ec9df-222">If you create a locally pinned volume and then create another locally pinned volume immediately afterwards, the volume creation jobs run sequentially.</span></span> <span data-ttu-id="ec9df-223">必須先完成第一個磁碟區建立作業，才能開始下一個磁碟區建立作業。</span><span class="sxs-lookup"><span data-stu-id="ec9df-223">The first volume creation job must finish before the next volume creation job can begin.</span></span>

## <a name="modify-a-volume"></a><span data-ttu-id="ec9df-224">修改磁碟區</span><span class="sxs-lookup"><span data-stu-id="ec9df-224">Modify a volume</span></span>

<span data-ttu-id="ec9df-225">當您需要擴充磁碟區，或變更存取該磁碟區的主機時，請修改磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-225">Modify a volume when you need to expand it or change the hosts that access the volume.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="ec9df-226">如果您修改裝置上的磁碟區大小，也必須變更主機上的磁碟區大小。</span><span class="sxs-lookup"><span data-stu-id="ec9df-226">If you modify the volume size on the device, the volume size needs to be changed on the host as well.</span></span>
> * <span data-ttu-id="ec9df-227">此處所述的主機端步驟適用於 Windows Server 2012 (2012R2)。</span><span class="sxs-lookup"><span data-stu-id="ec9df-227">The host-side steps described here are for Windows Server 2012 (2012R2).</span></span> <span data-ttu-id="ec9df-228">Linux 或其他主機作業系統的程序會有所不同。</span><span class="sxs-lookup"><span data-stu-id="ec9df-228">Procedures for Linux or other host operating systems will be different.</span></span> <span data-ttu-id="ec9df-229">如果要在執行其他作業系統的主機上修改磁碟區，請參考主機作業系統的指示。</span><span class="sxs-lookup"><span data-stu-id="ec9df-229">Refer to your host operating system instructions when modifying the volume on a host running another operating system.</span></span>

#### <a name="to-modify-a-volume"></a><span data-ttu-id="ec9df-230">若要修改磁碟區</span><span class="sxs-lookup"><span data-stu-id="ec9df-230">To modify a volume</span></span>

1. <span data-ttu-id="ec9df-231">移至 StorSimple 裝置管理員服務，然後按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-231">Go to your StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="ec9df-232">從裝置的表格式清單中，選取您想要修改磁碟區的裝置。</span><span class="sxs-lookup"><span data-stu-id="ec9df-232">From the tabular listing of the devices, select the device that has the volume that you intend to modify.</span></span> <span data-ttu-id="ec9df-233">按一下 [設定] > [磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-233">Click **Settings > Volumes**.</span></span>

    ![移至 [磁碟區] 刀鋒視窗](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

2. <span data-ttu-id="ec9df-235">從磁碟區的表格式清單中，選取磁碟區，然後按一下滑鼠右鍵以叫用操作功能表。</span><span class="sxs-lookup"><span data-stu-id="ec9df-235">From the tabular listing of volumes, select the volume and right-click to invoke the context menu.</span></span> <span data-ttu-id="ec9df-236">選取 [離線]，讓您要修改的磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="ec9df-236">Select **Take offline** to take the volume you will modify offline.</span></span>

    ![選取並讓磁碟區離線](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. <span data-ttu-id="ec9df-238">在 [離線] 刀鋒視窗中，檢閱讓磁碟區離線的影響，並選取對應的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="ec9df-238">In the **Take offline** blade, review the impact of taking the volume offline and select the corresponding checkbox.</span></span> <span data-ttu-id="ec9df-239">請先確認主機上的對應磁碟區為離線狀態。</span><span class="sxs-lookup"><span data-stu-id="ec9df-239">Ensure that the corresponding volume on the host is offline first.</span></span> <span data-ttu-id="ec9df-240">如需更多資訊以瞭解如何將連線到 StorSimple 之主機伺服器上的磁碟區離線，請參閱作業系統特定指示。</span><span class="sxs-lookup"><span data-stu-id="ec9df-240">For information on how to take a volume offline on your host server connected to StorSimple, refer to operating system specific instructions.</span></span> <span data-ttu-id="ec9df-241">按一下 [離線]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-241">Click **Take offline**.</span></span>

    ![檢閱讓磁碟區離線的影響](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

4. <span data-ttu-id="ec9df-243">磁碟區離線之後 (如磁碟區狀態所示)，請選取磁碟區，並按一下滑鼠右鍵以叫用操作功能表。</span><span class="sxs-lookup"><span data-stu-id="ec9df-243">After the volume is offline (as shown by the volume status), select the volume and right-click to invoke the context menu.</span></span> <span data-ttu-id="ec9df-244">選取 [修改磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-244">Select **Modify volume**.</span></span>

    ![選取 [修改磁碟區]](./media/storsimple-8000-manage-volumes-u2/modifyvol9.png)


5. <span data-ttu-id="ec9df-246">在 [修改磁碟區] 刀鋒視窗中，可以進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="ec9df-246">In the **Modify volume** blade, you can make the following changes:</span></span>
   
   1. <span data-ttu-id="ec9df-247">無法編輯磁碟區的 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-247">The volume **Name** cannot be edited.</span></span>
   2. <span data-ttu-id="ec9df-248">將 [類型] 從固定在本機轉換為分層，或從分層轉換為固定在本機 (如需詳細資訊，請參閱[變更磁碟區類型](#change-the-volume-type))。</span><span class="sxs-lookup"><span data-stu-id="ec9df-248">Convert the **Type** from locally pinned to tiered or from tiered to locally pinned (see [Change the volume type](#change-the-volume-type) for more information).</span></span>
   3. <span data-ttu-id="ec9df-249">增加 [佈建的容量] 。</span><span class="sxs-lookup"><span data-stu-id="ec9df-249">Increase the **Provisioned Capacity**.</span></span> <span data-ttu-id="ec9df-250">[佈建的容量]  只能增加。</span><span class="sxs-lookup"><span data-stu-id="ec9df-250">The **Provisioned Capacity** can only be increased.</span></span> <span data-ttu-id="ec9df-251">您無法在磁碟區建立後予以壓縮。</span><span class="sxs-lookup"><span data-stu-id="ec9df-251">You cannot shrink a volume after it is created.</span></span>
   4. <span data-ttu-id="ec9df-252">在 [已連線的主機] 下，您可以修改 ACR。</span><span class="sxs-lookup"><span data-stu-id="ec9df-252">Under **Connected hosts**, you can modify the ACR.</span></span> <span data-ttu-id="ec9df-253">若要修改 ACR，磁碟區必須處於離線狀態。</span><span class="sxs-lookup"><span data-stu-id="ec9df-253">To modify an ACR, the volume must be offline.</span></span>

       ![檢閱讓磁碟區離線的影響](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

5. <span data-ttu-id="ec9df-255">按一下 [確定] 儲存變更。</span><span class="sxs-lookup"><span data-stu-id="ec9df-255">Click **Save** to save your changes.</span></span> <span data-ttu-id="ec9df-256">系統提示您進行確認時，按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="ec9df-256">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="ec9df-257">Azure 入口網站將會顯示更新磁碟區訊息。</span><span class="sxs-lookup"><span data-stu-id="ec9df-257">The Azure portal will display an updating volume message.</span></span> <span data-ttu-id="ec9df-258">如果磁碟區已成功更新，即會顯示成功訊息。</span><span class="sxs-lookup"><span data-stu-id="ec9df-258">It will display a success message when the volume has been successfully updated.</span></span>

    ![檢閱讓磁碟區離線的影響](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

7. <span data-ttu-id="ec9df-260">如果您要延伸磁碟區，請在 Windows 主機電腦上完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ec9df-260">If you are expanding a volume, complete the following steps on your Windows host computer:</span></span>
   
   1. <span data-ttu-id="ec9df-261">移至 [電腦管理]  ->[磁碟管理]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-261">Go to **Computer Management** ->**Disk Management**.</span></span>
   2. <span data-ttu-id="ec9df-262">以滑鼠右鍵按一下 [磁碟管理]，並選取 [重新掃描磁碟]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-262">Right-click **Disk Management** and select **Rescan Disks**.</span></span>
   3. <span data-ttu-id="ec9df-263">在磁碟清單中，選取您已更新的磁碟區，按一下滑鼠右鍵，然後選取 [延伸磁碟區] 。</span><span class="sxs-lookup"><span data-stu-id="ec9df-263">In the list of disks, select the volume that you updated, right-click, and then select **Extend Volume**.</span></span> <span data-ttu-id="ec9df-264">[延伸磁碟區精靈] 隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="ec9df-264">The Extend Volume wizard starts.</span></span> <span data-ttu-id="ec9df-265">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="ec9df-265">Click **Next**.</span></span>
   4. <span data-ttu-id="ec9df-266">使用預設值完成精靈。</span><span class="sxs-lookup"><span data-stu-id="ec9df-266">Complete the wizard, accepting the default values.</span></span> <span data-ttu-id="ec9df-267">完成精靈後，磁碟區應該會顯示增加的大小。</span><span class="sxs-lookup"><span data-stu-id="ec9df-267">After the wizard is finished, the volume should show the increased size.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="ec9df-268">如果您擴充固定在本機的磁碟區，然後立即擴充另一個固定在本機的磁碟區，磁碟區擴充作業會依序執行。</span><span class="sxs-lookup"><span data-stu-id="ec9df-268">If you expand a locally pinned volume and then expand another locally pinned volume immediately afterwards, the volume expansion jobs run sequentially.</span></span> <span data-ttu-id="ec9df-269">必須先完成第一個磁碟區擴充作業，才能開始下一個磁碟區擴充作業。</span><span class="sxs-lookup"><span data-stu-id="ec9df-269">The first volume expansion job must finish before the next volume expansion job can begin.</span></span>
      

## <a name="change-the-volume-type"></a><span data-ttu-id="ec9df-270">變更磁碟區類型</span><span class="sxs-lookup"><span data-stu-id="ec9df-270">Change the volume type</span></span>

<span data-ttu-id="ec9df-271">您可以將磁碟區類型從分層變更為固定在本機或從固定在本機變更為分層。</span><span class="sxs-lookup"><span data-stu-id="ec9df-271">You can change the volume type from tiered to locally pinned or from locally pinned to tiered.</span></span> <span data-ttu-id="ec9df-272">不過，這種轉換不應該經常發生。</span><span class="sxs-lookup"><span data-stu-id="ec9df-272">However, this conversion should not be a frequent occurrence.</span></span>

### <a name="tiered-to-local-volume-conversion-considerations"></a><span data-ttu-id="ec9df-273">分層到本機磁碟區的轉換注意事項</span><span class="sxs-lookup"><span data-stu-id="ec9df-273">Tiered to local volume conversion considerations</span></span>

<span data-ttu-id="ec9df-274">將磁碟區從分層轉換為固定在本機的部分原因為：</span><span class="sxs-lookup"><span data-stu-id="ec9df-274">Some reasons for converting a volume from tiered to locally pinned are:</span></span>

* <span data-ttu-id="ec9df-275">關於資料可用性和效能的本機保證</span><span class="sxs-lookup"><span data-stu-id="ec9df-275">Local guarantees regarding data availability and performance</span></span>
* <span data-ttu-id="ec9df-276">消除雲端延遲和雲端連線問題。</span><span class="sxs-lookup"><span data-stu-id="ec9df-276">Elimination of cloud latencies and cloud connectivity issues.</span></span>

<span data-ttu-id="ec9df-277">通常，這些磁碟區是您想要經常存取的小的現有磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-277">Typically, these are small existing volumes that you want to access frequently.</span></span> <span data-ttu-id="ec9df-278">當固定在本機的磁碟區建立時，它就會完整佈建。</span><span class="sxs-lookup"><span data-stu-id="ec9df-278">A locally pinned volume is fully provisioned when it is created.</span></span> 

<span data-ttu-id="ec9df-279">如果您要將分層磁碟區轉換為固定在本機的磁碟區，StorSimple 會先確認您在裝置上有足夠的空間，再開始轉換。</span><span class="sxs-lookup"><span data-stu-id="ec9df-279">If you are converting a tiered volume to a locally pinned volume, StorSimple verifies that you have sufficient space on your device before it starts the conversion.</span></span> <span data-ttu-id="ec9df-280">如果您沒有足夠的空間，您會收到錯誤，且作業將會取消。</span><span class="sxs-lookup"><span data-stu-id="ec9df-280">If you have insufficient space, you will receive an error and the operation will be canceled.</span></span> 

> [!NOTE]
> <span data-ttu-id="ec9df-281">在您開始從分層轉換為固定在本機之前，請確定您為其他工作負載考量空間需求。</span><span class="sxs-lookup"><span data-stu-id="ec9df-281">Before you begin a conversion from tiered to locally pinned, make sure that you consider the space requirements of your other workloads.</span></span> 

<span data-ttu-id="ec9df-282">從階層式轉換成固定在本機的磁碟區，可能會對裝置效能產生負面影響。</span><span class="sxs-lookup"><span data-stu-id="ec9df-282">Conversion from a tiered to a locally pinned volume can adversely affect device performance.</span></span> <span data-ttu-id="ec9df-283">此外，下列因素可能會增加完成轉換所需的時間：</span><span class="sxs-lookup"><span data-stu-id="ec9df-283">Additionally, the following factors might increase the time it takes to complete the conversion:</span></span>

* <span data-ttu-id="ec9df-284">頻寬不足。</span><span class="sxs-lookup"><span data-stu-id="ec9df-284">There is insufficient bandwidth.</span></span>
* <span data-ttu-id="ec9df-285">沒有最新備份。</span><span class="sxs-lookup"><span data-stu-id="ec9df-285">There is no current backup.</span></span>

<span data-ttu-id="ec9df-286">若要將這些因素可能造成的影響降到最低：</span><span class="sxs-lookup"><span data-stu-id="ec9df-286">To minimize the effects that these factors may have:</span></span>

* <span data-ttu-id="ec9df-287">請檢閱頻寬節流設定原則，並確認有專用的 40 Mbps 頻寬。</span><span class="sxs-lookup"><span data-stu-id="ec9df-287">Review your bandwidth throttling policies and make sure that a dedicated 40 Mbps bandwidth is available.</span></span>
* <span data-ttu-id="ec9df-288">將轉換排在離峰時間。</span><span class="sxs-lookup"><span data-stu-id="ec9df-288">Schedule the conversion for off-peak hours.</span></span>
* <span data-ttu-id="ec9df-289">在開始轉換之前，請先建立雲端快照。</span><span class="sxs-lookup"><span data-stu-id="ec9df-289">Take a cloud snapshot before you start the conversion.</span></span>

<span data-ttu-id="ec9df-290">如果您要轉換多個磁碟區 (支援不同的工作負載)，您應該設定磁碟區轉換的優先權，讓優先權較高的磁碟區先行轉換。</span><span class="sxs-lookup"><span data-stu-id="ec9df-290">If you are converting multiple volumes (supporting different workloads), then you should prioritize the volume conversion so that higher priority volumes are converted first.</span></span> <span data-ttu-id="ec9df-291">例如，您應該先轉換裝載虛擬機器 (VM) 的磁碟區，或具有 SQL 工作負載的磁碟區，然後才轉換檔案共用工作負載的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-291">For example, you should convert volumes that host virtual machines (VMs) or volumes with SQL workloads before you convert volumes with file share workloads.</span></span>

### <a name="local-to-tiered-volume-conversion-considerations"></a><span data-ttu-id="ec9df-292">本機到分層磁碟區的轉換注意事項</span><span class="sxs-lookup"><span data-stu-id="ec9df-292">Local to tiered volume conversion considerations</span></span>

<span data-ttu-id="ec9df-293">如果您需要額外空間來佈建其他磁碟區，您可能想要將固定在本機的磁碟區變更為分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-293">You may want to change a locally pinned volume to a tiered volume if you need additional space to provision other volumes.</span></span> <span data-ttu-id="ec9df-294">當您將固定在本機的磁碟區轉換為分層時，裝置上的可用容量會隨著釋放的容量大小增加。</span><span class="sxs-lookup"><span data-stu-id="ec9df-294">When you convert the locally pinned volume to tiered, the available capacity on the device increases by the size of the released capacity.</span></span> <span data-ttu-id="ec9df-295">如果連線問題讓磁碟區無法從本機類型轉換為分層類型，本機磁碟區會展示分層磁碟區的屬性，直到完成轉換為止。</span><span class="sxs-lookup"><span data-stu-id="ec9df-295">If connectivity issues prevent the conversion of a volume from the local type to the tiered type, the local volume will exhibit properties of a tiered volume until the conversion is complete.</span></span> <span data-ttu-id="ec9df-296">這是因為可能有部分資料溢出到雲端。</span><span class="sxs-lookup"><span data-stu-id="ec9df-296">This is because some data might have spilled to the cloud.</span></span> <span data-ttu-id="ec9df-297">此溢出的資料會繼續佔用裝置上的本機空間，無法釋放，直到重新啟動並完成作業。</span><span class="sxs-lookup"><span data-stu-id="ec9df-297">This spilled data continues to occupy local space on the device that cannot be freed until the operation is restarted and completed.</span></span>

> [!NOTE]
> <span data-ttu-id="ec9df-298">轉換磁碟區可能需要一些時間，且您在啟動之後無法取消轉換。</span><span class="sxs-lookup"><span data-stu-id="ec9df-298">Converting a volume can take some time and you cannot cancel a conversion after it starts.</span></span> <span data-ttu-id="ec9df-299">磁碟區在轉換時仍然保持連線，您可以建立備份，但是您無法在轉換正在進行時擴充或還原磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-299">The volume remains online during the conversion, and you can take backups, but you cannot expand or restore the volume while the conversion is taking place.</span></span>


#### <a name="to-change-the-volume-type"></a><span data-ttu-id="ec9df-300">變更磁碟區類型</span><span class="sxs-lookup"><span data-stu-id="ec9df-300">To change the volume type</span></span>

1. <span data-ttu-id="ec9df-301">移至 StorSimple 裝置管理員服務，然後按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-301">Go to your StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="ec9df-302">從裝置的表格式清單中，選取您想要修改磁碟區的裝置。</span><span class="sxs-lookup"><span data-stu-id="ec9df-302">From the tabular listing of the devices, select the device that has the volume that you intend to modify.</span></span> <span data-ttu-id="ec9df-303">按一下 [設定] > [磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-303">Click **Settings > Volumes**.</span></span>

    ![移至 [磁碟區] 刀鋒視窗](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. <span data-ttu-id="ec9df-305">從磁碟區的表格式清單中，選取磁碟區，然後按一下滑鼠右鍵以叫用操作功能表。</span><span class="sxs-lookup"><span data-stu-id="ec9df-305">From the tabular listing of volumes, select the volume and right-click to invoke the context menu.</span></span> <span data-ttu-id="ec9df-306">選取 [修改]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-306">Select **Modify**.</span></span>

    ![從操作功能表選取 [修改]](./media/storsimple-8000-manage-volumes-u2/changevoltype2.png)

4. <span data-ttu-id="ec9df-308">在 [修改磁碟區] 刀鋒視窗中，從 [類型] 下拉式清單選取新的類型，以變更磁碟區類型。</span><span class="sxs-lookup"><span data-stu-id="ec9df-308">On the **Modify volume** blade, change the volume type by selecting the new type from the **Type** drop-down list.</span></span>
   
   * <span data-ttu-id="ec9df-309">如果您將類型變更為 [固定在本機] ，StorSimple 會檢查是否有足夠的容量。</span><span class="sxs-lookup"><span data-stu-id="ec9df-309">If you are changing the type to **Locally pinned**, StorSimple will check to see if there is sufficient capacity.</span></span>
   * <span data-ttu-id="ec9df-310">如果您將類型變更為 [分層]，且此磁碟區將會用於封存資料，請選取 [使用此磁碟區存放不常存取的封存資料] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="ec9df-310">If you are changing the type to **Tiered** and this volume will be used for archival data, select the **Use this volume for less frequently accessed archival data** check box.</span></span>
   * <span data-ttu-id="ec9df-311">如果您要將固定在本機的磁碟區設為分層，或_相反情況_，則會顯示下列訊息。</span><span class="sxs-lookup"><span data-stu-id="ec9df-311">If you are configuring a locally pinned volume as tiered or _vice-versa_, the following message appears.</span></span>
   
    ![變更磁碟區類型訊息](./media/storsimple-8000-manage-volumes-u2/changevoltype3.png)

7. <span data-ttu-id="ec9df-313">按一下 [儲存]  儲存變更。</span><span class="sxs-lookup"><span data-stu-id="ec9df-313">Click **Save** to save the changes.</span></span> <span data-ttu-id="ec9df-314">當系統提示您確認時，按一下 [是] 以開始轉換程序。</span><span class="sxs-lookup"><span data-stu-id="ec9df-314">When prompted for confirmation, click **Yes** to start the conversion process.</span></span> 

    ![儲存並確認](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

8. <span data-ttu-id="ec9df-316">Azure 入口網站會顯示通知，告知已建立會更新磁碟區的作業。</span><span class="sxs-lookup"><span data-stu-id="ec9df-316">The Azure portal displays a notification for the job creation that would update the volume.</span></span> <span data-ttu-id="ec9df-317">按一下通知，以監視磁碟區轉換作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="ec9df-317">Click on the notification to monitor the status of the volume conversion job.</span></span>

    ![磁碟區轉換作業](./media/storsimple-8000-manage-volumes-u2/changevoltype5.png)

## <a name="take-a-volume-offline"></a><span data-ttu-id="ec9df-319">使磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="ec9df-319">Take a volume offline</span></span>

<span data-ttu-id="ec9df-320">當您打算修改或刪除磁碟區時，可能需要先使磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="ec9df-320">You may need to take a volume offline when you are planning to modify or delete the volume.</span></span> <span data-ttu-id="ec9df-321">當磁碟區離線時，即無法進行讀寫存取。</span><span class="sxs-lookup"><span data-stu-id="ec9df-321">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="ec9df-322">您必須使主機和裝置上的磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="ec9df-322">You must take the volume offline on the host and the device.</span></span>

#### <a name="to-take-a-volume-offline"></a><span data-ttu-id="ec9df-323">若要使磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="ec9df-323">To take a volume offline</span></span>

1. <span data-ttu-id="ec9df-324">請確定有問題的磁碟區不在使用中後，再使其離線。</span><span class="sxs-lookup"><span data-stu-id="ec9df-324">Make sure that the volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="ec9df-325">先使主機上的磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="ec9df-325">Take the volume offline on the host first.</span></span> <span data-ttu-id="ec9df-326">這樣做可以排除任何會造成磁碟區上資料損毀的潛在風險。</span><span class="sxs-lookup"><span data-stu-id="ec9df-326">This eliminates any potential risk of data corruption on the volume.</span></span> <span data-ttu-id="ec9df-327">如需特定步驟，請參閱主機作業系統的指示。</span><span class="sxs-lookup"><span data-stu-id="ec9df-327">For specific steps, refer to the instructions for your host operating system.</span></span>
3. <span data-ttu-id="ec9df-328">在主機離線之後，請執行下列步驟以使裝置上的磁碟區離線：</span><span class="sxs-lookup"><span data-stu-id="ec9df-328">After the host is offline, take the volume on the device offline by performing the following steps:</span></span>
   
    1. <span data-ttu-id="ec9df-329">移至 StorSimple 裝置管理員服務，然後按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-329">Go to your StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="ec9df-330">從裝置的表格式清單中，選取您想要修改磁碟區的裝置。</span><span class="sxs-lookup"><span data-stu-id="ec9df-330">From the tabular listing of the devices, select the device that has the volume that you intend to modify.</span></span> <span data-ttu-id="ec9df-331">按一下 [設定] > [磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-331">Click **Settings > Volumes**.</span></span>

        ![移至 [磁碟區] 刀鋒視窗](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

    2. <span data-ttu-id="ec9df-333">從磁碟區的表格式清單中，選取磁碟區，然後按一下滑鼠右鍵以叫用操作功能表。</span><span class="sxs-lookup"><span data-stu-id="ec9df-333">From the tabular listing of volumes, select the volume and right-click to invoke the context menu.</span></span> <span data-ttu-id="ec9df-334">選取 [離線]，讓您要修改的磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="ec9df-334">Select **Take offline** to take the volume you will modify offline.</span></span>

        ![選取並讓磁碟區離線](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. <span data-ttu-id="ec9df-336">在 [離線] 刀鋒視窗中，檢閱讓磁碟區離線的影響，並選取對應的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="ec9df-336">In the **Take offline** blade, review the impact of taking the volume offline and select the corresponding checkbox.</span></span> <span data-ttu-id="ec9df-337">按一下 [離線]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-337">Click **Take offline**.</span></span> 

    ![檢閱讓磁碟區離線的影響](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)
      
      <span data-ttu-id="ec9df-339">磁碟區離線時，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="ec9df-339">You are notified when the volume is offline.</span></span> <span data-ttu-id="ec9df-340">磁碟區狀態也會更新為離線。</span><span class="sxs-lookup"><span data-stu-id="ec9df-340">The volume status also updates to Offline.</span></span>
      
4. <span data-ttu-id="ec9df-341">當磁碟區離線之後，如果您選取磁碟區並按一下滑鼠右鍵，操作功能表的 [上線] 選項會變成可用狀態。</span><span class="sxs-lookup"><span data-stu-id="ec9df-341">After a volume is offline, if you select the volume and right-click, **Bring Online** option becomes available in the context menu.</span></span>

> [!NOTE]
> <span data-ttu-id="ec9df-342">[離線] 命令會將要求傳送到裝置，以使磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="ec9df-342">The **Take Offline** command sends a request to the device to take the volume offline.</span></span> <span data-ttu-id="ec9df-343">如果主機仍在使用該磁碟區，這會導致連線中斷，但是使磁碟區離線不會失敗。</span><span class="sxs-lookup"><span data-stu-id="ec9df-343">If hosts are still using the volume, this results in broken connections, but taking the volume offline will not fail.</span></span>

## <a name="delete-a-volume"></a><span data-ttu-id="ec9df-344">刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="ec9df-344">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec9df-345">只有當磁碟區離線時，您才能予以刪除。</span><span class="sxs-lookup"><span data-stu-id="ec9df-345">You can delete a volume only if it is offline.</span></span>

<span data-ttu-id="ec9df-346">請完成下列步驟來刪除磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-346">Complete the following steps to delete a volume.</span></span>

#### <a name="to-delete-a-volume"></a><span data-ttu-id="ec9df-347">若要刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="ec9df-347">To delete a volume</span></span>

1. <span data-ttu-id="ec9df-348">移至 StorSimple 裝置管理員服務，然後按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-348">Go to your StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="ec9df-349">從裝置的表格式清單中，選取您想要修改磁碟區的裝置。</span><span class="sxs-lookup"><span data-stu-id="ec9df-349">From the tabular listing of the devices, select the device that has the volume that you intend to modify.</span></span> <span data-ttu-id="ec9df-350">按一下 [設定] > [磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-350">Click **Settings > Volumes**.</span></span>

    ![移至 [磁碟區] 刀鋒視窗](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. <span data-ttu-id="ec9df-352">檢查您想要刪除之磁碟區的狀態。</span><span class="sxs-lookup"><span data-stu-id="ec9df-352">Check the status of the volume you want to delete.</span></span> <span data-ttu-id="ec9df-353">如果您想要刪除的磁碟區未離線，請先讓它離線。</span><span class="sxs-lookup"><span data-stu-id="ec9df-353">If the volume you want to delete is not offline, take it offline first.</span></span> <span data-ttu-id="ec9df-354">請遵循 [使磁碟區離線](#take-a-volume-offline)中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="ec9df-354">Follow the steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="ec9df-355">磁碟區離線之後，選取磁碟區，按一下滑鼠右鍵以叫用操作功能表，然後選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-355">After the volume is offline, select the volume, right-click to invoke the context menu and then select **Delete**.</span></span>

    ![從操作功能表選取 [刪除]](./media/storsimple-8000-manage-volumes-u2/deletevol1.png)

5. <span data-ttu-id="ec9df-357">在 [刪除] 刀鋒視窗中，檢閱刪除磁碟區會造成的影響，並選取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="ec9df-357">In the **Delete** blade, review and select the checkbox against the impact of deleting a volume.</span></span> <span data-ttu-id="ec9df-358">當您刪除磁碟區時，存放在磁碟區的所有資料都會遺失。</span><span class="sxs-lookup"><span data-stu-id="ec9df-358">When you delete a volume, all the data that resides on the volume is lost.</span></span> 

    ![儲存並確認變更](./media/storsimple-8000-manage-volumes-u2/deletevol2.png)

6. <span data-ttu-id="ec9df-360">刪除磁碟區之後，磁碟區的表格式清單會一併更新以顯示刪除。</span><span class="sxs-lookup"><span data-stu-id="ec9df-360">After the volume is deleted, the tabular list of volumes updates to indicate the deletion.</span></span>

    ![更新磁碟區清單](./media/storsimple-8000-manage-volumes-u2/deletevol3.png)
   
   > [!NOTE]
   > <span data-ttu-id="ec9df-362">如果您刪除固定在本機的磁碟區，新的磁碟區的可用空間可能不會立即更新。</span><span class="sxs-lookup"><span data-stu-id="ec9df-362">If you delete a locally pinned volume, the space available for new volumes may not be updated immediately.</span></span> <span data-ttu-id="ec9df-363">StorSimple 裝置管理員服務會定期更新本機可用空間。</span><span class="sxs-lookup"><span data-stu-id="ec9df-363">The StorSimple Device Manager Service updates the local space available periodically.</span></span> <span data-ttu-id="ec9df-364">建議您等候幾分鐘，然後再嘗試建立新的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-364">We suggest you wait for a few minutes before you try to create the new volume.</span></span>
   >
   > <span data-ttu-id="ec9df-365">此外，如果您刪除固定在本機的磁碟區，然後立即刪除另一個固定在本機的磁碟區，磁碟區刪除作業會依序執行。</span><span class="sxs-lookup"><span data-stu-id="ec9df-365">Additionally, if you delete a locally pinned volume and then delete another locally pinned volume immediately afterwards, the volume deletion jobs run sequentially.</span></span> <span data-ttu-id="ec9df-366">必須先完成第一個磁碟區刪除作業，才能開始下一個磁碟區刪除作業。</span><span class="sxs-lookup"><span data-stu-id="ec9df-366">The first volume deletion job must finish before the next volume deletion job can begin.</span></span>

## <a name="monitor-a-volume"></a><span data-ttu-id="ec9df-367">監視磁碟區</span><span class="sxs-lookup"><span data-stu-id="ec9df-367">Monitor a volume</span></span>

<span data-ttu-id="ec9df-368">監視磁碟區可讓您為磁碟區收集 I/O 相關的統計資料。</span><span class="sxs-lookup"><span data-stu-id="ec9df-368">Volume monitoring allows you to collect I/O-related statistics for a volume.</span></span> <span data-ttu-id="ec9df-369">根據預設，您建立的前 32 個磁碟區會啟用監視。</span><span class="sxs-lookup"><span data-stu-id="ec9df-369">Monitoring is enabled by default for the first 32 volumes that you create.</span></span> <span data-ttu-id="ec9df-370">預設會停用監視其他磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-370">Monitoring of additional volumes is disabled by default.</span></span> 

> [!NOTE]
> <span data-ttu-id="ec9df-371">預設會停用監視複製的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-371">Monitoring of cloned volumes is disabled by default.</span></span>


<span data-ttu-id="ec9df-372">請執行下列步驟來啟用或停用監視磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ec9df-372">Perform the following steps to enable or disable monitoring for a volume.</span></span>

#### <a name="to-enable-or-disable-volume-monitoring"></a><span data-ttu-id="ec9df-373">若要啟用或停用監視磁碟區</span><span class="sxs-lookup"><span data-stu-id="ec9df-373">To enable or disable volume monitoring</span></span>

1. <span data-ttu-id="ec9df-374">移至 StorSimple 裝置管理員服務，然後按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-374">Go to your StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="ec9df-375">從裝置的表格式清單中，選取您想要修改磁碟區的裝置。</span><span class="sxs-lookup"><span data-stu-id="ec9df-375">From the tabular listing of the devices, select the device that has the volume that you intend to modify.</span></span> <span data-ttu-id="ec9df-376">按一下 [設定] > [磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-376">Click **Settings > Volumes**.</span></span>
2. <span data-ttu-id="ec9df-377">從磁碟區的表格式清單中，選取磁碟區，然後按一下滑鼠右鍵以叫用操作功能表。</span><span class="sxs-lookup"><span data-stu-id="ec9df-377">From the tabular listing of volumes, select the volume and right-click to invoke the context menu.</span></span> <span data-ttu-id="ec9df-378">選取 [修改]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-378">Select **Modify**.</span></span>
3. <span data-ttu-id="ec9df-379">在 [修改磁碟區] 刀鋒視窗中，將 [監視] 選取 [啟用] 或 [停用]，以啟用或停用監視。</span><span class="sxs-lookup"><span data-stu-id="ec9df-379">In the **Modify volume** blade, for **Monitoring** select **Enable** or **Disable** to enable or disable monitoring.</span></span>

    ![停用監視](./media/storsimple-8000-manage-volumes-u2/monitorvol1.png) 

4. <span data-ttu-id="ec9df-381">按一下 [儲存]，當系統提示您進行確認時，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="ec9df-381">Click **Save** and when prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="ec9df-382">成功更新磁碟區之後，Azure 入口網站會顯示更新磁碟區的通知，然後出現成功訊息。</span><span class="sxs-lookup"><span data-stu-id="ec9df-382">The Azure portal displays a notification for updating the volume and then a success message, after the volume is successfully updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec9df-383">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ec9df-383">Next steps</span></span>

* <span data-ttu-id="ec9df-384">了解如何 [複製 StorSimple 磁碟區](storsimple-8000-clone-volume-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="ec9df-384">Learn how to [clone a StorSimple volume](storsimple-8000-clone-volume-u2.md).</span></span>
* <span data-ttu-id="ec9df-385">了解如何[使用 StorSimple 裝置管理員服務管理 StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="ec9df-385">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>


---
title: "aaaManage StorSimple 磁碟區 (Update 3) |Microsoft 文件"
description: "說明如何 tooadd、 修改、 監視及刪除 StorSimple 磁碟區，以及如何 tootake 它們只有在必要時離線。"
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
ms.openlocfilehash: 6228c4486dd5a7887df670c4c4584c4edcdfc509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-volumes-update-3-or-later"></a><span data-ttu-id="007c3-103">使用 hello StorSimple 裝置管理員服務 toomanage 磁碟區 (Update 3 或更新版本)</span><span class="sxs-lookup"><span data-stu-id="007c3-103">Use hello StorSimple Device Manager service toomanage volumes (Update 3 or later)</span></span>

## <a name="overview"></a><span data-ttu-id="007c3-104">概觀</span><span class="sxs-lookup"><span data-stu-id="007c3-104">Overview</span></span>

<span data-ttu-id="007c3-105">本教學課程將說明 toouse hello StorSimple 裝置管理員服務 toocreate 並管理執行 Update 3 及更新版本的 hello StorSimple 8000 系列裝置上的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage volumes on hello StorSimple 8000 series devices running Update 3 and later.</span></span>

<span data-ttu-id="007c3-106">hello StorSimple 裝置管理員服務是 hello Azure 入口網站，可讓您從單一 web 介面來管理您的 StorSimple 解決方案中的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="007c3-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="007c3-107">所有裝置上使用 hello Azure 入口網站 toomanage 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-107">Use hello Azure portal toomanage volumes on all your devices.</span></span> <span data-ttu-id="007c3-108">您也可以建立和管理 StorSimple 服務、管理裝置、備份原則，以及備份類別目錄，並檢視警示。</span><span class="sxs-lookup"><span data-stu-id="007c3-108">You can also create and manage StorSimple services, manage devices, backup policies, and backup catalog, and view alerts.</span></span>

## <a name="volume-types"></a><span data-ttu-id="007c3-109">磁碟區類型</span><span class="sxs-lookup"><span data-stu-id="007c3-109">Volume types</span></span>

<span data-ttu-id="007c3-110">StorSimple 磁碟區可以是：</span><span class="sxs-lookup"><span data-stu-id="007c3-110">StorSimple volumes can be:</span></span>

* <span data-ttu-id="007c3-111">**固定在本機磁碟區**： 隨時都能在這些磁碟區中的資料會保留在 hello 本機 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="007c3-111">**Locally pinned volumes**: Data in these volumes remains on hello local StorSimple device at all times.</span></span>
* <span data-ttu-id="007c3-112">**分層磁碟區**： 這些磁碟區中的資料可以 spill toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="007c3-112">**Tiered volumes**: Data in these volumes can spill toohello cloud.</span></span>

<span data-ttu-id="007c3-113">封存的磁碟區是一種分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-113">An archival volume is a type of tiered volume.</span></span> <span data-ttu-id="007c3-114">hello 較大重複資料刪除區塊大小用於封存磁碟區，可讓資料 toohello 雲端的 hello 裝置 tootransfer 較區段。</span><span class="sxs-lookup"><span data-stu-id="007c3-114">hello larger deduplication chunk size used for archival volumes allows hello device tootransfer larger segments of data toohello cloud.</span></span>

<span data-ttu-id="007c3-115">如有必要，您可以變更 hello 磁碟區類型從本機 tootiered 或階層式 toolocal。</span><span class="sxs-lookup"><span data-stu-id="007c3-115">If necessary, you can change hello volume type from local tootiered or from tiered toolocal.</span></span> <span data-ttu-id="007c3-116">如需詳細資訊，請移至太[變更 hello 磁碟區類型](#change-the-volume-type)。</span><span class="sxs-lookup"><span data-stu-id="007c3-116">For more information, go too[Change hello volume type](#change-the-volume-type).</span></span>

### <a name="locally-pinned-volumes"></a><span data-ttu-id="007c3-117">固定在本機的磁碟區</span><span class="sxs-lookup"><span data-stu-id="007c3-117">Locally pinned volumes</span></span>

<span data-ttu-id="007c3-118">本機固定磁碟區是不層資料 toohello 雲端的完整佈建磁碟區，以確保本機可保證，針對主要資料，獨立於雲端連線。</span><span class="sxs-lookup"><span data-stu-id="007c3-118">Locally pinned volumes are fully provisioned volumes that do not tier data toohello cloud, thereby ensuring local guarantees for primary data, independent of cloud connectivity.</span></span> <span data-ttu-id="007c3-119">固定在本機的磁碟區的資料不會進行重複資料刪除和壓縮，但是，固定在本機的磁碟區的快照會進行重複資料刪除。</span><span class="sxs-lookup"><span data-stu-id="007c3-119">Data on locally pinned volumes is not deduplicated and compressed; however, snapshots of locally pinned volumes are deduplicated.</span></span> 

<span data-ttu-id="007c3-120">固定在本機的磁碟區是完整佈建，因此，當您建立它們時，必須在裝置上有足夠的空間。</span><span class="sxs-lookup"><span data-stu-id="007c3-120">Locally pinned volumes are fully provisioned; therefore, you must have sufficient space on your device when you create them.</span></span> <span data-ttu-id="007c3-121">您可以佈建本機固定磁碟區總 tooa hello StorSimple 8100 裝置上為 8 TB 和 20 TB hello 8600 裝置上的大小上限。</span><span class="sxs-lookup"><span data-stu-id="007c3-121">You can provision locally pinned volumes up tooa maximum size of 8 TB on hello StorSimple 8100 device and 20 TB on hello 8600 device.</span></span> <span data-ttu-id="007c3-122">StorSimple 會保留 hello 剩餘本機裝置上的空間 hello 快照集、 中繼資料，以及資料處理。</span><span class="sxs-lookup"><span data-stu-id="007c3-122">StorSimple reserves hello remaining local space on hello device for snapshots, metadata, and data processing.</span></span> <span data-ttu-id="007c3-123">您可以增加 hello 的本機固定磁碟區 toohello 最大可用空間的大小，但您無法減少 hello 一次建立的磁碟區大小。</span><span class="sxs-lookup"><span data-stu-id="007c3-123">You can increase hello size of a locally pinned volume toohello maximum space available, but you cannot decrease hello size of a volume once created.</span></span>

<span data-ttu-id="007c3-124">當您建立本機固定磁碟區時，則會減少 hello 建立分層磁碟區的可用空間。</span><span class="sxs-lookup"><span data-stu-id="007c3-124">When you create a locally pinned volume, hello available space for creation of tiered volumes is reduced.</span></span> <span data-ttu-id="007c3-125">hello 反向也是如此： 如果您有現有的階層式磁碟區時，會低於 hello 最大限制上述 hello 空間可供建立本機固定磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-125">hello reverse is also true: if you have existing tiered volumes, hello space available for creating locally pinned volumes will be lower than hello maximum limits stated above.</span></span> <span data-ttu-id="007c3-126">如需有關本機磁碟區的詳細資訊，請參閱 toohello[本機固定磁碟區上的常見問題集](storsimple-8000-local-volume-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="007c3-126">For more information on local volumes, refer toohello [frequently asked questions on locally pinned volumes](storsimple-8000-local-volume-faq.md).</span></span>

### <a name="tiered-volumes"></a><span data-ttu-id="007c3-127">分層磁碟區</span><span class="sxs-lookup"><span data-stu-id="007c3-127">Tiered volumes</span></span>

<span data-ttu-id="007c3-128">階層式磁碟區是在哪一個 hello 經常存取的資料會保持在 hello 裝置上的本機和較不常用資料，則會自動分層 toohello 雲端的精簡佈建磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-128">Tiered volumes are thinly provisioned volumes in which hello frequently accessed data stays local on hello device and less frequently used data is automatically tiered toohello cloud.</span></span> <span data-ttu-id="007c3-129">精簡佈建是一種虛擬化技術，可用的存放裝置會出現 tooexceed 實體資源。</span><span class="sxs-lookup"><span data-stu-id="007c3-129">Thin provisioning is a virtualization technology in which available storage appears tooexceed physical resources.</span></span> <span data-ttu-id="007c3-130">而是會預先保留足夠的儲存空間，StorSimple 會使用精簡佈建 tooallocate 剛好足夠空間 toomeet 目前的需求。</span><span class="sxs-lookup"><span data-stu-id="007c3-130">Instead of reserving sufficient storage in advance, StorSimple uses thin provisioning tooallocate just enough space toomeet current requirements.</span></span> <span data-ttu-id="007c3-131">hello 彈性本質的雲端儲存體促進這種方法，因為 StorSimple 可以增加或減少雲端儲存體 toomeet 需求的變更。</span><span class="sxs-lookup"><span data-stu-id="007c3-131">hello elastic nature of cloud storage facilitates this approach because StorSimple can increase or decrease cloud storage toomeet changing demands.</span></span>

<span data-ttu-id="007c3-132">如果您使用 hello 分層磁碟區的封存資料，選取 hello**對於不常存取的封存資料，使用此磁碟區**核取方塊 toochange hello 重複資料刪除區塊大小的磁碟區 too512 KB。</span><span class="sxs-lookup"><span data-stu-id="007c3-132">If you are using hello tiered volume for archival data, select hello **Use this volume for less frequently accessed archival data** check box toochange hello deduplication chunk size for your volume too512 KB.</span></span> <span data-ttu-id="007c3-133">如果您未選取此選項，hello 對應的階層式磁碟區會使用 64 KB 的區塊大小。</span><span class="sxs-lookup"><span data-stu-id="007c3-133">If you do not select this option, hello corresponding tiered volume will use a chunk size of 64 KB.</span></span> <span data-ttu-id="007c3-134">較大的重複資料刪除區塊大小可讓大型的封存資料 toohello 雲端的 hello 裝置 tooexpedite hello 傳輸。</span><span class="sxs-lookup"><span data-stu-id="007c3-134">A larger deduplication chunk size allows hello device tooexpedite hello transfer of large archival data toohello cloud.</span></span>


### <a name="provisioned-capacity"></a><span data-ttu-id="007c3-135">佈建的容量</span><span class="sxs-lookup"><span data-stu-id="007c3-135">Provisioned capacity</span></span>

<span data-ttu-id="007c3-136">請參閱下表針對每個裝置和磁碟區類型的最大佈建的容量 toohello。</span><span class="sxs-lookup"><span data-stu-id="007c3-136">Refer toohello following table for maximum provisioned capacity for each device and volume type.</span></span> <span data-ttu-id="007c3-137">(請注意，固定在本機的磁碟區無法在虛擬裝置上使用。)</span><span class="sxs-lookup"><span data-stu-id="007c3-137">(Note that locally pinned volumes are not available on a virtual device.)</span></span>

|  | <span data-ttu-id="007c3-138">最大的分層磁碟區大小</span><span class="sxs-lookup"><span data-stu-id="007c3-138">Maximum tiered volume size</span></span> | <span data-ttu-id="007c3-139">最大的固定在本機的磁碟區大小</span><span class="sxs-lookup"><span data-stu-id="007c3-139">Maximum locally pinned volume size</span></span> |
| --- | --- | --- |
| <span data-ttu-id="007c3-140">**實體裝置**</span><span class="sxs-lookup"><span data-stu-id="007c3-140">**Physical devices**</span></span> | | |
| <span data-ttu-id="007c3-141">8100</span><span class="sxs-lookup"><span data-stu-id="007c3-141">8100</span></span> |<span data-ttu-id="007c3-142">64 TB</span><span class="sxs-lookup"><span data-stu-id="007c3-142">64 TB</span></span> |<span data-ttu-id="007c3-143">8 TB</span><span class="sxs-lookup"><span data-stu-id="007c3-143">8 TB</span></span> |
| <span data-ttu-id="007c3-144">8600</span><span class="sxs-lookup"><span data-stu-id="007c3-144">8600</span></span> |<span data-ttu-id="007c3-145">64 TB</span><span class="sxs-lookup"><span data-stu-id="007c3-145">64 TB</span></span> |<span data-ttu-id="007c3-146">20 TB</span><span class="sxs-lookup"><span data-stu-id="007c3-146">20 TB</span></span> |
| <span data-ttu-id="007c3-147">**虛擬裝置**</span><span class="sxs-lookup"><span data-stu-id="007c3-147">**Virtual devices**</span></span> | | |
| <span data-ttu-id="007c3-148">8010</span><span class="sxs-lookup"><span data-stu-id="007c3-148">8010</span></span> |<span data-ttu-id="007c3-149">30 TB</span><span class="sxs-lookup"><span data-stu-id="007c3-149">30 TB</span></span> |<span data-ttu-id="007c3-150">N/A</span><span class="sxs-lookup"><span data-stu-id="007c3-150">N/A</span></span> |
| <span data-ttu-id="007c3-151">8020</span><span class="sxs-lookup"><span data-stu-id="007c3-151">8020</span></span> |<span data-ttu-id="007c3-152">64 TB</span><span class="sxs-lookup"><span data-stu-id="007c3-152">64 TB</span></span> |<span data-ttu-id="007c3-153">N/A</span><span class="sxs-lookup"><span data-stu-id="007c3-153">N/A</span></span> |

## <a name="hello-volumes-blade"></a><span data-ttu-id="007c3-154">hello 磁碟區 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="007c3-154">hello volumes blade</span></span>

<span data-ttu-id="007c3-155">hello**磁碟區**刀鋒視窗可讓您 toomanage hello 存放磁碟區 hello 為啟動器 （伺服器） 的 Microsoft Azure StorSimple 裝置上佈建。</span><span class="sxs-lookup"><span data-stu-id="007c3-155">hello **Volumes** blade allows you toomanage hello storage volumes that are provisioned on hello Microsoft Azure StorSimple device for your initiators (servers).</span></span> <span data-ttu-id="007c3-156">它會顯示 hello StorSimple 裝置連線的 tooyour 服務 hello 的磁碟區的清單。</span><span class="sxs-lookup"><span data-stu-id="007c3-156">It displays hello list of volumes on hello StorSimple devices connected tooyour service.</span></span>

 ![磁碟區頁面](./media/storsimple-8000-manage-volumes-u2/volumeslist.png)

<span data-ttu-id="007c3-158">磁碟區是由一系列屬性所組成：</span><span class="sxs-lookup"><span data-stu-id="007c3-158">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="007c3-159">**磁碟區名稱**– 描述性的名稱必須是唯一的可協助識別 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-159">**Volume Name** – A descriptive name that must be unique and helps identify hello volume.</span></span> <span data-ttu-id="007c3-160">這個名稱也可在您篩選特定磁碟區時用於監視報告。</span><span class="sxs-lookup"><span data-stu-id="007c3-160">This name is also used in monitoring reports when you filter on a specific volume.</span></span> <span data-ttu-id="007c3-161">一旦建立 hello 磁碟區，但無法重新命名。</span><span class="sxs-lookup"><span data-stu-id="007c3-161">Once hello volume is created, it cannot be renamed.</span></span>
* <span data-ttu-id="007c3-162">**狀態** – 可為連線或離線。</span><span class="sxs-lookup"><span data-stu-id="007c3-162">**Status** – Can be online or offline.</span></span> <span data-ttu-id="007c3-163">如果磁碟區已離線，就不允許存取 toouse hello 磁碟區的可見 tooinitiators （伺服器）。</span><span class="sxs-lookup"><span data-stu-id="007c3-163">If a volume is offline, it is not visible tooinitiators (servers) that are allowed access toouse hello volume.</span></span>
* <span data-ttu-id="007c3-164">**容量**– 指定 hello 的 hello 啟動器 （伺服器） 來儲存的資料量總計。</span><span class="sxs-lookup"><span data-stu-id="007c3-164">**Capacity** – specifies hello total amount of data that can be stored by hello initiator (server).</span></span> <span data-ttu-id="007c3-165">固定在本機磁碟區完全佈建，而且位於 hello StorSimple 裝置上。</span><span class="sxs-lookup"><span data-stu-id="007c3-165">Locally-pinned volumes are fully provisioned and reside on hello StorSimple device.</span></span> <span data-ttu-id="007c3-166">精簡佈建分層磁碟區和 hello 資料重複資料刪除。</span><span class="sxs-lookup"><span data-stu-id="007c3-166">Tiered volumes are thinly provisioned and hello data is deduplicated.</span></span> <span data-ttu-id="007c3-167">使用精簡佈建磁碟區，您的裝置不會預先配置實體儲存容量在內部或根據 tooconfigured 磁碟區容量的 hello 雲端。</span><span class="sxs-lookup"><span data-stu-id="007c3-167">With thinly provisioned volumes, your device doesn’t pre-allocate physical storage capacity internally or on hello cloud according tooconfigured volume capacity.</span></span> <span data-ttu-id="007c3-168">配置及取用視 hello 磁碟區容量。</span><span class="sxs-lookup"><span data-stu-id="007c3-168">hello volume capacity is allocated and consumed on demand.</span></span>
* <span data-ttu-id="007c3-169">**型別**– 指出 hello 磁碟區是否為**分層**(hello 預設) 或**固定在本機**。</span><span class="sxs-lookup"><span data-stu-id="007c3-169">**Type** – Indicates whether hello volume is **Tiered** (hello default) or **Locally pinned**.</span></span>

<span data-ttu-id="007c3-170">使用 hello 指示在本教學課程 tooperform hello，下列工作：</span><span class="sxs-lookup"><span data-stu-id="007c3-170">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="007c3-171">新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="007c3-171">Add a volume</span></span> 
* <span data-ttu-id="007c3-172">修改磁碟區</span><span class="sxs-lookup"><span data-stu-id="007c3-172">Modify a volume</span></span> 
* <span data-ttu-id="007c3-173">變更 hello 磁碟區類型</span><span class="sxs-lookup"><span data-stu-id="007c3-173">Change hello volume type</span></span>
* <span data-ttu-id="007c3-174">刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="007c3-174">Delete a volume</span></span> 
* <span data-ttu-id="007c3-175">使磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="007c3-175">Take a volume offline</span></span> 
* <span data-ttu-id="007c3-176">監視磁碟區</span><span class="sxs-lookup"><span data-stu-id="007c3-176">Monitor a volume</span></span> 

## <a name="add-a-volume"></a><span data-ttu-id="007c3-177">新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="007c3-177">Add a volume</span></span>

<span data-ttu-id="007c3-178">您已在部署 StorSimple 8000 系列裝置期間[建立磁碟區](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume)。</span><span class="sxs-lookup"><span data-stu-id="007c3-178">You [created a volume](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume) during deployment of your StorSimple 8000 series device.</span></span> <span data-ttu-id="007c3-179">新增磁碟區會是類似的程序。</span><span class="sxs-lookup"><span data-stu-id="007c3-179">Adding a volume is a similar procedure.</span></span>

#### <a name="tooadd-a-volume"></a><span data-ttu-id="007c3-180">tooadd 磁碟區</span><span class="sxs-lookup"><span data-stu-id="007c3-180">tooadd a volume</span></span>

1. <span data-ttu-id="007c3-181">從 hello 表格清單中的 hello 裝置 hello**裝置**刀鋒視窗中，選取您的裝置。</span><span class="sxs-lookup"><span data-stu-id="007c3-181">From hello tabular listing of hello devices in hello **Devices** blade, select your device.</span></span> <span data-ttu-id="007c3-182">按一下 [+ 新增磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="007c3-182">Click **+ Add volume**.</span></span>

    ![新增磁碟區](./media/storsimple-8000-manage-volumes-u2/step5createvol1.png)

2. <span data-ttu-id="007c3-184">在 hello**加入磁碟區**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="007c3-184">In hello **Add a volume** blade:</span></span>
   
    1. <span data-ttu-id="007c3-185">hello**選取裝置**欄位會自動填入您目前的裝置。</span><span class="sxs-lookup"><span data-stu-id="007c3-185">hello **Select device** field is automatically populated with your current device.</span></span>

    2. <span data-ttu-id="007c3-186">從 hello 下拉式清單中，選取 hello 磁碟區容器，您需要 tooadd 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-186">From hello drop-down list, select hello volume container where you need tooadd a volume.</span></span>

    3.  <span data-ttu-id="007c3-187">輸入磁碟區的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="007c3-187">Type a **Name** for your volume.</span></span> <span data-ttu-id="007c3-188">Hello 磁碟區建立之後，您無法重新命名 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-188">Once hello volume is created, you cannot rename hello volume.</span></span>

    4. <span data-ttu-id="007c3-189">在 hello 下拉式清單中，選取 hello**類型**磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-189">On hello drop-down list, select hello **Type** for your volume.</span></span> <span data-ttu-id="007c3-190">需要本機保證、低延遲，以及高效能的工作負載，請選取 [固定在本機]  磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-190">For workloads that require local guarantees, low latencies, and higher performance, select a **Locally pinned** volume.</span></span> <span data-ttu-id="007c3-191">針對所有其他資料，請選取 [分層]  磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-191">For all other data, select a **Tiered** volume.</span></span> <span data-ttu-id="007c3-192">如果您將此磁碟區用於封存資料，請核取 [將此磁碟區用於較不常存取的封存資料] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="007c3-192">If you are using this volume for archival data, check **Use this volume for less frequently accessed archival data**.</span></span>
      
       <span data-ttu-id="007c3-193">分層磁碟區已精簡佈建，而且可以快速地建立。</span><span class="sxs-lookup"><span data-stu-id="007c3-193">A tiered volume is thinly provisioned and can be created quickly.</span></span> <span data-ttu-id="007c3-194">選取**對於不常存取的封存資料，使用此磁碟區**封存資料變更 hello 重複資料刪除區塊大小的磁碟區為目標的階層式磁碟區 too512 KB。</span><span class="sxs-lookup"><span data-stu-id="007c3-194">Selecting **Use this volume for less frequently accessed archival data** for tiered volume targeted for archival data changes hello deduplication chunk size for your volume too512 KB.</span></span> <span data-ttu-id="007c3-195">如果未核取此欄位，hello 對應的階層式磁碟區會使用 64 KB 的區塊大小。</span><span class="sxs-lookup"><span data-stu-id="007c3-195">If this field is not checked, hello corresponding tiered volume uses a chunk size of 64 KB.</span></span> <span data-ttu-id="007c3-196">較大的重複資料刪除區塊大小可讓大型的封存資料 toohello 雲端的 hello 裝置 tooexpedite hello 傳輸。</span><span class="sxs-lookup"><span data-stu-id="007c3-196">A larger deduplication chunk size allows hello device tooexpedite hello transfer of large archival data toohello cloud.</span></span>
       
       <span data-ttu-id="007c3-197">本機固定磁碟區以佈建，並確保維持本機 toohello 裝置 hello hello 磁碟區上的主要資料，並不 spill toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="007c3-197">A locally pinned volume is thickly provisioned and ensures that hello primary data on hello volume stays local toohello device and does not spill toohello cloud.</span></span>  <span data-ttu-id="007c3-198">如果您建立本機固定磁碟區，hello 裝置檢查 hello 本機層上的可用空間的 hello tooprovision hello 大量要求的大小。</span><span class="sxs-lookup"><span data-stu-id="007c3-198">If you create a locally pinned volume, hello device checks for available space on hello local tiers tooprovision hello volume of hello requested size.</span></span> <span data-ttu-id="007c3-199">建立本機固定磁碟區的 hello 作業可能會溢出 hello 裝置 toohello 雲端的現有資料並採取 toocreate hello 磁碟區的 hello 時間可能較長。</span><span class="sxs-lookup"><span data-stu-id="007c3-199">hello operation of creating a locally pinned volume may involve spilling existing data from hello device toohello cloud and hello time taken toocreate hello volume may be long.</span></span> <span data-ttu-id="007c3-200">hello 總時間取決於 hello 大小 hello 佈建磁碟區、 可用的網路頻寬及裝置上的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="007c3-200">hello total time depends on hello size of hello provisioned volume, available network bandwidth, and hello data on your device.</span></span>

    5. <span data-ttu-id="007c3-201">指定 hello**佈建的容量**磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-201">Specify hello **Provisioned Capacity** for your volume.</span></span> <span data-ttu-id="007c3-202">記下的 hello 容量可根據選取的 hello 磁碟區類型。</span><span class="sxs-lookup"><span data-stu-id="007c3-202">Make a note of hello capacity that is available based on hello volume type selected.</span></span> <span data-ttu-id="007c3-203">hello 指定磁碟區大小不能超過 hello 可用空間。</span><span class="sxs-lookup"><span data-stu-id="007c3-203">hello specified volume size must not exceed hello available space.</span></span>
      
       <span data-ttu-id="007c3-204">您可以佈建本機固定磁碟區總 too8.5 TB 或向上 too200 TB hello 8100 裝置上的階層式磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-204">You can provision locally pinned volumes up too8.5 TB or tiered volumes up too200 TB on hello 8100 device.</span></span> <span data-ttu-id="007c3-205">您可以在較大 8600 裝置 hello，佈建本機固定磁碟區總 too22.5 TB 或分層的磁碟區總 too500 TB。</span><span class="sxs-lookup"><span data-stu-id="007c3-205">On hello larger 8600 device, you can provision locally pinned volumes up too22.5 TB or tiered volumes up too500 TB.</span></span> <span data-ttu-id="007c3-206">因為 hello 裝置上的本機空間是必要的 toohost hello 工作組的階層式磁碟區，建立本機固定磁碟區會影響 hello 空間可供佈建分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-206">As local space on hello device is required toohost hello working set of tiered volumes, creation of locally pinned volumes impacts hello space available for provisioning tiered volumes.</span></span> <span data-ttu-id="007c3-207">因此，如果您建立固定在本機的磁碟區，建立分層磁碟區的可用空間就會縮小。</span><span class="sxs-lookup"><span data-stu-id="007c3-207">Therefore, if you create a locally pinned volume, space available for creation of tiered volumes is reduced.</span></span> <span data-ttu-id="007c3-208">同樣地，如果建立為分層磁碟區時，就會降低 hello 的可用空間來建立本機固定磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-208">Similarly, if a tiered volume is created, hello available space for creation of locally pinned volumes is reduced.</span></span>
      
       <span data-ttu-id="007c3-209">8100 裝置上佈建 8.5 TB （最大容許大小） 的本機固定磁碟區，如果您已耗盡所有 hello 本機上的可用空間 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="007c3-209">If you provision a locally pinned volume of 8.5 TB (maximum allowable size) on your 8100 device, then you have exhausted all hello local space available on hello device.</span></span> <span data-ttu-id="007c3-210">您無法建立任何階層式磁碟區從該點以後 hello 裝置 toohost hello 工作集 hello 上沒有本機空間分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-210">You can't create any tiered volume from that point onwards as there is no local space on hello device toohost hello working set of hello tiered volume.</span></span> <span data-ttu-id="007c3-211">現有的階層式磁碟區也會影響 hello 的可用空間。</span><span class="sxs-lookup"><span data-stu-id="007c3-211">Existing tiered volumes also affect hello space available.</span></span> <span data-ttu-id="007c3-212">例如，如果您的 8100 裝置已經有大約 106 TB 的分層磁碟區，則固定在本機的磁碟區僅只有 4 TB 的可用空間。</span><span class="sxs-lookup"><span data-stu-id="007c3-212">For example, if you have an 8100 device that already has tiered volumes of roughly 106 TB, only 4 TB of space is available for locally pinned volumes.</span></span>

    6. <span data-ttu-id="007c3-213">在 hello**連線主機**欄位中，按一下 hello 箭號。</span><span class="sxs-lookup"><span data-stu-id="007c3-213">In hello **Connected hosts** field, click hello arrow.</span></span> 

        ![已連線的主機](./media/storsimple-8000-manage-volumes-u2/step5createvol2.png)

    7. <span data-ttu-id="007c3-215">在 hello**連線主機**刀鋒視窗中，選擇現有的 ACR，或加入新的 ACR。</span><span class="sxs-lookup"><span data-stu-id="007c3-215">In hello **Connected hosts** blade, choose an existing ACR or add a new ACR.</span></span> <span data-ttu-id="007c3-216">如果您選擇新的 ACR，然後提供**名稱**acr，提供 hello **iSCSI Qualified Name** (IQN) 的 Windows 主機。</span><span class="sxs-lookup"><span data-stu-id="007c3-216">If you choose a new ACR, then supply a **Name** for your ACR, provide hello **iSCSI Qualified Name** (IQN) of your Windows host.</span></span> <span data-ttu-id="007c3-217">如果您沒有 hello IQN，請移至太[Get hello Windows Server 主機的 IQN](#get-the-iqn-of-a-windows-server-host)。</span><span class="sxs-lookup"><span data-stu-id="007c3-217">If you don't have hello IQN, go too[Get hello IQN of a Windows Server host](#get-the-iqn-of-a-windows-server-host).</span></span> <span data-ttu-id="007c3-218">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="007c3-218">Click **Create**.</span></span> <span data-ttu-id="007c3-219">以指定的 hello 建立磁碟區設定。</span><span class="sxs-lookup"><span data-stu-id="007c3-219">A volume is created with hello specified settings.</span></span>

        ![Click Create](./media/storsimple-8000-manage-volumes-u2/step5createvol3.png)

<span data-ttu-id="007c3-221">您新的磁碟區現在已準備好 toouse。</span><span class="sxs-lookup"><span data-stu-id="007c3-221">Your new volume is now ready toouse.</span></span>

> [!NOTE]
> <span data-ttu-id="007c3-222">如果您建立本機固定磁碟區，然後再建立另一部本機固定磁碟區，立即 hello 磁碟區建立工作之後，以循序方式執行。</span><span class="sxs-lookup"><span data-stu-id="007c3-222">If you create a locally pinned volume and then create another locally pinned volume immediately afterwards, hello volume creation jobs run sequentially.</span></span> <span data-ttu-id="007c3-223">hello 第一個磁碟區建立作業必須完成才能開始進行 hello 下一個磁碟區建立工作。</span><span class="sxs-lookup"><span data-stu-id="007c3-223">hello first volume creation job must finish before hello next volume creation job can begin.</span></span>

## <a name="modify-a-volume"></a><span data-ttu-id="007c3-224">修改磁碟區</span><span class="sxs-lookup"><span data-stu-id="007c3-224">Modify a volume</span></span>

<span data-ttu-id="007c3-225">當您需要 tooexpand 它或變更 hello 存取 hello 的磁碟區的主機時，請修改磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-225">Modify a volume when you need tooexpand it or change hello hosts that access hello volume.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="007c3-226">如果您修改 hello hello 裝置上的磁碟區大小，hello 磁碟區大小需要 toobe hello 主控件上的變更。</span><span class="sxs-lookup"><span data-stu-id="007c3-226">If you modify hello volume size on hello device, hello volume size needs toobe changed on hello host as well.</span></span>
> * <span data-ttu-id="007c3-227">此處所述的 hello 主機端步驟適用於 Windows Server 2012 (2012R2)。</span><span class="sxs-lookup"><span data-stu-id="007c3-227">hello host-side steps described here are for Windows Server 2012 (2012R2).</span></span> <span data-ttu-id="007c3-228">Linux 或其他主機作業系統的程序會有所不同。</span><span class="sxs-lookup"><span data-stu-id="007c3-228">Procedures for Linux or other host operating systems will be different.</span></span> <span data-ttu-id="007c3-229">修改 hello 執行另一個作業系統的主機上的磁碟區時，請參閱 tooyour 主機作業系統的指示。</span><span class="sxs-lookup"><span data-stu-id="007c3-229">Refer tooyour host operating system instructions when modifying hello volume on a host running another operating system.</span></span>

#### <a name="toomodify-a-volume"></a><span data-ttu-id="007c3-230">toomodify 磁碟區</span><span class="sxs-lookup"><span data-stu-id="007c3-230">toomodify a volume</span></span>

1. <span data-ttu-id="007c3-231">在 tooyour StorSimple 裝置管理員服務的 **裝置**。</span><span class="sxs-lookup"><span data-stu-id="007c3-231">Go tooyour StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="007c3-232">從 hello 表格清單中的 hello 裝置，選取您想 toomodify hello 磁碟區的 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="007c3-232">From hello tabular listing of hello devices, select hello device that has hello volume that you intend toomodify.</span></span> <span data-ttu-id="007c3-233">按一下 [設定] > [磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="007c3-233">Click **Settings > Volumes**.</span></span>

    ![移 tooVolumes 刀鋒視窗](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

2. <span data-ttu-id="007c3-235">從 hello 表格式的磁碟區清單，選取 hello 磁碟區，然後 tooinvoke hello 操作功能表上按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="007c3-235">From hello tabular listing of volumes, select hello volume and right-click tooinvoke hello context menu.</span></span> <span data-ttu-id="007c3-236">選取**離線**tootake hello 磁碟區離線，您將修改。</span><span class="sxs-lookup"><span data-stu-id="007c3-236">Select **Take offline** tootake hello volume you will modify offline.</span></span>

    ![選取並讓磁碟區離線](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. <span data-ttu-id="007c3-238">在 hello**離線**刀鋒視窗中，檢閱 hello 影響 hello 磁碟區離線，並選取 hello 對應的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="007c3-238">In hello **Take offline** blade, review hello impact of taking hello volume offline and select hello corresponding checkbox.</span></span> <span data-ttu-id="007c3-239">請確認 hello hello 主機上的對應磁碟區離線第一次。</span><span class="sxs-lookup"><span data-stu-id="007c3-239">Ensure that hello corresponding volume on hello host is offline first.</span></span> <span data-ttu-id="007c3-240">如需如何 tootake 離線的磁碟區在主機伺服器上連接 tooStorSimple 資訊，請參閱 toooperating 系統的特定指示。</span><span class="sxs-lookup"><span data-stu-id="007c3-240">For information on how tootake a volume offline on your host server connected tooStorSimple, refer toooperating system specific instructions.</span></span> <span data-ttu-id="007c3-241">按一下 [離線]。</span><span class="sxs-lookup"><span data-stu-id="007c3-241">Click **Take offline**.</span></span>

    ![檢閱讓磁碟區離線的影響](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

4. <span data-ttu-id="007c3-243">Hello 磁碟區已離線 （如所示 hello 磁碟區狀態） 之後，選擇 hello 磁碟區，然後以滑鼠右鍵按一下 tooinvoke hello 操作功能表。</span><span class="sxs-lookup"><span data-stu-id="007c3-243">After hello volume is offline (as shown by hello volume status), select hello volume and right-click tooinvoke hello context menu.</span></span> <span data-ttu-id="007c3-244">選取 [修改磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="007c3-244">Select **Modify volume**.</span></span>

    ![選取 [修改磁碟區]](./media/storsimple-8000-manage-volumes-u2/modifyvol9.png)


5. <span data-ttu-id="007c3-246">在 hello**修改磁碟區**刀鋒視窗中，您可以進行下列變更 hello:</span><span class="sxs-lookup"><span data-stu-id="007c3-246">In hello **Modify volume** blade, you can make hello following changes:</span></span>
   
   1. <span data-ttu-id="007c3-247">hello 磁碟區**名稱**無法編輯。</span><span class="sxs-lookup"><span data-stu-id="007c3-247">hello volume **Name** cannot be edited.</span></span>
   2. <span data-ttu-id="007c3-248">轉換 hello**類型**從本機固定 tootiered 或釘選的分層式 toolocally (請參閱[變更 hello 磁碟區類型](#change-the-volume-type)如需詳細資訊)。</span><span class="sxs-lookup"><span data-stu-id="007c3-248">Convert hello **Type** from locally pinned tootiered or from tiered toolocally pinned (see [Change hello volume type](#change-the-volume-type) for more information).</span></span>
   3. <span data-ttu-id="007c3-249">增加 hello**佈建的容量**。</span><span class="sxs-lookup"><span data-stu-id="007c3-249">Increase hello **Provisioned Capacity**.</span></span> <span data-ttu-id="007c3-250">hello**佈建的容量**只能增加。</span><span class="sxs-lookup"><span data-stu-id="007c3-250">hello **Provisioned Capacity** can only be increased.</span></span> <span data-ttu-id="007c3-251">您無法在磁碟區建立後予以壓縮。</span><span class="sxs-lookup"><span data-stu-id="007c3-251">You cannot shrink a volume after it is created.</span></span>
   4. <span data-ttu-id="007c3-252">在下**連線主機**，您可以修改 hello ACR。</span><span class="sxs-lookup"><span data-stu-id="007c3-252">Under **Connected hosts**, you can modify hello ACR.</span></span> <span data-ttu-id="007c3-253">toomodify ACR，hello 磁碟區必須處於離線狀態。</span><span class="sxs-lookup"><span data-stu-id="007c3-253">toomodify an ACR, hello volume must be offline.</span></span>

       ![檢閱讓磁碟區離線的影響](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

5. <span data-ttu-id="007c3-255">按一下**儲存**toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="007c3-255">Click **Save** toosave your changes.</span></span> <span data-ttu-id="007c3-256">系統提示您進行確認時，按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="007c3-256">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="007c3-257">hello Azure 入口網站將會顯示更新的磁碟區訊息。</span><span class="sxs-lookup"><span data-stu-id="007c3-257">hello Azure portal will display an updating volume message.</span></span> <span data-ttu-id="007c3-258">已成功更新 hello 磁碟區時，它會顯示成功訊息。</span><span class="sxs-lookup"><span data-stu-id="007c3-258">It will display a success message when hello volume has been successfully updated.</span></span>

    ![檢閱讓磁碟區離線的影響](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

7. <span data-ttu-id="007c3-260">如果您要擴充磁碟區，完成下列步驟在您的 Windows 主機電腦上的 hello:</span><span class="sxs-lookup"><span data-stu-id="007c3-260">If you are expanding a volume, complete hello following steps on your Windows host computer:</span></span>
   
   1. <span data-ttu-id="007c3-261">跳過**電腦管理** ->**磁碟管理**。</span><span class="sxs-lookup"><span data-stu-id="007c3-261">Go too**Computer Management** ->**Disk Management**.</span></span>
   2. <span data-ttu-id="007c3-262">以滑鼠右鍵按一下 [磁碟管理]，並選取 [重新掃描磁碟]。</span><span class="sxs-lookup"><span data-stu-id="007c3-262">Right-click **Disk Management** and select **Rescan Disks**.</span></span>
   3. <span data-ttu-id="007c3-263">在 hello 清單中的磁碟，選取您更新的 hello 磁碟區、 按一下滑鼠右鍵，然後選取**延伸磁碟區**。</span><span class="sxs-lookup"><span data-stu-id="007c3-263">In hello list of disks, select hello volume that you updated, right-click, and then select **Extend Volume**.</span></span> <span data-ttu-id="007c3-264">hello 延伸磁碟區精靈 隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="007c3-264">hello Extend Volume wizard starts.</span></span> <span data-ttu-id="007c3-265">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="007c3-265">Click **Next**.</span></span>
   4. <span data-ttu-id="007c3-266">完成 hello 精靈，接受 hello 的預設值。</span><span class="sxs-lookup"><span data-stu-id="007c3-266">Complete hello wizard, accepting hello default values.</span></span> <span data-ttu-id="007c3-267">Hello 精靈完成後，hello 磁碟區應該會顯示 hello 增加大小。</span><span class="sxs-lookup"><span data-stu-id="007c3-267">After hello wizard is finished, hello volume should show hello increased size.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="007c3-268">如果您展開本機固定磁碟區，然後展開本機另一個 hello 磁碟區延伸作業之後，以循序方式執行，請立即固定磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-268">If you expand a locally pinned volume and then expand another locally pinned volume immediately afterwards, hello volume expansion jobs run sequentially.</span></span> <span data-ttu-id="007c3-269">hello 第一個磁碟區擴充工作必須完成才能開始進行下一個磁碟區擴充工作 hello。</span><span class="sxs-lookup"><span data-stu-id="007c3-269">hello first volume expansion job must finish before hello next volume expansion job can begin.</span></span>
      

## <a name="change-hello-volume-type"></a><span data-ttu-id="007c3-270">變更 hello 磁碟區類型</span><span class="sxs-lookup"><span data-stu-id="007c3-270">Change hello volume type</span></span>

<span data-ttu-id="007c3-271">您可以變更 hello 磁碟區類型從分層式 toolocally 釘選，或從本機固定 tootiered。</span><span class="sxs-lookup"><span data-stu-id="007c3-271">You can change hello volume type from tiered toolocally pinned or from locally pinned tootiered.</span></span> <span data-ttu-id="007c3-272">不過，這種轉換不應該經常發生。</span><span class="sxs-lookup"><span data-stu-id="007c3-272">However, this conversion should not be a frequent occurrence.</span></span>

### <a name="tiered-toolocal-volume-conversion-considerations"></a><span data-ttu-id="007c3-273">階層式的 toolocal 磁碟區轉換考量</span><span class="sxs-lookup"><span data-stu-id="007c3-273">Tiered toolocal volume conversion considerations</span></span>

<span data-ttu-id="007c3-274">某些階層式 toolocally 釘選的轉換磁碟區的原因如下：</span><span class="sxs-lookup"><span data-stu-id="007c3-274">Some reasons for converting a volume from tiered toolocally pinned are:</span></span>

* <span data-ttu-id="007c3-275">關於資料可用性和效能的本機保證</span><span class="sxs-lookup"><span data-stu-id="007c3-275">Local guarantees regarding data availability and performance</span></span>
* <span data-ttu-id="007c3-276">消除雲端延遲和雲端連線問題。</span><span class="sxs-lookup"><span data-stu-id="007c3-276">Elimination of cloud latencies and cloud connectivity issues.</span></span>

<span data-ttu-id="007c3-277">一般來說，這些是小型經常想 tooaccess 的現有磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-277">Typically, these are small existing volumes that you want tooaccess frequently.</span></span> <span data-ttu-id="007c3-278">當固定在本機的磁碟區建立時，它就會完整佈建。</span><span class="sxs-lookup"><span data-stu-id="007c3-278">A locally pinned volume is fully provisioned when it is created.</span></span> 

<span data-ttu-id="007c3-279">如果您想要轉換的階層式磁碟區 tooa 固定在本機磁碟區，StorSimple 會確認您在裝置上有足夠的空間，開始 hello 轉換之前。</span><span class="sxs-lookup"><span data-stu-id="007c3-279">If you are converting a tiered volume tooa locally pinned volume, StorSimple verifies that you have sufficient space on your device before it starts hello conversion.</span></span> <span data-ttu-id="007c3-280">如果您有足夠的空間，您會收到錯誤，且會取消 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="007c3-280">If you have insufficient space, you will receive an error and hello operation will be canceled.</span></span> 

> [!NOTE]
> <span data-ttu-id="007c3-281">開始從釘選的分層式 toolocally 轉換之前，請確定您考慮 hello 空間需求的其他工作負載。</span><span class="sxs-lookup"><span data-stu-id="007c3-281">Before you begin a conversion from tiered toolocally pinned, make sure that you consider hello space requirements of your other workloads.</span></span> 

<span data-ttu-id="007c3-282">從階層式的 tooa 固定在本機磁碟區的轉換可能會影響裝置的效能。</span><span class="sxs-lookup"><span data-stu-id="007c3-282">Conversion from a tiered tooa locally pinned volume can adversely affect device performance.</span></span> <span data-ttu-id="007c3-283">此外，hello 下列因素可能會增加 hello toocomplete hello 轉換所花費的時間：</span><span class="sxs-lookup"><span data-stu-id="007c3-283">Additionally, hello following factors might increase hello time it takes toocomplete hello conversion:</span></span>

* <span data-ttu-id="007c3-284">頻寬不足。</span><span class="sxs-lookup"><span data-stu-id="007c3-284">There is insufficient bandwidth.</span></span>
* <span data-ttu-id="007c3-285">沒有最新備份。</span><span class="sxs-lookup"><span data-stu-id="007c3-285">There is no current backup.</span></span>

<span data-ttu-id="007c3-286">這些因素可能會有的 toominimize hello 效果：</span><span class="sxs-lookup"><span data-stu-id="007c3-286">toominimize hello effects that these factors may have:</span></span>

* <span data-ttu-id="007c3-287">請檢閱頻寬節流設定原則，並確認有專用的 40 Mbps 頻寬。</span><span class="sxs-lookup"><span data-stu-id="007c3-287">Review your bandwidth throttling policies and make sure that a dedicated 40 Mbps bandwidth is available.</span></span>
* <span data-ttu-id="007c3-288">排程離峰時間的 hello 轉換。</span><span class="sxs-lookup"><span data-stu-id="007c3-288">Schedule hello conversion for off-peak hours.</span></span>
* <span data-ttu-id="007c3-289">在開始 hello 轉換之前，請建立的雲端快照。</span><span class="sxs-lookup"><span data-stu-id="007c3-289">Take a cloud snapshot before you start hello conversion.</span></span>

<span data-ttu-id="007c3-290">如果您想要轉換多個磁碟區 （支援不同的工作負載），您應該設定 hello 磁碟區轉換優先權，優先權較高的磁碟區會先轉換。</span><span class="sxs-lookup"><span data-stu-id="007c3-290">If you are converting multiple volumes (supporting different workloads), then you should prioritize hello volume conversion so that higher priority volumes are converted first.</span></span> <span data-ttu-id="007c3-291">例如，您應該先轉換裝載虛擬機器 (VM) 的磁碟區，或具有 SQL 工作負載的磁碟區，然後才轉換檔案共用工作負載的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-291">For example, you should convert volumes that host virtual machines (VMs) or volumes with SQL workloads before you convert volumes with file share workloads.</span></span>

### <a name="local-tootiered-volume-conversion-considerations"></a><span data-ttu-id="007c3-292">本機 tootiered 磁碟區轉換考量</span><span class="sxs-lookup"><span data-stu-id="007c3-292">Local tootiered volume conversion considerations</span></span>

<span data-ttu-id="007c3-293">您可以在本機固定磁碟區 tooa toochange 分層磁碟區如果您需要額外的空間 tooprovision 其他磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-293">You may want toochange a locally pinned volume tooa tiered volume if you need additional space tooprovision other volumes.</span></span> <span data-ttu-id="007c3-294">當您轉換 hello 固定在本機磁碟區 tootiered 時，hello hello 釋出容量大小會增加 hello hello 裝置上的可用容量。</span><span class="sxs-lookup"><span data-stu-id="007c3-294">When you convert hello locally pinned volume tootiered, hello available capacity on hello device increases by hello size of hello released capacity.</span></span> <span data-ttu-id="007c3-295">如果連線問題會使磁碟區的 hello 轉換從 hello 區域型別 toohello 層型別，hello 本機磁碟區會展示分層磁碟區的內容之前 hello 轉換已完成。</span><span class="sxs-lookup"><span data-stu-id="007c3-295">If connectivity issues prevent hello conversion of a volume from hello local type toohello tiered type, hello local volume will exhibit properties of a tiered volume until hello conversion is complete.</span></span> <span data-ttu-id="007c3-296">這是因為某些資料可能會溢出 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="007c3-296">This is because some data might have spilled toohello cloud.</span></span> <span data-ttu-id="007c3-297">此餘力的資料會繼續 toooccupy hello 作業會重新啟動時，完成之前無法釋放的 hello 裝置上的本機空間。</span><span class="sxs-lookup"><span data-stu-id="007c3-297">This spilled data continues toooccupy local space on hello device that cannot be freed until hello operation is restarted and completed.</span></span>

> [!NOTE]
> <span data-ttu-id="007c3-298">轉換磁碟區可能需要一些時間，且您在啟動之後無法取消轉換。</span><span class="sxs-lookup"><span data-stu-id="007c3-298">Converting a volume can take some time and you cannot cancel a conversion after it starts.</span></span> <span data-ttu-id="007c3-299">hello 磁碟區仍在進行 hello 轉換時，線上和才能進行備份，但您無法展開或 hello 轉換正在進行時，還原 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-299">hello volume remains online during hello conversion, and you can take backups, but you cannot expand or restore hello volume while hello conversion is taking place.</span></span>


#### <a name="toochange-hello-volume-type"></a><span data-ttu-id="007c3-300">toochange hello 磁碟區類型</span><span class="sxs-lookup"><span data-stu-id="007c3-300">toochange hello volume type</span></span>

1. <span data-ttu-id="007c3-301">在 tooyour StorSimple 裝置管理員服務的 **裝置**。</span><span class="sxs-lookup"><span data-stu-id="007c3-301">Go tooyour StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="007c3-302">從 hello 表格清單中的 hello 裝置，選取您想 toomodify hello 磁碟區的 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="007c3-302">From hello tabular listing of hello devices, select hello device that has hello volume that you intend toomodify.</span></span> <span data-ttu-id="007c3-303">按一下 [設定] > [磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="007c3-303">Click **Settings > Volumes**.</span></span>

    ![移 tooVolumes 刀鋒視窗](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. <span data-ttu-id="007c3-305">從 hello 表格式的磁碟區清單，選取 hello 磁碟區，然後 tooinvoke hello 操作功能表上按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="007c3-305">From hello tabular listing of volumes, select hello volume and right-click tooinvoke hello context menu.</span></span> <span data-ttu-id="007c3-306">選取 [修改]。</span><span class="sxs-lookup"><span data-stu-id="007c3-306">Select **Modify**.</span></span>

    ![從操作功能表選取 [修改]](./media/storsimple-8000-manage-volumes-u2/changevoltype2.png)

4. <span data-ttu-id="007c3-308">在 hello**修改磁碟區**刀鋒視窗中，變更 hello 磁碟區類型從 hello 選取 hello 新類型**類型**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="007c3-308">On hello **Modify volume** blade, change hello volume type by selecting hello new type from hello **Type** drop-down list.</span></span>
   
   * <span data-ttu-id="007c3-309">如果您要變更 hello 類型太**固定在本機**，StorSimple 會檢查 toosee，如果沒有足夠的容量。</span><span class="sxs-lookup"><span data-stu-id="007c3-309">If you are changing hello type too**Locally pinned**, StorSimple will check toosee if there is sufficient capacity.</span></span>
   * <span data-ttu-id="007c3-310">如果您要變更 hello 類型太**分層**及此磁碟區會用於封存資料，選取 hello**對於不常存取的封存資料，使用此磁碟區**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="007c3-310">If you are changing hello type too**Tiered** and this volume will be used for archival data, select hello **Use this volume for less frequently accessed archival data** check box.</span></span>
   * <span data-ttu-id="007c3-311">如果您要設定本機固定磁碟區，如層或_反之亦然_，hello 會出現下列訊息。</span><span class="sxs-lookup"><span data-stu-id="007c3-311">If you are configuring a locally pinned volume as tiered or _vice-versa_, hello following message appears.</span></span>
   
    ![變更磁碟區類型訊息](./media/storsimple-8000-manage-volumes-u2/changevoltype3.png)

7. <span data-ttu-id="007c3-313">按一下**儲存**toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="007c3-313">Click **Save** toosave hello changes.</span></span> <span data-ttu-id="007c3-314">當提示確認，請按一下**是**toostart hello 轉換程序。</span><span class="sxs-lookup"><span data-stu-id="007c3-314">When prompted for confirmation, click **Yes** toostart hello conversion process.</span></span> 

    ![儲存並確認](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

8. <span data-ttu-id="007c3-316">hello Azure 入口網站會顯示 hello 建立工作，會更新 hello 磁碟區的通知。</span><span class="sxs-lookup"><span data-stu-id="007c3-316">hello Azure portal displays a notification for hello job creation that would update hello volume.</span></span> <span data-ttu-id="007c3-317">按一下 hello 通知 toomonitor hello 狀態 hello 磁碟區轉換工作。</span><span class="sxs-lookup"><span data-stu-id="007c3-317">Click on hello notification toomonitor hello status of hello volume conversion job.</span></span>

    ![磁碟區轉換作業](./media/storsimple-8000-manage-volumes-u2/changevoltype5.png)

## <a name="take-a-volume-offline"></a><span data-ttu-id="007c3-319">使磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="007c3-319">Take a volume offline</span></span>

<span data-ttu-id="007c3-320">當您計劃 toomodify 或刪除 hello 磁碟區時，您可能需要 tootake 磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="007c3-320">You may need tootake a volume offline when you are planning toomodify or delete hello volume.</span></span> <span data-ttu-id="007c3-321">當磁碟區離線時，即無法進行讀寫存取。</span><span class="sxs-lookup"><span data-stu-id="007c3-321">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="007c3-322">您必須採取 hello 上的磁碟區離線 hello 主機和 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="007c3-322">You must take hello volume offline on hello host and hello device.</span></span>

#### <a name="tootake-a-volume-offline"></a><span data-ttu-id="007c3-323">tootake 磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="007c3-323">tootake a volume offline</span></span>

1. <span data-ttu-id="007c3-324">請確定有問題的 hello 磁碟區不是使用中，再將其離線。</span><span class="sxs-lookup"><span data-stu-id="007c3-324">Make sure that hello volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="007c3-325">Hello 主機上的 hello 磁碟區離線讓第一次。</span><span class="sxs-lookup"><span data-stu-id="007c3-325">Take hello volume offline on hello host first.</span></span> <span data-ttu-id="007c3-326">這可免除 hello 磁碟區上的資料損毀的任何潛在風險。</span><span class="sxs-lookup"><span data-stu-id="007c3-326">This eliminates any potential risk of data corruption on hello volume.</span></span> <span data-ttu-id="007c3-327">如需特定步驟，請參閱主機作業系統的 toohello 指示。</span><span class="sxs-lookup"><span data-stu-id="007c3-327">For specific steps, refer toohello instructions for your host operating system.</span></span>
3. <span data-ttu-id="007c3-328">Hello 主機已離線後，採用的離線 hello 裝置 hello 磁碟區，藉由執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="007c3-328">After hello host is offline, take hello volume on hello device offline by performing hello following steps:</span></span>
   
    1. <span data-ttu-id="007c3-329">在 tooyour StorSimple 裝置管理員服務的 **裝置**。</span><span class="sxs-lookup"><span data-stu-id="007c3-329">Go tooyour StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="007c3-330">從 hello 表格清單中的 hello 裝置，選取您想 toomodify hello 磁碟區的 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="007c3-330">From hello tabular listing of hello devices, select hello device that has hello volume that you intend toomodify.</span></span> <span data-ttu-id="007c3-331">按一下 [設定] > [磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="007c3-331">Click **Settings > Volumes**.</span></span>

        ![移 tooVolumes 刀鋒視窗](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

    2. <span data-ttu-id="007c3-333">從 hello 表格式的磁碟區清單，選取 hello 磁碟區，然後 tooinvoke hello 操作功能表上按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="007c3-333">From hello tabular listing of volumes, select hello volume and right-click tooinvoke hello context menu.</span></span> <span data-ttu-id="007c3-334">選取**離線**tootake hello 磁碟區離線，您將修改。</span><span class="sxs-lookup"><span data-stu-id="007c3-334">Select **Take offline** tootake hello volume you will modify offline.</span></span>

        ![選取並讓磁碟區離線](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. <span data-ttu-id="007c3-336">在 hello**離線**刀鋒視窗中，檢閱 hello 影響 hello 磁碟區離線，並選取 hello 對應的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="007c3-336">In hello **Take offline** blade, review hello impact of taking hello volume offline and select hello corresponding checkbox.</span></span> <span data-ttu-id="007c3-337">按一下 [離線]。</span><span class="sxs-lookup"><span data-stu-id="007c3-337">Click **Take offline**.</span></span> 

    ![檢閱讓磁碟區離線的影響](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)
      
      <span data-ttu-id="007c3-339">Hello 磁碟區離線時，會通知您。</span><span class="sxs-lookup"><span data-stu-id="007c3-339">You are notified when hello volume is offline.</span></span> <span data-ttu-id="007c3-340">hello 磁碟區狀態也會更新 tooOffline。</span><span class="sxs-lookup"><span data-stu-id="007c3-340">hello volume status also updates tooOffline.</span></span>
      
4. <span data-ttu-id="007c3-341">磁碟區離線，如果您選取 hello 磁碟區並按一下滑鼠右鍵後,**上線**hello 內容功能表中的選項可用。</span><span class="sxs-lookup"><span data-stu-id="007c3-341">After a volume is offline, if you select hello volume and right-click, **Bring Online** option becomes available in hello context menu.</span></span>

> [!NOTE]
> <span data-ttu-id="007c3-342">hello**離線**命令會傳送要求 toohello 裝置 tootake hello 磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="007c3-342">hello **Take Offline** command sends a request toohello device tootake hello volume offline.</span></span> <span data-ttu-id="007c3-343">如果主機仍在使用 hello 磁碟區，這會導致連線中斷，但離線 hello 磁碟區將不會失敗。</span><span class="sxs-lookup"><span data-stu-id="007c3-343">If hosts are still using hello volume, this results in broken connections, but taking hello volume offline will not fail.</span></span>

## <a name="delete-a-volume"></a><span data-ttu-id="007c3-344">刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="007c3-344">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="007c3-345">只有當磁碟區離線時，您才能予以刪除。</span><span class="sxs-lookup"><span data-stu-id="007c3-345">You can delete a volume only if it is offline.</span></span>

<span data-ttu-id="007c3-346">完成下列步驟 toodelete 磁碟區的 hello。</span><span class="sxs-lookup"><span data-stu-id="007c3-346">Complete hello following steps toodelete a volume.</span></span>

#### <a name="toodelete-a-volume"></a><span data-ttu-id="007c3-347">toodelete 磁碟區</span><span class="sxs-lookup"><span data-stu-id="007c3-347">toodelete a volume</span></span>

1. <span data-ttu-id="007c3-348">在 tooyour StorSimple 裝置管理員服務的 **裝置**。</span><span class="sxs-lookup"><span data-stu-id="007c3-348">Go tooyour StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="007c3-349">從 hello 表格清單中的 hello 裝置，選取您想 toomodify hello 磁碟區的 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="007c3-349">From hello tabular listing of hello devices, select hello device that has hello volume that you intend toomodify.</span></span> <span data-ttu-id="007c3-350">按一下 [設定] > [磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="007c3-350">Click **Settings > Volumes**.</span></span>

    ![移 tooVolumes 刀鋒視窗](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. <span data-ttu-id="007c3-352">檢查 hello 狀態想 toodelete hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-352">Check hello status of hello volume you want toodelete.</span></span> <span data-ttu-id="007c3-353">如果您想要 toodelete hello 磁碟區未離線，先使其離線。</span><span class="sxs-lookup"><span data-stu-id="007c3-353">If hello volume you want toodelete is not offline, take it offline first.</span></span> <span data-ttu-id="007c3-354">中的 hello 步驟[使磁碟區離線](#take-a-volume-offline)。</span><span class="sxs-lookup"><span data-stu-id="007c3-354">Follow hello steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="007c3-355">Hello 磁碟區離線後，選取 hello 磁碟區、 tooinvoke hello 操作功能表上按一下滑鼠右鍵，然後選取**刪除**。</span><span class="sxs-lookup"><span data-stu-id="007c3-355">After hello volume is offline, select hello volume, right-click tooinvoke hello context menu and then select **Delete**.</span></span>

    ![從操作功能表選取 [刪除]](./media/storsimple-8000-manage-volumes-u2/deletevol1.png)

5. <span data-ttu-id="007c3-357">在 hello**刪除**刀鋒視窗中，檢閱和選取 hello 針對 hello 影響刪除磁碟區的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="007c3-357">In hello **Delete** blade, review and select hello checkbox against hello impact of deleting a volume.</span></span> <span data-ttu-id="007c3-358">當您刪除磁碟區時，位於 hello 磁碟區的所有 hello 資料都會遺失。</span><span class="sxs-lookup"><span data-stu-id="007c3-358">When you delete a volume, all hello data that resides on hello volume is lost.</span></span> 

    ![儲存並確認變更](./media/storsimple-8000-manage-volumes-u2/deletevol2.png)

6. <span data-ttu-id="007c3-360">刪除 hello 磁碟區之後，更新 tooindicate hello 刪除磁碟區 hello 表格式清單。</span><span class="sxs-lookup"><span data-stu-id="007c3-360">After hello volume is deleted, hello tabular list of volumes updates tooindicate hello deletion.</span></span>

    ![更新磁碟區清單](./media/storsimple-8000-manage-volumes-u2/deletevol3.png)
   
   > [!NOTE]
   > <span data-ttu-id="007c3-362">如果您刪除本機固定磁碟區，可能不會立即更新 hello 空間供新磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-362">If you delete a locally pinned volume, hello space available for new volumes may not be updated immediately.</span></span> <span data-ttu-id="007c3-363">hello StorSimple 裝置管理員服務會定期更新 hello 可用的本機空間。</span><span class="sxs-lookup"><span data-stu-id="007c3-363">hello StorSimple Device Manager Service updates hello local space available periodically.</span></span> <span data-ttu-id="007c3-364">我們建議您等待幾分鐘的時間再 toocreate hello 新磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-364">We suggest you wait for a few minutes before you try toocreate hello new volume.</span></span>
   >
   > <span data-ttu-id="007c3-365">此外，如果您刪除本機固定磁碟區，然後再刪除另一部本機固定磁碟區，立即 hello 大量刪除作業之後，以循序方式執行。</span><span class="sxs-lookup"><span data-stu-id="007c3-365">Additionally, if you delete a locally pinned volume and then delete another locally pinned volume immediately afterwards, hello volume deletion jobs run sequentially.</span></span> <span data-ttu-id="007c3-366">hello 第一個磁碟區刪除工作必須完成才能開始進行下一個磁碟區刪除工作 hello。</span><span class="sxs-lookup"><span data-stu-id="007c3-366">hello first volume deletion job must finish before hello next volume deletion job can begin.</span></span>

## <a name="monitor-a-volume"></a><span data-ttu-id="007c3-367">監視磁碟區</span><span class="sxs-lookup"><span data-stu-id="007c3-367">Monitor a volume</span></span>

<span data-ttu-id="007c3-368">磁碟區監視可讓您的磁碟區的 toocollect 我 I/O 相關統計資料。</span><span class="sxs-lookup"><span data-stu-id="007c3-368">Volume monitoring allows you toocollect I/O-related statistics for a volume.</span></span> <span data-ttu-id="007c3-369">預設值為 hello 會啟用監視您所建立的前 32 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-369">Monitoring is enabled by default for hello first 32 volumes that you create.</span></span> <span data-ttu-id="007c3-370">預設會停用監視其他磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-370">Monitoring of additional volumes is disabled by default.</span></span> 

> [!NOTE]
> <span data-ttu-id="007c3-371">預設會停用監視複製的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="007c3-371">Monitoring of cloned volumes is disabled by default.</span></span>


<span data-ttu-id="007c3-372">執行下列步驟 tooenable hello 或停用磁碟區的監視。</span><span class="sxs-lookup"><span data-stu-id="007c3-372">Perform hello following steps tooenable or disable monitoring for a volume.</span></span>

#### <a name="tooenable-or-disable-volume-monitoring"></a><span data-ttu-id="007c3-373">tooenable 或停用磁碟區監視</span><span class="sxs-lookup"><span data-stu-id="007c3-373">tooenable or disable volume monitoring</span></span>

1. <span data-ttu-id="007c3-374">在 tooyour StorSimple 裝置管理員服務的 **裝置**。</span><span class="sxs-lookup"><span data-stu-id="007c3-374">Go tooyour StorSimple Device Manager service and then click **Devices**.</span></span> <span data-ttu-id="007c3-375">從 hello 表格清單中的 hello 裝置，選取您想 toomodify hello 磁碟區的 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="007c3-375">From hello tabular listing of hello devices, select hello device that has hello volume that you intend toomodify.</span></span> <span data-ttu-id="007c3-376">按一下 [設定] > [磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="007c3-376">Click **Settings > Volumes**.</span></span>
2. <span data-ttu-id="007c3-377">從 hello 表格式的磁碟區清單，選取 hello 磁碟區，然後 tooinvoke hello 操作功能表上按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="007c3-377">From hello tabular listing of volumes, select hello volume and right-click tooinvoke hello context menu.</span></span> <span data-ttu-id="007c3-378">選取 [修改]。</span><span class="sxs-lookup"><span data-stu-id="007c3-378">Select **Modify**.</span></span>
3. <span data-ttu-id="007c3-379">在 hello**修改磁碟區**刀鋒視窗中，針對**監視**選取**啟用**或**停用**tooenable 或停用監視。</span><span class="sxs-lookup"><span data-stu-id="007c3-379">In hello **Modify volume** blade, for **Monitoring** select **Enable** or **Disable** tooenable or disable monitoring.</span></span>

    ![停用監視](./media/storsimple-8000-manage-volumes-u2/monitorvol1.png) 

4. <span data-ttu-id="007c3-381">按一下 [儲存]，當系統提示您進行確認時，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="007c3-381">Click **Save** and when prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="007c3-382">hello Azure 入口網站會顯示 hello 磁碟區已成功更新之後更新 hello 磁碟區，然後成功訊息的通知。</span><span class="sxs-lookup"><span data-stu-id="007c3-382">hello Azure portal displays a notification for updating hello volume and then a success message, after hello volume is successfully updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="007c3-383">後續步驟</span><span class="sxs-lookup"><span data-stu-id="007c3-383">Next steps</span></span>

* <span data-ttu-id="007c3-384">了解如何太[複製 StorSimple 磁碟區](storsimple-8000-clone-volume-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="007c3-384">Learn how too[clone a StorSimple volume](storsimple-8000-clone-volume-u2.md).</span></span>
* <span data-ttu-id="007c3-385">了解如何太[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="007c3-385">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>


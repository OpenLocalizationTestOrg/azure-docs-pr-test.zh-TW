---
title: "aaaManage StorSimple 磁碟區 |Microsoft 文件"
description: "說明如何 tooadd、 修改、 監視及刪除 StorSimple 磁碟區，以及如何 tootake 它們只有在必要時離線。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ccabd859-590c-4568-a81d-6ff38f125be3
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/11/2016
ms.author: v-sharos
ms.openlocfilehash: 8dc646261ee2ad8f2b80291518716f4de55b63f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-volumes"></a><span data-ttu-id="c193b-103">使用 hello StorSimple Manager 服務 toomanage 磁碟區</span><span class="sxs-lookup"><span data-stu-id="c193b-103">Use hello StorSimple Manager service toomanage volumes</span></span>
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a><span data-ttu-id="c193b-104">概觀</span><span class="sxs-lookup"><span data-stu-id="c193b-104">Overview</span></span>
<span data-ttu-id="c193b-105">本教學課程將說明 toouse hello StorSimple Manager 服務 toocreate 並管理 hello StorSimple 裝置和 StorSimple 虛擬裝置上的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c193b-105">This tutorial explains how toouse hello StorSimple Manager service toocreate and manage volumes on hello StorSimple device and StorSimple virtual device.</span></span>

<span data-ttu-id="c193b-106">hello StorSimple Manager 服務是 hello Azure 傳統入口網站，可讓您從單一 web 介面來管理您的 StorSimple 解決方案的延伸。</span><span class="sxs-lookup"><span data-stu-id="c193b-106">hello StorSimple Manager service is an extension of hello Azure classic portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="c193b-107">加法 toomanaging 磁碟區，您可以使用 hello StorSimple Manager 服務 toocreate 和管理 StorSimple 服務、 檢視和管理裝置、 檢視警示，以及檢視和管理備份原則與 hello 備份類別目錄。</span><span class="sxs-lookup"><span data-stu-id="c193b-107">In addition toomanaging volumes, you can use hello StorSimple Manager service toocreate and manage StorSimple services, view and manage devices, view alerts, and view and manage backup policies and hello backup catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="c193b-108">Azure StorSimple 只能建立精簡佈建的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c193b-108">Azure StorSimple can create thinly provisioned volumes only.</span></span> <span data-ttu-id="c193b-109">您無法在 Azure StorSimple 系統上建立完整佈建或部分佈建的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c193b-109">You cannot create fully provisioned or partially provisioned volumes on an Azure StorSimple system.</span></span>
> 
> <span data-ttu-id="c193b-110">精簡佈建是一種虛擬化技術，可用的存放裝置會出現 tooexceed 實體資源。</span><span class="sxs-lookup"><span data-stu-id="c193b-110">Thin provisioning is a virtualization technology in which available storage appears tooexceed physical resources.</span></span> <span data-ttu-id="c193b-111">而是會預先保留足夠的儲存空間，Azure StorSimple 會使用精簡佈建 tooallocate 剛好足夠空間 toomeet 目前的需求。</span><span class="sxs-lookup"><span data-stu-id="c193b-111">Instead of reserving sufficient storage in advance, Azure StorSimple uses thin provisioning tooallocate just enough space toomeet current requirements.</span></span> <span data-ttu-id="c193b-112">hello 彈性本質的雲端儲存體促進這種方法，因為 Azure StorSimple 可以增加或減少雲端儲存體 toomeet 需求的變更。</span><span class="sxs-lookup"><span data-stu-id="c193b-112">hello elastic nature of cloud storage facilitates this approach because Azure StorSimple can increase or decrease cloud storage toomeet changing demands.</span></span>
> 
> 

## <a name="hello-volumes-page"></a><span data-ttu-id="c193b-113">hello 磁碟區 頁面</span><span class="sxs-lookup"><span data-stu-id="c193b-113">hello Volumes page</span></span>
<span data-ttu-id="c193b-114">hello**磁碟區**頁面可讓您 toomanage hello 存放磁碟區 hello 為啟動器 （伺服器） 的 Microsoft Azure StorSimple 裝置上佈建。</span><span class="sxs-lookup"><span data-stu-id="c193b-114">hello **Volumes** page allows you toomanage hello storage volumes that are provisioned on hello Microsoft Azure StorSimple device for your initiators (servers).</span></span> <span data-ttu-id="c193b-115">它會顯示您的 StorSimple 裝置的磁碟區的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="c193b-115">It displays hello list of volumes on your StorSimple device.</span></span>

 ![磁碟區頁面](./media/storsimple-manage-volumes/HCS_VolumesPage.png)

<span data-ttu-id="c193b-117">磁碟區是由一系列屬性所組成：</span><span class="sxs-lookup"><span data-stu-id="c193b-117">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="c193b-118">**名稱**– 描述性的名稱必須是唯一的可協助識別 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c193b-118">**Name** – A descriptive name that must be unique and helps identify hello volume.</span></span> <span data-ttu-id="c193b-119">這個名稱也可在您篩選特定磁碟區時用於監視報告。</span><span class="sxs-lookup"><span data-stu-id="c193b-119">This name is also used in monitoring reports when you filter on a specific volume.</span></span>
* <span data-ttu-id="c193b-120">**狀態** – 可為連線或離線。</span><span class="sxs-lookup"><span data-stu-id="c193b-120">**Status** – Can be online or offline.</span></span> <span data-ttu-id="c193b-121">如果磁碟區離線，並不允許存取 toouse hello 磁碟區的可見 tooinitiators （伺服器）。</span><span class="sxs-lookup"><span data-stu-id="c193b-121">If a volume if offline, it is not visible tooinitiators (servers) that are allowed access toouse hello volume.</span></span>
* <span data-ttu-id="c193b-122">**容量**– 指定 hello 多大的磁碟區時，看得見 hello 啟動器 （伺服器）。</span><span class="sxs-lookup"><span data-stu-id="c193b-122">**Capacity** – Specifies how large hello volume is, as perceived by hello initiator (server).</span></span> <span data-ttu-id="c193b-123">容量指定 hello 的 hello 啟動器 （伺服器） 來儲存的資料量總計。</span><span class="sxs-lookup"><span data-stu-id="c193b-123">Capacity specifies hello total amount of data that can be stored by hello initiator (server).</span></span> <span data-ttu-id="c193b-124">磁碟區採精簡佈建，而且會刪除重複的資料。</span><span class="sxs-lookup"><span data-stu-id="c193b-124">Volumes are thinly provisioned, and data is deduplicated.</span></span> <span data-ttu-id="c193b-125">這表示您的裝置不會預先配置實體儲存容量在內部或 hello 雲端根據 tooconfigured 磁碟區容量。</span><span class="sxs-lookup"><span data-stu-id="c193b-125">This implies that your device doesn’t pre-allocate physical storage capacity internally or on hello cloud according tooconfigured volume capacity.</span></span> <span data-ttu-id="c193b-126">配置及取用視 hello 磁碟區容量。</span><span class="sxs-lookup"><span data-stu-id="c193b-126">hello volume capacity is allocated and consumed on demand.</span></span>
* <span data-ttu-id="c193b-127">**型別**– hello 磁碟區類型可以是階層式或封存 （其子型別的階層）</span><span class="sxs-lookup"><span data-stu-id="c193b-127">**Type** – hello volume type can be tiered or archival (a sub-type of tiered)</span></span>
* <span data-ttu-id="c193b-128">**存取**– 指定允許存取 toothis 磁碟區的 hello 啟動器 （伺服器）。</span><span class="sxs-lookup"><span data-stu-id="c193b-128">**Access** – Specifies hello initiators (servers) that are allowed access toothis volume.</span></span> <span data-ttu-id="c193b-129">不是成員的存取控制記錄 (ACR) 與 hello 磁碟區相關聯的啟動器不會看到 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c193b-129">Initiators that are not members of access control record (ACR) that is associated with hello volume will not see hello volume.</span></span>
* <span data-ttu-id="c193b-130">**監視** – 指定是否正在監視磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c193b-130">**Monitoring** – Specifies whether or not a volume is being monitored.</span></span> <span data-ttu-id="c193b-131">預設會在建立磁碟區時啟用監視。</span><span class="sxs-lookup"><span data-stu-id="c193b-131">A volume will have monitoring enabled by default when it is created.</span></span> <span data-ttu-id="c193b-132">不過，磁碟區複製會停用監視。</span><span class="sxs-lookup"><span data-stu-id="c193b-132">Monitoring will, however, be disabled for a volume clone.</span></span> <span data-ttu-id="c193b-133">為磁碟區，監視 tooenable 遵循 hello 指示監視磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c193b-133">tooenable monitoring for a volume, follow hello instructions in Monitor a volume.</span></span>

<span data-ttu-id="c193b-134">hello 與磁碟區相關聯的最常見工作包括：</span><span class="sxs-lookup"><span data-stu-id="c193b-134">hello most common tasks associated with a volume are:</span></span>

* <span data-ttu-id="c193b-135">新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="c193b-135">Add a volume</span></span>
* <span data-ttu-id="c193b-136">修改磁碟區</span><span class="sxs-lookup"><span data-stu-id="c193b-136">Modify a volume</span></span>
* <span data-ttu-id="c193b-137">刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="c193b-137">Delete a volume</span></span>
* <span data-ttu-id="c193b-138">使磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="c193b-138">Take a volume offline</span></span>
* <span data-ttu-id="c193b-139">監視磁碟區</span><span class="sxs-lookup"><span data-stu-id="c193b-139">Monitor a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="c193b-140">新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="c193b-140">Add a volume</span></span>
<span data-ttu-id="c193b-141">您已在部署 StorSimple 方案期間 [建立磁碟區](storsimple-deployment-walkthrough-u1.md#step-6-create-a-volume) 。</span><span class="sxs-lookup"><span data-stu-id="c193b-141">You [created a volume](storsimple-deployment-walkthrough-u1.md#step-6-create-a-volume) during deployment of your StorSimple solution.</span></span> <span data-ttu-id="c193b-142">新增磁碟區會是類似的程序。</span><span class="sxs-lookup"><span data-stu-id="c193b-142">Adding a volume is a similar procedure.</span></span>

### <a name="tooadd-a-volume"></a><span data-ttu-id="c193b-143">tooadd 磁碟區</span><span class="sxs-lookup"><span data-stu-id="c193b-143">tooadd a volume</span></span>
1. <span data-ttu-id="c193b-144">在 [hello**裝置**頁面、 選取 hello 裝置、 按兩下，然後再按一下 hello**磁碟區容器**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c193b-144">On hello **Devices** page, select hello device, double-click it, and then click hello **Volume Containers** tab.</span></span>
2. <span data-ttu-id="c193b-145">選取磁碟區容器，然後按一下箭號 hello hello 對應資料列 tooaccess hello 磁碟區與 hello 容器相關聯。</span><span class="sxs-lookup"><span data-stu-id="c193b-145">Select a volume container and click hello arrow in hello corresponding row tooaccess hello volumes associated with hello container.</span></span>
3. <span data-ttu-id="c193b-146">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="c193b-146">Click **Add** at hello bottom of hello page.</span></span> <span data-ttu-id="c193b-147">hello 新增磁碟區精靈 會啟動。</span><span class="sxs-lookup"><span data-stu-id="c193b-147">hello Add a volume wizard starts.</span></span>
   
     ![加入磁碟區精靈基本設定](./media/storsimple-manage-volumes/AddVolume1.png)
4. <span data-ttu-id="c193b-149">在 [hello 新增磁碟區精靈] 中，在**基本設定**，不要遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="c193b-149">In hello Add a volume wizard, under **Basic Settings**, do hello following:</span></span>
   
   1. <span data-ttu-id="c193b-150">輸入磁碟區的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="c193b-150">Supply a **Name** for your volume.</span></span>
   2. <span data-ttu-id="c193b-151">指定 hello**佈建的容量**以 GB 或 TB 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c193b-151">Specify hello **Provisioned Capacity** for your volume in GB or TB.</span></span> <span data-ttu-id="c193b-152">hello 容量必須介於 1 GB 到 64 TB 之間的實體裝置。</span><span class="sxs-lookup"><span data-stu-id="c193b-152">hello capacity must be between 1 GB and 64 TB for a physical device.</span></span> <span data-ttu-id="c193b-153">hello 可以佈建 StorSimple 虛擬裝置上的磁碟區的最大容量為 30 TB。</span><span class="sxs-lookup"><span data-stu-id="c193b-153">hello maximum capacity that can be provisioned for a volume on a StorSimple virtual device is 30 TB.</span></span>
   3. <span data-ttu-id="c193b-154">選取 hello**使用類型**磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c193b-154">Select hello **Usage Type** for your volume.</span></span> <span data-ttu-id="c193b-155">如果您使用 hello 分層磁碟區，對於封存的資料，選取 hello**對於不常存取的封存資料，使用此磁碟區**核取方塊，變更您的磁碟區的 hello 重複資料刪除區塊大小 too512 KB。</span><span class="sxs-lookup"><span data-stu-id="c193b-155">If you are using hello tiered volume for archival data, selecting hello **Use this volume for less frequently accessed archival data** check box changes hello deduplication chunk size for your volume too512 KB.</span></span> <span data-ttu-id="c193b-156">如果您未選取此選項，hello 對應的階層式磁碟區會使用 64 KB 的區塊大小。</span><span class="sxs-lookup"><span data-stu-id="c193b-156">If you do not select this option, hello corresponding tiered volume will use a chunk size of 64 KB.</span></span> <span data-ttu-id="c193b-157">較大的重複資料刪除區塊大小可讓大型的封存資料 toohello 雲端的 hello 裝置 tooexpedite hello 傳輸。（分層磁碟區已之前稱為主要磁碟區）。</span><span class="sxs-lookup"><span data-stu-id="c193b-157">A larger deduplication chunk size allows hello device tooexpedite hello transfer of large archival data toohello cloud.(Tiered volumes were formerly called primary volumes.)</span></span>
   4. <span data-ttu-id="c193b-158">按一下 [hello] 箭號圖示![箭號圖示](./media/storsimple-manage-volumes/HCS_ArrowIcon.png)toogo toohello**其他設定**頁面。</span><span class="sxs-lookup"><span data-stu-id="c193b-158">Click hello arrow icon ![Arrow icon](./media/storsimple-manage-volumes/HCS_ArrowIcon.png)toogo toohello **Additional Settings** page.</span></span>
      
        ![加入磁碟區精靈其他設定](./media/storsimple-manage-volumes/AddVolume2.png)
5. <span data-ttu-id="c193b-160">在 [其他設定] 下，加入新的存取控制記錄 (ACR)：</span><span class="sxs-lookup"><span data-stu-id="c193b-160">Under **Additional Settings**, add a new access control record (ACR):</span></span>
   
   1. <span data-ttu-id="c193b-161">從 hello 下拉式清單中選取存取控制記錄 (ACR)。</span><span class="sxs-lookup"><span data-stu-id="c193b-161">Select an access control record (ACR) from hello drop-down list.</span></span> <span data-ttu-id="c193b-162">或者，您可以加入新的 ACR。</span><span class="sxs-lookup"><span data-stu-id="c193b-162">Alternatively, you can add a new ACR.</span></span> <span data-ttu-id="c193b-163">Acr 可讓您判斷哪些主機可以存取您的磁碟區比對的 hello 使用 hello 記錄中列出的主機 IQN。</span><span class="sxs-lookup"><span data-stu-id="c193b-163">ACRs determine which hosts can access your volumes by matching hello host IQN with that listed in hello record.</span></span>
   2. <span data-ttu-id="c193b-164">我們建議您藉由選取 hello 啟用預設備份**啟用此磁碟區的預設備份**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="c193b-164">We recommend that you enable a default backup by selecting hello **Enable a default backup for this volume** check box.</span></span>
   3. <span data-ttu-id="c193b-165">按一下 [hello] 核取圖示</span><span class="sxs-lookup"><span data-stu-id="c193b-165">Click hello check icon</span></span> ![核取圖示](./media/storsimple-manage-volumes/HCS_CheckIcon.png) <span data-ttu-id="c193b-167">以 hello toocreate hello 磁碟區指定的設定。</span><span class="sxs-lookup"><span data-stu-id="c193b-167">toocreate hello volume with hello specified settings.</span></span>

<span data-ttu-id="c193b-168">您新的磁碟區現在已準備好 toouse。</span><span class="sxs-lookup"><span data-stu-id="c193b-168">Your new volume is now ready toouse.</span></span>

## <a name="modify-a-volume"></a><span data-ttu-id="c193b-169">修改磁碟區</span><span class="sxs-lookup"><span data-stu-id="c193b-169">Modify a volume</span></span>
<span data-ttu-id="c193b-170">當您需要 tooexpand 它或變更 hello 存取 hello 的磁碟區的主機時，請修改磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c193b-170">Modify a volume when you need tooexpand it or change hello hosts that access hello volume.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="c193b-171">如果您修改 hello hello 裝置上的磁碟區大小，hello 磁碟區大小需要 toobe hello 主控件上的變更。</span><span class="sxs-lookup"><span data-stu-id="c193b-171">If you modify hello volume size on hello device, hello volume size needs toobe changed on hello host as well.</span></span>
> * <span data-ttu-id="c193b-172">此處所述的 hello 主機端步驟適用於 Windows Server 2012 (2012R2)。</span><span class="sxs-lookup"><span data-stu-id="c193b-172">hello host-side steps described here are for Windows Server 2012 (2012R2).</span></span> <span data-ttu-id="c193b-173">Linux 或其他主機作業系統的程序會有所不同。</span><span class="sxs-lookup"><span data-stu-id="c193b-173">Procedures for Linux or other host operating systems will be different.</span></span> <span data-ttu-id="c193b-174">修改 hello 執行另一個作業系統的主機上的磁碟區時，請參閱 tooyour 主機作業系統的指示。</span><span class="sxs-lookup"><span data-stu-id="c193b-174">Refer tooyour host operating system instructions when modifying hello volume on a host running another operating system.</span></span>
> 
> 

### <a name="toomodify-a-volume"></a><span data-ttu-id="c193b-175">toomodify 磁碟區</span><span class="sxs-lookup"><span data-stu-id="c193b-175">toomodify a volume</span></span>
1. <span data-ttu-id="c193b-176">在 [hello**裝置**頁面、 選取 hello 裝置、 按兩下，然後再按一下 hello**磁碟區容器**] 索引標籤。此頁面會列出以表格格式與 hello 裝置相關聯的所有 hello 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="c193b-176">On hello **Devices** page, select hello device, double-click it, and then click hello **Volume Container** tab. This page lists in a tabular format all hello volume containers that are associated with hello device.</span></span>
2. <span data-ttu-id="c193b-177">選取磁碟區容器，然後按一下它 toodisplay hello hello 容器內的所有 hello 磁碟區清單。</span><span class="sxs-lookup"><span data-stu-id="c193b-177">Select a volume container and click it toodisplay hello list of all hello volumes within hello container.</span></span>
3. <span data-ttu-id="c193b-178">在 hello**磁碟區**頁面上選取的磁碟區，然後按一下**修改**。</span><span class="sxs-lookup"><span data-stu-id="c193b-178">On hello **Volumes** page, select a volume and click **Modify**.</span></span>
4. <span data-ttu-id="c193b-179">在 hello 修改磁碟區精靈 在**基本設定**，您可以 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="c193b-179">In hello Modify volume wizard, under **Basic Settings**, you can do hello following:</span></span>
   
   * <span data-ttu-id="c193b-180">編輯 hello**名稱**和**類型**如果您想 toomodify 分層磁碟區的 tooan 封存磁碟區選取 hello**對於不常存取的封存資料，使用此磁碟區**核取方塊 toochange hello 重複資料刪除區塊大小的磁碟區 too512 KB。</span><span class="sxs-lookup"><span data-stu-id="c193b-180">Edit hello **Name** and **Type** if you wish toomodify a tiered volume tooan archival volume by selecting hello **Use this volume for less frequently accessed archival data** check box toochange hello deduplication chunk size for your volume too512 KB.</span></span>
   * <span data-ttu-id="c193b-181">增加 hello**佈建的容量**。</span><span class="sxs-lookup"><span data-stu-id="c193b-181">Increase hello **Provisioned Capacity**.</span></span> <span data-ttu-id="c193b-182">hello**佈建的容量**只能增加。</span><span class="sxs-lookup"><span data-stu-id="c193b-182">hello **Provisioned Capacity** can only be increased.</span></span> <span data-ttu-id="c193b-183">您無法在磁碟區建立後予以壓縮。</span><span class="sxs-lookup"><span data-stu-id="c193b-183">You cannot shrink a volume after it is created.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="c193b-184">指派給 tooa 磁碟區之後，您無法變更 hello 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="c193b-184">You cannot change hello volume container after it is assigned tooa volume.</span></span>
     > 
     > 
5. <span data-ttu-id="c193b-185">在下**其他設定**，您可以 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="c193b-185">Under **Additional Settings**, you can do hello following:</span></span>
   
   * <span data-ttu-id="c193b-186">修改 hello Acr 提供 hello 磁碟區已離線。</span><span class="sxs-lookup"><span data-stu-id="c193b-186">Modify hello ACRs, provided that hello volume is offline.</span></span> <span data-ttu-id="c193b-187">Hello 磁碟區已上線時，如果您需要 tootake 它離線的第一個。</span><span class="sxs-lookup"><span data-stu-id="c193b-187">If hello volume is online, you will need tootake it offline first.</span></span> <span data-ttu-id="c193b-188">Toohello 中的步驟，請參閱[使磁碟區離線](#take-a-volume-offline)先前 toomodifying hello ACR。</span><span class="sxs-lookup"><span data-stu-id="c193b-188">Refer toohello steps in [Take a volume offline](#take-a-volume-offline) prior toomodifying hello ACR.</span></span>
   * <span data-ttu-id="c193b-189">Hello 磁碟區離線之後，請修改 Acr hello 清單。</span><span class="sxs-lookup"><span data-stu-id="c193b-189">Modify hello list of ACRs after hello volume is offline.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="c193b-190">您無法變更 hello**啟用此磁碟區的預設備份**hello 磁碟區的選項。</span><span class="sxs-lookup"><span data-stu-id="c193b-190">You cannot change hello **Enable a default backup for this volume** option for hello volume.</span></span>
     > 
     > 
6. <span data-ttu-id="c193b-191">按一下 hello 核取圖示以儲存您的變更</span><span class="sxs-lookup"><span data-stu-id="c193b-191">Save your changes by clicking hello check icon</span></span> ![核取圖示](./media/storsimple-manage-volumes/HCS_CheckIcon.png)<span data-ttu-id="c193b-193">.</span><span class="sxs-lookup"><span data-stu-id="c193b-193">.</span></span> <span data-ttu-id="c193b-194">hello Azure 傳統入口網站將會顯示更新的磁碟區訊息。</span><span class="sxs-lookup"><span data-stu-id="c193b-194">hello Azure classic portal will display an updating volume message.</span></span> <span data-ttu-id="c193b-195">已成功更新 hello 磁碟區時，它會顯示成功訊息。</span><span class="sxs-lookup"><span data-stu-id="c193b-195">It will display a success message when hello volume has been successfully updated.</span></span>
7. <span data-ttu-id="c193b-196">如果您要擴充磁碟區，完成下列步驟在您的 Windows 主機電腦上的 hello:</span><span class="sxs-lookup"><span data-stu-id="c193b-196">If you are expanding a volume, complete hello following steps on your Windows host computer:</span></span>
   
   1. <span data-ttu-id="c193b-197">跳過**電腦管理** ->**磁碟管理**。</span><span class="sxs-lookup"><span data-stu-id="c193b-197">Go too**Computer Management** ->**Disk Management**.</span></span>
   2. <span data-ttu-id="c193b-198">以滑鼠右鍵按一下 [磁碟管理]，並選取 [重新掃描磁碟]。</span><span class="sxs-lookup"><span data-stu-id="c193b-198">Right-click **Disk Management** and select **Rescan Disks**.</span></span>
   3. <span data-ttu-id="c193b-199">在 hello 清單中的磁碟，選取您更新的 hello 磁碟區、 按一下滑鼠右鍵，然後選取**延伸磁碟區**。</span><span class="sxs-lookup"><span data-stu-id="c193b-199">In hello list of disks, select hello volume that you updated, right-click, and then select **Extend Volume**.</span></span> <span data-ttu-id="c193b-200">hello 延伸磁碟區精靈 隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="c193b-200">hello Extend Volume wizard starts.</span></span> <span data-ttu-id="c193b-201">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="c193b-201">Click **Next**.</span></span>
   4. <span data-ttu-id="c193b-202">完成 hello 精靈，接受 hello 的預設值。</span><span class="sxs-lookup"><span data-stu-id="c193b-202">Complete hello wizard, accepting hello default values.</span></span> <span data-ttu-id="c193b-203">Hello 精靈完成後，hello 磁碟區應該會顯示 hello 增加大小。</span><span class="sxs-lookup"><span data-stu-id="c193b-203">After hello wizard is finished, hello volume should show hello increased size.</span></span>

<span data-ttu-id="c193b-204">![提供的影片](./media/storsimple-manage-volumes/Video_icon.png) **提供的影片**</span><span class="sxs-lookup"><span data-stu-id="c193b-204">![Video available](./media/storsimple-manage-volumes/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="c193b-205">toowatch 的視訊示範，如何 tooexpand 磁碟區，按一下[這裡](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/)。</span><span class="sxs-lookup"><span data-stu-id="c193b-205">toowatch a video that demonstrates how tooexpand a volume, click [here](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/).</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="c193b-206">使磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="c193b-206">Take a volume offline</span></span>
<span data-ttu-id="c193b-207">您可能需要 tootake 磁碟區離線，當您計劃 toomodify 它或刪除它。</span><span class="sxs-lookup"><span data-stu-id="c193b-207">You may need tootake a volume offline when you are planning toomodify it or delete it.</span></span> <span data-ttu-id="c193b-208">當磁碟區離線時，即無法進行讀寫存取。</span><span class="sxs-lookup"><span data-stu-id="c193b-208">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="c193b-209">您將需要 tootake hello 磁碟區離線 hello 裝置以及 hello 主機上。</span><span class="sxs-lookup"><span data-stu-id="c193b-209">You will need tootake hello volume offline on hello host as well as on hello device.</span></span> <span data-ttu-id="c193b-210">執行下列步驟 tootake 磁碟區離線 hello。</span><span class="sxs-lookup"><span data-stu-id="c193b-210">Perform hello following steps tootake a volume offline.</span></span>

### <a name="tootake-a-volume-offline"></a><span data-ttu-id="c193b-211">tootake 磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="c193b-211">tootake a volume offline</span></span>
1. <span data-ttu-id="c193b-212">請確定有問題的 hello 磁碟區不是使用中，再將其離線。</span><span class="sxs-lookup"><span data-stu-id="c193b-212">Make sure that hello volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="c193b-213">Hello 主機上的 hello 磁碟區離線讓第一次。</span><span class="sxs-lookup"><span data-stu-id="c193b-213">Take hello volume offline on hello host first.</span></span> <span data-ttu-id="c193b-214">這可免除 hello 磁碟區上的資料損毀的任何潛在風險。</span><span class="sxs-lookup"><span data-stu-id="c193b-214">This eliminates any potential risk of data corruption on hello volume.</span></span> <span data-ttu-id="c193b-215">如需特定步驟，請參閱主機作業系統的 toohello 指示。</span><span class="sxs-lookup"><span data-stu-id="c193b-215">For specific steps, refer toohello instructions for your host operating system.</span></span>
3. <span data-ttu-id="c193b-216">Hello 主機已離線後，採用的離線 hello 裝置 hello 磁碟區，藉由執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c193b-216">After hello host is offline, take hello volume on hello device offline by performing hello following steps:</span></span>
   
   1. <span data-ttu-id="c193b-217">在 hello**裝置**頁面、 選取 hello 裝置、 按兩下，然後再按一下 hello**磁碟區容器** 索引標籤 hello**磁碟區容器**索引標籤上列出所有以表格格式hello 與 hello 裝置相關聯的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="c193b-217">On hello **Devices** page, select hello device, double-click it, and then click hello **Volume Containers** tab. hello **Volume Containers** tab lists in a tabular format all hello volume containers that are associated with hello device.</span></span>
   2. <span data-ttu-id="c193b-218">選取磁碟區容器，然後按一下它 toodisplay hello hello 容器內的所有 hello 磁碟區清單。</span><span class="sxs-lookup"><span data-stu-id="c193b-218">Select a volume container and click it toodisplay hello list of all hello volumes within hello container.</span></span>
   3. <span data-ttu-id="c193b-219">選取磁碟區，然後按一下 [離線] 。</span><span class="sxs-lookup"><span data-stu-id="c193b-219">Select a volume and click **Take offline**.</span></span>
   4. <span data-ttu-id="c193b-220">系統提示您進行確認時，按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="c193b-220">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="c193b-221">hello 磁碟區現在應該可以離線。</span><span class="sxs-lookup"><span data-stu-id="c193b-221">hello volume should now be offline.</span></span>
      
      <span data-ttu-id="c193b-222">磁碟區離線後，hello**上線**選項就會變成可用。</span><span class="sxs-lookup"><span data-stu-id="c193b-222">After a volume is offline, hello **Bring Online** option becomes available.</span></span>

> [!NOTE]
> <span data-ttu-id="c193b-223">hello**離線**命令會傳送要求 toohello 裝置 tootake hello 磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="c193b-223">hello **Take Offline** command sends a request toohello device tootake hello volume offline.</span></span> <span data-ttu-id="c193b-224">如果主機仍在使用 hello 磁碟區，這會導致連線中斷，但離線 hello 磁碟區將不會失敗。</span><span class="sxs-lookup"><span data-stu-id="c193b-224">If hosts are still using hello volume, this results in broken connections, but taking hello volume offline will not fail.</span></span>
> 
> 

## <a name="delete-a-volume"></a><span data-ttu-id="c193b-225">刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="c193b-225">Delete a volume</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c193b-226">只有當磁碟區離線時，您才能予以刪除。</span><span class="sxs-lookup"><span data-stu-id="c193b-226">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="c193b-227">完成下列步驟 toodelete 磁碟區的 hello。</span><span class="sxs-lookup"><span data-stu-id="c193b-227">Complete hello following steps toodelete a volume.</span></span>

### <a name="toodelete-a-volume"></a><span data-ttu-id="c193b-228">toodelete 磁碟區</span><span class="sxs-lookup"><span data-stu-id="c193b-228">toodelete a volume</span></span>
1. <span data-ttu-id="c193b-229">在 [hello**裝置**頁面、 選取 hello 裝置、 按兩下，然後再按一下 hello**磁碟區容器**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c193b-229">On hello **Devices** page, select hello device, double-click it, and then click hello **Volume Containers** tab.</span></span>
2. <span data-ttu-id="c193b-230">選取您想要 toodelete hello 磁碟區的 hello 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="c193b-230">Select hello volume container that has hello volume you want toodelete.</span></span> <span data-ttu-id="c193b-231">按一下 hello 磁碟區容器 tooaccess hello**磁碟區**頁面。</span><span class="sxs-lookup"><span data-stu-id="c193b-231">Click hello volume container tooaccess hello **Volumes** page.</span></span>
3. <span data-ttu-id="c193b-232">與這個容器相關聯的所有 hello 磁碟區會以表格格式都顯示。</span><span class="sxs-lookup"><span data-stu-id="c193b-232">All hello volumes associated with this container are displayed in a tabular format.</span></span> <span data-ttu-id="c193b-233">檢查 hello 狀態想 toodelete hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c193b-233">Check hello status of hello volume you want toodelete.</span></span> <span data-ttu-id="c193b-234">如果您想要 toodelete hello 磁碟區未離線，使其離線的第一個步驟，下列 hello 步驟[使磁碟區離線](#take-a-volume-offline)。</span><span class="sxs-lookup"><span data-stu-id="c193b-234">If hello volume you want toodelete is not offline, take it offline first, following hello steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="c193b-235">Hello 磁碟區離線後，請按一下**刪除**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="c193b-235">After hello volume is offline, click **Delete** at hello bottom of hello page.</span></span>
5. <span data-ttu-id="c193b-236">系統提示您進行確認時，按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="c193b-236">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="c193b-237">hello 磁碟區現在將會刪除與 hello**磁碟區**頁面會顯示更新的 hello hello 容器內的磁碟區清單。</span><span class="sxs-lookup"><span data-stu-id="c193b-237">hello volume will now be deleted and hello **Volumes** page will show hello updated list of volumes within hello container.</span></span>

## <a name="monitor-a-volume"></a><span data-ttu-id="c193b-238">監視磁碟區</span><span class="sxs-lookup"><span data-stu-id="c193b-238">Monitor a volume</span></span>
<span data-ttu-id="c193b-239">磁碟區監視可讓您的磁碟區的 toocollect 我 I/O 相關統計資料。</span><span class="sxs-lookup"><span data-stu-id="c193b-239">Volume monitoring allows you toocollect I/O-related statistics for a volume.</span></span> <span data-ttu-id="c193b-240">預設值為 hello 會啟用監視您所建立的前 32 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c193b-240">Monitoring is enabled by default for hello first 32 volumes that you create.</span></span> <span data-ttu-id="c193b-241">預設會停用監視其他磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c193b-241">Monitoring of additional volumes is disabled by default.</span></span> <span data-ttu-id="c193b-242">預設也會停用監視複製的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c193b-242">Monitoring of cloned volumes is also disabled by default.</span></span>

<span data-ttu-id="c193b-243">執行下列步驟 tooenable hello 或停用磁碟區的監視。</span><span class="sxs-lookup"><span data-stu-id="c193b-243">Perform hello following steps tooenable or disable monitoring for a volume.</span></span>

### <a name="tooenable-or-disable-volume-monitoring"></a><span data-ttu-id="c193b-244">tooenable 或停用磁碟區監視</span><span class="sxs-lookup"><span data-stu-id="c193b-244">tooenable or disable volume monitoring</span></span>
1. <span data-ttu-id="c193b-245">在 [hello**裝置**頁面、 選取 hello 裝置、 按兩下，然後再按一下 hello**磁碟區容器**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c193b-245">On hello **Devices** page, select hello device, double-click it, and then click hello **Volume Containers** tab.</span></span>
2. <span data-ttu-id="c193b-246">選取哪些 hello 磁碟區所在，hello 磁碟區容器，然後按一下hello 磁碟區容器 tooaccess hello**磁碟區**頁面。</span><span class="sxs-lookup"><span data-stu-id="c193b-246">Select hello volume container in which hello volume resides, and then click hello volume container tooaccess hello **Volumes** page.</span></span>
3. <span data-ttu-id="c193b-247">與這個容器相關聯的所有 hello 磁碟區會都列在 hello 表格式顯示中。</span><span class="sxs-lookup"><span data-stu-id="c193b-247">All hello volumes associated with this container are listed in hello tabular display.</span></span> <span data-ttu-id="c193b-248">按一下並選取 hello 磁碟區或磁碟區再製。</span><span class="sxs-lookup"><span data-stu-id="c193b-248">Click and select hello volume or volume clone.</span></span>
4. <span data-ttu-id="c193b-249">在 hello hello 頁面底部，按一下**修改**。</span><span class="sxs-lookup"><span data-stu-id="c193b-249">At hello bottom of hello page, click **Modify**.</span></span>
5. <span data-ttu-id="c193b-250">在 hello 修改磁碟區精靈 在**基本設定**，選取**啟用**或**停用**從 hello**監視**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="c193b-250">In hello Modify Volume wizard, under **Basic Settings**, select **Enable** or **Disable** from hello **Monitoring** drop-down list.</span></span>
   
    ![修改磁碟區基本設定](./media/storsimple-manage-volumes/HCS_MonitorVolumeM.png)

## <a name="next-steps"></a><span data-ttu-id="c193b-252">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c193b-252">Next steps</span></span>
* <span data-ttu-id="c193b-253">了解如何太[複製 StorSimple 磁碟區](storsimple-clone-volume.md)。</span><span class="sxs-lookup"><span data-stu-id="c193b-253">Learn how too[clone a StorSimple volume](storsimple-clone-volume.md).</span></span>
* <span data-ttu-id="c193b-254">了解如何太[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="c193b-254">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>


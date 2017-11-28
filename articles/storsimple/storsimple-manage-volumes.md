---
title: "管理 StorSimple 磁碟區 | Microsoft Docs"
description: "說明如何加入、修改及監視 StorSimple 磁碟區，以及如何在必要時使其離線。"
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
ms.openlocfilehash: 31ed9dad8ba56a3746873b7b35e678e97743fbfe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-volumes"></a><span data-ttu-id="dadee-103">使用 StorSimple Manager 服務來管理磁碟區</span><span class="sxs-lookup"><span data-stu-id="dadee-103">Use the StorSimple Manager service to manage volumes</span></span>
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a><span data-ttu-id="dadee-104">概觀</span><span class="sxs-lookup"><span data-stu-id="dadee-104">Overview</span></span>
<span data-ttu-id="dadee-105">本教學課程說明如何使用 StorSimple Manager 服務來建立和管理 StorSimple 裝置與 StorSimple 虛擬裝置上的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dadee-105">This tutorial explains how to use the StorSimple Manager service to create and manage volumes on the StorSimple device and StorSimple virtual device.</span></span>

<span data-ttu-id="dadee-106">StorSimple Manager 服務是 Azure 傳統入口網站的延伸模組，可讓您透過單一 Web 介面管理 StorSimple 解決方案。</span><span class="sxs-lookup"><span data-stu-id="dadee-106">The StorSimple Manager service is an extension of the Azure classic portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="dadee-107">除了管理磁碟區，您可以使用 StorSimple Manager 服務來建立和管理 StorSimple 服務、檢視和管理裝置、檢視警示，以及檢視和管理備份原則與備份類別目錄。</span><span class="sxs-lookup"><span data-stu-id="dadee-107">In addition to managing volumes, you can use the StorSimple Manager service to create and manage StorSimple services, view and manage devices, view alerts, and view and manage backup policies and the backup catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="dadee-108">Azure StorSimple 只能建立精簡佈建的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dadee-108">Azure StorSimple can create thinly provisioned volumes only.</span></span> <span data-ttu-id="dadee-109">您無法在 Azure StorSimple 系統上建立完整佈建或部分佈建的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dadee-109">You cannot create fully provisioned or partially provisioned volumes on an Azure StorSimple system.</span></span>
> 
> <span data-ttu-id="dadee-110">精簡佈建是一項虛擬化技術，讓可用的儲存空間超過實體資源。</span><span class="sxs-lookup"><span data-stu-id="dadee-110">Thin provisioning is a virtualization technology in which available storage appears to exceed physical resources.</span></span> <span data-ttu-id="dadee-111">Azure StorSimple 不預先保留足夠的儲存空間，而是利用精簡佈建來配置剛好符合目前需求的空間。</span><span class="sxs-lookup"><span data-stu-id="dadee-111">Instead of reserving sufficient storage in advance, Azure StorSimple uses thin provisioning to allocate just enough space to meet current requirements.</span></span> <span data-ttu-id="dadee-112">雲端儲存體本質有彈性可協助這種方法，因為 Azure StorSimple 可以隨需求變化，增加或減少雲端儲存體。</span><span class="sxs-lookup"><span data-stu-id="dadee-112">The elastic nature of cloud storage facilitates this approach because Azure StorSimple can increase or decrease cloud storage to meet changing demands.</span></span>
> 
> 

## <a name="the-volumes-page"></a><span data-ttu-id="dadee-113">[磁碟區] 頁面</span><span class="sxs-lookup"><span data-stu-id="dadee-113">The Volumes page</span></span>
<span data-ttu-id="dadee-114">您為啟動器 (伺服器) 佈建在 Microsoft Azure StorSimple 裝置的存放磁碟區，可以在 [磁碟區]  頁面管理 。</span><span class="sxs-lookup"><span data-stu-id="dadee-114">The **Volumes** page allows you to manage the storage volumes that are provisioned on the Microsoft Azure StorSimple device for your initiators (servers).</span></span> <span data-ttu-id="dadee-115">它會顯示 StorSimple 裝置上的磁碟區清單。</span><span class="sxs-lookup"><span data-stu-id="dadee-115">It displays the list of volumes on your StorSimple device.</span></span>

 ![磁碟區頁面](./media/storsimple-manage-volumes/HCS_VolumesPage.png)

<span data-ttu-id="dadee-117">磁碟區是由一系列屬性所組成：</span><span class="sxs-lookup"><span data-stu-id="dadee-117">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="dadee-118">**名稱** – 必須是唯一且有助於識別磁碟區的描述性名稱。</span><span class="sxs-lookup"><span data-stu-id="dadee-118">**Name** – A descriptive name that must be unique and helps identify the volume.</span></span> <span data-ttu-id="dadee-119">這個名稱也可在您篩選特定磁碟區時用於監視報告。</span><span class="sxs-lookup"><span data-stu-id="dadee-119">This name is also used in monitoring reports when you filter on a specific volume.</span></span>
* <span data-ttu-id="dadee-120">**狀態** – 可為連線或離線。</span><span class="sxs-lookup"><span data-stu-id="dadee-120">**Status** – Can be online or offline.</span></span> <span data-ttu-id="dadee-121">如果是離線的磁碟區，允許存取使用它的啟動器 (伺服器) 會看不到該磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dadee-121">If a volume if offline, it is not visible to initiators (servers) that are allowed access to use the volume.</span></span>
* <span data-ttu-id="dadee-122">**容量** – 指定啟動器 (伺服器) 所認知的磁碟區大小。</span><span class="sxs-lookup"><span data-stu-id="dadee-122">**Capacity** – Specifies how large the volume is, as perceived by the initiator (server).</span></span> <span data-ttu-id="dadee-123">容量指定啟動器 (伺服器) 可以儲存的總資料量。</span><span class="sxs-lookup"><span data-stu-id="dadee-123">Capacity specifies the total amount of data that can be stored by the initiator (server).</span></span> <span data-ttu-id="dadee-124">磁碟區採精簡佈建，而且會刪除重複的資料。</span><span class="sxs-lookup"><span data-stu-id="dadee-124">Volumes are thinly provisioned, and data is deduplicated.</span></span> <span data-ttu-id="dadee-125">這表示您的裝置不會根據設定的磁碟區容量，在內部或在雲端預先配置實體儲存體容量。</span><span class="sxs-lookup"><span data-stu-id="dadee-125">This implies that your device doesn’t pre-allocate physical storage capacity internally or on the cloud according to configured volume capacity.</span></span> <span data-ttu-id="dadee-126">磁碟區容量會依需求來配置和耗用。</span><span class="sxs-lookup"><span data-stu-id="dadee-126">The volume capacity is allocated and consumed on demand.</span></span>
* <span data-ttu-id="dadee-127">**類型** – 磁碟區類型可以是分層或封存 (子類型分層)</span><span class="sxs-lookup"><span data-stu-id="dadee-127">**Type** – The volume type can be tiered or archival (a sub-type of tiered)</span></span>
* <span data-ttu-id="dadee-128">**存取** – 指定允許存取此磁碟區的啟動器 (伺服器)。</span><span class="sxs-lookup"><span data-stu-id="dadee-128">**Access** – Specifies the initiators (servers) that are allowed access to this volume.</span></span> <span data-ttu-id="dadee-129">啟動器不是與磁碟區相關聯的存取控制記錄 (ACR) 成員，就看不到磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dadee-129">Initiators that are not members of access control record (ACR) that is associated with the volume will not see the volume.</span></span>
* <span data-ttu-id="dadee-130">**監視** – 指定是否正在監視磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dadee-130">**Monitoring** – Specifies whether or not a volume is being monitored.</span></span> <span data-ttu-id="dadee-131">預設會在建立磁碟區時啟用監視。</span><span class="sxs-lookup"><span data-stu-id="dadee-131">A volume will have monitoring enabled by default when it is created.</span></span> <span data-ttu-id="dadee-132">不過，磁碟區複製會停用監視。</span><span class="sxs-lookup"><span data-stu-id="dadee-132">Monitoring will, however, be disabled for a volume clone.</span></span> <span data-ttu-id="dadee-133">若要啟用監視磁碟區，請依照＜監視磁碟區＞中的指示執行。</span><span class="sxs-lookup"><span data-stu-id="dadee-133">To enable monitoring for a volume, follow the instructions in Monitor a volume.</span></span>

<span data-ttu-id="dadee-134">最常見與磁碟區相關聯的工作如下：</span><span class="sxs-lookup"><span data-stu-id="dadee-134">The most common tasks associated with a volume are:</span></span>

* <span data-ttu-id="dadee-135">新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="dadee-135">Add a volume</span></span>
* <span data-ttu-id="dadee-136">修改磁碟區</span><span class="sxs-lookup"><span data-stu-id="dadee-136">Modify a volume</span></span>
* <span data-ttu-id="dadee-137">刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="dadee-137">Delete a volume</span></span>
* <span data-ttu-id="dadee-138">使磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="dadee-138">Take a volume offline</span></span>
* <span data-ttu-id="dadee-139">監視磁碟區</span><span class="sxs-lookup"><span data-stu-id="dadee-139">Monitor a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="dadee-140">新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="dadee-140">Add a volume</span></span>
<span data-ttu-id="dadee-141">您已在部署 StorSimple 方案期間 [建立磁碟區](storsimple-deployment-walkthrough-u1.md#step-6-create-a-volume) 。</span><span class="sxs-lookup"><span data-stu-id="dadee-141">You [created a volume](storsimple-deployment-walkthrough-u1.md#step-6-create-a-volume) during deployment of your StorSimple solution.</span></span> <span data-ttu-id="dadee-142">新增磁碟區會是類似的程序。</span><span class="sxs-lookup"><span data-stu-id="dadee-142">Adding a volume is a similar procedure.</span></span>

### <a name="to-add-a-volume"></a><span data-ttu-id="dadee-143">若要新增磁碟區</span><span class="sxs-lookup"><span data-stu-id="dadee-143">To add a volume</span></span>
1. <span data-ttu-id="dadee-144">在 [裝置] 頁面中，選取並按兩下裝置，然後按一下 [磁碟區容器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="dadee-144">On the **Devices** page, select the device, double-click it, and then click the **Volume Containers** tab.</span></span>
2. <span data-ttu-id="dadee-145">選取磁碟區容器，然後按一下對應資料列的箭號來存取與該容器相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dadee-145">Select a volume container and click the arrow in the corresponding row to access the volumes associated with the container.</span></span>
3. <span data-ttu-id="dadee-146">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="dadee-146">Click **Add** at the bottom of the page.</span></span> <span data-ttu-id="dadee-147">[新增磁碟區精靈] 隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="dadee-147">The Add a volume wizard starts.</span></span>
   
     ![加入磁碟區精靈基本設定](./media/storsimple-manage-volumes/AddVolume1.png)
4. <span data-ttu-id="dadee-149">在 [新增磁碟區精靈] 的 [基本設定] 下，執行列動作：</span><span class="sxs-lookup"><span data-stu-id="dadee-149">In the Add a volume wizard, under **Basic Settings**, do the following:</span></span>
   
   1. <span data-ttu-id="dadee-150">輸入磁碟區的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="dadee-150">Supply a **Name** for your volume.</span></span>
   2. <span data-ttu-id="dadee-151">為磁碟區指定 [佈建的容量]  \(GB 或 TB)。</span><span class="sxs-lookup"><span data-stu-id="dadee-151">Specify the **Provisioned Capacity** for your volume in GB or TB.</span></span> <span data-ttu-id="dadee-152">實體裝置的容量必須介於 1 GB 到 64 TB 之間。</span><span class="sxs-lookup"><span data-stu-id="dadee-152">The capacity must be between 1 GB and 64 TB for a physical device.</span></span> <span data-ttu-id="dadee-153">可為 StorSimple 虛擬裝置上的磁碟區佈建的最大容量為 30 TB。</span><span class="sxs-lookup"><span data-stu-id="dadee-153">The maximum capacity that can be provisioned for a volume on a StorSimple virtual device is 30 TB.</span></span>
   3. <span data-ttu-id="dadee-154">為磁碟區選取 [使用類型]  。</span><span class="sxs-lookup"><span data-stu-id="dadee-154">Select the **Usage Type** for your volume.</span></span> <span data-ttu-id="dadee-155">如果您針對封存資料使用分層磁碟區，選取 [使用此磁碟區存放不常存取的封存資料]  核取方塊會將您磁碟區的重複資料刪除區塊大小變更為 512 KB。</span><span class="sxs-lookup"><span data-stu-id="dadee-155">If you are using the tiered volume for archival data, selecting the **Use this volume for less frequently accessed archival data** check box changes the deduplication chunk size for your volume to 512 KB.</span></span> <span data-ttu-id="dadee-156">如果未核取此選項，對應的分層磁碟區會使用 64 KB 的區塊大小。</span><span class="sxs-lookup"><span data-stu-id="dadee-156">If you do not select this option, the corresponding tiered volume will use a chunk size of 64 KB.</span></span> <span data-ttu-id="dadee-157">較大的重複資料刪除區塊大小可讓裝置加速傳送大型封存資料到雲端 (分層式磁碟區之前稱為主要磁碟區)。</span><span class="sxs-lookup"><span data-stu-id="dadee-157">A larger deduplication chunk size allows the device to expedite the transfer of large archival data to the cloud.(Tiered volumes were formerly called primary volumes.)</span></span>
   4. <span data-ttu-id="dadee-158">按一下箭頭圖示![箭頭圖示](./media/storsimple-manage-volumes/HCS_ArrowIcon.png)，前往 [其他設定] 頁面。</span><span class="sxs-lookup"><span data-stu-id="dadee-158">Click the arrow icon ![Arrow icon](./media/storsimple-manage-volumes/HCS_ArrowIcon.png)to go to the **Additional Settings** page.</span></span>
      
        ![加入磁碟區精靈其他設定](./media/storsimple-manage-volumes/AddVolume2.png)
5. <span data-ttu-id="dadee-160">在 [其他設定] 下，加入新的存取控制記錄 (ACR)：</span><span class="sxs-lookup"><span data-stu-id="dadee-160">Under **Additional Settings**, add a new access control record (ACR):</span></span>
   
   1. <span data-ttu-id="dadee-161">在下拉式清單中選取存取控制記錄 (ACR)。</span><span class="sxs-lookup"><span data-stu-id="dadee-161">Select an access control record (ACR) from the drop-down list.</span></span> <span data-ttu-id="dadee-162">或者，您可以加入新的 ACR。</span><span class="sxs-lookup"><span data-stu-id="dadee-162">Alternatively, you can add a new ACR.</span></span> <span data-ttu-id="dadee-163">ACR 會藉由比對主機與記錄中列出的 IQN 來決定哪些主機可以存取磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dadee-163">ACRs determine which hosts can access your volumes by matching the host IQN with that listed in the record.</span></span>
   2. <span data-ttu-id="dadee-164">建議選取 [ **啟用此磁碟區的預設備份** ] 核取方塊啟用預設備份。</span><span class="sxs-lookup"><span data-stu-id="dadee-164">We recommend that you enable a default backup by selecting the **Enable a default backup for this volume** check box.</span></span>
   3. <span data-ttu-id="dadee-165">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="dadee-165">Click the check icon</span></span> ![核取圖示](./media/storsimple-manage-volumes/HCS_CheckIcon.png) <span data-ttu-id="dadee-167">，以利用指定的設定來建立磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dadee-167">to create the volume with the specified settings.</span></span>

<span data-ttu-id="dadee-168">新的磁碟區現在已備妥可供使用。</span><span class="sxs-lookup"><span data-stu-id="dadee-168">Your new volume is now ready to use.</span></span>

## <a name="modify-a-volume"></a><span data-ttu-id="dadee-169">修改磁碟區</span><span class="sxs-lookup"><span data-stu-id="dadee-169">Modify a volume</span></span>
<span data-ttu-id="dadee-170">當您需要擴充磁碟區，或變更存取該磁碟區的主機時，請修改磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dadee-170">Modify a volume when you need to expand it or change the hosts that access the volume.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="dadee-171">如果您修改裝置上的磁碟區大小，也必須變更主機上的磁碟區大小。</span><span class="sxs-lookup"><span data-stu-id="dadee-171">If you modify the volume size on the device, the volume size needs to be changed on the host as well.</span></span>
> * <span data-ttu-id="dadee-172">此處所述的主機端步驟適用於 Windows Server 2012 (2012R2)。</span><span class="sxs-lookup"><span data-stu-id="dadee-172">The host-side steps described here are for Windows Server 2012 (2012R2).</span></span> <span data-ttu-id="dadee-173">Linux 或其他主機作業系統的程序會有所不同。</span><span class="sxs-lookup"><span data-stu-id="dadee-173">Procedures for Linux or other host operating systems will be different.</span></span> <span data-ttu-id="dadee-174">如果要在執行其他作業系統的主機上修改磁碟區，請參考主機作業系統的指示。</span><span class="sxs-lookup"><span data-stu-id="dadee-174">Refer to your host operating system instructions when modifying the volume on a host running another operating system.</span></span>
> 
> 

### <a name="to-modify-a-volume"></a><span data-ttu-id="dadee-175">若要修改磁碟區</span><span class="sxs-lookup"><span data-stu-id="dadee-175">To modify a volume</span></span>
1. <span data-ttu-id="dadee-176">在 [裝置] 頁面中，選取並按兩下裝置，然後按一下 [磁碟區容器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="dadee-176">On the **Devices** page, select the device, double-click it, and then click the **Volume Container** tab.</span></span> <span data-ttu-id="dadee-177">此頁面會以表格列出與裝置相關聯的所有磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="dadee-177">This page lists in a tabular format all the volume containers that are associated with the device.</span></span>
2. <span data-ttu-id="dadee-178">選取並按一下磁碟區容器，以清單顯示該容器內的所有磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dadee-178">Select a volume container and click it to display the list of all the volumes within the container.</span></span>
3. <span data-ttu-id="dadee-179">在 [磁碟區] 頁面上，選取磁碟區，然後按一下 [修改]。</span><span class="sxs-lookup"><span data-stu-id="dadee-179">On the **Volumes** page, select a volume and click **Modify**.</span></span>
4. <span data-ttu-id="dadee-180">在 [修改磁碟區精靈] 的 [基本設定] 下，您可以執行列動作：</span><span class="sxs-lookup"><span data-stu-id="dadee-180">In the Modify volume wizard, under **Basic Settings**, you can do the following:</span></span>
   
   * <span data-ttu-id="dadee-181">如果您要藉由選取 [使用此磁碟區存放不常存取的封存資料] 核取方塊，將您磁碟區的重複資料刪除區塊大小變更為 512 KB，將分層磁碟區修改為封存磁碟區，請編輯 [名稱] 和 [類型]。</span><span class="sxs-lookup"><span data-stu-id="dadee-181">Edit the **Name** and **Type** if you wish to modify a tiered volume to an archival volume by selecting the **Use this volume for less frequently accessed archival data** check box to change the deduplication chunk size for your volume to 512 KB.</span></span>
   * <span data-ttu-id="dadee-182">增加 [佈建的容量] 。</span><span class="sxs-lookup"><span data-stu-id="dadee-182">Increase the **Provisioned Capacity**.</span></span> <span data-ttu-id="dadee-183">[佈建的容量]  只能增加。</span><span class="sxs-lookup"><span data-stu-id="dadee-183">The **Provisioned Capacity** can only be increased.</span></span> <span data-ttu-id="dadee-184">您無法在磁碟區建立後予以壓縮。</span><span class="sxs-lookup"><span data-stu-id="dadee-184">You cannot shrink a volume after it is created.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="dadee-185">磁碟區容器一經指派給磁碟區後，便無法變更。</span><span class="sxs-lookup"><span data-stu-id="dadee-185">You cannot change the volume container after it is assigned to a volume.</span></span>
     > 
     > 
5. <span data-ttu-id="dadee-186">在 [其他設定] 下，您可以執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="dadee-186">Under **Additional Settings**, you can do the following:</span></span>
   
   * <span data-ttu-id="dadee-187">修改 ACR，若是磁碟區已離線。</span><span class="sxs-lookup"><span data-stu-id="dadee-187">Modify the ACRs, provided that the volume is offline.</span></span> <span data-ttu-id="dadee-188">如果磁碟區已連線，您必須先讓它離線。</span><span class="sxs-lookup"><span data-stu-id="dadee-188">If the volume is online, you will need to take it offline first.</span></span> <span data-ttu-id="dadee-189">修改 ACR 之前，請參閱 [使磁碟區離線](#take-a-volume-offline) 中的步驟。</span><span class="sxs-lookup"><span data-stu-id="dadee-189">Refer to the steps in [Take a volume offline](#take-a-volume-offline) prior to modifying the ACR.</span></span>
   * <span data-ttu-id="dadee-190">在磁碟區離線之後，才修改 ACR 清單。</span><span class="sxs-lookup"><span data-stu-id="dadee-190">Modify the list of ACRs after the volume is offline.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="dadee-191">您無法變更此磁碟區的 [ **啟用此磁碟區的預設備份** ] 選項。</span><span class="sxs-lookup"><span data-stu-id="dadee-191">You cannot change the **Enable a default backup for this volume** option for the volume.</span></span>
     > 
     > 
6. <span data-ttu-id="dadee-192">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="dadee-192">Save your changes by clicking the check icon</span></span> ![核取圖示](./media/storsimple-manage-volumes/HCS_CheckIcon.png)<span data-ttu-id="dadee-194">。</span><span class="sxs-lookup"><span data-stu-id="dadee-194">.</span></span> <span data-ttu-id="dadee-195">Azure 傳統入口網站將會顯示更新磁碟區訊息。</span><span class="sxs-lookup"><span data-stu-id="dadee-195">The Azure classic portal will display an updating volume message.</span></span> <span data-ttu-id="dadee-196">如果磁碟區已成功更新，即會顯示成功訊息。</span><span class="sxs-lookup"><span data-stu-id="dadee-196">It will display a success message when the volume has been successfully updated.</span></span>
7. <span data-ttu-id="dadee-197">如果您要延伸磁碟區，請在 Windows 主機電腦上完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="dadee-197">If you are expanding a volume, complete the following steps on your Windows host computer:</span></span>
   
   1. <span data-ttu-id="dadee-198">移至 [電腦管理]  ->[磁碟管理]。</span><span class="sxs-lookup"><span data-stu-id="dadee-198">Go to **Computer Management** ->**Disk Management**.</span></span>
   2. <span data-ttu-id="dadee-199">以滑鼠右鍵按一下 [磁碟管理]，並選取 [重新掃描磁碟]。</span><span class="sxs-lookup"><span data-stu-id="dadee-199">Right-click **Disk Management** and select **Rescan Disks**.</span></span>
   3. <span data-ttu-id="dadee-200">在磁碟清單中，選取您已更新的磁碟區，按一下滑鼠右鍵，然後選取 [延伸磁碟區] 。</span><span class="sxs-lookup"><span data-stu-id="dadee-200">In the list of disks, select the volume that you updated, right-click, and then select **Extend Volume**.</span></span> <span data-ttu-id="dadee-201">[延伸磁碟區精靈] 隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="dadee-201">The Extend Volume wizard starts.</span></span> <span data-ttu-id="dadee-202">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="dadee-202">Click **Next**.</span></span>
   4. <span data-ttu-id="dadee-203">使用預設值完成精靈。</span><span class="sxs-lookup"><span data-stu-id="dadee-203">Complete the wizard, accepting the default values.</span></span> <span data-ttu-id="dadee-204">完成精靈後，磁碟區應該會顯示增加的大小。</span><span class="sxs-lookup"><span data-stu-id="dadee-204">After the wizard is finished, the volume should show the increased size.</span></span>

<span data-ttu-id="dadee-205">![提供的影片](./media/storsimple-manage-volumes/Video_icon.png) **提供的影片**</span><span class="sxs-lookup"><span data-stu-id="dadee-205">![Video available](./media/storsimple-manage-volumes/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="dadee-206">若要觀看影片示範如何擴充磁碟區，請按一下 [這裡](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/)。</span><span class="sxs-lookup"><span data-stu-id="dadee-206">To watch a video that demonstrates how to expand a volume, click [here](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/).</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="dadee-207">使磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="dadee-207">Take a volume offline</span></span>
<span data-ttu-id="dadee-208">您想要修改或刪除磁碟區時，可能需要先使其離線。</span><span class="sxs-lookup"><span data-stu-id="dadee-208">You may need to take a volume offline when you are planning to modify it or delete it.</span></span> <span data-ttu-id="dadee-209">當磁碟區離線時，即無法進行讀寫存取。</span><span class="sxs-lookup"><span data-stu-id="dadee-209">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="dadee-210">您必須使主機與裝置上的磁碟區同時離線。</span><span class="sxs-lookup"><span data-stu-id="dadee-210">You will need to take the volume offline on the host as well as on the device.</span></span> <span data-ttu-id="dadee-211">請執行下列步驟以使磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="dadee-211">Perform the following steps to take a volume offline.</span></span>

### <a name="to-take-a-volume-offline"></a><span data-ttu-id="dadee-212">若要使磁碟區離線</span><span class="sxs-lookup"><span data-stu-id="dadee-212">To take a volume offline</span></span>
1. <span data-ttu-id="dadee-213">請確定有問題的磁碟區不在使用中後，再使其離線。</span><span class="sxs-lookup"><span data-stu-id="dadee-213">Make sure that the volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="dadee-214">先使主機上的磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="dadee-214">Take the volume offline on the host first.</span></span> <span data-ttu-id="dadee-215">這樣做可以排除任何會造成磁碟區上資料損毀的潛在風險。</span><span class="sxs-lookup"><span data-stu-id="dadee-215">This eliminates any potential risk of data corruption on the volume.</span></span> <span data-ttu-id="dadee-216">如需特定步驟，請參閱主機作業系統的指示。</span><span class="sxs-lookup"><span data-stu-id="dadee-216">For specific steps, refer to the instructions for your host operating system.</span></span>
3. <span data-ttu-id="dadee-217">在主機離線之後，請執行下列步驟以使裝置上的磁碟區離線：</span><span class="sxs-lookup"><span data-stu-id="dadee-217">After the host is offline, take the volume on the device offline by performing the following steps:</span></span>
   
   1. <span data-ttu-id="dadee-218">在 [裝置] 頁面中，選取並按兩下裝置，然後按一下 [磁碟區容器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="dadee-218">On the **Devices** page, select the device, double-click it, and then click the **Volume Containers** tab.</span></span> <span data-ttu-id="dadee-219">[磁碟區容器]  索引標籤會以表格列出與裝置相關聯的所有磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="dadee-219">The **Volume Containers** tab lists in a tabular format all the volume containers that are associated with the device.</span></span>
   2. <span data-ttu-id="dadee-220">選取並按一下磁碟區容器，以清單顯示該容器內的所有磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dadee-220">Select a volume container and click it to display the list of all the volumes within the container.</span></span>
   3. <span data-ttu-id="dadee-221">選取磁碟區，然後按一下 [離線] 。</span><span class="sxs-lookup"><span data-stu-id="dadee-221">Select a volume and click **Take offline**.</span></span>
   4. <span data-ttu-id="dadee-222">系統提示您進行確認時，按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="dadee-222">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="dadee-223">磁碟區現在應已離線。</span><span class="sxs-lookup"><span data-stu-id="dadee-223">The volume should now be offline.</span></span>
      
      <span data-ttu-id="dadee-224">磁碟區離線之後，[上線]  選項就會變成可用。</span><span class="sxs-lookup"><span data-stu-id="dadee-224">After a volume is offline, the **Bring Online** option becomes available.</span></span>

> [!NOTE]
> <span data-ttu-id="dadee-225">[離線] 命令會將要求傳送到裝置，以使磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="dadee-225">The **Take Offline** command sends a request to the device to take the volume offline.</span></span> <span data-ttu-id="dadee-226">如果主機仍在使用該磁碟區，這會導致連線中斷，但是使磁碟區離線不會失敗。</span><span class="sxs-lookup"><span data-stu-id="dadee-226">If hosts are still using the volume, this results in broken connections, but taking the volume offline will not fail.</span></span>
> 
> 

## <a name="delete-a-volume"></a><span data-ttu-id="dadee-227">刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="dadee-227">Delete a volume</span></span>
> [!IMPORTANT]
> <span data-ttu-id="dadee-228">只有當磁碟區離線時，您才能予以刪除。</span><span class="sxs-lookup"><span data-stu-id="dadee-228">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="dadee-229">請完成下列步驟來刪除磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dadee-229">Complete the following steps to delete a volume.</span></span>

### <a name="to-delete-a-volume"></a><span data-ttu-id="dadee-230">若要刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="dadee-230">To delete a volume</span></span>
1. <span data-ttu-id="dadee-231">在 [裝置] 頁面中，選取並按兩下裝置，然後按一下 [磁碟區容器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="dadee-231">On the **Devices** page, select the device, double-click it, and then click the **Volume Containers** tab.</span></span>
2. <span data-ttu-id="dadee-232">選取含有您想要刪除之磁碟區的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="dadee-232">Select the volume container that has the volume you want to delete.</span></span> <span data-ttu-id="dadee-233">按一下該磁碟區容器，即可存取 [磁碟區]  頁面。</span><span class="sxs-lookup"><span data-stu-id="dadee-233">Click the volume container to access the **Volumes** page.</span></span>
3. <span data-ttu-id="dadee-234">與這個容器相關聯的所有磁碟區會以表格顯示。</span><span class="sxs-lookup"><span data-stu-id="dadee-234">All the volumes associated with this container are displayed in a tabular format.</span></span> <span data-ttu-id="dadee-235">檢查您想要刪除之磁碟區的狀態。</span><span class="sxs-lookup"><span data-stu-id="dadee-235">Check the status of the volume you want to delete.</span></span> <span data-ttu-id="dadee-236">如果您想要刪除的磁碟區未離線，請先使其離線，請依照 [使磁碟區離線](#take-a-volume-offline)中的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="dadee-236">If the volume you want to delete is not offline, take it offline first, following the steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="dadee-237">在磁碟區離線之後，按一下頁面底部的 [刪除]  。</span><span class="sxs-lookup"><span data-stu-id="dadee-237">After the volume is offline, click **Delete** at the bottom of the page.</span></span>
5. <span data-ttu-id="dadee-238">系統提示您進行確認時，按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="dadee-238">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="dadee-239">現已刪除磁碟區，而 [磁碟區]  頁面會顯示容器內已更新的磁碟區清單。</span><span class="sxs-lookup"><span data-stu-id="dadee-239">The volume will now be deleted and the **Volumes** page will show the updated list of volumes within the container.</span></span>

## <a name="monitor-a-volume"></a><span data-ttu-id="dadee-240">監視磁碟區</span><span class="sxs-lookup"><span data-stu-id="dadee-240">Monitor a volume</span></span>
<span data-ttu-id="dadee-241">監視磁碟區可讓您為磁碟區收集 I/O 相關的統計資料。</span><span class="sxs-lookup"><span data-stu-id="dadee-241">Volume monitoring allows you to collect I/O-related statistics for a volume.</span></span> <span data-ttu-id="dadee-242">根據預設，您建立的前 32 個磁碟區會啟用監視。</span><span class="sxs-lookup"><span data-stu-id="dadee-242">Monitoring is enabled by default for the first 32 volumes that you create.</span></span> <span data-ttu-id="dadee-243">預設會停用監視其他磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dadee-243">Monitoring of additional volumes is disabled by default.</span></span> <span data-ttu-id="dadee-244">預設也會停用監視複製的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dadee-244">Monitoring of cloned volumes is also disabled by default.</span></span>

<span data-ttu-id="dadee-245">請執行下列步驟來啟用或停用監視磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dadee-245">Perform the following steps to enable or disable monitoring for a volume.</span></span>

### <a name="to-enable-or-disable-volume-monitoring"></a><span data-ttu-id="dadee-246">若要啟用或停用監視磁碟區</span><span class="sxs-lookup"><span data-stu-id="dadee-246">To enable or disable volume monitoring</span></span>
1. <span data-ttu-id="dadee-247">在 [裝置] 頁面中，選取並按兩下裝置，然後按一下 [磁碟區容器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="dadee-247">On the **Devices** page, select the device, double-click it, and then click the **Volume Containers** tab.</span></span>
2. <span data-ttu-id="dadee-248">選取磁碟區所在的磁碟區容器，然後按一下該磁碟區容器來存取 [磁碟區]  頁面。</span><span class="sxs-lookup"><span data-stu-id="dadee-248">Select the volume container in which the volume resides, and then click the volume container to access the **Volumes** page.</span></span>
3. <span data-ttu-id="dadee-249">以表格顯示所列出與這個容器相關聯的所有磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dadee-249">All the volumes associated with this container are listed in the tabular display.</span></span> <span data-ttu-id="dadee-250">按一下並選取磁碟區或磁碟區複製。</span><span class="sxs-lookup"><span data-stu-id="dadee-250">Click and select the volume or volume clone.</span></span>
4. <span data-ttu-id="dadee-251">按一下頁面底部的 [修改] 。</span><span class="sxs-lookup"><span data-stu-id="dadee-251">At the bottom of the page, click **Modify**.</span></span>
5. <span data-ttu-id="dadee-252">在 [修改磁碟區精靈] 的 [基本設定] 下，從 [監視] 下拉式清單中選取 [啟用] 或 [停用]。</span><span class="sxs-lookup"><span data-stu-id="dadee-252">In the Modify Volume wizard, under **Basic Settings**, select **Enable** or **Disable** from the **Monitoring** drop-down list.</span></span>
   
    ![修改磁碟區基本設定](./media/storsimple-manage-volumes/HCS_MonitorVolumeM.png)

## <a name="next-steps"></a><span data-ttu-id="dadee-254">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dadee-254">Next steps</span></span>
* <span data-ttu-id="dadee-255">了解如何 [複製 StorSimple 磁碟區](storsimple-clone-volume.md)。</span><span class="sxs-lookup"><span data-stu-id="dadee-255">Learn how to [clone a StorSimple volume](storsimple-clone-volume.md).</span></span>
* <span data-ttu-id="dadee-256">了解如何 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="dadee-256">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>


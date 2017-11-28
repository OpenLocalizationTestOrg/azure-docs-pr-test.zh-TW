---
title: "管理 StorSimple 中的存取控制記錄 | Microsoft Docs"
description: "說明如何使用存取控制記錄 (ACR) 以判斷哪些主機可以連接至 StorSimple 裝置上的磁碟區。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2f1475d8-36a5-4cc4-84b9-adf8a310b60c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: a87624b5706c1d9b8c2b9926e5580996a89ce984
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-access-control-records"></a><span data-ttu-id="9882b-103">使用 StorSimple Manager 服務管理存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="9882b-103">Use the StorSimple Manager service to manage access control records</span></span>
## <a name="overview"></a><span data-ttu-id="9882b-104">Overview</span><span class="sxs-lookup"><span data-stu-id="9882b-104">Overview</span></span>
<span data-ttu-id="9882b-105">存取控制記錄 (ACR) 可讓您指定哪些主機可連接至 StorSimple 裝置上的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9882b-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple device.</span></span> <span data-ttu-id="9882b-106">ACR 設為特定的磁碟區，並且包含主機的 iSCSI 限定名稱 (IQN)。</span><span class="sxs-lookup"><span data-stu-id="9882b-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="9882b-107">當主機嘗試連線到磁碟區時，裝置會檢查與該磁碟區相關聯的 ACR 的 IQN 名稱，如果相符，則會建立連接。</span><span class="sxs-lookup"><span data-stu-id="9882b-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name and if there is a match, then the connection is established.</span></span> <span data-ttu-id="9882b-108">[ **設定** ] 頁面上的存取控制記錄區段會顯示具有主機對應 IQN 的所有存取控制記錄。</span><span class="sxs-lookup"><span data-stu-id="9882b-108">The access control records section on the **Configure** page displays all the access control records with the corresponding IQNs of the hosts.</span></span>

<span data-ttu-id="9882b-109">本教學課程將說明下列常見 ACR 相關工作：</span><span class="sxs-lookup"><span data-stu-id="9882b-109">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="9882b-110">加入存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="9882b-110">Add an access control record</span></span> 
* <span data-ttu-id="9882b-111">編輯存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="9882b-111">Edit an access control record</span></span> 
* <span data-ttu-id="9882b-112">刪除存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="9882b-112">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="9882b-113">將 ACR 指派到磁碟區時，請注意磁碟區並未被多個非叢集主機並行存取，因為這可能會損毀磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9882b-113">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span> 
> * <span data-ttu-id="9882b-114">從磁碟區刪除 ACR 時，請確定對應的主機未存取磁碟區，因為刪除作業可能會導致讀寫中斷。</span><span class="sxs-lookup"><span data-stu-id="9882b-114">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="add-an-access-control-record"></a><span data-ttu-id="9882b-115">加入存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="9882b-115">Add an access control record</span></span>
<span data-ttu-id="9882b-116">使用 StorSimple Manager 服務的 [設定]  頁面加入 ACR。</span><span class="sxs-lookup"><span data-stu-id="9882b-116">You use the StorSimple Manager service **Configure** page to add ACRs.</span></span> <span data-ttu-id="9882b-117">一般而言，您會讓一個 ACR 與一個磁碟區產生關聯。</span><span class="sxs-lookup"><span data-stu-id="9882b-117">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="9882b-118">執行下列步驟以加入 ACR。</span><span class="sxs-lookup"><span data-stu-id="9882b-118">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-access-control-record"></a><span data-ttu-id="9882b-119">加入存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="9882b-119">To add an access control record</span></span>
1. <span data-ttu-id="9882b-120">在服務登陸頁面上，選取您的服務，連按兩下該服務名稱，然後按一下 [ **設定** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9882b-120">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="9882b-121">在 [存取控制記錄] 底下的表格式清單中，提供 ACR 的 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="9882b-121">In the tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="9882b-122">在 [ **iSCSI 啟動器名稱**] 下方，提供 Windows 主機的 IQN 名稱。</span><span class="sxs-lookup"><span data-stu-id="9882b-122">Provide the IQN name of your Windows host under **iSCSI Initiator Name**.</span></span> <span data-ttu-id="9882b-123">若要取得 Windows Server 主機的 IQN，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="9882b-123">To get the IQN of your Windows Server host, do the following:</span></span>
   
   * <span data-ttu-id="9882b-124">在 Windows 主機上啟動 Microsoft iSCSI 啟動器。</span><span class="sxs-lookup"><span data-stu-id="9882b-124">Start the Microsoft iSCSI initiator on your Windows host.</span></span>
   * <span data-ttu-id="9882b-125">在 [iSCSI 啟動器屬性] 視窗的 [設定] 索引標籤上，選取並複製 [啟動器名稱] 欄位的字串。</span><span class="sxs-lookup"><span data-stu-id="9882b-125">In the **iSCSI Initiator Properties** window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span></span>
   * <span data-ttu-id="9882b-126">在 Azure 傳統入口網站的 ACR 表格上的 [iSCSI 啟動器名稱  ] 欄位中貼上此字串。</span><span class="sxs-lookup"><span data-stu-id="9882b-126">Paste this string in the **iSCSI Initiator Name** field on the ACRs table in the Azure classic portal.</span></span>
4. <span data-ttu-id="9882b-127">按一下 [ **儲存** ] 以儲存新建立的 ACR。</span><span class="sxs-lookup"><span data-stu-id="9882b-127">Click **Save** to save the newly created ACR.</span></span> <span data-ttu-id="9882b-128">表格式清單會更新以反映此新增。</span><span class="sxs-lookup"><span data-stu-id="9882b-128">The tabular listing will be updated to reflect this addition.</span></span>

## <a name="edit-an-access-control-record"></a><span data-ttu-id="9882b-129">編輯存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="9882b-129">Edit an access control record</span></span>
<span data-ttu-id="9882b-130">您可以使用 Azure 傳統入口網站中的 [設定]  頁面編輯 ACR。</span><span class="sxs-lookup"><span data-stu-id="9882b-130">You use the **Configure** page in the Azure classic portal to edit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="9882b-131">您只能修改目前未在使用中的 ACR。</span><span class="sxs-lookup"><span data-stu-id="9882b-131">You can modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="9882b-132">若要編輯與目前正在使用中的磁碟區相關聯的 ACR，您必須先讓磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="9882b-132">To edit an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="9882b-133">執行下列步驟以編輯 ACR。</span><span class="sxs-lookup"><span data-stu-id="9882b-133">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-access-control-record"></a><span data-ttu-id="9882b-134">編輯存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="9882b-134">To edit an access control record</span></span>
1. <span data-ttu-id="9882b-135">在服務登陸頁面上，選取您的服務，連按兩下該服務名稱，然後按一下 [ **設定** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9882b-135">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="9882b-136">在存取控制記錄的表格式清單中，將滑鼠停留在您想要修改的 ACR 上。</span><span class="sxs-lookup"><span data-stu-id="9882b-136">In the tabular listing of the access control records, hover over the ACR that you wish to modify.</span></span>
3. <span data-ttu-id="9882b-137">為 ACR 提供新的名稱和/或 IQN。</span><span class="sxs-lookup"><span data-stu-id="9882b-137">Supply a new name and/or IQN for the ACR.</span></span>
4. <span data-ttu-id="9882b-138">按一下 [ **儲存** ] 以儲存修改的 ACR。</span><span class="sxs-lookup"><span data-stu-id="9882b-138">Click **Save** to save the modified ACR.</span></span> <span data-ttu-id="9882b-139">表格式清單會更新以反映此變更。</span><span class="sxs-lookup"><span data-stu-id="9882b-139">The tabular listing will be updated to reflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="9882b-140">刪除存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="9882b-140">Delete an access control record</span></span>
<span data-ttu-id="9882b-141">您可以使用 Azure 傳統入口網站中的 [設定]  頁面刪除 ACR。</span><span class="sxs-lookup"><span data-stu-id="9882b-141">You use the **Configure** page in the Azure classic portal to delete ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="9882b-142">您只能刪除目前未在使用中的 ACR。</span><span class="sxs-lookup"><span data-stu-id="9882b-142">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="9882b-143">若要刪除與目前正在使用中的磁碟區相關聯的 ACR，您必須先讓磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="9882b-143">To delete an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="9882b-144">執行下列步驟來刪除存取控制記錄。</span><span class="sxs-lookup"><span data-stu-id="9882b-144">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="9882b-145">刪除存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="9882b-145">To delete an access control record</span></span>
1. <span data-ttu-id="9882b-146">在服務登陸頁面上，選取您的服務，連按兩下該服務名稱，然後按一下 [ **設定** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9882b-146">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="9882b-147">在存取控制記錄 (ACR) 的表格式清單中，將滑鼠停留在您想要刪除的 ACR 上。</span><span class="sxs-lookup"><span data-stu-id="9882b-147">In the tabular listing of the access control records (ACRs), hover over the ACR that you wish to delete.</span></span>
3. <span data-ttu-id="9882b-148">刪除圖示 (**x**) 會出現在您選取之 ACR 資料行的最右邊。</span><span class="sxs-lookup"><span data-stu-id="9882b-148">A delete icon (**x**) will appear in the extreme right column for the ACR that you select.</span></span> <span data-ttu-id="9882b-149">按一下 [ **x** ] 圖示，以刪除 ACR。</span><span class="sxs-lookup"><span data-stu-id="9882b-149">Click the **x** icon to delete the ACR.</span></span>
4. <span data-ttu-id="9882b-150">當系統提示您確認時，按一下 [ **是** ] 繼續進行刪除。</span><span class="sxs-lookup"><span data-stu-id="9882b-150">When prompted for confirmation, click **YES** to continue with the deletion.</span></span> <span data-ttu-id="9882b-151">表格式清單會更新以反映刪除。</span><span class="sxs-lookup"><span data-stu-id="9882b-151">The tabular listing will be updated to reflect the deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9882b-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9882b-152">Next steps</span></span>
* <span data-ttu-id="9882b-153">深入了解 [管理 StorSimple 磁碟區](storsimple-manage-volumes.md)。</span><span class="sxs-lookup"><span data-stu-id="9882b-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="9882b-154">深入了解 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="9882b-154">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>


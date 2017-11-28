---
title: "管理 StorSimple 中的存取控制記錄 | Microsoft Docs"
description: "說明如何使用存取控制記錄 (ACR) 以判斷哪些主機可以連接至 StorSimple 裝置上的磁碟區。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: alkohli
ms.openlocfilehash: 9173e34f889ce1c082b20bb382cb6ca9a03dd797
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-access-control-records"></a><span data-ttu-id="e278b-103">使用 StorSimple Manager 服務管理存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="e278b-103">Use the StorSimple Manager service to manage access control records</span></span>

## <a name="overview"></a><span data-ttu-id="e278b-104">Overview</span><span class="sxs-lookup"><span data-stu-id="e278b-104">Overview</span></span>
<span data-ttu-id="e278b-105">存取控制記錄 (ACR) 可讓您指定哪些主機可連接至 StorSimple 裝置上的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e278b-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple device.</span></span> <span data-ttu-id="e278b-106">ACR 設為特定的磁碟區，並且包含主機的 iSCSI 限定名稱 (IQN)。</span><span class="sxs-lookup"><span data-stu-id="e278b-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="e278b-107">當主機嘗試連線到磁碟區時，裝置會檢查與該磁碟區相關聯的 ACR 的 IQN 名稱，如果相符，則會建立連接。</span><span class="sxs-lookup"><span data-stu-id="e278b-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name and if there is a match, then the connection is established.</span></span> <span data-ttu-id="e278b-108">[StorSimple 裝置管理員服務] 刀鋒視窗之 [設定] 區段中，存取控制記錄會顯示主機的所有存取控制記錄及對應的 IQN。</span><span class="sxs-lookup"><span data-stu-id="e278b-108">The access control records in the **Configuration** section of your StorSimple Device Manager service blade display all the access control records with the corresponding IQNs of the hosts.</span></span>

<span data-ttu-id="e278b-109">本教學課程將說明下列常見 ACR 相關工作：</span><span class="sxs-lookup"><span data-stu-id="e278b-109">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="e278b-110">加入存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="e278b-110">Add an access control record</span></span>
* <span data-ttu-id="e278b-111">編輯存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="e278b-111">Edit an access control record</span></span>
* <span data-ttu-id="e278b-112">刪除存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="e278b-112">Delete an access control record</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="e278b-113">將 ACR 指派到磁碟區時，請注意磁碟區並未被多個非叢集主機並行存取，因為這可能會損毀磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e278b-113">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>
> * <span data-ttu-id="e278b-114">從磁碟區刪除 ACR 時，請確定對應的主機未存取磁碟區，因為刪除作業可能會導致讀寫中斷。</span><span class="sxs-lookup"><span data-stu-id="e278b-114">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>

## <a name="get-the-iqn"></a><span data-ttu-id="e278b-115">取得 IQN</span><span class="sxs-lookup"><span data-stu-id="e278b-115">Get the IQN</span></span>

<span data-ttu-id="e278b-116">請執行下列步驟，以取得正在執行 Windows Server 2012 之 Windows 主機的 IQN。</span><span class="sxs-lookup"><span data-stu-id="e278b-116">Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a><span data-ttu-id="e278b-117">加入存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="e278b-117">Add an access control record</span></span>
<span data-ttu-id="e278b-118">您可以使用 [StorSimple 裝置管理員服務] 刀鋒視窗中的 [設定] 區段來新增 ACR。</span><span class="sxs-lookup"><span data-stu-id="e278b-118">You use the **Configuration** section in the StorSimple Device Manager service blade to add ACRs.</span></span> <span data-ttu-id="e278b-119">一般而言，您會讓一個 ACR 與一個磁碟區產生關聯。</span><span class="sxs-lookup"><span data-stu-id="e278b-119">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="e278b-120">執行下列步驟以加入 ACR。</span><span class="sxs-lookup"><span data-stu-id="e278b-120">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-acr"></a><span data-ttu-id="e278b-121">加入 ACR</span><span class="sxs-lookup"><span data-stu-id="e278b-121">To add an ACR</span></span>

1. <span data-ttu-id="e278b-122">移至 StorSimple 裝置管理員服務，按兩下服務名稱，然後在 [設定] 區段內按一下 [存取控制記錄]。</span><span class="sxs-lookup"><span data-stu-id="e278b-122">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="e278b-123">在 [存取控制記錄] 刀鋒視窗中，按一下 [+ 新增 ACR]。</span><span class="sxs-lookup"><span data-stu-id="e278b-123">In the **Access control records** blade, click **+ Add ACR**.</span></span>

    ![按一下 [新增 ACR]](./media/storsimple-8000-manage-acrs/createacr1.png)

3. <span data-ttu-id="e278b-125">在 [新增 ACR] 刀鋒視窗中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e278b-125">In the **Add ACR** blade, do the following steps:</span></span>

    1. <span data-ttu-id="e278b-126">提供 ACR 的名稱。</span><span class="sxs-lookup"><span data-stu-id="e278b-126">Supply a name for your ACR.</span></span>
    
    2. <span data-ttu-id="e278b-127">在 [iSCSI 啟動器名稱 \(IQN)\] 下方，提供 Windows Server 主機的 IQN 名稱。</span><span class="sxs-lookup"><span data-stu-id="e278b-127">Provide the IQN name of your Windows Server host under **iSCSI Initiator Name (IQN)**.</span></span>

    3. <span data-ttu-id="e278b-128">按一下 [新增] 以建立 ACR。</span><span class="sxs-lookup"><span data-stu-id="e278b-128">Click **Add** to create the ACR.</span></span>

        ![按一下 [新增 ACR]](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  <span data-ttu-id="e278b-130">新增的 ACR 會顯示在 ACR 的表格式清單中。</span><span class="sxs-lookup"><span data-stu-id="e278b-130">The newly added ACR will display in the tabular listing of ACRs.</span></span>

    ![按一下 [新增 ACR]](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a><span data-ttu-id="e278b-132">編輯存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="e278b-132">Edit an access control record</span></span>
<span data-ttu-id="e278b-133">您可以使用 [StorSimple 裝置管理員服務] 刀鋒視窗中的 [設定] 區段來編輯 ACR。</span><span class="sxs-lookup"><span data-stu-id="e278b-133">You use the **Configuration** section in the StorSimple Device Manager service blade to edit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="e278b-134">建議您只修改目前未在使用中的 ACR。</span><span class="sxs-lookup"><span data-stu-id="e278b-134">It is recommended that you modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="e278b-135">若要編輯與目前正在使用中的磁碟區相關聯的 ACR，您必須先讓磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="e278b-135">To edit an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>

<span data-ttu-id="e278b-136">執行下列步驟以編輯 ACR。</span><span class="sxs-lookup"><span data-stu-id="e278b-136">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-access-control-record"></a><span data-ttu-id="e278b-137">編輯存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="e278b-137">To edit an access control record</span></span>
1.  <span data-ttu-id="e278b-138">移至 StorSimple 裝置管理員服務，按兩下服務名稱，然後在 [設定] 區段內按一下 [存取控制記錄]。</span><span class="sxs-lookup"><span data-stu-id="e278b-138">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>

    ![移至存取控制記錄](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="e278b-140">在存取控制記錄的表格式清單中，按一下並選取您想要修改的 ACR。</span><span class="sxs-lookup"><span data-stu-id="e278b-140">In the tabular listing of the access control records, click and select the ACR that you wish to modify.</span></span>

    ![編輯存取控制記錄](./media/storsimple-8000-manage-acrs/editacr1.png)

3. <span data-ttu-id="e278b-142">在 [編輯存取控制記錄] 刀鋒視窗中，提供對應至其他主機的不同 IQN。</span><span class="sxs-lookup"><span data-stu-id="e278b-142">In the **Edit access control record** blade, provide a different IQN corresponding to another host.</span></span>

    ![編輯存取控制記錄](./media/storsimple-8000-manage-acrs/editacr2.png)

4. <span data-ttu-id="e278b-144">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="e278b-144">Click **Save**.</span></span> <span data-ttu-id="e278b-145">系統提示您進行確認時，按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="e278b-145">When prompted for confirmation, click **Yes**.</span></span> 

    ![編輯存取控制記錄](./media/storsimple-8000-manage-acrs/editacr3.png)

5. <span data-ttu-id="e278b-147">ACR 更新時，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="e278b-147">You are notified when the ACR is updated.</span></span> <span data-ttu-id="e278b-148">表格式清單也會一併更新以反映變更。</span><span class="sxs-lookup"><span data-stu-id="e278b-148">The tabular listing also updates to reflect the change.</span></span>

   
## <a name="delete-an-access-control-record"></a><span data-ttu-id="e278b-149">刪除存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="e278b-149">Delete an access control record</span></span>
<span data-ttu-id="e278b-150">您可以使用 [StorSimple 裝置管理員服務] 刀鋒視窗中的 [設定] 區段來刪除 ACR。</span><span class="sxs-lookup"><span data-stu-id="e278b-150">You use the **Configuration** section in the StorSimple Device Manager service blade to delete ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="e278b-151">您只能刪除目前未在使用中的 ACR。</span><span class="sxs-lookup"><span data-stu-id="e278b-151">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="e278b-152">若要刪除與目前正在使用中的磁碟區相關聯的 ACR，您必須先讓磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="e278b-152">To delete an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>

<span data-ttu-id="e278b-153">執行下列步驟來刪除存取控制記錄。</span><span class="sxs-lookup"><span data-stu-id="e278b-153">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="e278b-154">刪除存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="e278b-154">To delete an access control record</span></span>
1.  <span data-ttu-id="e278b-155">移至 StorSimple 裝置管理員服務，按兩下服務名稱，然後在 [設定] 區段內按一下 [存取控制記錄]。</span><span class="sxs-lookup"><span data-stu-id="e278b-155">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>

    ![移至存取控制記錄](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="e278b-157">在存取控制記錄的表格式清單中，按一下並選取您想要刪除的 ACR。</span><span class="sxs-lookup"><span data-stu-id="e278b-157">In the tabular listing of the access control records, click and select the ACR that you wish to delete.</span></span>

    ![移至存取控制記錄](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. <span data-ttu-id="e278b-159">以滑鼠右鍵按一下可叫用操作功能表，然後選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="e278b-159">Right-click to invoke the context menu and select **Delete**.</span></span>

    ![移至存取控制記錄](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. <span data-ttu-id="e278b-161">當出現提示確認時，請檢閱資訊，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="e278b-161">When prompted for confirmation, review the information and then click **Delete**.</span></span>

    ![移至存取控制記錄](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. <span data-ttu-id="e278b-163">當刪除作業完成時，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="e278b-163">You are notified when the deletion completes.</span></span> <span data-ttu-id="e278b-164">表格式清單會更新以反映此刪除動作。</span><span class="sxs-lookup"><span data-stu-id="e278b-164">The tabular listing is updated to reflect the deletion.</span></span>

    ![移至存取控制記錄](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a><span data-ttu-id="e278b-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e278b-166">Next steps</span></span>
* <span data-ttu-id="e278b-167">深入了解 [管理 StorSimple 磁碟區](storsimple-8000-manage-volumes-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="e278b-167">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="e278b-168">深入了解 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="e278b-168">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>


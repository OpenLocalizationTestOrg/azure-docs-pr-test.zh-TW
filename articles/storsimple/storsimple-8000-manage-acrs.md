---
title: "在 StorSimple aaaManage 存取控制記錄 |Microsoft 文件"
description: "描述 toouse 存取控制記錄 (Acr) toodetermine 哪些主機可連接 tooa hello StorSimple 裝置上的磁碟區的方式。"
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
ms.openlocfilehash: cf532206e2c0bc49da853663ba34ae993ec2981d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a><span data-ttu-id="b96e6-103">使用 hello StorSimple Manager 服務 toomanage 存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="b96e6-103">Use hello StorSimple Manager service toomanage access control records</span></span>

## <a name="overview"></a><span data-ttu-id="b96e6-104">概觀</span><span class="sxs-lookup"><span data-stu-id="b96e6-104">Overview</span></span>
<span data-ttu-id="b96e6-105">存取控制記錄 (Acr) 可讓您 toospecify 哪些主機可連接 tooa hello StorSimple 裝置上的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b96e6-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple device.</span></span> <span data-ttu-id="b96e6-106">Acr tooa 特定磁碟區，並設定包含 hello iSCSI hello 主機的限定名稱 （iqn 相關聯）。</span><span class="sxs-lookup"><span data-stu-id="b96e6-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="b96e6-107">當主機嘗試 tooconnect tooa 磁碟區時，hello 裝置會檢查的 hello 與 hello IQN 名稱，如果沒有符合項目，然後 hello 建立連接該磁碟區相關聯的 ACR。</span><span class="sxs-lookup"><span data-stu-id="b96e6-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="b96e6-108">hello hello 中的存取控制記錄**組態**您 StorSimple 裝置管理員服務刀鋒視窗的區段顯示以 hello 對應 iqn 相關聯的 hello 主機的所有 hello 存取控制記錄。</span><span class="sxs-lookup"><span data-stu-id="b96e6-108">hello access control records in hello **Configuration** section of your StorSimple Device Manager service blade display all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

<span data-ttu-id="b96e6-109">本教學課程將說明下列 ACR 相關的一般工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="b96e6-109">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="b96e6-110">加入存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="b96e6-110">Add an access control record</span></span>
* <span data-ttu-id="b96e6-111">編輯存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="b96e6-111">Edit an access control record</span></span>
* <span data-ttu-id="b96e6-112">刪除存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="b96e6-112">Delete an access control record</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="b96e6-113">指派的 ACR tooa 磁碟區時，小心，hello 存取磁碟區不同時由多個非叢集主機因為這可能會損毀 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b96e6-113">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>
> * <span data-ttu-id="b96e6-114">當從磁碟區刪除 ACR，請確定該 hello 對應的主機未存取 hello 磁碟區，因為 hello 刪除可能會導致讀寫中斷。</span><span class="sxs-lookup"><span data-stu-id="b96e6-114">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>

## <a name="get-hello-iqn"></a><span data-ttu-id="b96e6-115">取得 hello IQN</span><span class="sxs-lookup"><span data-stu-id="b96e6-115">Get hello IQN</span></span>

<span data-ttu-id="b96e6-116">執行下列步驟 tooget hello 執行 Windows Server 2012 的 Windows 主機的 IQN hello。</span><span class="sxs-lookup"><span data-stu-id="b96e6-116">Perform hello following steps tooget hello IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a><span data-ttu-id="b96e6-117">加入存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="b96e6-117">Add an access control record</span></span>
<span data-ttu-id="b96e6-118">使用 hello**組態**hello StorSimple 裝置管理員服務刀鋒視窗 tooadd Acr > 一節。</span><span class="sxs-lookup"><span data-stu-id="b96e6-118">You use hello **Configuration** section in hello StorSimple Device Manager service blade tooadd ACRs.</span></span> <span data-ttu-id="b96e6-119">一般而言，您會讓一個 ACR 與一個磁碟區產生關聯。</span><span class="sxs-lookup"><span data-stu-id="b96e6-119">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="b96e6-120">執行下列步驟 tooadd ACR hello。</span><span class="sxs-lookup"><span data-stu-id="b96e6-120">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-acr"></a><span data-ttu-id="b96e6-121">tooadd ACR</span><span class="sxs-lookup"><span data-stu-id="b96e6-121">tooadd an ACR</span></span>

1. <span data-ttu-id="b96e6-122">移 tooyour StorSimple 裝置管理員服務、 按兩下 hello 服務名稱，然後再內 hello**組態**區段中，按一下**存取控制記錄**。</span><span class="sxs-lookup"><span data-stu-id="b96e6-122">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="b96e6-123">在 hello**存取控制記錄**刀鋒視窗中，按一下  **+ 新增 ACR**。</span><span class="sxs-lookup"><span data-stu-id="b96e6-123">In hello **Access control records** blade, click **+ Add ACR**.</span></span>

    ![按一下 [新增 ACR]](./media/storsimple-8000-manage-acrs/createacr1.png)

3. <span data-ttu-id="b96e6-125">在 hello**新增 ACR**刀鋒視窗中，執行下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="b96e6-125">In hello **Add ACR** blade, do hello following steps:</span></span>

    1. <span data-ttu-id="b96e6-126">提供 ACR 的名稱。</span><span class="sxs-lookup"><span data-stu-id="b96e6-126">Supply a name for your ACR.</span></span>
    
    2. <span data-ttu-id="b96e6-127">提供在 Windows Server 主機 hello IQN 名稱**iSCSI 啟動器名稱 (IQN)**。</span><span class="sxs-lookup"><span data-stu-id="b96e6-127">Provide hello IQN name of your Windows Server host under **iSCSI Initiator Name (IQN)**.</span></span>

    3. <span data-ttu-id="b96e6-128">按一下**新增**toocreate hello ACR。</span><span class="sxs-lookup"><span data-stu-id="b96e6-128">Click **Add** toocreate hello ACR.</span></span>

        ![按一下 [新增 ACR]](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  <span data-ttu-id="b96e6-130">hello 新增 ACR 會顯示在 hello 表格 Acr 清單。</span><span class="sxs-lookup"><span data-stu-id="b96e6-130">hello newly added ACR will display in hello tabular listing of ACRs.</span></span>

    ![按一下 [新增 ACR]](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a><span data-ttu-id="b96e6-132">編輯存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="b96e6-132">Edit an access control record</span></span>
<span data-ttu-id="b96e6-133">使用 hello**組態**hello StorSimple 裝置管理員服務刀鋒視窗 tooedit Acr > 一節。</span><span class="sxs-lookup"><span data-stu-id="b96e6-133">You use hello **Configuration** section in hello StorSimple Device Manager service blade tooedit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="b96e6-134">建議您只修改目前未在使用中的 ACR。</span><span class="sxs-lookup"><span data-stu-id="b96e6-134">It is recommended that you modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="b96e6-135">tooedit 與目前正在使用的磁碟區相關聯的 ACR，您必須先進行 hello 磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="b96e6-135">tooedit an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>

<span data-ttu-id="b96e6-136">執行下列步驟 tooedit ACR hello。</span><span class="sxs-lookup"><span data-stu-id="b96e6-136">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-access-control-record"></a><span data-ttu-id="b96e6-137">tooedit 存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="b96e6-137">tooedit an access control record</span></span>
1.  <span data-ttu-id="b96e6-138">移 tooyour StorSimple 裝置管理員服務、 按兩下 hello 服務名稱，然後再內 hello**組態**區段中，按一下**存取控制記錄**。</span><span class="sxs-lookup"><span data-stu-id="b96e6-138">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>

    ![移 tooaccess 控制記錄](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="b96e6-140">在 hello 表格清單中的 hello 存取控制記錄，按一下並選取您想 toomodify ACR hello。</span><span class="sxs-lookup"><span data-stu-id="b96e6-140">In hello tabular listing of hello access control records, click and select hello ACR that you wish toomodify.</span></span>

    ![編輯存取控制記錄](./media/storsimple-8000-manage-acrs/editacr1.png)

3. <span data-ttu-id="b96e6-142">在 hello**編輯存取控制記錄**刀鋒視窗中，提供不同的 IQN 對應 tooanother 主機。</span><span class="sxs-lookup"><span data-stu-id="b96e6-142">In hello **Edit access control record** blade, provide a different IQN corresponding tooanother host.</span></span>

    ![編輯存取控制記錄](./media/storsimple-8000-manage-acrs/editacr2.png)

4. <span data-ttu-id="b96e6-144">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b96e6-144">Click **Save**.</span></span> <span data-ttu-id="b96e6-145">系統提示您進行確認時，按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="b96e6-145">When prompted for confirmation, click **Yes**.</span></span> 

    ![編輯存取控制記錄](./media/storsimple-8000-manage-acrs/editacr3.png)

5. <span data-ttu-id="b96e6-147">Hello ACR 更新時，會通知您。</span><span class="sxs-lookup"><span data-stu-id="b96e6-147">You are notified when hello ACR is updated.</span></span> <span data-ttu-id="b96e6-148">hello 表格清單也會更新 tooreflect hello 變更。</span><span class="sxs-lookup"><span data-stu-id="b96e6-148">hello tabular listing also updates tooreflect hello change.</span></span>

   
## <a name="delete-an-access-control-record"></a><span data-ttu-id="b96e6-149">刪除存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="b96e6-149">Delete an access control record</span></span>
<span data-ttu-id="b96e6-150">使用 hello**組態**hello StorSimple 裝置管理員服務刀鋒視窗 toodelete Acr > 一節。</span><span class="sxs-lookup"><span data-stu-id="b96e6-150">You use hello **Configuration** section in hello StorSimple Device Manager service blade toodelete ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="b96e6-151">您只能刪除目前未在使用中的 ACR。</span><span class="sxs-lookup"><span data-stu-id="b96e6-151">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="b96e6-152">toodelete 與目前正在使用的磁碟區相關聯的 ACR，您必須先進行 hello 磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="b96e6-152">toodelete an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>

<span data-ttu-id="b96e6-153">執行下列步驟 toodelete 存取控制記錄的 hello。</span><span class="sxs-lookup"><span data-stu-id="b96e6-153">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="b96e6-154">toodelete 存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="b96e6-154">toodelete an access control record</span></span>
1.  <span data-ttu-id="b96e6-155">移 tooyour StorSimple 裝置管理員服務、 按兩下 hello 服務名稱，然後再內 hello**組態**區段中，按一下**存取控制記錄**。</span><span class="sxs-lookup"><span data-stu-id="b96e6-155">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>

    ![移 tooaccess 控制記錄](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="b96e6-157">在 hello 表格清單中的 hello 存取控制記錄，按一下並選取您想 toodelete ACR hello。</span><span class="sxs-lookup"><span data-stu-id="b96e6-157">In hello tabular listing of hello access control records, click and select hello ACR that you wish toodelete.</span></span>

    ![移 tooaccess 控制記錄](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. <span data-ttu-id="b96e6-159">Tooinvoke hello 操作功能表上按一下滑鼠右鍵，然後選取**刪除**。</span><span class="sxs-lookup"><span data-stu-id="b96e6-159">Right-click tooinvoke hello context menu and select **Delete**.</span></span>

    ![移 tooaccess 控制記錄](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. <span data-ttu-id="b96e6-161">當提示確認時，檢閱 hello 資訊，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="b96e6-161">When prompted for confirmation, review hello information and then click **Delete**.</span></span>

    ![移 tooaccess 控制記錄](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. <span data-ttu-id="b96e6-163">Hello 刪除完成時，會通知您。</span><span class="sxs-lookup"><span data-stu-id="b96e6-163">You are notified when hello deletion completes.</span></span> <span data-ttu-id="b96e6-164">hello 表格清單是更新的 tooreflect hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="b96e6-164">hello tabular listing is updated tooreflect hello deletion.</span></span>

    ![移 tooaccess 控制記錄](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a><span data-ttu-id="b96e6-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b96e6-166">Next steps</span></span>
* <span data-ttu-id="b96e6-167">深入了解 [管理 StorSimple 磁碟區](storsimple-8000-manage-volumes-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="b96e6-167">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="b96e6-168">深入了解[使用您的 StorSimple 裝置 hello StorSimple Manager 服務 tooadminister](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="b96e6-168">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>


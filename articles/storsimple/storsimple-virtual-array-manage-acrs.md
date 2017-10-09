---
title: "為 StorSimple Virtual Array aaaManage 存取控制記錄 |Microsoft 文件"
description: "描述 toomanage 存取控制記錄 (Acr) toodetermine 哪些主機可連接 tooa hello StorSimple Virtual Array 上的磁碟區的方式。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e154bb4f-faab-4d92-a593-900c3ddc9595
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 608fdf72413761ce3c9c4bf297a748489c415685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-access-control-records-for-storsimple-virtual-array"></a><span data-ttu-id="43a49-103">StorSimple Virtual Array 的使用 StorSimple 裝置管理員 toomanage 存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="43a49-103">Use StorSimple Device Manager toomanage access control records for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="43a49-104">概觀</span><span class="sxs-lookup"><span data-stu-id="43a49-104">Overview</span></span>

<span data-ttu-id="43a49-105">存取控制記錄 (Acr) 可讓您 toospecify 哪些主機可連接 tooa hello StorSimple Virtual Array （也稱為 hello StorSimple 內部部署虛擬裝置） 上的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="43a49-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple Virtual Array (also known as hello StorSimple on-premises virtual device).</span></span> <span data-ttu-id="43a49-106">Acr tooa 特定磁碟區，並設定包含 hello iSCSI hello 主機的限定名稱 （iqn 相關聯）。</span><span class="sxs-lookup"><span data-stu-id="43a49-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="43a49-107">Hello 裝置當主機嘗試 tooconnect tooa 磁碟區時，會檢查 hello 與 hello IQN 名稱，該磁碟區相關聯的 ACR，如果沒有相符項目，然後 hello 建立連接。</span><span class="sxs-lookup"><span data-stu-id="43a49-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name, and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="43a49-108">hello**存取控制記錄**刀鋒視窗內 hello**組態**您的裝置管理員服務 區段會顯示以 hello 對應 iqn 相關聯的 hello 主機的所有 hello 存取控制記錄。</span><span class="sxs-lookup"><span data-stu-id="43a49-108">hello **Access control records** blade within hello **Configuration** section of your Device Manager service displays all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

![管理存取控制記錄](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

<span data-ttu-id="43a49-110">本教學課程將說明下列 ACR 相關的一般工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="43a49-110">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="43a49-111">取得 hello IQN</span><span class="sxs-lookup"><span data-stu-id="43a49-111">Get hello IQN</span></span>
* <span data-ttu-id="43a49-112">加入存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="43a49-112">Add an access control record</span></span>
* <span data-ttu-id="43a49-113">編輯存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="43a49-113">Edit an access control record</span></span>
* <span data-ttu-id="43a49-114">刪除存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="43a49-114">Delete an access control record</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="43a49-115">指派的 ACR tooa 磁碟區時，小心，hello 存取磁碟區不同時由多個非叢集主機因為這可能會損毀 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="43a49-115">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>
> * <span data-ttu-id="43a49-116">當從磁碟區刪除 ACR，請確定該 hello 對應的主機未存取 hello 磁碟區，因為 hello 刪除可能會導致讀寫中斷。</span><span class="sxs-lookup"><span data-stu-id="43a49-116">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>


## <a name="get-hello-iqn"></a><span data-ttu-id="43a49-117">取得 hello IQN</span><span class="sxs-lookup"><span data-stu-id="43a49-117">Get hello IQN</span></span>

<span data-ttu-id="43a49-118">執行下列步驟 tooget hello 執行 Windows Server 2012 的 Windows 主機的 IQN hello。</span><span class="sxs-lookup"><span data-stu-id="43a49-118">Perform hello following steps tooget hello IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a><span data-ttu-id="43a49-119">加入 ACR</span><span class="sxs-lookup"><span data-stu-id="43a49-119">Add an ACR</span></span>

<span data-ttu-id="43a49-120">您使用**存取控制記錄**刀鋒視窗內 hello**組態**您 StorSimple 裝置管理員服務 tooadd Acr 的區段。</span><span class="sxs-lookup"><span data-stu-id="43a49-120">You use **Access control records** blade within hello **Configuration** section of your StorSimple Device Manager service tooadd ACRs.</span></span> <span data-ttu-id="43a49-121">一般而言，您會讓一個 ACR 與一個磁碟區產生關聯。</span><span class="sxs-lookup"><span data-stu-id="43a49-121">Typically, you associate one ACR with one volume.</span></span>

<span data-ttu-id="43a49-122">如需將一個 ACR 與磁碟區產生關聯的資訊，請太[加入磁碟區](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume)。</span><span class="sxs-lookup"><span data-stu-id="43a49-122">For information about associating an ACR with a volume, go too[add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43a49-123">指派的 ACR tooa 磁碟區時，小心，hello 存取磁碟區不同時由多個非叢集主機因為這可能會損毀 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="43a49-123">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>


<span data-ttu-id="43a49-124">執行下列步驟 tooadd ACR hello。</span><span class="sxs-lookup"><span data-stu-id="43a49-124">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-acr"></a><span data-ttu-id="43a49-125">tooadd ACR</span><span class="sxs-lookup"><span data-stu-id="43a49-125">tooadd an ACR</span></span>

1. <span data-ttu-id="43a49-126">在 hello 服務登陸頁面上，選取您的服務、 按兩下 hello 服務名稱，然後再內 hello**組態**區段中，按一下**存取控制記錄**。</span><span class="sxs-lookup"><span data-stu-id="43a49-126">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="43a49-127">在 hello**存取控制記錄**刀鋒視窗中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="43a49-127">In hello **Access control records** blade, click **Add**.</span></span>
3. <span data-ttu-id="43a49-128">在 hello**新增 ACR**刀鋒視窗中，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="43a49-128">In hello **Add ACR** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="43a49-129">提供 ACR 的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="43a49-129">Supply a **Name** for your ACR.</span></span>
    
    2. <span data-ttu-id="43a49-130">在下**iSCSI 啟動器名稱**，提供 hello Windows 主機的 IQN 名稱。</span><span class="sxs-lookup"><span data-stu-id="43a49-130">Under **iSCSI Initiator Name**, provide hello IQN name of your Windows host.</span></span> <span data-ttu-id="43a49-131">tooget hello 您 Windows Server 主機的 IQN，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="43a49-131">tooget hello IQN of your Windows Server host, do hello following:</span></span>
   
    3. <span data-ttu-id="43a49-132">在 Windows 主機上啟動 hello Microsoft iSCSI 啟動器。</span><span class="sxs-lookup"><span data-stu-id="43a49-132">Start hello Microsoft iSCSI initiator on your Windows host.</span></span> <span data-ttu-id="43a49-133">Hello iSCSI 啟動器屬性 視窗中，在 hello**組態**索引標籤上，選取並複製 hello 字串 hello 從**啟動器名稱**欄位。</span><span class="sxs-lookup"><span data-stu-id="43a49-133">In hello iSCSI Initiator Properties window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
    <span data-ttu-id="43a49-134">貼上此字串在 hello **IQN**欄位 hello**新增 ACR**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="43a49-134">Paste this string in hello **IQN** field in hello **Add ACR** blade.</span></span>
   
    6. <span data-ttu-id="43a49-135">按一下**新增**tooadd hello ACR。</span><span class="sxs-lookup"><span data-stu-id="43a49-135">Click **Add** tooadd hello ACR.</span></span>  
   
        ![新增存取控制記錄](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. <span data-ttu-id="43a49-137">hello 表格清單是更新的 tooreflect 這個額外功能。</span><span class="sxs-lookup"><span data-stu-id="43a49-137">hello tabular listing is updated tooreflect this addition.</span></span>

## <a name="edit-an-acr"></a><span data-ttu-id="43a49-138">編輯 ACR</span><span class="sxs-lookup"><span data-stu-id="43a49-138">Edit an ACR</span></span>

<span data-ttu-id="43a49-139">使用 hello**存取控制記錄**刀鋒視窗內 hello**組態**您的裝置管理員服務在 Azure 入口網站 tooedit Acr hello > 一節。</span><span class="sxs-lookup"><span data-stu-id="43a49-139">You use hello **Access control records** blade within hello **Configuration** section of your Device Manager service in hello Azure portal tooedit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="43a49-140">請勿修改目前正在使用的 ACR。</span><span class="sxs-lookup"><span data-stu-id="43a49-140">You should not modify an ACR that is currently in use.</span></span> <span data-ttu-id="43a49-141">tooedit 與目前正在使用的磁碟區相關聯的 ACR，您應該先進行 hello 磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="43a49-141">tooedit an ACR associated with a volume that is currently in use, you should first take hello volume offline.</span></span>


<span data-ttu-id="43a49-142">執行下列步驟 tooedit ACR hello。</span><span class="sxs-lookup"><span data-stu-id="43a49-142">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-acr"></a><span data-ttu-id="43a49-143">tooedit ACR</span><span class="sxs-lookup"><span data-stu-id="43a49-143">tooedit an ACR</span></span>

1. <span data-ttu-id="43a49-144">在 hello 服務登陸頁面上，選取您的服務、 按兩下 hello 服務名稱，然後再內 hello**組態** 區段中，**存取控制記錄**。</span><span class="sxs-lookup"><span data-stu-id="43a49-144">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, **Access control records**.</span></span>
2. <span data-ttu-id="43a49-145">在 hello**存取控制記錄**刀鋒視窗中，從 hello 表格清單中的 hello 存取控制記錄，連按兩下您想 toomodify ACR hello。</span><span class="sxs-lookup"><span data-stu-id="43a49-145">In hello **Access control records** blade, from hello tabular listing of hello access control records, double-click hello ACR that you wish toomodify.</span></span>
3. <span data-ttu-id="43a49-146">在 hello**編輯存取控制記錄**刀鋒視窗中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="43a49-146">In hello **Edit access control records** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="43a49-147">提供 hello IQN hello ACR。</span><span class="sxs-lookup"><span data-stu-id="43a49-147">Supply hello IQN for hello ACR.</span></span>
   
    2. <span data-ttu-id="43a49-148">按一下**儲存**頂端的 hello 刀鋒視窗 toosave hello hello 修改 ACR。</span><span class="sxs-lookup"><span data-stu-id="43a49-148">Click **Save** at hello top of hello blade toosave hello modified ACR.</span></span> <span data-ttu-id="43a49-149">您會看到下列確認訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="43a49-149">You see hello following confirmation message:</span></span>
   
        ![編輯存取控制記錄](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a><span data-ttu-id="43a49-151">刪除存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="43a49-151">Delete an access control record</span></span>

<span data-ttu-id="43a49-152">使用 hello**組態**hello Azure 入口網站 toodelete Acr 中的頁面。</span><span class="sxs-lookup"><span data-stu-id="43a49-152">You use hello **Configuration** page in hello Azure portal toodelete ACRs.</span></span>

> [!NOTE]
> 
> * <span data-ttu-id="43a49-153">請勿刪除目前正在使用的 ACR。</span><span class="sxs-lookup"><span data-stu-id="43a49-153">You should not delete an ACR that is currently in use.</span></span> <span data-ttu-id="43a49-154">toodelete 與目前正在使用的磁碟區相關聯的 ACR，您應該先進行 hello 磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="43a49-154">toodelete an ACR associated with a volume that is currently in use, you should first take hello volume offline.</span></span>
> * <span data-ttu-id="43a49-155">當從磁碟區刪除 ACR，請確定該 hello 對應的主機未存取 hello 磁碟區，因為 hello 刪除可能會導致讀寫中斷。</span><span class="sxs-lookup"><span data-stu-id="43a49-155">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>


<span data-ttu-id="43a49-156">執行下列步驟 toodelete 存取控制記錄的 hello。</span><span class="sxs-lookup"><span data-stu-id="43a49-156">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="43a49-157">toodelete 存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="43a49-157">toodelete an access control record</span></span>

1. <span data-ttu-id="43a49-158">在 hello 服務登陸頁面上，選取您的服務、 按兩下 hello 服務名稱，然後再內 hello**組態** 區段中，**存取控制記錄**。</span><span class="sxs-lookup"><span data-stu-id="43a49-158">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, **Access control records**.</span></span>

2. <span data-ttu-id="43a49-159">在 hello**存取控制記錄**刀鋒視窗中，從 hello 表格清單中的 hello 存取控制記錄，連按兩下您想 toodelete ACR hello。</span><span class="sxs-lookup"><span data-stu-id="43a49-159">In hello **Access control records** blade, from hello tabular listing of hello access control records, double-click hello ACR that you wish toodelete.</span></span>

3. <span data-ttu-id="43a49-160">在 hello 編輯存取控制記錄刀鋒視窗中，按一下 **刪除**。</span><span class="sxs-lookup"><span data-stu-id="43a49-160">In hello Edit access control records blade, click **Delete**.</span></span>
   
    ![刪除 ACR](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. <span data-ttu-id="43a49-162">當提示確認，請按一下**刪除**toocontinue 與 hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="43a49-162">When prompted for confirmation, click **Delete** toocontinue with hello deletion.</span></span> <span data-ttu-id="43a49-163">hello 表格清單是更新的 tooreflect hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="43a49-163">hello tabular listing is updated tooreflect hello deletion.</span></span>
   
   ![警告訊息](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a><span data-ttu-id="43a49-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="43a49-165">Next steps</span></span>

* <span data-ttu-id="43a49-166">深入了解[新增和設定 ACR](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume)。</span><span class="sxs-lookup"><span data-stu-id="43a49-166">Learn more about [adding volumes and configuring ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>


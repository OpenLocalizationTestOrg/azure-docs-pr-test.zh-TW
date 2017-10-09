---
title: "在 StorSimple aaaManage 存取控制記錄 |Microsoft 文件"
description: "描述 toouse 存取控制記錄 (Acr) toodetermine 哪些主機可連接 tooa hello StorSimple 裝置上的磁碟區的方式。"
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
ms.openlocfilehash: a1e718c2679301b34221a233557a1eaae869a94f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a><span data-ttu-id="4f24b-103">使用 hello StorSimple Manager 服務 toomanage 存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="4f24b-103">Use hello StorSimple Manager service toomanage access control records</span></span>
## <a name="overview"></a><span data-ttu-id="4f24b-104">概觀</span><span class="sxs-lookup"><span data-stu-id="4f24b-104">Overview</span></span>
<span data-ttu-id="4f24b-105">存取控制記錄 (Acr) 可讓您 toospecify 哪些主機可連接 tooa hello StorSimple 裝置上的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="4f24b-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple device.</span></span> <span data-ttu-id="4f24b-106">Acr tooa 特定磁碟區，並設定包含 hello iSCSI hello 主機的限定名稱 （iqn 相關聯）。</span><span class="sxs-lookup"><span data-stu-id="4f24b-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="4f24b-107">當主機嘗試 tooconnect tooa 磁碟區時，hello 裝置會檢查的 hello 與 hello IQN 名稱，如果沒有符合項目，然後 hello 建立連接該磁碟區相關聯的 ACR。</span><span class="sxs-lookup"><span data-stu-id="4f24b-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="4f24b-108">hello 存取控制記錄區段 hello**設定**頁面會顯示以 hello 對應 iqn 相關聯的 hello 主機的所有 hello 存取控制記錄。</span><span class="sxs-lookup"><span data-stu-id="4f24b-108">hello access control records section on hello **Configure** page displays all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

<span data-ttu-id="4f24b-109">本教學課程將說明下列 ACR 相關的一般工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="4f24b-109">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="4f24b-110">加入存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="4f24b-110">Add an access control record</span></span> 
* <span data-ttu-id="4f24b-111">編輯存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="4f24b-111">Edit an access control record</span></span> 
* <span data-ttu-id="4f24b-112">刪除存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="4f24b-112">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="4f24b-113">指派的 ACR tooa 磁碟區時，小心，hello 存取磁碟區不同時由多個非叢集主機因為這可能會損毀 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="4f24b-113">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span> 
> * <span data-ttu-id="4f24b-114">當從磁碟區刪除 ACR，請確定該 hello 對應的主機未存取 hello 磁碟區，因為 hello 刪除可能會導致讀寫中斷。</span><span class="sxs-lookup"><span data-stu-id="4f24b-114">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="add-an-access-control-record"></a><span data-ttu-id="4f24b-115">加入存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="4f24b-115">Add an access control record</span></span>
<span data-ttu-id="4f24b-116">使用 hello StorSimple Manager 服務**設定**頁面 tooadd Acr。</span><span class="sxs-lookup"><span data-stu-id="4f24b-116">You use hello StorSimple Manager service **Configure** page tooadd ACRs.</span></span> <span data-ttu-id="4f24b-117">一般而言，您會讓一個 ACR 與一個磁碟區產生關聯。</span><span class="sxs-lookup"><span data-stu-id="4f24b-117">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="4f24b-118">執行下列步驟 tooadd ACR hello。</span><span class="sxs-lookup"><span data-stu-id="4f24b-118">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-access-control-record"></a><span data-ttu-id="4f24b-119">tooadd 存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="4f24b-119">tooadd an access control record</span></span>
1. <span data-ttu-id="4f24b-120">在 hello 服務登陸頁面上，選取您的服務、 按兩下 hello 的服務名稱，然後按一下 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4f24b-120">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="4f24b-121">在表格式底下列出的 hello**存取控制記錄**、 提供**名稱**acr。</span><span class="sxs-lookup"><span data-stu-id="4f24b-121">In hello tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="4f24b-122">提供 hello 下 Windows 主機的 IQN 名稱**iSCSI 啟動器名稱**。</span><span class="sxs-lookup"><span data-stu-id="4f24b-122">Provide hello IQN name of your Windows host under **iSCSI Initiator Name**.</span></span> <span data-ttu-id="4f24b-123">tooget hello 您 Windows Server 主機的 IQN，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="4f24b-123">tooget hello IQN of your Windows Server host, do hello following:</span></span>
   
   * <span data-ttu-id="4f24b-124">在 Windows 主機上啟動 hello Microsoft iSCSI 啟動器。</span><span class="sxs-lookup"><span data-stu-id="4f24b-124">Start hello Microsoft iSCSI initiator on your Windows host.</span></span>
   * <span data-ttu-id="4f24b-125">在 hello **iSCSI 啟動器屬性**視窗的 hello**組態**索引標籤上，選取並複製 hello 字串 hello 從**啟動器名稱**欄位。</span><span class="sxs-lookup"><span data-stu-id="4f24b-125">In hello **iSCSI Initiator Properties** window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
   * <span data-ttu-id="4f24b-126">貼上此字串在 hello **iSCSI 啟動器名稱**hello Azure 傳統入口網站中的 hello Acr 資料表上的欄位。</span><span class="sxs-lookup"><span data-stu-id="4f24b-126">Paste this string in hello **iSCSI Initiator Name** field on hello ACRs table in hello Azure classic portal.</span></span>
4. <span data-ttu-id="4f24b-127">按一下**儲存**toosave hello 新建立的 ACR。</span><span class="sxs-lookup"><span data-stu-id="4f24b-127">Click **Save** toosave hello newly created ACR.</span></span> <span data-ttu-id="4f24b-128">hello 表格式清單將會更新的 tooreflect 此新增功能。</span><span class="sxs-lookup"><span data-stu-id="4f24b-128">hello tabular listing will be updated tooreflect this addition.</span></span>

## <a name="edit-an-access-control-record"></a><span data-ttu-id="4f24b-129">編輯存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="4f24b-129">Edit an access control record</span></span>
<span data-ttu-id="4f24b-130">使用 hello**設定**hello Azure 傳統入口網站 tooedit Acr 中的頁面。</span><span class="sxs-lookup"><span data-stu-id="4f24b-130">You use hello **Configure** page in hello Azure classic portal tooedit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="4f24b-131">您只能修改目前未在使用中的 ACR。</span><span class="sxs-lookup"><span data-stu-id="4f24b-131">You can modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="4f24b-132">tooedit 與目前正在使用的磁碟區相關聯的 ACR，您必須先進行 hello 磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="4f24b-132">tooedit an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>
> 
> 

<span data-ttu-id="4f24b-133">執行下列步驟 tooedit ACR hello。</span><span class="sxs-lookup"><span data-stu-id="4f24b-133">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-access-control-record"></a><span data-ttu-id="4f24b-134">tooedit 存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="4f24b-134">tooedit an access control record</span></span>
1. <span data-ttu-id="4f24b-135">在 hello 服務登陸頁面上，選取您的服務、 按兩下 hello 的服務名稱，然後按一下 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4f24b-135">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="4f24b-136">在 hello 表格清單中的 hello 存取控制記錄，請將滑鼠停留在 hello 想 toomodify 的 ACR。</span><span class="sxs-lookup"><span data-stu-id="4f24b-136">In hello tabular listing of hello access control records, hover over hello ACR that you wish toomodify.</span></span>
3. <span data-ttu-id="4f24b-137">Hello ACR 提供新的名稱和/或 IQN。</span><span class="sxs-lookup"><span data-stu-id="4f24b-137">Supply a new name and/or IQN for hello ACR.</span></span>
4. <span data-ttu-id="4f24b-138">按一下**儲存**toosave hello 修改 ACR。</span><span class="sxs-lookup"><span data-stu-id="4f24b-138">Click **Save** toosave hello modified ACR.</span></span> <span data-ttu-id="4f24b-139">hello 表格式清單將會更新的 tooreflect 這項變更。</span><span class="sxs-lookup"><span data-stu-id="4f24b-139">hello tabular listing will be updated tooreflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="4f24b-140">刪除存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="4f24b-140">Delete an access control record</span></span>
<span data-ttu-id="4f24b-141">使用 hello**設定**hello Azure 傳統入口網站 toodelete Acr 中的頁面。</span><span class="sxs-lookup"><span data-stu-id="4f24b-141">You use hello **Configure** page in hello Azure classic portal toodelete ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="4f24b-142">您只能刪除目前未在使用中的 ACR。</span><span class="sxs-lookup"><span data-stu-id="4f24b-142">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="4f24b-143">toodelete 與目前正在使用的磁碟區相關聯的 ACR，您必須先進行 hello 磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="4f24b-143">toodelete an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>
> 
> 

<span data-ttu-id="4f24b-144">執行下列步驟 toodelete 存取控制記錄的 hello。</span><span class="sxs-lookup"><span data-stu-id="4f24b-144">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="4f24b-145">toodelete 存取控制記錄</span><span class="sxs-lookup"><span data-stu-id="4f24b-145">toodelete an access control record</span></span>
1. <span data-ttu-id="4f24b-146">在 hello 服務登陸頁面上，選取您的服務、 按兩下 hello 的服務名稱，然後按一下 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4f24b-146">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="4f24b-147">在 hello 表格清單中的 hello 存取控制記錄 (Acr)，請將滑鼠停留在 hello 想 toodelete 的 ACR。</span><span class="sxs-lookup"><span data-stu-id="4f24b-147">In hello tabular listing of hello access control records (ACRs), hover over hello ACR that you wish toodelete.</span></span>
3. <span data-ttu-id="4f24b-148">刪除圖示 (**x**) 會出現在 hello 極端右側的欄 hello 您選取的 ACR。</span><span class="sxs-lookup"><span data-stu-id="4f24b-148">A delete icon (**x**) will appear in hello extreme right column for hello ACR that you select.</span></span> <span data-ttu-id="4f24b-149">按一下 hello **x**圖示 toodelete hello ACR。</span><span class="sxs-lookup"><span data-stu-id="4f24b-149">Click hello **x** icon toodelete hello ACR.</span></span>
4. <span data-ttu-id="4f24b-150">當提示確認，請按一下**是**toocontinue 與 hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="4f24b-150">When prompted for confirmation, click **YES** toocontinue with hello deletion.</span></span> <span data-ttu-id="4f24b-151">hello 表格式清單將會更新的 tooreflect hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="4f24b-151">hello tabular listing will be updated tooreflect hello deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f24b-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4f24b-152">Next steps</span></span>
* <span data-ttu-id="4f24b-153">深入了解 [管理 StorSimple 磁碟區](storsimple-manage-volumes.md)。</span><span class="sxs-lookup"><span data-stu-id="4f24b-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="4f24b-154">深入了解[使用您的 StorSimple 裝置 hello StorSimple Manager 服務 tooadminister](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="4f24b-154">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>


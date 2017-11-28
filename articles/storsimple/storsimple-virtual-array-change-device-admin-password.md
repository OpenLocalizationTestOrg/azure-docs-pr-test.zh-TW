---
title: "aaaChange StorSimple Virtual Array 裝置系統管理員密碼 |Microsoft 文件"
description: "描述如何 toouse 或是 hello Azure 入口網站或 StorSimple Virtual Array web UI toochange hello 裝置系統管理員密碼。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 11490814-d9fd-4dc7-9c3b-55dd2c23eaf1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 531b395df7aeade0a909360797c6b0f0abd9fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a><span data-ttu-id="28842-103">變更 hello StorSimple Virtual Array 裝置系統管理員密碼透過 StorSimple 裝置管理員</span><span class="sxs-lookup"><span data-stu-id="28842-103">Change hello StorSimple Virtual Array device administrator password via StorSimple Device Manager</span></span>

## <a name="overview"></a><span data-ttu-id="28842-104">概觀</span><span class="sxs-lookup"><span data-stu-id="28842-104">Overview</span></span>

<span data-ttu-id="28842-105">當您使用 hello Windows PowerShell 介面 tooaccess hello StorSimple Virtual Array，您會需要的 tooenter 裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="28842-105">When you use hello Windows PowerShell interface tooaccess hello StorSimple Virtual Array, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="28842-106">當 hello StorSimple 裝置就會先佈建並啟動時，hello 預設密碼是*Password1*。</span><span class="sxs-lookup"><span data-stu-id="28842-106">When hello StorSimple device is first provisioned and started, hello default password is *Password1*.</span></span> <span data-ttu-id="28842-107">Hello 資料的安全性，如 hello 預設密碼到期 hello 登入的第一次，而且您會需要的 toochange 這個密碼。</span><span class="sxs-lookup"><span data-stu-id="28842-107">For hello security of your data, hello default password expires hello first time that you sign in and you are required toochange this password.</span></span>

<span data-ttu-id="28842-108">您也可以在任何時間之後 hello 裝置部署在生產環境使用任一 hello 本機 web UI 或 hello Azure 入口網站 toochange hello 裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="28842-108">You can also use either hello local web UI or hello Azure portal toochange hello device administrator password at any time after hello device is deployed in your production environment.</span></span> <span data-ttu-id="28842-109">本文章說明上述各程序。</span><span class="sxs-lookup"><span data-stu-id="28842-109">Each of these procedures is described in this article.</span></span>

 ![裝置刀鋒視窗](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-hello-azure-portal-toochange-hello-password"></a><span data-ttu-id="28842-111">使用 hello Azure 入口網站 toochange hello 密碼</span><span class="sxs-lookup"><span data-stu-id="28842-111">Use hello Azure portal toochange hello password</span></span>

<span data-ttu-id="28842-112">執行下列步驟 toochange hello 裝置系統管理員密碼透過 hello Azure 入口網站的 hello。</span><span class="sxs-lookup"><span data-stu-id="28842-112">Perform hello following steps toochange hello device administrator password through hello Azure portal.</span></span>

#### <a name="toochange-hello-device-administrator-password-via-hello-azure-portal"></a><span data-ttu-id="28842-113">透過 Azure 入口網站 hello toochange hello 裝置系統管理員密碼</span><span class="sxs-lookup"><span data-stu-id="28842-113">toochange hello device administrator password via hello Azure portal</span></span>

1. <span data-ttu-id="28842-114">在 hello 服務登陸頁面上，選取您的服務、 按兩下 hello 服務名稱，然後再內 hello**管理**區段中，按一下**裝置**。</span><span class="sxs-lookup"><span data-stu-id="28842-114">On hello service landing page, select your service, double-click hello service name, and then within hello **Management** section, click **Devices**.</span></span> <span data-ttu-id="28842-115">這會開啟 hello**裝置**刀鋒視窗，其中列出所有 StorSimple Virtual Array 裝置。</span><span class="sxs-lookup"><span data-stu-id="28842-115">This opens hello **Devices** blade that lists all your StorSimple Virtual Array devices.</span></span>

2. <span data-ttu-id="28842-116">在 hello**裝置**刀鋒視窗中，按兩下 hello 裝置需要密碼的變更。</span><span class="sxs-lookup"><span data-stu-id="28842-116">In hello **Devices** blade, double-click hello device that requires a change of password.</span></span>

3. <span data-ttu-id="28842-117">在 hello**設定**刀鋒視窗，您的裝置，請按一下**安全性**。</span><span class="sxs-lookup"><span data-stu-id="28842-117">In hello **Settings** blade for your device, click **Security**.</span></span>

4. <span data-ttu-id="28842-118">在 hello**安全性設定**刀鋒視窗中，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="28842-118">In hello **Security Settings** blade, do hello following:</span></span>
   
   1. <span data-ttu-id="28842-119">捲動 toohello**裝置系統管理員密碼**> 一節。</span><span class="sxs-lookup"><span data-stu-id="28842-119">Scroll down toohello **Device Administrator Password** section.</span></span> <span data-ttu-id="28842-120">提供系統管理員密碼包含 8 too15 個字元。</span><span class="sxs-lookup"><span data-stu-id="28842-120">Provide an administrator password that contains from 8 too15 characters.</span></span>
   2. <span data-ttu-id="28842-121">確認 hello 的密碼。</span><span class="sxs-lookup"><span data-stu-id="28842-121">Confirm hello password.</span></span>
   3. <span data-ttu-id="28842-122">按一下**儲存**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="28842-122">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="28842-123">現在更新 hello 裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="28842-123">hello device administrator password is now updated.</span></span> <span data-ttu-id="28842-124">您可以在本機上使用這個修改過的密碼 tooaccess hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="28842-124">You can use this modified password tooaccess hello device locally.</span></span>

![安全性設定刀鋒視窗](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-hello-local-web-ui-toochange-hello-password"></a><span data-ttu-id="28842-126">使用 hello 本機 web UI toochange hello 密碼</span><span class="sxs-lookup"><span data-stu-id="28842-126">Use hello local web UI toochange hello password</span></span>

<span data-ttu-id="28842-127">執行下列步驟 toochange hello 裝置系統管理員密碼透過 hello 本機 web UI 的 hello。</span><span class="sxs-lookup"><span data-stu-id="28842-127">Perform hello following steps toochange hello device administrator password through hello local web UI.</span></span>

#### <a name="toochange-hello-device-administrator-password-via-hello-local-web-ui"></a><span data-ttu-id="28842-128">透過 hello 本機 web UI toochange hello 裝置系統管理員密碼</span><span class="sxs-lookup"><span data-stu-id="28842-128">toochange hello device administrator password via hello local web UI</span></span>

1. <span data-ttu-id="28842-129">在 hello 本機 web UI，按一下 **維護** > **密碼變更**為您的裝置。</span><span class="sxs-lookup"><span data-stu-id="28842-129">In hello local web UI, click **Maintenance** > **Password change** for your device.</span></span>
   
    ![變更 password1](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. <span data-ttu-id="28842-131">輸入 hello**目前密碼**。</span><span class="sxs-lookup"><span data-stu-id="28842-131">Enter hello **Current password**.</span></span>
3. <span data-ttu-id="28842-132">提供 **新密碼**。</span><span class="sxs-lookup"><span data-stu-id="28842-132">Provide a **New Password**.</span></span> <span data-ttu-id="28842-133">hello 密碼必須至少 8 個字元。</span><span class="sxs-lookup"><span data-stu-id="28842-133">hello password must be at least 8 characters long.</span></span> <span data-ttu-id="28842-134">它必須包含 3，4 個 hello 下列： 大寫字母、 小寫、 數字及特殊字元。</span><span class="sxs-lookup"><span data-stu-id="28842-134">It must contain 3 of 4 of hello following: uppercase, lowercase, numeric, and special characters.</span></span>
   
    <span data-ttu-id="28842-135">請注意，您的密碼不能 hello 與 hello 最後 24 個密碼相同。</span><span class="sxs-lookup"><span data-stu-id="28842-135">Note that your password cannot be hello same as hello last 24 passwords.</span></span>
4. <span data-ttu-id="28842-136">重新輸入 hello 密碼 tooconfirm 它。</span><span class="sxs-lookup"><span data-stu-id="28842-136">Reenter hello password tooconfirm it.</span></span>
   
    ![變更 password2](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. <span data-ttu-id="28842-138">在 hello hello 頁面底部，按一下**套用**。</span><span class="sxs-lookup"><span data-stu-id="28842-138">At hello bottom of hello page, click **Apply**.</span></span> <span data-ttu-id="28842-139">hello 新密碼會立即套用。</span><span class="sxs-lookup"><span data-stu-id="28842-139">hello new password is now applied.</span></span> <span data-ttu-id="28842-140">如果不成功 hello 密碼變更時，您會看見 hello 下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="28842-140">If hello password change is not successful, you see hello following error:</span></span>
   
    ![密碼錯誤](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    <span data-ttu-id="28842-142">已成功更新 hello 密碼之後，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="28842-142">After hello password is successfully updated, you are notified.</span></span> <span data-ttu-id="28842-143">您接著可以在本機使用這個修改過的密碼 tooaccess hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="28842-143">You can then use this modified password tooaccess hello device locally.</span></span>


## <a name="next-steps"></a><span data-ttu-id="28842-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="28842-144">Next steps</span></span>
<span data-ttu-id="28842-145">了解如何太[管理您的 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="28842-145">Learn how too[administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>


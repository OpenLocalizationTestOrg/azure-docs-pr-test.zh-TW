---
title: "變更 StorSimple Virtual Array 裝置系統管理員密碼 | Microsoft Docs"
description: "說明如何使用 Azure 入口網站或 StorSimple Virtual Array Web UI 來變更裝置系統管理員密碼。"
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
ms.openlocfilehash: 260a23003d705e6598da8c51bb5a96f2539a0014
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a><span data-ttu-id="75015-103">透過 StorSimple 裝置管理員變更 StorSimple Virtual Array 裝置系統管理員密碼</span><span class="sxs-lookup"><span data-stu-id="75015-103">Change the StorSimple Virtual Array device administrator password via StorSimple Device Manager</span></span>

## <a name="overview"></a><span data-ttu-id="75015-104">概觀</span><span class="sxs-lookup"><span data-stu-id="75015-104">Overview</span></span>

<span data-ttu-id="75015-105">當您使用 Windows PowerShell 介面來存取 StorSimple Virtual Array 時，您需要輸入裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="75015-105">When you use the Windows PowerShell interface to access the StorSimple Virtual Array, you are required to enter a device administrator password.</span></span> <span data-ttu-id="75015-106">StorSimple 裝置第一次佈建並啟動時，預設的密碼是 *Password1*。</span><span class="sxs-lookup"><span data-stu-id="75015-106">When the StorSimple device is first provisioned and started, the default password is *Password1*.</span></span> <span data-ttu-id="75015-107">為了資料的安全性，您第一次登入時預設密碼便會過期，且系統會要求您變更密碼。</span><span class="sxs-lookup"><span data-stu-id="75015-107">For the security of your data, the default password expires the first time that you sign in and you are required to change this password.</span></span>

<span data-ttu-id="75015-108">裝置部署到生產環境之後，您隨時可以使用本機 Web UI 或 Azure 入口網站變更裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="75015-108">You can also use either the local web UI or the Azure portal to change the device administrator password at any time after the device is deployed in your production environment.</span></span> <span data-ttu-id="75015-109">本文章說明上述各程序。</span><span class="sxs-lookup"><span data-stu-id="75015-109">Each of these procedures is described in this article.</span></span>

 ![裝置刀鋒視窗](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-the-azure-portal-to-change-the-password"></a><span data-ttu-id="75015-111">使用 Azure 入口網站變更密碼</span><span class="sxs-lookup"><span data-stu-id="75015-111">Use the Azure portal to change the password</span></span>

<span data-ttu-id="75015-112">執行下列步驟來透過 Azure 入口網站變更裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="75015-112">Perform the following steps to change the device administrator password through the Azure portal.</span></span>

#### <a name="to-change-the-device-administrator-password-via-the-azure-portal"></a><span data-ttu-id="75015-113">透過 Azure 入口網站變更裝置系統管理員密碼</span><span class="sxs-lookup"><span data-stu-id="75015-113">To change the device administrator password via the Azure portal</span></span>

1. <span data-ttu-id="75015-114">在服務登陸頁面上，選取您的服務，按兩下服務名稱，然後按一下在 [管理] 區段內按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="75015-114">On the service landing page, select your service, double-click the service name, and then within the **Management** section, click **Devices**.</span></span> <span data-ttu-id="75015-115">這會開啟 [裝置] 刀鋒視窗來列出您的所有 StorSimple Virtual Array 裝置。</span><span class="sxs-lookup"><span data-stu-id="75015-115">This opens the **Devices** blade that lists all your StorSimple Virtual Array devices.</span></span>

2. <span data-ttu-id="75015-116">在 [裝置] 刀鋒視窗中，按兩下需要變更密碼的裝置。</span><span class="sxs-lookup"><span data-stu-id="75015-116">In the **Devices** blade, double-click the device that requires a change of password.</span></span>

3. <span data-ttu-id="75015-117">在裝置的 [設定] 刀鋒視窗中，按一下 [安全性]。</span><span class="sxs-lookup"><span data-stu-id="75015-117">In the **Settings** blade for your device, click **Security**.</span></span>

4. <span data-ttu-id="75015-118">在 [安全性設定] 刀鋒視窗中，執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="75015-118">In the **Security Settings** blade, do the following:</span></span>
   
   1. <span data-ttu-id="75015-119">向下捲動至 [ **裝置系統管理員密碼** ] 區段。</span><span class="sxs-lookup"><span data-stu-id="75015-119">Scroll down to the **Device Administrator Password** section.</span></span> <span data-ttu-id="75015-120">提供含有 8 到 15 個字元的系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="75015-120">Provide an administrator password that contains from 8 to 15 characters.</span></span>
   2. <span data-ttu-id="75015-121">確認密碼。</span><span class="sxs-lookup"><span data-stu-id="75015-121">Confirm the password.</span></span>
   3. <span data-ttu-id="75015-122">按一下刀鋒視窗頂端的 [儲存]  。</span><span class="sxs-lookup"><span data-stu-id="75015-122">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="75015-123">現在已變更裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="75015-123">The device administrator password is now updated.</span></span> <span data-ttu-id="75015-124">您可以使用修改的密碼在本機存取該裝置。</span><span class="sxs-lookup"><span data-stu-id="75015-124">You can use this modified password to access the device locally.</span></span>

![安全性設定刀鋒視窗](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-the-local-web-ui-to-change-the-password"></a><span data-ttu-id="75015-126">使用本機 Web UI 來變更密碼</span><span class="sxs-lookup"><span data-stu-id="75015-126">Use the local web UI to change the password</span></span>

<span data-ttu-id="75015-127">執行下列步驟來透過本機 Web UI 變更裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="75015-127">Perform the following steps to change the device administrator password through the local web UI.</span></span>

#### <a name="to-change-the-device-administrator-password-via-the-local-web-ui"></a><span data-ttu-id="75015-128">透過本機 Web UI 變更裝置系統管理員密碼</span><span class="sxs-lookup"><span data-stu-id="75015-128">To change the device administrator password via the local web UI</span></span>

1. <span data-ttu-id="75015-129">在本機 Web UI 中，對您的裝置按一下 [維護]  >  [變更密碼]。</span><span class="sxs-lookup"><span data-stu-id="75015-129">In the local web UI, click **Maintenance** > **Password change** for your device.</span></span>
   
    ![變更 password1](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. <span data-ttu-id="75015-131">輸入 **目前的密碼**。</span><span class="sxs-lookup"><span data-stu-id="75015-131">Enter the **Current password**.</span></span>
3. <span data-ttu-id="75015-132">提供 **新密碼**。</span><span class="sxs-lookup"><span data-stu-id="75015-132">Provide a **New Password**.</span></span> <span data-ttu-id="75015-133">密碼長度必須至少為 8 個字元。</span><span class="sxs-lookup"><span data-stu-id="75015-133">The password must be at least 8 characters long.</span></span> <span data-ttu-id="75015-134">密碼必須包含下列 4 項的其中 3 項：大寫、小寫、數字和特殊字元。</span><span class="sxs-lookup"><span data-stu-id="75015-134">It must contain 3 of 4 of the following: uppercase, lowercase, numeric, and special characters.</span></span>
   
    <span data-ttu-id="75015-135">請注意，您的密碼不能與最近的 24 個密碼相同。</span><span class="sxs-lookup"><span data-stu-id="75015-135">Note that your password cannot be the same as the last 24 passwords.</span></span>
4. <span data-ttu-id="75015-136">請重新輸入密碼來加以確認。</span><span class="sxs-lookup"><span data-stu-id="75015-136">Reenter the password to confirm it.</span></span>
   
    ![變更 password2](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. <span data-ttu-id="75015-138">在頁面底部，按一下 [套用] 。</span><span class="sxs-lookup"><span data-stu-id="75015-138">At the bottom of the page, click **Apply**.</span></span> <span data-ttu-id="75015-139">現在已套用新的密碼。</span><span class="sxs-lookup"><span data-stu-id="75015-139">The new password is now applied.</span></span> <span data-ttu-id="75015-140">如果變更密碼未成功，您會看到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="75015-140">If the password change is not successful, you see the following error:</span></span>
   
    ![密碼錯誤](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    <span data-ttu-id="75015-142">成功更新密碼之後會通知您。</span><span class="sxs-lookup"><span data-stu-id="75015-142">After the password is successfully updated, you are notified.</span></span> <span data-ttu-id="75015-143">您即可使用修改的密碼在本機存取該裝置。</span><span class="sxs-lookup"><span data-stu-id="75015-143">You can then use this modified password to access the device locally.</span></span>


## <a name="next-steps"></a><span data-ttu-id="75015-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="75015-144">Next steps</span></span>
<span data-ttu-id="75015-145">了解如何 [管理 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="75015-145">Learn how to [administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>


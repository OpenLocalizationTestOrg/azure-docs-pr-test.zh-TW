---
title: "變更 StorSimple 密碼 | Microsoft Docs"
description: "描述如何使用 StorSimple 裝置管理員服務變更 StorSimple Snapshot Manager 與裝置系統管理員密碼。"
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
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 7762f8499c67672f0a2ffed99e98baea4c940fa0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-change-your-storsimple-passwords"></a><span data-ttu-id="13993-103">使用 StorSimple 裝置管理員服務變更您的 StorSimple 密碼</span><span class="sxs-lookup"><span data-stu-id="13993-103">Use the StorSimple Device Manager service to change your StorSimple passwords</span></span>

## <a name="overview"></a><span data-ttu-id="13993-104">概觀</span><span class="sxs-lookup"><span data-stu-id="13993-104">Overview</span></span>
<span data-ttu-id="13993-105">Azure 入口網站的 [裝置設定] 選項包含所有裝置參數，可讓您重新設定 StorSimple 裝置管理員服務所管理的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="13993-105">The Azure portal **Device settings** option contains all the device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="13993-106">本教學課程說明如何使用 [裝置設定] 下的 [安全性] 選項，變更您的裝置系統管理員或 StorSimple Snapshot Manager 密碼。</span><span class="sxs-lookup"><span data-stu-id="13993-106">This tutorial explains how you can use the **Security** option under **Device settings** to change your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-the-device-administrator-password"></a><span data-ttu-id="13993-107">變更裝置系統管理員密碼</span><span class="sxs-lookup"><span data-stu-id="13993-107">Change the device administrator password</span></span>
<span data-ttu-id="13993-108">當您使用 Windows PowerShell 介面來存取 StorSimple 裝置時，需要輸入裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="13993-108">When you use Windows PowerShell interface to access the StorSimple device, you are required to enter a device administrator password.</span></span> <span data-ttu-id="13993-109">向服務註冊第一個 StorSimple 裝置時，此介面的預設密碼為 *Password1*。</span><span class="sxs-lookup"><span data-stu-id="13993-109">When the first StorSimple device is registered with a service, the default password for this interface is *Password1*.</span></span> <span data-ttu-id="13993-110">為了確保資料的安全性，您必須在註冊程序結束時變更此密碼。</span><span class="sxs-lookup"><span data-stu-id="13993-110">For the security of your data, you are required to change this password at the end of the registration process.</span></span> <span data-ttu-id="13993-111">若未變更此密碼，您就無法結束註冊程序。</span><span class="sxs-lookup"><span data-stu-id="13993-111">You cannot exit from the registration process without changing this password.</span></span> <span data-ttu-id="13993-112">如需詳細資訊，請參閱 [步驟 3：透過 Windows PowerShell for StorSimple 設定和註冊裝置](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)。</span><span class="sxs-lookup"><span data-stu-id="13993-112">For more information, see [Step 3: Configure and register the device through Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="13993-113">之後可以透過 Azure 入口網站，變更在註冊期間先透過 Windows PowerShell 介面設定的密碼。</span><span class="sxs-lookup"><span data-stu-id="13993-113">The password that was first set through the Windows PowerShell interface during registration can be changed later via the Azure portal.</span></span> <span data-ttu-id="13993-114">執行下列步驟來變更裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="13993-114">Perform the following steps to change the device administrator password.</span></span>

#### <a name="to-change-the-device-administrator-password"></a><span data-ttu-id="13993-115">若要變更裝置系統管理員密碼：</span><span class="sxs-lookup"><span data-stu-id="13993-115">To change the device administrator password</span></span>
1. <span data-ttu-id="13993-116">移至 StorSimple 裝置管理員服務，然後按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="13993-116">Go to your StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="13993-117">從裝置的表格式清單中，選取並按一下您想要變更其密碼的裝置。</span><span class="sxs-lookup"><span data-stu-id="13993-117">From the tabular listing of devices, select and click the device whose password you intend to change.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="13993-118">在 [設定] 刀鋒視窗中，移至 [裝置設定] > [安全性]。</span><span class="sxs-lookup"><span data-stu-id="13993-118">In the **Settings** blade, go to **Device settings > Security**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="13993-119">在 [安全性設定] 刀鋒視窗中，按一下 [密碼]，以變更裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="13993-119">In the **Security settings** blade, click **Password** to change the device administrator password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. <span data-ttu-id="13993-120">在 [密碼] 刀鋒視窗中，提供含有 8 到 15 個字元的系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="13993-120">In the **Password** blade, provide an administrator password that contains from 8 to 15 characters.</span></span> <span data-ttu-id="13993-121">密碼必須是 3 個以上大寫、小寫、數字和特殊字元的組合。</span><span class="sxs-lookup"><span data-stu-id="13993-121">The password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="13993-122">確認密碼。</span><span class="sxs-lookup"><span data-stu-id="13993-122">Confirm the password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. <span data-ttu-id="13993-123">按一下 [儲存]，當系統提示您進行確認時，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="13993-123">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="13993-124">現在應該已更新裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="13993-124">The device administrator password should now be updated.</span></span> <span data-ttu-id="13993-125">您可以使用此修改過的密碼來存取 Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="13993-125">You can use this modified password to access the Windows PowerShell interface.</span></span>

## <a name="set-the-storsimple-snapshot-manager-password"></a><span data-ttu-id="13993-126">設定 StorSimple Snapshot Manager 密碼</span><span class="sxs-lookup"><span data-stu-id="13993-126">Set the StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="13993-127">StorSimple Snapshot Manager 軟體位於您的 Windows 主機上，而且可讓系統管理員以本機和雲端快照的形式管理 StorSimple 裝置的備份。</span><span class="sxs-lookup"><span data-stu-id="13993-127">StorSimple Snapshot Manager software resides on your Windows host and allows administrators to manage backups of your StorSimple device in the form of local and cloud snapshots.</span></span>

<span data-ttu-id="13993-128">當您在 StorSimple Snapshot Manager 中設定裝置時，系統將提示您提供裝置 IP 位址和密碼來驗證您的儲存裝置。</span><span class="sxs-lookup"><span data-stu-id="13993-128">When configuring a device in StorSimple Snapshot Manager, you will be prompted to provide the device IP address and password to authenticate your storage device.</span></span>

<span data-ttu-id="13993-129">您可以透過 Azure 入口網站設定或變更 StorSimple Snapshot Manager 密碼。</span><span class="sxs-lookup"><span data-stu-id="13993-129">You can set or change the password for StorSimple Snapshot Manager via the Azure portal.</span></span> <span data-ttu-id="13993-130">執行下列步驟來設定或變更 StorSimple Snapshot Manager 密碼。</span><span class="sxs-lookup"><span data-stu-id="13993-130">Perform the following steps to set or change the StorSimple Snapshot Manager password.</span></span>

#### <a name="to-set-the-storsimple-snapshot-manager-password"></a><span data-ttu-id="13993-131">若要設定 StorSimple Snapshot Manager 密碼</span><span class="sxs-lookup"><span data-stu-id="13993-131">To set the StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="13993-132">移至 StorSimple 裝置管理員服務，然後按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="13993-132">Go to your StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="13993-133">從裝置的表格式清單中，選取並按一下您想要設定或變更其 StorSimple Snapshot Manager 密碼的裝置。</span><span class="sxs-lookup"><span data-stu-id="13993-133">From the tabular listing of devices, select and click the device whose StorSimple Snapshot Manager password you intend to set or change.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="13993-134">在 [設定] 刀鋒視窗中，移至 [裝置設定] > [安全性]。</span><span class="sxs-lookup"><span data-stu-id="13993-134">In the **Settings** blade, go to **Device settings > Security**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="13993-135">在 [安全性設定] 刀鋒視窗中，按一下 [密碼]，以設定或變更 StorSimple Snapshot Manager 密碼。</span><span class="sxs-lookup"><span data-stu-id="13993-135">In the **Security settings** blade, click **Password** to set or change the StorSimple Snapshot Manager password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. <span data-ttu-id="13993-136">在 [密碼] 刀鋒視窗中，輸入 14 或 15 個字元的密碼。</span><span class="sxs-lookup"><span data-stu-id="13993-136">In the **Password** blade, enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="13993-137">請確定密碼包含 3 個以上大寫、小寫、數字和特殊字元的組合。</span><span class="sxs-lookup"><span data-stu-id="13993-137">Make sure that the password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="13993-138">確認密碼。</span><span class="sxs-lookup"><span data-stu-id="13993-138">Confirm the password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. <span data-ttu-id="13993-139">按一下 [儲存]，當系統提示您進行確認時，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="13993-139">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="13993-140">StorSimple Snapshot Manager 密碼現在應該已更新。</span><span class="sxs-lookup"><span data-stu-id="13993-140">The StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13993-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13993-141">Next steps</span></span>
* <span data-ttu-id="13993-142">深入了解 [StorSimple 安全性](storsimple-8000-security.md)。</span><span class="sxs-lookup"><span data-stu-id="13993-142">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="13993-143">[深入了解修改您的裝置組態](storsimple-8000-modify-device-config.md)。</span><span class="sxs-lookup"><span data-stu-id="13993-143">Learn more about [modifying your device configuration](storsimple-8000-modify-device-config.md).</span></span>
* <span data-ttu-id="13993-144">深入了解[使用 StorSimple 裝置管理員服務管理 StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="13993-144">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>


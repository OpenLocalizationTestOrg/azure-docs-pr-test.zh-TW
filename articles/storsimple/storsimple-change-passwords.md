---
title: "透過 StorSimple 裝置管理員變更密碼 | Microsoft Docs"
description: "描述如何使用 StorSimple Manager 服務變更 StorSimple Snapshot Manager 與裝置系統管理員密碼。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: f178509c-f4e1-48a8-90b2-d4ad050eeb30
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d890b59595628ca3eeff1df258847c2bb54d29ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-change-your-storsimple-passwords"></a><span data-ttu-id="412c4-103">使用 StorSimple Manager 服務變更 StorSimple 密碼</span><span class="sxs-lookup"><span data-stu-id="412c4-103">Use the StorSimple Manager service to change your StorSimple passwords</span></span>
## <a name="overview"></a><span data-ttu-id="412c4-104">Overview</span><span class="sxs-lookup"><span data-stu-id="412c4-104">Overview</span></span>
<span data-ttu-id="412c4-105">Azure 傳統入口網站 [設定]  頁面包含所有裝置參數，可讓您重新設定 StorSimple Manager 服務所管理的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="412c4-105">The Azure classic portal **Configure** page contains all the device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Manager service.</span></span> <span data-ttu-id="412c4-106">本教學課程說明如何使用 [設定]  頁面，變更您的裝置系統管理員或 StorSimple Snapshot Manager 密碼。</span><span class="sxs-lookup"><span data-stu-id="412c4-106">This tutorial explains how you can use the **Configure** page to change your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-the-device-administrator-password"></a><span data-ttu-id="412c4-107">變更裝置系統管理員密碼</span><span class="sxs-lookup"><span data-stu-id="412c4-107">Change the device administrator password</span></span>
<span data-ttu-id="412c4-108">當您使用 Windows PowerShell 介面來存取 StorSimple 裝置時，需要輸入裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="412c4-108">When you use Windows PowerShell interface to access the StorSimple device, you are required to enter a device administrator password.</span></span> <span data-ttu-id="412c4-109">向服務註冊第一個 StorSimple 裝置時，此介面的預設密碼為 *Password1*。</span><span class="sxs-lookup"><span data-stu-id="412c4-109">When the first StorSimple device is registered with a service, the default password for this interface is *Password1*.</span></span> <span data-ttu-id="412c4-110">為了確保資料的安全性，您必須在註冊程序結束時變更此密碼。</span><span class="sxs-lookup"><span data-stu-id="412c4-110">For the security of your data, you are required to change this password at the end of the registration process.</span></span> <span data-ttu-id="412c4-111">若未變更此密碼，您就無法結束註冊程序。</span><span class="sxs-lookup"><span data-stu-id="412c4-111">You cannot exit from the registration process without changing this password.</span></span> <span data-ttu-id="412c4-112">如需詳細資訊，請參閱 [步驟 3：透過 Windows PowerShell for StorSimple 設定和註冊裝置](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)。</span><span class="sxs-lookup"><span data-stu-id="412c4-112">For more information, see [Step 3: Configure and register the device through Windows PowerShell for StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="412c4-113">然後可以透過 Azure 傳統入口網站，變更在註冊期間先透過 Windows PowerShell 介面設定的密碼。</span><span class="sxs-lookup"><span data-stu-id="412c4-113">The password that was first set through the Windows PowerShell interface during registration can then be changed via the Azure classic portal.</span></span> <span data-ttu-id="412c4-114">執行下列步驟來變更裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="412c4-114">Perform the following steps to change the device administrator password.</span></span>

#### <a name="to-change-the-device-administrator-password"></a><span data-ttu-id="412c4-115">若要變更裝置系統管理員密碼：</span><span class="sxs-lookup"><span data-stu-id="412c4-115">To change the device administrator password</span></span>
1. <span data-ttu-id="412c4-116">在傳統入口網站中，對您的裝置按一下 [裝置] > [設定]。</span><span class="sxs-lookup"><span data-stu-id="412c4-116">In the classic portal, click **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="412c4-117">向下捲動至 [ **裝置系統管理員密碼** ] 區段。</span><span class="sxs-lookup"><span data-stu-id="412c4-117">Scroll down to the **Device Administrator Password** section.</span></span> <span data-ttu-id="412c4-118">提供含有 8 到 15 個字元的系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="412c4-118">Provide an administrator password that contains from 8 to 15 characters.</span></span> <span data-ttu-id="412c4-119">密碼必須是 3 個以上大寫、小寫、數字和特殊字元的組合。</span><span class="sxs-lookup"><span data-stu-id="412c4-119">The password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>
3. <span data-ttu-id="412c4-120">確認密碼。</span><span class="sxs-lookup"><span data-stu-id="412c4-120">Confirm the password.</span></span>
4. <span data-ttu-id="412c4-121">按一下頁面底部的 [儲存]  。</span><span class="sxs-lookup"><span data-stu-id="412c4-121">Click **Save** at the bottom of the page.</span></span>

<span data-ttu-id="412c4-122">現在應該已更新裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="412c4-122">The device administrator password should now be updated.</span></span> <span data-ttu-id="412c4-123">您可以使用此修改過的密碼來存取 Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="412c4-123">You can use this modified password to access the Windows PowerShell interface.</span></span>

## <a name="change-the-storsimple-snapshot-manager-password"></a><span data-ttu-id="412c4-124">變更 StorSimple Snapshot Manager 密碼</span><span class="sxs-lookup"><span data-stu-id="412c4-124">Change the StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="412c4-125">StorSimple Snapshot Manager 軟體位於您的 Windows 主機上，而且可讓系統管理員以本機和雲端快照的形式管理 StorSimple 裝置的備份。</span><span class="sxs-lookup"><span data-stu-id="412c4-125">StorSimple Snapshot Manager software resides on your Windows host and allows administrators to manage backups of your StorSimple device in the form of local and cloud snapshots.</span></span>

<span data-ttu-id="412c4-126">當您在 StorSimple Snapshot Manager 中設定裝置時，系統將提示您提供裝置 IP 位址和密碼來驗證您的儲存裝置。</span><span class="sxs-lookup"><span data-stu-id="412c4-126">When configuring a device in StorSimple Snapshot Manager, you will be prompted to provide the device IP address and password to authenticate your storage device.</span></span> <span data-ttu-id="412c4-127">此密碼最初是透過 Windows PowerShell 介面來設定。</span><span class="sxs-lookup"><span data-stu-id="412c4-127">This password is first configured through the Windows PowerShell interface.</span></span> <span data-ttu-id="412c4-128">如需詳細資訊，請參閱 [步驟 3：透過 Windows PowerShell for StorSimple 設定和註冊裝置](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)。</span><span class="sxs-lookup"><span data-stu-id="412c4-128">For more information, see [Step 3: Configure and register the device through Windows PowerShell for StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="412c4-129">然後可以透過傳統入口網站，變更在註冊期間先透過 Windows PowerShell 介面設定的密碼。</span><span class="sxs-lookup"><span data-stu-id="412c4-129">The password that was first set through the Windows PowerShell interface during registration can then be changed via the classic portal.</span></span> <span data-ttu-id="412c4-130">執行下列步驟來變更 StorSimple Snapshot Manager 密碼。</span><span class="sxs-lookup"><span data-stu-id="412c4-130">Perform the following steps to change the StorSimple Snapshot Manager password.</span></span>

#### <a name="to-change-the-storsimple-snapshot-manager-password"></a><span data-ttu-id="412c4-131">若要變更 StorSimple Snapshot Manager 密碼：</span><span class="sxs-lookup"><span data-stu-id="412c4-131">To change the StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="412c4-132">在傳統入口網站中，對您的裝置按一下 [裝置] > [設定]。</span><span class="sxs-lookup"><span data-stu-id="412c4-132">In the classic portal, click **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="412c4-133">向下捲動到 [ **StorSimple Snapshot Manager** ] 區段。</span><span class="sxs-lookup"><span data-stu-id="412c4-133">Scroll down to the **StorSimple Snapshot Manager** section.</span></span> <span data-ttu-id="412c4-134">輸入 14 或 15 個字元的密碼。</span><span class="sxs-lookup"><span data-stu-id="412c4-134">Enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="412c4-135">請確定密碼包含 3 個以上大寫、小寫、數字和特殊字元的組合。</span><span class="sxs-lookup"><span data-stu-id="412c4-135">Make sure that the password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>
3. <span data-ttu-id="412c4-136">確認密碼。</span><span class="sxs-lookup"><span data-stu-id="412c4-136">Confirm the password.</span></span>
4. <span data-ttu-id="412c4-137">按一下頁面底部的 [儲存]  。</span><span class="sxs-lookup"><span data-stu-id="412c4-137">Click **Save** at the bottom of the page.</span></span>

<span data-ttu-id="412c4-138">StorSimple Snapshot Manager 密碼現在應該已更新。</span><span class="sxs-lookup"><span data-stu-id="412c4-138">The StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="412c4-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="412c4-139">Next steps</span></span>
* <span data-ttu-id="412c4-140">深入了解 [StorSimple 安全性](storsimple-security.md)。</span><span class="sxs-lookup"><span data-stu-id="412c4-140">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="412c4-141">[深入了解修改您的裝置組態](storsimple-modify-device-config.md)。</span><span class="sxs-lookup"><span data-stu-id="412c4-141">Learn more about [modifying your device configuration](storsimple-modify-device-config.md).</span></span>
* <span data-ttu-id="412c4-142">深入了解 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="412c4-142">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

---
title: "aaaChange StorSimple 密碼 |Microsoft 文件"
description: "描述如何 toouse 會 hello StorSimple 裝置管理員服務 toochange StorSimple Snapshot Manager 」 和 「 裝置系統管理員密碼。"
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
ms.openlocfilehash: cf884be31b4bbf9e372c0aa11b9da2eadcda35dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a><span data-ttu-id="8b10e-103">使用 hello StorSimple 裝置管理員服務 toochange StorSimple 密碼</span><span class="sxs-lookup"><span data-stu-id="8b10e-103">Use hello StorSimple Device Manager service toochange your StorSimple passwords</span></span>

## <a name="overview"></a><span data-ttu-id="8b10e-104">概觀</span><span class="sxs-lookup"><span data-stu-id="8b10e-104">Overview</span></span>
<span data-ttu-id="8b10e-105">hello Azure 入口網站**裝置設定**選項包含所有您可以重新設定 StorSimple 裝置管理員服務所管理的 StorSimple 裝置的 hello 裝置參數。</span><span class="sxs-lookup"><span data-stu-id="8b10e-105">hello Azure portal **Device settings** option contains all hello device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Device Manager service.</span></span> <span data-ttu-id="8b10e-106">本教學課程說明如何使用 hello**安全性**選項在**裝置設定**toochange 您裝置的系統管理員或 StorSimple Snapshot Manager 密碼。</span><span class="sxs-lookup"><span data-stu-id="8b10e-106">This tutorial explains how you can use hello **Security** option under **Device settings** toochange your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-hello-device-administrator-password"></a><span data-ttu-id="8b10e-107">變更 hello 裝置系統管理員密碼</span><span class="sxs-lookup"><span data-stu-id="8b10e-107">Change hello device administrator password</span></span>
<span data-ttu-id="8b10e-108">當您使用 Windows PowerShell 介面 tooaccess hello StorSimple 裝置時，您就需要的 tooenter 裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="8b10e-108">When you use Windows PowerShell interface tooaccess hello StorSimple device, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="8b10e-109">當服務中註冊第一個 StorSimple 裝置 hello 時，此介面的 hello 預設密碼是*Password1*。</span><span class="sxs-lookup"><span data-stu-id="8b10e-109">When hello first StorSimple device is registered with a service, hello default password for this interface is *Password1*.</span></span> <span data-ttu-id="8b10e-110">Hello 資料的安全性，您對於需要的 toochange 這個密碼 hello hello 註冊程序的結尾。</span><span class="sxs-lookup"><span data-stu-id="8b10e-110">For hello security of your data, you are required toochange this password at hello end of hello registration process.</span></span> <span data-ttu-id="8b10e-111">您無法結束 hello 註冊程序，而不需要變更這個密碼。</span><span class="sxs-lookup"><span data-stu-id="8b10e-111">You cannot exit from hello registration process without changing this password.</span></span> <span data-ttu-id="8b10e-112">如需詳細資訊，請參閱[步驟 3： 設定和註冊 hello 裝置透過 Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)。</span><span class="sxs-lookup"><span data-stu-id="8b10e-112">For more information, see [Step 3: Configure and register hello device through Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="8b10e-113">在註冊期間第一次設定 hello Windows PowerShell 介面透過 hello 密碼可以稍後變更透過 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="8b10e-113">hello password that was first set through hello Windows PowerShell interface during registration can be changed later via hello Azure portal.</span></span> <span data-ttu-id="8b10e-114">執行下列步驟 toochange hello 裝置系統管理員密碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="8b10e-114">Perform hello following steps toochange hello device administrator password.</span></span>

#### <a name="toochange-hello-device-administrator-password"></a><span data-ttu-id="8b10e-115">toochange hello 裝置系統管理員密碼</span><span class="sxs-lookup"><span data-stu-id="8b10e-115">toochange hello device administrator password</span></span>
1. <span data-ttu-id="8b10e-116">移 tooyour StorSimple 裝置管理員服務，然後按一下**裝置**。</span><span class="sxs-lookup"><span data-stu-id="8b10e-116">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="8b10e-117">從 hello 表格清單中的裝置，選取，然後按一下 hello 裝置密碼想 toochange。</span><span class="sxs-lookup"><span data-stu-id="8b10e-117">From hello tabular listing of devices, select and click hello device whose password you intend toochange.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="8b10e-118">在 hello**設定**刀鋒視窗中，跳過**裝置設定 > 安全性**。</span><span class="sxs-lookup"><span data-stu-id="8b10e-118">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="8b10e-119">在 hello**安全性設定**刀鋒視窗中，按一下 **密碼**toochange hello 裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="8b10e-119">In hello **Security settings** blade, click **Password** toochange hello device administrator password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. <span data-ttu-id="8b10e-120">在 hello**密碼**刀鋒視窗中，提供系統管理員密碼包含 8 too15 個字元。</span><span class="sxs-lookup"><span data-stu-id="8b10e-120">In hello **Password** blade, provide an administrator password that contains from 8 too15 characters.</span></span> <span data-ttu-id="8b10e-121">hello 密碼必須是 3 個以上的大寫、 小寫、 數字及特殊字元的組合。</span><span class="sxs-lookup"><span data-stu-id="8b10e-121">hello password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="8b10e-122">確認 hello 的密碼。</span><span class="sxs-lookup"><span data-stu-id="8b10e-122">Confirm hello password.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. <span data-ttu-id="8b10e-123">按一下 [儲存]，當系統提示您進行確認時，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="8b10e-123">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="8b10e-124">hello 裝置系統管理員密碼現在應已更新。</span><span class="sxs-lookup"><span data-stu-id="8b10e-124">hello device administrator password should now be updated.</span></span> <span data-ttu-id="8b10e-125">您可以使用這個修改過的密碼 tooaccess hello Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="8b10e-125">You can use this modified password tooaccess hello Windows PowerShell interface.</span></span>

## <a name="set-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="8b10e-126">設定 hello StorSimple Snapshot Manager 密碼</span><span class="sxs-lookup"><span data-stu-id="8b10e-126">Set hello StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="8b10e-127">StorSimple Snapshot Manager 軟體位於您的 Windows 主機上，而且可讓系統管理員 toomanage 備份您的 StorSimple 裝置在 hello 表單的本機和雲端快照。</span><span class="sxs-lookup"><span data-stu-id="8b10e-127">StorSimple Snapshot Manager software resides on your Windows host and allows administrators toomanage backups of your StorSimple device in hello form of local and cloud snapshots.</span></span>

<span data-ttu-id="8b10e-128">時設定 StorSimple Snapshot Manager 中的裝置，您將看到 tooprovide hello 裝置 IP 位址和密碼 tooauthenticate 存放裝置。</span><span class="sxs-lookup"><span data-stu-id="8b10e-128">When configuring a device in StorSimple Snapshot Manager, you will be prompted tooprovide hello device IP address and password tooauthenticate your storage device.</span></span>

<span data-ttu-id="8b10e-129">您可以設定或變更 hello 密碼 StorSimple Snapshot Manager 透過 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="8b10e-129">You can set or change hello password for StorSimple Snapshot Manager via hello Azure portal.</span></span> <span data-ttu-id="8b10e-130">執行下列步驟 tooset hello 或變更 hello StorSimple Snapshot Manager 密碼。</span><span class="sxs-lookup"><span data-stu-id="8b10e-130">Perform hello following steps tooset or change hello StorSimple Snapshot Manager password.</span></span>

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="8b10e-131">tooset hello StorSimple Snapshot Manager 密碼</span><span class="sxs-lookup"><span data-stu-id="8b10e-131">tooset hello StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="8b10e-132">移 tooyour StorSimple 裝置管理員服務，然後按一下**裝置**。</span><span class="sxs-lookup"><span data-stu-id="8b10e-132">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span>

2. <span data-ttu-id="8b10e-133">從 hello 表格清單中的裝置，選取，然後按一下 hello 裝置想 tooset，或變更其 StorSimple Snapshot Manager 密碼。</span><span class="sxs-lookup"><span data-stu-id="8b10e-133">From hello tabular listing of devices, select and click hello device whose StorSimple Snapshot Manager password you intend tooset or change.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. <span data-ttu-id="8b10e-134">在 hello**設定**刀鋒視窗中，跳過**裝置設定 > 安全性**。</span><span class="sxs-lookup"><span data-stu-id="8b10e-134">In hello **Settings** blade, go too**Device settings > Security**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. <span data-ttu-id="8b10e-135">在 hello**安全性設定**刀鋒視窗中，按一下 **密碼**tooset 或變更 hello StorSimple Snapshot Manager 密碼。</span><span class="sxs-lookup"><span data-stu-id="8b10e-135">In hello **Security settings** blade, click **Password** tooset or change hello StorSimple Snapshot Manager password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. <span data-ttu-id="8b10e-136">在 hello**密碼**刀鋒視窗中，輸入 14 或 15 個字元的密碼。</span><span class="sxs-lookup"><span data-stu-id="8b10e-136">In hello **Password** blade, enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="8b10e-137">請確定該 hello 密碼包含 3 個以上的大寫、 小寫、 數字及特殊字元的組合。</span><span class="sxs-lookup"><span data-stu-id="8b10e-137">Make sure that hello password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>

6. <span data-ttu-id="8b10e-138">確認 hello 的密碼。</span><span class="sxs-lookup"><span data-stu-id="8b10e-138">Confirm hello password.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. <span data-ttu-id="8b10e-139">按一下 [儲存]，當系統提示您進行確認時，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="8b10e-139">Click **Save** and when prompted for confirmation, click **Yes**.</span></span>

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

<span data-ttu-id="8b10e-140">hello StorSimple Snapshot Manager 密碼現在應已更新。</span><span class="sxs-lookup"><span data-stu-id="8b10e-140">hello StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b10e-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8b10e-141">Next steps</span></span>
* <span data-ttu-id="8b10e-142">深入了解 [StorSimple 安全性](storsimple-8000-security.md)。</span><span class="sxs-lookup"><span data-stu-id="8b10e-142">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="8b10e-143">[深入了解修改您的裝置組態](storsimple-8000-modify-device-config.md)。</span><span class="sxs-lookup"><span data-stu-id="8b10e-143">Learn more about [modifying your device configuration](storsimple-8000-modify-device-config.md).</span></span>
* <span data-ttu-id="8b10e-144">深入了解[使用您的 StorSimple 裝置 hello StorSimple 裝置管理員服務 tooadminister](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="8b10e-144">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>


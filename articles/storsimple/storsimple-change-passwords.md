---
title: "aaaChange 密碼透過 StorSimple 裝置管理員 |Microsoft 文件"
description: "描述如何 toouse 會 hello StorSimple Manager 服務 toochange StorSimple Snapshot Manager 」 和 「 裝置系統管理員密碼。"
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
ms.openlocfilehash: b2836eb4d3a05e1d2a5eeeeefe66c75f63ba38ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toochange-your-storsimple-passwords"></a><span data-ttu-id="a9b89-103">使用 hello StorSimple Manager 服務 toochange StorSimple 密碼</span><span class="sxs-lookup"><span data-stu-id="a9b89-103">Use hello StorSimple Manager service toochange your StorSimple passwords</span></span>
## <a name="overview"></a><span data-ttu-id="a9b89-104">概觀</span><span class="sxs-lookup"><span data-stu-id="a9b89-104">Overview</span></span>
<span data-ttu-id="a9b89-105">hello Azure 傳統入口網站**設定**頁面包含您可以重新設定 StorSimple Manager 服務所管理的 StorSimple 裝置的所有 hello 裝置參數。</span><span class="sxs-lookup"><span data-stu-id="a9b89-105">hello Azure classic portal **Configure** page contains all hello device parameters that you can reconfigure on a StorSimple device that is managed by a StorSimple Manager service.</span></span> <span data-ttu-id="a9b89-106">本教學課程說明如何使用 hello**設定**頁面 toochange，您的裝置系統管理員或 StorSimple Snapshot Manager 密碼。</span><span class="sxs-lookup"><span data-stu-id="a9b89-106">This tutorial explains how you can use hello **Configure** page toochange your device administrator or StorSimple Snapshot Manager password.</span></span>

## <a name="change-hello-device-administrator-password"></a><span data-ttu-id="a9b89-107">變更 hello 裝置系統管理員密碼</span><span class="sxs-lookup"><span data-stu-id="a9b89-107">Change hello device administrator password</span></span>
<span data-ttu-id="a9b89-108">當您使用 Windows PowerShell 介面 tooaccess hello StorSimple 裝置時，您就需要的 tooenter 裝置系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="a9b89-108">When you use Windows PowerShell interface tooaccess hello StorSimple device, you are required tooenter a device administrator password.</span></span> <span data-ttu-id="a9b89-109">當服務中註冊第一個 StorSimple 裝置 hello 時，此介面的 hello 預設密碼是*Password1*。</span><span class="sxs-lookup"><span data-stu-id="a9b89-109">When hello first StorSimple device is registered with a service, hello default password for this interface is *Password1*.</span></span> <span data-ttu-id="a9b89-110">Hello 資料的安全性，您對於需要的 toochange 這個密碼 hello hello 註冊程序的結尾。</span><span class="sxs-lookup"><span data-stu-id="a9b89-110">For hello security of your data, you are required toochange this password at hello end of hello registration process.</span></span> <span data-ttu-id="a9b89-111">您無法結束 hello 註冊程序，而不需要變更這個密碼。</span><span class="sxs-lookup"><span data-stu-id="a9b89-111">You cannot exit from hello registration process without changing this password.</span></span> <span data-ttu-id="a9b89-112">如需詳細資訊，請參閱[步驟 3： 設定和註冊 hello 裝置透過 Windows PowerShell for StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)。</span><span class="sxs-lookup"><span data-stu-id="a9b89-112">For more information, see [Step 3: Configure and register hello device through Windows PowerShell for StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="a9b89-113">第一次設定透過 hello Windows PowerShell 介面註冊期間的 hello 密碼然後可以透過 hello Azure 傳統入口網站變更。</span><span class="sxs-lookup"><span data-stu-id="a9b89-113">hello password that was first set through hello Windows PowerShell interface during registration can then be changed via hello Azure classic portal.</span></span> <span data-ttu-id="a9b89-114">執行下列步驟 toochange hello 裝置系統管理員密碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="a9b89-114">Perform hello following steps toochange hello device administrator password.</span></span>

#### <a name="toochange-hello-device-administrator-password"></a><span data-ttu-id="a9b89-115">toochange hello 裝置系統管理員密碼</span><span class="sxs-lookup"><span data-stu-id="a9b89-115">toochange hello device administrator password</span></span>
1. <span data-ttu-id="a9b89-116">在 hello 傳統入口網站，按一下 **裝置** > **設定**為您的裝置。</span><span class="sxs-lookup"><span data-stu-id="a9b89-116">In hello classic portal, click **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="a9b89-117">捲動 toohello**裝置系統管理員密碼**> 一節。</span><span class="sxs-lookup"><span data-stu-id="a9b89-117">Scroll down toohello **Device Administrator Password** section.</span></span> <span data-ttu-id="a9b89-118">提供系統管理員密碼包含 8 too15 個字元。</span><span class="sxs-lookup"><span data-stu-id="a9b89-118">Provide an administrator password that contains from 8 too15 characters.</span></span> <span data-ttu-id="a9b89-119">hello 密碼必須是 3 個以上的大寫、 小寫、 數字及特殊字元的組合。</span><span class="sxs-lookup"><span data-stu-id="a9b89-119">hello password must be a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>
3. <span data-ttu-id="a9b89-120">確認 hello 的密碼。</span><span class="sxs-lookup"><span data-stu-id="a9b89-120">Confirm hello password.</span></span>
4. <span data-ttu-id="a9b89-121">按一下**儲存**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="a9b89-121">Click **Save** at hello bottom of hello page.</span></span>

<span data-ttu-id="a9b89-122">hello 裝置系統管理員密碼現在應已更新。</span><span class="sxs-lookup"><span data-stu-id="a9b89-122">hello device administrator password should now be updated.</span></span> <span data-ttu-id="a9b89-123">您可以使用這個修改過的密碼 tooaccess hello Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="a9b89-123">You can use this modified password tooaccess hello Windows PowerShell interface.</span></span>

## <a name="change-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="a9b89-124">變更 hello StorSimple Snapshot Manager 密碼</span><span class="sxs-lookup"><span data-stu-id="a9b89-124">Change hello StorSimple Snapshot Manager password</span></span>
<span data-ttu-id="a9b89-125">StorSimple Snapshot Manager 軟體位於您的 Windows 主機上，而且可讓系統管理員 toomanage 備份您的 StorSimple 裝置在 hello 表單的本機和雲端快照。</span><span class="sxs-lookup"><span data-stu-id="a9b89-125">StorSimple Snapshot Manager software resides on your Windows host and allows administrators toomanage backups of your StorSimple device in hello form of local and cloud snapshots.</span></span>

<span data-ttu-id="a9b89-126">時設定 StorSimple Snapshot Manager 中的裝置，您將看到 tooprovide hello 裝置 IP 位址和密碼 tooauthenticate 存放裝置。</span><span class="sxs-lookup"><span data-stu-id="a9b89-126">When configuring a device in StorSimple Snapshot Manager, you will be prompted tooprovide hello device IP address and password tooauthenticate your storage device.</span></span> <span data-ttu-id="a9b89-127">透過 hello Windows PowerShell 介面，會先設定這個密碼。</span><span class="sxs-lookup"><span data-stu-id="a9b89-127">This password is first configured through hello Windows PowerShell interface.</span></span> <span data-ttu-id="a9b89-128">如需詳細資訊，請參閱[步驟 3： 設定和註冊 hello 裝置透過 Windows PowerShell for StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)。</span><span class="sxs-lookup"><span data-stu-id="a9b89-128">For more information, see [Step 3: Configure and register hello device through Windows PowerShell for StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).</span></span>

<span data-ttu-id="a9b89-129">第一次設定透過 hello Windows PowerShell 介面註冊期間的 hello 密碼然後可以透過 hello 傳統入口網站變更。</span><span class="sxs-lookup"><span data-stu-id="a9b89-129">hello password that was first set through hello Windows PowerShell interface during registration can then be changed via hello classic portal.</span></span> <span data-ttu-id="a9b89-130">執行下列步驟 toochange hello StorSimple Snapshot Manager 密碼 hello。</span><span class="sxs-lookup"><span data-stu-id="a9b89-130">Perform hello following steps toochange hello StorSimple Snapshot Manager password.</span></span>

#### <a name="toochange-hello-storsimple-snapshot-manager-password"></a><span data-ttu-id="a9b89-131">toochange hello StorSimple Snapshot Manager 密碼</span><span class="sxs-lookup"><span data-stu-id="a9b89-131">toochange hello StorSimple Snapshot Manager password</span></span>
1. <span data-ttu-id="a9b89-132">在 hello 傳統入口網站，按一下 **裝置** > **設定**為您的裝置。</span><span class="sxs-lookup"><span data-stu-id="a9b89-132">In hello classic portal, click **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="a9b89-133">捲動 toohello **StorSimple Snapshot Manager** > 一節。</span><span class="sxs-lookup"><span data-stu-id="a9b89-133">Scroll down toohello **StorSimple Snapshot Manager** section.</span></span> <span data-ttu-id="a9b89-134">輸入 14 或 15 個字元的密碼。</span><span class="sxs-lookup"><span data-stu-id="a9b89-134">Enter a password that is 14 or 15 characters.</span></span> <span data-ttu-id="a9b89-135">請確定該 hello 密碼包含 3 個以上的大寫、 小寫、 數字及特殊字元的組合。</span><span class="sxs-lookup"><span data-stu-id="a9b89-135">Make sure that hello password contains a combination of 3 or more of uppercase, lowercase, numeric, and special characters.</span></span>
3. <span data-ttu-id="a9b89-136">確認 hello 的密碼。</span><span class="sxs-lookup"><span data-stu-id="a9b89-136">Confirm hello password.</span></span>
4. <span data-ttu-id="a9b89-137">按一下**儲存**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="a9b89-137">Click **Save** at hello bottom of hello page.</span></span>

<span data-ttu-id="a9b89-138">hello StorSimple Snapshot Manager 密碼現在應已更新。</span><span class="sxs-lookup"><span data-stu-id="a9b89-138">hello StorSimple Snapshot Manager password should now be updated.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9b89-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a9b89-139">Next steps</span></span>
* <span data-ttu-id="a9b89-140">深入了解 [StorSimple 安全性](storsimple-security.md)。</span><span class="sxs-lookup"><span data-stu-id="a9b89-140">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="a9b89-141">[深入了解修改您的裝置組態](storsimple-modify-device-config.md)。</span><span class="sxs-lookup"><span data-stu-id="a9b89-141">Learn more about [modifying your device configuration](storsimple-modify-device-config.md).</span></span>
* <span data-ttu-id="a9b89-142">深入了解[使用您的 StorSimple 裝置 hello StorSimple Manager 服務 tooadminister](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="a9b89-142">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>


---
title: "針對 StorSimple 8000 系列裝置設定 CHAP | Microsoft Docs"
description: "描述如何在 StorSimple 裝置上設定 Challenge Handshake 驗證通訊協定 (CHAP)。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 61e0877187759d76b6f7efcef0a5ed8bec8500fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="e327e-103">為 StorSimple 裝置設定 CHAP</span><span class="sxs-lookup"><span data-stu-id="e327e-103">Configure CHAP for your StorSimple device</span></span>

<span data-ttu-id="e327e-104">本教學課程說明如何為 StorSimple 裝置設定 CHAP。</span><span class="sxs-lookup"><span data-stu-id="e327e-104">This tutorial explains how to configure CHAP for your StorSimple device.</span></span> <span data-ttu-id="e327e-105">這篇文章詳述的程序適用於 StorSimple 8000 系列裝置。</span><span class="sxs-lookup"><span data-stu-id="e327e-105">The procedure detailed in this article applies to StorSimple 8000 series devices.</span></span>

<span data-ttu-id="e327e-106">CHAP 代表 Challenge Handshake 驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="e327e-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="e327e-107">它是伺服器用來驗證遠端用戶端身分識別的驗證配置。</span><span class="sxs-lookup"><span data-stu-id="e327e-107">It is an authentication scheme used by servers to validate the identity of remote clients.</span></span> <span data-ttu-id="e327e-108">此驗證以共用密碼或密碼為基礎。</span><span class="sxs-lookup"><span data-stu-id="e327e-108">The verification is based on a shared password or secret.</span></span> <span data-ttu-id="e327e-109">CHAP 可以是單向 (單向) 或相互 (雙向)。</span><span class="sxs-lookup"><span data-stu-id="e327e-109">CHAP can be one way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="e327e-110">目標驗證啟動器時，會使用單向 CHAP。</span><span class="sxs-lookup"><span data-stu-id="e327e-110">One way CHAP is when the target authenticates an initiator.</span></span> <span data-ttu-id="e327e-111">在相互或反相 CHAP 中，目標會驗證啟動器，然後啟動器會驗證目標。</span><span class="sxs-lookup"><span data-stu-id="e327e-111">In mutual or reverse CHAP, the target authenticates the initiator and then the initiator authenticates the target.</span></span> <span data-ttu-id="e327e-112">不需要目標驗證也能實作啟動器驗證。</span><span class="sxs-lookup"><span data-stu-id="e327e-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="e327e-113">不過，必須同時實作啟動器驗證，才能實作目標驗證。</span><span class="sxs-lookup"><span data-stu-id="e327e-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span>

<span data-ttu-id="e327e-114">以最佳作法而言，建議您使用 CHAP 以增強 iSCSI 安全性。</span><span class="sxs-lookup"><span data-stu-id="e327e-114">As a best practice, we recommend that you use CHAP to enhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="e327e-115">請記住，StorSimple 裝置目前不支援 IPSEC。</span><span class="sxs-lookup"><span data-stu-id="e327e-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>

<span data-ttu-id="e327e-116">在 StorSimple 裝置上可以使用下列方式設定 CHAP 設定：</span><span class="sxs-lookup"><span data-stu-id="e327e-116">The CHAP settings on the StorSimple device can be configured in the following ways:</span></span>

* <span data-ttu-id="e327e-117">單向驗證</span><span class="sxs-lookup"><span data-stu-id="e327e-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="e327e-118">雙向、相互或反向驗證</span><span class="sxs-lookup"><span data-stu-id="e327e-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="e327e-119">在這每一種情況下，都需要設定裝置入口網站和伺服器 iSCSI 啟動器軟體。</span><span class="sxs-lookup"><span data-stu-id="e327e-119">In each of these cases, the portal for the device and the server iSCSI initiator software needs to be configured.</span></span> <span data-ttu-id="e327e-120">下列教學課程將說明這項設定的詳細步驟。</span><span class="sxs-lookup"><span data-stu-id="e327e-120">The detailed steps for this configuration are described in the following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="e327e-121">單向驗證</span><span class="sxs-lookup"><span data-stu-id="e327e-121">Unidirectional or one-way authentication</span></span>

<span data-ttu-id="e327e-122">在單向驗證中，目標會驗證啟動器。</span><span class="sxs-lookup"><span data-stu-id="e327e-122">In unidirectional authentication, the target authenticates the initiator.</span></span> <span data-ttu-id="e327e-123">此驗證會要求您設定 StorSimple 裝置上的 CHAP 啟動器設定，以及主機上的 iSCSI 啟動器軟體。</span><span class="sxs-lookup"><span data-stu-id="e327e-123">This authentication requires that you configure the CHAP initiator settings on the StorSimple device and the iSCSI Initiator software on the host.</span></span> <span data-ttu-id="e327e-124">接下來說明您的 StorSimple 裝置和 Windows 主機的詳細程序。</span><span class="sxs-lookup"><span data-stu-id="e327e-124">The detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="to-configure-your-device-for-one-way-authentication"></a><span data-ttu-id="e327e-125">設定裝置進行單向驗證</span><span class="sxs-lookup"><span data-stu-id="e327e-125">To configure your device for one-way authentication</span></span>

1. <span data-ttu-id="e327e-126">在 Azure 入口網站中，移至您的 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="e327e-126">In the Azure portal, go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="e327e-127">按一下 [裝置]，然後選取並按一下您想要設定 CHAP 的裝置。</span><span class="sxs-lookup"><span data-stu-id="e327e-127">Click **Devices** and select and click a device you wish to configure CHAP for.</span></span> <span data-ttu-id="e327e-128">移至 [裝置設定] > [安全性]。</span><span class="sxs-lookup"><span data-stu-id="e327e-128">Go to **Device settings > Security**.</span></span> <span data-ttu-id="e327e-129">在 [安全性設定] 刀鋒視窗中，按一下 [CHAP]。</span><span class="sxs-lookup"><span data-stu-id="e327e-129">In the **Security settings** blade, click **CHAP**.</span></span>
   
    ![CHAP 啟動器](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="e327e-131">在 [CHAP] 刀鋒視窗的 [CHAP 啟動器] 區段中：</span><span class="sxs-lookup"><span data-stu-id="e327e-131">In the **CHAP** blade, and in the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="e327e-132">提供 CHAP 啟動器的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="e327e-132">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="e327e-133">提供 CHAP 啟動器的密碼。</span><span class="sxs-lookup"><span data-stu-id="e327e-133">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="e327e-134">CHAP 使用者名稱不得超過 233 個字元。</span><span class="sxs-lookup"><span data-stu-id="e327e-134">The CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="e327e-135">CHAP 密碼必須介於 12 到 16 個字元。</span><span class="sxs-lookup"><span data-stu-id="e327e-135">The CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="e327e-136">較長的使用者名稱或密碼會導致 Windows 主機上發生驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="e327e-136">A longer user name or password results in an authentication failure on the Windows host.</span></span>
   
   3. <span data-ttu-id="e327e-137">確認密碼。</span><span class="sxs-lookup"><span data-stu-id="e327e-137">Confirm the password.</span></span>

       ![CHAP 啟動器](./media/storsimple-8000-configure-chap/configure-chap6.png)
3. <span data-ttu-id="e327e-139">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="e327e-139">Click **Save**.</span></span> <span data-ttu-id="e327e-140">隨即顯示確認訊息。</span><span class="sxs-lookup"><span data-stu-id="e327e-140">A confirmation message is displayed.</span></span> <span data-ttu-id="e327e-141">按一下 [確定]  儲存變更。</span><span class="sxs-lookup"><span data-stu-id="e327e-141">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-one-way-authentication-on-the-windows-host-server"></a><span data-ttu-id="e327e-142">在 Windows 主機伺服器上設定單向驗證</span><span class="sxs-lookup"><span data-stu-id="e327e-142">To configure one-way authentication on the Windows host server</span></span>
1. <span data-ttu-id="e327e-143">在 Windows 主機伺服器上啟動 iSCSI 啟動器。</span><span class="sxs-lookup"><span data-stu-id="e327e-143">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="e327e-144">在 [iSCSI 啟動器屬性]  視窗中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e327e-144">In the **iSCSI Initiator Properties** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="e327e-145">按一下 [探索]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e327e-145">Click the **Discovery** tab.</span></span>
      
       ![iSCSI 啟動器屬性](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="e327e-147">按一下 [探索入口網站] 。</span><span class="sxs-lookup"><span data-stu-id="e327e-147">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="e327e-148">在 [探索目標入口網站]  對話方塊中：</span><span class="sxs-lookup"><span data-stu-id="e327e-148">In the **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="e327e-149">指定裝置的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e327e-149">Specify the IP address of your device.</span></span>
   2. <span data-ttu-id="e327e-150">按一下 [進階] 。</span><span class="sxs-lookup"><span data-stu-id="e327e-150">Click **Advanced**.</span></span>
      
       ![探索目標入口網站](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="e327e-152">在 [進階設定]  對話方塊中：</span><span class="sxs-lookup"><span data-stu-id="e327e-152">In the **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="e327e-153">選取 [啟用 CHAP 登入]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="e327e-153">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="e327e-154">在 [名稱]  欄位中，提供您在傳統入口網站中指定給 CHAP 啟動器的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="e327e-154">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="e327e-155">在 [目標密碼]  欄位中，提供您在傳統入口網站中指定給 CHAP 啟動器的密碼。</span><span class="sxs-lookup"><span data-stu-id="e327e-155">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="e327e-156">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e327e-156">Click **OK**.</span></span>
      
       ![進階設定 - 一般](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="e327e-158">在 [iSCSI 啟動器屬性] 視窗的 [目標] 索引標籤上，裝置狀態應該會顯示為 [已連線]。</span><span class="sxs-lookup"><span data-stu-id="e327e-158">On the **Targets** tab of the **iSCSI Initiator Properties** window, the device status should appear as **Connected**.</span></span> <span data-ttu-id="e327e-159">如果您使用 StorSimple 1200 裝置，則每個磁碟區會掛接為 iSCSI 目標。</span><span class="sxs-lookup"><span data-stu-id="e327e-159">If you are using a StorSimple 1200 device, then each volume is mounted as an iSCSI target.</span></span> <span data-ttu-id="e327e-160">因此，需要對每個磁碟區重複執行步驟 3-4。</span><span class="sxs-lookup"><span data-stu-id="e327e-160">Hence, steps 3-4 will need to be repeated for each volume.</span></span>
   
    ![做為個別目標掛接的磁碟區](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="e327e-162">如果您變更 iSCSI 名稱，新的名稱會用於新的 iSCSI 工作階段。</span><span class="sxs-lookup"><span data-stu-id="e327e-162">If you change the iSCSI name, the new name is used for new iSCSI sessions.</span></span> <span data-ttu-id="e327e-163">您必須先登出再登入，現有的工作階段才會使用新的設定。</span><span class="sxs-lookup"><span data-stu-id="e327e-163">New settings are not used for existing sessions until you log off and log on again.</span></span>

<span data-ttu-id="e327e-164">如需在 Windows 主機伺服器上設定 CHAP 的詳細資訊，請移至 [其他考量](#additional-considerations)。</span><span class="sxs-lookup"><span data-stu-id="e327e-164">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="e327e-165">雙向或相互驗證</span><span class="sxs-lookup"><span data-stu-id="e327e-165">Bidirectional or mutual authentication</span></span>

<span data-ttu-id="e327e-166">在雙向驗證中，目標會驗證啟動器，然後啟動器再驗證目標。</span><span class="sxs-lookup"><span data-stu-id="e327e-166">In bidirectional authentication, the target authenticates the initiator and then the initiator authenticates the target.</span></span> <span data-ttu-id="e327e-167">此程序需要使用者設定 CHAP 啟動器設定、裝置上的反向 CHAP 啟動器設定以及主機上的 iSCSI 啟動器軟體。</span><span class="sxs-lookup"><span data-stu-id="e327e-167">This procedure requires the user to configure the CHAP initiator settings, reverse CHAP settings on the device, and iSCSI Initiator software on the host.</span></span> <span data-ttu-id="e327e-168">下列程序說明在裝置和 Windows 主機上設定相互驗證的步驟。</span><span class="sxs-lookup"><span data-stu-id="e327e-168">The following procedures describe the steps to configure mutual authentication on the device and on the Windows host.</span></span>

#### <a name="to-configure-your-device-for-mutual-authentication"></a><span data-ttu-id="e327e-169">設定裝置進行雙向驗證</span><span class="sxs-lookup"><span data-stu-id="e327e-169">To configure your device for mutual authentication</span></span>

1. <span data-ttu-id="e327e-170">在 Azure 入口網站中，移至您的 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="e327e-170">In the Azure portal, go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="e327e-171">按一下 [裝置]，然後選取並按一下您想要設定 CHAP 的裝置。</span><span class="sxs-lookup"><span data-stu-id="e327e-171">Click **Devices** and select and click a device you wish to configure CHAP for.</span></span> <span data-ttu-id="e327e-172">移至 [裝置設定] > [安全性]。</span><span class="sxs-lookup"><span data-stu-id="e327e-172">Go to **Device settings > Security**.</span></span> <span data-ttu-id="e327e-173">在 [安全性設定] 刀鋒視窗中，按一下 [CHAP]。</span><span class="sxs-lookup"><span data-stu-id="e327e-173">In the **Security settings** blade, click **CHAP**.</span></span>
   
    ![CHAP 目標](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="e327e-175">在此頁面向下捲動，並在 [CHAP 目標]  區段中：</span><span class="sxs-lookup"><span data-stu-id="e327e-175">Scroll down on this page, and in the **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="e327e-176">提供裝置的 [反向 CHAP 使用者名稱]  。</span><span class="sxs-lookup"><span data-stu-id="e327e-176">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="e327e-177">提供裝置的 [反向 CHAP 密碼]  。</span><span class="sxs-lookup"><span data-stu-id="e327e-177">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="e327e-178">確認密碼。</span><span class="sxs-lookup"><span data-stu-id="e327e-178">Confirm the password.</span></span>
3. <span data-ttu-id="e327e-179">在 [CHAP 啟動器]  區段中：</span><span class="sxs-lookup"><span data-stu-id="e327e-179">In the **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="e327e-180">提供裝置的 [使用者名稱]  。</span><span class="sxs-lookup"><span data-stu-id="e327e-180">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="e327e-181">提供裝置的 [密碼]  。</span><span class="sxs-lookup"><span data-stu-id="e327e-181">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="e327e-182">確認密碼。</span><span class="sxs-lookup"><span data-stu-id="e327e-182">Confirm the password.</span></span>

       ![CHAP 啟動器](./media/storsimple-8000-configure-chap/configure-chap11.png)
4. <span data-ttu-id="e327e-184">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="e327e-184">Click **Save**.</span></span> <span data-ttu-id="e327e-185">隨即顯示確認訊息。</span><span class="sxs-lookup"><span data-stu-id="e327e-185">A confirmation message is displayed.</span></span> <span data-ttu-id="e327e-186">按一下 [確定]  儲存變更。</span><span class="sxs-lookup"><span data-stu-id="e327e-186">Click **OK** to save the changes.</span></span>

#### <a name="to-configure-bidirectional-authentication-on-the-windows-host-server"></a><span data-ttu-id="e327e-187">在 Windows 主機伺服器上設定雙向驗證</span><span class="sxs-lookup"><span data-stu-id="e327e-187">To configure bidirectional authentication on the Windows host server</span></span>

1. <span data-ttu-id="e327e-188">在 Windows 主機伺服器上啟動 iSCSI 啟動器。</span><span class="sxs-lookup"><span data-stu-id="e327e-188">On the Windows host server, start the iSCSI Initiator.</span></span>
2. <span data-ttu-id="e327e-189">在 [iSCSI 啟動器屬性] 視窗中，按一下 [組態] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e327e-189">In the **iSCSI Initiator Properties** window, click the **Configuration** tab.</span></span>
3. <span data-ttu-id="e327e-190">按一下 [CHAP] 。</span><span class="sxs-lookup"><span data-stu-id="e327e-190">Click **CHAP**.</span></span>
4. <span data-ttu-id="e327e-191">在 [iSCSI 啟動器相互 CHAP 密碼]  對話方塊中：</span><span class="sxs-lookup"><span data-stu-id="e327e-191">In the **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="e327e-192">輸入您在 Azure 入口網站中設定的 [反向 CHAP 密碼]。</span><span class="sxs-lookup"><span data-stu-id="e327e-192">Type the **Reverse CHAP Password** that you configured in the Azure portal.</span></span>
   2. <span data-ttu-id="e327e-193">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e327e-193">Click **OK**.</span></span>
      
       ![iSCSI 啟動器相互 CHAP 密碼](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="e327e-195">按一下 [目標]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e327e-195">Click the **Targets** tab.</span></span>
6. <span data-ttu-id="e327e-196">按一下 [連線]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e327e-196">Click the **Connect** button.</span></span> 
7. <span data-ttu-id="e327e-197">在 [連線至目標] 對話方塊中，按一下 [進階]。</span><span class="sxs-lookup"><span data-stu-id="e327e-197">In the **Connect To Target** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="e327e-198">在 [進階屬性]  對話方塊中：</span><span class="sxs-lookup"><span data-stu-id="e327e-198">In the **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="e327e-199">選取 [啟用 CHAP 登入]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="e327e-199">Select the **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="e327e-200">在 [名稱]  欄位中，提供您在傳統入口網站中指定給 CHAP 啟動器的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="e327e-200">In the **Name** field, supply the user name that you specified for the CHAP Initiator in the classic portal.</span></span>
   3. <span data-ttu-id="e327e-201">在 [目標密碼]  欄位中，提供您在傳統入口網站中指定給 CHAP 啟動器的密碼。</span><span class="sxs-lookup"><span data-stu-id="e327e-201">In the **Target secret** field, supply the password that you specified for the CHAP Initiator in the classic portal.</span></span>
   4. <span data-ttu-id="e327e-202">選取 [執行相互驗證]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="e327e-202">Select the **Perform mutual authentication** check box.</span></span>
      
       ![進階設定 - 相互驗證](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="e327e-204">按一下 [確定]  以完成 CHAP 設定。</span><span class="sxs-lookup"><span data-stu-id="e327e-204">Click **OK** to complete the CHAP configuration</span></span>

<span data-ttu-id="e327e-205">如需在 Windows 主機伺服器上設定 CHAP 的詳細資訊，請移至 [其他考量](#additional-considerations)。</span><span class="sxs-lookup"><span data-stu-id="e327e-205">For more information about configuring CHAP on the Windows host server, go to [Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="e327e-206">其他考量</span><span class="sxs-lookup"><span data-stu-id="e327e-206">Additional considerations</span></span>

<span data-ttu-id="e327e-207">**快速連線** 功能不支援已啟用 CHAP 的連線。</span><span class="sxs-lookup"><span data-stu-id="e327e-207">The **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="e327e-208">啟用 CHAP 時，請確定您使用 [目標] 索引標籤上的 [連線] 按鈕來連線到目標。</span><span class="sxs-lookup"><span data-stu-id="e327e-208">When CHAP is enabled, make sure that you use the **Connect** button that is available on the **Targets** tab to connect to a target.</span></span>

![連線至目標](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="e327e-210">在出現的 [連線至目標] 對話方塊中，選取 [將此連線新增到我的最愛目標清單] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="e327e-210">In the **Connect to Target** dialog box that is presented, select the **Add this connection to the list of Favorite Targets** check box.</span></span> <span data-ttu-id="e327e-211">此選項可確保每次電腦重新啟動時，就會嘗試恢復連線到 iSCSI 我的最愛目標。</span><span class="sxs-lookup"><span data-stu-id="e327e-211">This selection ensures that every time the computer restarts, an attempt is made to restore the connection to the iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="e327e-212">設定期間發生錯誤</span><span class="sxs-lookup"><span data-stu-id="e327e-212">Errors during configuration</span></span>

<span data-ttu-id="e327e-213">如果 CHAP 設定不正確，您可能會看到 **驗證失敗** 錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="e327e-213">If your CHAP configuration is incorrect, then you are likely to see an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="e327e-214">CHAP 設定的驗證</span><span class="sxs-lookup"><span data-stu-id="e327e-214">Verification of CHAP configuration</span></span>

<span data-ttu-id="e327e-215">您可以完成下列步驟來確認正在使用 CHAP。</span><span class="sxs-lookup"><span data-stu-id="e327e-215">You can verify that CHAP is being used by completing the following steps.</span></span>

#### <a name="to-verify-your-chap-configuration"></a><span data-ttu-id="e327e-216">驗證 CHAP 設定</span><span class="sxs-lookup"><span data-stu-id="e327e-216">To verify your CHAP configuration</span></span>
1. <span data-ttu-id="e327e-217">按一下 [我的最愛目標] 。</span><span class="sxs-lookup"><span data-stu-id="e327e-217">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="e327e-218">選取您已啟用驗證的目標。</span><span class="sxs-lookup"><span data-stu-id="e327e-218">Select the target for which you enabled authentication.</span></span>
3. <span data-ttu-id="e327e-219">按一下 [詳細資訊] 。</span><span class="sxs-lookup"><span data-stu-id="e327e-219">Click **Details**.</span></span>
   
    ![iSCSI 啟動器屬性 - 我的最愛目標](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="e327e-221">在 [我的最愛目標詳細資訊] 對話方塊中，注意 [驗證] 欄位中的項目。</span><span class="sxs-lookup"><span data-stu-id="e327e-221">In the **Favorite Target Details** dialog box, note the entry in the **Authentication** field.</span></span> <span data-ttu-id="e327e-222">如果設定成功，應該會顯示 **CHAP**。</span><span class="sxs-lookup"><span data-stu-id="e327e-222">If the configuration was successful, it should say **CHAP**.</span></span>
   
    ![我的最愛目標詳細資料](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="e327e-224">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e327e-224">Next steps</span></span>

* <span data-ttu-id="e327e-225">深入了解 [StorSimple 安全性](storsimple-8000-security.md)。</span><span class="sxs-lookup"><span data-stu-id="e327e-225">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="e327e-226">深入了解[使用 StorSimple 裝置管理員服務管理 StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="e327e-226">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>


---
title: "StorSimple 8000 系列裝置的 aaaConfigure CHAP |Microsoft 文件"
description: "描述如何 tooconfigure hello StorSimple 裝置上的 Challenge Handshake 驗證通訊協定 (CHAP)。"
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
ms.openlocfilehash: 3351184b0317da7e3deae398bc0d63c3e5bd930f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="092b2-103">為 StorSimple 裝置設定 CHAP</span><span class="sxs-lookup"><span data-stu-id="092b2-103">Configure CHAP for your StorSimple device</span></span>

<span data-ttu-id="092b2-104">本教學課程說明如何 tooconfigure CHAP 您 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="092b2-104">This tutorial explains how tooconfigure CHAP for your StorSimple device.</span></span> <span data-ttu-id="092b2-105">此文件中詳述的 hello 程序適用於 8000 系列裝置 tooStorSimple。</span><span class="sxs-lookup"><span data-stu-id="092b2-105">hello procedure detailed in this article applies tooStorSimple 8000 series devices.</span></span>

<span data-ttu-id="092b2-106">CHAP 代表 Challenge Handshake 驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="092b2-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="092b2-107">它是伺服器 toovalidate hello 身分識別的遠端用戶端所使用的驗證配置。</span><span class="sxs-lookup"><span data-stu-id="092b2-107">It is an authentication scheme used by servers toovalidate hello identity of remote clients.</span></span> <span data-ttu-id="092b2-108">hello 驗證根據共用的密碼或密碼。</span><span class="sxs-lookup"><span data-stu-id="092b2-108">hello verification is based on a shared password or secret.</span></span> <span data-ttu-id="092b2-109">CHAP 可以是單向 (單向) 或相互 (雙向)。</span><span class="sxs-lookup"><span data-stu-id="092b2-109">CHAP can be one way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="092b2-110">單向 CHAP 時，hello 目標驗證啟動器。</span><span class="sxs-lookup"><span data-stu-id="092b2-110">One way CHAP is when hello target authenticates an initiator.</span></span> <span data-ttu-id="092b2-111">在相互或反向 CHAP hello 目標驗證啟動器 hello，然後 hello 啟動器驗證目標 hello。</span><span class="sxs-lookup"><span data-stu-id="092b2-111">In mutual or reverse CHAP, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="092b2-112">不需要目標驗證也能實作啟動器驗證。</span><span class="sxs-lookup"><span data-stu-id="092b2-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="092b2-113">不過，必須同時實作啟動器驗證，才能實作目標驗證。</span><span class="sxs-lookup"><span data-stu-id="092b2-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span>

<span data-ttu-id="092b2-114">最佳做法，我們建議您使用 CHAP tooenhance iSCSI 安全性。</span><span class="sxs-lookup"><span data-stu-id="092b2-114">As a best practice, we recommend that you use CHAP tooenhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="092b2-115">請記住，StorSimple 裝置目前不支援 IPSEC。</span><span class="sxs-lookup"><span data-stu-id="092b2-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>

<span data-ttu-id="092b2-116">hello hello StorSimple 裝置上的 CHAP 設定可以在 hello 下列方式設定：</span><span class="sxs-lookup"><span data-stu-id="092b2-116">hello CHAP settings on hello StorSimple device can be configured in hello following ways:</span></span>

* <span data-ttu-id="092b2-117">單向驗證</span><span class="sxs-lookup"><span data-stu-id="092b2-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="092b2-118">雙向、相互或反向驗證</span><span class="sxs-lookup"><span data-stu-id="092b2-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="092b2-119">在每個這種情況下，hello hello 裝置與 hello 伺服器 iSCSI 啟動器軟體的入口網站會需要 toobe 設定。</span><span class="sxs-lookup"><span data-stu-id="092b2-119">In each of these cases, hello portal for hello device and hello server iSCSI initiator software needs toobe configured.</span></span> <span data-ttu-id="092b2-120">hello 詳細的步驟，此組態中有描述 hello 教學課程。</span><span class="sxs-lookup"><span data-stu-id="092b2-120">hello detailed steps for this configuration are described in hello following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="092b2-121">單向驗證</span><span class="sxs-lookup"><span data-stu-id="092b2-121">Unidirectional or one-way authentication</span></span>

<span data-ttu-id="092b2-122">在單向驗證中，hello 目標驗證啟動器 hello。</span><span class="sxs-lookup"><span data-stu-id="092b2-122">In unidirectional authentication, hello target authenticates hello initiator.</span></span> <span data-ttu-id="092b2-123">此驗證，您必須設定 hello CHAP 啟動器設定 hello StorSimple 裝置和 hello iSCSI 啟動器軟體 hello 主機上。</span><span class="sxs-lookup"><span data-stu-id="092b2-123">This authentication requires that you configure hello CHAP initiator settings on hello StorSimple device and hello iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="092b2-124">接下來說明 Windows 主機及 hello StorSimple 裝置的詳細程序。</span><span class="sxs-lookup"><span data-stu-id="092b2-124">hello detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a><span data-ttu-id="092b2-125">tooconfigure 單向驗證您的裝置</span><span class="sxs-lookup"><span data-stu-id="092b2-125">tooconfigure your device for one-way authentication</span></span>

1. <span data-ttu-id="092b2-126">在 hello Azure 入口網站，移 tooyour StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="092b2-126">In hello Azure portal, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="092b2-127">按一下**裝置**並選取，然後按一下您想 tooconfigure CHAP 裝置的。</span><span class="sxs-lookup"><span data-stu-id="092b2-127">Click **Devices** and select and click a device you wish tooconfigure CHAP for.</span></span> <span data-ttu-id="092b2-128">跳過**裝置設定 > 安全性**。</span><span class="sxs-lookup"><span data-stu-id="092b2-128">Go too**Device settings > Security**.</span></span> <span data-ttu-id="092b2-129">在 hello**安全性設定**刀鋒視窗中，按一下  **CHAP**。</span><span class="sxs-lookup"><span data-stu-id="092b2-129">In hello **Security settings** blade, click **CHAP**.</span></span>
   
    ![CHAP 啟動器](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="092b2-131">在 hello **CHAP**刀鋒視窗中，在 hello **CHAP 啟動器**> 一節：</span><span class="sxs-lookup"><span data-stu-id="092b2-131">In hello **CHAP** blade, and in hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="092b2-132">提供 CHAP 啟動器的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="092b2-132">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="092b2-133">提供 CHAP 啟動器的密碼。</span><span class="sxs-lookup"><span data-stu-id="092b2-133">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="092b2-134">hello CHAP 使用者名稱必須包含少於 233 個字元。</span><span class="sxs-lookup"><span data-stu-id="092b2-134">hello CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="092b2-135">hello CHAP 密碼必須介於 12 到 16 個字元。</span><span class="sxs-lookup"><span data-stu-id="092b2-135">hello CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="092b2-136">較長的使用者名稱或密碼會導致 hello Windows 主機上的驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="092b2-136">A longer user name or password results in an authentication failure on hello Windows host.</span></span>
   
   3. <span data-ttu-id="092b2-137">確認 hello 的密碼。</span><span class="sxs-lookup"><span data-stu-id="092b2-137">Confirm hello password.</span></span>

       ![CHAP 啟動器](./media/storsimple-8000-configure-chap/configure-chap6.png)
3. <span data-ttu-id="092b2-139">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="092b2-139">Click **Save**.</span></span> <span data-ttu-id="092b2-140">隨即顯示確認訊息。</span><span class="sxs-lookup"><span data-stu-id="092b2-140">A confirmation message is displayed.</span></span> <span data-ttu-id="092b2-141">按一下**確定**toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="092b2-141">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a><span data-ttu-id="092b2-142">tooconfigure hello Windows 上的單向驗證主機伺服器</span><span class="sxs-lookup"><span data-stu-id="092b2-142">tooconfigure one-way authentication on hello Windows host server</span></span>
1. <span data-ttu-id="092b2-143">Hello Windows 主機伺服器上，啟動 hello iSCSI 啟動器。</span><span class="sxs-lookup"><span data-stu-id="092b2-143">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="092b2-144">在 hello **iSCSI 啟動器屬性**視窗中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="092b2-144">In hello **iSCSI Initiator Properties** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="092b2-145">按一下 hello**探索** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="092b2-145">Click hello **Discovery** tab.</span></span>
      
       ![iSCSI 啟動器屬性](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="092b2-147">按一下 [探索入口網站] 。</span><span class="sxs-lookup"><span data-stu-id="092b2-147">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="092b2-148">在 hello**探索目標入口網站**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="092b2-148">In hello **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="092b2-149">指定您的裝置 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="092b2-149">Specify hello IP address of your device.</span></span>
   2. <span data-ttu-id="092b2-150">按一下 [進階] 。</span><span class="sxs-lookup"><span data-stu-id="092b2-150">Click **Advanced**.</span></span>
      
       ![探索目標入口網站](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="092b2-152">在 hello**進階設定**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="092b2-152">In hello **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="092b2-153">選取 hello**啟用 CHAP 登入**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="092b2-153">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="092b2-154">在 hello**名稱**欄位，您為 hello 傳統入口網站中的 hello CHAP 啟動器指定的供應 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="092b2-154">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="092b2-155">在 hello**目標密碼**欄位，您為 hello 傳統入口網站中的 hello CHAP 啟動器指定的供應 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="092b2-155">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="092b2-156">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="092b2-156">Click **OK**.</span></span>
      
       ![進階設定 - 一般](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="092b2-158">在 [hello**目標**hello] 索引標籤**iSCSI 啟動器屬性**hello 裝置狀態應顯示視窗中，為**已連接**。</span><span class="sxs-lookup"><span data-stu-id="092b2-158">On hello **Targets** tab of hello **iSCSI Initiator Properties** window, hello device status should appear as **Connected**.</span></span> <span data-ttu-id="092b2-159">如果您使用 StorSimple 1200 裝置，則每個磁碟區會掛接為 iSCSI 目標。</span><span class="sxs-lookup"><span data-stu-id="092b2-159">If you are using a StorSimple 1200 device, then each volume is mounted as an iSCSI target.</span></span> <span data-ttu-id="092b2-160">步驟 3-4，因此，需要 toobe 重複每個磁碟區。</span><span class="sxs-lookup"><span data-stu-id="092b2-160">Hence, steps 3-4 will need toobe repeated for each volume.</span></span>
   
    ![做為個別目標掛接的磁碟區](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="092b2-162">如果您變更 hello iSCSI 名稱，hello 新名稱會針對新的 iSCSI 工作階段。</span><span class="sxs-lookup"><span data-stu-id="092b2-162">If you change hello iSCSI name, hello new name is used for new iSCSI sessions.</span></span> <span data-ttu-id="092b2-163">您必須先登出再登入，現有的工作階段才會使用新的設定。</span><span class="sxs-lookup"><span data-stu-id="092b2-163">New settings are not used for existing sessions until you log off and log on again.</span></span>

<span data-ttu-id="092b2-164">如需 hello Windows 主機伺服器上設定 CHAP 的詳細資訊，請移至太[其他考量](#additional-considerations)。</span><span class="sxs-lookup"><span data-stu-id="092b2-164">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="092b2-165">雙向或相互驗證</span><span class="sxs-lookup"><span data-stu-id="092b2-165">Bidirectional or mutual authentication</span></span>

<span data-ttu-id="092b2-166">在雙向驗證 hello 目標驗證啟動器 hello，然後 hello 啟動器驗證目標 hello。</span><span class="sxs-lookup"><span data-stu-id="092b2-166">In bidirectional authentication, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="092b2-167">此程序需要 hello 使用者 tooconfigure hello CHAP 啟動器設定、 反向 CHAP 設定 hello 裝置和 iSCSI 啟動器軟體 hello 主機上。</span><span class="sxs-lookup"><span data-stu-id="092b2-167">This procedure requires hello user tooconfigure hello CHAP initiator settings, reverse CHAP settings on hello device, and iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="092b2-168">hello 下列程序說明 hello 步驟 tooconfigure 相互驗證 hello 裝置上和 hello Windows 主機上。</span><span class="sxs-lookup"><span data-stu-id="092b2-168">hello following procedures describe hello steps tooconfigure mutual authentication on hello device and on hello Windows host.</span></span>

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a><span data-ttu-id="092b2-169">tooconfigure 您的裝置進行相互驗證</span><span class="sxs-lookup"><span data-stu-id="092b2-169">tooconfigure your device for mutual authentication</span></span>

1. <span data-ttu-id="092b2-170">在 hello Azure 入口網站，移 tooyour StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="092b2-170">In hello Azure portal, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="092b2-171">按一下**裝置**並選取，然後按一下您想 tooconfigure CHAP 裝置的。</span><span class="sxs-lookup"><span data-stu-id="092b2-171">Click **Devices** and select and click a device you wish tooconfigure CHAP for.</span></span> <span data-ttu-id="092b2-172">跳過**裝置設定 > 安全性**。</span><span class="sxs-lookup"><span data-stu-id="092b2-172">Go too**Device settings > Security**.</span></span> <span data-ttu-id="092b2-173">在 hello**安全性設定**刀鋒視窗中，按一下  **CHAP**。</span><span class="sxs-lookup"><span data-stu-id="092b2-173">In hello **Security settings** blade, click **CHAP**.</span></span>
   
    ![CHAP 目標](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="092b2-175">向下捲動這個頁面上，然後在 hello **CHAP 目標**> 一節：</span><span class="sxs-lookup"><span data-stu-id="092b2-175">Scroll down on this page, and in hello **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="092b2-176">提供裝置的 [反向 CHAP 使用者名稱]  。</span><span class="sxs-lookup"><span data-stu-id="092b2-176">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="092b2-177">提供裝置的 [反向 CHAP 密碼]  。</span><span class="sxs-lookup"><span data-stu-id="092b2-177">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="092b2-178">確認 hello 的密碼。</span><span class="sxs-lookup"><span data-stu-id="092b2-178">Confirm hello password.</span></span>
3. <span data-ttu-id="092b2-179">在 hello **CHAP 啟動器**> 一節：</span><span class="sxs-lookup"><span data-stu-id="092b2-179">In hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="092b2-180">提供裝置的 [使用者名稱]  。</span><span class="sxs-lookup"><span data-stu-id="092b2-180">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="092b2-181">提供裝置的 [密碼]  。</span><span class="sxs-lookup"><span data-stu-id="092b2-181">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="092b2-182">確認 hello 的密碼。</span><span class="sxs-lookup"><span data-stu-id="092b2-182">Confirm hello password.</span></span>

       ![CHAP 啟動器](./media/storsimple-8000-configure-chap/configure-chap11.png)
4. <span data-ttu-id="092b2-184">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="092b2-184">Click **Save**.</span></span> <span data-ttu-id="092b2-185">隨即顯示確認訊息。</span><span class="sxs-lookup"><span data-stu-id="092b2-185">A confirmation message is displayed.</span></span> <span data-ttu-id="092b2-186">按一下**確定**toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="092b2-186">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a><span data-ttu-id="092b2-187">在 hello Windows tooconfigure 雙向驗證主機伺服器</span><span class="sxs-lookup"><span data-stu-id="092b2-187">tooconfigure bidirectional authentication on hello Windows host server</span></span>

1. <span data-ttu-id="092b2-188">Hello Windows 主機伺服器上，啟動 hello iSCSI 啟動器。</span><span class="sxs-lookup"><span data-stu-id="092b2-188">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="092b2-189">在 [hello **iSCSI 啟動器屬性**視窗中，按一下 hello**組態**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="092b2-189">In hello **iSCSI Initiator Properties** window, click hello **Configuration** tab.</span></span>
3. <span data-ttu-id="092b2-190">按一下 [CHAP] 。</span><span class="sxs-lookup"><span data-stu-id="092b2-190">Click **CHAP**.</span></span>
4. <span data-ttu-id="092b2-191">在 hello **iSCSI 啟動器相互 CHAP 密碼**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="092b2-191">In hello **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="092b2-192">型別 hello**反向 CHAP 密碼**hello Azure 入口網站中設定。</span><span class="sxs-lookup"><span data-stu-id="092b2-192">Type hello **Reverse CHAP Password** that you configured in hello Azure portal.</span></span>
   2. <span data-ttu-id="092b2-193">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="092b2-193">Click **OK**.</span></span>
      
       ![iSCSI 啟動器相互 CHAP 密碼](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="092b2-195">按一下 hello**目標** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="092b2-195">Click hello **Targets** tab.</span></span>
6. <span data-ttu-id="092b2-196">按一下 hello**連接** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="092b2-196">Click hello **Connect** button.</span></span> 
7. <span data-ttu-id="092b2-197">在 hello**連接 tooTarget**對話方塊中，按一下 **進階**。</span><span class="sxs-lookup"><span data-stu-id="092b2-197">In hello **Connect tooTarget** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="092b2-198">在 hello**進階屬性**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="092b2-198">In hello **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="092b2-199">選取 hello**啟用 CHAP 登入**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="092b2-199">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="092b2-200">在 hello**名稱**欄位，您為 hello 傳統入口網站中的 hello CHAP 啟動器指定的供應 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="092b2-200">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="092b2-201">在 hello**目標密碼**欄位，您為 hello 傳統入口網站中的 hello CHAP 啟動器指定的供應 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="092b2-201">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="092b2-202">選取 hello**執行相互驗證**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="092b2-202">Select hello **Perform mutual authentication** check box.</span></span>
      
       ![進階設定 - 相互驗證](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="092b2-204">按一下**確定**toocomplete hello CHAP 設定</span><span class="sxs-lookup"><span data-stu-id="092b2-204">Click **OK** toocomplete hello CHAP configuration</span></span>

<span data-ttu-id="092b2-205">如需 hello Windows 主機伺服器上設定 CHAP 的詳細資訊，請移至太[其他考量](#additional-considerations)。</span><span class="sxs-lookup"><span data-stu-id="092b2-205">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="092b2-206">其他考量</span><span class="sxs-lookup"><span data-stu-id="092b2-206">Additional considerations</span></span>

<span data-ttu-id="092b2-207">hello**快速連線**功能不支援已啟用 CHAP 的連線。</span><span class="sxs-lookup"><span data-stu-id="092b2-207">hello **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="092b2-208">啟用 CHAP 時，請確定您使用 hello**連接**按鈕上 hello**目標**標籤 tooconnect tooa 目標。</span><span class="sxs-lookup"><span data-stu-id="092b2-208">When CHAP is enabled, make sure that you use hello **Connect** button that is available on hello **Targets** tab tooconnect tooa target.</span></span>

![連接 tootarget](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="092b2-210">在 hello**連接 tooTarget**對話方塊會呈現，請選取 hello**新增我的最愛目標連線 toohello 清單**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="092b2-210">In hello **Connect tooTarget** dialog box that is presented, select hello **Add this connection toohello list of Favorite Targets** check box.</span></span> <span data-ttu-id="092b2-211">此選項可確保，每次 hello 電腦重新啟動，就會試著 toorestore hello 連接 toohello iSCSI 我的最愛目標。</span><span class="sxs-lookup"><span data-stu-id="092b2-211">This selection ensures that every time hello computer restarts, an attempt is made toorestore hello connection toohello iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="092b2-212">設定期間發生錯誤</span><span class="sxs-lookup"><span data-stu-id="092b2-212">Errors during configuration</span></span>

<span data-ttu-id="092b2-213">如果您的 CHAP 設定不正確，則您必須有可能 toosee**驗證失敗**錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="092b2-213">If your CHAP configuration is incorrect, then you are likely toosee an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="092b2-214">CHAP 設定的驗證</span><span class="sxs-lookup"><span data-stu-id="092b2-214">Verification of CHAP configuration</span></span>

<span data-ttu-id="092b2-215">您可以確認藉由完成下列步驟的 hello 使用 CHAP。</span><span class="sxs-lookup"><span data-stu-id="092b2-215">You can verify that CHAP is being used by completing hello following steps.</span></span>

#### <a name="tooverify-your-chap-configuration"></a><span data-ttu-id="092b2-216">tooverify 您的 CHAP 設定</span><span class="sxs-lookup"><span data-stu-id="092b2-216">tooverify your CHAP configuration</span></span>
1. <span data-ttu-id="092b2-217">按一下 [我的最愛目標] 。</span><span class="sxs-lookup"><span data-stu-id="092b2-217">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="092b2-218">選取您已啟用驗證的 hello 目標。</span><span class="sxs-lookup"><span data-stu-id="092b2-218">Select hello target for which you enabled authentication.</span></span>
3. <span data-ttu-id="092b2-219">按一下 [詳細資訊] 。</span><span class="sxs-lookup"><span data-stu-id="092b2-219">Click **Details**.</span></span>
   
    ![iSCSI 啟動器屬性 - 我的最愛目標](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="092b2-221">在 hello**我的最愛目標詳細資料**對話方塊中，注意 hello 項目在 hello**驗證**欄位。</span><span class="sxs-lookup"><span data-stu-id="092b2-221">In hello **Favorite Target Details** dialog box, note hello entry in hello **Authentication** field.</span></span> <span data-ttu-id="092b2-222">Hello 設定是否成功，它應該**CHAP**。</span><span class="sxs-lookup"><span data-stu-id="092b2-222">If hello configuration was successful, it should say **CHAP**.</span></span>
   
    ![我的最愛目標詳細資料](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="092b2-224">後續步驟</span><span class="sxs-lookup"><span data-stu-id="092b2-224">Next steps</span></span>

* <span data-ttu-id="092b2-225">深入了解 [StorSimple 安全性](storsimple-8000-security.md)。</span><span class="sxs-lookup"><span data-stu-id="092b2-225">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="092b2-226">深入了解[使用您的 StorSimple 裝置 hello StorSimple 裝置管理員服務 tooadminister](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="092b2-226">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>


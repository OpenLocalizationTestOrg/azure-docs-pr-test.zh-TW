---
title: "StorSimple 8000 系列裝置的 aaaConfigure CHAP |Microsoft 文件"
description: "描述如何 tooconfigure hello StorSimple 裝置上的 Challenge Handshake 驗證通訊協定 (CHAP)。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 467044d7-7885-4382-90bd-3148dbbd341f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 272ef2c184f56ad262e55410357494c72e45cf83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="df725-103">為 StorSimple 裝置設定 CHAP</span><span class="sxs-lookup"><span data-stu-id="df725-103">Configure CHAP for your StorSimple device</span></span>
<span data-ttu-id="df725-104">本教學課程說明如何 tooconfigure CHAP 您 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="df725-104">This tutorial explains how tooconfigure CHAP for your StorSimple device.</span></span> <span data-ttu-id="df725-105">此文件中詳述的 hello 程序適用於 tooStorSimple 8000 系列以及 StorSimple 1200 裝置。</span><span class="sxs-lookup"><span data-stu-id="df725-105">hello procedure detailed in this article applies tooStorSimple 8000 series as well as StorSimple 1200 devices.</span></span>

<span data-ttu-id="df725-106">CHAP 代表 Challenge Handshake 驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="df725-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="df725-107">它是伺服器 toovalidate hello 身分識別的遠端用戶端所使用的驗證配置。</span><span class="sxs-lookup"><span data-stu-id="df725-107">It is an authentication scheme used by servers toovalidate hello identity of remote clients.</span></span> <span data-ttu-id="df725-108">hello 驗證根據共用的密碼或密碼。</span><span class="sxs-lookup"><span data-stu-id="df725-108">hello verification is based on a shared password or secret.</span></span> <span data-ttu-id="df725-109">CHAP 可以是單向 (單向) 或相互 (雙向)。</span><span class="sxs-lookup"><span data-stu-id="df725-109">CHAP can be one-way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="df725-110">單向 CHAP 時，hello 目標驗證啟動器。</span><span class="sxs-lookup"><span data-stu-id="df725-110">One-way CHAP is when hello target authenticates an initiator.</span></span> <span data-ttu-id="df725-111">相互或反向 CHAP 時，在 hello 相反地，必須先 hello 目標驗證 hello 啟動器，再 hello 啟動器驗證目標 hello。</span><span class="sxs-lookup"><span data-stu-id="df725-111">Mutual or reverse CHAP, on hello other hand, requires that hello target authenticate hello initiator and then hello initiator authenticate hello target.</span></span> <span data-ttu-id="df725-112">不需要目標驗證也能實作啟動器驗證。</span><span class="sxs-lookup"><span data-stu-id="df725-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="df725-113">不過，必須同時實作啟動器驗證，才能實作目標驗證。</span><span class="sxs-lookup"><span data-stu-id="df725-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span> 

<span data-ttu-id="df725-114">最佳做法，我們建議您使用 CHAP tooenhance iSCSI 安全性。</span><span class="sxs-lookup"><span data-stu-id="df725-114">As a best practice, we recommend that you use CHAP tooenhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="df725-115">請記住，StorSimple 裝置目前不支援 IPSEC。</span><span class="sxs-lookup"><span data-stu-id="df725-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>
> 
> 

<span data-ttu-id="df725-116">hello hello StorSimple 裝置上的 CHAP 設定可以在 hello 下列方式設定：</span><span class="sxs-lookup"><span data-stu-id="df725-116">hello CHAP settings on hello StorSimple device can be configured in hello following ways:</span></span>

* <span data-ttu-id="df725-117">單向驗證</span><span class="sxs-lookup"><span data-stu-id="df725-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="df725-118">雙向、相互或反向驗證</span><span class="sxs-lookup"><span data-stu-id="df725-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="df725-119">在每個這種情況下，hello hello 裝置與 hello 伺服器 iSCSI 啟動器軟體的入口網站會需要 toobe 設定。</span><span class="sxs-lookup"><span data-stu-id="df725-119">In each of these cases, hello portal for hello device and hello server iSCSI initiator software needs toobe configured.</span></span> <span data-ttu-id="df725-120">hello 詳細的步驟，此組態中有描述 hello 教學課程。</span><span class="sxs-lookup"><span data-stu-id="df725-120">hello detailed steps for this configuration are described in hello following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="df725-121">單向驗證</span><span class="sxs-lookup"><span data-stu-id="df725-121">Unidirectional or one-way authentication</span></span>
<span data-ttu-id="df725-122">在單向驗證中，hello 目標驗證啟動器 hello。</span><span class="sxs-lookup"><span data-stu-id="df725-122">In unidirectional authentication, hello target authenticates hello initiator.</span></span> <span data-ttu-id="df725-123">此驗證，您必須設定 hello CHAP 啟動器設定 hello StorSimple 裝置和 hello iSCSI 啟動器軟體 hello 主機上。</span><span class="sxs-lookup"><span data-stu-id="df725-123">This authentication requires that you configure hello CHAP initiator settings on hello StorSimple device and hello iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="df725-124">接下來說明 Windows 主機及 hello StorSimple 裝置的詳細程序。</span><span class="sxs-lookup"><span data-stu-id="df725-124">hello detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a><span data-ttu-id="df725-125">tooconfigure 單向驗證您的裝置</span><span class="sxs-lookup"><span data-stu-id="df725-125">tooconfigure your device for one-way authentication</span></span>
1. <span data-ttu-id="df725-126">在 Azure 傳統入口網站，在 [hello hello**裝置**頁面上，按一下 hello**設定**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="df725-126">In hello Azure classic portal, on hello **Devices** page, click hello **Configure** tab.</span></span>
   
    ![CHAP 啟動器](./media/storsimple-configure-chap/IC740943.png)
2. <span data-ttu-id="df725-128">向下捲動這個頁面上，然後在 hello **CHAP 啟動器**> 一節：</span><span class="sxs-lookup"><span data-stu-id="df725-128">Scroll down on this page, and in hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="df725-129">提供 CHAP 啟動器的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="df725-129">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="df725-130">提供 CHAP 啟動器的密碼。</span><span class="sxs-lookup"><span data-stu-id="df725-130">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="df725-131">hello CHAP 使用者名稱必須包含少於 233 個字元。</span><span class="sxs-lookup"><span data-stu-id="df725-131">hello CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="df725-132">hello CHAP 密碼必須介於 12 到 16 個字元。</span><span class="sxs-lookup"><span data-stu-id="df725-132">hello CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="df725-133">較長的使用者名稱或密碼會導致 hello Windows 主機上的驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="df725-133">A longer user name or password will result in an authentication failure on hello Windows host.</span></span>
   
   3. <span data-ttu-id="df725-134">確認 hello 的密碼。</span><span class="sxs-lookup"><span data-stu-id="df725-134">Confirm hello password.</span></span>
3. <span data-ttu-id="df725-135">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="df725-135">Click **Save**.</span></span> <span data-ttu-id="df725-136">將顯示確認訊息。</span><span class="sxs-lookup"><span data-stu-id="df725-136">A confirmation message will be displayed.</span></span> <span data-ttu-id="df725-137">按一下**確定**toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="df725-137">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a><span data-ttu-id="df725-138">tooconfigure hello Windows 上的單向驗證主機伺服器</span><span class="sxs-lookup"><span data-stu-id="df725-138">tooconfigure one-way authentication on hello Windows host server</span></span>
1. <span data-ttu-id="df725-139">Hello Windows 主機伺服器上，啟動 hello iSCSI 啟動器。</span><span class="sxs-lookup"><span data-stu-id="df725-139">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="df725-140">在 hello **iSCSI 啟動器屬性**視窗中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="df725-140">In hello **iSCSI Initiator Properties** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="df725-141">按一下 hello**探索** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="df725-141">Click hello **Discovery** tab.</span></span>
      
       ![iSCSI 啟動器屬性](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="df725-143">按一下 [探索入口網站] 。</span><span class="sxs-lookup"><span data-stu-id="df725-143">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="df725-144">在 hello**探索目標入口網站**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="df725-144">In hello **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="df725-145">指定您的裝置 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="df725-145">Specify hello IP address of your device.</span></span>
   2. <span data-ttu-id="df725-146">按一下 [進階] 。</span><span class="sxs-lookup"><span data-stu-id="df725-146">Click **Advanced**.</span></span>
      
       ![探索目標入口網站](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="df725-148">在 hello**進階設定**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="df725-148">In hello **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="df725-149">選取 hello**啟用 CHAP 登入**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="df725-149">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="df725-150">在 hello**名稱**欄位，您為 hello 傳統入口網站中的 hello CHAP 啟動器指定的供應 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="df725-150">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="df725-151">在 hello**目標密碼**欄位，您為 hello 傳統入口網站中的 hello CHAP 啟動器指定的供應 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="df725-151">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="df725-152">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="df725-152">Click **OK**.</span></span>
      
       ![進階設定 - 一般](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="df725-154">在 [hello**目標**hello] 索引標籤**iSCSI 啟動器屬性**hello 裝置狀態應顯示視窗中，為**已連接**。</span><span class="sxs-lookup"><span data-stu-id="df725-154">On hello **Targets** tab of hello **iSCSI Initiator Properties** window, hello device status should appear as **Connected**.</span></span> <span data-ttu-id="df725-155">如果您使用 StorSimple 1200 裝置，則每個磁碟區將可掛接為 iSCSI 目標，如下所示。</span><span class="sxs-lookup"><span data-stu-id="df725-155">If you are using a StorSimple 1200 device, then each volume will be mounted as an iSCSI target as shown below.</span></span> <span data-ttu-id="df725-156">步驟 3-4，因此，需要 toobe 重複每個磁碟區。</span><span class="sxs-lookup"><span data-stu-id="df725-156">Hence, steps  3-4 will need toobe repeated for each volume.</span></span>
   
    ![做為個別目標掛接的磁碟區](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="df725-158">如果您變更 hello iSCSI 名稱，則會使用 hello 新名稱，新的 iSCSI 工作階段。</span><span class="sxs-lookup"><span data-stu-id="df725-158">If you change hello iSCSI name, hello new name will be used for new iSCSI sessions.</span></span> <span data-ttu-id="df725-159">您必須先登出再登入，現有的工作階段才會使用新的設定。</span><span class="sxs-lookup"><span data-stu-id="df725-159">New settings are not used for existing sessions until you log off and log on again.</span></span>
   > 
   > 

<span data-ttu-id="df725-160">如需 hello Windows 主機伺服器上設定 CHAP 的詳細資訊，請移至太[其他考量](#additional-considerations)。</span><span class="sxs-lookup"><span data-stu-id="df725-160">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="df725-161">雙向或相互驗證</span><span class="sxs-lookup"><span data-stu-id="df725-161">Bidirectional or mutual authentication</span></span>
<span data-ttu-id="df725-162">在雙向驗證 hello 目標驗證啟動器 hello，然後 hello 啟動器驗證目標 hello。</span><span class="sxs-lookup"><span data-stu-id="df725-162">In bidirectional authentication, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="df725-163">這需要 hello 使用者 tooconfigure hello CHAP 啟動器設定，以及 hello 反向 CHAP 設定 hello 裝置和 iSCSI 啟動器軟體 hello 主機上。</span><span class="sxs-lookup"><span data-stu-id="df725-163">This requires hello user tooconfigure hello CHAP initiator settings, as well as hello reverse CHAP settings on hello device and iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="df725-164">hello 下列程序說明 hello 步驟 tooconfigure 相互驗證 hello 裝置上和 hello Windows 主機上。</span><span class="sxs-lookup"><span data-stu-id="df725-164">hello following procedures describe hello steps tooconfigure mutual authentication on hello device and on hello Windows host.</span></span>

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a><span data-ttu-id="df725-165">tooconfigure 您的裝置進行相互驗證</span><span class="sxs-lookup"><span data-stu-id="df725-165">tooconfigure your device for mutual authentication</span></span>
1. <span data-ttu-id="df725-166">在 Azure 傳統入口網站，在 [hello hello**裝置**頁面上，按一下 hello**設定**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="df725-166">In hello Azure classic portal, on hello **Devices** page, click hello **Configure** tab.</span></span>
   
    ![CHAP 目標](./media/storsimple-configure-chap/IC740948.png)
2. <span data-ttu-id="df725-168">向下捲動這個頁面上，然後在 hello **CHAP 目標**> 一節：</span><span class="sxs-lookup"><span data-stu-id="df725-168">Scroll down on this page, and in hello **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="df725-169">提供裝置的 [反向 CHAP 使用者名稱]  。</span><span class="sxs-lookup"><span data-stu-id="df725-169">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="df725-170">提供裝置的 [反向 CHAP 密碼]  。</span><span class="sxs-lookup"><span data-stu-id="df725-170">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="df725-171">確認 hello 的密碼。</span><span class="sxs-lookup"><span data-stu-id="df725-171">Confirm hello password.</span></span>
3. <span data-ttu-id="df725-172">在 hello **CHAP 啟動器**> 一節：</span><span class="sxs-lookup"><span data-stu-id="df725-172">In hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="df725-173">提供裝置的 [使用者名稱]  。</span><span class="sxs-lookup"><span data-stu-id="df725-173">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="df725-174">提供裝置的 [密碼]  。</span><span class="sxs-lookup"><span data-stu-id="df725-174">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="df725-175">確認 hello 的密碼。</span><span class="sxs-lookup"><span data-stu-id="df725-175">Confirm hello password.</span></span>
4. <span data-ttu-id="df725-176">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="df725-176">Click **Save**.</span></span> <span data-ttu-id="df725-177">將顯示確認訊息。</span><span class="sxs-lookup"><span data-stu-id="df725-177">A confirmation message will be displayed.</span></span> <span data-ttu-id="df725-178">按一下**確定**toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="df725-178">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a><span data-ttu-id="df725-179">在 hello Windows tooconfigure 雙向驗證主機伺服器</span><span class="sxs-lookup"><span data-stu-id="df725-179">tooconfigure bidirectional authentication on hello Windows host server</span></span>
1. <span data-ttu-id="df725-180">Hello Windows 主機伺服器上，啟動 hello iSCSI 啟動器。</span><span class="sxs-lookup"><span data-stu-id="df725-180">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="df725-181">在 [hello **iSCSI 啟動器屬性**視窗中，按一下 hello**組態**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="df725-181">In hello **iSCSI Initiator Properties** window, click hello **Configuration** tab.</span></span>
3. <span data-ttu-id="df725-182">按一下 [CHAP] 。</span><span class="sxs-lookup"><span data-stu-id="df725-182">Click **CHAP**.</span></span>
4. <span data-ttu-id="df725-183">在 hello **iSCSI 啟動器相互 CHAP 密碼**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="df725-183">In hello **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="df725-184">型別 hello**反向 CHAP 密碼**hello Azure 傳統入口網站中設定。</span><span class="sxs-lookup"><span data-stu-id="df725-184">Type hello **Reverse CHAP Password** that you configured in hello Azure classic portal.</span></span>
   2. <span data-ttu-id="df725-185">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="df725-185">Click **OK**.</span></span>
      
       ![iSCSI 啟動器相互 CHAP 密碼](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="df725-187">按一下 hello**目標** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="df725-187">Click hello **Targets** tab.</span></span>
6. <span data-ttu-id="df725-188">按一下 hello**連接** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="df725-188">Click hello **Connect** button.</span></span> 
7. <span data-ttu-id="df725-189">在 hello**連接 tooTarget**對話方塊中，按一下 **進階**。</span><span class="sxs-lookup"><span data-stu-id="df725-189">In hello **Connect tooTarget** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="df725-190">在 hello**進階屬性**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="df725-190">In hello **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="df725-191">選取 hello**啟用 CHAP 登入**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="df725-191">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="df725-192">在 hello**名稱**欄位，您為 hello 傳統入口網站中的 hello CHAP 啟動器指定的供應 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="df725-192">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="df725-193">在 hello**目標密碼**欄位，您為 hello 傳統入口網站中的 hello CHAP 啟動器指定的供應 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="df725-193">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="df725-194">選取 hello**執行相互驗證**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="df725-194">Select hello **Perform mutual authentication** check box.</span></span>
      
       ![進階設定 - 相互驗證](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="df725-196">按一下**確定**toocomplete hello CHAP 設定</span><span class="sxs-lookup"><span data-stu-id="df725-196">Click **OK** toocomplete hello CHAP configuration</span></span>

<span data-ttu-id="df725-197">如需 hello Windows 主機伺服器上設定 CHAP 的詳細資訊，請移至太[其他考量](#additional-considerations)。</span><span class="sxs-lookup"><span data-stu-id="df725-197">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="df725-198">其他考量</span><span class="sxs-lookup"><span data-stu-id="df725-198">Additional considerations</span></span>
<span data-ttu-id="df725-199">hello**快速連線**功能不支援已啟用 CHAP 的連線。</span><span class="sxs-lookup"><span data-stu-id="df725-199">hello **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="df725-200">啟用 CHAP 時，請確定您使用 hello**連接**按鈕上 hello**目標**標籤 tooconnect tooa 目標。</span><span class="sxs-lookup"><span data-stu-id="df725-200">When CHAP is enabled, make sure that you use hello **Connect** button that is available on hello **Targets** tab tooconnect tooa target.</span></span>

![連接 tootarget](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="df725-202">在 hello**連接 tooTarget**對話方塊會呈現，請選取 hello**新增我的最愛目標連線 toohello 清單**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="df725-202">In hello **Connect tooTarget** dialog box that is presented, select hello **Add this connection toohello list of Favorite Targets** check box.</span></span> <span data-ttu-id="df725-203">這可確保，每次 hello 電腦重新啟動，就會試著 toorestore hello 連接 toohello iSCSI 我的最愛目標。</span><span class="sxs-lookup"><span data-stu-id="df725-203">This ensures that every time hello computer restarts, an attempt is made toorestore hello connection toohello iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="df725-204">設定期間發生錯誤</span><span class="sxs-lookup"><span data-stu-id="df725-204">Errors during configuration</span></span>
<span data-ttu-id="df725-205">如果您的 CHAP 設定不正確，則您必須有可能 toosee**驗證失敗**錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="df725-205">If your CHAP configuration is incorrect, then you are likely toosee an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="df725-206">CHAP 設定的驗證</span><span class="sxs-lookup"><span data-stu-id="df725-206">Verification of CHAP configuration</span></span>
<span data-ttu-id="df725-207">您可以確認藉由完成下列步驟的 hello 使用 CHAP。</span><span class="sxs-lookup"><span data-stu-id="df725-207">You can verify that CHAP is being used by completing hello following steps.</span></span>

#### <a name="tooverify-your-chap-configuration"></a><span data-ttu-id="df725-208">tooverify 您的 CHAP 設定</span><span class="sxs-lookup"><span data-stu-id="df725-208">tooverify your CHAP configuration</span></span>
1. <span data-ttu-id="df725-209">按一下 [我的最愛目標] 。</span><span class="sxs-lookup"><span data-stu-id="df725-209">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="df725-210">選取您已啟用驗證的 hello 目標。</span><span class="sxs-lookup"><span data-stu-id="df725-210">Select hello target for which you enabled authentication.</span></span>
3. <span data-ttu-id="df725-211">按一下 [詳細資訊] 。</span><span class="sxs-lookup"><span data-stu-id="df725-211">Click **Details**.</span></span>
   
    ![iSCSI 啟動器屬性 - 我的最愛目標](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="df725-213">在 hello**我的最愛目標詳細資料**對話方塊中，注意 hello 項目在 hello**驗證**欄位。</span><span class="sxs-lookup"><span data-stu-id="df725-213">In hello **Favorite Target Details** dialog box, note hello entry in hello **Authentication** field.</span></span> <span data-ttu-id="df725-214">Hello 設定是否成功，它應該**CHAP**。</span><span class="sxs-lookup"><span data-stu-id="df725-214">If hello configuration was successful, it should say **CHAP**.</span></span>
   
    ![我的最愛目標詳細資料](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="df725-216">後續步驟</span><span class="sxs-lookup"><span data-stu-id="df725-216">Next steps</span></span>
* <span data-ttu-id="df725-217">深入了解 [StorSimple 安全性](storsimple-security.md)。</span><span class="sxs-lookup"><span data-stu-id="df725-217">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="df725-218">深入了解[使用您的 StorSimple 裝置 hello StorSimple Manager 服務 tooadminister](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="df725-218">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>


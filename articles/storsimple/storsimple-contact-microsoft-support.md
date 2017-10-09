---
title: "aaaLog StorSimple 8000 系列的支援票證 |Microsoft 文件"
description: "了解如何 toocreate 支援要求並啟動您的 StorSimple 裝置上的支援工作階段。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e1a3aa3c56e036c782c4fb502c477dc0feaa0ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a><span data-ttu-id="a0d80-103">連絡 Microsoft 支援服務以解決 StorSimple 問題</span><span class="sxs-lookup"><span data-stu-id="a0d80-103">Contact Microsoft Support for your StorSimple</span></span>
<span data-ttu-id="a0d80-104">如果您使用 Microsoft Azure StorSimple 解決方案時遇到任何問題，您可以向技術支援人員提出服務要求。</span><span class="sxs-lookup"><span data-stu-id="a0d80-104">If you encounter any issues with your Microsoft Azure StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="a0d80-105">在線上工作階段與支援工程師，您也可能需要支援工作階段的 toostart StorSimple 裝置上。</span><span class="sxs-lookup"><span data-stu-id="a0d80-105">In an online session with your support engineer, you may also need toostart a support session on your StorSimple device.</span></span> <span data-ttu-id="a0d80-106">本文將引導您：</span><span class="sxs-lookup"><span data-stu-id="a0d80-106">This article walks you through:</span></span>

* <span data-ttu-id="a0d80-107">Toocreate 支援的要求。</span><span class="sxs-lookup"><span data-stu-id="a0d80-107">How toocreate a support request.</span></span>
* <span data-ttu-id="a0d80-108">如何支援工作階段中 toostart hello 您的 StorSimple 裝置的 Windows PowerShell 介面。</span><span class="sxs-lookup"><span data-stu-id="a0d80-108">How toostart a support session in hello Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="a0d80-109">檢閱 hello [StorSimple 8000 系列支援 Sla 和資訊](https://msdn.microsoft.com/library/mt433077.aspx)建立支援要求之前。</span><span class="sxs-lookup"><span data-stu-id="a0d80-109">Review hello [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="a0d80-110">建立支援要求</span><span class="sxs-lookup"><span data-stu-id="a0d80-110">Create a support request</span></span>
<span data-ttu-id="a0d80-111">執行下列步驟 toocreate 支援要求的 hello:</span><span class="sxs-lookup"><span data-stu-id="a0d80-111">Perform hello following steps toocreate a support request:</span></span>

#### <a name="toocreate-a-support-request"></a><span data-ttu-id="a0d80-112">toocreate 支援要求</span><span class="sxs-lookup"><span data-stu-id="a0d80-112">toocreate a support request</span></span>
1. <span data-ttu-id="a0d80-113">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)hello 右上角，按一下您的帳戶名稱，然後按**請連絡 Microsoft 支援**。</span><span class="sxs-lookup"><span data-stu-id="a0d80-113">In hello [Azure classic portal](https://manage.windowsazure.com/), in hello upper right corner, click your account name and then click **Contact Microsoft Support**.</span></span>
   
    ![透過 ManagementPortal 連絡 MS 支援服務](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. <span data-ttu-id="a0d80-115">您將會重新導向的 toohello 新版 Azure 入口網站 (portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a0d80-115">You will be redirected toohello new Azure portal (portal.azure.com).</span></span> <span data-ttu-id="a0d80-116">按一下 hello**新增支援要求**磚。</span><span class="sxs-lookup"><span data-stu-id="a0d80-116">Click hello **New support request** tile.</span></span>
   
    ![透過新的入口網站連絡 MS 支援服務](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    <span data-ttu-id="a0d80-118">右側 hello 囉 」 畫面，hello**新增支援要求** 窗格隨即出現。</span><span class="sxs-lookup"><span data-stu-id="a0d80-118">On hello right side of hello screen, hello **New support request** pane appears.</span></span> 
   
    ![新的支援要求窗格](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. <span data-ttu-id="a0d80-120">在 hello**基本概念**對話方塊中，下列的完整 hello:</span><span class="sxs-lookup"><span data-stu-id="a0d80-120">In hello **Basics** dialog box, complete hello following:</span></span>                                
   
   1. <span data-ttu-id="a0d80-121">從 hello**發出型別**下拉式清單中，選取**技術**。</span><span class="sxs-lookup"><span data-stu-id="a0d80-121">From hello **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="a0d80-122">選取**訂用帳戶**hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="a0d80-122">Select a **Subscription** from hello drop-down list.</span></span>
   3. <span data-ttu-id="a0d80-123">從 hello**服務**下拉式清單中，選取**StorSimple**。</span><span class="sxs-lookup"><span data-stu-id="a0d80-123">From hello **Service** drop-down list, select **StorSimple**.</span></span> 
   4. <span data-ttu-id="a0d80-124">選取**支援計劃**hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="a0d80-124">Select a **Support plan** from hello drop-down list.</span></span> <span data-ttu-id="a0d80-125">您需要付費的支援計劃 tooenable 技術支援。</span><span class="sxs-lookup"><span data-stu-id="a0d80-125">You need a paid support plan tooenable Technical Support.</span></span>
4. <span data-ttu-id="a0d80-126">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a0d80-126">Click **Next**.</span></span> <span data-ttu-id="a0d80-127">hello**問題** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="a0d80-127">hello **Problem** dialog box appears.</span></span>
   
    ![新的支援要求窗格](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. <span data-ttu-id="a0d80-129">在 hello**問題**對話方塊中，下列的完整 hello:</span><span class="sxs-lookup"><span data-stu-id="a0d80-129">In hello **Problem** dialog box, complete hello following:</span></span>
   
   1. <span data-ttu-id="a0d80-130">選取**嚴重性**hello 下拉式清單中的層級。</span><span class="sxs-lookup"><span data-stu-id="a0d80-130">Select a **Severity** level from hello drop-down list.</span></span>
   2. <span data-ttu-id="a0d80-131">選取**問題類型**hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="a0d80-131">Select a **Problem type** from hello drop-down list.</span></span>
   3. <span data-ttu-id="a0d80-132">選取**類別**hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="a0d80-132">Select a **Category** from hello drop-down list.</span></span> 
   4. <span data-ttu-id="a0d80-133">在 hello**詳細資料**方塊中，簡要描述您的問題。</span><span class="sxs-lookup"><span data-stu-id="a0d80-133">In hello **Details** box, briefly describe your issue.</span></span>
   5. <span data-ttu-id="a0d80-134">在 hello**時間範圍**方塊中，表示 hello 日期、 時間和時區對應 toohello 最近發生的問題。</span><span class="sxs-lookup"><span data-stu-id="a0d80-134">In hello **Time frame** box, indicate hello date, time, and time zone that corresponds toohello most recent occurrence of your issue.</span></span>
   6. <span data-ttu-id="a0d80-135">在下**檔案上傳**，按一下 hello 資料夾圖示 toobrowse tooyour 支援封裝。</span><span class="sxs-lookup"><span data-stu-id="a0d80-135">Under **File upload**, click hello folder icon toobrowse tooyour support package.</span></span>
   7. <span data-ttu-id="a0d80-136">選取 hello**共用診斷資訊**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a0d80-136">Select hello **Share diagnostic information** check box.</span></span>
6. <span data-ttu-id="a0d80-137">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a0d80-137">Click **Next**.</span></span> <span data-ttu-id="a0d80-138">hello**連絡資訊** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="a0d80-138">hello **Contact information** dialog box appears.</span></span>
   
    ![新的支援要求窗格](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. <span data-ttu-id="a0d80-140">輸入您的連絡資訊，並選取一個連絡方法 (電話或電子郵件)。</span><span class="sxs-lookup"><span data-stu-id="a0d80-140">Enter your contact information and select a contact method (phone or email).</span></span> 
8. <span data-ttu-id="a0d80-141">選取 hello**儲存連絡人變更，以供後續支援要求**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a0d80-141">Select hello **Save contact changes for future support requests** check box.</span></span>
9. <span data-ttu-id="a0d80-142">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a0d80-142">Click **Create**.</span></span>

<span data-ttu-id="a0d80-143">提交您的要求之後，支援工程師會與您連絡儘速 tooproceed 您的要求。</span><span class="sxs-lookup"><span data-stu-id="a0d80-143">After you have submitted your request, a Support engineer will contact you as soon as possible tooproceed with your request.</span></span>

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="a0d80-144">在 Windows PowerShell for StorSimple 中啟動支援工作階段</span><span class="sxs-lookup"><span data-stu-id="a0d80-144">Start a support session in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="a0d80-145">tootroubleshoot 所有問題，您可能會遇到與 hello StorSimple 裝置，您將需要 tooengage 與 hello Microsoft 技術支援小組。</span><span class="sxs-lookup"><span data-stu-id="a0d80-145">tootroubleshoot any issues that you might experience with hello StorSimple device, you will need tooengage with hello Microsoft Support team.</span></span> <span data-ttu-id="a0d80-146">Microsoft 支援服務可能需要 toouse 支援工作階段 toolog tooyour 裝置上。</span><span class="sxs-lookup"><span data-stu-id="a0d80-146">Microsoft Support may need toouse a support session toolog on tooyour device.</span></span> 

<span data-ttu-id="a0d80-147">執行下列 hello toostart 支援工作階段的步驟：</span><span class="sxs-lookup"><span data-stu-id="a0d80-147">Perform hello following steps toostart a support session:</span></span>

#### <a name="toostart-a-support-session"></a><span data-ttu-id="a0d80-148">toostart 支援工作階段</span><span class="sxs-lookup"><span data-stu-id="a0d80-148">toostart a support session</span></span>
1. <span data-ttu-id="a0d80-149">存取 hello 裝置直接使用 hello 序列主控台或透過 telnet 工作階段從遠端電腦。</span><span class="sxs-lookup"><span data-stu-id="a0d80-149">Access hello device directly by using hello serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="a0d80-150">toodo 中的，遵循 hello 步驟[使用 PuTTY tooconnect toohello 裝置序列主控台](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)。</span><span class="sxs-lookup"><span data-stu-id="a0d80-150">toodo this, follow hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="a0d80-151">在開啟的 hello 工作階段，請按 hello **Enter**金鑰 tooget 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="a0d80-151">In hello session that opens, press hello **Enter** key tooget a command prompt.</span></span>
3. <span data-ttu-id="a0d80-152">在 hello 序列主控台功能表中，選取選項 1，**登入的完整存取**。</span><span class="sxs-lookup"><span data-stu-id="a0d80-152">In hello serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="a0d80-153">在 hello 提示字元中輸入下列密碼 hello:</span><span class="sxs-lookup"><span data-stu-id="a0d80-153">At hello prompt, type hello following password:</span></span> 
   
    `Password1`
5. <span data-ttu-id="a0d80-154">在 hello 提示字元中輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a0d80-154">At hello prompt, type hello following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="a0d80-155">加密的字串將會出現 tooyou。</span><span class="sxs-lookup"><span data-stu-id="a0d80-155">An encrypted string will be presented tooyou.</span></span> <span data-ttu-id="a0d80-156">將此字串複製到 [記事本] 之類的文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="a0d80-156">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="a0d80-157">儲存這個字串，並將它傳送電子郵件訊息 tooMicrosoft 支援。</span><span class="sxs-lookup"><span data-stu-id="a0d80-157">Save this string and send it in an email message tooMicrosoft Support.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="a0d80-158">您可以執行 `Disable-HcsSupportAccess` 來停用支援存取。</span><span class="sxs-lookup"><span data-stu-id="a0d80-158">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="a0d80-159">hello StorSimple 裝置也會嘗試 toodisable 支援服務存取 8 小時 hello 工作階段起始後。</span><span class="sxs-lookup"><span data-stu-id="a0d80-159">hello StorSimple device will also attempt toodisable support access 8 hours after hello session was initiated.</span></span> <span data-ttu-id="a0d80-160">啟動支援工作階段後認證您的 StorSimple 裝置的最佳作法 toochange 它。</span><span class="sxs-lookup"><span data-stu-id="a0d80-160">It is a best practice toochange your StorSimple device credentials after initiating a support session.</span></span>
> 
> 


---
title: "針對 StorSimple 8000 系列記錄支援票證 | Microsoft Docs"
description: "了解如何建立支援要求和在 StorSimple 裝置上啟動支援工作階段。"
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
ms.openlocfilehash: cecc2566b432e897b5eff0c12e66598f0518ed80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a><span data-ttu-id="16cbd-103">連絡 Microsoft 支援服務以解決 StorSimple 問題</span><span class="sxs-lookup"><span data-stu-id="16cbd-103">Contact Microsoft Support for your StorSimple</span></span>
<span data-ttu-id="16cbd-104">如果您使用 Microsoft Azure StorSimple 解決方案時遇到任何問題，您可以向技術支援人員提出服務要求。</span><span class="sxs-lookup"><span data-stu-id="16cbd-104">If you encounter any issues with your Microsoft Azure StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="16cbd-105">在與支援工程師進行線上工作階段時，可能也需要在您的 StorSimple 裝置上啟動支援工作階段。</span><span class="sxs-lookup"><span data-stu-id="16cbd-105">In an online session with your support engineer, you may also need to start a support session on your StorSimple device.</span></span> <span data-ttu-id="16cbd-106">本文將引導您：</span><span class="sxs-lookup"><span data-stu-id="16cbd-106">This article walks you through:</span></span>

* <span data-ttu-id="16cbd-107">如何建立支援要求。</span><span class="sxs-lookup"><span data-stu-id="16cbd-107">How to create a support request.</span></span>
* <span data-ttu-id="16cbd-108">如何在 StorSimple 裝置的 Windows PowerShell 介面中啟動支援工作階段。</span><span class="sxs-lookup"><span data-stu-id="16cbd-108">How to start a support session in the Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="16cbd-109">建立支援要求之前，請先檢閱 [StorSimple 8000 系列支援 SLA 和資訊](https://msdn.microsoft.com/library/mt433077.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="16cbd-109">Review the [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="16cbd-110">建立支援要求</span><span class="sxs-lookup"><span data-stu-id="16cbd-110">Create a support request</span></span>
<span data-ttu-id="16cbd-111">執行下列步驟來建立支援要求：</span><span class="sxs-lookup"><span data-stu-id="16cbd-111">Perform the following steps to create a support request:</span></span>

#### <a name="to-create-a-support-request"></a><span data-ttu-id="16cbd-112">建立支援要求</span><span class="sxs-lookup"><span data-stu-id="16cbd-112">To create a support request</span></span>
1. <span data-ttu-id="16cbd-113">在 [Azure 傳統入口網站](https://manage.windowsazure.com/)的右上角，依序按一下您的帳戶名稱和 [連絡 Microsoft 支援服務]。</span><span class="sxs-lookup"><span data-stu-id="16cbd-113">In the [Azure classic portal](https://manage.windowsazure.com/), in the upper right corner, click your account name and then click **Contact Microsoft Support**.</span></span>
   
    ![透過 ManagementPortal 連絡 MS 支援服務](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. <span data-ttu-id="16cbd-115">系統便會將您重新導向至新的 Azure 入口網站 (portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="16cbd-115">You will be redirected to the new Azure portal (portal.azure.com).</span></span> <span data-ttu-id="16cbd-116">按一下 [新的支援要求]  磚。</span><span class="sxs-lookup"><span data-stu-id="16cbd-116">Click the **New support request** tile.</span></span>
   
    ![透過新的入口網站連絡 MS 支援服務](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    <span data-ttu-id="16cbd-118">畫面右側則會出現 [新的支援要求]  窗格。</span><span class="sxs-lookup"><span data-stu-id="16cbd-118">On the right side of the screen, the **New support request** pane appears.</span></span> 
   
    ![新的支援要求窗格](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. <span data-ttu-id="16cbd-120">在 [基本資料]  對話方塊中，完成下列操作：</span><span class="sxs-lookup"><span data-stu-id="16cbd-120">In the **Basics** dialog box, complete the following:</span></span>                                
   
   1. <span data-ttu-id="16cbd-121">從 [問題類型] 下拉式清單中，選取 [技術]。</span><span class="sxs-lookup"><span data-stu-id="16cbd-121">From the **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="16cbd-122">從下拉式清單中，選取 [訂用帳戶]  。</span><span class="sxs-lookup"><span data-stu-id="16cbd-122">Select a **Subscription** from the drop-down list.</span></span>
   3. <span data-ttu-id="16cbd-123">從 [服務] 下拉式清單中，選取 [StorSimple]。</span><span class="sxs-lookup"><span data-stu-id="16cbd-123">From the **Service** drop-down list, select **StorSimple**.</span></span> 
   4. <span data-ttu-id="16cbd-124">從下拉式清單中，選取 [支援方案]  。</span><span class="sxs-lookup"><span data-stu-id="16cbd-124">Select a **Support plan** from the drop-down list.</span></span> <span data-ttu-id="16cbd-125">您必須已付費購買支援方案，才能啟用技術支援。</span><span class="sxs-lookup"><span data-stu-id="16cbd-125">You need a paid support plan to enable Technical Support.</span></span>
4. <span data-ttu-id="16cbd-126">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="16cbd-126">Click **Next**.</span></span> <span data-ttu-id="16cbd-127">[問題]  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="16cbd-127">The **Problem** dialog box appears.</span></span>
   
    ![新的支援要求窗格](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. <span data-ttu-id="16cbd-129">在 [問題]  對話方塊中，完成下列操作：</span><span class="sxs-lookup"><span data-stu-id="16cbd-129">In the **Problem** dialog box, complete the following:</span></span>
   
   1. <span data-ttu-id="16cbd-130">從下拉式清單中，選取 [嚴重性]  層級。</span><span class="sxs-lookup"><span data-stu-id="16cbd-130">Select a **Severity** level from the drop-down list.</span></span>
   2. <span data-ttu-id="16cbd-131">從下拉式清單中，選取 [問題類型]  。</span><span class="sxs-lookup"><span data-stu-id="16cbd-131">Select a **Problem type** from the drop-down list.</span></span>
   3. <span data-ttu-id="16cbd-132">從下拉式清單中，選取 [類別]  。</span><span class="sxs-lookup"><span data-stu-id="16cbd-132">Select a **Category** from the drop-down list.</span></span> 
   4. <span data-ttu-id="16cbd-133">在 [詳細資料]  方塊中，簡短描述您的問題。</span><span class="sxs-lookup"><span data-stu-id="16cbd-133">In the **Details** box, briefly describe your issue.</span></span>
   5. <span data-ttu-id="16cbd-134">在 [時間範圍]  方塊中，指出對應到最近發生問題的日期、時間和時區。</span><span class="sxs-lookup"><span data-stu-id="16cbd-134">In the **Time frame** box, indicate the date, time, and time zone that corresponds to the most recent occurrence of your issue.</span></span>
   6. <span data-ttu-id="16cbd-135">在 [檔案上傳] 底下，按一下資料夾圖示，即可瀏覽至您的支援封裝。</span><span class="sxs-lookup"><span data-stu-id="16cbd-135">Under **File upload**, click the folder icon to browse to your support package.</span></span>
   7. <span data-ttu-id="16cbd-136">選取 [共用診斷資訊]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="16cbd-136">Select the **Share diagnostic information** check box.</span></span>
6. <span data-ttu-id="16cbd-137">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="16cbd-137">Click **Next**.</span></span> <span data-ttu-id="16cbd-138">[連絡資訊]  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="16cbd-138">The **Contact information** dialog box appears.</span></span>
   
    ![新的支援要求窗格](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. <span data-ttu-id="16cbd-140">輸入您的連絡資訊，並選取一個連絡方法 (電話或電子郵件)。</span><span class="sxs-lookup"><span data-stu-id="16cbd-140">Enter your contact information and select a contact method (phone or email).</span></span> 
8. <span data-ttu-id="16cbd-141">選取 [儲存連絡人變更以供未來的支援要求使用]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="16cbd-141">Select the **Save contact changes for future support requests** check box.</span></span>
9. <span data-ttu-id="16cbd-142">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="16cbd-142">Click **Create**.</span></span>

<span data-ttu-id="16cbd-143">提交您的要求之後，支援工程師會儘速連絡您來處理您的要求。</span><span class="sxs-lookup"><span data-stu-id="16cbd-143">After you have submitted your request, a Support engineer will contact you as soon as possible to proceed with your request.</span></span>

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="16cbd-144">在 Windows PowerShell for StorSimple 中啟動支援工作階段</span><span class="sxs-lookup"><span data-stu-id="16cbd-144">Start a support session in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="16cbd-145">若要對您使用 StorSimple 裝置時可能會遇到的任何問題進行疑難排解，您必須連絡 Microsoft 支援服務小組。</span><span class="sxs-lookup"><span data-stu-id="16cbd-145">To troubleshoot any issues that you might experience with the StorSimple device, you will need to engage with the Microsoft Support team.</span></span> <span data-ttu-id="16cbd-146">Microsoft 支援服務可能需要使用支援工作階段來登入您的裝置。</span><span class="sxs-lookup"><span data-stu-id="16cbd-146">Microsoft Support may need to use a support session to log on to your device.</span></span> 

<span data-ttu-id="16cbd-147">執行下列步驟來啟動支援工作階段：</span><span class="sxs-lookup"><span data-stu-id="16cbd-147">Perform the following steps to start a support session:</span></span>

#### <a name="to-start-a-support-session"></a><span data-ttu-id="16cbd-148">啟動支援工作階段</span><span class="sxs-lookup"><span data-stu-id="16cbd-148">To start a support session</span></span>
1. <span data-ttu-id="16cbd-149">從遠端電腦使用序列主控台或透過 telnet 工作階段，直接存取裝置。</span><span class="sxs-lookup"><span data-stu-id="16cbd-149">Access the device directly by using the serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="16cbd-150">如果要這樣做，請依照 [使用 PuTTY 來連接至裝置序列主控台](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="16cbd-150">To do this, follow the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="16cbd-151">在開啟的工作階段中，按 **Enter** 鍵來取得命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="16cbd-151">In the session that opens, press the **Enter** key to get a command prompt.</span></span>
3. <span data-ttu-id="16cbd-152">在序列主控台功能表中，選取選項 1 [使用完整存取權登入] 。</span><span class="sxs-lookup"><span data-stu-id="16cbd-152">In the serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="16cbd-153">在提示字元中輸入下列密碼：</span><span class="sxs-lookup"><span data-stu-id="16cbd-153">At the prompt, type the following password:</span></span> 
   
    `Password1`
5. <span data-ttu-id="16cbd-154">在出現提示時輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="16cbd-154">At the prompt, type the following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="16cbd-155">您會看到加密的字串。</span><span class="sxs-lookup"><span data-stu-id="16cbd-155">An encrypted string will be presented to you.</span></span> <span data-ttu-id="16cbd-156">將此字串複製到 [記事本] 之類的文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="16cbd-156">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="16cbd-157">儲存這個字串，並透過電子郵件傳送給 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="16cbd-157">Save this string and send it in an email message to Microsoft Support.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="16cbd-158">您可以執行 `Disable-HcsSupportAccess` 來停用支援存取。</span><span class="sxs-lookup"><span data-stu-id="16cbd-158">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="16cbd-159">在起始工作階段之後 8 小時，StorSimple 裝置也會嘗試停用支援存取。</span><span class="sxs-lookup"><span data-stu-id="16cbd-159">The StorSimple device will also attempt to disable support access 8 hours after the session was initiated.</span></span> <span data-ttu-id="16cbd-160">最好在起始支援工作階段之後變更 StorSimple 裝置認證。</span><span class="sxs-lookup"><span data-stu-id="16cbd-160">It is a best practice to change your StorSimple device credentials after initiating a support session.</span></span>
> 
> 


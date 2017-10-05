---
title: "針對 StorSimple 8000 系列建立支援票證或案例 | Microsoft Docs"
description: "了解如何記錄支援要求和在 StorSimple 8000 系列裝置上啟動支援工作階段。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: alkohli;
ms.openlocfilehash: 4b5a14237ce79100f980b2186b2c3c887abaa296
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="contact-microsoft-support"></a><span data-ttu-id="6cd2f-103">連絡 Microsoft 支援服務</span><span class="sxs-lookup"><span data-stu-id="6cd2f-103">Contact Microsoft Support</span></span>

<span data-ttu-id="6cd2f-104">StorSimple 裝置管理員可讓您在服務摘要刀鋒視窗中**登錄新的支援要求**。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-104">The StorSimple Device Manager provides the capability to **log a new support request** within the service summary blade.</span></span> <span data-ttu-id="6cd2f-105">如果您使用 StorSimple 解決方案時遇到任何問題，您可以向技術支援人員提出服務要求。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-105">If you encounter any issues with your StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="6cd2f-106">在與支援工程師進行線上工作階段時，可能也需要在您的 StorSimple 裝置上啟動支援工作階段。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-106">In an online session with your support engineer, you may also need to start a support session on your StorSimple device.</span></span> <span data-ttu-id="6cd2f-107">本文將引導您：</span><span class="sxs-lookup"><span data-stu-id="6cd2f-107">This article walks you through:</span></span>

* <span data-ttu-id="6cd2f-108">如何建立支援要求。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-108">How to create a support request.</span></span>
* <span data-ttu-id="6cd2f-109">如何在入口網站上管理支援要求的生命週期。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-109">How to manage a support request lifecycle from within the portal.</span></span>
* <span data-ttu-id="6cd2f-110">如何在 StorSimple 裝置的 Windows PowerShell 介面中啟動支援工作階段。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-110">How to start a support session in the Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="6cd2f-111">建立支援要求之前，請先檢閱 [StorSimple 8000 系列支援 SLA 和資訊](https://msdn.microsoft.com/library/mt433077.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-111">Review the [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="6cd2f-112">建立支援要求</span><span class="sxs-lookup"><span data-stu-id="6cd2f-112">Create a support request</span></span>

<span data-ttu-id="6cd2f-113">視您的[支援方案](https://azure.microsoft.com/support/plans/)而定，您可以直接從 StorSimple 裝置管理員服務摘要刀鋒視窗中，針對 StorSimple 裝置的問題建立支援票證。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-113">Depending upon your [support plan](https://azure.microsoft.com/support/plans/), you can create support tickets for an issue on your StorSimple device directly from the StorSimple Device Manager service summary blade.</span></span> <span data-ttu-id="6cd2f-114">執行下列步驟來建立支援要求：</span><span class="sxs-lookup"><span data-stu-id="6cd2f-114">Perform the following steps to create a support request:</span></span>

#### <a name="to-create-a-support-request"></a><span data-ttu-id="6cd2f-115">建立支援要求</span><span class="sxs-lookup"><span data-stu-id="6cd2f-115">To create a support request</span></span>

1. <span data-ttu-id="6cd2f-116">移至您的 StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-116">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="6cd2f-117">在服務摘要刀鋒視窗的設定中，移至 [支援 + 疑難排解] 區段，然後按一下 [新增支援要求]。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-117">In the service summary blade settings, go to **SUPPORT + TROUBLESHOOTING** section and then click **New support request**.</span></span>
     
    ![透過新的入口網站連絡 MS 支援服務](./media/storsimple-8000-contact-microsoft-support/contactsupport1.png)
   
2. <span data-ttu-id="6cd2f-119">在 [新增支援要求] 刀鋒視窗中，選取 [基本]。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-119">In the **New support request** blade, select **Basics**.</span></span> <span data-ttu-id="6cd2f-120">在 [基本] 刀鋒視窗中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6cd2f-120">In the **Basics** blade, do the following steps:</span></span>
   1. <span data-ttu-id="6cd2f-121">從 [問題類型] 下拉式清單中，選取 [技術]。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-121">From the **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="6cd2f-122">自動會選擇目前的 [訂用帳戶]、[服務] 類型和 [資源] \(StorSimple 裝置管理員服務)。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-122">The current **Subscription**, **Service** type, and the **Resource** (StorSimple Device Manager service) are automatically chosen.</span></span> 
   3. <span data-ttu-id="6cd2f-123">如果您的訂用帳戶有多個相關聯的方案，請從下拉式清單選取**支援方案**。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-123">Select a **Support plan** from the drop-down list if you have multiple plans associated with your subscription.</span></span> <span data-ttu-id="6cd2f-124">您必須已付費購買支援方案，才能啟用技術支援。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-124">You need a paid support plan to enable Technical Support.</span></span>
   4. <span data-ttu-id="6cd2f-125">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-125">Click **Next**.</span></span>

       ![透過新的入口網站連絡 MS 支援服務](./media/storsimple-8000-contact-microsoft-support/contactsupport2.png)

3. <span data-ttu-id="6cd2f-127">在 [新增支援要求] 刀鋒視窗中，選取 [步驟 2 問題]。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-127">In the **New support request** blade, select **Step 2 Problem**.</span></span> <span data-ttu-id="6cd2f-128">在 [問題] 刀鋒視窗中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6cd2f-128">In the **Problem** blade, do the following steps:</span></span>
    
    1. <span data-ttu-id="6cd2f-129">選擇 [嚴重性]。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-129">Choose the **Severity**.</span></span>
    2. <span data-ttu-id="6cd2f-130">指定問題是與設備還是 StorSimple 裝置管理員服務有關。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-130">Specify if the issue is related to the appliance or the StorSimple Device Manager service.</span></span>
    3. <span data-ttu-id="6cd2f-131">選擇這個問題的 [類別]，並提供問題的其他 [詳細資料]。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-131">Choose a **Category** for this issue and provide more **Details** about the issue.</span></span>
    4. <span data-ttu-id="6cd2f-132">提供問題開始日期與時間。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-132">Provide the start date and time for the problem.</span></span>
    5. <span data-ttu-id="6cd2f-133">在 [檔案上傳] 中，按一下資料夾圖示，即可瀏覽至您的支援封裝。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-133">In the **File upload**, click the folder icon to browse to your support package.</span></span>
    6. <span data-ttu-id="6cd2f-134">勾選 [共用診斷資訊]。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-134">Check **Share diagnostic information**.</span></span>
    7. <span data-ttu-id="6cd2f-135">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-135">Click **Next**.</span></span>

       ![透過新的入口網站連絡 MS 支援服務](./media/storsimple-8000-contact-microsoft-support/contactsupport3.png) 

4. <span data-ttu-id="6cd2f-137">在 [新增支援要求] 刀鋒視窗中，按一下 [步驟 3 連絡人資訊]。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-137">In the **New support request** blade, click **Step 3 Contact information**.</span></span> <span data-ttu-id="6cd2f-138">在 [連絡人資訊] 刀鋒視窗中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6cd2f-138">In the **Contact information** blade, do the following steps:</span></span>

    1. <span data-ttu-id="6cd2f-139">在 [連絡人選項] 中，提供您偏好的連絡方法 (電話或電子郵件) 以及語言。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-139">In the **Contact options**, provide your preferred contact method (phone or email) and the language.</span></span> <span data-ttu-id="6cd2f-140">會根據您的訂用帳戶方案自動選擇回應時間。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-140">The response time is automatically selected based on your subscription plan.</span></span>
    2. <span data-ttu-id="6cd2f-141">在 [連絡人資訊] 中，提供您的姓名、電子郵件、選用連絡方法、國家/地區。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-141">In the Contact information, provide your name, email, optional contact, country.</span></span> <span data-ttu-id="6cd2f-142">選取 [儲存連絡人變更以供未來的支援要求使用]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-142">Select the **Save contact changes for future support requests** check box.</span></span>
    3. <span data-ttu-id="6cd2f-143">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-143">Click **Create**.</span></span>
   
        ![透過新的入口網站連絡 MS 支援服務](./media/storsimple-8000-contact-microsoft-support/contactsupport5.png)   

    <span data-ttu-id="6cd2f-145">Microsoft 支援服務會利用此資訊來連絡您，以取得進一步資訊、進行診斷及解決。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-145">Microsoft Support will use this information to reach out to you for further information, diagnosis, and resolution.</span></span>
<span data-ttu-id="6cd2f-146">提交您的要求之後，支援工程師會儘速連絡您來處理您的要求。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-146">After you have submitted your request, a Support engineer will contact you as soon as possible to proceed with your request.</span></span>

## <a name="manage-a-support-request"></a><span data-ttu-id="6cd2f-147">管理支援要求</span><span class="sxs-lookup"><span data-stu-id="6cd2f-147">Manage a support request</span></span>

<span data-ttu-id="6cd2f-148">建立支援票證之後，您便可以從入口網站中管理票證的生命週期。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-148">After creating a support ticket, you can manage the lifecycle of the ticket from within the portal.</span></span>

#### <a name="to-manage-your-support-requests"></a><span data-ttu-id="6cd2f-149">若要管理支援要求</span><span class="sxs-lookup"><span data-stu-id="6cd2f-149">To manage your support requests</span></span>

1. <span data-ttu-id="6cd2f-150">若要移至說明和支援頁面，請瀏覽至 [瀏覽] > [說明 + 支援]。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-150">To get to the help and support page, navigate to **Browse > Help + support**.</span></span>

    ![管理支援要求](./media/storsimple-8000-contact-microsoft-support/managesupport1.png)

2. <span data-ttu-id="6cd2f-152">[說明 + 支援] 刀鋒視窗中會以表格式清單列出全部的支援要求。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-152">A tabular listing of All the support requests is displayed in the **Help + support** blade.</span></span>

    ![管理支援要求](./media/storsimple-8000-contact-microsoft-support/managesupport2.png)

3. <span data-ttu-id="6cd2f-154">選取並按一下支援要求。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-154">Select and click a support request.</span></span> <span data-ttu-id="6cd2f-155">您可以檢視此要求的狀態與詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-155">You can view the status and the details for this request.</span></span> <span data-ttu-id="6cd2f-156">如果您想要追蹤此要求，請按一下 [+ New message]\(+ 新訊息\)。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-156">Click **+ New message** if you want to follow up on this request.</span></span>

    ![管理支援要求](./media/storsimple-8000-contact-microsoft-support/managesupport3.png)

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="6cd2f-158">在 Windows PowerShell for StorSimple 中啟動支援工作階段</span><span class="sxs-lookup"><span data-stu-id="6cd2f-158">Start a support session in Windows PowerShell for StorSimple</span></span>

<span data-ttu-id="6cd2f-159">若要對您使用 StorSimple 裝置時可能會遇到的任何問題進行疑難排解，您必須連絡 Microsoft 支援服務小組。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-159">To troubleshoot any issues that you might experience with the StorSimple device, you will need to engage with the Microsoft Support team.</span></span> <span data-ttu-id="6cd2f-160">Microsoft 支援服務可能需要使用支援工作階段來登入您的裝置。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-160">Microsoft Support may need to use a support session to log on to your device.</span></span>

<span data-ttu-id="6cd2f-161">執行下列步驟來啟動支援工作階段：</span><span class="sxs-lookup"><span data-stu-id="6cd2f-161">Perform the following steps to start a support session:</span></span>

#### <a name="to-start-a-support-session"></a><span data-ttu-id="6cd2f-162">啟動支援工作階段</span><span class="sxs-lookup"><span data-stu-id="6cd2f-162">To start a support session</span></span>

1. <span data-ttu-id="6cd2f-163">從遠端電腦使用序列主控台或透過 telnet 工作階段，直接存取裝置。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-163">Access the device directly by using the serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="6cd2f-164">如果要這樣做，請依照 [使用 PuTTY 來連接至裝置序列主控台](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-164">To do this, follow the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="6cd2f-165">在開啟的工作階段中，按 **Enter** 鍵來取得命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-165">In the session that opens, press the **Enter** key to get a command prompt.</span></span>
3. <span data-ttu-id="6cd2f-166">在序列主控台功能表中，選取選項 1 [使用完整存取權登入] 。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-166">In the serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="6cd2f-167">在提示字元中輸入下列密碼：</span><span class="sxs-lookup"><span data-stu-id="6cd2f-167">At the prompt, type the following password:</span></span>
   
    `Password1`
5. <span data-ttu-id="6cd2f-168">在出現提示時輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="6cd2f-168">At the prompt, type the following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="6cd2f-169">您會看到加密的字串。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-169">An encrypted string will be presented to you.</span></span> <span data-ttu-id="6cd2f-170">將此字串複製到 [記事本] 之類的文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-170">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="6cd2f-171">儲存這個字串，並透過電子郵件傳送給 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-171">Save this string and send it in an email message to Microsoft Support.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6cd2f-172">您可以執行 `Disable-HcsSupportAccess` 來停用支援存取。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-172">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="6cd2f-173">在起始工作階段之後 8 小時，StorSimple 裝置也會嘗試停用支援存取。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-173">The StorSimple device will also attempt to disable support access 8 hours after the session was initiated.</span></span> <span data-ttu-id="6cd2f-174">最好在起始支援工作階段之後變更 StorSimple 裝置認證。</span><span class="sxs-lookup"><span data-stu-id="6cd2f-174">It is a best practice to change your StorSimple device credentials after initiating a support session.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6cd2f-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6cd2f-175">Next steps</span></span>

<span data-ttu-id="6cd2f-176">了解如何[診斷並解決 StorSimple 8000 系列裝置的相關問題](storsimple-troubleshoot-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="6cd2f-176">Learn how to [diagnose and solve problems related to your StorSimple 8000 series device](storsimple-troubleshoot-deployment.md)</span></span>

---
title: "aaaHow toouse hello Azure Active Directory Power BI 內容套件 |Microsoft 文件"
description: "了解如何 toouse hello Azure Active Directory Power BI 內容套件"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d07d678aedbe3089c4ea5f981f72311bdb389a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-active-directory-power-bi-content-pack"></a><span data-ttu-id="63f99-103">如何 toouse hello Azure Active Directory Power BI 內容套件</span><span class="sxs-lookup"><span data-stu-id="63f99-103">How toouse hello Azure Active Directory Power BI Content Pack</span></span>

<span data-ttu-id="63f99-104">身為 IT 管理員，了解您的使用者如何採用及使用 Azure Active Directory 功能相當重要。它可讓您 tooplan IT 基礎結構和通訊 tooincrease 使用量和 tooget hello 最 AAD 功能。</span><span class="sxs-lookup"><span data-stu-id="63f99-104">Understanding how your users adopt and use Azure Active Directory features is critical for you as an IT admin. It allows you tooplan your IT infrastructure and communication tooincrease usage and tooget hello most out of AAD features.</span></span> <span data-ttu-id="63f99-105">Power BI 內容套件提供 hello 能力 toofurther 分析您的資料 toounderstand 方式，您可以使用此資料 toogather 更豐富深入了解與 hello 其 Azure Active Directory 的 Azure Active Directory 的各種功能您有很大依賴。</span><span class="sxs-lookup"><span data-stu-id="63f99-105">Power BI Content Pack for Azure Active Directory gives you hello ability toofurther analyze your data toounderstand how you can use this data toogather richer insights into what’s going on with their Azure Active Directory for hello various capabilities you heavily rely on.</span></span>  <span data-ttu-id="63f99-106">與 hello 整合 Azure Active Directory 應用程式開發介面放入 Power BI，您可以輕鬆地下載 hello 預先建立的內容套件，並在您使用 Power BI 提供豐富的視覺效果經驗的 Azure Active Directory 中獲得見解 tooall hello 活動。</span><span class="sxs-lookup"><span data-stu-id="63f99-106">With hello integration of Azure Active Directory APIs into Power BI, you can easily download hello pre-built content packs and gain insights tooall hello activities within your Azure Active Directory using rich visualization experience Power BI offers.</span></span> <span data-ttu-id="63f99-107">您可以建立自己的儀表板，並輕鬆地與組織中所有人共用。</span><span class="sxs-lookup"><span data-stu-id="63f99-107">You can create your own dashboard and share it easily with anyone in your organization.</span></span> 

<span data-ttu-id="63f99-108">本主題提供您 tooinstall 並用 hello 內容的逐步指示與組件，您的環境中。</span><span class="sxs-lookup"><span data-stu-id="63f99-108">This topic provides you with step-by-step instructions on how tooinstall and use hello content pack in your environment.</span></span>

## <a name="installation"></a><span data-ttu-id="63f99-109">安裝</span><span class="sxs-lookup"><span data-stu-id="63f99-109">Installation</span></span>  

<span data-ttu-id="63f99-110">**tooinstall hello Power BI 內容套件：**</span><span class="sxs-lookup"><span data-stu-id="63f99-110">**tooinstall hello Power BI Content Pack:**</span></span>

1. <span data-ttu-id="63f99-111">登入[Power BI](https://app.powerbi.com/groups/me/getdata/services)與您的 Power BI 帳戶 (這是 hello 做為您的 O365 或 Azure AD 帳戶的相同帳戶)。</span><span class="sxs-lookup"><span data-stu-id="63f99-111">Log into [Power BI](https://app.powerbi.com/groups/me/getdata/services) with your Power BI Account (this is hello same account as your O365 or Azure AD Account).</span></span>

2. <span data-ttu-id="63f99-112">在 hello hello 左側瀏覽窗格底部，選取**取得資料**。</span><span class="sxs-lookup"><span data-stu-id="63f99-112">At hello bottom of hello left navigation pane, select **Get Data**.</span></span>

    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/01.png)
 
3. <span data-ttu-id="63f99-114">在 hello**服務**方塊中，按一下**取得**。</span><span class="sxs-lookup"><span data-stu-id="63f99-114">In hello **Services** box, click **Get**.</span></span>
   
    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/02.png)

4.  <span data-ttu-id="63f99-116">搜尋 **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="63f99-116">Search for **Azure Active Directory**.</span></span>

    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/03.png)
 
5.  <span data-ttu-id="63f99-118">出現提示時，輸入您的 Azure AD 租用戶識別碼，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="63f99-118">When prompted, type your Azure AD Tenant ID, and then click **Next**.</span></span>

    > [!TIP] 
    > <span data-ttu-id="63f99-119">您的 Office 365 / Azure AD 租用戶快速 tooget hello 租用戶識別碼是 toologin toohello Azure AD 入口網站、 向下鑽研 toohello 目錄並複製 hello 識別碼，從下列 URL 的 hello: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ActiveDirectoryExtension/Directory/<tenantid>/directoryQuickStart</span><span class="sxs-lookup"><span data-stu-id="63f99-119">A quick way tooget hello Tenant Id for your Office 365 / Azure AD tenant is toologin toohello Azure AD Portal, drill down toohello directory and copy hello ID from hello following URL: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ActiveDirectoryExtension/Directory/<tenantid>/directoryQuickStart</span></span>

    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/04.png) 

6.  <span data-ttu-id="63f99-121">按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="63f99-121">Click **Sign-in**.</span></span> 
 
    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/05.png) 



7.  <span data-ttu-id="63f99-123">輸入您的使用者名稱和密碼，然後按一下登入。</span><span class="sxs-lookup"><span data-stu-id="63f99-123">Enter your username and password, and then click **Sign in**.</span></span>
 
    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/06.png) 

8.  <span data-ttu-id="63f99-125">在 hello 應用程式的同意對話方塊中，按一下 **接受**。</span><span class="sxs-lookup"><span data-stu-id="63f99-125">On hello app consent dialog, click **Accept**.</span></span>
 
9.  <span data-ttu-id="63f99-126">建立好 Azure Active Directory 活動記錄儀表板後，按一下該儀表板。</span><span class="sxs-lookup"><span data-stu-id="63f99-126">When your Azure Active Directory Activity logs dashboard has been created, click it.</span></span>
 
    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/08.png) 

## <a name="what-can-i-do-with-this-content-pack"></a><span data-ttu-id="63f99-128">此內容套件有何功用？</span><span class="sxs-lookup"><span data-stu-id="63f99-128">What can I do with this content pack?</span></span>

<span data-ttu-id="63f99-129">我們進到您可以執行與此內容套件之前，此處的預覽 hello hello 內容中的各種報表組件。</span><span class="sxs-lookup"><span data-stu-id="63f99-129">Before we jump into what you can do with this content pack, here’s quick preview of hello various reports in hello content pack.</span></span> <span data-ttu-id="63f99-130">報表資料會回到 toohello**過去 30 天內**。</span><span class="sxs-lookup"><span data-stu-id="63f99-130">Report data goes back toohello **last 30 days**.</span></span>

### <a name="reports-included-in-this-version-of-azure-active-directory-logs-content-pack"></a><span data-ttu-id="63f99-131">此版 Azure Active Directory 記錄內容套件中包含的報表</span><span class="sxs-lookup"><span data-stu-id="63f99-131">Reports included in this version of Azure Active Directory logs Content Pack</span></span>

<span data-ttu-id="63f99-132">**應用程式使用量和趨勢報表**： 取得深入了解 hello 的應用程式中使用您的組織，以及正在使用哪些最 hello 與時機。</span><span class="sxs-lookup"><span data-stu-id="63f99-132">**App Usage and Trend report**:  Get insights into hello apps used in your organization and which ones are being used hello most and when.</span></span> <span data-ttu-id="63f99-133">您可以使用此報表 toogather 深入了解如何使用您最近推出您組織中的應用程式，或找出哪些應用程式上相當普遍。</span><span class="sxs-lookup"><span data-stu-id="63f99-133">You can use this report toogather insights into how an app you recently rolled out in your organization is being used or find out which apps are popular.</span></span> <span data-ttu-id="63f99-134">這樣，如果您看到 是否未使用 hello 應用程式，來改善使用方式。</span><span class="sxs-lookup"><span data-stu-id="63f99-134">By doing this, you can improve usage if you see if hello app is not being used.</span></span>

<span data-ttu-id="63f99-135">**依位置和使用者的登入**： 取得深入了解所有 hello 登入使用 Azure 身分識別與可提供深入了解 hello hello 使用者身分執行。</span><span class="sxs-lookup"><span data-stu-id="63f99-135">**Sign-ins by location and users**: Get insights into all hello sign-ins performed using Azure Identity and gives insights into hello identity of hello users.</span></span> <span data-ttu-id="63f99-136">透過此項目，您可以更深入地了解個人登入狀況並回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="63f99-136">With this, you can dig deeper into individual sign-ins and answer questions like:</span></span>

- <span data-ttu-id="63f99-137">此使用者從何處登入？</span><span class="sxs-lookup"><span data-stu-id="63f99-137">From where did this user sign-ins?</span></span>
- <span data-ttu-id="63f99-138">哪些使用者擁有 hello 大部分的登入和其中執行他們登入從嗎？</span><span class="sxs-lookup"><span data-stu-id="63f99-138">Which user has hello most sign-ins and where do they sign-in from?</span></span> 
- <span data-ttu-id="63f99-139">成功 hello 登入？</span><span class="sxs-lookup"><span data-stu-id="63f99-139">Was hello sign-in successful?</span></span>  
 
<span data-ttu-id="63f99-140">您可以按一下特定日期或位置，以深入探詢詳細資料。</span><span class="sxs-lookup"><span data-stu-id="63f99-140">You can drill into details by clicking on a specific date or location.</span></span>

<span data-ttu-id="63f99-141">**每個應用程式的唯一使用者**：檢視使用指定應用程式的所有唯一使用者。</span><span class="sxs-lookup"><span data-stu-id="63f99-141">**Unique users per app**:  Get a view of all unique users using a given app.</span></span> <span data-ttu-id="63f99-142">此項目僅包括「*成功*」登入應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="63f99-142">This includes only users who have “*successfully*” signed into an application.</span></span>

<span data-ttu-id="63f99-143">**裝置登入**: hello 的 OS 類型檢視和瀏覽器正在使用的 hello 使用者包括的詳細資訊與您組織中的使用者：</span><span class="sxs-lookup"><span data-stu-id="63f99-143">**Device sign-ins**: Get a view of hello type of OS and browsers are being used by users in your organization with detailed information on hello users including:</span></span>

- <span data-ttu-id="63f99-144">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="63f99-144">User Name</span></span>
- <span data-ttu-id="63f99-145">IP 位址</span><span class="sxs-lookup"><span data-stu-id="63f99-145">IP Address</span></span>
- <span data-ttu-id="63f99-146">位置</span><span class="sxs-lookup"><span data-stu-id="63f99-146">Location</span></span> 
- <span data-ttu-id="63f99-147">登入狀態</span><span class="sxs-lookup"><span data-stu-id="63f99-147">Sign-in status</span></span> 

<span data-ttu-id="63f99-148">使用這份報表，您可以了解在組織內使用各種裝置設定檔，並判斷根據用途的裝置原則的 hello</span><span class="sxs-lookup"><span data-stu-id="63f99-148">With this report, you can understand hello various device profiles used within your organization and determine device policies based on what’s used</span></span>

<span data-ttu-id="63f99-149">**SSPR 漏斗圖**：了解在組織中如何完成密碼重設。</span><span class="sxs-lookup"><span data-stu-id="63f99-149">**SSPR Funnel**: Get an understanding on how password resets are being done in your organization.</span></span> <span data-ttu-id="63f99-150">查看進入多少密碼重設嘗試透過 hello SSPR 工具，以及多少個成功。</span><span class="sxs-lookup"><span data-stu-id="63f99-150">Get a peek into how many password resets were attempted through hello SSPR tool and how many of them were successful.</span></span> <span data-ttu-id="63f99-151">更深入發掘 hello 使用 hello SSPR 漏斗圖的密碼重設失敗，並了解特定失敗的發生原因。</span><span class="sxs-lookup"><span data-stu-id="63f99-151">Dig deeper into hello Password resets failure using hello SSPR funnel and understand why certain failures occurred.</span></span> <span data-ttu-id="63f99-152">此報表會提供更深入的了解如何 hello SSPR 工具使用的組織內進行 hello 正確的決策。</span><span class="sxs-lookup"><span data-stu-id="63f99-152">This report gives a deeper understanding of how hello SSPR tool is used within your organization so you can make hello right decisions.</span></span>

## <a name="customizing-azure-ad-activity-content-pack"></a><span data-ttu-id="63f99-153">自訂 Azure AD 的活動內容套件</span><span class="sxs-lookup"><span data-stu-id="63f99-153">Customizing Azure AD Activity content pack</span></span>

<span data-ttu-id="63f99-154">**變更視覺效果**： 您可以按一下來變更報表視覺效果**編輯報表**和選取您想要的 hello 視覺效果。</span><span class="sxs-lookup"><span data-stu-id="63f99-154">**Change Visualization**:  You can change a report visualization by clicking **Edit Report** and select hello visualization you want.</span></span>
 
![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/09.png) 
 
![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/10.png) 

<span data-ttu-id="63f99-157">**包含其他欄位**： 您可以加入欄位 toohello 報表或選取您希望 tooadd/移除 hello 欄位 hello visual toowhich 移除它。</span><span class="sxs-lookup"><span data-stu-id="63f99-157">**Include additional fields**:  You can add a field toohello report or remove it by selecting hello visual toowhich you want tooadd/remove hello field.</span></span> <span data-ttu-id="63f99-158">在 hello 下列範例中，我加入 「 登入狀態 」 欄位 toohello 資料表檢視表。</span><span class="sxs-lookup"><span data-stu-id="63f99-158">In hello example below, I am adding “sign-in status” field toohello table view.</span></span> 
 
![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/11.png) 

<span data-ttu-id="63f99-160">**釘選視覺效果 tooyour 儀表板**： 您可以自訂儀表板和包含您自己的視覺效果 toohello 報表並將其釘選 toohello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="63f99-160">**Pin visualizations tooyour dashboard**:  You can customize your dashboard and include your own visualizations toohello report and pin it toohello dashboard.</span></span> <span data-ttu-id="63f99-161">在 hello 面範例中，我要加入新的篩選器，稱為 「 登入狀態 」，並包含 hello 報表中。</span><span class="sxs-lookup"><span data-stu-id="63f99-161">In hello example below, I added a new filter called “Sign-in Status” and included it in hello report.</span></span> <span data-ttu-id="63f99-162">我也從橫條圖 tooa 折線圖變更 hello 視覺效果，並可以將這個新的視覺 toohello 儀表板釘選。</span><span class="sxs-lookup"><span data-stu-id="63f99-162">I also changed hello visualization from bar chart tooa line chart and can pin this new visual toohello dashboard.</span></span>

![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/12.png) 

![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/13.png) 
 

 


<span data-ttu-id="63f99-165">**共用儀表板**： 當您建立您想要的 hello 內容之後時，您可以在組織中與 hello 使用者共用 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="63f99-165">**Sharing your dashboard**: Once you have created hello content you want, you can share hello dashboard with hello users in your organization.</span></span> <span data-ttu-id="63f99-166">請記住一旦共用 hello 報表時，他們可以看到您所選取 hello 報表中的 hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="63f99-166">Please remember that once you share hello report, they can see hello fields you have selected in hello report.</span></span>
 
![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/14.png) 



## <a name="scheduling-a-daily-refresh-of-your-power-bi-report"></a><span data-ttu-id="63f99-168">排定每日重新整理 Power BI 報表</span><span class="sxs-lookup"><span data-stu-id="63f99-168">Scheduling a daily refresh of your Power BI report</span></span>

<span data-ttu-id="63f99-169">tooschedule 每日重新整理 Power BI 報表中，跳過**資料集 > 設定 > 排程重新整理**並將其設定，如下所示。</span><span class="sxs-lookup"><span data-stu-id="63f99-169">tooschedule a daily refresh of your Power BI report, go too**Datasets > Settings > Schedule Refresh** and set it as shown below.</span></span>
 
![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/15.png) 

## <a name="updating-toonewer-version-of-content-pack"></a><span data-ttu-id="63f99-171">更新 toonewer 版本內容套件</span><span class="sxs-lookup"><span data-stu-id="63f99-171">Updating toonewer version of content pack</span></span>

<span data-ttu-id="63f99-172">如果您想 tooupdate 內容 pack tooget 較新版本：</span><span class="sxs-lookup"><span data-stu-id="63f99-172">If you want tooupdate your content pack tooget a newer version:</span></span>

- <span data-ttu-id="63f99-173">下載 hello 新內容套件，並設定根據本文所列的指示。</span><span class="sxs-lookup"><span data-stu-id="63f99-173">Download hello new content pack and set it up as per instructions listed in this article.</span></span>

- <span data-ttu-id="63f99-174">在您設定它，請移過**資料來源 > 設定 > 資料來源認證**，然後重新輸入您的認證，如下所示</span><span class="sxs-lookup"><span data-stu-id="63f99-174">Once you have set it up, go too**Data Source > Settings > Data source credentials** and re-enter your credentials as shown below</span></span>

    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/16.png) 

<span data-ttu-id="63f99-176">Hello hello 內容套件的新版本可以運作，因為您可以在必要時刪除 hello 基礎報表和與該內容套件相關聯的資料集移除 hello 舊版本。</span><span class="sxs-lookup"><span data-stu-id="63f99-176">As soon as hello new version of hello content pack is working, you can remove hello old version if needed by deleting hello underlying reports and datasets associated with that content pack.</span></span>

## <a name="still-having-issues"></a><span data-ttu-id="63f99-177">仍然有問題嗎？</span><span class="sxs-lookup"><span data-stu-id="63f99-177">Still having issues?</span></span> 

<span data-ttu-id="63f99-178">請參閱我們的[疑難排解指南](active-directory-reporting-troubleshoot-content-pack.md)。</span><span class="sxs-lookup"><span data-stu-id="63f99-178">Check out our [troubleshooting guide](active-directory-reporting-troubleshoot-content-pack.md).</span></span> <span data-ttu-id="63f99-179">如需使用 Power BI 的一般說明，請參閱這些[說明文章](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/)。</span><span class="sxs-lookup"><span data-stu-id="63f99-179">For general help with Power BI, check out these [help articles](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).</span></span>
 

## <a name="next-steps"></a><span data-ttu-id="63f99-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="63f99-180">Next steps</span></span>

<span data-ttu-id="63f99-181">如需報告的概觀，請參閱 hello [Azure Active Directory 報告](active-directory-reporting-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="63f99-181">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>

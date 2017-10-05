---
title: "如何使用 Azure Active Directory Power BI 內容套件 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory Power BI 內容套件"
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
ms.openlocfilehash: 5c642bb814a279756e8391f12fdc86b6ec0b4a8f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-active-directory-power-bi-content-pack"></a><span data-ttu-id="c7f2f-103">如何使用 Azure Active Directory Power BI 內容套件</span><span class="sxs-lookup"><span data-stu-id="c7f2f-103">How to use the Azure Active Directory Power BI Content Pack</span></span>

<span data-ttu-id="c7f2f-104">身為 IT 管理員，了解您的使用者如何採用及使用 Azure Active Directory 功能相當重要。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-104">Understanding how your users adopt and use Azure Active Directory features is critical for you as an IT admin.</span></span> <span data-ttu-id="c7f2f-105">這可讓您規劃 IT 基礎結構及通訊，以增加使用量和充分運用 AAD 功能。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-105">It allows you to plan your IT infrastructure and communication to increase usage and to get the most out of AAD features.</span></span> <span data-ttu-id="c7f2f-106">Azure Active Directory 的 power BI 內容套件可讓您進一步分析資料，以了解如何使用此資料來收集更豐富的分析結果，讓您清楚知道 Azure Active Directory 中您重度依賴的各種功能狀況。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-106">Power BI Content Pack for Azure Active Directory gives you the ability to further analyze your data to understand how you can use this data to gather richer insights into what’s going on with their Azure Active Directory for the various capabilities you heavily rely on.</span></span>  <span data-ttu-id="c7f2f-107">透過將 Azure Active Directory API 與 Power BI 整合，您可以輕鬆地下載預先建立的內容套件，並使用 Power BI 提供的豐富視覺效果經驗深入了解 Azure Active Directory 中所有活動。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-107">With the integration of Azure Active Directory APIs into Power BI, you can easily download the pre-built content packs and gain insights to all the activities within your Azure Active Directory using rich visualization experience Power BI offers.</span></span> <span data-ttu-id="c7f2f-108">您可以建立自己的儀表板，並輕鬆地與組織中所有人共用。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-108">You can create your own dashboard and share it easily with anyone in your organization.</span></span> 

<span data-ttu-id="c7f2f-109">本主題會提供逐步指示，說明如何在您的環境中安裝及使用內容套件。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-109">This topic provides you with step-by-step instructions on how to install and use the content pack in your environment.</span></span>

## <a name="installation"></a><span data-ttu-id="c7f2f-110">安裝</span><span class="sxs-lookup"><span data-stu-id="c7f2f-110">Installation</span></span>  

<span data-ttu-id="c7f2f-111">**安裝 Power BI 內容套件：**</span><span class="sxs-lookup"><span data-stu-id="c7f2f-111">**To install the Power BI Content Pack:**</span></span>

1. <span data-ttu-id="c7f2f-112">使用 Power BI 帳戶登入 [Power BI](https://app.powerbi.com/groups/me/getdata/services) (此帳戶與您的 O365 或 Azure AD 帳戶相同)。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-112">Log into [Power BI](https://app.powerbi.com/groups/me/getdata/services) with your Power BI Account (this is the same account as your O365 or Azure AD Account).</span></span>

2. <span data-ttu-id="c7f2f-113">在左側導覽窗格的底部，選取 [取得資料]。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-113">At the bottom of the left navigation pane, select **Get Data**.</span></span>

    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/01.png)
 
3. <span data-ttu-id="c7f2f-115">在 [服務] 方塊中，按一下 [取得]。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-115">In the **Services** box, click **Get**.</span></span>
   
    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/02.png)

4.  <span data-ttu-id="c7f2f-117">搜尋 **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-117">Search for **Azure Active Directory**.</span></span>

    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/03.png)
 
5.  <span data-ttu-id="c7f2f-119">出現提示時，輸入您的 Azure AD 租用戶識別碼，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-119">When prompted, type your Azure AD Tenant ID, and then click **Next**.</span></span>

    > [!TIP] 
    > <span data-ttu-id="c7f2f-120">登入 Azure AD 入口網站可快速取得您 Office 365 / Azure AD 租用戶的租用戶識別碼，請從下列 URL 深入探詢至目錄並複製識別碼：https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ActiveDirectoryExtension/Directory/<tenantid>/directoryQuickStart</span><span class="sxs-lookup"><span data-stu-id="c7f2f-120">A quick way to get the Tenant Id for your Office 365 / Azure AD tenant is to login to the Azure AD Portal, drill down to the directory and copy the ID from the following URL: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ActiveDirectoryExtension/Directory/<tenantid>/directoryQuickStart</span></span>

    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/04.png) 

6.  <span data-ttu-id="c7f2f-122">按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-122">Click **Sign-in**.</span></span> 
 
    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/05.png) 



7.  <span data-ttu-id="c7f2f-124">輸入您的使用者名稱和密碼，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-124">Enter your username and password, and then click **Sign in**.</span></span>
 
    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/06.png) 

8.  <span data-ttu-id="c7f2f-126">在應用程式的同意對話方塊中，按一下 [接受]。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-126">On the app consent dialog, click **Accept**.</span></span>
 
9.  <span data-ttu-id="c7f2f-127">建立好 Azure Active Directory 活動記錄儀表板後，按一下該儀表板。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-127">When your Azure Active Directory Activity logs dashboard has been created, click it.</span></span>
 
    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/08.png) 

## <a name="what-can-i-do-with-this-content-pack"></a><span data-ttu-id="c7f2f-129">此內容套件有何功用？</span><span class="sxs-lookup"><span data-stu-id="c7f2f-129">What can I do with this content pack?</span></span>

<span data-ttu-id="c7f2f-130">在說明此內容套件的功用前，您可以快速預覽內容套件中的各種報表。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-130">Before we jump into what you can do with this content pack, here’s quick preview of the various reports in the content pack.</span></span> <span data-ttu-id="c7f2f-131">報表資料可回溯至 **30 天前**。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-131">Report data goes back to the **last 30 days**.</span></span>

### <a name="reports-included-in-this-version-of-azure-active-directory-logs-content-pack"></a><span data-ttu-id="c7f2f-132">此版 Azure Active Directory 記錄內容套件中包含的報表</span><span class="sxs-lookup"><span data-stu-id="c7f2f-132">Reports included in this version of Azure Active Directory logs Content Pack</span></span>

<span data-ttu-id="c7f2f-133">**應用程式使用量和趨勢報表**：分析您組織中使用的應用程式，以及哪些應用程式最常使用和使用時機。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-133">**App Usage and Trend report**:  Get insights into the apps used in your organization and which ones are being used the most and when.</span></span> <span data-ttu-id="c7f2f-134">您可以使用此報表來收集分析結果，了解您最近在組織中推出的應用程式使用狀況，或找出哪些應用程式較受歡迎。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-134">You can use this report to gather insights into how an app you recently rolled out in your organization is being used or find out which apps are popular.</span></span> <span data-ttu-id="c7f2f-135">透過執行這些動作，您可以在發現未使用的應用程式時，改善使用方式。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-135">By doing this, you can improve usage if you see if the app is not being used.</span></span>

<span data-ttu-id="c7f2f-136">**不同位置和不同使用者的登入狀況**：分析使用 Azure 識別碼的登入狀況，以及分析使用者的識別碼。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-136">**Sign-ins by location and users**: Get insights into all the sign-ins performed using Azure Identity and gives insights into the identity of the users.</span></span> <span data-ttu-id="c7f2f-137">透過此項目，您可以更深入地了解個人登入狀況並回答下列問題：</span><span class="sxs-lookup"><span data-stu-id="c7f2f-137">With this, you can dig deeper into individual sign-ins and answer questions like:</span></span>

- <span data-ttu-id="c7f2f-138">此使用者從何處登入？</span><span class="sxs-lookup"><span data-stu-id="c7f2f-138">From where did this user sign-ins?</span></span>
- <span data-ttu-id="c7f2f-139">哪一個使用者最常登入，以及從何處登入？</span><span class="sxs-lookup"><span data-stu-id="c7f2f-139">Which user has the most sign-ins and where do they sign-in from?</span></span> 
- <span data-ttu-id="c7f2f-140">登入是否成功？</span><span class="sxs-lookup"><span data-stu-id="c7f2f-140">Was the sign-in successful?</span></span>  
 
<span data-ttu-id="c7f2f-141">您可以按一下特定日期或位置，以深入探詢詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-141">You can drill into details by clicking on a specific date or location.</span></span>

<span data-ttu-id="c7f2f-142">**每個應用程式的唯一使用者**：檢視使用指定應用程式的所有唯一使用者。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-142">**Unique users per app**:  Get a view of all unique users using a given app.</span></span> <span data-ttu-id="c7f2f-143">此項目僅包括「*成功*」登入應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-143">This includes only users who have “*successfully*” signed into an application.</span></span>

<span data-ttu-id="c7f2f-144">**裝置登入**：檢視您組織中使用者使用的作業系統和瀏覽器類型，其中包含使用者的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="c7f2f-144">**Device sign-ins**: Get a view of the type of OS and browsers are being used by users in your organization with detailed information on the users including:</span></span>

- <span data-ttu-id="c7f2f-145">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="c7f2f-145">User Name</span></span>
- <span data-ttu-id="c7f2f-146">IP 位址</span><span class="sxs-lookup"><span data-stu-id="c7f2f-146">IP Address</span></span>
- <span data-ttu-id="c7f2f-147">位置</span><span class="sxs-lookup"><span data-stu-id="c7f2f-147">Location</span></span> 
- <span data-ttu-id="c7f2f-148">登入狀態</span><span class="sxs-lookup"><span data-stu-id="c7f2f-148">Sign-in status</span></span> 

<span data-ttu-id="c7f2f-149">透過此報表，您可以了解組織中的各種裝置設定檔，並根據使用內容決定裝置原則</span><span class="sxs-lookup"><span data-stu-id="c7f2f-149">With this report, you can understand the various device profiles used within your organization and determine device policies based on what’s used</span></span>

<span data-ttu-id="c7f2f-150">**SSPR 漏斗圖**：了解在組織中如何完成密碼重設。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-150">**SSPR Funnel**: Get an understanding on how password resets are being done in your organization.</span></span> <span data-ttu-id="c7f2f-151">了解透過 SSPR 工具嘗試進行密碼重設的次數，以及成功重設的次數。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-151">Get a peek into how many password resets were attempted through the SSPR tool and how many of them were successful.</span></span> <span data-ttu-id="c7f2f-152">使用 SSPR 漏斗圖可更深入了解密碼重設錯誤的狀況，以及了解發生特定錯誤的原因。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-152">Dig deeper into the Password resets failure using the SSPR funnel and understand why certain failures occurred.</span></span> <span data-ttu-id="c7f2f-153">此報表會提供更深入的說明，讓您了解如何在組織中使用 SSPR 工具，如此一來，您就可以做出正確決策。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-153">This report gives a deeper understanding of how the SSPR tool is used within your organization so you can make the right decisions.</span></span>

## <a name="customizing-azure-ad-activity-content-pack"></a><span data-ttu-id="c7f2f-154">自訂 Azure AD 的活動內容套件</span><span class="sxs-lookup"><span data-stu-id="c7f2f-154">Customizing Azure AD Activity content pack</span></span>

<span data-ttu-id="c7f2f-155">**變更視覺效果**：您可以按一下 [編輯報表] 並選取您想要的視覺效果，來變更報表的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-155">**Change Visualization**:  You can change a report visualization by clicking **Edit Report** and select the visualization you want.</span></span>
 
![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/09.png) 
 
![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/10.png) 

<span data-ttu-id="c7f2f-158">**包含其他欄位**：您可以透過選取要加入/移除的欄位，來將欄位新增至報表，或從報表中移除。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-158">**Include additional fields**:  You can add a field to the report or remove it by selecting the visual to which you want to add/remove the field.</span></span> <span data-ttu-id="c7f2f-159">在下列範例中，我會將 [登入狀態] 欄位新增至資料表檢視。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-159">In the example below, I am adding “sign-in status” field to the table view.</span></span> 
 
![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/11.png) 

<span data-ttu-id="c7f2f-161">**在儀表板中釘選視覺效果**：您可以自訂儀表板，並將自己的視覺效果新增至報表，然後將其釘選至儀表板。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-161">**Pin visualizations to your dashboard**:  You can customize your dashboard and include your own visualizations to the report and pin it to the dashboard.</span></span> <span data-ttu-id="c7f2f-162">在下列範例中，我已新增名為「登入狀態」的篩選器，並將其包含在報表中。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-162">In the example below, I added a new filter called “Sign-in Status” and included it in the report.</span></span> <span data-ttu-id="c7f2f-163">我也會將橫條圖的視覺效果變更為折線圖，且新的視覺效果可釘選制儀表板中。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-163">I also changed the visualization from bar chart to a line chart and can pin this new visual to the dashboard.</span></span>

![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/12.png) 

![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/13.png) 
 

 


<span data-ttu-id="c7f2f-166">**共用儀表板**：當您建立您想要的內容之後，您可以與組織中的使用者共用儀表板。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-166">**Sharing your dashboard**: Once you have created the content you want, you can share the dashboard with the users in your organization.</span></span> <span data-ttu-id="c7f2f-167">請記住，當您共用報表時，其他人可以看到您在報表中選取的欄位。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-167">Please remember that once you share the report, they can see the fields you have selected in the report.</span></span>
 
![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/14.png) 



## <a name="scheduling-a-daily-refresh-of-your-power-bi-report"></a><span data-ttu-id="c7f2f-169">排定每日重新整理 Power BI 報表</span><span class="sxs-lookup"><span data-stu-id="c7f2f-169">Scheduling a daily refresh of your Power BI report</span></span>

<span data-ttu-id="c7f2f-170">若要排定每日重新整理 Power BI 報表，請移至 [資料集 > 設定 > 排定重新整理]，並執行下列設定。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-170">To schedule a daily refresh of your Power BI report, go to **Datasets > Settings > Schedule Refresh** and set it as shown below.</span></span>
 
![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/15.png) 

## <a name="updating-to-newer-version-of-content-pack"></a><span data-ttu-id="c7f2f-172">更新至較新版本的內容套件</span><span class="sxs-lookup"><span data-stu-id="c7f2f-172">Updating to newer version of content pack</span></span>

<span data-ttu-id="c7f2f-173">如果您想要更新內容套件，以取得較新版本：</span><span class="sxs-lookup"><span data-stu-id="c7f2f-173">If you want to update your content pack to get a newer version:</span></span>

- <span data-ttu-id="c7f2f-174">下載新的內容套件，並根據本文所列的指示進行設定。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-174">Download the new content pack and set it up as per instructions listed in this article.</span></span>

- <span data-ttu-id="c7f2f-175">設定為成後，請移至 [資料來源 > 設定 > 資料來源認證]，然後重新輸入您的認證，如下所示</span><span class="sxs-lookup"><span data-stu-id="c7f2f-175">Once you have set it up, go to **Data Source > Settings > Data source credentials** and re-enter your credentials as shown below</span></span>

    ![Azure Active Directory Power BI 內容套件](./media/active-directory-reporting-power-bi-content-pack-how-to/16.png) 

<span data-ttu-id="c7f2f-177">新版的內容套件開始運作時，您就可以透過刪除與舊版相關聯的基礎報表和資料庫來移除舊版。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-177">As soon as the new version of the content pack is working, you can remove the old version if needed by deleting the underlying reports and datasets associated with that content pack.</span></span>

## <a name="still-having-issues"></a><span data-ttu-id="c7f2f-178">仍然有問題嗎？</span><span class="sxs-lookup"><span data-stu-id="c7f2f-178">Still having issues?</span></span> 

<span data-ttu-id="c7f2f-179">請參閱我們的[疑難排解指南](active-directory-reporting-troubleshoot-content-pack.md)。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-179">Check out our [troubleshooting guide](active-directory-reporting-troubleshoot-content-pack.md).</span></span> <span data-ttu-id="c7f2f-180">如需使用 Power BI 的一般說明，請參閱這些[說明文章](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/)。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-180">For general help with Power BI, check out these [help articles](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).</span></span>
 

## <a name="next-steps"></a><span data-ttu-id="c7f2f-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c7f2f-181">Next steps</span></span>

<span data-ttu-id="c7f2f-182">如需報告概觀，請參閱 [Azure Active Directory 報告](active-directory-reporting-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="c7f2f-182">For an overview of reporting, see the [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>

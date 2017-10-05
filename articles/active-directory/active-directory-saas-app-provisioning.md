---
title: "在 Azure AD 中自動化 SaaS 應用程式使用者佈建 | Microsoft Docs"
description: "簡介如何使用 Azure AD 自動佈建、解除佈建，以及跨多個協力廠商 SaaS 應用程式持續更新使用者帳戶。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 58c5fa2d-bb33-4fba-8742-4441adf2cb62
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: curtand
ms.openlocfilehash: 7cb780117d64d67449146b9757f8162e23e65d1e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="automate-user-provisioning-and-deprovisioning-to-saas-applications-with-azure-active-directory"></a><span data-ttu-id="b0ecb-103">自動化使用 Azure Active Directory 對於 SaaS 應用程式的使用者佈建和取消佈建</span><span class="sxs-lookup"><span data-stu-id="b0ecb-103">Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory</span></span>
## <a name="what-is-automated-user-provisioning-for-saas-apps"></a><span data-ttu-id="b0ecb-104">SaaS 應用程式的自動化使用者佈建是什麼？</span><span class="sxs-lookup"><span data-stu-id="b0ecb-104">What is automated user provisioning for SaaS apps?</span></span>
<span data-ttu-id="b0ecb-105">Azure Active Directory (Azure AD) 可讓您自動化在雲端 ([SaaS](https://azure.microsoft.com/overview/what-is-saas/)) 應用程式中建立、維護和移除使用者身分識別，例如 Dropbox、Salesforce、ServiceNow 等等。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-105">Azure Active Directory (Azure AD) allows you to automate the creation, maintenance, and removal of user identities in cloud ([SaaS](https://azure.microsoft.com/overview/what-is-saas/)) applications such as Dropbox, Salesforce, ServiceNow, and more.</span></span>

<span data-ttu-id="b0ecb-106">**以下是這項功能可讓您執行的一些範例：**</span><span class="sxs-lookup"><span data-stu-id="b0ecb-106">**Below are some examples of what this feature allows you to do:**</span></span>

* <span data-ttu-id="b0ecb-107">當人員加入您的小組時，在正確的 SaaS 應用程式中為新的人員自動建立新帳戶。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-107">Automatically create new accounts in the right SaaS apps for new people when they join your team.</span></span>
* <span data-ttu-id="b0ecb-108">當人員離開小組時，自動從 SaaS 應用程式停用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-108">Automatically deactivate accounts from SaaS apps when people inevitably leave the team.</span></span>
* <span data-ttu-id="b0ecb-109">確保您的 SaaS 應用程式中的身分識別，根據目錄中的變更保持最新狀態。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-109">Ensure that the identities in your SaaS apps are kept up to date based on changes in the directory.</span></span>
* <span data-ttu-id="b0ecb-110">將支援的非使用者物件，例如群組，佈建至 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-110">Provision non-user objects, such as groups, to SaaS apps that support them.</span></span>

<span data-ttu-id="b0ecb-111">**自動化使用者佈建也包含下列功能：**</span><span class="sxs-lookup"><span data-stu-id="b0ecb-111">**Automated user provisioning also includes the following functionality:**</span></span>

* <span data-ttu-id="b0ecb-112">比對 Azure AD 和 SaaS 應用程式之間現有身分識別的能力。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-112">The ability to match existing identities between Azure AD and SaaS apps.</span></span>
* <span data-ttu-id="b0ecb-113">自訂選項，協助 Azure AD 符合您目前使用之 SaaS 應用程式的目前組態。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-113">Customization options to help Azure AD fit the current configurations of the SaaS apps that your organization is currently using.</span></span>
* <span data-ttu-id="b0ecb-114">佈建錯誤的選用電子郵件警示。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-114">Optional email alerts for provisioning errors.</span></span>
* <span data-ttu-id="b0ecb-115">報告和活動記錄檔，協助監視與疑難排解。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-115">Reporting and activity logs to help with monitoring and troubleshooting.</span></span>

## <a name="why-use-automated-provisioning"></a><span data-ttu-id="b0ecb-116">為何要使用自動化佈建？</span><span class="sxs-lookup"><span data-stu-id="b0ecb-116">Why Use Automated Provisioning?</span></span>
<span data-ttu-id="b0ecb-117">一些使用這項功能的常見動機包括：</span><span class="sxs-lookup"><span data-stu-id="b0ecb-117">Some common motivations for using this feature include:</span></span>

* <span data-ttu-id="b0ecb-118">為了避免成本、效率不彰，以及與手動佈建程序相關聯的人為錯誤。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-118">To avoid the costs, inefficiencies, and human error associated with manual provisioning processes.</span></span>
* <span data-ttu-id="b0ecb-119">為了在使用者離開組織時，立即從主要 SaaS 應用程式移除使用者的身分識別以保護您的組織。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-119">To secure your organization by instantly removing users' identities from key SaaS apps when they leave the organization.</span></span>
* <span data-ttu-id="b0ecb-120">為了輕鬆將大量使用者數目匯入特定 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-120">To easily import a bulk number of users into a particular SaaS application.</span></span>
* <span data-ttu-id="b0ecb-121">為了享受讓佈建方案以您針對 Azure AD 單一登入定義的相同應用程式存取原則執行的便利性。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-121">To enjoy the convenience of having your provisioning solution run off of the same app access policies that you defined for Azure AD Single Sign-On.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="b0ecb-122">常見問題集</span><span class="sxs-lookup"><span data-stu-id="b0ecb-122">Frequently Asked Questions</span></span>
<span data-ttu-id="b0ecb-123">**Azure AD 將目錄變更寫入至 SaaS 應用程式的頻率為何？**</span><span class="sxs-lookup"><span data-stu-id="b0ecb-123">**How frequently does Azure AD write directory changes to the SaaS app?**</span></span>

<span data-ttu-id="b0ecb-124">Azure AD 每隔五到十分鐘就會檢查變更。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-124">Azure AD checks for changes every five to ten minutes.</span></span> <span data-ttu-id="b0ecb-125">如果 SaaS 應用程式傳回數個錯誤 (例如無效的系統管理認證)，則 Azure AD 會逐漸降低其頻率，最多每日一次直到修正錯誤為止。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-125">If the SaaS app is returning several errors (such as in the case of invalid admin credentials), then Azure AD will gradually slow its frequency to up to once per day until the errors are fixed.</span></span>

<span data-ttu-id="b0ecb-126">**佈建我的使用者需要多久時間？**</span><span class="sxs-lookup"><span data-stu-id="b0ecb-126">**How long will it take to provision my users?**</span></span>

<span data-ttu-id="b0ecb-127">累加變更幾乎是立即發生，但是如果您嘗試佈建大部分的目錄，則取決於您擁有的使用者和群組數目。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-127">Incremental changes happen nearly instantly but if you are trying to provision most of your directory, then it depends on the number of users and groups that you have.</span></span> <span data-ttu-id="b0ecb-128">小型目錄只需要幾分鐘的時間，中型目錄可能需要數分鐘，而非常大型的目錄可能需要數小時。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-128">Small directories take only a few minutes, medium-sized directories may take several minutes, and very large directories may take several hours.</span></span>

<span data-ttu-id="b0ecb-129">**我要如何追蹤目前佈建作業的進度？**</span><span class="sxs-lookup"><span data-stu-id="b0ecb-129">**How can I track the progress of the current provisioning job?**</span></span>

<span data-ttu-id="b0ecb-130">您可以檢閱目錄的 [報告] 區段底下的 [帳戶佈建報告]。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-130">You can review the Account Provisioning Report under the Reports section of your directory.</span></span> <span data-ttu-id="b0ecb-131">另一個選項是造訪您的佈建目標之 SaaS 應用程式的 [儀表板] 索引標籤，並且查看頁面底部附近的 [整合狀態] 區段底下。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-131">Another option is to visit the Dashboard tab for the SaaS application that you are provisioning to, and look under the "Integration Status" section near the bottom of the page.</span></span>

<span data-ttu-id="b0ecb-132">**如何得知使用者無法正確佈建？**</span><span class="sxs-lookup"><span data-stu-id="b0ecb-132">**How will I know if users fail to get provisioned properly?**</span></span>

<span data-ttu-id="b0ecb-133">在佈建組態精靈的結尾，有一個選項可以訂閱佈建失敗的電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-133">At the end of the provisioning configuration wizard there is an option to subscribe to email notifications for provisioning failures.</span></span> <span data-ttu-id="b0ecb-134">您也可以檢查佈建錯誤報告，以查看哪些使用者無法佈建及其原因。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-134">You can also check the Provisioning Errors Report to see which users failed to be provisioned and why.</span></span>

<span data-ttu-id="b0ecb-135">**Azure AD 是否可以將變更從 SaaS 應用程式寫回至目錄？**</span><span class="sxs-lookup"><span data-stu-id="b0ecb-135">**Can Azure AD write changes from the SaaS app back to the directory?**</span></span>

<span data-ttu-id="b0ecb-136">對於大多數 SaaS 應用程式，佈建僅限輸出，這表示使用者會從目錄寫入應用程式，而變更無法從應用程式寫回至目錄。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-136">For most SaaS apps, provisioning is outbound-only, which means that users are written from the directory to the application, and changes from the application cannot be written back to the directory.</span></span> <span data-ttu-id="b0ecb-137">但是，針對 [Workday](https://msdn.microsoft.com/library/azure/dn762434.aspx)，佈建僅限輸入，這表示使用者會從 Workday 匯入目錄，同樣地，目錄中的變更無法寫回至 Workday。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-137">For [Workday](https://msdn.microsoft.com/library/azure/dn762434.aspx), however, provisioning is inbound-only, which means that that users are imported into the directory from Workday, and likewise, changes in the directory do not get written back into Workday.</span></span>

<span data-ttu-id="b0ecb-138">**我要如何提交意見反應給工程小組？**</span><span class="sxs-lookup"><span data-stu-id="b0ecb-138">**How can I submit feedback to the engineering team?**</span></span>

<span data-ttu-id="b0ecb-139">請透過 [Azure Active Directory 意見反應論壇](https://feedback.azure.com/forums/169401-azure-active-directory/)與我們連絡。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-139">Please contact us through the [Azure Active Directory feedback forum](https://feedback.azure.com/forums/169401-azure-active-directory/).</span></span>

## <a name="how-does-automated-provisioning-work"></a><span data-ttu-id="b0ecb-140">自動化佈建如何運作？</span><span class="sxs-lookup"><span data-stu-id="b0ecb-140">How Does Automated Provisioning Work?</span></span>
<span data-ttu-id="b0ecb-141">Azure AD 會藉由連接到每個應用程式廠商所提供的佈建端點，將使用者佈建至 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-141">Azure AD provisions users to SaaS apps by connecting to provisioning endpoints provided by each application vendor.</span></span> <span data-ttu-id="b0ecb-142">這些端點可以讓 Azure AD 以程式設計方式建立、更新和移除使用者。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-142">These endpoints allow Azure AD to programmatically create, update, and remove users.</span></span> <span data-ttu-id="b0ecb-143">以下是 Azure AD 進行自動化佈建的不同步驟的簡短概觀。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-143">Below is a brief overview of the different steps that Azure AD takes to automate provisioning.</span></span>

1. <span data-ttu-id="b0ecb-144">當您第一次對應用程式啟用佈建時，會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="b0ecb-144">When you enable provisioning for an application for the first time, the following actions are performed:</span></span>
   * <span data-ttu-id="b0ecb-145">Azure AD 會嘗試比對 SaaS 應用程式中任何現有使用者與其在目錄中的對應身分識別。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-145">Azure AD will attempt to match any existing users in the SaaS app with their corresponding identities in the directory.</span></span> <span data-ttu-id="b0ecb-146">若有使用者符合時，就「不會」  自動啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-146">When a user is matched, they are *not* automatically enabled for single sign-on.</span></span> <span data-ttu-id="b0ecb-147">為了讓使用者能存取應用程式，必須在 Azure AD 中直接或透過群組成員資格，明確將他們指派至應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-147">In order for a user to have access to the application, they must be explicitly assigned to the app in Azure AD, either directly or via group membership.</span></span>
   * <span data-ttu-id="b0ecb-148">如果您已經指定哪些使用者應指派給應用程式，且 Azure AD 無法找到這些使用者的現有帳戶，則 Azure AD 會在應用程式中為其佈建新帳戶。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-148">If you have already specified which users should be assigned to the application, and if Azure AD fails to find existing accounts for those users, Azure AD will provision new accounts for them in the application.</span></span>
2. <span data-ttu-id="b0ecb-149">一旦完成上述的初始同步處理之後，Azure AD 會每隔 10 分鐘檢查下列變更：</span><span class="sxs-lookup"><span data-stu-id="b0ecb-149">Once the initial synchronization has been completed as described above, Azure AD will check every 10 minutes for the following changes:</span></span>
   * <span data-ttu-id="b0ecb-150">如果新使用者已指派至應用程式 (直接或透過群組成員資格)，則系統會為他們在 SaaS 應用程式中佈建新的帳戶。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-150">If new users have been assigned to the application (either directly or through group membership), then they will be provisioned a new account in the SaaS app.</span></span>
   * <span data-ttu-id="b0ecb-151">如果已移除使用者的存取權，則其帳戶在 SaaS 應用程式中會標示為停用 (使用者永遠不會完全刪除，以保護您在錯誤設定時不會遺失資料)。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-151">If a user's access has been removed, then their account in the SaaS app will be marked as disabled (users are never fully deleted, which protects you from data loss in the event of a misconfiguration).</span></span>
   * <span data-ttu-id="b0ecb-152">如果使用者最近指派至應用程式，而且他們已經在 SaaS 應用程式中有帳戶，則該帳戶會標示為已啟用，如果相較於目錄是過時的，則可能會更新某些使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-152">If a user was recently assigned to the application and they already had an account in the SaaS app, that account will be marked as enabled, and certain user properties may be updated if they are out-of-date compared to the directory.</span></span>
   * <span data-ttu-id="b0ecb-153">如果使用者的資訊 (例如電話號碼、辦公室位置等等) 在目錄中已變更，則該資訊也會在 SaaS 應用程式中更新。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-153">If a user's information (such as phone number, office location, etc) has been changed in the directory, then that information will also be updated in the SaaS application.</span></span>

<span data-ttu-id="b0ecb-154">如需有關如何在 Azure AD 和 SaaS 應用程式之間對應屬性的詳細資訊，請參閱 [自訂屬性對應](active-directory-saas-customizing-attribute-mappings.md)上的文章。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-154">For more information on how attributes are mapped between Azure AD and your SaaS app, see the article on [Customizing Attribute Mappings](active-directory-saas-customizing-attribute-mappings.md).</span></span>

## <a name="list-of-apps-that-support-automated-user-provisioning"></a><span data-ttu-id="b0ecb-155">支援自動化使用者佈建的應用程式清單</span><span class="sxs-lookup"><span data-stu-id="b0ecb-155">List of Apps that Support Automated User Provisioning</span></span>
<span data-ttu-id="b0ecb-156">Azure AD 應用程式資源庫中的所有「精選」應用程式都支援自動化使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-156">All of the "Featured" apps in the Azure AD application gallery support automated user provisioning.</span></span> [<span data-ttu-id="b0ecb-157">精選應用程式的清單可以在此檢視̂。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-157">The list of featured apps can be viewed here.</span></span>](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured)

<span data-ttu-id="b0ecb-158">為了讓應用程式支援自動化使用者佈建，它必須先提供必要的端點，讓外部程式自動化建立、維護及移除使用者。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-158">In order for an application to support automated user provisioning, it must first provide the necessary endpoints that allow for external programs to automate the creation, maintenance, and removal of users.</span></span> <span data-ttu-id="b0ecb-159">因此，並非所有 SaaS 應用程式都與此功能相容。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-159">Therefore, not all SaaS apps are compatible with this feature.</span></span> <span data-ttu-id="b0ecb-160">針對支援此功能的應用程式，Azure AD 工程小組則是能夠建置與這些應用程式的佈建連接器，這項工作是以目前和潛在客戶的需求來排定優先順序。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-160">For apps that do support this, the Azure AD engineering team will then be able to build a provisioning connector to those apps, and this work is prioritized by the needs of current and prospective customers.</span></span>

<span data-ttu-id="b0ecb-161">若要連絡 Azure AD 工程小組以要求對於其他應用程式的佈建支援，請透過 [Azure Active Directory 意見反應論壇](https://feedback.azure.com/forums/374982-azure-active-directory-application-requests/category/172035-user-provisioning)提交訊息。</span><span class="sxs-lookup"><span data-stu-id="b0ecb-161">To contact the Azure AD engineering team to request provisioning support for additional applications, please submit a message through the [Azure Active Directory feedback forum](https://feedback.azure.com/forums/374982-azure-active-directory-application-requests/category/172035-user-provisioning).</span></span>

## <a name="related-articles"></a><span data-ttu-id="b0ecb-162">相關文章</span><span class="sxs-lookup"><span data-stu-id="b0ecb-162">Related Articles</span></span>
* [<span data-ttu-id="b0ecb-163">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="b0ecb-163">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="b0ecb-164">自訂使用者佈建的屬性對應</span><span class="sxs-lookup"><span data-stu-id="b0ecb-164">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="b0ecb-165">撰寫屬性對應的運算式</span><span class="sxs-lookup"><span data-stu-id="b0ecb-165">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="b0ecb-166">適用於使用者佈建的範圍篩選器</span><span class="sxs-lookup"><span data-stu-id="b0ecb-166">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="b0ecb-167">使用 SCIM 以啟用從 Azure Active Directory 到應用程式的使用者和群組自動佈建</span><span class="sxs-lookup"><span data-stu-id="b0ecb-167">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="b0ecb-168">帳戶佈建通知</span><span class="sxs-lookup"><span data-stu-id="b0ecb-168">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="b0ecb-169">如何整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="b0ecb-169">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)


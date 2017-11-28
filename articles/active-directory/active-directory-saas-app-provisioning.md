---
title: "aaaAutomated SaaS 應用程式使用者佈建 Azure AD 中 |Microsoft 文件"
description: "您可以使用 Azure AD tooautomatically 佈建、 簡介 toohow 解除佈建，並持續更新多個協力廠商 SaaS 應用程式的使用者帳戶。"
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
ms.openlocfilehash: a1f3ecdd513e2b603f8ad9901e9f551b3b982b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automate-user-provisioning-and-deprovisioning-toosaas-applications-with-azure-active-directory"></a><span data-ttu-id="91ecc-103">自動化使用者佈建和解除佈建 tooSaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="91ecc-103">Automate user provisioning and deprovisioning tooSaaS applications with Azure Active Directory</span></span>
## <a name="what-is-automated-user-provisioning-for-saas-apps"></a><span data-ttu-id="91ecc-104">SaaS 應用程式的自動化使用者佈建是什麼？</span><span class="sxs-lookup"><span data-stu-id="91ecc-104">What is automated user provisioning for SaaS apps?</span></span>
<span data-ttu-id="91ecc-105">Azure Active Directory (Azure AD) 可讓您 tooautomate hello 建立、 維護和移除的雲端中的使用者身分 ([SaaS](https://azure.microsoft.com/overview/what-is-saas/)) 應用程式，例如 Dropbox、 Salesforce、 ServiceNow、 等等。</span><span class="sxs-lookup"><span data-stu-id="91ecc-105">Azure Active Directory (Azure AD) allows you tooautomate hello creation, maintenance, and removal of user identities in cloud ([SaaS](https://azure.microsoft.com/overview/what-is-saas/)) applications such as Dropbox, Salesforce, ServiceNow, and more.</span></span>

<span data-ttu-id="91ecc-106">**以下是一些範例項目這項功能可讓您 toodo 的：**</span><span class="sxs-lookup"><span data-stu-id="91ecc-106">**Below are some examples of what this feature allows you toodo:**</span></span>

* <span data-ttu-id="91ecc-107">在自動建立新帳戶 hello 右 SaaS 應用程式為新的人在加入您的小組。</span><span class="sxs-lookup"><span data-stu-id="91ecc-107">Automatically create new accounts in hello right SaaS apps for new people when they join your team.</span></span>
* <span data-ttu-id="91ecc-108">人員勢必會離開 hello 小組時，自動停用從 SaaS 應用程式的帳戶。</span><span class="sxs-lookup"><span data-stu-id="91ecc-108">Automatically deactivate accounts from SaaS apps when people inevitably leave hello team.</span></span>
* <span data-ttu-id="91ecc-109">確保您的 SaaS 應用程式中的 hello 身分識別都保持向上 toodate 根據 hello 目錄中的變更。</span><span class="sxs-lookup"><span data-stu-id="91ecc-109">Ensure that hello identities in your SaaS apps are kept up toodate based on changes in hello directory.</span></span>
* <span data-ttu-id="91ecc-110">非使用者物件，例如群組，支援這些 tooSaaS 應用程式佈建。</span><span class="sxs-lookup"><span data-stu-id="91ecc-110">Provision non-user objects, such as groups, tooSaaS apps that support them.</span></span>

<span data-ttu-id="91ecc-111">**自動的使用者佈建也會包含下列功能的 hello:**</span><span class="sxs-lookup"><span data-stu-id="91ecc-111">**Automated user provisioning also includes hello following functionality:**</span></span>

* <span data-ttu-id="91ecc-112">hello 能力 toomatch 現有之間的身分識別 Azure AD 與 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="91ecc-112">hello ability toomatch existing identities between Azure AD and SaaS apps.</span></span>
* <span data-ttu-id="91ecc-113">Azure AD 的自訂選項 toohelp 容納 hello hello SaaS 應用程式目前正在使用您的組織目前的設定。</span><span class="sxs-lookup"><span data-stu-id="91ecc-113">Customization options toohelp Azure AD fit hello current configurations of hello SaaS apps that your organization is currently using.</span></span>
* <span data-ttu-id="91ecc-114">佈建錯誤的選用電子郵件警示。</span><span class="sxs-lookup"><span data-stu-id="91ecc-114">Optional email alerts for provisioning errors.</span></span>
* <span data-ttu-id="91ecc-115">報告和活動記錄檔 toohelp 監視和疑難排解。</span><span class="sxs-lookup"><span data-stu-id="91ecc-115">Reporting and activity logs toohelp with monitoring and troubleshooting.</span></span>

## <a name="why-use-automated-provisioning"></a><span data-ttu-id="91ecc-116">為何要使用自動化佈建？</span><span class="sxs-lookup"><span data-stu-id="91ecc-116">Why Use Automated Provisioning?</span></span>
<span data-ttu-id="91ecc-117">一些使用這項功能的常見動機包括：</span><span class="sxs-lookup"><span data-stu-id="91ecc-117">Some common motivations for using this feature include:</span></span>

* <span data-ttu-id="91ecc-118">tooavoid hello 成本、 無效率，以及手動佈建程序相關聯的人為錯誤。</span><span class="sxs-lookup"><span data-stu-id="91ecc-118">tooavoid hello costs, inefficiencies, and human error associated with manual provisioning processes.</span></span>
* <span data-ttu-id="91ecc-119">toosecure 立即移除使用者的身分識別，從您的組織金鑰 SaaS 應用程式時離開 hello 組織。</span><span class="sxs-lookup"><span data-stu-id="91ecc-119">toosecure your organization by instantly removing users' identities from key SaaS apps when they leave hello organization.</span></span>
* <span data-ttu-id="91ecc-120">tooeasily 匯入大量使用者數目特定 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="91ecc-120">tooeasily import a bulk number of users into a particular SaaS application.</span></span>
* <span data-ttu-id="91ecc-121">tooenjoy hello 方便起見，讓您佈建的方案從 hello 執行您的 Azure AD 單一登入所定義的相同應用程式存取原則。</span><span class="sxs-lookup"><span data-stu-id="91ecc-121">tooenjoy hello convenience of having your provisioning solution run off of hello same app access policies that you defined for Azure AD Single Sign-On.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="91ecc-122">常見問題集</span><span class="sxs-lookup"><span data-stu-id="91ecc-122">Frequently Asked Questions</span></span>
<span data-ttu-id="91ecc-123">**Azure AD 頻率撰寫目錄變更 toohello SaaS 應用程式？**</span><span class="sxs-lookup"><span data-stu-id="91ecc-123">**How frequently does Azure AD write directory changes toohello SaaS app?**</span></span>

<span data-ttu-id="91ecc-124">Azure AD 會每五鐘顯示 tooten 檢查有變更。</span><span class="sxs-lookup"><span data-stu-id="91ecc-124">Azure AD checks for changes every five tooten minutes.</span></span> <span data-ttu-id="91ecc-125">如果 hello SaaS 應用程式傳回的幾個錯誤 （例如在 hello 大小寫不正確的系統管理員認證），Azure AD 將會逐漸減緩其每日 hello 錯誤修正之前的頻率 tooup tooonce。</span><span class="sxs-lookup"><span data-stu-id="91ecc-125">If hello SaaS app is returning several errors (such as in hello case of invalid admin credentials), then Azure AD will gradually slow its frequency tooup tooonce per day until hello errors are fixed.</span></span>

<span data-ttu-id="91ecc-126">**時間會花費 tooprovision 我的使用者？**</span><span class="sxs-lookup"><span data-stu-id="91ecc-126">**How long will it take tooprovision my users?**</span></span>

<span data-ttu-id="91ecc-127">累加變更，就可能發生幾乎立即嘗試 tooprovision 但大部分的目錄，則依賴 hello 使用者和群組的數目。</span><span class="sxs-lookup"><span data-stu-id="91ecc-127">Incremental changes happen nearly instantly but if you are trying tooprovision most of your directory, then it depends on hello number of users and groups that you have.</span></span> <span data-ttu-id="91ecc-128">小型目錄只需要幾分鐘的時間，中型目錄可能需要數分鐘，而非常大型的目錄可能需要數小時。</span><span class="sxs-lookup"><span data-stu-id="91ecc-128">Small directories take only a few minutes, medium-sized directories may take several minutes, and very large directories may take several hours.</span></span>

<span data-ttu-id="91ecc-129">**如何追蹤 hello hello 的目前佈建作業進度？**</span><span class="sxs-lookup"><span data-stu-id="91ecc-129">**How can I track hello progress of hello current provisioning job?**</span></span>

<span data-ttu-id="91ecc-130">您可以檢閱 hello 報表區段的目錄下的 hello 帳戶佈建報表。</span><span class="sxs-lookup"><span data-stu-id="91ecc-130">You can review hello Account Provisioning Report under hello Reports section of your directory.</span></span> <span data-ttu-id="91ecc-131">另一個選項是 toovisit hello SaaS 應用程式，您要佈建，hello 儀表板索引標籤，然後查看底下 hello hello hello 頁面底部附近的 「 Integration 狀態 」 一節。</span><span class="sxs-lookup"><span data-stu-id="91ecc-131">Another option is toovisit hello Dashboard tab for hello SaaS application that you are provisioning to, and look under hello "Integration Status" section near hello bottom of hello page.</span></span>

<span data-ttu-id="91ecc-132">**我怎麼知道的使用者是否無法佈建正確 tooget？**</span><span class="sxs-lookup"><span data-stu-id="91ecc-132">**How will I know if users fail tooget provisioned properly?**</span></span>

<span data-ttu-id="91ecc-133">結尾 hello hello 有佈建組態精靈是進行佈建失敗選項 toosubscribe tooemail 通知。</span><span class="sxs-lookup"><span data-stu-id="91ecc-133">At hello end of hello provisioning configuration wizard there is an option toosubscribe tooemail notifications for provisioning failures.</span></span> <span data-ttu-id="91ecc-134">您也可以查看哪些使用者無法佈建 toobe hello 佈建錯誤報表 toosee 和原因。</span><span class="sxs-lookup"><span data-stu-id="91ecc-134">You can also check hello Provisioning Errors Report toosee which users failed toobe provisioned and why.</span></span>

<span data-ttu-id="91ecc-135">**Azure AD 可以從 hello SaaS 應用程式後 toohello 目錄寫入變更嗎？**</span><span class="sxs-lookup"><span data-stu-id="91ecc-135">**Can Azure AD write changes from hello SaaS app back toohello directory?**</span></span>

<span data-ttu-id="91ecc-136">針對大部分的 SaaS 應用程式，佈建是僅輸出，這表示使用者會從 hello 目錄 toohello 應用程式、 寫入和 hello 應用程式的變更無法寫回 toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="91ecc-136">For most SaaS apps, provisioning is outbound-only, which means that users are written from hello directory toohello application, and changes from hello application cannot be written back toohello directory.</span></span> <span data-ttu-id="91ecc-137">如[Workday](https://msdn.microsoft.com/library/azure/dn762434.aspx)，不過，佈建僅限輸入，這表示，使用者會匯入至 hello 目錄從 Workday，而且同樣地，hello 目錄中的變更執行未取得寫回至 Workday。</span><span class="sxs-lookup"><span data-stu-id="91ecc-137">For [Workday](https://msdn.microsoft.com/library/azure/dn762434.aspx), however, provisioning is inbound-only, which means that that users are imported into hello directory from Workday, and likewise, changes in hello directory do not get written back into Workday.</span></span>

<span data-ttu-id="91ecc-138">**如何可提交意見反應 toohello 工程小組？**</span><span class="sxs-lookup"><span data-stu-id="91ecc-138">**How can I submit feedback toohello engineering team?**</span></span>

<span data-ttu-id="91ecc-139">請與我們連絡透過 hello [Azure Active Directory 意見反應論壇](https://feedback.azure.com/forums/169401-azure-active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="91ecc-139">Please contact us through hello [Azure Active Directory feedback forum](https://feedback.azure.com/forums/169401-azure-active-directory/).</span></span>

## <a name="how-does-automated-provisioning-work"></a><span data-ttu-id="91ecc-140">自動化佈建如何運作？</span><span class="sxs-lookup"><span data-stu-id="91ecc-140">How Does Automated Provisioning Work?</span></span>
<span data-ttu-id="91ecc-141">Azure AD 佈建使用者 tooSaaS 應用程式，藉由連接提供每個應用程式廠商 tooprovisioning 端點。</span><span class="sxs-lookup"><span data-stu-id="91ecc-141">Azure AD provisions users tooSaaS apps by connecting tooprovisioning endpoints provided by each application vendor.</span></span> <span data-ttu-id="91ecc-142">這些端點可讓 Azure AD tooprogrammatically 建立、 更新及移除使用者。</span><span class="sxs-lookup"><span data-stu-id="91ecc-142">These endpoints allow Azure AD tooprogrammatically create, update, and remove users.</span></span> <span data-ttu-id="91ecc-143">以下是不同的步驟，Azure AD 會佈建 tooautomate hello 的簡短概觀。</span><span class="sxs-lookup"><span data-stu-id="91ecc-143">Below is a brief overview of hello different steps that Azure AD takes tooautomate provisioning.</span></span>

1. <span data-ttu-id="91ecc-144">當您啟用佈建應用程式的 hello 第一次時，請執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="91ecc-144">When you enable provisioning for an application for hello first time, hello following actions are performed:</span></span>
   * <span data-ttu-id="91ecc-145">Azure AD 將會嘗試 toomatch hello SaaS 應用程式中的 hello 目錄中其對應身分識別任何現有使用者。</span><span class="sxs-lookup"><span data-stu-id="91ecc-145">Azure AD will attempt toomatch any existing users in hello SaaS app with their corresponding identities in hello directory.</span></span> <span data-ttu-id="91ecc-146">若有使用者符合時，就「不會」  自動啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="91ecc-146">When a user is matched, they are *not* automatically enabled for single sign-on.</span></span> <span data-ttu-id="91ecc-147">為了讓使用者 toohave 存取 toohello 應用程式，則必須明確地指派 toohello 應用程式在 Azure AD 中直接或透過群組成員資格。</span><span class="sxs-lookup"><span data-stu-id="91ecc-147">In order for a user toohave access toohello application, they must be explicitly assigned toohello app in Azure AD, either directly or via group membership.</span></span>
   * <span data-ttu-id="91ecc-148">如果您已經指定哪些使用者應該指派 toohello 應用程式，且 Azure AD 失敗 toofind 現有的帳戶，這些使用者，Azure AD 將會在佈建新帳戶，hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="91ecc-148">If you have already specified which users should be assigned toohello application, and if Azure AD fails toofind existing accounts for those users, Azure AD will provision new accounts for them in hello application.</span></span>
2. <span data-ttu-id="91ecc-149">一旦完成 hello 初始同步處理之後上面所述，Azure AD 會檢查每隔 10 分鐘 hello 下列變更：</span><span class="sxs-lookup"><span data-stu-id="91ecc-149">Once hello initial synchronization has been completed as described above, Azure AD will check every 10 minutes for hello following changes:</span></span>
   * <span data-ttu-id="91ecc-150">如果新的使用者已指派給 toohello 應用程式 （直接或透過群組成員資格），然後將其佈建 hello SaaS 應用程式中的新帳戶。</span><span class="sxs-lookup"><span data-stu-id="91ecc-150">If new users have been assigned toohello application (either directly or through group membership), then they will be provisioned a new account in hello SaaS app.</span></span>
   * <span data-ttu-id="91ecc-151">如果已移除使用者的存取權，則 hello SaaS 應用程式中的帳戶將會標示為停用 （絕對不會完全刪除使用者，這會防止您的設定不正確的 hello 事件中的資料遺失）。</span><span class="sxs-lookup"><span data-stu-id="91ecc-151">If a user's access has been removed, then their account in hello SaaS app will be marked as disabled (users are never fully deleted, which protects you from data loss in hello event of a misconfiguration).</span></span>
   * <span data-ttu-id="91ecc-152">如果使用者最近指派 toohello 應用程式，且他們已經有帳戶 hello SaaS 應用程式中帳戶將會標示為已啟用，以及在有過期的時間比較的 toohello 目錄，可能會更新某些使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="91ecc-152">If a user was recently assigned toohello application and they already had an account in hello SaaS app, that account will be marked as enabled, and certain user properties may be updated if they are out-of-date compared toohello directory.</span></span>
   * <span data-ttu-id="91ecc-153">如果 hello 目錄中已經變更使用者的資訊 （例如電話、 辦公室位置等等），則該資訊都會也更新 hello SaaS 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="91ecc-153">If a user's information (such as phone number, office location, etc) has been changed in hello directory, then that information will also be updated in hello SaaS application.</span></span>

<span data-ttu-id="91ecc-154">如需有關 Azure AD 之間如何對應屬性及 SaaS 應用程式，請參閱 hello 文件[自訂屬性對應](active-directory-saas-customizing-attribute-mappings.md)。</span><span class="sxs-lookup"><span data-stu-id="91ecc-154">For more information on how attributes are mapped between Azure AD and your SaaS app, see hello article on [Customizing Attribute Mappings](active-directory-saas-customizing-attribute-mappings.md).</span></span>

## <a name="list-of-apps-that-support-automated-user-provisioning"></a><span data-ttu-id="91ecc-155">支援自動化使用者佈建的應用程式清單</span><span class="sxs-lookup"><span data-stu-id="91ecc-155">List of Apps that Support Automated User Provisioning</span></span>
<span data-ttu-id="91ecc-156">所有 hello Azure AD 應用程式庫中的 hello 「 精選 」 應用程式都支援自動的使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="91ecc-156">All of hello "Featured" apps in hello Azure AD application gallery support automated user provisioning.</span></span> [<span data-ttu-id="91ecc-157">hello 份精選應用程式可以在此檢視。</span><span class="sxs-lookup"><span data-stu-id="91ecc-157">hello list of featured apps can be viewed here.</span></span>](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured)

<span data-ttu-id="91ecc-158">為了讓應用程式 toosupport 自動化使用者佈建，它必須先提供 hello 允許外部程式 tooautomate hello 建立、 維護和移除使用者的必要端點。</span><span class="sxs-lookup"><span data-stu-id="91ecc-158">In order for an application toosupport automated user provisioning, it must first provide hello necessary endpoints that allow for external programs tooautomate hello creation, maintenance, and removal of users.</span></span> <span data-ttu-id="91ecc-159">因此，並非所有 SaaS 應用程式都與此功能相容。</span><span class="sxs-lookup"><span data-stu-id="91ecc-159">Therefore, not all SaaS apps are compatible with this feature.</span></span> <span data-ttu-id="91ecc-160">針對支援此應用程式，hello Azure AD 的工程小組將則無法 toobuild 佈建的連接器 toothose 應用程式，而且這項工作已設定優先權，由 hello 的目前和潛在客戶的需求。</span><span class="sxs-lookup"><span data-stu-id="91ecc-160">For apps that do support this, hello Azure AD engineering team will then be able toobuild a provisioning connector toothose apps, and this work is prioritized by hello needs of current and prospective customers.</span></span>

<span data-ttu-id="91ecc-161">toocontact hello Azure AD 的工程小組 toorequest 佈建其他的應用程式的支援，請送出 hello 訊息[Azure Active Directory 意見反應論壇](https://feedback.azure.com/forums/374982-azure-active-directory-application-requests/category/172035-user-provisioning)。</span><span class="sxs-lookup"><span data-stu-id="91ecc-161">toocontact hello Azure AD engineering team toorequest provisioning support for additional applications, please submit a message through hello [Azure Active Directory feedback forum](https://feedback.azure.com/forums/374982-azure-active-directory-application-requests/category/172035-user-provisioning).</span></span>

## <a name="related-articles"></a><span data-ttu-id="91ecc-162">相關文章</span><span class="sxs-lookup"><span data-stu-id="91ecc-162">Related Articles</span></span>
* [<span data-ttu-id="91ecc-163">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="91ecc-163">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="91ecc-164">自訂使用者佈建的屬性對應</span><span class="sxs-lookup"><span data-stu-id="91ecc-164">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="91ecc-165">撰寫屬性對應的運算式</span><span class="sxs-lookup"><span data-stu-id="91ecc-165">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="91ecc-166">適用於使用者佈建的範圍篩選器</span><span class="sxs-lookup"><span data-stu-id="91ecc-166">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="91ecc-167">使用 SCIM tooenable 自動佈建的 Azure Active Directory tooapplications 來自使用者和群組</span><span class="sxs-lookup"><span data-stu-id="91ecc-167">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="91ecc-168">帳戶佈建通知</span><span class="sxs-lookup"><span data-stu-id="91ecc-168">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="91ecc-169">如何教學課程清單 tooIntegrate SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="91ecc-169">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)


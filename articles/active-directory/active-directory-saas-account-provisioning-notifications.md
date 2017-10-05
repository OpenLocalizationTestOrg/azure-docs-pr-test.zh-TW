---
title: "帳戶佈建通知 | Microsoft Docs"
description: "藉由啟用帳戶佈建通知，了解如何確保您會收到與使用者佈建相關問題的通知要您特別注意。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a637aac7-f06b-48ef-a66d-639835a8edec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: b99037fc28eca1a3ebffefb9e99991e74f52c9a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="account-provisioning-notifications"></a><span data-ttu-id="3edd8-103">帳戶佈建通知</span><span class="sxs-lookup"><span data-stu-id="3edd8-103">Account Provisioning Notifications</span></span>
<span data-ttu-id="3edd8-104">透過使用者佈建，您可以自動化在協力廠商 SaaS 應用程式中管理使用者的程序。</span><span class="sxs-lookup"><span data-stu-id="3edd8-104">With user provisioning, you can automate the process of managing users in third party SaaS applications.</span></span> <br>
<span data-ttu-id="3edd8-105">雖然這是自動化的程序，但是您還是不時需要與此程序互動。</span><span class="sxs-lookup"><span data-stu-id="3edd8-105">While this is an automated process, your interaction with this process is from time to time required.</span></span> <br>
<span data-ttu-id="3edd8-106">例如以下這個範例，當您設定與協力廠商 SaaS 應用程式交換資料的帳戶密碼已經到期。</span><span class="sxs-lookup"><span data-stu-id="3edd8-106">This is, for example the case, when the password of the account you have configured to exchange data with a third party SaaS application has expired.</span></span> 

<span data-ttu-id="3edd8-107">藉由啟用帳戶佈建通知，您就可以確保您會收到與使用者佈建相關問題的通知要您特別注意。</span><span class="sxs-lookup"><span data-stu-id="3edd8-107">By enabling account provisioning notifications, you can ensure that you are notified of issues related to user provisioning that require your attention.</span></span>

<span data-ttu-id="3edd8-108">您在為協力廠商 SaaS 應用程式設定使用者佈建時，就可以啟用或停用帳戶佈建通知。</span><span class="sxs-lookup"><span data-stu-id="3edd8-108">You activate or deactivate account provisioning notifications as part of your user provisioning configuration for a third party SaaS application.</span></span>

![使用者佈建][1] 

<span data-ttu-id="3edd8-110">若要啟用帳戶佈建通知，請在 [確認]  對話方塊頁面上選取相關的核取方塊，然後輸入收件者的電子郵件別名。</span><span class="sxs-lookup"><span data-stu-id="3edd8-110">To activate account provisioning notifications, select the related checkbox on the **Confirmation** dialog page, and then type the email alias of the recipient.</span></span>

![帳戶佈建通知][2]

<span data-ttu-id="3edd8-112">您可以輸入通訊群組清單做為收件者。不過請務必注意，通知電子郵件所包含的報表連結，只能由 Azure AD 系統管理員存取。</span><span class="sxs-lookup"><span data-stu-id="3edd8-112">You can enter a distribution list as recipient; however, it is important to note that the notification email contains links to reports that are only accessible by the Azure AD administrators.</span></span>

<span data-ttu-id="3edd8-113">如果您啟用了帳戶佈建通知，您將會收到電子郵件，通知您與使用者佈建相關的重大問題。</span><span class="sxs-lookup"><span data-stu-id="3edd8-113">If you have account provisioning notifications enabled, you will receive emails about critical issues that are related to user provisioning.</span></span> <span data-ttu-id="3edd8-114">不過為了避免電子郵件多載，對於已啟用電子郵件通知的每個 SaaS 應用程式，您每天只會收到一封通知電子郵件。</span><span class="sxs-lookup"><span data-stu-id="3edd8-114">However, to avoid an email overload, you will only receive one notification email per day for each SaaS application the notification email is enabled for.</span></span>

## <a name="related-articles"></a><span data-ttu-id="3edd8-115">相關文章</span><span class="sxs-lookup"><span data-stu-id="3edd8-115">Related Articles</span></span>
* [<span data-ttu-id="3edd8-116">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="3edd8-116">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="3edd8-117">自動化 SaaS 應用程式使用者佈建/解除佈建</span><span class="sxs-lookup"><span data-stu-id="3edd8-117">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="3edd8-118">自訂使用者佈建的屬性對應</span><span class="sxs-lookup"><span data-stu-id="3edd8-118">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="3edd8-119">撰寫屬性對應的運算式</span><span class="sxs-lookup"><span data-stu-id="3edd8-119">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="3edd8-120">適用於使用者佈建的範圍篩選器</span><span class="sxs-lookup"><span data-stu-id="3edd8-120">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="3edd8-121">使用 SCIM 以啟用從 Azure Active Directory 到應用程式的使用者和群組自動佈建</span><span class="sxs-lookup"><span data-stu-id="3edd8-121">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="3edd8-122">如何整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="3edd8-122">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-account-provisioning-notifications/ic766307.png
[2]: ./media/active-directory-saas-account-provisioning-notifications/ic766308.png

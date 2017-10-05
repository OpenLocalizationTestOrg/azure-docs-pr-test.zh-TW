---
title: "開發適用於 Azure AD 的應用程式 | Microsoft Docs'"
description: "針對 IT 專業人員所撰寫，本文提供整合 Azure 應用程式與 Active Directory 的指導方針。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: dd69f2bc-37c5-457c-857d-27acb84267fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6b119be9c06d8c1ccc8e747168429e6c2d2e7a8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a><span data-ttu-id="0af9d-103">開發適用於 Azure Active Directory 的企業營運應用程式</span><span class="sxs-lookup"><span data-stu-id="0af9d-103">Develop line-of-business apps for Azure Active Directory</span></span>
<span data-ttu-id="0af9d-104">本指南提供開發適用於 Azure Active Directory (AD) 的企業營運 (LoB) 應用程式的概觀。適用對象為 Active Directory/Office 365 全域系統管理員。</span><span class="sxs-lookup"><span data-stu-id="0af9d-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).The intended audience is Active Directory/Office 365 global administrators.</span></span>

## <a name="overview"></a><span data-ttu-id="0af9d-105">概觀</span><span class="sxs-lookup"><span data-stu-id="0af9d-105">Overview</span></span>
<span data-ttu-id="0af9d-106">建置整合 Azure AD 的應用程式，可讓您組織的使用者使用 Office 365 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0af9d-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span></span> <span data-ttu-id="0af9d-107">將應用程式置於 Azure AD 中可讓您掌控應用程式設定的驗證原則。</span><span class="sxs-lookup"><span data-stu-id="0af9d-107">Having the application in Azure AD gives you control over the authentication policy for the application.</span></span> <span data-ttu-id="0af9d-108">若要深入了解條件式存取和如何使用多重要素驗證 (MFA) 來保護應用程式，請參閱 [設定存取規則](active-directory-conditional-access-azuread-connected-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="0af9d-108">To learn more about conditional access and how to protect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

<span data-ttu-id="0af9d-109">註冊應用程式以使用 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="0af9d-109">Register your application to use Azure Active Directory.</span></span> <span data-ttu-id="0af9d-110">註冊應用程式意謂著開發人員可以使用 Azure AD 來驗證使用者，以及要求對使用者資源 (例如電子郵件、行事曆及文件) 的存取權。</span><span class="sxs-lookup"><span data-stu-id="0af9d-110">Registering the application means that your developers can use Azure AD to authenticate users and request access to user resources such as email, calendar, and documents.</span></span>

<span data-ttu-id="0af9d-111">您目錄的任何成員 (不是來賓) 都可以註冊應用程式，亦稱為 *建立應用程式物件*。</span><span class="sxs-lookup"><span data-stu-id="0af9d-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span></span>

<span data-ttu-id="0af9d-112">註冊應用程式可讓任一使用者執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="0af9d-112">Registering an application allows any user to do the following:</span></span>

* <span data-ttu-id="0af9d-113">取得 Azure AD 識別的應用程式的身分識別</span><span class="sxs-lookup"><span data-stu-id="0af9d-113">Get an identity for their application that Azure AD recognizes</span></span>
* <span data-ttu-id="0af9d-114">取得應用程式可用來向 AD 驗證其身分的一個或多個密碼/金鑰</span><span class="sxs-lookup"><span data-stu-id="0af9d-114">Get one or more secrets/keys that the application can use to authenticate itself to AD</span></span>
* <span data-ttu-id="0af9d-115">在 Azure 入口網站中以自訂名稱、標誌等指定應用程式的品牌形象</span><span class="sxs-lookup"><span data-stu-id="0af9d-115">Brand the application in the Azure portal with a custom name, logo, etc.</span></span>
* <span data-ttu-id="0af9d-116">將 Azure AD 授權功能套用至其應用程式，包括：</span><span class="sxs-lookup"><span data-stu-id="0af9d-116">Apply Azure AD authorization features to their app, including:</span></span>

  * <span data-ttu-id="0af9d-117">角色型存取控制 (RBAC)</span><span class="sxs-lookup"><span data-stu-id="0af9d-117">Role-Based Access Control (RBAC)</span></span>
  * <span data-ttu-id="0af9d-118">以 Azure Active Directory 做為 oAuth 授權伺服器 (保護應用程式公開的 API)</span><span class="sxs-lookup"><span data-stu-id="0af9d-118">Azure Active Directory as oAuth authorization server (secure an API exposed by the application)</span></span>
* <span data-ttu-id="0af9d-119">宣告讓應用程式如預期般運作所需的必要權限，包括：</span><span class="sxs-lookup"><span data-stu-id="0af9d-119">Declare required permissions necessary for the application to function as expected, including:</span></span>

      - <span data-ttu-id="0af9d-120">應用程式權限 (僅限全域系統管理員)。</span><span class="sxs-lookup"><span data-stu-id="0af9d-120">App permissions (global administrators only).</span></span> <span data-ttu-id="0af9d-121">例如：另一個 Azure AD 應用程式中的角色成員資格，或相對於「Azure 資源」、「資源群組」或「訂用帳戶」的角色成員資格</span><span class="sxs-lookup"><span data-stu-id="0af9d-121">For example: Role membership in another Azure AD application or role membership relative to an Azure Resource, Resource Group, or Subscription</span></span>
      - <span data-ttu-id="0af9d-122">委派的權限 (任何使用者)。</span><span class="sxs-lookup"><span data-stu-id="0af9d-122">Delegated permissions (any user).</span></span> <span data-ttu-id="0af9d-123">例如：Azure AD、登入及讀取設定檔</span><span class="sxs-lookup"><span data-stu-id="0af9d-123">For example: Azure AD, Sign-in, and Read Profile</span></span>

> [!NOTE]
> <span data-ttu-id="0af9d-124">根據預設，任何成員都可以註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="0af9d-124">By default, any member can register an application.</span></span> <span data-ttu-id="0af9d-125">若要了解如何限制向特定成員註冊應用程式的權限，請參閱 [如何將應用程式新增到 Azure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance)。</span><span class="sxs-lookup"><span data-stu-id="0af9d-125">To learn how to restrict permissions for registering applications to specific members, see [How applications are added to Azure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span></span>
>
>

<span data-ttu-id="0af9d-126">身為全域系統管理員，若要協助開發人員完成讓應用程式進入生產階段的準備工作，您必須執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="0af9d-126">Here’s what you, the global administrator, need to do to help developers make their application ready for production:</span></span>

* <span data-ttu-id="0af9d-127">設定存取規則 (存取原則/MFA)</span><span class="sxs-lookup"><span data-stu-id="0af9d-127">Configure access rules (access policy/MFA)</span></span>
* <span data-ttu-id="0af9d-128">設定應用程式要求指派使用者並指派使用者</span><span class="sxs-lookup"><span data-stu-id="0af9d-128">Configure the app to require user assignment and assign users</span></span>
* <span data-ttu-id="0af9d-129">隱藏預設的使用者同意體驗</span><span class="sxs-lookup"><span data-stu-id="0af9d-129">Suppress the default user consent experience</span></span>

## <a name="configure-access-rules"></a><span data-ttu-id="0af9d-130">設定存取規則</span><span class="sxs-lookup"><span data-stu-id="0af9d-130">Configure access rules</span></span>
<span data-ttu-id="0af9d-131">針對您的 SaaS 應用程式設定每個應用程式的存取規則</span><span class="sxs-lookup"><span data-stu-id="0af9d-131">Configure per-application access rules to your SaaS apps.</span></span> <span data-ttu-id="0af9d-132">例如，您可以要求執行 MFA 或只允許受信任網路上的使用者進行存取。</span><span class="sxs-lookup"><span data-stu-id="0af9d-132">For example, you can require MFA or only allow access to users on trusted networks.</span></span> <span data-ttu-id="0af9d-133">如需這方面的詳細資料，請參閱[設定存取規則](active-directory-conditional-access-azuread-connected-apps.md)文件。</span><span class="sxs-lookup"><span data-stu-id="0af9d-133">The details for this are available in the document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

## <a name="configure-the-app-to-require-user-assignment-and-assign-users"></a><span data-ttu-id="0af9d-134">設定應用程式要求指派使用者並指派使用者</span><span class="sxs-lookup"><span data-stu-id="0af9d-134">Configure the app to require user assignment and assign users</span></span>
<span data-ttu-id="0af9d-135">根據預設，使用者不須獲得指派，即可存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="0af9d-135">By default, users can access applications without being assigned.</span></span> <span data-ttu-id="0af9d-136">不過，如果應用程式公開角色或您希望應用程式出現在使用者的存取面板上，則應該要求指派使用者。</span><span class="sxs-lookup"><span data-stu-id="0af9d-136">However, if the application exposes roles or if you want the application to appear on a user’s access panel, you should require user assignment.</span></span>

[<span data-ttu-id="0af9d-137">需要指派使用者</span><span class="sxs-lookup"><span data-stu-id="0af9d-137">Requiring user assignment</span></span>](active-directory-applications-guiding-developers-requiring-user-assignment.md)

<span data-ttu-id="0af9d-138">如果您是 Azure AD Premium 或 Enterprise Mobility Suite (EMS) 的訂閱者，則強烈建議使用群組。</span><span class="sxs-lookup"><span data-stu-id="0af9d-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span></span> <span data-ttu-id="0af9d-139">將群組指派給應用程式，可讓您將持續進行的存取管理委派給群組擁有者。</span><span class="sxs-lookup"><span data-stu-id="0af9d-139">Assigning groups to the application allows you to delegate ongoing access management to the owner of the group.</span></span> <span data-ttu-id="0af9d-140">您可以建立群組，或使用群組管理功能要求您組織中負責的對象建立群組。</span><span class="sxs-lookup"><span data-stu-id="0af9d-140">You can create the group or ask the responsible party in your organization to create the group using your group management facility.</span></span>

[<span data-ttu-id="0af9d-141">將使用者指派給應用程式</span><span class="sxs-lookup"><span data-stu-id="0af9d-141">Assigning users to an application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)  
[<span data-ttu-id="0af9d-142">將群組指派給應用程式</span><span class="sxs-lookup"><span data-stu-id="0af9d-142">Assigning groups to an application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a><span data-ttu-id="0af9d-143">隱藏使用者同意</span><span class="sxs-lookup"><span data-stu-id="0af9d-143">Suppress user consent</span></span>
<span data-ttu-id="0af9d-144">根據預設，每個使用者都必須經歷同意體驗才能登入。</span><span class="sxs-lookup"><span data-stu-id="0af9d-144">By default, each user goes through a consent experience to sign in.</span></span> <span data-ttu-id="0af9d-145">同意體驗 (要求使用者將權限授與應用程式) 會使得不熟悉做這類決定的使用者不知所措。</span><span class="sxs-lookup"><span data-stu-id="0af9d-145">The consent experience, asking users to grant permissions to an application, can be disconcerting for users who are unfamiliar with making such decisions.</span></span>

<span data-ttu-id="0af9d-146">對於您信任的應用程式，您可以代表您的組織來同意應用程式，以簡化使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="0af9d-146">For applications that you trust, you can simplify the user experience by consenting to the application on behalf of your organization.</span></span>

<span data-ttu-id="0af9d-147">如需有關 Azure 中使用者同意和同意體驗的詳細資訊，請參閱 [整合應用程式與 Azure Active Directory](active-directory-integrating-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="0af9d-147">For more information about user consent and the consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="0af9d-148">相關文章</span><span class="sxs-lookup"><span data-stu-id="0af9d-148">Related Articles</span></span>
* [<span data-ttu-id="0af9d-149">使用 Azure AD 應用程式 Proxy 啟用對內部部署應用程式的安全遠端存取</span><span class="sxs-lookup"><span data-stu-id="0af9d-149">Enable secure remote access to on-premises applications with Azure AD Application Proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="0af9d-150">SaaS 應用程式的 Azure 條件式存取預覽</span><span class="sxs-lookup"><span data-stu-id="0af9d-150">Azure Conditional Access Preview for SaaS Apps</span></span>](active-directory-conditional-access-azuread-connected-apps.md)
* [<span data-ttu-id="0af9d-151">使用 Azure AD 管理應用程式的存取</span><span class="sxs-lookup"><span data-stu-id="0af9d-151">Managing access to apps with Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="0af9d-152">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="0af9d-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

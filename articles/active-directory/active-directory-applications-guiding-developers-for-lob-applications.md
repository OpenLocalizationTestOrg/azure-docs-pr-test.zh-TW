---
title: "Azure AD 的 aaaDevelop 應用程式 |Microsoft 文件 '"
description: "這篇文章針對 hello IT 專業人員所撰寫，與 Active Directory 整合 Azure 應用程式提供指導方針。"
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
ms.openlocfilehash: d2924be752af0be2843b1d9b74d9ec446d3fe1ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a><span data-ttu-id="27776-103">開發適用於 Azure Active Directory 的企業營運應用程式</span><span class="sxs-lookup"><span data-stu-id="27776-103">Develop line-of-business apps for Azure Active Directory</span></span>
<span data-ttu-id="27776-104">本指南提供的開發特定業務 (LoB) 應用程式的 Azure Active Directory (AD).hello 概觀主要適用對象是 Active Directory/Office 365 全域管理員。</span><span class="sxs-lookup"><span data-stu-id="27776-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).hello intended audience is Active Directory/Office 365 global administrators.</span></span>

## <a name="overview"></a><span data-ttu-id="27776-105">概觀</span><span class="sxs-lookup"><span data-stu-id="27776-105">Overview</span></span>
<span data-ttu-id="27776-106">建置整合 Azure AD 的應用程式，可讓您組織的使用者使用 Office 365 單一登入。</span><span class="sxs-lookup"><span data-stu-id="27776-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span></span> <span data-ttu-id="27776-107">Azure AD 可讓您控制 hello hello 應用程式的驗證原則中都有 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="27776-107">Having hello application in Azure AD gives you control over hello authentication policy for hello application.</span></span> <span data-ttu-id="27776-108">深入了解條件式存取並 tooprotect 應用程式與多重要素驗證 (MFA) 如何查看 toolearn[設定存取規則](active-directory-conditional-access-azuread-connected-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="27776-108">toolearn more about conditional access and how tooprotect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

<span data-ttu-id="27776-109">註冊您的應用程式 toouse Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="27776-109">Register your application toouse Azure Active Directory.</span></span> <span data-ttu-id="27776-110">註冊 hello 應用程式時，表示您的開發人員可以使用 Azure AD tooauthenticate 使用者，並要求存取 toouser 資源，例如電子郵件、 行事曆及文件。</span><span class="sxs-lookup"><span data-stu-id="27776-110">Registering hello application means that your developers can use Azure AD tooauthenticate users and request access toouser resources such as email, calendar, and documents.</span></span>

<span data-ttu-id="27776-111">您目錄的任何成員 (不是來賓) 都可以註冊應用程式，亦稱為 *建立應用程式物件*。</span><span class="sxs-lookup"><span data-stu-id="27776-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span></span>

<span data-ttu-id="27776-112">登錄應用程式可讓任何使用者 toodo hello 下列：</span><span class="sxs-lookup"><span data-stu-id="27776-112">Registering an application allows any user toodo hello following:</span></span>

* <span data-ttu-id="27776-113">取得 Azure AD 識別的應用程式的身分識別</span><span class="sxs-lookup"><span data-stu-id="27776-113">Get an identity for their application that Azure AD recognizes</span></span>
* <span data-ttu-id="27776-114">取得一個或多個密碼/金鑰 hello 應用程式可以使用本身 tooauthenticate tooAD</span><span class="sxs-lookup"><span data-stu-id="27776-114">Get one or more secrets/keys that hello application can use tooauthenticate itself tooAD</span></span>
* <span data-ttu-id="27776-115">在 hello Azure 入口網站的自訂名稱、 標誌等品牌 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="27776-115">Brand hello application in hello Azure portal with a custom name, logo, etc.</span></span>
* <span data-ttu-id="27776-116">適用於 Azure AD 授權功能 tootheir 應用程式，包括：</span><span class="sxs-lookup"><span data-stu-id="27776-116">Apply Azure AD authorization features tootheir app, including:</span></span>

  * <span data-ttu-id="27776-117">角色型存取控制 (RBAC)</span><span class="sxs-lookup"><span data-stu-id="27776-117">Role-Based Access Control (RBAC)</span></span>
  * <span data-ttu-id="27776-118">為 oAuth 授權伺服器的 azure Active Directory （安全 hello 應用程式所公開的 API）</span><span class="sxs-lookup"><span data-stu-id="27776-118">Azure Active Directory as oAuth authorization server (secure an API exposed by hello application)</span></span>
* <span data-ttu-id="27776-119">宣告所需的權限所需的 hello 應用程式 toofunction，如預期般，包括：</span><span class="sxs-lookup"><span data-stu-id="27776-119">Declare required permissions necessary for hello application toofunction as expected, including:</span></span>

      - <span data-ttu-id="27776-120">應用程式權限 (僅限全域系統管理員)。</span><span class="sxs-lookup"><span data-stu-id="27776-120">App permissions (global administrators only).</span></span> <span data-ttu-id="27776-121">例如： 角色成員資格，在另一個 Azure AD 應用程式或角色成員資格相對 tooan Azure 資源，資源群組或訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="27776-121">For example: Role membership in another Azure AD application or role membership relative tooan Azure Resource, Resource Group, or Subscription</span></span>
      - <span data-ttu-id="27776-122">委派的權限 (任何使用者)。</span><span class="sxs-lookup"><span data-stu-id="27776-122">Delegated permissions (any user).</span></span> <span data-ttu-id="27776-123">例如：Azure AD、登入及讀取設定檔</span><span class="sxs-lookup"><span data-stu-id="27776-123">For example: Azure AD, Sign-in, and Read Profile</span></span>

> [!NOTE]
> <span data-ttu-id="27776-124">根據預設，任何成員都可以註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="27776-124">By default, any member can register an application.</span></span> <span data-ttu-id="27776-125">如何 toorestrict 使用權限註冊應用程式 toospecific 成員，請參閱的 toolearn[應用程式如何加入 tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance)。</span><span class="sxs-lookup"><span data-stu-id="27776-125">toolearn how toorestrict permissions for registering applications toospecific members, see [How applications are added tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span></span>
>
>

<span data-ttu-id="27776-126">以下是您，hello 全域管理員，需要 toodo toohelp 開發人員透過他們的應用程式準備好實際執行：</span><span class="sxs-lookup"><span data-stu-id="27776-126">Here’s what you, hello global administrator, need toodo toohelp developers make their application ready for production:</span></span>

* <span data-ttu-id="27776-127">設定存取規則 (存取原則/MFA)</span><span class="sxs-lookup"><span data-stu-id="27776-127">Configure access rules (access policy/MFA)</span></span>
* <span data-ttu-id="27776-128">設定 hello 應用程式 toorequire 使用者指派，並將使用者指派</span><span class="sxs-lookup"><span data-stu-id="27776-128">Configure hello app toorequire user assignment and assign users</span></span>
* <span data-ttu-id="27776-129">隱藏 hello 預設使用者同意經驗</span><span class="sxs-lookup"><span data-stu-id="27776-129">Suppress hello default user consent experience</span></span>

## <a name="configure-access-rules"></a><span data-ttu-id="27776-130">設定存取規則</span><span class="sxs-lookup"><span data-stu-id="27776-130">Configure access rules</span></span>
<span data-ttu-id="27776-131">設定每個應用程式的存取規則 tooyour SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="27776-131">Configure per-application access rules tooyour SaaS apps.</span></span> <span data-ttu-id="27776-132">例如，您可以要求使用 MFA，或只允許存取 toousers 受信任的網路。</span><span class="sxs-lookup"><span data-stu-id="27776-132">For example, you can require MFA or only allow access toousers on trusted networks.</span></span> <span data-ttu-id="27776-133">hello 文件中的 hello 詳細資料，這可用[設定存取規則](active-directory-conditional-access-azuread-connected-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="27776-133">hello details for this are available in hello document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

## <a name="configure-hello-app-toorequire-user-assignment-and-assign-users"></a><span data-ttu-id="27776-134">設定 hello 應用程式 toorequire 使用者指派，並將使用者指派</span><span class="sxs-lookup"><span data-stu-id="27776-134">Configure hello app toorequire user assignment and assign users</span></span>
<span data-ttu-id="27776-135">根據預設，使用者不須獲得指派，即可存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="27776-135">By default, users can access applications without being assigned.</span></span> <span data-ttu-id="27776-136">不過，如果 hello 應用程式公開的角色，或您想要將應用程式 tooappear hello 使用者的存取面板上，您應該要求使用者指派。</span><span class="sxs-lookup"><span data-stu-id="27776-136">However, if hello application exposes roles or if you want hello application tooappear on a user’s access panel, you should require user assignment.</span></span>

[<span data-ttu-id="27776-137">要求使用者指派</span><span class="sxs-lookup"><span data-stu-id="27776-137">Requiring user assignment</span></span>](active-directory-applications-guiding-developers-requiring-user-assignment.md)

<span data-ttu-id="27776-138">如果您是 Azure AD Premium 或 Enterprise Mobility Suite (EMS) 的訂閱者，則強烈建議使用群組。</span><span class="sxs-lookup"><span data-stu-id="27776-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span></span> <span data-ttu-id="27776-139">將群組指派 toohello 應用程式可讓您 toodelegate 持續存取管理 toohello 群組的擁有者 hello。</span><span class="sxs-lookup"><span data-stu-id="27776-139">Assigning groups toohello application allows you toodelegate ongoing access management toohello owner of hello group.</span></span> <span data-ttu-id="27776-140">您可以建立 hello 群組，或要求使用群組管理設備組織 toocreate hello 群組中的 hello 負責合作對象。</span><span class="sxs-lookup"><span data-stu-id="27776-140">You can create hello group or ask hello responsible party in your organization toocreate hello group using your group management facility.</span></span>

[<span data-ttu-id="27776-141">將使用者指派 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="27776-141">Assigning users tooan application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)  
[<span data-ttu-id="27776-142">將群組指派 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="27776-142">Assigning groups tooan application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a><span data-ttu-id="27776-143">隱藏使用者同意</span><span class="sxs-lookup"><span data-stu-id="27776-143">Suppress user consent</span></span>
<span data-ttu-id="27776-144">根據預設，每個使用者經歷了同意體驗 toosign 中。</span><span class="sxs-lookup"><span data-stu-id="27776-144">By default, each user goes through a consent experience toosign in.</span></span> <span data-ttu-id="27776-145">hello 同意體驗，詢問使用者 toogrant 權限 tooan 應用程式，可以是令人不安的使用者不熟悉這類的決策。</span><span class="sxs-lookup"><span data-stu-id="27776-145">hello consent experience, asking users toogrant permissions tooan application, can be disconcerting for users who are unfamiliar with making such decisions.</span></span>

<span data-ttu-id="27776-146">對於您信任的應用程式，您可以簡化 hello 使用者體驗同意 toohello 應用程式代表您的組織。</span><span class="sxs-lookup"><span data-stu-id="27776-146">For applications that you trust, you can simplify hello user experience by consenting toohello application on behalf of your organization.</span></span>

<span data-ttu-id="27776-147">如需有關使用者同意和 hello 同意體驗 Azure 中，請參閱[整合應用程式與 Azure Active Directory](active-directory-integrating-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="27776-147">For more information about user consent and hello consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="27776-148">相關文章</span><span class="sxs-lookup"><span data-stu-id="27776-148">Related Articles</span></span>
* [<span data-ttu-id="27776-149">啟用安全的遠端存取 tooon 內部部署應用程式與 Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="27776-149">Enable secure remote access tooon-premises applications with Azure AD Application Proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="27776-150">SaaS 應用程式的 Azure 條件式存取預覽</span><span class="sxs-lookup"><span data-stu-id="27776-150">Azure Conditional Access Preview for SaaS Apps</span></span>](active-directory-conditional-access-azuread-connected-apps.md)
* [<span data-ttu-id="27776-151">管理與 Azure AD 存取 tooapps</span><span class="sxs-lookup"><span data-stu-id="27776-151">Managing access tooapps with Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="27776-152">Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)</span><span class="sxs-lookup"><span data-stu-id="27776-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

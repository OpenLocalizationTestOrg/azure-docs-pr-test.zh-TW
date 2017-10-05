---
title: "登入存取面板網站時遇到問題 | Microsoft Docs"
description: "針對您嘗試登入使用存取面板時可能遇到的問題進行疑難排解的指引"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviwer: japere
ms.openlocfilehash: 28d91237adf745e591b02322de7881c8122827ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="problem-signing-in-to-the-access-panel-website"></a><span data-ttu-id="4a9de-103">登入存取面板網站時遇到問題</span><span class="sxs-lookup"><span data-stu-id="4a9de-103">Problem signing in to the access panel website</span></span>

<span data-ttu-id="4a9de-104">存取面板是網頁型入口網站，可讓在 Azure Active Directory (Azure AD) 中具有公司或學校帳戶的使用者，檢視和啟動 Azure AD 系統管理員已授權他們存取的雲端式應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a9de-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="4a9de-105">具有 Azure AD 版本的使用者也可以透過存取面板使用自助群組和應用程式管理功能。</span><span class="sxs-lookup"><span data-stu-id="4a9de-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="4a9de-106">存取面板與 Azure 入口網站分開，使用者不需要具備 Azure 訂用帳戶也能使用。</span><span class="sxs-lookup"><span data-stu-id="4a9de-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="4a9de-107">如果使用者在 Azure AD 中有公司或學校帳戶，他們就可以登入存取面板。</span><span class="sxs-lookup"><span data-stu-id="4a9de-107">Users can sign in to the Access Panel if they have a work or school account in Azure AD.</span></span>

-   <span data-ttu-id="4a9de-108">使用者可以直接由 Azure AD 驗證。</span><span class="sxs-lookup"><span data-stu-id="4a9de-108">Users can be authenticated by Azure AD directly.</span></span>

-   <span data-ttu-id="4a9de-109">使用者可以透過 Active Directory Federation Services (AD FS) 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="4a9de-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span></span>

-   <span data-ttu-id="4a9de-110">使用者可以由 Windows Server Active Directory 驗證。</span><span class="sxs-lookup"><span data-stu-id="4a9de-110">Users can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="4a9de-111">如果使用者具備 Azure 或 Office 365 的訂用帳戶，而且已經在使用 Azure 入口網站或 Office 365 應用程式，他們就可以直接使用存取面板，而不需要再次登入。</span><span class="sxs-lookup"><span data-stu-id="4a9de-111">If a user has a subscription for Azure or Office 365 and has been using the Azure portal or an Office 365 application, they'll be able to use the Access Panel seamlessly without needing to sign in again.</span></span> <span data-ttu-id="4a9de-112">對於未經過驗證的使用者，系統會提示他們輸入 Azure AD 中的帳戶使用者名稱和密碼來登入。</span><span class="sxs-lookup"><span data-stu-id="4a9de-112">Users who are not authenticated be prompted to sign in by using the username and password for their account in Azure AD.</span></span> <span data-ttu-id="4a9de-113">如果組織已設定同盟，則輸入使用者名稱已經足夠。</span><span class="sxs-lookup"><span data-stu-id="4a9de-113">If the organization has configured federation, typing the username is sufficient.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="4a9de-114">首先檢查的一般問題</span><span class="sxs-lookup"><span data-stu-id="4a9de-114">General issues to check first</span></span> 

-   <span data-ttu-id="4a9de-115">確定使用者登入**正確 URL**：<https://myapps.microsoft.com></span><span class="sxs-lookup"><span data-stu-id="4a9de-115">Make sure the user is signing in to the **correct URL**: <https://myapps.microsoft.com></span></span>

-   <span data-ttu-id="4a9de-116">確定使用者的瀏覽器已將此 URL 新增至**信任的網站**</span><span class="sxs-lookup"><span data-stu-id="4a9de-116">Make sure the user’s browser has added the URL to its **trusted sites**</span></span>

-   <span data-ttu-id="4a9de-117">確定使用者的帳戶**已啟用**登入。</span><span class="sxs-lookup"><span data-stu-id="4a9de-117">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="4a9de-118">確定使用者的帳戶**未鎖定**。</span><span class="sxs-lookup"><span data-stu-id="4a9de-118">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="4a9de-119">確定使用者的**密碼未過期或忘記**。</span><span class="sxs-lookup"><span data-stu-id="4a9de-119">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="4a9de-120">確定 **Multi-Factor Authentication** 未封鎖使用者存取。</span><span class="sxs-lookup"><span data-stu-id="4a9de-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="4a9de-121">確定**條件式存取原則**或**身分識別保護**原則未封鎖使用者存取。</span><span class="sxs-lookup"><span data-stu-id="4a9de-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="4a9de-122">確定使用者的**驗證連絡資訊**為最新版本，而可強制執行 Multi-Factor Authentication 或條件式存取原則。</span><span class="sxs-lookup"><span data-stu-id="4a9de-122">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="4a9de-123">也要確定嘗試清除瀏覽器的 Cookie，然後嘗試再次登入。</span><span class="sxs-lookup"><span data-stu-id="4a9de-123">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="4a9de-124">符合存取面板的瀏覽器需求</span><span class="sxs-lookup"><span data-stu-id="4a9de-124">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="4a9de-125">存取面板需要支援 JavaScript 且已啟用 CSS 的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="4a9de-125">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="4a9de-126">若要在存取面板中使用密碼單一登入 (SSO)，必須在使用者的瀏覽器中安裝存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="4a9de-126">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="4a9de-127">當使用者選取已設定密碼 SSO 的應用程式時，就會自動下載此存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="4a9de-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="4a9de-128">若是密碼 SSO，則使用者的瀏覽器可以是：</span><span class="sxs-lookup"><span data-stu-id="4a9de-128">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="4a9de-129">Internet Explorer 8、9、10、11 -- 在 Windows 7 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="4a9de-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="4a9de-130">Windows 10 Anniversary Edition 或更新版本上的 Edge</span><span class="sxs-lookup"><span data-stu-id="4a9de-130">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="4a9de-131">Chrome - 在 Windows 7 或更新版本，和在 MacOS X 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="4a9de-131">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="4a9de-132">Firefox 26.0 或更新版本 - 在 Windows XP SP2 或更新版本，和在 Mac OS X 10.6 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="4a9de-132">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>


## <a name="problems-with-the-users-account"></a><span data-ttu-id="4a9de-133">使用者帳戶的問題</span><span class="sxs-lookup"><span data-stu-id="4a9de-133">Problems with the user’s account</span></span>

<span data-ttu-id="4a9de-134">使用者帳戶發生問題時可能會封鎖對存取面板的存取。</span><span class="sxs-lookup"><span data-stu-id="4a9de-134">Access to the Access Panel can be blocked due to a problem with the user’s account.</span></span> <span data-ttu-id="4a9de-135">以下是針對使用者和其帳戶設定進行疑難排解的一些方法︰</span><span class="sxs-lookup"><span data-stu-id="4a9de-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="4a9de-136">檢查 Azure Active Directory 中是否存在使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="4a9de-136">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="4a9de-137">檢查使用者帳戶的狀態</span><span class="sxs-lookup"><span data-stu-id="4a9de-137">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="4a9de-138">重設使用者的密碼</span><span class="sxs-lookup"><span data-stu-id="4a9de-138">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="4a9de-139">啟用自助密碼重設</span><span class="sxs-lookup"><span data-stu-id="4a9de-139">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="4a9de-140">檢查使用者的多重要素驗證狀態</span><span class="sxs-lookup"><span data-stu-id="4a9de-140">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="4a9de-141">檢查使用者的驗證連絡資訊</span><span class="sxs-lookup"><span data-stu-id="4a9de-141">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="4a9de-142">檢查使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="4a9de-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="4a9de-143">檢查使用者獲指派的授權</span><span class="sxs-lookup"><span data-stu-id="4a9de-143">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="4a9de-144">指派授權至使用者</span><span class="sxs-lookup"><span data-stu-id="4a9de-144">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="4a9de-145">檢查 Azure Active Directory 中是否存在使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="4a9de-145">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="4a9de-146">若要檢查使用者的帳戶是否存在，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="4a9de-146">To check if a user’s account is present, follow the steps below:</span></span>

1.  <span data-ttu-id="4a9de-147">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="4a9de-147">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4a9de-148">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-148">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4a9de-149">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="4a9de-149">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4a9de-150">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-150">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4a9de-151">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-151">click **All users**.</span></span>

6.  <span data-ttu-id="4a9de-152">**搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。</span><span class="sxs-lookup"><span data-stu-id="4a9de-152">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4a9de-153">檢查使用者物件的屬性，確定符合您的預期，沒有遺失資料。</span><span class="sxs-lookup"><span data-stu-id="4a9de-153">Check the properties of the user object to be sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="4a9de-154">檢查使用者帳戶的狀態</span><span class="sxs-lookup"><span data-stu-id="4a9de-154">Check a user’s account status</span></span>

<span data-ttu-id="4a9de-155">若要檢查使用者帳戶的狀態，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="4a9de-155">To check a user’s account status, follow the steps below:</span></span>

1.  <span data-ttu-id="4a9de-156">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="4a9de-156">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4a9de-157">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-157">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4a9de-158">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="4a9de-158">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4a9de-159">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-159">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4a9de-160">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-160">click **All users**.</span></span>

6.  <span data-ttu-id="4a9de-161">**搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。</span><span class="sxs-lookup"><span data-stu-id="4a9de-161">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4a9de-162">按一下 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-162">click **Profile**.</span></span>

8.  <span data-ttu-id="4a9de-163">在 [設定] 下，確定 [封鎖登入] 設為 [否]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-163">Under **Settings** ensure that **Block sign in** is set to **No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="4a9de-164">重設使用者的密碼</span><span class="sxs-lookup"><span data-stu-id="4a9de-164">Reset a user’s password</span></span>

<span data-ttu-id="4a9de-165">若要重設使用者的密碼，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="4a9de-165">To reset a user’s password, follow the steps below:</span></span>

1.  <span data-ttu-id="4a9de-166">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="4a9de-166">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4a9de-167">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-167">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4a9de-168">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="4a9de-168">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4a9de-169">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-169">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4a9de-170">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-170">click **All users**.</span></span>

6.  <span data-ttu-id="4a9de-171">**搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。</span><span class="sxs-lookup"><span data-stu-id="4a9de-171">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4a9de-172">按一下使用者刀鋒視窗頂端的 [重設密碼]按鈕。</span><span class="sxs-lookup"><span data-stu-id="4a9de-172">click the **Reset password** button at the top of the user blade.</span></span>

8.  <span data-ttu-id="4a9de-173">在出現的 [重設密碼] 刀鋒視窗上，按一下 [重設密碼] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4a9de-173">click the **Reset password** button on the **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="4a9de-174">為使用者複製**暫時密碼**或**輸入新密碼**。</span><span class="sxs-lookup"><span data-stu-id="4a9de-174">Copy the **temporary password** or **enter a new password** for the user.</span></span>

10. <span data-ttu-id="4a9de-175">將這個新的密碼告知使用者，他們下次登入 Azure Active Directory 時必須變更此密碼。</span><span class="sxs-lookup"><span data-stu-id="4a9de-175">Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="4a9de-176">啟用自助式密碼重設</span><span class="sxs-lookup"><span data-stu-id="4a9de-176">Enable self-service password reset</span></span>

<span data-ttu-id="4a9de-177">若要啟用自助式密碼重設，請遵循下列部署步驟︰</span><span class="sxs-lookup"><span data-stu-id="4a9de-177">To enable self-service password reset, follow the deployment steps below:</span></span>

-   [<span data-ttu-id="4a9de-178">讓使用者重設其 Azure Active Directory 密碼</span><span class="sxs-lookup"><span data-stu-id="4a9de-178">Enable users to reset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="4a9de-179">讓使用者重設或變更其 Active Directory 內部部署密碼</span><span class="sxs-lookup"><span data-stu-id="4a9de-179">Enable users to reset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="4a9de-180">檢查使用者的多重要素驗證狀態</span><span class="sxs-lookup"><span data-stu-id="4a9de-180">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="4a9de-181">若要檢查使用者的多重要素驗證狀態，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="4a9de-181">To check a user’s multi-factor authentication status, follow the steps below:</span></span>

1.  <span data-ttu-id="4a9de-182">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="4a9de-182">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4a9de-183">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-183">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4a9de-184">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="4a9de-184">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4a9de-185">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-185">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4a9de-186">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-186">click **All users**.</span></span>

6.  <span data-ttu-id="4a9de-187">按一下刀鋒視窗頂端的 [Multi-Factor Authentication] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4a9de-187">click the **Multi-Factor Authentication** button at the top of the blade.</span></span>

7.  <span data-ttu-id="4a9de-188">當 **Multi-Factor Authentication 管理網站**載入後，請確定您位於 [使用者] 索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="4a9de-188">Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.</span></span>

8.  <span data-ttu-id="4a9de-189">在使用者清單中搜尋、篩選或排序來尋找使用者。</span><span class="sxs-lookup"><span data-stu-id="4a9de-189">Find the user in the list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="4a9de-190">從使用者清單中選取使用者，然後視需要 [啟用]、[停用] 或 [強制執行] 多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="4a9de-190">Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

   >[!NOTE]
   ><span data-ttu-id="4a9de-191">如果使用者處於 [已強制] 狀態，您可以暫時將他們設為 [已停用]，讓他們回到各自的帳戶。</span><span class="sxs-lookup"><span data-stu-id="4a9de-191">If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account.</span></span> <span data-ttu-id="4a9de-192">退回之後，您可以再次將其狀態變更為 [已啟用]，以要求他們在下次登入時重新註冊連絡資訊。</span><span class="sxs-lookup"><span data-stu-id="4a9de-192">Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in.</span></span> <span data-ttu-id="4a9de-193">或者，您可以依照[檢查使用者的驗證連絡資訊](#check-a-users-authentication-contact-info)中的步驟，為他們確認或設定此資料。</span><span class="sxs-lookup"><span data-stu-id="4a9de-193">Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.</span></span>
   >
   >

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="4a9de-194">檢查使用者的驗證連絡資訊</span><span class="sxs-lookup"><span data-stu-id="4a9de-194">Check a user’s authentication contact info</span></span>

<span data-ttu-id="4a9de-195">若要檢查用於多重要素驗證、條件式存取、身分識別保護和密碼重設的使用者驗證連絡資訊，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="4a9de-195">To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:</span></span>

1.  <span data-ttu-id="4a9de-196">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="4a9de-196">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4a9de-197">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-197">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4a9de-198">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="4a9de-198">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4a9de-199">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-199">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4a9de-200">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-200">click **All users**.</span></span>

6.  <span data-ttu-id="4a9de-201">**搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。</span><span class="sxs-lookup"><span data-stu-id="4a9de-201">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4a9de-202">按一下 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-202">click **Profile**.</span></span>

8.  <span data-ttu-id="4a9de-203">向下捲動至 [驗證連絡資訊]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-203">Scroll down to **Authentication contact info**.</span></span>

9.  <span data-ttu-id="4a9de-204">**檢閱**使用者註冊的資料，並視需要予以更新。</span><span class="sxs-lookup"><span data-stu-id="4a9de-204">**Review** the data registered for the user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="4a9de-205">檢查使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="4a9de-205">Check a user’s group memberships</span></span>

<span data-ttu-id="4a9de-206">若要檢查使用者的群組成員資格，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="4a9de-206">To check a user’s group memberships, follow the steps below:</span></span>

1.  <span data-ttu-id="4a9de-207">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="4a9de-207">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4a9de-208">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-208">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4a9de-209">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="4a9de-209">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4a9de-210">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-210">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4a9de-211">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-211">click **All users**.</span></span>

6.  <span data-ttu-id="4a9de-212">**搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。</span><span class="sxs-lookup"><span data-stu-id="4a9de-212">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4a9de-213">按一下 [群組]，查看使用者是哪些群組的成員。</span><span class="sxs-lookup"><span data-stu-id="4a9de-213">click **Groups** to see which groups the user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="4a9de-214">檢查使用者獲指派的授權</span><span class="sxs-lookup"><span data-stu-id="4a9de-214">Check a user’s assigned licenses</span></span>

<span data-ttu-id="4a9de-215">若要檢查使用者獲指派的授權，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="4a9de-215">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="4a9de-216">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="4a9de-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4a9de-217">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4a9de-218">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="4a9de-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4a9de-219">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-219">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4a9de-220">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-220">click **All users**.</span></span>

6.  <span data-ttu-id="4a9de-221">**搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。</span><span class="sxs-lookup"><span data-stu-id="4a9de-221">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4a9de-222">按一下 [授權]，查看使用者目前已指派的授權。</span><span class="sxs-lookup"><span data-stu-id="4a9de-222">click **Licenses** to see which licenses the user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="4a9de-223">指派授權至使用者</span><span class="sxs-lookup"><span data-stu-id="4a9de-223">Assign a user a license</span></span> 

<span data-ttu-id="4a9de-224">若要指派授權至使用者，請依照下列步驟執行︰</span><span class="sxs-lookup"><span data-stu-id="4a9de-224">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="4a9de-225">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="4a9de-225">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="4a9de-226">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-226">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4a9de-227">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="4a9de-227">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4a9de-228">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-228">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="4a9de-229">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-229">click **All users**.</span></span>

6.  <span data-ttu-id="4a9de-230">**搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。</span><span class="sxs-lookup"><span data-stu-id="4a9de-230">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="4a9de-231">按一下 [授權]，查看使用者目前已指派的授權。</span><span class="sxs-lookup"><span data-stu-id="4a9de-231">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="4a9de-232">按一下 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4a9de-232">click the **Assign** button.</span></span>

9.  <span data-ttu-id="4a9de-233">從可用產品清單中選取**一或多個產品**。</span><span class="sxs-lookup"><span data-stu-id="4a9de-233">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="4a9de-234">(**選擇性**) 按一下 [指派選項] 項目，更細微地指派產品。</span><span class="sxs-lookup"><span data-stu-id="4a9de-234">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="4a9de-235">完成時按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="4a9de-235">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="4a9de-236">按一下 [指派] 按鈕，將這些授權指派給這位使用者。</span><span class="sxs-lookup"><span data-stu-id="4a9de-236">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="4a9de-237">如果這些疑難排解步驟無法解決問題</span><span class="sxs-lookup"><span data-stu-id="4a9de-237">If these troubleshooting steps do not resolve the issue</span></span>

<span data-ttu-id="4a9de-238">使用下列資訊 (若有的話) 開啟支援票證︰</span><span class="sxs-lookup"><span data-stu-id="4a9de-238">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="4a9de-239">相互關聯錯誤 ID</span><span class="sxs-lookup"><span data-stu-id="4a9de-239">Correlation error ID</span></span>

-   <span data-ttu-id="4a9de-240">UPN (使用者電子郵件地址)</span><span class="sxs-lookup"><span data-stu-id="4a9de-240">UPN (user email address)</span></span>

-   <span data-ttu-id="4a9de-241">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="4a9de-241">Tenant ID</span></span>

-   <span data-ttu-id="4a9de-242">瀏覽器類型</span><span class="sxs-lookup"><span data-stu-id="4a9de-242">Browser type</span></span>

-   <span data-ttu-id="4a9de-243">錯誤發生期間的時區和時間/時間範圍</span><span class="sxs-lookup"><span data-stu-id="4a9de-243">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="4a9de-244">Fiddler 追蹤</span><span class="sxs-lookup"><span data-stu-id="4a9de-244">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a9de-245">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4a9de-245">Next steps</span></span>
[<span data-ttu-id="4a9de-246">使用應用程式 Proxy 提供單一登入應用程式</span><span class="sxs-lookup"><span data-stu-id="4a9de-246">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

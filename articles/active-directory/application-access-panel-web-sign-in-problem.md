---
title: "登入存取面板 」 toohello 網站 aaaProblem |Microsoft 文件"
description: "您可能會發生在嘗試 toosign toouse 中的指引 tootroubleshoot 問題 hello 存取面板"
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
ms.openlocfilehash: 1037f7c5fbaa9425760ad5739b383c716d5fc3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problem-signing-in-toohello-access-panel-website"></a><span data-ttu-id="091a9-103">登入存取面板 toohello 」 網站的問題</span><span class="sxs-lookup"><span data-stu-id="091a9-103">Problem signing in toohello access panel website</span></span>

<span data-ttu-id="091a9-104">hello 存取面板是網頁型入口網站讓使用者具有工作或學校帳戶在 Azure Active Directory (Azure AD) tooview 並啟動雲端型應用程式中的 hello Azure AD 系統管理員已被授與存取權。</span><span class="sxs-lookup"><span data-stu-id="091a9-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="091a9-105">自助式群組並透過 hello 存取面板應用程式管理功能，也可以使用具有 Azure AD 版本的使用者。</span><span class="sxs-lookup"><span data-stu-id="091a9-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="091a9-106">hello 存取面板是分開 hello Azure 入口網站，而且不需要使用者 toohave Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="091a9-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="091a9-107">使用者可以登入 toohello 存取面板中，如果他們擁有在 Azure AD 中的工作或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="091a9-107">Users can sign in toohello Access Panel if they have a work or school account in Azure AD.</span></span>

-   <span data-ttu-id="091a9-108">使用者可以直接由 Azure AD 驗證。</span><span class="sxs-lookup"><span data-stu-id="091a9-108">Users can be authenticated by Azure AD directly.</span></span>

-   <span data-ttu-id="091a9-109">使用者可以透過 Active Directory Federation Services (AD FS) 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="091a9-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span></span>

-   <span data-ttu-id="091a9-110">使用者可以由 Windows Server Active Directory 驗證。</span><span class="sxs-lookup"><span data-stu-id="091a9-110">Users can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="091a9-111">如果使用者擁有 Azure 或 Office 365 訂閱，且 hello Azure 入口網站或 Office 365 應用程式已使用，他們必須能夠 toouse 順暢地 hello 存取面板，而不需要在 toosign 一次。</span><span class="sxs-lookup"><span data-stu-id="091a9-111">If a user has a subscription for Azure or Office 365 and has been using hello Azure portal or an Office 365 application, they'll be able toouse hello Access Panel seamlessly without needing toosign in again.</span></span> <span data-ttu-id="091a9-112">未驗證的使用者會在提示的 toosign hello 使用者名稱和密碼，使用 Azure AD 中為其帳戶。</span><span class="sxs-lookup"><span data-stu-id="091a9-112">Users who are not authenticated be prompted toosign in by using hello username and password for their account in Azure AD.</span></span> <span data-ttu-id="091a9-113">如果 hello 組織已設定同盟，輸入 hello 使用者名稱便已足夠。</span><span class="sxs-lookup"><span data-stu-id="091a9-113">If hello organization has configured federation, typing hello username is sufficient.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="091a9-114">一般會先發出 toocheck</span><span class="sxs-lookup"><span data-stu-id="091a9-114">General issues toocheck first</span></span> 

-   <span data-ttu-id="091a9-115">請確定 hello 使用者登入 toohello**更正 URL**: <https://myapps.microsoft.com></span><span class="sxs-lookup"><span data-stu-id="091a9-115">Make sure hello user is signing in toohello **correct URL**: <https://myapps.microsoft.com></span></span>

-   <span data-ttu-id="091a9-116">請確定 hello 使用者的瀏覽器已新增 hello URL tooits**信任的網站**</span><span class="sxs-lookup"><span data-stu-id="091a9-116">Make sure hello user’s browser has added hello URL tooits **trusted sites**</span></span>

-   <span data-ttu-id="091a9-117">請確定 hello 使用者帳戶是**啟用**的登入。</span><span class="sxs-lookup"><span data-stu-id="091a9-117">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="091a9-118">請確定 hello 使用者帳戶是**並未鎖定。**</span><span class="sxs-lookup"><span data-stu-id="091a9-118">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="091a9-119">請確定 hello 使用者的**密碼未過期或遺失。**</span><span class="sxs-lookup"><span data-stu-id="091a9-119">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="091a9-120">確定 **Multi-Factor Authentication** 未封鎖使用者存取。</span><span class="sxs-lookup"><span data-stu-id="091a9-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="091a9-121">確定**條件式存取原則**或**身分識別保護**原則未封鎖使用者存取。</span><span class="sxs-lookup"><span data-stu-id="091a9-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="091a9-122">請確定使用者的**驗證連絡人資訊**已啟動 toodate tooallow Multi-factor Authentication 或條件式存取原則 toobe 強制執行。</span><span class="sxs-lookup"><span data-stu-id="091a9-122">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="091a9-123">請確定 tooalso 請嘗試清除瀏覽器的 cookie，然後再試一次 toosign 中的。</span><span class="sxs-lookup"><span data-stu-id="091a9-123">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="091a9-124">會議 hello 存取面板 的瀏覽器需求</span><span class="sxs-lookup"><span data-stu-id="091a9-124">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="091a9-125">存取面板 hello 需要支援 JavaScript 的瀏覽器，並啟用 CSS。</span><span class="sxs-lookup"><span data-stu-id="091a9-125">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="091a9-126">toouse 密碼型單一登入 (SSO) 在 hello 存取面板，hello 存取面板延伸模組必須安裝在 hello 使用者的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="091a9-126">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="091a9-127">當使用者選取已設定密碼 SSO 的應用程式時，就會自動下載此存取面板延伸模組。</span><span class="sxs-lookup"><span data-stu-id="091a9-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="091a9-128">針對密碼型 SSO，hello 終端使用者的瀏覽器可以是：</span><span class="sxs-lookup"><span data-stu-id="091a9-128">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="091a9-129">Internet Explorer 8、9、10、11 -- 在 Windows 7 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="091a9-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="091a9-130">Windows 10 Anniversary Edition 或更新版本上的 Edge</span><span class="sxs-lookup"><span data-stu-id="091a9-130">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="091a9-131">Chrome - 在 Windows 7 或更新版本，和在 MacOS X 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="091a9-131">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="091a9-132">Firefox 26.0 或更新版本 - 在 Windows XP SP2 或更新版本，和在 Mac OS X 10.6 或更新版本上</span><span class="sxs-lookup"><span data-stu-id="091a9-132">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>


## <a name="problems-with-hello-users-account"></a><span data-ttu-id="091a9-133">Hello 使用者帳戶的問題</span><span class="sxs-lookup"><span data-stu-id="091a9-133">Problems with hello user’s account</span></span>

<span data-ttu-id="091a9-134">存取 toohello 存取面板可以被封鎖，因為 tooa 問題與 hello 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="091a9-134">Access toohello Access Panel can be blocked due tooa problem with hello user’s account.</span></span> <span data-ttu-id="091a9-135">以下是針對使用者和其帳戶設定進行疑難排解的一些方法︰</span><span class="sxs-lookup"><span data-stu-id="091a9-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="091a9-136">檢查 Azure Active Directory 中是否存在使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="091a9-136">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="091a9-137">檢查使用者帳戶的狀態</span><span class="sxs-lookup"><span data-stu-id="091a9-137">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="091a9-138">重設使用者的密碼</span><span class="sxs-lookup"><span data-stu-id="091a9-138">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="091a9-139">啟用自助密碼重設</span><span class="sxs-lookup"><span data-stu-id="091a9-139">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="091a9-140">檢查使用者的多重要素驗證狀態</span><span class="sxs-lookup"><span data-stu-id="091a9-140">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="091a9-141">檢查使用者的驗證連絡資訊</span><span class="sxs-lookup"><span data-stu-id="091a9-141">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="091a9-142">檢查使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="091a9-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="091a9-143">檢查使用者獲指派的授權</span><span class="sxs-lookup"><span data-stu-id="091a9-143">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="091a9-144">指派授權至使用者</span><span class="sxs-lookup"><span data-stu-id="091a9-144">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="091a9-145">檢查 Azure Active Directory 中是否存在使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="091a9-145">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="091a9-146">toocheck 使用者帳戶是否存在，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="091a9-146">toocheck if a user’s account is present, follow hello steps below:</span></span>

1.  <span data-ttu-id="091a9-147">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="091a9-147">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="091a9-148">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="091a9-148">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="091a9-149">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="091a9-149">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="091a9-150">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="091a9-150">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="091a9-151">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="091a9-151">click **All users**.</span></span>

6.  <span data-ttu-id="091a9-152">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="091a9-152">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="091a9-153">檢查確定它們看起來如您預期且不會遺失任何資料的 hello 使用者物件 toobe hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="091a9-153">Check hello properties of hello user object toobe sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="091a9-154">檢查使用者帳戶的狀態</span><span class="sxs-lookup"><span data-stu-id="091a9-154">Check a user’s account status</span></span>

<span data-ttu-id="091a9-155">toocheck 使用者的帳戶狀態，請遵循下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="091a9-155">toocheck a user’s account status, follow hello steps below:</span></span>

1.  <span data-ttu-id="091a9-156">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="091a9-156">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="091a9-157">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="091a9-157">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="091a9-158">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="091a9-158">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="091a9-159">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="091a9-159">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="091a9-160">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="091a9-160">click **All users**.</span></span>

6.  <span data-ttu-id="091a9-161">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="091a9-161">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="091a9-162">按一下 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="091a9-162">click **Profile**.</span></span>

8.  <span data-ttu-id="091a9-163">在下**設定**確定**區塊登入**設定得**否**。</span><span class="sxs-lookup"><span data-stu-id="091a9-163">Under **Settings** ensure that **Block sign in** is set too**No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="091a9-164">重設使用者的密碼</span><span class="sxs-lookup"><span data-stu-id="091a9-164">Reset a user’s password</span></span>

<span data-ttu-id="091a9-165">tooreset 使用者的密碼，後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="091a9-165">tooreset a user’s password, follow hello steps below:</span></span>

1.  <span data-ttu-id="091a9-166">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="091a9-166">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="091a9-167">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="091a9-167">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="091a9-168">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="091a9-168">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="091a9-169">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="091a9-169">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="091a9-170">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="091a9-170">click **All users**.</span></span>

6.  <span data-ttu-id="091a9-171">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="091a9-171">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="091a9-172">按一下 hello**重設密碼**在 hello hello 使用者 刀鋒視窗頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="091a9-172">click hello **Reset password** button at hello top of hello user blade.</span></span>

8.  <span data-ttu-id="091a9-173">按一下 hello**重設密碼**按鈕 hello**重設密碼**刀鋒視窗中出現。</span><span class="sxs-lookup"><span data-stu-id="091a9-173">click hello **Reset password** button on hello **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="091a9-174">複製 hello**暫時密碼**或**輸入新密碼**hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="091a9-174">Copy hello **temporary password** or **enter a new password** for hello user.</span></span>

10. <span data-ttu-id="091a9-175">這個新的密碼 toohello 使用者進行通訊，它們是必要的 toochange 他們下一步 在此密碼登入 tooAzure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="091a9-175">Communicate this new password toohello user, they be required toochange this password during their next sign in tooAzure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="091a9-176">啟用自助式密碼重設</span><span class="sxs-lookup"><span data-stu-id="091a9-176">Enable self-service password reset</span></span>

<span data-ttu-id="091a9-177">tooenable 自助式密碼重設，請遵循下列的 hello 部署步驟：</span><span class="sxs-lookup"><span data-stu-id="091a9-177">tooenable self-service password reset, follow hello deployment steps below:</span></span>

-   [<span data-ttu-id="091a9-178">啟用使用者 tooreset 其 Azure Active Directory 密碼</span><span class="sxs-lookup"><span data-stu-id="091a9-178">Enable users tooreset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="091a9-179">啟用使用者 tooreset 或變更其 Active Directory 內部部署密碼</span><span class="sxs-lookup"><span data-stu-id="091a9-179">Enable users tooreset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="091a9-180">檢查使用者的多重要素驗證狀態</span><span class="sxs-lookup"><span data-stu-id="091a9-180">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="091a9-181">toocheck 使用者的多重要素驗證狀態，後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="091a9-181">toocheck a user’s multi-factor authentication status, follow hello steps below:</span></span>

1.  <span data-ttu-id="091a9-182">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="091a9-182">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="091a9-183">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="091a9-183">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="091a9-184">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="091a9-184">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="091a9-185">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="091a9-185">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="091a9-186">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="091a9-186">click **All users**.</span></span>

6.  <span data-ttu-id="091a9-187">按一下 hello **Multi-factor Authentication**在 hello hello 刀鋒視窗頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="091a9-187">click hello **Multi-Factor Authentication** button at hello top of hello blade.</span></span>

7.  <span data-ttu-id="091a9-188">一次 hello**多因素驗證管理網站**載入，請確定您是在 hello**使用者** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="091a9-188">Once hello **Multi-Factor Authentication Administration Portal** loads, ensure you are on hello **Users** tab.</span></span>

8.  <span data-ttu-id="091a9-189">Hello 的使用者清單中尋找 hello 使用者搜尋、 篩選或排序。</span><span class="sxs-lookup"><span data-stu-id="091a9-189">Find hello user in hello list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="091a9-190">選取 hello 使用者的使用者清單，hello 和**啟用**，**停用**，或**強制**所需的多因素驗證。</span><span class="sxs-lookup"><span data-stu-id="091a9-190">Select hello user from hello list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

   >[!NOTE]
   ><span data-ttu-id="091a9-191">如果使用者存在於**強制**狀態時，您可能設定太**已停用**暫時 toolet 它們放回其帳戶。</span><span class="sxs-lookup"><span data-stu-id="091a9-191">If a user is in an **Enforced** state, you may set them too**Disabled** temporarily toolet them back into their account.</span></span> <span data-ttu-id="091a9-192">當它們位於上一步時，您可以變更其狀態太**啟用**再次 toorequire 它們 toore 註冊他們的連絡資訊在其下一步 期間登入。</span><span class="sxs-lookup"><span data-stu-id="091a9-192">Once they are back in, you can then change their state too**Enabled** again toorequire them toore-register their contact information during their next sign in.</span></span> <span data-ttu-id="091a9-193">或者，您可以依照 hello 中的 hello 步驟[檢查使用者的驗證連絡人資訊](#check-a-users-authentication-contact-info)tooverify 或設定此資料。</span><span class="sxs-lookup"><span data-stu-id="091a9-193">Alternatively, you can follow hello steps in hello [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) tooverify or set this data for them.</span></span>
   >
   >

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="091a9-194">檢查使用者的驗證連絡資訊</span><span class="sxs-lookup"><span data-stu-id="091a9-194">Check a user’s authentication contact info</span></span>

<span data-ttu-id="091a9-195">toocheck 位使用者的驗證連絡資訊用於多重要素驗證、 條件式存取、 識別身分保護和重設密碼，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="091a9-195">toocheck a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow hello steps below:</span></span>

1.  <span data-ttu-id="091a9-196">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="091a9-196">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="091a9-197">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="091a9-197">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="091a9-198">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="091a9-198">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="091a9-199">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="091a9-199">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="091a9-200">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="091a9-200">click **All users**.</span></span>

6.  <span data-ttu-id="091a9-201">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="091a9-201">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="091a9-202">按一下 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="091a9-202">click **Profile**.</span></span>

8.  <span data-ttu-id="091a9-203">向下捲動太**驗證連絡人資訊**。</span><span class="sxs-lookup"><span data-stu-id="091a9-203">Scroll down too**Authentication contact info**.</span></span>

9.  <span data-ttu-id="091a9-204">**檢閱**視 hello 資料註冊 hello 使用者和更新。</span><span class="sxs-lookup"><span data-stu-id="091a9-204">**Review** hello data registered for hello user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="091a9-205">檢查使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="091a9-205">Check a user’s group memberships</span></span>

<span data-ttu-id="091a9-206">toocheck 使用者的群組成員資格，請遵循下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="091a9-206">toocheck a user’s group memberships, follow hello steps below:</span></span>

1.  <span data-ttu-id="091a9-207">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="091a9-207">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="091a9-208">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="091a9-208">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="091a9-209">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="091a9-209">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="091a9-210">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="091a9-210">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="091a9-211">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="091a9-211">click **All users**.</span></span>

6.  <span data-ttu-id="091a9-212">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="091a9-212">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="091a9-213">按一下**群組**toosee 以分組 hello 使用者隸屬。</span><span class="sxs-lookup"><span data-stu-id="091a9-213">click **Groups** toosee which groups hello user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="091a9-214">檢查使用者獲指派的授權</span><span class="sxs-lookup"><span data-stu-id="091a9-214">Check a user’s assigned licenses</span></span>

<span data-ttu-id="091a9-215">toocheck 使用者的指派授權，後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="091a9-215">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="091a9-216">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="091a9-216">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="091a9-217">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="091a9-217">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="091a9-218">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="091a9-218">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="091a9-219">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="091a9-219">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="091a9-220">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="091a9-220">click **All users**.</span></span>

6.  <span data-ttu-id="091a9-221">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="091a9-221">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="091a9-222">按一下**授權**toosee 授權 hello 使用者目前已指派。</span><span class="sxs-lookup"><span data-stu-id="091a9-222">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="091a9-223">指派授權至使用者</span><span class="sxs-lookup"><span data-stu-id="091a9-223">Assign a user a license</span></span> 

<span data-ttu-id="091a9-224">tooassign 授權 tooa 使用者，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="091a9-224">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="091a9-225">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="091a9-225">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="091a9-226">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="091a9-226">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="091a9-227">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="091a9-227">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="091a9-228">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="091a9-228">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="091a9-229">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="091a9-229">click **All users**.</span></span>

6.  <span data-ttu-id="091a9-230">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="091a9-230">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="091a9-231">按一下**授權**toosee 授權 hello 使用者目前已指派。</span><span class="sxs-lookup"><span data-stu-id="091a9-231">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="091a9-232">按一下 hello**指派** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="091a9-232">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="091a9-233">選取**一或多個產品**hello 清單中的可用產品。</span><span class="sxs-lookup"><span data-stu-id="091a9-233">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="091a9-234">**選擇性**按一下 hello**指派選項**項目 toogranularly 指派產品。</span><span class="sxs-lookup"><span data-stu-id="091a9-234">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="091a9-235">完成時按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="091a9-235">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="091a9-236">按一下 hello**指派**按鈕 tooassign 這些授權 toothis 使用者。</span><span class="sxs-lookup"><span data-stu-id="091a9-236">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="091a9-237">如果這些疑難排解步驟無法解決 hello 問題</span><span class="sxs-lookup"><span data-stu-id="091a9-237">If these troubleshooting steps do not resolve hello issue</span></span>

<span data-ttu-id="091a9-238">開啟支援票證以 hello 如果有的話，下列資訊：</span><span class="sxs-lookup"><span data-stu-id="091a9-238">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="091a9-239">相互關聯錯誤 ID</span><span class="sxs-lookup"><span data-stu-id="091a9-239">Correlation error ID</span></span>

-   <span data-ttu-id="091a9-240">UPN (使用者電子郵件地址)</span><span class="sxs-lookup"><span data-stu-id="091a9-240">UPN (user email address)</span></span>

-   <span data-ttu-id="091a9-241">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="091a9-241">Tenant ID</span></span>

-   <span data-ttu-id="091a9-242">瀏覽器類型</span><span class="sxs-lookup"><span data-stu-id="091a9-242">Browser type</span></span>

-   <span data-ttu-id="091a9-243">錯誤發生期間的時區和時間/時間範圍</span><span class="sxs-lookup"><span data-stu-id="091a9-243">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="091a9-244">Fiddler 追蹤</span><span class="sxs-lookup"><span data-stu-id="091a9-244">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="091a9-245">後續步驟</span><span class="sxs-lookup"><span data-stu-id="091a9-245">Next steps</span></span>
[<span data-ttu-id="091a9-246">提供單一登入 tooyour 應用程式與應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="091a9-246">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

---
title: "我的應用程式清單中的 aaaUnexpected 應用程式 |Microsoft 文件"
description: "如何 toosee 租用戶中的所有應用程式，並了解應用程式如何出現在所有應用程式清單中，在企業應用程式"
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
ms.openlocfilehash: 2f974046b655bc36a05f002c56511a8a988cd01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-application-in-my-applications-list"></a><span data-ttu-id="6077c-103">我的應用程式清單中有未預期的應用程式</span><span class="sxs-lookup"><span data-stu-id="6077c-103">Unexpected application in my applications list</span></span>

<span data-ttu-id="6077c-104">本文將協助您 toounderstand 應用程式出現在您**所有應用程式**清單下**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6077c-104">This article help you toounderstand how applications appear in your **All Applications** list under **Enterprise Applications**.</span></span> 

## <a name="how-toosee-all-applications-in-your-tenant"></a><span data-ttu-id="6077c-105">如何 toosee 租用戶中的所有應用程式</span><span class="sxs-lookup"><span data-stu-id="6077c-105">How toosee all applications in your tenant</span></span>

<span data-ttu-id="6077c-106">toosee 所有 hello 租用戶中的應用程式，您需要 toouse hello**篩選**控制 tooshow**所有應用程式**下 hello**所有應用程式**清單。</span><span class="sxs-lookup"><span data-stu-id="6077c-106">toosee all hello applications in your tenant, you need toouse hello **Filter** control tooshow **All Applications** under hello **All Applications** list.</span></span> <span data-ttu-id="6077c-107">toodo，後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="6077c-107">toodo this, follow hello steps below:</span></span>

1.  <span data-ttu-id="6077c-108">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="6077c-108">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="6077c-109">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="6077c-109">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="6077c-110">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="6077c-110">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="6077c-111">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="6077c-111">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="6077c-112">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="6077c-112">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="6077c-113">按一下 hello 使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**。</span><span class="sxs-lookup"><span data-stu-id="6077c-113">click hello use hello **Filter** control at hello top of hello **All Applications List**.</span></span>

7.  <span data-ttu-id="6077c-114">在 hello**篩選**刀鋒視窗中，設定 hello**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="6077c-114">On hello **Filter** blade, set hello **Show** option too**All Applications.**</span></span>

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a><span data-ttu-id="6077c-115">特定應用程式為何出現在我的所有應用程式清單中？</span><span class="sxs-lookup"><span data-stu-id="6077c-115">Why does a specific application appear in my all applications list?</span></span>

<span data-ttu-id="6077c-116">當篩選太**所有應用程式**，hello**所有應用程式****清單**顯示租用戶中的每個服務主體物件。</span><span class="sxs-lookup"><span data-stu-id="6077c-116">When filtered too**All Applications**, hello **All Applications** **List** shows every Service Principal object in your tenant.</span></span> <span data-ttu-id="6077c-117">服務主體物件可能以各種方式出現在此清單中︰</span><span class="sxs-lookup"><span data-stu-id="6077c-117">Service Principal objects can appear in this list in a various ways:</span></span>

1.  <span data-ttu-id="6077c-118">當您從 hello 應用程式庫，新增任何應用程式時，包括：</span><span class="sxs-lookup"><span data-stu-id="6077c-118">When you add any application from hello application gallery, including:</span></span>

   1. <span data-ttu-id="6077c-119">**Azure AD 資源庫應用程式** – 與 Azure AD 預先整合以啟用單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6077c-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

   2. <span data-ttu-id="6077c-120">**應用程式 Proxy 應用程式**– 您想 tooprovide 安全單一登入 tooexternally 在內部部署環境中執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6077c-120">**Application Proxy Applications** – An application running in your on-premises environment that you want tooprovide secure single-sign on tooexternally.</span></span>

   3. <span data-ttu-id="6077c-121">**自訂開發的應用程式**– 的應用程式，您的組織希望 toodevelop 上 hello Azure AD 應用程式開發平台，但所可能尚不存在。</span><span class="sxs-lookup"><span data-stu-id="6077c-121">**Custom-developed Applications** – An application that your organization wishes toodevelop on hello Azure AD Application Development Platform, but that may not exist yet.</span></span>

   4. <span data-ttu-id="6077c-122">**不在資源庫內的應用程式** – 引進您自己的應用程式！</span><span class="sxs-lookup"><span data-stu-id="6077c-122">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="6077c-123">您想，任何網頁連結或呈現使用者名稱和密碼欄位中，任何應用程式支援 SAML 或 OpenID Connect 通訊協定，或支援您想進行單一登入 Azure AD 與 toointegrate SCIM。</span><span class="sxs-lookup"><span data-stu-id="6077c-123">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish toointegrate for single sign-on with Azure AD.</span></span>

2.  <span data-ttu-id="6077c-124">註冊或登入與 Azure Active Directory 整合的第三方<sup></sup>應用程式時。</span><span class="sxs-lookup"><span data-stu-id="6077c-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span></span> <span data-ttu-id="6077c-125">例如，[Smartsheet](https://app.smartsheet.com/b/home) 或 [DocuSign](https://www.docusign.net/member/MemberLogin.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6077c-125">One example of this is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span></span>

3.  <span data-ttu-id="6077c-126">當註冊，或新增授權 tooa 使用者或群組 tooa 第一個合作對象應用程式，就像[Microsoft Office 365](http://products.office.com/)。</span><span class="sxs-lookup"><span data-stu-id="6077c-126">When signing up for, or adding a license tooa user or a group tooa first party application, like [Microsoft Office 365](http://products.office.com/).</span></span>

4.  <span data-ttu-id="6077c-127">當您新增新的應用程式註冊藉由建立自訂開發的應用程式使用 hello [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration)。</span><span class="sxs-lookup"><span data-stu-id="6077c-127">When you add a new application registration by creating a custom-developed application using hello [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span></span>

5.  <span data-ttu-id="6077c-128">當您新增新的應用程式註冊藉由建立自訂開發的應用程式使用 hello [V2.0 應用程式註冊入口網站](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal)。</span><span class="sxs-lookup"><span data-stu-id="6077c-128">When you add a new application registration by creating a custom-developed application using hello [V2.0 Application Registration Portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span></span>

6.  <span data-ttu-id="6077c-129">當您新增您使用 Visual Studio 的 [ASP.net 驗證方法](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions)或[已連線服務](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx)所開發的應用程式時。</span><span class="sxs-lookup"><span data-stu-id="6077c-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span></span>

7.  <span data-ttu-id="6077c-130">當您建立服務主體物件，使用 hello [Azure AD PowerShell 模組](/powershell/azure/install-adv2?view=azureadps-2.0)。</span><span class="sxs-lookup"><span data-stu-id="6077c-130">When you create a service principal object using hello [Azure AD PowerShell Module](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

8.  <span data-ttu-id="6077c-131">當您[tooan 應用程式的同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)為您的租用戶系統管理員 toouse 資料。</span><span class="sxs-lookup"><span data-stu-id="6077c-131">When you [consent tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator toouse data in your tenant.</span></span>

9.  <span data-ttu-id="6077c-132">當[tooan 應用程式取得使用者同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)toouse 租用戶中的資料。</span><span class="sxs-lookup"><span data-stu-id="6077c-132">When a [user consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse data in your tenant.</span></span>

10. <span data-ttu-id="6077c-133">當您啟用的某些服務會在您的租用戶中儲存資料時。</span><span class="sxs-lookup"><span data-stu-id="6077c-133">When you enable certain services that store data in your tenant.</span></span> <span data-ttu-id="6077c-134">重設密碼，這建立模型的一個範例是以服務主體的 toostore 密碼重設原則安全的方式。</span><span class="sxs-lookup"><span data-stu-id="6077c-134">One example of this is Password Reset, which is modeled as a service principal toostore your password reset policy securely.</span></span>

<span data-ttu-id="6077c-135">tooget 更多詳細資料上的應用程式如何加入 tooyour 目錄讀取[如何及為何將應用程式加入 tooAzure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added)。</span><span class="sxs-lookup"><span data-stu-id="6077c-135">tooget more details on how apps are added tooyour directory, read [How and why applications are added tooAzure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span></span>

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a><span data-ttu-id="6077c-136">我想 tooremove 在特定的使用者或群組的指派 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="6077c-136">I want tooremove a specific user’s or group’s assignment tooan application</span></span>

<span data-ttu-id="6077c-137">tooremove 的使用者或群組指派 tooan 應用程式，請遵循 hello 中所列的 hello 步驟[移除企業應用程式在 Azure Active Directory 中的使用者或群組指派](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal)發行項。</span><span class="sxs-lookup"><span data-stu-id="6077c-137">tooremove a user or group assignment tooan application, follow hello steps listed in hello [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

## <a name="i-want-toodisable-all-access-tooan-application-for-every-user"></a><span data-ttu-id="6077c-138">我想 toodisable 針對每個使用者的所有存取 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="6077c-138">I want toodisable all access tooan application for every user</span></span>

<span data-ttu-id="6077c-139">toodisable 所有使用者登入 tooan 應用程式，所列出的 hello 後續 hello 步驟[停用使用者登入企業應用程式在 Azure Active Directory 的](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal)發行項。</span><span class="sxs-lookup"><span data-stu-id="6077c-139">toodisable all user sign-ins tooan application, follow hello steps listed in hello [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-toodelete-an-application-entirely"></a><span data-ttu-id="6077c-140">我想完全 toodelete 應用程式</span><span class="sxs-lookup"><span data-stu-id="6077c-140">I want toodelete an application entirely</span></span>

<span data-ttu-id="6077c-141">太**刪除應用程式**，請遵循下列指示 hello:</span><span class="sxs-lookup"><span data-stu-id="6077c-141">too**delete an application**, follow hello instructions below:</span></span>

1.  <span data-ttu-id="6077c-142">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="6077c-142">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="6077c-143">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="6077c-143">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="6077c-144">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="6077c-144">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="6077c-145">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="6077c-145">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="6077c-146">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="6077c-146">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="6077c-147">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="6077c-147">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="6077c-148">選取您想要 toodelete hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6077c-148">Select hello application you want toodelete.</span></span>

7.  <span data-ttu-id="6077c-149">一旦 hello 應用程式載入時，按一下 **刪除**hello 最上層應用程式的圖示**概觀**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6077c-149">Once hello application loads, click **Delete** icon from hello top application’s **Overview** blade.</span></span>

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a><span data-ttu-id="6077c-150">我想 toodisable 所有未來的使用者同意作業 tooany 應用程式</span><span class="sxs-lookup"><span data-stu-id="6077c-150">I want toodisable all future user consent operations tooany application</span></span>

<span data-ttu-id="6077c-151">針對整個目錄防止終端使用者同意 tooany 應用程式，請停用使用者同意。</span><span class="sxs-lookup"><span data-stu-id="6077c-151">Disabling user consent for your entire directory prevent end users from consenting tooany application.</span></span> <span data-ttu-id="6077c-152">系統管理員仍然可以代表使用者行使同意。</span><span class="sxs-lookup"><span data-stu-id="6077c-152">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="6077c-153">同意 toolearn 進一步了解應用程式，以及為什麼您可能會或可能不希望 toodo，讀取[了解使用者和系統管理員同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)。</span><span class="sxs-lookup"><span data-stu-id="6077c-153">toolearn more about application consent, and why you may or may not wish toodo this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="6077c-154">太**停用整個目錄中的所有未來的使用者同意作業**，請遵循下列指示 hello:</span><span class="sxs-lookup"><span data-stu-id="6077c-154">too**disable all future user consent operations in your entire directory**, follow hello instructions below:</span></span>

1.  <span data-ttu-id="6077c-155">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="6077c-155">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="6077c-156">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="6077c-156">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="6077c-157">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="6077c-157">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="6077c-158">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="6077c-158">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="6077c-159">按一下 [使用者設定]。</span><span class="sxs-lookup"><span data-stu-id="6077c-159">click **User settings**.</span></span>

6.  <span data-ttu-id="6077c-160">停用所有未來的使用者同意作業設定 hello**使用者可以允許其資料應用程式 tooaccess**太切換**否**按一下 hello**儲存** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6077c-160">Disable all future user consent operations by setting hello **Users can allow apps tooaccess their data** toggle too**No** and click hello **Save** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6077c-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6077c-161">Next steps</span></span>
[<span data-ttu-id="6077c-162">使用 Azure Active Directory 管理應用程式</span><span class="sxs-lookup"><span data-stu-id="6077c-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)

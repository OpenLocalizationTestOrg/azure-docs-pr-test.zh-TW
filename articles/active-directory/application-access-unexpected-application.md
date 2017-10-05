---
title: "我的應用程式清單中有未預期的應用程式 | Microsoft Docs"
description: "如何檢視租用戶中的所有應用程式，並了解應用程式如何出現在 [企業應用程式] 下的 [所有應用程式] 清單中。"
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
ms.openlocfilehash: 0f8136cb066fa6e3e4a8dd06e34b9f866e3916f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-application-in-my-applications-list"></a><span data-ttu-id="ec8f1-103">我的應用程式清單中有未預期的應用程式</span><span class="sxs-lookup"><span data-stu-id="ec8f1-103">Unexpected application in my applications list</span></span>

<span data-ttu-id="ec8f1-104">本文協助您了解應用程式如何出現在 [企業應用程式] 下的 [所有應用程式] 清單中。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-104">This article help you to understand how applications appear in your **All Applications** list under **Enterprise Applications**.</span></span> 

## <a name="how-to-see-all-applications-in-your-tenant"></a><span data-ttu-id="ec8f1-105">如何查看租用戶中的所有應用程式</span><span class="sxs-lookup"><span data-stu-id="ec8f1-105">How to see all applications in your tenant</span></span>

<span data-ttu-id="ec8f1-106">若要查看租用戶中的所有應用程式，您需要使用 [篩選] 控制項，以顯示 [所有應用程式] 清單下的 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-106">To see all the applications in your tenant, you need to use the **Filter** control to show **All Applications** under the **All Applications** list.</span></span> <span data-ttu-id="ec8f1-107">若要這樣做，請遵循下面的步驟：</span><span class="sxs-lookup"><span data-stu-id="ec8f1-107">To do this, follow the steps below:</span></span>

1.  <span data-ttu-id="ec8f1-108">開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**或 **共同管理員**身分登入</span><span class="sxs-lookup"><span data-stu-id="ec8f1-108">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ec8f1-109">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-109">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ec8f1-110">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ec8f1-111">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-111">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ec8f1-112">按一下 [所有應用程式] 以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-112">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="ec8f1-113">按一下使用 [所有應用程式清單] 頂端的 [篩選]控制項。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-113">click the use the **Filter** control at the top of the **All Applications List**.</span></span>

7.  <span data-ttu-id="ec8f1-114">在 [篩選] 刀鋒視窗上，將 [顯示] 選項設為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-114">On the **Filter** blade, set the **Show** option to **All Applications.**</span></span>

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a><span data-ttu-id="ec8f1-115">特定應用程式為何出現在我的所有應用程式清單中？</span><span class="sxs-lookup"><span data-stu-id="ec8f1-115">Why does a specific application appear in my all applications list?</span></span>

<span data-ttu-id="ec8f1-116">篩選為 [所有應用程式] 時，[所有應用程式清單] 會顯示租用戶中的每個服務主體物件。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-116">When filtered to **All Applications**, the **All Applications** **List** shows every Service Principal object in your tenant.</span></span> <span data-ttu-id="ec8f1-117">服務主體物件可能以各種方式出現在此清單中︰</span><span class="sxs-lookup"><span data-stu-id="ec8f1-117">Service Principal objects can appear in this list in a various ways:</span></span>

1.  <span data-ttu-id="ec8f1-118">當您從應用程式庫新增任何應用程式時，包括︰</span><span class="sxs-lookup"><span data-stu-id="ec8f1-118">When you add any application from the application gallery, including:</span></span>

   1. <span data-ttu-id="ec8f1-119">**Azure AD 資源庫應用程式** – 與 Azure AD 預先整合以啟用單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

   2. <span data-ttu-id="ec8f1-120">**應用程式 Proxy** – 您想要提供從對外進行安全單一登入的應用程式 (在內部部署環境中執行)。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-120">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span></span>

   3. <span data-ttu-id="ec8f1-121">**自訂開發的應用程式** – 您的組織想要在 Azure AD 應用程式開發平台上開發的應用程式，但可能尚不存在。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-121">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span></span>

   4. <span data-ttu-id="ec8f1-122">**不在資源庫內的應用程式** – 引進您自己的應用程式！</span><span class="sxs-lookup"><span data-stu-id="ec8f1-122">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="ec8f1-123">您想要的任何網頁連結，或任何呈現使用者名稱和密碼欄位的應用程式，都支援 SAML 或 OpenID Connect 通訊協定，或支援您想要與 Azure AD 整合以啟用單一登入的 SCIM。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-123">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish to integrate for single sign-on with Azure AD.</span></span>

2.  <span data-ttu-id="ec8f1-124">註冊或登入與 Azure Active Directory 整合的第三方<sup></sup>應用程式時。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span></span> <span data-ttu-id="ec8f1-125">例如，[Smartsheet](https://app.smartsheet.com/b/home) 或 [DocuSign](https://www.docusign.net/member/MemberLogin.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-125">One example of this is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span></span>

3.  <span data-ttu-id="ec8f1-126">註冊或將使用者或群組的授權新增至第一方應用程式時，例如 [Microsoft Office 365](http://products.office.com/)。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-126">When signing up for, or adding a license to a user or a group to a first party application, like [Microsoft Office 365](http://products.office.com/).</span></span>

4.  <span data-ttu-id="ec8f1-127">當您使用[應用程式登錄](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration)建立自訂開發的應用程式來新增應用程式註冊時。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-127">When you add a new application registration by creating a custom-developed application using the [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span></span>

5.  <span data-ttu-id="ec8f1-128">當您使用 [V2.0 應用程式註冊入口網站](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal)建立自訂開發的應用程式來新增應用程式註冊時。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-128">When you add a new application registration by creating a custom-developed application using the [V2.0 Application Registration Portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span></span>

6.  <span data-ttu-id="ec8f1-129">當您新增您使用 Visual Studio 的 [ASP.net 驗證方法](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions)或[已連線服務](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx)所開發的應用程式時。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span></span>

7.  <span data-ttu-id="ec8f1-130">當您使用 [Azure AD PowerShell 模組](/powershell/azure/install-adv2?view=azureadps-2.0)建立服務主體物件。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-130">When you create a service principal object using the [Azure AD PowerShell Module](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

8.  <span data-ttu-id="ec8f1-131">當您以系統管理員身分[同意應用程式](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)使用您租用戶中的資料時。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-131">When you [consent to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator to use data in your tenant.</span></span>

9.  <span data-ttu-id="ec8f1-132">當[使用者同意應用程式](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)使用您租用戶中的資料時。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-132">When a [user consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to use data in your tenant.</span></span>

10. <span data-ttu-id="ec8f1-133">當您啟用的某些服務會在您的租用戶中儲存資料時。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-133">When you enable certain services that store data in your tenant.</span></span> <span data-ttu-id="ec8f1-134">例如重設密碼，它模擬成服務主體安全地儲存您的密碼重設原則。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-134">One example of this is Password Reset, which is modeled as a service principal to store your password reset policy securely.</span></span>

<span data-ttu-id="ec8f1-135">若要取得如何將應用程式新增至目錄的詳細資訊，請參閱[如何及為何將應用程式新增至 Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added)。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-135">To get more details on how apps are added to your directory, read [How and why applications are added to Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="ec8f1-136">我想要移除特定使用者或群組的應用程式指派</span><span class="sxs-lookup"><span data-stu-id="ec8f1-136">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="ec8f1-137">若要移除使用者或群組的應用程式指派，請依照[在 Azure Active Directory 中從企業應用程式移除使用者或群組指派](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal)文件列出的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-137">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

## <a name="i-want-to-disable-all-access-to-an-application-for-every-user"></a><span data-ttu-id="ec8f1-138">我想要讓每個使用者都無法存取應用程式</span><span class="sxs-lookup"><span data-stu-id="ec8f1-138">I want to disable all access to an application for every user</span></span>

<span data-ttu-id="ec8f1-139">若要讓所有使用者都無法登入應用程式，請依照[在 Azure Active Directory 中停用使用者登入企業應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal)文件列出的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-139">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="ec8f1-140">我想要完全刪除應用程式</span><span class="sxs-lookup"><span data-stu-id="ec8f1-140">I want to delete an application entirely</span></span>

<span data-ttu-id="ec8f1-141">若要**刪除應用程式**，請遵循下列指示：</span><span class="sxs-lookup"><span data-stu-id="ec8f1-141">To **delete an application**, follow the instructions below:</span></span>

1.  <span data-ttu-id="ec8f1-142">開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**或 **共同管理員**身分登入</span><span class="sxs-lookup"><span data-stu-id="ec8f1-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ec8f1-143">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ec8f1-144">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ec8f1-145">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ec8f1-146">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="ec8f1-147">若在這裡沒看到您要的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="ec8f1-148">選取您要刪除的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-148">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="ec8f1-149">應用程式載入後，從頂端應用程式的 [概觀] 刀鋒視窗按一下 [刪除] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-149">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="ec8f1-150">我想要停用任何應用程式的所有未來使用者同意作業</span><span class="sxs-lookup"><span data-stu-id="ec8f1-150">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="ec8f1-151">停用整個目錄的使用者同意會阻止使用者同意任何應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-151">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="ec8f1-152">系統管理員仍然可以代表使用者行使同意。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-152">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="ec8f1-153">若要進一步了解應用程式同意，以及為什麼您想要或不不想這樣做，請參閱[了解使用者和系統管理員同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-153">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="ec8f1-154">若要**停用整個目錄中的所有未來使用者同意作業**，請遵循下列指示：</span><span class="sxs-lookup"><span data-stu-id="ec8f1-154">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span></span>

1.  <span data-ttu-id="ec8f1-155">開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-155">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="ec8f1-156">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-156">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ec8f1-157">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-157">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ec8f1-158">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-158">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="ec8f1-159">按一下 [使用者設定]。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-159">click **User settings**.</span></span>

6.  <span data-ttu-id="ec8f1-160">將 [使用者可以允許應用程式存取其資料] 切換開關設為 [否]，並按一下 [儲存] 按鈕，以停用所有未來的使用者同意作業。</span><span class="sxs-lookup"><span data-stu-id="ec8f1-160">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec8f1-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ec8f1-161">Next steps</span></span>
[<span data-ttu-id="ec8f1-162">使用 Azure Active Directory 管理應用程式</span><span class="sxs-lookup"><span data-stu-id="ec8f1-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)

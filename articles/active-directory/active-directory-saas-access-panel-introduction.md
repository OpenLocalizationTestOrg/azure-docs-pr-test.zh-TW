---
title: "什麼是 Azure Active Directory 中的存取面板？ | Microsoft Docs"
description: "了解如何使用各種存取面板 (網頁瀏覽器、Android 應用程式、iPhone 和 iPad 應用程式) 存取 SaaS 應用程式。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: c0252d01-7e6e-4f79-a70e-600479577dfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd9066c251188c0f18fe1a9403baa2beaeeb987c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-the-access-panel"></a><span data-ttu-id="46ecc-104">什麼是存取面板？</span><span class="sxs-lookup"><span data-stu-id="46ecc-104">What is the access panel?</span></span>

<span data-ttu-id="46ecc-105">存取面板是網頁型入口網站。</span><span class="sxs-lookup"><span data-stu-id="46ecc-105">The access panel is a web-based portal.</span></span> <span data-ttu-id="46ecc-106">它可讓在 Azure Active Directory 中具有公司或學校帳戶的使用者，檢視和啟動 Azure AD 系統管理員已授權他們存取的雲端式應用程式。</span><span class="sxs-lookup"><span data-stu-id="46ecc-106">It enables a user with a work or school account in Azure Active Directory to view and start cloud-based applications an Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="46ecc-107">您也可以透過存取面板使用自助群組和應用程式管理功能。</span><span class="sxs-lookup"><span data-stu-id="46ecc-107">You can also use self-service group and app management capabilities through the access panel.</span></span>

<span data-ttu-id="46ecc-108">存取面板與 Azure 入口網站分開，您不需要具備 Azure 訂用帳戶也能使用。</span><span class="sxs-lookup"><span data-stu-id="46ecc-108">The access panel is separate from the Azure portal and does not you to have an Azure subscription.</span></span>

![存取面板][1]

<span data-ttu-id="46ecc-110">存取面板可讓您編輯某些設定檔設定，包括以下功能：</span><span class="sxs-lookup"><span data-stu-id="46ecc-110">The access panel enables you to edit some of your profile settings, including the ability to:</span></span>

- <span data-ttu-id="46ecc-111">變更與公司或學校帳戶相關聯的密碼</span><span class="sxs-lookup"><span data-stu-id="46ecc-111">Change the password associated with a work or school account</span></span>

- <span data-ttu-id="46ecc-112">編輯密碼重設設定</span><span class="sxs-lookup"><span data-stu-id="46ecc-112">Edit password reset settings</span></span>

- <span data-ttu-id="46ecc-113">編輯與 Multi-Factor Authentication 相關的連絡人和喜好設定的設定 (系統管理員已要求使用此功能的帳戶)</span><span class="sxs-lookup"><span data-stu-id="46ecc-113">Edit contact and preference settings related to multi-factor authentication (for accounts that have been required to use it by an administrator)</span></span>

- <span data-ttu-id="46ecc-114">檢視帳戶詳細資料，例如，使用者識別碼、替代電子郵件、行動電話和辦公室電話號碼以及裝置</span><span class="sxs-lookup"><span data-stu-id="46ecc-114">View account details, such as user ID, alternate email, and mobile and office phone numbers, and devices</span></span>

- <span data-ttu-id="46ecc-115">檢視和啟動 Azure AD 系統管理員已授權存取的雲端式應用程式。</span><span class="sxs-lookup"><span data-stu-id="46ecc-115">View and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="46ecc-116">如需以使用者觀點為主的存取面板詳細資訊，請參閱使用存取面板。</span><span class="sxs-lookup"><span data-stu-id="46ecc-116">For more information about the access panel from the users’ perspective, see Using the access panel.</span></span> 

- <span data-ttu-id="46ecc-117">自我管理群組。</span><span class="sxs-lookup"><span data-stu-id="46ecc-117">Self-manage groups.</span></span> <span data-ttu-id="46ecc-118">更具體地說，系統管理員可以在 Azure AD 中建立及管理安全性群組，並要求安全性群組成員資格。</span><span class="sxs-lookup"><span data-stu-id="46ecc-118">More specifically, the administrator can create and manage security groups and request security group memberships in Azure AD.</span></span> <span data-ttu-id="46ecc-119">如需詳細資訊，請參閱 [Azure AD 中使用者的自助群組管理](active-directory-accessmanagement-self-service-group-management.md)與[管理群組](active-directory-manage-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="46ecc-119">For more information, see [Self-service group management for users in Azure AD](active-directory-accessmanagement-self-service-group-management.md) and [Manage your groups](active-directory-manage-groups.md).</span></span>




## <a name="accessing-the-access-panel"></a><span data-ttu-id="46ecc-120">存取存取面板</span><span class="sxs-lookup"><span data-stu-id="46ecc-120">Accessing the access panel</span></span>

<span data-ttu-id="46ecc-121">您可以在網頁瀏覽器中瀏覽以下 URL，以存取「存取面板」：`http://myapps.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="46ecc-121">You can access the access panel by visiting the following URL in a web browser: `http://myapps.microsoft.com`</span></span>

<span data-ttu-id="46ecc-122">如果您已經為您的登入頁面設定自訂商標，您可以將您組織的網域附加到 URL 結尾以載入此商標：`http://myapps.microsoft.com/<your domain>.com`</span><span class="sxs-lookup"><span data-stu-id="46ecc-122">If you have custom branding configured for your sign-in page, you can load this branding by appending your organization’s domain to the end of the URL: `http://myapps.microsoft.com/<your domain>.com`</span></span>

<span data-ttu-id="46ecc-123">在此情況下，您可以使用已在 Azure 入口網站中設定的任何作用中或已驗證網域名稱。</span><span class="sxs-lookup"><span data-stu-id="46ecc-123">In this case, you can use any active or verified domain name that has been configured in your Azure portal.</span></span>

![Wingtip Toys 網域名稱][2]  

<span data-ttu-id="46ecc-125">您必須將 URL 散佈給要登入與 Azure AD 整合之應用程式的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="46ecc-125">You need to distribute the URL to all users who will sign in to applications that are integrated with Azure AD.</span></span>

## <a name="authentication"></a><span data-ttu-id="46ecc-126">驗證</span><span class="sxs-lookup"><span data-stu-id="46ecc-126">Authentication</span></span>

<span data-ttu-id="46ecc-127">若要觸達存取面板，您必須透過 Azure AD 中的公司或學校帳戶進行驗證。</span><span class="sxs-lookup"><span data-stu-id="46ecc-127">To reach the access panel, you must be authenticated through a work or school account in Azure AD.</span></span> <span data-ttu-id="46ecc-128">Azure AD 可以直接驗證您。</span><span class="sxs-lookup"><span data-stu-id="46ecc-128">You can be authenticated to Azure AD directly.</span></span> <span data-ttu-id="46ecc-129">或者，如果組織已經使用 Active Directory 同盟服務 (ADFS) 或其他技術設定同盟，則可由 Windows Server Active Directory 驗證您。</span><span class="sxs-lookup"><span data-stu-id="46ecc-129">Alternatively, if an organization has configured federation by using Active Directory Federation Services (AD FS) or other technologies, you can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="46ecc-130">如果您具備 Azure 或 Office 365 的訂用帳戶，而且已在使用 Azure 入口網站或 Office 365 應用程式，您可以看到應用程式清單，而不需再次登入。</span><span class="sxs-lookup"><span data-stu-id="46ecc-130">If you have a subscription for Azure or Office 365 and you have been using the Azure portal or an Office 365 application, you can see the list of applications without signing-in again.</span></span> <span data-ttu-id="46ecc-131">如果您未經過驗證，系統會提示您在 Azure AD 中使用您帳戶的使用者名稱和密碼進行登入。</span><span class="sxs-lookup"><span data-stu-id="46ecc-131">If you are are not authenticated you are prompted to sign in by using the username and password for your account in Azure AD.</span></span> <span data-ttu-id="46ecc-132">如果您的組織已設定同盟，則輸入使用者名稱已經足夠。</span><span class="sxs-lookup"><span data-stu-id="46ecc-132">If your organization has configured federation, typing the username is sufficient.</span></span>

<span data-ttu-id="46ecc-133">經過驗證後，您就能夠與由系統管理員整合到目錄的應用程式互動。</span><span class="sxs-lookup"><span data-stu-id="46ecc-133">When you are authenticated, you can interact with the applications that your administrator has integrated with the directory.</span></span> <span data-ttu-id="46ecc-134">若要了解如何整合應用程式與 Azure AD，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="46ecc-134">To learn how to integrate applications with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="web-browser-requirements"></a><span data-ttu-id="46ecc-135">網頁瀏覽器需求</span><span class="sxs-lookup"><span data-stu-id="46ecc-135">Web browser requirements</span></span>

<span data-ttu-id="46ecc-136">存取面板至少需要有支援 JavaScript 且啟用 CSS 的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="46ecc-136">At a minimum, the access panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="46ecc-137">若要讓使用者透過密碼單一登入 (SSO) 登入應用程式，必須在您的瀏覽器中安裝存取面板擴充功能。</span><span class="sxs-lookup"><span data-stu-id="46ecc-137">For the user to be signed in to applications through password-based single sign-on (SSO), the access panel extension must be installed in your browser.</span></span> <span data-ttu-id="46ecc-138">當您選取已設定密碼型 SSO 的應用程式時，系統就會自動下載此擴充功能。</span><span class="sxs-lookup"><span data-stu-id="46ecc-138">The extension is downloaded automatically when you select an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="46ecc-139">存取面板延伸模組目前適用於 Internet Explorer 8 和更新版本、Edge、Chrome 與 Firefox 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="46ecc-139">The access panel extension is currently available for Internet Explorer 8 and later, Edge, Chrome, and Firefox browsers.</span></span>

## <a name="mobile-app-support"></a><span data-ttu-id="46ecc-140">行動應用程式支援</span><span class="sxs-lookup"><span data-stu-id="46ecc-140">Mobile app support</span></span>

<span data-ttu-id="46ecc-141">Azure Active Directory 團隊發佈 My Apps 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="46ecc-141">The Azure Active Directory team publishes the my apps mobile app.</span></span> <span data-ttu-id="46ecc-142">當您安裝此應用程式時，可以在 iOS 和 Android 裝置上登入密碼 SSO 應用程式。</span><span class="sxs-lookup"><span data-stu-id="46ecc-142">When you install the app, you can sign in to password-based SSO applications on iOS and Android devices.</span></span>

> [!NOTE]
> <span data-ttu-id="46ecc-143">您不需要外掛程式或行動應用程式，就能在幾乎任何裝置的任何網頁瀏覽器上，登入支援與 Azure AD 同盟的應用程式 (包括 Salesforce、Google Apps、Dropbox、Box、Concur、Workday、Office 365 和其他 70 種以上的應用程式)。</span><span class="sxs-lookup"><span data-stu-id="46ecc-143">You can sign in to applications that support federation with Azure AD (including Salesforce, Google Apps, Dropbox, Box, Concur, Workday, Office 365, and more than 70 others) on virtually any web browser, on any device, without needing a plug-in or mobile app.</span></span> <span data-ttu-id="46ecc-144">同時也不需要在行動裝置上使用 My Apps 行動應用程式，就能[體驗其餘存取面板](https://myapps.microsoft.com/)的功能。</span><span class="sxs-lookup"><span data-stu-id="46ecc-144">All other [access panel experiences](https://myapps.microsoft.com/) do also not require the my apps mobile app to be used on a mobile device.</span></span>
>
>

### <a name="my-apps-for-android"></a><span data-ttu-id="46ecc-145">My Apps for Android</span><span class="sxs-lookup"><span data-stu-id="46ecc-145">My apps for Android</span></span>

<span data-ttu-id="46ecc-146">執行 Android 4.1 版和更新版本的任何 Android 裝置支援 My Apps for Android。</span><span class="sxs-lookup"><span data-stu-id="46ecc-146">My apps for Android is supported on any Android device that is running Android version 4.1 and later.</span></span>  
<span data-ttu-id="46ecc-147">已在 [Google Play 商店](https://play.google.com/store/apps/details?id=com.microsoft.myapps)中提供。</span><span class="sxs-lookup"><span data-stu-id="46ecc-147">It is available in the [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.myapps).</span></span>

![My Apps for Android][3]   

### <a name="my-apps-for-iphone-and-ipad"></a><span data-ttu-id="46ecc-149">My Apps for iPhone 和 iPad</span><span class="sxs-lookup"><span data-stu-id="46ecc-149">My apps for iPhone and iPad</span></span>

<span data-ttu-id="46ecc-150">執行 iOS 版本 7 和更新版本的任何 iPhone 或 iPad 均支援 My Apps for iOS。</span><span class="sxs-lookup"><span data-stu-id="46ecc-150">My apps for iOS is supported on any iPhone or iPad that is running iOS version 7 and later.</span></span>  
<span data-ttu-id="46ecc-151">已在 [Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8) 中提供。</span><span class="sxs-lookup"><span data-stu-id="46ecc-151">It is available in the [Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).</span></span>

![My Apps for iOS][4]    



## <a name="managed-browser-for-my-apps"></a><span data-ttu-id="46ecc-153">My Apps 適用的受管理瀏覽器</span><span class="sxs-lookup"><span data-stu-id="46ecc-153">Managed browser for my apps</span></span>

<span data-ttu-id="46ecc-154">My Apps 也已在 Intune Managed Browser 中整合。</span><span class="sxs-lookup"><span data-stu-id="46ecc-154">My apps is also integrated in the Intune Managed Browser.</span></span> <span data-ttu-id="46ecc-155">確保行動裝置上的資料安全無虞時，適用於 iOS 和 Android 裝置的 Intune Managed Browser 扮演重要角色。</span><span class="sxs-lookup"><span data-stu-id="46ecc-155">The Intune Managed Browser for iOS and Android devices plays a key role in ensuring that data on mobile devices stays secure.</span></span> <span data-ttu-id="46ecc-156">它可讓您安全地檢視和瀏覽可能包含公司資訊的網頁，並提供安全的網頁瀏覽經驗。</span><span class="sxs-lookup"><span data-stu-id="46ecc-156">It lets you safely view and navigate web pages that might contain company information, and provides a secure web-browsing experience.</span></span>  
<span data-ttu-id="46ecc-157">您可在 Managed Browser 首頁上以及您的書籤中尋求快速存取 My Apps，只有按幾下滑鼠就可以觸達您想要存取的任何應用程式。</span><span class="sxs-lookup"><span data-stu-id="46ecc-157">You find quick access to my apps on your Managed Browser homepage and in your bookmarks, giving you fewer clicks to reach any application you want to access.</span></span>

<span data-ttu-id="46ecc-158">已在 [Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) 和 [Google Play 商店](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en)中提供。</span><span class="sxs-lookup"><span data-stu-id="46ecc-158">It is available in the [Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) and [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).</span></span>

![My Apps 適用的受管理瀏覽器][5]    





## <a name="tips-for-testing-the-user-experience"></a><span data-ttu-id="46ecc-160">測試使用者體驗的秘訣</span><span class="sxs-lookup"><span data-stu-id="46ecc-160">Tips for testing the user experience</span></span>

<span data-ttu-id="46ecc-161">如果您是 Azure 系統管理員，而且已使用目錄中的帳戶登入 Azure 入口網站，則會自動以目前的帳戶登入存取面板。</span><span class="sxs-lookup"><span data-stu-id="46ecc-161">If you are an Azure administrator and you are signed in to the Azure portal by using an account in the directory, you are automatically signed in to the access panel as your current account.</span></span> <span data-ttu-id="46ecc-162">在此情況下，您可以看到已指派給您的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="46ecc-162">In this case, you can see all applications that have been assigned to you.</span></span>

<span data-ttu-id="46ecc-163">**若要以「不同」的使用者帳戶測試：**</span><span class="sxs-lookup"><span data-stu-id="46ecc-163">**To test as a *different* user account:**</span></span>

1. <span data-ttu-id="46ecc-164">按一下 Azure 入口網站或存取面板右上角的使用者功能表，然後選取 [登出]。</span><span class="sxs-lookup"><span data-stu-id="46ecc-164">Click the user menu in the upper-right corner of the Azure portal or the access panel, and then select **Sign Out**.</span></span> 
2. <span data-ttu-id="46ecc-165">前往[存取面板](http://myapps.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="46ecc-165">Go to the [access panel](http://myapps.microsoft.com).</span></span>
3. <span data-ttu-id="46ecc-166">在登入頁面上，針對您在目錄中想要測試的帳戶，輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="46ecc-166">On the sign-in page, type the username and password for the account in your directory you want to test.</span></span>


## <a name="starting-applications"></a><span data-ttu-id="46ecc-167">啟動應用程式</span><span class="sxs-lookup"><span data-stu-id="46ecc-167">Starting applications</span></span>

<span data-ttu-id="46ecc-168">存取面板上可能出現許多種應用程式。</span><span class="sxs-lookup"><span data-stu-id="46ecc-168">Several types of applications can appear on the access panel.</span></span>

### <a name="office-365-applications"></a><span data-ttu-id="46ecc-169">Office 365 應用程式</span><span class="sxs-lookup"><span data-stu-id="46ecc-169">Office 365 applications</span></span>

<span data-ttu-id="46ecc-170">如果組織使用 Office 365 應用程式，且您已取得其授權，則 Office 365 應用程式會出現在您的存取面板上。</span><span class="sxs-lookup"><span data-stu-id="46ecc-170">If your organization is using Office 365 applications and you are licensed for them, the Office 365 applications appear on your access panel.</span></span>

<span data-ttu-id="46ecc-171">當您按一下 Office 365 應用程式的應用程式圖格時，系統會將您重新導向至該應用程式，並自動登入。</span><span class="sxs-lookup"><span data-stu-id="46ecc-171">When you click an application tile for an Office 365 application, you are redirected to the application and automatically signed in.</span></span>

### <a name="microsoft-and-third-party-applications-configured-with-federation-based-sso"></a><span data-ttu-id="46ecc-172">已設定同盟 SSO 的 Microsoft 及第三方應用程式</span><span class="sxs-lookup"><span data-stu-id="46ecc-172">Microsoft and third-party applications configured with federation-based SSO</span></span>

<span data-ttu-id="46ecc-173">系統管理員可以在 Azure 入口網站的 Active Directory 區段中新增應用程式，並將 SSO 模式設定為 [Azure AD 單一登入]。</span><span class="sxs-lookup"><span data-stu-id="46ecc-173">Your administrator can add applications in the Active Directory section of the Azure portal with the SSO mode set to **Azure AD Single Sign-On**.</span></span> <span data-ttu-id="46ecc-174">只有當系統管理員已明確授權您存取應用程式時，您才能看到這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="46ecc-174">You can only see these applications if your administrator has explicitly granted you access to the applications.</span></span>

<span data-ttu-id="46ecc-175">當您按一下其中一個應用程式的圖格時，系統會將您重新導向並自動登入該應用程式。</span><span class="sxs-lookup"><span data-stu-id="46ecc-175">When you click a tile for one of these applications, you are redirected and automatically signed in to the application.</span></span>

### <a name="password-based-sso-without-identity-provisioning"></a><span data-ttu-id="46ecc-176">不含身分識別佈建的密碼 SSO</span><span class="sxs-lookup"><span data-stu-id="46ecc-176">Password-based SSO without identity provisioning</span></span>

<span data-ttu-id="46ecc-177">系統管理員可以在 Azure 入口網站的 Active Directory 區段中新增應用程式，並將 SSO 模式設定為 [密碼單一登入]。</span><span class="sxs-lookup"><span data-stu-id="46ecc-177">Your administrator can add applications in the Active Directory section of the Azure portal with the SSO mode set to **Password-based Single Sign-On**.</span></span> <span data-ttu-id="46ecc-178">目錄中的所有使用者都可以看到已設定為此模式的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="46ecc-178">All users in the directory can see all applications that have been configured in this mode.</span></span>

<span data-ttu-id="46ecc-179">您第一次按一下其中一個應用程式的圖格時，系統會提示您在 Internet Explorer 或 Chrome 中安裝密碼 SSO 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="46ecc-179">The first time, you click a tile for one of these applications, you are prompted to install the Password SSO plug-in for Internet Explorer or Chrome.</span></span> <span data-ttu-id="46ecc-180">安裝之後，您可能需要重新啟動網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="46ecc-180">The installation might require you to restart your web browser.</span></span> <span data-ttu-id="46ecc-181">當您返回存取面板，再次按一下應用程式圖格時，系統會提示您針對應用程式輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="46ecc-181">When you return to the access panel and click the application tile again, you are prompted for a username and password for the application.</span></span> <span data-ttu-id="46ecc-182">您已輸入使用者名稱和密碼之後，這些認證會安全地儲存並連結至您在 Azure AD 中的帳戶。</span><span class="sxs-lookup"><span data-stu-id="46ecc-182">When you have entered your username and password, these credentials are securely stored and linked to your account in Azure AD.</span></span>

<span data-ttu-id="46ecc-183">您下次按一下應用程式圖格時，您將會自動登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="46ecc-183">The next time you click the application tile, you are automatically signed in to the application.</span></span>  
<span data-ttu-id="46ecc-184">您不需要再次輸入認證，或安裝密碼 SSO 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="46ecc-184">You don't have to enter your credentials again and or install the Password SSO plug-in.</span></span>

<span data-ttu-id="46ecc-185">如果您的認證已在目標第三方應用程式中變更，那麼您也必須更新儲存在 Azure AD 中的認證。</span><span class="sxs-lookup"><span data-stu-id="46ecc-185">If your credentials have changed in the target third-party application, you must also update your credentials that are stored in Azure AD.</span></span> 

<span data-ttu-id="46ecc-186">**若要更新認證：**</span><span class="sxs-lookup"><span data-stu-id="46ecc-186">**To update credentials:**</span></span>

1. <span data-ttu-id="46ecc-187">選取應用程式圖格上的圖示。</span><span class="sxs-lookup"><span data-stu-id="46ecc-187">Select the icon on the application tile.</span></span>
2. <span data-ttu-id="46ecc-188">選取 [更新認證]，重新輸入應用程式的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="46ecc-188">Select **update credentials** to reenter the username and password for the application.</span></span>


### <a name="password-based-sso-with-identity-provisioning"></a><span data-ttu-id="46ecc-189">含身分識別佈建的密碼 SSO</span><span class="sxs-lookup"><span data-stu-id="46ecc-189">Password-based SSO with identity provisioning</span></span>

<span data-ttu-id="46ecc-190">系統管理員可以在 Azure 入口網站的 [Active Directory] 區段中新增應用程式，並將 SSO 模式設定為 [密碼單一登入]，同時佈建身分識別。</span><span class="sxs-lookup"><span data-stu-id="46ecc-190">Your administrator can add applications in the **Active Directory** section of the Azure portal with the SSO mode set to **Password-based Single Sign-On**, along with identity provisioning.</span></span>

<span data-ttu-id="46ecc-191">您第一次按一下其中一個應用程式的應用程式圖格時，系統會提示您安裝**適用於 Internet Explorer 或 Chrome 的密碼 SSO 外掛程式**。</span><span class="sxs-lookup"><span data-stu-id="46ecc-191">The first time, you click an application tile for one of these applications, you are prompted to install the **Password SSO plug-in for Internet Explorer or Chrome**.</span></span> <span data-ttu-id="46ecc-192">安裝之後，您可能需要重新啟動網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="46ecc-192">The installation might require you to restart your web browser.</span></span>  
<span data-ttu-id="46ecc-193">當您返回存取面板，再次按一下應用程式圖格時，您會自動登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="46ecc-193">When you return to the access panel and click the application tile again, you are automatically signed in to the application.</span></span>

<span data-ttu-id="46ecc-194">有些應用程式可能會要求您在第一次登入時變更密碼。</span><span class="sxs-lookup"><span data-stu-id="46ecc-194">Some applications might require you to change your password on the first sign-in.</span></span> <span data-ttu-id="46ecc-195">如果您的認證已在目標第三方應用程式中變更，那麼您也必須更新儲存在 Azure AD 中的認證。</span><span class="sxs-lookup"><span data-stu-id="46ecc-195">If your credentials have changed in the target third-party application, you must also update the credentials that are stored in Azure AD.</span></span> 

<span data-ttu-id="46ecc-196">**若要更新認證：**</span><span class="sxs-lookup"><span data-stu-id="46ecc-196">**To update credentials:**</span></span>

1. <span data-ttu-id="46ecc-197">選取應用程式圖格上的圖示。</span><span class="sxs-lookup"><span data-stu-id="46ecc-197">Select the icon on the application tile.</span></span>
2. <span data-ttu-id="46ecc-198">選取 [更新認證]，重新輸入應用程式的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="46ecc-198">Select **update credentials** to reenter the username and password for the application.</span></span>


### <a name="application-with-existing-sso-solutions"></a><span data-ttu-id="46ecc-199">含現有 SSO 解決方案的應用程式</span><span class="sxs-lookup"><span data-stu-id="46ecc-199">Application with existing SSO solutions</span></span>

<span data-ttu-id="46ecc-200">若要為應用程式設定 SSO，Azure 入口網站會提供稱為 [現有的單一登入] 的第三個選項。</span><span class="sxs-lookup"><span data-stu-id="46ecc-200">To configure SSO for an application, the Azure portal provides a third option called **Existing Single Sign-On**.</span></span> <span data-ttu-id="46ecc-201">這個選項可讓系統管理員建立應用程式的連結，並將連結放在選定使用者的存取面板上。</span><span class="sxs-lookup"><span data-stu-id="46ecc-201">This option enables your administrator to create a link to an application and place it on the access panel for selected users.</span></span>

<span data-ttu-id="46ecc-202">例如，如果應用程式設定為使用 AD FS 2.0 來驗證使用者，系統管理員可以使用 [現有的單一登入] 選項，在存取面板上建立該應用程式的連結。</span><span class="sxs-lookup"><span data-stu-id="46ecc-202">For example, if an application is configured to authenticate users by using AD FS 2.0, your administrator can use the **Existing Single Sign-On** option to create a link to it on the access panel.</span></span> <span data-ttu-id="46ecc-203">當您存取連結時，將會透過 AD FS 2.0 或應用程式提供的任何現有 SSO 解決方案來驗證您。</span><span class="sxs-lookup"><span data-stu-id="46ecc-203">When you access the link, you are authenticated through AD FS 2.0 or whatever existing SSO solution the application provides.</span></span>


## <a name="next-steps"></a><span data-ttu-id="46ecc-204">後續步驟</span><span class="sxs-lookup"><span data-stu-id="46ecc-204">Next steps</span></span>

- <span data-ttu-id="46ecc-205">若要查看與應用程式管理相關的所有主題清單，請參閱 [Azure Active Directory 中的應用程式管理文章索引](active-directory-apps-index.md)。</span><span class="sxs-lookup"><span data-stu-id="46ecc-205">To see a list of all topics that are related to application management, see the [article index for application management in Azure Active Directory](active-directory-apps-index.md).</span></span>
 
- <span data-ttu-id="46ecc-206">若要深入了解如何將 SaaS 應用程式整合到 Azure AD 中，請參閱[有關如何整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)。</span><span class="sxs-lookup"><span data-stu-id="46ecc-206">To learn how to integrate a SaaS app into Azure AD, see the [list of tutorials on how to integrate SaaS apps](active-directory-saas-tutorial-list.md).</span></span>
 
- <span data-ttu-id="46ecc-207">若要深入了解如何使用 Azure AD 管理應用程式，請參閱[單一登入及使用 Azure Active Directory 管理應用程式存取的簡介](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="46ecc-207">To learn more about managing apps with Azure AD, see the [introduction to single sign-on and managing app access with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>
 
- <span data-ttu-id="46ecc-208">若要深入了解使用者佈建，請參閱 [SaaS 應用程式的自動化使用者佈建和解除佈建](active-directory-saas-app-provisioning.md)。</span><span class="sxs-lookup"><span data-stu-id="46ecc-208">To learn more about user provisioning, see [automate user provisioning and deprovisioning to SaaS applications](active-directory-saas-app-provisioning.md).</span></span>

<!--Image references-->
[1]: ./media/active-directory-saas-access-panel-introduction/01.png
[2]: ./media/active-directory-saas-access-panel-introduction/02.png
[3]: ./media/active-directory-saas-access-panel-introduction/03.png
[4]: ./media/active-directory-saas-access-panel-introduction/04.png
[5]: ./media/active-directory-saas-access-panel-introduction/05.png

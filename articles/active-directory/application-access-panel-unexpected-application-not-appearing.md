---
title: "指派的應用程式未出現在存取面板上 | Microsoft Docs"
description: "針對應用程式為什麼未出現在存取面板上進行疑難排解"
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
ms.openlocfilehash: 9ea5744d77b90929598ea5feb80c7bbdff3772fc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="an-assigned-application-is-not-appearing-on-the-access-panel"></a><span data-ttu-id="885fa-103">指派的應用程式未出現在存取面板上</span><span class="sxs-lookup"><span data-stu-id="885fa-103">An assigned application is not appearing on the access panel</span></span>

<span data-ttu-id="885fa-104">存取面板是網頁型入口網站，可讓在 Azure Active Directory (Azure AD) 中具有公司或學校帳戶的使用者，檢視和啟動 Azure AD 系統管理員已授權他們存取的雲端式應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="885fa-105">在 Azure AD 入口網站中可代表使用者設定這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="885fa-106">應用程式必須經過正確的設定並指派至使用者或使用者所屬的群組，才能在存取面板中顯示該應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="885fa-107">使用者能看見的應用程式類型可分為以下類別：</span><span class="sxs-lookup"><span data-stu-id="885fa-107">The type of apps a user may be seeing fall in the following categories:</span></span>

-   <span data-ttu-id="885fa-108">Office 365 應用程式</span><span class="sxs-lookup"><span data-stu-id="885fa-108">Office 365 Applications</span></span>

-   <span data-ttu-id="885fa-109">已設定同盟 SSO 的 Microsoft 及第三方應用程式</span><span class="sxs-lookup"><span data-stu-id="885fa-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="885fa-110">密碼型 SSO 應用程式</span><span class="sxs-lookup"><span data-stu-id="885fa-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="885fa-111">含現有 SSO 解決方案的應用程式</span><span class="sxs-lookup"><span data-stu-id="885fa-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="885fa-112">首先檢查一般問題</span><span class="sxs-lookup"><span data-stu-id="885fa-112">General issues to check first</span></span>

-   <span data-ttu-id="885fa-113">如果才剛將應用程式新增至使用者，請在幾分鐘之後嘗試登入並再次登出使用者的存取面板，以查明是否已新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-113">If an application was just added to a user, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is added.</span></span>

-   <span data-ttu-id="885fa-114">如果才剛從使用者或使用者所屬群組移除授權，則根據群組的大小和複雜度而定，可能要經過一段很長的時間，變更才會生效。</span><span class="sxs-lookup"><span data-stu-id="885fa-114">If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span></span> <span data-ttu-id="885fa-115">登入存取面板之前，請多等一些時間。</span><span class="sxs-lookup"><span data-stu-id="885fa-115">Allow for extra time before signing into the Access Panel.</span></span>

## <a name="problems-related-to-application-configuration"></a><span data-ttu-id="885fa-116">應用程式設定的相關問題</span><span class="sxs-lookup"><span data-stu-id="885fa-116">Problems related to application configuration</span></span>

<span data-ttu-id="885fa-117">應用程式未出現在使用者的存取面板上可能是因為並未正確設定。</span><span class="sxs-lookup"><span data-stu-id="885fa-117">An application may not be appearing in a user’s Access Panel because it is not configured properly.</span></span> <span data-ttu-id="885fa-118">以下提供一些方式，可讓您用來針對應用程式設定的相關問題進行疑難排解：</span><span class="sxs-lookup"><span data-stu-id="885fa-118">Below are some ways you can troubleshoot issues related to application configuration:</span></span>

-   [<span data-ttu-id="885fa-119">如何為 Azure AD 資源庫應用程式設定同盟單一登入</span><span class="sxs-lookup"><span data-stu-id="885fa-119">How to configure federated single sign-on for an Azure AD gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [<span data-ttu-id="885fa-120">如何為不在資源庫內的應用程式設定同盟單一登入</span><span class="sxs-lookup"><span data-stu-id="885fa-120">How to configure federated single sign-on for a non-gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="885fa-121">如何為 Azure AD 資源庫應用程式設定密碼單一登入應用程式</span><span class="sxs-lookup"><span data-stu-id="885fa-121">How to configure a password single sign-on application for an Azure AD gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="885fa-122">如何為不在資源庫內的應用程式設定密碼單一登入應用程式</span><span class="sxs-lookup"><span data-stu-id="885fa-122">How to configure a password single sign-on application for a non-gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="885fa-123">如何為 Azure AD 資源庫應用程式設定同盟單一登入</span><span class="sxs-lookup"><span data-stu-id="885fa-123">How to configure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="885fa-124">Azure AD 資源庫中所有透過企業單一登入功能啟用的應用程式都提供逐步教學課程。</span><span class="sxs-lookup"><span data-stu-id="885fa-124">All applications in the Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="885fa-125">您可以存取[如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/)，以取得詳細的逐步指引。</span><span class="sxs-lookup"><span data-stu-id="885fa-125">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="885fa-126">若要設定 Azure AD 資源庫中的應用程式，您必須：</span><span class="sxs-lookup"><span data-stu-id="885fa-126">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="885fa-127">從 Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="885fa-127">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="885fa-128">在 Azure AD 中設定應用程式的中繼資料值 (登入 URL、識別碼、回覆 URL)</span><span class="sxs-lookup"><span data-stu-id="885fa-128">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="885fa-129">選取使用者識別碼並新增要傳送到應用程式的使用者屬性</span><span class="sxs-lookup"><span data-stu-id="885fa-129">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="885fa-130">擷取 Azure AD 中繼資料與憑證</span><span class="sxs-lookup"><span data-stu-id="885fa-130">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="885fa-131">在應用程式中設定 Azure AD 中繼資料值 (登入 URL、簽發者、登出 URL 與憑證)</span><span class="sxs-lookup"><span data-stu-id="885fa-131">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="885fa-132">從 Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="885fa-132">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="885fa-133">若要從 Azure AD 資源庫新增應用程式，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="885fa-133">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="885fa-134">開啟 [Azure 入口網站](https://portal.azure.com)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="885fa-134">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="885fa-135">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-135">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="885fa-136">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="885fa-136">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="885fa-137">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-137">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="885fa-138">按一下 [企業應用程式] 刀鋒視窗右上角的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="885fa-138">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="885fa-139">在 [從資源庫新增] 區段的 [輸入名稱] 文字方塊中，輸入應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="885fa-139">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="885fa-140">選取您要設為單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-140">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="885fa-141">新增應用程式之前，您可以從 [名稱] 文字方塊變更其名稱。</span><span class="sxs-lookup"><span data-stu-id="885fa-141">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="885fa-142">按一下 [新增] 按鈕新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-142">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="885fa-143">稍候片刻，您便能看見應用程式的設定刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="885fa-143">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="885fa-144">從 Azure AD 資源庫為應用程式設定單一登入</span><span class="sxs-lookup"><span data-stu-id="885fa-144">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="885fa-145">若要設定應用程式使用單一登入，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="885fa-145">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="885fa-146">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="885fa-146">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="885fa-147">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-147">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="885fa-148">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="885fa-148">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="885fa-149">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-149">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="885fa-150">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="885fa-150">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="885fa-151">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-151">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="885fa-152">選取您要設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-152">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="885fa-153">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="885fa-153">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="885fa-154">從 [模式] 下拉式清單選取 [SAML 登入]。</span><span class="sxs-lookup"><span data-stu-id="885fa-154">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="885fa-155">在 [網域及 URL] 中輸入必要值。</span><span class="sxs-lookup"><span data-stu-id="885fa-155">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="885fa-156">這些值應從應用程式廠商處取得。</span><span class="sxs-lookup"><span data-stu-id="885fa-156">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="885fa-157">若要將應用程式設定為 SP 啟始的 SSO，則登入 URL 為必要值。</span><span class="sxs-lookup"><span data-stu-id="885fa-157">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="885fa-158">對於某些應用程式，識別碼也是必要值。</span><span class="sxs-lookup"><span data-stu-id="885fa-158">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="885fa-159">若要將應用程式設定為 IdP 啟始的單一登入，則 [登入 URL] 為必要值。</span><span class="sxs-lookup"><span data-stu-id="885fa-159">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="885fa-160">對於某些應用程式，識別碼也是必要值。</span><span class="sxs-lookup"><span data-stu-id="885fa-160">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="885fa-161">**選擇性：**如果您想要看到非必要值，請按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="885fa-161">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="885fa-162">在 [使用者屬性] 中，從 [使用者識別碼] 下拉式清單選取使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="885fa-162">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="885fa-163">**選擇性：**按一下 [檢視和編輯所有其他使用者屬性]，以編輯當使用者登入時要以 SAML 權杖傳送至應用程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="885fa-163">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="885fa-164">新增屬性：</span><span class="sxs-lookup"><span data-stu-id="885fa-164">To add an attribute:</span></span>

   1. <span data-ttu-id="885fa-165">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="885fa-165">click **Add attribute**.</span></span> <span data-ttu-id="885fa-166">輸入 [名稱]，然後從下拉式清單選取 [值]。</span><span class="sxs-lookup"><span data-stu-id="885fa-166">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="885fa-167">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="885fa-167">click **Save.**</span></span> <span data-ttu-id="885fa-168">您會在資料表中看到新屬性。</span><span class="sxs-lookup"><span data-stu-id="885fa-168">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="885fa-169">按一下 [設定 &lt;應用程式名稱&gt;]，以存取如何在應用程式中設定單一登入的文件。</span><span class="sxs-lookup"><span data-stu-id="885fa-169">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="885fa-170">此外，您會有透過該應用程式設定 SSO 所需的中繼資料 URL 與憑證。</span><span class="sxs-lookup"><span data-stu-id="885fa-170">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="885fa-171">按一下 [儲存] 以儲存組態。</span><span class="sxs-lookup"><span data-stu-id="885fa-171">click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="885fa-172">將使用者指派至應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-172">Assign users to the application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="885fa-173">選取使用者識別碼並新增要傳送到應用程式的使用者屬性</span><span class="sxs-lookup"><span data-stu-id="885fa-173">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="885fa-174">若要選取使用者識別碼或新增使用者屬性，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="885fa-174">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="885fa-175">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="885fa-175">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="885fa-176">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-176">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="885fa-177">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="885fa-177">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="885fa-178">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-178">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="885fa-179">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="885fa-179">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="885fa-180">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-180">If you do not see the application you want to show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="885fa-181">選取您已設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-181">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="885fa-182">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="885fa-182">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="885fa-183">在 [使用者屬性] 區段下，從 [使用者識別碼] 下拉式清單選取使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="885fa-183">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="885fa-184">所選的選項必須符合應用程式中預期的值，才能驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="885fa-184">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="885fa-185">Azure AD 會根據應用程式在 SAML AuthRequest 中選取的值或要求的格式，來選取 NameID 屬性 (使用者識別碼) 的格式。</span><span class="sxs-lookup"><span data-stu-id="885fa-185">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="885fa-186">如需詳細資訊，請參閱[單一登入 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)文章中的＜NameIDPolicy＞一節。</span><span class="sxs-lookup"><span data-stu-id="885fa-186">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="885fa-187">若要新增使用者屬性，按一下 [檢視和編輯所有其他使用者屬性]，以編輯當使用者登入時要以 SAML 權杖傳送至應用程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="885fa-187">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="885fa-188">新增屬性：</span><span class="sxs-lookup"><span data-stu-id="885fa-188">To add an attribute:</span></span>

   1. <span data-ttu-id="885fa-189">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="885fa-189">click **Add attribute**.</span></span> <span data-ttu-id="885fa-190">輸入 [名稱]，然後從下拉式清單選取 [值]。</span><span class="sxs-lookup"><span data-stu-id="885fa-190">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="885fa-191">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="885fa-191">click **Save.**</span></span> <span data-ttu-id="885fa-192">您會在資料表中看到新屬性。</span><span class="sxs-lookup"><span data-stu-id="885fa-192">You will see the new attribute in the table.</span></span>

#### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="885fa-193">下載 Azure AD 中繼資料或憑證</span><span class="sxs-lookup"><span data-stu-id="885fa-193">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="885fa-194">若要從 Azure AD 下載應用程式中繼資料或憑證，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="885fa-194">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="885fa-195">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="885fa-195">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="885fa-196">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-196">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="885fa-197">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="885fa-197">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="885fa-198">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-198">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="885fa-199">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="885fa-199">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="885fa-200">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-200">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="885fa-201">選取您已設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-201">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="885fa-202">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="885fa-202">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="885fa-203">移至 [SAML 簽署憑證] 區段，然後按一下 [下載] 資料行值。</span><span class="sxs-lookup"><span data-stu-id="885fa-203">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="885fa-204">根據應用程式設定單一登入時所需的項目，您會看到下載中繼資料 XML 或憑證的選項。</span><span class="sxs-lookup"><span data-stu-id="885fa-204">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="885fa-205">Azure AD 不提供取得中繼資料的 URL。</span><span class="sxs-lookup"><span data-stu-id="885fa-205">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="885fa-206">只能將中繼資料擷取為 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="885fa-206">The metadata can only be retrieved as a XML file.</span></span>

### <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="885fa-207">如何為不在資源庫內的應用程式設定同盟單一登入</span><span class="sxs-lookup"><span data-stu-id="885fa-207">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="885fa-208">若要設定不在資源庫內的應用程式，您必須有 Azure AD Premium，且應用程式必須支援 SAML 2.0。</span><span class="sxs-lookup"><span data-stu-id="885fa-208">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="885fa-209">如需有關 Azure AD 版本的詳細資訊，請參閱 [Azure AD 定價](https://azure.microsoft.com/pricing/details/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="885fa-209">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="885fa-210">在 Azure AD 中設定應用程式的中繼資料值 (登入 URL、識別碼、回覆 URL)</span><span class="sxs-lookup"><span data-stu-id="885fa-210">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="885fa-211">選取使用者識別碼並新增要傳送到應用程式的使用者屬性</span><span class="sxs-lookup"><span data-stu-id="885fa-211">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="885fa-212">擷取 Azure AD 中繼資料與憑證</span><span class="sxs-lookup"><span data-stu-id="885fa-212">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="885fa-213">在應用程式中設定 Azure AD 中繼資料值 (登入 URL、簽發者、登出 URL 與憑證)</span><span class="sxs-lookup"><span data-stu-id="885fa-213">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

#### <a name="configure-the-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="885fa-214">在 Azure AD 中設定應用程式的中繼資料值 (登入 URL、識別碼、回覆 URL)</span><span class="sxs-lookup"><span data-stu-id="885fa-214">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="885fa-215">若要為不在 Azure AD 資源庫中的應用程式設定單一登入，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="885fa-215">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="885fa-216">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="885fa-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="885fa-217">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="885fa-218">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="885fa-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="885fa-219">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-219">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="885fa-220">按一下 [企業應用程式] 刀鋒視窗右上角的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="885fa-220">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="885fa-221">按一下 [新增您自己的應用程式] 區段中的 [不在資源庫內的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-221">click **Non-gallery application** in the **Add your own app** section.</span></span>

7.  <span data-ttu-id="885fa-222">在 [名稱] 文字方塊中輸入應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="885fa-222">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="885fa-223">按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-223">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="885fa-224">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="885fa-224">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="885fa-225">在 [模式] 下拉式清單中選取 [SAML 登入]。</span><span class="sxs-lookup"><span data-stu-id="885fa-225">Select **SAML-based Sign-on** in the **Mode** dropdown.</span></span>

11. <span data-ttu-id="885fa-226">在 [網域及 URL] 中輸入必要值。</span><span class="sxs-lookup"><span data-stu-id="885fa-226">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="885fa-227">這些值應從應用程式廠商處取得。</span><span class="sxs-lookup"><span data-stu-id="885fa-227">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="885fa-228">若要將應用程式設定為 IdP 啟始的 SSO，請輸入回覆 URL 與識別碼。</span><span class="sxs-lookup"><span data-stu-id="885fa-228">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

   2.  <span data-ttu-id="885fa-229">**選擇性：**若要將應用程式設定為 SP 啟始的 SSO，則登入 URL 為必要值。</span><span class="sxs-lookup"><span data-stu-id="885fa-229">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="885fa-230">在 [使用者屬性] 中，從 [使用者識別碼] 下拉式清單選取使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="885fa-230">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="885fa-231">**選擇性：**按一下 [檢視和編輯所有其他使用者屬性]，以編輯當使用者登入時要以 SAML 權杖傳送至應用程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="885fa-231">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="885fa-232">新增屬性：</span><span class="sxs-lookup"><span data-stu-id="885fa-232">To add an attribute:</span></span>

   1. <span data-ttu-id="885fa-233">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="885fa-233">click **Add attribute**.</span></span> <span data-ttu-id="885fa-234">輸入 [名稱]，然後從下拉式清單選取 [值]。</span><span class="sxs-lookup"><span data-stu-id="885fa-234">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="885fa-235">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="885fa-235">Click **Save.**</span></span> <span data-ttu-id="885fa-236">您會在資料表中看到新屬性。</span><span class="sxs-lookup"><span data-stu-id="885fa-236">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="885fa-237">按一下 [設定 &lt;應用程式名稱&gt;]，以存取如何在應用程式中設定單一登入的文件。</span><span class="sxs-lookup"><span data-stu-id="885fa-237">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="885fa-238">此外，您有應用程式所需的 Azure AD URL 與憑證。</span><span class="sxs-lookup"><span data-stu-id="885fa-238">Also, you has Azure AD URLs and certificate required for the application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="885fa-239">選取使用者識別碼並新增要傳送到應用程式的使用者屬性</span><span class="sxs-lookup"><span data-stu-id="885fa-239">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="885fa-240">若要選取使用者識別碼或新增使用者屬性，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="885fa-240">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="885fa-241">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="885fa-241">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="885fa-242">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-242">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="885fa-243">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="885fa-243">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="885fa-244">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-244">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="885fa-245">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="885fa-245">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="885fa-246">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-246">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="885fa-247">選取您已設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-247">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="885fa-248">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="885fa-248">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="885fa-249">在 [使用者屬性] 區段下，從 [使用者識別碼] 下拉式清單選取使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="885fa-249">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="885fa-250">所選的選項必須符合應用程式中預期的值，才能驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="885fa-250">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="885fa-251">Azure AD 會根據應用程式在 SAML AuthRequest 中選取的值或要求的格式，來選取 NameID 屬性 (使用者識別碼) 的格式。</span><span class="sxs-lookup"><span data-stu-id="885fa-251">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="885fa-252">如需詳細資訊，請參閱[單一登入 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)文章中的＜NameIDPolicy＞一節。</span><span class="sxs-lookup"><span data-stu-id="885fa-252">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="885fa-253">若要新增使用者屬性，按一下 [檢視和編輯所有其他使用者屬性]，以編輯當使用者登入時要以 SAML 權杖傳送至應用程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="885fa-253">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="885fa-254">新增屬性：</span><span class="sxs-lookup"><span data-stu-id="885fa-254">To add an attribute:</span></span>

   1. <span data-ttu-id="885fa-255">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="885fa-255">click **Add attribute**.</span></span> <span data-ttu-id="885fa-256">輸入 [名稱]，然後從下拉式清單選取 [值]。</span><span class="sxs-lookup"><span data-stu-id="885fa-256">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="885fa-257">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="885fa-257">Click **Save.**</span></span> <span data-ttu-id="885fa-258">您會在資料表中看到新屬性。</span><span class="sxs-lookup"><span data-stu-id="885fa-258">You see the new attribute in the table.</span></span>

#### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="885fa-259">下載 Azure AD 中繼資料或憑證</span><span class="sxs-lookup"><span data-stu-id="885fa-259">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="885fa-260">若要從 Azure AD 下載應用程式中繼資料或憑證，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="885fa-260">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="885fa-261">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="885fa-261">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="885fa-262">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-262">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="885fa-263">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="885fa-263">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="885fa-264">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-264">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="885fa-265">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="885fa-265">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="885fa-266">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-266">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="885fa-267">選取您已設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-267">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="885fa-268">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="885fa-268">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="885fa-269">移至 [SAML 簽署憑證] 區段，然後按一下 [下載] 資料行值。</span><span class="sxs-lookup"><span data-stu-id="885fa-269">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="885fa-270">根據應用程式設定單一登入時所需的項目，您會看到下載中繼資料 XML 或憑證的選項。</span><span class="sxs-lookup"><span data-stu-id="885fa-270">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="885fa-271">Azure AD 不提供取得中繼資料的 URL。</span><span class="sxs-lookup"><span data-stu-id="885fa-271">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="885fa-272">只能將中繼資料擷取為 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="885fa-272">The metadata can only be retrieved as a XML file.</span></span>

### <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="885fa-273">如何為 Azure AD 資源庫應用程式設定密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="885fa-273">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="885fa-274">若要設定 Azure AD 資源庫中的應用程式，您必須：</span><span class="sxs-lookup"><span data-stu-id="885fa-274">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="885fa-275">從 Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="885fa-275">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="885fa-276">設定應用程式使用密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="885fa-276">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="885fa-277">從 Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="885fa-277">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="885fa-278">若要從 Azure AD 資源庫新增應用程式，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="885fa-278">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="885fa-279">開啟 [Azure 入口網站](https://portal.azure.com)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="885fa-279">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="885fa-280">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-280">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="885fa-281">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="885fa-281">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="885fa-282">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-282">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="885fa-283">按一下 [企業應用程式] 刀鋒視窗右上角的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="885fa-283">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="885fa-284">在 [從資源庫新增] 區段的 [輸入名稱] 文字方塊中，輸入應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="885fa-284">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="885fa-285">選取您要設為單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-285">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="885fa-286">新增應用程式之前，您可以從 [名稱] 文字方塊變更其名稱。</span><span class="sxs-lookup"><span data-stu-id="885fa-286">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="885fa-287">按一下 [新增] 按鈕新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-287">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="885fa-288">稍候片刻，您便能看見應用程式的設定刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="885fa-288">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="885fa-289">設定應用程式使用密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="885fa-289">Configure the application for password single sign-on</span></span>

<span data-ttu-id="885fa-290">若要設定應用程式使用單一登入，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="885fa-290">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="885fa-291">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="885fa-291">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="885fa-292">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-292">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="885fa-293">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="885fa-293">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="885fa-294">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-294">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="885fa-295">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="885fa-295">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="885fa-296">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-296">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="885fa-297">選取您要設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-297">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="885fa-298">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="885fa-298">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="885fa-299">選取 [以密碼為基礎的登入] 模式。</span><span class="sxs-lookup"><span data-stu-id="885fa-299">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="885fa-300">[將使用者指派至應用程式](#how-to-assign-a-user-to-an-application-directly)。</span><span class="sxs-lookup"><span data-stu-id="885fa-300">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="885fa-301">此外，您也可以選取使用者資料列，按一下 [更新認證]，然後代表使用者輸入使用者名稱和密碼，以代表使用者提供認證。</span><span class="sxs-lookup"><span data-stu-id="885fa-301">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="885fa-302">否則，系統會提示使用者在啟動時自行輸入認證。</span><span class="sxs-lookup"><span data-stu-id="885fa-302">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="885fa-303">如何為不在資源庫內的應用程式設定密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="885fa-303">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="885fa-304">若要設定 Azure AD 資源庫中的應用程式，您必須：</span><span class="sxs-lookup"><span data-stu-id="885fa-304">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="885fa-305">新增不在資源庫內的應用程式</span><span class="sxs-lookup"><span data-stu-id="885fa-305">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="885fa-306">設定應用程式使用密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="885fa-306">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a><span data-ttu-id="885fa-307">新增不在資源庫內的應用程式</span><span class="sxs-lookup"><span data-stu-id="885fa-307">Add a non-gallery application</span></span>

<span data-ttu-id="885fa-308">若要從 Azure AD 資源庫新增應用程式，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="885fa-308">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="885fa-309">開啟 [Azure 入口網站](https://portal.azure.com)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="885fa-309">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="885fa-310">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-310">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="885fa-311">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="885fa-311">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="885fa-312">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-312">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="885fa-313">按一下 [企業應用程式] 刀鋒視窗右上角的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="885fa-313">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="885fa-314">按一下 [不在資源庫內的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-314">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="885fa-315">在 [名稱] 文字方塊中輸入應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="885fa-315">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="885fa-316">選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="885fa-316">Select **Add.**</span></span>

<span data-ttu-id="885fa-317">稍候片刻，您便能看見應用程式的設定刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="885fa-317">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="885fa-318">設定應用程式使用密碼單一登入</span><span class="sxs-lookup"><span data-stu-id="885fa-318">Configure the application for password single sign-on</span></span>

<span data-ttu-id="885fa-319">若要設定應用程式使用單一登入，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="885fa-319">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="885fa-320">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="885fa-320">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="885fa-321">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-321">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="885fa-322">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="885fa-322">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="885fa-323">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-323">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="885fa-324">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="885fa-324">click **All Applications** to view a list of all your applications.</span></span>

    1.  <span data-ttu-id="885fa-325">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-325">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="885fa-326">選取您要設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-326">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="885fa-327">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="885fa-327">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="885fa-328">選取 [以密碼為基礎的登入] 模式。</span><span class="sxs-lookup"><span data-stu-id="885fa-328">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="885fa-329">輸入**登入 URL**。</span><span class="sxs-lookup"><span data-stu-id="885fa-329">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="885fa-330">這是使用者輸入使用者名稱和密碼來登入的 URL。</span><span class="sxs-lookup"><span data-stu-id="885fa-330">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="885fa-331">確定在該 URL 上看得到登入欄位。</span><span class="sxs-lookup"><span data-stu-id="885fa-331">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="885fa-332">[將使用者指派給應用程式](#how-to-assign-a-user-to-an-application-directly)。</span><span class="sxs-lookup"><span data-stu-id="885fa-332">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

11. <span data-ttu-id="885fa-333">此外，您也可以選取使用者資料列，按一下 [更新認證]，然後代表使用者輸入使用者名稱和密碼，以代表使用者提供認證。</span><span class="sxs-lookup"><span data-stu-id="885fa-333">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="885fa-334">否則，系統會提示使用者在啟動時自行輸入認證。</span><span class="sxs-lookup"><span data-stu-id="885fa-334">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="problems-related-to-assigning-applications-to-users"></a><span data-ttu-id="885fa-335">將應用程式指派給使用者的相關問題</span><span class="sxs-lookup"><span data-stu-id="885fa-335">Problems related to assigning applications to users</span></span>

<span data-ttu-id="885fa-336">使用者可能因為未將他們指派給應用程式，而無法在其存取面板上看見該應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-336">A user may not be seeing an application on their Access Panel because they are not assigned to the application.</span></span> <span data-ttu-id="885fa-337">以下是一些檢查方法：</span><span class="sxs-lookup"><span data-stu-id="885fa-337">Below are some ways to check:</span></span>

-   [<span data-ttu-id="885fa-338">檢查是否已將使用者指派給應用程式</span><span class="sxs-lookup"><span data-stu-id="885fa-338">Check if a user is assigned to the application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="885fa-339">如何將使用者直接指派給應用程式</span><span class="sxs-lookup"><span data-stu-id="885fa-339">How to assign a user to an application directly</span></span>](#how-to-assign-a-user-to-an-application-directly)

-   [<span data-ttu-id="885fa-340">檢查是否已為使用者指派應用程式相關的授權</span><span class="sxs-lookup"><span data-stu-id="885fa-340">Check if a user is assigned to a license related to the application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)

-   <span data-ttu-id="885fa-341">如何[將授權指派給 Azure AD 中的使用者](#how-to-assign-a-user-a-license)</span><span class="sxs-lookup"><span data-stu-id="885fa-341">[How to assign a license to a user](#how-to-assign-a-user-a-license)</span></span>

### <a name="check-if-a-user-is-assigned-to-the-application"></a><span data-ttu-id="885fa-342">檢查是否已將使用者指派給應用程式</span><span class="sxs-lookup"><span data-stu-id="885fa-342">Check if a user is assigned to the application</span></span>

<span data-ttu-id="885fa-343">若要檢查是否已將使用者指派給應用程式，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="885fa-343">To check if a user is assigned to the application, follow the steps below:</span></span>

1.  <span data-ttu-id="885fa-344">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="885fa-344">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="885fa-345">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-345">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="885fa-346">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="885fa-346">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="885fa-347">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-347">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="885fa-348">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="885fa-348">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="885fa-349">**搜尋**相關應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="885fa-349">**Search** for the name of the application in question.</span></span>

7.  <span data-ttu-id="885fa-350">按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-350">click **Users and groups**.</span></span>

8.  <span data-ttu-id="885fa-351">檢查是否已將使用者指派給應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-351">Check to see if your user is assigned to the application.</span></span>

   * <span data-ttu-id="885fa-352">如果沒有，請依照＜如何將使用者直接指派給應用程式＞中的步驟來執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="885fa-352">If not follow the steps in “How to assign a user to an application directly” to do so.</span></span>

### <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="885fa-353">如何將使用者直接指派給應用程式</span><span class="sxs-lookup"><span data-stu-id="885fa-353">How to assign a user to an application directly</span></span>

<span data-ttu-id="885fa-354">若要直接將一或多個使用者指派至應用程式，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="885fa-354">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="885fa-355">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="885fa-355">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="885fa-356">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-356">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="885fa-357">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="885fa-357">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="885fa-358">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-358">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="885fa-359">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="885fa-359">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="885fa-360">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-360">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="885fa-361">從清單中選取您想要指派使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-361">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="885fa-362">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-362">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="885fa-363">按一下 [使用者和群組] 清單頂端的 [新增] 按鈕，以開啟 [新增指派] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="885fa-363">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="885fa-364">從 [新增指派] 刀鋒視窗按一下 [使用者和群組] 選取器。</span><span class="sxs-lookup"><span data-stu-id="885fa-364">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="885fa-365">在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入您有興趣指派之使用者的**全名**或**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="885fa-365">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="885fa-366">將滑鼠停留在清單中的**使用者**上方，以顯示**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="885fa-366">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="885fa-367">按一下使用者設定檔照片或標誌旁邊的核取方塊，將使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="885fa-367">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="885fa-368">**選擇性︰**如果您想要**新增多位使用者**，請在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入另一個**全名**或**電子郵件地址**，然後按一下核取方塊，將此使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="885fa-368">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="885fa-369">當您完成選取使用者時，按一下 [選取] 按鈕，將他們新增到要指派至應用程式的使用者和群組清單。</span><span class="sxs-lookup"><span data-stu-id="885fa-369">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="885fa-370">**選擇性︰**按一下 [新增指派] 刀鋒視窗中的 [選取角色] 選取器，以選取要指派給您已選取使用者的角色。</span><span class="sxs-lookup"><span data-stu-id="885fa-370">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="885fa-371">按一下 [指派] 按鈕，將應用程式指派給選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="885fa-371">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="885fa-372">稍後片刻，您已選取的使用者便能在存取面板中啟動這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-372">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-to-the-application"></a><span data-ttu-id="885fa-373">檢查使用者是否已獲應用程式相關的授權</span><span class="sxs-lookup"><span data-stu-id="885fa-373">Check if a user is under a license related to the application</span></span>

<span data-ttu-id="885fa-374">若要檢查指派給使用者的授權，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="885fa-374">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="885fa-375">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="885fa-375">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="885fa-376">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-376">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="885fa-377">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="885fa-377">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="885fa-378">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-378">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="885fa-379">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="885fa-379">click **All users**.</span></span>

6.  <span data-ttu-id="885fa-380">**搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。</span><span class="sxs-lookup"><span data-stu-id="885fa-380">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="885fa-381">按一下 [授權]，以查看目前已指派給使用者的授權。</span><span class="sxs-lookup"><span data-stu-id="885fa-381">click **Licenses** to see which licenses the user currently has assigned.</span></span>

  * <span data-ttu-id="885fa-382">如果已為使用者指派 Office 授權，這會讓第一方 Office 應用程式出現在使用者的存取面板上。</span><span class="sxs-lookup"><span data-stu-id="885fa-382">If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.</span></span>

### <a name="how-to-assign-a-user-a-license"></a><span data-ttu-id="885fa-383">如何為使用者指派授權</span><span class="sxs-lookup"><span data-stu-id="885fa-383">How to assign a user a license</span></span> 

<span data-ttu-id="885fa-384">若要為使用者指派授權，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="885fa-384">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="885fa-385">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="885fa-385">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="885fa-386">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-386">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="885fa-387">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="885fa-387">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="885fa-388">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-388">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="885fa-389">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="885fa-389">click **All users**.</span></span>

6.  <span data-ttu-id="885fa-390">**搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。</span><span class="sxs-lookup"><span data-stu-id="885fa-390">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="885fa-391">按一下 [授權]，查看使用者目前已指派的授權。</span><span class="sxs-lookup"><span data-stu-id="885fa-391">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="885fa-392">按一下 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="885fa-392">click the **Assign** button.</span></span>

9.  <span data-ttu-id="885fa-393">從可用產品清單中選取**一或多個產品**。</span><span class="sxs-lookup"><span data-stu-id="885fa-393">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="885fa-394">(**選擇性**) 按一下 [指派選項] 項目，更細微地指派產品。</span><span class="sxs-lookup"><span data-stu-id="885fa-394">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="885fa-395">完成時按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="885fa-395">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="885fa-396">按一下 [指派] 按鈕，將這些授權指派給這位使用者。</span><span class="sxs-lookup"><span data-stu-id="885fa-396">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="problems-related-to-assigning-applications-to-groups"></a><span data-ttu-id="885fa-397">將應用程式指派給群組的相關問題</span><span class="sxs-lookup"><span data-stu-id="885fa-397">Problems related to assigning applications to groups</span></span>

<span data-ttu-id="885fa-398">使用者可能因為屬於已被指派應用程式的群組，所以能在存取面板上看見該應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-398">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span></span> <span data-ttu-id="885fa-399">以下是一些檢查方法：</span><span class="sxs-lookup"><span data-stu-id="885fa-399">Below are some ways to check:</span></span>

-   [<span data-ttu-id="885fa-400">檢查使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="885fa-400">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="885fa-401">如何將應用程式直接指派給群組</span><span class="sxs-lookup"><span data-stu-id="885fa-401">How to assign an application to a group directly</span></span>](#how-to-assign-an-application-to-a-group-directly)

-   [<span data-ttu-id="885fa-402">檢查使用者是否屬於指派給授權的群組</span><span class="sxs-lookup"><span data-stu-id="885fa-402">Check if a user is part of group assigned to a license</span></span>](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [<span data-ttu-id="885fa-403">如何將授權指派給群組</span><span class="sxs-lookup"><span data-stu-id="885fa-403">How to assign a license to a group</span></span>](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="885fa-404">檢查使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="885fa-404">Check a user’s group memberships</span></span>

<span data-ttu-id="885fa-405">若要檢查群組的成員資格，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="885fa-405">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="885fa-406">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="885fa-406">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="885fa-407">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-407">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="885fa-408">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="885fa-408">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="885fa-409">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-409">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="885fa-410">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="885fa-410">click **All users**.</span></span>

6.  <span data-ttu-id="885fa-411">**搜尋**您感興趣的使用者，然後**按一下資料列**加以選取。</span><span class="sxs-lookup"><span data-stu-id="885fa-411">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="885fa-412">按一下 [群組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-412">click **Groups**.</span></span>

8.  <span data-ttu-id="885fa-413">檢查使用者是否屬於已指派給應用程式的群組。</span><span class="sxs-lookup"><span data-stu-id="885fa-413">Check to see if your user is part of a Group assigned to the application.</span></span>

  * <span data-ttu-id="885fa-414">如果您想要從群組移除使用者，請**按一下群組的資料列**，然後選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="885fa-414">If you want to remove the user from the group, **click the row** of the group and select delete.</span></span>

### <a name="how-to-assign-an-application-to-a-group-directly"></a><span data-ttu-id="885fa-415">如何將應用程式直接指派給群組</span><span class="sxs-lookup"><span data-stu-id="885fa-415">How to assign an application to a group directly</span></span>

<span data-ttu-id="885fa-416">若要將一或多個群組直接指派給應用程式，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="885fa-416">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="885fa-417">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="885fa-417">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="885fa-418">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-418">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="885fa-419">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="885fa-419">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="885fa-420">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-420">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="885fa-421">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="885fa-421">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="885fa-422">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="885fa-422">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="885fa-423">從清單中選取您想要指派使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-423">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="885fa-424">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-424">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="885fa-425">按一下 [使用者和群組] 清單頂端的 [新增] 按鈕，以開啟 [新增指派] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="885fa-425">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="885fa-426">從 [新增指派] 刀鋒視窗按一下 [使用者和群組] 選取器。</span><span class="sxs-lookup"><span data-stu-id="885fa-426">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="885fa-427">在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入您有興趣指派之群組的**完整群組名稱**。</span><span class="sxs-lookup"><span data-stu-id="885fa-427">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="885fa-428">將滑鼠停留在清單中的**群組**上方，以顯示**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="885fa-428">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="885fa-429">按一下群組設定檔照片或標誌旁邊的核取方塊，將使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="885fa-429">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="885fa-430">**選擇性︰**如果您想要**新增多個群組**，請在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入另一個**完整群組名稱**，然後按一下核取方塊，將此群組新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="885fa-430">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="885fa-431">當您完成選取群組時，按一下 [選取] 按鈕，將它們新增到要指派給應用程式的使用者和群組清單。</span><span class="sxs-lookup"><span data-stu-id="885fa-431">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="885fa-432">**選擇性︰**按一下 [新增指派] 刀鋒視窗中的 [選取角色] 選取器，以選取要指派給您已選取群組的角色。</span><span class="sxs-lookup"><span data-stu-id="885fa-432">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="885fa-433">按一下 [指派] 按鈕，將應用程式指派給選取的群組。</span><span class="sxs-lookup"><span data-stu-id="885fa-433">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="885fa-434">稍後片刻，您已選取的使用者便能在存取面板中啟動這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="885fa-434">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

### <a name="check-if-a-user-is-part-of-group-assigned-to-a-license"></a><span data-ttu-id="885fa-435">檢查使用者是否屬於指派給授權的群組</span><span class="sxs-lookup"><span data-stu-id="885fa-435">Check if a user is part of group assigned to a license</span></span>

1.  <span data-ttu-id="885fa-436">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="885fa-436">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="885fa-437">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-437">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="885fa-438">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="885fa-438">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="885fa-439">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-439">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="885fa-440">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="885fa-440">click **All users**.</span></span>

6.  <span data-ttu-id="885fa-441">**搜尋**您感興趣的使用者，然後**按一下資料列**加以選取。</span><span class="sxs-lookup"><span data-stu-id="885fa-441">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="885fa-442">按一下 [群組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-442">click **Groups**.</span></span>

8.  <span data-ttu-id="885fa-443">按一下特定群組的資料列。</span><span class="sxs-lookup"><span data-stu-id="885fa-443">click the row of a specific group.</span></span>

9.  <span data-ttu-id="885fa-444">按一下 [授權]，以查看已指派給群組的授權。</span><span class="sxs-lookup"><span data-stu-id="885fa-444">click **Licenses** to see which licenses the group has assigned to it.</span></span>

   * <span data-ttu-id="885fa-445">如果已將群組指派給 Office 授權，這可能會讓某些第一方 Office 應用程式出現在使用者的存取面板上。</span><span class="sxs-lookup"><span data-stu-id="885fa-445">If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.</span></span>

### <a name="how-to-assign-a-license-to-a-group"></a><span data-ttu-id="885fa-446">如何將授權指派給群組</span><span class="sxs-lookup"><span data-stu-id="885fa-446">How to assign a license to a group</span></span>

<span data-ttu-id="885fa-447">若要將授權指派給群組，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="885fa-447">To assign a license to a group, follow the steps below:</span></span>

1.  <span data-ttu-id="885fa-448">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="885fa-448">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="885fa-449">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-449">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="885fa-450">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="885fa-450">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="885fa-451">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-451">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="885fa-452">按一下 [所有群組]。</span><span class="sxs-lookup"><span data-stu-id="885fa-452">click **All groups**.</span></span>

6.  <span data-ttu-id="885fa-453">**搜尋**您感興趣的群組，然後**按一下資料列**加以選取。</span><span class="sxs-lookup"><span data-stu-id="885fa-453">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="885fa-454">按一下 [授權]，以查看目前已指派至群組的授權。</span><span class="sxs-lookup"><span data-stu-id="885fa-454">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="885fa-455">按一下 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="885fa-455">click the **Assign** button.</span></span>

9.  <span data-ttu-id="885fa-456">從可用產品清單中選取**一或多個產品**。</span><span class="sxs-lookup"><span data-stu-id="885fa-456">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="885fa-457">(**選擇性**) 按一下 [指派選項] 項目，更細微地指派產品。</span><span class="sxs-lookup"><span data-stu-id="885fa-457">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="885fa-458">完成時按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="885fa-458">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="885fa-459">按一下 [指派] 按鈕，將這些授權指派至這個群組。</span><span class="sxs-lookup"><span data-stu-id="885fa-459">Click the **Assign** button to assign these licenses to this group.</span></span> <span data-ttu-id="885fa-460">根據群組的大小和複雜度，這可能需要很長的時間。</span><span class="sxs-lookup"><span data-stu-id="885fa-460">This may take a long time, depending on the size and complexity of the group.</span></span>

>[!NOTE]
><span data-ttu-id="885fa-461">若要更快速執行此作業，請考慮暫時將授權直接指派給使用者。</span><span class="sxs-lookup"><span data-stu-id="885fa-461">To do this faster, consider temporarily assigning a license to the user directly.</span></span> 
>
>

## <a name="next-steps"></a><span data-ttu-id="885fa-462">後續步驟</span><span class="sxs-lookup"><span data-stu-id="885fa-462">Next steps</span></span>
[<span data-ttu-id="885fa-463">將新的使用者加入 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="885fa-463">Add new users to Azure Active Directory</span></span>](active-directory-users-create-azure-portal.md)


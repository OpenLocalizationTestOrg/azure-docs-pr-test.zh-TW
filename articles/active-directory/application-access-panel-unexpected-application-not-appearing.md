---
title: "aaaAn 指派應用程式不會顯示在 hello 存取面板 |Microsoft 文件"
description: "應用程式並未出現在 hello 存取面板進行疑難排解"
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
ms.openlocfilehash: 089883f406267df4552c7fc991883f335ad49fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="an-assigned-application-is-not-appearing-on-hello-access-panel"></a><span data-ttu-id="bdbe3-103">指派的應用程式不會顯示 hello 存取面板上</span><span class="sxs-lookup"><span data-stu-id="bdbe3-103">An assigned application is not appearing on hello access panel</span></span>

<span data-ttu-id="bdbe3-104">hello 存取面板是網頁型的入口網站，可讓使用者使用工作或學校帳戶，Azure Active Directory (Azure AD) tooview 並啟動雲端架構應用程式中的 hello Azure AD 系統管理員已授與它們存取權。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="bdbe3-105">這些應用程式會代表 hello Azure AD 入口網站中的 hello 使用者設定。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="bdbe3-106">hello 應用程式必須正確設定並指派的 toohello 使用者或群組 hello 使用者是 toosee hello 存取面板中的 hello 應用程式的成員。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="bdbe3-107">應用程式的使用者會看見 hello 類型落在 hello 下列類別：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-107">hello type of apps a user may be seeing fall in hello following categories:</span></span>

-   <span data-ttu-id="bdbe3-108">Office 365 應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-108">Office 365 Applications</span></span>

-   <span data-ttu-id="bdbe3-109">已設定同盟 SSO 的 Microsoft 及第三方應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="bdbe3-110">密碼型 SSO 應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="bdbe3-111">含現有 SSO 解決方案的應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="bdbe3-112">一般會先發出 toocheck</span><span class="sxs-lookup"><span data-stu-id="bdbe3-112">General issues toocheck first</span></span>

-   <span data-ttu-id="bdbe3-113">如果應用程式剛加入 tooa 使用者，toosign 入和登出再試一次到 hello 使用者的存取面板後幾分鐘的時間 toosee 如果 hello 應用程式會加入。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-113">If an application was just added tooa user, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is added.</span></span>

-   <span data-ttu-id="bdbe3-114">授權就已從使用者或群組 hello 使用者隸屬這可能需要很長的時間，取決於 hello 大小和複雜度所做的變更 toobe hello 群組。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-114">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="bdbe3-115">允許額外的時間才能登入存取面板 hello。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-115">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooapplication-configuration"></a><span data-ttu-id="bdbe3-116">問題相關的 tooapplication 組態</span><span class="sxs-lookup"><span data-stu-id="bdbe3-116">Problems related tooapplication configuration</span></span>

<span data-ttu-id="bdbe3-117">應用程式未出現在使用者的存取面板上可能是因為並未正確設定。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-117">An application may not be appearing in a user’s Access Panel because it is not configured properly.</span></span> <span data-ttu-id="bdbe3-118">下面是的一些您可以疑難排解問題相關的 tooapplication 組態：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-118">Below are some ways you can troubleshoot issues related tooapplication configuration:</span></span>

-   [<span data-ttu-id="bdbe3-119">如何 tooconfigure 同盟單一登入 Azure AD 圖庫應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-119">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [<span data-ttu-id="bdbe3-120">如何 tooconfigure 同盟單一登入非組件庫的應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-120">How tooconfigure federated single sign-on for a non-gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="bdbe3-121">如何 tooconfigure 密碼單一登入應用程式的 Azure AD 圖庫應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-121">How tooconfigure a password single sign-on application for an Azure AD gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="bdbe3-122">如何 tooconfigure 密碼單一登入應用程式的非組件庫的應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-122">How tooconfigure a password single sign-on application for a non-gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="bdbe3-123">如何 tooconfigure 同盟單一登入 Azure AD 圖庫應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-123">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="bdbe3-124">啟用具備企業單一登入功能的 hello Azure AD 資源庫中的所有應用程式有可用的逐步教學課程。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-124">All applications in hello Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="bdbe3-125">您可以存取 hello[如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/)如需詳細資料的逐步指引。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-125">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="bdbe3-126">您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-126">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="bdbe3-127">從 hello Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-127">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="bdbe3-128">設定 Azure AD （登入 URL，識別項，回覆 URL） 中的 hello 應用程式的中繼資料值</span><span class="sxs-lookup"><span data-stu-id="bdbe3-128">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="bdbe3-129">選取使用者的識別項並新增使用者屬性傳送 toobe toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-129">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="bdbe3-130">擷取 Azure AD 中繼資料與憑證</span><span class="sxs-lookup"><span data-stu-id="bdbe3-130">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="bdbe3-131">在 hello 應用程式 （登入 URL、 簽發者、 登出 URL 和憑證） 中設定 Azure AD 中繼資料值</span><span class="sxs-lookup"><span data-stu-id="bdbe3-131">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="bdbe3-132">從 hello Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-132">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="bdbe3-133">tooadd hello Azure AD 資源庫，從應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-133">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="bdbe3-134">開啟 hello [Azure 入口網站](https://portal.azure.com)身分登入和**全域管理員**或**共同管理員**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-134">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="bdbe3-135">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-135">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bdbe3-136">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-136">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bdbe3-137">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-137">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bdbe3-138">按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-138">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="bdbe3-139">在 hello**輸入的名稱**文字方塊中，從 hello**從 hello 圖庫新增**> 一節中，輸入 hello 名稱 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-139">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="bdbe3-140">選取要用於單一登入 tooconfigure hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-140">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="bdbe3-141">然後再加入 hello 應用程式，您可以變更其名稱從 hello**名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-141">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="bdbe3-142">按一下**新增**按鈕，tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-142">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="bdbe3-143">短時間，就能 toosee hello 應用程式的組態刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-143">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="bdbe3-144">設定單一登入應用程式從 hello Azure AD 資源庫</span><span class="sxs-lookup"><span data-stu-id="bdbe3-144">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="bdbe3-145">tooconfigure 單一登入的應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-145">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="bdbe3-146">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-146">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="bdbe3-147">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-147">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bdbe3-148">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-148">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bdbe3-149">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-149">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bdbe3-150">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-150">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="bdbe3-151">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-151">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="bdbe3-152">選取您想 tooconfigure 單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-152">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="bdbe3-153">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-153">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="bdbe3-154">選取**SAML 型登入**從 hello**模式**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-154">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="bdbe3-155">輸入中的所需的 hello 值**網域和 Url。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-155">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="bdbe3-156">您應該從 hello 應用程式廠商，以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-156">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="bdbe3-157">tooconfigure hello 應用程式做為 SP 起始的 SSO hello 登入 URL 是必要的值。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-157">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="bdbe3-158">有些應用程式識別碼 hello 也是必要的值。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-158">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="bdbe3-159">tooconfigure hello 應用程式做為 IdP 初始化的 SSO，hello 回覆 URL 是必要的值。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-159">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="bdbe3-160">有些應用程式識別碼 hello 也是必要的值。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-160">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="bdbe3-161">**選擇性：**按一下**顯示進階的 URL 設定**您希望 toosee hello 非必要的值。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-161">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="bdbe3-162">在 hello**使用者屬性**，選取 hello hello 中使用者的唯一識別碼**使用者識別碼**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-162">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="bdbe3-163">**選擇性：**按一下**檢視和編輯所有其他使用者屬性**tooedit hello 屬性 hello SAML 權杖中傳送的 toobe toohello 應用程式，當使用者登入。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-163">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="bdbe3-164">tooadd 屬性：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-164">tooadd an attribute:</span></span>

   1. <span data-ttu-id="bdbe3-165">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-165">click **Add attribute**.</span></span> <span data-ttu-id="bdbe3-166">輸入 hello**名稱**和 hello 選取 hello**值**從 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-166">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="bdbe3-167">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-167">click **Save.**</span></span> <span data-ttu-id="bdbe3-168">您會看到 hello hello 資料表中的新屬性。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-168">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="bdbe3-169">按一下**設定&lt;應用程式名稱&gt;** tooaccess 文件中的有關 tooconfigure 單一登入 hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-169">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="bdbe3-170">此外，您有 hello 中繼資料 Url 和與 hello 應用程式所需的憑證 toosetup SSO。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-170">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="bdbe3-171">按一下**儲存**toosave hello 組態。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-171">click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="bdbe3-172">將使用者指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-172">Assign users toohello application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="bdbe3-173">選取使用者的識別項並新增使用者屬性傳送 toobe toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-173">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="bdbe3-174">tooselect hello 使用者識別碼或新增使用者屬性，請遵循下列的 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-174">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="bdbe3-175">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-175">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="bdbe3-176">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-176">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bdbe3-177">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-177">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bdbe3-178">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-178">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bdbe3-179">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-179">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="bdbe3-180">如果看不到您想 tooshow 這裡的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-180">If you do not see hello application you want tooshow up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="bdbe3-181">選取您已設定單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-181">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="bdbe3-182">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-182">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="bdbe3-183">在 hello**使用者屬性**區段中，選取 hello hello 中使用者的唯一識別碼**使用者識別碼**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-183">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="bdbe3-184">hello 選取的選項必須在 hello 應用程式 tooauthenticate hello 使用者 toomatch hello 預期的值。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-184">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="bdbe3-185">Hello NameID 屬性 （使用者識別碼） 的 azure AD 選取 hello 格式會根據選取的 hello 值或 hello hello hello SAML AuthRequest 中的應用程式所要求的格式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-185">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="bdbe3-186">如需詳細資訊，請造訪 hello 文章[單一登入的 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)hello 下一節 NameIDPolicy。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-186">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="bdbe3-187">tooadd 使用者屬性，按一下**檢視和編輯所有其他使用者屬性**tooedit hello 屬性 hello SAML 權杖中傳送的 toobe toohello 應用程式，當使用者登入。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-187">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="bdbe3-188">tooadd 屬性：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-188">tooadd an attribute:</span></span>

   1. <span data-ttu-id="bdbe3-189">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-189">click **Add attribute**.</span></span> <span data-ttu-id="bdbe3-190">輸入 hello**名稱**和 hello 選取 hello**值**從 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-190">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="bdbe3-191">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-191">click **Save.**</span></span> <span data-ttu-id="bdbe3-192">您會看見 hello hello 資料表中的新屬性。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-192">You will see hello new attribute in hello table.</span></span>

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="bdbe3-193">下載 hello Azure AD 中繼資料或憑證</span><span class="sxs-lookup"><span data-stu-id="bdbe3-193">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="bdbe3-194">toodownload hello 應用程式中繼資料或憑證從 Azure AD，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-194">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="bdbe3-195">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-195">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="bdbe3-196">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-196">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bdbe3-197">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-197">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bdbe3-198">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-198">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bdbe3-199">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-199">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="bdbe3-200">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-200">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="bdbe3-201">選取您已設定單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-201">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="bdbe3-202">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-202">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="bdbe3-203">跳過**SAML 簽章憑證**區段，然後按一下 **下載**資料行值。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-203">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="bdbe3-204">根據哪些 hello 應用程式需要設定單一登入，您會看到其中一個 hello 選項 toodownload hello 中繼資料 XML 或 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-204">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="bdbe3-205">Azure AD 不會提供 URL tooget hello 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-205">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="bdbe3-206">hello 中繼資料，才能擷取為 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-206">hello metadata can only be retrieved as a XML file.</span></span>

### <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="bdbe3-207">如何 tooconfigure 同盟單一登入非組件庫的應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-207">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="bdbe3-208">tooconfigure 非組件庫的應用程式，您必須具備 toohave Azure AD premium 與 hello 應用程式支援 SAML 2.0。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-208">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="bdbe3-209">如需有關 Azure AD 版本的詳細資訊，請參閱 [Azure AD 定價](https://azure.microsoft.com/pricing/details/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-209">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="bdbe3-210">設定 Azure AD （登入 URL，識別項，回覆 URL） 中的 hello 應用程式的中繼資料值</span><span class="sxs-lookup"><span data-stu-id="bdbe3-210">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="bdbe3-211">選取使用者的識別項並新增使用者屬性傳送 toobe toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-211">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="bdbe3-212">擷取 Azure AD 中繼資料與憑證</span><span class="sxs-lookup"><span data-stu-id="bdbe3-212">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="bdbe3-213">在 hello 應用程式 （登入 URL、 簽發者、 登出 URL 和憑證） 中設定 Azure AD 中繼資料值</span><span class="sxs-lookup"><span data-stu-id="bdbe3-213">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

#### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="bdbe3-214">設定 Azure AD （登入 URL，識別項，回覆 URL） 中的 hello 應用程式的中繼資料值</span><span class="sxs-lookup"><span data-stu-id="bdbe3-214">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="bdbe3-215">tooconfigure 單一登入的應用程式不在 hello Azure AD 資源庫，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-215">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="bdbe3-216">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-216">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="bdbe3-217">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-217">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bdbe3-218">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-218">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bdbe3-219">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-219">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bdbe3-220">按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-220">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="bdbe3-221">按一下**非組件庫的應用程式**在 hello**新增您自己的應用程式**> 一節。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-221">click **Non-gallery application** in hello **Add your own app** section.</span></span>

7.  <span data-ttu-id="bdbe3-222">輸入 hello hello 應用程式名稱在 hello**名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-222">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="bdbe3-223">按一下**新增**按鈕，tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-223">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="bdbe3-224">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-224">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="bdbe3-225">選取**SAML 型登入**在 hello**模式**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-225">Select **SAML-based Sign-on** in hello **Mode** dropdown.</span></span>

11. <span data-ttu-id="bdbe3-226">輸入中的所需的 hello 值**網域和 Url。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-226">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="bdbe3-227">您應該從 hello 應用程式廠商，以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-227">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="bdbe3-228">tooconfigure hello IdP 初始化的 SSO 應用程式輸入 hello 回覆 URL 和識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-228">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

   2.  <span data-ttu-id="bdbe3-229">**選擇性：** tooconfigure hello 應用程式做為 SP 起始的 SSO hello 登入 URL 是必要的值。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-229">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="bdbe3-230">在 hello**使用者屬性**，選取 hello hello 中使用者的唯一識別碼**使用者識別碼**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-230">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="bdbe3-231">**選擇性：**按一下**檢視和編輯所有其他使用者屬性**tooedit hello 屬性 hello SAML 權杖中傳送的 toobe toohello 應用程式，當使用者登入。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-231">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="bdbe3-232">tooadd 屬性：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-232">tooadd an attribute:</span></span>

   1. <span data-ttu-id="bdbe3-233">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-233">click **Add attribute**.</span></span> <span data-ttu-id="bdbe3-234">輸入 hello**名稱**和 hello 選取 hello**值**從 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-234">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="bdbe3-235">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-235">Click **Save.**</span></span> <span data-ttu-id="bdbe3-236">您會看到 hello hello 資料表中的新屬性。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-236">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="bdbe3-237">按一下**設定&lt;應用程式名稱&gt;** tooaccess 文件中的有關 tooconfigure 單一登入 hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-237">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="bdbe3-238">此外，您有 Azure AD Url 和 hello 應用程式所需的憑證。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-238">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="bdbe3-239">選取使用者的識別項並新增使用者屬性傳送 toobe toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-239">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="bdbe3-240">tooselect hello 使用者識別碼或新增使用者屬性，請遵循下列的 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-240">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="bdbe3-241">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-241">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="bdbe3-242">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-242">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bdbe3-243">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-243">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bdbe3-244">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-244">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bdbe3-245">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-245">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="bdbe3-246">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-246">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="bdbe3-247">選取您已設定單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-247">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="bdbe3-248">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-248">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="bdbe3-249">在 hello**使用者屬性**區段中，選取 hello hello 中使用者的唯一識別碼**使用者識別碼**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-249">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="bdbe3-250">hello 選取的選項必須在 hello 應用程式 tooauthenticate hello 使用者 toomatch hello 預期的值。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-250">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="bdbe3-251">Hello NameID 屬性 （使用者識別碼） 的 azure AD 選取 hello 格式會根據選取的 hello 值或 hello hello hello SAML AuthRequest 中的應用程式所要求的格式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-251">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="bdbe3-252">如需詳細資訊，請造訪 hello 文章[單一登入的 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)hello 下一節 NameIDPolicy。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-252">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="bdbe3-253">tooadd 使用者屬性，按一下**檢視和編輯所有其他使用者屬性**tooedit hello 屬性 hello SAML 權杖中傳送的 toobe toohello 應用程式，當使用者登入。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-253">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="bdbe3-254">tooadd 屬性：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-254">tooadd an attribute:</span></span>

   1. <span data-ttu-id="bdbe3-255">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-255">click **Add attribute**.</span></span> <span data-ttu-id="bdbe3-256">輸入 hello**名稱**和 hello 選取 hello**值**從 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-256">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="bdbe3-257">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-257">Click **Save.**</span></span> <span data-ttu-id="bdbe3-258">您會看到 hello hello 資料表中的新屬性。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-258">You see hello new attribute in hello table.</span></span>

#### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="bdbe3-259">下載 hello Azure AD 中繼資料或憑證</span><span class="sxs-lookup"><span data-stu-id="bdbe3-259">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="bdbe3-260">toodownload hello 應用程式中繼資料或憑證從 Azure AD，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-260">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="bdbe3-261">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-261">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="bdbe3-262">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-262">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bdbe3-263">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-263">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bdbe3-264">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-264">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bdbe3-265">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-265">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="bdbe3-266">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-266">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="bdbe3-267">選取您已設定單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-267">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="bdbe3-268">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-268">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="bdbe3-269">跳過**SAML 簽章憑證**區段，然後按一下 **下載**資料行值。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-269">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="bdbe3-270">根據哪些 hello 應用程式需要設定單一登入，您會看到其中一個 hello 選項 toodownload hello 中繼資料 XML 或 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-270">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="bdbe3-271">Azure AD 不會提供 URL tooget hello 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-271">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="bdbe3-272">hello 中繼資料，才能擷取為 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-272">hello metadata can only be retrieved as a XML file.</span></span>

### <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="bdbe3-273">如何 tooconfigure 密碼單一登入 Azure AD 圖庫應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-273">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="bdbe3-274">您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-274">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="bdbe3-275">從 hello Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-275">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="bdbe3-276">設定密碼單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-276">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="bdbe3-277">從 hello Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-277">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="bdbe3-278">tooadd hello Azure AD 資源庫，從應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-278">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="bdbe3-279">開啟 hello [Azure 入口網站](https://portal.azure.com)身分登入和**全域管理員**或**共同管理員**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-279">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="bdbe3-280">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-280">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bdbe3-281">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-281">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bdbe3-282">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-282">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bdbe3-283">按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-283">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="bdbe3-284">在 hello**輸入的名稱**文字方塊中，從 hello**從 hello 圖庫新增**> 一節中，輸入 hello 名稱 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-284">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="bdbe3-285">選取要用於單一登入 tooconfigure hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-285">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="bdbe3-286">然後再加入 hello 應用程式，您可以變更其名稱從 hello**名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-286">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="bdbe3-287">按一下**新增**按鈕，tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-287">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="bdbe3-288">短時間，就能 toosee hello 應用程式的組態刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-288">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="bdbe3-289">設定密碼單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-289">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="bdbe3-290">tooconfigure 單一登入的應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-290">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="bdbe3-291">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-291">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="bdbe3-292">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-292">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bdbe3-293">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-293">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bdbe3-294">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-294">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bdbe3-295">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-295">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="bdbe3-296">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-296">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="bdbe3-297">選取您想 tooconfigure 單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-297">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="bdbe3-298">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-298">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="bdbe3-299">選取 hello 模式**密碼式登入。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-299">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="bdbe3-300">[將使用者指派 toohello 應用程式](#how-to-assign-a-user-to-an-application-directly)。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-300">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="bdbe3-301">此外，您也可以提供代表 hello 使用者認證選取 hello 的 hello 使用者的資料列，並按一下**更新認證**並代表 hello 使用者輸入 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-301">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="bdbe3-302">否則，使用者在提示的 tooenter hello 認證本身在啟動。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-302">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="bdbe3-303">如何 tooconfigure 密碼單一登入非組件庫的應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-303">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="bdbe3-304">您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-304">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="bdbe3-305">新增不在資源庫內的應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-305">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="bdbe3-306">設定密碼單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-306">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a><span data-ttu-id="bdbe3-307">新增不在資源庫內的應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-307">Add a non-gallery application</span></span>

<span data-ttu-id="bdbe3-308">tooadd hello Azure AD 資源庫，從應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-308">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="bdbe3-309">開啟 hello [Azure 入口網站](https://portal.azure.com)身分登入和**全域管理員**或**共同管理員**。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-309">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="bdbe3-310">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-310">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bdbe3-311">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-311">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bdbe3-312">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-312">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bdbe3-313">按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-313">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="bdbe3-314">按一下 [不在資源庫內的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-314">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="bdbe3-315">輸入 hello 應用程式的名稱在 hello**名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-315">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="bdbe3-316">選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-316">Select **Add.**</span></span>

<span data-ttu-id="bdbe3-317">短時間，就能 toosee hello 應用程式的組態刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-317">After a short period, you be able toosee hello application’s configuration blade.</span></span>

#### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="bdbe3-318">設定密碼單一登入的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-318">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="bdbe3-319">tooconfigure 單一登入的應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-319">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="bdbe3-320">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-320">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="bdbe3-321">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-321">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bdbe3-322">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-322">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bdbe3-323">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-323">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bdbe3-324">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-324">click **All Applications** tooview a list of all your applications.</span></span>

    1.  <span data-ttu-id="bdbe3-325">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-325">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="bdbe3-326">選取您想 tooconfigure 單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-326">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="bdbe3-327">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-327">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="bdbe3-328">選取 hello 模式**密碼式登入。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-328">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="bdbe3-329">輸入 hello**登入 URL**。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-329">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="bdbe3-330">這是讓使用者輸入其使用者名稱和密碼 toosign 中的以 hello URL。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-330">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="bdbe3-331">請確定 hello 登入欄位會顯示在 hello URL。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-331">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="bdbe3-332">[將使用者指派 toohello 應用程式](#how-to-assign-a-user-to-an-application-directly)。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-332">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

11. <span data-ttu-id="bdbe3-333">此外，您也可以提供代表 hello 使用者認證選取 hello 的 hello 使用者的資料列，並按一下**更新認證**並代表 hello 使用者輸入 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-333">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="bdbe3-334">否則，使用者在提示的 tooenter hello 認證本身在啟動。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-334">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="bdbe3-335">問題相關的 tooassigning 應用程式 toousers</span><span class="sxs-lookup"><span data-stu-id="bdbe3-335">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="bdbe3-336">使用者可能不只可看見應用程式存取面板上因為它們不會指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-336">A user may not be seeing an application on their Access Panel because they are not assigned toohello application.</span></span> <span data-ttu-id="bdbe3-337">以下是一些方式 toocheck:</span><span class="sxs-lookup"><span data-stu-id="bdbe3-337">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="bdbe3-338">檢查 toohello 應用程式時，是否要指派使用者</span><span class="sxs-lookup"><span data-stu-id="bdbe3-338">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="bdbe3-339">如何 tooassign 使用者 tooan 應用程式直接</span><span class="sxs-lookup"><span data-stu-id="bdbe3-339">How tooassign a user tooan application directly</span></span>](#how-to-assign-a-user-to-an-application-directly)

-   [<span data-ttu-id="bdbe3-340">如果 tooa 授權指派給使用者的核取相關 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-340">Check if a user is assigned tooa license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [<span data-ttu-id="bdbe3-341">如何 tooassign 授權 tooa 使用者</span><span class="sxs-lookup"><span data-stu-id="bdbe3-341">How tooassign a license tooa user</span></span>](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="bdbe3-342">檢查 toohello 應用程式時，是否要指派使用者</span><span class="sxs-lookup"><span data-stu-id="bdbe3-342">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="bdbe3-343">toocheck 如果使用者被指派 toohello 應用程式，請遵循 hello 執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-343">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="bdbe3-344">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-344">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bdbe3-345">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-345">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bdbe3-346">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-346">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bdbe3-347">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-347">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bdbe3-348">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-348">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="bdbe3-349">**搜尋**hello hello 有問題的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-349">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="bdbe3-350">按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-350">click **Users and groups**.</span></span>

8.  <span data-ttu-id="bdbe3-351">如果您的使用者被指派 toohello 應用程式，請檢查 toosee。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-351">Check toosee if your user is assigned toohello application.</span></span>

   * <span data-ttu-id="bdbe3-352">如果沒有依照中的 hello 步驟 「 如何 tooassign 使用者 tooan 應用程式直接"toodo 讓。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-352">If not follow hello steps in “How tooassign a user tooan application directly” toodo so.</span></span>

### <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="bdbe3-353">如何 tooassign 使用者 tooan 應用程式直接</span><span class="sxs-lookup"><span data-stu-id="bdbe3-353">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="bdbe3-354">tooassign 一或多個使用者 tooan 應用程式直接管理，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-354">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="bdbe3-355">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-355">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="bdbe3-356">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-356">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bdbe3-357">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-357">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bdbe3-358">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-358">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bdbe3-359">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-359">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="bdbe3-360">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-360">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="bdbe3-361">選取您想要使用者 toofrom hello 清單 tooassign hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-361">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="bdbe3-362">一旦 hello 應用程式載入時，按一下 **使用者和群組**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-362">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="bdbe3-363">按一下 hello**新增**hello 頂端的按鈕**使用者和群組**清單 tooopen hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-363">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="bdbe3-364">按一下 hello**使用者和群組**選取器從 hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-364">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="bdbe3-365">Hello 中的型別**全名**或**電子郵件地址**hello 使用者您感興趣指派到 hello 的**依名稱或電子郵件地址搜尋**搜尋 方塊。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-365">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="bdbe3-366">將滑鼠停留在 hello**使用者**在 hello 清單 tooreveal**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-366">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="bdbe3-367">按一下 [hello] 核取方塊下一步 toohello 使用者的設定檔的相片或標誌 tooadd 使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-367">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="bdbe3-368">**選擇性：**如果您希望太**新增多個使用者**，在另一個類型**全名**或**電子郵件地址**到 hello**依名稱搜尋電子郵件地址或**搜尋 方塊中，然後按一下 hello 核取方塊 tooadd 這個使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-368">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="bdbe3-369">當您完成選取的使用者，請按一下 hello**選取**按鈕 tooadd 它們的使用者和群組 toobe toohello 清單指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-369">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="bdbe3-370">**選擇性：**按一下 hello**選取角色**hello 中的選取器**將作業加入**刀鋒視窗 tooselect 角色 tooassign toohello 使用者已選取。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-370">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="bdbe3-371">按一下 hello**指派**按鈕 tooassign hello 應用程式 toohello 選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-371">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="bdbe3-372">在短時間，您已選取的 hello 使用者會無法 toolaunch 中的這些應用程式之後 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-372">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="bdbe3-373">檢查是否授權使用者相關 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="bdbe3-373">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="bdbe3-374">toocheck 使用者的指派授權，後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-374">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="bdbe3-375">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-375">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bdbe3-376">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-376">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bdbe3-377">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-377">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bdbe3-378">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-378">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bdbe3-379">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-379">click **All users**.</span></span>

6.  <span data-ttu-id="bdbe3-380">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-380">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="bdbe3-381">按一下**授權**toosee 授權 hello 使用者目前已指派。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-381">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

  * <span data-ttu-id="bdbe3-382">如果這啟用第一個合作對象 Office 應用程式 tooappear tooan Office 授權指派給 hello 使用者 hello 使用者的存取面板。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-382">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

### <a name="how-tooassign-a-user-a-license"></a><span data-ttu-id="bdbe3-383">如何 tooassign 使用者授權</span><span class="sxs-lookup"><span data-stu-id="bdbe3-383">How tooassign a user a license</span></span> 

<span data-ttu-id="bdbe3-384">tooassign 授權 tooa 使用者，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-384">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="bdbe3-385">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-385">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bdbe3-386">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-386">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bdbe3-387">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-387">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bdbe3-388">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-388">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bdbe3-389">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-389">click **All users**.</span></span>

6.  <span data-ttu-id="bdbe3-390">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-390">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="bdbe3-391">按一下**授權**toosee 授權 hello 使用者目前已指派。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-391">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="bdbe3-392">按一下 hello**指派** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-392">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="bdbe3-393">選取**一或多個產品**hello 清單中的可用產品。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-393">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="bdbe3-394">**選擇性**按一下 hello**指派選項**項目 toogranularly 指派產品。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-394">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="bdbe3-395">完成時按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-395">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="bdbe3-396">按一下 hello**指派**按鈕 tooassign 這些授權 toothis 使用者。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-396">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="bdbe3-397">問題相關的 tooassigning 應用程式 toogroups</span><span class="sxs-lookup"><span data-stu-id="bdbe3-397">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="bdbe3-398">使用者會看見應用程式存取面板上因為它們已被指派 hello 應用程式群組的一部分。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-398">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="bdbe3-399">以下是一些方式 toocheck:</span><span class="sxs-lookup"><span data-stu-id="bdbe3-399">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="bdbe3-400">檢查使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="bdbe3-400">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="bdbe3-401">如何 tooassign 應用程式 tooa 群組直接</span><span class="sxs-lookup"><span data-stu-id="bdbe3-401">How tooassign an application tooa group directly</span></span>](#how-to-assign-an-application-to-a-group-directly)

-   [<span data-ttu-id="bdbe3-402">檢查使用者是否屬於 tooa 授權指派給群組</span><span class="sxs-lookup"><span data-stu-id="bdbe3-402">Check if a user is part of group assigned tooa license</span></span>](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [<span data-ttu-id="bdbe3-403">如何 tooassign 授權 tooa 群組</span><span class="sxs-lookup"><span data-stu-id="bdbe3-403">How tooassign a license tooa group</span></span>](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="bdbe3-404">檢查使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="bdbe3-404">Check a user’s group memberships</span></span>

<span data-ttu-id="bdbe3-405">toocheck 群組的成員資格，後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-405">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="bdbe3-406">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-406">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bdbe3-407">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-407">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bdbe3-408">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-408">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bdbe3-409">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-409">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bdbe3-410">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-410">click **All users**.</span></span>

6.  <span data-ttu-id="bdbe3-411">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-411">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="bdbe3-412">按一下 [群組]。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-412">click **Groups**.</span></span>

8.  <span data-ttu-id="bdbe3-413">如果您的使用者屬於群組的核取 toosee 指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-413">Check toosee if your user is part of a Group assigned toohello application.</span></span>

  * <span data-ttu-id="bdbe3-414">如果您想從 hello 群組 tooremove hello 使用者**按一下 hello 列**hello 群組和選取的刪除。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-414">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="how-tooassign-an-application-tooa-group-directly"></a><span data-ttu-id="bdbe3-415">如何 tooassign 應用程式 tooa 群組直接</span><span class="sxs-lookup"><span data-stu-id="bdbe3-415">How tooassign an application tooa group directly</span></span>

<span data-ttu-id="bdbe3-416">tooassign 一或多個群組 tooan 的應用程式直接管理，後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-416">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="bdbe3-417">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-417">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="bdbe3-418">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-418">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bdbe3-419">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-419">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bdbe3-420">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-420">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="bdbe3-421">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-421">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="bdbe3-422">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-422">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="bdbe3-423">選取您想要使用者 toofrom hello 清單 tooassign hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-423">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="bdbe3-424">一旦 hello 應用程式載入時，按一下 **使用者和群組**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-424">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="bdbe3-425">按一下 hello**新增**hello 頂端的按鈕**使用者和群組**清單 tooopen hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-425">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="bdbe3-426">按一下 hello**使用者和群組**選取器從 hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-426">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="bdbe3-427">型別在 hello**完整的群組名稱**您感興趣指派到 hello hello 群組的**依名稱或電子郵件地址搜尋**搜尋 方塊。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-427">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="bdbe3-428">將滑鼠停留在 hello**群組**在 hello 清單 tooreveal**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-428">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="bdbe3-429">按一下 [hello] 核取方塊下一步 toohello 群組的設定檔的相片或標誌 tooadd 使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-429">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="bdbe3-430">**選擇性：**如果您希望太**新增多個群組**，在另一個類型**完整的群組名稱**到 hello**依名稱或電子郵件地址搜尋**搜尋方塊中，按一下此群組 toohello hello 核取方塊 tooadd**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-430">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="bdbe3-431">當您完成選取群組，請按一下 hello**選取**按鈕 tooadd 它們的使用者和群組 toobe toohello 清單指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-431">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="bdbe3-432">**選擇性：**按一下 hello**選取角色**hello 中的選取器**將作業加入**刀鋒視窗 tooselect 角色 tooassign toohello 群組您已選取。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-432">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="bdbe3-433">按一下 hello**指派**按鈕 tooassign hello 應用程式 toohello 選取的群組。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-433">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="bdbe3-434">在短時間，您已選取的 hello 使用者會無法 toolaunch 中的這些應用程式之後 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-434">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

### <a name="check-if-a-user-is-part-of-group-assigned-tooa-license"></a><span data-ttu-id="bdbe3-435">檢查使用者是否屬於 tooa 授權指派給群組</span><span class="sxs-lookup"><span data-stu-id="bdbe3-435">Check if a user is part of group assigned tooa license</span></span>

1.  <span data-ttu-id="bdbe3-436">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-436">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bdbe3-437">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-437">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bdbe3-438">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-438">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bdbe3-439">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-439">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bdbe3-440">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-440">click **All users**.</span></span>

6.  <span data-ttu-id="bdbe3-441">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-441">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="bdbe3-442">按一下 [群組]。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-442">click **Groups**.</span></span>

8.  <span data-ttu-id="bdbe3-443">按一下 特定群組的 hello 資料列。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-443">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="bdbe3-444">按一下**授權**toosee 授權 hello 群組已指派 tooit。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-444">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

   * <span data-ttu-id="bdbe3-445">如果這可能會讓特定的第一個合作對象 Office 應用程式 tooappear tooan Office 授權指派給 hello 群組 hello 使用者的存取面板。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-445">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>

### <a name="how-tooassign-a-license-tooa-group"></a><span data-ttu-id="bdbe3-446">如何 tooassign 授權 tooa 群組</span><span class="sxs-lookup"><span data-stu-id="bdbe3-446">How tooassign a license tooa group</span></span>

<span data-ttu-id="bdbe3-447">tooassign 授權 tooa 群組，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="bdbe3-447">tooassign a license tooa group, follow hello steps below:</span></span>

1.  <span data-ttu-id="bdbe3-448">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="bdbe3-448">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="bdbe3-449">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-449">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="bdbe3-450">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-450">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="bdbe3-451">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-451">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="bdbe3-452">按一下 [所有群組]。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-452">click **All groups**.</span></span>

6.  <span data-ttu-id="bdbe3-453">**搜尋**hello 您感興趣的群組和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-453">**Search** for hello group you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="bdbe3-454">按一下**授權**toosee 授權 hello 群組目前已指派。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-454">click **Licenses** toosee which licenses hello group currently has assigned.</span></span>

8.  <span data-ttu-id="bdbe3-455">按一下 hello**指派** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-455">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="bdbe3-456">選取**一或多個產品**hello 清單中的可用產品。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-456">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="bdbe3-457">**選擇性**按一下 hello**指派選項**項目 toogranularly 指派產品。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-457">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="bdbe3-458">完成時按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-458">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="bdbe3-459">按一下 hello**指派**按鈕 tooassign 這些授權 toothis 群組。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-459">Click hello **Assign** button tooassign these licenses toothis group.</span></span> <span data-ttu-id="bdbe3-460">這可能需要很長的時間，取決於 hello 大小和複雜度 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-460">This may take a long time, depending on hello size and complexity of hello group.</span></span>

>[!NOTE]
><span data-ttu-id="bdbe3-461">toodo 這速度更快，請考慮暫時直接指派授權 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="bdbe3-461">toodo this faster, consider temporarily assigning a license toohello user directly.</span></span> 
>
>

## <a name="next-steps"></a><span data-ttu-id="bdbe3-462">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bdbe3-462">Next steps</span></span>
[<span data-ttu-id="bdbe3-463">加入新使用者 tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bdbe3-463">Add new users tooAzure Active Directory</span></span>](active-directory-users-create-azure-portal.md)


---
title: "aaaHow tooconfigure 同盟單一登入非組件庫的應用程式 |Microsoft 文件"
description: "如何 tooconfigure 同盟單一登入您想使用 Azure AD toointegrate 自訂非組件庫應用程式"
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
ms.openlocfilehash: f4a37cb500c075d0ce917ad8f13411f2ce208c56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="70fcb-103">如何 tooconfigure 同盟單一登入非組件庫的應用程式</span><span class="sxs-lookup"><span data-stu-id="70fcb-103">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="70fcb-104">tooconfigure 非組件庫的應用程式，您必須具備 toohave Azure AD premium 與 hello 應用程式支援 SAML 2.0。</span><span class="sxs-lookup"><span data-stu-id="70fcb-104">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="70fcb-105">如需有關 Azure AD 版本的詳細資訊，請參閱 [Azure AD 定價](https://azure.microsoft.com/pricing/details/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="70fcb-105">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="70fcb-106">所需步驟的概觀</span><span class="sxs-lookup"><span data-stu-id="70fcb-106">Overview of steps required</span></span>
<span data-ttu-id="70fcb-107">以下是 hello 步驟需要的 tooconfigure 同盟單一登入非圖庫的高層級概觀 (例如，自訂) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="70fcb-107">Below is a high level overview of hello steps required tooconfigure federated single sign-on for a non-gallery (e.g., custom) application.</span></span>

-   [<span data-ttu-id="70fcb-108">設定 Azure AD （登入 URL，識別項，回覆 URL） 中的 hello 應用程式的中繼資料值</span><span class="sxs-lookup"><span data-stu-id="70fcb-108">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="70fcb-109">選取使用者的識別項並新增使用者屬性傳送 toobe toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="70fcb-109">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="70fcb-110">擷取 Azure AD 中繼資料與憑證</span><span class="sxs-lookup"><span data-stu-id="70fcb-110">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="70fcb-111">在 hello 應用程式 （登入 URL、 簽發者、 登出 URL 和憑證） 中設定 Azure AD 中繼資料值</span><span class="sxs-lookup"><span data-stu-id="70fcb-111">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="70fcb-112">將使用者指派 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="70fcb-112">Assign users toohello application</span></span>](#_Assign_users_to_the_application)

## <a name="configuring-single-sign-on-toonon-gallery-applications"></a><span data-ttu-id="70fcb-113">設定單一登入 toonon-組件庫的應用程式</span><span class="sxs-lookup"><span data-stu-id="70fcb-113">Configuring single sign-on toonon-gallery applications</span></span>

<span data-ttu-id="70fcb-114">tooconfigure 單一登入的應用程式不在 hello Azure AD 資源庫，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="70fcb-114">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="70fcb-115">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="70fcb-115">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="70fcb-116">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="70fcb-116">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70fcb-117">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="70fcb-117">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70fcb-118">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="70fcb-118">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="70fcb-119">按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="70fcb-119">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="70fcb-120">按一下**非組件庫的應用程式**在 hello**新增您自己的應用程式**區段</span><span class="sxs-lookup"><span data-stu-id="70fcb-120">click **Non-gallery application** in hello **Add your own app** section</span></span>

7.  <span data-ttu-id="70fcb-121">輸入 hello hello 應用程式名稱在 hello**名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="70fcb-121">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="70fcb-122">按一下**新增**按鈕，tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="70fcb-122">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="70fcb-123">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="70fcb-123">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="70fcb-124">選取**SAML 型登入**在 hello**模式**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="70fcb-124">Select **SAML-based Sign-on** in hello **Mode** dropdown.</span></span>

11. <span data-ttu-id="70fcb-125">輸入中的所需的 hello 值**網域和 Url。**</span><span class="sxs-lookup"><span data-stu-id="70fcb-125">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="70fcb-126">您應該從 hello 應用程式廠商，以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="70fcb-126">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="70fcb-127">tooconfigure hello IdP 初始化的 SSO 應用程式輸入 hello 回覆 URL 和識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="70fcb-127">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

   2. <span data-ttu-id="70fcb-128">**選擇性：** tooconfigure hello 應用程式做為 SP 起始的 SSO hello 登入 URL 是必要的值。</span><span class="sxs-lookup"><span data-stu-id="70fcb-128">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="70fcb-129">在 hello**使用者屬性**，選取 hello hello 中使用者的唯一識別碼**使用者識別碼**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="70fcb-129">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="70fcb-130">**選擇性：**按一下**檢視和編輯所有其他使用者屬性**tooedit hello 屬性 hello SAML 權杖中傳送的 toobe toohello 應用程式，當使用者登入。</span><span class="sxs-lookup"><span data-stu-id="70fcb-130">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="70fcb-131">tooadd 屬性：</span><span class="sxs-lookup"><span data-stu-id="70fcb-131">tooadd an attribute:</span></span>

   1. <span data-ttu-id="70fcb-132">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="70fcb-132">click **Add attribute**.</span></span> <span data-ttu-id="70fcb-133">輸入 hello**名稱**和 hello 選取 hello**值**從 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="70fcb-133">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="70fcb-134">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="70fcb-134">Click **Save.**</span></span> <span data-ttu-id="70fcb-135">您會看到 hello hello 資料表中的新屬性。</span><span class="sxs-lookup"><span data-stu-id="70fcb-135">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="70fcb-136">按一下**設定&lt;應用程式名稱&gt;** tooaccess 文件中的有關 tooconfigure 單一登入 hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="70fcb-136">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="70fcb-137">此外，您有 Azure AD Url 和 hello 應用程式所需的憑證。</span><span class="sxs-lookup"><span data-stu-id="70fcb-137">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

15. [<span data-ttu-id="70fcb-138">將使用者指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="70fcb-138">Assign users toohello application.</span></span>](#assign-users-to-the-application)

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="70fcb-139">選取使用者的識別項並新增使用者屬性傳送 toobe toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="70fcb-139">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="70fcb-140">tooselect hello 使用者識別碼或新增使用者屬性，請遵循下列的 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="70fcb-140">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="70fcb-141">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="70fcb-141">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="70fcb-142">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="70fcb-142">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70fcb-143">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="70fcb-143">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70fcb-144">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="70fcb-144">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="70fcb-145">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="70fcb-145">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="70fcb-146">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="70fcb-146">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="70fcb-147">選取您已設定單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="70fcb-147">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="70fcb-148">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="70fcb-148">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="70fcb-149">在 hello**使用者屬性**區段中，選取 hello hello 中使用者的唯一識別碼**使用者識別碼**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="70fcb-149">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="70fcb-150">hello 選取的選項必須在 hello 應用程式 tooauthenticate hello 使用者 toomatch hello 預期的值。</span><span class="sxs-lookup"><span data-stu-id="70fcb-150">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

 ><span data-ttu-id="70fcb-151">[!請注意} Azure AD 選取 hello 根據選取的 hello 值 hello NameID 屬性 （使用者識別碼） 格式或 hello hello hello SAML AuthRequest 中的應用程式所要求的格式。</span><span class="sxs-lookup"><span data-stu-id="70fcb-151">[!NOTE} Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="70fcb-152">如需詳細資訊，請造訪 hello 文章[單一登入的 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)hello 下一節 NameIDPolicy。</span><span class="sxs-lookup"><span data-stu-id="70fcb-152">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
 >
 >

9.  <span data-ttu-id="70fcb-153">tooadd 使用者屬性，按一下**檢視和編輯所有其他使用者屬性**tooedit hello 屬性 hello SAML 權杖中傳送的 toobe toohello 應用程式，當使用者登入。</span><span class="sxs-lookup"><span data-stu-id="70fcb-153">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="70fcb-154">tooadd 屬性：</span><span class="sxs-lookup"><span data-stu-id="70fcb-154">tooadd an attribute:</span></span>

   1. <span data-ttu-id="70fcb-155">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="70fcb-155">click **Add attribute**.</span></span> <span data-ttu-id="70fcb-156">輸入 hello**名稱**和 hello 選取 hello**值**從 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="70fcb-156">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="70fcb-157">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="70fcb-157">Click **Save.**</span></span> <span data-ttu-id="70fcb-158">您會看到 hello hello 資料表中的新屬性。</span><span class="sxs-lookup"><span data-stu-id="70fcb-158">You see hello new attribute in hello table.</span></span>

## <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="70fcb-159">下載 hello Azure AD 中繼資料或憑證</span><span class="sxs-lookup"><span data-stu-id="70fcb-159">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="70fcb-160">toodownload hello 應用程式中繼資料或憑證從 Azure AD，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="70fcb-160">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="70fcb-161">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="70fcb-161">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="70fcb-162">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="70fcb-162">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70fcb-163">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="70fcb-163">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70fcb-164">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="70fcb-164">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="70fcb-165">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="70fcb-165">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="70fcb-166">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="70fcb-166">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="70fcb-167">選取您已設定單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="70fcb-167">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="70fcb-168">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="70fcb-168">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="70fcb-169">跳過**SAML 簽章憑證**區段，然後按一下 **下載**資料行值。</span><span class="sxs-lookup"><span data-stu-id="70fcb-169">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="70fcb-170">根據哪些 hello 應用程式需要設定單一登入，您會看到其中一個 hello 選項 toodownload hello 中繼資料 XML 或 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="70fcb-170">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="70fcb-171">Azure AD 不會提供 URL tooget hello 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="70fcb-171">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="70fcb-172">hello 中繼資料，才能擷取為 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="70fcb-172">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-toohello-application"></a><span data-ttu-id="70fcb-173">將使用者指派 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="70fcb-173">Assign users toohello application</span></span>

<span data-ttu-id="70fcb-174">tooassign 一或多個使用者 tooan 應用程式直接管理，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="70fcb-174">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="70fcb-175">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="70fcb-175">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="70fcb-176">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="70fcb-176">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70fcb-177">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="70fcb-177">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70fcb-178">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="70fcb-178">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="70fcb-179">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="70fcb-179">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="70fcb-180">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="70fcb-180">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="70fcb-181">選取您想要使用者 toofrom hello 清單 tooassign hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="70fcb-181">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="70fcb-182">一旦 hello 應用程式載入時，按一下 **使用者和群組**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="70fcb-182">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="70fcb-183">按一下 hello**新增**hello 頂端的按鈕**使用者和群組**清單 tooopen hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="70fcb-183">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="70fcb-184">按一下 hello**使用者和群組**選取器從 hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="70fcb-184">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="70fcb-185">Hello 中的型別**全名**或**電子郵件地址**hello 使用者您感興趣指派到 hello 的**依名稱或電子郵件地址搜尋**搜尋 方塊。</span><span class="sxs-lookup"><span data-stu-id="70fcb-185">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="70fcb-186">將滑鼠停留在 hello**使用者**在 hello 清單 tooreveal**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="70fcb-186">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="70fcb-187">按一下 [hello] 核取方塊下一步 toohello 使用者的設定檔的相片或標誌 tooadd 使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="70fcb-187">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="70fcb-188">**選擇性：**如果您希望太**新增多個使用者**，在另一個類型**全名**或**電子郵件地址**到 hello**依名稱搜尋電子郵件地址或**搜尋 方塊中，然後按一下 hello 核取方塊 tooadd 這個使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="70fcb-188">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="70fcb-189">當您完成選取的使用者，請按一下 hello**選取**按鈕 tooadd 它們的使用者和群組 toobe toohello 清單指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="70fcb-189">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="70fcb-190">**選擇性：**按一下 hello**選取角色**hello 中的選取器**將作業加入**刀鋒視窗 tooselect 角色 tooassign toohello 使用者已選取。</span><span class="sxs-lookup"><span data-stu-id="70fcb-190">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="70fcb-191">按一下 hello**指派**按鈕 tooassign hello 應用程式 toohello 選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="70fcb-191">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="70fcb-192">一段短時間，您已選取的 hello 使用者是使用這些應用程式 hello hello 方案描述 部分中所述的方法可以 toolaunch。</span><span class="sxs-lookup"><span data-stu-id="70fcb-192">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="70fcb-193">自訂 hello SAML 宣告傳送 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="70fcb-193">Customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="70fcb-194">toolearn 如何 toocustomize hello SAML 屬性宣告傳送 tooyour 應用程式，請參閱[宣告 Azure Active Directory 中的對應](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="70fcb-194">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70fcb-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="70fcb-195">Next steps</span></span>
[<span data-ttu-id="70fcb-196">提供單一登入 tooyour 應用程式與應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="70fcb-196">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

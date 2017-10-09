---
title: "aaaHow tooconfigure 同盟單一登入 Azure AD 庫應用程式 |Microsoft 文件"
description: "如何 tooconfigure 同盟單一登入的現有 Azure AD 庫應用程式並使用教學課程 tooget 快速地移"
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
ms.openlocfilehash: a93de021fddd253e4fe663c221b822d12625fd54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="e9147-103">如何 tooconfigure 同盟單一登入 Azure AD 庫應用程式</span><span class="sxs-lookup"><span data-stu-id="e9147-103">How tooconfigure federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="e9147-104">Hello Azure AD 啟用具備企業單一登入功能的組件庫中的所有應用程式有可用的逐步教學課程。</span><span class="sxs-lookup"><span data-stu-id="e9147-104">All applications in hello Azure AD gallery enabled with Enterprise single sign-on capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="e9147-105">您可以存取 hello[如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/)如需詳細的逐步指引。</span><span class="sxs-lookup"><span data-stu-id="e9147-105">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for detailed step-by-step guidance.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="e9147-106">所需步驟的概觀</span><span class="sxs-lookup"><span data-stu-id="e9147-106">Overview of steps required</span></span>
<span data-ttu-id="e9147-107">您需要 tooconfigure 從 hello Azure AD 的組件庫的應用程式：</span><span class="sxs-lookup"><span data-stu-id="e9147-107">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="e9147-108">從 hello Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="e9147-108">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="e9147-109">設定 Azure AD （登入 URL，識別項，回覆 URL） 中的 hello 應用程式的中繼資料值</span><span class="sxs-lookup"><span data-stu-id="e9147-109">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="e9147-110">選取使用者的識別項並新增使用者屬性傳送 toobe toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e9147-110">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="e9147-111">擷取 Azure AD 中繼資料與憑證</span><span class="sxs-lookup"><span data-stu-id="e9147-111">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="e9147-112">在 hello 應用程式 （登入 URL、 簽發者、 登出 URL 和憑證） 中設定 Azure AD 中繼資料值</span><span class="sxs-lookup"><span data-stu-id="e9147-112">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="e9147-113">將使用者指派 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e9147-113">Assign users toohello application</span></span>](#assign-users-to-the-application)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="e9147-114">從 hello Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="e9147-114">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="e9147-115">tooadd hello Azure AD 資源庫，從應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="e9147-115">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="e9147-116">開啟 hello [Azure 入口網站](https://portal.azure.com)身分登入和**全域管理員**或**共同管理員**</span><span class="sxs-lookup"><span data-stu-id="e9147-116">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="e9147-117">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="e9147-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e9147-118">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="e9147-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e9147-119">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e9147-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e9147-120">按一下 hello**新增**上 hello hello 右上角的按鈕**企業應用程式**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e9147-120">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="e9147-121">在 hello**輸入的名稱**文字方塊中，從 hello**從 hello 圖庫新增**> 一節中，輸入 hello 名稱 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e9147-121">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="e9147-122">選取要用於單一登入 tooconfigure hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e9147-122">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="e9147-123">然後再加入 hello 應用程式，您可以變更其名稱從 hello**名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="e9147-123">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="e9147-124">按一下**新增**按鈕，tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e9147-124">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="e9147-125">在短時間之後, 就無法 toosee hello 應用程式的組態刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e9147-125">After a short period of time, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="e9147-126">設定單一登入應用程式從 hello Azure AD 資源庫</span><span class="sxs-lookup"><span data-stu-id="e9147-126">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="e9147-127">tooconfigure 單一登入的應用程式，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="e9147-127">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="e9147-128">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員**。</span><span class="sxs-lookup"><span data-stu-id="e9147-128">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="e9147-129">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="e9147-129">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e9147-130">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="e9147-130">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e9147-131">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e9147-131">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e9147-132">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="e9147-132">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="e9147-133">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="e9147-133">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e9147-134">選取您想 tooconfigure 單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e9147-134">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="e9147-135">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e9147-135">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e9147-136">選取**SAML 型登入**從 hello**模式**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="e9147-136">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="e9147-137">輸入中的所需的 hello 值**網域和 Url。**</span><span class="sxs-lookup"><span data-stu-id="e9147-137">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="e9147-138">您應該從 hello 應用程式廠商，以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="e9147-138">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="e9147-139">tooconfigure hello 應用程式做為 SP 起始的 SSO hello 登入 URL 是必要的值。</span><span class="sxs-lookup"><span data-stu-id="e9147-139">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="e9147-140">有些應用程式識別碼 hello 也是必要的值。</span><span class="sxs-lookup"><span data-stu-id="e9147-140">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="e9147-141">tooconfigure hello 應用程式做為 IdP 初始化的 SSO，hello 回覆 URL 是必要的值。</span><span class="sxs-lookup"><span data-stu-id="e9147-141">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="e9147-142">有些應用程式識別碼 hello 也是必要的值。</span><span class="sxs-lookup"><span data-stu-id="e9147-142">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="e9147-143">**選擇性：**按一下**顯示進階的 URL 設定**您希望 toosee hello 非必要的值。</span><span class="sxs-lookup"><span data-stu-id="e9147-143">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="e9147-144">在 hello**使用者屬性**，選取 hello hello 中使用者的唯一識別碼**使用者識別碼**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="e9147-144">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="e9147-145">**選擇性：**按一下**檢視和編輯所有其他使用者屬性**tooedit hello 屬性 hello SAML 權杖中傳送的 toobe toohello 應用程式，當使用者登入。</span><span class="sxs-lookup"><span data-stu-id="e9147-145">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

  <span data-ttu-id="e9147-146">tooadd 屬性：</span><span class="sxs-lookup"><span data-stu-id="e9147-146">tooadd an attribute:</span></span>
   
   1. <span data-ttu-id="e9147-147">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="e9147-147">click **Add attribute**.</span></span> <span data-ttu-id="e9147-148">輸入 hello**名稱**和 hello 選取 hello**值**從 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="e9147-148">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   1. <span data-ttu-id="e9147-149">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="e9147-149">Click **Save.**</span></span> <span data-ttu-id="e9147-150">您會看到 hello hello 資料表中的新屬性。</span><span class="sxs-lookup"><span data-stu-id="e9147-150">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="e9147-151">按一下**設定&lt;應用程式名稱&gt;** tooaccess 文件中的有關 tooconfigure 單一登入 hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="e9147-151">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="e9147-152">此外，您有 hello 中繼資料 Url 和與 hello 應用程式所需的憑證 toosetup SSO。</span><span class="sxs-lookup"><span data-stu-id="e9147-152">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="e9147-153">按一下**儲存**toosave hello 組態。</span><span class="sxs-lookup"><span data-stu-id="e9147-153">Click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="e9147-154">將使用者指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e9147-154">Assign users toohello application.</span></span>

## <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="e9147-155">選取使用者的識別項並新增使用者屬性傳送 toobe toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e9147-155">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="e9147-156">tooselect hello 使用者識別碼或新增使用者屬性，請遵循下列的 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="e9147-156">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="e9147-157">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="e9147-157">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e9147-158">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="e9147-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e9147-159">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="e9147-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e9147-160">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e9147-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e9147-161">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="e9147-161">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="e9147-162">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="e9147-162">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e9147-163">選取您已設定單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e9147-163">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="e9147-164">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e9147-164">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e9147-165">在 hello**使用者屬性**區段中，選取 hello hello 中使用者的唯一識別碼**使用者識別碼**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="e9147-165">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="e9147-166">hello 選取的選項必須在 hello 應用程式 tooauthenticate hello 使用者 toomatch hello 預期的值。</span><span class="sxs-lookup"><span data-stu-id="e9147-166">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

  >[!NOTE] 
  ><span data-ttu-id="e9147-167">Hello NameID 屬性 （使用者識別碼） 的 azure AD 選取 hello 格式會根據選取的 hello 值或 hello hello hello SAML AuthRequest 中的應用程式所要求的格式。</span><span class="sxs-lookup"><span data-stu-id="e9147-167">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="e9147-168">如需詳細資訊，請造訪 hello 文章[單一登入的 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)hello 下一節 NameIDPolicy。</span><span class="sxs-lookup"><span data-stu-id="e9147-168">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
  >
  >

9.  <span data-ttu-id="e9147-169">tooadd 使用者屬性，按一下**檢視和編輯所有其他使用者屬性**tooedit hello 屬性 hello SAML 權杖中傳送的 toobe toohello 應用程式，當使用者登入。</span><span class="sxs-lookup"><span data-stu-id="e9147-169">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="e9147-170">tooadd 屬性：</span><span class="sxs-lookup"><span data-stu-id="e9147-170">tooadd an attribute:</span></span>
  
   1. <span data-ttu-id="e9147-171">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="e9147-171">click **Add attribute**.</span></span> <span data-ttu-id="e9147-172">輸入 hello**名稱**和 hello 選取 hello**值**從 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="e9147-172">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="e9147-173">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="e9147-173">Click **Save**.</span></span> <span data-ttu-id="e9147-174">您會看到 hello hello 資料表中的新屬性。</span><span class="sxs-lookup"><span data-stu-id="e9147-174">You see hello new attribute in hello table.</span></span>

## <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="e9147-175">下載 hello Azure AD 中繼資料或憑證</span><span class="sxs-lookup"><span data-stu-id="e9147-175">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="e9147-176">toodownload hello 應用程式中繼資料或憑證從 Azure AD，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="e9147-176">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="e9147-177">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="e9147-177">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e9147-178">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="e9147-178">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e9147-179">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="e9147-179">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e9147-180">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e9147-180">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e9147-181">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="e9147-181">click **All Applications** tooview a list of all your applications.</span></span>

  *  <span data-ttu-id="e9147-182">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e9147-182">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications**.</span></span>

6.  <span data-ttu-id="e9147-183">選取您已設定單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e9147-183">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="e9147-184">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e9147-184">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e9147-185">跳過**SAML 簽章憑證**區段，然後按一下 **下載**資料行值。</span><span class="sxs-lookup"><span data-stu-id="e9147-185">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="e9147-186">根據哪些 hello 應用程式需要設定單一登入，您會看到其中一個 hello 選項 toodownload hello 中繼資料 XML 或 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="e9147-186">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="e9147-187">Azure AD 不會提供 URL tooget hello 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="e9147-187">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="e9147-188">hello 中繼資料，才能擷取為 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="e9147-188">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-toohello-application"></a><span data-ttu-id="e9147-189">將使用者指派 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e9147-189">Assign users toohello application</span></span>

<span data-ttu-id="e9147-190">tooassign 一或多個使用者 tooan 應用程式直接管理，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="e9147-190">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="e9147-191">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="e9147-191">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="e9147-192">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="e9147-192">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e9147-193">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="e9147-193">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e9147-194">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e9147-194">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e9147-195">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="e9147-195">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e9147-196">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="e9147-196">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e9147-197">選取您想要使用者 toofrom hello 清單 tooassign hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e9147-197">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="e9147-198">一旦 hello 應用程式載入時，按一下 **使用者和群組**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e9147-198">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e9147-199">按一下 hello**新增**hello 頂端的按鈕**使用者和群組**清單 tooopen hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e9147-199">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="e9147-200">按一下 hello**使用者和群組**選取器從 hello**將作業加入**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e9147-200">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="e9147-201">Hello 中的型別**全名**或**電子郵件地址**hello 使用者您感興趣指派到 hello 的**依名稱或電子郵件地址搜尋**搜尋 方塊。</span><span class="sxs-lookup"><span data-stu-id="e9147-201">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="e9147-202">將滑鼠停留在 hello**使用者**在 hello 清單 tooreveal**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="e9147-202">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="e9147-203">按一下 [hello] 核取方塊下一步 toohello 使用者的設定檔的相片或標誌 tooadd 使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="e9147-203">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="e9147-204">**選擇性：**如果您希望太**新增多個使用者**，在另一個類型**全名**或**電子郵件地址**到 hello**依名稱搜尋電子郵件地址或**搜尋 方塊中，然後按一下 hello 核取方塊 tooadd 這個使用者 toohello**選取**清單。</span><span class="sxs-lookup"><span data-stu-id="e9147-204">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="e9147-205">當您完成選取的使用者，請按一下 hello**選取**按鈕 tooadd 它們的使用者和群組 toobe toohello 清單指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e9147-205">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="e9147-206">**選擇性：**按一下 hello**選取角色**hello 中的選取器**將作業加入**刀鋒視窗 tooselect 角色 tooassign toohello 使用者已選取。</span><span class="sxs-lookup"><span data-stu-id="e9147-206">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="e9147-207">按一下 hello**指派**按鈕 tooassign hello 應用程式 toohello 選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="e9147-207">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="e9147-208">一段短時間，您已選取的 hello 使用者是使用這些應用程式 hello hello 方案描述 部分中所述的方法可以 toolaunch。</span><span class="sxs-lookup"><span data-stu-id="e9147-208">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="e9147-209">自訂 hello SAML 宣告傳送 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="e9147-209">Customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="e9147-210">toolearn 如何 toocustomize hello SAML 屬性宣告傳送 tooyour 應用程式，請參閱[宣告 Azure Active Directory 中的對應](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e9147-210">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9147-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e9147-211">Next steps</span></span>
[<span data-ttu-id="e9147-212">提供單一登入 tooyour 應用程式與應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="e9147-212">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)




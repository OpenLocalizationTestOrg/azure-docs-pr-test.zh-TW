---
title: "設定同盟單一登入 Azure AD 庫應用程式的 aaaProblem |Microsoft 文件"
description: "解決部分 hello 常見的問題，您可能會遇到當設定同盟單一登入使用 SAML hello Azure AD 應用程式庫中所列的應用程式"
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
ms.openlocfilehash: 2ae1e511bd49b19159e1ab83cf79a7db5403b9a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="c7e6d-103">為 Azure AD 資源庫應用程式設定同盟單一登入時遇到的問題</span><span class="sxs-lookup"><span data-stu-id="c7e6d-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="c7e6d-104">如果您在設定應用程式時遇到問題。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="c7e6d-105">請確認您已依照 hello 應用程式的 hello 教學課程中的 hello 的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-105">Verify you have followed all hello steps in hello tutorial for hello application.</span></span> <span data-ttu-id="c7e6d-106">在 hello 應用程式組態中，您必須上如何 tooconfigure hello 應用程式的內嵌文件。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-106">In hello application’s configuration, you have inline documentation on how tooconfigure hello application.</span></span> <span data-ttu-id="c7e6d-107">此外，您可以存取 hello[如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/)如需詳細資料的逐步指引。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-107">Also, you can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="c7e6d-108">無法加入 hello 應用程式的另一個執行個體</span><span class="sxs-lookup"><span data-stu-id="c7e6d-108">Can’t add another instance of hello application</span></span>

<span data-ttu-id="c7e6d-109">tooadd 應用程式的第二個執行個體，您需要 toobe 能夠：</span><span class="sxs-lookup"><span data-stu-id="c7e6d-109">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="c7e6d-110">設定 hello 第二個執行個體的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-110">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="c7e6d-111">您必須能夠 tooconfigure hello 相同識別項用於 hello 第一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-111">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="c7e6d-112">設定用於 hello 第一個執行個體的 hello 與不同的憑證。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-112">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="c7e6d-113">如果 hello 應用程式不支援任何上述 hello。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-113">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="c7e6d-114">然後，您必須能夠 tooconfigure 第二個執行個體。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-114">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="cant-add-hello-identifier-or-hello-reply-url"></a><span data-ttu-id="c7e6d-115">無法新增識別碼 hello 或 hello 回覆 URL</span><span class="sxs-lookup"><span data-stu-id="c7e6d-115">Can’t add hello Identifier or hello Reply URL</span></span>

<span data-ttu-id="c7e6d-116">如果您不能 tooconfigure hello 識別碼或 hello 回覆 URL，確認 hello 識別碼，而且回覆 URL 值符合 hello 模式預先設定的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-116">If you’re not able tooconfigure hello Identifier or hello Reply URL, confirm hello Identifier and Reply URL values match hello patterns pre-configured for hello application.</span></span>

<span data-ttu-id="c7e6d-117">tooknow hello 模式預先設定的 hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="c7e6d-117">tooknow hello patterns pre-configured for hello application:</span></span>

1.  <span data-ttu-id="c7e6d-118">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**移 toostep 7。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.** Go toostep 7.</span></span> <span data-ttu-id="c7e6d-119">如果您已經在 hello 應用程式設定 刀鋒視窗上 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-119">If you are already in hello application configuration blade on Azure AD.</span></span>

2.  <span data-ttu-id="c7e6d-120">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c7e6d-121">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c7e6d-122">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c7e6d-123">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="c7e6d-124">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="c7e6d-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c7e6d-125">選取您想 tooconfigure 單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-125">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="c7e6d-126">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c7e6d-127">選取**SAML 型登入**從 hello**模式**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-127">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="c7e6d-128">移 toohello**識別碼**或**回覆 URL**文字方塊中，在 hello**網域和 Url 的區段。**</span><span class="sxs-lookup"><span data-stu-id="c7e6d-128">Go toohello **Identifier** or **Reply URL** textbox, under hello **Domain and URLs section.**</span></span>

10. <span data-ttu-id="c7e6d-129">有三種方式 hello 應用程式的 tooknow hello 支援模式：</span><span class="sxs-lookup"><span data-stu-id="c7e6d-129">There are three ways tooknow hello supported patterns for hello application:</span></span>

   * <span data-ttu-id="c7e6d-130">在 [hello] 文字方塊中，您會看到 hello 支援模式做為預留位置*範例：* <https://contoso.com>。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-130">In hello textbox, you see hello supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span></span>

   * <span data-ttu-id="c7e6d-131">如果不支援 hello 模式，您會看到紅色驚嘆號時 tooenter hello 文字方塊中的 hello 值再試一次。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-131">if hello pattern is not supported, you see a red exclamation mark when you try tooenter hello value in hello textbox.</span></span> <span data-ttu-id="c7e6d-132">如果您將滑鼠停留 hello 紅色驚嘆號，您會看到 hello 支援模式。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-132">If you hover your mouse over hello red exclamation mark, you see hello supported patterns.</span></span>

   * <span data-ttu-id="c7e6d-133">Hello 教學課程中的 hello 應用程式，您也可以取得支援的 hello 模式的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-133">In hello tutorial for hello application, you can also get information about hello supported patterns.</span></span> <span data-ttu-id="c7e6d-134">在 hello**設定 Azure AD 單一登入**> 一節。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-134">Under hello **Configure Azure AD single sign-on** section.</span></span> <span data-ttu-id="c7e6d-135">設定的 hello 值在 hello 移 toohello 步驟**網域和 Url** > 一節。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-135">Go toohello step for configured hello values under hello **Domain and URLs** section.</span></span>

<span data-ttu-id="c7e6d-136">如果 hello 值不符合使用預先設定的 Azure AD 上 hello 模式。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-136">If hello values don’t match with hello patterns pre-configured on Azure AD.</span></span> <span data-ttu-id="c7e6d-137">您可以：</span><span class="sxs-lookup"><span data-stu-id="c7e6d-137">You can:</span></span>

-   <span data-ttu-id="c7e6d-138">搭配 hello 應用程式廠商 tooget 值符合預先設定的 Azure AD 上 hello 模式</span><span class="sxs-lookup"><span data-stu-id="c7e6d-138">Work with hello application vendor tooget values that match hello pattern pre-configured on Azure AD</span></span>

-   <span data-ttu-id="c7e6d-139">或者，您可以連絡 Azure AD 團隊< aadapprequest@microsoft.com >或留下的 hello 應用程式的支援 hello 模式 hello 教學課程 toorequest hello 更新中的註解</span><span class="sxs-lookup"><span data-stu-id="c7e6d-139">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in hello tutorial toorequest hello update of hello supported patterns for hello application</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="c7e6d-140">其中將 hello EntityID （使用者識別碼） 格式的設定</span><span class="sxs-lookup"><span data-stu-id="c7e6d-140">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="c7e6d-141">您必須能夠 tooselect hello EntityID （使用者識別碼） 格式，Azure AD 會傳送 toohello 應用程式以 hello 回應使用者驗證之後。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-141">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="c7e6d-142">Hello NameID 屬性 （使用者識別碼） 的 azure AD 選取 hello 格式會根據選取的 hello 值或 hello hello hello SAML AuthRequest 中的應用程式所要求的格式。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-142">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="c7e6d-143">如需詳細資訊，請造訪 hello 文章[單一登入的 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)hello 之下 NameIDPolicy，</span><span class="sxs-lookup"><span data-stu-id="c7e6d-143">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="cant-find-hello-azure-ad-metadata-toocomplete-hello-configuration-with-hello-application"></a><span data-ttu-id="c7e6d-144">找不到 hello Azure AD 中繼資料 toocomplete hello 組態與 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="c7e6d-144">Can’t find hello Azure AD metadata toocomplete hello configuration with hello application</span></span>

<span data-ttu-id="c7e6d-145">toodownload hello 應用程式中繼資料或憑證從 Azure AD，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="c7e6d-145">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="c7e6d-146">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員**或**共同管理員。**</span><span class="sxs-lookup"><span data-stu-id="c7e6d-146">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c7e6d-147">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-147">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c7e6d-148">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-148">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c7e6d-149">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-149">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c7e6d-150">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-150">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="c7e6d-151">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="c7e6d-151">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="c7e6d-152">選取您已設定單一登入的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-152">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="c7e6d-153">一旦 hello 應用程式載入時，按一下 hello**單一登入**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-153">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="c7e6d-154">跳過**SAML 簽章憑證**區段，然後按一下 **下載**資料行值。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-154">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="c7e6d-155">根據哪些 hello 應用程式需要設定單一登入，您會看到其中一個 hello 選項 toodownload hello 中繼資料 XML 或 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-155">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="c7e6d-156">Azure AD 不會提供 URL tooget hello 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-156">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="c7e6d-157">hello 中繼資料，才能擷取為 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-157">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="c7e6d-158">不知道如何 toocustomize SAML 宣告傳送 tooan 應用程式</span><span class="sxs-lookup"><span data-stu-id="c7e6d-158">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="c7e6d-159">toolearn 如何 toocustomize hello SAML 屬性宣告傳送 tooyour 應用程式，請參閱[宣告 Azure Active Directory 中的對應](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c7e6d-159">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7e6d-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c7e6d-160">Next steps</span></span>
[<span data-ttu-id="c7e6d-161">使用 Azure Active Directory 管理應用程式</span><span class="sxs-lookup"><span data-stu-id="c7e6d-161">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)

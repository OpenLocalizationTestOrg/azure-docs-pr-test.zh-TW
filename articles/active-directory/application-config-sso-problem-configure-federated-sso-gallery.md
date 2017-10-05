---
title: "為 Azure AD 資源庫應用程式設定同盟單一登入時遇到的問題 | Microsoft Docs"
description: "解決您可能會在為 Azure AD 應用程式庫中所列的應用程式，使用 SAML 設定同盟單一登入時遇到的一些常見問題"
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
ms.openlocfilehash: 290ca66048281de5e031b0404919bed84ab19ffa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="535b7-103">為 Azure AD 資源庫應用程式設定同盟單一登入時遇到的問題</span><span class="sxs-lookup"><span data-stu-id="535b7-103">Problem configuring federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="535b7-104">如果您在設定應用程式時遇到問題。</span><span class="sxs-lookup"><span data-stu-id="535b7-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="535b7-105">請確認您已經依照應用程式教學課程中的所有步驟執行。</span><span class="sxs-lookup"><span data-stu-id="535b7-105">Verify you have followed all the steps in the tutorial for the application.</span></span> <span data-ttu-id="535b7-106">在應用程式的設定中，您擁有如何設定應用程式的內嵌文件。</span><span class="sxs-lookup"><span data-stu-id="535b7-106">In the application’s configuration, you have inline documentation on how to configure the application.</span></span> <span data-ttu-id="535b7-107">此外，您可以存取[如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/)，以取得詳細的逐步指引。</span><span class="sxs-lookup"><span data-stu-id="535b7-107">Also, you can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

## <a name="cant-add-another-instance-of-the-application"></a><span data-ttu-id="535b7-108">無法新增應用程式的另一個執行個體</span><span class="sxs-lookup"><span data-stu-id="535b7-108">Can’t add another instance of the application</span></span>

<span data-ttu-id="535b7-109">若要新增應用程式的第二個執行個體，您需要能夠：</span><span class="sxs-lookup"><span data-stu-id="535b7-109">To add a second instance of an application, you need to be able to:</span></span>

-   <span data-ttu-id="535b7-110">設定第二個執行個體的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="535b7-110">Configure a unique identifier for the second instance.</span></span> <span data-ttu-id="535b7-111">您無法設定已用於第一個執行個體的相同識別碼。</span><span class="sxs-lookup"><span data-stu-id="535b7-111">You won’t be able to configure the same identifier used for the first instance.</span></span>

-   <span data-ttu-id="535b7-112">設定與第一個執行個體所使用的憑證不同的憑證。</span><span class="sxs-lookup"><span data-stu-id="535b7-112">Configure a different certificate than the one used for the first instance.</span></span>

<span data-ttu-id="535b7-113">如果應用程式不支援上述任一種方法。</span><span class="sxs-lookup"><span data-stu-id="535b7-113">If the application doesn’t support any of the above.</span></span> <span data-ttu-id="535b7-114">則您將無法設定第二個執行個體。</span><span class="sxs-lookup"><span data-stu-id="535b7-114">Then, you won’t be able to configure a second instance.</span></span>

## <a name="cant-add-the-identifier-or-the-reply-url"></a><span data-ttu-id="535b7-115">無法新增識別碼或回覆 URL</span><span class="sxs-lookup"><span data-stu-id="535b7-115">Can’t add the Identifier or the Reply URL</span></span>

<span data-ttu-id="535b7-116">如果您無法設定識別碼或回覆 URL，請確認識別碼和回覆 URL 值符合針對應用程式預先設定的模式。</span><span class="sxs-lookup"><span data-stu-id="535b7-116">If you’re not able to configure the Identifier or the Reply URL, confirm the Identifier and Reply URL values match the patterns pre-configured for the application.</span></span>

<span data-ttu-id="535b7-117">了解針對應用程式預先設定的模式：</span><span class="sxs-lookup"><span data-stu-id="535b7-117">To know the patterns pre-configured for the application:</span></span>

1.  <span data-ttu-id="535b7-118">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="535b7-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> <span data-ttu-id="535b7-119">移至步驟 7。</span><span class="sxs-lookup"><span data-stu-id="535b7-119">Go to step 7.</span></span> <span data-ttu-id="535b7-120">如果您已經有位於 Azure AD 的應用程式設定刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="535b7-120">If you are already in the application configuration blade on Azure AD.</span></span>

2.  <span data-ttu-id="535b7-121">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="535b7-121">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="535b7-122">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="535b7-122">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="535b7-123">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="535b7-123">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="535b7-124">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="535b7-124">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="535b7-125">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="535b7-125">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="535b7-126">選取您要設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="535b7-126">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="535b7-127">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="535b7-127">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="535b7-128">從 [模式] 下拉式清單選取 [SAML 登入]。</span><span class="sxs-lookup"><span data-stu-id="535b7-128">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="535b7-129">移至 [網域及 URL] 區段下方的 [識別碼] 或 [回覆 URL] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="535b7-129">Go to the **Identifier** or **Reply URL** textbox, under the **Domain and URLs section.**</span></span>

10. <span data-ttu-id="535b7-130">有三種方式可以知道應用程式支援的模式：</span><span class="sxs-lookup"><span data-stu-id="535b7-130">There are three ways to know the supported patterns for the application:</span></span>

   * <span data-ttu-id="535b7-131">在文字方塊中，您可以看到支援模式是以預留位置的形式 (範例︰<https://contoso.com>) 出現。</span><span class="sxs-lookup"><span data-stu-id="535b7-131">In the textbox, you see the supported pattern(s) as a placeholder *Example:* <https://contoso.com>.</span></span>

   * <span data-ttu-id="535b7-132">如果模式不受支援，則當您嘗試在文字方塊中輸入值時，會看到紅色驚嘆號。</span><span class="sxs-lookup"><span data-stu-id="535b7-132">if the pattern is not supported, you see a red exclamation mark when you try to enter the value in the textbox.</span></span> <span data-ttu-id="535b7-133">如果您將滑鼠移到紅色驚嘆號上方，就會看到支援的模式。</span><span class="sxs-lookup"><span data-stu-id="535b7-133">If you hover your mouse over the red exclamation mark, you see the supported patterns.</span></span>

   * <span data-ttu-id="535b7-134">在應用程式的教學課程中，您也可以取得支援模式的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="535b7-134">In the tutorial for the application, you can also get information about the supported patterns.</span></span> <span data-ttu-id="535b7-135">在**設定 Azure AD 單一登入**一節中。</span><span class="sxs-lookup"><span data-stu-id="535b7-135">Under the **Configure Azure AD single sign-on** section.</span></span> <span data-ttu-id="535b7-136">移至在 [網域及 URL] 區段下方設定值的步驟。</span><span class="sxs-lookup"><span data-stu-id="535b7-136">Go to the step for configured the values under the **Domain and URLs** section.</span></span>

<span data-ttu-id="535b7-137">如果值不符合 Azure AD 上預先設定的模式。</span><span class="sxs-lookup"><span data-stu-id="535b7-137">If the values don’t match with the patterns pre-configured on Azure AD.</span></span> <span data-ttu-id="535b7-138">您可以：</span><span class="sxs-lookup"><span data-stu-id="535b7-138">You can:</span></span>

-   <span data-ttu-id="535b7-139">洽詢應用程式廠商，以取得符合 Azure AD 上預先設定之模式的值</span><span class="sxs-lookup"><span data-stu-id="535b7-139">Work with the application vendor to get values that match the pattern pre-configured on Azure AD</span></span>

-   <span data-ttu-id="535b7-140">或者，您可以連絡 Azure AD 小組 <aadapprequest@microsoft.com> ，或在教學課程中留下註解，以要求應用程式支援模式的更新</span><span class="sxs-lookup"><span data-stu-id="535b7-140">Or, you can contact Azure AD team at <aadapprequest@microsoft.com> or leave a comment in the tutorial to request the update of the supported patterns for the application</span></span>

## <a name="where-do-i-set-the-entityid-user-identifier-format"></a><span data-ttu-id="535b7-141">我可以在何處設定 EntityID (使用者識別碼) 格式</span><span class="sxs-lookup"><span data-stu-id="535b7-141">Where do I set the EntityID (User Identifier) format</span></span>

<span data-ttu-id="535b7-142">在使用者驗證之後，您將無法選取 Azure AD 要在回應中傳送至應用程式的 EntityID (使用者識別碼) 格式。</span><span class="sxs-lookup"><span data-stu-id="535b7-142">You won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="535b7-143">Azure AD 會根據應用程式在 SAML AuthRequest 中選取的值或要求的格式，來選取 NameID 屬性 (使用者識別碼) 的格式。</span><span class="sxs-lookup"><span data-stu-id="535b7-143">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="535b7-144">如需詳細資訊，請參閱[單一登入 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)文章中的＜NameIDPolicy＞一節。</span><span class="sxs-lookup"><span data-stu-id="535b7-144">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span></span>

## <a name="cant-find-the-azure-ad-metadata-to-complete-the-configuration-with-the-application"></a><span data-ttu-id="535b7-145">找不到 Azure AD 中繼資料以完成應用程式的設定</span><span class="sxs-lookup"><span data-stu-id="535b7-145">Can’t find the Azure AD metadata to complete the configuration with the application</span></span>

<span data-ttu-id="535b7-146">若要從 Azure AD 下載應用程式中繼資料或憑證，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="535b7-146">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="535b7-147">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="535b7-147">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="535b7-148">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="535b7-148">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="535b7-149">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="535b7-149">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="535b7-150">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="535b7-150">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="535b7-151">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="535b7-151">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="535b7-152">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="535b7-152">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="535b7-153">選取您已設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="535b7-153">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="535b7-154">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="535b7-154">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="535b7-155">移至 [SAML 簽署憑證] 區段，然後按一下 [下載] 資料行值。</span><span class="sxs-lookup"><span data-stu-id="535b7-155">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="535b7-156">根據應用程式設定單一登入時所需的項目，您會看到下載中繼資料 XML 或憑證的選項。</span><span class="sxs-lookup"><span data-stu-id="535b7-156">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="535b7-157">Azure AD 不提供取得中繼資料的 URL。</span><span class="sxs-lookup"><span data-stu-id="535b7-157">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="535b7-158">只能將中繼資料擷取為 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="535b7-158">The metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-to-customize-saml-claims-sent-to-an-application"></a><span data-ttu-id="535b7-159">不知道如何自訂傳送至應用程式的 SAML 宣告</span><span class="sxs-lookup"><span data-stu-id="535b7-159">Don't know how to customize SAML claims sent to an application</span></span>

<span data-ttu-id="535b7-160">若要了解如何自訂傳送至應用程式的 SAML 屬性宣告，請參閱 [Azure Active Directory 中的宣告對應](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping)以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="535b7-160">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="535b7-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="535b7-161">Next steps</span></span>
[<span data-ttu-id="535b7-162">使用 Azure Active Directory 管理應用程式</span><span class="sxs-lookup"><span data-stu-id="535b7-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)

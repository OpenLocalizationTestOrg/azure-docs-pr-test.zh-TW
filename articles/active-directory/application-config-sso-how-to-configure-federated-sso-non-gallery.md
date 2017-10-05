---
title: "如何為不在資源庫內的應用程式設定同盟單一登入 | Microsoft Docs"
description: "如何為您想要與 Azure AD 整合且不在資源庫內的自訂應用程式設定同盟單一登入"
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
ms.openlocfilehash: da7bc05c6452cde4d0236806f249559f178dd4e1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="673e7-103">如何為不在資源庫內的應用程式設定同盟單一登入</span><span class="sxs-lookup"><span data-stu-id="673e7-103">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="673e7-104">若要設定不在資源庫內的應用程式，您必須有 Azure AD Premium，且應用程式必須支援 SAML 2.0。</span><span class="sxs-lookup"><span data-stu-id="673e7-104">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="673e7-105">如需有關 Azure AD 版本的詳細資訊，請參閱 [Azure AD 定價](https://azure.microsoft.com/pricing/details/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="673e7-105">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="673e7-106">所需步驟的概觀</span><span class="sxs-lookup"><span data-stu-id="673e7-106">Overview of steps required</span></span>
<span data-ttu-id="673e7-107">以下是為不在資源庫內 (例如，自訂) 的應用程式設定同盟單一登入所需步驟的概觀。</span><span class="sxs-lookup"><span data-stu-id="673e7-107">Below is a high level overview of the steps required to configure federated single sign-on for a non-gallery (e.g., custom) application.</span></span>

-   [<span data-ttu-id="673e7-108">在 Azure AD 中設定應用程式的中繼資料值 (登入 URL、識別碼、回覆 URL)</span><span class="sxs-lookup"><span data-stu-id="673e7-108">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="673e7-109">選取使用者識別碼並新增要傳送到應用程式的使用者屬性</span><span class="sxs-lookup"><span data-stu-id="673e7-109">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="673e7-110">擷取 Azure AD 中繼資料與憑證</span><span class="sxs-lookup"><span data-stu-id="673e7-110">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="673e7-111">在應用程式中設定 Azure AD 中繼資料值 (登入 URL、簽發者、登出 URL 與憑證)</span><span class="sxs-lookup"><span data-stu-id="673e7-111">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="673e7-112">將使用者指派給應用程式</span><span class="sxs-lookup"><span data-stu-id="673e7-112">Assign users to the application</span></span>](#_Assign_users_to_the_application)

## <a name="configuring-single-sign-on-to-non-gallery-applications"></a><span data-ttu-id="673e7-113">為不在資源庫內的應用程式設定單一登入</span><span class="sxs-lookup"><span data-stu-id="673e7-113">Configuring single sign-on to non-gallery applications</span></span>

<span data-ttu-id="673e7-114">若要為不在 Azure AD 資源庫中的應用程式設定單一登入，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="673e7-114">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="673e7-115">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="673e7-115">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="673e7-116">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="673e7-116">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="673e7-117">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="673e7-117">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="673e7-118">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="673e7-118">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="673e7-119">按一下 [企業應用程式] 刀鋒視窗右上角的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="673e7-119">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="673e7-120">按一下 [新增您自己的應用程式] 區段中的 [不在資源庫內的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="673e7-120">click **Non-gallery application** in the **Add your own app** section</span></span>

7.  <span data-ttu-id="673e7-121">在 [名稱] 文字方塊中輸入應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="673e7-121">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="673e7-122">按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="673e7-122">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="673e7-123">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="673e7-123">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="673e7-124">在 [模式] 下拉式清單中選取 [SAML 登入]。</span><span class="sxs-lookup"><span data-stu-id="673e7-124">Select **SAML-based Sign-on** in the **Mode** dropdown.</span></span>

11. <span data-ttu-id="673e7-125">在 [網域及 URL] 中輸入必要值。</span><span class="sxs-lookup"><span data-stu-id="673e7-125">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="673e7-126">這些值應從應用程式廠商處取得。</span><span class="sxs-lookup"><span data-stu-id="673e7-126">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="673e7-127">若要將應用程式設定為 IdP 啟始的 SSO，請輸入回覆 URL 與識別碼。</span><span class="sxs-lookup"><span data-stu-id="673e7-127">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

   2. <span data-ttu-id="673e7-128">**選擇性：**若要將應用程式設定為 SP 啟始的 SSO，則登入 URL 為必要值。</span><span class="sxs-lookup"><span data-stu-id="673e7-128">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="673e7-129">在 [使用者屬性] 中，從 [使用者識別碼] 下拉式清單選取使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="673e7-129">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="673e7-130">**選擇性：**按一下 [檢視和編輯所有其他使用者屬性]，以編輯當使用者登入時要以 SAML 權杖傳送至應用程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="673e7-130">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="673e7-131">新增屬性：</span><span class="sxs-lookup"><span data-stu-id="673e7-131">To add an attribute:</span></span>

   1. <span data-ttu-id="673e7-132">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="673e7-132">click **Add attribute**.</span></span> <span data-ttu-id="673e7-133">輸入 [名稱]，然後從下拉式清單選取 [值]。</span><span class="sxs-lookup"><span data-stu-id="673e7-133">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="673e7-134">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="673e7-134">Click **Save.**</span></span> <span data-ttu-id="673e7-135">您會在資料表中看到新屬性。</span><span class="sxs-lookup"><span data-stu-id="673e7-135">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="673e7-136">按一下 [設定 &lt;應用程式名稱&gt;]，以存取如何在應用程式中設定單一登入的文件。</span><span class="sxs-lookup"><span data-stu-id="673e7-136">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="673e7-137">此外，您有應用程式所需的 Azure AD URL 與憑證。</span><span class="sxs-lookup"><span data-stu-id="673e7-137">Also, you has Azure AD URLs and certificate required for the application.</span></span>

15. <span data-ttu-id="673e7-138">[將使用者指派給應用程式](#assign-users-to-the-application)。</span><span class="sxs-lookup"><span data-stu-id="673e7-138">[Assign users to the application.](#assign-users-to-the-application)</span></span>

## <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="673e7-139">選取使用者識別碼並新增要傳送到應用程式的使用者屬性</span><span class="sxs-lookup"><span data-stu-id="673e7-139">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="673e7-140">若要選取使用者識別碼或新增使用者屬性，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="673e7-140">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="673e7-141">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="673e7-141">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="673e7-142">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="673e7-142">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="673e7-143">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="673e7-143">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="673e7-144">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="673e7-144">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="673e7-145">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="673e7-145">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="673e7-146">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="673e7-146">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="673e7-147">選取您已設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="673e7-147">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="673e7-148">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="673e7-148">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="673e7-149">在 [使用者屬性] 區段下，從 [使用者識別碼] 下拉式清單選取使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="673e7-149">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="673e7-150">所選的選項必須符合應用程式中預期的值，才能驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="673e7-150">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

 ><span data-ttu-id="673e7-151">[!NOTE} Azure AD 會根據應用程式在 SAML AuthRequest 中選取的值或要求的格式，來選取 NameID 屬性 (使用者識別碼) 的格式。</span><span class="sxs-lookup"><span data-stu-id="673e7-151">[!NOTE} Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="673e7-152">如需詳細資訊，請參閱[單一登入 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)文章中的＜NameIDPolicy＞一節。</span><span class="sxs-lookup"><span data-stu-id="673e7-152">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
 >
 >

9.  <span data-ttu-id="673e7-153">若要新增使用者屬性，按一下 [檢視和編輯所有其他使用者屬性]，以編輯當使用者登入時要以 SAML 權杖傳送至應用程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="673e7-153">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="673e7-154">新增屬性：</span><span class="sxs-lookup"><span data-stu-id="673e7-154">To add an attribute:</span></span>

   1. <span data-ttu-id="673e7-155">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="673e7-155">click **Add attribute**.</span></span> <span data-ttu-id="673e7-156">輸入 [名稱]，然後從下拉式清單選取 [值]。</span><span class="sxs-lookup"><span data-stu-id="673e7-156">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="673e7-157">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="673e7-157">Click **Save.**</span></span> <span data-ttu-id="673e7-158">您會在資料表中看到新屬性。</span><span class="sxs-lookup"><span data-stu-id="673e7-158">You see the new attribute in the table.</span></span>

## <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="673e7-159">下載 Azure AD 中繼資料或憑證</span><span class="sxs-lookup"><span data-stu-id="673e7-159">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="673e7-160">若要從 Azure AD 下載應用程式中繼資料或憑證，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="673e7-160">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="673e7-161">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="673e7-161">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="673e7-162">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="673e7-162">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="673e7-163">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="673e7-163">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="673e7-164">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="673e7-164">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="673e7-165">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="673e7-165">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="673e7-166">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="673e7-166">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="673e7-167">選取您已設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="673e7-167">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="673e7-168">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="673e7-168">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="673e7-169">移至 [SAML 簽署憑證] 區段，然後按一下 [下載] 資料行值。</span><span class="sxs-lookup"><span data-stu-id="673e7-169">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="673e7-170">根據應用程式設定單一登入時所需的項目，您會看到下載中繼資料 XML 或憑證的選項。</span><span class="sxs-lookup"><span data-stu-id="673e7-170">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="673e7-171">Azure AD 不提供取得中繼資料的 URL。</span><span class="sxs-lookup"><span data-stu-id="673e7-171">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="673e7-172">只能將中繼資料擷取為 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="673e7-172">The metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-to-the-application"></a><span data-ttu-id="673e7-173">將使用者指派給應用程式</span><span class="sxs-lookup"><span data-stu-id="673e7-173">Assign users to the application</span></span>

<span data-ttu-id="673e7-174">若要直接將一或多個使用者指派至應用程式，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="673e7-174">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="673e7-175">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="673e7-175">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="673e7-176">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="673e7-176">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="673e7-177">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="673e7-177">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="673e7-178">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="673e7-178">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="673e7-179">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="673e7-179">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="673e7-180">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="673e7-180">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="673e7-181">從清單中選取您想要指派使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="673e7-181">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="673e7-182">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="673e7-182">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="673e7-183">按一下 [使用者和群組] 清單頂端的 [新增] 按鈕，以開啟 [新增指派] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="673e7-183">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="673e7-184">從 [新增指派] 刀鋒視窗按一下 [使用者和群組] 選取器。</span><span class="sxs-lookup"><span data-stu-id="673e7-184">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="673e7-185">在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入您有興趣指派之使用者的**全名**或**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="673e7-185">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="673e7-186">將滑鼠停留在清單中的**使用者**上方，以顯示**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="673e7-186">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="673e7-187">按一下使用者設定檔照片或標誌旁邊的核取方塊，將使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="673e7-187">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="673e7-188">**選擇性︰**如果您想要**新增多位使用者**，請在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入另一個**全名**或**電子郵件地址**，然後按一下核取方塊，將此使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="673e7-188">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="673e7-189">當您完成選取使用者時，按一下 [選取] 按鈕，將他們新增到要指派至應用程式的使用者和群組清單。</span><span class="sxs-lookup"><span data-stu-id="673e7-189">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="673e7-190">**選擇性︰**按一下 [新增指派] 刀鋒視窗中的 [選取角色] 選取器，以選取要指派給您已選取使用者的角色。</span><span class="sxs-lookup"><span data-stu-id="673e7-190">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="673e7-191">按一下 [指派] 按鈕，將應用程式指派給選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="673e7-191">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="673e7-192">稍待片刻，您已選取的使用者就能夠使用解決方案描述一節所述的方法，啟動這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="673e7-192">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="673e7-193">自訂傳送至應用程式的 SAML 宣告</span><span class="sxs-lookup"><span data-stu-id="673e7-193">Customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="673e7-194">若要了解如何自訂傳送至應用程式的 SAML 屬性宣告，請參閱 [Azure Active Directory 中的宣告對應](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping)以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="673e7-194">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="673e7-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="673e7-195">Next steps</span></span>
[<span data-ttu-id="673e7-196">使用應用程式 Proxy 提供單一登入應用程式</span><span class="sxs-lookup"><span data-stu-id="673e7-196">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

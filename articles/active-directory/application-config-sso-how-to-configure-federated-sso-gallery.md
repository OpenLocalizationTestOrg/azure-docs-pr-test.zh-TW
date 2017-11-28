---
title: "如何為 Azure AD 資源庫應用程式設定同盟單一登入 | Microsoft Docs"
description: "如何為現有的 Azure AD 資源庫應用程式設定同盟單一登入，並使用教學課程快速開始使用"
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
ms.openlocfilehash: 1b1d00718981b2c7d11f5b88428d02e16dd0b34d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="70060-103">如何為 Azure AD 資源庫應用程式設定同盟單一登入</span><span class="sxs-lookup"><span data-stu-id="70060-103">How to configure federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="70060-104">Azure AD 資源庫中所有透過企業單一登入功能啟用的應用程式都提供逐步教學課程。</span><span class="sxs-lookup"><span data-stu-id="70060-104">All applications in the Azure AD gallery enabled with Enterprise single sign-on capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="70060-105">您可以存取[如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/)，以取得詳細的逐步指引。</span><span class="sxs-lookup"><span data-stu-id="70060-105">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for detailed step-by-step guidance.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="70060-106">所需步驟的概觀</span><span class="sxs-lookup"><span data-stu-id="70060-106">Overview of steps required</span></span>
<span data-ttu-id="70060-107">若要設定 Azure AD 資源庫中的應用程式，您必須：</span><span class="sxs-lookup"><span data-stu-id="70060-107">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="70060-108">從 Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="70060-108">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="70060-109">在 Azure AD 中設定應用程式的中繼資料值 (登入 URL、識別碼、回覆 URL)</span><span class="sxs-lookup"><span data-stu-id="70060-109">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="70060-110">選取使用者識別碼並新增要傳送到應用程式的使用者屬性</span><span class="sxs-lookup"><span data-stu-id="70060-110">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="70060-111">擷取 Azure AD 中繼資料與憑證</span><span class="sxs-lookup"><span data-stu-id="70060-111">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="70060-112">在應用程式中設定 Azure AD 中繼資料值 (登入 URL、簽發者、登出 URL 與憑證)</span><span class="sxs-lookup"><span data-stu-id="70060-112">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="70060-113">將使用者指派給應用程式</span><span class="sxs-lookup"><span data-stu-id="70060-113">Assign users to the application</span></span>](#assign-users-to-the-application)

## <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="70060-114">從 Azure AD 資源庫新增應用程式</span><span class="sxs-lookup"><span data-stu-id="70060-114">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="70060-115">若要從 Azure AD 資源庫新增應用程式，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="70060-115">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="70060-116">開啟 [Azure 入口網站](https://portal.azure.com)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="70060-116">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="70060-117">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="70060-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70060-118">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="70060-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70060-119">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="70060-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="70060-120">按一下 [企業應用程式] 刀鋒視窗右上角的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="70060-120">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="70060-121">在 [從資源庫新增] 區段的 [輸入名稱] 文字方塊中，輸入應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="70060-121">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="70060-122">選取您要設為單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="70060-122">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="70060-123">新增應用程式之前，您可以從 [名稱] 文字方塊變更其名稱。</span><span class="sxs-lookup"><span data-stu-id="70060-123">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="70060-124">按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="70060-124">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="70060-125">稍候片刻，您便能看見應用程式的設定刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="70060-125">After a short period of time, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="70060-126">從 Azure AD 資源庫為應用程式設定單一登入</span><span class="sxs-lookup"><span data-stu-id="70060-126">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="70060-127">若要設定應用程式使用單一登入，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="70060-127">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="70060-128">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="70060-128">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="70060-129">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="70060-129">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70060-130">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="70060-130">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70060-131">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="70060-131">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="70060-132">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="70060-132">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="70060-133">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="70060-133">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="70060-134">選取您要設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="70060-134">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="70060-135">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="70060-135">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="70060-136">從 [模式] 下拉式清單選取 [SAML 登入]。</span><span class="sxs-lookup"><span data-stu-id="70060-136">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="70060-137">在 [網域及 URL] 中輸入必要值。</span><span class="sxs-lookup"><span data-stu-id="70060-137">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="70060-138">這些值應從應用程式廠商處取得。</span><span class="sxs-lookup"><span data-stu-id="70060-138">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="70060-139">若要將應用程式設定為 SP 啟始的 SSO，則登入 URL 為必要值。</span><span class="sxs-lookup"><span data-stu-id="70060-139">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="70060-140">對於某些應用程式，識別碼也是必要值。</span><span class="sxs-lookup"><span data-stu-id="70060-140">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="70060-141">若要將應用程式設定為 IdP 啟始的單一登入，則 [登入 URL] 為必要值。</span><span class="sxs-lookup"><span data-stu-id="70060-141">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="70060-142">對於某些應用程式，識別碼也是必要值。</span><span class="sxs-lookup"><span data-stu-id="70060-142">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="70060-143">**選擇性：**如果您想要看到非必要值，請按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="70060-143">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="70060-144">在 [使用者屬性] 中，從 [使用者識別碼] 下拉式清單選取使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="70060-144">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="70060-145">**選擇性：**按一下 [檢視和編輯所有其他使用者屬性]，以編輯當使用者登入時要以 SAML 權杖傳送至應用程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="70060-145">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

  <span data-ttu-id="70060-146">新增屬性：</span><span class="sxs-lookup"><span data-stu-id="70060-146">To add an attribute:</span></span>
   
   1. <span data-ttu-id="70060-147">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="70060-147">click **Add attribute**.</span></span> <span data-ttu-id="70060-148">輸入 [名稱]，然後從下拉式清單選取 [值]。</span><span class="sxs-lookup"><span data-stu-id="70060-148">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   1. <span data-ttu-id="70060-149">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="70060-149">Click **Save.**</span></span> <span data-ttu-id="70060-150">您會在資料表中看到新屬性。</span><span class="sxs-lookup"><span data-stu-id="70060-150">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="70060-151">按一下 [設定 &lt;應用程式名稱&gt;]，以存取如何在應用程式中設定單一登入的文件。</span><span class="sxs-lookup"><span data-stu-id="70060-151">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="70060-152">此外，您會有透過該應用程式設定 SSO 所需的中繼資料 URL 與憑證。</span><span class="sxs-lookup"><span data-stu-id="70060-152">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="70060-153">按一下 [儲存] 儲存組態。</span><span class="sxs-lookup"><span data-stu-id="70060-153">Click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="70060-154">將使用者指派給應用程式。</span><span class="sxs-lookup"><span data-stu-id="70060-154">Assign users to the application.</span></span>

## <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="70060-155">選取使用者識別碼並新增要傳送到應用程式的使用者屬性</span><span class="sxs-lookup"><span data-stu-id="70060-155">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="70060-156">若要選取使用者識別碼或新增使用者屬性，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="70060-156">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="70060-157">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="70060-157">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="70060-158">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="70060-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70060-159">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="70060-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70060-160">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="70060-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="70060-161">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="70060-161">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="70060-162">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="70060-162">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="70060-163">選取您已設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="70060-163">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="70060-164">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="70060-164">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="70060-165">在 [使用者屬性] 區段下，從 [使用者識別碼] 下拉式清單選取使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="70060-165">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="70060-166">所選的選項必須符合應用程式中預期的值，才能驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="70060-166">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

  >[!NOTE] 
  ><span data-ttu-id="70060-167">Azure AD 會根據應用程式在 SAML AuthRequest 中選取的值或要求的格式，來選取 NameID 屬性 (使用者識別碼) 的格式。</span><span class="sxs-lookup"><span data-stu-id="70060-167">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="70060-168">如需詳細資訊，請參閱[單一登入 SAML 通訊協定](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest)文章中的＜NameIDPolicy＞一節。</span><span class="sxs-lookup"><span data-stu-id="70060-168">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
  >
  >

9.  <span data-ttu-id="70060-169">若要新增使用者屬性，按一下 [檢視和編輯所有其他使用者屬性]，以編輯當使用者登入時要以 SAML 權杖傳送至應用程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="70060-169">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="70060-170">新增屬性：</span><span class="sxs-lookup"><span data-stu-id="70060-170">To add an attribute:</span></span>
  
   1. <span data-ttu-id="70060-171">按一下 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="70060-171">click **Add attribute**.</span></span> <span data-ttu-id="70060-172">輸入**名稱**，然後從下拉式清單選取**值**。</span><span class="sxs-lookup"><span data-stu-id="70060-172">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="70060-173">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="70060-173">Click **Save**.</span></span> <span data-ttu-id="70060-174">您會在資料表中看到新屬性。</span><span class="sxs-lookup"><span data-stu-id="70060-174">You see the new attribute in the table.</span></span>

## <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="70060-175">下載 Azure AD 中繼資料或憑證</span><span class="sxs-lookup"><span data-stu-id="70060-175">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="70060-176">若要從 Azure AD 下載應用程式中繼資料或憑證，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="70060-176">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="70060-177">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**或**共同管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="70060-177">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="70060-178">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="70060-178">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70060-179">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="70060-179">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70060-180">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="70060-180">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="70060-181">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="70060-181">click **All Applications** to view a list of all your applications.</span></span>

  *  <span data-ttu-id="70060-182">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="70060-182">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications**.</span></span>

6.  <span data-ttu-id="70060-183">選取您已設定單一登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="70060-183">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="70060-184">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="70060-184">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="70060-185">移至 [SAML 簽署憑證] 區段，然後按一下 [下載] 資料行值。</span><span class="sxs-lookup"><span data-stu-id="70060-185">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="70060-186">根據應用程式設定單一登入時所需的項目，您會看到下載中繼資料 XML 或憑證的選項。</span><span class="sxs-lookup"><span data-stu-id="70060-186">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="70060-187">Azure AD 不提供取得中繼資料的 URL。</span><span class="sxs-lookup"><span data-stu-id="70060-187">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="70060-188">只能將中繼資料擷取為 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="70060-188">The metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-to-the-application"></a><span data-ttu-id="70060-189">將使用者指派給應用程式</span><span class="sxs-lookup"><span data-stu-id="70060-189">Assign users to the application</span></span>

<span data-ttu-id="70060-190">若要直接將一或多個使用者指派至應用程式，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="70060-190">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="70060-191">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="70060-191">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="70060-192">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="70060-192">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="70060-193">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="70060-193">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="70060-194">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="70060-194">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="70060-195">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="70060-195">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="70060-196">若在這裡沒看到您要顯示的應用程式，請使用 [所有應用程式清單] 頂端的 [篩選] 控制項，並將 [顯示] 選項設定為 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="70060-196">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="70060-197">從清單中選取您想要指派使用者的應用程式。</span><span class="sxs-lookup"><span data-stu-id="70060-197">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="70060-198">應用程式載入之後，按一下應用程式左邊瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="70060-198">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="70060-199">按一下 [使用者和群組] 清單頂端的 [新增] 按鈕，以開啟 [新增指派] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="70060-199">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="70060-200">從 [新增指派] 刀鋒視窗按一下 [使用者和群組] 選取器。</span><span class="sxs-lookup"><span data-stu-id="70060-200">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="70060-201">在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入您有興趣指派之使用者的**全名**或**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="70060-201">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="70060-202">將滑鼠停留在清單中的**使用者**上方，以顯示**核取方塊**。</span><span class="sxs-lookup"><span data-stu-id="70060-202">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="70060-203">按一下使用者設定檔照片或標誌旁邊的核取方塊，將使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="70060-203">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="70060-204">**選擇性︰**如果您想要**新增多位使用者**，請在 [依姓名或電子郵件地址搜尋] 搜尋方塊中，輸入另一個**全名**或**電子郵件地址**，然後按一下核取方塊，將此使用者新增至 [已選取] 清單。</span><span class="sxs-lookup"><span data-stu-id="70060-204">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="70060-205">當您完成選取使用者時，按一下 [選取] 按鈕，將他們新增到要指派至應用程式的使用者和群組清單。</span><span class="sxs-lookup"><span data-stu-id="70060-205">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="70060-206">**選擇性︰**按一下 [新增指派] 刀鋒視窗中的 [選取角色] 選取器，以選取要指派給您已選取使用者的角色。</span><span class="sxs-lookup"><span data-stu-id="70060-206">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="70060-207">按一下 [指派] 按鈕，將應用程式指派給選取的使用者。</span><span class="sxs-lookup"><span data-stu-id="70060-207">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="70060-208">稍待片刻，您已選取的使用者就能夠使用解決方案描述一節所述的方法，啟動這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="70060-208">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="70060-209">自訂傳送至應用程式的 SAML 宣告</span><span class="sxs-lookup"><span data-stu-id="70060-209">Customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="70060-210">若要了解如何自訂傳送至應用程式的 SAML 屬性宣告，請參閱 [Azure Active Directory 中的宣告對應](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping)以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="70060-210">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70060-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="70060-211">Next steps</span></span>
[<span data-ttu-id="70060-212">使用應用程式 Proxy 提供單一登入應用程式</span><span class="sxs-lookup"><span data-stu-id="70060-212">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)




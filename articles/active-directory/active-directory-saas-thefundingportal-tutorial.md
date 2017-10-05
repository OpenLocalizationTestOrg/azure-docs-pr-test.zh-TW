---
title: "教學課程：Azure Active Directory 與 The Funding Portal 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 The Funding Portal 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4663cc8a-976a-4c6c-b3b4-1e5df9b66744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: d0bfc793bb26c551f85706eaec857962a3415e1f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-the-funding-portal"></a><span data-ttu-id="310b3-103">教學課程：Azure Active Directory 與 The Funding Portal 整合</span><span class="sxs-lookup"><span data-stu-id="310b3-103">Tutorial: Azure Active Directory integration with The Funding Portal</span></span>

<span data-ttu-id="310b3-104">在本教學課程中，您將了解如何整合 The Funding Portal 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="310b3-104">In this tutorial, you learn how to integrate The Funding Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="310b3-105">將 The Funding Portal 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="310b3-105">Integrating The Funding Portal with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="310b3-106">您可以在 Azure AD 中控制可存取 The Funding Portal 的人員</span><span class="sxs-lookup"><span data-stu-id="310b3-106">You can control in Azure AD who has access to The Funding Portal</span></span>
- <span data-ttu-id="310b3-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 The Funding Portal (單一登入)</span><span class="sxs-lookup"><span data-stu-id="310b3-107">You can enable your users to automatically get signed-on to The Funding Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="310b3-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="310b3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="310b3-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="310b3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="310b3-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="310b3-110">Prerequisites</span></span>

<span data-ttu-id="310b3-111">若要設定與 The Funding Portal 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="310b3-111">To configure Azure AD integration with The Funding Portal, you need the following items:</span></span>

- <span data-ttu-id="310b3-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="310b3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="310b3-113">已啟用 The Funding Portal 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="310b3-113">A The Funding Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="310b3-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="310b3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="310b3-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="310b3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="310b3-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="310b3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="310b3-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="310b3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="310b3-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="310b3-118">Scenario description</span></span>
<span data-ttu-id="310b3-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="310b3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="310b3-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="310b3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="310b3-121">從資源庫新增 The Funding Portal</span><span class="sxs-lookup"><span data-stu-id="310b3-121">Adding The Funding Portal from the gallery</span></span>
2. <span data-ttu-id="310b3-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="310b3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-the-funding-portal-from-the-gallery"></a><span data-ttu-id="310b3-123">從資源庫新增 The Funding Portal</span><span class="sxs-lookup"><span data-stu-id="310b3-123">Adding The Funding Portal from the gallery</span></span>
<span data-ttu-id="310b3-124">若要設定將 The Funding Portal 整合到 Azure AD 中，您需要從資源庫將 The Funding Portal 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="310b3-124">To configure the integration of The Funding Portal into Azure AD, you need to add The Funding Portal from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="310b3-125">**若要從資源庫新增 The Funding Portal，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="310b3-125">**To add The Funding Portal from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="310b3-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="310b3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="310b3-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="310b3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="310b3-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="310b3-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="310b3-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="310b3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="310b3-133">在搜尋方塊中，輸入 **The Funding Portal**。</span><span class="sxs-lookup"><span data-stu-id="310b3-133">In the search box, type **The Funding Portal**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_search.png)

5. <span data-ttu-id="310b3-135">在結果窗格中，選取 [The Funding Portal]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="310b3-135">In the results panel, select **The Funding Portal**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="310b3-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="310b3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="310b3-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 The Funding Portal 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="310b3-138">In this section, you configure and test Azure AD single sign-on with The Funding Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="310b3-139">若要讓單一登入能夠運作，Azure AD 必須知道 The Funding Portal 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="310b3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in The Funding Portal is to a user in Azure AD.</span></span> <span data-ttu-id="310b3-140">換句話說，必須在 Azure AD 使用者與 The Funding Portal 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="310b3-140">In other words, a link relationship between an Azure AD user and the related user in The Funding Portal needs to be established.</span></span>

<span data-ttu-id="310b3-141">在 The Funding Portal 中，將 [Username] 的值指派為 Azure AD 中 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="310b3-141">In The Funding Portal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="310b3-142">若要搭配 The Funding Portal 來設定及測試 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="310b3-142">To configure and test Azure AD single sign-on with The Funding Portal, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="310b3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="310b3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="310b3-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="310b3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="310b3-145">**[建立 The Funding Portal 測試使用者](#creating-the-funding-portal-test-user)** - 使 The Funding Portal 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="310b3-145">**[Creating The Funding Portal test user](#creating-the-funding-portal-test-user)** - to have a counterpart of Britta Simon in The Funding Portal that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="310b3-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="310b3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="310b3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="310b3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="310b3-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="310b3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="310b3-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 The Funding Portal 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="310b3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your The Funding Portal application.</span></span>

<span data-ttu-id="310b3-150">**若要設定透過 The Funding Portal 使用 Azure AD 單一登入功能，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="310b3-150">**To configure Azure AD single sign-on with The Funding Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="310b3-151">在 Azure 入口網站的 [The Funding Portal] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="310b3-151">In the Azure portal, on the **The Funding Portal** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="310b3-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="310b3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_samlbase.png)

3. <span data-ttu-id="310b3-155">在 [The Funding Portal 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="310b3-155">On the **The Funding Portal Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_url.png)

    <span data-ttu-id="310b3-157">a.</span><span class="sxs-lookup"><span data-stu-id="310b3-157">a.</span></span> <span data-ttu-id="310b3-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<subdomain>.regenteducation.net/`</span><span class="sxs-lookup"><span data-stu-id="310b3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.regenteducation.net/`</span></span>

    <span data-ttu-id="310b3-159">b.</span><span class="sxs-lookup"><span data-stu-id="310b3-159">b.</span></span> <span data-ttu-id="310b3-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<subdomain>.regenteducation.net`</span><span class="sxs-lookup"><span data-stu-id="310b3-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.regenteducation.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="310b3-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="310b3-161">These values are not real.</span></span> <span data-ttu-id="310b3-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="310b3-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="310b3-163">請連絡 [The Funding Portal 客戶支援小組](mailto:info@regenteducation.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="310b3-163">Contact [The Funding Portal Client support team](mailto:info@regenteducation.com) to get these values.</span></span> 

4. <span data-ttu-id="310b3-164">The Funding Portal 應用程式預期 SAML 判斷提示會包含名為 "externalId1" 的屬性。</span><span class="sxs-lookup"><span data-stu-id="310b3-164">The Funding Portal application expects the SAML assertions to contain an attribute named "externalId1".</span></span> <span data-ttu-id="310b3-165">"externalId1" 的值應該是可辨識的 studentID。</span><span class="sxs-lookup"><span data-stu-id="310b3-165">The value of "externalId1" should be a recognized studentID.</span></span> <span data-ttu-id="310b3-166">請設定此應用程式的 "externalId1" 宣告。</span><span class="sxs-lookup"><span data-stu-id="310b3-166">Configure the "externalId1" claim for this application.</span></span> <span data-ttu-id="310b3-167">您可以從應用程式的 [使用者屬性] 管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="310b3-167">You can manage the values of these attributes from the **User Attributes** of the application.</span></span> <span data-ttu-id="310b3-168">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="310b3-168">The following screenshot shows an example for this.</span></span>

    ![設定單一登入](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_attribute.png)

5. <span data-ttu-id="310b3-170">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如圖所示設定 SAML 權杖屬性，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="310b3-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>

    | <span data-ttu-id="310b3-171">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="310b3-171">Attribute Name</span></span> | <span data-ttu-id="310b3-172">屬性值</span><span class="sxs-lookup"><span data-stu-id="310b3-172">Attribute Value</span></span> |
    | ------------------- | ---------------- |
    | <span data-ttu-id="310b3-173">externalId1</span><span class="sxs-lookup"><span data-stu-id="310b3-173">externalId1</span></span> | <span data-ttu-id="310b3-174">user.extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="310b3-174">user.extensionattribute1</span></span> |

    <span data-ttu-id="310b3-175">a.</span><span class="sxs-lookup"><span data-stu-id="310b3-175">a.</span></span> <span data-ttu-id="310b3-176">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="310b3-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_04.png)

    ![設定單一登入](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="310b3-179">b.</span><span class="sxs-lookup"><span data-stu-id="310b3-179">b.</span></span> <span data-ttu-id="310b3-180">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="310b3-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="310b3-181">c.</span><span class="sxs-lookup"><span data-stu-id="310b3-181">c.</span></span> <span data-ttu-id="310b3-182">從 [屬性值] 清單中，選取您想要用於實作的屬性。</span><span class="sxs-lookup"><span data-stu-id="310b3-182">From the **Attribute Value** list, select the attribute you want to use for your implementation.</span></span> <span data-ttu-id="310b3-183">例如，如果您已在 ExtensionAttribute1 中儲存 StudentID 值，則選取 user.extensionattribute1。</span><span class="sxs-lookup"><span data-stu-id="310b3-183">For example, if you have stored the StudentID value in the ExtensionAttribute1, then select user.extensionattribute1.</span></span>
    
    <span data-ttu-id="310b3-184">d.</span><span class="sxs-lookup"><span data-stu-id="310b3-184">d.</span></span> <span data-ttu-id="310b3-185">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="310b3-185">Click **Ok**.</span></span>
 
6. <span data-ttu-id="310b3-186">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="310b3-186">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_certificate.png) 

7. <span data-ttu-id="310b3-188">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="310b3-188">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="310b3-190">若要在 **The Funding Portal** 端設定單一登入，您必須將已下載的**中繼資料 XML** 傳送給 [The Funding Portal 支援小組](mailto:info@regenteducation.com)。</span><span class="sxs-lookup"><span data-stu-id="310b3-190">To configure single sign-on on **The Funding Portal** side, you need to send the downloaded **Metadata XML** to [The Funding Portal support team](mailto:info@regenteducation.com).</span></span> <span data-ttu-id="310b3-191">他們會進行此設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="310b3-191">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="310b3-192">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="310b3-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="310b3-193">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="310b3-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="310b3-194">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="310b3-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="310b3-195">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="310b3-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="310b3-196">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="310b3-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="310b3-198">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="310b3-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="310b3-199">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="310b3-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="310b3-201">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="310b3-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="310b3-203">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="310b3-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="310b3-205">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="310b3-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="310b3-207">a.</span><span class="sxs-lookup"><span data-stu-id="310b3-207">a.</span></span> <span data-ttu-id="310b3-208">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="310b3-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="310b3-209">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="310b3-209">b.</span></span> <span data-ttu-id="310b3-210">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="310b3-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="310b3-211">c.</span><span class="sxs-lookup"><span data-stu-id="310b3-211">c.</span></span> <span data-ttu-id="310b3-212">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="310b3-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="310b3-213">d.</span><span class="sxs-lookup"><span data-stu-id="310b3-213">d.</span></span> <span data-ttu-id="310b3-214">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="310b3-214">Click **Create**.</span></span>
 
### <a name="creating-the-funding-portal-test-user"></a><span data-ttu-id="310b3-215">建立 The Funding Portal 測試使用者</span><span class="sxs-lookup"><span data-stu-id="310b3-215">Creating The Funding Portal test user</span></span>

<span data-ttu-id="310b3-216">在本節中，您要在 The Funding Portal 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="310b3-216">In this section, you create a user called Britta Simon in The Funding Portal.</span></span> <span data-ttu-id="310b3-217">請與 [The Funding Portal 支援小組](mailto:info@regenteducation.com)合作，以新增測試使用者並啟用 SSO。</span><span class="sxs-lookup"><span data-stu-id="310b3-217">Work with [The Funding Portal support team](mailto:info@regenteducation.com) to add the test user and enable SSO.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="310b3-218">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="310b3-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="310b3-219">在本節中，您會將 The Funding Portal 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="310b3-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to The Funding Portal.</span></span>

![指派使用者][200] 

<span data-ttu-id="310b3-221">**若要將 Britta Simon 指派到 The Funding Portal，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="310b3-221">**To assign Britta Simon to The Funding Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="310b3-222">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="310b3-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="310b3-224">在應用程式清單中，選取 [The Funding Portal] 。</span><span class="sxs-lookup"><span data-stu-id="310b3-224">In the applications list, select **The Funding Portal**.</span></span>

    ![設定單一登入](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_app.png) 

3. <span data-ttu-id="310b3-226">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="310b3-226">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="310b3-228">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="310b3-228">Click **Add** button.</span></span> <span data-ttu-id="310b3-229">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="310b3-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="310b3-231">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="310b3-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="310b3-232">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="310b3-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="310b3-233">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="310b3-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="310b3-234">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="310b3-234">Testing single sign-on</span></span>

<span data-ttu-id="310b3-235">本節的目標是要使用存取面板來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="310b3-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="310b3-236">當您在存取面板中按一下 [The Funding Portal] 圖格時，應該會自動登入您的 The Funding Portal 應用程式。</span><span class="sxs-lookup"><span data-stu-id="310b3-236">When you click the The Funding Portal tile in the Access Panel, you should get automatically signed-on to your The Funding Portal application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="310b3-237">其他資源</span><span class="sxs-lookup"><span data-stu-id="310b3-237">Additional resources</span></span>

* [<span data-ttu-id="310b3-238">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="310b3-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="310b3-239">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="310b3-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_203.png


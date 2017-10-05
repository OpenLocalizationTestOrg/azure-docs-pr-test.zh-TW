---
title: "教學課程：Azure Active Directory 與 Learningpool Act 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Learningpool Act 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 51e8695f-31e1-4d09-8eb3-13241999d99f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 932f5f12c75299e532d3fa2c31f1805a7df30158
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learningpool-act"></a><span data-ttu-id="cfeca-103">教學課程：Azure Active Directory 與 Learningpool Act 整合</span><span class="sxs-lookup"><span data-stu-id="cfeca-103">Tutorial: Azure Active Directory integration with Learningpool Act</span></span>

<span data-ttu-id="cfeca-104">在本教學課程中，您將了解如何整合 Learningpool Act 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="cfeca-104">In this tutorial, you learn how to integrate Learningpool Act with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cfeca-105">Learningpool Act 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="cfeca-105">Integrating Learningpool Act with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cfeca-106">您可以在 Azure AD 中控制可存取 Learningpool Act 的人員</span><span class="sxs-lookup"><span data-stu-id="cfeca-106">You can control in Azure AD who has access to Learningpool Act</span></span>
- <span data-ttu-id="cfeca-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Learningpool Act (單一登入)</span><span class="sxs-lookup"><span data-stu-id="cfeca-107">You can enable your users to automatically get signed-on to Learningpool Act (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cfeca-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="cfeca-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cfeca-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="cfeca-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfeca-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="cfeca-110">Prerequisites</span></span>

<span data-ttu-id="cfeca-111">如要設定 Azure AD 與 Learningpool Act 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="cfeca-111">To configure Azure AD integration with Learningpool Act, you need the following items:</span></span>

- <span data-ttu-id="cfeca-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cfeca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cfeca-113">已啟用 Learningpool Act 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cfeca-113">A Learningpool Act single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cfeca-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="cfeca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cfeca-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="cfeca-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cfeca-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="cfeca-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cfeca-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="cfeca-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cfeca-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="cfeca-118">Scenario description</span></span>
<span data-ttu-id="cfeca-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cfeca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cfeca-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="cfeca-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cfeca-121">從資源庫新增 Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="cfeca-121">Adding Learningpool Act from the gallery</span></span>
2. <span data-ttu-id="cfeca-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cfeca-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learningpool-act-from-the-gallery"></a><span data-ttu-id="cfeca-123">從資源庫新增 Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="cfeca-123">Adding Learningpool Act from the gallery</span></span>
<span data-ttu-id="cfeca-124">若要設定將 Learningpool Act 整合到 Azure AD 中，您需要從資源庫將 Learningpool Act 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="cfeca-124">To configure the integration of Learningpool Act into Azure AD, you need to add Learningpool Act from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cfeca-125">**若要從資源庫新增 Learningpool Act，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="cfeca-125">**To add Learningpool Act from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cfeca-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="cfeca-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cfeca-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="cfeca-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cfeca-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="cfeca-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="cfeca-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cfeca-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="cfeca-133">在搜尋方塊中，輸入 **Learningpool Act**。</span><span class="sxs-lookup"><span data-stu-id="cfeca-133">In the search box, type **Learningpool Act**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_search.png)

5. <span data-ttu-id="cfeca-135">在結果窗格中，選取 [Learningpool Act]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="cfeca-135">In the results panel, select **Learningpool Act**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cfeca-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cfeca-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cfeca-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Learningpool Act 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cfeca-138">In this section, you configure and test Azure AD single sign-on with Learningpool Act based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cfeca-139">若要讓單一登入能夠運作，Azure AD 必須知道 Learningpool Act 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="cfeca-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learningpool Act is to a user in Azure AD.</span></span> <span data-ttu-id="cfeca-140">換句話說，必須在 Azure AD 使用者與 Learningpool Act 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="cfeca-140">In other words, a link relationship between an Azure AD user and the related user in Learningpool Act needs to be established.</span></span>

<span data-ttu-id="cfeca-141">在 Learningpool Act 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="cfeca-141">In Learningpool Act, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cfeca-142">若要設定及測試與 Learningpool Act 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="cfeca-142">To configure and test Azure AD single sign-on with Learningpool Act, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cfeca-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="cfeca-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cfeca-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cfeca-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cfeca-145">**[建立 Learningpool Act 測試使用者](#creating-a-learningpool-act-test-user)** - 使 Learningpool Act 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="cfeca-145">**[Creating a Learningpool Act test user](#creating-a-learningpool-act-test-user)** - to have a counterpart of Britta Simon in Learningpool Act that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cfeca-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cfeca-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cfeca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="cfeca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cfeca-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cfeca-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cfeca-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Learningpool Act 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="cfeca-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learningpool Act application.</span></span>

<span data-ttu-id="cfeca-150">**若要設定與 Learningpool Act 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="cfeca-150">**To configure Azure AD single sign-on with Learningpool Act, perform the following steps:**</span></span>

1. <span data-ttu-id="cfeca-151">在 Azure 入口網站的 [Learningpool Act] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="cfeca-151">In the Azure portal, on the **Learningpool Act** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="cfeca-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="cfeca-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_samlbase.png)

3. <span data-ttu-id="cfeca-155">在 [Learningpool Act 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cfeca-155">On the **Learningpool Act Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_url.png)

    <span data-ttu-id="cfeca-157">a.</span><span class="sxs-lookup"><span data-stu-id="cfeca-157">a.</span></span> <span data-ttu-id="cfeca-158">在 [登入 URL] 文字方塊中，輸入 URL：`https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span><span class="sxs-lookup"><span data-stu-id="cfeca-158">In the **Sign-on URL** textbox, type the URL: `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span></span>

    <span data-ttu-id="cfeca-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="cfeca-159">b.</span></span> <span data-ttu-id="cfeca-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="cfeca-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.Learningpool.com/shibboleth` |
    | `https://<subdomain>.preview.Learningpool.com/shibboleth` |

    > [!NOTE] 
    > <span data-ttu-id="cfeca-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="cfeca-161">These values are not real.</span></span> <span data-ttu-id="cfeca-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="cfeca-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cfeca-163">請連絡 [Learningpool Act 客戶支援小組](https://www.Learningpool.com/support)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="cfeca-163">Contact [Learningpool Act Client support team](https://www.Learningpool.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="cfeca-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="cfeca-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_certificate.png) 

5. <span data-ttu-id="cfeca-166">Learningpool Act 應用程式需要特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="cfeca-166">Learningpool Act application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="cfeca-167">請設定此應用程式的下列宣告。</span><span class="sxs-lookup"><span data-stu-id="cfeca-167">Please configure the following claims for this application.</span></span> <span data-ttu-id="cfeca-168">您可以從應用程式的 [屬性]  索引標籤來管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="cfeca-168">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="cfeca-169">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="cfeca-169">The following screenshot shows an example for this.</span></span> 

    ![設定單一登入](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_attribute.png) 

6. <span data-ttu-id="cfeca-171">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如圖所示設定 SAML 權杖屬性，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cfeca-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="cfeca-172">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="cfeca-172">Attribute Name</span></span> | <span data-ttu-id="cfeca-173">屬性值</span><span class="sxs-lookup"><span data-stu-id="cfeca-173">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="cfeca-174">urn:oid:1.2.840.113556.1.4.221</span><span class="sxs-lookup"><span data-stu-id="cfeca-174">urn:oid:1.2.840.113556.1.4.221</span></span> | <span data-ttu-id="cfeca-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="cfeca-175">user.userprincipalname</span></span> |
    | <span data-ttu-id="cfeca-176">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="cfeca-176">urn:oid:2.5.4.42</span></span> | <span data-ttu-id="cfeca-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="cfeca-177">user.givenname</span></span> |
    | <span data-ttu-id="cfeca-178">urn:oid:0.9.2342.19200300.100.1.3</span><span class="sxs-lookup"><span data-stu-id="cfeca-178">urn:oid:0.9.2342.19200300.100.1.3</span></span> | <span data-ttu-id="cfeca-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="cfeca-179">user.mail</span></span> |    
    | <span data-ttu-id="cfeca-180">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="cfeca-180">urn:oid:2.5.4.4</span></span> | <span data-ttu-id="cfeca-181">user.surname</span><span class="sxs-lookup"><span data-stu-id="cfeca-181">user.surname</span></span> |
    
    <span data-ttu-id="cfeca-182">a.</span><span class="sxs-lookup"><span data-stu-id="cfeca-182">a.</span></span> <span data-ttu-id="cfeca-183">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="cfeca-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_04.png)

    ![設定單一登入](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="cfeca-186">b.</span><span class="sxs-lookup"><span data-stu-id="cfeca-186">b.</span></span> <span data-ttu-id="cfeca-187">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="cfeca-187">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="cfeca-188">c.</span><span class="sxs-lookup"><span data-stu-id="cfeca-188">c.</span></span> <span data-ttu-id="cfeca-189">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="cfeca-189">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="cfeca-190">d.</span><span class="sxs-lookup"><span data-stu-id="cfeca-190">d.</span></span> <span data-ttu-id="cfeca-191">讓 [命名空間] 保持空白。</span><span class="sxs-lookup"><span data-stu-id="cfeca-191">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="cfeca-192">e.</span><span class="sxs-lookup"><span data-stu-id="cfeca-192">e.</span></span> <span data-ttu-id="cfeca-193">按一下 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="cfeca-193">Click **Ok**.</span></span>

7. <span data-ttu-id="cfeca-194">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="cfeca-194">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-Learningpool-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="cfeca-196">若要在 **Learningpool Act** 端設定單一登入，您必須將已下載的**中繼資料 XML** 傳送給 [Learningpool Act 支援小組](https://www.Learningpool.com/support)。</span><span class="sxs-lookup"><span data-stu-id="cfeca-196">To configure single sign-on on **Learningpool Act** side, you need to send the downloaded **Metadata XML** to [Learningpool Act support team](https://www.Learningpool.com/support).</span></span> <span data-ttu-id="cfeca-197">他們會進行此設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="cfeca-197">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="cfeca-198">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="cfeca-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cfeca-199">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="cfeca-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cfeca-200">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cfeca-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cfeca-201">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cfeca-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="cfeca-202">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="cfeca-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="cfeca-204">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="cfeca-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cfeca-205">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="cfeca-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cfeca-207">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="cfeca-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cfeca-209">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cfeca-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cfeca-211">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cfeca-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cfeca-213">a.</span><span class="sxs-lookup"><span data-stu-id="cfeca-213">a.</span></span> <span data-ttu-id="cfeca-214">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="cfeca-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cfeca-215">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="cfeca-215">b.</span></span> <span data-ttu-id="cfeca-216">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="cfeca-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cfeca-217">c.</span><span class="sxs-lookup"><span data-stu-id="cfeca-217">c.</span></span> <span data-ttu-id="cfeca-218">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="cfeca-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cfeca-219">d.</span><span class="sxs-lookup"><span data-stu-id="cfeca-219">d.</span></span> <span data-ttu-id="cfeca-220">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="cfeca-220">Click **Create**.</span></span>
 
### <a name="creating-a-learningpool-act-test-user"></a><span data-ttu-id="cfeca-221">建立 Learningpool Act 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cfeca-221">Creating a Learningpool Act test user</span></span>

<span data-ttu-id="cfeca-222">若要讓 Azure AD 使用者能夠登入 Learningpool Act，則必須將他們佈建到 Learningpool Act。</span><span class="sxs-lookup"><span data-stu-id="cfeca-222">To enable Azure AD users to log in to Learningpool Act, they must be provisioned into Learningpool Act.</span></span>

<span data-ttu-id="cfeca-223">沒有動作項目可讓您設定 Learningpool Act 使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="cfeca-223">There is no action item for you to configure user provisioning to Learningpool Act.</span></span>  
<span data-ttu-id="cfeca-224">使用者必須由您的 [Learningpool Act 支援小組](https://www.Learningpool.com/support)建立。</span><span class="sxs-lookup"><span data-stu-id="cfeca-224">Users need to be created by your [Learningpool Act support team](https://www.Learningpool.com/support).</span></span>

>[!NOTE]
><span data-ttu-id="cfeca-225">您可以使用任何其他的 Learningpool Act 使用者帳戶建立工具或 Learningpool Act 提供的 API，佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="cfeca-225">You can use any other Learningpool Act user account creation tools or APIs provided by Learningpool Act to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cfeca-226">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cfeca-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cfeca-227">在本節中，您會將 Learningpool Act 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cfeca-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learningpool Act.</span></span>

![指派使用者][200] 

<span data-ttu-id="cfeca-229">**若要將 Britta Simon 指派到 Learningpool Act，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="cfeca-229">**To assign Britta Simon to Learningpool Act, perform the following steps:**</span></span>

1. <span data-ttu-id="cfeca-230">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="cfeca-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="cfeca-232">在應用程式清單中，選取 [Learningpool Act]。</span><span class="sxs-lookup"><span data-stu-id="cfeca-232">In the applications list, select **Learningpool Act**.</span></span>

    ![設定單一登入](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_app.png) 

3. <span data-ttu-id="cfeca-234">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="cfeca-234">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="cfeca-236">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cfeca-236">Click **Add** button.</span></span> <span data-ttu-id="cfeca-237">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="cfeca-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="cfeca-239">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="cfeca-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cfeca-240">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cfeca-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cfeca-241">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cfeca-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cfeca-242">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="cfeca-242">Testing single sign-on</span></span>

<span data-ttu-id="cfeca-243">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="cfeca-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cfeca-244">當您在存取面板中按一下 [Learningpool Act] 圖格時，應該會自動登入您的 Learningpool Act 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cfeca-244">When you click the Learningpool Act tile in the Access Panel, you should get automatically signed-on to your Learningpool Act application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cfeca-245">其他資源</span><span class="sxs-lookup"><span data-stu-id="cfeca-245">Additional resources</span></span>

* [<span data-ttu-id="cfeca-246">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="cfeca-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cfeca-247">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="cfeca-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_203.png


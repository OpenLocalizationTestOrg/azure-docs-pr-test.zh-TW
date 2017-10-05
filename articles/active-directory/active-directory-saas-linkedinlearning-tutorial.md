---
title: "教學課程：Azure Active Directory 與 LinkedIn Learning 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 LinkedIn Learning 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 6ad28cb3adaa63ddc3d3769a650d26ca6a7e2695
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="e6844-103">教學課程：Azure Active Directory 與 LinkedIn Learning 整合</span><span class="sxs-lookup"><span data-stu-id="e6844-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="e6844-104">在本教學課程中，您將了解如何整合 LinkedIn Learning 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="e6844-104">In this tutorial, you learn how to integrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e6844-105">LinkedIn Learning 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="e6844-105">Integrating LinkedIn Learning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e6844-106">您可以在 Azure AD 中控制可存取 LinkedIn Learning 的人員</span><span class="sxs-lookup"><span data-stu-id="e6844-106">You can control in Azure AD who has access to LinkedIn Learning</span></span>
- <span data-ttu-id="e6844-107">您可以讓使用者利用自己的 Azure AD 帳戶，來自動登入 LinkedIn Learning (單一登入)</span><span class="sxs-lookup"><span data-stu-id="e6844-107">You can enable your users to automatically get signed-on to LinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e6844-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="e6844-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e6844-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="e6844-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6844-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="e6844-110">Prerequisites</span></span>

<span data-ttu-id="e6844-111">如要設定 Azure AD 與 LinkedIn Learning 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="e6844-111">To configure Azure AD integration with LinkedIn Learning, you need the following items:</span></span>

- <span data-ttu-id="e6844-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e6844-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e6844-113">已啟用 LinkedIn Learning 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e6844-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e6844-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e6844-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e6844-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="e6844-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e6844-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e6844-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e6844-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="e6844-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e6844-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="e6844-118">Scenario description</span></span>
<span data-ttu-id="e6844-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6844-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e6844-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="e6844-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e6844-121">從資源庫新增 LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="e6844-121">Adding LinkedIn Learning from the gallery</span></span>
2. <span data-ttu-id="e6844-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e6844-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-the-gallery"></a><span data-ttu-id="e6844-123">從資源庫新增 LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="e6844-123">Adding LinkedIn Learning from the gallery</span></span>
<span data-ttu-id="e6844-124">如要設定將 LinkedIn Learning 整合到 Azure AD 中，您需要從資源庫中將 LinkedIn Learning 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="e6844-124">To configure the integration of LinkedIn Learning into Azure AD, you need to add LinkedIn Learning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e6844-125">**若要從資源庫新增 LinkedIn Learning，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e6844-125">**To add LinkedIn Learning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e6844-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e6844-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e6844-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e6844-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e6844-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e6844-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="e6844-131">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6844-131">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="e6844-133">在搜尋方塊中，輸入 **LinkedIn Learning**。</span><span class="sxs-lookup"><span data-stu-id="e6844-133">In the search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="e6844-134">從結果面板中，按一下 [LinkedIn Learning] 以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="e6844-134">From results panel, click **LinkedIn Learning** to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e6844-136">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e6844-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e6844-137">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 LinkedIn Learning 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6844-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e6844-138">若要讓單一登入能夠運作，Azure AD 必須知道 LinkedIn Learning 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="e6844-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Learning is to a user in Azure AD.</span></span> <span data-ttu-id="e6844-139">換句話說，必須要建立某位 Azure AD 使用者與 LinkedIn Learning 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e6844-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Learning needs to be established.</span></span>

<span data-ttu-id="e6844-140">建立此連結關聯性的方法是將 Azure AD 中**使用者名稱**的值，指派為 LinkedIn Learning 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="e6844-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="e6844-141">若要設定及測試與 LinkedIn Learning 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="e6844-141">To configure and test Azure AD single sign-on with LinkedIn Learning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e6844-142">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="e6844-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e6844-143">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6844-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e6844-144">**[建立 LinkedIn Learning 測試使用者](#creating-a-linkedin-learning-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6844-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="e6844-145">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6844-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e6844-146">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="e6844-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e6844-147">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e6844-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e6844-148">在本節中，您將在 Azure 入口網站中啟用 Azure AD 單一登入，並在 LinkedIn Learning 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6844-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="e6844-149">**如要設定搭配 LinkedIn Learning 的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e6844-149">**To configure Azure AD single sign-on with LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="e6844-150">在 Azure 入口網站的 [LinkedIn Learning] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="e6844-150">In the Azure portal, on the **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="e6844-152">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6844-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="e6844-154">在不同的網頁瀏覽器視窗中，以管理員身分登入您的 LinkedIn Learning 租用戶。</span><span class="sxs-lookup"><span data-stu-id="e6844-154">In a different web browser window, sign-on to your LinkedIn Learning tenant as an administrator.</span></span>

4. <span data-ttu-id="e6844-155">在 [帳戶中心] 中，按一下 [設定] 底下的 [全域設定]。</span><span class="sxs-lookup"><span data-stu-id="e6844-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="e6844-156">此外，從下拉式清單選取 [學習 - 預設]。</span><span class="sxs-lookup"><span data-stu-id="e6844-156">Also, select **Learning - Default** from the dropdown list.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="e6844-158">按一下 [或按一下這裡以從表單載入和複製個別欄位]，並複製 [實體識別碼] 和 [判斷提示取用者存取 (ACS) URL]</span><span class="sxs-lookup"><span data-stu-id="e6844-158">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="e6844-160">如果您想要在 [IdP 起始] 模式下設定 SSO，請在 Azure 入口網站的 [LinkedIn Learning 網域和 URL] 下方執行下列步驟</span><span class="sxs-lookup"><span data-stu-id="e6844-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="e6844-162">a.</span><span class="sxs-lookup"><span data-stu-id="e6844-162">a.</span></span> <span data-ttu-id="e6844-163">在 [識別碼] 文字方塊中，輸入從 LinkedIn 入口網站複製的 [實體 ID]</span><span class="sxs-lookup"><span data-stu-id="e6844-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="e6844-164">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e6844-164">b.</span></span> <span data-ttu-id="e6844-165">在 [回覆 URL] 文字方塊中，輸入從 LinkedIn 入口網站複製的 [判斷提示取用者存取 (ACS) URL]</span><span class="sxs-lookup"><span data-stu-id="e6844-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="e6844-166">如果您想要在 [SP 起始] 下設定 SSO，請按一下 [設定] 區段中的 [顯示進階 URL 設定] 選項，然後以下列模式設定登入 URL：</span><span class="sxs-lookup"><span data-stu-id="e6844-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign-on URL with the following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. <span data-ttu-id="e6844-168">LinkedIn Learning 應用程式需要特定格式的 SAML 判斷提示，要求您將自訂屬性對應新增到您的 SAML 權杖屬性組態。</span><span class="sxs-lookup"><span data-stu-id="e6844-168">Your LinkedIn Learning application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="e6844-169">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="e6844-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="e6844-170">[使用者識別碼] 的預設值是 **user.userprincipalname**，但是 LinkedIn Learning 預期它是與使用者電子郵件地址對應的值。</span><span class="sxs-lookup"><span data-stu-id="e6844-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="e6844-171">對此您可以使用清單中的 **user.mail** 屬性，或者根據組織組態使用適當的屬性值。</span><span class="sxs-lookup"><span data-stu-id="e6844-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. <span data-ttu-id="e6844-173">在 [使用者屬性] 區段中，按一下 [檢視及編輯所有其他使用者屬性]，然後設定屬性。</span><span class="sxs-lookup"><span data-stu-id="e6844-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="e6844-174">使用者需要新增名稱為 **email**、**department**、**firstname** 和 **lastname** 的四個宣告，而且值必須分別與 **user.mail**、**user.department**、**user.givenname** 和 **user.surname** 對應</span><span class="sxs-lookup"><span data-stu-id="e6844-174">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="e6844-175">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="e6844-175">Attribute Name</span></span> | <span data-ttu-id="e6844-176">屬性值</span><span class="sxs-lookup"><span data-stu-id="e6844-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="e6844-177">電子郵件</span><span class="sxs-lookup"><span data-stu-id="e6844-177">email</span></span>| <span data-ttu-id="e6844-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="e6844-178">user.mail</span></span> |    
    | <span data-ttu-id="e6844-179">department</span><span class="sxs-lookup"><span data-stu-id="e6844-179">department</span></span>| <span data-ttu-id="e6844-180">user.department</span><span class="sxs-lookup"><span data-stu-id="e6844-180">user.department</span></span> |
    | <span data-ttu-id="e6844-181">firstname</span><span class="sxs-lookup"><span data-stu-id="e6844-181">firstname</span></span>| <span data-ttu-id="e6844-182">user.givenname</span><span class="sxs-lookup"><span data-stu-id="e6844-182">user.givenname</span></span> |
    | <span data-ttu-id="e6844-183">lastname</span><span class="sxs-lookup"><span data-stu-id="e6844-183">lastname</span></span>| <span data-ttu-id="e6844-184">user.surname</span><span class="sxs-lookup"><span data-stu-id="e6844-184">user.surname</span></span> |
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    <span data-ttu-id="e6844-186">a.</span><span class="sxs-lookup"><span data-stu-id="e6844-186">a.</span></span> <span data-ttu-id="e6844-187">按一下 [新增屬性] 以開啟 [屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="e6844-187">Click **Add Attribute** to open the attribute dialog.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="e6844-190">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e6844-190">b.</span></span> <span data-ttu-id="e6844-191">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="e6844-191">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="e6844-192">c.</span><span class="sxs-lookup"><span data-stu-id="e6844-192">c.</span></span> <span data-ttu-id="e6844-193">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="e6844-193">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="e6844-194">d.</span><span class="sxs-lookup"><span data-stu-id="e6844-194">d.</span></span> <span data-ttu-id="e6844-195">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e6844-195">Click **Ok**</span></span>

10. <span data-ttu-id="e6844-196">針對 **name** 屬性執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e6844-196">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="e6844-197">a.</span><span class="sxs-lookup"><span data-stu-id="e6844-197">a.</span></span> <span data-ttu-id="e6844-198">按一下該屬性，以開啟 [編輯屬性] 視窗。</span><span class="sxs-lookup"><span data-stu-id="e6844-198">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    <span data-ttu-id="e6844-200">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e6844-200">b.</span></span> <span data-ttu-id="e6844-201">刪除**命名空間**中的 URL 值。</span><span class="sxs-lookup"><span data-stu-id="e6844-201">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="e6844-202">c.</span><span class="sxs-lookup"><span data-stu-id="e6844-202">c.</span></span> <span data-ttu-id="e6844-203">按一下 [確定] 以儲存設定。</span><span class="sxs-lookup"><span data-stu-id="e6844-203">Click **Ok** to save the setting.</span></span>

11. <span data-ttu-id="e6844-204">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="e6844-204">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. <span data-ttu-id="e6844-206">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="e6844-206">Click **Save**.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="e6844-208">移至 [LinkedIn 系統管理員設定] 區段。</span><span class="sxs-lookup"><span data-stu-id="e6844-208">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="e6844-209">按一下 [上傳 XML 檔案] 選項，將您從 Azure 入口網站下載的 XML 檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="e6844-209">Upload the XML file you downloaded from the Azure portal by clicking the Upload XML file option.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="e6844-211">按一下 [開啟] 以啟用 SSO。</span><span class="sxs-lookup"><span data-stu-id="e6844-211">Click **On** to enable SSO.</span></span> <span data-ttu-id="e6844-212">SSO 狀態會從 [未連線] 變更為 [已連線]</span><span class="sxs-lookup"><span data-stu-id="e6844-212">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e6844-214">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e6844-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="e6844-215">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="e6844-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="e6844-217">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e6844-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e6844-218">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e6844-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e6844-220">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="e6844-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e6844-222">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e6844-222">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e6844-224">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e6844-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e6844-226">a.</span><span class="sxs-lookup"><span data-stu-id="e6844-226">a.</span></span> <span data-ttu-id="e6844-227">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="e6844-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e6844-228">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e6844-228">b.</span></span> <span data-ttu-id="e6844-229">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="e6844-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e6844-230">c.</span><span class="sxs-lookup"><span data-stu-id="e6844-230">c.</span></span> <span data-ttu-id="e6844-231">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="e6844-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e6844-232">d.</span><span class="sxs-lookup"><span data-stu-id="e6844-232">d.</span></span> <span data-ttu-id="e6844-233">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="e6844-233">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="e6844-234">建立 LinkedIn Learning 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e6844-234">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="e6844-235">Linked Learning 應用程式支援。</span><span class="sxs-lookup"><span data-stu-id="e6844-235">Linked Learning Application supports.</span></span> <span data-ttu-id="e6844-236">及時使用者佈建，以及在驗證之後，會在應用程式中建立使用者。</span><span class="sxs-lookup"><span data-stu-id="e6844-236">Just in time user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="e6844-237">在 LinkedIn Learning 入口網站的系統管理設定頁面上，將 [自動指派授權] 切換為作用中，以在佈建時啟用，這個動作也會將授權指派給使用者。</span><span class="sxs-lookup"><span data-stu-id="e6844-237">On the admin settings page on the LinkedIn Learning portal flip the switch **Automatically Assign licenses** to active to enable Just in time provisioning and this will also assign a license to the user.</span></span>
   
   ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e6844-239">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e6844-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e6844-240">在本節中，您將把 LinkedIn Learning 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6844-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Learning.</span></span>

![指派使用者][200] 

<span data-ttu-id="e6844-242">**若要將 Britta Simon 指派到 LinkedIn Learning，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e6844-242">**To assign Britta Simon to LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="e6844-243">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e6844-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="e6844-245">在應用程式清單中，選取 [LinkedIn Learning]。</span><span class="sxs-lookup"><span data-stu-id="e6844-245">In the applications list, select **LinkedIn Learning**.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. <span data-ttu-id="e6844-247">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e6844-247">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="e6844-249">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6844-249">Click **Add** button.</span></span> <span data-ttu-id="e6844-250">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e6844-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="e6844-252">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="e6844-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e6844-253">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6844-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e6844-254">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6844-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e6844-255">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="e6844-255">Testing single sign-on</span></span>

<span data-ttu-id="e6844-256">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="e6844-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e6844-257">當您在「存取面板」中按一下 LinkedIn Learning 圖格時，您應該會進入 Azure 登入頁面，成功登入之後，您應該會進入 LinkedIn Learning 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e6844-257">When you click the LinkedIn Learning tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e6844-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="e6844-258">Additional resources</span></span>

* [<span data-ttu-id="e6844-259">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="e6844-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e6844-260">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="e6844-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png
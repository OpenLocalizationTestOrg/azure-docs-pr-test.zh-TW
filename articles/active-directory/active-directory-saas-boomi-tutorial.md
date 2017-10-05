---
title: "教學課程：Azure Active Directory 與 Boomi 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Boomi 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 1121d22beddf73fd2109a4b410422f76dd37478e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a><span data-ttu-id="f1b38-103">教學課程：Azure Active Directory 與 Boomi 整合</span><span class="sxs-lookup"><span data-stu-id="f1b38-103">Tutorial: Azure Active Directory integration with Boomi</span></span>

<span data-ttu-id="f1b38-104">在本教學課程中，您會了解如何整合 Boomi 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="f1b38-104">In this tutorial, you learn how to integrate Boomi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f1b38-105">Boomi 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="f1b38-105">Integrating Boomi with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f1b38-106">您可以在 Azure AD 中控制可存取 Boomi 的人員</span><span class="sxs-lookup"><span data-stu-id="f1b38-106">You can control in Azure AD who has access to Boomi</span></span>
- <span data-ttu-id="f1b38-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Boomi (單一登入)</span><span class="sxs-lookup"><span data-stu-id="f1b38-107">You can enable your users to automatically get signed-on to Boomi (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f1b38-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="f1b38-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f1b38-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="f1b38-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1b38-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f1b38-110">Prerequisites</span></span>

<span data-ttu-id="f1b38-111">若要設定 Azure AD 與 Boomi 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="f1b38-111">To configure Azure AD integration with Boomi, you need the following items:</span></span>

- <span data-ttu-id="f1b38-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f1b38-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f1b38-113">啟用 Boomi 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f1b38-113">A Boomi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f1b38-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f1b38-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f1b38-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="f1b38-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f1b38-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f1b38-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f1b38-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="f1b38-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f1b38-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="f1b38-118">Scenario description</span></span>
<span data-ttu-id="f1b38-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f1b38-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f1b38-120">本教學課程中說明的案例由二項主要的基本工作組成：</span><span class="sxs-lookup"><span data-stu-id="f1b38-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f1b38-121">從資源庫新增 Boomi</span><span class="sxs-lookup"><span data-stu-id="f1b38-121">Adding Boomi from the gallery</span></span>
2. <span data-ttu-id="f1b38-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f1b38-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-boomi-from-the-gallery"></a><span data-ttu-id="f1b38-123">從資源庫新增 Boomi</span><span class="sxs-lookup"><span data-stu-id="f1b38-123">Adding Boomi from the gallery</span></span>
<span data-ttu-id="f1b38-124">若要設定將 Boomi 整合至 Azure AD 中，您需要從資源庫將 Boomi 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="f1b38-124">To configure the integration of Boomi into Azure AD, you need to add Boomi from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f1b38-125">**若要從資源庫新增 Boomi，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f1b38-125">**To add Boomi from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f1b38-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f1b38-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f1b38-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f1b38-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f1b38-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f1b38-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="f1b38-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f1b38-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="f1b38-133">在搜尋方塊中，輸入 **Boomi**。</span><span class="sxs-lookup"><span data-stu-id="f1b38-133">In the search box, type **Boomi**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. <span data-ttu-id="f1b38-135">在結果窗格中，選取 [Boomi]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1b38-135">In the results panel, select **Boomi**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f1b38-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f1b38-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f1b38-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Boomi 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f1b38-138">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f1b38-139">若要讓單一登入運作，Azure AD 必須知道 Boomi 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="f1b38-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Boomi is to a user in Azure AD.</span></span> <span data-ttu-id="f1b38-140">換句話說，必須建立 Azure AD 使用者和 Boomi 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f1b38-140">In other words, a link relationship between an Azure AD user and the related user in Boomi needs to be established.</span></span>

<span data-ttu-id="f1b38-141">在 BeeLine 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f1b38-141">In Boomi, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f1b38-142">若要設定及測試與 Boomi 搭配運作的 Azure AD 單一登入，您需要完成下列基本工作：</span><span class="sxs-lookup"><span data-stu-id="f1b38-142">To configure and test Azure AD single sign-on with Boomi, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f1b38-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="f1b38-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f1b38-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f1b38-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f1b38-145">**[建立 Boomi 測試使用者](#creating-a-boomi-test-user)** - 讓 Britta Simon 在 Boomi 中有一個對應項目連結至使用者的 Azure AD 代表身分。</span><span class="sxs-lookup"><span data-stu-id="f1b38-145">**[Creating a Boomi test user](#creating-a-boomi-test-user)** - to have a counterpart of Britta Simon in Boomi that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f1b38-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f1b38-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f1b38-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="f1b38-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f1b38-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f1b38-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f1b38-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Boomi 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="f1b38-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Boomi application.</span></span>

<span data-ttu-id="f1b38-150">**若要設定與 Boomi 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f1b38-150">**To configure Azure AD single sign-on with Boomi, perform the following steps:**</span></span>

1. <span data-ttu-id="f1b38-151">在 Azure 入口網站的 [Boomi] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="f1b38-151">In the Azure portal, on the **Boomi** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="f1b38-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="f1b38-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. <span data-ttu-id="f1b38-155">在 [Boomi 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f1b38-155">On the **Boomi Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    <span data-ttu-id="f1b38-157">a.</span><span class="sxs-lookup"><span data-stu-id="f1b38-157">a.</span></span> <span data-ttu-id="f1b38-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="f1b38-158">In the **Identifier** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    <span data-ttu-id="f1b38-159">b.</span><span class="sxs-lookup"><span data-stu-id="f1b38-159">b.</span></span> <span data-ttu-id="f1b38-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="f1b38-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f1b38-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="f1b38-161">These values are not real.</span></span> <span data-ttu-id="f1b38-162">請使用實際的識別碼和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="f1b38-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="f1b38-163">請連絡 [Boomi 支援小組](https://boomi.com/company/contact/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="f1b38-163">Contact [Boomi support team](https://boomi.com/company/contact/) to get these values.</span></span>

4. <span data-ttu-id="f1b38-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="f1b38-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. <span data-ttu-id="f1b38-166">Boomi 應用程式需要特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="f1b38-166">Boomi application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="f1b38-167">請設定此應用程式的下列宣告。</span><span class="sxs-lookup"><span data-stu-id="f1b38-167">Please configure the following claims for this application.</span></span> <span data-ttu-id="f1b38-168">您可以在應用程式整合頁面的 [使用者屬性] 區段中管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="f1b38-168">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="f1b38-169">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="f1b38-169">The following screenshot shows an example for this.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="f1b38-171">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，針對下表顯示的每一列執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f1b38-171">In the **User Attributes** section on the **Single sign-on** dialog, for each row shown in the table below, perform the following steps:</span></span>

    | <span data-ttu-id="f1b38-172">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="f1b38-172">Attribute Name</span></span> | <span data-ttu-id="f1b38-173">屬性值</span><span class="sxs-lookup"><span data-stu-id="f1b38-173">Attribute Value</span></span> |
    | -------------- | --------------- |
    | <span data-ttu-id="f1b38-174">FEDERATION_ID</span><span class="sxs-lookup"><span data-stu-id="f1b38-174">FEDERATION_ID</span></span> | <span data-ttu-id="f1b38-175">user.mail</span><span class="sxs-lookup"><span data-stu-id="f1b38-175">user.mail</span></span> |
    
    <span data-ttu-id="f1b38-176">a.</span><span class="sxs-lookup"><span data-stu-id="f1b38-176">a.</span></span> <span data-ttu-id="f1b38-177">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f1b38-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![設定單一登入](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="f1b38-180">b.</span><span class="sxs-lookup"><span data-stu-id="f1b38-180">b.</span></span> <span data-ttu-id="f1b38-181">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="f1b38-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="f1b38-182">c.</span><span class="sxs-lookup"><span data-stu-id="f1b38-182">c.</span></span> <span data-ttu-id="f1b38-183">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="f1b38-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="f1b38-184">d.</span><span class="sxs-lookup"><span data-stu-id="f1b38-184">d.</span></span> <span data-ttu-id="f1b38-185">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f1b38-185">Click **Ok**.</span></span>

6. <span data-ttu-id="f1b38-186">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="f1b38-186">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f1b38-188">在 [Boomi 組態] 區段上，按一下 [設定 Boomi] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="f1b38-188">On the **Boomi Configuration** section, click **Configure Boomi** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f1b38-189">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="f1b38-189">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. <span data-ttu-id="f1b38-191">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Boomi 公司網站。</span><span class="sxs-lookup"><span data-stu-id="f1b38-191">In a different web browser window, log into your Boomi company site as an administrator.</span></span> 

9. <span data-ttu-id="f1b38-192">瀏覽至 [公司名稱]，並移至 [設定]。</span><span class="sxs-lookup"><span data-stu-id="f1b38-192">Navigate to **Company Name** and go to **Set up**.</span></span>

10. <span data-ttu-id="f1b38-193">按一下 [SSO 選項] 索引標籤並執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="f1b38-193">Click the **SSO Options** tab and perform below steps.</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    <span data-ttu-id="f1b38-195">a.</span><span class="sxs-lookup"><span data-stu-id="f1b38-195">a.</span></span> <span data-ttu-id="f1b38-196">選取 [啟用 SAML 單一登入] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="f1b38-196">Check **Enable SAML Single Sign-On** checkbox.</span></span>

    <span data-ttu-id="f1b38-197">b.</span><span class="sxs-lookup"><span data-stu-id="f1b38-197">b.</span></span> <span data-ttu-id="f1b38-198">按一下 [匯入]，將已從 Azure AD 下載的憑證上傳至**識別提供者憑證**。</span><span class="sxs-lookup"><span data-stu-id="f1b38-198">Click **Import** to upload the downloaded certificate from Azure AD to **Identity Provider Certificate**.</span></span>
    
    <span data-ttu-id="f1b38-199">c.</span><span class="sxs-lookup"><span data-stu-id="f1b38-199">c.</span></span> <span data-ttu-id="f1b38-200">在 [識別提供者登入 URL] 文字方塊中，放入來自 Azure AD 應用程式組態視窗的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="f1b38-200">In the **Identity Provider Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="f1b38-201">d.</span><span class="sxs-lookup"><span data-stu-id="f1b38-201">d.</span></span> <span data-ttu-id="f1b38-202">針對 [同盟識別碼位置]，選取 [同盟識別碼位於 FEDERATION_ID 屬性元素] 選項按鈕。</span><span class="sxs-lookup"><span data-stu-id="f1b38-202">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span></span> 

    <span data-ttu-id="f1b38-203">e.</span><span class="sxs-lookup"><span data-stu-id="f1b38-203">e.</span></span> <span data-ttu-id="f1b38-204">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="f1b38-204">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="f1b38-205">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="f1b38-205">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f1b38-206">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="f1b38-206">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f1b38-207">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f1b38-207">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f1b38-208">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f1b38-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="f1b38-209">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="f1b38-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="f1b38-211">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f1b38-211">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f1b38-212">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f1b38-212">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f1b38-214">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="f1b38-214">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f1b38-216">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f1b38-216">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f1b38-218">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f1b38-218">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f1b38-220">a.</span><span class="sxs-lookup"><span data-stu-id="f1b38-220">a.</span></span> <span data-ttu-id="f1b38-221">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="f1b38-221">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f1b38-222">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1b38-222">b.</span></span> <span data-ttu-id="f1b38-223">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="f1b38-223">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f1b38-224">c.</span><span class="sxs-lookup"><span data-stu-id="f1b38-224">c.</span></span> <span data-ttu-id="f1b38-225">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="f1b38-225">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f1b38-226">d.</span><span class="sxs-lookup"><span data-stu-id="f1b38-226">d.</span></span> <span data-ttu-id="f1b38-227">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f1b38-227">Click **Create**.</span></span>
 
### <a name="creating-a-boomi-test-user"></a><span data-ttu-id="f1b38-228">建立 Boomi 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f1b38-228">Creating a Boomi test user</span></span>

<span data-ttu-id="f1b38-229">若要讓 Azure AD 使用者可以登入 Boomi，必須將他們佈建到 Boomi。</span><span class="sxs-lookup"><span data-stu-id="f1b38-229">In order to enable Azure AD users to log in to Boomi, they must be provisioned into Boomi.</span></span> <span data-ttu-id="f1b38-230">Boomi 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="f1b38-230">In the case of Boomi, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="f1b38-231">若要佈建使用者帳戶，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f1b38-231">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="f1b38-232">以系統管理員身分登入您的 Boomi 公司網站。</span><span class="sxs-lookup"><span data-stu-id="f1b38-232">Log in to your Boomi company site as an administrator.</span></span>

2. <span data-ttu-id="f1b38-233">登入之後，瀏覽至 [使用者管理]，然後移至 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="f1b38-233">After logging in, navigate to **User Management** and go to **Users**.</span></span>

    <span data-ttu-id="f1b38-234">![使用者](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="f1b38-234">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")</span></span>

3. <span data-ttu-id="f1b38-235">按一下 **+** 圖示，[新增/維護使用者角色] 對話方塊隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="f1b38-235">Click **+**  icon and the **Add/Maintain User Roles** dialog opens.</span></span>

    <span data-ttu-id="f1b38-236">![使用者](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="f1b38-236">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")</span></span>

    <span data-ttu-id="f1b38-237">![使用者](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="f1b38-237">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")</span></span>

    <span data-ttu-id="f1b38-238">a.</span><span class="sxs-lookup"><span data-stu-id="f1b38-238">a.</span></span> <span data-ttu-id="f1b38-239">在 [使用者電子郵件地址] 文字方塊中，輸入像是 BrittaSimon@contoso.com 的使用者電子郵件。</span><span class="sxs-lookup"><span data-stu-id="f1b38-239">In the **User e-mail address** textbox, type the email of user like BrittaSimon@contoso.com.</span></span>
    
    <span data-ttu-id="f1b38-240">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1b38-240">b.</span></span> <span data-ttu-id="f1b38-241">在 [名字] 文字方塊中，輸入使用者的名字，例如 Britta。</span><span class="sxs-lookup"><span data-stu-id="f1b38-241">In the **First name** textbox, type the First name of user like Britta.</span></span>

    <span data-ttu-id="f1b38-242">c.</span><span class="sxs-lookup"><span data-stu-id="f1b38-242">c.</span></span> <span data-ttu-id="f1b38-243">在 [姓氏] 文字方塊中，輸入使用者的姓氏，例如 Simon。</span><span class="sxs-lookup"><span data-stu-id="f1b38-243">In the **Last name** textbox, type the Last name of user like Simon.</span></span>
    
    <span data-ttu-id="f1b38-244">d.</span><span class="sxs-lookup"><span data-stu-id="f1b38-244">d.</span></span> <span data-ttu-id="f1b38-245">輸入使用者的 [同盟識別碼]。</span><span class="sxs-lookup"><span data-stu-id="f1b38-245">Enter the user's **Federation ID**.</span></span> <span data-ttu-id="f1b38-246">每位使用者必須有同盟識別碼，以唯一地識別帳戶內的使用者。</span><span class="sxs-lookup"><span data-stu-id="f1b38-246">Each user must have a Federation ID that uniquely identifies the user within the account.</span></span>
    
    <span data-ttu-id="f1b38-247">e.</span><span class="sxs-lookup"><span data-stu-id="f1b38-247">e.</span></span> <span data-ttu-id="f1b38-248">指派 [標準使用者] 角色給使用者。</span><span class="sxs-lookup"><span data-stu-id="f1b38-248">Assign the **Standard User** role to the user.</span></span> <span data-ttu-id="f1b38-249">請勿指派系統管理員角色，因為這樣他會取得正常 Atmosphere 存取權和單一登入存取權。</span><span class="sxs-lookup"><span data-stu-id="f1b38-249">Do not assign the Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span></span>
    
    <span data-ttu-id="f1b38-250">f.</span><span class="sxs-lookup"><span data-stu-id="f1b38-250">f.</span></span> <span data-ttu-id="f1b38-251">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f1b38-251">Click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="f1b38-252">使用者的密碼是透過識別提供者來管理，他不會收到附上 AtomSphere 帳戶登入密碼的歡迎通知電子郵件。</span><span class="sxs-lookup"><span data-stu-id="f1b38-252">The user will not receive a welcome notification email containing a password that can be used to log in to the AtomSphere account because his password is managed through the identity provider.</span></span> <span data-ttu-id="f1b38-253">您可以使用任何其他的 Boomi 使用者帳戶建立工具或 Boomi 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="f1b38-253">You may use any other Boomi user account creation tools or APIs provided by Boomi to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f1b38-254">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f1b38-254">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f1b38-255">在本節中，您會將 Boomi 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f1b38-255">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Boomi.</span></span>

![指派使用者][200] 

<span data-ttu-id="f1b38-257">**若要將 Britta Simon 指派至 Boomi，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f1b38-257">**To assign Britta Simon to Boomi, perform the following steps:**</span></span>

1. <span data-ttu-id="f1b38-258">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f1b38-258">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="f1b38-260">在應用程式清單中，選取 [Boomi]。</span><span class="sxs-lookup"><span data-stu-id="f1b38-260">In the applications list, select **Boomi**.</span></span>

    ![設定單一登入](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. <span data-ttu-id="f1b38-262">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f1b38-262">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="f1b38-264">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f1b38-264">Click **Add** button.</span></span> <span data-ttu-id="f1b38-265">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f1b38-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="f1b38-267">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="f1b38-267">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f1b38-268">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f1b38-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f1b38-269">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f1b38-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f1b38-270">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="f1b38-270">Testing single sign-on</span></span>

<span data-ttu-id="f1b38-271">在本節中，您會使用「存取面板」來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="f1b38-271">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f1b38-272">當您在「存取面板」中按一下 [Boomi] 圖格時，應該會自動登入您的 Boomi 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f1b38-272">When you click the Boomi tile in the Access Panel, you should get automatically signed-on to your Boomi application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f1b38-273">其他資源</span><span class="sxs-lookup"><span data-stu-id="f1b38-273">Additional resources</span></span>

* [<span data-ttu-id="f1b38-274">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="f1b38-274">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f1b38-275">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="f1b38-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png


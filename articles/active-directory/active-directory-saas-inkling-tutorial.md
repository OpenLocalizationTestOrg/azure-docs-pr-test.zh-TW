---
title: "教學課程：Azure Active Directory 與 Inkling 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Inkling 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 64c7ee45-ee8a-42f7-bf04-fd0e00833ea9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 7b0639c6515298731f88346c2e4ca82664653a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-inkling"></a><span data-ttu-id="2a09c-103">教學課程：Azure Active Directory 與 Inkling 整合</span><span class="sxs-lookup"><span data-stu-id="2a09c-103">Tutorial: Azure Active Directory integration with Inkling</span></span>

<span data-ttu-id="2a09c-104">在本教學課程中，您將了解如何整合 Inkling 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="2a09c-104">In this tutorial, you learn how to integrate Inkling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2a09c-105">Inkling 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="2a09c-105">Integrating Inkling with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2a09c-106">您可以在 Azure AD 中控制可存取 Inkling 的人員</span><span class="sxs-lookup"><span data-stu-id="2a09c-106">You can control in Azure AD who has access to Inkling</span></span>
- <span data-ttu-id="2a09c-107">您可以讓使用者透過其 Azure AD 帳戶自動登入 Inkling (單一登入)</span><span class="sxs-lookup"><span data-stu-id="2a09c-107">You can enable your users to automatically get signed-on to Inkling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2a09c-108">您可以在 Azure 管理入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="2a09c-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="2a09c-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="2a09c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a09c-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="2a09c-110">Prerequisites</span></span>

<span data-ttu-id="2a09c-111">若要設定 Azure AD 與 Inkling 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="2a09c-111">To configure Azure AD integration with Inkling, you need the following items:</span></span>

- <span data-ttu-id="2a09c-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="2a09c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2a09c-113">已啟用 Inkling 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="2a09c-113">An Inkling single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="2a09c-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="2a09c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="2a09c-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="2a09c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2a09c-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="2a09c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2a09c-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="2a09c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="2a09c-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="2a09c-118">Scenario description</span></span>
<span data-ttu-id="2a09c-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="2a09c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2a09c-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="2a09c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2a09c-121">從資源庫新增 Inkling</span><span class="sxs-lookup"><span data-stu-id="2a09c-121">Adding Inkling from the gallery</span></span>
2. <span data-ttu-id="2a09c-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="2a09c-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-inkling-from-the-gallery"></a><span data-ttu-id="2a09c-123">從資源庫新增 Inkling</span><span class="sxs-lookup"><span data-stu-id="2a09c-123">Adding Inkling from the gallery</span></span>
<span data-ttu-id="2a09c-124">若要設定將 Inkling 整合到 Azure AD 中，您需要從資源庫將 Inkling 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="2a09c-124">To configure the integration of Inkling into Azure AD, you need to add Inkling from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2a09c-125">**若要從資源庫新增 Inkling，執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="2a09c-125">**To add Inkling from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2a09c-126">在 **[Azure 管理入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="2a09c-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2a09c-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="2a09c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2a09c-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="2a09c-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="2a09c-131">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2a09c-131">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="2a09c-133">在搜尋方塊中，輸入 **Inkling**。</span><span class="sxs-lookup"><span data-stu-id="2a09c-133">In the search box, type **Inkling**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_001.png)

5. <span data-ttu-id="2a09c-135">在結果窗格中，選取 [Inkling]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="2a09c-135">In the results panel, select **Inkling**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2a09c-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="2a09c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2a09c-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Inkling 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="2a09c-138">In this section, you configure and test Azure AD single sign-on with Inkling based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2a09c-139">若要讓單一登入能夠運作，Azure AD 必須知道 Inkling 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="2a09c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Inkling is to a user in Azure AD.</span></span> <span data-ttu-id="2a09c-140">換句話說，必須建立 Azure AD 使用者和 Inkling 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="2a09c-140">In other words, a link relationship between an Azure AD user and the related user in Inkling needs to be established.</span></span>

<span data-ttu-id="2a09c-141">建立此連結關聯性的方法，就是指派 Azure AD 中**使用者名稱**的值做為 Inkling 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="2a09c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Inkling.</span></span>

<span data-ttu-id="2a09c-142">若要設定及測試與 Inkling 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="2a09c-142">To configure and test Azure AD single sign-on with Inkling, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2a09c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="2a09c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2a09c-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="2a09c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2a09c-145">**[建立 Inkling 測試使用者](#creating-an-inkling-test-user)** - 在 Inkling 中建立 Britta Simon 的對應項目，且該項目必須與 Azure AD 中代表 Britta Simon 的項目連結。</span><span class="sxs-lookup"><span data-stu-id="2a09c-145">**[Creating an Inkling test user](#creating-an-inkling-test-user)** - to have a counterpart of Britta Simon in Inkling that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="2a09c-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="2a09c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2a09c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="2a09c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2a09c-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="2a09c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2a09c-149">在本節中，您會在 Azure 管理入口網站中啟用 Azure AD 單一登入，並在您的 Inkling 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="2a09c-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Inkling application.</span></span>

<span data-ttu-id="2a09c-150">**若要使用 Inkling 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="2a09c-150">**To configure Azure AD single sign-on with Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="2a09c-151">在 Azure 管理入口網站的 [Inkling] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="2a09c-151">In the Azure Management portal, on the **Inkling** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="2a09c-153">在 [單一登入] 對話方塊上，選取 [SAML 型登入] 做為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="2a09c-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-inkling-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="2a09c-155">在 [Inkling 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2a09c-155">On the **Inkling Domain and URLs** section, perform the following steps:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_01.png)

    <span data-ttu-id="2a09c-157">a.</span><span class="sxs-lookup"><span data-stu-id="2a09c-157">a.</span></span> <span data-ttu-id="2a09c-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://api.inkling.com/saml/v2/metadata/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="2a09c-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span></span>

    <span data-ttu-id="2a09c-159">b.</span><span class="sxs-lookup"><span data-stu-id="2a09c-159">b.</span></span> <span data-ttu-id="2a09c-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://api.inkling.com/saml/v2/acs/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="2a09c-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/acs/<user-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2a09c-161">請注意這些不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="2a09c-161">Please note that these are not the real values.</span></span> <span data-ttu-id="2a09c-162">您必須使用實際的識別碼和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="2a09c-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="2a09c-163">請連絡 [Inkling 支援小組](mailto:press@inkling.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="2a09c-163">Contact [Inkling support team](mailto:press@inkling.com) to get these values.</span></span>

4. <span data-ttu-id="2a09c-164">在 [SAML 簽署憑證] 區段上，按一下 [建立新憑證]。</span><span class="sxs-lookup"><span data-stu-id="2a09c-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![設定單一登入](./media/active-directory-saas-inkling-tutorial/tutorial_general_400.png)    

5. <span data-ttu-id="2a09c-166">在 [建立新憑證] 對話方塊中，按一下行事曆圖示並選取 [到期日]。</span><span class="sxs-lookup"><span data-stu-id="2a09c-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="2a09c-167">然後按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2a09c-167">Then click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-inkling-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="2a09c-169">在 [SAML 簽署憑證] 區段中，選取 [啟用新憑證] 並按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2a09c-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_02.png)

7. <span data-ttu-id="2a09c-171">在 [變換憑證] 快顯視窗上，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2a09c-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![設定單一登入](./media/active-directory-saas-inkling-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="2a09c-173">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="2a09c-173">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_03.png) 

9. <span data-ttu-id="2a09c-175">若要為您的應用程式設定 SSO，請連絡 [Inkling 支援小組](mailto:press@inkling.com)並提供所下載的「中繼資料」。</span><span class="sxs-lookup"><span data-stu-id="2a09c-175">To get SSO configured for your application, contact [Inkling support team](mailto:press@inkling.com) and provide them with downloaded **metadata**.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2a09c-176">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="2a09c-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="2a09c-177">本節目標是在 Azure 管理入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="2a09c-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="2a09c-179">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="2a09c-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2a09c-180">在 **Azure 管理入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="2a09c-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-inkling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2a09c-182">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="2a09c-182">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-inkling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2a09c-184">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="2a09c-184">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-inkling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2a09c-186">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2a09c-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-inkling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2a09c-188">a.</span><span class="sxs-lookup"><span data-stu-id="2a09c-188">a.</span></span> <span data-ttu-id="2a09c-189">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="2a09c-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2a09c-190">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="2a09c-190">b.</span></span> <span data-ttu-id="2a09c-191">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="2a09c-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2a09c-192">c.</span><span class="sxs-lookup"><span data-stu-id="2a09c-192">c.</span></span> <span data-ttu-id="2a09c-193">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="2a09c-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2a09c-194">d.</span><span class="sxs-lookup"><span data-stu-id="2a09c-194">d.</span></span> <span data-ttu-id="2a09c-195">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="2a09c-195">Click **Create**.</span></span> 



### <a name="creating-an-inkling-test-user"></a><span data-ttu-id="2a09c-196">建立 Inkling 測試使用者</span><span class="sxs-lookup"><span data-stu-id="2a09c-196">Creating an Inkling test user</span></span>

<span data-ttu-id="2a09c-197">在本節中，您要在 Inkling 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="2a09c-197">In this section, you create a user called Britta Simon in Inkling.</span></span> <span data-ttu-id="2a09c-198">請與 [Inkling 支援小組](mailto:press@inkling.com)合作，在 Inkling 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="2a09c-198">Please work with [Inkling support team](mailto:press@inkling.com) to add the users in the Inkling platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2a09c-199">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="2a09c-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2a09c-200">在本節中，您會將 Inkling 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="2a09c-200">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Inkling.</span></span>

![指派使用者][200] 

<span data-ttu-id="2a09c-202">**若要將 Britta Simon 指派至 Inkling，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="2a09c-202">**To assign Britta Simon to Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="2a09c-203">在 Azure 管理入口網站中，開啟應用程式檢視，然後瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="2a09c-203">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="2a09c-205">在應用程式清單中，選取 [Inkling] 。</span><span class="sxs-lookup"><span data-stu-id="2a09c-205">In the applications list, select **Inkling**.</span></span>

    ![設定單一登入](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_50.png) 

3. <span data-ttu-id="2a09c-207">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="2a09c-207">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="2a09c-209">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2a09c-209">Click **Add** button.</span></span> <span data-ttu-id="2a09c-210">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="2a09c-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="2a09c-212">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="2a09c-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2a09c-213">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2a09c-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2a09c-214">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2a09c-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="2a09c-215">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="2a09c-215">Testing single sign-on</span></span>

<span data-ttu-id="2a09c-216">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="2a09c-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2a09c-217">當您在存取面板中按一下 [Inkling] 圖格時，應該會自動登入您的 Inkling 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2a09c-217">When you click the Inkling tile in the Access Panel, you should get automatically signed-on to your Inkling application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2a09c-218">其他資源</span><span class="sxs-lookup"><span data-stu-id="2a09c-218">Additional resources</span></span>

* [<span data-ttu-id="2a09c-219">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="2a09c-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2a09c-220">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="2a09c-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_203.png
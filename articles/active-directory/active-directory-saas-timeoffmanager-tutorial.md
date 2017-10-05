---
title: "教學課程：Azure Active Directory 與 TimeOffManager 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 TimeOffManager 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 3f944ffbf704694b293b4b1e5bdb4f2c93ae35a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a><span data-ttu-id="e1f28-103">教學課程：Azure Active Directory 與 TimeOffManager 整合</span><span class="sxs-lookup"><span data-stu-id="e1f28-103">Tutorial: Azure Active Directory integration with TimeOffManager</span></span>

<span data-ttu-id="e1f28-104">在本教學課程中，您將了解如何整合 TimeOffManager 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="e1f28-104">In this tutorial, you learn how to integrate TimeOffManager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1f28-105">TimeOffManager 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="e1f28-105">Integrating TimeOffManager with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e1f28-106">您可以在 Azure AD 中管控可存取 TimeOffManager 的人員</span><span class="sxs-lookup"><span data-stu-id="e1f28-106">You can control in Azure AD who has access to TimeOffManager</span></span>
- <span data-ttu-id="e1f28-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 TimeOffManager (單一登入)</span><span class="sxs-lookup"><span data-stu-id="e1f28-107">You can enable your users to automatically get signed-on to TimeOffManager (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e1f28-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="e1f28-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e1f28-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="e1f28-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1f28-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="e1f28-110">Prerequisites</span></span>

<span data-ttu-id="e1f28-111">若要設定 Azure AD 與 TimeOffManager 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="e1f28-111">To configure Azure AD integration with TimeOffManager, you need the following items:</span></span>

- <span data-ttu-id="e1f28-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e1f28-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e1f28-113">啟用 TimeOffManager 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e1f28-113">A TimeOffManager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e1f28-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e1f28-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e1f28-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="e1f28-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e1f28-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e1f28-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e1f28-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="e1f28-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e1f28-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="e1f28-118">Scenario description</span></span>
<span data-ttu-id="e1f28-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e1f28-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e1f28-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="e1f28-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e1f28-121">從資源庫新增 TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="e1f28-121">Add TimeOffManager from the gallery</span></span>
2. <span data-ttu-id="e1f28-122">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e1f28-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-timeoffmanager-from-the-gallery"></a><span data-ttu-id="e1f28-123">從資源庫新增 TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="e1f28-123">Add TimeOffManager from the gallery</span></span>
<span data-ttu-id="e1f28-124">若要設定將 TimeOffManager 整合到 Azure AD 中，您需要從資源庫將 TimeOffManager 新增到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="e1f28-124">To configure the integration of TimeOffManager into Azure AD, you need to add TimeOffManager from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e1f28-125">**若要從資源庫新增 TimeOffManager，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e1f28-125">**To add TimeOffManager from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e1f28-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e1f28-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e1f28-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e1f28-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e1f28-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e1f28-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="e1f28-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e1f28-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="e1f28-133">在搜尋方塊中，輸入 **TimeOffManager**，從結果面板中選取 [TimeOffManager]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1f28-133">In the search box, type **TimeOffManager**, select **TimeOffManager** from result panel and then click **Add** button to add the application.</span></span>

    ![從資源庫新增](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e1f28-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e1f28-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="e1f28-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 TimeOffManager 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e1f28-136">In this section, you configure and test Azure AD single sign-on with TimeOffManager based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e1f28-137">若要讓單一登入能夠運作，Azure AD 必須知道 TimeOffManager 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="e1f28-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TimeOffManager is to a user in Azure AD.</span></span> <span data-ttu-id="e1f28-138">換句話說，必須在 Azure AD 使用者和 TimeOffManager 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e1f28-138">In other words, a link relationship between an Azure AD user and the related user in TimeOffManager needs to be established.</span></span>

<span data-ttu-id="e1f28-139">在 TimeOffManager 中，將 Azure AD 中 [使用者名稱] 的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e1f28-139">In TimeOffManager, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e1f28-140">若要使用 TimeOffManager 來設定並測試 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="e1f28-140">To configure and test Azure AD single sign-on with TimeOffManager, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e1f28-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="e1f28-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e1f28-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e1f28-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e1f28-143">**[建立 TimeOffManager 測試使用者](#create-a-timeoffmanager-test-user)** - 使 TimeOffManager 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="e1f28-143">**[Create a TimeOffManager test user](#create-a-timeoffmanager-test-user)** - to have a counterpart of Britta Simon in TimeOffManager that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e1f28-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e1f28-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e1f28-145">**[測試單一登入](#test-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="e1f28-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e1f28-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e1f28-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e1f28-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 TimeOffManager 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="e1f28-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TimeOffManager application.</span></span>

<span data-ttu-id="e1f28-148">**若要使用 TimeOffManager 設定 Azure AD 單一登入功能，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e1f28-148">**To configure Azure AD single sign-on with TimeOffManager, perform the following steps:**</span></span>

1. <span data-ttu-id="e1f28-149">在 Azure 入口網站的 [TimeOffManager] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="e1f28-149">In the Azure portal, on the **TimeOffManager** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="e1f28-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="e1f28-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML 型登入](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. <span data-ttu-id="e1f28-153">在 [TimeOffManager 網域與 URL] 區段中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="e1f28-153">On the **TimeOffManager Domain and URLs** section, perform the following:</span></span>

     ![[TimeOffManager 網域與 URL] 區段](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    <span data-ttu-id="e1f28-155">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span><span class="sxs-lookup"><span data-stu-id="e1f28-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e1f28-156">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="e1f28-156">This value is not real.</span></span> <span data-ttu-id="e1f28-157">請使用實際的「回覆 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="e1f28-157">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="e1f28-158">您可以從 [單一登入設定] 頁面取得此值，稍後會在本教學課程中加以說明，或連絡 [TimeOffManager 支援小組](http://www.timeoffmanager.com/contact-us.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e1f28-158">You can get this value from **Single Sign on settings page** which is explained later in the tutorial or Contact [TimeOffManager support team](http://www.timeoffmanager.com/contact-us.aspx).</span></span>
 
4. <span data-ttu-id="e1f28-159">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="e1f28-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![[SAML 簽署憑證] 區段](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. <span data-ttu-id="e1f28-161">本節的目的是要說明如何依據 SAML 通訊協定來使用同盟，讓使用者能夠用自己在 Azure AD 中的帳戶驗證至 TimeOffManger。</span><span class="sxs-lookup"><span data-stu-id="e1f28-161">The objective of this section is to outline how to enable users to authenticate to TimeOffManger with their account in Azure AD using federation based on the SAML protocol.</span></span>
    
    <span data-ttu-id="e1f28-162">您的 TimeOffManger 應用程式需要特定格式的 SAML 判斷提示，因此您必須將自訂屬性對應加入 SAML 權杖屬性設定。</span><span class="sxs-lookup"><span data-stu-id="e1f28-162">Your TimeOffManger application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="e1f28-163">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="e1f28-163">The following screenshot shows an example for this.</span></span>

    <span data-ttu-id="e1f28-164">![saml 權杖屬性](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml 權杖屬性")</span><span class="sxs-lookup"><span data-stu-id="e1f28-164">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span></span>
    
    | <span data-ttu-id="e1f28-165">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="e1f28-165">Attribute Name</span></span> | <span data-ttu-id="e1f28-166">屬性值</span><span class="sxs-lookup"><span data-stu-id="e1f28-166">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="e1f28-167">Firstname</span><span class="sxs-lookup"><span data-stu-id="e1f28-167">Firstname</span></span> |<span data-ttu-id="e1f28-168">User.givenname</span><span class="sxs-lookup"><span data-stu-id="e1f28-168">User.givenname</span></span> |
    | <span data-ttu-id="e1f28-169">lastname</span><span class="sxs-lookup"><span data-stu-id="e1f28-169">Lastname</span></span> |<span data-ttu-id="e1f28-170">User.surname</span><span class="sxs-lookup"><span data-stu-id="e1f28-170">User.surname</span></span> |
    | <span data-ttu-id="e1f28-171">電子郵件</span><span class="sxs-lookup"><span data-stu-id="e1f28-171">Email</span></span> |<span data-ttu-id="e1f28-172">User.mail</span><span class="sxs-lookup"><span data-stu-id="e1f28-172">User.mail</span></span> |
    
    <span data-ttu-id="e1f28-173">a.</span><span class="sxs-lookup"><span data-stu-id="e1f28-173">a.</span></span>  <span data-ttu-id="e1f28-174">針對上表中的每個資料列，按一下 [新增使用者屬性] 。</span><span class="sxs-lookup"><span data-stu-id="e1f28-174">For each data row in the table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="e1f28-175">![saml 權杖屬性](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml 權杖屬性")</span><span class="sxs-lookup"><span data-stu-id="e1f28-175">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span></span>
    
    <span data-ttu-id="e1f28-176">![saml 權杖屬性](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml 權杖屬性")</span><span class="sxs-lookup"><span data-stu-id="e1f28-176">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span></span>
    
    <span data-ttu-id="e1f28-177">b.</span><span class="sxs-lookup"><span data-stu-id="e1f28-177">b.</span></span>  <span data-ttu-id="e1f28-178">在 [屬性名稱]  文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="e1f28-178">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="e1f28-179">c.</span><span class="sxs-lookup"><span data-stu-id="e1f28-179">c.</span></span>  <span data-ttu-id="e1f28-180">在 [屬性值] 文字方塊中，選取該資料列所顯示的屬性值。</span><span class="sxs-lookup"><span data-stu-id="e1f28-180">In the **Attribute Value** textbox, select the attribute  value shown for that row.</span></span>
    
    <span data-ttu-id="e1f28-181">d.</span><span class="sxs-lookup"><span data-stu-id="e1f28-181">d.</span></span>  <span data-ttu-id="e1f28-182">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e1f28-182">Click **Ok**.</span></span>
    
6. <span data-ttu-id="e1f28-183">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e1f28-183">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="e1f28-185">在 [TimeOffManager 設定] 區段上，按一下 [設定 TimeOffManager] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="e1f28-185">On the **TimeOffManager Configuration** section, click **Configure TimeOffManager** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e1f28-186">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="e1f28-186">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![[TimeOffManager 設定] 區段](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. <span data-ttu-id="e1f28-188">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 TimeOffManager 公司網站。</span><span class="sxs-lookup"><span data-stu-id="e1f28-188">In a different web browser window, log into your TimeOffManager company site as an administrator.</span></span>

9. <span data-ttu-id="e1f28-189">移至 [帳戶] \> [帳戶選項] \> [單一登入設定]。</span><span class="sxs-lookup"><span data-stu-id="e1f28-189">Go to **Account \> Account Options \> Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="e1f28-190">![單一登入設定](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="e1f28-190">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span></span>
7. <span data-ttu-id="e1f28-191">在 [單一登入設定]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e1f28-191">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="e1f28-192">![單一登入設定](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="e1f28-192">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="e1f28-193">a.</span><span class="sxs-lookup"><span data-stu-id="e1f28-193">a.</span></span> <span data-ttu-id="e1f28-194">在記事本中開啟您的 base-64 編碼的憑證，將它的內容複製到您的剪貼簿，然後將整個憑證貼到 [X.509 憑證]  文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="e1f28-194">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>
   
   <span data-ttu-id="e1f28-195">b.</span><span class="sxs-lookup"><span data-stu-id="e1f28-195">b.</span></span> <span data-ttu-id="e1f28-196">在 [IdP 簽發者] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="e1f28-196">In **Idp Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="e1f28-197">c.</span><span class="sxs-lookup"><span data-stu-id="e1f28-197">c.</span></span> <span data-ttu-id="e1f28-198">在 [IdP 端點 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="e1f28-198">In **IdP Endpoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="e1f28-199">d.</span><span class="sxs-lookup"><span data-stu-id="e1f28-199">d.</span></span> <span data-ttu-id="e1f28-200">在 [強制 SAML] 選取 [否]。</span><span class="sxs-lookup"><span data-stu-id="e1f28-200">As **Enforce SAML**, select **No**.</span></span>
   
   <span data-ttu-id="e1f28-201">e.</span><span class="sxs-lookup"><span data-stu-id="e1f28-201">e.</span></span> <span data-ttu-id="e1f28-202">在 [自動建立使用者] 選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="e1f28-202">As **Auto-Create Users**, select **Yes**.</span></span>
   
   <span data-ttu-id="e1f28-203">f.</span><span class="sxs-lookup"><span data-stu-id="e1f28-203">f.</span></span> <span data-ttu-id="e1f28-204">在 [登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="e1f28-204">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="e1f28-205">g.</span><span class="sxs-lookup"><span data-stu-id="e1f28-205">g.</span></span> <span data-ttu-id="e1f28-206">按一下 [儲存變更]。</span><span class="sxs-lookup"><span data-stu-id="e1f28-206">click **Save Changes**.</span></span>

11. <span data-ttu-id="e1f28-207">在 [單一登入設定] 頁面中，複製 [判斷提示取用者服務 URL] 的值，並將其貼在 Azure 入口網站之 [TimeOffManager 網域與 URL] 區段下的 [回覆 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="e1f28-207">In **Single Sign on settings** page, copy the value of **Assertion Consumer Service URL** and paste it in the **Reply URL** text box under **TimeOffManager Domain and URLs** section in Azure portal.</span></span> 

      <span data-ttu-id="e1f28-208">![單一登入設定](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="e1f28-208">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span></span>

> [!TIP]
> <span data-ttu-id="e1f28-209">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="e1f28-209">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e1f28-210">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="e1f28-210">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e1f28-211">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e1f28-211">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e1f28-212">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e1f28-212">Create an Azure AD test user</span></span>
<span data-ttu-id="e1f28-213">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="e1f28-213">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="e1f28-215">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e1f28-215">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e1f28-216">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e1f28-216">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e1f28-218">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="e1f28-218">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![[使用者和群組] --> [所有使用者]](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e1f28-220">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e1f28-220">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![[新增] 按鈕](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e1f28-222">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e1f28-222">On the **User** dialog page, perform the following steps:</span></span>
 
    ![使用者對話方塊頁面](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e1f28-224">a.</span><span class="sxs-lookup"><span data-stu-id="e1f28-224">a.</span></span> <span data-ttu-id="e1f28-225">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="e1f28-225">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e1f28-226">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1f28-226">b.</span></span> <span data-ttu-id="e1f28-227">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="e1f28-227">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e1f28-228">c.</span><span class="sxs-lookup"><span data-stu-id="e1f28-228">c.</span></span> <span data-ttu-id="e1f28-229">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="e1f28-229">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e1f28-230">d.</span><span class="sxs-lookup"><span data-stu-id="e1f28-230">d.</span></span> <span data-ttu-id="e1f28-231">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="e1f28-231">Click **Create**.</span></span>
 
### <a name="create-a-timeoffmanager-test-user"></a><span data-ttu-id="e1f28-232">建立 TimeOffManager 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e1f28-232">Create a TimeOffManager test user</span></span>

<span data-ttu-id="e1f28-233">若要讓 Azure AD 使用者可以登入 TimeOffManager，則必須將他們佈建到 TimeOffManager。</span><span class="sxs-lookup"><span data-stu-id="e1f28-233">In order to enable Azure AD users to log into TimeOffManager, they must be provisioned to TimeOffManager.</span></span>  

<span data-ttu-id="e1f28-234">TimeOffManager 支援即時使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="e1f28-234">TimeOffManager supports just in time user provisioning.</span></span> <span data-ttu-id="e1f28-235">沒有您適用的動作項目。</span><span class="sxs-lookup"><span data-stu-id="e1f28-235">There is no action item for you.</span></span>  

<span data-ttu-id="e1f28-236">在第一次登入時使用單一登入，便會自動加入使用者。</span><span class="sxs-lookup"><span data-stu-id="e1f28-236">The users are added automatically during the first login using single sign on.</span></span>

>[!NOTE]
><span data-ttu-id="e1f28-237">您可以使用任何其他的 TimeOffManager 使用者帳戶建立工具或 TimeOffManager 提供的 API 來佈建 Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="e1f28-237">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager to provision Azure AD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e1f28-238">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e1f28-238">Assign the Azure AD test user</span></span>

<span data-ttu-id="e1f28-239">在本節中，您會把 TimeOffManager 的存取權授予 Britta Simon，讓 Britta Simon 能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e1f28-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TimeOffManager.</span></span>

![指派使用者][200] 

<span data-ttu-id="e1f28-241">**若要將 Britta Simon 指派給 TimeOffManager，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e1f28-241">**To assign Britta Simon to TimeOffManager, perform the following steps:**</span></span>

1. <span data-ttu-id="e1f28-242">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e1f28-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="e1f28-244">在應用程式清單中，選取 [TimeOffManager]。</span><span class="sxs-lookup"><span data-stu-id="e1f28-244">In the applications list, select **TimeOffManager**.</span></span>

    ![應用程式清單中的 TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. <span data-ttu-id="e1f28-246">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e1f28-246">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="e1f28-248">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e1f28-248">Click **Add** button.</span></span> <span data-ttu-id="e1f28-249">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e1f28-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="e1f28-251">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="e1f28-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e1f28-252">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e1f28-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e1f28-253">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e1f28-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e1f28-254">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="e1f28-254">Test single sign-on</span></span>

<span data-ttu-id="e1f28-255">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="e1f28-255">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e1f28-256">當您在存取面板中按一下 TimeOffManager 圖格時，應該會自動登入您的 TimeOffManager 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1f28-256">When you click the TimeOffManager tile in the Access Panel, you should get automatically signed-on to your TimeOffManager application.</span></span> <span data-ttu-id="e1f28-257">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="e1f28-257">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e1f28-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="e1f28-258">Additional resources</span></span>

* [<span data-ttu-id="e1f28-259">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="e1f28-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e1f28-260">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="e1f28-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png


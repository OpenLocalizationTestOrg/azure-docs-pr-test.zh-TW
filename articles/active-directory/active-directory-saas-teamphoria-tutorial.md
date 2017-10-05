---
title: "教學課程：Azure Active Directory 與 Teamphoria 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Teamphoria 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: 2a35efb04d7fe22abc6894c149caf090666ce016
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="27007-103">教學課程：Azure Active Directory 與 Teamphoria 整合</span><span class="sxs-lookup"><span data-stu-id="27007-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="27007-104">在本教學課程中，您會了解如何整合 Teamphoria 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="27007-104">In this tutorial, you learn how to integrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="27007-105">Teamphoria 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="27007-105">Integrating Teamphoria with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="27007-106">您可以在 Azure AD 中控制可存取 Teamphoria 的人員</span><span class="sxs-lookup"><span data-stu-id="27007-106">You can control in Azure AD who has access to Teamphoria</span></span>
- <span data-ttu-id="27007-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Teamphoria (單一登入)</span><span class="sxs-lookup"><span data-stu-id="27007-107">You can enable your users to automatically get signed-on to Teamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="27007-108">您可以在 Azure 管理入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="27007-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="27007-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="27007-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Teamphoria, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="27007-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="27007-110">Prerequisites</span></span>

<span data-ttu-id="27007-111">如要設定 Azure AD 與 Teamphoria 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="27007-111">To configure Azure AD integration with Teamphoria, you need the following items:</span></span>

- <span data-ttu-id="27007-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="27007-112">An Azure AD subscription</span></span>
- <span data-ttu-id="27007-113">一個已啟用 Teamphoria 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="27007-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="27007-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="27007-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="27007-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="27007-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="27007-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="27007-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="27007-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="27007-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="27007-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="27007-118">Scenario description</span></span>
<span data-ttu-id="27007-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="27007-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="27007-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="27007-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="27007-121">從資源庫新增 Teamphoria</span><span class="sxs-lookup"><span data-stu-id="27007-121">Adding Teamphoria from the gallery</span></span>
2. <span data-ttu-id="27007-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="27007-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-the-gallery"></a><span data-ttu-id="27007-123">從資源庫新增 Teamphoria</span><span class="sxs-lookup"><span data-stu-id="27007-123">Adding Teamphoria from the gallery</span></span>
<span data-ttu-id="27007-124">若要設定將 Teamphoria 整合到 Azure AD 中，您需要從資源庫將 Teamphoria 新增到受管理的 SaaS app 清單。</span><span class="sxs-lookup"><span data-stu-id="27007-124">To configure the integration of Teamphoria into Azure AD, you need to add Teamphoria from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="27007-125">**若要從資源庫新增 Teamphoria，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="27007-125">**To add Teamphoria from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="27007-126">在 **[Azure 管理入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="27007-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="27007-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="27007-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="27007-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="27007-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="27007-131">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="27007-131">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="27007-133">在搜尋方塊中，輸入 **Teamphoria**。</span><span class="sxs-lookup"><span data-stu-id="27007-133">In the search box, type **Teamphoria**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="27007-135">在結果窗格中，選取 [Teamphoria]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="27007-135">In the results panel, select **Teamphoria**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="27007-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="27007-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="27007-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Teamphoria 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="27007-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="27007-139">若要讓單一登入能夠運作，Azure AD 必須知道 Teamphoria 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="27007-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamphoria is to a user in Azure AD.</span></span> <span data-ttu-id="27007-140">換句話說，必須在 Azure AD 使用者與 Teamphoria 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="27007-140">In other words, a link relationship between an Azure AD user and the related user in Teamphoria needs to be established.</span></span>

<span data-ttu-id="27007-141">建立此連結關聯性的方法，就是指派 Azure AD 中**使用者名稱**的值作為 Teamphoria 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="27007-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamphoria.</span></span>

<span data-ttu-id="27007-142">若要設定及測試與 Teamphoria 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="27007-142">To configure and test Azure AD single sign-on with Teamphoria, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="27007-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="27007-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="27007-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="27007-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="27007-145">**[建立 Teamphoria 測試使用者](#creating-a-teamphoria-test-user)** - 使 Teamphoria 中，Britta Simon 的對應使用者能夠連結到代表她在 Azure AD 中的項目。</span><span class="sxs-lookup"><span data-stu-id="27007-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - to have a counterpart of Britta Simon in Teamphoria that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="27007-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="27007-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="27007-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="27007-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="27007-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="27007-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="27007-149">在本節中，您會在 Azure 管理入口網站中啟用 Azure AD 單一登入，並在您的 Teamphoria 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="27007-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="27007-150">**若要設定與 Teamphoria 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="27007-150">**To configure Azure AD single sign-on with Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="27007-151">在 Azure 管理入口網站的 [Teamphoria] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="27007-151">In the Azure Management portal, on the **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="27007-153">在 [單一登入] 對話方塊上，選取 [SAML 型登入] 做為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="27007-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="27007-155">在 [Teamphoria 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="27007-155">On the **Teamphoria Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="27007-157">a.</span><span class="sxs-lookup"><span data-stu-id="27007-157">a.</span></span> <span data-ttu-id="27007-158">在 [登入 URL] 文字方塊中，以下列模式輸入 URL：`https://<sub-domain>.teamphoria.com/login`</span><span class="sxs-lookup"><span data-stu-id="27007-158">In the **Sign-on URL** textbox, type the URL using the following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>    

    > [!NOTE] 
    > <span data-ttu-id="27007-159">請注意這些不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="27007-159">Please note that these are not the real values.</span></span> <span data-ttu-id="27007-160">您必須以實際的登入 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="27007-160">You have to update these values with the actual Sign-On URL.</span></span> <span data-ttu-id="27007-161">請連絡 [Teamphoria 用戶端支援小組](https://www.teamphoria.com/)以取得登入 URL。</span><span class="sxs-lookup"><span data-stu-id="27007-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) to get the Sign-on URL.</span></span> 

4. <span data-ttu-id="27007-162">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="27007-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="27007-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="27007-164">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="27007-166">在 [Teamphoria 組態] 區段上，按一下 [設定 Teamphoria] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="27007-166">On the **Teamphoria Configuration** section, click **Configure Teamphoria** to open **Configure sign-on** window.</span></span> <span data-ttu-id="27007-167">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="27007-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="27007-169">若要在 **Teamphoria** 端設定單一登入，請以系統管理員身分登入 Teamphoria 應用程式。</span><span class="sxs-lookup"><span data-stu-id="27007-169">To configure single sign-on on **Teamphoria** side, Login to your Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="27007-170">移至左側工具列中的 [系統管理員設定] 選項，然後在 [設定] 索引標籤上按一下 [單一登入] 以開啟 SSO 組態視窗。</span><span class="sxs-lookup"><span data-stu-id="27007-170">Go to **ADMIN SETTINGS** option in the left toolbar and under the the Configure Tab click on **SINGLE SIGN-ON** to open the SSO configuration window.</span></span>

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="27007-172">按一下右上角的 [新增識別提供者] 選項來開啟表單，以供新增 SSO 的設定。</span><span class="sxs-lookup"><span data-stu-id="27007-172">Click on **ADD NEW IDENTITY PROVIDER** option in the top right corner to open the form for adding the settings for SSO.</span></span>

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="27007-174">在欄位中輸入詳細資料，如下所示</span><span class="sxs-lookup"><span data-stu-id="27007-174">Enter the details in the fields as described below-</span></span>

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="27007-176">a.</span><span class="sxs-lookup"><span data-stu-id="27007-176">a.</span></span> <span data-ttu-id="27007-177">**顯示名稱**：在 [系統管理] 頁面輸入外掛程式的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="27007-177">**DISPLAY NAME** : Enter the display name of the plugin on the admin page.</span></span>

    <span data-ttu-id="27007-178">b.</span><span class="sxs-lookup"><span data-stu-id="27007-178">b.</span></span> <span data-ttu-id="27007-179">**按鈕名稱**︰索引標籤的名稱，會在用於透過 SSO 登入的登入頁面上顯示。</span><span class="sxs-lookup"><span data-stu-id="27007-179">**BUTTON NAME** : The name of the tab which will display on the login page for logging in via SSO.</span></span>

    <span data-ttu-id="27007-180">c.</span><span class="sxs-lookup"><span data-stu-id="27007-180">c.</span></span> <span data-ttu-id="27007-181">**憑證**︰在記事本中開啟您稍早從 Azure 入口網站下載的憑證，複製相同的內容並貼到這裡的方塊中。</span><span class="sxs-lookup"><span data-stu-id="27007-181">**CERTIFICATE** : Open the Certificate downloaded earlier from the Azure portal in notepad, copy the contents of the same and paste it here in the box.</span></span>

    <span data-ttu-id="27007-182">d.</span><span class="sxs-lookup"><span data-stu-id="27007-182">d.</span></span> <span data-ttu-id="27007-183">**進入點**︰貼上稍早從 Azure 入口網站複製的 **SAML 單一登入服務 URL**。</span><span class="sxs-lookup"><span data-stu-id="27007-183">**ENTRY POINT** : Paste the **SAML Single Sign-On Service URL** copied earlier form the Azure portal.</span></span>

    <span data-ttu-id="27007-184">e.</span><span class="sxs-lookup"><span data-stu-id="27007-184">e.</span></span> <span data-ttu-id="27007-185">將選項切換為 [開啟]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="27007-185">Switch the option to **ON** and click on **SAVE**.</span></span>   

<!--### Next steps

To ensure users can sign-in to Teamphoria after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Teamphoria in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="27007-186">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="27007-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="27007-187">本節目標是在 Azure 管理入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="27007-187">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="27007-189">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="27007-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="27007-190">在 **Azure 管理入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="27007-190">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="27007-192">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="27007-192">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="27007-194">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="27007-194">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="27007-196">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="27007-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="27007-198">a.</span><span class="sxs-lookup"><span data-stu-id="27007-198">a.</span></span> <span data-ttu-id="27007-199">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="27007-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="27007-200">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="27007-200">b.</span></span> <span data-ttu-id="27007-201">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="27007-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="27007-202">c.</span><span class="sxs-lookup"><span data-stu-id="27007-202">c.</span></span> <span data-ttu-id="27007-203">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="27007-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="27007-204">d.</span><span class="sxs-lookup"><span data-stu-id="27007-204">d.</span></span> <span data-ttu-id="27007-205">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="27007-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="27007-206">建立 Teamphoria 測試使用者</span><span class="sxs-lookup"><span data-stu-id="27007-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="27007-207">若要讓 Azure AD 使用者可以登入 Teamphoria，則必須將他們佈建到 Teamphoria。</span><span class="sxs-lookup"><span data-stu-id="27007-207">In order to enable Azure AD users to log into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="27007-208">Teamphoria 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="27007-208">In the case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="27007-209">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="27007-209">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="27007-210">以系統管理員身分登入您的 Teamphoria 公司網站。</span><span class="sxs-lookup"><span data-stu-id="27007-210">Log in to your Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="27007-211">按一下左側工具列上的 [系統管理員] 設定，然後在 [管理] 索引標籤底下按一下 [使用者]，以開啟使用者的 [系統管理] 頁面。</span><span class="sxs-lookup"><span data-stu-id="27007-211">Click on **ADMIN** settings on the left toolbar and under the **MANAGE** tab Click on **USERS** to open the admin page for users.</span></span>

    ![新增員工](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="27007-213">按一下 [手動邀請] 選項。</span><span class="sxs-lookup"><span data-stu-id="27007-213">Click on the **MANUAL INVITE** option.</span></span>

    ![邀請人員](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. <span data-ttu-id="27007-215">在這個頁面上執行下列動作。</span><span class="sxs-lookup"><span data-stu-id="27007-215">On this page, perform following action.</span></span> 
    
    ![邀請人員](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    <span data-ttu-id="27007-217">a.</span><span class="sxs-lookup"><span data-stu-id="27007-217">a.</span></span> <span data-ttu-id="27007-218">在 [電子郵件地址] 文字方塊中，輸入 Britta Simon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="27007-218">In the **EMAIL ADDRESS** textbox, the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="27007-219">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="27007-219">b.</span></span> <span data-ttu-id="27007-220">在 [名字] 文字方塊中，輸入 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="27007-220">In the **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="27007-221">c.</span><span class="sxs-lookup"><span data-stu-id="27007-221">c.</span></span> <span data-ttu-id="27007-222">在 [姓氏] 文字方塊中，輸入 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="27007-222">In the **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="27007-223">d.</span><span class="sxs-lookup"><span data-stu-id="27007-223">d.</span></span> <span data-ttu-id="27007-224">按一下 [邀請 1 位使用者]。</span><span class="sxs-lookup"><span data-stu-id="27007-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="27007-225">使用者必須接受邀請才能建立到系統中。</span><span class="sxs-lookup"><span data-stu-id="27007-225">User needs to accept the invite to get created in the system.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="27007-226">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="27007-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="27007-227">在本節中，您會將 Teamphoria 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="27007-227">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamphoria.</span></span>

![指派使用者][200] 

<span data-ttu-id="27007-229">**如要將 Britta Simon 指派給 Teamphoria，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="27007-229">**To assign Britta Simon to Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="27007-230">在 Azure 管理入口網站中，開啟應用程式檢視，然後瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="27007-230">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="27007-232">在應用程式清單中，選取 [Teamphoria]。</span><span class="sxs-lookup"><span data-stu-id="27007-232">In the applications list, select **Teamphoria**.</span></span>

    ![設定單一登入](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="27007-234">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="27007-234">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="27007-236">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="27007-236">Click **Add** button.</span></span> <span data-ttu-id="27007-237">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="27007-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="27007-239">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="27007-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="27007-240">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="27007-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="27007-241">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="27007-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="27007-242">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="27007-242">Testing single sign-on</span></span>

<span data-ttu-id="27007-243">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="27007-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="27007-244">如果要測試您的單一登入設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="27007-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="27007-245">如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="27007-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="27007-246">其他資源</span><span class="sxs-lookup"><span data-stu-id="27007-246">Additional resources</span></span>

* [<span data-ttu-id="27007-247">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="27007-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="27007-248">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="27007-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png


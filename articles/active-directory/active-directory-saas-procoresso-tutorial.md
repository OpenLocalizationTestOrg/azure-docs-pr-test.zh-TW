---
title: "教學課程：Azure Active Directory 與 Procore SSO 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Procore SSO 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: 042a41eaa6bb21670b4c12068f1b017222f64b99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a><span data-ttu-id="31109-103">教學課程：Azure Active Directory 與 Procore SSO 整合</span><span class="sxs-lookup"><span data-stu-id="31109-103">Tutorial: Azure Active Directory integration with Procore SSO</span></span>

<span data-ttu-id="31109-104">在本教學課程中，您會了解如何整合 Procore SSO 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="31109-104">In this tutorial, you learn how to integrate Procore SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="31109-105">Procore SSO 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="31109-105">Integrating Procore SSO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="31109-106">您可以在 Azure AD 中控制可存取 Procore SSO 的人員</span><span class="sxs-lookup"><span data-stu-id="31109-106">You can control in Azure AD who has access to Procore SSO</span></span>
- <span data-ttu-id="31109-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Procore SSO (單一登入)</span><span class="sxs-lookup"><span data-stu-id="31109-107">You can enable your users to automatically get signed-on to Procore SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="31109-108">您可以在 Azure 管理入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="31109-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="31109-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="31109-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Procore SSO, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="31109-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="31109-110">Prerequisites</span></span>

<span data-ttu-id="31109-111">若要設定 Procore SSO 與 Azure AD 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="31109-111">To configure Azure AD integration with Procore SSO, you need the following items:</span></span>

- <span data-ttu-id="31109-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="31109-112">An Azure AD subscription</span></span>
- <span data-ttu-id="31109-113">已啟用 Procore SSO 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="31109-113">A Procore SSO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="31109-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="31109-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="31109-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="31109-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="31109-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="31109-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="31109-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="31109-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="31109-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="31109-118">Scenario description</span></span>
<span data-ttu-id="31109-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="31109-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="31109-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="31109-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="31109-121">從資源庫新增 Procore SSO</span><span class="sxs-lookup"><span data-stu-id="31109-121">Adding Procore SSO from the gallery</span></span>
2. <span data-ttu-id="31109-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="31109-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-procore-sso-from-the-gallery"></a><span data-ttu-id="31109-123">從資源庫新增 Procore SSO</span><span class="sxs-lookup"><span data-stu-id="31109-123">Adding Procore SSO from the gallery</span></span>
<span data-ttu-id="31109-124">若要設定將 Procore SSO 整合到 Azure AD 中，您需要從資源庫將 Procore SSO 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="31109-124">To configure the integration of Procore SSO into Azure AD, you need to add Procore SSO from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="31109-125">**若要從資源庫新增 Procore SSO，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="31109-125">**To add Procore SSO from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="31109-126">在 **[Azure 管理入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="31109-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="31109-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="31109-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="31109-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="31109-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="31109-131">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="31109-131">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="31109-133">在搜尋方塊中，輸入 **Procore SSO**。</span><span class="sxs-lookup"><span data-stu-id="31109-133">In the search box, type **Procore SSO**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. <span data-ttu-id="31109-135">在結果窗格中，選取 [Procore SSO]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="31109-135">In the results panel, select **Procore SSO**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="31109-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="31109-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="31109-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Procore SSO 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="31109-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="31109-139">若要讓單一登入運作，Azure AD 必須知道 Procore SSO 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="31109-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Procore SSO is to a user in Azure AD.</span></span> <span data-ttu-id="31109-140">換句話說，必須建立 Azure AD 使用者和 Procore SSO 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="31109-140">In other words, a link relationship between an Azure AD user and the related user in Procore SSO needs to be established.</span></span>

<span data-ttu-id="31109-141">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指派為 Procore SSO 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="31109-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Procore SSO.</span></span>

<span data-ttu-id="31109-142">若要設定及測試與 Procore SSO 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="31109-142">To configure and test Azure AD single sign-on with Procore SSO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="31109-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="31109-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="31109-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="31109-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="31109-145">**[建立 Procore SSO 測試使用者](#creating-a-procore-sso-test-user)** - 讓 Procore SSO 中對應的 Britta Simon 連結到她在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="31109-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - to have a counterpart of Britta Simon in Procore SSO that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="31109-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="31109-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="31109-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="31109-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="31109-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="31109-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="31109-149">在本節中，您會在 Azure 管理入口網站中啟用 Azure AD 單一登入，並在您的 Procore SSO 中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="31109-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Procore SSO application.</span></span>

<span data-ttu-id="31109-150">**若要設定與 Procore SSO 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="31109-150">**To configure Azure AD single sign-on with Procore SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="31109-151">在 Azure 管理入口網站的 [Procore SSO] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="31109-151">In the Azure Management portal, on the **Procore SSO** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="31109-153">在 [單一登入] 對話方塊上，選取 [SAML 型登入] 作為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="31109-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. <span data-ttu-id="31109-155">在 [Procore SSO 網域和 URL] 區段中，使用者不需要執行任何步驟，因為應用程式已預先與 Azure 整合。</span><span class="sxs-lookup"><span data-stu-id="31109-155">On the **Procore SSO Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. <span data-ttu-id="31109-157">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="31109-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. <span data-ttu-id="31109-159">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="31109-159">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="31109-161">在 [Procore SSO 組態] 區段上，按一下 [設定 Procore SSO] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="31109-161">On the **Procore SSO Configuration** section, click **Configure Procore SSO** to open **Configure sign-on** window.</span></span> <span data-ttu-id="31109-162">從 [快速參考] 區段中複製 [SAML 實體 ID 和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="31109-162">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. <span data-ttu-id="31109-164">若要在 **Procore SSO** 端設定單一登入，請以系統管理員身分登入 procore 公司網站。</span><span class="sxs-lookup"><span data-stu-id="31109-164">To configure single sign-on on **Procore SSO** side, login to your procore company site as an administrator.</span></span>

8. <span data-ttu-id="31109-165">從工具箱下拉式清單按一下 [管理] 以開啟 SSO 設定頁面。</span><span class="sxs-lookup"><span data-stu-id="31109-165">From the toolbox drop down, click on **Admin** to open the SSO settings page.</span></span>

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. <span data-ttu-id="31109-167">如下所述貼上方塊中的值-</span><span class="sxs-lookup"><span data-stu-id="31109-167">Paste the values in the boxes as described below-</span></span>

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    <span data-ttu-id="31109-169">a.</span><span class="sxs-lookup"><span data-stu-id="31109-169">a.</span></span> <span data-ttu-id="31109-170">在 [單一登入簽發者 URL] 方塊中，貼上從 Azure 入口網站複製的 SAML 實體 ID。</span><span class="sxs-lookup"><span data-stu-id="31109-170">In the **Single Sign On Issuer URL** box, paste the SAML Entity ID copied from the Azure portal.</span></span>

    <span data-ttu-id="31109-171">b.</span><span class="sxs-lookup"><span data-stu-id="31109-171">b.</span></span> <span data-ttu-id="31109-172">在 [SAML 登入目標 URL] 方塊中，貼上從 Azure 入口網站複製的 SAML 單一登入服務 URL。</span><span class="sxs-lookup"><span data-stu-id="31109-172">In the **SAML Sign On Target URL** box, paste the SAML Single Sign-On Service URL copied from the Azure portal.</span></span>

    <span data-ttu-id="31109-173">c.</span><span class="sxs-lookup"><span data-stu-id="31109-173">c.</span></span> <span data-ttu-id="31109-174">現在開啟上述從 Azure 入口網站下載的**中繼資料 XML**，然後複製名為 **X509Certificate**之標記中的憑證。</span><span class="sxs-lookup"><span data-stu-id="31109-174">Now open the **Metadata XML** downloaded above from the Azure portal and copy the certficate in the tag named **X509Certificate**.</span></span> <span data-ttu-id="31109-175">將複製的值貼至 [單一登入 x509 憑證] 方塊。</span><span class="sxs-lookup"><span data-stu-id="31109-175">Paste the copied value into the **Single Sign On x509 Certificate** box.</span></span>

10. <span data-ttu-id="31109-176">按一下 [儲存變更]。</span><span class="sxs-lookup"><span data-stu-id="31109-176">Click on **Save Changes**.</span></span>

11. <span data-ttu-id="31109-177">在進行這些設定之後，您必須將透過它來登入 Procore 的 **網域名稱** (例如 **contoso.com**)，傳送給 [Procore 支援小組](https://support.procore.com/)，支援小組會為該網域啟動同盟 SSO。</span><span class="sxs-lookup"><span data-stu-id="31109-177">After these settings, you needs to send the **domain name** (e.g **contoso.com**) through which you are logging into Procore to the [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span></span>

<!--### Next steps

To ensure users can sign-in to Procore SSO after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Procore SSO in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="31109-178">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="31109-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="31109-179">本節目標是在 Azure 管理入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="31109-179">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="31109-181">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="31109-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="31109-182">在 **Azure 管理入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="31109-182">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="31109-184">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="31109-184">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="31109-186">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="31109-186">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="31109-188">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="31109-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="31109-190">a.</span><span class="sxs-lookup"><span data-stu-id="31109-190">a.</span></span> <span data-ttu-id="31109-191">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="31109-191">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="31109-192">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="31109-192">b.</span></span> <span data-ttu-id="31109-193">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="31109-193">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="31109-194">c.</span><span class="sxs-lookup"><span data-stu-id="31109-194">c.</span></span> <span data-ttu-id="31109-195">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="31109-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="31109-196">d.</span><span class="sxs-lookup"><span data-stu-id="31109-196">d.</span></span> <span data-ttu-id="31109-197">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="31109-197">Click **Create**.</span></span>
 
### <a name="creating-a-procore-sso-test-user"></a><span data-ttu-id="31109-198">建立 Procore SSO 測試使用者</span><span class="sxs-lookup"><span data-stu-id="31109-198">Creating a Procore SSO test user</span></span>

<span data-ttu-id="31109-199">請遵循下列步驟以在 Procore 端建立 Procore 測試使用者。</span><span class="sxs-lookup"><span data-stu-id="31109-199">Please follow the below steps to create a Procore test user on their side.</span></span>

1. <span data-ttu-id="31109-200">以系統管理員身分登入您的 procore 公司網站。</span><span class="sxs-lookup"><span data-stu-id="31109-200">Login to your procore company site as an administrator.</span></span>  

2. <span data-ttu-id="31109-201">從工具箱下拉式清單按一下 [目錄] 以開啟公司目錄頁面。</span><span class="sxs-lookup"><span data-stu-id="31109-201">From the toolbox drop down, click on **Directory** to open the company directory page.</span></span>

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. <span data-ttu-id="31109-203">按一下 [新增人員] 選項來開啟表單，然後輸入執行以下選項-</span><span class="sxs-lookup"><span data-stu-id="31109-203">Click on **Add a Person** option to open the form and enter perform following options -</span></span>

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    <span data-ttu-id="31109-205">a.</span><span class="sxs-lookup"><span data-stu-id="31109-205">a.</span></span> <span data-ttu-id="31109-206">在 [名字] 文字方塊中，輸入使用者的名字，例如 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="31109-206">In the **First Name** textbox, type user's first name like **Britta**.</span></span>

    <span data-ttu-id="31109-207">b.</span><span class="sxs-lookup"><span data-stu-id="31109-207">b.</span></span> <span data-ttu-id="31109-208">在 [姓氏] 文字方塊中，輸入使用者的姓氏，例如 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="31109-208">In the **Last name** textbox, type user's last name like **Simon**.</span></span>

    <span data-ttu-id="31109-209">c.</span><span class="sxs-lookup"><span data-stu-id="31109-209">c.</span></span> <span data-ttu-id="31109-210">在 [電子郵件] 文字方塊中，輸入使用者的電子郵件地址，例如 **BrittaSimon@contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="31109-210">In the **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="31109-211">d.</span><span class="sxs-lookup"><span data-stu-id="31109-211">d.</span></span> <span data-ttu-id="31109-212">將 [權限範本] 選取為 [稍後套用權限範本]。</span><span class="sxs-lookup"><span data-stu-id="31109-212">Select **Permission Template** as **Apply Permission Template Later**.</span></span>

    <span data-ttu-id="31109-213">e.</span><span class="sxs-lookup"><span data-stu-id="31109-213">e.</span></span> <span data-ttu-id="31109-214">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="31109-214">Click **Create**.</span></span>

4. <span data-ttu-id="31109-215">檢查並更新新增之連絡人的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="31109-215">Check and update the details for the newly added contact.</span></span>

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. <span data-ttu-id="31109-217">按一下 [儲存並傳送邀請] \(如果透過郵件邀請是必要的)，或者按一下 [儲存] \(直接儲存) 以完成使用者註冊。</span><span class="sxs-lookup"><span data-stu-id="31109-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) to complete the user registration.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="31109-219">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="31109-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="31109-220">在本節中，您會將 Procore SSO 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="31109-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Procore SSO.</span></span>

![指派使用者][200] 

<span data-ttu-id="31109-222">**若要將 Britta Simon 指派給 Procore SSO，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="31109-222">**To assign Britta Simon to Procore SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="31109-223">在 Azure 管理入口網站中，開啟應用程式檢視，然後瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="31109-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="31109-225">在應用程式清單中，選取 [Procore SSO]。</span><span class="sxs-lookup"><span data-stu-id="31109-225">In the applications list, select **Procore SSO**.</span></span>

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. <span data-ttu-id="31109-227">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="31109-227">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="31109-229">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="31109-229">Click **Add** button.</span></span> <span data-ttu-id="31109-230">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="31109-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="31109-232">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="31109-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="31109-233">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="31109-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="31109-234">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="31109-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="31109-235">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="31109-235">Testing single sign-on</span></span>

<span data-ttu-id="31109-236">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="31109-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="31109-237">如果要測試您的單一登入設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="31109-237">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="31109-238">如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="31109-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> <span data-ttu-id="31109-239">當您按一下「存取面板」中的 Procore SSO 圖格時，應該會自動登入您的 Procore SSO 應用程式。</span><span class="sxs-lookup"><span data-stu-id="31109-239">When you click the Procore SSO tile in the Access Panel, you should get automatically signed-on to your Procore SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="31109-240">其他資源</span><span class="sxs-lookup"><span data-stu-id="31109-240">Additional resources</span></span>

* [<span data-ttu-id="31109-241">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="31109-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="31109-242">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="31109-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png


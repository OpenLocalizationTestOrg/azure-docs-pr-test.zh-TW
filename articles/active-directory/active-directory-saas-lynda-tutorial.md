---
title: "教學課程：Azure Active Directory 與 Lynda.com 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Lynda.com 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 84ed2adcc2d49ddbb6bd2e9cc3b93b967ebed063
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a><span data-ttu-id="a8a0c-103">教學課程：Azure Active Directory 與 Lynda.com 整合</span><span class="sxs-lookup"><span data-stu-id="a8a0c-103">Tutorial: Azure Active Directory integration with Lynda.com</span></span>

<span data-ttu-id="a8a0c-104">在本教學課程中，您將了解如何整合 Lynda.com 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-104">In this tutorial, you learn how to integrate Lynda.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a8a0c-105">Lynda.com 與 Azure AD 整合有下列優點：</span><span class="sxs-lookup"><span data-stu-id="a8a0c-105">Integrating Lynda.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a8a0c-106">您可以在 Azure AD 中控制可存取 Lynda.com 的人員</span><span class="sxs-lookup"><span data-stu-id="a8a0c-106">You can control in Azure AD who has access to Lynda.com</span></span>
- <span data-ttu-id="a8a0c-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Lynda.com (單一登入)</span><span class="sxs-lookup"><span data-stu-id="a8a0c-107">You can enable your users to automatically get signed-on to Lynda.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a8a0c-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="a8a0c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a8a0c-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8a0c-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a8a0c-110">Prerequisites</span></span>

<span data-ttu-id="a8a0c-111">若要進行 Azure AD 與 Lynda.com 整合的設定，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="a8a0c-111">To configure Azure AD integration with Lynda.com, you need the following items:</span></span>

- <span data-ttu-id="a8a0c-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a8a0c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a8a0c-113">已啟用 Lynda.com 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a8a0c-113">A Lynda.com single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a8a0c-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a8a0c-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="a8a0c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a8a0c-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a8a0c-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a8a0c-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="a8a0c-118">Scenario description</span></span>
<span data-ttu-id="a8a0c-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a8a0c-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="a8a0c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a8a0c-121">從資源庫新增 Lynda.com</span><span class="sxs-lookup"><span data-stu-id="a8a0c-121">Adding Lynda.com from the gallery</span></span>
2. <span data-ttu-id="a8a0c-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a8a0c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lyndacom-from-the-gallery"></a><span data-ttu-id="a8a0c-123">從資源庫新增 Lynda.com</span><span class="sxs-lookup"><span data-stu-id="a8a0c-123">Adding Lynda.com from the gallery</span></span>
<span data-ttu-id="a8a0c-124">若要進行 Lynda.com 與 Azure AD 整合的設定，您需要從資源庫將 Lynda.com 新增至受管理 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-124">To configure the integration of Lynda.com into Azure AD, you need to add Lynda.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a8a0c-125">**若要從資源庫新增 Lynda.com，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a8a0c-125">**To add Lynda.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a8a0c-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a8a0c-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a8a0c-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="a8a0c-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="a8a0c-133">在搜尋方塊中，輸入 **Lynda.com**。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-133">In the search box, type **Lynda.com**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_search.png)

5. <span data-ttu-id="a8a0c-135">在結果面板中，選取 [Lynda.com]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-135">In the results panel, select **Lynda.com**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a8a0c-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a8a0c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a8a0c-138">在本節中，您將以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Lynda.com 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-138">In this section, you configure and test Azure AD single sign-on with Lynda.com based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a8a0c-139">為了讓單一登入正常運作，Azure AD 必須知道 Azure AD 使用者在 Lynda.com 中的對應使用者是誰。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lynda.com is to a user in Azure AD.</span></span> <span data-ttu-id="a8a0c-140">換句話說，必須在 Azure AD 使用者與 Lynda.com 的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-140">In other words, a link relationship between an Azure AD user and the related user in Lynda.com needs to be established.</span></span>

<span data-ttu-id="a8a0c-141">建立此連結關聯性的方法，就是將 Azure AD 中 [使用者名稱] 的值指派為 Lynda.com 中 [使用者名稱] 的值。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lynda.com.</span></span>

<span data-ttu-id="a8a0c-142">若要設定及測試與 Lynda.com 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="a8a0c-142">To configure and test Azure AD single sign-on with Lynda.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a8a0c-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a8a0c-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a8a0c-145">**[建立 Lynda.com 測試使用者](#creating-a-lyndacom-test-user)** - 使 Lynda.com 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-145">**[Creating a Lynda.com test user](#creating-a-lyndacom-test-user)** - to have a counterpart of Britta Simon in Lynda.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a8a0c-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a8a0c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a8a0c-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a8a0c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a8a0c-149">在本節中，您將在 Azure 入口網站中啟用 Azure AD 單一登入，並在 Lynda.com 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lynda.com application.</span></span>

<span data-ttu-id="a8a0c-150">**若要設定 Lynda.com 的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a8a0c-150">**To configure Azure AD single sign-on with Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="a8a0c-151">在 Azure 入口網站的 [Lynda.com] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-151">In the Azure portal, on the **Lynda.com** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="a8a0c-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_samlbase.png)

3. <span data-ttu-id="a8a0c-155">在 [Lynda.com 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a8a0c-155">On the **Lynda.com Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_url.png)

    <span data-ttu-id="a8a0c-157">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span><span class="sxs-lookup"><span data-stu-id="a8a0c-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a8a0c-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-158">This value is not real.</span></span> <span data-ttu-id="a8a0c-159">使用實際的登入 URL 來更新此值。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="a8a0c-160">請連絡 [Lynda.com 用戶端支援小組](https://www.linkedin.com/help/lynda/ask)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-160">Contact [Lynda.com Client support team](https://www.linkedin.com/help/lynda/ask) to get these values.</span></span> 
 
4. <span data-ttu-id="a8a0c-161">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_certificate.png) 

5. <span data-ttu-id="a8a0c-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-lynda-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a8a0c-165">若要在 **Lynda.com** 端設定單一登入，您必須將已下載的**中繼資料 XML** 傳送給 [Lynda.com 支援](https://www.linkedin.com/help/lynda/ask)。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-165">To configure single sign-on on **Lynda.com** side, you need to send the downloaded **Metadata XML** [Lynda.com support](https://www.linkedin.com/help/lynda/ask).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a8a0c-166">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a8a0c-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="a8a0c-167">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="a8a0c-169">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a8a0c-169">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a8a0c-170">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-170">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lynda-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a8a0c-172">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-172">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lynda-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a8a0c-174">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-174">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lynda-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a8a0c-176">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a8a0c-176">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lynda-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a8a0c-178">a.</span><span class="sxs-lookup"><span data-stu-id="a8a0c-178">a.</span></span> <span data-ttu-id="a8a0c-179">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-179">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a8a0c-180">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-180">b.</span></span> <span data-ttu-id="a8a0c-181">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-181">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a8a0c-182">c.</span><span class="sxs-lookup"><span data-stu-id="a8a0c-182">c.</span></span> <span data-ttu-id="a8a0c-183">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-183">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a8a0c-184">d.</span><span class="sxs-lookup"><span data-stu-id="a8a0c-184">d.</span></span> <span data-ttu-id="a8a0c-185">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-185">Click **Create**.</span></span>
 
### <a name="creating-a-lyndacom-test-user"></a><span data-ttu-id="a8a0c-186">建立 Lynda.com 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a8a0c-186">Creating a Lynda.com test user</span></span>

<span data-ttu-id="a8a0c-187">沒有動作項目可讓您設定 Lynda.com 使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-187">There is no action item for you to configure user provisioning to Lynda.com.</span></span>  
<span data-ttu-id="a8a0c-188">當指派的使用者使用存取面板嘗試登入 Lynda.com 時，Lynda.com 會檢查該使用者是否存在。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-188">When an assigned user tries to log in to Lynda.com using the access panel, Lynda.com checks whether the user exists.</span></span>  

<span data-ttu-id="a8a0c-189">如果尚無可用的使用者帳戶，Lynda.com 會自動予以建立。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-189">If there is no user account available yet, it is automatically created by Lynda.com.</span></span>

>[!NOTE]
><span data-ttu-id="a8a0c-190">您可以使用 Lynda.com 提供的任何其他 Lynda.com 使用者帳戶建立工具或 API，佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-190">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a8a0c-191">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a8a0c-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a8a0c-192">在本節中，您將把 Lynda.com 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lynda.com.</span></span>

![指派使用者][200] 

<span data-ttu-id="a8a0c-194">**若要將 Britta Simon 指派到 Lynda.com，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a8a0c-194">**To assign Britta Simon to Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="a8a0c-195">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="a8a0c-197">在應用程式清單中，選取 [Lynda.com]。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-197">In the applications list, select **Lynda.com**.</span></span>

    ![設定單一登入](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_app.png) 

3. <span data-ttu-id="a8a0c-199">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-199">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="a8a0c-201">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-201">Click **Add** button.</span></span> <span data-ttu-id="a8a0c-202">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="a8a0c-204">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a8a0c-205">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a8a0c-206">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a8a0c-207">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="a8a0c-207">Testing single sign-on</span></span>

<span data-ttu-id="a8a0c-208">如果要測試您的單一登入設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-208">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="a8a0c-209">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="a8a0c-209">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a8a0c-210">其他資源</span><span class="sxs-lookup"><span data-stu-id="a8a0c-210">Additional resources</span></span>

* [<span data-ttu-id="a8a0c-211">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="a8a0c-211">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a8a0c-212">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a8a0c-212">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_203.png


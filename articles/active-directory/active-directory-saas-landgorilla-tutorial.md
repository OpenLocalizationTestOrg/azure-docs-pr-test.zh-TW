---
title: "教學課程：Azure Active Directory 與 Land Gorilla Client 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Land Gorilla 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: jeedes
ms.openlocfilehash: 744c420aa0298c59c44e645b95a716ad876752de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-land-gorilla-client"></a><span data-ttu-id="734b8-103">教學課程：Azure Active Directory 與 Land Gorilla Client 整合</span><span class="sxs-lookup"><span data-stu-id="734b8-103">Tutorial: Azure Active Directory integration with Land Gorilla Client</span></span>

<span data-ttu-id="734b8-104">在本教學課程中，您將了解如何整合 Land Gorilla Client 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="734b8-104">In this tutorial, you learn how to integrate Land Gorilla Client with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="734b8-105">將 Land Gorilla Client 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="734b8-105">Integrating Land Gorilla Client with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="734b8-106">您可以在 Azure AD 中控制可存取 Land Gorilla Client 的人員</span><span class="sxs-lookup"><span data-stu-id="734b8-106">You can control in Azure AD who has access to Land Gorilla Client</span></span>
- <span data-ttu-id="734b8-107">您可以讓使用者透過其 Azure AD 帳戶自動登入 Land Gorilla Client (單一登入)</span><span class="sxs-lookup"><span data-stu-id="734b8-107">You can enable your users to automatically get signed-on to Land Gorilla Client (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="734b8-108">您可以在 Azure 管理入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="734b8-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="734b8-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="734b8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="734b8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="734b8-110">Prerequisites</span></span>

<span data-ttu-id="734b8-111">若要設定 Azure AD 與 Land Gorilla Client 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="734b8-111">To configure Azure AD integration with Land Gorilla Client, you need the following items:</span></span>

- <span data-ttu-id="734b8-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="734b8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="734b8-113">啟用 Land Gorilla Client 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="734b8-113">A Land Gorilla Client single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="734b8-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="734b8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="734b8-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="734b8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="734b8-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="734b8-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="734b8-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="734b8-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="734b8-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="734b8-118">Scenario description</span></span>
<span data-ttu-id="734b8-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="734b8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="734b8-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="734b8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="734b8-121">從資源庫新增 Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="734b8-121">Adding Land Gorilla Client from the gallery</span></span>
2. <span data-ttu-id="734b8-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="734b8-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-land-gorilla-client-from-the-gallery"></a><span data-ttu-id="734b8-123">從資源庫新增 Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="734b8-123">Adding Land Gorilla Client from the gallery</span></span>
<span data-ttu-id="734b8-124">若要設定將 Land Gorilla Client 整合到 Azure AD 中，您需要從資源庫將 Land Gorilla Client 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="734b8-124">To configure the integration of Land Gorilla Client into Azure AD, you need to add Land Gorilla Client from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="734b8-125">**若要從資源庫新增 Land Gorilla Client，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="734b8-125">**To add Land Gorilla Client from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="734b8-126">在 **[Azure 管理入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="734b8-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="734b8-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="734b8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="734b8-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="734b8-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="734b8-131">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="734b8-131">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="734b8-133">在 [搜尋] 方塊中，輸入 **Land Gorilla Client**。</span><span class="sxs-lookup"><span data-stu-id="734b8-133">In the search box, type **Land Gorilla Client**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_search.png)

5. <span data-ttu-id="734b8-135">在結果窗格中，選取 [Land Gorilla Client]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="734b8-135">In the results panel, select **Land Gorilla Client**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="734b8-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="734b8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="734b8-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Land Gorilla Client 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="734b8-138">In this section, you configure and test Azure AD single sign-on with Land Gorilla Client based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="734b8-139">若要讓單一登入能夠運作，Azure AD 必須知道 Land Gorilla Client 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="734b8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Land Gorilla Client is to a user in Azure AD.</span></span> <span data-ttu-id="734b8-140">換句話說，必須在 Azure AD 使用者與 Land Gorilla Client 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="734b8-140">In other words, a link relationship between an Azure AD user and the related user in Land Gorilla Client needs to be established.</span></span>

<span data-ttu-id="734b8-141">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指派為 Land Gorilla Client 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="734b8-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Land Gorilla Client.</span></span>

<span data-ttu-id="734b8-142">若要設定及測試與 Land Gorilla Client 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="734b8-142">To configure and test Azure AD single sign-on with Land Gorilla Client, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="734b8-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="734b8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="734b8-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用受限制的群組測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="734b8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with limited group.</span></span>
3. <span data-ttu-id="734b8-145">**[建立 Land Gorilla 測試使用者](#creating-a-land-gorilla-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="734b8-145">**[Creating a Land Gorilla test user](#creating-a-land-gorilla-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="734b8-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="734b8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="734b8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="734b8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="734b8-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="734b8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="734b8-149">在本節中，您會在 Azure 管理入口網站中啟用 Azure AD 單一登入，並在您的 Land Gorilla Client 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="734b8-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Land Gorilla Client application.</span></span>

<span data-ttu-id="734b8-150">**若要使用 Land Gorilla Client 設定 Azure AD 單一登入功能，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="734b8-150">**To configure Azure AD single sign-on with Land Gorilla Client, perform the following steps:**</span></span>

1. <span data-ttu-id="734b8-151">在 Azure 管理入口網站的 [Land Gorilla Client] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="734b8-151">In the Azure Management portal, on the **Land Gorilla Client** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="734b8-153">在 [單一登入] 對話方塊上，選取 [SAML 型登入] 做為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="734b8-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_samlbase.png)

3. <span data-ttu-id="734b8-155">在 [Land Gorilla Client 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="734b8-155">On the **Land Gorilla Client Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_url_02.png)

    <span data-ttu-id="734b8-157">a.</span><span class="sxs-lookup"><span data-stu-id="734b8-157">a.</span></span> <span data-ttu-id="734b8-158">在 [識別碼] 文字方塊中，以下列其中一個模式輸入值：</span><span class="sxs-lookup"><span data-stu-id="734b8-158">In the **Identifier** textbox, type the value using one of the following pattern:</span></span> 
    
    `https://<customer domain>.landgorilla.com/` 
    
    `https://www.<customer domain>.landgorilla.com`

    <span data-ttu-id="734b8-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="734b8-159">b.</span></span> <span data-ttu-id="734b8-160">在 [回覆 URL] 文字方塊中，以下列其中一個模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="734b8-160">In the **Reply URL** textbox, type a URL using one of the following pattern:</span></span>

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`
    
    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`

    > [!NOTE] 
    > <span data-ttu-id="734b8-161">請注意這些不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="734b8-161">Please note that these are not the real values.</span></span> <span data-ttu-id="734b8-162">您必須使用實際的識別碼和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="734b8-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="734b8-163">在此建議您在 [識別碼] 中使用唯一的字串值。</span><span class="sxs-lookup"><span data-stu-id="734b8-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="734b8-164">請連絡 [Land Gorilla Client 小組](https://www.landgorilla.com/support/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="734b8-164">Contact [Land Gorilla Client team](https://www.landgorilla.com/support/) to get these values.</span></span> 

4. <span data-ttu-id="734b8-165">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="734b8-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_certificate.png) 

5. <span data-ttu-id="734b8-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="734b8-167">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-landgorilla-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="734b8-169">若要在 Land Gorilla 結尾為您的應用程式完成 SSO 組態，請連絡 [Land Gorilla Client 支援小組](https://www.landgorilla.com/support/)，並且提供已下載的「中繼資料 XML」檔案。</span><span class="sxs-lookup"><span data-stu-id="734b8-169">To get SSO configuration complete for your application at Land Gorilla end, Contact [Land Gorilla Client support team](https://www.landgorilla.com/support/) and provide them with the downloaded **“Metadata XML** file.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="734b8-170">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="734b8-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="734b8-171">本節目標是在 Azure 管理入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="734b8-171">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="734b8-173">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="734b8-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="734b8-174">在 **Azure 管理入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="734b8-174">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="734b8-176">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="734b8-176">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="734b8-178">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="734b8-178">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="734b8-180">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="734b8-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="734b8-182">a.</span><span class="sxs-lookup"><span data-stu-id="734b8-182">a.</span></span> <span data-ttu-id="734b8-183">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="734b8-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="734b8-184">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="734b8-184">b.</span></span> <span data-ttu-id="734b8-185">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="734b8-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="734b8-186">c.</span><span class="sxs-lookup"><span data-stu-id="734b8-186">c.</span></span> <span data-ttu-id="734b8-187">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="734b8-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="734b8-188">d.</span><span class="sxs-lookup"><span data-stu-id="734b8-188">d.</span></span> <span data-ttu-id="734b8-189">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="734b8-189">Click **Create**.</span></span> 

### <a name="creating-a-land-gorilla-test-user"></a><span data-ttu-id="734b8-190">建立 Land Gorilla 測試使用者</span><span class="sxs-lookup"><span data-stu-id="734b8-190">Creating a Land Gorilla test user</span></span>

<span data-ttu-id="734b8-191">請與 [Land Gorilla 支援小組](https://www.landgorilla.com/support/)合作，以在 Land Gorilla 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="734b8-191">Please work with [Land Gorilla support team](https://www.landgorilla.com/support/) to add the users in the Land Gorilla platform.</span></span>
    
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="734b8-192">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="734b8-192">Assigning the Azure AD test user</span></span>

<span data-ttu-id="734b8-193">在本節中，您會將 Land Gorilla Client 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="734b8-193">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Land Gorilla Client.</span></span>

![指派使用者][200] 

<span data-ttu-id="734b8-195">**若要將 Britta Simon 指派到 Land Gorilla Client，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="734b8-195">**To assign Britta Simon to Land Gorilla Client, perform the following steps:**</span></span>

1. <span data-ttu-id="734b8-196">在 Azure 管理入口網站中，開啟應用程式檢視，然後瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="734b8-196">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="734b8-198">在應用程式清單中，選取 [Land Gorilla Client]。</span><span class="sxs-lookup"><span data-stu-id="734b8-198">In the applications list, select **Land Gorilla Client**.</span></span>

    ![設定單一登入](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_app.png) 

3. <span data-ttu-id="734b8-200">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="734b8-200">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="734b8-202">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="734b8-202">Click **Add** button.</span></span> <span data-ttu-id="734b8-203">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="734b8-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="734b8-205">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="734b8-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="734b8-206">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="734b8-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="734b8-207">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="734b8-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="734b8-208">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="734b8-208">Testing single sign-on</span></span>

<span data-ttu-id="734b8-209">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="734b8-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="734b8-210">當您在「存取面板」中按一下 [Land Gorilla Client] 圖格時，應該會自動登入您的 Land Gorilla Client 應用程式。</span><span class="sxs-lookup"><span data-stu-id="734b8-210">When you click the Land Gorilla Client tile in the Access Panel, you should get automatically signed-on to your Land Gorilla Client application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="734b8-211">其他資源</span><span class="sxs-lookup"><span data-stu-id="734b8-211">Additional resources</span></span>

* [<span data-ttu-id="734b8-212">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="734b8-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="734b8-213">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="734b8-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_203.png

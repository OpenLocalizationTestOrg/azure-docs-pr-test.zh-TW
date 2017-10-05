---
title: "教學課程：Azure Active Directory 與 Pingboard 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Pingboard 之間的單一登入。"
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
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 008c670a8043da0c67ccefde48d5ef721c75d97c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="31ecf-103">教學課程：Azure Active Directory 與 Pingboard 整合</span><span class="sxs-lookup"><span data-stu-id="31ecf-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="31ecf-104">在本教學課程中，您會了解如何整合 Pingboard 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="31ecf-104">In this tutorial, you learn how to integrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="31ecf-105">Pingboard 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="31ecf-105">Integrating Pingboard with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="31ecf-106">您可以在 Azure AD 中控制可存取 Pingboard 的人員</span><span class="sxs-lookup"><span data-stu-id="31ecf-106">You can control in Azure AD who has access to Pingboard</span></span>
- <span data-ttu-id="31ecf-107">您可以讓使用者利用自己的 Azure AD 帳戶，來自動登入 Pingboard (單一登入)</span><span class="sxs-lookup"><span data-stu-id="31ecf-107">You can enable your users to automatically get signed-on to Pingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="31ecf-108">您可以在 Azure 管理入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="31ecf-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="31ecf-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="31ecf-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31ecf-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="31ecf-110">Prerequisites</span></span>

<span data-ttu-id="31ecf-111">若要設定 Pingboard 與 Azure AD 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="31ecf-111">To configure Azure AD integration with Pingboard, you need the following items:</span></span>

- <span data-ttu-id="31ecf-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="31ecf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="31ecf-113">已啟用 Pingboard 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="31ecf-113">A Pingboard single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="31ecf-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="31ecf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="31ecf-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="31ecf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="31ecf-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="31ecf-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="31ecf-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="31ecf-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="31ecf-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="31ecf-118">Scenario description</span></span>
<span data-ttu-id="31ecf-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="31ecf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="31ecf-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="31ecf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="31ecf-121">從資源庫新增 Pingboard</span><span class="sxs-lookup"><span data-stu-id="31ecf-121">Adding Pingboard from the gallery</span></span>
2. <span data-ttu-id="31ecf-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="31ecf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-the-gallery"></a><span data-ttu-id="31ecf-123">從資源庫新增 Pingboard</span><span class="sxs-lookup"><span data-stu-id="31ecf-123">Adding Pingboard from the gallery</span></span>
<span data-ttu-id="31ecf-124">若要設定將 Pingboard 整合到 Azure AD 中，您需要從資源庫將 Pingboard 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="31ecf-124">To configure the integration of Pingboard into Azure AD, you need to add Pingboard from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="31ecf-125">**若要從資源庫新增 Pingboard，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="31ecf-125">**To add Pingboard from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="31ecf-126">在 **[Azure 管理入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="31ecf-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="31ecf-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="31ecf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="31ecf-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="31ecf-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="31ecf-131">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="31ecf-131">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="31ecf-133">在搜尋方塊中，輸入 [Pingboard]。</span><span class="sxs-lookup"><span data-stu-id="31ecf-133">In the search box, type **Pingboard**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. <span data-ttu-id="31ecf-135">在結果窗格中，選取 [Pingboard]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="31ecf-135">In the results panel, select **Pingboard**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="31ecf-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="31ecf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="31ecf-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Pingboard 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="31ecf-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="31ecf-139">若要讓單一登入運作，Azure AD 必須知道 Pingboard 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="31ecf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pingboard is to a user in Azure AD.</span></span> <span data-ttu-id="31ecf-140">換句話說，必須建立 Azure AD 使用者和 Pingboard 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="31ecf-140">In other words, a link relationship between an Azure AD user and the related user in Pingboard needs to be established.</span></span>

<span data-ttu-id="31ecf-141">建立此連結關聯性的方法是將 Azure AD 中**使用者名稱**的值指定為 Pingboard 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="31ecf-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Pingboard.</span></span>

<span data-ttu-id="31ecf-142">若要設定及測試與 Pingboard 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="31ecf-142">To configure and test Azure AD single sign-on with Pingboard, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="31ecf-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="31ecf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="31ecf-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="31ecf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="31ecf-145">**[建立 Pingboard 測試使用者](#creating-a-pingboard-test-user)** - 在 Pingboard 中建立 Britta Simon 的對應項目，且該項目必須與 Azure AD 中代表 Britta Simon 的項目連結。</span><span class="sxs-lookup"><span data-stu-id="31ecf-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - to have a counterpart of Britta Simon in Pingboard that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="31ecf-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="31ecf-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="31ecf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="31ecf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="31ecf-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="31ecf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="31ecf-149">在本節中，您會在 Azure 管理入口網站中啟用 Azure AD 單一登入，並在您的 Pingboard 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="31ecf-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="31ecf-150">**若要使用 Pingboard 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="31ecf-150">**To configure Azure AD single sign-on with Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="31ecf-151">在 Azure 管理入口網站的 [Pingboard] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="31ecf-151">In the Azure Management portal, on the **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="31ecf-153">在 [單一登入] 對話方塊上，選取 [SAML 型登入] 做為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="31ecf-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. <span data-ttu-id="31ecf-155">如果您想要以 **IDP** 起始模式設定應用程式，請在 [Pingboard 網域和 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="31ecf-155">On the **Pingboard Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="31ecf-157">a.</span><span class="sxs-lookup"><span data-stu-id="31ecf-157">a.</span></span> <span data-ttu-id="31ecf-158">在 [識別碼] 文字方塊中，以下列形式輸入值：`http://<entity-id>.pingboard.com/sp`</span><span class="sxs-lookup"><span data-stu-id="31ecf-158">In the **Identifier** textbox, type the value as: `http://<entity-id>.pingboard.com/sp`</span></span>

    <span data-ttu-id="31ecf-159">b.</span><span class="sxs-lookup"><span data-stu-id="31ecf-159">b.</span></span> <span data-ttu-id="31ecf-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<entity-id>.pingboard.com/auth/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="31ecf-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="31ecf-161">請注意這些不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="31ecf-161">Please note that these are not the real values.</span></span> <span data-ttu-id="31ecf-162">您必須使用實際的識別碼和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="31ecf-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="31ecf-163">在此建議您在 [識別碼] 中使用唯一的字串值。</span><span class="sxs-lookup"><span data-stu-id="31ecf-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="31ecf-164">請連絡 [Pingboard 用戶端支援小組](https://support.pingboard.com/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="31ecf-164">Contact [Pingboard Client support team](https://support.pingboard.com/) to get these values.</span></span> 

4. <span data-ttu-id="31ecf-165">如果您想要以 **SP** 起始模式設定應用程式，請勾選 [顯示進階 URL 設定]：</span><span class="sxs-lookup"><span data-stu-id="31ecf-165">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    <span data-ttu-id="31ecf-167">a.</span><span class="sxs-lookup"><span data-stu-id="31ecf-167">a.</span></span> <span data-ttu-id="31ecf-168">在 [登入 URL] 文字方塊中，輸入下列值：`http://<sub-domain>.pingboard.com/sign_in`</span><span class="sxs-lookup"><span data-stu-id="31ecf-168">In the **Sign-on URL** textbox, type the value as: `http://<sub-domain>.pingboard.com/sign_in`</span></span>
     
5. <span data-ttu-id="31ecf-169">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="31ecf-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. <span data-ttu-id="31ecf-171">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="31ecf-171">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="31ecf-173">若要在 Pingboard 端上設定 SSO，請開啟新的瀏覽器視窗，然後登入 Pingboard 帳戶。</span><span class="sxs-lookup"><span data-stu-id="31ecf-173">To configure SSO on Pingboard side, open a new browser window and log in to your Pingboard Account.</span></span> <span data-ttu-id="31ecf-174">您必須是 Pingboard 管理員才能設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="31ecf-174">You must be a Pingboard admin to set up single sign on.</span></span>

8. <span data-ttu-id="31ecf-175">從頂端功能表中選取 [應用程式 > 整合]</span><span class="sxs-lookup"><span data-stu-id="31ecf-175">From the top menu select **Apps > Integrations**</span></span>

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  <span data-ttu-id="31ecf-177">在 [整合] 頁面上，尋找 [Azure Active Directory] 圖格，然後按一下它。</span><span class="sxs-lookup"><span data-stu-id="31ecf-177">On the **Integrations** page, find the **"Azure Active Directory"** tile, and click it.</span></span>

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. <span data-ttu-id="31ecf-179">在接下來的強制回應中按一下 [設定]</span><span class="sxs-lookup"><span data-stu-id="31ecf-179">In the modal that follows click **"Configure"**</span></span>

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. <span data-ttu-id="31ecf-181">在下列頁面上，您會注意到「Azure SSO 整合已啟用」。</span><span class="sxs-lookup"><span data-stu-id="31ecf-181">On the following page, you will notice that "Azure SSO Integration is enabled.".</span></span> <span data-ttu-id="31ecf-182">在記事本中開啟下載的中繼資料 XML 檔案，並且將內容貼上到 **IDP 中繼資料**。</span><span class="sxs-lookup"><span data-stu-id="31ecf-182">Open the downloaded Metadata XML file in a notepad and paste the content in **IDP Metadata**.</span></span>

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. <span data-ttu-id="31ecf-184">系統將會驗證檔案，如果所有項目都正確，則會立即啟用單一登入</span><span class="sxs-lookup"><span data-stu-id="31ecf-184">The file will be validated, and if everything is correct, single sign on will now be enabled</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="31ecf-185">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="31ecf-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="31ecf-186">本節目標是在 Azure 管理入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="31ecf-186">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="31ecf-188">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="31ecf-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="31ecf-189">在 **Azure 管理入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="31ecf-189">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="31ecf-191">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="31ecf-191">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="31ecf-193">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="31ecf-193">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="31ecf-195">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="31ecf-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="31ecf-197">a.</span><span class="sxs-lookup"><span data-stu-id="31ecf-197">a.</span></span> <span data-ttu-id="31ecf-198">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="31ecf-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="31ecf-199">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="31ecf-199">b.</span></span> <span data-ttu-id="31ecf-200">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="31ecf-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="31ecf-201">c.</span><span class="sxs-lookup"><span data-stu-id="31ecf-201">c.</span></span> <span data-ttu-id="31ecf-202">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="31ecf-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="31ecf-203">d.</span><span class="sxs-lookup"><span data-stu-id="31ecf-203">d.</span></span> <span data-ttu-id="31ecf-204">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="31ecf-204">Click **Create**.</span></span>
 
### <a name="creating-a-pingboard-test-user"></a><span data-ttu-id="31ecf-205">建立 Pingboard 測試使用者</span><span class="sxs-lookup"><span data-stu-id="31ecf-205">Creating a Pingboard test user</span></span>

<span data-ttu-id="31ecf-206">若要讓 Azure AD 使用者可以登入 Pingboard，則必須將他們佈建到 Pingboard。</span><span class="sxs-lookup"><span data-stu-id="31ecf-206">In order to enable Azure AD users to log into Pingboard, they must be provisioned into Pingboard.</span></span>  
<span data-ttu-id="31ecf-207">Pingboard 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="31ecf-207">In the case of Pingboard, provisioning is a manual task.</span></span>

<span data-ttu-id="31ecf-208">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="31ecf-208">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="31ecf-209">以系統管理員身分登入您的 Pingboard 公司網站。</span><span class="sxs-lookup"><span data-stu-id="31ecf-209">Log in to your Pingboard company site as an administrator.</span></span>

2. <span data-ttu-id="31ecf-210">按一下 [目錄] 頁面上的 [新增員工] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="31ecf-210">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![新增員工](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. <span data-ttu-id="31ecf-212">在 [新增員工] 對話方塊頁面上，執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="31ecf-212">On the **“Add Employee”** dialog page, perform the following steps.</span></span>

    ![邀請人員](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    <span data-ttu-id="31ecf-214">a.</span><span class="sxs-lookup"><span data-stu-id="31ecf-214">a.</span></span> <span data-ttu-id="31ecf-215">在 [全名] 文字方塊中，輸入 Britta Simon 的全名。</span><span class="sxs-lookup"><span data-stu-id="31ecf-215">In the **Full Name** textbox, type the full name of Britta Simon.</span></span>

    <span data-ttu-id="31ecf-216">b.</span><span class="sxs-lookup"><span data-stu-id="31ecf-216">b.</span></span> <span data-ttu-id="31ecf-217">在 [電子郵件] 文字方塊中，輸入 Britta Simon 帳戶的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="31ecf-217">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="31ecf-218">c.</span><span class="sxs-lookup"><span data-stu-id="31ecf-218">c.</span></span> <span data-ttu-id="31ecf-219">在 [職稱] 文字方塊中，輸入 Britta Simon 的職稱。</span><span class="sxs-lookup"><span data-stu-id="31ecf-219">In the **Job Title** textbox, type the job title of Britta Simon.</span></span>

    <span data-ttu-id="31ecf-220">d.</span><span class="sxs-lookup"><span data-stu-id="31ecf-220">d.</span></span> <span data-ttu-id="31ecf-221">在 [位置] 下拉式清單中，選取 Britta Simon 的位置。</span><span class="sxs-lookup"><span data-stu-id="31ecf-221">In the **Location** dropdown, select the location  of Britta Simon.</span></span>
    
    <span data-ttu-id="31ecf-222">e.</span><span class="sxs-lookup"><span data-stu-id="31ecf-222">e.</span></span> <span data-ttu-id="31ecf-223">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="31ecf-223">Click **Add**.</span></span>   

4. <span data-ttu-id="31ecf-224">確認畫面會顯示，供確認新增使用者。</span><span class="sxs-lookup"><span data-stu-id="31ecf-224">A confirmation screen will come up to confirm the addition of user.</span></span>
    
    ![確認](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > <span data-ttu-id="31ecf-226">Azure Active Directory 帳戶的持有者會收到一封電子郵件，並依照連結在啟用其帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="31ecf-226">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="31ecf-227">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="31ecf-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="31ecf-228">在本節中，您會將 Pingboard 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="31ecf-228">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Pingboard.</span></span>

![指派使用者][200] 

<span data-ttu-id="31ecf-230">**若要將 Britta Simon 指派到 Pingboard，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="31ecf-230">**To assign Britta Simon to Pingboard, perform the following steps:**</span></span>

1. <span data-ttu-id="31ecf-231">在 Azure 管理入口網站中，開啟應用程式檢視，然後瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="31ecf-231">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="31ecf-233">在應用程式清單中，選取 [Pingboard]。</span><span class="sxs-lookup"><span data-stu-id="31ecf-233">In the applications list, select **Pingboard**.</span></span>

    ![設定單一登入](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. <span data-ttu-id="31ecf-235">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="31ecf-235">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="31ecf-237">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="31ecf-237">Click **Add** button.</span></span> <span data-ttu-id="31ecf-238">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="31ecf-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="31ecf-240">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="31ecf-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="31ecf-241">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="31ecf-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="31ecf-242">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="31ecf-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="31ecf-243">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="31ecf-243">Testing single sign-on</span></span>

<span data-ttu-id="31ecf-244">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="31ecf-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="31ecf-245">當您在「存取面板」中按一下 Pingboard 圖格時，應該會自動登入您的 Pingboard 應用程式。</span><span class="sxs-lookup"><span data-stu-id="31ecf-245">When you click the Pingboard tile in the Access Panel, you should get automatically signed-on to your Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="31ecf-246">其他資源</span><span class="sxs-lookup"><span data-stu-id="31ecf-246">Additional resources</span></span>

* [<span data-ttu-id="31ecf-247">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="31ecf-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="31ecf-248">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="31ecf-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png

---
title: "教學課程：Azure Active Directory 與 SpringCM 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 SpringCM 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: edfd06a06c730597fee4569ca1ce29092b45244a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a><span data-ttu-id="91635-103">教學課程：Azure Active Directory 與 SpringCM 整合</span><span class="sxs-lookup"><span data-stu-id="91635-103">Tutorial: Azure Active Directory integration with SpringCM</span></span>

<span data-ttu-id="91635-104">在本教學課程中，您將了解如何整合 SpringCM 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="91635-104">In this tutorial, you learn how to integrate SpringCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="91635-105">SpringCM 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="91635-105">Integrating SpringCM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="91635-106">您可以在 Azure AD 中控制可存取 SpringCM 的人員</span><span class="sxs-lookup"><span data-stu-id="91635-106">You can control in Azure AD who has access to SpringCM</span></span>
- <span data-ttu-id="91635-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 SpringCM (單一登入)</span><span class="sxs-lookup"><span data-stu-id="91635-107">You can enable your users to automatically get signed-on to SpringCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="91635-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="91635-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="91635-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="91635-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91635-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="91635-110">Prerequisites</span></span>

<span data-ttu-id="91635-111">若要設定 Azure AD 與 SpringCM 的整合作業，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="91635-111">To configure Azure AD integration with SpringCM, you need the following items:</span></span>

- <span data-ttu-id="91635-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="91635-112">An Azure AD subscription</span></span>
- <span data-ttu-id="91635-113">啟用 SpringCM 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="91635-113">A SpringCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="91635-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="91635-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="91635-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="91635-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="91635-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="91635-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="91635-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="91635-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="91635-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="91635-118">Scenario description</span></span>
<span data-ttu-id="91635-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="91635-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="91635-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="91635-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="91635-121">從資源庫新增 SpringCM</span><span class="sxs-lookup"><span data-stu-id="91635-121">Adding SpringCM from the gallery</span></span>
2. <span data-ttu-id="91635-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="91635-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springcm-from-the-gallery"></a><span data-ttu-id="91635-123">從資源庫新增 SpringCM</span><span class="sxs-lookup"><span data-stu-id="91635-123">Adding SpringCM from the gallery</span></span>
<span data-ttu-id="91635-124">若要設定 SpringCM 與 Azure AD 整合，您需要從資源庫將 SpringCM 加入受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="91635-124">To configure the integration of SpringCM into Azure AD, you need to add SpringCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="91635-125">**若要從資源庫新增 SpringCM，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="91635-125">**To add SpringCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="91635-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="91635-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="91635-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="91635-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="91635-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="91635-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="91635-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="91635-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="91635-133">在搜尋方塊中，輸入 **SpringCM**。</span><span class="sxs-lookup"><span data-stu-id="91635-133">In the search box, type **SpringCM**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_search.png)

5. <span data-ttu-id="91635-135">在結果窗格中，選取 [SpringCM]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="91635-135">In the results panel, select **SpringCM**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="91635-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="91635-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="91635-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 SpringCM 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="91635-138">In this section, you configure and test Azure AD single sign-on with SpringCM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="91635-139">若要讓單一登入運作，Azure AD 必須知道 SpringCM 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="91635-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SpringCM is to a user in Azure AD.</span></span> <span data-ttu-id="91635-140">換句話說，必須在 Azure AD 使用者和 SpringCM 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="91635-140">In other words, a link relationship between an Azure AD user and the related user in SpringCM needs to be established.</span></span>

<span data-ttu-id="91635-141">在 SpringCM 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="91635-141">In SpringCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="91635-142">若要設定及測試與 SpringCM 搭配運作的 Azure AD 單一登入，您需要完成下列建構元素：</span><span class="sxs-lookup"><span data-stu-id="91635-142">To configure and test Azure AD single sign-on with SpringCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="91635-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="91635-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="91635-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="91635-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="91635-145">**[建立 SpringCM 測試使用者](#creating-a-springcm-test-user)** - 使 SpringCM 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="91635-145">**[Creating a SpringCM test user](#creating-a-springcm-test-user)** - to have a counterpart of Britta Simon in SpringCM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="91635-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="91635-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="91635-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="91635-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="91635-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="91635-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="91635-149">在本節中，您會於 Azure 入口網站啟用 Azure AD 單一登入，然後在您的 SpringCM 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="91635-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SpringCM application.</span></span>

<span data-ttu-id="91635-150">**若要使用 SpringCM 設定 Azure AD 單一登入功能，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="91635-150">**To configure Azure AD single sign-on with SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="91635-151">在 Azure 入口網站的 [SpringCM] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="91635-151">In the Azure portal, on the **SpringCM** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="91635-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="91635-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_samlbase.png)

3. <span data-ttu-id="91635-155">在 [SpringCM 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="91635-155">On the **SpringCM Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_url.png)

    <span data-ttu-id="91635-157">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="91635-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="91635-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="91635-158">This value is not real.</span></span> <span data-ttu-id="91635-159">請使用實際的登入 URL 來更新此值。</span><span class="sxs-lookup"><span data-stu-id="91635-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="91635-160">請連絡 [SpringCM 用戶端支援小組](https://knowledge.springcm.com/support)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="91635-160">Contact [SpringCM Client support team](https://knowledge.springcm.com/support) to get this value.</span></span> 
 
4. <span data-ttu-id="91635-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證]\(原始\)，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="91635-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_certificate.png) 

5. <span data-ttu-id="91635-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="91635-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-spring-cm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="91635-165">在 [SpringCM 設定] 區段上，按一下 [設定 SpringCM] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="91635-165">On the **SpringCM Configuration** section, click **Configure SpringCM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="91635-166">從 [快速參考] 區段中複製 [SAML 實體識別碼] 和 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="91635-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_configure.png)   

7. <span data-ttu-id="91635-168">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 **SpringCM** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="91635-168">In a different web browser window, sign on to your **SpringCM** company site as administrator.</span></span>

8. <span data-ttu-id="91635-169">在上方功能表中，依序按一下 [移至]、[喜好設定]，以及 [帳戶喜好設定] 區段中的 [SAML SSO]。</span><span class="sxs-lookup"><span data-stu-id="91635-169">In the menu on the top, click **GO TO**, click **Preferences**, and then, in the **Account Preferences** section, click **SAML SSO**.</span></span>
   
    <span data-ttu-id="91635-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span><span class="sxs-lookup"><span data-stu-id="91635-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span></span>

9. <span data-ttu-id="91635-171">在 [識別提供者組態] 區段執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="91635-171">In the Identity Provider Configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="91635-172">![識別提供者組態](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "識別提供者組態")</span><span class="sxs-lookup"><span data-stu-id="91635-172">![Identity Provider Configuration](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Identity Provider Configuration")</span></span>
    
    <span data-ttu-id="91635-173">a.</span><span class="sxs-lookup"><span data-stu-id="91635-173">a.</span></span> <span data-ttu-id="91635-174">若要上傳已下載的 Azure Active Directory 憑證，請按一下 [選取簽發者憑證] 或 [變更簽發者憑證]。</span><span class="sxs-lookup"><span data-stu-id="91635-174">To upload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span></span>
    
    <span data-ttu-id="91635-175">b.</span><span class="sxs-lookup"><span data-stu-id="91635-175">b.</span></span> <span data-ttu-id="91635-176">將您從 Azure 入口網站複製的 [SAML 實體識別碼] 值貼至 [簽發者] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="91635-176">Paste **SAML Entity ID** value, which you have copied from Azure portal into the **Issuer** textbox.</span></span>
    
    <span data-ttu-id="91635-177">c.</span><span class="sxs-lookup"><span data-stu-id="91635-177">c.</span></span> <span data-ttu-id="91635-178">將您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值，貼到 [服務提供者 (SP) 起始端點] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="91635-178">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **Service Provider (SP) Initiated Endpoint** textbox.</span></span>
            
    <span data-ttu-id="91635-179">d.</span><span class="sxs-lookup"><span data-stu-id="91635-179">d.</span></span> <span data-ttu-id="91635-180">針對 [已啟用 SAML] 選取 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="91635-180">Select **SAML Enabled** as **Enable**.</span></span>

    <span data-ttu-id="91635-181">e.</span><span class="sxs-lookup"><span data-stu-id="91635-181">e.</span></span> <span data-ttu-id="91635-182">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="91635-182">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="91635-183">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="91635-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="91635-184">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="91635-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="91635-185">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="91635-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="91635-186">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="91635-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="91635-187">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="91635-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="91635-189">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="91635-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="91635-190">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="91635-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="91635-192">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="91635-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="91635-194">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="91635-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="91635-196">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="91635-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="91635-198">a.</span><span class="sxs-lookup"><span data-stu-id="91635-198">a.</span></span> <span data-ttu-id="91635-199">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="91635-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="91635-200">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="91635-200">b.</span></span> <span data-ttu-id="91635-201">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="91635-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="91635-202">c.</span><span class="sxs-lookup"><span data-stu-id="91635-202">c.</span></span> <span data-ttu-id="91635-203">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="91635-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="91635-204">d.</span><span class="sxs-lookup"><span data-stu-id="91635-204">d.</span></span> <span data-ttu-id="91635-205">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="91635-205">Click **Create**.</span></span>
 
### <a name="creating-a-springcm-test-user"></a><span data-ttu-id="91635-206">建立 SpringCM 測試使用者</span><span class="sxs-lookup"><span data-stu-id="91635-206">Creating a SpringCM test user</span></span>

<span data-ttu-id="91635-207">若要讓 Azure Active Directory 使用者能夠登入 SpringCM，必須將他們佈建到 SpringCM。</span><span class="sxs-lookup"><span data-stu-id="91635-207">To enable Azure Active Directory users to log in to SpringCM, they must be provisioned into SpringCM.</span></span> <span data-ttu-id="91635-208">SpringCM 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="91635-208">In the case of SpringCM, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="91635-209">如需詳細資訊，請參閱[建立和編輯 SpringCM 使用者](http://knowledge.springcm.com/create-and-edit-a-springcm-user) (英文)。</span><span class="sxs-lookup"><span data-stu-id="91635-209">For more information, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span></span> 

<span data-ttu-id="91635-210">**若要將使用者帳戶佈建到 SpringCM，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="91635-210">**To provision a user account to SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="91635-211">以系統管理員身分登入您的 **SpringCM** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="91635-211">Log in to your **SpringCM** company site as administrator.</span></span>

2. <span data-ttu-id="91635-212">按一下 [移至]，然後按一下 [通訊錄]。</span><span class="sxs-lookup"><span data-stu-id="91635-212">Click **GOTO**, and then click **ADDRESS BOOK**.</span></span>
   
    <span data-ttu-id="91635-213">![建立使用者](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "建立使用者")</span><span class="sxs-lookup"><span data-stu-id="91635-213">![Create User](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Create User")</span></span>

3. <span data-ttu-id="91635-214">按一下 [建立使用者] 。</span><span class="sxs-lookup"><span data-stu-id="91635-214">Click **Create User**.</span></span>

4. <span data-ttu-id="91635-215">選取 [使用者角色] 。</span><span class="sxs-lookup"><span data-stu-id="91635-215">Select a **User Role**.</span></span>

5. <span data-ttu-id="91635-216">選取 [傳送啟用電子郵件] 。</span><span class="sxs-lookup"><span data-stu-id="91635-216">Select **Send Activation Email**.</span></span>

6. <span data-ttu-id="91635-217">在相關的文字方塊中，輸入您想要佈建之有效 Azure Active Directory 使用者帳戶的名字、姓氏和電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="91635-217">Type the first name, last name, and email address of a valid Azure Active Directory user account you want to provision into the related textboxes.</span></span>

7. <span data-ttu-id="91635-218">將該使用者加入 [安全性群組] 。</span><span class="sxs-lookup"><span data-stu-id="91635-218">Add the user to a **Security group**.</span></span>

8. <span data-ttu-id="91635-219">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="91635-219">Click **Save**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="91635-220">您可以使用任何其他的 SpringCM 使用者帳戶建立工具或 SpringCM 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="91635-220">You can use any other SpringCM user account creation tools or APIs provided by SpringCM to provision AAD user accounts.</span></span>  
  > 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="91635-221">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="91635-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="91635-222">在本節中，您會將 SpringCM 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="91635-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SpringCM.</span></span>

![指派使用者][200] 

<span data-ttu-id="91635-224">**若要將 Britta Simon 指派給 SpringCM，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="91635-224">**To assign Britta Simon to SpringCM, perform the following steps:**</span></span>

1. <span data-ttu-id="91635-225">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="91635-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="91635-227">在應用程式清單中，選取 [SpringCM]。</span><span class="sxs-lookup"><span data-stu-id="91635-227">In the applications list, select **SpringCM**.</span></span>

    ![設定單一登入](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_app.png) 

3. <span data-ttu-id="91635-229">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="91635-229">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="91635-231">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="91635-231">Click **Add** button.</span></span> <span data-ttu-id="91635-232">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="91635-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="91635-234">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="91635-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="91635-235">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="91635-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="91635-236">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="91635-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="91635-237">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="91635-237">Testing single sign-on</span></span>

<span data-ttu-id="91635-238">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="91635-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="91635-239">當您在「存取面板」中按一下 [SpringCM] 圖格時，應該會自動登入您的 SpringCM 應用程式。</span><span class="sxs-lookup"><span data-stu-id="91635-239">When you click the SpringCM tile in the Access Panel, you should get automatically signed-on to your SpringCM application.</span></span>

<span data-ttu-id="91635-240">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="91635-240">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="91635-241">其他資源</span><span class="sxs-lookup"><span data-stu-id="91635-241">Additional resources</span></span>

* [<span data-ttu-id="91635-242">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="91635-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="91635-243">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="91635-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_203.png


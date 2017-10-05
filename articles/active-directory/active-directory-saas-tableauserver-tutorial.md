---
title: "教學課程：Azure Active Directory 與 Tableau Server 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Tableau Server 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 6b35609d88fbbf649e15863901d521886db2a4d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="e3532-103">教學課程：Azure Active Directory 與 Tableau Server 整合</span><span class="sxs-lookup"><span data-stu-id="e3532-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>

<span data-ttu-id="e3532-104">在本教學課程中，您將了解如何整合 Tableau Server 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="e3532-104">In this tutorial, you learn how to integrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e3532-105">Tableau Server 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="e3532-105">Integrating Tableau Server with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e3532-106">您可以在 Azure AD 中控制可存取 Tableau Server 的人員</span><span class="sxs-lookup"><span data-stu-id="e3532-106">You can control in Azure AD who has access to Tableau Server</span></span>
- <span data-ttu-id="e3532-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Tableau Server (單一登入)</span><span class="sxs-lookup"><span data-stu-id="e3532-107">You can enable your users to automatically get signed-on to Tableau Server (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e3532-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="e3532-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e3532-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="e3532-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3532-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="e3532-110">Prerequisites</span></span>

<span data-ttu-id="e3532-111">若要設定 Azure AD 與 Tableau Server 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="e3532-111">To configure Azure AD integration with Tableau Server, you need the following items:</span></span>

- <span data-ttu-id="e3532-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e3532-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e3532-113">已啟用 Tableau Server 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e3532-113">A Tableau Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e3532-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e3532-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e3532-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="e3532-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e3532-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e3532-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e3532-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="e3532-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e3532-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="e3532-118">Scenario description</span></span>
<span data-ttu-id="e3532-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e3532-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e3532-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="e3532-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e3532-121">從資源庫新增 Tableau Server</span><span class="sxs-lookup"><span data-stu-id="e3532-121">Adding Tableau Server from the gallery</span></span>
2. <span data-ttu-id="e3532-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e3532-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-server-from-the-gallery"></a><span data-ttu-id="e3532-123">從資源庫新增 Tableau Server</span><span class="sxs-lookup"><span data-stu-id="e3532-123">Adding Tableau Server from the gallery</span></span>
<span data-ttu-id="e3532-124">若要設定 Tableau Server 與 Azure AD 整合，您需要從資源庫將 Tableau Server 加入到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="e3532-124">To configure the integration of Tableau Server into Azure AD, you need to add Tableau Server from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e3532-125">**如要從資源庫新增 Tableau Server，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e3532-125">**To add Tableau Server from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e3532-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e3532-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e3532-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e3532-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e3532-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e3532-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="e3532-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e3532-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="e3532-133">在搜尋方塊中，輸入 **Tableau Server**。</span><span class="sxs-lookup"><span data-stu-id="e3532-133">In the search box, type **Tableau Server**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. <span data-ttu-id="e3532-135">在結果窗格中，選取 [Tableau Server]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="e3532-135">In the results panel, select **Tableau Server**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e3532-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e3532-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e3532-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Tableau Server 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e3532-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e3532-139">若要讓單一登入運作，Azure AD 必須知道 Tableau Server 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="e3532-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Server is to a user in Azure AD.</span></span> <span data-ttu-id="e3532-140">換句話說，必須在 Azure AD 使用者和 Tableau Server 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e3532-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Server needs to be established.</span></span>

<span data-ttu-id="e3532-141">在 Tableau Server 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e3532-141">In Tableau Server, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e3532-142">若要使用 Tableau Server 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="e3532-142">To configure and test Azure AD single sign-on with Tableau Server, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e3532-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="e3532-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e3532-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e3532-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e3532-145">**[建立 Tableau Server 測試使用者](#creating-a-tableau-server-test-user)** - 使 Tableau Server 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="e3532-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - to have a counterpart of Britta Simon in Tableau Server that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e3532-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e3532-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e3532-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="e3532-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e3532-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e3532-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e3532-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Tableau Server 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="e3532-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Server application.</span></span>

<span data-ttu-id="e3532-150">**若要設定透過 Tableau Server 使用 Azure AD 單一登入功能，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e3532-150">**To configure Azure AD single sign-on with Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="e3532-151">在 Azure 入口網站的 [Tableau Server] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="e3532-151">In the Azure portal, on the **Tableau Server** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="e3532-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="e3532-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. <span data-ttu-id="e3532-155">在 [Tableau Server 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e3532-155">On the **Tableau Server Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    <span data-ttu-id="e3532-157">a.</span><span class="sxs-lookup"><span data-stu-id="e3532-157">a.</span></span> <span data-ttu-id="e3532-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="e3532-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span></span>
    
    <span data-ttu-id="e3532-159">b.</span><span class="sxs-lookup"><span data-stu-id="e3532-159">b.</span></span> <span data-ttu-id="e3532-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="e3532-160">In the **Identifier** textbox, type a URL using the following pattern: `https://azure.<domain name>.link`</span></span>

    <span data-ttu-id="e3532-161">c.</span><span class="sxs-lookup"><span data-stu-id="e3532-161">c.</span></span> <span data-ttu-id="e3532-162">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://azure.<domain name>.link/wg/saml/SSO/index.html`</span><span class="sxs-lookup"><span data-stu-id="e3532-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="e3532-163">上述值並非真正的值。</span><span class="sxs-lookup"><span data-stu-id="e3532-163">The preceding values are not real values.</span></span> <span data-ttu-id="e3532-164">稍後您將使用 [Tableau Server 設定] 頁面中實際的 URL 和識別碼來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="e3532-164">Later, you update the values with the actual URL and identifier from the Tableau Server configuration page.</span></span> 

4. <span data-ttu-id="e3532-165">Tableau Server 應用程式需要特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="e3532-165">Tableau Server application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="e3532-166">設定此應用程式的下列宣告。</span><span class="sxs-lookup"><span data-stu-id="e3532-166">Configure the following claims for this application.</span></span> <span data-ttu-id="e3532-167">您可以在應用程式整合頁面的 [使用者屬性] 區段中管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="e3532-167">You can manage the values of these attributes from the **"User Attributes"** section on application integration page.</span></span> <span data-ttu-id="e3532-168">下列螢幕擷取畫面顯示相同範例。</span><span class="sxs-lookup"><span data-stu-id="e3532-168">The following screenshot shows an example for the same.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. <span data-ttu-id="e3532-170">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如上圖所示設定 SAML 權杖屬性，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e3532-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="e3532-171">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="e3532-171">Attribute Name</span></span> | <span data-ttu-id="e3532-172">屬性值</span><span class="sxs-lookup"><span data-stu-id="e3532-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="e3532-173">username</span><span class="sxs-lookup"><span data-stu-id="e3532-173">username</span></span> | <span data-ttu-id="e3532-174">*user.displayname*</span><span class="sxs-lookup"><span data-stu-id="e3532-174">*user.displayname*</span></span> |

    <span data-ttu-id="e3532-175">a.</span><span class="sxs-lookup"><span data-stu-id="e3532-175">a.</span></span> <span data-ttu-id="e3532-176">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="e3532-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="e3532-179">b.</span><span class="sxs-lookup"><span data-stu-id="e3532-179">b.</span></span> <span data-ttu-id="e3532-180">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="e3532-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="e3532-181">c.</span><span class="sxs-lookup"><span data-stu-id="e3532-181">c.</span></span> <span data-ttu-id="e3532-182">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="e3532-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="e3532-183">d.</span><span class="sxs-lookup"><span data-stu-id="e3532-183">d.</span></span> <span data-ttu-id="e3532-184">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e3532-184">Click **Ok**</span></span>


6. <span data-ttu-id="e3532-185">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="e3532-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. <span data-ttu-id="e3532-187">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e3532-187">Click **Save** button.</span></span>

    <span data-ttu-id="e3532-188">![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="e3532-188">![Configure Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span></span>
8. <span data-ttu-id="e3532-189">若要取得為應用程式設定的 SSO，您必須以系統管理員身分登入 Tableau Server 租用戶。</span><span class="sxs-lookup"><span data-stu-id="e3532-189">To get SSO configured for your application, you need to sign-on to your Tableau Server tenant as an administrator.</span></span>
   
   <span data-ttu-id="e3532-190">a.</span><span class="sxs-lookup"><span data-stu-id="e3532-190">a.</span></span> <span data-ttu-id="e3532-191">在 Tableau Server 組態中，按一下 [SAML] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e3532-191">In the Tableau Server configuration, click the **SAML** tab.</span></span>
  
    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   <span data-ttu-id="e3532-193">b.</span><span class="sxs-lookup"><span data-stu-id="e3532-193">b.</span></span> <span data-ttu-id="e3532-194">選取 [使用 SAML 進行單一登入] 的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="e3532-194">Select the checkbox of **Use SAML for single sign-on**.</span></span>
   
   <span data-ttu-id="e3532-195">c.</span><span class="sxs-lookup"><span data-stu-id="e3532-195">c.</span></span> <span data-ttu-id="e3532-196">Tableau Server 傳回 URL—Tableau Server 使用者將存取的 URL，例如 http://tableau_server。</span><span class="sxs-lookup"><span data-stu-id="e3532-196">Tableau Server return URL—The URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="e3532-197">不建議使用 http://localhost。</span><span class="sxs-lookup"><span data-stu-id="e3532-197">Using http://localhost is not recommended.</span></span> <span data-ttu-id="e3532-198">不支援使用包含結尾斜線的 URL (例如，http://tableau_server/)。</span><span class="sxs-lookup"><span data-stu-id="e3532-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="e3532-199">複製 [Tableau Server 傳回 URL]，並將其貼到 [Tableau Server 網域及 URL] 區段中的 Azure AD [單一登入 URL] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="e3532-199">Copy **Tableau Server return URL** and paste it to Azure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="e3532-200">d.</span><span class="sxs-lookup"><span data-stu-id="e3532-200">d.</span></span> <span data-ttu-id="e3532-201">SAML 實體識別碼—實體識別碼可唯一識別安裝至 IdP 的 Tableau Server。</span><span class="sxs-lookup"><span data-stu-id="e3532-201">SAML entity ID—The entity ID uniquely identifies your Tableau Server installation to the IdP.</span></span> <span data-ttu-id="e3532-202">您可以依意願再次在這裡輸入 Tableau Server URL，但是它不一定是您的 Tableau Server URL。</span><span class="sxs-lookup"><span data-stu-id="e3532-202">You can enter your Tableau Server URL again here, if you like, but it does not have to be your Tableau Server URL.</span></span> <span data-ttu-id="e3532-203">複製 [SAML 實體識別碼]，並將其貼到 [Tableau Server 網域及 URL] 區段中的 Azure AD [識別碼] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="e3532-203">Copy **SAML entity ID** and paste it to Azure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span></span>
     
   <span data-ttu-id="e3532-204">e.</span><span class="sxs-lookup"><span data-stu-id="e3532-204">e.</span></span> <span data-ttu-id="e3532-205">按一下 [匯出中繼資料檔案]，並在文字編輯器應用程式中將其開啟。</span><span class="sxs-lookup"><span data-stu-id="e3532-205">Click the **Export Metadata File** and open it in the text editor application.</span></span> <span data-ttu-id="e3532-206">利用 Http Post 與索引 0 找出判斷提示取用者服務 URL，並複製 URL。</span><span class="sxs-lookup"><span data-stu-id="e3532-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy the URL.</span></span> <span data-ttu-id="e3532-207">現在將其貼到 [Tableau Server 網域及 URL] 區段中的 Azure AD [回覆 URL] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="e3532-207">Now paste it to Azure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="e3532-208">f.</span><span class="sxs-lookup"><span data-stu-id="e3532-208">f.</span></span> <span data-ttu-id="e3532-209">尋找從 Azure 入口網站下載的同盟中繼資料檔案，然後在 [SAML Idp 中繼資料檔案] 中將其上傳。</span><span class="sxs-lookup"><span data-stu-id="e3532-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in the **SAML Idp metadata file**.</span></span>
   
   <span data-ttu-id="e3532-210">g.</span><span class="sxs-lookup"><span data-stu-id="e3532-210">g.</span></span> <span data-ttu-id="e3532-211">按一下 [Tableau Server 設定] 頁面中的 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e3532-211">Click the **OK** button in the Tableau Server Configuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="e3532-212">客戶必須在 [Tableau Server SAML SSO 設定] 中上傳任何憑證，系統將在 SSO 流程中忽略該憑證。</span><span class="sxs-lookup"><span data-stu-id="e3532-212">Customer have to upload any certificate in the Tableau Server SAML SSO configuration and it will get ignored in the SSO flow.</span></span>
    ><span data-ttu-id="e3532-213">如果您需要在 Tableau Server 上設定 SAML 的協助，請參閱[設定 SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm)。</span><span class="sxs-lookup"><span data-stu-id="e3532-213">If you need help configuring SAML on Tableau Server then please refer to this article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >
<CE>

> [!TIP]
> <span data-ttu-id="e3532-214">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="e3532-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e3532-215">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="e3532-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e3532-216">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e3532-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e3532-217">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e3532-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="e3532-218">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="e3532-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="e3532-220">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e3532-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e3532-221">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e3532-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e3532-223">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="e3532-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e3532-225">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e3532-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e3532-227">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e3532-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e3532-229">a.</span><span class="sxs-lookup"><span data-stu-id="e3532-229">a.</span></span> <span data-ttu-id="e3532-230">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="e3532-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e3532-231">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e3532-231">b.</span></span> <span data-ttu-id="e3532-232">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="e3532-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e3532-233">c.</span><span class="sxs-lookup"><span data-stu-id="e3532-233">c.</span></span> <span data-ttu-id="e3532-234">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="e3532-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e3532-235">d.</span><span class="sxs-lookup"><span data-stu-id="e3532-235">d.</span></span> <span data-ttu-id="e3532-236">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="e3532-236">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-server-test-user"></a><span data-ttu-id="e3532-237">建立 Tableau Server 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e3532-237">Creating a Tableau Server test user</span></span>

<span data-ttu-id="e3532-238">本節目標是在 Tableau Server 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="e3532-238">The objective of this section is to create a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="e3532-239">您必須在 Tableau Server 中佈建所有使用者。</span><span class="sxs-lookup"><span data-stu-id="e3532-239">You need to provision all the users in the Tableau server.</span></span> 

<span data-ttu-id="e3532-240">使用者的使用者名稱應符合您在 Azure AD 自訂屬性 **username** 中設定的值。</span><span class="sxs-lookup"><span data-stu-id="e3532-240">That username of the user should match the value which you have configured in the Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="e3532-241">透過正確的對應，應該可以有效整合， [設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)。</span><span class="sxs-lookup"><span data-stu-id="e3532-241">With the correct mapping the integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="e3532-242">如果您需要以手動方式建立使用者，您必須連絡貴組織的 Tableau Server 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="e3532-242">If you need to create a user manually, you need to contact the Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e3532-243">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e3532-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e3532-244">在本節中，您會將 Tableau Server 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e3532-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Server.</span></span>

![指派使用者][200] 

<span data-ttu-id="e3532-246">**如要將 Britta Simon 指派給 Tableau Server，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e3532-246">**To assign Britta Simon to Tableau Server, perform the following steps:**</span></span>

1. <span data-ttu-id="e3532-247">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e3532-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="e3532-249">在應用程式清單中，選取 [Tableau Server] 。</span><span class="sxs-lookup"><span data-stu-id="e3532-249">In the applications list, select **Tableau Server**.</span></span>

    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. <span data-ttu-id="e3532-251">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e3532-251">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="e3532-253">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e3532-253">Click **Add** button.</span></span> <span data-ttu-id="e3532-254">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e3532-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="e3532-256">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="e3532-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e3532-257">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e3532-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e3532-258">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e3532-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e3532-259">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="e3532-259">Testing single sign-on</span></span>

<span data-ttu-id="e3532-260">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="e3532-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e3532-261">當您在存取面板中按一下 [Tableau Server] 圖格時，應該會自動登入您的 Tableau Server 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e3532-261">When you click the Tableau Server tile in the Access Panel, you should get automatically signed-on to your Tableau Server application.</span></span>
<span data-ttu-id="e3532-262">如需存取面板的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="e3532-262">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e3532-263">其他資源</span><span class="sxs-lookup"><span data-stu-id="e3532-263">Additional resources</span></span>

* [<span data-ttu-id="e3532-264">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="e3532-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e3532-265">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="e3532-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png


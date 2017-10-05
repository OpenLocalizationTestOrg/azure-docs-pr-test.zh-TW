---
title: "教學課程：Azure Active Directory 與 Velpic SAML 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Velpic SAML 之間的單一登入。"
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
ms.openlocfilehash: 5325f3cca00167e6b7b687509ce43435447ad2f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="81d47-103">教學課程：Azure Active Directory 與 Velpic SAML 整合</span><span class="sxs-lookup"><span data-stu-id="81d47-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="81d47-104">在本教學課程中，您將了解如何整合 Velpic SAML 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="81d47-104">In this tutorial, you learn how to integrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="81d47-105">Velpic SAML 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="81d47-105">Integrating Velpic SAML with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="81d47-106">您可以在 Azure AD 中控制可存取 Velpic SAML 的人員</span><span class="sxs-lookup"><span data-stu-id="81d47-106">You can control in Azure AD who has access to Velpic SAML</span></span>
- <span data-ttu-id="81d47-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Velpic SAML (單一登入)</span><span class="sxs-lookup"><span data-stu-id="81d47-107">You can enable your users to automatically get signed-on to Velpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="81d47-108">您可以在 Azure 管理入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="81d47-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="81d47-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="81d47-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81d47-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="81d47-110">Prerequisites</span></span>

<span data-ttu-id="81d47-111">若要設定與 Velpic SAML 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="81d47-111">To configure Azure AD integration with Velpic SAML, you need the following items:</span></span>

- <span data-ttu-id="81d47-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="81d47-112">An Azure AD subscription</span></span>
- <span data-ttu-id="81d47-113">啟用 Velpic SAML 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="81d47-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="81d47-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="81d47-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="81d47-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="81d47-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="81d47-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="81d47-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="81d47-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="81d47-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="81d47-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="81d47-118">Scenario description</span></span>
<span data-ttu-id="81d47-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="81d47-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="81d47-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="81d47-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="81d47-121">從資源庫新增 Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="81d47-121">Adding Velpic SAML from the gallery</span></span>
2. <span data-ttu-id="81d47-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="81d47-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-the-gallery"></a><span data-ttu-id="81d47-123">從資源庫新增 Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="81d47-123">Adding Velpic SAML from the gallery</span></span>
<span data-ttu-id="81d47-124">若要設定 Velpic SAML 與 Azure AD 整合，您需要從資源庫將 Velpic SAML 新增到受管理的 SaaS app 清單。</span><span class="sxs-lookup"><span data-stu-id="81d47-124">To configure the integration of Velpic SAML into Azure AD, you need to add Velpic SAML from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="81d47-125">**若要從資源庫新增 Velpic SAML，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="81d47-125">**To add Velpic SAML from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="81d47-126">在 **[Azure 管理入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="81d47-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="81d47-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="81d47-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="81d47-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="81d47-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="81d47-131">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="81d47-131">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="81d47-133">在搜尋方塊中，輸入 **Velpic SAML**。</span><span class="sxs-lookup"><span data-stu-id="81d47-133">In the search box, type **Velpic SAML**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="81d47-135">在結果窗格中，選取 [Velpic SAML]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="81d47-135">In the results panel, select **Velpic SAML**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="81d47-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="81d47-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="81d47-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Velpic SAML 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="81d47-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="81d47-139">若要讓單一登入運作，Azure AD 必須知道 Velpic SAML 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="81d47-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Velpic SAML is to a user in Azure AD.</span></span> <span data-ttu-id="81d47-140">換句話說，必須建立 Azure AD 使用者和 Velpic SAML 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="81d47-140">In other words, a link relationship between an Azure AD user and the related user in Velpic SAML needs to be established.</span></span>

<span data-ttu-id="81d47-141">建立此連結關聯性的方法是將 Azure AD 中**使用者名稱**的值指定為 Velpic SAML 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="81d47-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Velpic SAML.</span></span>

<span data-ttu-id="81d47-142">若要設定及測試與 Velpic SAML 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="81d47-142">To configure and test Azure AD single sign-on with Velpic SAML, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="81d47-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="81d47-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="81d47-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="81d47-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="81d47-145">**[建立 Velpic SAML 測試使用者](#creating-a-velpic-saml-test-user)** - 在 Velpic SAML 中建立一個與 Azure AD 中代表 Britta Simon 的項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="81d47-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - to have a counterpart of Britta Simon in Velpic SAML that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="81d47-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="81d47-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="81d47-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="81d47-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="81d47-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="81d47-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="81d47-149">在本節中，您會在 Azure 管理入口網站中啟用 Azure AD 單一登入，並在您的 Velpic SAML 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="81d47-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="81d47-150">**若要設定與 Velpic SAML 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="81d47-150">**To configure Azure AD single sign-on with Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="81d47-151">在 Azure 管理入口網站的 [Velpic SAML] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="81d47-151">In the Azure Management portal, on the **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="81d47-153">在 [單一登入] 對話方塊上，選取 [SAML 型登入] 做為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="81d47-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="81d47-155">在 [Velpic SAML 網域和 URL] 區段中輸入詳細資料</span><span class="sxs-lookup"><span data-stu-id="81d47-155">Enter the details in the **Velpic SAML Domain and URLs** section-</span></span>

    ![設定單一登入](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="81d47-157">a.</span><span class="sxs-lookup"><span data-stu-id="81d47-157">a.</span></span> <span data-ttu-id="81d47-158">在 [登入 URL] 文字方塊中，輸入下列值：`https://<sub-domain>.velpicsaml.net`</span><span class="sxs-lookup"><span data-stu-id="81d47-158">In the **Sign-on URL** textbox, type the value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="81d47-159">b.</span><span class="sxs-lookup"><span data-stu-id="81d47-159">b.</span></span> <span data-ttu-id="81d47-160">在 [識別碼] 文字方塊中，貼上**「單一登入 URL」**值`https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="81d47-160">In the **Identifier** textbox, paste the **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="81d47-161">請注意，登入 URL 會由 Velpic SAML 小組提供，而識別碼值則會在您於 Velpic SAML 端設定 SSO 外掛程式時可供取得。</span><span class="sxs-lookup"><span data-stu-id="81d47-161">Please note that the Sign on URL will be provided by the Velpic SAML team and Identifier value will be available when you configure the SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="81d47-162">您需要從 Velpic SAML 應用程式頁面將該值複製並貼到此處。</span><span class="sxs-lookup"><span data-stu-id="81d47-162">You need to copy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="81d47-163">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="81d47-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="81d47-165">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="81d47-165">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="81d47-167">在 [Velpic SAML 組態] 區段上，按一下 [設定 Velpic SAML] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="81d47-167">On the Velpic SAML Configuration section, click Configure Velpic SAML to open Configure sign-on window.</span></span> <span data-ttu-id="81d47-168">從 [快速參考] 區段複製 SAML 實體識別碼。</span><span class="sxs-lookup"><span data-stu-id="81d47-168">Copy the SAML Entity ID from the Quick Reference section.</span></span>

7. <span data-ttu-id="81d47-169">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Velpic SAML 公司網站。</span><span class="sxs-lookup"><span data-stu-id="81d47-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="81d47-170">按一下 [管理] 索引標籤，然後移至 [整合] 區段，您必須在此處按一下 [外掛程式] 按鈕以建立用於登入的新外掛程式。</span><span class="sxs-lookup"><span data-stu-id="81d47-170">Click on **Manage** tab and go to **Integration** section where you need to click on **Plugins** button to create new plugin for Sign-In.</span></span>

    ![外掛程式](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="81d47-172">按一下 [新增外掛程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="81d47-172">Click on the **‘Add plugin’** button.</span></span>
    
    ![外掛程式](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="81d47-174">按一下 [新增外掛程式] 頁面中的 [SAML] 圖格。</span><span class="sxs-lookup"><span data-stu-id="81d47-174">Click on the **SAML** tile in the Add Plugin page.</span></span>
    
    ![外掛程式](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="81d47-176">為新的 SAML 外掛程式輸入名稱，然後按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="81d47-176">Enter the name of the new SAML plugin and click the **‘Add’** button.</span></span>

    ![外掛程式](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="81d47-178">輸入詳細資料，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="81d47-178">Enter the details as follows:</span></span>

    ![外掛程式](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="81d47-180">a.</span><span class="sxs-lookup"><span data-stu-id="81d47-180">a.</span></span> <span data-ttu-id="81d47-181">在 [名稱] 文字方塊中，輸入 SAML 外掛程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="81d47-181">In the **Name** textbox, type the name of SAML plugin.</span></span>

    <span data-ttu-id="81d47-182">b.</span><span class="sxs-lookup"><span data-stu-id="81d47-182">b.</span></span> <span data-ttu-id="81d47-183">在 [簽發者 URL] 文字方塊中，貼上您從 Azure 入口網站的 [設定登入] 視窗中所複製的 [SAML 實體識別碼]。</span><span class="sxs-lookup"><span data-stu-id="81d47-183">In the **Issuer URL** textbox, paste the **SAML Entity ID** you copied from the **Configure sign-on** window of the Azure portal.</span></span>

    <span data-ttu-id="81d47-184">c.</span><span class="sxs-lookup"><span data-stu-id="81d47-184">c.</span></span> <span data-ttu-id="81d47-185">在 [提供者中繼資料設定] 中，上傳您從 Azure 入口網站下載的中繼資料 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="81d47-185">In the **Provider Metadata Config** upload the Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="81d47-186">d.</span><span class="sxs-lookup"><span data-stu-id="81d47-186">d.</span></span> <span data-ttu-id="81d47-187">您也可以選擇啟用 [自動建立新使用者] 核取方塊，來啟用 SAML 即時佈建。</span><span class="sxs-lookup"><span data-stu-id="81d47-187">You can also choose to enable SAML just in time provisioning by enabling the **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="81d47-188">如果使用者不存在於 Velpic，而且這個旗標未啟用，從 Azure 登入時就會失敗。</span><span class="sxs-lookup"><span data-stu-id="81d47-188">If a user doesn’t exist in Velpic and this flag is not enabled, the login from Azure will fail.</span></span> <span data-ttu-id="81d47-189">如果該旗標已啟用，則系統會在使用者登入時自動將其佈建到 Velpic。</span><span class="sxs-lookup"><span data-stu-id="81d47-189">If the flag is enabled the user will automatically be provisioned into Velpic at the time of login.</span></span> 

    <span data-ttu-id="81d47-190">e.</span><span class="sxs-lookup"><span data-stu-id="81d47-190">e.</span></span> <span data-ttu-id="81d47-191">從文字方塊複製**單一登入 URL**，並將它貼到 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="81d47-191">Copy the **Single sign on URL** from the text box and paste it in the Azure portal.</span></span>
    
    <span data-ttu-id="81d47-192">f.</span><span class="sxs-lookup"><span data-stu-id="81d47-192">f.</span></span> <span data-ttu-id="81d47-193">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="81d47-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="81d47-194">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="81d47-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="81d47-195">本節目標是在 Azure 管理入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="81d47-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="81d47-197">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="81d47-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="81d47-198">在 **Azure 管理入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="81d47-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="81d47-200">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="81d47-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="81d47-202">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="81d47-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="81d47-204">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="81d47-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="81d47-206">a.</span><span class="sxs-lookup"><span data-stu-id="81d47-206">a.</span></span> <span data-ttu-id="81d47-207">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="81d47-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="81d47-208">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="81d47-208">b.</span></span> <span data-ttu-id="81d47-209">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="81d47-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="81d47-210">c.</span><span class="sxs-lookup"><span data-stu-id="81d47-210">c.</span></span> <span data-ttu-id="81d47-211">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="81d47-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="81d47-212">d.</span><span class="sxs-lookup"><span data-stu-id="81d47-212">d.</span></span> <span data-ttu-id="81d47-213">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="81d47-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="81d47-214">建立 Velpic SAML 測試使用者</span><span class="sxs-lookup"><span data-stu-id="81d47-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="81d47-215">您通常不需要進行此步驟，因為應用程式支援即時使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="81d47-215">This step is usually not required as the application supports just in time user provisioning.</span></span> <span data-ttu-id="81d47-216">如果自動使用者佈建未啟用，那麼您可以如下所述手動建立使用者。</span><span class="sxs-lookup"><span data-stu-id="81d47-216">If the automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="81d47-217">以系統管理員身分登入您的 Velpic SAML 公司網站，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="81d47-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="81d47-218">按一下 [管理] 索引標籤並移至 [使用者] 區段，然後按一下 [新增] 按鈕來新增使用者。</span><span class="sxs-lookup"><span data-stu-id="81d47-218">Click on Manage tab and go to Users section, then click on New button to add users.</span></span>

    ![新增使用者](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="81d47-220">在 [建立新的使用者] 對話方塊中，執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="81d47-220">On the **“Create New User”** dialog page, perform the following steps.</span></span>

    ![user](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="81d47-222">a.</span><span class="sxs-lookup"><span data-stu-id="81d47-222">a.</span></span> <span data-ttu-id="81d47-223">在 [名字] 文字方塊中，輸入 Britta Simon 的名字。</span><span class="sxs-lookup"><span data-stu-id="81d47-223">In the **First Name** textbox, type the first name of Britta Simon.</span></span>

    <span data-ttu-id="81d47-224">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="81d47-224">b.</span></span> <span data-ttu-id="81d47-225">在 [姓氏] 文字方塊中，輸入 Britta Simon 的姓氏。</span><span class="sxs-lookup"><span data-stu-id="81d47-225">In the **Last Name** textbox, type the last name of Britta Simon.</span></span>

    <span data-ttu-id="81d47-226">c.</span><span class="sxs-lookup"><span data-stu-id="81d47-226">c.</span></span> <span data-ttu-id="81d47-227">在 [使用者名稱] 文字方塊中，輸入 Britta Simon 的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="81d47-227">In the **User Name** textbox, type the user name of Britta Simon.</span></span>

    <span data-ttu-id="81d47-228">d.</span><span class="sxs-lookup"><span data-stu-id="81d47-228">d.</span></span> <span data-ttu-id="81d47-229">在 [電子郵件] 文字方塊中，輸入 Britta Simon 帳戶的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="81d47-229">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="81d47-230">e.</span><span class="sxs-lookup"><span data-stu-id="81d47-230">e.</span></span> <span data-ttu-id="81d47-231">其餘資訊是選擇性的，您可以視需要來填入。</span><span class="sxs-lookup"><span data-stu-id="81d47-231">Rest of the information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="81d47-232">f.</span><span class="sxs-lookup"><span data-stu-id="81d47-232">f.</span></span> <span data-ttu-id="81d47-233">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="81d47-233">Click **SAVE**.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="81d47-234">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="81d47-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="81d47-235">在本節中，您會授權 Britta Simon 存取 Velpic SAML，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="81d47-235">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Velpic SAML.</span></span>

![指派使用者][200] 

<span data-ttu-id="81d47-237">**若要將 Britta Simon 指派到 Velpic SAML，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="81d47-237">**To assign Britta Simon to Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="81d47-238">在 Azure 管理入口網站中，開啟應用程式檢視，然後瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="81d47-238">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="81d47-240">在應用程式清單中，選取 [Velpic SAML]。</span><span class="sxs-lookup"><span data-stu-id="81d47-240">In the applications list, select **Velpic SAML**.</span></span>

    ![設定單一登入](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="81d47-242">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="81d47-242">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="81d47-244">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="81d47-244">Click **Add** button.</span></span> <span data-ttu-id="81d47-245">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="81d47-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="81d47-247">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="81d47-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="81d47-248">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="81d47-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="81d47-249">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="81d47-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="81d47-250">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="81d47-250">Testing single sign-on</span></span>

<span data-ttu-id="81d47-251">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="81d47-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="81d47-252">當您按一下存取面板中的 [Velpic SAML] 圖格時，您應該會看到 Velpic SAML 應用程式的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="81d47-252">When you click the Velpic SAML tile in the Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="81d47-253">您應該會在登入頁面上看到 [以 Azure AD 登入] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="81d47-253">You should see the **‘Log In With Azure AD’** button on the sign in page.</span></span>

    ![外掛程式](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="81d47-255">按一下 [以 Azure AD 登入] 按鈕以使用 Azure AD 帳戶登入 Velpic。</span><span class="sxs-lookup"><span data-stu-id="81d47-255">Click on the **‘Log In With Azure AD’** button to log in to Velpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="81d47-256">其他資源</span><span class="sxs-lookup"><span data-stu-id="81d47-256">Additional resources</span></span>

* [<span data-ttu-id="81d47-257">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="81d47-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="81d47-258">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="81d47-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png


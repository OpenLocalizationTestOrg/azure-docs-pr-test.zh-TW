---
title: "教學課程：Azure Active Directory 與 Replicon Gateway 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Reward Gateway 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34336386-998a-4d47-ab55-721d97708e5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: b1a468caa22159ad603dbec1ef530e7e0e24f96d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-reward-gateway"></a><span data-ttu-id="ba862-103">教學課程：Azure Active Directory 與 Replicon Gateway 整合</span><span class="sxs-lookup"><span data-stu-id="ba862-103">Tutorial: Azure Active Directory integration with Reward Gateway</span></span>

<span data-ttu-id="ba862-104">在本教學課程中，您會了解如何將 Reward Gateway 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="ba862-104">In this tutorial, you learn how to integrate Reward Gateway with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ba862-105">將 Reward Gateway 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="ba862-105">Integrating Reward Gateway with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ba862-106">您可以在 Azure AD 中控制可存取 Reward Gateway 的人員</span><span class="sxs-lookup"><span data-stu-id="ba862-106">You can control in Azure AD who has access to Reward Gateway</span></span>
- <span data-ttu-id="ba862-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Reward Gateway (單一登入)</span><span class="sxs-lookup"><span data-stu-id="ba862-107">You can enable your users to automatically get signed-on to Reward Gateway (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ba862-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="ba862-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ba862-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ba862-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba862-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ba862-110">Prerequisites</span></span>

<span data-ttu-id="ba862-111">若要設定 Azure AD 與 Reward Gateway 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="ba862-111">To configure Azure AD integration with Reward Gateway, you need the following items:</span></span>

- <span data-ttu-id="ba862-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ba862-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ba862-113">已啟用 Reward Gateway 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ba862-113">A Reward Gateway single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ba862-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ba862-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ba862-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="ba862-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ba862-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ba862-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ba862-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="ba862-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ba862-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="ba862-118">Scenario description</span></span>
<span data-ttu-id="ba862-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ba862-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ba862-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="ba862-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ba862-121">從資源庫新增 Reward Gateway</span><span class="sxs-lookup"><span data-stu-id="ba862-121">Adding Reward Gateway from the gallery</span></span>
2. <span data-ttu-id="ba862-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ba862-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-reward-gateway-from-the-gallery"></a><span data-ttu-id="ba862-123">從資源庫新增 Reward Gateway</span><span class="sxs-lookup"><span data-stu-id="ba862-123">Adding Reward Gateway from the gallery</span></span>
<span data-ttu-id="ba862-124">若要設定將 Reward Gateway 整合到 Azure AD 中，您需要從資源庫將 Reward Gateway 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="ba862-124">To configure the integration of Reward Gateway into Azure AD, you need to add Reward Gateway from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ba862-125">**若要從資源庫新增 Reward Gateway，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ba862-125">**To add Reward Gateway from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ba862-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ba862-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ba862-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ba862-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ba862-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ba862-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="ba862-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ba862-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="ba862-133">在搜尋方塊中，輸入 **Reward Gateway**。</span><span class="sxs-lookup"><span data-stu-id="ba862-133">In the search box, type **Reward Gateway**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_search.png)

5. <span data-ttu-id="ba862-135">在結果窗格中，選取 [Reward Gateway]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="ba862-135">In the results panel, select **Reward Gateway**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ba862-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ba862-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ba862-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Reward Gateway 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ba862-138">In this section, you configure and test Azure AD single sign-on with Reward Gateway based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ba862-139">若要讓單一登入能夠運作，Azure AD 必須知道 Reward Gateway 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="ba862-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Reward Gateway is to a user in Azure AD.</span></span> <span data-ttu-id="ba862-140">換句話說，必須要建立某位 Azure AD 使用者與 Reward Gateway 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ba862-140">In other words, a link relationship between an Azure AD user and the related user in Reward Gateway needs to be established.</span></span>

<span data-ttu-id="ba862-141">在 Reward Gateway 中，將**使用者名稱**的值指派為 Azure AD 中**使用者名稱**的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ba862-141">In Reward Gateway, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ba862-142">若要設定及測試與 Reward Gateway 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="ba862-142">To configure and test Azure AD single sign-on with Reward Gateway, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ba862-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="ba862-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ba862-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ba862-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ba862-145">**[建立 Reward Gateway 測試使用者](#creating-a-reward-gateway-test-user)** - 使 Reward Gateway 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="ba862-145">**[Creating a Reward Gateway test user](#creating-a-reward-gateway-test-user)** - to have a counterpart of Britta Simon in Reward Gateway that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ba862-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ba862-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ba862-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="ba862-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ba862-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ba862-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ba862-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Reward Gateway 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="ba862-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Reward Gateway application.</span></span>

<span data-ttu-id="ba862-150">**若要設定 Azure AD 單一登入搭配 Reward Gateway 運作 ，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ba862-150">**To configure Azure AD single sign-on with Reward Gateway, perform the following steps:**</span></span>

1. <span data-ttu-id="ba862-151">在 Azure 入口網站的 [Reward Gateway] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="ba862-151">In the Azure portal, on the **Reward Gateway** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="ba862-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="ba862-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_samlbase.png)

3. <span data-ttu-id="ba862-155">在 [Reward Gateway 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ba862-155">On the **Reward Gateway Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_url.png)

    <span data-ttu-id="ba862-157">a.</span><span class="sxs-lookup"><span data-stu-id="ba862-157">a.</span></span> <span data-ttu-id="ba862-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="ba862-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.rewardgateway.com` |
    | `https://<companyname>.rewardgateway.co.uk/` |
    | `https://<companyname>.rewardgateway.co.nz/` |
    | `https://<companyname>.rewardgateway.com.au/` |

    <span data-ttu-id="ba862-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ba862-159">b.</span></span> <span data-ttu-id="ba862-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="ba862-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    |  `https://<companyname>.rewardgateway.com/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.co.uk/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.co.nz/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.com.au/Authentication/EndLogin?idp=<Unique Id>` |

    > [!NOTE] 
    > <span data-ttu-id="ba862-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="ba862-161">These values are not real.</span></span> <span data-ttu-id="ba862-162">請使用實際的識別碼和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="ba862-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="ba862-163">請連絡 [Reward Gateway 支援小組](mailto:clientsupport@rewardgateway.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="ba862-163">Contact [Reward Gateway support team](mailto:clientsupport@rewardgateway.com) to get these values.</span></span>
 
4. <span data-ttu-id="ba862-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="ba862-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_certificate.png) 

5. <span data-ttu-id="ba862-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ba862-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ba862-168">若要在 **Reward Gateway** 端設定單一登入，您必須將已下載的**中繼資料 XML** 傳送給 [Reward Gateway 支援小組](mailto:clientsupport@rewardgateway.com)。</span><span class="sxs-lookup"><span data-stu-id="ba862-168">To configure single sign-on on **Reward Gateway** side, you need to send the downloaded **Metadata XML** to [Reward Gateway support team](mailto:clientsupport@rewardgateway.com).</span></span> <span data-ttu-id="ba862-169">他們會進行此設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="ba862-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ba862-170">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="ba862-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ba862-171">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="ba862-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ba862-172">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ba862-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ba862-173">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ba862-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="ba862-174">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ba862-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="ba862-176">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ba862-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ba862-177">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ba862-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ba862-179">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="ba862-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ba862-181">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ba862-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ba862-183">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ba862-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ba862-185">a.</span><span class="sxs-lookup"><span data-stu-id="ba862-185">a.</span></span> <span data-ttu-id="ba862-186">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="ba862-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ba862-187">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ba862-187">b.</span></span> <span data-ttu-id="ba862-188">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="ba862-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ba862-189">c.</span><span class="sxs-lookup"><span data-stu-id="ba862-189">c.</span></span> <span data-ttu-id="ba862-190">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="ba862-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ba862-191">d.</span><span class="sxs-lookup"><span data-stu-id="ba862-191">d.</span></span> <span data-ttu-id="ba862-192">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ba862-192">Click **Create**.</span></span>
 
### <a name="creating-a-reward-gateway-test-user"></a><span data-ttu-id="ba862-193">建立 Reward Gateway 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ba862-193">Creating a Reward Gateway test user</span></span>

<span data-ttu-id="ba862-194">在本節中，您會在 Reward Gateway 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="ba862-194">In this section, you create a user called Britta Simon in Reward Gateway.</span></span> <span data-ttu-id="ba862-195">請與 Reward Gateway [支援小組](mailto:clientsupport@rewardgateway.com)合作以在 Reward Gateway 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="ba862-195">Work with Reward Gateway [support team](mailto:clientsupport@rewardgateway.com) to add the users in the Reward Gateway platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ba862-196">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ba862-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ba862-197">在本節中，您會授與 Britta Simon 對 Reward Gateway 的存取權，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ba862-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Reward Gateway.</span></span>

![指派使用者][200] 

<span data-ttu-id="ba862-199">**若要將 Britta Simon 指派到 Reward Gateway，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="ba862-199">**To assign Britta Simon to Reward Gateway, perform the following steps:**</span></span>

1. <span data-ttu-id="ba862-200">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ba862-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="ba862-202">在應用程式清單中，選取 [Reward Gateway]。</span><span class="sxs-lookup"><span data-stu-id="ba862-202">In the applications list, select **Reward Gateway**.</span></span>

    ![設定單一登入](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_app.png) 

3. <span data-ttu-id="ba862-204">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ba862-204">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="ba862-206">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ba862-206">Click **Add** button.</span></span> <span data-ttu-id="ba862-207">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ba862-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="ba862-209">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="ba862-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ba862-210">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ba862-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ba862-211">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ba862-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ba862-212">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="ba862-212">Testing single sign-on</span></span>

<span data-ttu-id="ba862-213">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="ba862-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ba862-214">當您在存取面板中按一下 [Reward Gateway] 磚時，應該會自動登入您的 Reward Gateway 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ba862-214">When you click the Reward Gateway tile in the Access Panel, you should get automatically signed-on to your Reward Gateway application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ba862-215">其他資源</span><span class="sxs-lookup"><span data-stu-id="ba862-215">Additional resources</span></span>

* [<span data-ttu-id="ba862-216">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="ba862-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ba862-217">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ba862-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_203.png


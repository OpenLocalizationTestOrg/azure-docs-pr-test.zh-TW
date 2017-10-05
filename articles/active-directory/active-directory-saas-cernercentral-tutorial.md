---
title: "教學課程：Azure Active Directory 與 Cerner Central 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Cerner Central 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 77b5fb94cdfa5722081198aabc59fbf86229c2b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a><span data-ttu-id="000dc-103">教學課程：Azure Active Directory 與 Cerner Central 整合</span><span class="sxs-lookup"><span data-stu-id="000dc-103">Tutorial: Azure Active Directory integration with Cerner Central</span></span>

<span data-ttu-id="000dc-104">在本教學課程中，您會了解如何整合 Cerner Central 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="000dc-104">In this tutorial, you learn how to integrate Cerner Central with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="000dc-105">將 Cerner Central 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="000dc-105">Integrating Cerner Central with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="000dc-106">您可以在 Azure AD 中控制可存取 Cerner Central 的人員</span><span class="sxs-lookup"><span data-stu-id="000dc-106">You can control in Azure AD who has access to Cerner Central</span></span>
- <span data-ttu-id="000dc-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Cerner Central (單一登入)</span><span class="sxs-lookup"><span data-stu-id="000dc-107">You can enable your users to automatically get signed-on to Cerner Central (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="000dc-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="000dc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="000dc-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="000dc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="000dc-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="000dc-110">Prerequisites</span></span>

<span data-ttu-id="000dc-111">若要設定 Azure AD 與 Cerner Central 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="000dc-111">To configure Azure AD integration with Cerner Central, you need the following items:</span></span>

- <span data-ttu-id="000dc-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="000dc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="000dc-113">已核准的 Cerner Central 系統帳戶</span><span class="sxs-lookup"><span data-stu-id="000dc-113">An approved Cerner Central System Account</span></span>

> [!NOTE]
> <span data-ttu-id="000dc-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="000dc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="000dc-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="000dc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="000dc-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="000dc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="000dc-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="000dc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="000dc-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="000dc-118">Scenario description</span></span>
<span data-ttu-id="000dc-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="000dc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="000dc-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="000dc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="000dc-121">從資源庫新增 Cerner Central</span><span class="sxs-lookup"><span data-stu-id="000dc-121">Adding Cerner Central from the gallery</span></span>
2. <span data-ttu-id="000dc-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="000dc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cerner-central-from-the-gallery"></a><span data-ttu-id="000dc-123">從資源庫新增 Cerner Central</span><span class="sxs-lookup"><span data-stu-id="000dc-123">Adding Cerner Central from the gallery</span></span>
<span data-ttu-id="000dc-124">若要設定將 Cerner Central 整合到 Azure AD 中，您需要從資源庫將 Cerner Central 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="000dc-124">To configure the integration of Cerner Central into Azure AD, you need to add Cerner Central from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="000dc-125">**若要從資源庫新增 Cerner Central，執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="000dc-125">**To add Cerner Central from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="000dc-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="000dc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="000dc-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="000dc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="000dc-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="000dc-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="000dc-131">若要新增新的應用程式，按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="000dc-131">To add new application, click **New application** button on top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="000dc-133">在搜尋方塊中輸入 **Cerner Central**。</span><span class="sxs-lookup"><span data-stu-id="000dc-133">In the search box, type **Cerner Central**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. <span data-ttu-id="000dc-135">在結果面板中，選取 [Cerner Central]，然後按一下 [新增] 按鈕以新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="000dc-135">In the results panel, select **Cerner Central**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="000dc-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="000dc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="000dc-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Cerner Central 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="000dc-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="000dc-139">若要讓單一登入能夠運作，Azure AD 必須知道 Cerner Central 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="000dc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cerner Central is to a user in Azure AD.</span></span> <span data-ttu-id="000dc-140">換句話說，必須在 Azure AD 使用者與 Cerner Central 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="000dc-140">In other words, a link relationship between an Azure AD user and the related user in Cerner Central needs to be established.</span></span>

<span data-ttu-id="000dc-141">若要設定及測試 Azure AD 與 Cerner Central 的單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="000dc-141">To configure and test Azure AD single sign-on with Cerner Central, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="000dc-142">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="000dc-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="000dc-143">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="000dc-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="000dc-144">**[建立 Cerner Central 測試使用者](#creating-a-cerner-central-test-user)** - 在 Cerner Central 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="000dc-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - to have a counterpart of Britta Simon in Cerner Central that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="000dc-145">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="000dc-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="000dc-146">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="000dc-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="000dc-147">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="000dc-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="000dc-148">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Cerner Central 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="000dc-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cerner Central application.</span></span>

<span data-ttu-id="000dc-149">**若要設定與 Cerner Central 搭配運作的 Azure AD 單一登入，執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="000dc-149">**To configure Azure AD single sign-on with Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="000dc-150">在 Azure 入口網站的 [Cerner Central] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="000dc-150">In the Azure portal, on the **Cerner Central** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="000dc-152">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="000dc-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. <span data-ttu-id="000dc-154">在 [Cerner Central 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="000dc-154">On the **Cerner Central Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    <span data-ttu-id="000dc-156">a.</span><span class="sxs-lookup"><span data-stu-id="000dc-156">a.</span></span> <span data-ttu-id="000dc-157">在 [識別碼] 文字方塊中，使用下列模式來輸入值：</span><span class="sxs-lookup"><span data-stu-id="000dc-157">In the **Identifier** textbox, type the value using the following patterns:</span></span>
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    <span data-ttu-id="000dc-158">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="000dc-158">b.</span></span> <span data-ttu-id="000dc-159">在 [回覆 URL] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="000dc-159">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="000dc-160">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="000dc-160">These values are not the real.</span></span> <span data-ttu-id="000dc-161">請使用實際的識別碼和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="000dc-161">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="000dc-162">請連絡 [Cerner Central 支援小組](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="000dc-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) to get these values.</span></span>
 
4. <span data-ttu-id="000dc-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="000dc-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="000dc-165">若要產生**中繼資料** URL，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="000dc-165">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="000dc-166">a.</span><span class="sxs-lookup"><span data-stu-id="000dc-166">a.</span></span> <span data-ttu-id="000dc-167">按一下 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="000dc-167">Click **App registrations**.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    <span data-ttu-id="000dc-169">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="000dc-169">b.</span></span> <span data-ttu-id="000dc-170">按一下 [端點] 以開啟 [端點] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="000dc-170">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![設定單一登入](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    <span data-ttu-id="000dc-172">c.</span><span class="sxs-lookup"><span data-stu-id="000dc-172">c.</span></span> <span data-ttu-id="000dc-173">按一下複製按鈕複製 [同盟中繼資料文件] URL，並將它貼到 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="000dc-173">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    <span data-ttu-id="000dc-175">d.</span><span class="sxs-lookup"><span data-stu-id="000dc-175">d.</span></span> <span data-ttu-id="000dc-176">現在，移至 [Cerner Central] 的屬性頁面，使用 [複製] 按鈕複製 [應用程式識別碼]，並將它貼到 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="000dc-176">Now go to the property page of **Cerner Central** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    <span data-ttu-id="000dc-178">e.</span><span class="sxs-lookup"><span data-stu-id="000dc-178">e.</span></span> <span data-ttu-id="000dc-179">使用下列模式產生**中繼資料 URL**︰`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="000dc-179">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

6. <span data-ttu-id="000dc-180">為了要在 **Cerner Central** 端設定單一登入，您必須將已下載的**中繼資料 XML** 傳送給 [Cerner Central 支援小組](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations)。</span><span class="sxs-lookup"><span data-stu-id="000dc-180">To configure single sign-on on **Cerner Central** side, you need to send the **Metadata URL** to [Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span></span> <span data-ttu-id="000dc-181">由他們設定應用程式端的單一登入以完成整合。</span><span class="sxs-lookup"><span data-stu-id="000dc-181">They configure the SSO on application side to complete the integration.</span></span>

> [!TIP]
> <span data-ttu-id="000dc-182">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="000dc-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="000dc-183">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="000dc-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="000dc-184">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="000dc-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="000dc-185">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="000dc-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="000dc-186">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="000dc-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span> 

![建立 Azure AD 使用者][100]

<span data-ttu-id="000dc-188">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="000dc-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="000dc-189">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="000dc-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="000dc-191">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="000dc-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="000dc-193">按一下 [新增] 開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="000dc-193">To open the **User** dialog, click **Add**.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="000dc-195">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="000dc-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="000dc-197">a.</span><span class="sxs-lookup"><span data-stu-id="000dc-197">a.</span></span> <span data-ttu-id="000dc-198">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="000dc-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="000dc-199">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="000dc-199">b.</span></span> <span data-ttu-id="000dc-200">在 [使用者名稱] 文字方塊中，輸入 Britta Simon 的「電子郵件地址」。</span><span class="sxs-lookup"><span data-stu-id="000dc-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="000dc-201">c.</span><span class="sxs-lookup"><span data-stu-id="000dc-201">c.</span></span> <span data-ttu-id="000dc-202">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="000dc-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="000dc-203">d.</span><span class="sxs-lookup"><span data-stu-id="000dc-203">d.</span></span> <span data-ttu-id="000dc-204">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="000dc-204">Click **Create**.</span></span>
 
### <a name="creating-a-cerner-central-test-user"></a><span data-ttu-id="000dc-205">建立 Cerner Central 測試使用者</span><span class="sxs-lookup"><span data-stu-id="000dc-205">Creating a Cerner Central test user</span></span>

<span data-ttu-id="000dc-206">**Cerner Central** 應用程式可允許從任何同盟身分識別提供者進行驗證。</span><span class="sxs-lookup"><span data-stu-id="000dc-206">**Cerner Central** application allows authentication from any federated identity provider.</span></span> <span data-ttu-id="000dc-207">如果使用者能夠登入應用程式首頁，即表示他們已同盟，而不需進行任何手動佈建。</span><span class="sxs-lookup"><span data-stu-id="000dc-207">If a user is able to log in to the application home page, they are federated and have no need for any manual provisioning.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="000dc-208">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="000dc-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="000dc-209">在本節中，您會將 Cerner Central 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="000dc-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cerner Central.</span></span>

![指派使用者][200] 

<span data-ttu-id="000dc-211">**若要將 Britta Simon 指派給 Cerner Central ，執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="000dc-211">**To assign Britta Simon to Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="000dc-212">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="000dc-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="000dc-214">在應用程式清單中，選取 [Cerner Central]。</span><span class="sxs-lookup"><span data-stu-id="000dc-214">In the applications list, select **Cerner Central**.</span></span>

    ![設定單一登入](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. <span data-ttu-id="000dc-216">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="000dc-216">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="000dc-218">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="000dc-218">Click **Add** button.</span></span> <span data-ttu-id="000dc-219">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="000dc-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="000dc-221">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="000dc-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="000dc-222">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="000dc-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="000dc-223">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="000dc-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="000dc-224">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="000dc-224">Testing single sign-on</span></span>

<span data-ttu-id="000dc-225">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="000dc-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="000dc-226">當您在「存取面板」中按一下 [Cerner Central] 圖格時，應該會自動登入您的 Cerner Central 應用程式。</span><span class="sxs-lookup"><span data-stu-id="000dc-226">When you click the Cerner Central tile in the Access Panel, you should get automatically signed-on to your Cerner Central application.</span></span> <span data-ttu-id="000dc-227">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="000dc-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="000dc-228">其他資源</span><span class="sxs-lookup"><span data-stu-id="000dc-228">Additional resources</span></span>

* [<span data-ttu-id="000dc-229">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="000dc-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="000dc-230">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="000dc-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png


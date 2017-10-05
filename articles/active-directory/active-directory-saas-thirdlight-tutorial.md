---
title: "教學課程：Azure Active Directory 與 ThirdLight 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 ThirdLight 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 168aae9a-54ee-4c2b-ab12-650a2c62b901
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: ee7710cfea3a13907c0cc940a98c875bf83607a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thirdlight"></a><span data-ttu-id="78ec8-103">教學課程：Azure Active Directory 與 ThirdLight 整合</span><span class="sxs-lookup"><span data-stu-id="78ec8-103">Tutorial: Azure Active Directory integration with ThirdLight</span></span>

<span data-ttu-id="78ec8-104">在本教學課程中，您將了解如何整合 ThirdLight 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="78ec8-104">In this tutorial, you learn how to integrate ThirdLight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="78ec8-105">ThirdLight 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="78ec8-105">Integrating ThirdLight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="78ec8-106">您可以在 Azure AD 中控制可存取 ThirdLight 的人員</span><span class="sxs-lookup"><span data-stu-id="78ec8-106">You can control in Azure AD who has access to ThirdLight</span></span>
- <span data-ttu-id="78ec8-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 ThirdLight (單一登入)</span><span class="sxs-lookup"><span data-stu-id="78ec8-107">You can enable your users to automatically get signed-on to ThirdLight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="78ec8-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="78ec8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="78ec8-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="78ec8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78ec8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="78ec8-110">Prerequisites</span></span>

<span data-ttu-id="78ec8-111">若要設定 Azure AD 與 ThirdLight 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="78ec8-111">To configure Azure AD integration with ThirdLight, you need the following items:</span></span>

- <span data-ttu-id="78ec8-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="78ec8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="78ec8-113">已啟用 ThirdLight 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="78ec8-113">A ThirdLight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="78ec8-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="78ec8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="78ec8-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="78ec8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="78ec8-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="78ec8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="78ec8-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="78ec8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="78ec8-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="78ec8-118">Scenario description</span></span>
<span data-ttu-id="78ec8-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="78ec8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="78ec8-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="78ec8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="78ec8-121">從資源庫新增 ThirdLight</span><span class="sxs-lookup"><span data-stu-id="78ec8-121">Adding ThirdLight from the gallery</span></span>
2. <span data-ttu-id="78ec8-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="78ec8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thirdlight-from-the-gallery"></a><span data-ttu-id="78ec8-123">從資源庫新增 ThirdLight</span><span class="sxs-lookup"><span data-stu-id="78ec8-123">Adding ThirdLight from the gallery</span></span>
<span data-ttu-id="78ec8-124">若要設定 ThirdLight 與 Azure AD 整合，您需要從資源庫將 ThirdLight 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="78ec8-124">To configure the integration of ThirdLight into Azure AD, you need to add ThirdLight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="78ec8-125">**若要從資源庫新增 ThirdLight，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="78ec8-125">**To add ThirdLight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="78ec8-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="78ec8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="78ec8-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="78ec8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="78ec8-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="78ec8-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="78ec8-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="78ec8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="78ec8-133">在搜尋方塊中，輸入 **ThirdLight**。</span><span class="sxs-lookup"><span data-stu-id="78ec8-133">In the search box, type **ThirdLight**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_search.png)

5. <span data-ttu-id="78ec8-135">在結果窗格中，選取 [ThirdLight]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="78ec8-135">In the results panel, select **ThirdLight**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="78ec8-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="78ec8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="78ec8-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 ThirdLight 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="78ec8-138">In this section, you configure and test Azure AD single sign-on with ThirdLight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="78ec8-139">若要讓單一登入運作，Azure AD 必須知道 ThirdLight 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="78ec8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ThirdLight is to a user in Azure AD.</span></span> <span data-ttu-id="78ec8-140">換句話說，必須在 Azure AD 使用者和 ThirdLight 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="78ec8-140">In other words, a link relationship between an Azure AD user and the related user in ThirdLight needs to be established.</span></span>

<span data-ttu-id="78ec8-141">建立此連結關聯性的方法，就是將 Azure AD 中 [使用者名稱] 的值指派為 ThirdLight 中 [使用者名稱] 的值。</span><span class="sxs-lookup"><span data-stu-id="78ec8-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ThirdLight.</span></span>

<span data-ttu-id="78ec8-142">若要設定及測試與 ThirdLight 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="78ec8-142">To configure and test Azure AD single sign-on with ThirdLight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="78ec8-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="78ec8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="78ec8-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="78ec8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="78ec8-145">**[建立 ThirdLight 測試使用者](#creating-a-thirdlight-test-user)** - 使 ThirdLight 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="78ec8-145">**[Creating a ThirdLight test user](#creating-a-thirdlight-test-user)** - to have a counterpart of Britta Simon in ThirdLight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="78ec8-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="78ec8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="78ec8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="78ec8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="78ec8-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="78ec8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="78ec8-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 ThirdLight 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="78ec8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ThirdLight application.</span></span>

<span data-ttu-id="78ec8-150">**若要設定與 ThirdLight 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="78ec8-150">**To configure Azure AD single sign-on with ThirdLight, perform the following steps:**</span></span>

1. <span data-ttu-id="78ec8-151">在 Azure 入口網站的 [ThirdLight] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="78ec8-151">In the Azure portal, on the **ThirdLight** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="78ec8-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="78ec8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_samlbase.png)

3. <span data-ttu-id="78ec8-155">在 [ThirdLight 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="78ec8-155">On the **ThirdLight Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_url.png)

    <span data-ttu-id="78ec8-157">a.</span><span class="sxs-lookup"><span data-stu-id="78ec8-157">a.</span></span> <span data-ttu-id="78ec8-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<subdomain>.thirdlight.com/`</span><span class="sxs-lookup"><span data-stu-id="78ec8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/`</span></span>

    <span data-ttu-id="78ec8-159">b.</span><span class="sxs-lookup"><span data-stu-id="78ec8-159">b.</span></span> <span data-ttu-id="78ec8-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<subdomain>.thirdlight.com/saml/sp`</span><span class="sxs-lookup"><span data-stu-id="78ec8-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/saml/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="78ec8-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="78ec8-161">These values are not real.</span></span> <span data-ttu-id="78ec8-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="78ec8-162">Update these values with the actual Sign-On URL and Identiifer.</span></span> <span data-ttu-id="78ec8-163">請連絡 [ThirdLight 客戶支援小組](https://www.thirdlight.com/support)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="78ec8-163">Contact [ThirdLight Client support team](https://www.thirdlight.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="78ec8-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="78ec8-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_certificate.png) 

5. <span data-ttu-id="78ec8-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="78ec8-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-thirdlight-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="78ec8-168">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 ThirdLight 公司網站。</span><span class="sxs-lookup"><span data-stu-id="78ec8-168">In a different web browser window, log in to your ThirdLight company site as an administrator.</span></span>

7. <span data-ttu-id="78ec8-169">移至 [組態] \> [系統管理]，然後按一下 [SAML2]。</span><span class="sxs-lookup"><span data-stu-id="78ec8-169">Go to **Configuration \> System Administration**, and then click **SAML2**.</span></span>
   
    <span data-ttu-id="78ec8-170">![系統管理](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "系統管理")</span><span class="sxs-lookup"><span data-stu-id="78ec8-170">![System Administration](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "System Administration")</span></span>

8. <span data-ttu-id="78ec8-171">在 [SAML2 組態] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="78ec8-171">In the SAML2 configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="78ec8-172">![SAML 單一登入](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML 單一登入")</span><span class="sxs-lookup"><span data-stu-id="78ec8-172">![SAML Single Sign-On](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML Single Sign-On")</span></span>   

     <span data-ttu-id="78ec8-173">a.</span><span class="sxs-lookup"><span data-stu-id="78ec8-173">a.</span></span> <span data-ttu-id="78ec8-174">選取 [啟用 SAML2 單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="78ec8-174">Select **Enable SAML2 Single Sign-On**.</span></span>
 
     <span data-ttu-id="78ec8-175">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="78ec8-175">b.</span></span> <span data-ttu-id="78ec8-176">在 [IdP 中繼資料的來源] 選取 [從 XML 載入 IdP 中繼資料]。</span><span class="sxs-lookup"><span data-stu-id="78ec8-176">As **Source for IdP Metadata**, select **Load IdP Metadata from XML**.</span></span>
 
     <span data-ttu-id="78ec8-177">c.</span><span class="sxs-lookup"><span data-stu-id="78ec8-177">c.</span></span> <span data-ttu-id="78ec8-178">開啟下載的中繼資料檔案，然後複製內容並貼到 [IdP 中繼資料 XML]  文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="78ec8-178">Open the downloaded metadata file, copy the content, and then paste it into the **IdP Metadata XML** textbox.</span></span> 
     
     <span data-ttu-id="78ec8-179">d.</span><span class="sxs-lookup"><span data-stu-id="78ec8-179">d.</span></span> <span data-ttu-id="78ec8-180">按一下 [儲存 SAML2 設定] 。</span><span class="sxs-lookup"><span data-stu-id="78ec8-180">Click **Save SAML2 settings**.</span></span>

> [!TIP]
> <span data-ttu-id="78ec8-181">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="78ec8-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="78ec8-182">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="78ec8-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="78ec8-183">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="78ec8-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="78ec8-184">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="78ec8-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="78ec8-185">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="78ec8-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="78ec8-187">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="78ec8-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="78ec8-188">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="78ec8-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="78ec8-190">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="78ec8-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="78ec8-192">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="78ec8-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="78ec8-194">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="78ec8-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="78ec8-196">a.</span><span class="sxs-lookup"><span data-stu-id="78ec8-196">a.</span></span> <span data-ttu-id="78ec8-197">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="78ec8-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="78ec8-198">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="78ec8-198">b.</span></span> <span data-ttu-id="78ec8-199">在 [使用者名稱] 文字方塊中，輸入 Britta Simon 的「電子郵件地址」。</span><span class="sxs-lookup"><span data-stu-id="78ec8-199">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="78ec8-200">c.</span><span class="sxs-lookup"><span data-stu-id="78ec8-200">c.</span></span> <span data-ttu-id="78ec8-201">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="78ec8-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="78ec8-202">d.</span><span class="sxs-lookup"><span data-stu-id="78ec8-202">d.</span></span> <span data-ttu-id="78ec8-203">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="78ec8-203">Click **Create**.</span></span>
 
### <a name="creating-a-thirdlight-test-user"></a><span data-ttu-id="78ec8-204">建立 ThirdLight 測試使用者</span><span class="sxs-lookup"><span data-stu-id="78ec8-204">Creating a ThirdLight test user</span></span>

<span data-ttu-id="78ec8-205">若要讓 Azure AD 使用者可以登入 ThirdLight，則必須將他們佈建到 ThirdLight。</span><span class="sxs-lookup"><span data-stu-id="78ec8-205">To enable Azure AD users to log in to ThirdLight, they must be provisioned into ThirdLight.</span></span>  
<span data-ttu-id="78ec8-206">ThirdLight 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="78ec8-206">In the case of ThirdLight, provisioning is a manual task.</span></span>

<span data-ttu-id="78ec8-207">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="78ec8-207">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="78ec8-208">以系統管理員身分登入您的 **ThirdLight** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="78ec8-208">Log in to your **ThirdLight** company site as an administrator.</span></span>

2. <span data-ttu-id="78ec8-209">移至 [使用者]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="78ec8-209">Go to **Users** tab.</span></span>

3. <span data-ttu-id="78ec8-210">選取 [使用者和群組] 。</span><span class="sxs-lookup"><span data-stu-id="78ec8-210">Select **Users and Groups**.</span></span>

4. <span data-ttu-id="78ec8-211">按一下 [新增使用者]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="78ec8-211">Click **Add new User** button.</span></span>

5. <span data-ttu-id="78ec8-212">輸入使用者名稱、名稱或描述、電子郵件，選擇您想要佈建之有效 AAD 帳戶新成員的 [預設] 或 [群組]  。</span><span class="sxs-lookup"><span data-stu-id="78ec8-212">Enter **the Username, Name or Description, Email, Choose a Preset or Group of New Members** of a valid AAD account you want to provision.</span></span>

6. <span data-ttu-id="78ec8-213">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="78ec8-213">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="78ec8-214">您可以使用任何其他的 Thirdlight 使用者帳戶建立工具或 Thirdlight 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="78ec8-214">You can use any other Thirdlight user account creation tools or APIs provided by Thirdlight to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="78ec8-215">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="78ec8-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="78ec8-216">在本節中，您會將 ThirdLight 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="78ec8-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ThirdLight.</span></span>

![指派使用者][200] 

<span data-ttu-id="78ec8-218">**若要將 Britta Simon 指派給 ThirdLight，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="78ec8-218">**To assign Britta Simon to ThirdLight, perform the following steps:**</span></span>

1. <span data-ttu-id="78ec8-219">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="78ec8-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="78ec8-221">在應用程式清單中，選取 [ThirdLight]。</span><span class="sxs-lookup"><span data-stu-id="78ec8-221">In the applications list, select **ThirdLight**.</span></span>

    ![設定單一登入](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_app.png) 

3. <span data-ttu-id="78ec8-223">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="78ec8-223">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="78ec8-225">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="78ec8-225">Click **Add** button.</span></span> <span data-ttu-id="78ec8-226">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="78ec8-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="78ec8-228">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="78ec8-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="78ec8-229">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="78ec8-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="78ec8-230">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="78ec8-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="78ec8-231">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="78ec8-231">Testing single sign-on</span></span>

<span data-ttu-id="78ec8-232">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="78ec8-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="78ec8-233">當您在存取面板中按一下 [ThirdLight] 圖格時，應該會自動登入您的 ThirdLight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="78ec8-233">When you click the ThirdLight tile in the Access Panel, you should get automatically signed-on to your ThirdLight application.</span></span>
<span data-ttu-id="78ec8-234">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="78ec8-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="78ec8-235">其他資源</span><span class="sxs-lookup"><span data-stu-id="78ec8-235">Additional resources</span></span>

* [<span data-ttu-id="78ec8-236">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="78ec8-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="78ec8-237">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="78ec8-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_203.png


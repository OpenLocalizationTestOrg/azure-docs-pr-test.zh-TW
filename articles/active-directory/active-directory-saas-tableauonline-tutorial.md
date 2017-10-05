---
title: "教學課程：Azure Active Directory 與 Tableau Online 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Tableau Online 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 443fab1198a91a4d5749e6421f7b8603fc75a81e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="ea691-103">教學課程：Azure Active Directory 與 Tableau Online 整合</span><span class="sxs-lookup"><span data-stu-id="ea691-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>

<span data-ttu-id="ea691-104">在本教學課程中，您將了解如何整合 Tableau Online 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="ea691-104">In this tutorial, you learn how to integrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ea691-105">Tableau Online 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="ea691-105">Integrating Tableau Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ea691-106">您可以在 Azure AD 中控制可存取 Tableau Online 的人員</span><span class="sxs-lookup"><span data-stu-id="ea691-106">You can control in Azure AD who has access to Tableau Online</span></span>
- <span data-ttu-id="ea691-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Tableau Online (單一登入)</span><span class="sxs-lookup"><span data-stu-id="ea691-107">You can enable your users to automatically get signed-on to Tableau Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ea691-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="ea691-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ea691-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ea691-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea691-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ea691-110">Prerequisites</span></span>

<span data-ttu-id="ea691-111">若要設定 Azure AD 與 Tableau Online 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="ea691-111">To configure Azure AD integration with Tableau Online, you need the following items:</span></span>

- <span data-ttu-id="ea691-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ea691-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ea691-113">已啟用 Tableau Online 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ea691-113">A Tableau Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ea691-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ea691-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ea691-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="ea691-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ea691-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ea691-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ea691-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="ea691-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ea691-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="ea691-118">Scenario description</span></span>
<span data-ttu-id="ea691-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ea691-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ea691-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="ea691-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ea691-121">從資源庫新增 Tableau Online</span><span class="sxs-lookup"><span data-stu-id="ea691-121">Adding Tableau Online from the gallery</span></span>
2. <span data-ttu-id="ea691-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ea691-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-online-from-the-gallery"></a><span data-ttu-id="ea691-123">從資源庫新增 Tableau Online</span><span class="sxs-lookup"><span data-stu-id="ea691-123">Adding Tableau Online from the gallery</span></span>
<span data-ttu-id="ea691-124">若要設定 Tableau Online 與 Azure AD 整合，您需要從資源庫將 Tableau Online 加入到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="ea691-124">To configure the integration of Tableau Online into Azure AD, you need to add Tableau Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ea691-125">**如要從資源庫新增 Tableau Online，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ea691-125">**To add Tableau Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ea691-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ea691-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ea691-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ea691-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ea691-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ea691-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="ea691-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ea691-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="ea691-133">在搜尋方塊中，輸入 **Tableau Online**。</span><span class="sxs-lookup"><span data-stu-id="ea691-133">In the search box, type **Tableau Online**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. <span data-ttu-id="ea691-135">在結果窗格中，選取 [Tableau Online]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea691-135">In the results panel, select **Tableau Online**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ea691-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ea691-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ea691-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Tableau Online 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ea691-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ea691-139">若要讓單一登入能夠運作，Azure AD 必須知道 Tableau Online 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="ea691-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Online is to a user in Azure AD.</span></span> <span data-ttu-id="ea691-140">換句話說，必須在 Azure AD 使用者和 Tableau Online 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ea691-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Online needs to be established.</span></span>

<span data-ttu-id="ea691-141">在 Tableau Online 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ea691-141">In Tableau Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ea691-142">若要使用 Tableau Online 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="ea691-142">To configure and test Azure AD single sign-on with Tableau Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ea691-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="ea691-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ea691-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ea691-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ea691-145">**[建立 Tableau Online 測試使用者](#creating-a-tableau-online-test-user)** - 使 Tableau Online 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="ea691-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - to have a counterpart of Britta Simon in Tableau Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ea691-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ea691-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ea691-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="ea691-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ea691-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ea691-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ea691-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Tableau Online 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="ea691-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Online application.</span></span>

<span data-ttu-id="ea691-150">**若要設定透過 Tableau Online 使用 Azure AD 單一登入功能，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ea691-150">**To configure Azure AD single sign-on with Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="ea691-151">在 Azure 入口網站的 [Tableau Online] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="ea691-151">In the Azure portal, on the **Tableau Online** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="ea691-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="ea691-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. <span data-ttu-id="ea691-155">在 [Tableau Online 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ea691-155">On the **Tableau Online Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    <span data-ttu-id="ea691-157">a.</span><span class="sxs-lookup"><span data-stu-id="ea691-157">a.</span></span> <span data-ttu-id="ea691-158">在 [登入 URL] 文字方塊中，輸入 URL：`https://sso.online.tableau.com`</span><span class="sxs-lookup"><span data-stu-id="ea691-158">In the **Sign-on URL** textbox, type the URL: `https://sso.online.tableau.com`</span></span>

    <span data-ttu-id="ea691-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea691-159">b.</span></span> <span data-ttu-id="ea691-160">在 [識別碼] 文字方塊中，輸入 URL：`https://sso.online.tableau.com/public/sp/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="ea691-160">In the **Identifier** textbox, type the URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span></span>

4. <span data-ttu-id="ea691-161">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="ea691-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. <span data-ttu-id="ea691-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ea691-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ea691-165">在不同的瀏覽器視窗中，登入您的 Tableau Online 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea691-165">In a different browser window, sign-on to your Tableau Online application.</span></span> <span data-ttu-id="ea691-166">依序前往 [設定] 和 [驗證]。</span><span class="sxs-lookup"><span data-stu-id="ea691-166">Go to **Settings** and then **Authentication**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. <span data-ttu-id="ea691-168">若要在 [驗證類型] 區段下啟用 SAML，請</span><span class="sxs-lookup"><span data-stu-id="ea691-168">To enable SAML, Under **Authentication Types** section.</span></span> <span data-ttu-id="ea691-169">勾選 [使用 SAML 的單一登入] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="ea691-169">Check the **Single sign-on with SAML** checkbox.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. <span data-ttu-id="ea691-171">向下捲動到 [將中繼資料檔匯入到 Tableau Online]  區段。</span><span class="sxs-lookup"><span data-stu-id="ea691-171">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="ea691-172">按一下 [瀏覽]，然後匯入您從 Azure AD 下載的中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="ea691-172">Click Browse and import the metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="ea691-173">然後，按一下 [套用] 。</span><span class="sxs-lookup"><span data-stu-id="ea691-173">Then, click **Apply**.</span></span>
   
   ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. <span data-ttu-id="ea691-175">在 [比對判斷提示] 區段中，針對 [電子郵件地址]、[名字] 和 [姓氏] 插入對應的識別提供者判斷提示名稱。</span><span class="sxs-lookup"><span data-stu-id="ea691-175">In the **Match assertions** section, insert the corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span></span> <span data-ttu-id="ea691-176">若要從 Azure AD 取得這項資訊︰</span><span class="sxs-lookup"><span data-stu-id="ea691-176">To get this information from Azure AD:</span></span> 
  
    <span data-ttu-id="ea691-177">a.</span><span class="sxs-lookup"><span data-stu-id="ea691-177">a.</span></span> <span data-ttu-id="ea691-178">在 Azure 入口網站中，移至 [Tableau Online] 應用程式整合頁面。</span><span class="sxs-lookup"><span data-stu-id="ea691-178">In the Azure portal, go on the **Tableau Online** application integration page.</span></span>
    
    <span data-ttu-id="ea691-179">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea691-179">b.</span></span> <span data-ttu-id="ea691-180">在屬性區段中，選取 [檢視及編輯所有其他使用者屬性] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="ea691-180">In the attributes section, Select the **"view and edit all other user attributes"** checkbox.</span></span> 
    
   ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    <span data-ttu-id="ea691-182">c.</span><span class="sxs-lookup"><span data-stu-id="ea691-182">c.</span></span> <span data-ttu-id="ea691-183">使用下列步驟複製 givenname、email 和 surname 屬性的命名空間值：</span><span class="sxs-lookup"><span data-stu-id="ea691-183">Copy the namespace value for these attributes: givenname, email and surname by using the following steps:</span></span>

   ![Azure AD 單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    <span data-ttu-id="ea691-185">d.</span><span class="sxs-lookup"><span data-stu-id="ea691-185">d.</span></span> <span data-ttu-id="ea691-186">按一下 [user.givenname] 值</span><span class="sxs-lookup"><span data-stu-id="ea691-186">Click **user.givenname** value</span></span> 
    
    <span data-ttu-id="ea691-187">e.</span><span class="sxs-lookup"><span data-stu-id="ea691-187">e.</span></span> <span data-ttu-id="ea691-188">從 [命名空間] 文字方塊複製該值。</span><span class="sxs-lookup"><span data-stu-id="ea691-188">Copy the value from the **namespace** textbox.</span></span>

   ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    <span data-ttu-id="ea691-190">f.</span><span class="sxs-lookup"><span data-stu-id="ea691-190">f.</span></span> <span data-ttu-id="ea691-191">若要複製 email 和 surname 的命名空間值，請遵循上述步驟。</span><span class="sxs-lookup"><span data-stu-id="ea691-191">To copy the namesapce values for the email and surname follow the preceding steps.</span></span>

    <span data-ttu-id="ea691-192">g.</span><span class="sxs-lookup"><span data-stu-id="ea691-192">g.</span></span> <span data-ttu-id="ea691-193">切換至 Tableau Online 應用程式，然後將 [Tableau Online 屬性] 區段設定如下：</span><span class="sxs-lookup"><span data-stu-id="ea691-193">Switch to the Tableau Online application, then set the **Tableau Online Attributes** section as follows:</span></span>
     * <span data-ttu-id="ea691-194">電子郵件︰**mail** 或 **userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="ea691-194">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="ea691-195">名字︰ **givenname**</span><span class="sxs-lookup"><span data-stu-id="ea691-195">First name: **givenname**</span></span>
     * <span data-ttu-id="ea691-196">姓氏︰ **surname**</span><span class="sxs-lookup"><span data-stu-id="ea691-196">Last name: **surname**</span></span>
   
   ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> <span data-ttu-id="ea691-198">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="ea691-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ea691-199">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="ea691-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ea691-200">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ea691-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ea691-201">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ea691-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="ea691-202">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ea691-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="ea691-204">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ea691-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ea691-205">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ea691-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ea691-207">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="ea691-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ea691-209">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ea691-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ea691-211">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ea691-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ea691-213">a.</span><span class="sxs-lookup"><span data-stu-id="ea691-213">a.</span></span> <span data-ttu-id="ea691-214">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="ea691-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ea691-215">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea691-215">b.</span></span> <span data-ttu-id="ea691-216">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="ea691-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ea691-217">c.</span><span class="sxs-lookup"><span data-stu-id="ea691-217">c.</span></span> <span data-ttu-id="ea691-218">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="ea691-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ea691-219">d.</span><span class="sxs-lookup"><span data-stu-id="ea691-219">d.</span></span> <span data-ttu-id="ea691-220">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ea691-220">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-online-test-user"></a><span data-ttu-id="ea691-221">建立 Tableau Online 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ea691-221">Creating a Tableau Online test user</span></span>

<span data-ttu-id="ea691-222">在本節中，您要在 Tableau Online 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="ea691-222">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="ea691-223">在 [Tableau Online] 中，依序按一下 [設定] 和 [驗證] 區段。</span><span class="sxs-lookup"><span data-stu-id="ea691-223">On **Tableau Online**, click **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="ea691-224">向下捲動至 [選取使用者]  區段。</span><span class="sxs-lookup"><span data-stu-id="ea691-224">Scroll down to **Select Users** section.</span></span> <span data-ttu-id="ea691-225">依序按一下 [新增使用者] 和 [輸入電子郵件地址]。</span><span class="sxs-lookup"><span data-stu-id="ea691-225">Click **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. <span data-ttu-id="ea691-227">選取 [新增單一登入 (SSO) 驗證的使用者] 。</span><span class="sxs-lookup"><span data-stu-id="ea691-227">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="ea691-228">在 [輸入電子郵件地址] 文字方塊中，新增 britta.simon@contoso.com</span><span class="sxs-lookup"><span data-stu-id="ea691-228">In the **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. <span data-ttu-id="ea691-230">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ea691-230">Click **Create**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ea691-231">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ea691-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ea691-232">在本節中，您會將 Tableau Online 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ea691-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Online.</span></span>

![指派使用者][200] 

<span data-ttu-id="ea691-234">**如要將 Britta Simon 指派給 Tableau Online，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ea691-234">**To assign Britta Simon to Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="ea691-235">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ea691-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="ea691-237">在應用程式清單中，選取 [Tableau Online] 。</span><span class="sxs-lookup"><span data-stu-id="ea691-237">In the applications list, select **Tableau Online**.</span></span>

    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. <span data-ttu-id="ea691-239">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ea691-239">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="ea691-241">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ea691-241">Click **Add** button.</span></span> <span data-ttu-id="ea691-242">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ea691-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="ea691-244">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="ea691-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ea691-245">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ea691-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ea691-246">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ea691-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ea691-247">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="ea691-247">Testing single sign-on</span></span>

<span data-ttu-id="ea691-248">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="ea691-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="ea691-249">當您在存取面板中按一下 [Tableau Online ] 圖格時，應該會自動登入您的 Tableau Online 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea691-249">When you click the Tableau Online tile in the Access Panel, you should get automatically signed-on to your Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ea691-250">其他資源</span><span class="sxs-lookup"><span data-stu-id="ea691-250">Additional resources</span></span>

* [<span data-ttu-id="ea691-251">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="ea691-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ea691-252">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ea691-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png


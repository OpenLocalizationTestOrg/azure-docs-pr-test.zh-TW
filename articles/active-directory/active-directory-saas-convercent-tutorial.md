---
title: "教學課程：Azure Active Directory 與 Convercent 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Convercent 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9c9d290-0e13-490b-b559-0be772d6a690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: 7af33cae7448a212734d327570b5082d0278fa0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-convercent"></a><span data-ttu-id="c0c55-103">教學課程：Azure Active Directory 與 Convercent 整合</span><span class="sxs-lookup"><span data-stu-id="c0c55-103">Tutorial: Azure Active Directory integration with Convercent</span></span>

<span data-ttu-id="c0c55-104">在本教學課程中，您會了解如何整合 Convercent 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="c0c55-104">In this tutorial, you learn how to integrate Convercent with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0c55-105">將 Convercent 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="c0c55-105">Integrating Convercent with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c0c55-106">您可以在 Azure AD 中控制可存取 Convercent 的人員</span><span class="sxs-lookup"><span data-stu-id="c0c55-106">You can control in Azure AD who has access to Convercent</span></span>
- <span data-ttu-id="c0c55-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Convercent (單一登入)</span><span class="sxs-lookup"><span data-stu-id="c0c55-107">You can enable your users to automatically get signed-on to Convercent (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0c55-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="c0c55-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c0c55-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="c0c55-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0c55-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="c0c55-110">Prerequisites</span></span>

<span data-ttu-id="c0c55-111">若要設定 Azure AD 與 Convercent 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="c0c55-111">To configure Azure AD integration with Convercent, you need the following items:</span></span>

- <span data-ttu-id="c0c55-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c0c55-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0c55-113">已啟用 Convercent 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c0c55-113">A Convercent single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0c55-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="c0c55-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0c55-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="c0c55-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0c55-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="c0c55-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c0c55-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="c0c55-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0c55-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="c0c55-118">Scenario description</span></span>
<span data-ttu-id="c0c55-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c0c55-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0c55-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="c0c55-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0c55-121">從資源庫中新增 Convercent</span><span class="sxs-lookup"><span data-stu-id="c0c55-121">Adding Convercent from the gallery</span></span>
2. <span data-ttu-id="c0c55-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c0c55-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-convercent-from-the-gallery"></a><span data-ttu-id="c0c55-123">從資源庫中新增 Convercent</span><span class="sxs-lookup"><span data-stu-id="c0c55-123">Adding Convercent from the gallery</span></span>
<span data-ttu-id="c0c55-124">若要設定將 Convercent 整合到 Azure AD 中，您需要從資源庫將 Convercent 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="c0c55-124">To configure the integration of Convercent into Azure AD, you need to add Convercent from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c0c55-125">**若要從資源庫加入 Convercent，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c0c55-125">**To add Convercent from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c0c55-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="c0c55-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c0c55-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c0c55-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c0c55-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c0c55-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="c0c55-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c0c55-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="c0c55-133">在搜尋方塊中，輸入 **Convercent**。</span><span class="sxs-lookup"><span data-stu-id="c0c55-133">In the search box, type **Convercent**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_search.png)

5. <span data-ttu-id="c0c55-135">在結果窗格中，選取 [Convercent]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0c55-135">In the results panel, select **Convercent**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0c55-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c0c55-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0c55-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Convercent 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c0c55-138">In this section, you configure and test Azure AD single sign-on with Convercent based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c0c55-139">若要讓單一登入運作，Azure AD 必須知道 Convercent 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="c0c55-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Convercent is to a user in Azure AD.</span></span> <span data-ttu-id="c0c55-140">換句話說，必須在 Azure AD 使用者和 Convercent 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="c0c55-140">In other words, a link relationship between an Azure AD user and the related user in Convercent needs to be established.</span></span>

<span data-ttu-id="c0c55-141">建立此連結關聯性的方法，就是將 Azure AD 中 [使用者名稱] 的值，指派為 Convercent 中 [使用者名稱] 的值。</span><span class="sxs-lookup"><span data-stu-id="c0c55-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Convercent.</span></span>

<span data-ttu-id="c0c55-142">若要使用 Convercent 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="c0c55-142">To configure and test Azure AD single sign-on with Convercent, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c0c55-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="c0c55-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c0c55-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c0c55-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0c55-145">**[建立 Convercent 測試使用者](#creating-a-convercent-test-user)** - 在 Convercent 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="c0c55-145">**[Creating a Convercent test user](#creating-a-convercent-test-user)** - to have a counterpart of Britta Simon in Convercent that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c0c55-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c0c55-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0c55-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="c0c55-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0c55-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c0c55-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0c55-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Convercent 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="c0c55-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Convercent application.</span></span>

<span data-ttu-id="c0c55-150">**若要設定與 Convercent 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c0c55-150">**To configure Azure AD single sign-on with Convercent, perform the following steps:**</span></span>

1. <span data-ttu-id="c0c55-151">在 Azure 入口網站的 [Convercent] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="c0c55-151">In the Azure portal, on the **Convercent** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="c0c55-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="c0c55-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_samlbase.png)

3. <span data-ttu-id="c0c55-155">如果您想要以 **IDP 起始模式**設定應用程式，請在 [Convercent 網域和 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c0c55-155">On the **Convercent Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following step:</span></span>

    ![設定單一登入](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url.png)

    <span data-ttu-id="c0c55-157">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="c0c55-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.convercent.com/`</span></span>
 
4. <span data-ttu-id="c0c55-158">如果您想要以 **SP 起始模式**設定應用程式，請在 [Convercent 網域和 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c0c55-158">If you wish to configure the application in **SP initiated mode**, on the **Convercent Domain and URLs** section perform the following steps:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url1.png)

     <span data-ttu-id="c0c55-160">a.</span><span class="sxs-lookup"><span data-stu-id="c0c55-160">a.</span></span> <span data-ttu-id="c0c55-161">按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="c0c55-161">Click **"Show advanced URL settings."**</span></span> 

     <span data-ttu-id="c0c55-162">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0c55-162">b.</span></span> <span data-ttu-id="c0c55-163">在 [登入 URL] 文字方塊中，以下列模式輸入值：`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="c0c55-163">In the **Sign On URL** textbox, type the value using the following pattern: `https://<instancename>.convercent.com/`</span></span>

     <span data-ttu-id="c0c55-164">c.</span><span class="sxs-lookup"><span data-stu-id="c0c55-164">c.</span></span> <span data-ttu-id="c0c55-165">在 [轉送狀態] 文字方塊中，輸入使用下列模式的值：`https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="c0c55-165">In the **Relay State** textbox, type the value using the following pattern: `https://<instancename>.convercent.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c0c55-166">這些值都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="c0c55-166">These values are not the real values.</span></span> <span data-ttu-id="c0c55-167">使用實際的「識別碼」、「登入 URL」及「轉送狀態」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="c0c55-167">Update these values with the actual Identifier, Sign On URL and Relay State.</span></span> <span data-ttu-id="c0c55-168">請連絡 [Convercent 用戶端支援小組](http://support.convercent.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="c0c55-168">Contact [Convercent Client support team](http://support.convercent.com) to get these values.</span></span>

5. <span data-ttu-id="c0c55-169">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="c0c55-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_certificate.png) 

6. <span data-ttu-id="c0c55-171">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="c0c55-171">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-convercent-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="c0c55-173">若要為您的應用程式設定 SSO，請連絡 [Convercent 支援小組](mailto:support@convercent.com)並提供下載的**中繼資料 XML**。</span><span class="sxs-lookup"><span data-stu-id="c0c55-173">To get SSO configured for your application, contact [Convercent support team](mailto:support@convercent.com) and provide them with the downloaded **Metadata XML**.</span></span>

> [!TIP]
> <span data-ttu-id="c0c55-174">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="c0c55-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c0c55-175">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="c0c55-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c0c55-176">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c0c55-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0c55-177">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c0c55-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0c55-178">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="c0c55-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="c0c55-180">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c0c55-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c0c55-181">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="c0c55-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-convercent-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c0c55-183">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="c0c55-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-convercent-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0c55-185">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="c0c55-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-convercent-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0c55-187">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c0c55-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-convercent-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0c55-189">a.</span><span class="sxs-lookup"><span data-stu-id="c0c55-189">a.</span></span> <span data-ttu-id="c0c55-190">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="c0c55-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c0c55-191">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0c55-191">b.</span></span> <span data-ttu-id="c0c55-192">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="c0c55-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c0c55-193">c.</span><span class="sxs-lookup"><span data-stu-id="c0c55-193">c.</span></span> <span data-ttu-id="c0c55-194">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="c0c55-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c0c55-195">d.</span><span class="sxs-lookup"><span data-stu-id="c0c55-195">d.</span></span> <span data-ttu-id="c0c55-196">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="c0c55-196">Click **Create**.</span></span>
 
### <a name="creating-a-convercent-test-user"></a><span data-ttu-id="c0c55-197">建立 Convercent 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c0c55-197">Creating a Convercent test user</span></span>

<span data-ttu-id="c0c55-198">請與 [Convercent 支援小組](mailto:support@convercent.com)合作，在 Convercent 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="c0c55-198">Work with [Convercent support team](mailto:support@convercent.com) to add the users in the Convercent platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c0c55-199">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c0c55-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c0c55-200">在本節中，您會將 Convercent 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c0c55-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Convercent.</span></span>

![指派使用者][200] 

<span data-ttu-id="c0c55-202">**若要將 Britta Simon 指派到 Convercent，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c0c55-202">**To assign Britta Simon to Convercent, perform the following steps:**</span></span>

1. <span data-ttu-id="c0c55-203">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="c0c55-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="c0c55-205">在應用程式清單中，選取 [Convercent]。</span><span class="sxs-lookup"><span data-stu-id="c0c55-205">In the applications list, select **Convercent**.</span></span>

    ![設定單一登入](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_app.png) 

3. <span data-ttu-id="c0c55-207">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="c0c55-207">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="c0c55-209">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c0c55-209">Click **Add** button.</span></span> <span data-ttu-id="c0c55-210">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="c0c55-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="c0c55-212">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="c0c55-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c0c55-213">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c0c55-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0c55-214">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c0c55-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0c55-215">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="c0c55-215">Testing single sign-on</span></span>

<span data-ttu-id="c0c55-216">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="c0c55-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c0c55-217">當您在存取面板中按一下 [Convercent] 圖格時，應該會自動登入您的 Convercent 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0c55-217">When you click the Convercent tile in the Access Panel, you should get automatically signed-on to your Convercent application.</span></span>
<span data-ttu-id="c0c55-218">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="c0c55-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c0c55-219">其他資源</span><span class="sxs-lookup"><span data-stu-id="c0c55-219">Additional resources</span></span>

* [<span data-ttu-id="c0c55-220">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="c0c55-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0c55-221">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="c0c55-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_203.png


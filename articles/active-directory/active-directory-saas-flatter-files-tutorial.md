---
title: "教學課程：Azure Active Directory 與 Flatter Files 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Flatter Files 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: e02150cb27768d7b403bdca191bc1f189821def4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a><span data-ttu-id="1af24-103">教學課程：Azure Active Directory 與 Flatter Files 整合</span><span class="sxs-lookup"><span data-stu-id="1af24-103">Tutorial: Azure Active Directory integration with Flatter Files</span></span>

<span data-ttu-id="1af24-104">在本教學課程中，您將了解如何整合 Flatter Files 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="1af24-104">In this tutorial, you learn how to integrate Flatter Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1af24-105">Flatter Files 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="1af24-105">Integrating Flatter Files with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1af24-106">您可以在 Azure AD 中控制可存取 Flatter Files 的人員</span><span class="sxs-lookup"><span data-stu-id="1af24-106">You can control in Azure AD who has access to Flatter Files</span></span>
- <span data-ttu-id="1af24-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Flatter Files (單一登入)</span><span class="sxs-lookup"><span data-stu-id="1af24-107">You can enable your users to automatically get signed-on to Flatter Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1af24-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="1af24-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1af24-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="1af24-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1af24-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1af24-110">Prerequisites</span></span>

<span data-ttu-id="1af24-111">若要設定 Azure AD 與 Flatter Files 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="1af24-111">To configure Azure AD integration with Flatter Files, you need the following items:</span></span>

- <span data-ttu-id="1af24-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1af24-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1af24-113">已啟用 Flatter Files 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1af24-113">A Flatter Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1af24-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1af24-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1af24-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="1af24-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1af24-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1af24-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1af24-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="1af24-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1af24-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="1af24-118">Scenario description</span></span>
<span data-ttu-id="1af24-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1af24-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1af24-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="1af24-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1af24-121">從資源庫加入 Flatter Files</span><span class="sxs-lookup"><span data-stu-id="1af24-121">Adding Flatter Files from the gallery</span></span>
2. <span data-ttu-id="1af24-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1af24-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-flatter-files-from-the-gallery"></a><span data-ttu-id="1af24-123">從資源庫加入 Flatter Files</span><span class="sxs-lookup"><span data-stu-id="1af24-123">Adding Flatter Files from the gallery</span></span>
<span data-ttu-id="1af24-124">若要設定 Flatter Files 與 Azure AD 整合，您需要從資源庫將 Flatter Files 加入到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="1af24-124">To configure the integration of Flatter Files into Azure AD, you need to add Flatter Files from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1af24-125">**若要從資源庫加入 Flatter Files，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1af24-125">**To add Flatter Files from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1af24-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="1af24-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1af24-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1af24-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1af24-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1af24-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="1af24-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1af24-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="1af24-133">在搜尋方塊中，輸入 **Flatter Files**。</span><span class="sxs-lookup"><span data-stu-id="1af24-133">In the search box, type **Flatter Files**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_search.png)

5. <span data-ttu-id="1af24-135">在結果窗格中，選取 [Flatter Files]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="1af24-135">In the results panel, select **Flatter Files**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1af24-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1af24-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1af24-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Flatter Files 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1af24-138">In this section, you configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1af24-139">若要讓單一登入運作，Azure AD 必須知道 Flatter Files 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="1af24-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Flatter Files is to a user in Azure AD.</span></span> <span data-ttu-id="1af24-140">換句話說，必須在 Azure AD 使用者和 Flatter Files 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1af24-140">In other words, a link relationship between an Azure AD user and the related user in Flatter Files needs to be established.</span></span>

<span data-ttu-id="1af24-141">在 Flatter Files 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1af24-141">In Flatter Files, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1af24-142">若要使用 Flatter Files 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="1af24-142">To configure and test Azure AD single sign-on with Flatter Files, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1af24-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="1af24-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1af24-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1af24-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1af24-145">**[建立 Flatter Files 測試使用者](#creating-a-flatter-files-test-user)** - 在 Flatter Files 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="1af24-145">**[Creating a Flatter Files test user](#creating-a-flatter-files-test-user)** - to have a counterpart of Britta Simon in Flatter Files that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1af24-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1af24-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1af24-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="1af24-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1af24-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1af24-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1af24-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Flatter Files 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="1af24-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Flatter Files application.</span></span>

<span data-ttu-id="1af24-150">**若要使用 Flatter Files 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1af24-150">**To configure Azure AD single sign-on with Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="1af24-151">在 Azure 入口網站的 [Flatter Files] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="1af24-151">In the Azure portal, on the **Flatter Files** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="1af24-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="1af24-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

3. <span data-ttu-id="1af24-155">在 [Flatter Files 網域和 URL] 區段中，使用者不需要執行任何步驟，因為應用程式已預先與 Azure 整合。</span><span class="sxs-lookup"><span data-stu-id="1af24-155">On the **Flatter Files Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![設定單一登入](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
4. <span data-ttu-id="1af24-157">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="1af24-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

5. <span data-ttu-id="1af24-159">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="1af24-159">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-flatter-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1af24-161">在 [Flatter Files 組態] 區段上，按一下 [設定 Flatter Files] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="1af24-161">On the **Flatter Files Configuration** section, click **Configure Flatter Files** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1af24-162">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="1af24-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

7. <span data-ttu-id="1af24-164">以系統管理員身分登入您的 Flatter Files 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1af24-164">Sign-on to your Flatter Files application as an administrator.</span></span>

8. <span data-ttu-id="1af24-165">按一下 [儀表板]。</span><span class="sxs-lookup"><span data-stu-id="1af24-165">Click **DASHBOARD**.</span></span> 
   
    ![設定單一登入](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_05.png)  

9. <span data-ttu-id="1af24-167">按一下 [設定]，然後在 [公司] 索引標籤上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1af24-167">Click **Settings**, and then perform the following steps on the **Company** tab:</span></span> 
   
    ![設定單一登入](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
    <span data-ttu-id="1af24-169">a.</span><span class="sxs-lookup"><span data-stu-id="1af24-169">a.</span></span> <span data-ttu-id="1af24-170">選取 [使用 SAML 2.0 進行驗證]。</span><span class="sxs-lookup"><span data-stu-id="1af24-170">Select **Use SAML 2.0 for Authentication**.</span></span>
    
    <span data-ttu-id="1af24-171">b.</span><span class="sxs-lookup"><span data-stu-id="1af24-171">b.</span></span> <span data-ttu-id="1af24-172">按一下 [設定 SAML]。</span><span class="sxs-lookup"><span data-stu-id="1af24-172">Click **Configure SAML**.</span></span>

8. <span data-ttu-id="1af24-173">在 [SAML 設定]  對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1af24-173">On the **SAML Configuration** dialog, perform the following steps:</span></span> 
   
    ![設定單一登入](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
    <span data-ttu-id="1af24-175">a.</span><span class="sxs-lookup"><span data-stu-id="1af24-175">a.</span></span> <span data-ttu-id="1af24-176">在 [網域] 文字方塊中，輸入您註冊的網域。</span><span class="sxs-lookup"><span data-stu-id="1af24-176">In the **Domain** textbox, type your registered domain.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="1af24-177">如果您沒有已註冊的網域，請透過 [support@flatterfiles.com](mailto:support@flatterfiles.com)。</span><span class="sxs-lookup"><span data-stu-id="1af24-177">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span></span> 
    
    <span data-ttu-id="1af24-178">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1af24-178">b.</span></span> <span data-ttu-id="1af24-179">在 [識別提供者 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="1af24-179">In **Identity Provider URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied form Azure portal.</span></span>
   
    <span data-ttu-id="1af24-180">c.</span><span class="sxs-lookup"><span data-stu-id="1af24-180">c.</span></span>  <span data-ttu-id="1af24-181">在記事本中開啟您的 base-64 編碼的憑證，將它的內容複製到您的剪貼簿，然後貼入 [識別提供者憑證] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="1af24-181">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="1af24-182">d.</span><span class="sxs-lookup"><span data-stu-id="1af24-182">d.</span></span> <span data-ttu-id="1af24-183">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="1af24-183">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="1af24-184">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="1af24-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1af24-185">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="1af24-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1af24-186">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1af24-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1af24-187">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1af24-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="1af24-188">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="1af24-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="1af24-190">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1af24-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1af24-191">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="1af24-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1af24-193">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="1af24-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1af24-195">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="1af24-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1af24-197">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1af24-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1af24-199">a.</span><span class="sxs-lookup"><span data-stu-id="1af24-199">a.</span></span> <span data-ttu-id="1af24-200">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="1af24-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1af24-201">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1af24-201">b.</span></span> <span data-ttu-id="1af24-202">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="1af24-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1af24-203">c.</span><span class="sxs-lookup"><span data-stu-id="1af24-203">c.</span></span> <span data-ttu-id="1af24-204">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="1af24-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1af24-205">d.</span><span class="sxs-lookup"><span data-stu-id="1af24-205">d.</span></span> <span data-ttu-id="1af24-206">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1af24-206">Click **Create**.</span></span>
 
### <a name="creating-a-flatter-files-test-user"></a><span data-ttu-id="1af24-207">建立 Flatter Files 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1af24-207">Creating a Flatter Files test user</span></span>

<span data-ttu-id="1af24-208">本節的目標是在 Flatter Files 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="1af24-208">The objective of this section is to create a user called Britta Simon in Flatter Files.</span></span>

<span data-ttu-id="1af24-209">**若要在 Flatter Files 中建立名為 Britta Simon 的使用者，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="1af24-209">**To create a user called Britta Simon in Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="1af24-210">以系統管理員身分登入您的 **Flatter Files** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="1af24-210">Sign on to your **Flatter Files** company site as administrator.</span></span>

2. <span data-ttu-id="1af24-211">在左側導覽窗格中，按一下 [設定]，然後按一下 [使用者] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="1af24-211">In the navigation pane on the left, click **Settings**, and then click the **Users** tab.</span></span>
   
    ![建立 Flatter Files 使用者](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_09.png)

3. <span data-ttu-id="1af24-213">按一下 [加入使用者] 。</span><span class="sxs-lookup"><span data-stu-id="1af24-213">Click **Add User**.</span></span> 

4. <span data-ttu-id="1af24-214">在 [加入使用者]  對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1af24-214">On the **Add User** dialog, perform the following steps:</span></span>
   
    ![建立 Flatter Files 使用者](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_10.png)

    <span data-ttu-id="1af24-216">a.</span><span class="sxs-lookup"><span data-stu-id="1af24-216">a.</span></span> <span data-ttu-id="1af24-217">在 [名字] 文字方塊中，輸入 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="1af24-217">In the **First Name** textbox, type **Britta**.</span></span>
   
    <span data-ttu-id="1af24-218">b.</span><span class="sxs-lookup"><span data-stu-id="1af24-218">b.</span></span> <span data-ttu-id="1af24-219">在 [姓氏] 文字方塊中，輸入 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="1af24-219">In the **Last Name** textbox, type **Simon**.</span></span> 
   
    <span data-ttu-id="1af24-220">c.</span><span class="sxs-lookup"><span data-stu-id="1af24-220">c.</span></span> <span data-ttu-id="1af24-221">在 [電子郵件位址] 文字方塊中，輸入 Britta 在 Azure 入口網站中的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="1af24-221">In the **Email Address** textbox, type Britta's email address in the Azure portal.</span></span>
   
    <span data-ttu-id="1af24-222">d.</span><span class="sxs-lookup"><span data-stu-id="1af24-222">d.</span></span> <span data-ttu-id="1af24-223">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="1af24-223">Click **Submit**.</span></span>   


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1af24-224">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1af24-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1af24-225">在本節中，您會將 Flatter Files 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1af24-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Flatter Files.</span></span>

![指派使用者][200] 

<span data-ttu-id="1af24-227">**若要將 Britta Simon 指派到 Flatter Files，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="1af24-227">**To assign Britta Simon to Flatter Files, perform the following steps:**</span></span>

1. <span data-ttu-id="1af24-228">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1af24-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="1af24-230">在應用程式清單中，選取 [Flatter Files] 。</span><span class="sxs-lookup"><span data-stu-id="1af24-230">In the applications list, select **Flatter Files**.</span></span>

    ![設定單一登入](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_app.png) 

3. <span data-ttu-id="1af24-232">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1af24-232">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="1af24-234">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1af24-234">Click **Add** button.</span></span> <span data-ttu-id="1af24-235">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1af24-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="1af24-237">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="1af24-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1af24-238">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1af24-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1af24-239">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1af24-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1af24-240">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="1af24-240">Testing single sign-on</span></span>

<span data-ttu-id="1af24-241">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="1af24-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1af24-242">當您在存取面板中按一下 Flatter Files 磚時，應該會自動登入您的 Flatter Files 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1af24-242">When you click the Flatter Files tile in the Access Panel, you should get automatically signed-on to your Flatter Files application.</span></span>
<span data-ttu-id="1af24-243">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="1af24-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1af24-244">其他資源</span><span class="sxs-lookup"><span data-stu-id="1af24-244">Additional resources</span></span>

* [<span data-ttu-id="1af24-245">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="1af24-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1af24-246">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="1af24-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_203.png


---
title: "教學課程：Azure Active Directory 與 Huddle 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Huddle 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 59d4019545d39ec76bf401696338140f430630c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="71154-103">教學課程：Azure Active Directory 與 Huddle 整合</span><span class="sxs-lookup"><span data-stu-id="71154-103">Tutorial: Azure Active Directory integration with Huddle</span></span>

<span data-ttu-id="71154-104">在本教學課程中，您將了解如何整合 Huddle 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="71154-104">In this tutorial, you learn how to integrate Huddle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="71154-105">Huddle 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="71154-105">Integrating Huddle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="71154-106">您可以在 Azure AD 中控制可存取 Huddle 的人員</span><span class="sxs-lookup"><span data-stu-id="71154-106">You can control in Azure AD who has access to Huddle</span></span>
- <span data-ttu-id="71154-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Huddle (單一登入)</span><span class="sxs-lookup"><span data-stu-id="71154-107">You can enable your users to automatically get signed-on to Huddle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="71154-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="71154-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="71154-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="71154-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71154-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="71154-110">Prerequisites</span></span>

<span data-ttu-id="71154-111">若要設定與 Huddle 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="71154-111">To configure Azure AD integration with Huddle, you need the following items:</span></span>

- <span data-ttu-id="71154-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="71154-112">An Azure AD subscription</span></span>
- <span data-ttu-id="71154-113">已啟用 Huddle 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="71154-113">A Huddle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="71154-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="71154-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="71154-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="71154-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="71154-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="71154-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="71154-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="71154-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="71154-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="71154-118">Scenario description</span></span>

<span data-ttu-id="71154-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="71154-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="71154-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="71154-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="71154-121">從資源庫新增 Huddle</span><span class="sxs-lookup"><span data-stu-id="71154-121">Adding Huddle from the gallery</span></span>
2. <span data-ttu-id="71154-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="71154-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-huddle-from-the-gallery"></a><span data-ttu-id="71154-123">從資源庫新增 Huddle</span><span class="sxs-lookup"><span data-stu-id="71154-123">Adding Huddle from the gallery</span></span>
<span data-ttu-id="71154-124">若要設定將 Huddle 整合到 Azure AD 中，您需要從資源庫將 Huddle 新增到受管理的 SaaS app 清單。</span><span class="sxs-lookup"><span data-stu-id="71154-124">To configure the integration of Huddle into Azure AD, you need to add Huddle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="71154-125">**若要從資源庫新增 Huddle，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="71154-125">**To add Huddle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="71154-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="71154-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="71154-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="71154-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="71154-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="71154-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="71154-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="71154-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="71154-133">在搜尋方塊中，輸入 **Huddle**。</span><span class="sxs-lookup"><span data-stu-id="71154-133">In the search box, type **Huddle**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. <span data-ttu-id="71154-135">在結果窗格中，選取 [Huddle]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="71154-135">In the results panel, select **Huddle**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="71154-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="71154-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="71154-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Huddle 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="71154-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="71154-139">若要讓單一登入運作，Azure AD 必須知道 Huddle 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="71154-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Huddle is to a user in Azure AD.</span></span> <span data-ttu-id="71154-140">換句話說，必須建立 Azure AD 使用者和 Huddle 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="71154-140">In other words, a link relationship between an Azure AD user and the related user in Huddle needs to be established.</span></span>

<span data-ttu-id="71154-141">在 Huddle 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="71154-141">In Huddle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="71154-142">若要設定及測試與 Huddle 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="71154-142">To configure and test Azure AD single sign-on with Huddle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="71154-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="71154-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>

2. <span data-ttu-id="71154-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="71154-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>

3. <span data-ttu-id="71154-145">**[建立 Huddle 測試使用者](#creating-a-huddle-test-user)** - 使 Huddle 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="71154-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - to have a counterpart of Britta Simon in Huddle that is linked to the Azure AD representation of user.</span></span>

4. <span data-ttu-id="71154-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="71154-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>

5. <span data-ttu-id="71154-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="71154-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="71154-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="71154-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="71154-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Huddle 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="71154-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Huddle application.</span></span>

<span data-ttu-id="71154-150">**若要設定與 Huddle 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="71154-150">**To configure Azure AD single sign-on with Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="71154-151">在 Azure 入口網站的 [Huddle] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="71154-151">In the Azure portal, on the **Huddle** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="71154-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="71154-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. <span data-ttu-id="71154-155">在 [Huddle 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="71154-155">On the **Huddle Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    <span data-ttu-id="71154-157">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`http://<company name>.huddle.com`</span><span class="sxs-lookup"><span data-stu-id="71154-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<company name>.huddle.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="71154-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="71154-158">This value is not real.</span></span> <span data-ttu-id="71154-159">請使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="71154-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="71154-160">請連絡 [Huddle 用戶端支援小組](https://huddle.zendesk.com)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="71154-160">Contact [Huddle Client support team](https://huddle.zendesk.com) to get this value.</span></span> 

4. <span data-ttu-id="71154-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="71154-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. <span data-ttu-id="71154-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="71154-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="71154-165">在 [Huddle 組態] 區段上，按一下 [設定 Huddle] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="71154-165">On the **Huddle Configuration** section, click **Configure Huddle** to open **Configure sign-on** window.</span></span> <span data-ttu-id="71154-166">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="71154-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span> 

    ![設定單一登入](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. <span data-ttu-id="71154-168">若要在 Huddle 端設定單一登入，您必須將已下載的「憑證」、「SAML 單一登入服務 URL」及「SAML 實體識別碼」傳送給 [Huddle 用戶端支援小組](https://huddle.zendesk.com)。</span><span class="sxs-lookup"><span data-stu-id="71154-168">To configure single sign-on on Huddle side, you need to send the downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** to [Huddle Client support team](https://huddle.zendesk.com).</span></span> <span data-ttu-id="71154-169">他們會進行此設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="71154-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>  
   
    >[!NOTE]
    > <span data-ttu-id="71154-170">單一登入必須由 Huddle 支援小組啟用。</span><span class="sxs-lookup"><span data-stu-id="71154-170">Single sign-on needs to be enabled by the Huddle support team.</span></span> <span data-ttu-id="71154-171">設定完成後，您將會收到通知。</span><span class="sxs-lookup"><span data-stu-id="71154-171">You get a notification when the configuration has been completed.</span></span> 
    > 

> [!TIP]
> <span data-ttu-id="71154-172">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="71154-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="71154-173">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="71154-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="71154-174">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="71154-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
   
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="71154-175">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="71154-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="71154-176">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="71154-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="71154-178">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="71154-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="71154-179">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="71154-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="71154-181">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="71154-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="71154-183">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="71154-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="71154-185">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="71154-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="71154-187">a.</span><span class="sxs-lookup"><span data-stu-id="71154-187">a.</span></span> <span data-ttu-id="71154-188">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="71154-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="71154-189">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="71154-189">b.</span></span> <span data-ttu-id="71154-190">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="71154-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="71154-191">c.</span><span class="sxs-lookup"><span data-stu-id="71154-191">c.</span></span> <span data-ttu-id="71154-192">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="71154-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="71154-193">d.</span><span class="sxs-lookup"><span data-stu-id="71154-193">d.</span></span> <span data-ttu-id="71154-194">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="71154-194">Click **Create**.</span></span>
 
### <a name="creating-a-huddle-test-user"></a><span data-ttu-id="71154-195">建立 Huddle 測試使用者</span><span class="sxs-lookup"><span data-stu-id="71154-195">Creating a Huddle test user</span></span>

<span data-ttu-id="71154-196">若要讓 Azure AD 使用者可以登入 Huddle，則必須將他們佈建至 Huddle。</span><span class="sxs-lookup"><span data-stu-id="71154-196">To enable Azure AD users to log in to Huddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="71154-197">在 Huddle 的情況下，需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="71154-197">In the case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="71154-198">**若要設定使用者佈建，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="71154-198">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="71154-199">以系統管理員身分登入您的 **Huddle** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="71154-199">Log in to your **Huddle** company site as administrator.</span></span>
2. <span data-ttu-id="71154-200">按一下 [工作區] 。</span><span class="sxs-lookup"><span data-stu-id="71154-200">Click **Workspace**.</span></span>
3. <span data-ttu-id="71154-201">按一下 [人員] \> [邀請人員]。</span><span class="sxs-lookup"><span data-stu-id="71154-201">Click **People \> Invite People**.</span></span>
   
   <span data-ttu-id="71154-202">![人員](./media/active-directory-saas-huddle-tutorial/IC787838.png "人員")</span><span class="sxs-lookup"><span data-stu-id="71154-202">![People](./media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span></span>

4. <span data-ttu-id="71154-203">在 [建立新的邀請]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="71154-203">In the **Create a new invitation** section, perform the following steps:</span></span>
   
   <span data-ttu-id="71154-204">![新的邀請](./media/active-directory-saas-huddle-tutorial/IC787839.png "新的邀請")</span><span class="sxs-lookup"><span data-stu-id="71154-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
   <span data-ttu-id="71154-205">a.</span><span class="sxs-lookup"><span data-stu-id="71154-205">a.</span></span> <span data-ttu-id="71154-206">在 [選擇要邀請人員加入的小組] 清單中，選取 [小組]。</span><span class="sxs-lookup"><span data-stu-id="71154-206">In the **Choose a team to invite people to join** list, select **team**.</span></span>

   <span data-ttu-id="71154-207">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="71154-207">b.</span></span> <span data-ttu-id="71154-208">在 [輸入您想要邀請之人員的電子郵件地址] 文字方塊中，輸入您想要在其中佈建之有效 Azure AD 帳戶的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="71154-208">Type the **Email Address** of a valid Azure AD account you want to provision in to **Enter email address for people you'd like to invite** textbox.</span></span>

   <span data-ttu-id="71154-209">c.</span><span class="sxs-lookup"><span data-stu-id="71154-209">c.</span></span> <span data-ttu-id="71154-210">按一下 [邀請] 。</span><span class="sxs-lookup"><span data-stu-id="71154-210">Click **Invite**.</span></span>   
   
    >[!NOTE]
    > <span data-ttu-id="71154-211">Azure AD 帳戶的持有者會收到一封包含連結的電子郵件，以在啟用帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="71154-211">The Azure AD account holder will receive an email including a link to confirm the account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="71154-212">您可以使用任何其他的 Huddle 使用者帳戶建立工具或 Huddle 提供的 API 來佈建 Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="71154-212">You can use any other Huddle user account creation tools or APIs provided by Huddle to provision Azure AD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="71154-213">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="71154-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="71154-214">在本節中，您會將 Huddle 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="71154-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Huddle.</span></span>

![指派使用者][200] 

<span data-ttu-id="71154-216">**若要將 Britta Simon 指派給 Huddle，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="71154-216">**To assign Britta Simon to Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="71154-217">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="71154-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="71154-219">在應用程式清單中，選取[Huddle]。</span><span class="sxs-lookup"><span data-stu-id="71154-219">In the applications list, select **Huddle**.</span></span>

    ![設定單一登入](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. <span data-ttu-id="71154-221">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="71154-221">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="71154-223">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="71154-223">Click **Add** button.</span></span> <span data-ttu-id="71154-224">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="71154-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="71154-226">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="71154-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="71154-227">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="71154-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="71154-228">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="71154-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="71154-229">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="71154-229">Testing single sign-on</span></span>

<span data-ttu-id="71154-230">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="71154-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="71154-231">當您在存取面板中按一下 [Huddle ] 圖格時，您應該會取得 Huddle 應用程式的自動登入頁面。</span><span class="sxs-lookup"><span data-stu-id="71154-231">When you click the Huddle tile in the Access Panel, you should get automatically login page of Huddle application.</span></span>
<span data-ttu-id="71154-232">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="71154-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="71154-233">其他資源</span><span class="sxs-lookup"><span data-stu-id="71154-233">Additional resources</span></span>

* [<span data-ttu-id="71154-234">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="71154-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="71154-235">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="71154-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png

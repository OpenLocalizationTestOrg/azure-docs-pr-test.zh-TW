---
title: "教學課程：Azure Active Directory 與 QuickHelp 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 QuickHelp 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 1c72b0ddee636090129dab7a5c7ec6ffd452434a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a><span data-ttu-id="33452-103">教學課程：Azure Active Directory 與 QuickHelp 整合</span><span class="sxs-lookup"><span data-stu-id="33452-103">Tutorial: Azure Active Directory integration with QuickHelp</span></span>

<span data-ttu-id="33452-104">在本教學課程中，您會了解如何整合 QuickHelp 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="33452-104">In this tutorial, you learn how to integrate QuickHelp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="33452-105">QuickHelp 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="33452-105">Integrating QuickHelp with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="33452-106">您可以在 Azure AD 中控制可存取 QuickHelp 的人員</span><span class="sxs-lookup"><span data-stu-id="33452-106">You can control in Azure AD who has access to QuickHelp</span></span>
- <span data-ttu-id="33452-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 QuickHelp (單一登入)</span><span class="sxs-lookup"><span data-stu-id="33452-107">You can enable your users to automatically get signed-on to QuickHelp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="33452-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="33452-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="33452-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="33452-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33452-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="33452-110">Prerequisites</span></span>

<span data-ttu-id="33452-111">若要設定 Azure AD 與 QuickHelp 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="33452-111">To configure Azure AD integration with QuickHelp, you need the following items:</span></span>

- <span data-ttu-id="33452-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="33452-112">An Azure AD subscription</span></span>
- <span data-ttu-id="33452-113">啟用 QuickHelp 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="33452-113">A QuickHelp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="33452-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="33452-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="33452-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="33452-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="33452-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="33452-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="33452-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="33452-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="33452-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="33452-118">Scenario description</span></span>
<span data-ttu-id="33452-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="33452-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="33452-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="33452-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="33452-121">從資源庫加入 QuickHelp</span><span class="sxs-lookup"><span data-stu-id="33452-121">Adding QuickHelp from the gallery</span></span>
2. <span data-ttu-id="33452-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="33452-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-quickhelp-from-the-gallery"></a><span data-ttu-id="33452-123">從資源庫加入 QuickHelp</span><span class="sxs-lookup"><span data-stu-id="33452-123">Adding QuickHelp from the gallery</span></span>
<span data-ttu-id="33452-124">若要設定 QuickHelp 與 Azure AD 整合，您需要從資源庫將 QuickHelp 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="33452-124">To configure the integration of QuickHelp into Azure AD, you need to add QuickHelp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="33452-125">**若要從資源庫新增 QuickHelp，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="33452-125">**To add QuickHelp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="33452-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="33452-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="33452-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="33452-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="33452-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="33452-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="33452-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="33452-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="33452-133">在搜尋方塊中，輸入 **QuickHelp**。</span><span class="sxs-lookup"><span data-stu-id="33452-133">In the search box, type **QuickHelp**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_search.png)

5. <span data-ttu-id="33452-135">在結果面板中，選取 [QuickHelp]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="33452-135">In the results panel, select **QuickHelp**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="33452-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="33452-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="33452-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 QuickHelp 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="33452-138">In this section, you configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="33452-139">若要讓單一登入運作，Azure AD 必須知道 QuickHelp 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="33452-139">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp is to a user in Azure AD.</span></span> <span data-ttu-id="33452-140">換句話說，必須在 Azure AD 使用者和 QuickHelp 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="33452-140">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="33452-141">在 QuickHelp 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="33452-141">In QuickHelp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="33452-142">若要使用 QuickHelp 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="33452-142">To configure and test Azure AD single sign-on with QuickHelp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="33452-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="33452-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="33452-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="33452-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="33452-145">**[建立 QuickHelp 測試使用者](#creating-a-quickhelp-test-user)** - 使 QuickHelp 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="33452-145">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - to have a counterpart of Britta Simon in QuickHelp that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="33452-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="33452-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="33452-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="33452-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="33452-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="33452-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="33452-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 QuickHelp 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="33452-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your QuickHelp application.</span></span>

<span data-ttu-id="33452-150">**若要使用 QuickHelp 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="33452-150">**To configure Azure AD single sign-on with QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="33452-151">在 Azure 入口網站的 [QuickHelp] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="33452-151">In the Azure portal, on the **QuickHelp** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="33452-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="33452-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_samlbase.png)

3. <span data-ttu-id="33452-155">在 [QuickHelp 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="33452-155">On the **QuickHelp Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_url.png)

    <span data-ttu-id="33452-157">a.</span><span class="sxs-lookup"><span data-stu-id="33452-157">a.</span></span> <span data-ttu-id="33452-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://quickhelp.com/<instancename>/#/Login`</span><span class="sxs-lookup"><span data-stu-id="33452-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://quickhelp.com/<instancename>/#/Login`</span></span>

    <span data-ttu-id="33452-159">b.</span><span class="sxs-lookup"><span data-stu-id="33452-159">b.</span></span> <span data-ttu-id="33452-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<subdomain>.quickhelp.com`</span><span class="sxs-lookup"><span data-stu-id="33452-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.quickhelp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="33452-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="33452-161">These values are not real.</span></span> <span data-ttu-id="33452-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="33452-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="33452-163">請連絡 [QuickHelp 客戶支援小組](https://support.quickhelp.com/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="33452-163">Contact [QuickHelp Client support team](https://support.quickhelp.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="33452-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="33452-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_certificate.png) 

5. <span data-ttu-id="33452-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="33452-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-quickhelp-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="33452-168">以系統管理員身分登入您的 QuickHelp 公司網站。</span><span class="sxs-lookup"><span data-stu-id="33452-168">Sign-on to your QuickHelp company site as administrator.</span></span>

7. <span data-ttu-id="33452-169">在頂端的功能表中，按一下 [系統管理員] 。</span><span class="sxs-lookup"><span data-stu-id="33452-169">In the menu on the top, click **Admin**.</span></span>
   
    ![設定單一登入][21]

8. <span data-ttu-id="33452-171">在 [QuickHelp 系統管理員] 功能表上，按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="33452-171">In the **QuickHelp Admin** menu, click **Settings**.</span></span>
   
    ![設定單一登入][22]

9. <span data-ttu-id="33452-173">按一下 [驗證設定] 。</span><span class="sxs-lookup"><span data-stu-id="33452-173">Click **Authentication Settings**.</span></span>

10. <span data-ttu-id="33452-174">在 [驗證設定]  頁面上，執行下列步驟</span><span class="sxs-lookup"><span data-stu-id="33452-174">On the **Authentication Settings** page, perform the following steps</span></span>
   
    ![設定單一登入][23]
   
    <span data-ttu-id="33452-176">a.</span><span class="sxs-lookup"><span data-stu-id="33452-176">a.</span></span> <span data-ttu-id="33452-177">對 [SSO 類型] 選取 [WSFederation]。</span><span class="sxs-lookup"><span data-stu-id="33452-177">As **SSO Type**, select **WSFederation**.</span></span>
   
    <span data-ttu-id="33452-178">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="33452-178">b.</span></span> <span data-ttu-id="33452-179">若要上傳您下載的 Azure 中繼資料檔案，請按一下 [瀏覽]、瀏覽至該檔案，然後按一下 [上傳中繼資料]。</span><span class="sxs-lookup"><span data-stu-id="33452-179">To upload your downloaded Azure metadata file, click **Browse**, navigate to the file, end then click **Upload Metadata**.</span></span>
   
    <span data-ttu-id="33452-180">c.</span><span class="sxs-lookup"><span data-stu-id="33452-180">c.</span></span> <span data-ttu-id="33452-181">在 [電子郵件] 文字方塊中，輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`。</span><span class="sxs-lookup"><span data-stu-id="33452-181">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
   
    <span data-ttu-id="33452-182">d.</span><span class="sxs-lookup"><span data-stu-id="33452-182">d.</span></span> <span data-ttu-id="33452-183">在 [名字] 文字方塊中，輸入 `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`。</span><span class="sxs-lookup"><span data-stu-id="33452-183">In the **First Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
   
    <span data-ttu-id="33452-184">e.</span><span class="sxs-lookup"><span data-stu-id="33452-184">e.</span></span> <span data-ttu-id="33452-185">在 [姓氏] 文字方塊中，輸入 `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`。</span><span class="sxs-lookup"><span data-stu-id="33452-185">In the **Last Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
   
    <span data-ttu-id="33452-186">f.</span><span class="sxs-lookup"><span data-stu-id="33452-186">f.</span></span> <span data-ttu-id="33452-187">在 [動作列] 中，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="33452-187">In the **Action Bar**, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="33452-188">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="33452-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="33452-189">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="33452-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="33452-190">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="33452-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="33452-191">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="33452-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="33452-192">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="33452-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="33452-194">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="33452-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="33452-195">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="33452-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="33452-197">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="33452-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="33452-199">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="33452-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="33452-201">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="33452-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="33452-203">a.</span><span class="sxs-lookup"><span data-stu-id="33452-203">a.</span></span> <span data-ttu-id="33452-204">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="33452-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="33452-205">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="33452-205">b.</span></span> <span data-ttu-id="33452-206">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="33452-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="33452-207">c.</span><span class="sxs-lookup"><span data-stu-id="33452-207">c.</span></span> <span data-ttu-id="33452-208">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="33452-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="33452-209">d.</span><span class="sxs-lookup"><span data-stu-id="33452-209">d.</span></span> <span data-ttu-id="33452-210">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="33452-210">Click **Create**.</span></span>
 
### <a name="creating-a-quickhelp-test-user"></a><span data-ttu-id="33452-211">建立 QuickHelp 測試使用者</span><span class="sxs-lookup"><span data-stu-id="33452-211">Creating a QuickHelp test user</span></span>

<span data-ttu-id="33452-212">本節目標是在 QuickHelp 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="33452-212">The objective of this section is to create a user called Britta Simon in QuickHelp.</span></span>
<span data-ttu-id="33452-213">若要讓單一登入運作，Azure AD 必須知道 QuickHelp 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="33452-213">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp to a user in Azure AD is.</span></span> <span data-ttu-id="33452-214">換句話說，必須在 Azure AD 使用者和 QuickHelp 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="33452-214">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="33452-215">QuickHelp 支援 Just-in-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="33452-215">QuickHelp supports just-in-time provisioning.</span></span> <span data-ttu-id="33452-216">這表示如果需要，會在 QuickHelp 中自動建立使用者帳戶，並將該帳戶連結至 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="33452-216">This means, if necessary, a user account is automatically created in QuickHelp and the account is linked to the Azure AD account.</span></span>

<span data-ttu-id="33452-217">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="33452-217">There is no action item for you in this section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="33452-218">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="33452-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="33452-219">在本節中，您會將 QuickHelp 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="33452-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to QuickHelp.</span></span>

![指派使用者][200] 

<span data-ttu-id="33452-221">**若要將 Britta Simon 指派到 QuickHelp，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="33452-221">**To assign Britta Simon to QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="33452-222">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="33452-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="33452-224">在應用程式清單中，選取 [QuickHelp] 。</span><span class="sxs-lookup"><span data-stu-id="33452-224">In the applications list, select **QuickHelp**.</span></span>

    ![設定單一登入](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_app.png) 

3. <span data-ttu-id="33452-226">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="33452-226">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="33452-228">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="33452-228">Click **Add** button.</span></span> <span data-ttu-id="33452-229">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="33452-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="33452-231">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="33452-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="33452-232">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="33452-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="33452-233">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="33452-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="33452-234">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="33452-234">Testing single sign-on</span></span>

<span data-ttu-id="33452-235">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="33452-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="33452-236">當您在存取面板中按一下 [QuickHelp] 磚時，應該會自動登入您的 QuickHelp 應用程式。</span><span class="sxs-lookup"><span data-stu-id="33452-236">When you click the QuickHelp tile in the Access Panel, you should get automatically signed-on to your QuickHelp application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="33452-237">其他資源</span><span class="sxs-lookup"><span data-stu-id="33452-237">Additional resources</span></span>

* [<span data-ttu-id="33452-238">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="33452-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="33452-239">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="33452-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_203.png
[21]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_07.png

---
title: "教學課程：Azure Active Directory 與 Jive 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Jive 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 6d2d4b777d7afd74598d2eba4a7e3571a8a18d6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a><span data-ttu-id="66457-103">教學課程：Azure Active Directory 與 Jive 整合</span><span class="sxs-lookup"><span data-stu-id="66457-103">Tutorial: Azure Active Directory integration with Jive</span></span>

<span data-ttu-id="66457-104">在本教學課程中，您會了解如何整合 Jive 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="66457-104">In this tutorial, you learn how to integrate Jive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="66457-105">Jive 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="66457-105">Integrating Jive with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="66457-106">您可以在 Azure AD 中控制可存取 Jive</span><span class="sxs-lookup"><span data-stu-id="66457-106">You can control in Azure AD who has access to Jive</span></span>
- <span data-ttu-id="66457-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Jive (單一登入)</span><span class="sxs-lookup"><span data-stu-id="66457-107">You can enable your users to automatically get signed-on to Jive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="66457-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="66457-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="66457-109">若您想了解 SaaS app 與 Azure AD 整合的更多資訊，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="66457-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66457-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="66457-110">Prerequisites</span></span>

<span data-ttu-id="66457-111">若要設定 Azure AD 與 Jive 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="66457-111">To configure Azure AD integration with Jive, you need the following items:</span></span>

- <span data-ttu-id="66457-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="66457-112">An Azure AD subscription</span></span>
- <span data-ttu-id="66457-113">啟用 Jive 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="66457-113">A Jive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="66457-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="66457-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="66457-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="66457-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="66457-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="66457-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="66457-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="66457-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="66457-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="66457-118">Scenario description</span></span>
<span data-ttu-id="66457-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="66457-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="66457-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="66457-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="66457-121">從資源庫新增 Jive</span><span class="sxs-lookup"><span data-stu-id="66457-121">Adding Jive from the gallery</span></span>
2. <span data-ttu-id="66457-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="66457-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jive-from-the-gallery"></a><span data-ttu-id="66457-123">從資源庫新增 Jive</span><span class="sxs-lookup"><span data-stu-id="66457-123">Adding Jive from the gallery</span></span>
<span data-ttu-id="66457-124">若要設定將 Jive 整合到 Azure AD 中，您需要從資源庫將 Jive 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="66457-124">To configure the integration of Jive into Azure AD, you need to add Jive from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="66457-125">**若要從資源庫新增 Jive，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="66457-125">**To add Jive from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="66457-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="66457-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="66457-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="66457-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="66457-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="66457-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="66457-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="66457-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="66457-133">在搜尋方塊中，輸入 **Jive**。</span><span class="sxs-lookup"><span data-stu-id="66457-133">In the search box, type **Jive**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jive-tutorial/tutorial_jive_search.png)

5. <span data-ttu-id="66457-135">在結果面板中，選取 [Jive]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="66457-135">In the results panel, select **Jive**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jive-tutorial/tutorial_jive_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="66457-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="66457-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="66457-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Jive 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="66457-138">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="66457-139">若要讓單一登入運作，Azure AD 必須知道 Jive 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="66457-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jive is to a user in Azure AD.</span></span> <span data-ttu-id="66457-140">換句話說，必須建立 Azure AD 使用者和 Jive 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="66457-140">In other words, a link relationship between an Azure AD user and the related user in Jive needs to be established.</span></span>

<span data-ttu-id="66457-141">建立此連結關聯性的方法，就是將 Azure AD 中 [使用者名稱] 的值，指派為 Jive 中 [Username] 的值。</span><span class="sxs-lookup"><span data-stu-id="66457-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Jive.</span></span>

<span data-ttu-id="66457-142">若要設定及測試與 Jive 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="66457-142">To configure and test Azure AD single sign-on with Jive, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="66457-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="66457-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="66457-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="66457-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="66457-145">**[建立 Jive 測試使用者](#creating-a-jive-test-user)** - 使 Jive 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="66457-145">**[Creating a Jive test user](#creating-a-jive-test-user)** - to have a counterpart of Britta Simon in Jive that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="66457-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="66457-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="66457-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="66457-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="66457-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="66457-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="66457-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Jive 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="66457-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jive application.</span></span>

<span data-ttu-id="66457-150">**若要設定與 Jive 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="66457-150">**To configure Azure AD single sign-on with Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="66457-151">在 Azure 入口網站的 [Jive] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="66457-151">In the Azure portal, on the **Jive** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="66457-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="66457-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-jive-tutorial/tutorial_jive_samlbase.png)

3. <span data-ttu-id="66457-155">在 [Jive 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="66457-155">On the **Jive Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-jive-tutorial/tutorial_jive_url.png)

    <span data-ttu-id="66457-157">a.</span><span class="sxs-lookup"><span data-stu-id="66457-157">a.</span></span> <span data-ttu-id="66457-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<instance name>.jivecustom.com`</span><span class="sxs-lookup"><span data-stu-id="66457-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance name>.jivecustom.com`</span></span>

    <span data-ttu-id="66457-159">b.</span><span class="sxs-lookup"><span data-stu-id="66457-159">b.</span></span> <span data-ttu-id="66457-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<instance name>.jiveon.com`</span><span class="sxs-lookup"><span data-stu-id="66457-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.jiveon.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="66457-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="66457-161">These values are not the real.</span></span> <span data-ttu-id="66457-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="66457-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="66457-163">請連絡 [Jive 客戶支援小組](https://www.jivesoftware.com/services-support/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="66457-163">Contact [Jive Client support team](https://www.jivesoftware.com/services-support/) to get these values.</span></span> 
 
4. <span data-ttu-id="66457-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="66457-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-jive-tutorial/tutorial_jive_certificate.png) 

5. <span data-ttu-id="66457-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="66457-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-jive-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="66457-168">若要在 **Jive** 端設定單一登入，請以系統管理員身分登入您的 Jive 租用戶。</span><span class="sxs-lookup"><span data-stu-id="66457-168">To configure single sign-on on **Jive** side, sign-on to your Jive tenant as an administrator.</span></span>

7. <span data-ttu-id="66457-169">在頂端的功能表中，按一下 [Saml]。</span><span class="sxs-lookup"><span data-stu-id="66457-169">In the menu on the top, Click "**Saml**."</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-jive-tutorial/tutorial_jive_002.png)

    <span data-ttu-id="66457-171">a.</span><span class="sxs-lookup"><span data-stu-id="66457-171">a.</span></span> <span data-ttu-id="66457-172">選取 [一般] 索引標籤下的 [已啟用]。</span><span class="sxs-lookup"><span data-stu-id="66457-172">Select **Enabled** under the **General** tab.</span></span>   
    <span data-ttu-id="66457-173">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="66457-173">b.</span></span> <span data-ttu-id="66457-174">按一下 [儲存所有 saml 設定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="66457-174">Click the "**Save all saml settings**" button.</span></span>

8. <span data-ttu-id="66457-175">瀏覽至 [Idp 中繼資料]索引標籤。</span><span class="sxs-lookup"><span data-stu-id="66457-175">Navigate to the "**Idp Metadata**" tab.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-jive-tutorial/tutorial_jive_003.png)
   
    <span data-ttu-id="66457-177">a.</span><span class="sxs-lookup"><span data-stu-id="66457-177">a.</span></span> <span data-ttu-id="66457-178">複製下載的中繼資料 XML 檔案內容，然後貼到 [識別提供者 (IDP) 中繼資料] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="66457-178">Copy the content of the downloaded metadata XML file, and then paste it into the **Identity Provider (IDP) Metadata** textbox.</span></span>
    
    <span data-ttu-id="66457-179">b.</span><span class="sxs-lookup"><span data-stu-id="66457-179">b.</span></span> <span data-ttu-id="66457-180">按一下 [儲存所有 saml 設定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="66457-180">Click the "**Save all saml settings**" button.</span></span> 

9. <span data-ttu-id="66457-181">移至 [使用者屬性對應]索引標籤。</span><span class="sxs-lookup"><span data-stu-id="66457-181">Go to the "**User Attribute Mapping**" tab.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-jive-tutorial/tutorial_jive_004.png)
   
    <span data-ttu-id="66457-183">a.</span><span class="sxs-lookup"><span data-stu-id="66457-183">a.</span></span> <span data-ttu-id="66457-184">在 [電子郵件] 文字方塊中，複製並貼上值為 **mail** 的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="66457-184">In the **Email** textbox, copy and paste the attribute name of **mail** value.</span></span>
   
    <span data-ttu-id="66457-185">b.</span><span class="sxs-lookup"><span data-stu-id="66457-185">b.</span></span> <span data-ttu-id="66457-186">在 [名字] 文字方塊中，複製並貼上值為 **givenname** 的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="66457-186">In the **First Name** textbox, copy and paste the attribute name of **givenname** value.</span></span>
   
    <span data-ttu-id="66457-187">c.</span><span class="sxs-lookup"><span data-stu-id="66457-187">c.</span></span> <span data-ttu-id="66457-188">在 [姓氏] 文字方塊中，複製並貼上值為 **surname** 的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="66457-188">In the **Last Name** textbox, copy and paste the attribute name of **surname** value.</span></span>

> [!TIP]
> <span data-ttu-id="66457-189">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="66457-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="66457-190">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="66457-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="66457-191">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="66457-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="66457-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="66457-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="66457-193">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="66457-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="66457-195">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="66457-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="66457-196">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="66457-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jive-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="66457-198">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="66457-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jive-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="66457-200">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="66457-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jive-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="66457-202">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="66457-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jive-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="66457-204">a.</span><span class="sxs-lookup"><span data-stu-id="66457-204">a.</span></span> <span data-ttu-id="66457-205">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="66457-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="66457-206">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="66457-206">b.</span></span> <span data-ttu-id="66457-207">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="66457-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="66457-208">c.</span><span class="sxs-lookup"><span data-stu-id="66457-208">c.</span></span> <span data-ttu-id="66457-209">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="66457-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="66457-210">d.</span><span class="sxs-lookup"><span data-stu-id="66457-210">d.</span></span> <span data-ttu-id="66457-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="66457-211">Click **Create**.</span></span>
 
### <a name="creating-a-jive-test-user"></a><span data-ttu-id="66457-212">建立 Jive 測試使用者</span><span class="sxs-lookup"><span data-stu-id="66457-212">Creating a Jive test user</span></span>

<span data-ttu-id="66457-213">請與 [Jive 客戶支援小組](https://www.jivesoftware.com/services-support/)合作，在 Jive 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="66457-213">Work with [Jive Client support team](https://www.jivesoftware.com/services-support/) to add the users in the Jive platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="66457-214">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="66457-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="66457-215">在本節中，您會將 Jive 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="66457-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jive.</span></span>

![指派使用者][200] 

<span data-ttu-id="66457-217">**若要將 Britta Simon 指派給 Jive，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="66457-217">**To assign Britta Simon to Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="66457-218">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="66457-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="66457-220">在應用程式清單中，選取 [Jive] 。</span><span class="sxs-lookup"><span data-stu-id="66457-220">In the applications list, select **Jive**.</span></span>

    ![設定單一登入](./media/active-directory-saas-jive-tutorial/tutorial_jive_app.png) 

3. <span data-ttu-id="66457-222">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="66457-222">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="66457-224">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="66457-224">Click **Add** button.</span></span> <span data-ttu-id="66457-225">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="66457-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="66457-227">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="66457-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="66457-228">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="66457-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="66457-229">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="66457-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="66457-230">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="66457-230">Testing single sign-on</span></span>

<span data-ttu-id="66457-231">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="66457-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="66457-232">當您按一下存取面板中的 Jive 圖格時，您應該會自動登入您的 Jive 應用程式。</span><span class="sxs-lookup"><span data-stu-id="66457-232">When you click the Jive tile in the Access Panel, you should get automatically signed-on to your Jive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="66457-233">其他資源</span><span class="sxs-lookup"><span data-stu-id="66457-233">Additional resources</span></span>

* [<span data-ttu-id="66457-234">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="66457-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="66457-235">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="66457-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="66457-236">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="66457-236">Configure User Provisioning</span></span>](active-directory-saas-jive-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jive-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jive-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jive-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jive-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jive-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jive-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jive-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jive-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jive-tutorial/tutorial_general_203.png


---
title: "教學課程：將 Azure Active Directory 與 StatusPage 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 StatusPage 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: fa16cdec7b89404c140435fe57d5aa4b08cfa985
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a><span data-ttu-id="e028f-103">教學課程：將 Azure Active Directory 與 StatusPage 整合</span><span class="sxs-lookup"><span data-stu-id="e028f-103">Tutorial: Azure Active Directory integration with StatusPage</span></span>

<span data-ttu-id="e028f-104">在本教學課程中，您將了解如何整合 StatusPage 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="e028f-104">In this tutorial, you learn how to integrate StatusPage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e028f-105">StatusPage 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="e028f-105">Integrating StatusPage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e028f-106">您可在 Azure AD 中控制可存取 StatusPage 的人員</span><span class="sxs-lookup"><span data-stu-id="e028f-106">You can control in Azure AD who has access to StatusPage</span></span>
- <span data-ttu-id="e028f-107">您可讓使用者使用他們的 Azure AD 帳戶自動登入 StatusPage (單一登入)</span><span class="sxs-lookup"><span data-stu-id="e028f-107">You can enable your users to automatically get signed-on to StatusPage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e028f-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="e028f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e028f-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="e028f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e028f-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="e028f-110">Prerequisites</span></span>

<span data-ttu-id="e028f-111">若要設定 Azure AD 與 StatusPage 的整合作業，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="e028f-111">To configure Azure AD integration with StatusPage, you need the following items:</span></span>

- <span data-ttu-id="e028f-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e028f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e028f-113">已啟用 StatusPage 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e028f-113">A StatusPage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e028f-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e028f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e028f-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="e028f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e028f-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e028f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e028f-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="e028f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e028f-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="e028f-118">Scenario description</span></span>
<span data-ttu-id="e028f-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e028f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e028f-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="e028f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e028f-121">從資源庫加入 StatusPage</span><span class="sxs-lookup"><span data-stu-id="e028f-121">Adding StatusPage from the gallery</span></span>
2. <span data-ttu-id="e028f-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e028f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-statuspage-from-the-gallery"></a><span data-ttu-id="e028f-123">從資源庫加入 StatusPage</span><span class="sxs-lookup"><span data-stu-id="e028f-123">Adding StatusPage from the gallery</span></span>
<span data-ttu-id="e028f-124">若要設定 StatusPage 與 Azure AD 的整合作業，您必須從資源庫將 StatusPage 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="e028f-124">To configure the integration of StatusPage into Azure AD, you need to add StatusPage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e028f-125">**若要從資源庫新增 StatusPage，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e028f-125">**To add StatusPage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e028f-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e028f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e028f-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e028f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e028f-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e028f-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="e028f-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e028f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="e028f-133">在搜尋方塊中，輸入 **StatusPage**。</span><span class="sxs-lookup"><span data-stu-id="e028f-133">In the search box, type **StatusPage**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_search.png)

5. <span data-ttu-id="e028f-135">在結果窗格中，選取 [StatusPage]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="e028f-135">In the results panel, select **StatusPage**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e028f-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e028f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e028f-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 StatusPage 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e028f-138">In this section, you configure and test Azure AD single sign-on with StatusPage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e028f-139">若要使單一登入作用，Azure AD 必須知道 StatusPage 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="e028f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in StatusPage is to a user in Azure AD.</span></span> <span data-ttu-id="e028f-140">換句話說，必須在 Azure AD 使用者和 StatusPage 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e028f-140">In other words, a link relationship between an Azure AD user and the related user in StatusPage needs to be established.</span></span>

<span data-ttu-id="e028f-141">在 StatusPage 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e028f-141">In StatusPage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e028f-142">若要設定並測試透過 StatusPage 使用 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="e028f-142">To configure and test Azure AD single sign-on with StatusPage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e028f-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="e028f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e028f-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e028f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e028f-145">**[建立 StatusPage 測試使用者](#creating-a-statuspage-test-user)** - 在 StatusPage 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="e028f-145">**[Creating a StatusPage test user](#creating-a-statuspage-test-user)** - to have a counterpart of Britta Simon in StatusPage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e028f-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e028f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e028f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="e028f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e028f-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e028f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e028f-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 StatusPage 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="e028f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your StatusPage application.</span></span>

<span data-ttu-id="e028f-150">**若要設定透過 StatusPage 使用 Azure AD 單一登入功能，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e028f-150">**To configure Azure AD single sign-on with StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="e028f-151">在 Azure 入口網站的 [StatusPage] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="e028f-151">In the Azure portal, on the **StatusPage** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="e028f-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="e028f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_samlbase.png)

3. <span data-ttu-id="e028f-155">在 [StatusPage 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e028f-155">On the **StatusPage Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_url.png)

    <span data-ttu-id="e028f-157">a.</span><span class="sxs-lookup"><span data-stu-id="e028f-157">a.</span></span> <span data-ttu-id="e028f-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="e028f-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |

    <span data-ttu-id="e028f-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e028f-159">b.</span></span> <span data-ttu-id="e028f-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="e028f-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span> 
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |

    > [!NOTE]
    > <span data-ttu-id="e028f-161">請透過 [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)連絡 StatusPage 支援小組，要求設定單一登入所需的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="e028f-161">Contact the StatusPage support team at [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)to request metadata necessary to configure single sign-on.</span></span> 
    >
    ><span data-ttu-id="e028f-162">a.</span><span class="sxs-lookup"><span data-stu-id="e028f-162">a.</span></span> <span data-ttu-id="e028f-163">從中繼資料複製簽發者值，然後貼至 [識別碼] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="e028f-163">From the metadata, copy the Issuer value, and then paste it into the **Identifier** textbox.</span></span>
    >
    ><span data-ttu-id="e028f-164">b.</span><span class="sxs-lookup"><span data-stu-id="e028f-164">b.</span></span> <span data-ttu-id="e028f-165">從中繼資料複製回覆 URL，然後貼至 [回覆 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="e028f-165">From the metadata, copy the Reply URL, and then paste it into the **Reply URL** textbox.</span></span>

4. <span data-ttu-id="e028f-166">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="e028f-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_certificate.png) 

5. <span data-ttu-id="e028f-168">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e028f-168">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e028f-170">在 [StatusPage 組態] 區段上，按一下 [設定 StatusPage] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="e028f-170">On the **StatusPage Configuration** section, click **Configure StatusPage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e028f-171">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="e028f-171">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_configure.png) 

7. <span data-ttu-id="e028f-173">在另一個瀏覽器視窗中，以系統管理員身分登入您的 StatusPage 公司網站。</span><span class="sxs-lookup"><span data-stu-id="e028f-173">In another browser window, sign on to your StatusPage company site as an administrator.</span></span>

8. <span data-ttu-id="e028f-174">在主工具列中，按一下 [管理帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="e028f-174">In the main toolbar, click **Manage Account**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png) 

10. <span data-ttu-id="e028f-176">按一下 [單一登入]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e028f-176">Click the **Single Sign-on** tab.</span></span> 
   
    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_07.png) 

11. <span data-ttu-id="e028f-178">在 [SSO 設定] 頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e028f-178">On the SSO Setup page, perform the following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_08.png) 

    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_09.png) 
 
    <span data-ttu-id="e028f-181">a.</span><span class="sxs-lookup"><span data-stu-id="e028f-181">a.</span></span> <span data-ttu-id="e028f-182">在 [SSO 目標 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="e028f-182">In the **SSO Target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e028f-183">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e028f-183">b.</span></span> <span data-ttu-id="e028f-184">在記事本中開啟下載的憑證，複製其內容，然後貼到 [憑證] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="e028f-184">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span> 

    <span data-ttu-id="e028f-185">c.</span><span class="sxs-lookup"><span data-stu-id="e028f-185">c.</span></span> <span data-ttu-id="e028f-186">按一下 [儲存組態]。</span><span class="sxs-lookup"><span data-stu-id="e028f-186">Click **SAVE CONFIGURATION**.</span></span>

> [!TIP]
> <span data-ttu-id="e028f-187">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="e028f-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e028f-188">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="e028f-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e028f-189">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e028f-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e028f-190">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e028f-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="e028f-191">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="e028f-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="e028f-193">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e028f-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e028f-194">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e028f-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-statuspage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e028f-196">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="e028f-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-statuspage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e028f-198">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e028f-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-statuspage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e028f-200">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e028f-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-statuspage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e028f-202">a.</span><span class="sxs-lookup"><span data-stu-id="e028f-202">a.</span></span> <span data-ttu-id="e028f-203">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="e028f-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e028f-204">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e028f-204">b.</span></span> <span data-ttu-id="e028f-205">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="e028f-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e028f-206">c.</span><span class="sxs-lookup"><span data-stu-id="e028f-206">c.</span></span> <span data-ttu-id="e028f-207">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="e028f-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e028f-208">d.</span><span class="sxs-lookup"><span data-stu-id="e028f-208">d.</span></span> <span data-ttu-id="e028f-209">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="e028f-209">Click **Create**.</span></span>
 
### <a name="creating-a-statuspage-test-user"></a><span data-ttu-id="e028f-210">建立 StatusPage 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e028f-210">Creating a StatusPage test user</span></span>

<span data-ttu-id="e028f-211">本節目標是在 StatusPage 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="e028f-211">The objective of this section is to create a user called Britta Simon in StatusPage.</span></span>

<span data-ttu-id="e028f-212">StatusPage 支援 Just-in-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="e028f-212">StatusPage supports just-in-time provisioning.</span></span> <span data-ttu-id="e028f-213">您已在 [設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)中啟用。</span><span class="sxs-lookup"><span data-stu-id="e028f-213">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="e028f-214">**若要在 StatusPage 中建立名為 Britta Simon 的使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e028f-214">**To create a user called Britta Simon in StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="e028f-215">以管理員身分登入您的 StatusPage 公司網站。</span><span class="sxs-lookup"><span data-stu-id="e028f-215">Sign-on to your StatusPage company site as an administrator.</span></span>

2. <span data-ttu-id="e028f-216">在頂端功能表中，按一下 [ **管理帳戶**]。</span><span class="sxs-lookup"><span data-stu-id="e028f-216">In the menu on the top, click **Manage Account**.</span></span>

    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png)

3. <span data-ttu-id="e028f-218">按一下 [小組成員] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e028f-218">Click the **Team Members** tab.</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_10.png) 

4. <span data-ttu-id="e028f-220">按一下 [新增小組成員]。</span><span class="sxs-lookup"><span data-stu-id="e028f-220">Click **ADD TEAM MEMBER**.</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_11.png) 

5. <span data-ttu-id="e028f-222">在相關的文字方塊中，輸入您想要佈建之有效使用者的 [電子郵件地址]、[名字] 和 [姓氏]。</span><span class="sxs-lookup"><span data-stu-id="e028f-222">Type the **Email Address**, **First Name**, and **Sur Name** of a valid user you want to provision into the related textboxes.</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_12.png) 

6. <span data-ttu-id="e028f-224">針對 [角色]，選擇 [用戶端系統管理員]。</span><span class="sxs-lookup"><span data-stu-id="e028f-224">As **Role**, choose **Client Administrator**.</span></span>

7. <span data-ttu-id="e028f-225">按一下 [建立帳戶]。</span><span class="sxs-lookup"><span data-stu-id="e028f-225">Click **CREATE ACCOUNT**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e028f-226">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e028f-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e028f-227">在本節中，您會將 StatusPage 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e028f-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to StatusPage.</span></span>

![指派使用者][200] 

<span data-ttu-id="e028f-229">**若要將 Britta Simon 指派到 StatusPage，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="e028f-229">**To assign Britta Simon to StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="e028f-230">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e028f-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="e028f-232">在應用程式清單中，選取 [StatusPage] 。</span><span class="sxs-lookup"><span data-stu-id="e028f-232">In the applications list, select **StatusPage**.</span></span>

    ![設定單一登入](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_app.png) 

3. <span data-ttu-id="e028f-234">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e028f-234">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="e028f-236">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e028f-236">Click **Add** button.</span></span> <span data-ttu-id="e028f-237">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e028f-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="e028f-239">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="e028f-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e028f-240">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e028f-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e028f-241">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e028f-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e028f-242">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="e028f-242">Testing single sign-on</span></span>

<span data-ttu-id="e028f-243">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="e028f-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e028f-244">當您在存取面板中按一下 StatusPage 磚時，應該會自動登入您的 StatusPage 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e028f-244">When you click the StatusPage tile in the Access Panel, you should get automatically signed-on to your StatusPage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e028f-245">其他資源</span><span class="sxs-lookup"><span data-stu-id="e028f-245">Additional resources</span></span>

* [<span data-ttu-id="e028f-246">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="e028f-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e028f-247">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="e028f-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_203.png


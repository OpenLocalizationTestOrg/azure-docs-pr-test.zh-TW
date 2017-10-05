---
title: "教學課程：Azure Active Directory 與 Hosted Graphite 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Hosted Graphite 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a1ac4d7f-d079-4f3c-b6da-0f520d427ceb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f6ed02cc67be4090402a115c30819ff6cff99c99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hosted-graphite"></a><span data-ttu-id="a9cb0-103">教學課程：Azure Active Directory 與 Hosted Graphite 整合</span><span class="sxs-lookup"><span data-stu-id="a9cb0-103">Tutorial: Azure Active Directory integration with Hosted Graphite</span></span>

<span data-ttu-id="a9cb0-104">在本教學課程中，您將了解如何整合 Hosted Graphite 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-104">In this tutorial, you learn how to integrate Hosted Graphite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a9cb0-105">將 Hosted Graphite 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="a9cb0-105">Integrating Hosted Graphite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a9cb0-106">您可以在 Azure AD 中控制可存取 Hosted Graphite 的人員</span><span class="sxs-lookup"><span data-stu-id="a9cb0-106">You can control in Azure AD who has access to Hosted Graphite</span></span>
- <span data-ttu-id="a9cb0-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Hosted Graphite (單一登入)</span><span class="sxs-lookup"><span data-stu-id="a9cb0-107">You can enable your users to automatically get signed-on to Hosted Graphite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a9cb0-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="a9cb0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a9cb0-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9cb0-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a9cb0-110">Prerequisites</span></span>

<span data-ttu-id="a9cb0-111">若要設定 Azure AD 與 Hosted Graphite 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="a9cb0-111">To configure Azure AD integration with Hosted Graphite, you need the following items:</span></span>

- <span data-ttu-id="a9cb0-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a9cb0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a9cb0-113">已啟用 Hosted Graphite 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a9cb0-113">A Hosted Graphite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a9cb0-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a9cb0-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="a9cb0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a9cb0-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a9cb0-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a9cb0-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="a9cb0-118">Scenario description</span></span>
<span data-ttu-id="a9cb0-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a9cb0-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="a9cb0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a9cb0-121">從資源庫新增 Hosted Graphite</span><span class="sxs-lookup"><span data-stu-id="a9cb0-121">Adding Hosted Graphite from the gallery</span></span>
2. <span data-ttu-id="a9cb0-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a9cb0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hosted-graphite-from-the-gallery"></a><span data-ttu-id="a9cb0-123">從資源庫新增 Hosted Graphite</span><span class="sxs-lookup"><span data-stu-id="a9cb0-123">Adding Hosted Graphite from the gallery</span></span>
<span data-ttu-id="a9cb0-124">若要設定將 Hosted Graphite 整合到 Azure AD 中，您需要從資源庫將 Hosted Graphite 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-124">To configure the integration of Hosted Graphite into Azure AD, you need to add Hosted Graphite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a9cb0-125">**若要從資源庫新增 Hosted Graphite，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a9cb0-125">**To add Hosted Graphite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a9cb0-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a9cb0-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a9cb0-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="a9cb0-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="a9cb0-133">在搜尋方塊中，輸入 **Hosted Graphite**。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-133">In the search box, type **Hosted Graphite**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_search.png)

5. <span data-ttu-id="a9cb0-135">在結果窗格中，選取 [Hosted Graphite]，然後按一下 [新增] 按鈕來新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-135">In the results panel, select **Hosted Graphite**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a9cb0-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a9cb0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a9cb0-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Hosted Graphite 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-138">In this section, you configure and test Azure AD single sign-on with Hosted Graphite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a9cb0-139">若要讓單一登入能夠運作，Azure AD 必須知道 Hosted Graphite 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Hosted Graphite is to a user in Azure AD.</span></span> <span data-ttu-id="a9cb0-140">換句話說，必須在 Azure AD 使用者與 Hosted Graphite 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-140">In other words, a link relationship between an Azure AD user and the related user in Hosted Graphite needs to be established.</span></span>

<span data-ttu-id="a9cb0-141">在 Hosted Graphite 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-141">In Hosted Graphite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a9cb0-142">若要設定及測試與 Hosted Graphite 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="a9cb0-142">To configure and test Azure AD single sign-on with Hosted Graphite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a9cb0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a9cb0-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a9cb0-145">**[建立 Hosted Graphite 測試使用者](#creating-a-hosted-graphite-test-user)** - 在 Hosted Graphite 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-145">**[Creating a Hosted Graphite test user](#creating-a-hosted-graphite-test-user)** - to have a counterpart of Britta Simon in Hosted Graphite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a9cb0-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a9cb0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a9cb0-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a9cb0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a9cb0-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Hosted Graphite 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Hosted Graphite application.</span></span>

<span data-ttu-id="a9cb0-150">**若要設定與 Hosted Graphite 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a9cb0-150">**To configure Azure AD single sign-on with Hosted Graphite, perform the following steps:**</span></span>

1. <span data-ttu-id="a9cb0-151">在 Azure 入口網站的 [Hosted Graphite] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-151">In the Azure portal, on the **Hosted Graphite** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="a9cb0-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_samlbase.png)

3. <span data-ttu-id="a9cb0-155">如果您想要以「IDP 起始模式」設定應用程式，請在 [Hosted Graphite 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a9cb0-155">On the **Hosted Graphite Domain and URLs** section, if you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_url.png)

    <span data-ttu-id="a9cb0-157">a.</span><span class="sxs-lookup"><span data-stu-id="a9cb0-157">a.</span></span> <span data-ttu-id="a9cb0-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://www.hostedgraphite.com/metadata/<user id>`</span><span class="sxs-lookup"><span data-stu-id="a9cb0-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.hostedgraphite.com/metadata/<user id>`</span></span>

    <span data-ttu-id="a9cb0-159">b.</span><span class="sxs-lookup"><span data-stu-id="a9cb0-159">b.</span></span> <span data-ttu-id="a9cb0-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://www.hostedgraphite.com/complete/saml/<user id>`</span><span class="sxs-lookup"><span data-stu-id="a9cb0-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.hostedgraphite.com/complete/saml/<user id>`</span></span>

4. <span data-ttu-id="a9cb0-161">如果您想要以「SP 起始模式」設定應用程式，請在 [Hosted Graphite 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a9cb0-161">On the **Hosted Graphite Domain and URLs** section, if you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_10.png)
  
    <span data-ttu-id="a9cb0-163">a.</span><span class="sxs-lookup"><span data-stu-id="a9cb0-163">a.</span></span> <span data-ttu-id="a9cb0-164">按一下 [顯示進階 URL 設定] 選項</span><span class="sxs-lookup"><span data-stu-id="a9cb0-164">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="a9cb0-165">b.</span><span class="sxs-lookup"><span data-stu-id="a9cb0-165">b.</span></span> <span data-ttu-id="a9cb0-166">在 [登入 URL] 文字方塊中，以下列模式輸入 URL：`https://www.hostedgraphite.com/login/saml/<user id>/`</span><span class="sxs-lookup"><span data-stu-id="a9cb0-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://www.hostedgraphite.com/login/saml/<user id>/`</span></span>   

    > [!NOTE] 
    > <span data-ttu-id="a9cb0-167">請注意這些不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-167">Please note that these are not the real values.</span></span> <span data-ttu-id="a9cb0-168">您必須使用實際的「識別碼」、「回覆 URL」及「單一登入 URL」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-168">You have to update these values with the actual Identifier, Reply URL and Sign On URL.</span></span> <span data-ttu-id="a9cb0-169">若要取得這些值，您可以移至您應用程式端的 [存取] -> [SAML 設定]，或與 [Hosted Graphite 支援小組](mailto:help@hostedgraphite.com)連絡。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-169">To get these values, you can go to Access->SAML setup on your Application side or Contact [Hosted Graphite support team](mailto:help@hostedgraphite.com).</span></span>
    >
 
5. <span data-ttu-id="a9cb0-170">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-170">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_certificate.png) 

6. <span data-ttu-id="a9cb0-172">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-172">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="a9cb0-174">在 [Hosted Graphite 組態] 區段上，按一下 [設定 Hosted Graphite] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-174">On the **Hosted Graphite Configuration** section, click **Configure Hosted Graphite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a9cb0-175">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-175">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_configure.png) 

8. <span data-ttu-id="a9cb0-177">以系統管理員身分登入 Hosted Graphite 租用戶。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-177">Sign-on to your Hosted Graphite tenant as an administrator.</span></span>

9. <span data-ttu-id="a9cb0-178">移至資訊看板中的「SAML 設定頁面」 ([存取] -> [SAML 設定])。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-178">Go to the **SAML Setup page** in the sidebar (**Access -> SAML Setup**).</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_000.png)

10. <span data-ttu-id="a9cb0-180">確認這些 URL 與您在 Azure 入口網站的 [Hosted Graphite 網域與 URL] 區段上完成的設定相符合。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-180">Confirm these URls match your configuration done on the **Hosted Graphite Domain and URLs** section of the Azure portal.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_001.png)

11. <span data-ttu-id="a9cb0-182">在 [實體或簽發者識別碼] 和 [SSO 登入 URL]文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 和 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-182">In  **Entity or Issuer ID** and **SSO Login URL** textboxes, paste the value of **SAML Entity ID** and **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_002.png)
   

12. <span data-ttu-id="a9cb0-184">選取 [唯讀] 做為 [預設使用者角色]。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-184">Select "**Read-only**" as **Default User Role**.</span></span>
    
    ![在應用程式端設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_004.png)

13. <span data-ttu-id="a9cb0-186">在從 Azure 入口網站下載的記事本檔案中開啟您的 base-64 編碼憑證，將憑證的內容複製到剪貼簿，再貼到 [X.509 憑證] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
    
    ![在應用程式端設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_005.png)

14. <span data-ttu-id="a9cb0-188">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="a9cb0-189">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="a9cb0-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a9cb0-190">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a9cb0-191">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a9cb0-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a9cb0-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a9cb0-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="a9cb0-193">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="a9cb0-195">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a9cb0-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a9cb0-196">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a9cb0-198">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a9cb0-200">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a9cb0-202">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a9cb0-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a9cb0-204">a.</span><span class="sxs-lookup"><span data-stu-id="a9cb0-204">a.</span></span> <span data-ttu-id="a9cb0-205">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a9cb0-206">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-206">b.</span></span> <span data-ttu-id="a9cb0-207">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a9cb0-208">c.</span><span class="sxs-lookup"><span data-stu-id="a9cb0-208">c.</span></span> <span data-ttu-id="a9cb0-209">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a9cb0-210">d.</span><span class="sxs-lookup"><span data-stu-id="a9cb0-210">d.</span></span> <span data-ttu-id="a9cb0-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-211">Click **Create**.</span></span>
 
### <a name="creating-a-hosted-graphite-test-user"></a><span data-ttu-id="a9cb0-212">建立 Hosted Graphite 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a9cb0-212">Creating a Hosted Graphite test user</span></span>

<span data-ttu-id="a9cb0-213">本節的目標是要在 Hosted Graphite 中建立一個名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-213">The objective of this section is to create a user called Britta Simon in Hosted Graphite.</span></span> <span data-ttu-id="a9cb0-214">Hosted Graphite 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-214">Hosted Graphite supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="a9cb0-215">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-215">There is no action item for you in this section.</span></span> <span data-ttu-id="a9cb0-216">嘗試存取 Hosted Graphite 時，如果使用者還不存在，就會建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-216">A new user will be created during an attempt to access Hosted Graphite if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="a9cb0-217">如果您需要手動建立使用者，您需要透過 <mailto:help@hostedgraphite.com> 連絡 Hosted Graphite 支援小組。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-217">If you need to create a user manually, you need to contact the Hosted Graphite support team via <mailto:help@hostedgraphite.com>.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a9cb0-218">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a9cb0-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a9cb0-219">在本節中，您會將 Hosted Graphite 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Hosted Graphite.</span></span>

![指派使用者][200] 

<span data-ttu-id="a9cb0-221">**若要將 Britta Simon 指派給 Hosted Graphite，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a9cb0-221">**To assign Britta Simon to Hosted Graphite, perform the following steps:**</span></span>

1. <span data-ttu-id="a9cb0-222">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="a9cb0-224">在應用程式清單中，選取 [Hosted Graphite] 。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-224">In the applications list, select **Hosted Graphite**.</span></span>

    ![設定單一登入](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_app.png) 

3. <span data-ttu-id="a9cb0-226">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-226">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="a9cb0-228">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-228">Click **Add** button.</span></span> <span data-ttu-id="a9cb0-229">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="a9cb0-231">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a9cb0-232">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a9cb0-233">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a9cb0-234">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="a9cb0-234">Testing single sign-on</span></span>

<span data-ttu-id="a9cb0-235">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-235">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="a9cb0-236">當您在「存取面板」中按一下 [Hosted Graphite] 磚時，應該會自動登入您的 Hosted Graphite 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a9cb0-236">When you click the Hosted Graphite tile in the Access Panel, you should get automatically signed-on to your Hosted Graphite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a9cb0-237">其他資源</span><span class="sxs-lookup"><span data-stu-id="a9cb0-237">Additional resources</span></span>

* [<span data-ttu-id="a9cb0-238">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="a9cb0-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a9cb0-239">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a9cb0-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_203.png

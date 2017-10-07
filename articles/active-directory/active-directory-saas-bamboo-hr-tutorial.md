---
title: "教學課程：Azure Active Directory 與 BambooHR 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 BambooHR 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f826b5d2-9c64-47df-bbbf-0adf9eb0fa71
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: jeedes
ms.openlocfilehash: f9083f846beb3a4bf4cebbf18b42aba2dfef2472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bamboohr"></a><span data-ttu-id="42e32-103">教學課程：Azure Active Directory 與 BambooHR 整合</span><span class="sxs-lookup"><span data-stu-id="42e32-103">Tutorial: Azure Active Directory integration with BambooHR</span></span>

<span data-ttu-id="42e32-104">在此教學課程中，您學會如何 toointegrate BambooHR 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="42e32-104">In this tutorial, you learn how toointegrate BambooHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42e32-105">與 Azure AD 整合 BambooHR 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="42e32-105">Integrating BambooHR with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="42e32-106">您可以控制存取 tooBambooHR Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="42e32-106">You can control in Azure AD who has access tooBambooHR</span></span>
- <span data-ttu-id="42e32-107">您可以啟用您的使用者 tooautomatically get 登入 tooBambooHR （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="42e32-107">You can enable your users tooautomatically get signed-on tooBambooHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="42e32-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="42e32-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="42e32-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="42e32-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42e32-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="42e32-110">Prerequisites</span></span>

<span data-ttu-id="42e32-111">tooconfigure 與 BambooHR 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="42e32-111">tooconfigure Azure AD integration with BambooHR, you need hello following items:</span></span>

- <span data-ttu-id="42e32-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="42e32-112">An Azure AD subscription</span></span>
- <span data-ttu-id="42e32-113">已啟用 BambooHR 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="42e32-113">A BambooHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42e32-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="42e32-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42e32-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="42e32-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42e32-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="42e32-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="42e32-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="42e32-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42e32-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="42e32-118">Scenario description</span></span>
<span data-ttu-id="42e32-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="42e32-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42e32-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="42e32-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42e32-121">從 hello 圖庫加入 BambooHR</span><span class="sxs-lookup"><span data-stu-id="42e32-121">Adding BambooHR from hello gallery</span></span>
2. <span data-ttu-id="42e32-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="42e32-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bamboohr-from-hello-gallery"></a><span data-ttu-id="42e32-123">從 hello 圖庫加入 BambooHR</span><span class="sxs-lookup"><span data-stu-id="42e32-123">Adding BambooHR from hello gallery</span></span>
<span data-ttu-id="42e32-124">tooconfigure hello 整合 BambooHR 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd BambooHR。</span><span class="sxs-lookup"><span data-stu-id="42e32-124">tooconfigure hello integration of BambooHR into Azure AD, you need tooadd BambooHR from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="42e32-125">**tooadd BambooHR 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="42e32-125">**tooadd BambooHR from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="42e32-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="42e32-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="42e32-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="42e32-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="42e32-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="42e32-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="42e32-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="42e32-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="42e32-133">在 [hello] 搜尋方塊中，輸入**BambooHR**。</span><span class="sxs-lookup"><span data-stu-id="42e32-133">In hello search box, type **BambooHR**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_search.png)

5. <span data-ttu-id="42e32-135">在 hello 結果 窗格中，選取  **BambooHR**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="42e32-135">In hello results panel, select **BambooHR**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="42e32-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="42e32-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="42e32-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 BambooHR 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="42e32-138">In this section, you configure and test Azure AD single sign-on with BambooHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="42e32-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 BambooHR 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="42e32-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BambooHR is tooa user in Azure AD.</span></span> <span data-ttu-id="42e32-140">換句話說，Azure AD 使用者與 hello BambooHR 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="42e32-140">In other words, a link relationship between an Azure AD user and hello related user in BambooHR needs toobe established.</span></span>

<span data-ttu-id="42e32-141">在 BambooHR 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="42e32-141">In BambooHR, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="42e32-142">tooconfigure 及測試 Azure AD 單一登入 BambooHR，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="42e32-142">tooconfigure and test Azure AD single sign-on with BambooHR, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="42e32-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="42e32-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="42e32-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="42e32-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="42e32-145">**[建立測試使用者 BambooHR](#creating-a-bamboohr-test-user)**  -toohave 許 Simon BambooHR 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="42e32-145">**[Creating a BambooHR test user](#creating-a-bamboohr-test-user)** - toohave a counterpart of Britta Simon in BambooHR that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="42e32-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="42e32-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="42e32-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="42e32-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="42e32-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="42e32-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="42e32-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 BambooHR 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="42e32-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BambooHR application.</span></span>

<span data-ttu-id="42e32-150">**tooconfigure Azure AD 單一登入 BambooHR 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="42e32-150">**tooconfigure Azure AD single sign-on with BambooHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="42e32-151">在 Azure 入口網站上 hello hello **BambooHR**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="42e32-151">In hello Azure portal, on hello **BambooHR** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="42e32-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="42e32-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_samlbase.png)

3. <span data-ttu-id="42e32-155">在 hello **BambooHR 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="42e32-155">On hello **BambooHR Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_url.png)

    <span data-ttu-id="42e32-157">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company>.bamboohr.com`</span><span class="sxs-lookup"><span data-stu-id="42e32-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.bamboohr.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="42e32-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="42e32-158">This value is not real.</span></span> <span data-ttu-id="42e32-159">更新此值以 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="42e32-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="42e32-160">請連絡[BambooHR 用戶端支援小組](https://www.bamboohr.com/contact.php)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="42e32-160">Contact [BambooHR Client support team](https://www.bamboohr.com/contact.php) tooget this value.</span></span> 
 
4. <span data-ttu-id="42e32-161">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="42e32-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_certificate.png) 

5. <span data-ttu-id="42e32-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="42e32-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="42e32-165">在 hello **BambooHR 組態**區段中，按一下**設定 BambooHR** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="42e32-165">On hello **BambooHR Configuration** section, click **Configure BambooHR** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="42e32-166">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="42e32-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_configure.png) 

6. <span data-ttu-id="42e32-168">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 BambooHR 公司網站。</span><span class="sxs-lookup"><span data-stu-id="42e32-168">In a different web browser window, log into your BambooHR company site as an administrator.</span></span>

7. <span data-ttu-id="42e32-169">在 hello 首頁上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="42e32-169">On hello homepage, perform hello following steps:</span></span>
   
    <span data-ttu-id="42e32-170">![單一登入](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="42e32-170">![Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Single Sign-On")</span></span>   

    <span data-ttu-id="42e32-171">a.</span><span class="sxs-lookup"><span data-stu-id="42e32-171">a.</span></span> <span data-ttu-id="42e32-172">按一下 [應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="42e32-172">Click **Apps**.</span></span>
   
    <span data-ttu-id="42e32-173">b.</span><span class="sxs-lookup"><span data-stu-id="42e32-173">b.</span></span> <span data-ttu-id="42e32-174">在左側 hello hello 應用程式功能表中，按一下**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="42e32-174">In hello apps menu on hello left, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="42e32-175">c.</span><span class="sxs-lookup"><span data-stu-id="42e32-175">c.</span></span> <span data-ttu-id="42e32-176">按一下 [SAML 單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="42e32-176">Click **SAML Single Sign-On**.</span></span>

8. <span data-ttu-id="42e32-177">在 hello **SAML 單一登入**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="42e32-177">In hello **SAML Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="42e32-178">![SAML 單一登入](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML 單一登入")</span><span class="sxs-lookup"><span data-stu-id="42e32-178">![SAML Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML Single Sign-On")</span></span>
   
    <span data-ttu-id="42e32-179">a.</span><span class="sxs-lookup"><span data-stu-id="42e32-179">a.</span></span> <span data-ttu-id="42e32-180">貼上 hello **SAML 單一登入服務 URL**值傳入 hello **SSO 登入 Url**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="42e32-180">Paste hello **SAML Single Sign-On Service URL** value into hello **SSO Login Url** textbox.</span></span>
      
    <span data-ttu-id="42e32-181">b.</span><span class="sxs-lookup"><span data-stu-id="42e32-181">b.</span></span> <span data-ttu-id="42e32-182">開啟 base-64 編碼的憑證，從 [記事本]，複製到剪貼簿，其內容的 hello Azure 入口網站下載，然後將它貼入 toohello **X.509 憑證**文字方塊</span><span class="sxs-lookup"><span data-stu-id="42e32-182">Open base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>
   
    <span data-ttu-id="42e32-183">c.</span><span class="sxs-lookup"><span data-stu-id="42e32-183">c.</span></span> <span data-ttu-id="42e32-184">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="42e32-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="42e32-185">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="42e32-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="42e32-186">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="42e32-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="42e32-187">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="42e32-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="42e32-188">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="42e32-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="42e32-189">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="42e32-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="42e32-191">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="42e32-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="42e32-192">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="42e32-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="42e32-194">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="42e32-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="42e32-196">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="42e32-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="42e32-198">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="42e32-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="42e32-200">a.</span><span class="sxs-lookup"><span data-stu-id="42e32-200">a.</span></span> <span data-ttu-id="42e32-201">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="42e32-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42e32-202">b.</span><span class="sxs-lookup"><span data-stu-id="42e32-202">b.</span></span> <span data-ttu-id="42e32-203">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="42e32-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="42e32-204">c.</span><span class="sxs-lookup"><span data-stu-id="42e32-204">c.</span></span> <span data-ttu-id="42e32-205">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="42e32-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="42e32-206">d.</span><span class="sxs-lookup"><span data-stu-id="42e32-206">d.</span></span> <span data-ttu-id="42e32-207">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="42e32-207">Click **Create**.</span></span>
 
### <a name="creating-a-bamboohr-test-user"></a><span data-ttu-id="42e32-208">建立 BambooHR 測試使用者</span><span class="sxs-lookup"><span data-stu-id="42e32-208">Creating a BambooHR test user</span></span>

<span data-ttu-id="42e32-209">tooenable Azure AD 使用者 toolog 中 tooBambooHR，它們必須佈建到 BambooHR。</span><span class="sxs-lookup"><span data-stu-id="42e32-209">tooenable Azure AD users toolog in tooBambooHR, they must be provisioned into BambooHR.</span></span>  

<span data-ttu-id="42e32-210">在 BambooHR 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="42e32-210">In hello case of BambooHR, provisioning is a manual task.</span></span>

<span data-ttu-id="42e32-211">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="42e32-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="42e32-212">登入 tooyour **BambooHR**站台系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="42e32-212">Log in tooyour **BambooHR** site as administrator.</span></span>

2. <span data-ttu-id="42e32-213">在 hello hello 上方的工具列中按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="42e32-213">In hello toolbar on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="42e32-214">![設定](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "設定")</span><span class="sxs-lookup"><span data-stu-id="42e32-214">![Setting](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Setting")</span></span>

3. <span data-ttu-id="42e32-215">按一下 [概觀] 。</span><span class="sxs-lookup"><span data-stu-id="42e32-215">Click **Overview**.</span></span>

4. <span data-ttu-id="42e32-216">在 hello 左側瀏覽窗格中，移過**安全性\>使用者**。</span><span class="sxs-lookup"><span data-stu-id="42e32-216">In hello left navigation pane, go too**Security \> Users**.</span></span>

5. <span data-ttu-id="42e32-217">輸入 hello 的使用者名稱、 密碼和想成 hello tooprovision 之有效 AAD 帳戶的電子郵件地址相關的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="42e32-217">Type hello user name, password, and email address of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

6. <span data-ttu-id="42e32-218">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="42e32-218">Click **Save**.</span></span>
        
>[!NOTE]
><span data-ttu-id="42e32-219">您可以使用任何其他 BambooHR 使用者帳戶建立工具或 Api 提供 BambooHR tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="42e32-219">You can use any other BambooHR user account creation tools or APIs provided by BambooHR tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="42e32-220">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="42e32-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="42e32-221">在本節中，您可以授與存取 tooBambooHR 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="42e32-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBambooHR.</span></span>

![指派使用者][200] 

<span data-ttu-id="42e32-223">**tooassign 許 Simon tooBambooHR，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="42e32-223">**tooassign Britta Simon tooBambooHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="42e32-224">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="42e32-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="42e32-226">在 [hello] 應用程式清單中，選取**BambooHR**。</span><span class="sxs-lookup"><span data-stu-id="42e32-226">In hello applications list, select **BambooHR**.</span></span>

    ![設定單一登入](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_app.png) 

3. <span data-ttu-id="42e32-228">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="42e32-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="42e32-230">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="42e32-230">Click **Add** button.</span></span> <span data-ttu-id="42e32-231">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="42e32-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="42e32-233">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="42e32-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="42e32-234">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="42e32-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="42e32-235">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="42e32-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="42e32-236">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="42e32-236">Testing single sign-on</span></span>

<span data-ttu-id="42e32-237">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="42e32-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="42e32-238">當您按一下 hello BambooHR 磚 hello 存取面板中的時，您應該取得 tooyour 自動登入 BambooHR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="42e32-238">When you click hello BambooHR tile in hello Access Panel, you should get automatically signed-on tooyour BambooHR application.</span></span>
<span data-ttu-id="42e32-239">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="42e32-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="42e32-240">其他資源</span><span class="sxs-lookup"><span data-stu-id="42e32-240">Additional resources</span></span>

* [<span data-ttu-id="42e32-241">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42e32-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42e32-242">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="42e32-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_203.png


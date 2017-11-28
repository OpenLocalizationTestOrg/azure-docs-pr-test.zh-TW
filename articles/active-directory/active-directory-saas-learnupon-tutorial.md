---
title: "教學課程：Azure Active Directory 與 LearnUpon 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 LearnUpon 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: fdb9c62172327a539f0459c98aa20e63fa441e4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="190a4-103">教學課程：Azure Active Directory 與 LearnUpon 整合</span><span class="sxs-lookup"><span data-stu-id="190a4-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>

<span data-ttu-id="190a4-104">在此教學課程中，您學會如何 toointegrate LearnUpon 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="190a4-104">In this tutorial, you learn how toointegrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="190a4-105">與 Azure AD 整合 LearnUpon 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="190a4-105">Integrating LearnUpon with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="190a4-106">您可以控制存取 tooLearnUpon Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="190a4-106">You can control in Azure AD who has access tooLearnUpon</span></span>
- <span data-ttu-id="190a4-107">您可以啟用您的使用者 tooautomatically get 登入 tooLearnUpon （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="190a4-107">You can enable your users tooautomatically get signed-on tooLearnUpon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="190a4-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="190a4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="190a4-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="190a4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="190a4-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="190a4-110">Prerequisites</span></span>

<span data-ttu-id="190a4-111">tooconfigure LearnUpon 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="190a4-111">tooconfigure Azure AD integration with LearnUpon, you need hello following items:</span></span>

- <span data-ttu-id="190a4-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="190a4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="190a4-113">已啟用 LearnUpon 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="190a4-113">A LearnUpon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="190a4-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="190a4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="190a4-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="190a4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="190a4-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="190a4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="190a4-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="190a4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="190a4-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="190a4-118">Scenario description</span></span>
<span data-ttu-id="190a4-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="190a4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="190a4-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="190a4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="190a4-121">從 hello 圖庫加入 LearnUpon</span><span class="sxs-lookup"><span data-stu-id="190a4-121">Adding LearnUpon from hello gallery</span></span>
2. <span data-ttu-id="190a4-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="190a4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learnupon-from-hello-gallery"></a><span data-ttu-id="190a4-123">從 hello 圖庫加入 LearnUpon</span><span class="sxs-lookup"><span data-stu-id="190a4-123">Adding LearnUpon from hello gallery</span></span>
<span data-ttu-id="190a4-124">tooconfigure hello 整合 LearnUpon 到 Azure AD，您需要 tooadd LearnUpon hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="190a4-124">tooconfigure hello integration of LearnUpon into Azure AD, you need tooadd LearnUpon from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="190a4-125">**tooadd LearnUpon 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="190a4-125">**tooadd LearnUpon from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="190a4-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="190a4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="190a4-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="190a4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="190a4-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="190a4-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="190a4-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="190a4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="190a4-133">在 [hello] 搜尋方塊中，輸入**LearnUpon**。</span><span class="sxs-lookup"><span data-stu-id="190a4-133">In hello search box, type **LearnUpon**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. <span data-ttu-id="190a4-135">在 hello 結果 窗格中，選取  **LearnUpon**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="190a4-135">In hello results panel, select **LearnUpon**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="190a4-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="190a4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="190a4-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 LearnUpon 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="190a4-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="190a4-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 LearnUpon 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="190a4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LearnUpon is tooa user in Azure AD.</span></span> <span data-ttu-id="190a4-140">換句話說，Azure AD 使用者與 hello LearnUpon 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="190a4-140">In other words, a link relationship between an Azure AD user and hello related user in LearnUpon needs toobe established.</span></span>

<span data-ttu-id="190a4-141">LearnUpon 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="190a4-141">In LearnUpon, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="190a4-142">tooconfigure 及 LearnUpon 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="190a4-142">tooconfigure and test Azure AD single sign-on with LearnUpon, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="190a4-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="190a4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="190a4-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="190a4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="190a4-145">**[建立測試使用者 LearnUpon](#creating-a-learnupon-test-user)**  -toohave 許 Simon LearnUpon 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="190a4-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - toohave a counterpart of Britta Simon in LearnUpon that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="190a4-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="190a4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="190a4-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="190a4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="190a4-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="190a4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="190a4-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 LearnUpon 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="190a4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="190a4-150">**tooconfigure Azure AD 單一登入與 LearnUpon，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="190a4-150">**tooconfigure Azure AD single sign-on with LearnUpon, perform hello following steps:**</span></span>

1. <span data-ttu-id="190a4-151">在 Azure 入口網站上 hello hello **LearnUpon**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="190a4-151">In hello Azure portal, on hello **LearnUpon** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="190a4-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="190a4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. <span data-ttu-id="190a4-155">在 hello **LearnUpon 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="190a4-155">On hello **LearnUpon Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    <span data-ttu-id="190a4-157">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.learnupon.com/saml/consumer`</span><span class="sxs-lookup"><span data-stu-id="190a4-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="190a4-158">請注意，這不是 hello 真正的價值。</span><span class="sxs-lookup"><span data-stu-id="190a4-158">Please note that this is not hello real value.</span></span> <span data-ttu-id="190a4-159">您有 tooupdate 這個值與 hello 實際的回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="190a4-159">you have tooupdate this value with hello actual Reply URL.</span></span> <span data-ttu-id="190a4-160">請連絡 tooget 此值[LearnUpon 支援小組](https://www.learnupon.com/features/support/)。</span><span class="sxs-lookup"><span data-stu-id="190a4-160">tooget this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span>



4. <span data-ttu-id="190a4-161">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Raw)**然後儲存 hello 憑證檔案儲存在您的電腦。</span><span class="sxs-lookup"><span data-stu-id="190a4-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. <span data-ttu-id="190a4-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="190a4-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="190a4-165">在 hello **LearnUpon 組態**區段中，按一下**設定 LearnUpon** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="190a4-165">On hello **LearnUpon Configuration** section, click **Configure LearnUpon** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="190a4-166">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="190a4-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. <span data-ttu-id="190a4-168">開啟另一個瀏覽器執行個體，並使用系統管理員帳戶登入 LearnUpon。</span><span class="sxs-lookup"><span data-stu-id="190a4-168">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 

8. <span data-ttu-id="190a4-169">按一下 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="190a4-169">Click hello **settings** tab.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. <span data-ttu-id="190a4-171">按一下**單一登入的 SAML**，然後按一下**一般設定**tooconfigure SAML 設定。</span><span class="sxs-lookup"><span data-stu-id="190a4-171">Click **Single Sign On - SAML**, and then click **General Settings** tooconfigure SAML settings.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. <span data-ttu-id="190a4-173">在 hello**一般設定**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="190a4-173">In hello **General Settings** section, perform hello following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    <span data-ttu-id="190a4-175">a.</span><span class="sxs-lookup"><span data-stu-id="190a4-175">a.</span></span> <span data-ttu-id="190a4-176">選取 [啟用] 。</span><span class="sxs-lookup"><span data-stu-id="190a4-176">Select **Enabled**.</span></span>

    <span data-ttu-id="190a4-177">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="190a4-177">b.</span></span> <span data-ttu-id="190a4-178">對於 [版本] 選取 [2.0]。</span><span class="sxs-lookup"><span data-stu-id="190a4-178">Select **Version** as **2.0**.</span></span>

    <span data-ttu-id="190a4-179">c.</span><span class="sxs-lookup"><span data-stu-id="190a4-179">c.</span></span> <span data-ttu-id="190a4-180">對於 [略過條件] 選取 [否]。</span><span class="sxs-lookup"><span data-stu-id="190a4-180">Select **Skip conditions** as **No**.</span></span>

    <span data-ttu-id="190a4-181">d.</span><span class="sxs-lookup"><span data-stu-id="190a4-181">d.</span></span> <span data-ttu-id="190a4-182">在 hello **SAML 權杖張貼 name**文字方塊中，型別要求 post 參數 toohello SAML 取用者 URL 所指示項，其中包含驗證和驗證-例如 hello SAML 判斷提示 toobe hello 名稱**SAMLResponse**。</span><span class="sxs-lookup"><span data-stu-id="190a4-182">In hello **SAML Token Post param name** textbox, type hello name of request post parameter toohello SAML consumer URL indicated above that contains hello SAML Assertion toobe verified and authenticated - for example **SAMLResponse**.</span></span>

    <span data-ttu-id="190a4-183">e.</span><span class="sxs-lookup"><span data-stu-id="190a4-183">e.</span></span> <span data-ttu-id="190a4-184">在 hello**名稱識別碼格式**文字方塊中，型別 hello 值，指出在 SAML 判斷提示的 hello 使用者識別碼 （電子郵件地址） 所在的位置-例如**urn: oasis： 名稱： tc: saml: 1.1 nameid-format-格式：emailAddress**。</span><span class="sxs-lookup"><span data-stu-id="190a4-184">In hello **Name Identifier Format** textbox, type hello value that indicates where in your SAML Assertion hello users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  
    <span data-ttu-id="190a4-185">f.</span><span class="sxs-lookup"><span data-stu-id="190a4-185">f.</span></span> <span data-ttu-id="190a4-186">在 hello**識別提供者位置**文字方塊中，型別 hello 值，指出在 hello two tooif 按一下您上傳的圖示，從 Azure 入口網站的登入畫面上。</span><span class="sxs-lookup"><span data-stu-id="190a4-186">In hello **Identify Provider Location** textbox, type hello value that indicates where hello users are sent tooif they click on your uploaded icon from your Azure portal login screen.</span></span>
  
    <span data-ttu-id="190a4-187">g.</span><span class="sxs-lookup"><span data-stu-id="190a4-187">g.</span></span> <span data-ttu-id="190a4-188">在 hello**登出 URL**文字方塊中，貼上 hello**登出 URL**從 hello Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="190a4-188">In hello **Sign out URL** textbox, paste hello **Sign-Out URL** which you have copied from hello Azure portal.</span></span>
    
    <span data-ttu-id="190a4-189">h.</span><span class="sxs-lookup"><span data-stu-id="190a4-189">h.</span></span> <span data-ttu-id="190a4-190">按一下**管理手指沖印**，然後再上傳您下載的憑證的 hello 指紋。</span><span class="sxs-lookup"><span data-stu-id="190a4-190">Click **Manage finger prints**, and then upload hello finger print of your downloaded certificate.</span></span>

11. <span data-ttu-id="190a4-191">按一下**使用者設定**，然後執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="190a4-191">Click **User Settings**, and then perform hello following steps:</span></span>
   
     ![設定單一登入](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    <span data-ttu-id="190a4-193">a.</span><span class="sxs-lookup"><span data-stu-id="190a4-193">a.</span></span> <span data-ttu-id="190a4-194">在 hello**第一個名稱識別碼格式**文字方塊中，告訴我們在您的 SAML 判斷提示 hello 使用者 firstname 其中的型別 hello 值位於-例如： **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**。</span><span class="sxs-lookup"><span data-stu-id="190a4-194">In hello **First Name Identifier Format** textbox, type hello value that tells us where in your SAML Assertion hello users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
  
    <span data-ttu-id="190a4-195">b.</span><span class="sxs-lookup"><span data-stu-id="190a4-195">b.</span></span> <span data-ttu-id="190a4-196">在 hello**最後一個名稱識別碼格式**文字方塊中，告訴我們您的 SAML 判斷提示 hello 使用者 lastname 中其中的型別 hello 值位於-例如： **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**。</span><span class="sxs-lookup"><span data-stu-id="190a4-196">In hello **Last Name Identifier Format** textbox, type hello value that tells us where in your SAML Assertion hello users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

> [!TIP]
> <span data-ttu-id="190a4-197">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="190a4-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="190a4-198">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="190a4-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="190a4-199">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="190a4-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="190a4-200">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="190a4-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="190a4-201">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="190a4-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="190a4-203">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="190a4-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="190a4-204">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="190a4-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="190a4-206">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="190a4-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="190a4-208">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="190a4-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="190a4-210">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="190a4-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="190a4-212">a.</span><span class="sxs-lookup"><span data-stu-id="190a4-212">a.</span></span> <span data-ttu-id="190a4-213">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="190a4-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="190a4-214">b.</span><span class="sxs-lookup"><span data-stu-id="190a4-214">b.</span></span> <span data-ttu-id="190a4-215">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="190a4-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="190a4-216">c.</span><span class="sxs-lookup"><span data-stu-id="190a4-216">c.</span></span> <span data-ttu-id="190a4-217">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="190a4-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="190a4-218">d.</span><span class="sxs-lookup"><span data-stu-id="190a4-218">d.</span></span> <span data-ttu-id="190a4-219">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="190a4-219">Click **Create**.</span></span>
 
### <a name="creating-a-learnupon-test-user"></a><span data-ttu-id="190a4-220">建立 LearnUpon 測試使用者</span><span class="sxs-lookup"><span data-stu-id="190a4-220">Creating a LearnUpon test user</span></span>

<span data-ttu-id="190a4-221">hello 本節目標在於 toocreate LearnUpon 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="190a4-221">hello objective of this section is toocreate a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="190a4-222">LearnUpon 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="190a4-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="190a4-223">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="190a4-223">There is no action item for you in this section.</span></span> <span data-ttu-id="190a4-224">如果尚未存在，將會嘗試 tooaccess LearnUpon 期間建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="190a4-224">A new user will be created during an attempt tooaccess LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="190a4-225">[設定 Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)。</span><span class="sxs-lookup"><span data-stu-id="190a4-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="190a4-226">若要手動 toocreate 使用者，您需要 toocontact [LearnUpon 支援小組](https://www.learnupon.com/features/support/)。</span><span class="sxs-lookup"><span data-stu-id="190a4-226">If you need toocreate an user manually, you need toocontact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="190a4-227">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="190a4-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="190a4-228">在本節中，您可以授與存取 tooLearnUpon 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="190a4-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearnUpon.</span></span>

![指派使用者][200] 

<span data-ttu-id="190a4-230">**tooassign 許 Simon tooLearnUpon，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="190a4-230">**tooassign Britta Simon tooLearnUpon, perform hello following steps:**</span></span>

1. <span data-ttu-id="190a4-231">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="190a4-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="190a4-233">在 [hello] 應用程式清單中，選取**LearnUpon**。</span><span class="sxs-lookup"><span data-stu-id="190a4-233">In hello applications list, select **LearnUpon**.</span></span>

    ![設定單一登入](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. <span data-ttu-id="190a4-235">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="190a4-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="190a4-237">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="190a4-237">Click **Add** button.</span></span> <span data-ttu-id="190a4-238">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="190a4-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="190a4-240">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="190a4-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="190a4-241">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="190a4-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="190a4-242">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="190a4-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="190a4-243">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="190a4-243">Testing single sign-on</span></span>

<span data-ttu-id="190a4-244">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="190a4-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="190a4-245">當您按一下 hello LearnUpon 磚 hello 存取面板中的時，您應該取得自動登入 tooyour LearnUpon 應用程式。</span><span class="sxs-lookup"><span data-stu-id="190a4-245">When you click hello LearnUpon tile in hello Access Panel, you should get automatically signed-on tooyour LearnUpon application.</span></span>
<span data-ttu-id="190a4-246">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="190a4-246">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="190a4-247">其他資源</span><span class="sxs-lookup"><span data-stu-id="190a4-247">Additional resources</span></span>

* [<span data-ttu-id="190a4-248">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="190a4-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="190a4-249">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="190a4-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png


---
title: "教學課程：Azure Active Directory 與 PurelyHR 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 PurelyHR 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 86a9c454-596d-4902-829a-fe126708f739
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: bdc1748ed650cff36b1ef7d7330dd2a17b3bc760
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-purelyhr"></a><span data-ttu-id="a22ee-103">教學課程：Azure Active Directory 與 PurelyHR 整合</span><span class="sxs-lookup"><span data-stu-id="a22ee-103">Tutorial: Azure Active Directory integration with PurelyHR</span></span>

<span data-ttu-id="a22ee-104">在此教學課程中，您學會如何 toointegrate PurelyHR 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="a22ee-104">In this tutorial, you learn how toointegrate PurelyHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a22ee-105">與 Azure AD 整合 PurelyHR 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="a22ee-105">Integrating PurelyHR with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a22ee-106">您可以控制存取 tooPurelyHR Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="a22ee-106">You can control in Azure AD who has access tooPurelyHR</span></span>
- <span data-ttu-id="a22ee-107">您可以啟用您的使用者 tooautomatically get 登入 tooPurelyHR （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="a22ee-107">You can enable your users tooautomatically get signed-on tooPurelyHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a22ee-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a22ee-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a22ee-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a22ee-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a22ee-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a22ee-110">Prerequisites</span></span>

<span data-ttu-id="a22ee-111">tooconfigure PurelyHR 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="a22ee-111">tooconfigure Azure AD integration with PurelyHR, you need hello following items:</span></span>

- <span data-ttu-id="a22ee-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a22ee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a22ee-113">已啟用 PurelyHR 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a22ee-113">A PurelyHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a22ee-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="a22ee-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a22ee-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="a22ee-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a22ee-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a22ee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a22ee-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="a22ee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a22ee-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="a22ee-118">Scenario description</span></span>
<span data-ttu-id="a22ee-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a22ee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a22ee-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="a22ee-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a22ee-121">從 hello 圖庫加入 PurelyHR</span><span class="sxs-lookup"><span data-stu-id="a22ee-121">Adding PurelyHR from hello gallery</span></span>
2. <span data-ttu-id="a22ee-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a22ee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-purelyhr-from-hello-gallery"></a><span data-ttu-id="a22ee-123">從 hello 圖庫加入 PurelyHR</span><span class="sxs-lookup"><span data-stu-id="a22ee-123">Adding PurelyHR from hello gallery</span></span>
<span data-ttu-id="a22ee-124">tooconfigure hello 整合 PurelyHR 到 Azure AD，您需要 tooadd PurelyHR hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a22ee-124">tooconfigure hello integration of PurelyHR into Azure AD, you need tooadd PurelyHR from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a22ee-125">**tooadd PurelyHR 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a22ee-125">**tooadd PurelyHR from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a22ee-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a22ee-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a22ee-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a22ee-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a22ee-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a22ee-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="a22ee-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a22ee-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="a22ee-133">在 [hello] 搜尋方塊中，輸入**PurelyHR**。</span><span class="sxs-lookup"><span data-stu-id="a22ee-133">In hello search box, type **PurelyHR**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_search.png)

5. <span data-ttu-id="a22ee-135">在 hello 結果 窗格中，選取  **PurelyHR**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a22ee-135">In hello results panel, select **PurelyHR**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a22ee-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a22ee-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a22ee-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 PurelyHR 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a22ee-138">In this section, you configure and test Azure AD single sign-on with PurelyHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a22ee-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 PurelyHR 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="a22ee-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PurelyHR is tooa user in Azure AD.</span></span> <span data-ttu-id="a22ee-140">換句話說，Azure AD 使用者與 hello PurelyHR 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="a22ee-140">In other words, a link relationship between an Azure AD user and hello related user in PurelyHR needs toobe established.</span></span>

<span data-ttu-id="a22ee-141">PurelyHR 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="a22ee-141">In PurelyHR, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a22ee-142">tooconfigure 及 PurelyHR 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="a22ee-142">tooconfigure and test Azure AD single sign-on with PurelyHR, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a22ee-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="a22ee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a22ee-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="a22ee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a22ee-145">**[建立測試使用者 PurelyHR](#creating-a-purelyhr-test-user)**  -toohave 許 Simon PurelyHR 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="a22ee-145">**[Creating a PurelyHR test user](#creating-a-purelyhr-test-user)** - toohave a counterpart of Britta Simon in PurelyHR that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a22ee-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a22ee-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a22ee-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="a22ee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a22ee-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a22ee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a22ee-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 PurelyHR 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="a22ee-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PurelyHR application.</span></span>

<span data-ttu-id="a22ee-150">**tooconfigure Azure AD 單一登入與 PurelyHR，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a22ee-150">**tooconfigure Azure AD single sign-on with PurelyHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="a22ee-151">在 Azure 入口網站上 hello hello **PurelyHR**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="a22ee-151">In hello Azure portal, on hello **PurelyHR** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="a22ee-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a22ee-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_samlbase.png)

3. <span data-ttu-id="a22ee-155">在 hello **PurelyHR 網域和 Url**區段中，執行下列步驟，如果您想 tooconfigure hello 應用程式中的 hello **IDP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="a22ee-155">On hello **PurelyHR Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url.png)
   
    <span data-ttu-id="a22ee-157">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyID>.purelyhr.com/sso-consume`</span><span class="sxs-lookup"><span data-stu-id="a22ee-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyID>.purelyhr.com/sso-consume`</span></span>

4. <span data-ttu-id="a22ee-158">請檢查**顯示進階的 URL 設定**，如果您想 tooconfigure hello 應用程式中的**SP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="a22ee-158">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url1.png)
    
    <span data-ttu-id="a22ee-160">在 hello**登入 URL**文字方塊中，使用下列模式的 hello 類型 hello 值：`https://<companyID>.purelyhr.com/sso-initiate`</span><span class="sxs-lookup"><span data-stu-id="a22ee-160">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<companyID>.purelyhr.com/sso-initiate`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="a22ee-161">這些值不是真正的 hello。</span><span class="sxs-lookup"><span data-stu-id="a22ee-161">These values are not hello real.</span></span> <span data-ttu-id="a22ee-162">Hello 實際的回覆 URL 和登入 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="a22ee-162">Update these values with hello actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="a22ee-163">請連絡[PurelyHR 用戶端支援小組](http://support.purelyhr.com/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="a22ee-163">Contact [PurelyHR Client support team](http://support.purelyhr.com/) tooget these values.</span></span> 

5. <span data-ttu-id="a22ee-164">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="a22ee-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_certificate.png) 

6. <span data-ttu-id="a22ee-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a22ee-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-purelyhr-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="a22ee-168">在 hello **PurelyHR 組態**區段中，按一下**設定 PurelyHR** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="a22ee-168">On hello **PurelyHR Configuration** section, click **Configure PurelyHR** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a22ee-169">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="a22ee-169">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_configure.png) 

8. <span data-ttu-id="a22ee-171">tooconfigure 單一登入上**PurelyHR**側邊，以系統管理員身分登入 tootheir 網站。</span><span class="sxs-lookup"><span data-stu-id="a22ee-171">tooconfigure single sign-on on **PurelyHR** side, login tootheir website as an administrator.</span></span>

9. <span data-ttu-id="a22ee-172">開啟 hello**儀表板**hello 工具列，並按一下中的 hello 選項從**SSO 設定**。</span><span class="sxs-lookup"><span data-stu-id="a22ee-172">Open hello **Dashboard** from hello options in hello toolbar and click **SSO Settings**.</span></span>

10. <span data-ttu-id="a22ee-173">貼上的 hello 值為 hello 方塊中所述以下-</span><span class="sxs-lookup"><span data-stu-id="a22ee-173">Paste hello values in hello boxes as described below-</span></span>

    ![設定單一登入](./media/active-directory-saas-purelyhr-tutorial/purelyhr-dashboard-sso-settings.png)    

    <span data-ttu-id="a22ee-175">a.</span><span class="sxs-lookup"><span data-stu-id="a22ee-175">a.</span></span> <span data-ttu-id="a22ee-176">開啟 hello **Certificate(Bas64)** hello 從 [記事本] 和複製 hello 憑證值中的 Azure 入口網站的下載。</span><span class="sxs-lookup"><span data-stu-id="a22ee-176">Open hello **Certificate(Bas64)** downloaded from hello Azure portal in notepad and copy hello certificate value.</span></span> <span data-ttu-id="a22ee-177">貼上 hello 複製值到 hello **X.509 憑證**方塊。</span><span class="sxs-lookup"><span data-stu-id="a22ee-177">Paste hello copied value into hello **X.509 Certificate** box.</span></span>

    <span data-ttu-id="a22ee-178">b.</span><span class="sxs-lookup"><span data-stu-id="a22ee-178">b.</span></span> <span data-ttu-id="a22ee-179">在 hello **Idp 簽發者 URL**方塊中，貼上 hello **SAML 實體識別碼**從 hello Azure 入口網站複製。</span><span class="sxs-lookup"><span data-stu-id="a22ee-179">In hello **Idp Issuer URL** box, paste hello **SAML Entity ID** copied from hello Azure portal.</span></span>

    <span data-ttu-id="a22ee-180">c.</span><span class="sxs-lookup"><span data-stu-id="a22ee-180">c.</span></span> <span data-ttu-id="a22ee-181">在 hello **Idp 端點 URL**方塊中，貼上 hello **SAML 單一登入服務 URL**從 hello Azure 入口網站複製。</span><span class="sxs-lookup"><span data-stu-id="a22ee-181">In hello **Idp Endpoint URL** box, paste hello **SAML Single Sign-On Service URL** copied from hello Azure portal.</span></span> 

    <span data-ttu-id="a22ee-182">d.</span><span class="sxs-lookup"><span data-stu-id="a22ee-182">d.</span></span> <span data-ttu-id="a22ee-183">檢查 hello**自動建立使用者**核取方塊 tooenable 自動使用者佈建 PurelyHR 中。</span><span class="sxs-lookup"><span data-stu-id="a22ee-183">Check hello **Auto-Create Users** checkbox tooenable automatic user provisioning in PurelyHR.</span></span>

    <span data-ttu-id="a22ee-184">e.</span><span class="sxs-lookup"><span data-stu-id="a22ee-184">e.</span></span> <span data-ttu-id="a22ee-185">按一下**儲存變更**toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="a22ee-185">Click **Save Changes** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="a22ee-186">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="a22ee-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a22ee-187">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="a22ee-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a22ee-188">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a22ee-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a22ee-189">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a22ee-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="a22ee-190">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a22ee-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="a22ee-192">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a22ee-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a22ee-193">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a22ee-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a22ee-195">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="a22ee-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a22ee-197">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="a22ee-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a22ee-199">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a22ee-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a22ee-201">a.</span><span class="sxs-lookup"><span data-stu-id="a22ee-201">a.</span></span> <span data-ttu-id="a22ee-202">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="a22ee-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a22ee-203">b.</span><span class="sxs-lookup"><span data-stu-id="a22ee-203">b.</span></span> <span data-ttu-id="a22ee-204">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="a22ee-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a22ee-205">c.</span><span class="sxs-lookup"><span data-stu-id="a22ee-205">c.</span></span> <span data-ttu-id="a22ee-206">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="a22ee-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a22ee-207">d.</span><span class="sxs-lookup"><span data-stu-id="a22ee-207">d.</span></span> <span data-ttu-id="a22ee-208">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a22ee-208">Click **Create**.</span></span>
 
### <a name="creating-a-purelyhr-test-user"></a><span data-ttu-id="a22ee-209">建立 PurelyHR 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a22ee-209">Creating a PurelyHR test user</span></span>

<span data-ttu-id="a22ee-210">tooenable Azure AD 使用者 toolog 中 tooPurelyHR，它們必須佈建到 PurelyHR。</span><span class="sxs-lookup"><span data-stu-id="a22ee-210">tooenable Azure AD users toolog in tooPurelyHR, they must be provisioned into PurelyHR.</span></span> <span data-ttu-id="a22ee-211">在 PurelyHR 中，佈建是自動進行的工作，當自動使用者佈建功能啟用時，您不需要進行任何手動步驟。</span><span class="sxs-lookup"><span data-stu-id="a22ee-211">In PurelyHR, provisioning is an automatic task and no manual steps are required when automatic user provisioning is enabled.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a22ee-212">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="a22ee-212">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a22ee-213">在本節中，您可以授與存取 tooPurelyHR 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a22ee-213">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPurelyHR.</span></span>

![指派使用者][200] 

<span data-ttu-id="a22ee-215">**tooassign 許 Simon tooPurelyHR，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a22ee-215">**tooassign Britta Simon tooPurelyHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="a22ee-216">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a22ee-216">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="a22ee-218">在 [hello] 應用程式清單中，選取**PurelyHR**。</span><span class="sxs-lookup"><span data-stu-id="a22ee-218">In hello applications list, select **PurelyHR**.</span></span>

    ![設定單一登入](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_app.png) 

3. <span data-ttu-id="a22ee-220">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="a22ee-220">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="a22ee-222">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a22ee-222">Click **Add** button.</span></span> <span data-ttu-id="a22ee-223">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a22ee-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="a22ee-225">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="a22ee-225">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a22ee-226">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a22ee-226">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a22ee-227">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a22ee-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a22ee-228">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="a22ee-228">Testing single sign-on</span></span>

<span data-ttu-id="a22ee-229">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="a22ee-229">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a22ee-230">按一下吸收 LMS 磚 hello 存取面板中的 hello 取得自動登入 tooyour 吸收 LMS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a22ee-230">Click hello Absorb LMS tile in hello Access Panel, you get automatically signed-on tooyour Absorb LMS application.</span></span>

<span data-ttu-id="a22ee-231">如需 hello 存取面板的詳細資訊，請參閱。</span><span class="sxs-lookup"><span data-stu-id="a22ee-231">For more information about hello Access Panel, see.</span></span> <span data-ttu-id="a22ee-232">[簡介 toohello 存取面板](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="a22ee-232">[Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a22ee-233">其他資源</span><span class="sxs-lookup"><span data-stu-id="a22ee-233">Additional resources</span></span>

* [<span data-ttu-id="a22ee-234">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a22ee-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a22ee-235">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a22ee-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_203.png


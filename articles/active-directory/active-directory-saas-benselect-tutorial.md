---
title: "教學課程：Azure Active Directory 與 BenSelect 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 BenSelect 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: c3705da337bf8f6e76de58cd21c5b047c8f5e12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a><span data-ttu-id="b1058-103">教學課程：Azure Active Directory 與 BenSelect 整合</span><span class="sxs-lookup"><span data-stu-id="b1058-103">Tutorial: Azure Active Directory integration with BenSelect</span></span>

<span data-ttu-id="b1058-104">在此教學課程中，您學會如何 toointegrate BenSelect 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="b1058-104">In this tutorial, you learn how toointegrate BenSelect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b1058-105">與 Azure AD 整合 BenSelect 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="b1058-105">Integrating BenSelect with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b1058-106">您可以控制存取 tooBenSelect Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="b1058-106">You can control in Azure AD who has access tooBenSelect</span></span>
- <span data-ttu-id="b1058-107">您可以啟用您的使用者 tooautomatically get 登入 tooBenSelect （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="b1058-107">You can enable your users tooautomatically get signed-on tooBenSelect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b1058-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b1058-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b1058-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b1058-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1058-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b1058-110">Prerequisites</span></span>

<span data-ttu-id="b1058-111">tooconfigure BenSelect 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="b1058-111">tooconfigure Azure AD integration with BenSelect, you need hello following items:</span></span>

- <span data-ttu-id="b1058-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b1058-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b1058-113">已啟用 BenSelect 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b1058-113">A BenSelect single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b1058-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="b1058-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b1058-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="b1058-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b1058-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b1058-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b1058-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="b1058-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b1058-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="b1058-118">Scenario description</span></span>
<span data-ttu-id="b1058-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b1058-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b1058-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="b1058-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b1058-121">從 hello 圖庫加入 BenSelect</span><span class="sxs-lookup"><span data-stu-id="b1058-121">Adding BenSelect from hello gallery</span></span>
2. <span data-ttu-id="b1058-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b1058-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benselect-from-hello-gallery"></a><span data-ttu-id="b1058-123">從 hello 圖庫加入 BenSelect</span><span class="sxs-lookup"><span data-stu-id="b1058-123">Adding BenSelect from hello gallery</span></span>
<span data-ttu-id="b1058-124">tooconfigure hello 整合 BenSelect 到 Azure AD，您需要 tooadd BenSelect hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b1058-124">tooconfigure hello integration of BenSelect into Azure AD, you need tooadd BenSelect from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b1058-125">**tooadd BenSelect 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b1058-125">**tooadd BenSelect from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1058-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="b1058-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b1058-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b1058-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b1058-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b1058-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="b1058-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b1058-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="b1058-133">在 [hello] 搜尋方塊中，輸入**BenSelect**。</span><span class="sxs-lookup"><span data-stu-id="b1058-133">In hello search box, type **BenSelect**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_search.png)

5. <span data-ttu-id="b1058-135">在 hello 結果 窗格中，選取  **BenSelect**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b1058-135">In hello results panel, select **BenSelect**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b1058-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b1058-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b1058-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 BenSelect 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b1058-138">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b1058-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 BenSelect 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="b1058-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BenSelect is tooa user in Azure AD.</span></span> <span data-ttu-id="b1058-140">換句話說，Azure AD 使用者與 hello BenSelect 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="b1058-140">In other words, a link relationship between an Azure AD user and hello related user in BenSelect needs toobe established.</span></span>

<span data-ttu-id="b1058-141">BenSelect 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b1058-141">In BenSelect, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b1058-142">tooconfigure 及 BenSelect 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="b1058-142">tooconfigure and test Azure AD single sign-on with BenSelect, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b1058-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="b1058-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b1058-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="b1058-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b1058-145">**[建立測試使用者 BenSelect](#creating-a-benselect-test-user)**  -toohave 許 Simon BenSelect 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="b1058-145">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - toohave a counterpart of Britta Simon in BenSelect that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b1058-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b1058-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b1058-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="b1058-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b1058-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b1058-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b1058-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 BenSelect 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="b1058-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BenSelect application.</span></span>

<span data-ttu-id="b1058-150">**tooconfigure Azure AD 單一登入與 BenSelect，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b1058-150">**tooconfigure Azure AD single sign-on with BenSelect, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1058-151">在 Azure 入口網站上 hello hello **BenSelect**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="b1058-151">In hello Azure portal, on hello **BenSelect** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="b1058-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b1058-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_samlbase.png)

3. <span data-ttu-id="b1058-155">在 hello **BenSelect 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b1058-155">On hello **BenSelect Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_url.png)

    <span data-ttu-id="b1058-157">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="b1058-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b1058-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="b1058-158">This value is not real.</span></span> <span data-ttu-id="b1058-159">更新此值與 hello 實際的回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="b1058-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="b1058-160">請連絡[BenSelect 支援小組](mailto:support@selerix.com)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="b1058-160">Contact [BenSelect support team](mailto:support@selerix.com) tooget this value.</span></span>
 
4. <span data-ttu-id="b1058-161">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Raw)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="b1058-161">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_certificate.png) 

5. <span data-ttu-id="b1058-163">BenSelect 應用程式預期 hello SAML 判斷提示，以特定格式。</span><span class="sxs-lookup"><span data-stu-id="b1058-163">BenSelect application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="b1058-164">設定下列宣告為此應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="b1058-164">Configure hello following claims for this application.</span></span> <span data-ttu-id="b1058-165">您可以從 hello 管理這些屬性的 hello 值**使用者屬性**應用程式整合頁面上的一節。</span><span class="sxs-lookup"><span data-stu-id="b1058-165">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="b1058-166">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="b1058-166">hello following screenshot shows an example for this.</span></span>

    ![設定單一登入](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_06.png)

6. <span data-ttu-id="b1058-168">在 hello**使用者屬性**區段 hello**單一登入**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="b1058-168">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="b1058-169">a.</span><span class="sxs-lookup"><span data-stu-id="b1058-169">a.</span></span> <span data-ttu-id="b1058-170">在 hello**使用者識別碼**下拉式清單中選取**ExtractMailPrefix**。</span><span class="sxs-lookup"><span data-stu-id="b1058-170">In hello **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="b1058-171">b.</span><span class="sxs-lookup"><span data-stu-id="b1058-171">b.</span></span> <span data-ttu-id="b1058-172">在 hello**郵件**下拉式清單中選取**user.userprincipalname**。</span><span class="sxs-lookup"><span data-stu-id="b1058-172">In hello **Mail** dropdown list, select **user.userprincipalname**.</span></span>

7. <span data-ttu-id="b1058-173">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b1058-173">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-benselect-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b1058-175">在 hello **BenSelect 組態**區段中，按一下**設定 BenSelect** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="b1058-175">On hello **BenSelect Configuration** section, click **Configure BenSelect** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b1058-176">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="b1058-176">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_configure.png) 

9. <span data-ttu-id="b1058-178">tooconfigure 單一登入上**BenSelect**端，您需要下載 toosend hello **Certificate(Raw)**和**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**太[BenSelect 支援小組](mailto:support@selerix.com)。</span><span class="sxs-lookup"><span data-stu-id="b1058-178">tooconfigure single sign-on on **BenSelect** side, you need toosend hello downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[BenSelect support team](mailto:support@selerix.com).</span></span>

   >[!NOTE]
   ><span data-ttu-id="b1058-179">您需要此項整合需要 hello SHA256 演算法 （不支援 SHA1） 的 toomention hello 適當的伺服器，例如 app2101 tooset hello SSO 等。</span><span class="sxs-lookup"><span data-stu-id="b1058-179">You need toomention that this integration requires hello SHA256 algorithm (SHA1 is not supported) tooset hello SSO on hello appropriate server like app2101 etc.</span></span> 
   
> [!TIP]
> <span data-ttu-id="b1058-180">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="b1058-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b1058-181">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="b1058-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b1058-182">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b1058-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b1058-183">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b1058-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="b1058-184">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="b1058-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="b1058-186">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b1058-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1058-187">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="b1058-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-benselect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b1058-189">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="b1058-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-benselect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b1058-191">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="b1058-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-benselect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b1058-193">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b1058-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-benselect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b1058-195">a.</span><span class="sxs-lookup"><span data-stu-id="b1058-195">a.</span></span> <span data-ttu-id="b1058-196">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b1058-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b1058-197">b.</span><span class="sxs-lookup"><span data-stu-id="b1058-197">b.</span></span> <span data-ttu-id="b1058-198">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="b1058-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b1058-199">c.</span><span class="sxs-lookup"><span data-stu-id="b1058-199">c.</span></span> <span data-ttu-id="b1058-200">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="b1058-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b1058-201">d.</span><span class="sxs-lookup"><span data-stu-id="b1058-201">d.</span></span> <span data-ttu-id="b1058-202">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b1058-202">Click **Create**.</span></span>
 
### <a name="creating-a-benselect-test-user"></a><span data-ttu-id="b1058-203">建立 BenSelect 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b1058-203">Creating a BenSelect test user</span></span>

<span data-ttu-id="b1058-204">hello 本節目標在於 toocreate BenSelect 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="b1058-204">hello objective of this section is toocreate a user called Britta Simon in BenSelect.</span></span> <span data-ttu-id="b1058-205">使用[BenSelect 支援小組](mailto:support@selerix.com)tooadd hello hello BenSelect 帳戶的使用者。</span><span class="sxs-lookup"><span data-stu-id="b1058-205">Work with [BenSelect support team](mailto:support@selerix.com) tooadd hello users in hello BenSelect account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b1058-206">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="b1058-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b1058-207">在本節中，您可以授與存取 tooBenSelect 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b1058-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBenSelect.</span></span>

![指派使用者][200] 

<span data-ttu-id="b1058-209">**tooassign 許 Simon tooBenSelect，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b1058-209">**tooassign Britta Simon tooBenSelect, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1058-210">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b1058-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="b1058-212">在 [hello] 應用程式清單中，選取**BenSelect**。</span><span class="sxs-lookup"><span data-stu-id="b1058-212">In hello applications list, select **BenSelect**.</span></span>

    ![設定單一登入](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_app.png) 

3. <span data-ttu-id="b1058-214">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="b1058-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="b1058-216">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b1058-216">Click **Add** button.</span></span> <span data-ttu-id="b1058-217">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b1058-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="b1058-219">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="b1058-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b1058-220">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b1058-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b1058-221">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b1058-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b1058-222">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="b1058-222">Testing single sign-on</span></span>

<span data-ttu-id="b1058-223">本節中，您可以測試使用存取面板 hello Azure AD 的 SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="b1058-223">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="b1058-224">當您按一下 hello BenSelect 磚 hello 存取面板中的時，您應該取得自動登入 tooyour BenSelect 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b1058-224">When you click hello BenSelect tile in hello Access Panel, you should get automatically signed-on tooyour BenSelect application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b1058-225">其他資源</span><span class="sxs-lookup"><span data-stu-id="b1058-225">Additional resources</span></span>

* [<span data-ttu-id="b1058-226">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b1058-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b1058-227">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b1058-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_203.png


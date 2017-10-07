---
title: "教學課程：Azure Active Directory 與 BeeLine 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 BeeLine 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0726859d-1dac-44a0-810b-da56d89039ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 92f228d33980c21ad934185ab89d73795f7f69bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-beeline"></a><span data-ttu-id="bf3d5-103">教學課程：Azure Active Directory 與 BeeLine 整合</span><span class="sxs-lookup"><span data-stu-id="bf3d5-103">Tutorial: Azure Active Directory integration with BeeLine</span></span>

<span data-ttu-id="bf3d5-104">在此教學課程中，您學會如何 toointegrate BeeLine 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-104">In this tutorial, you learn how toointegrate BeeLine with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bf3d5-105">與 Azure AD 整合 BeeLine 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="bf3d5-105">Integrating BeeLine with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bf3d5-106">您可以控制存取 tooBeeLine Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="bf3d5-106">You can control in Azure AD who has access tooBeeLine</span></span>
- <span data-ttu-id="bf3d5-107">您可以啟用您的使用者 tooautomatically get 登入 tooBeeLine （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="bf3d5-107">You can enable your users tooautomatically get signed-on tooBeeLine (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bf3d5-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="bf3d5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bf3d5-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf3d5-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="bf3d5-110">Prerequisites</span></span>

<span data-ttu-id="bf3d5-111">tooconfigure BeeLine 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="bf3d5-111">tooconfigure Azure AD integration with BeeLine, you need hello following items:</span></span>

- <span data-ttu-id="bf3d5-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bf3d5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bf3d5-113">一個已啟用 BeeLine 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bf3d5-113">A BeeLine single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bf3d5-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bf3d5-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="bf3d5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bf3d5-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bf3d5-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bf3d5-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="bf3d5-118">Scenario description</span></span>
<span data-ttu-id="bf3d5-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bf3d5-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="bf3d5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bf3d5-121">從 hello 圖庫加入 BeeLine</span><span class="sxs-lookup"><span data-stu-id="bf3d5-121">Adding BeeLine from hello gallery</span></span>
2. <span data-ttu-id="bf3d5-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="bf3d5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-beeline-from-hello-gallery"></a><span data-ttu-id="bf3d5-123">從 hello 圖庫加入 BeeLine</span><span class="sxs-lookup"><span data-stu-id="bf3d5-123">Adding BeeLine from hello gallery</span></span>
<span data-ttu-id="bf3d5-124">tooconfigure hello 整合 BeeLine 到 Azure AD，您需要 tooadd BeeLine hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-124">tooconfigure hello integration of BeeLine into Azure AD, you need tooadd BeeLine from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bf3d5-125">**tooadd BeeLine 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="bf3d5-125">**tooadd BeeLine from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf3d5-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bf3d5-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bf3d5-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="bf3d5-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="bf3d5-133">在 [hello] 搜尋方塊中，輸入**BeeLine**。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-133">In hello search box, type **BeeLine**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_search.png)

5. <span data-ttu-id="bf3d5-135">在 [hello [結果] 窗格中，選取 [ **BeeLine**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-135">In hello results panel, select **BeeLine**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bf3d5-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="bf3d5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bf3d5-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 BeeLine 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-138">In this section, you configure and test Azure AD single sign-on with BeeLine based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bf3d5-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 BeeLine 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BeeLine is tooa user in Azure AD.</span></span> <span data-ttu-id="bf3d5-140">換句話說，Azure AD 使用者與 hello BeeLine 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-140">In other words, a link relationship between an Azure AD user and hello related user in BeeLine needs toobe established.</span></span>

<span data-ttu-id="bf3d5-141">BeeLine 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-141">In BeeLine, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bf3d5-142">tooconfigure 及 BeeLine 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="bf3d5-142">tooconfigure and test Azure AD single sign-on with BeeLine, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bf3d5-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bf3d5-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bf3d5-145">**[建立測試使用者 BeeLine](#creating-a-beeline-test-user) ** -toohave 許 Simon BeeLine 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-145">**[Creating a BeeLine test user](#creating-a-beeline-test-user)** - toohave a counterpart of Britta Simon in BeeLine that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bf3d5-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bf3d5-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bf3d5-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="bf3d5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bf3d5-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 BeeLine 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BeeLine application.</span></span>

<span data-ttu-id="bf3d5-150">**tooconfigure Azure AD 單一登入與 BeeLine，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="bf3d5-150">**tooconfigure Azure AD single sign-on with BeeLine, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf3d5-151">在 Azure 入口網站上 hello hello **BeeLine**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-151">In hello Azure portal, on hello **BeeLine** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="bf3d5-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_samlbase.png)

3. <span data-ttu-id="bf3d5-155">在 [hello **BeeLine 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="bf3d5-155">On hello **BeeLine Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_url.png)

    <span data-ttu-id="bf3d5-157">a.</span><span class="sxs-lookup"><span data-stu-id="bf3d5-157">a.</span></span> <span data-ttu-id="bf3d5-158">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://projects.beeline.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="bf3d5-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://projects.beeline.net/<instancename>`</span></span>

    <span data-ttu-id="bf3d5-159">b.</span><span class="sxs-lookup"><span data-stu-id="bf3d5-159">b.</span></span> <span data-ttu-id="bf3d5-160">在 [hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="bf3d5-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://projects.beeline.net/<instancename>/SSO_External.ashx`|
    | `https://projects.beeline.net/<companyname>/SSO_External.ashx` |

    > [!NOTE] 
    > <span data-ttu-id="bf3d5-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-161">These values are not real.</span></span> <span data-ttu-id="bf3d5-162">以 hello 實際的識別項和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="bf3d5-163">請連絡[BeeLine 支援小組](https://www.beeline.com/contact-us/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-163">Contact [BeeLine support team](https://www.beeline.com/contact-us/) tooget these values.</span></span>
 
4. <span data-ttu-id="bf3d5-164">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_certificate.png) 

5. <span data-ttu-id="bf3d5-166">Beeline 應用程式預期 hello SAML 判斷提示，以特定格式。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-166">Your Beeline application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="bf3d5-167">請使用[BeeLine 支援小組](https://www.beeline.com/contact-us/)第一個 tooidentify hello 正確的使用者識別碼會對應到 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-167">Please work with [BeeLine support team](https://www.beeline.com/contact-us/) first tooidentify hello correct user identifier which will be mapped into hello application.</span></span> <span data-ttu-id="bf3d5-168">還請考慮從 hello 指引[BeeLine 支援小組](https://www.beeline.com/contact-us/)hello 相關屬性的 toouse 想讓此對應。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-168">Also please take hello guidance from [BeeLine support team](https://www.beeline.com/contact-us/) about hello attribute which they want toouse for this mapping.</span></span> <span data-ttu-id="bf3d5-169">您可以管理 hello 這個屬性的值從 hello**使用者屬性**hello 應用程式] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-169">You can manage hello value of this attribute from hello **User Attributes** tab of hello application.</span></span> <span data-ttu-id="bf3d5-170">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-170">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="bf3d5-171">我們已在這裡對應 hello**使用者識別碼**宣告 hello **userprincipalname**屬性，每個成功的 SAML 提供唯一的使用者識別碼，將會在 hello 傳送的 toohello Beeline 應用程式回應。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-171">Here we have mapped hello **User Identifier** claim with hello **userprincipalname** attribute, which provides unique user ID, which will be sent toohello Beeline application in hello every successful SAML Response.</span></span>

    ![設定單一登入](./media/active-directory-saas-beeline-tutorial/tutorial_attribute.png)  

6. <span data-ttu-id="bf3d5-173">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-173">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-beeline-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="bf3d5-175">在 [hello **BeeLine 組態**區段中，按一下**設定 BeeLine** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-175">On hello **BeeLine Configuration** section, click **Configure BeeLine** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bf3d5-176">複製 hello**登出 URL**和**SAML 實體識別碼**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="bf3d5-176">Copy hello **Sign-Out URL** and **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_configure.png) 

8. <span data-ttu-id="bf3d5-178">tooconfigure 單一登入上**BeeLine**端，您需要下載 toosend hello**中繼資料 XML**和**SAML 實體識別碼**，**登出 URL**太[BeeLine 支援小組](https://www.beeline.com/contact-us/)。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-178">tooconfigure single sign-on on **BeeLine** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID**, **Sign-Out URL** too[BeeLine support team](https://www.beeline.com/contact-us/).</span></span>

> [!TIP]
> <span data-ttu-id="bf3d5-179">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="bf3d5-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bf3d5-180">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bf3d5-181">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bf3d5-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bf3d5-182">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="bf3d5-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="bf3d5-183">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="bf3d5-185">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="bf3d5-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf3d5-186">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-beeline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bf3d5-188">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-beeline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bf3d5-190">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-beeline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bf3d5-192">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="bf3d5-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-beeline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bf3d5-194">a.</span><span class="sxs-lookup"><span data-stu-id="bf3d5-194">a.</span></span> <span data-ttu-id="bf3d5-195">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bf3d5-196">b.</span><span class="sxs-lookup"><span data-stu-id="bf3d5-196">b.</span></span> <span data-ttu-id="bf3d5-197">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bf3d5-198">c.</span><span class="sxs-lookup"><span data-stu-id="bf3d5-198">c.</span></span> <span data-ttu-id="bf3d5-199">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bf3d5-200">d.</span><span class="sxs-lookup"><span data-stu-id="bf3d5-200">d.</span></span> <span data-ttu-id="bf3d5-201">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-201">Click **Create**.</span></span>
 
### <a name="creating-a-beeline-test-user"></a><span data-ttu-id="bf3d5-202">建立 BeeLine 測試使用者</span><span class="sxs-lookup"><span data-stu-id="bf3d5-202">Creating a BeeLine test user</span></span>

<span data-ttu-id="bf3d5-203">在本節中，您會在 Beeline 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-203">In this section, you create a user called Britta Simon in Beeline.</span></span> <span data-ttu-id="bf3d5-204">Beeline 應用程式需要所有的 hello 使用者 toobe hello 進行單一登入前的應用程式中，佈建。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-204">Beeline application needs all hello users toobe provisioned in hello application before doing Single Sign On.</span></span> <span data-ttu-id="bf3d5-205">因此請與 hello [BeeLine 支援小組](https://www.beeline.com/contact-us/)tooprovision hello 應用程式的所有這些使用者。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-205">So work with hello [BeeLine support team](https://www.beeline.com/contact-us/) tooprovision all these users into hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bf3d5-206">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="bf3d5-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bf3d5-207">在本節中，您可以授與存取 tooBeeLine 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBeeLine.</span></span>

![指派使用者][200] 

<span data-ttu-id="bf3d5-209">**tooassign 許 Simon tooBeeLine，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="bf3d5-209">**tooassign Britta Simon tooBeeLine, perform hello following steps:**</span></span>

1. <span data-ttu-id="bf3d5-210">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="bf3d5-212">在 [hello] 應用程式清單中，選取**BeeLine**。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-212">In hello applications list, select **BeeLine**.</span></span>

    ![設定單一登入](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_app.png) 

3. <span data-ttu-id="bf3d5-214">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="bf3d5-216">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-216">Click **Add** button.</span></span> <span data-ttu-id="bf3d5-217">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="bf3d5-219">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bf3d5-220">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bf3d5-221">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bf3d5-222">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="bf3d5-222">Testing single sign-on</span></span>

<span data-ttu-id="bf3d5-223">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-223">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="bf3d5-224">當您按一下 hello Beeline 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Beeline 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bf3d5-224">When you click hello Beeline tile in hello Access Panel, you should get automatically signed-on tooyour Beeline application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bf3d5-225">其他資源</span><span class="sxs-lookup"><span data-stu-id="bf3d5-225">Additional resources</span></span>

* [<span data-ttu-id="bf3d5-226">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bf3d5-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bf3d5-227">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="bf3d5-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_203.png


---
title: "教學課程：Azure Active Directory 與 Showpad 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Showpad 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48b6bee0-dbc5-4863-964d-75b25e517741
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2c8c306b4b94c368a93f92123d3abe9fe35167db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-showpad"></a><span data-ttu-id="63db8-103">教學課程：Azure Active Directory 與 Showpad 整合</span><span class="sxs-lookup"><span data-stu-id="63db8-103">Tutorial: Azure Active Directory integration with Showpad</span></span>

<span data-ttu-id="63db8-104">在此教學課程中，您學會如何 toointegrate Showpad 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="63db8-104">In this tutorial, you learn how toointegrate Showpad with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="63db8-105">與 Azure AD 整合 Showpad 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="63db8-105">Integrating Showpad with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="63db8-106">您可以控制存取 tooShowpad Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="63db8-106">You can control in Azure AD who has access tooShowpad</span></span>
- <span data-ttu-id="63db8-107">您可以啟用您的使用者 tooautomatically get 登入 tooShowpad （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="63db8-107">You can enable your users tooautomatically get signed-on tooShowpad (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="63db8-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="63db8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="63db8-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="63db8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63db8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="63db8-110">Prerequisites</span></span>

<span data-ttu-id="63db8-111">tooconfigure Showpad 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="63db8-111">tooconfigure Azure AD integration with Showpad, you need hello following items:</span></span>

- <span data-ttu-id="63db8-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="63db8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="63db8-113">已啟用 Showpad 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="63db8-113">A Showpad single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="63db8-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="63db8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="63db8-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="63db8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="63db8-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="63db8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="63db8-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="63db8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="63db8-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="63db8-118">Scenario description</span></span>
<span data-ttu-id="63db8-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="63db8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="63db8-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="63db8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="63db8-121">從 hello 圖庫加入 Showpad</span><span class="sxs-lookup"><span data-stu-id="63db8-121">Adding Showpad from hello gallery</span></span>
2. <span data-ttu-id="63db8-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="63db8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-showpad-from-hello-gallery"></a><span data-ttu-id="63db8-123">從 hello 圖庫加入 Showpad</span><span class="sxs-lookup"><span data-stu-id="63db8-123">Adding Showpad from hello gallery</span></span>

<span data-ttu-id="63db8-124">tooconfigure hello 整合 Showpad 到 Azure AD，您需要 tooadd Showpad hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="63db8-124">tooconfigure hello integration of Showpad into Azure AD, you need tooadd Showpad from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="63db8-125">**tooadd Showpad 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="63db8-125">**tooadd Showpad from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="63db8-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="63db8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="63db8-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="63db8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="63db8-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="63db8-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="63db8-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="63db8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="63db8-133">在 [hello] 搜尋方塊中，輸入**Showpad**。</span><span class="sxs-lookup"><span data-stu-id="63db8-133">In hello search box, type **Showpad**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_search.png)

5. <span data-ttu-id="63db8-135">在 hello 結果 窗格中，選取  **Showpad**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="63db8-135">In hello results panel, select **Showpad**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="63db8-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="63db8-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="63db8-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Showpad 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="63db8-138">In this section, you configure and test Azure AD single sign-on with Showpad based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="63db8-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Showpad 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="63db8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Showpad is tooa user in Azure AD.</span></span> <span data-ttu-id="63db8-140">換句話說，Azure AD 使用者與 hello Showpad 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="63db8-140">In other words, a link relationship between an Azure AD user and hello related user in Showpad needs toobe established.</span></span>

<span data-ttu-id="63db8-141">Showpad 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="63db8-141">In Showpad, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="63db8-142">tooconfigure 及 Showpad 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="63db8-142">tooconfigure and test Azure AD single sign-on with Showpad, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="63db8-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="63db8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="63db8-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="63db8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="63db8-145">**[建立測試使用者 Showpad](#creating-a-showpad-test-user)**  -toohave 許 Simon Showpad 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="63db8-145">**[Creating a Showpad test user](#creating-a-showpad-test-user)** - toohave a counterpart of Britta Simon in Showpad that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="63db8-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="63db8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="63db8-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="63db8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="63db8-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="63db8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="63db8-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Showpad 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="63db8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Showpad application.</span></span>

<span data-ttu-id="63db8-150">**tooconfigure Azure AD 單一登入與 Showpad，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="63db8-150">**tooconfigure Azure AD single sign-on with Showpad, perform hello following steps:**</span></span>

1. <span data-ttu-id="63db8-151">在 Azure 入口網站上 hello hello **Showpad**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="63db8-151">In hello Azure portal, on hello **Showpad** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="63db8-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="63db8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_samlbase.png)

3. <span data-ttu-id="63db8-155">在 hello **Showpad 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="63db8-155">On hello **Showpad Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_url.png)

    <span data-ttu-id="63db8-157">a.</span><span class="sxs-lookup"><span data-stu-id="63db8-157">a.</span></span> <span data-ttu-id="63db8-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<comapany-name>.showpad.biz/login`</span><span class="sxs-lookup"><span data-stu-id="63db8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<comapany-name>.showpad.biz/login`</span></span>

    <span data-ttu-id="63db8-159">b.</span><span class="sxs-lookup"><span data-stu-id="63db8-159">b.</span></span> <span data-ttu-id="63db8-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company-name>.showpad.biz`</span><span class="sxs-lookup"><span data-stu-id="63db8-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company-name>.showpad.biz`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="63db8-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="63db8-161">These values are not real.</span></span> <span data-ttu-id="63db8-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="63db8-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="63db8-163">請連絡[Showpad 支援小組](https://help.showpad.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="63db8-163">Contact [Showpad support team](https://help.showpad.com) tooget these values.</span></span> 
 


4. <span data-ttu-id="63db8-164">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="63db8-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_certificate.png) 

5. <span data-ttu-id="63db8-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="63db8-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-showpad-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="63db8-168">以系統管理員身分登入 tooyour Showpad 租用戶。</span><span class="sxs-lookup"><span data-stu-id="63db8-168">Sign-on tooyour Showpad tenant as an administrator.</span></span>

7. <span data-ttu-id="63db8-169">在 hello 最上層顯示 hello 功能表上，按一下 hello**設定**。</span><span class="sxs-lookup"><span data-stu-id="63db8-169">In hello menu on hello top, click hello **Settings**.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_001.png) 

8. <span data-ttu-id="63db8-171">瀏覽過"**單一登入**"和按一下"**啟用**。 」</span><span class="sxs-lookup"><span data-stu-id="63db8-171">Navigate too"**Single Sign-On**" and click "**Enable**."</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_002.png)

9. <span data-ttu-id="63db8-173">在 [hello**新增 SAML 2.0 服務**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="63db8-173">On hello **Add a SAML 2.0 Service** dialog, perform hello following steps:</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_003.png) 
   
    <span data-ttu-id="63db8-175">a.</span><span class="sxs-lookup"><span data-stu-id="63db8-175">a.</span></span> <span data-ttu-id="63db8-176">在 hello**名稱**文字方塊中，識別提供者類型 hello 名稱 (例如： 您的公司名稱)。</span><span class="sxs-lookup"><span data-stu-id="63db8-176">In hello **Name** textbox, type hello name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="63db8-177">b.</span><span class="sxs-lookup"><span data-stu-id="63db8-177">b.</span></span> <span data-ttu-id="63db8-178">對於 [中繼資料來源]，選取 [XML]。</span><span class="sxs-lookup"><span data-stu-id="63db8-178">As **Metadata Source**, select **XML**.</span></span>
   
    <span data-ttu-id="63db8-179">c.</span><span class="sxs-lookup"><span data-stu-id="63db8-179">c.</span></span> <span data-ttu-id="63db8-180">Hello 內容的中繼資料 XML 檔案，您已從 hello Azure 入口網站下載，請複製並貼到 hello**中繼資料 XML**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="63db8-180">Copy hello content of metadata XML file, which you have downloaded from hello Azure portal, and then paste it into hello **Metadata XML** textbox.</span></span>
   
    <span data-ttu-id="63db8-181">d.</span><span class="sxs-lookup"><span data-stu-id="63db8-181">d.</span></span> <span data-ttu-id="63db8-182">選取 [在新使用者登入時自動佈建帳戶]。</span><span class="sxs-lookup"><span data-stu-id="63db8-182">Select **Auto-provision accounts for new users when they log in**.</span></span>
   
    <span data-ttu-id="63db8-183">e.</span><span class="sxs-lookup"><span data-stu-id="63db8-183">e.</span></span> <span data-ttu-id="63db8-184">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="63db8-184">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="63db8-185">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="63db8-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="63db8-186">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="63db8-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="63db8-187">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="63db8-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="63db8-188">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="63db8-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="63db8-189">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="63db8-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="63db8-191">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="63db8-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="63db8-192">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="63db8-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-showpad-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="63db8-194">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="63db8-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-showpad-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="63db8-196">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="63db8-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-showpad-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="63db8-198">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="63db8-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-showpad-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="63db8-200">a.</span><span class="sxs-lookup"><span data-stu-id="63db8-200">a.</span></span> <span data-ttu-id="63db8-201">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="63db8-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="63db8-202">b.</span><span class="sxs-lookup"><span data-stu-id="63db8-202">b.</span></span> <span data-ttu-id="63db8-203">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="63db8-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="63db8-204">c.</span><span class="sxs-lookup"><span data-stu-id="63db8-204">c.</span></span> <span data-ttu-id="63db8-205">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="63db8-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="63db8-206">d.</span><span class="sxs-lookup"><span data-stu-id="63db8-206">d.</span></span> <span data-ttu-id="63db8-207">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="63db8-207">Click **Create**.</span></span>
 
### <a name="creating-a-showpad-test-user"></a><span data-ttu-id="63db8-208">建立 Showpad 測試使用者</span><span class="sxs-lookup"><span data-stu-id="63db8-208">Creating a Showpad test user</span></span>

<span data-ttu-id="63db8-209">hello 本節目標在於 toocreate Showpad 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="63db8-209">hello objective of this section is toocreate a user called Britta Simon in Showpad.</span></span> 

<span data-ttu-id="63db8-210">Showpad 支援 Just-in-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="63db8-210">Showpad supports just-in-time provisioning.</span></span> <span data-ttu-id="63db8-211">您已在 **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)**。</span><span class="sxs-lookup"><span data-stu-id="63db8-211">You have enabled provisioning in **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**.</span></span> 

<span data-ttu-id="63db8-212">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="63db8-212">There is no action item for you in this section.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="63db8-213">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="63db8-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="63db8-214">在本節中，您可以授與存取 tooShowpad 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="63db8-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooShowpad.</span></span>

![指派使用者][200] 

<span data-ttu-id="63db8-216">**tooassign 許 Simon tooShowpad，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="63db8-216">**tooassign Britta Simon tooShowpad, perform hello following steps:**</span></span>

1. <span data-ttu-id="63db8-217">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="63db8-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="63db8-219">在 [hello] 應用程式清單中，選取**Showpad**。</span><span class="sxs-lookup"><span data-stu-id="63db8-219">In hello applications list, select **Showpad**.</span></span>

    ![設定單一登入](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_app.png) 

3. <span data-ttu-id="63db8-221">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="63db8-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="63db8-223">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="63db8-223">Click **Add** button.</span></span> <span data-ttu-id="63db8-224">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="63db8-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="63db8-226">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="63db8-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="63db8-227">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="63db8-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="63db8-228">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="63db8-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="63db8-229">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="63db8-229">Testing single sign-on</span></span>

<span data-ttu-id="63db8-230">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="63db8-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="63db8-231">當您按一下 hello Showpad 磚 hello 存取面板中的時，您應該取得自動登入 tooShowpad 應用程式。</span><span class="sxs-lookup"><span data-stu-id="63db8-231">When you click hello Showpad tile in hello Access Panel, you should get automatically signed-on tooShowpad application.</span></span>
<span data-ttu-id="63db8-232">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="63db8-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="63db8-233">其他資源</span><span class="sxs-lookup"><span data-stu-id="63db8-233">Additional resources</span></span>

* [<span data-ttu-id="63db8-234">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="63db8-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="63db8-235">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="63db8-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_203.png


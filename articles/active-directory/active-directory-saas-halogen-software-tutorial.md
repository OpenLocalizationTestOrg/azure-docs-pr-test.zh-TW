---
title: "教學課程：Azure Active Directory 與 Halogen Software 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Halogen 軟體之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: bdb67de713771d6e306f287c4b13895f6336f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="51294-103">教學課程：Azure Active Directory 與 Halogen Software 整合</span><span class="sxs-lookup"><span data-stu-id="51294-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="51294-104">在此教學課程中，您學會如何 toointegrate Halogen 軟體與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="51294-104">In this tutorial, you learn how toointegrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="51294-105">與 Azure AD 整合 Halogen 軟體可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="51294-105">Integrating Halogen Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="51294-106">您可以控制存取 tooHalogen 軟體的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="51294-106">You can control in Azure AD who has access tooHalogen Software</span></span>
- <span data-ttu-id="51294-107">您可以啟用您的使用者 tooautomatically get 登入 tooHalogen （單一登入） 的軟體與他們的 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="51294-107">You can enable your users tooautomatically get signed-on tooHalogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="51294-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="51294-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="51294-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="51294-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51294-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="51294-110">Prerequisites</span></span>

<span data-ttu-id="51294-111">tooconfigure 與 Halogen Software 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="51294-111">tooconfigure Azure AD integration with Halogen Software, you need hello following items:</span></span>

- <span data-ttu-id="51294-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="51294-112">An Azure AD subscription</span></span>
- <span data-ttu-id="51294-113">已啟用 Halogen Software 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="51294-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="51294-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="51294-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="51294-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="51294-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="51294-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="51294-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="51294-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="51294-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="51294-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="51294-118">Scenario description</span></span>

<span data-ttu-id="51294-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="51294-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="51294-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="51294-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="51294-121">從 hello 圖庫加入 Halogen 軟體</span><span class="sxs-lookup"><span data-stu-id="51294-121">Adding Halogen Software from hello gallery</span></span>
2. <span data-ttu-id="51294-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="51294-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-hello-gallery"></a><span data-ttu-id="51294-123">從 hello 圖庫加入 Halogen 軟體</span><span class="sxs-lookup"><span data-stu-id="51294-123">Adding Halogen Software from hello gallery</span></span>

<span data-ttu-id="51294-124">tooconfigure hello 整合 Halogen 軟體到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Halogen 軟體。</span><span class="sxs-lookup"><span data-stu-id="51294-124">tooconfigure hello integration of Halogen Software into Azure AD, you need tooadd Halogen Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="51294-125">**tooadd Halogen 軟體從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="51294-125">**tooadd Halogen Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="51294-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="51294-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="51294-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="51294-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="51294-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="51294-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="51294-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="51294-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="51294-133">在 [hello] 搜尋方塊中，輸入**Halogen 軟體**。</span><span class="sxs-lookup"><span data-stu-id="51294-133">In hello search box, type **Halogen Software**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. <span data-ttu-id="51294-135">在 hello 結果 窗格中，選取  **Halogen 軟體**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="51294-135">In hello results panel, select **Halogen Software**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="51294-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="51294-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="51294-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Halogen Software 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="51294-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="51294-139">單一登入 toowork，Azure AD 需要 tooknow Halogen 軟體中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="51294-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halogen Software is tooa user in Azure AD.</span></span> <span data-ttu-id="51294-140">換句話說，Azure AD 使用者與 hello Halogen 軟體相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="51294-140">In other words, a link relationship between an Azure AD user and hello related user in Halogen Software needs toobe established.</span></span>

<span data-ttu-id="51294-141">Halogen 軟體中指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="51294-141">In Halogen Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="51294-142">tooconfigure 及測試 Azure AD 單一登入與 Halogen 軟體，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="51294-142">tooconfigure and test Azure AD single sign-on with Halogen Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="51294-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="51294-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="51294-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="51294-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="51294-145">**[建立 Halogen 軟體測試使用者](#creating-a-halogen-software-test-user)** -toohave 許 Simon Halogen 軟體連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="51294-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in Halogen Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="51294-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="51294-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="51294-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="51294-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="51294-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="51294-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="51294-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Halogen 軟體應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="51294-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="51294-150">**tooconfigure Azure AD 單一登入 Halogen 軟體，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="51294-150">**tooconfigure Azure AD single sign-on with Halogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="51294-151">在 Azure 入口網站上 hello hello **Halogen 軟體**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="51294-151">In hello Azure portal, on hello **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="51294-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="51294-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. <span data-ttu-id="51294-155">在 hello **Halogen 軟體網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="51294-155">On hello **Halogen Software Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="51294-157">a.</span><span class="sxs-lookup"><span data-stu-id="51294-157">a.</span></span> <span data-ttu-id="51294-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="51294-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="51294-159">b.</span><span class="sxs-lookup"><span data-stu-id="51294-159">b.</span></span> <span data-ttu-id="51294-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello: `https://global.halogensoftware.com/<companyname>`，`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="51294-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="51294-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="51294-161">These values are not real.</span></span> <span data-ttu-id="51294-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="51294-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="51294-163">請連絡[Halogen 軟體用戶端支援小組](https://support.halogensoftware.com/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="51294-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="51294-164">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="51294-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. <span data-ttu-id="51294-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="51294-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="51294-168">在不同的瀏覽器視窗中，登入 tooyour **Halogen 軟體**身為系統管理員應用程式。</span><span class="sxs-lookup"><span data-stu-id="51294-168">In a different browser window, sign-on tooyour **Halogen Software** application as an administrator.</span></span>

7. <span data-ttu-id="51294-169">按一下 hello**選項** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="51294-169">Click hello **Options** tab.</span></span> 
   
    ![何謂 Azure AD Connect][12]

8. <span data-ttu-id="51294-171">在 hello 左側瀏覽窗格中，按一下  **SAML 設定**。</span><span class="sxs-lookup"><span data-stu-id="51294-171">In hello left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![何謂 Azure AD Connect][13]

9. <span data-ttu-id="51294-173">在 hello **SAML 設定**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="51294-173">On hello **SAML Configuration** page, perform hello following steps:</span></span> 

    ![何謂 Azure AD Connect][14]

     <span data-ttu-id="51294-175">a.</span><span class="sxs-lookup"><span data-stu-id="51294-175">a.</span></span> <span data-ttu-id="51294-176">對於 [唯一識別碼]，選取 [NameID]。</span><span class="sxs-lookup"><span data-stu-id="51294-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="51294-177">b.</span><span class="sxs-lookup"><span data-stu-id="51294-177">b.</span></span> <span data-ttu-id="51294-178">對於 [唯一識別碼對應到]，選取 [Username]。</span><span class="sxs-lookup"><span data-stu-id="51294-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="51294-179">c.</span><span class="sxs-lookup"><span data-stu-id="51294-179">c.</span></span> <span data-ttu-id="51294-180">tooupload 您下載的中繼資料檔案中，按一下 **瀏覽**tooselect hello 檔案，然後**上傳檔案**。</span><span class="sxs-lookup"><span data-stu-id="51294-180">tooupload your downloaded metadata file, click **Browse** tooselect hello file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="51294-181">d.</span><span class="sxs-lookup"><span data-stu-id="51294-181">d.</span></span> <span data-ttu-id="51294-182">tootest hello 組態中，按一下 **執行測試**。</span><span class="sxs-lookup"><span data-stu-id="51294-182">tootest hello configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="51294-183">您需要 toowait hello 訊息 「*hello SAML 測試已完成。*請關閉此視窗。」訊息顯示。</span><span class="sxs-lookup"><span data-stu-id="51294-183">You need toowait for hello message "*hello SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="51294-184">然後，關閉 hello 開啟的瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="51294-184">Then, close hello opened browser window.</span></span> <span data-ttu-id="51294-185">hello**啟用 SAML**核取方塊才會啟用 hello 測試已完成。</span><span class="sxs-lookup"><span data-stu-id="51294-185">hello **Enable SAML** checkbox is only enabled if hello test has been completed.</span></span> 
     
     <span data-ttu-id="51294-186">e.</span><span class="sxs-lookup"><span data-stu-id="51294-186">e.</span></span> <span data-ttu-id="51294-187">選取 [啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="51294-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="51294-188">f.</span><span class="sxs-lookup"><span data-stu-id="51294-188">f.</span></span> <span data-ttu-id="51294-189">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="51294-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="51294-190">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="51294-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="51294-191">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="51294-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="51294-192">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="51294-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="51294-193">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="51294-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="51294-194">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="51294-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="51294-196">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="51294-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="51294-197">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="51294-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="51294-199">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="51294-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="51294-201">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="51294-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="51294-203">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="51294-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="51294-205">a.</span><span class="sxs-lookup"><span data-stu-id="51294-205">a.</span></span> <span data-ttu-id="51294-206">在 hello**名稱**文字方塊中，型別名稱做為**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="51294-206">In hello **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="51294-207">b.</span><span class="sxs-lookup"><span data-stu-id="51294-207">b.</span></span> <span data-ttu-id="51294-208">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="51294-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="51294-209">c.</span><span class="sxs-lookup"><span data-stu-id="51294-209">c.</span></span> <span data-ttu-id="51294-210">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="51294-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="51294-211">d.</span><span class="sxs-lookup"><span data-stu-id="51294-211">d.</span></span> <span data-ttu-id="51294-212">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="51294-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="51294-213">建立 Halogen Software 測試使用者</span><span class="sxs-lookup"><span data-stu-id="51294-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="51294-214">hello 本節目標在於 toocreate 呼叫許 Simon Halogen 軟體中的使用者。</span><span class="sxs-lookup"><span data-stu-id="51294-214">hello objective of this section is toocreate a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="51294-215">**toocreate 呼叫許 Simon Halogen 軟體中的使用者執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="51294-215">**toocreate a user called Britta Simon in Halogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="51294-216">登入 tooyour **Halogen 軟體**身為系統管理員應用程式。</span><span class="sxs-lookup"><span data-stu-id="51294-216">Sign on tooyour **Halogen Software** application as an administrator.</span></span>

2. <span data-ttu-id="51294-217">按一下 hello**使用者中心**索引標籤，然後再按一下**Create User**。</span><span class="sxs-lookup"><span data-stu-id="51294-217">Click hello **User Center** tab, and then click **Create User**.</span></span>
   
    ![何謂 Azure AD Connect][300]  

3. <span data-ttu-id="51294-219">在 hello**新使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="51294-219">On hello **New User** dialog page, perform hello following steps:</span></span>
   
    ![何謂 Azure AD Connect][301]

    <span data-ttu-id="51294-221">a.</span><span class="sxs-lookup"><span data-stu-id="51294-221">a.</span></span> <span data-ttu-id="51294-222">在 hello**名字**文字方塊中，型別第一個名稱類似的 hello 使用者**許**。</span><span class="sxs-lookup"><span data-stu-id="51294-222">In hello **First Name** textbox, type first name of hello user like **Britta**.</span></span>
    
    <span data-ttu-id="51294-223">b.</span><span class="sxs-lookup"><span data-stu-id="51294-223">b.</span></span> <span data-ttu-id="51294-224">在 hello**姓氏**文字方塊中，姓氏類似 hello 使用者類型**Simon**。</span><span class="sxs-lookup"><span data-stu-id="51294-224">In hello **Last Name** textbox, type last name of hello user like **Simon**.</span></span> 

    <span data-ttu-id="51294-225">c.</span><span class="sxs-lookup"><span data-stu-id="51294-225">c.</span></span> <span data-ttu-id="51294-226">在 hello **Username**文字方塊中，輸入**許 Simon**，hello 與 hello Azure 入口網站的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="51294-226">In hello **Username** textbox, type **Britta Simon**, hello user name as in hello Azure portal.</span></span>

    <span data-ttu-id="51294-227">d.</span><span class="sxs-lookup"><span data-stu-id="51294-227">d.</span></span> <span data-ttu-id="51294-228">在 hello**密碼**文字方塊中，輸入許的密碼。</span><span class="sxs-lookup"><span data-stu-id="51294-228">In hello **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="51294-229">e.</span><span class="sxs-lookup"><span data-stu-id="51294-229">e.</span></span> <span data-ttu-id="51294-230">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="51294-230">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="51294-231">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="51294-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="51294-232">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooHalogen 軟體。</span><span class="sxs-lookup"><span data-stu-id="51294-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHalogen Software.</span></span>

![指派使用者][200] 

<span data-ttu-id="51294-234">**tooassign 許 Simon tooHalogen 軟體，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="51294-234">**tooassign Britta Simon tooHalogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="51294-235">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="51294-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="51294-237">在 [hello] 應用程式清單中，選取**Halogen 軟體**。</span><span class="sxs-lookup"><span data-stu-id="51294-237">In hello applications list, select **Halogen Software**.</span></span>

    ![設定單一登入](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. <span data-ttu-id="51294-239">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="51294-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="51294-241">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="51294-241">Click **Add** button.</span></span> <span data-ttu-id="51294-242">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="51294-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="51294-244">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="51294-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="51294-245">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="51294-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="51294-246">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="51294-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="51294-247">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="51294-247">Testing single sign-on</span></span>

<span data-ttu-id="51294-248">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="51294-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="51294-249">當您按一下 hello Halogen 軟體磚 hello 存取面板中的時，您應該取得自動登入 tooyour Halogen 軟體應用程式。</span><span class="sxs-lookup"><span data-stu-id="51294-249">When you click hello Halogen Software tile in hello Access Panel, you should get automatically signed-on tooyour Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="51294-250">其他資源</span><span class="sxs-lookup"><span data-stu-id="51294-250">Additional resources</span></span>

* [<span data-ttu-id="51294-251">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="51294-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="51294-252">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="51294-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png

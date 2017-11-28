---
title: "教學課程：Azure Active Directory 與 Panopto 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Panopto 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 76b30e1cd2782bb5fba3d229378b8f82652b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a><span data-ttu-id="845a9-103">教學課程：Azure Active Directory 與 Panopto 整合</span><span class="sxs-lookup"><span data-stu-id="845a9-103">Tutorial: Azure Active Directory integration with Panopto</span></span>

<span data-ttu-id="845a9-104">在此教學課程中，您學會如何 toointegrate Panopto 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="845a9-104">In this tutorial, you learn how toointegrate Panopto with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="845a9-105">整合 Azure AD 與 Panopto 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="845a9-105">Integrating Panopto with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="845a9-106">您可以控制存取 tooPanopto Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="845a9-106">You can control in Azure AD who has access tooPanopto</span></span>
- <span data-ttu-id="845a9-107">您可以啟用您的使用者 tooautomatically get 登入 tooPanopto （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="845a9-107">You can enable your users tooautomatically get signed-on tooPanopto (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="845a9-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="845a9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="845a9-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="845a9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="845a9-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="845a9-110">Prerequisites</span></span>

<span data-ttu-id="845a9-111">tooconfigure Azure AD 與 Panopto 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="845a9-111">tooconfigure Azure AD integration with Panopto, you need hello following items:</span></span>

- <span data-ttu-id="845a9-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="845a9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="845a9-113">已啟用 Panopto 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="845a9-113">A Panopto single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="845a9-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="845a9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="845a9-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="845a9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="845a9-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="845a9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="845a9-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="845a9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="845a9-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="845a9-118">Scenario description</span></span>
<span data-ttu-id="845a9-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="845a9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="845a9-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="845a9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="845a9-121">從 hello 圖庫加入 Panopto</span><span class="sxs-lookup"><span data-stu-id="845a9-121">Adding Panopto from hello gallery</span></span>
2. <span data-ttu-id="845a9-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="845a9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panopto-from-hello-gallery"></a><span data-ttu-id="845a9-123">從 hello 圖庫加入 Panopto</span><span class="sxs-lookup"><span data-stu-id="845a9-123">Adding Panopto from hello gallery</span></span>
<span data-ttu-id="845a9-124">tooconfigure hello 整合 Panopto 的 Azure AD，您需要 tooadd Panopto hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="845a9-124">tooconfigure hello integration of Panopto into Azure AD, you need tooadd Panopto from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="845a9-125">**tooadd Panopto 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="845a9-125">**tooadd Panopto from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="845a9-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="845a9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="845a9-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="845a9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="845a9-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="845a9-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="845a9-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="845a9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="845a9-133">在 [hello] 搜尋方塊中，輸入**Panopto**。</span><span class="sxs-lookup"><span data-stu-id="845a9-133">In hello search box, type **Panopto**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_search.png)

5. <span data-ttu-id="845a9-135">在 hello 結果 窗格中，選取  **Panopto**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="845a9-135">In hello results panel, select **Panopto**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="845a9-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="845a9-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="845a9-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Panopto 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="845a9-138">In this section, you configure and test Azure AD single sign-on with Panopto based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="845a9-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Panopto 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="845a9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Panopto is tooa user in Azure AD.</span></span> <span data-ttu-id="845a9-140">換句話說，Azure AD 使用者與 Panopto 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="845a9-140">In other words, a link relationship between an Azure AD user and hello related user in Panopto needs toobe established.</span></span>

<span data-ttu-id="845a9-141">Panopto 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="845a9-141">In Panopto, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="845a9-142">tooconfigure 及 Azure AD 單一登入與 Panopto 的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="845a9-142">tooconfigure and test Azure AD single sign-on with Panopto, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="845a9-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="845a9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="845a9-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="845a9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="845a9-145">**[建立測試使用者 Panopto](#creating-a-panopto-test-user)**  -toohave 許 Simon Panopto 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="845a9-145">**[Creating a Panopto test user](#creating-a-panopto-test-user)** - toohave a counterpart of Britta Simon in Panopto that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="845a9-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="845a9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="845a9-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="845a9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="845a9-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="845a9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="845a9-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Panopto 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="845a9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Panopto application.</span></span>

<span data-ttu-id="845a9-150">**tooconfigure Azure AD 單一登入與 Panopto，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="845a9-150">**tooconfigure Azure AD single sign-on with Panopto, perform hello following steps:**</span></span>

1. <span data-ttu-id="845a9-151">在 Azure 入口網站上 hello hello **Panopto**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="845a9-151">In hello Azure portal, on hello **Panopto** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="845a9-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="845a9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_samlbase.png)

3. <span data-ttu-id="845a9-155">在 hello **Panopto 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="845a9-155">On hello **Panopto Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_url.png)

    <span data-ttu-id="845a9-157">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenant-name>.panopto.com`</span><span class="sxs-lookup"><span data-stu-id="845a9-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.panopto.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="845a9-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="845a9-158">This value is not real.</span></span> <span data-ttu-id="845a9-159">更新此值以 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="845a9-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="845a9-160">請連絡[Panopto 用戶端支援小組](mailto:support@panopto.com‎)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="845a9-160">Contact [Panopto Client support team](mailto:support@panopto.com‎) tooget this value.</span></span> 
 
4. <span data-ttu-id="845a9-161">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="845a9-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_certificate.png) 

5. <span data-ttu-id="845a9-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="845a9-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-panopto-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="845a9-165">在 hello **Panopto 組態**區段中，按一下**設定 Panopto** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="845a9-165">On hello **Panopto Configuration** section, click **Configure Panopto** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="845a9-166">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="845a9-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_configure.png) 

7. <span data-ttu-id="845a9-168">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour Panopto 公司網站。</span><span class="sxs-lookup"><span data-stu-id="845a9-168">In a different web browser window, log in tooyour Panopto company site as an administrator.</span></span>

8. <span data-ttu-id="845a9-169">在左側 hello hello 工具列中按一下**系統**，然後按一下**身分識別提供者**。</span><span class="sxs-lookup"><span data-stu-id="845a9-169">In hello toolbar on hello left, click **System**, and then click **Identity Providers**.</span></span>
   
   <span data-ttu-id="845a9-170">![系統](./media/active-directory-saas-panopto-tutorial/ic777670.png "系統")</span><span class="sxs-lookup"><span data-stu-id="845a9-170">![System](./media/active-directory-saas-panopto-tutorial/ic777670.png "System")</span></span>
9. <span data-ttu-id="845a9-171">按一下 [新增提供者] 。</span><span class="sxs-lookup"><span data-stu-id="845a9-171">Click **Add Provider**.</span></span>
   
   <span data-ttu-id="845a9-172">![身分識別提供者](./media/active-directory-saas-panopto-tutorial/ic777671.png "身分識別提供者")</span><span class="sxs-lookup"><span data-stu-id="845a9-172">![Identity Providers](./media/active-directory-saas-panopto-tutorial/ic777671.png "Identity Providers")</span></span>
   
10. <span data-ttu-id="845a9-173">在 hello SAML 提供者 區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="845a9-173">In hello SAML provider section, perform hello following steps:</span></span>
   
    <span data-ttu-id="845a9-174">![SaaS 設定](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS 設定")</span><span class="sxs-lookup"><span data-stu-id="845a9-174">![SaaS configuration](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS configuration")</span></span>
    
    <span data-ttu-id="845a9-175">a.</span><span class="sxs-lookup"><span data-stu-id="845a9-175">a.</span></span> <span data-ttu-id="845a9-176">從 hello**提供者類型**清單中，選取**SAML20**。</span><span class="sxs-lookup"><span data-stu-id="845a9-176">From hello **Provider Type** list, select **SAML20**.</span></span>    
    
    <span data-ttu-id="845a9-177">b.</span><span class="sxs-lookup"><span data-stu-id="845a9-177">b.</span></span> <span data-ttu-id="845a9-178">在 hello**執行個體名稱**文字方塊中，輸入 hello 執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="845a9-178">In hello **Instance Name** textbox, type a name for hello instance.</span></span>

    <span data-ttu-id="845a9-179">c.</span><span class="sxs-lookup"><span data-stu-id="845a9-179">c.</span></span> <span data-ttu-id="845a9-180">在 hello**好記的描述**文字方塊中，輸入好記的描述。</span><span class="sxs-lookup"><span data-stu-id="845a9-180">In hello **Friendly Description** textbox, type a friendly description.</span></span>
    
    <span data-ttu-id="845a9-181">d.</span><span class="sxs-lookup"><span data-stu-id="845a9-181">d.</span></span> <span data-ttu-id="845a9-182">在**Bounce Page Url**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="845a9-182">In **Bounce Page Url** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="845a9-183">e.</span><span class="sxs-lookup"><span data-stu-id="845a9-183">e.</span></span> <span data-ttu-id="845a9-184">在 hello**簽發者**文字方塊中，貼上 hello 值**SAML 實體識別碼**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="845a9-184">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="845a9-185">f.</span><span class="sxs-lookup"><span data-stu-id="845a9-185">f.</span></span> <span data-ttu-id="845a9-186">開啟 base-64 編碼的憑證，您已從 Azure 入口網站中，複製 hello tooyour 剪貼簿內容的下載，其中，然後將它貼入 toohello**公開金鑰**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="845a9-186">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy hello content of it in tooyour clipboard, and then paste it toohello **Public Key**  textbox.</span></span>

11. <span data-ttu-id="845a9-187">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="845a9-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="845a9-188">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="845a9-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="845a9-189">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="845a9-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="845a9-190">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="845a9-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="845a9-191">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="845a9-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="845a9-192">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="845a9-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="845a9-194">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="845a9-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="845a9-195">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="845a9-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-panopto-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="845a9-197">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="845a9-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-panopto-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="845a9-199">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="845a9-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-panopto-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="845a9-201">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="845a9-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-panopto-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="845a9-203">a.</span><span class="sxs-lookup"><span data-stu-id="845a9-203">a.</span></span> <span data-ttu-id="845a9-204">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="845a9-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="845a9-205">b.</span><span class="sxs-lookup"><span data-stu-id="845a9-205">b.</span></span> <span data-ttu-id="845a9-206">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="845a9-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="845a9-207">c.</span><span class="sxs-lookup"><span data-stu-id="845a9-207">c.</span></span> <span data-ttu-id="845a9-208">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="845a9-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="845a9-209">d.</span><span class="sxs-lookup"><span data-stu-id="845a9-209">d.</span></span> <span data-ttu-id="845a9-210">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="845a9-210">Click **Create**.</span></span>
 
### <a name="creating-a-panopto-test-user"></a><span data-ttu-id="845a9-211">建立 Panopto 測試使用者</span><span class="sxs-lookup"><span data-stu-id="845a9-211">Creating a Panopto test user</span></span>

<span data-ttu-id="845a9-212">不沒有您 tooconfigure 使用者佈建 tooPanopto 任何動作項目。</span><span class="sxs-lookup"><span data-stu-id="845a9-212">There is no action item for you tooconfigure user provisioning tooPanopto.</span></span>  
<span data-ttu-id="845a9-213">當指派的使用者嘗試 toolog tooPanopto 使用 hello 存取面板中的時，Panopto 會檢查 hello 使用者是否存在。</span><span class="sxs-lookup"><span data-stu-id="845a9-213">When an assigned user tries toolog in tooPanopto using hello access panel, Panopto checks whether hello user exists.</span></span>  

<span data-ttu-id="845a9-214">如果尚無可用的使用者帳戶，Panopto 會自動予以建立。</span><span class="sxs-lookup"><span data-stu-id="845a9-214">If there is no user account available yet, it is automatically created by Panopto.</span></span>

>[!NOTE]
><span data-ttu-id="845a9-215">您可以使用任何其他 Panopto 使用者帳戶建立工具或 Api 提供 Panopto tooprovision Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="845a9-215">You can use any other Panopto user account creation tools or APIs provided by Panopto tooprovision Azure AD user accounts.</span></span>
>
>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="845a9-216">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="845a9-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="845a9-217">在本節中，您可以授與存取 tooPanopto 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="845a9-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPanopto.</span></span>

![指派使用者][200] 

<span data-ttu-id="845a9-219">**tooassign 許 Simon tooPanopto，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="845a9-219">**tooassign Britta Simon tooPanopto, perform hello following steps:**</span></span>

1. <span data-ttu-id="845a9-220">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="845a9-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="845a9-222">在 [hello] 應用程式清單中，選取**Panopto**。</span><span class="sxs-lookup"><span data-stu-id="845a9-222">In hello applications list, select **Panopto**.</span></span>

    ![設定單一登入](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_app.png) 

3. <span data-ttu-id="845a9-224">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="845a9-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="845a9-226">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="845a9-226">Click **Add** button.</span></span> <span data-ttu-id="845a9-227">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="845a9-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="845a9-229">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="845a9-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="845a9-230">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="845a9-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="845a9-231">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="845a9-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="845a9-232">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="845a9-232">Testing single sign-on</span></span>

<span data-ttu-id="845a9-233">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="845a9-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="845a9-234">當您按一下 hello Panopto 磚 hello 存取面板中的時，您應該取得自動登入頁面的 Panopto 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="845a9-234">When you click hello Panopto tile in hello Access Panel, you should get automatically login page of Panopto application.</span></span>
<span data-ttu-id="845a9-235">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="845a9-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="845a9-236">其他資源</span><span class="sxs-lookup"><span data-stu-id="845a9-236">Additional resources</span></span>

* [<span data-ttu-id="845a9-237">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="845a9-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="845a9-238">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="845a9-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_203.png


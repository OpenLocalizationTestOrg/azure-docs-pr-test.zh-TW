---
title: "教學課程：將 Azure Active Directory 與 Datahug 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Datahug 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: 79ccb939c7a19720bcf696af141f747db00c8a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a><span data-ttu-id="acbfd-103">教學課程：Azure Active Directory 與 Datahug 整合</span><span class="sxs-lookup"><span data-stu-id="acbfd-103">Tutorial: Azure Active Directory integration with Datahug</span></span>

<span data-ttu-id="acbfd-104">在此教學課程中，您學會如何 toointegrate Datahug 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="acbfd-104">In this tutorial, you learn how toointegrate Datahug with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="acbfd-105">與 Azure AD 整合 Datahug 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="acbfd-105">Integrating Datahug with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="acbfd-106">您可以控制存取 tooDatahug Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="acbfd-106">You can control in Azure AD who has access tooDatahug</span></span>
- <span data-ttu-id="acbfd-107">您可以啟用您的使用者 tooautomatically get 登入 tooDatahug （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="acbfd-107">You can enable your users tooautomatically get signed-on tooDatahug (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="acbfd-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="acbfd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="acbfd-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱。</span><span class="sxs-lookup"><span data-stu-id="acbfd-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="acbfd-110">[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="acbfd-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acbfd-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="acbfd-111">Prerequisites</span></span>

<span data-ttu-id="acbfd-112">tooconfigure Datahug 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="acbfd-112">tooconfigure Azure AD integration with Datahug, you need hello following items:</span></span>

- <span data-ttu-id="acbfd-113">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="acbfd-113">An Azure AD subscription</span></span>
- <span data-ttu-id="acbfd-114">啟用 Datahug 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="acbfd-114">A Datahug single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="acbfd-115">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="acbfd-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="acbfd-116">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="acbfd-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="acbfd-117">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="acbfd-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="acbfd-118">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="acbfd-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="acbfd-119">案例描述</span><span class="sxs-lookup"><span data-stu-id="acbfd-119">Scenario description</span></span>
<span data-ttu-id="acbfd-120">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="acbfd-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="acbfd-121">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="acbfd-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="acbfd-122">從 hello 圖庫加入 Datahug</span><span class="sxs-lookup"><span data-stu-id="acbfd-122">Adding Datahug from hello gallery</span></span>
2. <span data-ttu-id="acbfd-123">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="acbfd-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-datahug-from-hello-gallery"></a><span data-ttu-id="acbfd-124">從 hello 圖庫加入 Datahug</span><span class="sxs-lookup"><span data-stu-id="acbfd-124">Adding Datahug from hello gallery</span></span>
<span data-ttu-id="acbfd-125">tooconfigure hello 整合 Datahug 到 Azure AD，您需要 tooadd Datahug hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="acbfd-125">tooconfigure hello integration of Datahug into Azure AD, you need tooadd Datahug from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="acbfd-126">**tooadd Datahug 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="acbfd-126">**tooadd Datahug from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="acbfd-127">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="acbfd-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="acbfd-129">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="acbfd-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="acbfd-130">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="acbfd-130">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="acbfd-132">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="acbfd-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="acbfd-134">在 [hello] 搜尋方塊中，輸入**Datahug**。</span><span class="sxs-lookup"><span data-stu-id="acbfd-134">In hello search box, type **Datahug**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. <span data-ttu-id="acbfd-136">在 hello 結果 窗格中，選取  **Datahug**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="acbfd-136">In hello results panel, select **Datahug**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="acbfd-138">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="acbfd-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="acbfd-139">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Datahug 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="acbfd-139">In this section, you configure and test Azure AD single sign-on with Datahug based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="acbfd-140">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Datahug 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="acbfd-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Datahug is tooa user in Azure AD.</span></span> <span data-ttu-id="acbfd-141">換句話說，Azure AD 使用者與 hello Datahug 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="acbfd-141">In other words, a link relationship between an Azure AD user and hello related user in Datahug needs toobe established.</span></span>

<span data-ttu-id="acbfd-142">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Datahug 中。</span><span class="sxs-lookup"><span data-stu-id="acbfd-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Datahug.</span></span>

<span data-ttu-id="acbfd-143">tooconfigure 及 Datahug 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="acbfd-143">tooconfigure and test Azure AD single sign-on with Datahug, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="acbfd-144">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="acbfd-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="acbfd-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="acbfd-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="acbfd-146">**[建立測試使用者 Datahug](#creating-a-datahug-test-user)**  -toohave 許 Simon Datahug 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="acbfd-146">**[Creating a Datahug test user](#creating-a-datahug-test-user)** - toohave a counterpart of Britta Simon in Datahug that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="acbfd-147">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="acbfd-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="acbfd-148">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="acbfd-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="acbfd-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="acbfd-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="acbfd-150">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Datahug 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="acbfd-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Datahug application.</span></span>

<span data-ttu-id="acbfd-151">**tooconfigure Azure AD 單一登入與 Datahug，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="acbfd-151">**tooconfigure Azure AD single sign-on with Datahug, perform hello following steps:**</span></span>

1. <span data-ttu-id="acbfd-152">在 Azure 入口網站上 hello hello **Datahug**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="acbfd-152">In hello Azure portal, on hello **Datahug** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="acbfd-154">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="acbfd-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. <span data-ttu-id="acbfd-156">在 hello **Datahug 網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**IDP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="acbfd-156">On hello **Datahug Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    <span data-ttu-id="acbfd-158">a.</span><span class="sxs-lookup"><span data-stu-id="acbfd-158">a.</span></span> <span data-ttu-id="acbfd-159">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://apps.datahug.com/identity/<uniqueID>`</span><span class="sxs-lookup"><span data-stu-id="acbfd-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://apps.datahug.com/identity/<uniqueID>`</span></span>

    <span data-ttu-id="acbfd-160">b.</span><span class="sxs-lookup"><span data-stu-id="acbfd-160">b.</span></span> <span data-ttu-id="acbfd-161">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://apps.datahug.com/identity/<uniqueID>/acs`</span><span class="sxs-lookup"><span data-stu-id="acbfd-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://apps.datahug.com/identity/<uniqueID>/acs`</span></span>

4. <span data-ttu-id="acbfd-162">按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="acbfd-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="acbfd-163">如果您想 tooconfigure hello 應用程式中的**SP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="acbfd-163">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    <span data-ttu-id="acbfd-165">在 hello**登入 URL**文字方塊中，輸入與 URL:`https://apps.datahug.com/`</span><span class="sxs-lookup"><span data-stu-id="acbfd-165">In hello **Sign-on URL** textbox, type a URL as: `https://apps.datahug.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="acbfd-166">這些值不是真正的 hello。</span><span class="sxs-lookup"><span data-stu-id="acbfd-166">These values are not hello real.</span></span> <span data-ttu-id="acbfd-167">以 hello 實際的識別項和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="acbfd-167">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="acbfd-168">這裡我們建議您 toouse hello 唯一字串的值在 hello 識別碼和回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="acbfd-168">Here we suggest you toouse hello unique value of string in hello Identifier and Reply URL.</span></span> <span data-ttu-id="acbfd-169">請連絡[Datahug 用戶端支援小組](http://datahug.com/about/contact-us/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="acbfd-169">Contact [Datahug Client support team](http://datahug.com/about/contact-us/) tooget these values.</span></span> 

5. <span data-ttu-id="acbfd-170">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="acbfd-170">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  <span data-ttu-id="acbfd-172">請檢查**「 顯示進階憑證簽署設定 」**並執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="acbfd-172">Check **“Show advanced certificate signing settings”** and perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    <span data-ttu-id="acbfd-174">a.</span><span class="sxs-lookup"><span data-stu-id="acbfd-174">a.</span></span> <span data-ttu-id="acbfd-175">在 [簽署選項] 中，選取 [簽署 SAML 判斷提示]。</span><span class="sxs-lookup"><span data-stu-id="acbfd-175">In **Signing Option**, select **Sign SAML assertion**.</span></span>
    
    <span data-ttu-id="acbfd-176">b.</span><span class="sxs-lookup"><span data-stu-id="acbfd-176">b.</span></span> <span data-ttu-id="acbfd-177">在 [簽署演算法] 中，選取 [SHA1]。</span><span class="sxs-lookup"><span data-stu-id="acbfd-177">In **Signing algorithm**, select **SHA1**.</span></span>
 
7. <span data-ttu-id="acbfd-178">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="acbfd-178">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="acbfd-180">在 hello **Datahug 組態**區段中，按一下**設定 Datahug** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="acbfd-180">On hello **Datahug Configuration** section, click **Configure Datahug** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="acbfd-181">複製 hello **SAML 實體識別碼**和**SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="acbfd-181">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. <span data-ttu-id="acbfd-183">tooconfigure 單一登入上**Datahug**端，您需要下載 toosend hello**中繼資料 XML**， **SAML 實體識別碼**和**SAML 單一登入服務URL**太[Datahug 支援](http://datahug.com/about/contact-us/)。</span><span class="sxs-lookup"><span data-stu-id="acbfd-183">tooconfigure single sign-on on **Datahug** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** too[Datahug support](http://datahug.com/about/contact-us/).</span></span> <span data-ttu-id="acbfd-184">這些設定 toohave hello SAML SSO 連線兩端上正確設定此應用程式。</span><span class="sxs-lookup"><span data-stu-id="acbfd-184">They set this application up toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="acbfd-185">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="acbfd-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="acbfd-186">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="acbfd-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="acbfd-187">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="acbfd-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="acbfd-188">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="acbfd-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="acbfd-189">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="acbfd-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="acbfd-191">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="acbfd-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="acbfd-192">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="acbfd-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="acbfd-194">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="acbfd-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="acbfd-196">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="acbfd-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="acbfd-198">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="acbfd-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="acbfd-200">a.</span><span class="sxs-lookup"><span data-stu-id="acbfd-200">a.</span></span> <span data-ttu-id="acbfd-201">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="acbfd-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="acbfd-202">b.</span><span class="sxs-lookup"><span data-stu-id="acbfd-202">b.</span></span> <span data-ttu-id="acbfd-203">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="acbfd-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="acbfd-204">c.</span><span class="sxs-lookup"><span data-stu-id="acbfd-204">c.</span></span> <span data-ttu-id="acbfd-205">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="acbfd-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="acbfd-206">d.</span><span class="sxs-lookup"><span data-stu-id="acbfd-206">d.</span></span> <span data-ttu-id="acbfd-207">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="acbfd-207">Click **Create**.</span></span>
 
### <a name="creating-a-datahug-test-user"></a><span data-ttu-id="acbfd-208">建立 Datahug 測試使用者</span><span class="sxs-lookup"><span data-stu-id="acbfd-208">Creating a Datahug test user</span></span>

<span data-ttu-id="acbfd-209">tooenable Azure AD 使用者 toolog 中 tooDatahug，它們必須佈建到 Datahug。</span><span class="sxs-lookup"><span data-stu-id="acbfd-209">tooenable Azure AD users toolog in tooDatahug, they must be provisioned into Datahug.</span></span>  
<span data-ttu-id="acbfd-210">在 Datahug 時，佈建是手動工作。</span><span class="sxs-lookup"><span data-stu-id="acbfd-210">When Datahug, provisioning is a manual task.</span></span>

<span data-ttu-id="acbfd-211">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="acbfd-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="acbfd-212">登入 tooyour Datahug 公司網站的系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="acbfd-212">Log in tooyour Datahug company site as an administrator.</span></span>

2. <span data-ttu-id="acbfd-213">將滑鼠停留在 hello**齒輪**中 hello 右上角按一下**設定**</span><span class="sxs-lookup"><span data-stu-id="acbfd-213">Hover over hello **cog** in hello top right-hand corner and click **Settings**</span></span>
   
   ![新增員工](./media/active-directory-saas-datahug-tutorial/1.png)

3. <span data-ttu-id="acbfd-215">選擇**人員**按一下 hello**新增使用者** 索引標籤</span><span class="sxs-lookup"><span data-stu-id="acbfd-215">Choose **People** and click hello **Add Users** tab</span></span>

    ![新增員工](./media/active-directory-saas-datahug-tutorial/2.png)

4. <span data-ttu-id="acbfd-217">輸入您想要的 hello 人員 hello 電子郵件帳戶的 toocreate 按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="acbfd-217">Type hello email of hello person you would like toocreate an account for and click **Add**.</span></span>

    ![新增員工](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > <span data-ttu-id="acbfd-219">您可以透過選取傳送註冊郵件 toouser**傳送歡迎電子郵件**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="acbfd-219">You can send registration mail toouser by selecting **Send welcome email** checkbox.</span></span>  
    > <span data-ttu-id="acbfd-220">如果您要建立的 Salesforce 帳戶不會傳送 hello 歡迎電子郵件。</span><span class="sxs-lookup"><span data-stu-id="acbfd-220">If you are creating an account for Salesforce do not send hello welcome email.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="acbfd-221">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="acbfd-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="acbfd-222">在本節中，您可以授與存取 tooDatahug 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="acbfd-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDatahug.</span></span>

![指派使用者][200] 

<span data-ttu-id="acbfd-224">**tooassign 許 Simon tooDatahug，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="acbfd-224">**tooassign Britta Simon tooDatahug, perform hello following steps:**</span></span>

1. <span data-ttu-id="acbfd-225">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="acbfd-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="acbfd-227">在 [hello] 應用程式清單中，選取**Datahug**。</span><span class="sxs-lookup"><span data-stu-id="acbfd-227">In hello applications list, select **Datahug**.</span></span>

    ![設定單一登入](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. <span data-ttu-id="acbfd-229">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="acbfd-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="acbfd-231">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="acbfd-231">Click **Add** button.</span></span> <span data-ttu-id="acbfd-232">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="acbfd-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="acbfd-234">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="acbfd-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="acbfd-235">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="acbfd-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="acbfd-236">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="acbfd-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="acbfd-237">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="acbfd-237">Testing single sign-on</span></span>

<span data-ttu-id="acbfd-238">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="acbfd-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="acbfd-239">當您按一下 hello Datahug 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Datahug 應用程式。</span><span class="sxs-lookup"><span data-stu-id="acbfd-239">When you click hello Datahug tile in hello Access Panel, you should get automatically signed-on tooyour Datahug application.</span></span> <span data-ttu-id="acbfd-240">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="acbfd-240">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="acbfd-241">其他資源</span><span class="sxs-lookup"><span data-stu-id="acbfd-241">Additional resources</span></span>

* [<span data-ttu-id="acbfd-242">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="acbfd-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="acbfd-243">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="acbfd-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png


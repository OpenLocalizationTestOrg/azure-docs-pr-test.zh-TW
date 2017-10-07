---
title: "教學課程：Azure Active Directory 與 eDigitalResearch 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 eDigitalResearch 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c6b66ea0-16ba-45b4-b550-e81c56262b1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 6dd3cafb25ef8ede3a4c16902ed8da69cb7b715f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-edigitalresearch"></a><span data-ttu-id="72647-103">教學課程：Azure Active Directory 與 eDigitalResearch 整合</span><span class="sxs-lookup"><span data-stu-id="72647-103">Tutorial: Azure Active Directory integration with eDigitalResearch</span></span>

<span data-ttu-id="72647-104">在此教學課程中，您學會如何 toointegrate eDigitalResearch 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="72647-104">In this tutorial, you learn how toointegrate eDigitalResearch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="72647-105">與 Azure AD 整合 eDigitalResearch 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="72647-105">Integrating eDigitalResearch with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="72647-106">您可以控制存取 tooeDigitalResearch Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="72647-106">You can control in Azure AD who has access tooeDigitalResearch.</span></span>
- <span data-ttu-id="72647-107">您可以啟用您的使用者 tooautomatically get 登入 tooeDigitalResearch （單一登入） 具有其 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="72647-107">You can enable your users tooautomatically get signed-on tooeDigitalResearch (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="72647-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="72647-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="72647-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="72647-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72647-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="72647-110">Prerequisites</span></span>

<span data-ttu-id="72647-111">tooconfigure eDigitalResearch 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="72647-111">tooconfigure Azure AD integration with eDigitalResearch, you need hello following items:</span></span>

- <span data-ttu-id="72647-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="72647-112">An Azure AD subscription</span></span>
- <span data-ttu-id="72647-113">已啟用 eDigitalResearch 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="72647-113">A eDigitalResearch single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="72647-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="72647-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="72647-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="72647-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="72647-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="72647-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="72647-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="72647-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="72647-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="72647-118">Scenario description</span></span>
<span data-ttu-id="72647-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="72647-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="72647-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="72647-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="72647-121">從 hello 圖庫加入 eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="72647-121">Adding eDigitalResearch from hello gallery</span></span>
2. <span data-ttu-id="72647-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="72647-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-edigitalresearch-from-hello-gallery"></a><span data-ttu-id="72647-123">從 hello 圖庫加入 eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="72647-123">Adding eDigitalResearch from hello gallery</span></span>
<span data-ttu-id="72647-124">tooconfigure hello 整合 eDigitalResearch 到 Azure AD，您需要 tooadd eDigitalResearch hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="72647-124">tooconfigure hello integration of eDigitalResearch into Azure AD, you need tooadd eDigitalResearch from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="72647-125">**tooadd eDigitalResearch 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="72647-125">**tooadd eDigitalResearch from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="72647-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="72647-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="72647-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="72647-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="72647-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="72647-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="72647-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="72647-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="72647-133">在 hello 搜尋方塊中，輸入**eDigitalResearch**，選取**eDigitalResearch**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="72647-133">In hello search box, type **eDigitalResearch**, select **eDigitalResearch** from result panel then click **Add** button tooadd hello application.</span></span>

    ![eDigitalResearch hello [結果] 清單中](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="72647-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="72647-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="72647-136">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 eDigitalResearch 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="72647-136">In this section, you configure and test Azure AD single sign-on with eDigitalResearch based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="72647-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 eDigitalResearch 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="72647-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in eDigitalResearch is tooa user in Azure AD.</span></span> <span data-ttu-id="72647-138">換句話說，Azure AD 使用者與 hello eDigitalResearch 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="72647-138">In other words, a link relationship between an Azure AD user and hello related user in eDigitalResearch needs toobe established.</span></span>

<span data-ttu-id="72647-139">EDigitalResearch 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="72647-139">In eDigitalResearch, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="72647-140">tooconfigure 及 eDigitalResearch 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="72647-140">tooconfigure and test Azure AD single sign-on with eDigitalResearch, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="72647-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="72647-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="72647-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="72647-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="72647-143">**[建立測試使用者 eDigitalResearch](#create-a-edigitalresearch-test-user)**  -toohave 是連結的 toohello Azure AD 使用者表示法的 eDigitalResearch 的許 Simon 的對應項目。</span><span class="sxs-lookup"><span data-stu-id="72647-143">**[Create a eDigitalResearch test user](#create-a-edigitalresearch-test-user)** - toohave a counterpart of Britta Simon in eDigitalResearch that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="72647-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="72647-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="72647-145">**[測試單一登入](#test-single-sign-on)** tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="72647-145">**[Test single sign-on](#test-single-sign-on)**  tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="72647-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="72647-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="72647-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 eDigitalResearch 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="72647-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your eDigitalResearch application.</span></span>

<span data-ttu-id="72647-148">**tooconfigure Azure AD 單一登入與 eDigitalResearch，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="72647-148">**tooconfigure Azure AD single sign-on with eDigitalResearch, perform hello following steps:**</span></span>

1. <span data-ttu-id="72647-149">在 Azure 入口網站上 hello hello **eDigitalResearch**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="72647-149">In hello Azure portal, on hello **eDigitalResearch** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="72647-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="72647-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_samlbase.png)

3. <span data-ttu-id="72647-153">在 hello **eDigitalResearch 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="72647-153">On hello **eDigitalResearch Domain and URLs** section, perform hello following steps:</span></span>

    ![eDigitalResearch 網域和 URL 單一登入資訊](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_url.png)

    <span data-ttu-id="72647-155">a.</span><span class="sxs-lookup"><span data-stu-id="72647-155">a.</span></span> <span data-ttu-id="72647-156">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company-name>.edigitalresearch.com`</span><span class="sxs-lookup"><span data-stu-id="72647-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company-name>.edigitalresearch.com`</span></span>

    <span data-ttu-id="72647-157">b.</span><span class="sxs-lookup"><span data-stu-id="72647-157">b.</span></span> <span data-ttu-id="72647-158">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company-name>.edigitalresearch.com/login/consume`</span><span class="sxs-lookup"><span data-stu-id="72647-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company-name>.edigitalresearch.com/login/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="72647-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="72647-159">These values are not real.</span></span> <span data-ttu-id="72647-160">以 hello 實際的識別項和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="72647-160">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="72647-161">請連絡[eDigitalResearch 支援小組](http://www.maruedr.com/contact)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="72647-161">Contact [eDigitalResearch support team](http://www.maruedr.com/contact) tooget these values.</span></span>
 


4. <span data-ttu-id="72647-162">在 hello **SAML 簽章憑證**區段中，按一下**憑證 Base(64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="72647-162">On hello **SAML Signing Certificate** section, click **Certificate Base(64)** and then save hello certificate file on your computer.</span></span>

    <span data-ttu-id="72647-163">!</span><span class="sxs-lookup"><span data-stu-id="72647-163">!</span></span>![hello 憑證下載連結](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_certificate.png) 

5. <span data-ttu-id="72647-165">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="72647-165">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="72647-167">在 hello **eDigitalResearch 組態**區段中，按一下**設定 eDigitalResearch** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="72647-167">On hello **eDigitalResearch Configuration** section, click **Configure eDigitalResearch** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="72647-168">複製 hello**登出 URL、 SAML 實體識別碼**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="72647-168">Copy hello **Sign-Out URL, SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![eDigitalResearch 組態](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_configure.png) 

7. <span data-ttu-id="72647-170">tooconfigure 單一登入上**eDigitalResearch**端，您需要下載 toosend hello**憑證 (Base64) 檔案**， **SAML 實體識別碼**，和**登出 URL**太[eDigitalResearch 支援小組](http://www.maruedr.com/contact)。</span><span class="sxs-lookup"><span data-stu-id="72647-170">tooconfigure single sign-on on **eDigitalResearch** side, you need toosend hello downloaded **Certificate (Base64) File**, **SAML Entity ID**, and **Sign-Out URL** too[eDigitalResearch support team](http://www.maruedr.com/contact).</span></span> <span data-ttu-id="72647-171">設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。</span><span class="sxs-lookup"><span data-stu-id="72647-171">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="72647-172">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="72647-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="72647-173">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="72647-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="72647-174">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="72647-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="72647-175">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="72647-175">Create an Azure AD test user</span></span>

<span data-ttu-id="72647-176">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="72647-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="72647-178">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="72647-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="72647-179">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="72647-179">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="72647-181">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="72647-181">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="72647-183">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="72647-183">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="72647-185">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="72647-185">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_04.png)

    <span data-ttu-id="72647-187">a.</span><span class="sxs-lookup"><span data-stu-id="72647-187">a.</span></span> <span data-ttu-id="72647-188">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="72647-188">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="72647-189">b.</span><span class="sxs-lookup"><span data-stu-id="72647-189">b.</span></span> <span data-ttu-id="72647-190">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="72647-190">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="72647-191">c.</span><span class="sxs-lookup"><span data-stu-id="72647-191">c.</span></span> <span data-ttu-id="72647-192">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="72647-192">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="72647-193">d.</span><span class="sxs-lookup"><span data-stu-id="72647-193">d.</span></span> <span data-ttu-id="72647-194">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="72647-194">Click **Create**.</span></span>
  
### <a name="create-a-edigitalresearch-test-user"></a><span data-ttu-id="72647-195">建立 eDigitalResearch 測試使用者</span><span class="sxs-lookup"><span data-stu-id="72647-195">Create a eDigitalResearch test user</span></span>

<span data-ttu-id="72647-196">hello 本節目標在於 toocreate eDigitalResearch 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="72647-196">hello objective of this section is toocreate a user called Britta Simon in eDigitalResearch.</span></span> 

<span data-ttu-id="72647-197">使用 hello [eDigitalResearch 支援小組](http://www.maruedr.com/contact)tooget 所建立的使用者。</span><span class="sxs-lookup"><span data-stu-id="72647-197">Work with hello [eDigitalResearch support team](http://www.maruedr.com/contact) tooget users created.</span></span>       
    
 > [!NOTE]
 > <span data-ttu-id="72647-198">hello Azure Active Directory 帳戶持有者會收到一封電子郵件，並且遵循連結 tooconfirm 他們的帳戶之前就會生效。</span><span class="sxs-lookup"><span data-stu-id="72647-198">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="72647-199">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="72647-199">Assign hello Azure AD test user</span></span>

<span data-ttu-id="72647-200">在本節中，您可以授與存取 tooeDigitalResearch 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="72647-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooeDigitalResearch.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="72647-202">**tooassign 許 Simon tooeDigitalResearch，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="72647-202">**tooassign Britta Simon tooeDigitalResearch, perform hello following steps:**</span></span>

1. <span data-ttu-id="72647-203">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="72647-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="72647-205">在 [hello] 應用程式清單中，選取**eDigitalResearch**。</span><span class="sxs-lookup"><span data-stu-id="72647-205">In hello applications list, select **eDigitalResearch**.</span></span>

    ![hello 應用程式清單中的 hello eDigitalResearch 連結](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_app.png)  

3. <span data-ttu-id="72647-207">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="72647-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="72647-209">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="72647-209">Click **Add** button.</span></span> <span data-ttu-id="72647-210">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="72647-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="72647-212">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="72647-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="72647-213">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="72647-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="72647-214">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="72647-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="72647-215">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="72647-215">Test single sign-on</span></span>

<span data-ttu-id="72647-216">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="72647-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="72647-217">當您按一下 hello eDigitalResearch 磚 hello 存取面板中的時，您應該取得自動登入 tooyour eDigitalResearch 應用程式。</span><span class="sxs-lookup"><span data-stu-id="72647-217">When you click hello eDigitalResearch tile in hello Access Panel, you should get automatically signed-on tooyour eDigitalResearch application.</span></span>
<span data-ttu-id="72647-218">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="72647-218">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="72647-219">其他資源</span><span class="sxs-lookup"><span data-stu-id="72647-219">Additional resources</span></span>

* [<span data-ttu-id="72647-220">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="72647-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="72647-221">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="72647-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_203.png


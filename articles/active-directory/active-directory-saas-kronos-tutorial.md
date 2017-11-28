---
title: "教學課程：Azure Active Directory 與 Kronos 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與克羅納之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e28d6191-c375-43c6-b2df-22daa88d9939
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 16fd5c203162d10b78f51b00d79017adaf8632c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kronos"></a><span data-ttu-id="f52a1-103">教學課程：Azure Active Directory 與 Kronos 整合</span><span class="sxs-lookup"><span data-stu-id="f52a1-103">Tutorial: Azure Active Directory integration with Kronos</span></span>

<span data-ttu-id="f52a1-104">在此教學課程中，您學會如何 toointegrate 克羅納與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="f52a1-104">In this tutorial, you learn how toointegrate Kronos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f52a1-105">與 Azure AD 整合克羅納可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="f52a1-105">Integrating Kronos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f52a1-106">您可以控制存取 tooKronos Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="f52a1-106">You can control in Azure AD who has access tooKronos</span></span>
- <span data-ttu-id="f52a1-107">您可以啟用您的使用者 tooautomatically get 登入 tooKronos （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="f52a1-107">You can enable your users tooautomatically get signed-on tooKronos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f52a1-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f52a1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f52a1-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="f52a1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f52a1-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f52a1-110">Prerequisites</span></span>

<span data-ttu-id="f52a1-111">tooconfigure 克羅納與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="f52a1-111">tooconfigure Azure AD integration with Kronos, you need hello following items:</span></span>

- <span data-ttu-id="f52a1-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f52a1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f52a1-113">已啟用 **Kronos Workforce Central** SSO 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f52a1-113">A **Kronos Workforce Central** SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f52a1-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="f52a1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f52a1-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="f52a1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f52a1-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f52a1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f52a1-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="f52a1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f52a1-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="f52a1-118">Scenario description</span></span>
<span data-ttu-id="f52a1-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f52a1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f52a1-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="f52a1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f52a1-121">從 hello 圖庫加入克羅納</span><span class="sxs-lookup"><span data-stu-id="f52a1-121">Adding Kronos from hello gallery</span></span>
2. <span data-ttu-id="f52a1-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f52a1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kronos-from-hello-gallery"></a><span data-ttu-id="f52a1-123">從 hello 圖庫加入克羅納</span><span class="sxs-lookup"><span data-stu-id="f52a1-123">Adding Kronos from hello gallery</span></span>
<span data-ttu-id="f52a1-124">tooconfigure hello 整合克羅納到 Azure AD，您需要 tooadd 克羅納 hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f52a1-124">tooconfigure hello integration of Kronos into Azure AD, you need tooadd Kronos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f52a1-125">**tooadd 克羅納從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="f52a1-125">**tooadd Kronos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f52a1-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="f52a1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f52a1-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f52a1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f52a1-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f52a1-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="f52a1-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="f52a1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="f52a1-133">在 [hello] 搜尋方塊中，輸入**克羅納**。</span><span class="sxs-lookup"><span data-stu-id="f52a1-133">In hello search box, type **Kronos**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_search.png)

5. <span data-ttu-id="f52a1-135">在 hello 結果 窗格中，選取 **克羅納**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f52a1-135">In hello results panel, select **Kronos**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f52a1-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f52a1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f52a1-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Kronos 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f52a1-138">In this section, you configure and test Azure AD single sign-on with Kronos based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f52a1-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中克羅納是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="f52a1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kronos is tooa user in Azure AD.</span></span> <span data-ttu-id="f52a1-140">換句話說，Azure AD 使用者與 hello 克羅納中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="f52a1-140">In other words, a link relationship between an Azure AD user and hello related user in Kronos needs toobe established.</span></span>

<span data-ttu-id="f52a1-141">克羅納中, 指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f52a1-141">In Kronos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f52a1-142">tooconfigure 及克羅納與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="f52a1-142">tooconfigure and test Azure AD single sign-on with Kronos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f52a1-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="f52a1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f52a1-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="f52a1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f52a1-145">**[建立測試使用者克羅納](#creating-a-kronos-test-user)** -toohave 許 Simon 克羅納所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="f52a1-145">**[Creating a Kronos test user](#creating-a-kronos-test-user)** - toohave a counterpart of Britta Simon in Kronos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f52a1-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f52a1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f52a1-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="f52a1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f52a1-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f52a1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f52a1-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並克羅納應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="f52a1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kronos application.</span></span>

<span data-ttu-id="f52a1-150">**tooconfigure Azure AD 單一登入與克羅納，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="f52a1-150">**tooconfigure Azure AD single sign-on with Kronos, perform hello following steps:**</span></span>

1. <span data-ttu-id="f52a1-151">在 Azure 入口網站上 hello hello**克羅納**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="f52a1-151">In hello Azure portal, on hello **Kronos** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="f52a1-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f52a1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_samlbase.png)

3. <span data-ttu-id="f52a1-155">在 hello**克羅納網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="f52a1-155">On hello **Kronos Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_url.png)

    <span data-ttu-id="f52a1-157">a.</span><span class="sxs-lookup"><span data-stu-id="f52a1-157">a.</span></span> <span data-ttu-id="f52a1-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.kronos.net/`</span><span class="sxs-lookup"><span data-stu-id="f52a1-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.kronos.net/`</span></span>

    <span data-ttu-id="f52a1-159">b.</span><span class="sxs-lookup"><span data-stu-id="f52a1-159">b.</span></span> <span data-ttu-id="f52a1-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span><span class="sxs-lookup"><span data-stu-id="f52a1-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f52a1-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="f52a1-161">These values are not real.</span></span> <span data-ttu-id="f52a1-162">以 hello 實際的識別項和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="f52a1-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="f52a1-163">請連絡[克羅納支援小組](https://www.kronos.in/contact/en-in/form)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="f52a1-163">Contact [Kronos support team](https://www.kronos.in/contact/en-in/form) tooget these values.</span></span>
 
4. <span data-ttu-id="f52a1-164">克羅納應用程式預期 hello SAML 判斷提示，以特定格式。</span><span class="sxs-lookup"><span data-stu-id="f52a1-164">Your Kronos application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="f52a1-165">使用[克羅納支援小組](https://www.kronos.in/contact/en-in/form)第一個 tooidentify hello 正確的使用者識別碼，這個識別碼會對應到 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f52a1-165">Work with [Kronos support team](https://www.kronos.in/contact/en-in/form) first tooidentify hello correct user identifier, which is mapped into hello application.</span></span> <span data-ttu-id="f52a1-166">也請採取 hello 指引 hello 屬性，他們想要讓此對應 toouse。</span><span class="sxs-lookup"><span data-stu-id="f52a1-166">Also please take hello guidance about hello attribute, which they want toouse for this mapping.</span></span>
 
     <span data-ttu-id="f52a1-167">Microsoft 建議使用 hello **"NameIdentifier"**當做使用者識別碼屬性。</span><span class="sxs-lookup"><span data-stu-id="f52a1-167">Microsoft recommends using hello **"NameIdentifier"** attribute as user identifier.</span></span> <span data-ttu-id="f52a1-168">您可以從 hello 管理這些屬性的 hello 值**使用者屬性 」**應用程式整合頁面上的一節。</span><span class="sxs-lookup"><span data-stu-id="f52a1-168">You can manage hello values of these attributes from hello **"User Attributes"** section on application integration page.</span></span>
     
     <span data-ttu-id="f52a1-169">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="f52a1-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="f52a1-170">我們已在這裡對應 hello**使用者識別碼 (nameid)**與**ExtractMailPrefix()**函式的**user.userprincipalname**。</span><span class="sxs-lookup"><span data-stu-id="f52a1-170">Here we have mapped hello **User Identifier (nameid)** with **ExtractMailPrefix()** function of **user.userprincipalname**.</span></span> <span data-ttu-id="f52a1-171">這可讓 hello 的前置詞值，這是唯一的使用者 id。 hello hello 使用者的電子郵件</span><span class="sxs-lookup"><span data-stu-id="f52a1-171">This gives hello prefix value of email of hello user which is hello unique User ID.</span></span> <span data-ttu-id="f52a1-172">這是在每個成功的回應中傳送 toohello 克羅納應用程式。</span><span class="sxs-lookup"><span data-stu-id="f52a1-172">This is sent toohello Kronos application in every successful response.</span></span> 
     
    ![設定單一登入](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_attribute.png)

5. <span data-ttu-id="f52a1-174">在 hello**使用者屬性**區段 hello**單一登入**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="f52a1-174">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="f52a1-175">a.</span><span class="sxs-lookup"><span data-stu-id="f52a1-175">a.</span></span> <span data-ttu-id="f52a1-176">在 hello 使用者識別碼下拉式清單中，選取**ExtractMailPrefix**。</span><span class="sxs-lookup"><span data-stu-id="f52a1-176">In hello User Identifier dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="f52a1-177">b.</span><span class="sxs-lookup"><span data-stu-id="f52a1-177">b.</span></span> <span data-ttu-id="f52a1-178">在 hello**郵件**下拉式清單中選取**user.userprincipalname**。</span><span class="sxs-lookup"><span data-stu-id="f52a1-178">In hello **Mail** dropdown list, select **user.userprincipalname**.</span></span>

6. <span data-ttu-id="f52a1-179">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="f52a1-179">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_certificate.png) 

7. <span data-ttu-id="f52a1-181">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="f52a1-181">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-kronos-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f52a1-183">tooconfigure 單一登入上**克羅納**端，您需要下載 toosend hello**中繼資料 XML**太[克羅納支援小組](https://www.kronos.in/contact/en-in/form)。</span><span class="sxs-lookup"><span data-stu-id="f52a1-183">tooconfigure single sign-on on **Kronos** side, you need toosend hello downloaded **Metadata XML** too[Kronos support team](https://www.kronos.in/contact/en-in/form).</span></span> 

> [!TIP]
> <span data-ttu-id="f52a1-184">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="f52a1-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f52a1-185">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="f52a1-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f52a1-186">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f52a1-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f52a1-187">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f52a1-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="f52a1-188">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="f52a1-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="f52a1-190">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="f52a1-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f52a1-191">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="f52a1-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kronos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f52a1-193">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="f52a1-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kronos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f52a1-195">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="f52a1-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kronos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f52a1-197">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="f52a1-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kronos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f52a1-199">a.</span><span class="sxs-lookup"><span data-stu-id="f52a1-199">a.</span></span> <span data-ttu-id="f52a1-200">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="f52a1-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f52a1-201">b.</span><span class="sxs-lookup"><span data-stu-id="f52a1-201">b.</span></span> <span data-ttu-id="f52a1-202">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="f52a1-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f52a1-203">c.</span><span class="sxs-lookup"><span data-stu-id="f52a1-203">c.</span></span> <span data-ttu-id="f52a1-204">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="f52a1-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f52a1-205">d.</span><span class="sxs-lookup"><span data-stu-id="f52a1-205">d.</span></span> <span data-ttu-id="f52a1-206">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f52a1-206">Click **Create**.</span></span>
 
### <a name="creating-a-kronos-test-user"></a><span data-ttu-id="f52a1-207">建立 Kronos 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f52a1-207">Creating a Kronos test user</span></span>

<span data-ttu-id="f52a1-208">在本節中，您會在 Kronos 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="f52a1-208">In this section, you create a user called Britta Simon in Kronos.</span></span> <span data-ttu-id="f52a1-209">必須再執行 SSO 的 hello 應用程式中，佈建所有 hello 使用者 toobe 克羅納應用程式。</span><span class="sxs-lookup"><span data-stu-id="f52a1-209">Kronos application needs all hello users toobe provisioned in hello application before doing SSO.</span></span> 

<span data-ttu-id="f52a1-210">使用 hello[克羅納支援小組](https://www.kronos.in/contact/en-in/form)tooprovision hello 應用程式的所有這些使用者。</span><span class="sxs-lookup"><span data-stu-id="f52a1-210">Work with hello [Kronos support team](https://www.kronos.in/contact/en-in/form) tooprovision all these users into hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f52a1-211">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="f52a1-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f52a1-212">在本節中，您可以授與存取 tooKronos 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f52a1-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKronos.</span></span>

![指派使用者][200] 

<span data-ttu-id="f52a1-214">**tooassign 許 Simon tooKronos，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="f52a1-214">**tooassign Britta Simon tooKronos, perform hello following steps:**</span></span>

1. <span data-ttu-id="f52a1-215">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f52a1-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="f52a1-217">在 [hello] 應用程式清單中，選取**克羅納**。</span><span class="sxs-lookup"><span data-stu-id="f52a1-217">In hello applications list, select **Kronos**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_app.png) 

3. <span data-ttu-id="f52a1-219">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="f52a1-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="f52a1-221">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f52a1-221">Click **Add** button.</span></span> <span data-ttu-id="f52a1-222">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f52a1-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="f52a1-224">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="f52a1-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f52a1-225">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f52a1-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f52a1-226">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f52a1-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f52a1-227">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="f52a1-227">Testing single sign-on</span></span>

<span data-ttu-id="f52a1-228">本節中，您可以測試使用存取面板 hello Azure AD 的 SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="f52a1-228">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="f52a1-229">當您按一下的 hello 克羅納磚 hello 存取面板中時，您應該取得自動登入 tooyour 克羅納應用程式。</span><span class="sxs-lookup"><span data-stu-id="f52a1-229">When you click hello Kronos tile in hello Access Panel, you should get automatically signed-on tooyour Kronos application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f52a1-230">其他資源</span><span class="sxs-lookup"><span data-stu-id="f52a1-230">Additional resources</span></span>

* [<span data-ttu-id="f52a1-231">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f52a1-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f52a1-232">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="f52a1-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_203.png


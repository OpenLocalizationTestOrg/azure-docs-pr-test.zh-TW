---
title: "教學課程：Azure Active Directory 與 Blackboard Learn - Shibboleth 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與矩形色塊學習-Shibboleth 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e435cbb4-c0f0-400e-943c-5c923fa8ddf2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 40aa3ec5f42b93157af3c56daaadfa66203b21d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn---shibboleth"></a><span data-ttu-id="6c338-103">教學課程：Azure Active Directory 與 Blackboard Learn - Shibboleth 整合</span><span class="sxs-lookup"><span data-stu-id="6c338-103">Tutorial: Azure Active Directory integration with Blackboard Learn - Shibboleth</span></span>

<span data-ttu-id="6c338-104">在此教學課程中，您學會如何 toointegrate 矩形色塊深入了解-Shibboleth 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="6c338-104">In this tutorial, you learn how toointegrate Blackboard Learn - Shibboleth with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6c338-105">將矩形色塊學習-Shibboleth 與 Azure AD 整合可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="6c338-105">Integrating Blackboard Learn - Shibboleth with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6c338-106">您可以控制存取 tooBlackboard 深入了解-Shibboleth 的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="6c338-106">You can control in Azure AD who has access tooBlackboard Learn - Shibboleth</span></span>
- <span data-ttu-id="6c338-107">您可以啟用您的使用者 tooautomatically get 登入 tooBlackboard 深入了解-（單一登入） 的 Shibboleth 與 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="6c338-107">You can enable your users tooautomatically get signed-on tooBlackboard Learn - Shibboleth (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6c338-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6c338-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6c338-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="6c338-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c338-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6c338-110">Prerequisites</span></span>

<span data-ttu-id="6c338-111">tooconfigure Azure AD 與矩形色塊學習-Shibboleth，整合您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="6c338-111">tooconfigure Azure AD integration with Blackboard Learn - Shibboleth, you need hello following items:</span></span>

- <span data-ttu-id="6c338-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6c338-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6c338-113">已啟用 Blackboard Learn - Shibboleth 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6c338-113">A Blackboard Learn - Shibboleth single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6c338-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="6c338-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6c338-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="6c338-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6c338-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6c338-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6c338-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="6c338-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6c338-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="6c338-118">Scenario description</span></span>
<span data-ttu-id="6c338-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6c338-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6c338-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="6c338-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6c338-121">加入矩形色塊深入了解-從 hello 組件庫的 Shibboleth</span><span class="sxs-lookup"><span data-stu-id="6c338-121">Adding Blackboard Learn - Shibboleth from hello gallery</span></span>
2. <span data-ttu-id="6c338-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6c338-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn---shibboleth-from-hello-gallery"></a><span data-ttu-id="6c338-123">加入矩形色塊深入了解-從 hello 組件庫的 Shibboleth</span><span class="sxs-lookup"><span data-stu-id="6c338-123">Adding Blackboard Learn - Shibboleth from hello gallery</span></span>
<span data-ttu-id="6c338-124">tooconfigure hello 整合了矩形色塊-Shibboleth 到 Azure AD，您需要深入了解矩形色塊-tooadd Shibboleth hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c338-124">tooconfigure hello integration of Blackboard Learn - Shibboleth into Azure AD, you need tooadd Blackboard Learn - Shibboleth from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6c338-125">**tooadd 矩形色塊深入了解-Shibboleth hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6c338-125">**tooadd Blackboard Learn - Shibboleth from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6c338-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="6c338-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6c338-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6c338-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6c338-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6c338-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="6c338-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c338-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="6c338-133">在 [hello] 搜尋方塊中，輸入**矩形色塊學習-Shibboleth**。</span><span class="sxs-lookup"><span data-stu-id="6c338-133">In hello search box, type **Blackboard Learn - Shibboleth**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_search.png)

5. <span data-ttu-id="6c338-135">在 [hello [結果] 窗格中，選取 [**矩形色塊學習-Shibboleth**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c338-135">In hello results panel, select **Blackboard Learn - Shibboleth**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6c338-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6c338-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6c338-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Blackboard Learn - Shibboleth 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6c338-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6c338-139">針對單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中深入了解矩形色塊-Shibboleth tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="6c338-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Blackboard Learn - Shibboleth is tooa user in Azure AD.</span></span> <span data-ttu-id="6c338-140">換句話說，Azure AD 使用者與 hello 中深入了解矩形色塊-相關的使用者之間的連結關聯性 Shibboleth 需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="6c338-140">In other words, a link relationship between an Azure AD user and hello related user in Blackboard Learn - Shibboleth needs toobe established.</span></span>

<span data-ttu-id="6c338-141">在矩形色塊學習-Shibboleth，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6c338-141">In Blackboard Learn - Shibboleth, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6c338-142">tooconfigure 和測試 Azure AD 單一登入與矩形色塊學習-Shibboleth，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="6c338-142">tooconfigure and test Azure AD single sign-on with Blackboard Learn - Shibboleth, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6c338-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="6c338-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6c338-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="6c338-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6c338-145">**[建立矩形色塊深入了解-Shibboleth 測試使用者](#creating-a-blackboard-learn---shibboleth-test-user)** -toohave 許 Simon 深入了解矩形色塊中對應項目-Shibboleth 連結的 toohello Azure AD 表示的使用者。</span><span class="sxs-lookup"><span data-stu-id="6c338-145">**[Creating a Blackboard Learn - Shibboleth test user](#creating-a-blackboard-learn---shibboleth-test-user)** - toohave a counterpart of Britta Simon in Blackboard Learn - Shibboleth that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6c338-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6c338-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6c338-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="6c338-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6c338-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6c338-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6c338-149">在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並在您矩形色塊深入了解-Shibboleth 應用程式設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="6c338-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Blackboard Learn - Shibboleth application.</span></span>

<span data-ttu-id="6c338-150">**tooconfigure Azure AD 單一登入與矩形色塊學習-Shibboleth，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6c338-150">**tooconfigure Azure AD single sign-on with Blackboard Learn - Shibboleth, perform hello following steps:**</span></span>

1. <span data-ttu-id="6c338-151">在 Azure 入口網站上 hello hello**矩形色塊學習-Shibboleth**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="6c338-151">In hello Azure portal, on hello **Blackboard Learn - Shibboleth** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="6c338-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6c338-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_samlbase.png)

3. <span data-ttu-id="6c338-155">在 [hello**矩形色塊學習-Shibboleth 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6c338-155">On hello **Blackboard Learn - Shibboleth Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_url.png)

    <span data-ttu-id="6c338-157">a.</span><span class="sxs-lookup"><span data-stu-id="6c338-157">a.</span></span> <span data-ttu-id="6c338-158">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span><span class="sxs-lookup"><span data-stu-id="6c338-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span></span>

    <span data-ttu-id="6c338-159">b.</span><span class="sxs-lookup"><span data-stu-id="6c338-159">b.</span></span> <span data-ttu-id="6c338-160">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span><span class="sxs-lookup"><span data-stu-id="6c338-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span></span>

    <span data-ttu-id="6c338-161">c.</span><span class="sxs-lookup"><span data-stu-id="6c338-161">c.</span></span> <span data-ttu-id="6c338-162">在 [hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span><span class="sxs-lookup"><span data-stu-id="6c338-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="6c338-163">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="6c338-163">These values are not real.</span></span> <span data-ttu-id="6c338-164">更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="6c338-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="6c338-165">請連絡[矩形色塊學習-Shibboleth 用戶端支援小組](https://www.blackboard.com/forms/contact-us_form.aspx)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="6c338-165">Contact [Blackboard Learn - Shibboleth Client support team](https://www.blackboard.com/forms/contact-us_form.aspx) tooget these values.</span></span> 

4. <span data-ttu-id="6c338-166">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="6c338-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_certificate.png) 

5. <span data-ttu-id="6c338-168">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c338-168">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="6c338-170">在 [hello**矩形色塊學習-Shibboleth 組態**區段中，按一下**設定矩形色塊深入了解-Shibboleth** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="6c338-170">On hello **Blackboard Learn - Shibboleth Configuration** section, click **Configure Blackboard Learn - Shibboleth** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6c338-171">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="6c338-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_configure.png) 

7. <span data-ttu-id="6c338-173">tooconfigure 單一登入上**矩形色塊學習-Shibboleth**端，您需要下載 toosend hello**中繼資料 XML**和**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務URL**太[矩形色塊學習-Shibboleth 支援小組](https://www.blackboard.com/forms/contact-us_form.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6c338-173">tooconfigure single sign-on on **Blackboard Learn - Shibboleth** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="6c338-174">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="6c338-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6c338-175">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="6c338-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6c338-176">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6c338-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6c338-177">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6c338-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="6c338-178">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="6c338-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="6c338-180">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6c338-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6c338-181">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="6c338-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6c338-183">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="6c338-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6c338-185">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="6c338-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6c338-187">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6c338-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6c338-189">a.</span><span class="sxs-lookup"><span data-stu-id="6c338-189">a.</span></span> <span data-ttu-id="6c338-190">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="6c338-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6c338-191">b.</span><span class="sxs-lookup"><span data-stu-id="6c338-191">b.</span></span> <span data-ttu-id="6c338-192">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="6c338-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6c338-193">c.</span><span class="sxs-lookup"><span data-stu-id="6c338-193">c.</span></span> <span data-ttu-id="6c338-194">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="6c338-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6c338-195">d.</span><span class="sxs-lookup"><span data-stu-id="6c338-195">d.</span></span> <span data-ttu-id="6c338-196">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6c338-196">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn---shibboleth-test-user"></a><span data-ttu-id="6c338-197">建立 Blackboard Learn - Shibboleth 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6c338-197">Creating a Blackboard Learn - Shibboleth test user</span></span>

<span data-ttu-id="6c338-198">在本節中，您會在 Blackboard Learn - Shibboleth 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="6c338-198">In this section, you create a user called Britta Simon in Blackboard Learn - Shibboleth.</span></span> <span data-ttu-id="6c338-199">使用您[矩形色塊學習-Shibboleth 支援小組](https://www.blackboard.com/forms/contact-us_form.aspx)tooadd hello hello 矩形色塊學習-Shibboleth 平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="6c338-199">Work with your [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx) tooadd hello users in hello Blackboard Learn - Shibboleth platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6c338-200">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="6c338-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6c338-201">在本節中，您可以授與存取 tooBlackboard 深入了解-Shibboleth 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6c338-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlackboard Learn - Shibboleth.</span></span>

![指派使用者][200] 

<span data-ttu-id="6c338-203">**tooassign 許 Simon tooBlackboard 深入了解-Shibboleth，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6c338-203">**tooassign Britta Simon tooBlackboard Learn - Shibboleth, perform hello following steps:**</span></span>

1. <span data-ttu-id="6c338-204">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6c338-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="6c338-206">在 [hello] 應用程式清單中，選取**矩形色塊學習-Shibboleth**。</span><span class="sxs-lookup"><span data-stu-id="6c338-206">In hello applications list, select **Blackboard Learn - Shibboleth**.</span></span>

    ![設定單一登入](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_app.png) 

3. <span data-ttu-id="6c338-208">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="6c338-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="6c338-210">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c338-210">Click **Add** button.</span></span> <span data-ttu-id="6c338-211">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6c338-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="6c338-213">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="6c338-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6c338-214">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c338-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6c338-215">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c338-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6c338-216">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="6c338-216">Testing single sign-on</span></span>

<span data-ttu-id="6c338-217">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="6c338-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6c338-218">當您按一下 hello 矩形色塊學習-Shibboleth hello 存取面板中的磚時，您應該取得自動登入 tooyour 矩形色塊深入了解-Shibboleth 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c338-218">When you click hello Blackboard Learn - Shibboleth tile in hello Access Panel, you should get automatically signed-on tooyour Blackboard Learn - Shibboleth application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6c338-219">其他資源</span><span class="sxs-lookup"><span data-stu-id="6c338-219">Additional resources</span></span>

* [<span data-ttu-id="6c338-220">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6c338-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6c338-221">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="6c338-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_203.png


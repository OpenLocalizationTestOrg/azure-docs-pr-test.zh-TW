---
title: "教學課程：Azure Active Directory 與 Bridge 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與橋接器之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dbb6499-80c1-4d00-a0b4-e0ad5522cf0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 85e1917de63356a86aa87a0f82621391733ab2aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bridge"></a><span data-ttu-id="f20f7-103">教學課程：Azure Active Directory 與 Bridge 整合</span><span class="sxs-lookup"><span data-stu-id="f20f7-103">Tutorial: Azure Active Directory integration with Bridge</span></span>

<span data-ttu-id="f20f7-104">在此教學課程中，您學會如何 toointegrate 橋接與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="f20f7-104">In this tutorial, you learn how toointegrate Bridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f20f7-105">與 Azure AD 整合橋接器可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="f20f7-105">Integrating Bridge with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f20f7-106">您可以控制存取 tooBridge Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="f20f7-106">You can control in Azure AD who has access tooBridge</span></span>
- <span data-ttu-id="f20f7-107">您可以啟用您的使用者 tooautomatically get 登入 tooBridge （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="f20f7-107">You can enable your users tooautomatically get signed-on tooBridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f20f7-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f20f7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f20f7-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="f20f7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f20f7-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f20f7-110">Prerequisites</span></span>

<span data-ttu-id="f20f7-111">tooconfigure 與橋接器的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="f20f7-111">tooconfigure Azure AD integration with Bridge, you need hello following items:</span></span>

- <span data-ttu-id="f20f7-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f20f7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f20f7-113">已啟用 Bridge 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f20f7-113">A Bridge single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f20f7-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="f20f7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f20f7-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="f20f7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f20f7-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f20f7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f20f7-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="f20f7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f20f7-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="f20f7-118">Scenario description</span></span>
<span data-ttu-id="f20f7-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f20f7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f20f7-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="f20f7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f20f7-121">從 hello 圖庫加入橋接器</span><span class="sxs-lookup"><span data-stu-id="f20f7-121">Adding Bridge from hello gallery</span></span>
2. <span data-ttu-id="f20f7-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f20f7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bridge-from-hello-gallery"></a><span data-ttu-id="f20f7-123">從 hello 圖庫加入橋接器</span><span class="sxs-lookup"><span data-stu-id="f20f7-123">Adding Bridge from hello gallery</span></span>
<span data-ttu-id="f20f7-124">tooconfigure hello 整合橋接至 Azure AD，您會需要 tooadd 橋接器 hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f20f7-124">tooconfigure hello integration of Bridge into Azure AD, you need tooadd Bridge from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f20f7-125">**tooadd 橋接器從 hello 組件庫，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="f20f7-125">**tooadd Bridge from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f20f7-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="f20f7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f20f7-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f20f7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f20f7-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f20f7-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="f20f7-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="f20f7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="f20f7-133">在 [hello] 搜尋方塊中，輸入**橋接器**。</span><span class="sxs-lookup"><span data-stu-id="f20f7-133">In hello search box, type **Bridge**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_search.png)

5. <span data-ttu-id="f20f7-135">在 [hello [結果] 窗格中，選取 [**橋接器**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f20f7-135">In hello results panel, select **Bridge**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f20f7-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f20f7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f20f7-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Bridge 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f20f7-138">In this section, you configure and test Azure AD single sign-on with Bridge based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f20f7-139">單一登入 toowork，Azure AD 需要 tooknow 橋接器中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="f20f7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bridge is tooa user in Azure AD.</span></span> <span data-ttu-id="f20f7-140">換句話說，Azure AD 使用者與橋接器中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="f20f7-140">In other words, a link relationship between an Azure AD user and hello related user in Bridge needs toobe established.</span></span>

<span data-ttu-id="f20f7-141">在橋接器中指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f20f7-141">In Bridge, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f20f7-142">tooconfigure 及測試 Azure AD 單一登入與橋接器，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="f20f7-142">tooconfigure and test Azure AD single sign-on with Bridge, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f20f7-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="f20f7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f20f7-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="f20f7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f20f7-145">**[建立橋接器測試使用者](#creating-a-bridge-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的橋接器中對應項目。</span><span class="sxs-lookup"><span data-stu-id="f20f7-145">**[Creating a Bridge test user](#creating-a-bridge-test-user)** - toohave a counterpart of Britta Simon in Bridge that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f20f7-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f20f7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f20f7-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="f20f7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f20f7-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f20f7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f20f7-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並橋接器應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="f20f7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bridge application.</span></span>

<span data-ttu-id="f20f7-150">**tooconfigure Azure AD 單一登入與橋接器，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="f20f7-150">**tooconfigure Azure AD single sign-on with Bridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="f20f7-151">在 Azure 入口網站上 hello hello**橋接器**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="f20f7-151">In hello Azure portal, on hello **Bridge** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="f20f7-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f20f7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_samlbase.png)

3. <span data-ttu-id="f20f7-155">在 [hello**橋接器網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="f20f7-155">On hello **Bridge Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_url.png)

    <span data-ttu-id="f20f7-157">a.</span><span class="sxs-lookup"><span data-stu-id="f20f7-157">a.</span></span> <span data-ttu-id="f20f7-158">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.bridgeapp.com`</span><span class="sxs-lookup"><span data-stu-id="f20f7-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.bridgeapp.com`</span></span>

    <span data-ttu-id="f20f7-159">b.</span><span class="sxs-lookup"><span data-stu-id="f20f7-159">b.</span></span> <span data-ttu-id="f20f7-160">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.bridgeapp.com`</span><span class="sxs-lookup"><span data-stu-id="f20f7-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.bridgeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f20f7-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="f20f7-161">These values are not real.</span></span> <span data-ttu-id="f20f7-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="f20f7-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f20f7-163">請連絡[橋接器用戶端支援小組](https://community.bridgeapp.com/community/help)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="f20f7-163">Contact [Bridge Client support team](https://community.bridgeapp.com/community/help) tooget these values.</span></span> 
 
4. <span data-ttu-id="f20f7-164">在 [hello **SAML 簽章憑證**區段中，按一下**Certificate(Raw)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="f20f7-164">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_certificate.png) 

5. <span data-ttu-id="f20f7-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="f20f7-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-bridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f20f7-168">在 [hello**橋接器組態**區段中，按一下**設定橋接器**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="f20f7-168">On hello **Bridge Configuration** section, click **Configure Bridge** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f20f7-169">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="f20f7-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_configure.png) 

7. <span data-ttu-id="f20f7-171">tooconfigure 單一登入上**橋接器**端，您需要下載 toosend hello **Certificate(Raw)**和**SAML 實體識別碼、 SAML 單一登入服務 URL 和登出 URL**太[橋接器支援小組](https://community.bridgeapp.com/community/help)。</span><span class="sxs-lookup"><span data-stu-id="f20f7-171">tooconfigure single sign-on on **Bridge** side, you need toosend hello downloaded **Certificate(Raw)** and **SAML Entity ID, SAML Single Sign-On Service URL, and Sign-Out URL** too[Bridge support team](https://community.bridgeapp.com/community/help).</span></span> 

> [!TIP]
> <span data-ttu-id="f20f7-172">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="f20f7-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f20f7-173">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="f20f7-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f20f7-174">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f20f7-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f20f7-175">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f20f7-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="f20f7-176">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="f20f7-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="f20f7-178">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="f20f7-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f20f7-179">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="f20f7-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f20f7-181">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="f20f7-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f20f7-183">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="f20f7-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f20f7-185">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="f20f7-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f20f7-187">a.</span><span class="sxs-lookup"><span data-stu-id="f20f7-187">a.</span></span> <span data-ttu-id="f20f7-188">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="f20f7-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f20f7-189">b.</span><span class="sxs-lookup"><span data-stu-id="f20f7-189">b.</span></span> <span data-ttu-id="f20f7-190">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="f20f7-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f20f7-191">c.</span><span class="sxs-lookup"><span data-stu-id="f20f7-191">c.</span></span> <span data-ttu-id="f20f7-192">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="f20f7-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f20f7-193">d.</span><span class="sxs-lookup"><span data-stu-id="f20f7-193">d.</span></span> <span data-ttu-id="f20f7-194">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f20f7-194">Click **Create**.</span></span>
 
### <a name="creating-a-bridge-test-user"></a><span data-ttu-id="f20f7-195">建立 Bridge 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f20f7-195">Creating a Bridge test user</span></span>

<span data-ttu-id="f20f7-196">在本節中，您會在 Bridge 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="f20f7-196">In this section, you create a user called Britta Simon in Bridge.</span></span> <span data-ttu-id="f20f7-197">使用[橋接器用戶端支援小組](https://community.bridgeapp.com/community/help)toocreate hello 平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="f20f7-197">Work with [Bridge Client support team](https://community.bridgeapp.com/community/help) toocreate a user in hello platform.</span></span> <span data-ttu-id="f20f7-198">您可以提高 hello 支援票證，以從橋接器<a href="https://community.bridgeapp.com/community/help">這裡</a>tooadd hello hello 橋接器平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="f20f7-198">You can raise hello support ticket with Bridge from <a href="https://community.bridgeapp.com/community/help">here</a> tooadd hello users in hello Bridge platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f20f7-199">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="f20f7-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f20f7-200">在本節中，您可以授與存取 tooBridge 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f20f7-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBridge.</span></span>

![指派使用者][200] 

<span data-ttu-id="f20f7-202">**tooassign 許 Simon tooBridge，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="f20f7-202">**tooassign Britta Simon tooBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="f20f7-203">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f20f7-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="f20f7-205">在 [hello] 應用程式清單中，選取**橋接器**。</span><span class="sxs-lookup"><span data-stu-id="f20f7-205">In hello applications list, select **Bridge**.</span></span>

    ![設定單一登入](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_app.png) 

3. <span data-ttu-id="f20f7-207">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="f20f7-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="f20f7-209">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f20f7-209">Click **Add** button.</span></span> <span data-ttu-id="f20f7-210">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f20f7-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="f20f7-212">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="f20f7-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f20f7-213">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f20f7-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f20f7-214">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f20f7-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f20f7-215">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="f20f7-215">Testing single sign-on</span></span>

<span data-ttu-id="f20f7-216">本節中，您可以測試使用存取面板 hello Azure AD 的 SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="f20f7-216">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="f20f7-217">當您按一下 hello 橋接器磚 hello 存取面板中的時，您應該取得 tooyour 橋接器應用程式會自動登入。</span><span class="sxs-lookup"><span data-stu-id="f20f7-217">When you click hello Bridge tile in hello Access Panel, you should get automatically signed-on tooyour Bridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f20f7-218">其他資源</span><span class="sxs-lookup"><span data-stu-id="f20f7-218">Additional resources</span></span>

* [<span data-ttu-id="f20f7-219">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f20f7-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f20f7-220">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="f20f7-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_203.png


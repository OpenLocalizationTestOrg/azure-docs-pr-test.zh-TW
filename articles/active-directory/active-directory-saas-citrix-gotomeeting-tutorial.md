---
title: "教學課程：Azure Active Directory 與 Citrix GoToMeeting 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Citrix GoToMeeting 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 46a5da7504806202a5ec29f73c504e772c61bc2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="13327-103">教學課程：Azure Active Directory 與 Citrix GoToMeeting 整合</span><span class="sxs-lookup"><span data-stu-id="13327-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="13327-104">在此教學課程中，您學會如何 toointegrate Citrix GoToMeeting 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="13327-104">In this tutorial, you learn how toointegrate Citrix GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="13327-105">Citrix GoToMeeting 整合與 Azure AD 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="13327-105">Integrating Citrix GoToMeeting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="13327-106">您可以控制存取 tooCitrix GoToMeeting 的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="13327-106">You can control in Azure AD who has access tooCitrix GoToMeeting</span></span>
- <span data-ttu-id="13327-107">您可以啟用您的使用者 tooautomatically get 登入 tooCitrix GoToMeeting （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="13327-107">You can enable your users tooautomatically get signed-on tooCitrix GoToMeeting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="13327-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="13327-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="13327-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="13327-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13327-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="13327-110">Prerequisites</span></span>

<span data-ttu-id="13327-111">tooconfigure Azure AD 與 Citrix GoToMeeting 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="13327-111">tooconfigure Azure AD integration with Citrix GoToMeeting, you need hello following items:</span></span>

- <span data-ttu-id="13327-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="13327-112">An Azure AD subscription</span></span>
- <span data-ttu-id="13327-113">已啟用 Citrix GoToMeeting 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="13327-113">A Citrix GoToMeeting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="13327-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="13327-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="13327-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="13327-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="13327-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="13327-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="13327-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="13327-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="13327-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="13327-118">Scenario description</span></span>
<span data-ttu-id="13327-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="13327-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="13327-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="13327-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="13327-121">新增 Citrix GoToMeeting 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="13327-121">Adding Citrix GoToMeeting from hello gallery</span></span>
2. <span data-ttu-id="13327-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="13327-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-citrix-gotomeeting-from-hello-gallery"></a><span data-ttu-id="13327-123">新增 Citrix GoToMeeting 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="13327-123">Adding Citrix GoToMeeting from hello gallery</span></span>
<span data-ttu-id="13327-124">tooconfigure hello 整合 Citrix GoToMeeting 到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Citrix GoToMeeting。</span><span class="sxs-lookup"><span data-stu-id="13327-124">tooconfigure hello integration of Citrix GoToMeeting into Azure AD, you need tooadd Citrix GoToMeeting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="13327-125">**tooadd Citrix GoToMeeting 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="13327-125">**tooadd Citrix GoToMeeting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="13327-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="13327-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="13327-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="13327-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="13327-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="13327-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="13327-131">按一下**新的應用程式**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="13327-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="13327-133">在 [hello] 搜尋方塊中，輸入**Citrix GoToMeeting**。</span><span class="sxs-lookup"><span data-stu-id="13327-133">In hello search box, type **Citrix GoToMeeting**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. <span data-ttu-id="13327-135">在 [hello [結果] 窗格中，選取 [ **Citrix GoToMeeting**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="13327-135">In hello results panel, select **Citrix GoToMeeting**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="13327-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="13327-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="13327-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Citrix GoToMeeting 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="13327-138">In this section, you configure and test Azure AD single sign-on with Citrix GoToMeeting based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="13327-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 Citrix GoToMeeting 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="13327-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix GoToMeeting is tooa user in Azure AD.</span></span> <span data-ttu-id="13327-140">換句話說，Azure AD 使用者與 Citrix GoToMeeting 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="13327-140">In other words, a link relationship between an Azure AD user and hello related user in Citrix GoToMeeting needs toobe established.</span></span>

<span data-ttu-id="13327-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Citrix GoToMeeting 中。</span><span class="sxs-lookup"><span data-stu-id="13327-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Citrix GoToMeeting.</span></span>

<span data-ttu-id="13327-142">tooconfigure 及 Azure AD 單一登入與 Citrix GoToMeeting 的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="13327-142">tooconfigure and test Azure AD single sign-on with Citrix GoToMeeting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="13327-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="13327-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="13327-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="13327-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="13327-145">**[建立測試使用者 Citrix GoToMeeting](#creating-a-citrix-gotomeeting-test-user) ** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Citrix GoToMeeting 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="13327-145">**[Creating a Citrix GoToMeeting test user](#creating-a-citrix-gotomeeting-test-user)** - toohave a counterpart of Britta Simon in Citrix GoToMeeting that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="13327-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="13327-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="13327-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="13327-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="13327-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="13327-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="13327-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Citrix GoToMeeting 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="13327-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix GoToMeeting application.</span></span>

<span data-ttu-id="13327-150">**tooconfigure Azure AD 單一登入與 Citrix GoToMeeting，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="13327-150">**tooconfigure Azure AD single sign-on with Citrix GoToMeeting, perform hello following steps:**</span></span>

1. <span data-ttu-id="13327-151">在 Azure 入口網站上 hello hello **Citrix GoToMeeting**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="13327-151">In hello Azure portal, on hello **Citrix GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="13327-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="13327-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. <span data-ttu-id="13327-155">在 [hello **Citrix GoToMeeting 網域和 Url**區段中，不需要 tooperform 任何步驟。</span><span class="sxs-lookup"><span data-stu-id="13327-155">On hello **Citrix GoToMeeting Domain and URLs** section, no need tooperform any steps.</span></span>

    ![設定單一登入](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. <span data-ttu-id="13327-157">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="13327-157">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. <span data-ttu-id="13327-159">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="13327-159">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. <span data-ttu-id="13327-161">在 hello Citrix GoToMeeting SAML 組態] 區段中，按一下 [設定 Citrix GoToMeeting SAML tooopen 設定登入視窗。</span><span class="sxs-lookup"><span data-stu-id="13327-161">On hello Citrix GoToMeeting SAML Configuration section, click Configure Citrix GoToMeeting SAML tooopen Configure sign-on window.</span></span> <span data-ttu-id="13327-162">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="13327-162">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

6. <span data-ttu-id="13327-163">在不同的瀏覽器視窗中，登入 tooyour [Citrix 組織 Center](https://account.citrixonline.com/organization/administration/)。</span><span class="sxs-lookup"><span data-stu-id="13327-163">In a different browser window, log in tooyour [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

7. <span data-ttu-id="13327-164">按一下 hello**身分識別提供者**索引標籤，然後再執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="13327-164">Click hello **Identity Provider** tab, and then perform hello following steps:</span></span>  
   
    <span data-ttu-id="13327-165">![SAML 設定](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML 設定")</span><span class="sxs-lookup"><span data-stu-id="13327-165">![SAML setup](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="13327-166">a.</span><span class="sxs-lookup"><span data-stu-id="13327-166">a.</span></span> <span data-ttu-id="13327-167">選取 [手動]</span><span class="sxs-lookup"><span data-stu-id="13327-167">Select **Manual**</span></span>

    <span data-ttu-id="13327-168">b.</span><span class="sxs-lookup"><span data-stu-id="13327-168">b.</span></span> <span data-ttu-id="13327-169">在 Azure 入口網站上 hello hello**在 Citrix GoToMeeting 設定單一登入**對話方塊頁面上，複製 hello **SAML 單一登入服務 URL**值並貼到 hello**登入頁面URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="13327-169">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="13327-170">c.</span><span class="sxs-lookup"><span data-stu-id="13327-170">c.</span></span> <span data-ttu-id="13327-171">在 Azure 入口網站上 hello hello**在 Citrix GoToMeeting 設定單一登入**對話方塊頁面上，複製 hello**登出 URL**值並貼到 hello**登出頁面 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="13327-171">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **Sign-Out URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="13327-172">d.</span><span class="sxs-lookup"><span data-stu-id="13327-172">d.</span></span> <span data-ttu-id="13327-173">在 Azure 入口網站上 hello hello**在 Citrix GoToMeeting 設定單一登入**對話方塊頁面上，複製 hello **SAML 實體識別碼**值並貼到 hello**身分識別提供者的實體識別碼**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="13327-173">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **SAML Entity ID** value, and then paste it into hello **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="13327-174">e.</span><span class="sxs-lookup"><span data-stu-id="13327-174">e.</span></span> <span data-ttu-id="13327-175">tooupload 下載的憑證，按一下 [**上傳憑證**。</span><span class="sxs-lookup"><span data-stu-id="13327-175">tooupload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="13327-176">f.</span><span class="sxs-lookup"><span data-stu-id="13327-176">f.</span></span> <span data-ttu-id="13327-177">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="13327-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="13327-178">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="13327-178">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="13327-179">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="13327-179">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="13327-180">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="13327-180">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="13327-181">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="13327-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="13327-182">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="13327-182">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="13327-184">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="13327-184">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="13327-185">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="13327-185">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="13327-187">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="13327-187">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="13327-189">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="13327-189">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="13327-191">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="13327-191">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="13327-193">a.</span><span class="sxs-lookup"><span data-stu-id="13327-193">a.</span></span> <span data-ttu-id="13327-194">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="13327-194">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="13327-195">b.</span><span class="sxs-lookup"><span data-stu-id="13327-195">b.</span></span> <span data-ttu-id="13327-196">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="13327-196">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="13327-197">c.</span><span class="sxs-lookup"><span data-stu-id="13327-197">c.</span></span> <span data-ttu-id="13327-198">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="13327-198">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="13327-199">d.</span><span class="sxs-lookup"><span data-stu-id="13327-199">d.</span></span> <span data-ttu-id="13327-200">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="13327-200">Click **Create**.</span></span>
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a><span data-ttu-id="13327-201">建立 Citrix GoToMeeting 測試使用者</span><span class="sxs-lookup"><span data-stu-id="13327-201">Creating a Citrix GoToMeeting test user</span></span>

<span data-ttu-id="13327-202">本節會在 Citrix GoToMeeting 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="13327-202">In this section, a user called Britta Simon is created in Citrix GoToMeeting.</span></span> <span data-ttu-id="13327-203">Citrix GoToMeeting 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="13327-203">Citrix GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="13327-204">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="13327-204">There is no action item for you in this section.</span></span> <span data-ttu-id="13327-205">如果使用者不在 Citrix GoToMeeting 中，當您嘗試 tooaccess Citrix GoToMeeting，會建立一個新。</span><span class="sxs-lookup"><span data-stu-id="13327-205">If a user doesn't already exist in Citrix GoToMeeting, a new one is created when you attempt tooaccess Citrix GoToMeeting.</span></span>

>[!Note]
><span data-ttu-id="13327-206">如果您需要以手動方式，請連絡使用者 toocreate [Citrix GoToMeeting 支援小組](https://care.citrixonline.com/gotomeeting)</span><span class="sxs-lookup"><span data-stu-id="13327-206">If you need toocreate a user manually, Contact [Citrix GoToMeeting support team](https://care.citrixonline.com/gotomeeting)</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="13327-207">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="13327-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="13327-208">在本節中，您可以授與存取 tooCitrix GoToMeeting 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="13327-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix GoToMeeting.</span></span>

![指派使用者][200] 

<span data-ttu-id="13327-210">**tooassign 許 Simon tooCitrix GoToMeeting，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="13327-210">**tooassign Britta Simon tooCitrix GoToMeeting, perform hello following steps:**</span></span>

1. <span data-ttu-id="13327-211">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="13327-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="13327-213">在 [hello] 應用程式清單中，選取**Citrix GoToMeeting**。</span><span class="sxs-lookup"><span data-stu-id="13327-213">In hello applications list, select **Citrix GoToMeeting**.</span></span>

    ![設定單一登入](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. <span data-ttu-id="13327-215">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="13327-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="13327-217">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="13327-217">Click **Add** button.</span></span> <span data-ttu-id="13327-218">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="13327-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="13327-220">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="13327-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="13327-221">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="13327-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="13327-222">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="13327-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="13327-223">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="13327-223">Testing single sign-on</span></span>

<span data-ttu-id="13327-224">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="13327-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="13327-225">如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="13327-225">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="13327-226">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="13327-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="13327-227">其他資源</span><span class="sxs-lookup"><span data-stu-id="13327-227">Additional resources</span></span>

* [<span data-ttu-id="13327-228">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="13327-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="13327-229">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="13327-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="13327-230">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="13327-230">Configure User Provisioning</span></span>](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png


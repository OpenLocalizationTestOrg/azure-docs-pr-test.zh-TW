---
title: "教學課程：Azure Active Directory 與 Weekdone 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Weekdone 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34921f9a-5637-4420-ab4c-9beb34421909
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f997f1b49ff1aa0659a2409fdd945c6f96413b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-weekdone"></a><span data-ttu-id="34eb2-103">教學課程：Azure Active Directory 與 Weekdone 整合</span><span class="sxs-lookup"><span data-stu-id="34eb2-103">Tutorial: Azure Active Directory integration with Weekdone</span></span>

<span data-ttu-id="34eb2-104">在此教學課程中，您學會如何 toointegrate Weekdone 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="34eb2-104">In this tutorial, you learn how toointegrate Weekdone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="34eb2-105">與 Azure AD 整合 Weekdone 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="34eb2-105">Integrating Weekdone with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="34eb2-106">您可以控制存取 tooWeekdone Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="34eb2-106">You can control in Azure AD who has access tooWeekdone</span></span>
- <span data-ttu-id="34eb2-107">您可以啟用您的使用者 tooautomatically get 登入 tooWeekdone （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="34eb2-107">You can enable your users tooautomatically get signed-on tooWeekdone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="34eb2-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="34eb2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="34eb2-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="34eb2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34eb2-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="34eb2-110">Prerequisites</span></span>

<span data-ttu-id="34eb2-111">tooconfigure Weekdone 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="34eb2-111">tooconfigure Azure AD integration with Weekdone, you need hello following items:</span></span>

- <span data-ttu-id="34eb2-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="34eb2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="34eb2-113">已啟用 Weekdone 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="34eb2-113">A Weekdone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="34eb2-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="34eb2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="34eb2-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="34eb2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="34eb2-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="34eb2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="34eb2-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="34eb2-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="34eb2-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="34eb2-118">Scenario description</span></span>
<span data-ttu-id="34eb2-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="34eb2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="34eb2-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="34eb2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="34eb2-121">從 hello 圖庫加入 Weekdone</span><span class="sxs-lookup"><span data-stu-id="34eb2-121">Adding Weekdone from hello gallery</span></span>
2. <span data-ttu-id="34eb2-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="34eb2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-weekdone-from-hello-gallery"></a><span data-ttu-id="34eb2-123">從 hello 圖庫加入 Weekdone</span><span class="sxs-lookup"><span data-stu-id="34eb2-123">Adding Weekdone from hello gallery</span></span>
<span data-ttu-id="34eb2-124">tooconfigure hello 整合 Weekdone 到 Azure AD，您需要 tooadd Weekdone hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="34eb2-124">tooconfigure hello integration of Weekdone into Azure AD, you need tooadd Weekdone from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="34eb2-125">**tooadd Weekdone 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="34eb2-125">**tooadd Weekdone from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="34eb2-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="34eb2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="34eb2-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="34eb2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="34eb2-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="34eb2-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="34eb2-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="34eb2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="34eb2-133">在 [hello] 搜尋方塊中，輸入**Weekdone**。</span><span class="sxs-lookup"><span data-stu-id="34eb2-133">In hello search box, type **Weekdone**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_search.png)

5. <span data-ttu-id="34eb2-135">在 [hello [結果] 窗格中，選取 [ **Weekdone**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="34eb2-135">In hello results panel, select **Weekdone**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="34eb2-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="34eb2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="34eb2-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Weekdone 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="34eb2-138">In this section, you configure and test Azure AD single sign-on with Weekdone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="34eb2-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Weekdone 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="34eb2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Weekdone is tooa user in Azure AD.</span></span> <span data-ttu-id="34eb2-140">換句話說，Azure AD 使用者與 hello Weekdone 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="34eb2-140">In other words, a link relationship between an Azure AD user and hello related user in Weekdone needs toobe established.</span></span>

<span data-ttu-id="34eb2-141">Weekdone 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="34eb2-141">In Weekdone, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="34eb2-142">tooconfigure 及 Weekdone 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="34eb2-142">tooconfigure and test Azure AD single sign-on with Weekdone, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="34eb2-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="34eb2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="34eb2-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="34eb2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="34eb2-145">**[建立測試使用者 Weekdone](#creating-a-weekdone-test-user) ** -toohave 許 Simon Weekdone 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="34eb2-145">**[Creating a Weekdone test user](#creating-a-weekdone-test-user)** - toohave a counterpart of Britta Simon in Weekdone that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="34eb2-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="34eb2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="34eb2-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="34eb2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="34eb2-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="34eb2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="34eb2-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Weekdone 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="34eb2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Weekdone application.</span></span>

<span data-ttu-id="34eb2-150">**tooconfigure Azure AD 單一登入與 Weekdone，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="34eb2-150">**tooconfigure Azure AD single sign-on with Weekdone, perform hello following steps:**</span></span>

1. <span data-ttu-id="34eb2-151">在 Azure 入口網站上 hello hello **Weekdone**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="34eb2-151">In hello Azure portal, on hello **Weekdone** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="34eb2-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="34eb2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_samlbase.png)

3. <span data-ttu-id="34eb2-155">在 [hello **Weekdone 網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**IDP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="34eb2-155">On hello **Weekdone Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url1.png)

    <span data-ttu-id="34eb2-157">a.</span><span class="sxs-lookup"><span data-stu-id="34eb2-157">a.</span></span> <span data-ttu-id="34eb2-158">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="34eb2-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

    <span data-ttu-id="34eb2-159">b.</span><span class="sxs-lookup"><span data-stu-id="34eb2-159">b.</span></span> <span data-ttu-id="34eb2-160">在 [hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="34eb2-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

4. <span data-ttu-id="34eb2-161">按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="34eb2-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="34eb2-162">如果您想 tooconfigure hello 應用程式中的**SP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="34eb2-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url2.png)

    <span data-ttu-id="34eb2-164">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="34eb2-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://weekdone.com/a/<tenantname>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="34eb2-165">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="34eb2-165">These values are not real.</span></span> <span data-ttu-id="34eb2-166">更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="34eb2-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="34eb2-167">請連絡[Weekdone 用戶端支援小組](mailto:hello@weekdone.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="34eb2-167">Contact [Weekdone Client support team](mailto:hello@weekdone.com) tooget these values.</span></span> 

5. <span data-ttu-id="34eb2-168">在 [hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="34eb2-168">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_certificate.png) 

6. <span data-ttu-id="34eb2-170">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="34eb2-170">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-weekdone-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="34eb2-172">在 [hello **Weekdone 組態**區段中，按一下**設定 Weekdone** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="34eb2-172">On hello **Weekdone Configuration** section, click **Configure Weekdone** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="34eb2-173">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="34eb2-173">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_configure.png) 

8. <span data-ttu-id="34eb2-175">tooconfigure 單一登入上**Weekdone**端，您需要下載 toosend hello**中繼資料 XML、 登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**太[Weekdone 支援小組](mailto:hello@weekdone.com)。</span><span class="sxs-lookup"><span data-stu-id="34eb2-175">tooconfigure single sign-on on **Weekdone** side, you need toosend hello downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Weekdone support team](mailto:hello@weekdone.com).</span></span>

> [!TIP]
> <span data-ttu-id="34eb2-176">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="34eb2-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="34eb2-177">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="34eb2-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="34eb2-178">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="34eb2-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="34eb2-179">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="34eb2-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="34eb2-180">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="34eb2-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="34eb2-182">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="34eb2-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="34eb2-183">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="34eb2-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-weekdone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="34eb2-185">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="34eb2-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-weekdone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="34eb2-187">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="34eb2-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-weekdone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="34eb2-189">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="34eb2-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-weekdone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="34eb2-191">a.</span><span class="sxs-lookup"><span data-stu-id="34eb2-191">a.</span></span> <span data-ttu-id="34eb2-192">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="34eb2-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="34eb2-193">b.</span><span class="sxs-lookup"><span data-stu-id="34eb2-193">b.</span></span> <span data-ttu-id="34eb2-194">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="34eb2-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="34eb2-195">c.</span><span class="sxs-lookup"><span data-stu-id="34eb2-195">c.</span></span> <span data-ttu-id="34eb2-196">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="34eb2-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="34eb2-197">d.</span><span class="sxs-lookup"><span data-stu-id="34eb2-197">d.</span></span> <span data-ttu-id="34eb2-198">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="34eb2-198">Click **Create**.</span></span>
 
### <a name="creating-a-weekdone-test-user"></a><span data-ttu-id="34eb2-199">建立 Weekdone 測試使用者</span><span class="sxs-lookup"><span data-stu-id="34eb2-199">Creating a Weekdone test user</span></span>

<span data-ttu-id="34eb2-200">hello 本節目標在於 toocreate Weekdone 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="34eb2-200">hello objective of this section is toocreate a user called Britta Simon in Weekdone.</span></span> <span data-ttu-id="34eb2-201">Weekdone 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="34eb2-201">Weekdone supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="34eb2-202">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="34eb2-202">There is no action item for you in this section.</span></span> <span data-ttu-id="34eb2-203">如果尚未存在期間嘗試 tooaccess Weekdone，建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="34eb2-203">A new user is created during an attempt tooaccess Weekdone if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="34eb2-204">若要手動 toocreate 使用者，您需要 toocontact hello [Weekdone 用戶端支援小組](mailto:hello@weekdone.com)。</span><span class="sxs-lookup"><span data-stu-id="34eb2-204">If you need toocreate a user manually, you need toocontact hello [Weekdone Client support team](mailto:hello@weekdone.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="34eb2-205">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="34eb2-205">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="34eb2-206">在本節中，您可以授與存取 tooWeekdone 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="34eb2-206">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWeekdone.</span></span>

![指派使用者][200] 

<span data-ttu-id="34eb2-208">**tooassign 許 Simon tooWeekdone，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="34eb2-208">**tooassign Britta Simon tooWeekdone, perform hello following steps:**</span></span>

1. <span data-ttu-id="34eb2-209">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="34eb2-209">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="34eb2-211">在 [hello] 應用程式清單中，選取**Weekdone**。</span><span class="sxs-lookup"><span data-stu-id="34eb2-211">In hello applications list, select **Weekdone**.</span></span>

    ![設定單一登入](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_app.png) 

3. <span data-ttu-id="34eb2-213">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="34eb2-213">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="34eb2-215">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="34eb2-215">Click **Add** button.</span></span> <span data-ttu-id="34eb2-216">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="34eb2-216">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="34eb2-218">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="34eb2-218">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="34eb2-219">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="34eb2-219">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="34eb2-220">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="34eb2-220">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="34eb2-221">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="34eb2-221">Testing single sign-on</span></span>

<span data-ttu-id="34eb2-222">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="34eb2-222">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="34eb2-223">當您按一下 hello Weekdone 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Weekdone 應用程式。</span><span class="sxs-lookup"><span data-stu-id="34eb2-223">When you click hello Weekdone tile in hello Access Panel, you should get automatically signed-on tooyour Weekdone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="34eb2-224">其他資源</span><span class="sxs-lookup"><span data-stu-id="34eb2-224">Additional resources</span></span>

* [<span data-ttu-id="34eb2-225">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34eb2-225">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="34eb2-226">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="34eb2-226">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_203.png


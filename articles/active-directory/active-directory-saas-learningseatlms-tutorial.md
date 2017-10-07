---
title: "教學課程：Azure Active Directory 與 Learning Seat LMS 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 和學習基座 LMS 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bb056fcf-4135-478e-85b1-5015d1f07b85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: jeedes
ms.openlocfilehash: dc08aa444b85f35a4458768ac560ec663baa1c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-seat-lms"></a><span data-ttu-id="3ae2d-103">教學課程：Azure Active Directory 與 Learning Seat LMS 整合</span><span class="sxs-lookup"><span data-stu-id="3ae2d-103">Tutorial: Azure Active Directory integration with Learning Seat LMS</span></span>

<span data-ttu-id="3ae2d-104">在此教學課程中，您學會如何 toointegrate 學習基座 LMS 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-104">In this tutorial, you learn how toointegrate Learning Seat LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3ae2d-105">學習基座 LMS 整合與 Azure AD 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="3ae2d-105">Integrating Learning Seat LMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3ae2d-106">您可以控制存取 tooLearning 基座 LMS Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="3ae2d-106">You can control in Azure AD who has access tooLearning Seat LMS</span></span>
- <span data-ttu-id="3ae2d-107">您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooLearning 基座 LMS （單一登入）</span><span class="sxs-lookup"><span data-stu-id="3ae2d-107">You can enable your users tooautomatically get signed-on tooLearning Seat LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3ae2d-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="3ae2d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3ae2d-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="3ae2d-110">[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ae2d-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="3ae2d-111">Prerequisites</span></span>

<span data-ttu-id="3ae2d-112">tooconfigure Azure AD 與學習基座 LMS 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="3ae2d-112">tooconfigure Azure AD integration with Learning Seat LMS, you need hello following items:</span></span>

- <span data-ttu-id="3ae2d-113">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3ae2d-113">An Azure AD subscription</span></span>
- <span data-ttu-id="3ae2d-114">已啟用 Learning Seat LMS 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3ae2d-114">A Learning Seat LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3ae2d-115">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3ae2d-116">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="3ae2d-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3ae2d-117">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3ae2d-118">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3ae2d-119">案例描述</span><span class="sxs-lookup"><span data-stu-id="3ae2d-119">Scenario description</span></span>
<span data-ttu-id="3ae2d-120">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3ae2d-121">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="3ae2d-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3ae2d-122">從 hello 圖庫加入學習基座 LMS</span><span class="sxs-lookup"><span data-stu-id="3ae2d-122">Adding Learning Seat LMS from hello gallery</span></span>
2. <span data-ttu-id="3ae2d-123">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3ae2d-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-seat-lms-from-hello-gallery"></a><span data-ttu-id="3ae2d-124">從 hello 圖庫加入學習基座 LMS</span><span class="sxs-lookup"><span data-stu-id="3ae2d-124">Adding Learning Seat LMS from hello gallery</span></span>
<span data-ttu-id="3ae2d-125">tooconfigure hello 整合學習基座 LMS 到 Azure AD，您需要 tooadd 學習基座 LMS hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-125">tooconfigure hello integration of Learning Seat LMS into Azure AD, you need tooadd Learning Seat LMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3ae2d-126">**tooadd 學習基座 LMS 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3ae2d-126">**tooadd Learning Seat LMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ae2d-127">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3ae2d-129">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3ae2d-130">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-130">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="3ae2d-132">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="3ae2d-134">在 [hello] 搜尋方塊中，輸入**學習基座 LMS**。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-134">In hello search box, type **Learning Seat LMS**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_search.png)

5. <span data-ttu-id="3ae2d-136">在 hello 結果 窗格中，選取 **學習基座 LMS**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-136">In hello results panel, select **Learning Seat LMS**, and then click **Add** button tooadd hello application.</span></span>


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3ae2d-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3ae2d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3ae2d-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Learning Seat LMS 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-138">In this section, you configure and test Azure AD single sign-on with Learning Seat LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3ae2d-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中學習基座 LMS 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learning Seat LMS is tooa user in Azure AD.</span></span> <span data-ttu-id="3ae2d-140">換句話說，Azure AD 使用者與 hello 學習基座 LMS 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-140">In other words, a link relationship between an Azure AD user and hello related user in Learning Seat LMS needs toobe established.</span></span>

<span data-ttu-id="3ae2d-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username**學習基座 LMS 中。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Learning Seat LMS.</span></span>

<span data-ttu-id="3ae2d-142">tooconfigure 及學習基座 LMS 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="3ae2d-142">tooconfigure and test Azure AD single sign-on with Learning Seat LMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3ae2d-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3ae2d-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3ae2d-145">**[建立學習基座 LMS 測試使用者](#creating-a-learnconnect-test-user)** -toohave 許 Simon 是表示連結的 toohello Azure AD 使用者的學習基座 LMS 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-145">**[Creating a Learning Seat LMS test user](#creating-a-learnconnect-test-user)** - toohave a counterpart of Britta Simon in Learning Seat LMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3ae2d-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3ae2d-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3ae2d-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3ae2d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3ae2d-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並學習基座 LMS 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learning Seat LMS application.</span></span>

<span data-ttu-id="3ae2d-150">**學習基座 LMS，與 Azure AD 單一登入 tooconfigure 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3ae2d-150">**tooconfigure Azure AD single sign-on with Learning Seat LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ae2d-151">在 Azure 入口網站上 hello hello**學習基座 LMS**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-151">In hello Azure portal, on hello **Learning Seat LMS** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="3ae2d-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_samlbase.png)

3. <span data-ttu-id="3ae2d-155">在 hello**學習基座 LMS 網域和 Url**區段中，執行下列步驟，如果您想 tooconfigure hello 應用程式中的 hello **IDP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="3ae2d-155">On hello **Learning Seat LMS Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url.png)

    <span data-ttu-id="3ae2d-157">a.</span><span class="sxs-lookup"><span data-stu-id="3ae2d-157">a.</span></span> <span data-ttu-id="3ae2d-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="3ae2d-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com`</span></span>

    <span data-ttu-id="3ae2d-159">b.</span><span class="sxs-lookup"><span data-stu-id="3ae2d-159">b.</span></span> <span data-ttu-id="3ae2d-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span><span class="sxs-lookup"><span data-stu-id="3ae2d-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span></span>

4. <span data-ttu-id="3ae2d-161">請檢查**顯示進階的 URL 設定**，如果您想 tooconfigure hello 應用程式中的**SP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="3ae2d-161">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url2.png)

    <span data-ttu-id="3ae2d-163">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="3ae2d-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="3ae2d-164">這些值不是 hello 實際值。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-164">These values are not hello real values.</span></span> <span data-ttu-id="3ae2d-165">更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-165">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="3ae2d-166">請連絡[學習基座支援小組](http://help.learningseatlms.com/help)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-166">Contact [Learning Seat support team](http://help.learningseatlms.com/help) tooget these values.</span></span> 

5. <span data-ttu-id="3ae2d-167">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_certificate.png) 

6. <span data-ttu-id="3ae2d-169">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-169">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-learnconnect-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="3ae2d-171">tooconfigure 單一登入上**學習基座 LMS**端，您需要下載 toosend hello**中繼資料 XML**太[學習基座支援小組](http://help.learningseatlms.com/help)。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-171">tooconfigure single sign-on on **Learning Seat LMS** side, you need toosend hello downloaded **Metadata XML** too[Learning Seat support team](http://help.learningseatlms.com/help).</span></span>

> [!TIP]
> <span data-ttu-id="3ae2d-172">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="3ae2d-172">You can now read a concise version of these instructions inside hello [Azure  portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3ae2d-173">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3ae2d-174">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3ae2d-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3ae2d-175">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3ae2d-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="3ae2d-176">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="3ae2d-178">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3ae2d-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ae2d-179">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3ae2d-181">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3ae2d-183">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3ae2d-185">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3ae2d-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3ae2d-187">a.</span><span class="sxs-lookup"><span data-stu-id="3ae2d-187">a.</span></span> <span data-ttu-id="3ae2d-188">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3ae2d-189">b.</span><span class="sxs-lookup"><span data-stu-id="3ae2d-189">b.</span></span> <span data-ttu-id="3ae2d-190">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3ae2d-191">c.</span><span class="sxs-lookup"><span data-stu-id="3ae2d-191">c.</span></span> <span data-ttu-id="3ae2d-192">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3ae2d-193">d.</span><span class="sxs-lookup"><span data-stu-id="3ae2d-193">d.</span></span> <span data-ttu-id="3ae2d-194">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-seat-lms-test-user"></a><span data-ttu-id="3ae2d-195">建立 Learning Seat LMS 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3ae2d-195">Creating a Learning Seat LMS test user</span></span>

<span data-ttu-id="3ae2d-196">在本節中，您會在 Learning Seat LMS 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-196">In this section, you create a user called Britta Simon in Learning Seat LMS.</span></span> <span data-ttu-id="3ae2d-197">請連絡[學習基座支援小組](http://help.learningseatlms.com/help)與 hello 使用者資訊 tooadd hello 中所有使用者 hello 學習基座 LMS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-197">Contact [Learning Seat support team](http://help.learningseatlms.com/help) with all hello user information tooadd hello users in hello Learning Seat LMS application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3ae2d-198">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="3ae2d-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3ae2d-199">在本節中，您可以授與存取 tooLearning 基座 LMS 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearning Seat LMS.</span></span>

![指派使用者][200] 

<span data-ttu-id="3ae2d-201">**tooassign 許 Simon tooLearning 基座 LMS，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3ae2d-201">**tooassign Britta Simon tooLearning Seat LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ae2d-202">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="3ae2d-204">在 [hello] 應用程式清單中，選取**學習基座 LMS**。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-204">In hello applications list, select **Learning Seat LMS**.</span></span>

    ![設定單一登入](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_app.png) 

3. <span data-ttu-id="3ae2d-206">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="3ae2d-208">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-208">Click **Add** button.</span></span> <span data-ttu-id="3ae2d-209">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="3ae2d-211">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3ae2d-212">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3ae2d-213">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3ae2d-214">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="3ae2d-214">Testing single sign-on</span></span>

<span data-ttu-id="3ae2d-215">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> 

<span data-ttu-id="3ae2d-216">按一下的 hello 學習基座 LMS 磚中 hello 存取面板中，您將會自動登入 tooyour 學習基座 LMS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-216">Click hello Learning Seat LMS tile in hello Access Panel, you will be automatically signed-on tooyour Learning Seat LMS application.</span></span> <span data-ttu-id="3ae2d-217">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="3ae2d-217">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3ae2d-218">其他資源</span><span class="sxs-lookup"><span data-stu-id="3ae2d-218">Additional resources</span></span>

* [<span data-ttu-id="3ae2d-219">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3ae2d-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3ae2d-220">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="3ae2d-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_203.png


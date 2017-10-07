---
title: "教學課程：Azure Active Directory 與 Lesson.ly 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Lesson.ly 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c9dc6e6-5d85-4553-8a35-c7137064b928
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 23b339dcc26471b42aaa7e1baadcb42500d6b7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lessonly"></a><span data-ttu-id="0f856-103">教學課程：Azure Active Directory 與 Lesson.ly 整合</span><span class="sxs-lookup"><span data-stu-id="0f856-103">Tutorial: Azure Active Directory integration with Lesson.ly</span></span>

<span data-ttu-id="0f856-104">在此教學課程中，您學會如何 toointegrate Lesson.ly 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="0f856-104">In this tutorial, you learn how toointegrate Lesson.ly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0f856-105">與 Azure AD 整合 Lesson.ly 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="0f856-105">Integrating Lesson.ly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0f856-106">您可以控制存取 tooLesson.ly Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="0f856-106">You can control in Azure AD who has access tooLesson.ly</span></span>
- <span data-ttu-id="0f856-107">您可以啟用您的使用者 tooautomatically get 登入 tooLesson.ly （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="0f856-107">You can enable your users tooautomatically get signed-on tooLesson.ly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0f856-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0f856-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0f856-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="0f856-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f856-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="0f856-110">Prerequisites</span></span>

<span data-ttu-id="0f856-111">tooconfigure Lesson.ly 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="0f856-111">tooconfigure Azure AD integration with Lesson.ly, you need hello following items:</span></span>

- <span data-ttu-id="0f856-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0f856-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0f856-113">已啟用 Lesson.ly 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0f856-113">A Lesson.ly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0f856-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="0f856-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0f856-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="0f856-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0f856-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0f856-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0f856-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="0f856-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0f856-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="0f856-118">Scenario description</span></span>
<span data-ttu-id="0f856-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0f856-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0f856-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="0f856-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0f856-121">從 hello 圖庫加入 Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="0f856-121">Adding Lesson.ly from hello gallery</span></span>
2. <span data-ttu-id="0f856-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0f856-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lessonly-from-hello-gallery"></a><span data-ttu-id="0f856-123">從 hello 圖庫加入 Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="0f856-123">Adding Lesson.ly from hello gallery</span></span>
<span data-ttu-id="0f856-124">tooconfigure hello 整合 Lesson.ly 到 Azure AD，您需要 tooadd Lesson.ly hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f856-124">tooconfigure hello integration of Lesson.ly into Azure AD, you need tooadd Lesson.ly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0f856-125">**tooadd Lesson.ly 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0f856-125">**tooadd Lesson.ly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f856-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="0f856-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0f856-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0f856-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0f856-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0f856-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="0f856-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="0f856-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="0f856-133">在 [hello] 搜尋方塊中，輸入**Lesson.ly**。</span><span class="sxs-lookup"><span data-stu-id="0f856-133">In hello search box, type **Lesson.ly**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_search.png)

5. <span data-ttu-id="0f856-135">在 hello 結果 窗格中，選取  **Lesson.ly**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f856-135">In hello results panel, select **Lesson.ly**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0f856-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0f856-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0f856-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Lesson.ly 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0f856-138">In this section, you configure and test Azure AD single sign-on with Lesson.ly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0f856-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Lesson.ly 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="0f856-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lesson.ly is tooa user in Azure AD.</span></span> <span data-ttu-id="0f856-140">換句話說，Azure AD 使用者與 hello Lesson.ly 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="0f856-140">In other words, a link relationship between an Azure AD user and hello related user in Lesson.ly needs toobe established.</span></span>

<span data-ttu-id="0f856-141">Lesson.ly 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="0f856-141">In Lesson.ly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0f856-142">tooconfigure 及 Lesson.ly 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="0f856-142">tooconfigure and test Azure AD single sign-on with Lesson.ly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0f856-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="0f856-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0f856-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="0f856-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0f856-145">**[建立測試使用者 Lesson.ly](#creating-a-lessonly-test-user)**  -toohave 許 Simon Lesson.ly 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="0f856-145">**[Creating a Lesson.ly test user](#creating-a-lessonly-test-user)** - toohave a counterpart of Britta Simon in Lesson.ly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0f856-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0f856-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0f856-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="0f856-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0f856-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0f856-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0f856-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Lesson.ly 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="0f856-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lesson.ly application.</span></span>

<span data-ttu-id="0f856-150">**tooconfigure Azure AD 單一登入與 Lesson.ly，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0f856-150">**tooconfigure Azure AD single sign-on with Lesson.ly, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f856-151">在 Azure 入口網站上 hello hello **Lesson.ly**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="0f856-151">In hello Azure portal, on hello **Lesson.ly** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="0f856-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0f856-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_samlbase.png)

3. <span data-ttu-id="0f856-155">在 hello **Lesson.ly 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0f856-155">On hello **Lesson.ly Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_url.png)

    <span data-ttu-id="0f856-157">a.</span><span class="sxs-lookup"><span data-stu-id="0f856-157">a.</span></span> <span data-ttu-id="0f856-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="0f856-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/signin`|
    | `https://<companyname>.lessonly.com/signin`|

    >[!NOTE]
    ><span data-ttu-id="0f856-159">當參考泛型名稱**companyname**需要 toobe 以實際名稱取代。</span><span class="sxs-lookup"><span data-stu-id="0f856-159">When referencing a generic name that **companyname** needs toobe replaced by an actual name.</span></span>
    
    <span data-ttu-id="0f856-160">b.</span><span class="sxs-lookup"><span data-stu-id="0f856-160">b.</span></span> <span data-ttu-id="0f856-161">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="0f856-161">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/auth/saml/metadata`|
    | `https://<companyname>.lessonly.com/auth/saml/metadata`|

    > [!NOTE] 
    > <span data-ttu-id="0f856-162">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="0f856-162">These values are not real.</span></span> <span data-ttu-id="0f856-163">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="0f856-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0f856-164">請連絡[Lesson.ly 用戶端支援小組](mailto:dev@lessonly.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="0f856-164">Contact [Lesson.ly Client support team](mailto:dev@lessonly.com) tooget these values.</span></span> 

4. <span data-ttu-id="0f856-165">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="0f856-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_certificate.png)

5. <span data-ttu-id="0f856-167">hello Lesson.ly 應用程式需要特定格式，這需要您 tooadd 自訂屬性對應 tooyour hello SAML 判斷提示**SAML 權杖屬性**configuration.hello 下列螢幕擷取畫面顯示的範例此。</span><span class="sxs-lookup"><span data-stu-id="0f856-167">hello Lesson.ly application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.hello following screenshot shows an example for this.</span></span>

    ![設定單一登入](./media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_06.png)
           
6. <span data-ttu-id="0f856-169">在 hello**使用者屬性**hello 區段**單一登入** 對話方塊中，hello 上述影像中所示設定 SAML 權杖屬性和執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0f856-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>

    | <span data-ttu-id="0f856-170">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="0f856-170">Attribute Name</span></span>   | <span data-ttu-id="0f856-171">屬性值</span><span class="sxs-lookup"><span data-stu-id="0f856-171">Attribute Value</span></span> |
    | ---------------  | ----------------|
    | <span data-ttu-id="0f856-172">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="0f856-172">urn:oid:2.5.4.42</span></span> |<span data-ttu-id="0f856-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="0f856-173">user.givenname</span></span> |
    | <span data-ttu-id="0f856-174">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="0f856-174">urn:oid:2.5.4.4</span></span>  |<span data-ttu-id="0f856-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="0f856-175">user.surname</span></span> |
    | <span data-ttu-id="0f856-176">urn:oid:0.9.2342.19200300.1001.3</span><span class="sxs-lookup"><span data-stu-id="0f856-176">urn:oid:0.9.2342.19200300.1001.3</span></span> |<span data-ttu-id="0f856-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="0f856-177">user.mail</span></span> |

    <span data-ttu-id="0f856-178">a.</span><span class="sxs-lookup"><span data-stu-id="0f856-178">a.</span></span> <span data-ttu-id="0f856-179">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0f856-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_04.png)

    ![設定單一登入](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="0f856-182">b.</span><span class="sxs-lookup"><span data-stu-id="0f856-182">b.</span></span> <span data-ttu-id="0f856-183">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="0f856-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="0f856-184">c.</span><span class="sxs-lookup"><span data-stu-id="0f856-184">c.</span></span> <span data-ttu-id="0f856-185">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="0f856-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="0f856-186">d.</span><span class="sxs-lookup"><span data-stu-id="0f856-186">d.</span></span> <span data-ttu-id="0f856-187">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="0f856-187">Click **Ok**.</span></span>     

7. <span data-ttu-id="0f856-188">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="0f856-188">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-lessonly-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="0f856-190">在 hello **Lesson.ly 組態**區段中，按一下**設定 Lesson.ly** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="0f856-190">On hello **Lesson.ly Configuration** section, click **Configure Lesson.ly** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0f856-191">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="0f856-191">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_configure.png)

9. <span data-ttu-id="0f856-193">tooconfigure 單一登入上**Lesson.ly**端，您需要下載 toosend hello **Certificate(Base64)**和**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**太[Lesson.ly 支援小組](mailto:dev@lessonly.com)。</span><span class="sxs-lookup"><span data-stu-id="0f856-193">tooconfigure single sign-on on **Lesson.ly** side, you need toosend hello downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

> [!TIP]
> <span data-ttu-id="0f856-194">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="0f856-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0f856-195">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="0f856-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0f856-196">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0f856-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0f856-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0f856-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="0f856-198">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="0f856-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="0f856-200">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0f856-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f856-201">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="0f856-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lessonly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0f856-203">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="0f856-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lessonly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0f856-205">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="0f856-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lessonly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0f856-207">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0f856-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lessonly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0f856-209">a.</span><span class="sxs-lookup"><span data-stu-id="0f856-209">a.</span></span> <span data-ttu-id="0f856-210">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="0f856-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0f856-211">b.</span><span class="sxs-lookup"><span data-stu-id="0f856-211">b.</span></span> <span data-ttu-id="0f856-212">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="0f856-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0f856-213">c.</span><span class="sxs-lookup"><span data-stu-id="0f856-213">c.</span></span> <span data-ttu-id="0f856-214">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="0f856-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0f856-215">d.</span><span class="sxs-lookup"><span data-stu-id="0f856-215">d.</span></span> <span data-ttu-id="0f856-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0f856-216">Click **Create**.</span></span>
 
### <a name="creating-a-lessonly-test-user"></a><span data-ttu-id="0f856-217">建立 Lesson.ly 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0f856-217">Creating a Lesson.ly test user</span></span>

<span data-ttu-id="0f856-218">hello 本節目標在於 toocreate Lesson.ly 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="0f856-218">hello objective of this section is toocreate a user called Britta Simon in Lesson.ly.</span></span> <span data-ttu-id="0f856-219">Lesson.ly 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="0f856-219">Lesson.ly supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="0f856-220">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="0f856-220">There is no action item for you in this section.</span></span> <span data-ttu-id="0f856-221">如果尚未存在，將會嘗試 tooaccess Lesson.ly 期間建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="0f856-221">A new user will be created during an attempt tooaccess Lesson.ly if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="0f856-222">若要手動 toocreate 使用者，您需要 toocontact hello [Lesson.ly 支援小組](mailto:dev@lessonly.com)。</span><span class="sxs-lookup"><span data-stu-id="0f856-222">If you need toocreate an user manually, you need toocontact hello [Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0f856-223">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="0f856-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0f856-224">在本節中，您可以授與存取 tooLesson.ly 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0f856-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLesson.ly.</span></span>

![指派使用者][200] 

<span data-ttu-id="0f856-226">**tooassign 許 Simon tooLesson.ly，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0f856-226">**tooassign Britta Simon tooLesson.ly, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f856-227">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0f856-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="0f856-229">在 [hello] 應用程式清單中，選取**Lesson.ly**。</span><span class="sxs-lookup"><span data-stu-id="0f856-229">In hello applications list, select **Lesson.ly**.</span></span>

    ![設定單一登入](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_app.png) 

3. <span data-ttu-id="0f856-231">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="0f856-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="0f856-233">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0f856-233">Click **Add** button.</span></span> <span data-ttu-id="0f856-234">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0f856-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="0f856-236">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="0f856-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0f856-237">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0f856-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0f856-238">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0f856-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0f856-239">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="0f856-239">Testing single sign-on</span></span>

<span data-ttu-id="0f856-240">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="0f856-240">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0f856-241">當您按一下 hello Lesson.ly 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Lesson.ly 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f856-241">When you click hello Lesson.ly tile in hello Access Panel, you should get automatically signed-on tooyour Lesson.ly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0f856-242">其他資源</span><span class="sxs-lookup"><span data-stu-id="0f856-242">Additional resources</span></span>

* [<span data-ttu-id="0f856-243">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f856-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0f856-244">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="0f856-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_203.png


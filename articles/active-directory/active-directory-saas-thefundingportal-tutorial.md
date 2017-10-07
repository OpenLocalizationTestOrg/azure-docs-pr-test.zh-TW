---
title: "教學課程： Azure Active Directory 整合與 hello 資金入口網站 |Microsoft 文件"
description: "了解如何 tooconfigure 單一登入 Azure Active Directory 之間以及 hello 資金入口網站。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4663cc8a-976a-4c6c-b3b4-1e5df9b66744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 9f4329e02f91eb6d8034f17646ac7d15afe503e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hello-funding-portal"></a><span data-ttu-id="c5b97-103">教學課程： Azure Active Directory 整合與 hello 資金入口網站</span><span class="sxs-lookup"><span data-stu-id="c5b97-103">Tutorial: Azure Active Directory integration with hello Funding Portal</span></span>

<span data-ttu-id="c5b97-104">在本教學課程中，您學會如何 toointegrate hello 資金的入口網站與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="c5b97-104">In this tutorial, you learn how toointegrate hello Funding Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5b97-105">整合 hello 資金網站與 Azure AD 可讓您 hello 下列優點：</span><span class="sxs-lookup"><span data-stu-id="c5b97-105">Integrating hello Funding Portal with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c5b97-106">您可以控制存取 toohello Funding 入口網站的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="c5b97-106">You can control in Azure AD who has access toohello Funding Portal</span></span>
- <span data-ttu-id="c5b97-107">您可以啟用您的使用者 tooautomatically get 登入 toohello （單一登入） 具有其 Azure AD 帳戶的 Funding 入口網站</span><span class="sxs-lookup"><span data-stu-id="c5b97-107">You can enable your users tooautomatically get signed-on toohello Funding Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c5b97-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c5b97-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c5b97-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="c5b97-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5b97-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="c5b97-110">Prerequisites</span></span>

<span data-ttu-id="c5b97-111">tooconfigure Azure AD 整合以 hello Funding 入口網站，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="c5b97-111">tooconfigure Azure AD integration with hello Funding Portal, you need hello following items:</span></span>

- <span data-ttu-id="c5b97-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c5b97-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c5b97-113">Hello 資金入口網站單一登入啟用的訂閱</span><span class="sxs-lookup"><span data-stu-id="c5b97-113">A hello Funding Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c5b97-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="c5b97-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c5b97-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="c5b97-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c5b97-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="c5b97-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c5b97-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="c5b97-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5b97-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="c5b97-118">Scenario description</span></span>
<span data-ttu-id="c5b97-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c5b97-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c5b97-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="c5b97-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5b97-121">新增 hello Funding 入口網站，從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="c5b97-121">Adding hello Funding Portal from hello gallery</span></span>
2. <span data-ttu-id="c5b97-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c5b97-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hello-funding-portal-from-hello-gallery"></a><span data-ttu-id="c5b97-123">新增 hello Funding 入口網站，從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="c5b97-123">Adding hello Funding Portal from hello gallery</span></span>
<span data-ttu-id="c5b97-124">tooconfigure hello 整合 hello Funding 入口網站至 Azure AD，您需要 tooadd hello Funding 入口網站，從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單。</span><span class="sxs-lookup"><span data-stu-id="c5b97-124">tooconfigure hello integration of hello Funding Portal into Azure AD, you need tooadd hello Funding Portal from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c5b97-125">**tooadd hello 資金入口網站，從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c5b97-125">**tooadd hello Funding Portal from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5b97-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c5b97-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c5b97-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c5b97-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c5b97-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c5b97-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="c5b97-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5b97-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="c5b97-133">在 [hello] 搜尋方塊中，輸入**hello 資金入口網站**。</span><span class="sxs-lookup"><span data-stu-id="c5b97-133">In hello search box, type **hello Funding Portal**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_search.png)

5. <span data-ttu-id="c5b97-135">在 [hello [結果] 窗格中，選取 [ **hello 資金入口網站**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c5b97-135">In hello results panel, select **hello Funding Portal**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c5b97-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c5b97-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c5b97-138">在本節中，您可以設定及測試 Azure AD 單一登入以 hello 資金入口網站會根據稱為 「 許 Simon"的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="c5b97-138">In this section, you configure and test Azure AD single sign-on with hello Funding Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c5b97-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 hello 資金入口網站是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="c5b97-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in hello Funding Portal is tooa user in Azure AD.</span></span> <span data-ttu-id="c5b97-140">換句話說，Azure AD 使用者與 hello hello 中相關的使用者之間的連結關聯性資金入口網站需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="c5b97-140">In other words, a link relationship between an Azure AD user and hello related user in hello Funding Portal needs toobe established.</span></span>

<span data-ttu-id="c5b97-141">在 [hello 資金入口網站中的 hello hello 值指派**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="c5b97-141">In hello Funding Portal, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c5b97-142">tooconfigure 和測試 Azure AD 單一登入以 hello Funding 入口網站，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="c5b97-142">tooconfigure and test Azure AD single sign-on with hello Funding Portal, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c5b97-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="c5b97-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c5b97-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="c5b97-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c5b97-145">**[建立 hello 資金入口網站測試使用者](#creating-the-funding-portal-test-user)** -toohave hello Funding 入口網站，表示連結的 toohello Azure AD 使用者的許 Simon 的對應項目。</span><span class="sxs-lookup"><span data-stu-id="c5b97-145">**[Creating hello Funding Portal test user](#creating-the-funding-portal-test-user)** - toohave a counterpart of Britta Simon in hello Funding Portal that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c5b97-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c5b97-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5b97-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="c5b97-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c5b97-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c5b97-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c5b97-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您 hello 資金入口網站應用程式中。</span><span class="sxs-lookup"><span data-stu-id="c5b97-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your hello Funding Portal application.</span></span>

<span data-ttu-id="c5b97-150">**tooconfigure Azure AD 單一登入與 hello 資金入口網站中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c5b97-150">**tooconfigure Azure AD single sign-on with hello Funding Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5b97-151">在 Azure 入口網站上 hello hello **hello 資金入口網站**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="c5b97-151">In hello Azure portal, on hello **hello Funding Portal** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="c5b97-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c5b97-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_samlbase.png)

3. <span data-ttu-id="c5b97-155">在 [hello **hello 資金入口網站的網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c5b97-155">On hello **hello Funding Portal Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_url.png)

    <span data-ttu-id="c5b97-157">a.</span><span class="sxs-lookup"><span data-stu-id="c5b97-157">a.</span></span> <span data-ttu-id="c5b97-158">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.regenteducation.net/`</span><span class="sxs-lookup"><span data-stu-id="c5b97-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.regenteducation.net/`</span></span>

    <span data-ttu-id="c5b97-159">b.</span><span class="sxs-lookup"><span data-stu-id="c5b97-159">b.</span></span> <span data-ttu-id="c5b97-160">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.regenteducation.net`</span><span class="sxs-lookup"><span data-stu-id="c5b97-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.regenteducation.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c5b97-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="c5b97-161">These values are not real.</span></span> <span data-ttu-id="c5b97-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="c5b97-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c5b97-163">請連絡[hello 資金入口網站用戶端支援小組](mailto:info@regenteducation.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="c5b97-163">Contact [hello Funding Portal Client support team](mailto:info@regenteducation.com) tooget these values.</span></span> 

4. <span data-ttu-id="c5b97-164">hello 資金入口網站應用程式必須要有 hello SAML 判斷提示 toocontain 名為"externalId1"屬性。</span><span class="sxs-lookup"><span data-stu-id="c5b97-164">hello Funding Portal application expects hello SAML assertions toocontain an attribute named "externalId1".</span></span> <span data-ttu-id="c5b97-165">hello"externalId1"值應該是可辨識的 studentID。</span><span class="sxs-lookup"><span data-stu-id="c5b97-165">hello value of "externalId1" should be a recognized studentID.</span></span> <span data-ttu-id="c5b97-166">設定此應用程式的 hello"externalId1"宣告。</span><span class="sxs-lookup"><span data-stu-id="c5b97-166">Configure hello "externalId1" claim for this application.</span></span> <span data-ttu-id="c5b97-167">您可以從 hello 管理這些屬性的 hello 值**使用者屬性**hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c5b97-167">You can manage hello values of these attributes from hello **User Attributes** of hello application.</span></span> <span data-ttu-id="c5b97-168">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="c5b97-168">hello following screenshot shows an example for this.</span></span>

    ![設定單一登入](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_attribute.png)

5. <span data-ttu-id="c5b97-170">在 [hello**使用者屬性**hello] 區段**單一登入**] 對話方塊中，hello 映像中所示設定 SAML 權杖屬性並執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c5b97-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>

    | <span data-ttu-id="c5b97-171">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="c5b97-171">Attribute Name</span></span> | <span data-ttu-id="c5b97-172">屬性值</span><span class="sxs-lookup"><span data-stu-id="c5b97-172">Attribute Value</span></span> |
    | ------------------- | ---------------- |
    | <span data-ttu-id="c5b97-173">externalId1</span><span class="sxs-lookup"><span data-stu-id="c5b97-173">externalId1</span></span> | <span data-ttu-id="c5b97-174">user.extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="c5b97-174">user.extensionattribute1</span></span> |

    <span data-ttu-id="c5b97-175">a.</span><span class="sxs-lookup"><span data-stu-id="c5b97-175">a.</span></span> <span data-ttu-id="c5b97-176">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c5b97-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_04.png)

    ![設定單一登入](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="c5b97-179">b.</span><span class="sxs-lookup"><span data-stu-id="c5b97-179">b.</span></span> <span data-ttu-id="c5b97-180">在 [hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="c5b97-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="c5b97-181">c.</span><span class="sxs-lookup"><span data-stu-id="c5b97-181">c.</span></span> <span data-ttu-id="c5b97-182">從 hello**屬性值**清單中，您想要實作 toouse 選取 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="c5b97-182">From hello **Attribute Value** list, select hello attribute you want toouse for your implementation.</span></span> <span data-ttu-id="c5b97-183">例如，如果您已在 hello ExtensionAttribute1 儲存 hello StudentID 值，然後選取 user.extensionattribute1。</span><span class="sxs-lookup"><span data-stu-id="c5b97-183">For example, if you have stored hello StudentID value in hello ExtensionAttribute1, then select user.extensionattribute1.</span></span>
    
    <span data-ttu-id="c5b97-184">d.</span><span class="sxs-lookup"><span data-stu-id="c5b97-184">d.</span></span> <span data-ttu-id="c5b97-185">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="c5b97-185">Click **Ok**.</span></span>
 
6. <span data-ttu-id="c5b97-186">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="c5b97-186">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_certificate.png) 

7. <span data-ttu-id="c5b97-188">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5b97-188">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c5b97-190">tooconfigure 單一登入上**hello 資金入口網站**端，您需要下載 toosend hello**中繼資料 XML**太[hello 資金入口網站支援小組](mailto:info@regenteducation.com)。</span><span class="sxs-lookup"><span data-stu-id="c5b97-190">tooconfigure single sign-on on **hello Funding Portal** side, you need toosend hello downloaded **Metadata XML** too[hello Funding Portal support team](mailto:info@regenteducation.com).</span></span> <span data-ttu-id="c5b97-191">設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。</span><span class="sxs-lookup"><span data-stu-id="c5b97-191">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c5b97-192">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="c5b97-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c5b97-193">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="c5b97-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c5b97-194">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c5b97-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c5b97-195">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c5b97-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="c5b97-196">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="c5b97-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="c5b97-198">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c5b97-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5b97-199">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c5b97-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c5b97-201">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="c5b97-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c5b97-203">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="c5b97-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c5b97-205">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c5b97-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c5b97-207">a.</span><span class="sxs-lookup"><span data-stu-id="c5b97-207">a.</span></span> <span data-ttu-id="c5b97-208">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="c5b97-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c5b97-209">b.</span><span class="sxs-lookup"><span data-stu-id="c5b97-209">b.</span></span> <span data-ttu-id="c5b97-210">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="c5b97-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c5b97-211">c.</span><span class="sxs-lookup"><span data-stu-id="c5b97-211">c.</span></span> <span data-ttu-id="c5b97-212">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="c5b97-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c5b97-213">d.</span><span class="sxs-lookup"><span data-stu-id="c5b97-213">d.</span></span> <span data-ttu-id="c5b97-214">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="c5b97-214">Click **Create**.</span></span>
 
### <a name="creating-hello-funding-portal-test-user"></a><span data-ttu-id="c5b97-215">建立 hello 資金入口網站測試使用者</span><span class="sxs-lookup"><span data-stu-id="c5b97-215">Creating hello Funding Portal test user</span></span>

<span data-ttu-id="c5b97-216">在本節中，您可以建立稱為許 Simon hello Funding 入口網站中的使用者。</span><span class="sxs-lookup"><span data-stu-id="c5b97-216">In this section, you create a user called Britta Simon in hello Funding Portal.</span></span> <span data-ttu-id="c5b97-217">使用[hello 資金入口網站支援小組](mailto:info@regenteducation.com)tooadd hello 測試使用者並啟用 SSO。</span><span class="sxs-lookup"><span data-stu-id="c5b97-217">Work with [hello Funding Portal support team](mailto:info@regenteducation.com) tooadd hello test user and enable SSO.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c5b97-218">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="c5b97-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c5b97-219">在本節中，您可以授與存取 toohello Funding 入口網站啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c5b97-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access toohello Funding Portal.</span></span>

![指派使用者][200] 

<span data-ttu-id="c5b97-221">**tooassign 許 Simon toohello Funding 入口網站中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c5b97-221">**tooassign Britta Simon toohello Funding Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5b97-222">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c5b97-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="c5b97-224">在 [hello] 應用程式清單中，選取**hello 資金入口網站**。</span><span class="sxs-lookup"><span data-stu-id="c5b97-224">In hello applications list, select **hello Funding Portal**.</span></span>

    ![設定單一登入](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_app.png) 

3. <span data-ttu-id="c5b97-226">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="c5b97-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="c5b97-228">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5b97-228">Click **Add** button.</span></span> <span data-ttu-id="c5b97-229">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="c5b97-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="c5b97-231">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="c5b97-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c5b97-232">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5b97-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c5b97-233">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5b97-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c5b97-234">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="c5b97-234">Testing single sign-on</span></span>

<span data-ttu-id="c5b97-235">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="c5b97-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c5b97-236">當您按一下 hello 存取面板中的 hello hello 資金入口網站磚時，您應該取得自動登入 tooyour hello 資金入口網站應用程式。</span><span class="sxs-lookup"><span data-stu-id="c5b97-236">When you click hello hello Funding Portal tile in hello Access Panel, you should get automatically signed-on tooyour hello Funding Portal application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c5b97-237">其他資源</span><span class="sxs-lookup"><span data-stu-id="c5b97-237">Additional resources</span></span>

* [<span data-ttu-id="c5b97-238">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5b97-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c5b97-239">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="c5b97-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_203.png


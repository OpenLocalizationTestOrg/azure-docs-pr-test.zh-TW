---
title: "教學課程：Azure Active Directory 與 Blackboard Learn 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與矩形色塊學習之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: e94cdd6eaf876d4f66bdd783c442dc468f104e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="99575-103">教學課程：Azure Active Directory 與 Blackboard Learn 整合</span><span class="sxs-lookup"><span data-stu-id="99575-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="99575-104">在此教學課程中，您學會如何 toointegrate 矩形色塊深入了解與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="99575-104">In this tutorial, you learn how toointegrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="99575-105">整合與 Azure AD 的了解矩形色塊可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="99575-105">Integrating Blackboard Learn with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="99575-106">您可以控制存取 tooBlackboard 深入了解 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="99575-106">You can control in Azure AD who has access tooBlackboard Learn</span></span>
- <span data-ttu-id="99575-107">您可以啟用您使用者 tooautomatically get 登入 tooBlackboard （單一登入） 的深入了解使用其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="99575-107">You can enable your users tooautomatically get signed-on tooBlackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="99575-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="99575-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="99575-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="99575-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99575-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="99575-110">Prerequisites</span></span>

<span data-ttu-id="99575-111">tooconfigure 與矩形色塊深入了解 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="99575-111">tooconfigure Azure AD integration with Blackboard Learn, you need hello following items:</span></span>

- <span data-ttu-id="99575-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="99575-112">An Azure AD subscription</span></span>
- <span data-ttu-id="99575-113">已啟用 Blackboard Learn 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="99575-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="99575-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="99575-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="99575-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="99575-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="99575-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="99575-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="99575-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="99575-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="99575-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="99575-118">Scenario description</span></span>
<span data-ttu-id="99575-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="99575-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="99575-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="99575-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="99575-121">加入矩形色塊深入了解從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="99575-121">Adding Blackboard Learn from hello gallery</span></span>
2. <span data-ttu-id="99575-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="99575-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-hello-gallery"></a><span data-ttu-id="99575-123">加入矩形色塊深入了解從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="99575-123">Adding Blackboard Learn from hello gallery</span></span>
<span data-ttu-id="99575-124">tooconfigure hello 整合的矩形色塊深入了解 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd 矩形色塊深入了解。</span><span class="sxs-lookup"><span data-stu-id="99575-124">tooconfigure hello integration of Blackboard Learn into Azure AD, you need tooadd Blackboard Learn from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="99575-125">**tooadd 矩形色塊深入了解從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="99575-125">**tooadd Blackboard Learn from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="99575-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="99575-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="99575-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="99575-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="99575-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="99575-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="99575-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="99575-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="99575-133">在 [hello] 搜尋方塊中，輸入**矩形色塊學習**。</span><span class="sxs-lookup"><span data-stu-id="99575-133">In hello search box, type **Blackboard Learn**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

5. <span data-ttu-id="99575-135">在 [hello [結果] 窗格中，選取 [**矩形色塊深入了解**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="99575-135">In hello results panel, select **Blackboard Learn**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="99575-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="99575-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="99575-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Blackboard Learn 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="99575-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="99575-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中深入了解矩形色塊是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="99575-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Blackboard Learn is tooa user in Azure AD.</span></span> <span data-ttu-id="99575-140">換句話說，Azure AD 使用者與 hello 中 （矩形色塊） 深入了解相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="99575-140">In other words, a link relationship between an Azure AD user and hello related user in Blackboard Learn needs toobe established.</span></span>

<span data-ttu-id="99575-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**使用者名稱**深入了解矩形色塊中。</span><span class="sxs-lookup"><span data-stu-id="99575-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="99575-142">tooconfigure 及與矩形色塊深入了解 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="99575-142">tooconfigure and test Azure AD single sign-on with Blackboard Learn, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="99575-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="99575-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="99575-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="99575-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="99575-145">**[建立矩形色塊深入了解測試使用者](#creating-a-blackboard-learn-test-user)** -toohave 許 Simon，了解連結的 toohello Azure AD 使用者表示的矩形色塊中對應項目。</span><span class="sxs-lookup"><span data-stu-id="99575-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - toohave a counterpart of Britta Simon in Blackboard Learn that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="99575-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="99575-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="99575-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="99575-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="99575-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="99575-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="99575-149">在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入矩形色塊深入了解應用程式中。</span><span class="sxs-lookup"><span data-stu-id="99575-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="99575-150">**tooconfigure Azure AD 單一登入與矩形色塊瞭解，請執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="99575-150">**tooconfigure Azure AD single sign-on with Blackboard Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="99575-151">在 Azure 入口網站上 hello hello**矩形色塊學習**應用程式整合頁面上，按一下**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="99575-151">In hello Azure portal, on hello **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="99575-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="99575-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

3. <span data-ttu-id="99575-155">在 [hello**矩形色塊深入了解網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="99575-155">On hello **Blackboard Learn Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="99575-157">a.</span><span class="sxs-lookup"><span data-stu-id="99575-157">a.</span></span> <span data-ttu-id="99575-158">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.blackboard.com/`</span><span class="sxs-lookup"><span data-stu-id="99575-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="99575-159">b.</span><span class="sxs-lookup"><span data-stu-id="99575-159">b.</span></span> <span data-ttu-id="99575-160">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span><span class="sxs-lookup"><span data-stu-id="99575-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="99575-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="99575-161">These values are not real.</span></span> <span data-ttu-id="99575-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="99575-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="99575-163">請連絡[矩形色塊深入了解用戶端支援小組](https://www.blackboard.com/support/index.aspx)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="99575-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) tooget these values.</span></span> 

4. <span data-ttu-id="99575-164">矩形色塊深入了解應用程式預期 hello SAML 判斷提示，以特定格式。</span><span class="sxs-lookup"><span data-stu-id="99575-164">Blackboard Learn application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="99575-165">設定下列宣告為此應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="99575-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="99575-166">您可以從 hello 管理這些屬性的 hello 值**使用者屬性**應用程式整合頁面上的一節。</span><span class="sxs-lookup"><span data-stu-id="99575-166">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="99575-167">下列螢幕擷取畫面的 hello 顯示資訊，請參閱範例。</span><span class="sxs-lookup"><span data-stu-id="99575-167">hello following screenshot shows an example about it.</span></span>

    ![設定單一登入](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="99575-169">在 [hello**使用者屬性**區段**單一登入**] 對話方塊中，hello 映像中所示設定 SAML 權杖屬性並執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="99575-169">In hello **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in hello image and perform hello following steps.</span></span> <span data-ttu-id="99575-170">我們已對應 hello Userprincipalname 做 hello 唯一的使用者屬性，但您可以將它對應 toohello 適當的值，其中唯一區別 hello 組織中的 hello 使用者，並對應至 tooBlackboard 深入了解使用者名稱欄位。</span><span class="sxs-lookup"><span data-stu-id="99575-170">We have mapped hello Userprincipalname as hello unique user attribute here but you can map it toohello appropriate value, which uniquely distinguishes hello user in hello organization and that maps tooBlackboard Learn username field.</span></span>
           
    | <span data-ttu-id="99575-171">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="99575-171">Attribute Name</span></span> | <span data-ttu-id="99575-172">屬性值</span><span class="sxs-lookup"><span data-stu-id="99575-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="99575-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="99575-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="99575-174">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="99575-174">user.userprincipalname</span></span> |

    <span data-ttu-id="99575-175">a.</span><span class="sxs-lookup"><span data-stu-id="99575-175">a.</span></span> <span data-ttu-id="99575-176">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="99575-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![設定單一登入](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="99575-179">b.</span><span class="sxs-lookup"><span data-stu-id="99575-179">b.</span></span> <span data-ttu-id="99575-180">在 [hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="99575-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="99575-181">c.</span><span class="sxs-lookup"><span data-stu-id="99575-181">c.</span></span> <span data-ttu-id="99575-182">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="99575-182">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="99575-183">d.</span><span class="sxs-lookup"><span data-stu-id="99575-183">d.</span></span> <span data-ttu-id="99575-184">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="99575-184">Click **Ok**.</span></span>

4. <span data-ttu-id="99575-185">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="99575-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

7. <span data-ttu-id="99575-187">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="99575-187">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="99575-189">在 hello**矩形色塊深入了解組態**區段中，按一下**設定矩形色塊學習**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="99575-189">On hello **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="99575-190">複製 hello **SAML 實體識別碼**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="99575-190">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

9. <span data-ttu-id="99575-192">tooconfigure 單一登入上**矩形色塊學習**端，您需要下載 toosend hello**中繼資料 XML**和**SAML 實體識別碼**太[矩形色塊深入了解支援](https://www.blackboard.com/support/index.aspx)。</span><span class="sxs-lookup"><span data-stu-id="99575-192">tooconfigure single sign-on on **Blackboard Learn** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID** too[Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="99575-193">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="99575-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="99575-194">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="99575-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="99575-195">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="99575-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="99575-196">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="99575-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="99575-197">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="99575-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="99575-199">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="99575-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="99575-200">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="99575-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="99575-202">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="99575-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="99575-204">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="99575-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="99575-206">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="99575-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="99575-208">a.</span><span class="sxs-lookup"><span data-stu-id="99575-208">a.</span></span> <span data-ttu-id="99575-209">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="99575-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="99575-210">b.</span><span class="sxs-lookup"><span data-stu-id="99575-210">b.</span></span> <span data-ttu-id="99575-211">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**許 Simon。</span><span class="sxs-lookup"><span data-stu-id="99575-211">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="99575-212">c.</span><span class="sxs-lookup"><span data-stu-id="99575-212">c.</span></span> <span data-ttu-id="99575-213">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="99575-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="99575-214">d.</span><span class="sxs-lookup"><span data-stu-id="99575-214">d.</span></span> <span data-ttu-id="99575-215">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="99575-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="99575-216">建立 Blackboard Learn 測試使用者</span><span class="sxs-lookup"><span data-stu-id="99575-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="99575-217">在本節中，您會在 Blackboard Learn 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="99575-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="99575-218">Blackboard Learn 應用程式支援即時使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="99575-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="99575-219">請確定您擁有 hello > 一節中所述設定 hello 宣告**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)**</span><span class="sxs-lookup"><span data-stu-id="99575-219">Make sure that you have configured hello claims as described in hello section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="99575-220">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="99575-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="99575-221">在本節中，您可以授與存取 tooBlackboard 深入了解啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="99575-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlackboard Learn.</span></span>

![指派使用者][200] 

<span data-ttu-id="99575-223">**tooassign 許 Simon tooBlackboard 深入了解，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="99575-223">**tooassign Britta Simon tooBlackboard Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="99575-224">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="99575-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="99575-226">在 [hello] 應用程式清單中，選取**矩形色塊學習**。</span><span class="sxs-lookup"><span data-stu-id="99575-226">In hello applications list, select **Blackboard Learn**.</span></span>

    ![設定單一登入](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

3. <span data-ttu-id="99575-228">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="99575-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="99575-230">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="99575-230">Click **Add** button.</span></span> <span data-ttu-id="99575-231">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="99575-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="99575-233">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="99575-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="99575-234">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="99575-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="99575-235">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="99575-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="99575-236">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="99575-236">Testing single sign-on</span></span>

<span data-ttu-id="99575-237">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="99575-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="99575-238">當您按一下 hello 矩形色塊學習並排顯示 hello 存取面板中的時，您應該取得自動登入 tooyour 矩形色塊深入了解應用程式。</span><span class="sxs-lookup"><span data-stu-id="99575-238">When you click hello Blackboard Learn tile in hello Access Panel, you should get automatically signed-on tooyour Blackboard Learn application.</span></span> <span data-ttu-id="99575-239">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="99575-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="99575-240">其他資源</span><span class="sxs-lookup"><span data-stu-id="99575-240">Additional resources</span></span>

* [<span data-ttu-id="99575-241">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99575-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="99575-242">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="99575-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png


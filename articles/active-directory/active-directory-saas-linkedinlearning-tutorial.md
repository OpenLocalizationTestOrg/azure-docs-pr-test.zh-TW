---
title: "教學課程：Azure Active Directory 與 LinkedIn Learning 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 LinkedIn 學習之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 14610a25132ed0ccf5892cad6ccc4e1ef03ff280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="94d90-103">教學課程：Azure Active Directory 與 LinkedIn Learning 整合</span><span class="sxs-lookup"><span data-stu-id="94d90-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="94d90-104">在此教學課程中，您學會如何 toointegrate LinkedIn 學習與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="94d90-104">In this tutorial, you learn how toointegrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="94d90-105">與 Azure AD 整合 LinkedIn 學習可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="94d90-105">Integrating LinkedIn Learning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="94d90-106">您可以控制存取 tooLinkedIn Azure AD 中學習</span><span class="sxs-lookup"><span data-stu-id="94d90-106">You can control in Azure AD who has access tooLinkedIn Learning</span></span>
- <span data-ttu-id="94d90-107">您可以啟用您的使用者 tooautomatically get 登入 tooLinkedIn 機器學習其 Azure AD 帳戶 （單一登入）</span><span class="sxs-lookup"><span data-stu-id="94d90-107">You can enable your users tooautomatically get signed-on tooLinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="94d90-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="94d90-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="94d90-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="94d90-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94d90-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="94d90-110">Prerequisites</span></span>

<span data-ttu-id="94d90-111">tooconfigure LinkedIn 學習與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="94d90-111">tooconfigure Azure AD integration with LinkedIn Learning, you need hello following items:</span></span>

- <span data-ttu-id="94d90-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="94d90-112">An Azure AD subscription</span></span>
- <span data-ttu-id="94d90-113">已啟用 LinkedIn Learning 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="94d90-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="94d90-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="94d90-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="94d90-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="94d90-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="94d90-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="94d90-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="94d90-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="94d90-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="94d90-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="94d90-118">Scenario description</span></span>
<span data-ttu-id="94d90-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="94d90-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="94d90-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="94d90-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="94d90-121">從 hello 圖庫加入 LinkedIn 學習</span><span class="sxs-lookup"><span data-stu-id="94d90-121">Adding LinkedIn Learning from hello gallery</span></span>
2. <span data-ttu-id="94d90-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="94d90-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-hello-gallery"></a><span data-ttu-id="94d90-123">從 hello 圖庫加入 LinkedIn 學習</span><span class="sxs-lookup"><span data-stu-id="94d90-123">Adding LinkedIn Learning from hello gallery</span></span>
<span data-ttu-id="94d90-124">tooconfigure hello 整合 LinkedIn 學習到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd LinkedIn 學習。</span><span class="sxs-lookup"><span data-stu-id="94d90-124">tooconfigure hello integration of LinkedIn Learning into Azure AD, you need tooadd LinkedIn Learning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="94d90-125">**tooadd LinkedIn 學習 hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="94d90-125">**tooadd LinkedIn Learning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="94d90-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="94d90-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="94d90-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="94d90-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="94d90-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="94d90-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="94d90-131">按一下**新增**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="94d90-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="94d90-133">在 [hello] 搜尋方塊中，輸入**LinkedIn 學習**。</span><span class="sxs-lookup"><span data-stu-id="94d90-133">In hello search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="94d90-134">從 結果 窗格，按一下  **LinkedIn 學習**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="94d90-134">From results panel, click **LinkedIn Learning** tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="94d90-136">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="94d90-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="94d90-137">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 LinkedIn Learning 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="94d90-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="94d90-138">單一登入 toowork，Azure AD 需要 tooknow LinkedIn Learning 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="94d90-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Learning is tooa user in Azure AD.</span></span> <span data-ttu-id="94d90-139">換句話說，Azure AD 使用者與 hello LinkedIn 了解相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="94d90-139">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Learning needs toobe established.</span></span>

<span data-ttu-id="94d90-140">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**使用者名稱**LinkedIn 學習。</span><span class="sxs-lookup"><span data-stu-id="94d90-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="94d90-141">tooconfigure 及 LinkedIn 學習與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="94d90-141">tooconfigure and test Azure AD single sign-on with LinkedIn Learning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="94d90-142">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="94d90-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="94d90-143">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="94d90-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="94d90-144">**[建立測試使用者 LinkedIn 學習](#creating-a-linkedin-learning-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="94d90-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="94d90-145">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="94d90-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="94d90-146">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="94d90-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="94d90-147">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="94d90-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="94d90-148">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 LinkedIn 學習應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="94d90-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="94d90-149">**tooconfigure Azure AD 單一登入與 LinkedIn 學習 」 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="94d90-149">**tooconfigure Azure AD single sign-on with LinkedIn Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="94d90-150">在 Azure 入口網站上 hello hello **LinkedIn 學習**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="94d90-150">In hello Azure portal, on hello **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="94d90-152">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="94d90-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="94d90-154">在不同的網頁瀏覽器視窗中，以系統管理員身分登入 tooyour LinkedIn 學習租用戶。</span><span class="sxs-lookup"><span data-stu-id="94d90-154">In a different web browser window, sign-on tooyour LinkedIn Learning tenant as an administrator.</span></span>

4. <span data-ttu-id="94d90-155">在 [帳戶中心] 中，按一下 [設定] 底下的 [全域設定]。</span><span class="sxs-lookup"><span data-stu-id="94d90-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="94d90-156">此外，選取**學習-預設**hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="94d90-156">Also, select **Learning - Default** from hello dropdown list.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="94d90-158">按一下**或按一下這裡 tooload 並複製個別欄位從 hello 表單**和複製**實體識別碼**和**判斷提示取用者存取 (ACS) Url**</span><span class="sxs-lookup"><span data-stu-id="94d90-158">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="94d90-160">在 Azure 入口網站，在**LinkedIn 學習網域和 Url**，執行下列步驟，如果您想 tooconfigure SSO hello 中**IdP 初始化**模式</span><span class="sxs-lookup"><span data-stu-id="94d90-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform hello following steps if you want tooconfigure SSO in **IdP Initiated** mode</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="94d90-162">a.</span><span class="sxs-lookup"><span data-stu-id="94d90-162">a.</span></span> <span data-ttu-id="94d90-163">在 hello**識別碼**文字方塊中，輸入 hello**實體識別碼**從 LinkedIn 入口網站複製</span><span class="sxs-lookup"><span data-stu-id="94d90-163">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="94d90-164">b.</span><span class="sxs-lookup"><span data-stu-id="94d90-164">b.</span></span> <span data-ttu-id="94d90-165">在 hello**回覆 URL**文字方塊中，輸入 hello**判斷提示取用者存取 (ACS) Url**從 LinkedIn 入口網站複製</span><span class="sxs-lookup"><span data-stu-id="94d90-165">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="94d90-166">如果您想 tooconfigure SSO 中**SP 起始**，然後按一下 顯示進階的 URL hello 組態區段中的設定選項，並以下列模式的 hello 設定 hello 登入 URL:</span><span class="sxs-lookup"><span data-stu-id="94d90-166">If you want tooconfigure SSO in **SP Initiated**, then click Show Advanced URL setting option in hello configuration section and configure hello sign-on URL with hello following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. <span data-ttu-id="94d90-168">LinkedIn 學習應用程式預期 hello SAML 判斷提示，以特定格式，這需要您 tooadd 自訂屬性對應 tooyour SAML token 屬性設定。</span><span class="sxs-lookup"><span data-stu-id="94d90-168">Your LinkedIn Learning application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="94d90-169">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="94d90-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="94d90-170">hello 預設值是**使用者識別碼**是**user.userprincipalname**但 LinkedIn 學習預期這個 toobe hello 使用者的電子郵件地址的對應。</span><span class="sxs-lookup"><span data-stu-id="94d90-170">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="94d90-171">您可以使用該**user.mail**屬性從 hello 清單或使用您組織的組態為基礎的 hello 適當的屬性值。</span><span class="sxs-lookup"><span data-stu-id="94d90-171">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. <span data-ttu-id="94d90-173">在**使用者屬性**區段中，按一下**檢視和編輯所有其他使用者屬性**，並設定 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="94d90-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="94d90-174">hello 使用者需要 tooadd 四個宣告名為**電子郵件**，**部門**， **firstname**，和**lastname** hello 值是使用對應的 toobe**user.mail**， **user.department**， **user.givenname**，和**user.surname**分別</span><span class="sxs-lookup"><span data-stu-id="94d90-174">hello user needs tooadd four claims named **email**, **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="94d90-175">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="94d90-175">Attribute Name</span></span> | <span data-ttu-id="94d90-176">屬性值</span><span class="sxs-lookup"><span data-stu-id="94d90-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="94d90-177">電子郵件</span><span class="sxs-lookup"><span data-stu-id="94d90-177">email</span></span>| <span data-ttu-id="94d90-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="94d90-178">user.mail</span></span> |    
    | <span data-ttu-id="94d90-179">department</span><span class="sxs-lookup"><span data-stu-id="94d90-179">department</span></span>| <span data-ttu-id="94d90-180">user.department</span><span class="sxs-lookup"><span data-stu-id="94d90-180">user.department</span></span> |
    | <span data-ttu-id="94d90-181">firstname</span><span class="sxs-lookup"><span data-stu-id="94d90-181">firstname</span></span>| <span data-ttu-id="94d90-182">user.givenname</span><span class="sxs-lookup"><span data-stu-id="94d90-182">user.givenname</span></span> |
    | <span data-ttu-id="94d90-183">lastname</span><span class="sxs-lookup"><span data-stu-id="94d90-183">lastname</span></span>| <span data-ttu-id="94d90-184">user.surname</span><span class="sxs-lookup"><span data-stu-id="94d90-184">user.surname</span></span> |
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    <span data-ttu-id="94d90-186">a.</span><span class="sxs-lookup"><span data-stu-id="94d90-186">a.</span></span> <span data-ttu-id="94d90-187">按一下**加入屬性**tooopen hello 屬性 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="94d90-187">Click **Add Attribute** tooopen hello attribute dialog.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="94d90-190">b.</span><span class="sxs-lookup"><span data-stu-id="94d90-190">b.</span></span> <span data-ttu-id="94d90-191">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="94d90-191">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="94d90-192">c.</span><span class="sxs-lookup"><span data-stu-id="94d90-192">c.</span></span> <span data-ttu-id="94d90-193">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="94d90-193">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="94d90-194">d.</span><span class="sxs-lookup"><span data-stu-id="94d90-194">d.</span></span> <span data-ttu-id="94d90-195">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="94d90-195">Click **Ok**</span></span>

10. <span data-ttu-id="94d90-196">執行下列步驟在 hello hello**名稱**屬性-</span><span class="sxs-lookup"><span data-stu-id="94d90-196">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="94d90-197">a.</span><span class="sxs-lookup"><span data-stu-id="94d90-197">a.</span></span> <span data-ttu-id="94d90-198">按一下 hello 屬性 tooopen hello**編輯屬性**視窗。</span><span class="sxs-lookup"><span data-stu-id="94d90-198">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    <span data-ttu-id="94d90-200">b.</span><span class="sxs-lookup"><span data-stu-id="94d90-200">b.</span></span> <span data-ttu-id="94d90-201">從 hello 刪除 hello URL 值**命名空間**。</span><span class="sxs-lookup"><span data-stu-id="94d90-201">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="94d90-202">c.</span><span class="sxs-lookup"><span data-stu-id="94d90-202">c.</span></span> <span data-ttu-id="94d90-203">按一下**確定**toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="94d90-203">Click **Ok** toosave hello setting.</span></span>

11. <span data-ttu-id="94d90-204">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="94d90-204">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. <span data-ttu-id="94d90-206">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="94d90-206">Click **Save**.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="94d90-208">跳過**LinkedIn 的管理設定**> 一節。</span><span class="sxs-lookup"><span data-stu-id="94d90-208">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="94d90-209">上傳 hello hello 上載 XML 檔案的選項，即可從 hello Azure 入口網站下載的 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="94d90-209">Upload hello XML file you downloaded from hello Azure portal by clicking hello Upload XML file option.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="94d90-211">按一下**上**tooenable SSO。</span><span class="sxs-lookup"><span data-stu-id="94d90-211">Click **On** tooenable SSO.</span></span> <span data-ttu-id="94d90-212">SSO 狀態變更從**未連接**太**已連線**</span><span class="sxs-lookup"><span data-stu-id="94d90-212">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="94d90-214">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="94d90-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="94d90-215">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="94d90-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="94d90-217">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="94d90-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="94d90-218">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="94d90-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="94d90-220">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="94d90-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="94d90-222">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="94d90-222">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="94d90-224">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="94d90-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="94d90-226">a.</span><span class="sxs-lookup"><span data-stu-id="94d90-226">a.</span></span> <span data-ttu-id="94d90-227">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="94d90-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="94d90-228">b.</span><span class="sxs-lookup"><span data-stu-id="94d90-228">b.</span></span> <span data-ttu-id="94d90-229">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="94d90-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="94d90-230">c.</span><span class="sxs-lookup"><span data-stu-id="94d90-230">c.</span></span> <span data-ttu-id="94d90-231">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="94d90-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="94d90-232">d.</span><span class="sxs-lookup"><span data-stu-id="94d90-232">d.</span></span> <span data-ttu-id="94d90-233">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="94d90-233">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="94d90-234">建立 LinkedIn Learning 測試使用者</span><span class="sxs-lookup"><span data-stu-id="94d90-234">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="94d90-235">Linked Learning 應用程式支援。</span><span class="sxs-lookup"><span data-stu-id="94d90-235">Linked Learning Application supports.</span></span> <span data-ttu-id="94d90-236">即時使用者佈建和之後驗證使用者會自動建立 hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="94d90-236">Just in time user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="94d90-237">Hello LinkedIn 學習入口網站的翻轉 hello 交換器上 hello 管理設定 頁面上**自動指派的授權**tooactive tooenable 恰好即時佈建，而這也會指派授權 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="94d90-237">On hello admin settings page on hello LinkedIn Learning portal flip hello switch **Automatically Assign licenses** tooactive tooenable Just in time provisioning and this will also assign a license toohello user.</span></span>
   
   ![建立 Azure AD 測試使用者](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="94d90-239">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="94d90-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="94d90-240">在本節中，您必須啟用 Azure 單一登入許 Simon toouse 授與存取 tooLinkedIn 學習。</span><span class="sxs-lookup"><span data-stu-id="94d90-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Learning.</span></span>

![指派使用者][200] 

<span data-ttu-id="94d90-242">**tooassign 許 Simon tooLinkedIn 學習，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="94d90-242">**tooassign Britta Simon tooLinkedIn Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="94d90-243">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="94d90-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="94d90-245">在 [hello] 應用程式清單中，選取**LinkedIn 學習**。</span><span class="sxs-lookup"><span data-stu-id="94d90-245">In hello applications list, select **LinkedIn Learning**.</span></span>

    ![設定單一登入](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. <span data-ttu-id="94d90-247">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="94d90-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="94d90-249">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="94d90-249">Click **Add** button.</span></span> <span data-ttu-id="94d90-250">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="94d90-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="94d90-252">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="94d90-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="94d90-253">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="94d90-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="94d90-254">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="94d90-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="94d90-255">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="94d90-255">Testing single sign-on</span></span>

<span data-ttu-id="94d90-256">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="94d90-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="94d90-257">當您按一下 hello 存取面板中的 hello LinkedIn 學習磚時，您應該取得 hello Azure 登入頁面，並在之後成功登入，您應該取得 LinkedIn 學習應用程式。</span><span class="sxs-lookup"><span data-stu-id="94d90-257">When you click hello LinkedIn Learning tile in hello Access Panel, you should get hello Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="94d90-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="94d90-258">Additional resources</span></span>

* [<span data-ttu-id="94d90-259">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94d90-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="94d90-260">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="94d90-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png
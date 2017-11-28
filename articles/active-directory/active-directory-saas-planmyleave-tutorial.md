---
title: "教學課程：Azure Active Directory 與 PlanMyLeave | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 PlanMyLeave 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: 44a6782e44ef22fc957544960be1742f9eed6e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="cb662-103">教學課程：Azure Active Directory 與 PlanMyLeave 整合</span><span class="sxs-lookup"><span data-stu-id="cb662-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="cb662-104">在此教學課程中，您學會如何 toointegrate PlanMyLeave 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="cb662-104">In this tutorial, you learn how toointegrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cb662-105">與 Azure AD 整合 PlanMyLeave 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="cb662-105">Integrating PlanMyLeave with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cb662-106">您可以控制存取 tooPlanMyLeave Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="cb662-106">You can control in Azure AD who has access tooPlanMyLeave</span></span>
- <span data-ttu-id="cb662-107">您可以啟用您的使用者 tooautomatically get 登入 tooPlanMyLeave （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="cb662-107">You can enable your users tooautomatically get signed-on tooPlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cb662-108">您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站</span><span class="sxs-lookup"><span data-stu-id="cb662-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="cb662-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="cb662-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb662-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="cb662-110">Prerequisites</span></span>

<span data-ttu-id="cb662-111">tooconfigure PlanMyLeave 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="cb662-111">tooconfigure Azure AD integration with PlanMyLeave, you need hello following items:</span></span>

- <span data-ttu-id="cb662-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cb662-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cb662-113">啟用 PlanMyLeave 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cb662-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="cb662-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="cb662-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="cb662-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="cb662-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cb662-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="cb662-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="cb662-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="cb662-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="cb662-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="cb662-118">Scenario description</span></span>
<span data-ttu-id="cb662-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cb662-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cb662-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="cb662-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cb662-121">從 hello 圖庫加入 PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="cb662-121">Adding PlanMyLeave from hello gallery</span></span>
2. <span data-ttu-id="cb662-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cb662-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-hello-gallery"></a><span data-ttu-id="cb662-123">從 hello 圖庫加入 PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="cb662-123">Adding PlanMyLeave from hello gallery</span></span>
<span data-ttu-id="cb662-124">tooconfigure hello 整合 PlanMyLeave 到 Azure AD，您需要 tooadd PlanMyLeave hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cb662-124">tooconfigure hello integration of PlanMyLeave into Azure AD, you need tooadd PlanMyLeave from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cb662-125">**tooadd PlanMyLeave 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cb662-125">**tooadd PlanMyLeave from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb662-126">在 [hello ** [Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="cb662-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cb662-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cb662-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cb662-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cb662-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="cb662-131">按一下**新增**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="cb662-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="cb662-133">在 [hello] 搜尋方塊中，輸入**PlanMyLeave**。</span><span class="sxs-lookup"><span data-stu-id="cb662-133">In hello search box, type **PlanMyLeave**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="cb662-135">在 [hello [結果] 窗格中，選取 [ **PlanMyLeave**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cb662-135">In hello results panel, select **PlanMyLeave**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cb662-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cb662-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cb662-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 PlanMyLeave 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cb662-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cb662-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 PlanMyLeave 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="cb662-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PlanMyLeave is tooa user in Azure AD.</span></span> <span data-ttu-id="cb662-140">換句話說，Azure AD 使用者與 hello PlanMyLeave 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="cb662-140">In other words, a link relationship between an Azure AD user and hello related user in PlanMyLeave needs toobe established.</span></span>

<span data-ttu-id="cb662-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** PlanMyLeave 中。</span><span class="sxs-lookup"><span data-stu-id="cb662-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="cb662-142">tooconfigure 及 PlanMyLeave 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="cb662-142">tooconfigure and test Azure AD single sign-on with PlanMyLeave, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cb662-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="cb662-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cb662-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="cb662-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cb662-145">**[建立測試使用者 PlanMyLeave](#creating-a-planmyleave-test-user) ** -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 PlanMyLeave 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="cb662-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - toohave a counterpart of Britta Simon in PlanMyLeave that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="cb662-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cb662-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cb662-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="cb662-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cb662-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cb662-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cb662-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並 PlanMyLeave 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="cb662-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="cb662-150">**tooconfigure Azure AD 單一登入與 PlanMyLeave，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cb662-150">**tooconfigure Azure AD single sign-on with PlanMyLeave, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb662-151">在 hello Azure 管理入口網站上 hello **PlanMyLeave**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="cb662-151">In hello Azure Management portal, on hello **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="cb662-153">在 [hello**單一登入**對話方塊頁面上，為**模式**選取**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cb662-153">On hello **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="cb662-155">在 [hello **PlanMyLeave 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cb662-155">On hello **PlanMyLeave Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="cb662-157">a.</span><span class="sxs-lookup"><span data-stu-id="cb662-157">a.</span></span> <span data-ttu-id="cb662-158">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company-name>.planmyleave.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="cb662-158">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="cb662-159">b.</span><span class="sxs-lookup"><span data-stu-id="cb662-159">b.</span></span> <span data-ttu-id="cb662-160">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company-name>.planmyleave.com`</span><span class="sxs-lookup"><span data-stu-id="cb662-160">In hello **Identifer** textbox, type a URL using hello following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cb662-161">請注意這些不是 hello 實際值。</span><span class="sxs-lookup"><span data-stu-id="cb662-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="cb662-162">您有的 tooupdate 這些值與實際的 hello 登入 URL 和識別碼。</span><span class="sxs-lookup"><span data-stu-id="cb662-162">You have tooupdate these values with hello actual Sign On URL and Identifier.</span></span> <span data-ttu-id="cb662-163">請連絡[PlanMyLeave 支援小組](mailto:support@planmyleave.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="cb662-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) tooget these values.</span></span>

4. <span data-ttu-id="cb662-164">在 [hello **SAML 簽章憑證**區段中，按一下**建立新憑證**。</span><span class="sxs-lookup"><span data-stu-id="cb662-164">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. <span data-ttu-id="cb662-166">在 [hello**建立新的憑證**] 對話方塊中，按一下 hello 日曆圖示，然後選取**到期日**。</span><span class="sxs-lookup"><span data-stu-id="cb662-166">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="cb662-167">然後按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cb662-167">Then click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="cb662-169">在 hello **SAML 簽章憑證**區段中，選取**啟用新的憑證**按一下**儲存**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cb662-169">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="cb662-171">Hello 快顯視窗上**變換憑證**視窗中，按一下 [**確定**。</span><span class="sxs-lookup"><span data-stu-id="cb662-171">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="cb662-173">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="cb662-173">On hello **SAML Signing Certificate** section, click **Certificate (base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="cb662-175">在 [hello **PlanMyLeave 組態**區段中，按一下**設定 PlanMyLeave** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="cb662-175">On hello **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** tooopen **Configure sign-on** window.</span></span>

    ![設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="cb662-178">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 PlanMyLeave 租用戶。</span><span class="sxs-lookup"><span data-stu-id="cb662-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="cb662-179">跳過**系統安裝**。</span><span class="sxs-lookup"><span data-stu-id="cb662-179">Go too**System Setup**.</span></span> <span data-ttu-id="cb662-180">然後在 [hello**安全性管理**區段中，按一下**公司 SAML 設定**。</span><span class="sxs-lookup"><span data-stu-id="cb662-180">Then on hello **Security Management** section click **Company SAML settings** .</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="cb662-182">在 [hello **SAML 設定**區段中，按一下編輯器圖示。</span><span class="sxs-lookup"><span data-stu-id="cb662-182">On hello **SAML Settings** section, click editor icon.</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="cb662-184">在 [hello**更新 SAML 設定**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cb662-184">On hello **Update SAML Settings** section, perform hello following steps:</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="cb662-186">a.</span><span class="sxs-lookup"><span data-stu-id="cb662-186">a.</span></span>  <span data-ttu-id="cb662-187">在 [hello**登入 URL**文字方塊中，將 hello 值放**SAML 單一登入服務 URL**從 Azure AD 應用程式設定] 視窗。</span><span class="sxs-lookup"><span data-stu-id="cb662-187">In hello **Login URL** textbox, put hello value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="cb662-188">b.</span><span class="sxs-lookup"><span data-stu-id="cb662-188">b.</span></span>  <span data-ttu-id="cb662-189">在記事本中開啟下載的憑證檔案，只 hello 之間複製內容 hello---Begin Certificate---和---End certificate---它到剪貼簿，然後將它貼入 toohello**憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="cb662-189">Open your downloaded certificate file in notepad, copy only hello content between hello ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it toohello **Certificate** textbox.</span></span>

    <span data-ttu-id="cb662-190">c.</span><span class="sxs-lookup"><span data-stu-id="cb662-190">c.</span></span> <span data-ttu-id="cb662-191">設定 「**已啟用**」 太"**是**"。</span><span class="sxs-lookup"><span data-stu-id="cb662-191">Set "**Is Enable**" too"**Yes**".</span></span>

    <span data-ttu-id="cb662-192">d.</span><span class="sxs-lookup"><span data-stu-id="cb662-192">d.</span></span> <span data-ttu-id="cb662-193">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="cb662-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cb662-194">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cb662-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="cb662-195">hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="cb662-195">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="cb662-197">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cb662-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb662-198">在 [hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="cb662-198">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cb662-200">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="cb662-200">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cb662-202">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="cb662-202">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cb662-204">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cb662-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cb662-206">a.</span><span class="sxs-lookup"><span data-stu-id="cb662-206">a.</span></span> <span data-ttu-id="cb662-207">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="cb662-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cb662-208">b.</span><span class="sxs-lookup"><span data-stu-id="cb662-208">b.</span></span> <span data-ttu-id="cb662-209">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="cb662-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cb662-210">c.</span><span class="sxs-lookup"><span data-stu-id="cb662-210">c.</span></span> <span data-ttu-id="cb662-211">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="cb662-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cb662-212">d.</span><span class="sxs-lookup"><span data-stu-id="cb662-212">d.</span></span> <span data-ttu-id="cb662-213">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="cb662-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="cb662-214">建立 PlanMyLeave 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cb662-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="cb662-215">hello 本節目標在於 toocreate PlanMyLeave 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="cb662-215">hello objective of this section is toocreate a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="cb662-216">PlanMyLeave 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="cb662-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="cb662-217">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="cb662-217">There is no action item for you in this section.</span></span> <span data-ttu-id="cb662-218">如果尚未存在，將會嘗試 tooaccess PlanMyLeave 期間建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="cb662-218">A new user will be created during an attempt tooaccess PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="cb662-219">若要手動 toocreate 使用者，您需要 toocontact [PlanMyLeave 支援小組](mailto:support@planmyleave.com)。</span><span class="sxs-lookup"><span data-stu-id="cb662-219">If you need toocreate an user manually, you need toocontact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cb662-220">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="cb662-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cb662-221">在本節中，您可以授與他們存取 tooPlanMyLeave 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cb662-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooPlanMyLeave.</span></span>

![指派使用者][200] 

<span data-ttu-id="cb662-223">**tooassign 許 Simon tooPlanMyLeave，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cb662-223">**tooassign Britta Simon tooPlanMyLeave, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb662-224">在 [hello Azure 管理入口網站中，開啟 [hello 應用程式] 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cb662-224">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="cb662-226">在 [hello] 應用程式清單中，選取**PlanMyLeave**。</span><span class="sxs-lookup"><span data-stu-id="cb662-226">In hello applications list, select **PlanMyLeave**.</span></span>

    ![設定單一登入](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="cb662-228">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="cb662-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="cb662-230">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cb662-230">Click **Add** button.</span></span> <span data-ttu-id="cb662-231">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="cb662-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="cb662-233">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="cb662-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cb662-234">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cb662-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cb662-235">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cb662-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="cb662-236">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="cb662-236">Testing single sign-on</span></span>

<span data-ttu-id="cb662-237">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="cb662-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cb662-238">當您按一下 hello PlanMyLeave 磚 hello 存取面板中的時，您應該取得自動登入 tooyour PlanMyLeave 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cb662-238">When you click hello PlanMyLeave tile in hello Access Panel, you should get automatically signed-on tooyour PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="cb662-239">其他資源</span><span class="sxs-lookup"><span data-stu-id="cb662-239">Additional resources</span></span>

* [<span data-ttu-id="cb662-240">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb662-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cb662-241">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="cb662-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png
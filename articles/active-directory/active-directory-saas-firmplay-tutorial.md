---
title: "教學課程：Azure Active Directory 與 FirmPlay - Employee Advocacy for Recruiting 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 FirmPlay-招募的員工關注之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f143e0bb8f2a42de880d77e5f033694ce3f09cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a><span data-ttu-id="44818-103">教學課程：Azure Active Directory 與 FirmPlay - Employee Advocacy for Recruiting 整合</span><span class="sxs-lookup"><span data-stu-id="44818-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span></span>

<span data-ttu-id="44818-104">在此教學課程中，您學會如何 toointegrate FirmPlay-招募與 Azure Active Directory (Azure AD) 的員工關注。</span><span class="sxs-lookup"><span data-stu-id="44818-104">In this tutorial, you learn how toointegrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="44818-105">整合 FirmPlay-招募與 Azure AD 的員工關注可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="44818-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="44818-106">您可以控制存取 tooFirmPlay-招募的員工關注 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="44818-106">You can control in Azure AD who has access tooFirmPlay - Employee Advocacy for Recruiting</span></span>
- <span data-ttu-id="44818-107">您可以啟用您的使用者 tooautomatically get 登入 tooFirmPlay-招募 （單一登入） 的員工關注他們的 Azure AD 帳戶與</span><span class="sxs-lookup"><span data-stu-id="44818-107">You can enable your users tooautomatically get signed-on tooFirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="44818-108">您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站</span><span class="sxs-lookup"><span data-stu-id="44818-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="44818-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="44818-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44818-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="44818-110">Prerequisites</span></span>

<span data-ttu-id="44818-111">tooconfigure 與 FirmPlay-招募的員工關注的 Azure AD 整合您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="44818-111">tooconfigure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need hello following items:</span></span>

- <span data-ttu-id="44818-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="44818-112">An Azure AD subscription</span></span>
- <span data-ttu-id="44818-113">已啟用 FirmPlay - Employee Advocacy for Recruiting 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="44818-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="44818-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="44818-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="44818-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="44818-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="44818-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="44818-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="44818-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="44818-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="44818-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="44818-118">Scenario description</span></span>
<span data-ttu-id="44818-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="44818-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="44818-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="44818-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="44818-121">加入 FirmPlay-招募從 hello 組件庫的員工關注</span><span class="sxs-lookup"><span data-stu-id="44818-121">Adding FirmPlay - Employee Advocacy for Recruiting from hello gallery</span></span>
2. <span data-ttu-id="44818-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="44818-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-hello-gallery"></a><span data-ttu-id="44818-123">加入 FirmPlay-招募從 hello 組件庫的員工關注</span><span class="sxs-lookup"><span data-stu-id="44818-123">Adding FirmPlay - Employee Advocacy for Recruiting from hello gallery</span></span>
<span data-ttu-id="44818-124">tooconfigure hello 整合 FirmPlay 位員工關注，如招募到 Azure AD，您需要 tooadd FirmPlay-招募 hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式的員工關注。</span><span class="sxs-lookup"><span data-stu-id="44818-124">tooconfigure hello integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need tooadd FirmPlay - Employee Advocacy for Recruiting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="44818-125">**tooadd FirmPlay-hello 庫、 招募的員工關注執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="44818-125">**tooadd FirmPlay - Employee Advocacy for Recruiting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="44818-126">在 hello  **[Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="44818-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="44818-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="44818-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="44818-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="44818-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="44818-131">按一下**新增**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="44818-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="44818-133">在 [hello] 搜尋方塊中，輸入**FirmPlay-招募的員工關注**。</span><span class="sxs-lookup"><span data-stu-id="44818-133">In hello search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. <span data-ttu-id="44818-135">在 hello 結果 窗格中，選取  **FirmPlay-招募的員工關注**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="44818-135">In hello results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="44818-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="44818-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="44818-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 FirmPlay - Employee Advocacy for Recruiting 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="44818-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="44818-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 FirmPlay-招募的員工關注是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="44818-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FirmPlay - Employee Advocacy for Recruiting is tooa user in Azure AD.</span></span> <span data-ttu-id="44818-140">換句話說，Azure AD 使用者與 hello FirmPlay-招募的員工關注中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="44818-140">In other words, a link relationship between an Azure AD user and hello related user in FirmPlay - Employee Advocacy for Recruiting needs toobe established.</span></span>

<span data-ttu-id="44818-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** FirmPlay-招募的員工關注中。</span><span class="sxs-lookup"><span data-stu-id="44818-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FirmPlay - Employee Advocacy for Recruiting.</span></span>

<span data-ttu-id="44818-142">tooconfigure 和測試 Azure AD 單一登入與 FirmPlay 位員工關注，如招募，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="44818-142">tooconfigure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="44818-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="44818-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="44818-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="44818-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="44818-145">**[建立 FirmPlay-招募測試使用者的員工關注](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** -toohave 許 Simon FirmPlay 中對應項目： 員工關注，如招募也就連結 toohello Azure AD 的她的表示法。</span><span class="sxs-lookup"><span data-stu-id="44818-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - toohave a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="44818-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="44818-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="44818-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="44818-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="44818-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="44818-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="44818-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並設定單一登入您 FirmPlay 位員工關注招募應用程式中。</span><span class="sxs-lookup"><span data-stu-id="44818-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span></span>

<span data-ttu-id="44818-150">**Azure AD 單一登入與 FirmPlay-招募的員工關注的 tooconfigure 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="44818-150">**tooconfigure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform hello following steps:**</span></span>

1. <span data-ttu-id="44818-151">在 hello Azure 管理入口網站上 hello **FirmPlay-招募的員工關注**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="44818-151">In hello Azure Management portal, on hello **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="44818-153">在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="44818-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. <span data-ttu-id="44818-155">在 hello **FirmPlay-招募網域和 Url 的員工關注**區段中的，在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<your-subdomain>.firmplay.com/`</span><span class="sxs-lookup"><span data-stu-id="44818-155">On hello **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<your-subdomain>.firmplay.com/`</span></span>

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > <span data-ttu-id="44818-157">請注意，這不是 hello 真正的價值。</span><span class="sxs-lookup"><span data-stu-id="44818-157">Please note that this is not hello real value.</span></span> <span data-ttu-id="44818-158">您有的 tooupdate 這個值與實際的 hello 登入 URL。</span><span class="sxs-lookup"><span data-stu-id="44818-158">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="44818-159">請連絡[FirmPlay-招募支援小組的員工關注](mailto:engineering@firmplay.com)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="44818-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) tooget this value.</span></span> 

4. <span data-ttu-id="44818-160">在 hello **SAML 簽章憑證**區段中，按一下**建立新憑證**。</span><span class="sxs-lookup"><span data-stu-id="44818-160">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. <span data-ttu-id="44818-162">在 [hello**建立新的憑證**] 對話方塊中，按一下 hello 日曆圖示，然後選取**到期日**。</span><span class="sxs-lookup"><span data-stu-id="44818-162">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="44818-163">然後按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="44818-163">Then click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="44818-165">在 hello **SAML 簽章憑證**區段中，選取**啟用新的憑證**按一下**儲存** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="44818-165">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. <span data-ttu-id="44818-167">Hello 快顯視窗上**變換憑證**視窗中，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="44818-167">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="44818-169">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="44818-169">On hello **SAML Signing Certificate** section, click **Certificate (base64)** and then save hello certificate file on your computer.</span></span> 

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. <span data-ttu-id="44818-171">在 hello **FirmPlay-招募組態的員工關注**區段中，按一下**設定 FirmPlay-招募的員工關注**tooopen**設定登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="44818-171">On hello **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** tooopen **Configure sign-on** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. <span data-ttu-id="44818-174">tooget SSO 設定應用程式，請連絡[FirmPlay-招募支援小組的員工關注](mailto:engineering@firmplay.com)，提供下列 hello:</span><span class="sxs-lookup"><span data-stu-id="44818-174">tooget SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with hello following:</span></span> 

    <span data-ttu-id="44818-175">• hello 下載**憑證檔案**</span><span class="sxs-lookup"><span data-stu-id="44818-175">•  hello downloaded **Certificate file**</span></span>

    <span data-ttu-id="44818-176">• hello **SAML 單一登入服務 URL**</span><span class="sxs-lookup"><span data-stu-id="44818-176">•  hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="44818-177">• hello **SAML 實體識別碼**</span><span class="sxs-lookup"><span data-stu-id="44818-177">•  hello **SAML Entity ID**</span></span>

    <span data-ttu-id="44818-178">• hello**登出 URL**</span><span class="sxs-lookup"><span data-stu-id="44818-178">•  hello **Sign-Out URL**</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="44818-179">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="44818-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="44818-180">hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="44818-180">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="44818-182">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="44818-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="44818-183">在 hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="44818-183">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="44818-185">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="44818-185">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="44818-187">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="44818-187">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="44818-189">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="44818-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="44818-191">a.</span><span class="sxs-lookup"><span data-stu-id="44818-191">a.</span></span> <span data-ttu-id="44818-192">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="44818-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="44818-193">b.</span><span class="sxs-lookup"><span data-stu-id="44818-193">b.</span></span> <span data-ttu-id="44818-194">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="44818-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="44818-195">c.</span><span class="sxs-lookup"><span data-stu-id="44818-195">c.</span></span> <span data-ttu-id="44818-196">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="44818-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="44818-197">d.</span><span class="sxs-lookup"><span data-stu-id="44818-197">d.</span></span> <span data-ttu-id="44818-198">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="44818-198">Click **Create**.</span></span> 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a><span data-ttu-id="44818-199">建立 FirmPlay - Employee Advocacy for Recruiting 測試使用者</span><span class="sxs-lookup"><span data-stu-id="44818-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span></span>

<span data-ttu-id="44818-200">在本節中，您要在 FirmPlay - Employee Advocacy for Recruiting 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="44818-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span></span> <span data-ttu-id="44818-201">請使用[FirmPlay-招募支援小組的員工關注](mailto:engineering@firmplay.com)tooadd hello hello FirmPlay 位員工關注招募平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="44818-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) tooadd hello users in hello FirmPlay - Employee Advocacy for Recruiting platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="44818-202">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="44818-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="44818-203">在本節中，以啟用許 Simon toouse Azure 單一登入授與他們存取 tooFirmPlay-招募的員工關注。</span><span class="sxs-lookup"><span data-stu-id="44818-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFirmPlay - Employee Advocacy for Recruiting.</span></span>

![指派使用者][200] 

<span data-ttu-id="44818-205">**tooassign 許 Simon tooFirmPlay 位員工關注，如招募，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="44818-205">**tooassign Britta Simon tooFirmPlay - Employee Advocacy for Recruiting, perform hello following steps:**</span></span>

1. <span data-ttu-id="44818-206">在 hello Azure 管理入口網站中，開啟 hello 應用程式 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="44818-206">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="44818-208">在 [hello] 應用程式清單中，選取**FirmPlay-招募的員工關注**。</span><span class="sxs-lookup"><span data-stu-id="44818-208">In hello applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![設定單一登入](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. <span data-ttu-id="44818-210">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="44818-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="44818-212">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="44818-212">Click **Add** button.</span></span> <span data-ttu-id="44818-213">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="44818-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="44818-215">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="44818-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="44818-216">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="44818-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="44818-217">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="44818-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="44818-218">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="44818-218">Testing single sign-on</span></span>

<span data-ttu-id="44818-219">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="44818-219">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="44818-220">當您按一下 hello FirmPlay-招募磚 hello 存取面板中的員工關注您應該取得自動登入 tooyour FirmPlay-招募應用程式的員工關注。</span><span class="sxs-lookup"><span data-stu-id="44818-220">When you click hello FirmPlay - Employee Advocacy for Recruiting tile in hello Access Panel, you should get automatically signed-on tooyour FirmPlay - Employee Advocacy for Recruiting application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="44818-221">其他資源</span><span class="sxs-lookup"><span data-stu-id="44818-221">Additional resources</span></span>

* [<span data-ttu-id="44818-222">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44818-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="44818-223">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="44818-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png
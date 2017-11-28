---
title: "教學課程：Azure Active Directory 與 FreshGrade 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 FreshGrade 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1055bba6-f4df-462e-bc9b-1ad5ada0f638
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e2fe7cedd45290945ec5624453a9675abdd7726d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshgrade"></a><span data-ttu-id="04e6f-103">教學課程：Azure Active Directory 與 FreshGrade 整合</span><span class="sxs-lookup"><span data-stu-id="04e6f-103">Tutorial: Azure Active Directory integration with FreshGrade</span></span>

<span data-ttu-id="04e6f-104">在此教學課程中，您學會如何 toointegrate FreshGrade 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="04e6f-104">In this tutorial, you learn how toointegrate FreshGrade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="04e6f-105">與 Azure AD 整合 FreshGrade 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="04e6f-105">Integrating FreshGrade with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="04e6f-106">您可以控制存取 tooFreshGrade Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="04e6f-106">You can control in Azure AD who has access tooFreshGrade</span></span>
- <span data-ttu-id="04e6f-107">您可以啟用您的使用者 tooautomatically get 登入 tooFreshGrade （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="04e6f-107">You can enable your users tooautomatically get signed-on tooFreshGrade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="04e6f-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="04e6f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="04e6f-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="04e6f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04e6f-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="04e6f-110">Prerequisites</span></span>

<span data-ttu-id="04e6f-111">tooconfigure FreshGrade 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="04e6f-111">tooconfigure Azure AD integration with FreshGrade, you need hello following items:</span></span>

- <span data-ttu-id="04e6f-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="04e6f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="04e6f-113">已啟用 FreshGrade 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="04e6f-113">A FreshGrade single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="04e6f-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="04e6f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="04e6f-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="04e6f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="04e6f-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="04e6f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="04e6f-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="04e6f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="04e6f-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="04e6f-118">Scenario description</span></span>
<span data-ttu-id="04e6f-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="04e6f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="04e6f-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="04e6f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="04e6f-121">從 hello 圖庫加入 FreshGrade</span><span class="sxs-lookup"><span data-stu-id="04e6f-121">Adding FreshGrade from hello gallery</span></span>
2. <span data-ttu-id="04e6f-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="04e6f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshgrade-from-hello-gallery"></a><span data-ttu-id="04e6f-123">從 hello 圖庫加入 FreshGrade</span><span class="sxs-lookup"><span data-stu-id="04e6f-123">Adding FreshGrade from hello gallery</span></span>
<span data-ttu-id="04e6f-124">tooconfigure hello 整合 FreshGrade 到 Azure AD，您需要 tooadd FreshGrade hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="04e6f-124">tooconfigure hello integration of FreshGrade into Azure AD, you need tooadd FreshGrade from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="04e6f-125">**tooadd FreshGrade 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="04e6f-125">**tooadd FreshGrade from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="04e6f-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="04e6f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="04e6f-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="04e6f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="04e6f-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="04e6f-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="04e6f-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="04e6f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="04e6f-133">在 [hello] 搜尋方塊中，輸入**FreshGrade**。</span><span class="sxs-lookup"><span data-stu-id="04e6f-133">In hello search box, type **FreshGrade**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_search.png)

5. <span data-ttu-id="04e6f-135">在 hello 結果 窗格中，選取  **FreshGrade**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="04e6f-135">In hello results panel, select **FreshGrade**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="04e6f-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="04e6f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="04e6f-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 FreshGrade 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="04e6f-138">In this section, you configure and test Azure AD single sign-on with FreshGrade based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="04e6f-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 FreshGrade 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="04e6f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FreshGrade is tooa user in Azure AD.</span></span> <span data-ttu-id="04e6f-140">換句話說，Azure AD 使用者與 hello FreshGrade 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="04e6f-140">In other words, a link relationship between an Azure AD user and hello related user in FreshGrade needs toobe established.</span></span>

<span data-ttu-id="04e6f-141">FreshGrade 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="04e6f-141">In FreshGrade, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="04e6f-142">tooconfigure 及 FreshGrade 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="04e6f-142">tooconfigure and test Azure AD single sign-on with FreshGrade, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="04e6f-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="04e6f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="04e6f-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="04e6f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="04e6f-145">**[建立測試使用者 FreshGrade](#creating-a-freshgrade-test-user)**  -toohave 許 Simon FreshGrade 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="04e6f-145">**[Creating a FreshGrade test user](#creating-a-freshgrade-test-user)** - toohave a counterpart of Britta Simon in FreshGrade that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="04e6f-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="04e6f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="04e6f-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="04e6f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="04e6f-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="04e6f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="04e6f-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 FreshGrade 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="04e6f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FreshGrade application.</span></span>

<span data-ttu-id="04e6f-150">**tooconfigure Azure AD 單一登入與 FreshGrade，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="04e6f-150">**tooconfigure Azure AD single sign-on with FreshGrade, perform hello following steps:**</span></span>

1. <span data-ttu-id="04e6f-151">在 Azure 入口網站上 hello hello **FreshGrade**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="04e6f-151">In hello Azure portal, on hello **FreshGrade** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="04e6f-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="04e6f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_samlbase.png)

3. <span data-ttu-id="04e6f-155">在 hello **FreshGrade 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="04e6f-155">On hello **FreshGrade Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_url.png)

    <span data-ttu-id="04e6f-157">a.</span><span class="sxs-lookup"><span data-stu-id="04e6f-157">a.</span></span> <span data-ttu-id="04e6f-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列的 hello 模式：</span><span class="sxs-lookup"><span data-stu-id="04e6f-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
      | |
      |--|
      | `https://<subdomain>.freshgrade.com/login` |    
      | `https://<subdomain>.onboarding.freshgrade.com/login` |

    <span data-ttu-id="04e6f-159">b.</span><span class="sxs-lookup"><span data-stu-id="04e6f-159">b.</span></span> <span data-ttu-id="04e6f-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列的 hello 模式：</span><span class="sxs-lookup"><span data-stu-id="04e6f-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
      | |
      |--|
      | `https://login.onboarding.freshgrade.com:443/saml/metadata/alias/<instancename>` |      
      | `https://login.freshgrade.com:443/saml/metadata/alias/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="04e6f-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="04e6f-161">These values are not real.</span></span> <span data-ttu-id="04e6f-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="04e6f-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="04e6f-163">請連絡[FreshGrade 用戶端支援小組](mailTo:support@freshgrade.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="04e6f-163">Contact [FreshGrade Client support team](mailTo:support@freshgrade.com) tooget these values.</span></span> 
 


4. <span data-ttu-id="04e6f-164">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="04e6f-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_certificate.png) 

5. <span data-ttu-id="04e6f-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="04e6f-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshgrade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="04e6f-168">在 hello **FreshGrade 組態**區段中，按一下**設定 FreshGrade** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="04e6f-168">On hello **FreshGrade Configuration** section, click **Configure FreshGrade** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="04e6f-169">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="04e6f-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_configure.png) 

7. <span data-ttu-id="04e6f-171">toogenerate hello**中繼資料**url，請執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="04e6f-171">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="04e6f-172">a.</span><span class="sxs-lookup"><span data-stu-id="04e6f-172">a.</span></span> <span data-ttu-id="04e6f-173">按一下 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="04e6f-173">Click **App registrations**.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appregistrations.png)
   
    <span data-ttu-id="04e6f-175">b.</span><span class="sxs-lookup"><span data-stu-id="04e6f-175">b.</span></span> <span data-ttu-id="04e6f-176">按一下**端點**tooopen**端點** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="04e6f-176">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![設定單一登入](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpointicon.png)

    <span data-ttu-id="04e6f-178">c.</span><span class="sxs-lookup"><span data-stu-id="04e6f-178">c.</span></span> <span data-ttu-id="04e6f-179">按一下 hello 複製按鈕 toocopy**同盟中繼資料文件**url 並將它貼到 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="04e6f-179">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpoint.png)
     
    <span data-ttu-id="04e6f-181">d.</span><span class="sxs-lookup"><span data-stu-id="04e6f-181">d.</span></span> <span data-ttu-id="04e6f-182">現在請 toohello 屬性頁的**FreshGrade**和複製 hello**應用程式識別碼**使用**複製**按鈕，並將它貼到 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="04e6f-182">Now go toohello property page of **FreshGrade** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appid.png)

    <span data-ttu-id="04e6f-184">e.</span><span class="sxs-lookup"><span data-stu-id="04e6f-184">e.</span></span> <span data-ttu-id="04e6f-185">產生 hello**中繼資料 URL**使用 hello 下列模式：`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="04e6f-185">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

8. <span data-ttu-id="04e6f-186">tooconfigure 單一登入上**FreshGrade**側邊，您需要 toosend hello**中繼資料 URL**和**SAML 單一登入服務 URL**太[FreshGrade支援小組](mailTo:support@freshgrade.com)。</span><span class="sxs-lookup"><span data-stu-id="04e6f-186">tooconfigure single sign-on on **FreshGrade** side, you need toosend hello **Metadata URL** and **SAML Single Sign-On Service URL** too[FreshGrade support team](mailTo:support@freshgrade.com).</span></span> <span data-ttu-id="04e6f-187">設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。</span><span class="sxs-lookup"><span data-stu-id="04e6f-187">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="04e6f-188">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="04e6f-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="04e6f-189">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="04e6f-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="04e6f-190">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="04e6f-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="04e6f-191">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="04e6f-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="04e6f-192">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="04e6f-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="04e6f-194">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="04e6f-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="04e6f-195">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="04e6f-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="04e6f-197">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="04e6f-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="04e6f-199">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="04e6f-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="04e6f-201">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="04e6f-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="04e6f-203">a.</span><span class="sxs-lookup"><span data-stu-id="04e6f-203">a.</span></span> <span data-ttu-id="04e6f-204">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="04e6f-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="04e6f-205">b.</span><span class="sxs-lookup"><span data-stu-id="04e6f-205">b.</span></span> <span data-ttu-id="04e6f-206">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="04e6f-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="04e6f-207">c.</span><span class="sxs-lookup"><span data-stu-id="04e6f-207">c.</span></span> <span data-ttu-id="04e6f-208">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="04e6f-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="04e6f-209">d.</span><span class="sxs-lookup"><span data-stu-id="04e6f-209">d.</span></span> <span data-ttu-id="04e6f-210">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="04e6f-210">Click **Create**.</span></span>
 
### <a name="creating-a-freshgrade-test-user"></a><span data-ttu-id="04e6f-211">建立 FreshGrade 測試使用者</span><span class="sxs-lookup"><span data-stu-id="04e6f-211">Creating a FreshGrade test user</span></span>

<span data-ttu-id="04e6f-212">在本節中，您要在 FreshGrade 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="04e6f-212">In this section, you create a user called Britta Simon in FreshGrade.</span></span> <span data-ttu-id="04e6f-213">請使用[FreshGrade 支援小組](mailTo:support@freshgrade.com)tooadd hello hello FreshGrade 平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="04e6f-213">Please work with [FreshGrade support team](mailTo:support@freshgrade.com) tooadd hello users in hello FreshGrade platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="04e6f-214">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="04e6f-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="04e6f-215">在本節中，您可以授與存取 tooFreshGrade 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="04e6f-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFreshGrade.</span></span>

![指派使用者][200] 

<span data-ttu-id="04e6f-217">**tooassign 許 Simon tooFreshGrade，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="04e6f-217">**tooassign Britta Simon tooFreshGrade, perform hello following steps:**</span></span>

1. <span data-ttu-id="04e6f-218">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="04e6f-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="04e6f-220">在 [hello] 應用程式清單中，選取**FreshGrade**。</span><span class="sxs-lookup"><span data-stu-id="04e6f-220">In hello applications list, select **FreshGrade**.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_app.png) 

3. <span data-ttu-id="04e6f-222">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="04e6f-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="04e6f-224">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="04e6f-224">Click **Add** button.</span></span> <span data-ttu-id="04e6f-225">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="04e6f-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="04e6f-227">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="04e6f-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="04e6f-228">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="04e6f-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="04e6f-229">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="04e6f-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="04e6f-230">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="04e6f-230">Testing single sign-on</span></span>

<span data-ttu-id="04e6f-231">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="04e6f-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="04e6f-232">當您按一下 hello FreshGrade 磚 hello 存取面板中的時，您應該取得自動登入 tooyour FreshGrade 應用程式。</span><span class="sxs-lookup"><span data-stu-id="04e6f-232">When you click hello FreshGrade tile in hello Access Panel, you should get automatically signed-on tooyour FreshGrade application.</span></span>
<span data-ttu-id="04e6f-233">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="04e6f-233">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="04e6f-234">其他資源</span><span class="sxs-lookup"><span data-stu-id="04e6f-234">Additional resources</span></span>

* [<span data-ttu-id="04e6f-235">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="04e6f-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="04e6f-236">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="04e6f-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_203.png


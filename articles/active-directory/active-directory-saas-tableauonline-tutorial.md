---
title: "教學課程：Azure Active Directory 與 Tableau Online 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與線上 Tableau 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 590b2674270c340b4750c7b6feeaf4f0df4bf853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="1c09e-103">教學課程：Azure Active Directory 與 Tableau Online 整合</span><span class="sxs-lookup"><span data-stu-id="1c09e-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>

<span data-ttu-id="1c09e-104">在此教學課程中，您學會如何 toointegrate Tableau Online 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="1c09e-104">In this tutorial, you learn how toointegrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1c09e-105">與 Azure AD 整合 Tableau 線上可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="1c09e-105">Integrating Tableau Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1c09e-106">您可以控制存取 tooTableau 線上 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="1c09e-106">You can control in Azure AD who has access tooTableau Online</span></span>
- <span data-ttu-id="1c09e-107">您可以啟用您的使用者 tooautomatically get 登入 tooTableau 線上 （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="1c09e-107">You can enable your users tooautomatically get signed-on tooTableau Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1c09e-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="1c09e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1c09e-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="1c09e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c09e-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1c09e-110">Prerequisites</span></span>

<span data-ttu-id="1c09e-111">tooconfigure Tableau Online 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="1c09e-111">tooconfigure Azure AD integration with Tableau Online, you need hello following items:</span></span>

- <span data-ttu-id="1c09e-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1c09e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1c09e-113">已啟用 Tableau Online 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1c09e-113">A Tableau Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1c09e-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="1c09e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1c09e-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="1c09e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1c09e-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1c09e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1c09e-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="1c09e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1c09e-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="1c09e-118">Scenario description</span></span>
<span data-ttu-id="1c09e-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1c09e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1c09e-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="1c09e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1c09e-121">新增線上 Tableau 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="1c09e-121">Adding Tableau Online from hello gallery</span></span>
2. <span data-ttu-id="1c09e-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1c09e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-online-from-hello-gallery"></a><span data-ttu-id="1c09e-123">新增線上 Tableau 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="1c09e-123">Adding Tableau Online from hello gallery</span></span>
<span data-ttu-id="1c09e-124">tooconfigure hello 整合 Tableau 線上到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Tableau 線上。</span><span class="sxs-lookup"><span data-stu-id="1c09e-124">tooconfigure hello integration of Tableau Online into Azure AD, you need tooadd Tableau Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1c09e-125">**tooadd Tableau 線上 hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1c09e-125">**tooadd Tableau Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c09e-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="1c09e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1c09e-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1c09e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1c09e-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1c09e-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="1c09e-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="1c09e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="1c09e-133">在 [hello] 搜尋方塊中，輸入**Tableau 線上**。</span><span class="sxs-lookup"><span data-stu-id="1c09e-133">In hello search box, type **Tableau Online**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. <span data-ttu-id="1c09e-135">在 [hello [結果] 窗格中，選取 [ **Tableau 線上**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c09e-135">In hello results panel, select **Tableau Online**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1c09e-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1c09e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1c09e-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Tableau Online 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1c09e-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1c09e-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 Tableau 線上中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="1c09e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tableau Online is tooa user in Azure AD.</span></span> <span data-ttu-id="1c09e-140">換句話說，Azure AD 使用者與 hello Tableau 線上中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="1c09e-140">In other words, a link relationship between an Azure AD user and hello related user in Tableau Online needs toobe established.</span></span>

<span data-ttu-id="1c09e-141">Tableau 線上中指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1c09e-141">In Tableau Online, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1c09e-142">tooconfigure 和測試 Azure AD 單一登入與 Tableau Online，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="1c09e-142">tooconfigure and test Azure AD single sign-on with Tableau Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1c09e-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="1c09e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1c09e-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="1c09e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1c09e-145">**[建立測試使用者 Tableau 線上](#creating-a-tableau-online-test-user)** -toohave 許 Simon Tableau Online 連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="1c09e-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - toohave a counterpart of Britta Simon in Tableau Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1c09e-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1c09e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1c09e-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="1c09e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1c09e-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1c09e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1c09e-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Tableau 線上應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="1c09e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tableau Online application.</span></span>

<span data-ttu-id="1c09e-150">**tooconfigure Azure AD 單一登入與 Tableau Online，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1c09e-150">**tooconfigure Azure AD single sign-on with Tableau Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c09e-151">在 Azure 入口網站上 hello hello **Tableau 線上**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="1c09e-151">In hello Azure portal, on hello **Tableau Online** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="1c09e-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1c09e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. <span data-ttu-id="1c09e-155">在 [hello **Tableau 線上網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c09e-155">On hello **Tableau Online Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    <span data-ttu-id="1c09e-157">a.</span><span class="sxs-lookup"><span data-stu-id="1c09e-157">a.</span></span> <span data-ttu-id="1c09e-158">在 [hello**登入 URL**文字方塊中，型別 hello URL:`https://sso.online.tableau.com`</span><span class="sxs-lookup"><span data-stu-id="1c09e-158">In hello **Sign-on URL** textbox, type hello URL: `https://sso.online.tableau.com`</span></span>

    <span data-ttu-id="1c09e-159">b.</span><span class="sxs-lookup"><span data-stu-id="1c09e-159">b.</span></span> <span data-ttu-id="1c09e-160">在 [hello**識別碼**文字方塊中，型別 hello URL:`https://sso.online.tableau.com/public/sp/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="1c09e-160">In hello **Identifier** textbox, type hello URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span></span>

4. <span data-ttu-id="1c09e-161">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="1c09e-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. <span data-ttu-id="1c09e-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="1c09e-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1c09e-165">在不同的瀏覽器視窗中，登入 tooyour Tableau 線上應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c09e-165">In a different browser window, sign-on tooyour Tableau Online application.</span></span> <span data-ttu-id="1c09e-166">跳過**設定**然後**驗證**。</span><span class="sxs-lookup"><span data-stu-id="1c09e-166">Go too**Settings** and then **Authentication**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. <span data-ttu-id="1c09e-168">tooenable SAML 下**驗證類型**> 一節。</span><span class="sxs-lookup"><span data-stu-id="1c09e-168">tooenable SAML, Under **Authentication Types** section.</span></span> <span data-ttu-id="1c09e-169">檢查 hello**單一登入與 SAML**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1c09e-169">Check hello **Single sign-on with SAML** checkbox.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. <span data-ttu-id="1c09e-171">向下捲動到 [將中繼資料檔匯入到 Tableau Online]  區段。</span><span class="sxs-lookup"><span data-stu-id="1c09e-171">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="1c09e-172">按一下 [瀏覽，並匯入您從 Azure AD 已下載的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="1c09e-172">Click Browse and import hello metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="1c09e-173">然後，按一下 [套用] 。</span><span class="sxs-lookup"><span data-stu-id="1c09e-173">Then, click **Apply**.</span></span>
   
   ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. <span data-ttu-id="1c09e-175">在 [hello**比對判斷提示**區段中，插入 hello 對應身分識別提供者判斷提示名稱**電子郵件地址**，**名字**，和**姓氏**.</span><span class="sxs-lookup"><span data-stu-id="1c09e-175">In hello **Match assertions** section, insert hello corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span></span> <span data-ttu-id="1c09e-176">tooget Azure AD 的這項資訊：</span><span class="sxs-lookup"><span data-stu-id="1c09e-176">tooget this information from Azure AD:</span></span> 
  
    <span data-ttu-id="1c09e-177">a.</span><span class="sxs-lookup"><span data-stu-id="1c09e-177">a.</span></span> <span data-ttu-id="1c09e-178">在 [hello Azure 入口網站中移入 hello **Tableau 線上**應用程式整合頁面。</span><span class="sxs-lookup"><span data-stu-id="1c09e-178">In hello Azure portal, go on hello **Tableau Online** application integration page.</span></span>
    
    <span data-ttu-id="1c09e-179">b.</span><span class="sxs-lookup"><span data-stu-id="1c09e-179">b.</span></span> <span data-ttu-id="1c09e-180">在 [hello 屬性區段中，選取 [hello **」 檢視及編輯所有其他使用者的屬性"**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1c09e-180">In hello attributes section, Select hello **"view and edit all other user attributes"** checkbox.</span></span> 
    
   ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    <span data-ttu-id="1c09e-182">c.</span><span class="sxs-lookup"><span data-stu-id="1c09e-182">c.</span></span> <span data-ttu-id="1c09e-183">複製 hello 命名空間值，這些屬性： givenname、 電子郵件和姓氏使用 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1c09e-183">Copy hello namespace value for these attributes: givenname, email and surname by using hello following steps:</span></span>

   ![Azure AD 單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    <span data-ttu-id="1c09e-185">d.</span><span class="sxs-lookup"><span data-stu-id="1c09e-185">d.</span></span> <span data-ttu-id="1c09e-186">按一下 [user.givenname] 值</span><span class="sxs-lookup"><span data-stu-id="1c09e-186">Click **user.givenname** value</span></span> 
    
    <span data-ttu-id="1c09e-187">e.</span><span class="sxs-lookup"><span data-stu-id="1c09e-187">e.</span></span> <span data-ttu-id="1c09e-188">從 hello 複製 hello 值**命名空間**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="1c09e-188">Copy hello value from hello **namespace** textbox.</span></span>

   ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    <span data-ttu-id="1c09e-190">f.</span><span class="sxs-lookup"><span data-stu-id="1c09e-190">f.</span></span> <span data-ttu-id="1c09e-191">hello 電子郵件和姓氏 toocopy hello 為命名空間值會遵循上述步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="1c09e-191">toocopy hello namesapce values for hello email and surname follow hello preceding steps.</span></span>

    <span data-ttu-id="1c09e-192">g.</span><span class="sxs-lookup"><span data-stu-id="1c09e-192">g.</span></span> <span data-ttu-id="1c09e-193">切換 toohello Tableau 線上應用程式，然後設定 hello **Tableau 線上屬性**區段，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1c09e-193">Switch toohello Tableau Online application, then set hello **Tableau Online Attributes** section as follows:</span></span>
     * <span data-ttu-id="1c09e-194">電子郵件︰**mail** 或 **userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="1c09e-194">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="1c09e-195">名字︰ **givenname**</span><span class="sxs-lookup"><span data-stu-id="1c09e-195">First name: **givenname**</span></span>
     * <span data-ttu-id="1c09e-196">姓氏︰ **surname**</span><span class="sxs-lookup"><span data-stu-id="1c09e-196">Last name: **surname**</span></span>
   
   ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> <span data-ttu-id="1c09e-198">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="1c09e-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1c09e-199">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="1c09e-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1c09e-200">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1c09e-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1c09e-201">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1c09e-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="1c09e-202">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="1c09e-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="1c09e-204">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1c09e-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c09e-205">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="1c09e-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1c09e-207">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="1c09e-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1c09e-209">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="1c09e-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1c09e-211">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c09e-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1c09e-213">a.</span><span class="sxs-lookup"><span data-stu-id="1c09e-213">a.</span></span> <span data-ttu-id="1c09e-214">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="1c09e-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1c09e-215">b.</span><span class="sxs-lookup"><span data-stu-id="1c09e-215">b.</span></span> <span data-ttu-id="1c09e-216">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="1c09e-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1c09e-217">c.</span><span class="sxs-lookup"><span data-stu-id="1c09e-217">c.</span></span> <span data-ttu-id="1c09e-218">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="1c09e-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1c09e-219">d.</span><span class="sxs-lookup"><span data-stu-id="1c09e-219">d.</span></span> <span data-ttu-id="1c09e-220">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1c09e-220">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-online-test-user"></a><span data-ttu-id="1c09e-221">建立 Tableau Online 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1c09e-221">Creating a Tableau Online test user</span></span>

<span data-ttu-id="1c09e-222">在本節中，您要在 Tableau Online 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="1c09e-222">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="1c09e-223">在 [Tableau Online] 中，依序按一下 [設定] 和 [驗證] 區段。</span><span class="sxs-lookup"><span data-stu-id="1c09e-223">On **Tableau Online**, click **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="1c09e-224">向下捲動太**選取使用者**> 一節。</span><span class="sxs-lookup"><span data-stu-id="1c09e-224">Scroll down too**Select Users** section.</span></span> <span data-ttu-id="1c09e-225">依序按一下 [新增使用者] 和 [輸入電子郵件地址]。</span><span class="sxs-lookup"><span data-stu-id="1c09e-225">Click **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. <span data-ttu-id="1c09e-227">選取 [新增單一登入 (SSO) 驗證的使用者] 。</span><span class="sxs-lookup"><span data-stu-id="1c09e-227">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="1c09e-228">在 [hello**輸入電子郵件地址**加入文字方塊britta.simon@contoso.com</span><span class="sxs-lookup"><span data-stu-id="1c09e-228">In hello **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. <span data-ttu-id="1c09e-230">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1c09e-230">Click **Create**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1c09e-231">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="1c09e-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1c09e-232">在本節中，您可以授與存取 tooTableau 線上啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1c09e-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTableau Online.</span></span>

![指派使用者][200] 

<span data-ttu-id="1c09e-234">**tooassign 許 Simon tooTableau 上線，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1c09e-234">**tooassign Britta Simon tooTableau Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c09e-235">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1c09e-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="1c09e-237">在 [hello] 應用程式清單中，選取**Tableau 線上**。</span><span class="sxs-lookup"><span data-stu-id="1c09e-237">In hello applications list, select **Tableau Online**.</span></span>

    ![設定單一登入](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. <span data-ttu-id="1c09e-239">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="1c09e-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="1c09e-241">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1c09e-241">Click **Add** button.</span></span> <span data-ttu-id="1c09e-242">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1c09e-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="1c09e-244">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="1c09e-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1c09e-245">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1c09e-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1c09e-246">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1c09e-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1c09e-247">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="1c09e-247">Testing single sign-on</span></span>

<span data-ttu-id="1c09e-248">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="1c09e-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="1c09e-249">當您按一下 hello Tableau 線上磚 hello 存取面板中的時，您應該取得自動登入 tooyour Tableau 線上應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c09e-249">When you click hello Tableau Online tile in hello Access Panel, you should get automatically signed-on tooyour Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1c09e-250">其他資源</span><span class="sxs-lookup"><span data-stu-id="1c09e-250">Additional resources</span></span>

* [<span data-ttu-id="1c09e-251">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c09e-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1c09e-252">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="1c09e-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png


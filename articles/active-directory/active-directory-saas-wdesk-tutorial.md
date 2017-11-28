---
title: "教學課程：Azure Active Directory 與 Wdesk 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Wdesk 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 2c278a5e4f50cc362663efc0f826ff0c0fcf6e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a><span data-ttu-id="c1b1e-103">教學課程：Azure Active Directory 與 Wdesk 整合</span><span class="sxs-lookup"><span data-stu-id="c1b1e-103">Tutorial: Azure Active Directory integration with Wdesk</span></span>

<span data-ttu-id="c1b1e-104">在此教學課程中，您學會如何 toointegrate Wdesk 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-104">In this tutorial, you learn how toointegrate Wdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c1b1e-105">與 Azure AD 整合 Wdesk 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="c1b1e-105">Integrating Wdesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c1b1e-106">您可以控制存取 tooWdesk Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="c1b1e-106">You can control in Azure AD who has access tooWdesk</span></span>
- <span data-ttu-id="c1b1e-107">您可以啟用您的使用者 tooautomatically get 登入 tooWdesk （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="c1b1e-107">You can enable your users tooautomatically get signed-on tooWdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c1b1e-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c1b1e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c1b1e-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="c1b1e-110">[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1b1e-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="c1b1e-111">Prerequisites</span></span>

<span data-ttu-id="c1b1e-112">tooconfigure Wdesk 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="c1b1e-112">tooconfigure Azure AD integration with Wdesk, you need hello following items:</span></span>

- <span data-ttu-id="c1b1e-113">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c1b1e-113">An Azure AD subscription</span></span>
- <span data-ttu-id="c1b1e-114">已啟用 Wdesk 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c1b1e-114">A Wdesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c1b1e-115">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c1b1e-116">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="c1b1e-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c1b1e-117">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c1b1e-118">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c1b1e-119">案例描述</span><span class="sxs-lookup"><span data-stu-id="c1b1e-119">Scenario description</span></span>
<span data-ttu-id="c1b1e-120">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c1b1e-121">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="c1b1e-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c1b1e-122">從 hello 圖庫加入 Wdesk</span><span class="sxs-lookup"><span data-stu-id="c1b1e-122">Adding Wdesk from hello gallery</span></span>
2. <span data-ttu-id="c1b1e-123">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c1b1e-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wdesk-from-hello-gallery"></a><span data-ttu-id="c1b1e-124">從 hello 圖庫加入 Wdesk</span><span class="sxs-lookup"><span data-stu-id="c1b1e-124">Adding Wdesk from hello gallery</span></span>
<span data-ttu-id="c1b1e-125">tooconfigure hello 整合 Wdesk 到 Azure AD，您需要 tooadd Wdesk hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-125">tooconfigure hello integration of Wdesk into Azure AD, you need tooadd Wdesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c1b1e-126">**tooadd Wdesk 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c1b1e-126">**tooadd Wdesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1b1e-127">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c1b1e-129">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c1b1e-130">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-130">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="c1b1e-132">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="c1b1e-134">在 [hello] 搜尋方塊中，輸入**Wdesk**。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-134">In hello search box, type **Wdesk**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. <span data-ttu-id="c1b1e-136">在 [hello [結果] 窗格中，選取 [ **Wdesk**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-136">In hello results panel, select **Wdesk**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c1b1e-138">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c1b1e-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c1b1e-139">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Wdesk 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-139">In this section, you configure and test Azure AD single sign-on with Wdesk based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c1b1e-140">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Wdesk 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wdesk is tooa user in Azure AD.</span></span> <span data-ttu-id="c1b1e-141">換句話說，Azure AD 使用者與 hello Wdesk 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-141">In other words, a link relationship between an Azure AD user and hello related user in Wdesk needs toobe established.</span></span>

<span data-ttu-id="c1b1e-142">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Wdesk 中。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wdesk.</span></span>

<span data-ttu-id="c1b1e-143">tooconfigure 及 Wdesk 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="c1b1e-143">tooconfigure and test Azure AD single sign-on with Wdesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c1b1e-144">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c1b1e-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c1b1e-146">**[建立測試使用者 Wdesk](#creating-a-wdesk-test-user) ** -toohave 許 Simon Wdesk 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-146">**[Creating a Wdesk test user](#creating-a-wdesk-test-user)** - toohave a counterpart of Britta Simon in Wdesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c1b1e-147">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c1b1e-148">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c1b1e-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c1b1e-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c1b1e-150">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Wdesk 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wdesk application.</span></span>

<span data-ttu-id="c1b1e-151">**tooconfigure Azure AD 單一登入與 Wdesk，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c1b1e-151">**tooconfigure Azure AD single sign-on with Wdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1b1e-152">在 Azure 入口網站上 hello hello **Wdesk**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-152">In hello Azure portal, on hello **Wdesk** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="c1b1e-154">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. <span data-ttu-id="c1b1e-156">在 [hello **Wdesk 網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**IDP**初始的模式執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c1b1e-156">On hello **Wdesk Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    <span data-ttu-id="c1b1e-158">a.</span><span class="sxs-lookup"><span data-stu-id="c1b1e-158">a.</span></span> <span data-ttu-id="c1b1e-159">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="c1b1e-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span></span>

    <span data-ttu-id="c1b1e-160">b.</span><span class="sxs-lookup"><span data-stu-id="c1b1e-160">b.</span></span> <span data-ttu-id="c1b1e-161">在 [hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="c1b1e-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span></span>

4. <span data-ttu-id="c1b1e-162">按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="c1b1e-163">如果您想 tooconfigure hello 應用程式中的**SP**起始模式中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c1b1e-163">If you wish tooconfigure hello application in **SP** initiated mode, perform hello following step:</span></span>

    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    <span data-ttu-id="c1b1e-165">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="c1b1e-165">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="c1b1e-166">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-166">These values are not real.</span></span> <span data-ttu-id="c1b1e-167">更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="c1b1e-168">取得這些值從 WDesk 入口網站時設定 hello SSO。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-168">You get these values from WDesk portal when you configure hello SSO.</span></span> 
  
5. <span data-ttu-id="c1b1e-169">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. <span data-ttu-id="c1b1e-171">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-171">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="c1b1e-173">在不同的網頁瀏覽器視窗中，登入 tooWdesk 做為安全性系統管理員。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-173">In a different web browser window, login tooWdesk as a Security Administrator.</span></span>

8. <span data-ttu-id="c1b1e-174">在 [hello 左下方，按一下 [ **Admin**選擇**帳戶管理員**:</span><span class="sxs-lookup"><span data-stu-id="c1b1e-174">In hello bottom left, click **Admin** and choose **Account Admin**:</span></span>
 
     ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. <span data-ttu-id="c1b1e-176">Wdesk 系統管理員，在瀏覽過**安全性**，然後**SAML** > **SAML 設定**:</span><span class="sxs-lookup"><span data-stu-id="c1b1e-176">In Wdesk Admin, navigate too**Security**, then **SAML** > **SAML Settings**:</span></span>

    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. <span data-ttu-id="c1b1e-178">在下**一般設定**，檢查 hello**啟用 SAML 單一登入**:</span><span class="sxs-lookup"><span data-stu-id="c1b1e-178">Under **General Settings**, check hello **Enable SAML Single Sign On**:</span></span>

    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. <span data-ttu-id="c1b1e-180">在下**服務提供者詳細資料**，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c1b1e-180">Under **Service Provider Details**, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      <span data-ttu-id="c1b1e-182">a.</span><span class="sxs-lookup"><span data-stu-id="c1b1e-182">a.</span></span> <span data-ttu-id="c1b1e-183">複製 hello**登入 URL**中貼上和**登入 Url** Azure 入口網站上的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-183">Copy hello **Login URL** and paste it in **Sign-on Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="c1b1e-184">b.</span><span class="sxs-lookup"><span data-stu-id="c1b1e-184">b.</span></span> <span data-ttu-id="c1b1e-185">複製 hello**中繼資料 Url**中貼上和**識別碼**Azure 入口網站上的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-185">Copy hello **Metadata Url** and paste it in **Identifier** textbox on Azure portal.</span></span>
       
      <span data-ttu-id="c1b1e-186">c.</span><span class="sxs-lookup"><span data-stu-id="c1b1e-186">c.</span></span> <span data-ttu-id="c1b1e-187">複製 hello**取用者 url**中貼上和**回覆 Url** Azure 入口網站上的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-187">Copy hello **Consumer url** and paste it in **Reply Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="c1b1e-188">d.</span><span class="sxs-lookup"><span data-stu-id="c1b1e-188">d.</span></span> <span data-ttu-id="c1b1e-189">按一下**儲存**Azure 入口網站 toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-189">Click **Save** on Azure portal toosave hello changes.</span></span>      

12. <span data-ttu-id="c1b1e-190">按一下**設定 IdP** tooopen**編輯 IdP 設定**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-190">Click **Configure IdP Settings** tooopen **Edit IdP Settings** dialog.</span></span> <span data-ttu-id="c1b1e-191">按一下**選擇檔案**toolocate hello **Metadata.xml** Azure 入口網站，從儲存的檔案再將它上傳。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-191">Click **Choose File** toolocate hello **Metadata.xml** file you saved from Azure portal, then upload it.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. <span data-ttu-id="c1b1e-193">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-193">Click **Save changes**.</span></span>

    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> <span data-ttu-id="c1b1e-195">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="c1b1e-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c1b1e-196">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c1b1e-197">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c1b1e-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c1b1e-198">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c1b1e-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="c1b1e-199">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="c1b1e-201">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c1b1e-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1b1e-202">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c1b1e-204">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c1b1e-206">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c1b1e-208">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c1b1e-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c1b1e-210">a.</span><span class="sxs-lookup"><span data-stu-id="c1b1e-210">a.</span></span> <span data-ttu-id="c1b1e-211">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c1b1e-212">b.</span><span class="sxs-lookup"><span data-stu-id="c1b1e-212">b.</span></span> <span data-ttu-id="c1b1e-213">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c1b1e-214">c.</span><span class="sxs-lookup"><span data-stu-id="c1b1e-214">c.</span></span> <span data-ttu-id="c1b1e-215">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c1b1e-216">d.</span><span class="sxs-lookup"><span data-stu-id="c1b1e-216">d.</span></span> <span data-ttu-id="c1b1e-217">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-217">Click **Create**.</span></span>
 
### <a name="creating-a-wdesk-test-user"></a><span data-ttu-id="c1b1e-218">建立 Wdesk 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c1b1e-218">Creating a Wdesk test user</span></span>

<span data-ttu-id="c1b1e-219">tooenable Azure AD 使用者 toolog 中 tooWdesk，它們必須佈建到 Wdesk。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-219">tooenable Azure AD users toolog in tooWdesk, they must be provisioned into Wdesk.</span></span> <span data-ttu-id="c1b1e-220">在 Wdesk 中，需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-220">In Wdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="c1b1e-221">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c1b1e-221">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1b1e-222">安全性系統管理員身分登入 tooWdesk 中。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-222">Log in tooWdesk as a Security Administrator.</span></span>
2. <span data-ttu-id="c1b1e-223">瀏覽過**Admin** > **帳戶管理員**。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-223">Navigate too**Admin** > **Account Admin**.</span></span>

     ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. <span data-ttu-id="c1b1e-225">按一下 [人員] 下的 [成員]。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-225">Click **Members** under **People**.</span></span>

4. <span data-ttu-id="c1b1e-226">現在按一下**Add Member** tooopen **Add Member** ] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-226">Now click **Add Member** tooopen **Add Member** dialog box.</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. <span data-ttu-id="c1b1e-228">在**使用者**文字方塊中，輸入 hello 類似的使用者名稱** brittasimon@contoso.com **按一下**繼續**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-228">In **User** text box, enter hello username of user like **brittasimon@contoso.com** and click **Continue** button.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  <span data-ttu-id="c1b1e-230">輸入 hello 詳細資料，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c1b1e-230">Enter hello details as shown below:</span></span>
  
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    <span data-ttu-id="c1b1e-232">a.</span><span class="sxs-lookup"><span data-stu-id="c1b1e-232">a.</span></span> <span data-ttu-id="c1b1e-233">在**電子郵件**文字方塊中，輸入 hello 電子郵件的使用者，例如** brittasimon@contoso.com **。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-233">In **E-mail** text box, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="c1b1e-234">b.</span><span class="sxs-lookup"><span data-stu-id="c1b1e-234">b.</span></span> <span data-ttu-id="c1b1e-235">在**名字**文字方塊中，輸入 hello 名字，例如使用者的**許**。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-235">In **First Name** text box, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="c1b1e-236">c.</span><span class="sxs-lookup"><span data-stu-id="c1b1e-236">c.</span></span> <span data-ttu-id="c1b1e-237">在**姓氏**文字方塊中，輸入 hello 姓氏的使用者，例如**Simon**。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-237">In **Last Name** text box, enter hello last name of user like **Simon**.</span></span>

7. <span data-ttu-id="c1b1e-238">按一下 [儲存成員] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-238">Click **Save Member** button.</span></span>  

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c1b1e-240">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="c1b1e-240">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c1b1e-241">在本節中，您可以授與存取 tooWdesk 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-241">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWdesk.</span></span>

![指派使用者][200] 

<span data-ttu-id="c1b1e-243">**tooassign 許 Simon tooWdesk，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c1b1e-243">**tooassign Britta Simon tooWdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1b1e-244">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-244">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="c1b1e-246">在 [hello] 應用程式清單中，選取**Wdesk**。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-246">In hello applications list, select **Wdesk**.</span></span>

    ![設定單一登入](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. <span data-ttu-id="c1b1e-248">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-248">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="c1b1e-250">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-250">Click **Add** button.</span></span> <span data-ttu-id="c1b1e-251">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="c1b1e-253">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-253">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c1b1e-254">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c1b1e-255">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c1b1e-256">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="c1b1e-256">Testing single sign-on</span></span>

<span data-ttu-id="c1b1e-257">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-257">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c1b1e-258">當您按一下 hello Wdesk 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Wdesk 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-258">When you click hello Wdesk tile in hello Access Panel, you should get automatically signed-on tooyour Wdesk application.</span></span>
<span data-ttu-id="c1b1e-259">如需存取面板的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="c1b1e-259">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c1b1e-260">其他資源</span><span class="sxs-lookup"><span data-stu-id="c1b1e-260">Additional resources</span></span>

* [<span data-ttu-id="c1b1e-261">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1b1e-261">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c1b1e-262">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="c1b1e-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png


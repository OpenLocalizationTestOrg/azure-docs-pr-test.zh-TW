---
title: "教學課程：Azure Active Directory 與 T&E Express 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 和 （& h） E Express 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 9a568ace8dbc75fadbf37554996b1b597a813d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a><span data-ttu-id="53ee8-103">教學課程：Azure Active Directory 與 T&E Express 整合</span><span class="sxs-lookup"><span data-stu-id="53ee8-103">Tutorial: Azure Active Directory integration with T&E Express</span></span>

<span data-ttu-id="53ee8-104">在此教學課程中，您學會如何 toointegrate （& H) E Express 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="53ee8-104">In this tutorial, you learn how toointegrate T&E Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="53ee8-105">與 Azure AD 整合 （& h） E Express 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="53ee8-105">Integrating T&E Express with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="53ee8-106">您可以控制存取 tooT Azure AD 與 E Express</span><span class="sxs-lookup"><span data-stu-id="53ee8-106">You can control in Azure AD who has access tooT&E Express</span></span>
- <span data-ttu-id="53ee8-107">您可以使用其 Azure AD 帳戶啟用使用者 tooautomatically get 登入 tooT & 電子 Express （單一登入）</span><span class="sxs-lookup"><span data-stu-id="53ee8-107">You can enable your users tooautomatically get signed-on tooT&E Express (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="53ee8-108">您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站</span><span class="sxs-lookup"><span data-stu-id="53ee8-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="53ee8-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="53ee8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53ee8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="53ee8-110">Prerequisites</span></span>

<span data-ttu-id="53ee8-111">tooconfigure （& h） E Express 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="53ee8-111">tooconfigure Azure AD integration with T&E Express, you need hello following items:</span></span>

- <span data-ttu-id="53ee8-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="53ee8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="53ee8-113">已啟用 T&E Express 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="53ee8-113">A T&E Express single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="53ee8-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="53ee8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="53ee8-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="53ee8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="53ee8-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="53ee8-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="53ee8-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="53ee8-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="53ee8-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="53ee8-118">Scenario description</span></span>
<span data-ttu-id="53ee8-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="53ee8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="53ee8-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="53ee8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="53ee8-121">從 hello 圖庫加入 （& h） E Express</span><span class="sxs-lookup"><span data-stu-id="53ee8-121">Adding T&E Express from hello gallery</span></span>
2. <span data-ttu-id="53ee8-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="53ee8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-te-express-from-hello-gallery"></a><span data-ttu-id="53ee8-123">從 hello 圖庫加入 （& h） E Express</span><span class="sxs-lookup"><span data-stu-id="53ee8-123">Adding T&E Express from hello gallery</span></span>
<span data-ttu-id="53ee8-124">tooconfigure hello 整合 （& h） E Express 到 Azure AD，您需要 tooadd T & 電子 Express hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="53ee8-124">tooconfigure hello integration of T&E Express into Azure AD, you need tooadd T&E Express from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="53ee8-125">**tooadd T & 電子 Express 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="53ee8-125">**tooadd T&E Express from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="53ee8-126">在 [hello ** [Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="53ee8-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="53ee8-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="53ee8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="53ee8-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="53ee8-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="53ee8-131">按一下**新增**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="53ee8-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="53ee8-133">在 [hello] 搜尋方塊中，輸入**（& H) E Express**。</span><span class="sxs-lookup"><span data-stu-id="53ee8-133">In hello search box, type **T&E Express**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. <span data-ttu-id="53ee8-135">在 hello [結果] 窗格中，選取**（& H) E Express**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="53ee8-135">In hello results panel, select **T&E Express**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="53ee8-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="53ee8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="53ee8-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 T&E Express 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="53ee8-138">In this section, you configure and test Azure AD single sign-on with T&E Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="53ee8-139">單一登入 toowork，Azure AD 需要 tooknow 哪些 hello 對應項目中的使用者 （& h） E Express 都 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="53ee8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in T&E Express is tooa user in Azure AD.</span></span> <span data-ttu-id="53ee8-140">換句話說，Azure AD 使用者與 hello 之間的連結關聯性相關的建立 （& H) E Express 需求 toobe 中的使用者。</span><span class="sxs-lookup"><span data-stu-id="53ee8-140">In other words, a link relationship between an Azure AD user and hello related user in T&E Express needs toobe established.</span></span>

<span data-ttu-id="53ee8-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**使用者名稱**中 （& h） E Express。</span><span class="sxs-lookup"><span data-stu-id="53ee8-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in T&E Express.</span></span>

<span data-ttu-id="53ee8-142">tooconfigure 及 Azure AD 單一登入 （& h） E Express 使用的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="53ee8-142">tooconfigure and test Azure AD single sign-on with T&E Express, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="53ee8-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="53ee8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="53ee8-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="53ee8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="53ee8-145">**[建立測試使用者 （& h） E Express](#creating-a-te-express-test-user) ** -toohave 許 Simon 中 （& h） E Express 是連結的 toohello Azure AD 的她的表示法的對應項目。</span><span class="sxs-lookup"><span data-stu-id="53ee8-145">**[Creating a T&E Express test user](#creating-a-te-express-test-user)** - toohave a counterpart of Britta Simon in T&E Express that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="53ee8-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="53ee8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="53ee8-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="53ee8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="53ee8-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="53ee8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="53ee8-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並設定單一登入 （& h） E Express 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="53ee8-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your T&E Express application.</span></span>

<span data-ttu-id="53ee8-150">**tooconfigure Azure AD 單一登入 （& h） E Express 中，以執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="53ee8-150">**tooconfigure Azure AD single sign-on with T&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="53ee8-151">在 hello Azure 管理入口網站上 hello **（& H) E Express**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="53ee8-151">In hello Azure Management portal, on hello **T&E Express** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="53ee8-153">在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="53ee8-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. <span data-ttu-id="53ee8-155">在 [hello **T & 電子 Express 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="53ee8-155">On hello **T&E Express Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    <span data-ttu-id="53ee8-157">a.</span><span class="sxs-lookup"><span data-stu-id="53ee8-157">a.</span></span> <span data-ttu-id="53ee8-158">在 [hello**識別碼**文字方塊中，做為型別 hello 值：`https://<domain>.tyeexpress.com`</span><span class="sxs-lookup"><span data-stu-id="53ee8-158">In hello **Identifier** textbox, type hello value as: `https://<domain>.tyeexpress.com`</span></span>

    <span data-ttu-id="53ee8-159">b.</span><span class="sxs-lookup"><span data-stu-id="53ee8-159">b.</span></span> <span data-ttu-id="53ee8-160">在 [hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span><span class="sxs-lookup"><span data-stu-id="53ee8-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="53ee8-161">請注意這些不是 hello 實際值。</span><span class="sxs-lookup"><span data-stu-id="53ee8-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="53ee8-162">您有 tooupdate hello 實際的識別項和回覆 url 的這些值。</span><span class="sxs-lookup"><span data-stu-id="53ee8-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="53ee8-163">這裡我們建議您 toouse hello 唯一字串的值在 hello 識別項。</span><span class="sxs-lookup"><span data-stu-id="53ee8-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="53ee8-164">請連絡[（& h） E Express 支援小組](http://www.tyeexpress.com/contacto.aspx)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="53ee8-164">Contact [T&E Express support team](http://www.tyeexpress.com/contacto.aspx) tooget these values.</span></span>

5. <span data-ttu-id="53ee8-165">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="53ee8-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. <span data-ttu-id="53ee8-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="53ee8-167">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="53ee8-169">tooconfigure 單一登入上**（& H) E Express**端、 登入 toohello T & 電子快速應用程式沒有 SAML 單一登入使用管理員認證。</span><span class="sxs-lookup"><span data-stu-id="53ee8-169">tooconfigure single sign-on on **T&E Express** side, login toohello T&E express application without SAML single sign on using admin credentials.</span></span>

9. <span data-ttu-id="53ee8-170">在 hello **Admin**索引標籤上，按一下**SAML 網域**tooOpen hello SAML 設定] 頁面。</span><span class="sxs-lookup"><span data-stu-id="53ee8-170">Under hello **Admin** Tab, Click on **SAML domain** tooOpen hello SAML settings page.</span></span>

    ![設定單一登入](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. <span data-ttu-id="53ee8-172">選取 hello **Activar(Activate)**選項**否**太**SI(Yes)**。</span><span class="sxs-lookup"><span data-stu-id="53ee8-172">Select hello **Activar(Activate)** option from **No** too**SI(Yes)**.</span></span> <span data-ttu-id="53ee8-173">在 [hello**身分識別提供者中繼資料**文字方塊中，貼上 hello 中繼資料 XML 已 donwloaded 從 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="53ee8-173">In hello **Identity Provider Metadata** textbox, paste hello metadata XML which you have donwloaded from Azure portal.</span></span>

    ![設定單一登入](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. <span data-ttu-id="53ee8-175">按一下 hello **Guardar(Save)**按鈕 toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="53ee8-175">Click on hello **Guardar(Save)** button toosave hello settings.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="53ee8-176">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="53ee8-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="53ee8-177">hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="53ee8-177">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="53ee8-179">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="53ee8-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="53ee8-180">在 [hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="53ee8-180">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="53ee8-182">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="53ee8-182">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="53ee8-184">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="53ee8-184">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="53ee8-186">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="53ee8-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="53ee8-188">a.</span><span class="sxs-lookup"><span data-stu-id="53ee8-188">a.</span></span> <span data-ttu-id="53ee8-189">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="53ee8-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="53ee8-190">b.</span><span class="sxs-lookup"><span data-stu-id="53ee8-190">b.</span></span> <span data-ttu-id="53ee8-191">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="53ee8-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="53ee8-192">c.</span><span class="sxs-lookup"><span data-stu-id="53ee8-192">c.</span></span> <span data-ttu-id="53ee8-193">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="53ee8-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="53ee8-194">d.</span><span class="sxs-lookup"><span data-stu-id="53ee8-194">d.</span></span> <span data-ttu-id="53ee8-195">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="53ee8-195">Click **Create**.</span></span>
 
### <a name="creating-a-te-express-test-user"></a><span data-ttu-id="53ee8-196">建立 T&E Express 測試使用者</span><span class="sxs-lookup"><span data-stu-id="53ee8-196">Creating a T&E Express test user</span></span>

<span data-ttu-id="53ee8-197">在訂單 tooenable Azure AD 使用者 toolog 到 （& h） E Express，它們必須佈建到 （& h） E Express。</span><span class="sxs-lookup"><span data-stu-id="53ee8-197">In order tooenable Azure AD users toolog into T&E Express, they must be provisioned into T&E Express.</span></span>  
<span data-ttu-id="53ee8-198">T&E Express 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="53ee8-198">In case of T&E Express, provisioning is a manual task.</span></span>

<span data-ttu-id="53ee8-199">**tooprovision 使用者帳戶，執行下列步驟 hello:**</span><span class="sxs-lookup"><span data-stu-id="53ee8-199">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="53ee8-200">系統管理員身分登入 tooyour T & 電子 Express 公司網站。</span><span class="sxs-lookup"><span data-stu-id="53ee8-200">Log in tooyour T&E Express company site as an administrator.</span></span>

2. <span data-ttu-id="53ee8-201">管理標籤底下按一下使用者 tooopen hello 使用者主版頁面。</span><span class="sxs-lookup"><span data-stu-id="53ee8-201">Under Admin tag, click on Users tooopen hello Users master page.</span></span>

    ![新增員工](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. <span data-ttu-id="53ee8-203">在 [hello 首頁上，按一下** + ** tooadd hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="53ee8-203">On hello home page, click on **+** tooadd hello users.</span></span>

    ![新增員工](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. <span data-ttu-id="53ee8-205">要求在 hello 表單中輸入所有 hello 強制性的詳細資訊，然後按一下儲存按鈕 toosave hello 詳細資料的 hello。</span><span class="sxs-lookup"><span data-stu-id="53ee8-205">Enter all hello mandatory details as asked in hello form and click hello save button toosave hello details.</span></span>

    ![新增員工](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![新增員工](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="53ee8-208">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="53ee8-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="53ee8-209">在本節中，以啟用許 Simon toouse Azure 單一登入授與他們存取 tooT & 電子 Express。</span><span class="sxs-lookup"><span data-stu-id="53ee8-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooT&E Express.</span></span>

![指派使用者][200] 

<span data-ttu-id="53ee8-211">**tooassign 許 Simon tooT & 電子 Express，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="53ee8-211">**tooassign Britta Simon tooT&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="53ee8-212">在 [hello Azure 管理入口網站中，開啟 [hello 應用程式] 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="53ee8-212">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="53ee8-214">在 [hello] 應用程式清單中，選取**（& H) E Express**。</span><span class="sxs-lookup"><span data-stu-id="53ee8-214">In hello applications list, select **T&E Express**.</span></span>

    ![設定單一登入](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. <span data-ttu-id="53ee8-216">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="53ee8-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="53ee8-218">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="53ee8-218">Click **Add** button.</span></span> <span data-ttu-id="53ee8-219">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="53ee8-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="53ee8-221">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="53ee8-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="53ee8-222">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="53ee8-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="53ee8-223">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="53ee8-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="53ee8-224">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="53ee8-224">Testing single sign-on</span></span>

<span data-ttu-id="53ee8-225">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="53ee8-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="53ee8-226">當您按一下 hello T & 電子 Express 磚 hello 存取面板中的時，您應該取得自動登入 tooyour T & 電子 Express 應用程式。</span><span class="sxs-lookup"><span data-stu-id="53ee8-226">When you click hello T&E Express tile in hello Access Panel, you should get automatically signed-on tooyour T&E Express application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="53ee8-227">其他資源</span><span class="sxs-lookup"><span data-stu-id="53ee8-227">Additional resources</span></span>

* [<span data-ttu-id="53ee8-228">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="53ee8-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="53ee8-229">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="53ee8-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png


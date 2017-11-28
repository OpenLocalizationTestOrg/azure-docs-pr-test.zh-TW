---
title: "教學課程：Azure Active Directory 與 Land Gorilla Client 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與土地大猩猩之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: jeedes
ms.openlocfilehash: e95a30551e636108fe22a7ab6d1827bc12d7f9a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-land-gorilla-client"></a><span data-ttu-id="b2c79-103">教學課程：Azure Active Directory 與 Land Gorilla Client 整合</span><span class="sxs-lookup"><span data-stu-id="b2c79-103">Tutorial: Azure Active Directory integration with Land Gorilla Client</span></span>

<span data-ttu-id="b2c79-104">在此教學課程中，您學會如何 toointegrate 土地大猩猩用戶端與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="b2c79-104">In this tutorial, you learn how toointegrate Land Gorilla Client with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b2c79-105">與 Azure AD 整合土地大猩猩用戶端可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="b2c79-105">Integrating Land Gorilla Client with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b2c79-106">您可以控制存取 tooLand 大猩猩用戶端的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="b2c79-106">You can control in Azure AD who has access tooLand Gorilla Client</span></span>
- <span data-ttu-id="b2c79-107">您可以啟用您的使用者 tooautomatically get 登入 tooLand 大猩猩 （單一登入） 的用戶端使用其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="b2c79-107">You can enable your users tooautomatically get signed-on tooLand Gorilla Client (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b2c79-108">您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站</span><span class="sxs-lookup"><span data-stu-id="b2c79-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="b2c79-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b2c79-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b2c79-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b2c79-110">Prerequisites</span></span>

<span data-ttu-id="b2c79-111">tooconfigure 土地大猩猩用戶端與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="b2c79-111">tooconfigure Azure AD integration with Land Gorilla Client, you need hello following items:</span></span>

- <span data-ttu-id="b2c79-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b2c79-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b2c79-113">啟用 Land Gorilla Client 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b2c79-113">A Land Gorilla Client single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="b2c79-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="b2c79-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="b2c79-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="b2c79-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b2c79-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="b2c79-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b2c79-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="b2c79-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="b2c79-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="b2c79-118">Scenario description</span></span>
<span data-ttu-id="b2c79-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b2c79-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b2c79-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="b2c79-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b2c79-121">新增土地大猩猩用戶端從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="b2c79-121">Adding Land Gorilla Client from hello gallery</span></span>
2. <span data-ttu-id="b2c79-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b2c79-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-land-gorilla-client-from-hello-gallery"></a><span data-ttu-id="b2c79-123">新增土地大猩猩用戶端從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="b2c79-123">Adding Land Gorilla Client from hello gallery</span></span>
<span data-ttu-id="b2c79-124">tooconfigure hello 整合土地大猩猩用戶端到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd 土地大猩猩用戶端。</span><span class="sxs-lookup"><span data-stu-id="b2c79-124">tooconfigure hello integration of Land Gorilla Client into Azure AD, you need tooadd Land Gorilla Client from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b2c79-125">**tooadd 土地大猩猩用戶端 hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b2c79-125">**tooadd Land Gorilla Client from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b2c79-126">在 hello  **[Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="b2c79-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b2c79-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b2c79-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b2c79-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b2c79-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="b2c79-131">按一下**新增**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b2c79-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="b2c79-133">在 [hello] 搜尋方塊中，輸入**土地大猩猩用戶端**。</span><span class="sxs-lookup"><span data-stu-id="b2c79-133">In hello search box, type **Land Gorilla Client**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_search.png)

5. <span data-ttu-id="b2c79-135">在 hello 結果 窗格中，選取 **土地大猩猩用戶端**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2c79-135">In hello results panel, select **Land Gorilla Client**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b2c79-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b2c79-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b2c79-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Land Gorilla Client 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b2c79-138">In this section, you configure and test Azure AD single sign-on with Land Gorilla Client based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b2c79-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者土地大猩猩用戶端中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="b2c79-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Land Gorilla Client is tooa user in Azure AD.</span></span> <span data-ttu-id="b2c79-140">換句話說，Azure AD 使用者與 hello 土地大猩猩用戶端中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="b2c79-140">In other words, a link relationship between an Azure AD user and hello related user in Land Gorilla Client needs toobe established.</span></span>

<span data-ttu-id="b2c79-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username**土地大猩猩用戶端中。</span><span class="sxs-lookup"><span data-stu-id="b2c79-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Land Gorilla Client.</span></span>

<span data-ttu-id="b2c79-142">tooconfigure 及土地大猩猩用戶端與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="b2c79-142">tooconfigure and test Azure AD single sign-on with Land Gorilla Client, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b2c79-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="b2c79-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b2c79-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與有限的群組。</span><span class="sxs-lookup"><span data-stu-id="b2c79-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with limited group.</span></span>
3. <span data-ttu-id="b2c79-145">**[建立測試使用者土地大猩猩](#creating-a-land-gorilla-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="b2c79-145">**[Creating a Land Gorilla test user](#creating-a-land-gorilla-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="b2c79-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b2c79-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b2c79-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="b2c79-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b2c79-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b2c79-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b2c79-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並土地大猩猩用戶端應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="b2c79-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Land Gorilla Client application.</span></span>

<span data-ttu-id="b2c79-150">**tooconfigure Azure AD 單一登入使用土地大猩猩用戶端，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b2c79-150">**tooconfigure Azure AD single sign-on with Land Gorilla Client, perform hello following steps:**</span></span>

1. <span data-ttu-id="b2c79-151">在 hello Azure 管理入口網站上 hello**土地大猩猩用戶端**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="b2c79-151">In hello Azure Management portal, on hello **Land Gorilla Client** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="b2c79-153">在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b2c79-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_samlbase.png)

3. <span data-ttu-id="b2c79-155">在 hello**土地大猩猩用戶端的網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b2c79-155">On hello **Land Gorilla Client Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_url_02.png)

    <span data-ttu-id="b2c79-157">a.</span><span class="sxs-lookup"><span data-stu-id="b2c79-157">a.</span></span> <span data-ttu-id="b2c79-158">在 hello**識別碼**文字方塊中，類型 hello 值使用其中一種 hello 下列模式：</span><span class="sxs-lookup"><span data-stu-id="b2c79-158">In hello **Identifier** textbox, type hello value using one of hello following pattern:</span></span> 
    
    `https://<customer domain>.landgorilla.com/` 
    
    `https://www.<customer domain>.landgorilla.com`

    <span data-ttu-id="b2c79-159">b.</span><span class="sxs-lookup"><span data-stu-id="b2c79-159">b.</span></span> <span data-ttu-id="b2c79-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用其中一個 hello 下列模式：</span><span class="sxs-lookup"><span data-stu-id="b2c79-160">In hello **Reply URL** textbox, type a URL using one of hello following pattern:</span></span>

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`
    
    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`

    > [!NOTE] 
    > <span data-ttu-id="b2c79-161">請注意這些不是 hello 實際值。</span><span class="sxs-lookup"><span data-stu-id="b2c79-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="b2c79-162">您有 tooupdate hello 實際的識別項和回覆 url 的這些值。</span><span class="sxs-lookup"><span data-stu-id="b2c79-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="b2c79-163">這裡我們建議您 toouse hello 唯一字串的值在 hello 識別項。</span><span class="sxs-lookup"><span data-stu-id="b2c79-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="b2c79-164">請連絡[土地大猩猩用戶端小組](https://www.landgorilla.com/support/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="b2c79-164">Contact [Land Gorilla Client team](https://www.landgorilla.com/support/) tooget these values.</span></span> 

4. <span data-ttu-id="b2c79-165">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="b2c79-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_certificate.png) 

5. <span data-ttu-id="b2c79-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b2c79-167">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-landgorilla-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="b2c79-169">tooget SSO 組態在土地大猩猩結束時，請連絡您的應用程式完成[土地大猩猩用戶端支援小組](https://www.landgorilla.com/support/)並提供給他們，以下載 hello **"中繼資料 XML**檔案。</span><span class="sxs-lookup"><span data-stu-id="b2c79-169">tooget SSO configuration complete for your application at Land Gorilla end, Contact [Land Gorilla Client support team](https://www.landgorilla.com/support/) and provide them with hello downloaded **“Metadata XML** file.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b2c79-170">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b2c79-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="b2c79-171">hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="b2c79-171">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="b2c79-173">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b2c79-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b2c79-174">在 hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="b2c79-174">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b2c79-176">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="b2c79-176">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b2c79-178">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b2c79-178">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b2c79-180">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b2c79-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b2c79-182">a.</span><span class="sxs-lookup"><span data-stu-id="b2c79-182">a.</span></span> <span data-ttu-id="b2c79-183">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b2c79-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b2c79-184">b.</span><span class="sxs-lookup"><span data-stu-id="b2c79-184">b.</span></span> <span data-ttu-id="b2c79-185">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="b2c79-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b2c79-186">c.</span><span class="sxs-lookup"><span data-stu-id="b2c79-186">c.</span></span> <span data-ttu-id="b2c79-187">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="b2c79-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b2c79-188">d.</span><span class="sxs-lookup"><span data-stu-id="b2c79-188">d.</span></span> <span data-ttu-id="b2c79-189">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b2c79-189">Click **Create**.</span></span> 

### <a name="creating-a-land-gorilla-test-user"></a><span data-ttu-id="b2c79-190">建立 Land Gorilla 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b2c79-190">Creating a Land Gorilla test user</span></span>

<span data-ttu-id="b2c79-191">請使用[土地大猩猩支援小組](https://www.landgorilla.com/support/)tooadd hello hello 土地大猩猩平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="b2c79-191">Please work with [Land Gorilla support team](https://www.landgorilla.com/support/) tooadd hello users in hello Land Gorilla platform.</span></span>
    
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b2c79-192">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="b2c79-192">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b2c79-193">在本節中，以啟用許 Simon toouse Azure 單一登入授與他們存取 tooLand 大猩猩用戶端。</span><span class="sxs-lookup"><span data-stu-id="b2c79-193">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooLand Gorilla Client.</span></span>

![指派使用者][200] 

<span data-ttu-id="b2c79-195">**tooassign 許 Simon tooLand 大猩猩用戶端，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b2c79-195">**tooassign Britta Simon tooLand Gorilla Client, perform hello following steps:**</span></span>

1. <span data-ttu-id="b2c79-196">在 hello Azure 管理入口網站中，開啟 hello 應用程式 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b2c79-196">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="b2c79-198">在 [hello] 應用程式清單中，選取**土地大猩猩用戶端**。</span><span class="sxs-lookup"><span data-stu-id="b2c79-198">In hello applications list, select **Land Gorilla Client**.</span></span>

    ![設定單一登入](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_app.png) 

3. <span data-ttu-id="b2c79-200">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="b2c79-200">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="b2c79-202">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b2c79-202">Click **Add** button.</span></span> <span data-ttu-id="b2c79-203">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b2c79-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="b2c79-205">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="b2c79-205">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b2c79-206">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b2c79-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b2c79-207">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b2c79-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="b2c79-208">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="b2c79-208">Testing single sign-on</span></span>

<span data-ttu-id="b2c79-209">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="b2c79-209">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b2c79-210">當您按一下 hello 土地大猩猩用戶端的並排顯示 hello 存取面板中時，您應該取得自動登入 tooyour 土地大猩猩用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="b2c79-210">When you click hello Land Gorilla Client tile in hello Access Panel, you should get automatically signed-on tooyour Land Gorilla Client application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b2c79-211">其他資源</span><span class="sxs-lookup"><span data-stu-id="b2c79-211">Additional resources</span></span>

* [<span data-ttu-id="b2c79-212">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b2c79-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b2c79-213">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b2c79-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_203.png

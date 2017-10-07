---
title: "教學課程：Azure Active Directory 與 Concur 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Concur 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1eee0a5d-24fa-4986-9aef-3c543cfe3296
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 1012bf8c6f036306d0ca90689415d5e22e449989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-concur"></a><span data-ttu-id="de4e4-103">教學課程：Azure Active Directory 與 Concur 整合</span><span class="sxs-lookup"><span data-stu-id="de4e4-103">Tutorial: Azure Active Directory integration with Concur</span></span>

<span data-ttu-id="de4e4-104">在此教學課程中，您學會如何 toointegrate Concur 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="de4e4-104">In this tutorial, you learn how toointegrate Concur with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="de4e4-105">整合 Azure AD 與 Concur 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="de4e4-105">Integrating Concur with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="de4e4-106">您可以控制存取 tooConcur Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="de4e4-106">You can control in Azure AD who has access tooConcur</span></span>
- <span data-ttu-id="de4e4-107">您可以啟用您的使用者 tooautomatically get 登入 tooConcur （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="de4e4-107">You can enable your users tooautomatically get signed-on tooConcur (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="de4e4-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="de4e4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="de4e4-109">如果您想 tooknow 與 Azure AD SaaS 應用程式整合的詳細資訊，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="de4e4-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de4e4-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="de4e4-110">Prerequisites</span></span>

<span data-ttu-id="de4e4-111">tooconfigure Azure AD 與 Concur 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="de4e4-111">tooconfigure Azure AD integration with Concur, you need hello following items:</span></span>

- <span data-ttu-id="de4e4-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="de4e4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="de4e4-113">已啟用 Concur 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="de4e4-113">A Concur single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="de4e4-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="de4e4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="de4e4-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="de4e4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="de4e4-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="de4e4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="de4e4-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="de4e4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="de4e4-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="de4e4-118">Scenario description</span></span>
<span data-ttu-id="de4e4-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de4e4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="de4e4-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="de4e4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="de4e4-121">從 hello 圖庫加入 Concur</span><span class="sxs-lookup"><span data-stu-id="de4e4-121">Adding Concur from hello gallery</span></span>
2. <span data-ttu-id="de4e4-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="de4e4-122">Configuring and testing Azure AD single sign-on</span></span>

>[!NOTE]
><span data-ttu-id="de4e4-123">hello 透過 SAML 同盟 SSO 的 Concur 訂閱組態是個別的工作，您必須連絡[Concur 的用戶端支援小組](https://www.concur.co.in/contact)tooperform。</span><span class="sxs-lookup"><span data-stu-id="de4e4-123">hello configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) tooperform.</span></span> 

## <a name="adding-concur-from-hello-gallery"></a><span data-ttu-id="de4e4-124">從 hello 圖庫加入 Concur</span><span class="sxs-lookup"><span data-stu-id="de4e4-124">Adding Concur from hello gallery</span></span>
<span data-ttu-id="de4e4-125">tooconfigure hello 整合 Concur 到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Concur。</span><span class="sxs-lookup"><span data-stu-id="de4e4-125">tooconfigure hello integration of Concur into Azure AD, you need tooadd Concur from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="de4e4-126">**tooadd Concur hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="de4e4-126">**tooadd Concur from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="de4e4-127">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="de4e4-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="de4e4-129">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="de4e4-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="de4e4-130">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="de4e4-130">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="de4e4-132">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="de4e4-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="de4e4-134">在 [hello] 搜尋方塊中，輸入**Concur**。</span><span class="sxs-lookup"><span data-stu-id="de4e4-134">In hello search box, type **Concur**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-concur-tutorial/tutorial_concur_search.png)

5. <span data-ttu-id="de4e4-136">在 hello 結果 窗格中，選取  **Concur**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="de4e4-136">In hello results panel, select **Concur**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-concur-tutorial/tutorial_concur_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="de4e4-138">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="de4e4-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="de4e4-139">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Concur 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de4e4-139">In this section, you configure and test Azure AD single sign-on with Concur based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="de4e4-140">單一登入 toowork，Azure AD 需要 tooknow Concur 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="de4e4-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Concur is tooa user in Azure AD.</span></span> <span data-ttu-id="de4e4-141">換句話說，Azure AD 使用者與 Concur 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="de4e4-141">In other words, a link relationship between an Azure AD user and hello related user in Concur needs toobe established.</span></span>

<span data-ttu-id="de4e4-142">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Concur 中。</span><span class="sxs-lookup"><span data-stu-id="de4e4-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Concur.</span></span>

<span data-ttu-id="de4e4-143">tooconfigure 及 Azure AD 單一登入與 Concur 的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="de4e4-143">tooconfigure and test Azure AD single sign-on with Concur, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="de4e4-144">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="de4e4-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="de4e4-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="de4e4-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="de4e4-146">**[建立 Concur 的測試使用者](#creating-a-concur-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Concur 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="de4e4-146">**[Creating a Concur test user](#creating-a-concur-test-user)** - toohave a counterpart of Britta Simon in Concur that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="de4e4-147">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de4e4-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="de4e4-148">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="de4e4-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="de4e4-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="de4e4-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="de4e4-150">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Concur 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="de4e4-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Concur application.</span></span>

<span data-ttu-id="de4e4-151">**tooconfigure Azure AD 單一登入與 Concur，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="de4e4-151">**tooconfigure Azure AD single sign-on with Concur, perform hello following steps:**</span></span>

1. <span data-ttu-id="de4e4-152">在 Azure 入口網站上 hello hello **Concur**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="de4e4-152">In hello Azure portal, on hello **Concur** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="de4e4-154">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de4e4-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-concur-tutorial/tutorial_concur_samlbase.png)

3. <span data-ttu-id="de4e4-156">在 hello **Concur 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="de4e4-156">On hello **Concur Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-concur-tutorial/tutorial_concur_url.png)

    <span data-ttu-id="de4e4-158">a.</span><span class="sxs-lookup"><span data-stu-id="de4e4-158">a.</span></span> <span data-ttu-id="de4e4-159">在 hello**登入 URL**文字方塊中，使用下列模式的 hello 類型 hello 值：`https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span><span class="sxs-lookup"><span data-stu-id="de4e4-159">In hello **Sign on URL** textbox, type hello value using hello following pattern: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span></span>

    <span data-ttu-id="de4e4-160">b.</span><span class="sxs-lookup"><span data-stu-id="de4e4-160">b.</span></span> <span data-ttu-id="de4e4-161">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<customer-domain>.concursolutions.com`</span><span class="sxs-lookup"><span data-stu-id="de4e4-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<customer-domain>.concursolutions.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="de4e4-162">這些值不是真正的 hello。</span><span class="sxs-lookup"><span data-stu-id="de4e4-162">These values are not hello real.</span></span> <span data-ttu-id="de4e4-163">更新這些值與實際的 hello 登入 URL 和識別碼。</span><span class="sxs-lookup"><span data-stu-id="de4e4-163">Update these values with hello actual Sign on URL and Identifier.</span></span> <span data-ttu-id="de4e4-164">請連絡[Concur 的用戶端支援小組](https://www.concur.co.in/contact)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="de4e4-164">Contact [Concur Client support team](https://www.concur.co.in/contact) tooget these values.</span></span> 

4. <span data-ttu-id="de4e4-165">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="de4e4-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-concur-tutorial/tutorial_concur_certificate.png) 

5. <span data-ttu-id="de4e4-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="de4e4-167">Click **Save** button.</span></span>

    <span data-ttu-id="de4e4-168">![設定單一登入](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="de4e4-168">![Configure Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span></span>

6. <span data-ttu-id="de4e4-169">tooconfigure 單一登入上**Concur**端，您需要下載 toosend hello**中繼資料 XML** tooConcur 支援。</span><span class="sxs-lookup"><span data-stu-id="de4e4-169">tooconfigure single sign-on on **Concur** side, you need toosend hello downloaded **Metadata XML** tooConcur support.</span></span> <span data-ttu-id="de4e4-170">設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。</span><span class="sxs-lookup"><span data-stu-id="de4e4-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

  >[!NOTE]
  ><span data-ttu-id="de4e4-171">hello 透過 SAML 同盟 SSO 的 Concur 訂閱組態是個別的工作，您必須連絡[Concur 的用戶端支援小組](https://www.concur.co.in/contact)tooperform。</span><span class="sxs-lookup"><span data-stu-id="de4e4-171">hello configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) tooperform.</span></span> 
  
<CE>

> [!TIP]
> <span data-ttu-id="de4e4-172">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="de4e4-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="de4e4-173">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="de4e4-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="de4e4-174">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="de4e4-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="de4e4-175">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="de4e4-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="de4e4-176">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="de4e4-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="de4e4-178">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="de4e4-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="de4e4-179">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="de4e4-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-concur-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="de4e4-181">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="de4e4-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-concur-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="de4e4-183">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="de4e4-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-concur-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="de4e4-185">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="de4e4-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-concur-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="de4e4-187">a.</span><span class="sxs-lookup"><span data-stu-id="de4e4-187">a.</span></span> <span data-ttu-id="de4e4-188">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="de4e4-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="de4e4-189">b.</span><span class="sxs-lookup"><span data-stu-id="de4e4-189">b.</span></span> <span data-ttu-id="de4e4-190">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="de4e4-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="de4e4-191">c.</span><span class="sxs-lookup"><span data-stu-id="de4e4-191">c.</span></span> <span data-ttu-id="de4e4-192">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="de4e4-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="de4e4-193">d.</span><span class="sxs-lookup"><span data-stu-id="de4e4-193">d.</span></span> <span data-ttu-id="de4e4-194">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="de4e4-194">Click **Create**.</span></span>
 
### <a name="creating-a-concur-test-user"></a><span data-ttu-id="de4e4-195">建立 Concur 測試使用者</span><span class="sxs-lookup"><span data-stu-id="de4e4-195">Creating a Concur test user</span></span>

<span data-ttu-id="de4e4-196">應用程式支援 hello 恰好在即時使用者佈建，以及之後驗證使用者會自動建立 hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="de4e4-196">Application supports hello Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="de4e4-197">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="de4e4-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="de4e4-198">在本節中，您可以授與存取 tooConcur 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de4e4-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConcur.</span></span>

![指派使用者][200] 

<span data-ttu-id="de4e4-200">**tooassign 許 Simon tooConcur，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="de4e4-200">**tooassign Britta Simon tooConcur, perform hello following steps:**</span></span>

1. <span data-ttu-id="de4e4-201">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="de4e4-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="de4e4-203">在 [hello] 應用程式清單中，選取**Concur**。</span><span class="sxs-lookup"><span data-stu-id="de4e4-203">In hello applications list, select **Concur**.</span></span>

    ![設定單一登入](./media/active-directory-saas-concur-tutorial/tutorial_concur_app.png) 

3. <span data-ttu-id="de4e4-205">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="de4e4-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="de4e4-207">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="de4e4-207">Click **Add** button.</span></span> <span data-ttu-id="de4e4-208">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="de4e4-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="de4e4-210">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="de4e4-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="de4e4-211">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="de4e4-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="de4e4-212">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="de4e4-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="de4e4-213">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="de4e4-213">Testing single sign-on</span></span>

<span data-ttu-id="de4e4-214">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="de4e4-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="de4e4-215">當您按一下 hello Concur 磚 hello 存取面板中的時，您應該取得 Concur 的應用程式的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="de4e4-215">When you click hello Concur tile in hello Access Panel, you should get login page of Concur application.</span></span>
<span data-ttu-id="de4e4-216">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="de4e4-216">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="de4e4-217">其他資源</span><span class="sxs-lookup"><span data-stu-id="de4e4-217">Additional resources</span></span>

* [<span data-ttu-id="de4e4-218">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="de4e4-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="de4e4-219">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="de4e4-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="de4e4-220">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="de4e4-220">Configure User Provisioning</span></span>](active-directory-saas-concur-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-concur-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-concur-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-concur-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-concur-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-concur-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-concur-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-concur-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-concur-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-concur-tutorial/tutorial_general_203.png


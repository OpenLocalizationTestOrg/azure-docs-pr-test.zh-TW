---
title: "教學課程：Azure Active Directory 與 CA PPM 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 CA PPM 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca9d5e71-e429-4891-8d10-3498e7210e89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 571130f3be0529c986aa0d8a08e4172015cd0b40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ca-ppm"></a><span data-ttu-id="fdded-103">教學課程：Azure Active Directory 與 CA PPM 整合</span><span class="sxs-lookup"><span data-stu-id="fdded-103">Tutorial: Azure Active Directory integration with CA PPM</span></span>

<span data-ttu-id="fdded-104">在此教學課程中，您學會如何 toointegrate CA PPM 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="fdded-104">In this tutorial, you learn how toointegrate CA PPM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fdded-105">與 Azure AD 整合 CA PPM 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="fdded-105">Integrating CA PPM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fdded-106">您可以控制存取 tooCA PPM Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="fdded-106">You can control in Azure AD who has access tooCA PPM</span></span>
- <span data-ttu-id="fdded-107">您可以啟用您的使用者 tooautomatically get 登入 tooCA PPM （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="fdded-107">You can enable your users tooautomatically get signed-on tooCA PPM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fdded-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="fdded-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fdded-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="fdded-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fdded-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="fdded-110">Prerequisites</span></span>

<span data-ttu-id="fdded-111">tooconfigure CA PPM 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="fdded-111">tooconfigure Azure AD integration with CA PPM, you need hello following items:</span></span>

- <span data-ttu-id="fdded-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fdded-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fdded-113">已啟用 CA PPM 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fdded-113">A CA PPM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fdded-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="fdded-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fdded-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="fdded-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fdded-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="fdded-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fdded-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="fdded-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fdded-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="fdded-118">Scenario description</span></span>
<span data-ttu-id="fdded-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fdded-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fdded-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="fdded-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fdded-121">新增 CA PPM 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="fdded-121">Adding CA PPM from hello gallery</span></span>
2. <span data-ttu-id="fdded-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fdded-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ca-ppm-from-hello-gallery"></a><span data-ttu-id="fdded-123">新增 CA PPM 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="fdded-123">Adding CA PPM from hello gallery</span></span>
<span data-ttu-id="fdded-124">tooconfigure hello 整合 CA PPM 到 Azure AD，您需要 tooadd CA PPM hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fdded-124">tooconfigure hello integration of CA PPM into Azure AD, you need tooadd CA PPM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fdded-125">**tooadd CA PPM hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="fdded-125">**tooadd CA PPM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fdded-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="fdded-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fdded-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="fdded-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fdded-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="fdded-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="fdded-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="fdded-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="fdded-133">在 [hello] 搜尋方塊中，輸入**CA PPM**。</span><span class="sxs-lookup"><span data-stu-id="fdded-133">In hello search box, type **CA PPM**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_search.png)

5. <span data-ttu-id="fdded-135">在 hello 結果 窗格中，選取  **CA PPM**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fdded-135">In hello results panel, select **CA PPM**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fdded-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fdded-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fdded-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 CA PPM 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fdded-138">In this section, you configure and test Azure AD single sign-on with CA PPM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fdded-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 CA PPM 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="fdded-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CA PPM is tooa user in Azure AD.</span></span> <span data-ttu-id="fdded-140">換句話說，Azure AD 使用者與 hello CA PPM 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="fdded-140">In other words, a link relationship between an Azure AD user and hello related user in CA PPM needs toobe established.</span></span>

<span data-ttu-id="fdded-141">在 CA PPM hello hello 值指派**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="fdded-141">In CA PPM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fdded-142">tooconfigure 及 CA PPM 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="fdded-142">tooconfigure and test Azure AD single sign-on with CA PPM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fdded-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="fdded-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fdded-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="fdded-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fdded-145">**[建立 CA PPM 測試使用者](#creating-a-ca-ppm-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 CA PPM 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="fdded-145">**[Creating a CA PPM test user](#creating-a-ca-ppm-test-user)** - toohave a counterpart of Britta Simon in CA PPM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fdded-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fdded-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fdded-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="fdded-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fdded-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fdded-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fdded-149">在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 CA PPM 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="fdded-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CA PPM application.</span></span>

<span data-ttu-id="fdded-150">**tooconfigure Azure AD 單一登入與 CA PPM，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="fdded-150">**tooconfigure Azure AD single sign-on with CA PPM, perform hello following steps:**</span></span>

1. <span data-ttu-id="fdded-151">在 Azure 入口網站上 hello hello **CA PPM**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="fdded-151">In hello Azure portal, on hello **CA PPM** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="fdded-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fdded-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_samlbase.png)

3. <span data-ttu-id="fdded-155">在 hello **CA PPM 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="fdded-155">On hello **CA PPM Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_url.png)

    <span data-ttu-id="fdded-157">a.</span><span class="sxs-lookup"><span data-stu-id="fdded-157">a.</span></span> <span data-ttu-id="fdded-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://ca.ondemand.saml.20.post.<companyname>`</span><span class="sxs-lookup"><span data-stu-id="fdded-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://ca.ondemand.saml.20.post.<companyname>`</span></span>
    
    <span data-ttu-id="fdded-159">b.</span><span class="sxs-lookup"><span data-stu-id="fdded-159">b.</span></span> <span data-ttu-id="fdded-160">在 hello**回覆 URL**文字方塊中，做為輸入：`https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="fdded-160">In hello **Reply URL** textbox, type as: `https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fdded-161">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="fdded-161">This value is not real.</span></span> <span data-ttu-id="fdded-162">更新此值以 hello 實際的識別項。</span><span class="sxs-lookup"><span data-stu-id="fdded-162">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="fdded-163">請連絡[CA PPM 支援小組](mailto:catechnicalsupport@ca.com)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="fdded-163">Contact [CA PPM support team](mailto:catechnicalsupport@ca.com) tooget this value.</span></span>
 
4. <span data-ttu-id="fdded-164">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="fdded-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_certificate.png) 

5. <span data-ttu-id="fdded-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="fdded-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-cappm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fdded-168">在 hello **CA PPM 設定**區段中，按一下**設定 CA PPM** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="fdded-168">On hello **CA PPM Configuration** section, click **Configure CA PPM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fdded-169">複製 hello **SAML 實體識別碼**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="fdded-169">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_configure.png) 

7. <span data-ttu-id="fdded-171">tooconfigure 單一登入上**CA PPM**端，您需要下載 toosend hello **Certificate(Base64)**和**SAML 實體識別碼**太[CA PPM 支援小組](mailto:catechnicalsupport@ca.com).</span><span class="sxs-lookup"><span data-stu-id="fdded-171">tooconfigure single sign-on on **CA PPM** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Entity ID** too[CA PPM support team](mailto:catechnicalsupport@ca.com).</span></span>

> [!TIP]
> <span data-ttu-id="fdded-172">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="fdded-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fdded-173">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="fdded-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fdded-174">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fdded-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fdded-175">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="fdded-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="fdded-176">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="fdded-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="fdded-178">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="fdded-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fdded-179">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="fdded-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cappm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fdded-181">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="fdded-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cappm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fdded-183">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="fdded-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cappm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fdded-185">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="fdded-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cappm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fdded-187">a.</span><span class="sxs-lookup"><span data-stu-id="fdded-187">a.</span></span> <span data-ttu-id="fdded-188">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="fdded-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fdded-189">b.</span><span class="sxs-lookup"><span data-stu-id="fdded-189">b.</span></span> <span data-ttu-id="fdded-190">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="fdded-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fdded-191">c.</span><span class="sxs-lookup"><span data-stu-id="fdded-191">c.</span></span> <span data-ttu-id="fdded-192">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="fdded-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fdded-193">d.</span><span class="sxs-lookup"><span data-stu-id="fdded-193">d.</span></span> <span data-ttu-id="fdded-194">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="fdded-194">Click **Create**.</span></span>
 
### <a name="creating-a-ca-ppm-test-user"></a><span data-ttu-id="fdded-195">建立 CA PPM 測試使用者</span><span class="sxs-lookup"><span data-stu-id="fdded-195">Creating a CA PPM test user</span></span>

<span data-ttu-id="fdded-196">在本節中，您會在 CA PPM 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="fdded-196">In this section, you create a user called Britta Simon in CA PPM.</span></span> <span data-ttu-id="fdded-197">使用[CA PPM 支援小組](mailto:catechnicalsupport@ca.com)tooadd hello hello CA PPM 平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="fdded-197">Work with [CA PPM support team](mailto:catechnicalsupport@ca.com) tooadd hello users in hello CA PPM platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fdded-198">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="fdded-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fdded-199">在本節中，您可以授與存取 tooCA PPM 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fdded-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCA PPM.</span></span>

![指派使用者][200] 

<span data-ttu-id="fdded-201">**tooassign 許 Simon tooCA PPM，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="fdded-201">**tooassign Britta Simon tooCA PPM, perform hello following steps:**</span></span>

1. <span data-ttu-id="fdded-202">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="fdded-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="fdded-204">在 [hello] 應用程式清單中，選取**CA PPM**。</span><span class="sxs-lookup"><span data-stu-id="fdded-204">In hello applications list, select **CA PPM**.</span></span>

    ![設定單一登入](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_app.png) 

3. <span data-ttu-id="fdded-206">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="fdded-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="fdded-208">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fdded-208">Click **Add** button.</span></span> <span data-ttu-id="fdded-209">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="fdded-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="fdded-211">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="fdded-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fdded-212">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fdded-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fdded-213">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fdded-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fdded-214">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="fdded-214">Testing single sign-on</span></span>

<span data-ttu-id="fdded-215">本節中，您可以測試使用存取面板 hello Azure AD 的 SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="fdded-215">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="fdded-216">當您按一下 hello CA PPM 磚 hello 存取面板中的時，您應該取得自動登入 tooyour CA PPM 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fdded-216">When you click hello CA PPM tile in hello Access Panel, you should get automatically signed-on tooyour CA PPM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fdded-217">其他資源</span><span class="sxs-lookup"><span data-stu-id="fdded-217">Additional resources</span></span>

* [<span data-ttu-id="fdded-218">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fdded-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fdded-219">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="fdded-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_203.png


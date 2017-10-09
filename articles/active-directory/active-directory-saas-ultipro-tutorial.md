---
title: "教學課程：Azure Active Directory 與 UltiPro 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 UltiPro 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: afc0f2b9-2eac-47ec-af04-65ed0fb0ca5a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 8cb613228893e8cbf997957452d55d0ab7939171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ultipro"></a><span data-ttu-id="8d424-103">教學課程：Azure Active Directory 與 UltiPro 整合</span><span class="sxs-lookup"><span data-stu-id="8d424-103">Tutorial: Azure Active Directory integration with UltiPro</span></span>

<span data-ttu-id="8d424-104">在此教學課程中，您學會如何 toointegrate UltiPro 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="8d424-104">In this tutorial, you learn how toointegrate UltiPro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d424-105">與 Azure AD 整合 UltiPro 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="8d424-105">Integrating UltiPro with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8d424-106">您可以控制存取 tooUltiPro Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="8d424-106">You can control in Azure AD who has access tooUltiPro</span></span>
- <span data-ttu-id="8d424-107">您可以啟用您的使用者 tooautomatically get 登入 tooUltiPro （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="8d424-107">You can enable your users tooautomatically get signed-on tooUltiPro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8d424-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8d424-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8d424-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="8d424-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d424-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="8d424-110">Prerequisites</span></span>

<span data-ttu-id="8d424-111">tooconfigure UltiPro 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="8d424-111">tooconfigure Azure AD integration with UltiPro, you need hello following items:</span></span>

- <span data-ttu-id="8d424-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8d424-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d424-113">已啟用 UltiPro 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8d424-113">A UltiPro single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d424-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="8d424-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8d424-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="8d424-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8d424-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="8d424-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d424-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="8d424-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d424-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="8d424-118">Scenario description</span></span>
<span data-ttu-id="8d424-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8d424-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8d424-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="8d424-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d424-121">從 hello 圖庫加入 UltiPro</span><span class="sxs-lookup"><span data-stu-id="8d424-121">Adding UltiPro from hello gallery</span></span>
2. <span data-ttu-id="8d424-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8d424-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ultipro-from-hello-gallery"></a><span data-ttu-id="8d424-123">從 hello 圖庫加入 UltiPro</span><span class="sxs-lookup"><span data-stu-id="8d424-123">Adding UltiPro from hello gallery</span></span>
<span data-ttu-id="8d424-124">tooconfigure hello 整合 UltiPro 到 Azure AD，您需要 tooadd UltiPro hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d424-124">tooconfigure hello integration of UltiPro into Azure AD, you need tooadd UltiPro from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8d424-125">**tooadd UltiPro 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8d424-125">**tooadd UltiPro from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d424-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="8d424-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8d424-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8d424-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8d424-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8d424-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="8d424-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="8d424-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="8d424-133">在 [hello] 搜尋方塊中，輸入**UltiPro**。</span><span class="sxs-lookup"><span data-stu-id="8d424-133">In hello search box, type **UltiPro**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_search.png)

5. <span data-ttu-id="8d424-135">在 hello 結果 窗格中，選取  **UltiPro**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d424-135">In hello results panel, select **UltiPro**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8d424-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8d424-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8d424-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 UltiPro 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8d424-138">In this section, you configure and test Azure AD single sign-on with UltiPro based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8d424-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 UltiPro 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="8d424-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UltiPro is tooa user in Azure AD.</span></span> <span data-ttu-id="8d424-140">換句話說，Azure AD 使用者與 hello UltiPro 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="8d424-140">In other words, a link relationship between an Azure AD user and hello related user in UltiPro needs toobe established.</span></span>

<span data-ttu-id="8d424-141">UltiPro 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="8d424-141">In UltiPro, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8d424-142">tooconfigure 及 UltiPro 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="8d424-142">tooconfigure and test Azure AD single sign-on with UltiPro, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8d424-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="8d424-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8d424-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="8d424-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8d424-145">**[建立測試使用者 UltiPro](#creating-a-ultipro-test-user)**  -toohave 許 Simon UltiPro 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="8d424-145">**[Creating a UltiPro test user](#creating-a-ultipro-test-user)** - toohave a counterpart of Britta Simon in UltiPro that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8d424-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8d424-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8d424-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="8d424-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8d424-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8d424-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8d424-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 UltiPro 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="8d424-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UltiPro application.</span></span>

<span data-ttu-id="8d424-150">**tooconfigure Azure AD 單一登入與 UltiPro，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8d424-150">**tooconfigure Azure AD single sign-on with UltiPro, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d424-151">在 Azure 入口網站上 hello hello **UltiPro**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="8d424-151">In hello Azure portal, on hello **UltiPro** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="8d424-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8d424-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_samlbase.png)

3. <span data-ttu-id="8d424-155">在 hello **UltiPro 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8d424-155">On hello **UltiPro Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_url.png)

    <span data-ttu-id="8d424-157">a.</span><span class="sxs-lookup"><span data-stu-id="8d424-157">a.</span></span> <span data-ttu-id="8d424-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="8d424-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/`|
    | `https://<companyname>.ultiproworkplace.com?cpi=AZUREADISSSUERURL`|
    | ` https://<companyname>.ultipro.ca`|
    
    <span data-ttu-id="8d424-159">b.</span><span class="sxs-lookup"><span data-stu-id="8d424-159">b.</span></span> <span data-ttu-id="8d424-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="8d424-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/adfs/services/trust`|
    | `https://<companyname>.ultiproworkplace.com/adfs/services/trust`|
    | `https://<companyname>.ultipro.ca/adfs/services/trust`|
    
    <span data-ttu-id="8d424-161">c.</span><span class="sxs-lookup"><span data-stu-id="8d424-161">c.</span></span> <span data-ttu-id="8d424-162">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="8d424-162">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/<instancename>`|
    | `https://<companyname>.ultiproworkplace.com/<instancename>`|
    | `https://<companyname>.ultipro.ca/<instancename>`|
    
    > [!NOTE] 
    > <span data-ttu-id="8d424-163">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="8d424-163">These values are not real.</span></span> <span data-ttu-id="8d424-164">更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="8d424-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="8d424-165">請連絡[UltiPro 用戶端支援小組](https://www.ultimatesoftware.com/ContactUs)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="8d424-165">Contact [UltiPro Client support team](https://www.ultimatesoftware.com/ContactUs) tooget these values.</span></span> 

5. <span data-ttu-id="8d424-166">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="8d424-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_certificate.png) 

6. <span data-ttu-id="8d424-168">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8d424-168">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-ultipro-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="8d424-170">在 hello **UltiPro 組態**區段中，按一下**設定 UltiPro** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="8d424-170">On hello **UltiPro Configuration** section, click **Configure UltiPro** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8d424-171">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="8d424-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_configure.png) 

8. <span data-ttu-id="8d424-173">tooconfigure 單一登入上**UltiPro**端，您需要下載 toosend hello **Certificate(Base64)、 登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**太[UltiPro支援小組](https://www.ultimatesoftware.com/ContactUs)。</span><span class="sxs-lookup"><span data-stu-id="8d424-173">tooconfigure single sign-on on **UltiPro** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[UltiPro support team](https://www.ultimatesoftware.com/ContactUs).</span></span>

> [!TIP]
> <span data-ttu-id="8d424-174">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="8d424-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8d424-175">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="8d424-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8d424-176">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8d424-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8d424-177">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8d424-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="8d424-178">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="8d424-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="8d424-180">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8d424-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d424-181">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="8d424-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ultipro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8d424-183">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="8d424-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ultipro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8d424-185">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="8d424-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ultipro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8d424-187">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8d424-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ultipro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8d424-189">a.</span><span class="sxs-lookup"><span data-stu-id="8d424-189">a.</span></span> <span data-ttu-id="8d424-190">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="8d424-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8d424-191">b.</span><span class="sxs-lookup"><span data-stu-id="8d424-191">b.</span></span> <span data-ttu-id="8d424-192">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="8d424-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8d424-193">c.</span><span class="sxs-lookup"><span data-stu-id="8d424-193">c.</span></span> <span data-ttu-id="8d424-194">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="8d424-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8d424-195">d.</span><span class="sxs-lookup"><span data-stu-id="8d424-195">d.</span></span> <span data-ttu-id="8d424-196">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="8d424-196">Click **Create**.</span></span>
 
### <a name="creating-a-ultipro-test-user"></a><span data-ttu-id="8d424-197">建立 UltiPro 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8d424-197">Creating a UltiPro test user</span></span>

<span data-ttu-id="8d424-198">在本節中，您要在 UltiPro 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="8d424-198">In this section, you create a user called Britta Simon in UltiPro.</span></span> <span data-ttu-id="8d424-199">使用[UltiPro 支援小組](https://www.ultimatesoftware.com/ContactUs)hello UltiPro 平台中新增 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="8d424-199">Work with [UltiPro support team](https://www.ultimatesoftware.com/ContactUs) to add hello users in hello UltiPro platform.</span></span> <span data-ttu-id="8d424-200">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="8d424-200">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8d424-201">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="8d424-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8d424-202">在本節中，您可以授與存取 tooUltiPro 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8d424-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUltiPro.</span></span>

![指派使用者][200] 

<span data-ttu-id="8d424-204">**tooassign 許 Simon tooUltiPro，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8d424-204">**tooassign Britta Simon tooUltiPro, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d424-205">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8d424-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="8d424-207">在 [hello] 應用程式清單中，選取**UltiPro**。</span><span class="sxs-lookup"><span data-stu-id="8d424-207">In hello applications list, select **UltiPro**.</span></span>

    ![設定單一登入](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_app.png) 

3. <span data-ttu-id="8d424-209">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="8d424-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="8d424-211">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8d424-211">Click **Add** button.</span></span> <span data-ttu-id="8d424-212">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="8d424-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="8d424-214">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="8d424-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8d424-215">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8d424-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8d424-216">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8d424-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8d424-217">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="8d424-217">Testing single sign-on</span></span>

<span data-ttu-id="8d424-218">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="8d424-218">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="8d424-219">當您按一下 hello UltiPro 磚 hello 存取面板中的時，您應該取得自動登入 tooyour UltiPro 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d424-219">When you click hello UltiPro tile in hello Access Panel, you should get automatically signed-on tooyour UltiPro application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8d424-220">其他資源</span><span class="sxs-lookup"><span data-stu-id="8d424-220">Additional resources</span></span>

* [<span data-ttu-id="8d424-221">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d424-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8d424-222">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="8d424-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_203.png


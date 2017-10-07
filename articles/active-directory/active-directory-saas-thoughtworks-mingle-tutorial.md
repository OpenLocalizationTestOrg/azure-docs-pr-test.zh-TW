---
title: "教學課程：Azure Active Directory 與 Thoughtworks Mingle 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Thoughtworks Mingle 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c17f8e13d2db3de7d228d9b27128d134f98d6cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a><span data-ttu-id="1bb52-103">教學課程：Azure Active Directory 與 Thoughtworks Mingle 整合</span><span class="sxs-lookup"><span data-stu-id="1bb52-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span></span>

<span data-ttu-id="1bb52-104">在此教學課程中，您學會如何 toointegrate Thoughtworks Mingle 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="1bb52-104">In this tutorial, you learn how toointegrate Thoughtworks Mingle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1bb52-105">與 Azure AD 整合 [Thoughtworks Mingle 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="1bb52-105">Integrating Thoughtworks Mingle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1bb52-106">您可以控制存取 tooThoughtworks Mingle Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="1bb52-106">You can control in Azure AD who has access tooThoughtworks Mingle</span></span>
- <span data-ttu-id="1bb52-107">您可以啟用您的使用者 tooautomatically get 登入 tooThoughtworks Mingle （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="1bb52-107">You can enable your users tooautomatically get signed-on tooThoughtworks Mingle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1bb52-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="1bb52-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1bb52-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="1bb52-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bb52-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1bb52-110">Prerequisites</span></span>

<span data-ttu-id="1bb52-111">tooconfigure Azure AD 與 Thoughtworks Mingle 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="1bb52-111">tooconfigure Azure AD integration with Thoughtworks Mingle, you need hello following items:</span></span>

- <span data-ttu-id="1bb52-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1bb52-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1bb52-113">已啟用 Thoughtworks Mingle 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1bb52-113">A Thoughtworks Mingle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1bb52-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="1bb52-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1bb52-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="1bb52-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1bb52-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1bb52-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1bb52-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="1bb52-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1bb52-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="1bb52-118">Scenario description</span></span>
<span data-ttu-id="1bb52-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1bb52-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1bb52-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="1bb52-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1bb52-121">從 hello 組件庫中加入 [Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="1bb52-121">Adding Thoughtworks Mingle from hello gallery</span></span>
2. <span data-ttu-id="1bb52-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1bb52-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thoughtworks-mingle-from-hello-gallery"></a><span data-ttu-id="1bb52-123">從 hello 組件庫中加入 [Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="1bb52-123">Adding Thoughtworks Mingle from hello gallery</span></span>
<span data-ttu-id="1bb52-124">tooconfigure hello 整合 Thoughtworks Mingle 到 Azure AD，您需要 tooadd Thoughtworks Mingle hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1bb52-124">tooconfigure hello integration of Thoughtworks Mingle into Azure AD, you need tooadd Thoughtworks Mingle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1bb52-125">**tooadd Thoughtworks Mingle 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1bb52-125">**tooadd Thoughtworks Mingle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1bb52-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="1bb52-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory] 按鈕][1]

2. <span data-ttu-id="1bb52-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1bb52-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1bb52-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1bb52-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式] 刀鋒視窗][2]
    
3. <span data-ttu-id="1bb52-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="1bb52-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="1bb52-133">在 [hello] 搜尋方塊中，輸入**Thoughtworks Mingle**，選取**Thoughtworks Mingle**然後按一下 [從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1bb52-133">In hello search box, type **Thoughtworks Mingle**, select **Thoughtworks Mingle** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Thoughtworks Mingle hello [結果] 清單中](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1bb52-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1bb52-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="1bb52-136">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Thoughtworks Mingle 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1bb52-136">In this section, you configure and test Azure AD single sign-on with Thoughtworks Mingle based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1bb52-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Thoughtworks Mingle 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="1bb52-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Thoughtworks Mingle is tooa user in Azure AD.</span></span> <span data-ttu-id="1bb52-138">換句話說，Azure AD 使用者與 hello Thoughtworks Mingle 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="1bb52-138">In other words, a link relationship between an Azure AD user and hello related user in Thoughtworks Mingle needs toobe established.</span></span>

<span data-ttu-id="1bb52-139">在 Thoughtworks Mingle 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1bb52-139">In Thoughtworks Mingle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1bb52-140">tooconfigure 及測試 Azure AD 單一登入 Thoughtworks Mingle，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="1bb52-140">tooconfigure and test Azure AD single sign-on with Thoughtworks Mingle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1bb52-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="1bb52-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1bb52-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="1bb52-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1bb52-143">**[建立測試使用者 Thoughtworks Mingle](#create-a-thoughtworks-mingle-test-user) ** -toohave 許 Simon Thoughtworks Mingle 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="1bb52-143">**[Create a Thoughtworks Mingle test user](#create-a-thoughtworks-mingle-test-user)** - toohave a counterpart of Britta Simon in Thoughtworks Mingle that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1bb52-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1bb52-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1bb52-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="1bb52-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1bb52-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1bb52-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1bb52-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Thoughtworks Mingle 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="1bb52-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Thoughtworks Mingle application.</span></span>

<span data-ttu-id="1bb52-148">**tooconfigure Azure AD 單一登入 Thoughtworks Mingle 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1bb52-148">**tooconfigure Azure AD single sign-on with Thoughtworks Mingle, perform hello following steps:**</span></span>

1. <span data-ttu-id="1bb52-149">在 Azure 入口網站上 hello hello **Thoughtworks Mingle**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="1bb52-149">In hello Azure portal, on hello **Thoughtworks Mingle** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="1bb52-151">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1bb52-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. <span data-ttu-id="1bb52-153">在 [hello **Thoughtworks Mingle 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1bb52-153">On hello **Thoughtworks Mingle Domain and URLs** section, perform hello following steps:</span></span>

    ![Thoughtworks Mingle 網域和 URL 單一登入資訊](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    <span data-ttu-id="1bb52-155">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.mingle.thoughtworks.com`</span><span class="sxs-lookup"><span data-stu-id="1bb52-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.mingle.thoughtworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1bb52-156">hello 值不是真正的。</span><span class="sxs-lookup"><span data-stu-id="1bb52-156">hello value is not real.</span></span> <span data-ttu-id="1bb52-157">更新 hello 值與 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="1bb52-157">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="1bb52-158">請連絡[Thoughtworks Mingle 的用戶端支援小組](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support)tooget hello 值。</span><span class="sxs-lookup"><span data-stu-id="1bb52-158">Contact [Thoughtworks Mingle Client support team](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) tooget hello value.</span></span> 
 
4. <span data-ttu-id="1bb52-159">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="1bb52-159">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. <span data-ttu-id="1bb52-161">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="1bb52-161">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1bb52-163">登入 tooyour **Thoughtworks Mingle**以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="1bb52-163">Log in tooyour **Thoughtworks Mingle** company site as administrator.</span></span>

7. <span data-ttu-id="1bb52-164">按一下 hello **Admin**索引標籤，然後按 [下**SSO 組態**。</span><span class="sxs-lookup"><span data-stu-id="1bb52-164">Click hello **Admin** tab, and then, click **SSO Config**.</span></span>
   
    <span data-ttu-id="1bb52-165">![[管理] 索引標籤](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO 組態")</span><span class="sxs-lookup"><span data-stu-id="1bb52-165">![Admin tab](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO Config")</span></span>

8. <span data-ttu-id="1bb52-166">在 [hello **SSO 組態**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1bb52-166">In hello **SSO Config** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="1bb52-167">![SSO 組態](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO 組態")</span><span class="sxs-lookup"><span data-stu-id="1bb52-167">![SSO Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO Config")</span></span>
    
    <span data-ttu-id="1bb52-168">a.</span><span class="sxs-lookup"><span data-stu-id="1bb52-168">a.</span></span> <span data-ttu-id="1bb52-169">tooupload hello 中繼資料檔案，按一下 [**選擇檔案**。</span><span class="sxs-lookup"><span data-stu-id="1bb52-169">tooupload hello metadata file, click **Choose file**.</span></span> 

    <span data-ttu-id="1bb52-170">b.</span><span class="sxs-lookup"><span data-stu-id="1bb52-170">b.</span></span> <span data-ttu-id="1bb52-171">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="1bb52-171">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="1bb52-172">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="1bb52-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1bb52-173">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="1bb52-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1bb52-174">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1bb52-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1bb52-175">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1bb52-175">Create an Azure AD test user</span></span>
<span data-ttu-id="1bb52-176">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="1bb52-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 測試使用者][100]

<span data-ttu-id="1bb52-178">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1bb52-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1bb52-179">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="1bb52-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![hello Azure Active Directory] 按鈕](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1bb52-181">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="1bb52-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1bb52-183">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="1bb52-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![hello [新增] 按鈕](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1bb52-185">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1bb52-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1bb52-187">a.</span><span class="sxs-lookup"><span data-stu-id="1bb52-187">a.</span></span> <span data-ttu-id="1bb52-188">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="1bb52-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1bb52-189">b.</span><span class="sxs-lookup"><span data-stu-id="1bb52-189">b.</span></span> <span data-ttu-id="1bb52-190">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="1bb52-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1bb52-191">c.</span><span class="sxs-lookup"><span data-stu-id="1bb52-191">c.</span></span> <span data-ttu-id="1bb52-192">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="1bb52-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1bb52-193">d.</span><span class="sxs-lookup"><span data-stu-id="1bb52-193">d.</span></span> <span data-ttu-id="1bb52-194">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1bb52-194">Click **Create**.</span></span>
 
### <a name="create-a-thoughtworks-mingle-test-user"></a><span data-ttu-id="1bb52-195">建立 Thoughtworks Mingle 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1bb52-195">Create a Thoughtworks Mingle test user</span></span>

<span data-ttu-id="1bb52-196">Azure AD 使用者 toobe 無法 toosign 中，它們必須已佈建的 toohello Thoughtworks Mingle 的應用程式使用他們的 Azure Active Directory 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="1bb52-196">For Azure AD users toobe able toosign in, they must be provisioned toohello Thoughtworks Mingle application using their Azure Active Directory user names.</span></span> <span data-ttu-id="1bb52-197">在 Thoughtworks Mingle 的 hello 情況下，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="1bb52-197">In hello case of Thoughtworks Mingle, provisioning is a manual task.</span></span>

<span data-ttu-id="1bb52-198">**tooconfigure 使用者佈建，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1bb52-198">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="1bb52-199">Tooyour Thoughtworks Mingle 公司網站 administrator 身分登入。</span><span class="sxs-lookup"><span data-stu-id="1bb52-199">Log in tooyour Thoughtworks Mingle company site as administrator.</span></span>

2. <span data-ttu-id="1bb52-200">按一下 [設定檔] 。</span><span class="sxs-lookup"><span data-stu-id="1bb52-200">Click **Profile**.</span></span>
   
    <span data-ttu-id="1bb52-201">![第一個專案](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "第一個專案")</span><span class="sxs-lookup"><span data-stu-id="1bb52-201">![Your First Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Your First Project")</span></span>

3. <span data-ttu-id="1bb52-202">按一下 hello **Admin**索引標籤，然後再按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="1bb52-202">Click hello **Admin** tab, and then click **Users**.</span></span>
   
    <span data-ttu-id="1bb52-203">![使用者](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="1bb52-203">![Users](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Users")</span></span>

4. <span data-ttu-id="1bb52-204">按一下 [新使用者] 。</span><span class="sxs-lookup"><span data-stu-id="1bb52-204">Click **New User**.</span></span>
   
    <span data-ttu-id="1bb52-205">![新增使用者](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="1bb52-205">![New User](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "New User")</span></span>

5. <span data-ttu-id="1bb52-206">在 [hello**新使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1bb52-206">On hello **New User** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="1bb52-207">![[新增使用者] 對話方塊](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "[新增使用者]")</span><span class="sxs-lookup"><span data-stu-id="1bb52-207">![New User dialog](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "New User")</span></span>  
 
    <span data-ttu-id="1bb52-208">a.</span><span class="sxs-lookup"><span data-stu-id="1bb52-208">a.</span></span> <span data-ttu-id="1bb52-209">型別 hello**登入名稱**，**顯示名稱**，**選擇密碼**，**確認密碼**的有效 azure AD 帳戶想 tooprovisionhello 到相關的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="1bb52-209">Type hello **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span> 

    <span data-ttu-id="1bb52-210">b.</span><span class="sxs-lookup"><span data-stu-id="1bb52-210">b.</span></span> <span data-ttu-id="1bb52-211">選取 [完整使用者] 做為 [使用者類型]。</span><span class="sxs-lookup"><span data-stu-id="1bb52-211">As **User type**, select **Full user**.</span></span>

    <span data-ttu-id="1bb52-212">c.</span><span class="sxs-lookup"><span data-stu-id="1bb52-212">c.</span></span> <span data-ttu-id="1bb52-213">按一下 [建立這個設定檔] 。</span><span class="sxs-lookup"><span data-stu-id="1bb52-213">Click **Create This Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="1bb52-214">您可以使用任何其他 Thoughtworks Mingle 使用者帳戶建立工具或 Api 提供 Thoughtworks Mingle tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="1bb52-214">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle tooprovision AAD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1bb52-215">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1bb52-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1bb52-216">在本節中，您可以授與存取 tooThoughtworks Mingle 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1bb52-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThoughtworks Mingle.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="1bb52-218">**tooassign 許 Simon tooThoughtworks Mingle，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1bb52-218">**tooassign Britta Simon tooThoughtworks Mingle, perform hello following steps:**</span></span>

1. <span data-ttu-id="1bb52-219">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1bb52-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="1bb52-221">在 [hello] 應用程式清單中，選取**Thoughtworks Mingle**。</span><span class="sxs-lookup"><span data-stu-id="1bb52-221">In hello applications list, select **Thoughtworks Mingle**.</span></span>

    ![hello 應用程式清單中的 hello Thoughtworks Mingle 連結](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. <span data-ttu-id="1bb52-223">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="1bb52-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202] 

4. <span data-ttu-id="1bb52-225">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1bb52-225">Click **Add** button.</span></span> <span data-ttu-id="1bb52-226">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1bb52-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="1bb52-228">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="1bb52-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1bb52-229">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1bb52-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1bb52-230">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1bb52-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1bb52-231">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="1bb52-231">Test single sign-on</span></span>

<span data-ttu-id="1bb52-232">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="1bb52-232">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1bb52-233">當您按一下 hello Thoughtworks Mingle 並排顯示 hello 存取面板中的時，您應該取得自動登入 tooyour Thoughtworks Mingle 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1bb52-233">When you click hello Thoughtworks Mingle tile in hello Access Panel, you should get automatically signed-on tooyour Thoughtworks Mingle application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1bb52-234">其他資源</span><span class="sxs-lookup"><span data-stu-id="1bb52-234">Additional resources</span></span>

* [<span data-ttu-id="1bb52-235">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1bb52-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1bb52-236">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="1bb52-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png


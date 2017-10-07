---
title: "教學課程：Azure Active Directory 與 KnowBe4 Security Awareness Training 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 KnowBe4 安全性認知訓練之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b80d2212-cc5f-4adb-836c-570640810c39
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 907fa814b82c9ffb2376f73470b746a37104c66e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-knowbe4-security-awareness-training"></a><span data-ttu-id="605d8-103">教學課程：Azure Active Directory 與 KnowBe4 Security Awareness Training 整合</span><span class="sxs-lookup"><span data-stu-id="605d8-103">Tutorial: Azure Active Directory integration with KnowBe4 Security Awareness Training</span></span>

<span data-ttu-id="605d8-104">在此教學課程中，您學會如何 toointegrate KnowBe4 安全性認知訓練與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="605d8-104">In this tutorial, you learn how toointegrate KnowBe4 Security Awareness Training with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="605d8-105">與 Azure AD 整合 KnowBe4 安全性認知訓練可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="605d8-105">Integrating KnowBe4 Security Awareness Training with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="605d8-106">您可以在 Azure 中控制 AD 擁有存取 tooKnowBe4 安全性認知訓練</span><span class="sxs-lookup"><span data-stu-id="605d8-106">You can control in Azure AD who has access tooKnowBe4 Security Awareness Training</span></span>
- <span data-ttu-id="605d8-107">您可以啟用 tooautomatically 取得的使用者登入 （單一登入） tooKnowBe4 安全性認知訓練與他們的 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="605d8-107">You can enable your users tooautomatically get signed-on tooKnowBe4 Security Awareness Training (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="605d8-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="605d8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="605d8-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="605d8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="605d8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="605d8-110">Prerequisites</span></span>

<span data-ttu-id="605d8-111">tooconfigure KnowBe4 安全性認知訓練與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="605d8-111">tooconfigure Azure AD integration with KnowBe4 Security Awareness Training, you need hello following items:</span></span>

- <span data-ttu-id="605d8-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="605d8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="605d8-113">已啟用 KnowBe4 Security Awareness Training 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="605d8-113">A KnowBe4 Security Awareness Training single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="605d8-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="605d8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="605d8-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="605d8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="605d8-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="605d8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="605d8-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="605d8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="605d8-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="605d8-118">Scenario description</span></span>
<span data-ttu-id="605d8-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="605d8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="605d8-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="605d8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="605d8-121">從 hello 圖庫加入 KnowBe4 安全性認知訓練</span><span class="sxs-lookup"><span data-stu-id="605d8-121">Adding KnowBe4 Security Awareness Training from hello gallery</span></span>
2. <span data-ttu-id="605d8-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="605d8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-knowbe4-security-awareness-training-from-hello-gallery"></a><span data-ttu-id="605d8-123">從 hello 圖庫加入 KnowBe4 安全性認知訓練</span><span class="sxs-lookup"><span data-stu-id="605d8-123">Adding KnowBe4 Security Awareness Training from hello gallery</span></span>
<span data-ttu-id="605d8-124">tooconfigure hello 整合 KnowBe4 安全性認知訓練到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd KnowBe4 安全性認知訓練。</span><span class="sxs-lookup"><span data-stu-id="605d8-124">tooconfigure hello integration of KnowBe4 Security Awareness Training into Azure AD, you need tooadd KnowBe4 Security Awareness Training from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="605d8-125">**tooadd KnowBe4 安全性認知訓練 hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="605d8-125">**tooadd KnowBe4 Security Awareness Training from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="605d8-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="605d8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="605d8-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="605d8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="605d8-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="605d8-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="605d8-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="605d8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="605d8-133">在 [hello] 搜尋方塊中，輸入**KnowBe4 安全性認知訓練**。</span><span class="sxs-lookup"><span data-stu-id="605d8-133">In hello search box, type **KnowBe4 Security Awareness Training**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_search.png)

5. <span data-ttu-id="605d8-135">在 hello [結果] 窗格中，選取**KnowBe4 安全性認知訓練**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="605d8-135">In hello results panel, select **KnowBe4 Security Awareness Training**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="605d8-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="605d8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="605d8-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 KnowBe4 Security Awareness Training 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="605d8-138">In this section, you configure and test Azure AD single sign-on with KnowBe4 Security Awareness Training based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="605d8-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 KnowBe4 安全性認知定型中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="605d8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in KnowBe4 Security Awareness Training is tooa user in Azure AD.</span></span> <span data-ttu-id="605d8-140">換句話說，Azure AD 使用者與 hello KnowBe4 安全性認知定型中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="605d8-140">In other words, a link relationship between an Azure AD user and hello related user in KnowBe4 Security Awareness Training needs toobe established.</span></span>

<span data-ttu-id="605d8-141">在 KnowBe4 安全性認知訓練，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="605d8-141">In KnowBe4 Security Awareness Training, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="605d8-142">tooconfigure 及 KnowBe4 安全性認知訓練與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="605d8-142">tooconfigure and test Azure AD single sign-on with KnowBe4 Security Awareness Training, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="605d8-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="605d8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="605d8-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="605d8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="605d8-145">**[建立測試使用者 KnowBe4 安全性認知訓練](#creating-a-knowbe4-security-awareness-training-test-user)** -toohave 許 Simon KnowBe4 安全性感知定型所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="605d8-145">**[Creating a KnowBe4 Security Awareness Training test user](#creating-a-knowbe4-security-awareness-training-test-user)** - toohave a counterpart of Britta Simon in KnowBe4 Security Awareness Training that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="605d8-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="605d8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="605d8-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="605d8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="605d8-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="605d8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="605d8-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 KnowBe4 安全性認知訓練應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="605d8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your KnowBe4 Security Awareness Training application.</span></span>

<span data-ttu-id="605d8-150">**KnowBe4 安全性認知訓練與 Azure AD 單一登入 tooconfigure 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="605d8-150">**tooconfigure Azure AD single sign-on with KnowBe4 Security Awareness Training, perform hello following steps:**</span></span>

1. <span data-ttu-id="605d8-151">在 Azure 入口網站上 hello hello **KnowBe4 安全性認知訓練**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="605d8-151">In hello Azure portal, on hello **KnowBe4 Security Awareness Training** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="605d8-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="605d8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_samlbase.png)

3. <span data-ttu-id="605d8-155">在 hello **KnowBe4 安全性認知訓練網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="605d8-155">On hello **KnowBe4 Security Awareness Training Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_url.png)

    <span data-ttu-id="605d8-157">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="605d8-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="605d8-158">hello 值不是真正的。</span><span class="sxs-lookup"><span data-stu-id="605d8-158">hello value is not real.</span></span> <span data-ttu-id="605d8-159">更新 hello 值與 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="605d8-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="605d8-160">請連絡[KnowBe4 安全性認知訓練用戶端支援小組](mailto:support@KnowBe4.com)tooget hello 值。</span><span class="sxs-lookup"><span data-stu-id="605d8-160">Contact [KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com) tooget hello value.</span></span> 
 

4. <span data-ttu-id="605d8-161">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Raw)**然後儲存 hello 憑證檔案儲存在您的電腦。</span><span class="sxs-lookup"><span data-stu-id="605d8-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_certificate.png) 

5. <span data-ttu-id="605d8-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="605d8-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="605d8-165">在 hello **KnowBe4 安全性認知訓練設定**區段中，按一下**設定 KnowBe4 安全性認知訓練**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="605d8-165">On hello **KnowBe4 Security Awareness Training Configuration** section, click **Configure KnowBe4 Security Awareness Training** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="605d8-166">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="605d8-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_configure.png) 

7. <span data-ttu-id="605d8-168">tooconfigure 單一登入上**KnowBe4 安全性認知訓練**端，您需要下載 toosend hello**憑證 (Raw)**，**登出 URL、 SAML 實體識別碼和 SAML 單一登入服務 URL**太[KnowBe4 安全性認知訓練用戶端支援小組](mailto:support@KnowBe4.com)。</span><span class="sxs-lookup"><span data-stu-id="605d8-168">tooconfigure single sign-on on **KnowBe4 Security Awareness Training** side, you need toosend hello downloaded **Certificate (Raw)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com).</span></span>

> [!TIP]
> <span data-ttu-id="605d8-169">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="605d8-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="605d8-170">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="605d8-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="605d8-171">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="605d8-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="605d8-172">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="605d8-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="605d8-173">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="605d8-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="605d8-175">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="605d8-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="605d8-176">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="605d8-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="605d8-178">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="605d8-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="605d8-180">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="605d8-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="605d8-182">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="605d8-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="605d8-184">a.</span><span class="sxs-lookup"><span data-stu-id="605d8-184">a.</span></span> <span data-ttu-id="605d8-185">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="605d8-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="605d8-186">b.</span><span class="sxs-lookup"><span data-stu-id="605d8-186">b.</span></span> <span data-ttu-id="605d8-187">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="605d8-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="605d8-188">c.</span><span class="sxs-lookup"><span data-stu-id="605d8-188">c.</span></span> <span data-ttu-id="605d8-189">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="605d8-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="605d8-190">d.</span><span class="sxs-lookup"><span data-stu-id="605d8-190">d.</span></span> <span data-ttu-id="605d8-191">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="605d8-191">Click **Create**.</span></span>
 
### <a name="creating-a-knowbe4-security-awareness-training-test-user"></a><span data-ttu-id="605d8-192">建立 KnowBe4 Security Awareness Training 測試使用者</span><span class="sxs-lookup"><span data-stu-id="605d8-192">Creating a KnowBe4 Security Awareness Training test user</span></span>

<span data-ttu-id="605d8-193">hello 本節目標在於 toocreate 呼叫許 Simon KnowBe4 安全性認知定型中的使用者。</span><span class="sxs-lookup"><span data-stu-id="605d8-193">hello objective of this section is toocreate a user called Britta Simon in KnowBe4 Security Awareness Training.</span></span> <span data-ttu-id="605d8-194">KnowBe4 Security Awareness Training 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="605d8-194">KnowBe4 Security Awareness Training supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="605d8-195">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="605d8-195">There is no action item for you in this section.</span></span> <span data-ttu-id="605d8-196">如果尚未存在嘗試 tooaccess KnowBe4 安全性認知訓練期間，建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="605d8-196">A new user is created during an attempt tooaccess KnowBe4 Security Awareness Training if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="605d8-197">若要手動 toocreate 使用者，您需要 toocontact hello [KnowBe4 安全性認知訓練支援小組](mailto:support@KnowBe4.com)。</span><span class="sxs-lookup"><span data-stu-id="605d8-197">If you need toocreate a user manually, you need toocontact hello [KnowBe4 Security Awareness Training support team](mailto:support@KnowBe4.com).</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="605d8-198">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="605d8-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="605d8-199">在本節中，您可以啟用許 Simon toouse Azure 單一登入授與存取 tooKnowBe4 安全性認知訓練。</span><span class="sxs-lookup"><span data-stu-id="605d8-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKnowBe4 Security Awareness Training.</span></span>

![指派使用者][200] 

<span data-ttu-id="605d8-201">**tooassign 許 Simon tooKnowBe4 安全性認知訓練，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="605d8-201">**tooassign Britta Simon tooKnowBe4 Security Awareness Training, perform hello following steps:**</span></span>

1. <span data-ttu-id="605d8-202">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="605d8-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="605d8-204">在 [hello] 應用程式清單中，選取**KnowBe4 安全性認知訓練**。</span><span class="sxs-lookup"><span data-stu-id="605d8-204">In hello applications list, select **KnowBe4 Security Awareness Training**.</span></span>

    ![設定單一登入](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_app.png) 

3. <span data-ttu-id="605d8-206">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="605d8-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="605d8-208">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="605d8-208">Click **Add** button.</span></span> <span data-ttu-id="605d8-209">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="605d8-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="605d8-211">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="605d8-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="605d8-212">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="605d8-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="605d8-213">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="605d8-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="605d8-214">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="605d8-214">Testing single sign-on</span></span>

<span data-ttu-id="605d8-215">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="605d8-215">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
  
<span data-ttu-id="605d8-216">當您按一下 hello KnowBe4 安全性認知訓練磚 hello 存取面板中的時，您應該取得自動登入 tooyour KnowBe4 安全性認知訓練應用程式。</span><span class="sxs-lookup"><span data-stu-id="605d8-216">When you click hello KnowBe4 Security Awareness Training tile in hello Access Panel, you should get automatically signed-on tooyour KnowBe4 Security Awareness Training application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="605d8-217">其他資源</span><span class="sxs-lookup"><span data-stu-id="605d8-217">Additional resources</span></span>

* [<span data-ttu-id="605d8-218">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="605d8-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="605d8-219">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="605d8-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_203.png


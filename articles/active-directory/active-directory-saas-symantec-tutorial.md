---
title: "教學課程：Azure Active Directory 與 Symantec Web Security Service (WSS) 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Symantec 網站安全性服務 (WSS) 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9f02b3d4ce2073110c55af4b567b0e3b5a88404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="837f0-103">教學課程：Azure Active Directory 與 Symantec Web Security Service (WSS) 整合</span><span class="sxs-lookup"><span data-stu-id="837f0-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="837f0-104">在此教學課程中，您將學習如何 toointegrate 您 Symantec 網站安全性服務 (WSS) 帳戶與您的 Azure Active Directory (Azure AD) 帳戶，讓 WSS 可以驗證在 hello Azure AD 中佈建使用者使用 SAML 驗證並強制執行使用者或群組層級原則規則。</span><span class="sxs-lookup"><span data-stu-id="837f0-104">In this tutorial, you will learn how toointegrate your Symantec Web Security Service (WSS) account with your Azure Active Directory (Azure AD) account so that WSS can authenticate an end user provisioned in hello Azure AD using SAML authentication and enforce user or group level policy rules.</span></span>

<span data-ttu-id="837f0-105">與 Azure AD 整合 Symantec 網站安全性服務 (WSS) 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="837f0-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="837f0-106">管理所有 hello 一般使用者與您的 WSS 帳戶與您的 Azure AD 入口網站所使用的群組。</span><span class="sxs-lookup"><span data-stu-id="837f0-106">Manage all of hello end users and groups used by your WSS account from your Azure AD portal.</span></span> 

- <span data-ttu-id="837f0-107">允許 hello 結束使用者 tooauthenticate 本身中 WSS 使用其 Azure AD 認證。</span><span class="sxs-lookup"><span data-stu-id="837f0-107">Allow hello end users tooauthenticate themselves in WSS using their Azure AD credentials.</span></span>

- <span data-ttu-id="837f0-108">啟用 hello 強制的使用者和群組 WSS 帳戶中所定義的層級原則規則。</span><span class="sxs-lookup"><span data-stu-id="837f0-108">Enable hello enforcement of user and group level policy rules defined in your WSS account.</span></span>

<span data-ttu-id="837f0-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="837f0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="837f0-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="837f0-110">Prerequisites</span></span>

<span data-ttu-id="837f0-111">tooconfigure Azure AD 整合與 Symantec 網站安全性服務 (WSS)，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="837f0-111">tooconfigure Azure AD integration with Symantec Web Security Service (WSS), you need hello following items:</span></span>

- <span data-ttu-id="837f0-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="837f0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="837f0-113">Symantec Web Security Service (WSS) 帳戶</span><span class="sxs-lookup"><span data-stu-id="837f0-113">A Symantec Web Security Service (WSS) account</span></span>

> [!NOTE]
> <span data-ttu-id="837f0-114">本教學課程中的步驟 tootest hello，不建議使用 WSS 帳戶目前正用於生產用途。</span><span class="sxs-lookup"><span data-stu-id="837f0-114">tootest hello steps in this tutorial, we do not recommend using a WSS account that is currently being used for production purpose.</span></span>

<span data-ttu-id="837f0-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="837f0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="837f0-116">除非必要，否則請勿使用目前正用於生產用途的 WSS 帳戶來進行這項測試。</span><span class="sxs-lookup"><span data-stu-id="837f0-116">Do not use your WSS account that is currently being used for production purpose for this test unless it is necessary.</span></span>
- <span data-ttu-id="837f0-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="837f0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="837f0-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="837f0-118">Scenario description</span></span>
<span data-ttu-id="837f0-119">在本教學課程中，您將設定您 Azure AD tooenable 單一登入 tooWSS 使用 Azure AD 帳戶中定義的 hello 終端使用者認證。</span><span class="sxs-lookup"><span data-stu-id="837f0-119">In this tutorial, you will configure your Azure AD tooenable single sign-on tooWSS using hello end user credentials defined in your Azure AD account.</span></span>
<span data-ttu-id="837f0-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="837f0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="837f0-121">從 hello 圖庫加入 hello Symantec 網站安全性服務 (WSS) 應用程式</span><span class="sxs-lookup"><span data-stu-id="837f0-121">Adding hello Symantec Web Security Service (WSS) app from hello gallery</span></span>
2. <span data-ttu-id="837f0-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="837f0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a><span data-ttu-id="837f0-123">從 hello 圖庫加入 Symantec 網站安全性服務 (WSS)</span><span class="sxs-lookup"><span data-stu-id="837f0-123">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
<span data-ttu-id="837f0-124">tooconfigure hello 整合 Symantec 網站安全性服務 (WSS) 至 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Symantec 網站安全性服務 (WSS)。</span><span class="sxs-lookup"><span data-stu-id="837f0-124">tooconfigure hello integration of Symantec Web Security Service (WSS) into Azure AD, you need tooadd Symantec Web Security Service (WSS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="837f0-125">**tooadd Symantec 網站安全性服務 (WSS) 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="837f0-125">**tooadd Symantec Web Security Service (WSS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="837f0-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="837f0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="837f0-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="837f0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="837f0-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="837f0-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="837f0-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="837f0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="837f0-133">在 hello 搜尋方塊中，輸入**Symantec 網站安全性服務 (WSS)**，選取**Symantec 網站安全性服務 (WSS)**然後按一下 從結果面板**新增**按鈕 tooadd hello應用程式。</span><span class="sxs-lookup"><span data-stu-id="837f0-133">In hello search box, type **Symantec Web Security Service (WSS)**, select **Symantec Web Security Service (WSS)** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Symantec 網站安全性服務 (WSS) hello [結果] 清單中](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="837f0-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="837f0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="837f0-136">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Symantec Web Security Service (WSS) 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="837f0-136">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="837f0-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Symantec 網站安全性服務 (WSS) 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="837f0-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Symantec Web Security Service (WSS) is tooa user in Azure AD.</span></span> <span data-ttu-id="837f0-138">換句話說，Azure AD 使用者與 hello 相關的使用者在 Symantec 網站安全性服務 (WSS) 之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="837f0-138">In other words, a link relationship between an Azure AD user and hello related user in Symantec Web Security Service (WSS) needs toobe established.</span></span>

<span data-ttu-id="837f0-139">在 Symantec 網站安全性服務 (WSS)，將指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="837f0-139">In Symantec Web Security Service (WSS), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="837f0-140">tooconfigure 和測試 Azure AD 單一登入與 Symantec 網站安全性服務 (WSS)，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="837f0-140">tooconfigure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="837f0-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="837f0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="837f0-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="837f0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="837f0-143">**[建立 Symantec 網站安全性服務 (WSS) 測試使用者](#create-a-symantec-web-security-service-wss-test-user)** -toohave 許 Simon 中 Symantec Web 安全性服務 (WSS) 表示法連結的 toohello Azure AD 使用者的對應項目。</span><span class="sxs-lookup"><span data-stu-id="837f0-143">**[Create a Symantec Web Security Service (WSS) test user](#create-a-symantec-web-security-service-wss-test-user)** - toohave a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="837f0-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="837f0-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="837f0-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="837f0-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="837f0-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="837f0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="837f0-147">在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您的 Symantec 網站安全性服務 (WSS) 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="837f0-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="837f0-148">**tooconfigure Azure AD 單一登入與 Symantec 網站安全性服務 (WSS)，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="837f0-148">**tooconfigure Azure AD single sign-on with Symantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="837f0-149">在 Azure 入口網站上 hello hello **Symantec 網站安全性服務 (WSS)**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="837f0-149">In hello Azure portal, on hello **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="837f0-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="837f0-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="837f0-153">在 hello **Symantec 網站安全性服務 (WSS) 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="837f0-153">On hello **Symantec Web Security Service (WSS) Domain and URLs** section, perform hello following steps:</span></span>

    ![Symantec Web Security Service (WSS) 的網域和 URL 單一登入資訊](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="837f0-155">a.</span><span class="sxs-lookup"><span data-stu-id="837f0-155">a.</span></span> <span data-ttu-id="837f0-156">在 hello**識別碼**文字方塊中，型別 hello URL:`https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="837f0-156">In hello **Identifier** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    <span data-ttu-id="837f0-157">b.</span><span class="sxs-lookup"><span data-stu-id="837f0-157">b.</span></span> <span data-ttu-id="837f0-158">在 hello**回覆 URL**文字方塊中，型別 hello URL:`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span><span class="sxs-lookup"><span data-stu-id="837f0-158">In hello **Reply URL** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span></span>

    > [!NOTE]
    > <span data-ttu-id="837f0-159">Hello，請連絡[Symantec 網站安全性服務 (WSS) 用戶端支援小組](https://www.symantec.com/contact-us)如果值為 hello 的 hello**識別碼**和**回覆 URL**基於某些原因無法運作。</span><span class="sxs-lookup"><span data-stu-id="837f0-159">Please contact hello [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) if hello values for hello **Identifier** and **Reply URL** are not working for some reason.</span></span>

4. <span data-ttu-id="837f0-160">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="837f0-160">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="837f0-162">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="837f0-162">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="837f0-164">tooconfigure 單一登入 hello Symantec 網站安全性服務 (WSS) 端上，請參閱 toohello WSS 線上文件。</span><span class="sxs-lookup"><span data-stu-id="837f0-164">tooconfigure single sign-on on hello Symantec Web Security Service (WSS) side, refer toohello WSS online documentation.</span></span> <span data-ttu-id="837f0-165">下載的 hello**中繼資料 XML**檔案需要 toobe 匯入 hello WSS 入口網站。</span><span class="sxs-lookup"><span data-stu-id="837f0-165">hello downloaded **Metadata XML** file will need toobe imported into hello WSS portal.</span></span> <span data-ttu-id="837f0-166">連絡 hello [Symantec 網站安全性服務 (WSS) 支援小組](https://www.symantec.com/contact-us)如果您需要協助以 hello hello WSS 入口網站上的組態。</span><span class="sxs-lookup"><span data-stu-id="837f0-166">Contact hello [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) if you need assistance with hello configuration on hello WSS portal.</span></span>

> [!TIP]
> <span data-ttu-id="837f0-167">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="837f0-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="837f0-168">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="837f0-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="837f0-169">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="837f0-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="837f0-170">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="837f0-170">Create an Azure AD test user</span></span>

<span data-ttu-id="837f0-171">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="837f0-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="837f0-173">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="837f0-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="837f0-174">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="837f0-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="837f0-176">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="837f0-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="837f0-178">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="837f0-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="837f0-180">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="837f0-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    <span data-ttu-id="837f0-182">a.</span><span class="sxs-lookup"><span data-stu-id="837f0-182">a.</span></span> <span data-ttu-id="837f0-183">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="837f0-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="837f0-184">b.</span><span class="sxs-lookup"><span data-stu-id="837f0-184">b.</span></span> <span data-ttu-id="837f0-185">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="837f0-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="837f0-186">c.</span><span class="sxs-lookup"><span data-stu-id="837f0-186">c.</span></span> <span data-ttu-id="837f0-187">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="837f0-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="837f0-188">d.</span><span class="sxs-lookup"><span data-stu-id="837f0-188">d.</span></span> <span data-ttu-id="837f0-189">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="837f0-189">Click **Create**.</span></span>
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="837f0-190">建立 Symantec Web Security Service (WSS) 測試使用者</span><span class="sxs-lookup"><span data-stu-id="837f0-190">Create a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="837f0-191">在本節中，您要在 Symantec Web Security Service (WSS) 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="837f0-191">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="837f0-192">hello 對應結束使用者名稱可以 hello WSS 入口網站中手動建立，或您可以等候 hello 使用者/群組佈建在 hello Azure AD 同步處理的 toobe toohello WSS 網站後幾分鐘的時間 （~ 15 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="837f0-192">hello corresponding end username can be manually created in hello WSS portal or you can wait for hello users/groups provisioned in hello Azure AD toobe synchronized toohello WSS portal after a few minutes (~15 minutes).</span></span> <span data-ttu-id="837f0-193">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="837f0-193">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="837f0-194">hello 終端使用者電腦，將會使用的 toobrowse 網站的 hello 公用 IP 位址也需要 toobe hello Symantec 網站安全性服務 (WSS) 網站中佈建。</span><span class="sxs-lookup"><span data-stu-id="837f0-194">hello public IP address of hello end user machine, which will be used toobrowse websites also need toobe provisioned in hello Symantec Web Security Service (WSS) portal.</span></span>

> [!NOTE]
> <span data-ttu-id="837f0-195">請[按一下這裡](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1)tooget 您機器的公用 IPaddress。</span><span class="sxs-lookup"><span data-stu-id="837f0-195">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget your machine's public IPaddress.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="837f0-196">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="837f0-196">Assign hello Azure AD test user</span></span>

<span data-ttu-id="837f0-197">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooSymantec Web 安全性服務 (WSS)。</span><span class="sxs-lookup"><span data-stu-id="837f0-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSymantec Web Security Service (WSS).</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="837f0-199">**tooassign 許 Simon tooSymantec Web 安全性服務 (WSS) 執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="837f0-199">**tooassign Britta Simon tooSymantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="837f0-200">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="837f0-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="837f0-202">在 [hello] 應用程式清單中，選取**Symantec 網站安全性服務 (WSS)**。</span><span class="sxs-lookup"><span data-stu-id="837f0-202">In hello applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![hello 應用程式清單中的 hello Symantec 網站安全性服務 (WSS) 連結](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. <span data-ttu-id="837f0-204">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="837f0-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="837f0-206">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="837f0-206">Click **Add** button.</span></span> <span data-ttu-id="837f0-207">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="837f0-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="837f0-209">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="837f0-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="837f0-210">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="837f0-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="837f0-211">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="837f0-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="837f0-212">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="837f0-212">Test single sign-on</span></span>

<span data-ttu-id="837f0-213">在本節中，您將測試 hello 單一登入功能，現在您已設定您的 WSS 帳戶 toouse SAML 驗證您的 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="837f0-213">In this section, you'll test hello single sign-on functionality now that you've configured your WSS account toouse your Azure AD for SAML authentication.</span></span>

<span data-ttu-id="837f0-214">設定之後會 tooWSS，當您開啟網頁瀏覽器並 toobrowse tooa 站台，然後再試一次您網頁瀏覽器 tooproxy 流量重新導向 toohello Azure 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="837f0-214">After you have configured your web browser tooproxy traffic tooWSS, when you open your web browser and try toobrowse tooa site then you'll be redirected toohello Azure sign-on page.</span></span> <span data-ttu-id="837f0-215">輸入 hello Azure AD (也就是 BrittaSimon) 中的 hello 的已佈建的 hello 測試終端使用者的認證，以及相關聯的密碼。</span><span class="sxs-lookup"><span data-stu-id="837f0-215">Enter hello credentials of hello test end user that has been provisioned in hello Azure AD (that is, BrittaSimon) and associated password.</span></span> <span data-ttu-id="837f0-216">驗證之後，您會選擇可以 toobrowse toohello 網站。</span><span class="sxs-lookup"><span data-stu-id="837f0-216">Once authenticated, you'll be able toobrowse toohello website that you chose.</span></span> <span data-ttu-id="837f0-217">您應該從瀏覽 tooa 特定站台，則當您以使用者 BrittaSimon 嘗試 toobrowse toothat 站台時，您應該看見 hello WSS 區塊頁面 hello WSS 端 tooblock BrittaSimon 中建立的原則規則。</span><span class="sxs-lookup"><span data-stu-id="837f0-217">Should you create a policy rule on hello WSS side tooblock BrittaSimon from browsing tooa particular site then you should see hello WSS block page when you attempt toobrowse toothat site as user BrittaSimon.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="837f0-218">其他資源</span><span class="sxs-lookup"><span data-stu-id="837f0-218">Additional resources</span></span>

* [<span data-ttu-id="837f0-219">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="837f0-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="837f0-220">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="837f0-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png


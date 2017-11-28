---
title: "教學課程：Azure Active Directory 與 Asana 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Asana 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: 9ac35dedc809b2b3dfb461d92a5afb066ccdedde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a><span data-ttu-id="6d174-103">教學課程：Azure Active Directory 與 Asana 整合</span><span class="sxs-lookup"><span data-stu-id="6d174-103">Tutorial: Azure Active Directory integration with Asana</span></span>

<span data-ttu-id="6d174-104">在此教學課程中，您學會如何 toointegrate Asana 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="6d174-104">In this tutorial, you learn how toointegrate Asana with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6d174-105">與 Azure AD 整合 Asana 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="6d174-105">Integrating Asana with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6d174-106">您可以控制存取 tooAsana Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="6d174-106">You can control in Azure AD who has access tooAsana</span></span>
- <span data-ttu-id="6d174-107">您可以啟用您的使用者 tooautomatically get 登入 tooAsana （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="6d174-107">You can enable your users tooautomatically get signed-on tooAsana (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6d174-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6d174-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6d174-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="6d174-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d174-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6d174-110">Prerequisites</span></span>

<span data-ttu-id="6d174-111">tooconfigure Asana 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="6d174-111">tooconfigure Azure AD integration with Asana, you need hello following items:</span></span>

- <span data-ttu-id="6d174-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6d174-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6d174-113">已啟用 Asana 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6d174-113">An Asana single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6d174-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="6d174-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6d174-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="6d174-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6d174-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6d174-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6d174-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="6d174-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6d174-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="6d174-118">Scenario description</span></span>
<span data-ttu-id="6d174-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6d174-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6d174-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="6d174-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6d174-121">從 hello 圖庫加入 Asana</span><span class="sxs-lookup"><span data-stu-id="6d174-121">Adding Asana from hello gallery</span></span>
2. <span data-ttu-id="6d174-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6d174-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asana-from-hello-gallery"></a><span data-ttu-id="6d174-123">從 hello 圖庫加入 Asana</span><span class="sxs-lookup"><span data-stu-id="6d174-123">Adding Asana from hello gallery</span></span>
<span data-ttu-id="6d174-124">tooconfigure hello 整合 Asana 到 Azure AD，您需要 tooadd Asana hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6d174-124">tooconfigure hello integration of Asana into Azure AD, you need tooadd Asana from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6d174-125">**tooadd Asana 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6d174-125">**tooadd Asana from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d174-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="6d174-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="6d174-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6d174-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6d174-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6d174-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="6d174-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="6d174-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="6d174-133">在 hello 搜尋方塊中，輸入**Asana**，選取**Asana**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6d174-133">In hello search box, type **Asana**, select **Asana** from result panel then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6d174-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6d174-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6d174-136">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Asana 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6d174-136">In this section, you configure and test Azure AD single sign-on with Asana based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6d174-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Asana 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="6d174-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Asana is tooa user in Azure AD.</span></span> <span data-ttu-id="6d174-138">換句話說，Azure AD 使用者與 hello Asana 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="6d174-138">In other words, a link relationship between an Azure AD user and hello related user in Asana needs toobe established.</span></span>

<span data-ttu-id="6d174-139">Asana 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6d174-139">In Asana, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6d174-140">tooconfigure 及 Asana 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="6d174-140">tooconfigure and test Azure AD single sign-on with Asana, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6d174-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="6d174-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6d174-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="6d174-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6d174-143">**[建立測試使用者 Asana](#create-an-asana-test-user)**  -toohave 許 Simon Asana 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="6d174-143">**[Create an Asana test user](#create-an-asana-test-user)** - toohave a counterpart of Britta Simon in Asana that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6d174-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6d174-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6d174-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="6d174-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6d174-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6d174-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6d174-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Asana 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="6d174-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Asana application.</span></span>

<span data-ttu-id="6d174-148">**tooconfigure Azure AD 單一登入與 Asana，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6d174-148">**tooconfigure Azure AD single sign-on with Asana, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d174-149">在 Azure 入口網站上 hello hello **Asana**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="6d174-149">In hello Azure portal, on hello **Asana** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="6d174-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6d174-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. <span data-ttu-id="6d174-153">在 hello **Asana 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6d174-153">On hello **Asana Domain and URLs** section, perform hello following steps:</span></span>

    ![Asana 網域與 URL 單一登入資訊](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    <span data-ttu-id="6d174-155">a.</span><span class="sxs-lookup"><span data-stu-id="6d174-155">a.</span></span> <span data-ttu-id="6d174-156">在 hello**登入 URL**文字方塊中，型別 URL:`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="6d174-156">In hello **Sign-on URL** textbox, type URL: `https://app.asana.com/`</span></span>

    <span data-ttu-id="6d174-157">b.</span><span class="sxs-lookup"><span data-stu-id="6d174-157">b.</span></span> <span data-ttu-id="6d174-158">在 hello**識別碼**文字方塊中，型別值：`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="6d174-158">In hello **Identifier** textbox, type value: `https://app.asana.com/`</span></span>
 
4. <span data-ttu-id="6d174-159">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="6d174-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. <span data-ttu-id="6d174-161">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6d174-161">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6d174-163">在 hello **Asana 組態**區段中，按一下**設定 Asana** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="6d174-163">On hello **Asana Configuration** section, click **Configure Asana** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6d174-164">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="6d174-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Asana 設定](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. <span data-ttu-id="6d174-166">在不同的瀏覽器視窗中，登入 tooyour Asana 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6d174-166">In a different browser window, sign-on tooyour Asana application.</span></span> <span data-ttu-id="6d174-167">tooconfigure Asana，hello hello 右上角的囉 」 畫面上的工作區名稱，即可存取 hello 工作地區設定中的 SSO。</span><span class="sxs-lookup"><span data-stu-id="6d174-167">tooconfigure SSO in Asana, access hello workspace settings by clicking hello workspace name on hello top right corner of hello screen.</span></span> <span data-ttu-id="6d174-168">然後，按一下 [\<您的工作區名稱\> 設定]。</span><span class="sxs-lookup"><span data-stu-id="6d174-168">Then, click on **\<your workspace name\> Settings**.</span></span> 
   
    ![Asana sso 設定](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. <span data-ttu-id="6d174-170">在 hello**組織設定**視窗中，按一下 **管理**。</span><span class="sxs-lookup"><span data-stu-id="6d174-170">On hello **Organization settings** window, click **Administration**.</span></span> <span data-ttu-id="6d174-171">然後，按一下 **成員必須透過 SAML 登入**tooenable hello SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="6d174-171">Then, click **Members must log in via SAML** tooenable hello SSO configuration.</span></span> <span data-ttu-id="6d174-172">hello 執行 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6d174-172">hello perform hello following steps:</span></span>
   
    ![設定單一登入組織設定](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     <span data-ttu-id="6d174-174">a.</span><span class="sxs-lookup"><span data-stu-id="6d174-174">a.</span></span> <span data-ttu-id="6d174-175">在 hello**登入頁面 URL**文字方塊中，貼上 hello **SAML 單一登入服務 URL**。</span><span class="sxs-lookup"><span data-stu-id="6d174-175">In hello **Sign-in page URL** textbox, paste hello **SAML Single Sign-On Service URL**.</span></span>

     <span data-ttu-id="6d174-176">b.</span><span class="sxs-lookup"><span data-stu-id="6d174-176">b.</span></span> <span data-ttu-id="6d174-177">從 Azure 入口網站下載的 hello 憑證上按一下滑鼠右鍵，然後開啟 hello 憑證檔案，使用 [記事本] 或您慣用的文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="6d174-177">Right click hello certificate downloaded from Azure portal, then open hello certificate file using Notepad or your preferred text editor.</span></span> <span data-ttu-id="6d174-178">Hello 之間複製 hello 內容開始和 hello 結束憑證標題並將它貼在 hello **X.509 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="6d174-178">Copy hello content between hello begin and hello end certificate title and paste it in hello **X.509 Certificate** textbox.</span></span>

9. <span data-ttu-id="6d174-179">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="6d174-179">Click **Save**.</span></span> <span data-ttu-id="6d174-180">跳過[Asana 指南來設定 SSO](https://asana.com/guide/help/premium/authentication#gl-saml)如果您需要進一步協助。</span><span class="sxs-lookup"><span data-stu-id="6d174-180">Go too[Asana guide for setting up SSO](https://asana.com/guide/help/premium/authentication#gl-saml) if you need further assistance.</span></span>

> [!TIP]
> <span data-ttu-id="6d174-181">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="6d174-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6d174-182">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="6d174-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6d174-183">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6d174-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6d174-184">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6d174-184">Create an Azure AD test user</span></span>

<span data-ttu-id="6d174-185">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="6d174-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 測試使用者][100]

<span data-ttu-id="6d174-187">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6d174-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d174-188">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="6d174-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6d174-190">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="6d174-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6d174-192">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="6d174-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6d174-194">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6d174-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![hello [新增] 按鈕](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6d174-196">a.</span><span class="sxs-lookup"><span data-stu-id="6d174-196">a.</span></span> <span data-ttu-id="6d174-197">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="6d174-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6d174-198">b.</span><span class="sxs-lookup"><span data-stu-id="6d174-198">b.</span></span> <span data-ttu-id="6d174-199">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="6d174-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6d174-200">c.</span><span class="sxs-lookup"><span data-stu-id="6d174-200">c.</span></span> <span data-ttu-id="6d174-201">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="6d174-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6d174-202">d.</span><span class="sxs-lookup"><span data-stu-id="6d174-202">d.</span></span> <span data-ttu-id="6d174-203">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6d174-203">Click **Create**.</span></span>
 
### <a name="create-an-asana-test-user"></a><span data-ttu-id="6d174-204">建立 Asana 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6d174-204">Create an Asana test user</span></span>

<span data-ttu-id="6d174-205">在本節中，您要在 Asana 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="6d174-205">In this section, you create a user called Britta Simon in Asana.</span></span>

1. <span data-ttu-id="6d174-206">在**Asana**，go toohello**小組**hello 左面板上的一節。</span><span class="sxs-lookup"><span data-stu-id="6d174-206">On **Asana**, go toohello **Teams** section on hello left panel.</span></span> <span data-ttu-id="6d174-207">按一下 hello 加上簽章 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6d174-207">Click hello plus sign button.</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. <span data-ttu-id="6d174-209">輸入 hello 電子郵件britta.simon@contoso.com在 hello 文字方塊中，然後選取 **邀請**。</span><span class="sxs-lookup"><span data-stu-id="6d174-209">Type hello email britta.simon@contoso.com in hello text box and then select **Invite**.</span></span>

3. <span data-ttu-id="6d174-210">按一下 [傳送邀請] 。</span><span class="sxs-lookup"><span data-stu-id="6d174-210">Click **Send Invite**.</span></span> <span data-ttu-id="6d174-211">hello 新使用者會收到一封電子郵件到其電子郵件帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d174-211">hello new user will receive an email into her email account.</span></span> <span data-ttu-id="6d174-212">她將需要 toocreate 並驗證 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d174-212">She will need toocreate and validate hello account.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6d174-213">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6d174-213">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6d174-214">在本節中，您可以授與存取 tooAsana 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6d174-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAsana.</span></span>

![指派 hello 使用者角色][200]

<span data-ttu-id="6d174-216">**tooassign 許 Simon tooAsana，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6d174-216">**tooassign Britta Simon tooAsana, perform hello following steps:**</span></span>

1. <span data-ttu-id="6d174-217">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6d174-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="6d174-219">在 [hello] 應用程式清單中，選取**Asana**。</span><span class="sxs-lookup"><span data-stu-id="6d174-219">In hello applications list, select **Asana**.</span></span>

    ![hello 應用程式清單中的 hello Asana 連結](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. <span data-ttu-id="6d174-221">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="6d174-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="6d174-223">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6d174-223">Click **Add** button.</span></span> <span data-ttu-id="6d174-224">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6d174-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="6d174-226">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="6d174-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6d174-227">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6d174-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6d174-228">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6d174-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6d174-229">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="6d174-229">Test single sign-on</span></span>

<span data-ttu-id="6d174-230">本節目標 hello tootest 是您 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6d174-230">hello objective of this section is tootest your Azure AD single sign-on.</span></span>

<span data-ttu-id="6d174-231">移至 tooAsana 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="6d174-231">Go tooAsana login page.</span></span> <span data-ttu-id="6d174-232">在 hello 電子郵件地址 文字方塊中，插入 hello 電子郵件地址britta.simon@contoso.com。Hello 密碼文字方塊保留空白中，然後按**登入**。</span><span class="sxs-lookup"><span data-stu-id="6d174-232">In hello Email address textbox, insert hello email address britta.simon@contoso.com. Leave hello password textbox in blank and then click **Log In**.</span></span> <span data-ttu-id="6d174-233">您將會重新導向的 tooAzure AD 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="6d174-233">You will be redirected tooAzure AD login page.</span></span> <span data-ttu-id="6d174-234">完成您的 Azure AD 認證。</span><span class="sxs-lookup"><span data-stu-id="6d174-234">Complete your Azure AD credentials.</span></span> <span data-ttu-id="6d174-235">現在，您已在 Asana 上登入。</span><span class="sxs-lookup"><span data-stu-id="6d174-235">Now, you are logged in on Asana.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6d174-236">其他資源</span><span class="sxs-lookup"><span data-stu-id="6d174-236">Additional resources</span></span>

* [<span data-ttu-id="6d174-237">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6d174-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6d174-238">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="6d174-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png

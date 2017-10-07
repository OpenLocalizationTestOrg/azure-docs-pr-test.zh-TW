---
title: "教學課程：Azure Active Directory 與 Infor Retail – Information Management 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與這些零售 – 資訊管理之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ff49168-ef81-4169-8e5e-dc86e24dd5e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 9cd8ab65d41d01832e0611f7f8254aa257120508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-infor-retail--information-management"></a><span data-ttu-id="a356b-103">教學課程：Azure Active Directory 與 Infor Retail – Information Management 整合</span><span class="sxs-lookup"><span data-stu-id="a356b-103">Tutorial: Azure Active Directory integration with Infor Retail – Information Management</span></span>

<span data-ttu-id="a356b-104">在此教學課程中，您學會如何 toointegrate 資訊零售 – 資訊管理與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="a356b-104">In this tutorial, you learn how toointegrate Infor Retail – Information Management with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a356b-105">整合這些零售 – 資訊管理與 Azure AD 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="a356b-105">Integrating Infor Retail – Information Management with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a356b-106">您可以控制存取 tooInfor 零售 – 資訊管理 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="a356b-106">You can control in Azure AD who has access tooInfor Retail – Information Management.</span></span>
- <span data-ttu-id="a356b-107">您可以啟用您的使用者 tooautomatically get 登入 tooInfor 零售 – 使用其 Azure AD 帳戶的資訊管理 （單一登入）。</span><span class="sxs-lookup"><span data-stu-id="a356b-107">You can enable your users tooautomatically get signed-on tooInfor Retail – Information Management (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a356b-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="a356b-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="a356b-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a356b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a356b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a356b-110">Prerequisites</span></span>

<span data-ttu-id="a356b-111">tooconfigure 資訊零售 – 資訊管理與 Azure AD 整合您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="a356b-111">tooconfigure Azure AD integration with Infor Retail – Information Management, you need hello following items:</span></span>

- <span data-ttu-id="a356b-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a356b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a356b-113">已啟用 Infor Retail – Information Management 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a356b-113">An Infor Retail – Information Management single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a356b-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="a356b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a356b-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="a356b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a356b-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a356b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a356b-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="a356b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a356b-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="a356b-118">Scenario description</span></span>
<span data-ttu-id="a356b-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a356b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a356b-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="a356b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a356b-121">新增這些零售 – 從 hello 組件庫的資訊管理</span><span class="sxs-lookup"><span data-stu-id="a356b-121">Adding Infor Retail – Information Management from hello gallery</span></span>
2. <span data-ttu-id="a356b-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a356b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-infor-retail--information-management-from-hello-gallery"></a><span data-ttu-id="a356b-123">新增這些零售 – 從 hello 組件庫的資訊管理</span><span class="sxs-lookup"><span data-stu-id="a356b-123">Adding Infor Retail – Information Management from hello gallery</span></span>
<span data-ttu-id="a356b-124">tooconfigure hello 整合的資訊零售 – 資訊管理到 Azure AD，您需要 tooadd 資訊零售 – hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式的資訊管理。</span><span class="sxs-lookup"><span data-stu-id="a356b-124">tooconfigure hello integration of Infor Retail – Information Management into Azure AD, you need tooadd Infor Retail – Information Management from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a356b-125">**tooadd 資訊零售 – hello 庫、 資訊管理執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a356b-125">**tooadd Infor Retail – Information Management from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a356b-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a356b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="a356b-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a356b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a356b-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a356b-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="a356b-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a356b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="a356b-133">在 hello 搜尋方塊中，輸入**資訊零售 – 資訊管理**，選取**資訊零售 – 資訊管理**然後按一下 從結果面板**新增**按鈕 tooadd hello應用程式。</span><span class="sxs-lookup"><span data-stu-id="a356b-133">In hello search box, type **Infor Retail – Information Management**, select **Infor Retail – Information Management** from result panel then click **Add** button tooadd hello application.</span></span>

    ![這些零售 – hello [結果] 清單中的資訊管理](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a356b-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a356b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a356b-136">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Infor Retail – Information Management 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a356b-136">In this section, you configure and test Azure AD single sign-on with Infor Retail – Information Management based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a356b-137">針對單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在這些零售-資訊管理是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="a356b-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Infor Retail – Information Management is tooa user in Azure AD.</span></span> <span data-ttu-id="a356b-138">換句話說，Azure AD 使用者與 hello 資訊零售 – 資訊管理相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="a356b-138">In other words, a link relationship between an Azure AD user and hello related user in Infor Retail – Information Management needs toobe established.</span></span>

<span data-ttu-id="a356b-139">在這些零售 – Information Management 指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="a356b-139">In Infor Retail – Information Management, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a356b-140">tooconfigure 和測試 Azure AD 單一登入資訊零售 – 資訊管理與您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="a356b-140">tooconfigure and test Azure AD single sign-on with Infor Retail – Information Management, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a356b-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="a356b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a356b-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="a356b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a356b-143">**[建立這些零售 – 資訊管理測試使用者](#create-an-infor-retail--information-management-test-user)** -toohave 許 Simon 資訊零售中對應項目 – 是表示連結的 toohello Azure AD 使用者的資訊管理。</span><span class="sxs-lookup"><span data-stu-id="a356b-143">**[Create an Infor Retail – Information Management test user](#create-an-infor-retail--information-management-test-user)** - toohave a counterpart of Britta Simon in Infor Retail – Information Management that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a356b-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a356b-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a356b-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="a356b-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a356b-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a356b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a356b-147">在本節中，您要啟用 Azure AD 單一登入 hello Azure 入口網站中，並在您的資訊零售 – 資訊管理應用程式設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="a356b-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Infor Retail – Information Management application.</span></span>

<span data-ttu-id="a356b-148">**這些零售 – 資訊管理與 Azure AD 單一登入 tooconfigure 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a356b-148">**tooconfigure Azure AD single sign-on with Infor Retail – Information Management, perform hello following steps:**</span></span>

1. <span data-ttu-id="a356b-149">在 Azure 入口網站上 hello hello**資訊零售 – 資訊管理**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="a356b-149">In hello Azure portal, on hello **Infor Retail – Information Management** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="a356b-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a356b-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_samlbase.png)

3. <span data-ttu-id="a356b-153">在 hello**資訊零售 – 資訊管理網域和 Url**區段中，執行下列步驟，如果您想在 IDP tooconfigure hello 應用程式起始模式 hello:</span><span class="sxs-lookup"><span data-stu-id="a356b-153">On hello **Infor Retail – Information Management Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in IDP initiated mode:</span></span>

    ![Infor Retail – Information Management 網域與 URL 單一登入資訊 IDP](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_url.png)

    <span data-ttu-id="a356b-155">a.</span><span class="sxs-lookup"><span data-stu-id="a356b-155">a.</span></span> <span data-ttu-id="a356b-156">在 hello**識別碼**文字方塊中，輸入 URL，使用下列的 hello 模式：</span><span class="sxs-lookup"><span data-stu-id="a356b-156">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
    |   |
    | -- |
    | `https://<company name>.mingle.infor.com` |
    | `http://<company name>.mingledev.infor.com` |

    <span data-ttu-id="a356b-157">b.</span><span class="sxs-lookup"><span data-stu-id="a356b-157">b.</span></span> <span data-ttu-id="a356b-158">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.mingle.infor.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="a356b-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.mingle.infor.com/sp/ACS.saml2`</span></span>

4. <span data-ttu-id="a356b-159">請檢查**顯示進階的 URL 設定**並執行下列步驟，如果您想 tooconfigure hello 應用程式中的 hello **SP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="a356b-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Infor Retail – Information Management 網域與 URL 單一登入資訊 SP](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_url1.png)

    <span data-ttu-id="a356b-161">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.mingle.infor.com/<company code>`</span><span class="sxs-lookup"><span data-stu-id="a356b-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.mingle.infor.com/<company code>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="a356b-162">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="a356b-162">These values are not real.</span></span> <span data-ttu-id="a356b-163">更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="a356b-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="a356b-164">請連絡[資訊零售 – 資訊管理用戶端支援小組](mailto:innovate@infor.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="a356b-164">Contact [Infor Retail – Information Management Client support team](mailto:innovate@infor.com) tooget these values.</span></span> 

5. <span data-ttu-id="a356b-165">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="a356b-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_certificate.png) 

6. <span data-ttu-id="a356b-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a356b-167">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="a356b-169">tooconfigure 單一登入上**資訊零售 – 資訊管理**端，您需要下載 toosend hello**中繼資料 XML**太[資訊零售 – 資訊管理支援小組](mailto:innovate@infor.com).</span><span class="sxs-lookup"><span data-stu-id="a356b-169">tooconfigure single sign-on on **Infor Retail – Information Management** side, you need toosend hello downloaded **Metadata XML** too[Infor Retail – Information Management support team](mailto:innovate@infor.com).</span></span> <span data-ttu-id="a356b-170">設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。</span><span class="sxs-lookup"><span data-stu-id="a356b-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a356b-171">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="a356b-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a356b-172">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="a356b-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a356b-173">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a356b-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a356b-174">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a356b-174">Create an Azure AD test user</span></span>

<span data-ttu-id="a356b-175">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a356b-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="a356b-177">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a356b-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a356b-178">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a356b-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a356b-180">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="a356b-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a356b-182">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a356b-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a356b-184">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a356b-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-inforretailinformationmanagement-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a356b-186">a.</span><span class="sxs-lookup"><span data-stu-id="a356b-186">a.</span></span> <span data-ttu-id="a356b-187">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="a356b-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a356b-188">b.</span><span class="sxs-lookup"><span data-stu-id="a356b-188">b.</span></span> <span data-ttu-id="a356b-189">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="a356b-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="a356b-190">c.</span><span class="sxs-lookup"><span data-stu-id="a356b-190">c.</span></span> <span data-ttu-id="a356b-191">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="a356b-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="a356b-192">d.</span><span class="sxs-lookup"><span data-stu-id="a356b-192">d.</span></span> <span data-ttu-id="a356b-193">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a356b-193">Click **Create**.</span></span>
 
### <a name="create-an-infor-retail--information-management-test-user"></a><span data-ttu-id="a356b-194">建立 Infor Retail – Information Management 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a356b-194">Create an Infor Retail – Information Management test user</span></span>

<span data-ttu-id="a356b-195">在本節中，您要在 Infor Retail – Information Management 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="a356b-195">In this section, you create a user called Britta Simon in Infor Retail – Information Management.</span></span> <span data-ttu-id="a356b-196">請使用[資訊零售 – 資訊管理支援小組](mailto:innovate@infor.com)tooadd hello hello 資訊零售 – 資訊管理平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="a356b-196">Please work with [Infor Retail – Information Management support team](mailto:innovate@infor.com) tooadd hello users in hello Infor Retail – Information Management platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a356b-197">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a356b-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="a356b-198">本節中，您可以授與存取 tooInfor 零售 – 資訊管理啟用了許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a356b-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInfor Retail – Information Management.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="a356b-200">**tooassign 許 Simon tooInfor 零售 – 資訊管理執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a356b-200">**tooassign Britta Simon tooInfor Retail – Information Management, perform hello following steps:**</span></span>

1. <span data-ttu-id="a356b-201">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a356b-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="a356b-203">在 [hello] 應用程式清單中，選取**資訊零售 – 資訊管理**。</span><span class="sxs-lookup"><span data-stu-id="a356b-203">In hello applications list, select **Infor Retail – Information Management**.</span></span>

    ![hello 應用程式清單中的 hello 資訊零售 – 資訊管理連結](./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_inforretailinformationmanagement_app.png)  

3. <span data-ttu-id="a356b-205">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="a356b-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="a356b-207">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a356b-207">Click **Add** button.</span></span> <span data-ttu-id="a356b-208">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a356b-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="a356b-210">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="a356b-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a356b-211">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a356b-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a356b-212">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a356b-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a356b-213">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="a356b-213">Test single sign-on</span></span>

<span data-ttu-id="a356b-214">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="a356b-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a356b-215">當您按一下 hello 資訊零售 – hello 存取面板中的資訊管理圖格時，您應該取得自動登入 tooyour 資訊零售 – 資訊管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="a356b-215">When you click hello Infor Retail – Information Management tile in hello Access Panel, you should get automatically signed-on tooyour Infor Retail – Information Management application.</span></span>
<span data-ttu-id="a356b-216">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="a356b-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a356b-217">其他資源</span><span class="sxs-lookup"><span data-stu-id="a356b-217">Additional resources</span></span>

* [<span data-ttu-id="a356b-218">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a356b-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a356b-219">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a356b-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inforretailinformationmanagement-tutorial/tutorial_general_203.png


---
title: "教學課程：Azure Active Directory 與 Autotask Workplace 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 之間 Autotask 工作地點。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 7f820f24e8e9493fa2e1c075f2ef61d7eaa84f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a><span data-ttu-id="79f5e-103">教學課程：Azure Active Directory 與 Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="79f5e-103">Tutorial: Azure Active Directory integration with Autotask Workplace</span></span>

<span data-ttu-id="79f5e-104">在此教學課程中，您學會如何 toointegrate Autotask 與 Azure Active Directory (Azure AD) 的工作場所。</span><span class="sxs-lookup"><span data-stu-id="79f5e-104">In this tutorial, you learn how toointegrate Autotask Workplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79f5e-105">與 Azure AD 整合 Autotask 工作地點可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="79f5e-105">Integrating Autotask Workplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="79f5e-106">您可以控制存取 tooAutotask 工作地點的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="79f5e-106">You can control in Azure AD who has access tooAutotask Workplace</span></span>
- <span data-ttu-id="79f5e-107">您可以啟用您的使用者 tooautomatically get 登入 tooAutotask （單一登入） 的工作地點使用其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="79f5e-107">You can enable your users tooautomatically get signed-on tooAutotask Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79f5e-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="79f5e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="79f5e-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="79f5e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79f5e-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="79f5e-110">Prerequisites</span></span>

<span data-ttu-id="79f5e-111">tooconfigure Autotask 工作場所的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="79f5e-111">tooconfigure Azure AD integration with Autotask Workplace, you need hello following items:</span></span>

- <span data-ttu-id="79f5e-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="79f5e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="79f5e-113">已啟用 Autotask Workplace 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="79f5e-113">An Autotask Workplace single-sign on enabled subscription</span></span>
- <span data-ttu-id="79f5e-114">您必須是工作地點的系統管理員或進階系統管理員。</span><span class="sxs-lookup"><span data-stu-id="79f5e-114">You must be an administrator or super administrator in Workplace.</span></span>
- <span data-ttu-id="79f5e-115">Hello Azure AD 中，您必須擁有系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="79f5e-115">You must have an administrator account in hello Azure AD.</span></span>
- <span data-ttu-id="79f5e-116">會利用這項功能的 hello 使用者必須具有內工作地點和 hello Azure AD 的帳戶，而且兩個電子郵件地址必須相符。</span><span class="sxs-lookup"><span data-stu-id="79f5e-116">hello users that will utilize this feature must have accounts within Workplace and hello Azure AD, and their email addresses for both must match.</span></span>

> [!NOTE]
> <span data-ttu-id="79f5e-117">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="79f5e-117">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79f5e-118">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="79f5e-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79f5e-119">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="79f5e-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79f5e-120">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="79f5e-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79f5e-121">案例描述</span><span class="sxs-lookup"><span data-stu-id="79f5e-121">Scenario description</span></span>
<span data-ttu-id="79f5e-122">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="79f5e-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79f5e-123">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="79f5e-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79f5e-124">Autotask 工作地點加入從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="79f5e-124">Adding Autotask Workplace from hello gallery</span></span>
2. <span data-ttu-id="79f5e-125">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="79f5e-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-autotask-workplace-from-hello-gallery"></a><span data-ttu-id="79f5e-126">Autotask 工作地點加入從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="79f5e-126">Adding Autotask Workplace from hello gallery</span></span>
<span data-ttu-id="79f5e-127">tooconfigure hello 整合 Autotask 工作區到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Autotask 工作地點。</span><span class="sxs-lookup"><span data-stu-id="79f5e-127">tooconfigure hello integration of Autotask Workplace into Azure AD, you need tooadd Autotask Workplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="79f5e-128">**tooadd Autotask 工作場所 hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="79f5e-128">**tooadd Autotask Workplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="79f5e-129">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="79f5e-129">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory] 按鈕][1]

2. <span data-ttu-id="79f5e-131">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="79f5e-131">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="79f5e-132">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="79f5e-132">Then go too**All applications**.</span></span>

    ![hello 企業應用程式] 刀鋒視窗][2]
    
3. <span data-ttu-id="79f5e-134">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="79f5e-134">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="79f5e-136">在 hello 搜尋方塊中，輸入**Autotask 工作場所**，選取**Autotask 工作場所**然後按一下 [從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="79f5e-136">In hello search box, type **Autotask Workplace**, select  **Autotask Workplace**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Autotask 工作場所中 hello 結果清單](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="79f5e-138">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="79f5e-138">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="79f5e-139">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Autotask Workplace 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="79f5e-139">In this section, you configure and test Azure AD single sign-on with Autotask Workplace based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="79f5e-140">單一登入 toowork，Azure AD 需要 tooknow Autotask 工作地點中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="79f5e-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Autotask Workplace is tooa user in Azure AD.</span></span> <span data-ttu-id="79f5e-141">換句話說，Azure AD 使用者與 hello Autotask 工作地點中的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="79f5e-141">In other words, a link relationship between an Azure AD user and hello related user in Autotask Workplace needs toobe established.</span></span>

<span data-ttu-id="79f5e-142">Autotask 工作地點中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="79f5e-142">In Autotask Workplace, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="79f5e-143">tooconfigure 和測試 Azure AD 單一登入的 Autotask 工作地點網路，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="79f5e-143">tooconfigure and test Azure AD single sign-on with Autotask Workplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="79f5e-144">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="79f5e-144">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="79f5e-145">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="79f5e-145">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79f5e-146">**[建立 Autotask 工作地點的測試使用者](#create-an-autotask-workplace-test-user)** -toohave 許 Simon Autotask 工作地點所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="79f5e-146">**[Create an Autotask Workplace test user](#create-an-autotask-workplace-test-user)** - toohave a counterpart of Britta Simon in Autotask Workplace that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="79f5e-147">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="79f5e-147">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79f5e-148">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="79f5e-148">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="79f5e-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="79f5e-149">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="79f5e-150">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Autotask 工作場所應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="79f5e-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Autotask Workplace application.</span></span>

<span data-ttu-id="79f5e-151">**tooconfigure Azure AD 單一登入的 Autotask 工作地點網路，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="79f5e-151">**tooconfigure Azure AD single sign-on with Autotask Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="79f5e-152">在 Azure 入口網站上 hello hello **Autotask 工作場所**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="79f5e-152">In hello Azure portal, on hello **Autotask Workplace** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="79f5e-154">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="79f5e-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

3. <span data-ttu-id="79f5e-156">如果您想 tooconfigure hello 應用程式中的**IDP**起始模式中，執行下列步驟在 hello hello **Autotask 工作場所網域和 Url** > 一節：</span><span class="sxs-lookup"><span data-stu-id="79f5e-156">If you wish tooconfigure hello application in **IDP** initiated mode, perform hello following steps on hello **Autotask Workplace Domain and URLs** section:</span></span>

    ![IDP 的 Autotask Workplace 網域和 URL 單一登入資訊](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    <span data-ttu-id="79f5e-158">a.</span><span class="sxs-lookup"><span data-stu-id="79f5e-158">a.</span></span> <span data-ttu-id="79f5e-159">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="79f5e-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span></span>

    <span data-ttu-id="79f5e-160">b.</span><span class="sxs-lookup"><span data-stu-id="79f5e-160">b.</span></span> <span data-ttu-id="79f5e-161">在 [hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="79f5e-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span></span>

4. <span data-ttu-id="79f5e-162">如果您想 tooconfigure hello 應用程式中的**SP**初始的模式中，核取**顯示進階的 URL 設定**並執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="79f5e-162">If you wish tooconfigure hello application in **SP** initiated mode, check **Show advanced URL settings** and perform hello following steps:</span></span>

    ![SP 的 Autotask Workplace 網域和 URL 單一登入資訊](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    <span data-ttu-id="79f5e-164">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.awp.autotask.net/loginsso`</span><span class="sxs-lookup"><span data-stu-id="79f5e-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/loginsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="79f5e-165">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="79f5e-165">These values are not real.</span></span> <span data-ttu-id="79f5e-166">更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="79f5e-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="79f5e-167">請連絡[Autotask 工作地點的用戶端支援小組](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="79f5e-167">Contact [Autotask Workplace Client support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget these values.</span></span> 

5. <span data-ttu-id="79f5e-168">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="79f5e-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

6. <span data-ttu-id="79f5e-170">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="79f5e-170">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="79f5e-172">在不同的網頁瀏覽器視窗中，tooWorkplace 線上使用登入 hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="79f5e-172">In a different web browser window, Log in tooWorkplace Online using hello administrator credentials.</span></span>

    >[!Note]
    ><span data-ttu-id="79f5e-173">當設定 hello IdP，子網域必須 toobe 指定。</span><span class="sxs-lookup"><span data-stu-id="79f5e-173">When configuring hello IdP, a subdomain will need toobe specified.</span></span> <span data-ttu-id="79f5e-174">tooconfirm hello 正確子網域，登入 tooWorkplace 線上。</span><span class="sxs-lookup"><span data-stu-id="79f5e-174">tooconfirm hello correct subdomain, login tooWorkplace Online.</span></span> <span data-ttu-id="79f5e-175">登入之後，請注意 toohello 子網域 hello URL 中。</span><span class="sxs-lookup"><span data-stu-id="79f5e-175">Once logged in, make note toohello subdomain in hello URL.</span></span>
    ><span data-ttu-id="79f5e-176">hello 子網域屬於 hello hello"https://"和".awp.autotask.net/ 」 之間，而且應該是我們、 eu、 ca 或 au 登錄。</span><span class="sxs-lookup"><span data-stu-id="79f5e-176">hello subdomain is hello part between hello “https://“ and “.awp.autotask.net/“ and should be us, eu, ca, or au.</span></span>

8. <span data-ttu-id="79f5e-177">跳過**組態** > **單一登入**並執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="79f5e-177">Go too**Configuration** > **Single Sign-On** and perform hello following steps:</span></span>

    ![Autotask 單一登入組態](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    <span data-ttu-id="79f5e-179">a.</span><span class="sxs-lookup"><span data-stu-id="79f5e-179">a.</span></span> <span data-ttu-id="79f5e-180">選取 hello **XML 中繼資料檔**選項，然後再上傳 hello**中繼資料 XML**從 Azure 入口網站下載。</span><span class="sxs-lookup"><span data-stu-id="79f5e-180">Select hello **XML Metadata File** option, and then upload hello **Metadata XML** downloaded from Azure portal.</span></span>

    <span data-ttu-id="79f5e-181">b.</span><span class="sxs-lookup"><span data-stu-id="79f5e-181">b.</span></span> <span data-ttu-id="79f5e-182">按一下 [啟用 SSO]。</span><span class="sxs-lookup"><span data-stu-id="79f5e-182">Click **Enable SSO**.</span></span>
    
    ![Autotask 單一登入核准組態](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    <span data-ttu-id="79f5e-184">c.</span><span class="sxs-lookup"><span data-stu-id="79f5e-184">c.</span></span> <span data-ttu-id="79f5e-185">選取 hello**我確認這項資訊是否正確，以及我信任此 IdP**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="79f5e-185">Select hello **I confirm this information is correct and I trust this IdP** check box.</span></span>

    <span data-ttu-id="79f5e-186">d.</span><span class="sxs-lookup"><span data-stu-id="79f5e-186">d.</span></span> <span data-ttu-id="79f5e-187">按一下 [核准]。</span><span class="sxs-lookup"><span data-stu-id="79f5e-187">Click **Approve**.</span></span>
     
>[!Note]
><span data-ttu-id="79f5e-188">如果您需要設定 Autotask 工作地點的協助，請參閱[本頁](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm)tooget 協助您工作場所帳戶。</span><span class="sxs-lookup"><span data-stu-id="79f5e-188">If you require assistance with configuring Autotask Workplace, please see [this page](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget assistance with your Workplace account.</span></span>

> [!TIP]
> <span data-ttu-id="79f5e-189">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="79f5e-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="79f5e-190">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="79f5e-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="79f5e-191">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="79f5e-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="79f5e-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="79f5e-192">Create an Azure AD test user</span></span>

<span data-ttu-id="79f5e-193">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="79f5e-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="79f5e-195">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="79f5e-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="79f5e-196">在 [hello Azure 入口網站，hello 左窗格中，按一下 [hello **Azure Active Directory** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="79f5e-196">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory] 按鈕](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="79f5e-198">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下 [**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="79f5e-198">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="79f5e-200">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="79f5e-200">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="79f5e-202">在 [hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="79f5e-202">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="79f5e-204">a.</span><span class="sxs-lookup"><span data-stu-id="79f5e-204">a.</span></span> <span data-ttu-id="79f5e-205">在 [hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="79f5e-205">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79f5e-206">b.</span><span class="sxs-lookup"><span data-stu-id="79f5e-206">b.</span></span> <span data-ttu-id="79f5e-207">在 [hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="79f5e-207">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="79f5e-208">c.</span><span class="sxs-lookup"><span data-stu-id="79f5e-208">c.</span></span> <span data-ttu-id="79f5e-209">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 [hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="79f5e-209">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="79f5e-210">d.</span><span class="sxs-lookup"><span data-stu-id="79f5e-210">d.</span></span> <span data-ttu-id="79f5e-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="79f5e-211">Click **Create**.</span></span>

### <a name="create-an-autotask-workplace-test-user"></a><span data-ttu-id="79f5e-212">建立 Autotask Workplace 測試使用者</span><span class="sxs-lookup"><span data-stu-id="79f5e-212">Create an Autotask Workplace test user</span></span>

<span data-ttu-id="79f5e-213">在本節中，您會在 Autotask 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="79f5e-213">In this section, you create a user called Britta Simon in Autotask.</span></span> <span data-ttu-id="79f5e-214">請使用[Autotask 工作場所支援小組](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm)tooadd hello hello Autotask 工作場所平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="79f5e-214">Please work with [Autotask Workplace support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooadd hello users in hello Autotask Workplace platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="79f5e-215">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="79f5e-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="79f5e-216">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooAutotask 工作地點。</span><span class="sxs-lookup"><span data-stu-id="79f5e-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAutotask Workplace.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="79f5e-218">**tooassign 許 Simon tooAutotask 工作地點，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="79f5e-218">**tooassign Britta Simon tooAutotask Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="79f5e-219">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="79f5e-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="79f5e-221">在 [hello] 應用程式清單中，選取**Autotask 工作場所**。</span><span class="sxs-lookup"><span data-stu-id="79f5e-221">In hello applications list, select **Autotask Workplace**.</span></span>

    ![hello Autotask 工作場所 hello 應用程式清單中的連結](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

3. <span data-ttu-id="79f5e-223">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="79f5e-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="79f5e-225">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="79f5e-225">Click **Add** button.</span></span> <span data-ttu-id="79f5e-226">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="79f5e-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="79f5e-228">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="79f5e-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="79f5e-229">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="79f5e-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79f5e-230">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="79f5e-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="79f5e-231">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="79f5e-231">Test single sign-on</span></span>

<span data-ttu-id="79f5e-232">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="79f5e-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="79f5e-233">當您按一下的 hello Autotask 工作場所磚 hello 存取面板中時，您應該取得自動登入 tooyour Autotask 工作場所應用程式。</span><span class="sxs-lookup"><span data-stu-id="79f5e-233">When you click hello Autotask Workplace tile in hello Access Panel, you should get automatically signed-on tooyour Autotask Workplace application.</span></span>
<span data-ttu-id="79f5e-234">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="79f5e-234">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="79f5e-235">其他資源</span><span class="sxs-lookup"><span data-stu-id="79f5e-235">Additional resources</span></span>

* [<span data-ttu-id="79f5e-236">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79f5e-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79f5e-237">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="79f5e-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png


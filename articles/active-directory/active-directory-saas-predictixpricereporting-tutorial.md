---
title: "教學課程：Azure Active Directory 與 Predictix Price Reporting 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Predictix 價格 Reporting 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 691d0c43-3aa1-4220-9e46-e7a88db234ad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: c2ba85f613f5a71de72278a0d1916c135b835b60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-price-reporting"></a><span data-ttu-id="84735-103">教學課程：Azure Active Directory 與 Predictix Price Reporting 整合</span><span class="sxs-lookup"><span data-stu-id="84735-103">Tutorial: Azure Active Directory integration with Predictix Price Reporting</span></span>

<span data-ttu-id="84735-104">在此教學課程中，您學會如何 toointegrate Predictix 價格 Reporting 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="84735-104">In this tutorial, you learn how toointegrate Predictix Price Reporting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="84735-105">Azure AD 整合 Predictix 價格 Reporting 可以提供下列優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="84735-105">Integrating Predictix Price Reporting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="84735-106">您可以控制存取 tooPredictix 價格報告 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="84735-106">You can control in Azure AD who has access tooPredictix Price Reporting.</span></span>
- <span data-ttu-id="84735-107">您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooPredictix 價格 Reporting （單一登入）。</span><span class="sxs-lookup"><span data-stu-id="84735-107">You can enable your users tooautomatically get signed-on tooPredictix Price Reporting (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="84735-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="84735-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="84735-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="84735-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84735-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="84735-110">Prerequisites</span></span>

<span data-ttu-id="84735-111">tooconfigure 與 Predictix 價格 Reporting 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="84735-111">tooconfigure Azure AD integration with Predictix Price Reporting, you need hello following items:</span></span>

- <span data-ttu-id="84735-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="84735-112">An Azure AD subscription</span></span>
- <span data-ttu-id="84735-113">啟用 Predictix Price Reporting 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="84735-113">A Predictix Price Reporting single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="84735-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="84735-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="84735-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="84735-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="84735-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="84735-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="84735-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="84735-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="84735-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="84735-118">Scenario description</span></span>
<span data-ttu-id="84735-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="84735-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="84735-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="84735-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="84735-121">從 hello 組件庫中加入 Predictix 價格報告</span><span class="sxs-lookup"><span data-stu-id="84735-121">Adding Predictix Price Reporting from hello gallery</span></span>
2. <span data-ttu-id="84735-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="84735-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-predictix-price-reporting-from-hello-gallery"></a><span data-ttu-id="84735-123">從 hello 組件庫中加入 Predictix 價格報告</span><span class="sxs-lookup"><span data-stu-id="84735-123">Adding Predictix Price Reporting from hello gallery</span></span>
<span data-ttu-id="84735-124">tooconfigure hello 整合 Predictix 價格報告到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Predictix 價格報告。</span><span class="sxs-lookup"><span data-stu-id="84735-124">tooconfigure hello integration of Predictix Price Reporting into Azure AD, you need tooadd Predictix Price Reporting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="84735-125">**tooadd Predictix 價格 Reporting hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="84735-125">**tooadd Predictix Price Reporting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="84735-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="84735-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="84735-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="84735-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="84735-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="84735-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="84735-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="84735-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="84735-133">在 hello 搜尋方塊中，輸入**Predictix 價格 Reporting**，選取**Predictix 價格 Reporting**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="84735-133">In hello search box, type **Predictix Price Reporting**, select **Predictix Price Reporting** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Predictix 價格 Reporting hello [結果] 清單中](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="84735-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="84735-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="84735-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Predictix Price Reporting 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="84735-136">In this section, you configure and test Azure AD single sign-on with Predictix Price Reporting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="84735-137">單一登入 toowork，Azure AD 需要 tooknow Predictix 價格 Reporting 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="84735-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Predictix Price Reporting is tooa user in Azure AD.</span></span> <span data-ttu-id="84735-138">換句話說，Azure AD 使用者與 hello Predictix 價格 Reporting 中的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="84735-138">In other words, a link relationship between an Azure AD user and hello related user in Predictix Price Reporting needs toobe established.</span></span>

<span data-ttu-id="84735-139">Predictix 價格 Reporting 中指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="84735-139">In Predictix Price Reporting, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="84735-140">tooconfigure 及測試 Azure AD 單一登入與 Predictix 價格報告，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="84735-140">tooconfigure and test Azure AD single sign-on with Predictix Price Reporting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="84735-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="84735-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="84735-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="84735-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="84735-143">**[建立測試使用者 Predictix 價格 Reporting](#create-a-predictix-price-reporting-test-user)**  -toohave 許 Simon Predictix 價格 Reporting 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="84735-143">**[Create a Predictix Price Reporting test user](#create-a-predictix-price-reporting-test-user)** - toohave a counterpart of Britta Simon in Predictix Price Reporting that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="84735-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="84735-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="84735-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="84735-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="84735-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="84735-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="84735-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Predictix 價格報告應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="84735-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Predictix Price Reporting application.</span></span>

<span data-ttu-id="84735-148">**tooconfigure Azure AD 單一登入使用 Predictix 價格報告時，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="84735-148">**tooconfigure Azure AD single sign-on with Predictix Price Reporting, perform hello following steps:**</span></span>

1. <span data-ttu-id="84735-149">在 Azure 入口網站上 hello hello **Predictix 價格 Reporting**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="84735-149">In hello Azure portal, on hello **Predictix Price Reporting** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="84735-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="84735-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_samlbase.png)

3. <span data-ttu-id="84735-153">在 hello **Predictix 價格 Reporting 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="84735-153">On hello **Predictix Price Reporting Domain and URLs** section, perform hello following steps:</span></span>

    ![Predictix Price Reporting 網域及 URL 單一登入資訊](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_url.png)

    <span data-ttu-id="84735-155">a.</span><span class="sxs-lookup"><span data-stu-id="84735-155">a.</span></span> <span data-ttu-id="84735-156">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname-pricing>.predictix.com/sso/request`</span><span class="sxs-lookup"><span data-stu-id="84735-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname-pricing>.predictix.com/sso/request`</span></span>

    <span data-ttu-id="84735-157">b.</span><span class="sxs-lookup"><span data-stu-id="84735-157">b.</span></span> <span data-ttu-id="84735-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="84735-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname-pricing>.predictix.com` |
    | `https://<companyname-pricing>.dev.predictix.com` |

    > [!NOTE] 
    > <span data-ttu-id="84735-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="84735-159">These values are not real.</span></span> <span data-ttu-id="84735-160">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="84735-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="84735-161">請連絡[Predictix 價格報告用戶端支援小組](http://www.infor.com/company/customer-center/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="84735-161">Contact [Predictix Price Reporting Client support team](http://www.infor.com/company/customer-center/) tooget these values.</span></span> 
 
4. <span data-ttu-id="84735-162">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="84735-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_certificate.png) 

5. <span data-ttu-id="84735-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="84735-164">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="84735-166">在 hello **Predictix 價格 Reporting 組態**區段中，按一下**設定 Predictix 價格報告**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="84735-166">On hello **Predictix Price Reporting Configuration** section, click **Configure Predictix Price Reporting** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="84735-167">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="84735-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Predictix Price Reporting 設定](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_configure.png) 

7. <span data-ttu-id="84735-169">tooconfigure 單一登入上**Predictix 價格 Reporting**端，您需要下載 toosend hello**憑證 (Base64)**，**登出 URL、 SAML 實體識別碼和 SAML 單一登入服務 URL**太[Predictix 價格 Reporting 支援小組](http://www.infor.com/company/customer-center/)。</span><span class="sxs-lookup"><span data-stu-id="84735-169">tooconfigure single sign-on on **Predictix Price Reporting** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Predictix Price Reporting support team](http://www.infor.com/company/customer-center/).</span></span> <span data-ttu-id="84735-170">設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。</span><span class="sxs-lookup"><span data-stu-id="84735-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="84735-171">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="84735-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="84735-172">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="84735-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="84735-173">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="84735-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="84735-174">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="84735-174">Create an Azure AD test user</span></span>

<span data-ttu-id="84735-175">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="84735-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="84735-177">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="84735-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="84735-178">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="84735-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="84735-180">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="84735-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="84735-182">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="84735-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="84735-184">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="84735-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_04.png)

    <span data-ttu-id="84735-186">a.</span><span class="sxs-lookup"><span data-stu-id="84735-186">a.</span></span> <span data-ttu-id="84735-187">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="84735-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="84735-188">b.</span><span class="sxs-lookup"><span data-stu-id="84735-188">b.</span></span> <span data-ttu-id="84735-189">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="84735-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="84735-190">c.</span><span class="sxs-lookup"><span data-stu-id="84735-190">c.</span></span> <span data-ttu-id="84735-191">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="84735-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="84735-192">d.</span><span class="sxs-lookup"><span data-stu-id="84735-192">d.</span></span> <span data-ttu-id="84735-193">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="84735-193">Click **Create**.</span></span>
 
### <a name="create-a-predictix-price-reporting-test-user"></a><span data-ttu-id="84735-194">建立 Predictix Price Reporting 測試使用者</span><span class="sxs-lookup"><span data-stu-id="84735-194">Create a Predictix Price Reporting test user</span></span>

<span data-ttu-id="84735-195">在本節中，您要在 Predictix Price Reporting 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="84735-195">In this section, you create a user called Britta Simon in Predictix Price Reporting.</span></span> <span data-ttu-id="84735-196">使用[Predictix 價格 Reporting 支援小組](http://www.infor.com/company/customer-center/)tooadd hello hello Predictix 價格報告平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="84735-196">Work with [Predictix Price Reporting support team](http://www.infor.com/company/customer-center/) tooadd hello users in hello Predictix Price Reporting platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="84735-197">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="84735-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="84735-198">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooPredictix 價格報告。</span><span class="sxs-lookup"><span data-stu-id="84735-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPredictix Price Reporting.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="84735-200">**tooassign 許 Simon tooPredictix 價格報告，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="84735-200">**tooassign Britta Simon tooPredictix Price Reporting, perform hello following steps:**</span></span>

1. <span data-ttu-id="84735-201">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="84735-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="84735-203">在 [hello] 應用程式清單中，選取**Predictix 價格 Reporting**。</span><span class="sxs-lookup"><span data-stu-id="84735-203">In hello applications list, select **Predictix Price Reporting**.</span></span>

    ![hello 應用程式清單中的 hello Predictix 價格報告連結](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_app.png)  

3. <span data-ttu-id="84735-205">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="84735-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="84735-207">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="84735-207">Click **Add** button.</span></span> <span data-ttu-id="84735-208">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="84735-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="84735-210">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="84735-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="84735-211">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="84735-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="84735-212">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="84735-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="84735-213">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="84735-213">Test single sign-on</span></span>

<span data-ttu-id="84735-214">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="84735-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="84735-215">當您按一下 hello Predictix 價格 Reporting 並排顯示 hello 存取面板中的時，您應該取得自動登入 tooyour Predictix 價格報告應用程式。</span><span class="sxs-lookup"><span data-stu-id="84735-215">When you click hello Predictix Price Reporting tile in hello Access Panel, you should get automatically signed-on tooyour Predictix Price Reporting application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="84735-216">其他資源</span><span class="sxs-lookup"><span data-stu-id="84735-216">Additional resources</span></span>

* [<span data-ttu-id="84735-217">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="84735-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="84735-218">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="84735-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_203.png


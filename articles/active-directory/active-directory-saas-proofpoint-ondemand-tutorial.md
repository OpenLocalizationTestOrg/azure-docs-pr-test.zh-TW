---
title: "教學課程：Azure Active Directory 與 Proofpoint on Demand 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Proofpoint 視之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 0f9472ddc01f2c18ffc9e8d2b59a17b3b595515e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a><span data-ttu-id="2f05e-103">教學課程：Azure Active Directory 與 Proofpoint on Demand 整合</span><span class="sxs-lookup"><span data-stu-id="2f05e-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span></span>

<span data-ttu-id="2f05e-104">在此教學課程中，您學會如何 toointegrate Proofpoint 視與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="2f05e-104">In this tutorial, you learn how toointegrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f05e-105">與 Azure AD 整合 Proofpoint 視可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="2f05e-105">Integrating Proofpoint on Demand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2f05e-106">您可以控制存取 tooProofpoint 隨 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="2f05e-106">You can control in Azure AD who has access tooProofpoint on Demand</span></span>
- <span data-ttu-id="2f05e-107">您可以啟用您的使用者 tooautomatically get 登入 tooProofpoint 依需求 （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="2f05e-107">You can enable your users tooautomatically get signed-on tooProofpoint on Demand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2f05e-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="2f05e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2f05e-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="2f05e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f05e-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="2f05e-110">Prerequisites</span></span>

<span data-ttu-id="2f05e-111">tooconfigure Azure AD 整合 Proofpoint 依需求，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="2f05e-111">tooconfigure Azure AD integration with Proofpoint on Demand, you need hello following items:</span></span>

- <span data-ttu-id="2f05e-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="2f05e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2f05e-113">啟用 Proofpoint on Demand 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="2f05e-113">A Proofpoint on Demand single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2f05e-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="2f05e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2f05e-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="2f05e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2f05e-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="2f05e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2f05e-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="2f05e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2f05e-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="2f05e-118">Scenario description</span></span>
<span data-ttu-id="2f05e-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="2f05e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2f05e-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="2f05e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2f05e-121">依需求加入 Proofpoint，從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="2f05e-121">Adding Proofpoint on Demand from hello gallery</span></span>
2. <span data-ttu-id="2f05e-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="2f05e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-proofpoint-on-demand-from-hello-gallery"></a><span data-ttu-id="2f05e-123">依需求加入 Proofpoint，從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="2f05e-123">Adding Proofpoint on Demand from hello gallery</span></span>
<span data-ttu-id="2f05e-124">tooconfigure hello 整合視 Proofpoint 到 Azure AD，您需要 tooadd 視 Proofpoint hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f05e-124">tooconfigure hello integration of Proofpoint on Demand into Azure AD, you need tooadd Proofpoint on Demand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2f05e-125">**tooadd Proofpoint 視需要從 hello 圖庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="2f05e-125">**tooadd Proofpoint on Demand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f05e-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="2f05e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2f05e-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="2f05e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2f05e-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="2f05e-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="2f05e-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="2f05e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="2f05e-133">在 [hello] 搜尋方塊中，輸入**視 Proofpoint**。</span><span class="sxs-lookup"><span data-stu-id="2f05e-133">In hello search box, type **Proofpoint on Demand**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. <span data-ttu-id="2f05e-135">在 hello 結果 窗格中，選取**Proofpoint 視**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f05e-135">In hello results panel, select **Proofpoint on Demand**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2f05e-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="2f05e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2f05e-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Proofpoint on Demand 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="2f05e-138">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2f05e-139">單一登入 toowork，Azure AD 需要 tooknow 哪些 hello 對應項目中的使用者隨 Proofpoint 都 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="2f05e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Proofpoint on Demand is tooa user in Azure AD.</span></span> <span data-ttu-id="2f05e-140">換句話說，Azure AD 使用者與 hello 視 Proofpoint 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="2f05e-140">In other words, a link relationship between an Azure AD user and hello related user in Proofpoint on Demand needs toobe established.</span></span>

<span data-ttu-id="2f05e-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**使用者名稱**視 Proofpoint 中。</span><span class="sxs-lookup"><span data-stu-id="2f05e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Proofpoint on Demand.</span></span>

<span data-ttu-id="2f05e-142">tooconfigure 和測試 Azure AD 單一登入 Proofpoint 依需求，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="2f05e-142">tooconfigure and test Azure AD single sign-on with Proofpoint on Demand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2f05e-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="2f05e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2f05e-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="2f05e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2f05e-145">**[視需要測試使用者上建立 Proofpoint](#creating-a-proofpoint-on-demand-test-user)**  -toohave 許 Simon Proofpoint 視是連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="2f05e-145">**[Creating a Proofpoint on Demand test user](#creating-a-proofpoint-on-demand-test-user)** - toohave a counterpart of Britta Simon in Proofpoint on Demand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2f05e-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="2f05e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2f05e-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="2f05e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2f05e-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="2f05e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2f05e-149">在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並在您 Proofpoint 要求應用程式上設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="2f05e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Proofpoint on Demand application.</span></span>

<span data-ttu-id="2f05e-150">**tooconfigure Azure AD 單一登入與 Proofpoint 視情況下，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="2f05e-150">**tooconfigure Azure AD single sign-on with Proofpoint on Demand, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f05e-151">在 Azure 入口網站上 hello hello **Proofpoint 視**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="2f05e-151">In hello Azure portal, on hello **Proofpoint on Demand** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="2f05e-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="2f05e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
  
    ![設定單一登入](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. <span data-ttu-id="2f05e-155">在 hello**要求網域和 Url Proofpoint**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="2f05e-155">On hello **Proofpoint on Demand Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    <span data-ttu-id="2f05e-157">a.In hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<hostname>.pphosted.com/ppssamlsp_hostname`</span><span class="sxs-lookup"><span data-stu-id="2f05e-157">a.In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span></span>

    <span data-ttu-id="2f05e-158">b.</span><span class="sxs-lookup"><span data-stu-id="2f05e-158">b.</span></span> <span data-ttu-id="2f05e-159">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<hostname>.pphosted.com/ppssamlsp`</span><span class="sxs-lookup"><span data-stu-id="2f05e-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com/ppssamlsp`</span></span>

    <span data-ttu-id="2f05e-160">c.</span><span class="sxs-lookup"><span data-stu-id="2f05e-160">c.</span></span>  <span data-ttu-id="2f05e-161">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span><span class="sxs-lookup"><span data-stu-id="2f05e-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="2f05e-162">這些值不是真正的 hello。</span><span class="sxs-lookup"><span data-stu-id="2f05e-162">These values are not hello real.</span></span> <span data-ttu-id="2f05e-163">更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="2f05e-163">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="2f05e-164">請連絡[要求用戶端支援小組 Proofpoint](https://www.proofpoint.com/us/support-services) tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="2f05e-164">Contact [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) tooget these values.</span></span> 

4. <span data-ttu-id="2f05e-165">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="2f05e-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. <span data-ttu-id="2f05e-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="2f05e-167">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="2f05e-169">在 hello **Proofpoint 隨選安裝設定**區段中，按一下**設定 Proofpoint 視**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="2f05e-169">On hello **Proofpoint on Demand Configuration** section, click **Configure Proofpoint on Demand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2f05e-170">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="2f05e-170">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. <span data-ttu-id="2f05e-172">tooconfigure 單一登入上**視 Proofpoint**端，您需要下載 toosend hello **Certificate(Base64)**，**SAML 實體識別碼**，和**SAML單一登入服務 URL**太[要求用戶端支援小組 Proofpoint](https://www.proofpoint.com/us/support-services)。</span><span class="sxs-lookup"><span data-stu-id="2f05e-172">tooconfigure single sign-on on **Proofpoint on Demand** side, you need toosend hello downloaded **Certificate(Base64)**,**SAML Entity ID**, and **SAML Single Sign-On Service URL** too[Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services).</span></span>

> [!TIP]
> <span data-ttu-id="2f05e-173">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="2f05e-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2f05e-174">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="2f05e-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2f05e-175">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2f05e-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2f05e-176">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="2f05e-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="2f05e-177">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="2f05e-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="2f05e-179">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="2f05e-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f05e-180">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="2f05e-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2f05e-182">這些值不是真正的 hello。</span><span class="sxs-lookup"><span data-stu-id="2f05e-182">These values are not hello real.</span></span> <span data-ttu-id="2f05e-183">更新這些值與實際的 hello</span><span class="sxs-lookup"><span data-stu-id="2f05e-183">Update these values with hello actual</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2f05e-185">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="2f05e-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2f05e-187">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="2f05e-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2f05e-189">a.</span><span class="sxs-lookup"><span data-stu-id="2f05e-189">a.</span></span> <span data-ttu-id="2f05e-190">在 hello**名稱**文字方塊中，輸入**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="2f05e-190">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="2f05e-191">b.</span><span class="sxs-lookup"><span data-stu-id="2f05e-191">b.</span></span> <span data-ttu-id="2f05e-192">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**許 Simon。</span><span class="sxs-lookup"><span data-stu-id="2f05e-192">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="2f05e-193">c.</span><span class="sxs-lookup"><span data-stu-id="2f05e-193">c.</span></span> <span data-ttu-id="2f05e-194">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="2f05e-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2f05e-195">d.</span><span class="sxs-lookup"><span data-stu-id="2f05e-195">d.</span></span> <span data-ttu-id="2f05e-196">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="2f05e-196">Click **Create**.</span></span>
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a><span data-ttu-id="2f05e-197">建立 Proofpoint on Demand 測試使用者</span><span class="sxs-lookup"><span data-stu-id="2f05e-197">Creating a Proofpoint on Demand test user</span></span>

<span data-ttu-id="2f05e-198">在本節中，您會在 Proofpoint on Demand 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="2f05e-198">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span></span> <span data-ttu-id="2f05e-199">使用[要求用戶端支援小組 Proofpoint](https://www.proofpoint.com/us/support-services) tooadd hello Proofpoint 要求平台上的使用者。</span><span class="sxs-lookup"><span data-stu-id="2f05e-199">Work with [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) tooadd users in hello Proofpoint on Demand platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2f05e-200">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="2f05e-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2f05e-201">在本節中，您可以授與存取 tooProofpoint 視啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="2f05e-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooProofpoint on Demand.</span></span>

![指派使用者][200] 

<span data-ttu-id="2f05e-203">**tooassign 許 Simon tooProofpoint 視情況下，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="2f05e-203">**tooassign Britta Simon tooProofpoint on Demand, perform hello following steps:**</span></span>

1. <span data-ttu-id="2f05e-204">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="2f05e-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="2f05e-206">在 [hello] 應用程式清單中，選取**視 Proofpoint**。</span><span class="sxs-lookup"><span data-stu-id="2f05e-206">In hello applications list, select **Proofpoint on Demand**.</span></span>

    ![設定單一登入](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. <span data-ttu-id="2f05e-208">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="2f05e-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="2f05e-210">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2f05e-210">Click **Add** button.</span></span> <span data-ttu-id="2f05e-211">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="2f05e-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="2f05e-213">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="2f05e-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2f05e-214">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2f05e-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2f05e-215">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2f05e-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2f05e-216">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="2f05e-216">Testing single sign-on</span></span>

<span data-ttu-id="2f05e-217">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="2f05e-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2f05e-218">當您按一下 hello**視 Proofpoint**您應該會自動登入，視需要應用程式上 tooyour Proofpoint hello 存取面板上的磚。</span><span class="sxs-lookup"><span data-stu-id="2f05e-218">When you click hello **Proofpoint on Demand** tile on hello Access Panel, you should be automatically signed on tooyour Proofpoint on Demand application.</span></span>
<span data-ttu-id="2f05e-219">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="2f05e-219">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>  

## <a name="additional-resources"></a><span data-ttu-id="2f05e-220">其他資源</span><span class="sxs-lookup"><span data-stu-id="2f05e-220">Additional resources</span></span>

* [<span data-ttu-id="2f05e-221">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f05e-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2f05e-222">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="2f05e-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png


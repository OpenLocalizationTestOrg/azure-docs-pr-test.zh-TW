---
title: "教學課程：Azure Active Directory 與 SAP Business ByDesign 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 SAP Business ByDesign 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: c14714fd27f8d7fc555f25c7be83fad2b0d7f333
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="0146c-103">教學課程：Azure Active Directory 與 SAP Business ByDesign 整合</span><span class="sxs-lookup"><span data-stu-id="0146c-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="0146c-104">在此教學課程中，您學習如何 toointegrate SAP Business ByDesign 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="0146c-104">In this tutorial, you learn how toointegrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0146c-105">與 Azure AD 整合 SAP Business ByDesign 可以提供下列優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="0146c-105">Integrating SAP Business ByDesign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0146c-106">您可以控制存取 tooSAP 商務 ByDesign Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="0146c-106">You can control in Azure AD who has access tooSAP Business ByDesign.</span></span>
- <span data-ttu-id="0146c-107">您可以使用其 Azure AD 帳戶啟用您使用者 tooautomatically get 登入 tooSAP 商務 ByDesign （單一登入）。</span><span class="sxs-lookup"><span data-stu-id="0146c-107">You can enable your users tooautomatically get signed-on tooSAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0146c-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0146c-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="0146c-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="0146c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0146c-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="0146c-110">Prerequisites</span></span>

<span data-ttu-id="0146c-111">tooconfigure 與 SAP Business ByDesign 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="0146c-111">tooconfigure Azure AD integration with SAP Business ByDesign, you need hello following items:</span></span>

- <span data-ttu-id="0146c-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0146c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0146c-113">已啟用 SAP Business ByDesign 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0146c-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0146c-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="0146c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0146c-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="0146c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0146c-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0146c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0146c-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="0146c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0146c-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="0146c-118">Scenario description</span></span>
<span data-ttu-id="0146c-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0146c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0146c-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="0146c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0146c-121">加入 SAP Business ByDesign 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="0146c-121">Adding SAP Business ByDesign from hello gallery</span></span>
2. <span data-ttu-id="0146c-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0146c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-hello-gallery"></a><span data-ttu-id="0146c-123">加入 SAP Business ByDesign 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="0146c-123">Adding SAP Business ByDesign from hello gallery</span></span>
<span data-ttu-id="0146c-124">tooconfigure hello 整合 SAP Business ByDesign 到 Azure AD，您需要 tooadd SAP Business ByDesign hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0146c-124">tooconfigure hello integration of SAP Business ByDesign into Azure AD, you need tooadd SAP Business ByDesign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0146c-125">**tooadd SAP Business ByDesign 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0146c-125">**tooadd SAP Business ByDesign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0146c-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="0146c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory] 按鈕][1]

2. <span data-ttu-id="0146c-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0146c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0146c-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0146c-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式] 刀鋒視窗][2]
    
3. <span data-ttu-id="0146c-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="0146c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="0146c-133">在 [hello] 搜尋方塊中，輸入**SAP Business ByDesign**，選取**SAP Business ByDesign**然後按一下 [從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0146c-133">In hello search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button tooadd hello application.</span></span>

    ![SAP Business ByDesign hello [結果] 清單中](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0146c-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0146c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0146c-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SAP Business ByDesign 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0146c-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0146c-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 SAP Business ByDesign 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="0146c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP Business ByDesign is tooa user in Azure AD.</span></span> <span data-ttu-id="0146c-138">換句話說，Azure AD 使用者與 hello SAP Business ByDesign 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="0146c-138">In other words, a link relationship between an Azure AD user and hello related user in SAP Business ByDesign needs toobe established.</span></span>

<span data-ttu-id="0146c-139">在 SAP Business ByDesign，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="0146c-139">In SAP Business ByDesign, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0146c-140">tooconfigure 及 SAP Business ByDesign 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="0146c-140">tooconfigure and test Azure AD single sign-on with SAP Business ByDesign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0146c-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="0146c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0146c-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="0146c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0146c-143">**[建立 SAP Business ByDesign 測試使用者](#create-an-sap-business-bydesign-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 SAP 商業 ByDesign 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="0146c-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - toohave a counterpart of Britta Simon in SAP Business ByDesign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0146c-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0146c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0146c-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="0146c-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0146c-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0146c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0146c-147">在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 SAP Business ByDesign 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="0146c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="0146c-148">**tooconfigure Azure AD 單一登入與 SAP Business ByDesign，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0146c-148">**tooconfigure Azure AD single sign-on with SAP Business ByDesign, perform hello following steps:**</span></span>

1. <span data-ttu-id="0146c-149">在 Azure 入口網站上 hello hello **SAP Business ByDesign**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="0146c-149">In hello Azure portal, on hello **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="0146c-151">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0146c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. <span data-ttu-id="0146c-153">在 [hello **SAP 商務 ByDesign 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0146c-153">On hello **SAP Business ByDesign Domain and URLs** section, perform hello following steps:</span></span>

    ![SAP Business ByDesign 網域及 URL 單一登入資訊](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="0146c-155">a.</span><span class="sxs-lookup"><span data-stu-id="0146c-155">a.</span></span> <span data-ttu-id="0146c-156">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="0146c-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="0146c-157">b.</span><span class="sxs-lookup"><span data-stu-id="0146c-157">b.</span></span> <span data-ttu-id="0146c-158">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="0146c-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0146c-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="0146c-159">These values are not real.</span></span> <span data-ttu-id="0146c-160">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="0146c-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0146c-161">請連絡[SAP 商務 ByDesign 用戶端支援小組](https://www.sap.com/products/cloud-analytics.support.html)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="0146c-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) tooget these values.</span></span>

4. <span data-ttu-id="0146c-162">在 [hello**使用者屬性**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0146c-162">On hello **User Attributes** section, perform hello following steps:</span></span>

    ![[SAP Business ByDesign 屬性] 區段](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="0146c-164">a.</span><span class="sxs-lookup"><span data-stu-id="0146c-164">a.</span></span> <span data-ttu-id="0146c-165">在**使用者識別碼**清單中，選取 hello **ExtractMailPrefix()**函式。</span><span class="sxs-lookup"><span data-stu-id="0146c-165">In **User Identifier** list, select hello **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="0146c-166">b.</span><span class="sxs-lookup"><span data-stu-id="0146c-166">b.</span></span> <span data-ttu-id="0146c-167">從 hello**郵件**清單中，您想要實作 toouse 選取 hello 使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="0146c-167">From hello **Mail** list, select hello user attribute you want toouse for your implementation.</span></span> <span data-ttu-id="0146c-168">例如，如果您想 toouse hello EmployeeID 做為唯一的使用者識別碼，而且您已在 hello ExtensionAttribute2 儲存 hello 屬性值，然後選取 user.extensionattribute2。</span><span class="sxs-lookup"><span data-stu-id="0146c-168">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select user.extensionattribute2.</span></span>   

5. <span data-ttu-id="0146c-169">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="0146c-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. <span data-ttu-id="0146c-171">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="0146c-171">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="0146c-173">在 hello **SAP 商務 ByDesign 組態**區段中，按一下**設定 SAP Business ByDesign** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="0146c-173">On hello **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0146c-174">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="0146c-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![SAP Business ByDesign 設定](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. <span data-ttu-id="0146c-176">tooget SSO 設定應用程式執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0146c-176">tooget SSO configured for your application, perform hello following steps:</span></span>
   
    <span data-ttu-id="0146c-177">a.</span><span class="sxs-lookup"><span data-stu-id="0146c-177">a.</span></span> <span data-ttu-id="0146c-178">登入 tooyour SAP Business ByDesign 入口網站，以系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="0146c-178">Sign on tooyour SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="0146c-179">b.</span><span class="sxs-lookup"><span data-stu-id="0146c-179">b.</span></span> <span data-ttu-id="0146c-180">瀏覽過**應用程式和使用者管理的一般工作**按一下 hello**身分識別提供者**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0146c-180">Navigate too**Application and User Management Common Task** and click hello **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="0146c-181">c.</span><span class="sxs-lookup"><span data-stu-id="0146c-181">c.</span></span> <span data-ttu-id="0146c-182">按一下**新的身分識別提供者**和從 hello Azure 入口網站下載的選取 hello 中繼資料 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="0146c-182">Click **New Identity Provider** and select hello metadata XML file that you have downloaded from hello Azure portal.</span></span> <span data-ttu-id="0146c-183">匯入 hello 中繼資料，hello 系統會自動上傳 hello 需要的簽章憑證和加密憑證。</span><span class="sxs-lookup"><span data-stu-id="0146c-183">By importing hello metadata, hello system automatically uploads hello required signature certificate and encryption certificate.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="0146c-185">d.</span><span class="sxs-lookup"><span data-stu-id="0146c-185">d.</span></span> <span data-ttu-id="0146c-186">tooinclude hello**判斷提示取用者服務 URL**入 hello SAML 要求，請選取**包括判斷提示取用者服務 URL**。</span><span class="sxs-lookup"><span data-stu-id="0146c-186">tooinclude hello **Assertion Consumer Service URL** into hello SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="0146c-187">e.</span><span class="sxs-lookup"><span data-stu-id="0146c-187">e.</span></span> <span data-ttu-id="0146c-188">按一下 [啟用單一登入]。</span><span class="sxs-lookup"><span data-stu-id="0146c-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="0146c-189">f.</span><span class="sxs-lookup"><span data-stu-id="0146c-189">f.</span></span> <span data-ttu-id="0146c-190">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="0146c-190">Save your changes.</span></span>
   
    <span data-ttu-id="0146c-191">g.</span><span class="sxs-lookup"><span data-stu-id="0146c-191">g.</span></span> <span data-ttu-id="0146c-192">按一下 hello**我系統**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0146c-192">Click hello **My System** tab.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="0146c-194">h.</span><span class="sxs-lookup"><span data-stu-id="0146c-194">h.</span></span> <span data-ttu-id="0146c-195">貼上**SAML 單一登入服務 URL**，您已複製 hello Azure 入口網站從它到 hello **Azure AD 登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="0146c-195">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal it into hello **Azure AD Sign On URL** textbox.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="0146c-197">i.</span><span class="sxs-lookup"><span data-stu-id="0146c-197">i.</span></span> <span data-ttu-id="0146c-198">指定是否 hello 員工可以手動選擇選取登入以使用者識別碼和密碼或 SSO**手動身分識別提供者選取**。</span><span class="sxs-lookup"><span data-stu-id="0146c-198">Specify whether hello employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="0146c-199">j.</span><span class="sxs-lookup"><span data-stu-id="0146c-199">j.</span></span> <span data-ttu-id="0146c-200">在 [hello **SSO URL**區段中，指定應該由 hello 員工 toologon toohello 系統的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="0146c-200">In hello **SSO URL** section, specify hello URL that should be used by hello employee toologon toohello system.</span></span> 
    <span data-ttu-id="0146c-201">Hello URL 傳送 tooEmployee 下拉式清單中，您可以選擇下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="0146c-201">In hello URL Sent tooEmployee dropdown list, you can choose between hello following options:</span></span>
   
    <span data-ttu-id="0146c-202">**非 SSO URL**</span><span class="sxs-lookup"><span data-stu-id="0146c-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="0146c-203">hello 系統會傳送只 hello 一般系統 URL toohello 員工。</span><span class="sxs-lookup"><span data-stu-id="0146c-203">hello system sends only hello normal system URL toohello employee.</span></span> <span data-ttu-id="0146c-204">hello 員工無法登入使用 SSO，且必須使用密碼或改為憑證。</span><span class="sxs-lookup"><span data-stu-id="0146c-204">hello employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="0146c-205">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="0146c-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="0146c-206">hello 系統會傳送只 hello SSO URL toohello 員工。</span><span class="sxs-lookup"><span data-stu-id="0146c-206">hello system sends only hello SSO URL toohello employee.</span></span> <span data-ttu-id="0146c-207">hello 員工可以登入使用 SSO。</span><span class="sxs-lookup"><span data-stu-id="0146c-207">hello employee can log on using SSO.</span></span> <span data-ttu-id="0146c-208">驗證要求重新導向到 [hello IdP。</span><span class="sxs-lookup"><span data-stu-id="0146c-208">Authentication request is redirected through hello IdP.</span></span>
   
    <span data-ttu-id="0146c-209">**自動選取**</span><span class="sxs-lookup"><span data-stu-id="0146c-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="0146c-210">如果並未啟用 SSO，hello 系統會傳送 hello 一般系統 URL toohello 員工。</span><span class="sxs-lookup"><span data-stu-id="0146c-210">If SSO is not active, hello system sends hello normal system URL toohello employee.</span></span> <span data-ttu-id="0146c-211">如果 SSO 為作用中，hello 系統會檢查 hello 員工是否有密碼。</span><span class="sxs-lookup"><span data-stu-id="0146c-211">If SSO is active, hello system checks whether hello employee has a password.</span></span> <span data-ttu-id="0146c-212">如果密碼功能，同時 SSO URL 和非 SSO URL 傳送 toohello 員工。</span><span class="sxs-lookup"><span data-stu-id="0146c-212">If a password is available, both SSO URL and Non-SSO URL are sent toohello employee.</span></span> <span data-ttu-id="0146c-213">不過，如果 hello 員工沒有密碼，hello SSO URL 會傳送 toohello 員工。</span><span class="sxs-lookup"><span data-stu-id="0146c-213">However, if hello employee has no password, only hello SSO URL is sent toohello employee.</span></span>
   
    <span data-ttu-id="0146c-214">k.</span><span class="sxs-lookup"><span data-stu-id="0146c-214">k.</span></span> <span data-ttu-id="0146c-215">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="0146c-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="0146c-216">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="0146c-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0146c-217">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="0146c-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0146c-218">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0146c-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0146c-219">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0146c-219">Create an Azure AD test user</span></span>

<span data-ttu-id="0146c-220">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="0146c-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="0146c-222">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0146c-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0146c-223">在 [hello Azure 入口網站，hello 左窗格中，按一下 [hello **Azure Active Directory** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0146c-223">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory] 按鈕](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0146c-225">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下 [**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="0146c-225">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0146c-227">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0146c-227">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0146c-229">在 [hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0146c-229">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0146c-231">a.</span><span class="sxs-lookup"><span data-stu-id="0146c-231">a.</span></span> <span data-ttu-id="0146c-232">在 [hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="0146c-232">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0146c-233">b.</span><span class="sxs-lookup"><span data-stu-id="0146c-233">b.</span></span> <span data-ttu-id="0146c-234">在 [hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="0146c-234">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="0146c-235">c.</span><span class="sxs-lookup"><span data-stu-id="0146c-235">c.</span></span> <span data-ttu-id="0146c-236">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 [hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="0146c-236">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="0146c-237">d.</span><span class="sxs-lookup"><span data-stu-id="0146c-237">d.</span></span> <span data-ttu-id="0146c-238">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0146c-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="0146c-239">建立 SAP Business ByDesign 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0146c-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="0146c-240">在本節中，您要在 SAP Business ByDesign 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="0146c-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="0146c-241">請使用[SAP 商務 ByDesign 用戶端支援小組](https://www.sap.com/products/cloud-analytics.support.html)tooadd hello hello SAP Business ByDesign 平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="0146c-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) tooadd hello users in hello SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="0146c-242">請確定 NameID 值應該符合與 hello hello SAP Business ByDesign 平台中的使用者名稱欄位。</span><span class="sxs-lookup"><span data-stu-id="0146c-242">Please make sure that NameID value should match with hello username field in hello SAP Business ByDesign platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="0146c-243">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0146c-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="0146c-244">在本節中，您可以授與存取 tooSAP 商務 ByDesign 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0146c-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP Business ByDesign.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="0146c-246">**tooassign 許 Simon tooSAP 商務 ByDesign，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0146c-246">**tooassign Britta Simon tooSAP Business ByDesign, perform hello following steps:**</span></span>

1. <span data-ttu-id="0146c-247">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0146c-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="0146c-249">在 [hello] 應用程式清單中，選取**SAP Business ByDesign**。</span><span class="sxs-lookup"><span data-stu-id="0146c-249">In hello applications list, select **SAP Business ByDesign**.</span></span>

    ![hello 應用程式清單中的 hello SAP Business ByDesign 連結](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. <span data-ttu-id="0146c-251">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="0146c-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="0146c-253">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0146c-253">Click **Add** button.</span></span> <span data-ttu-id="0146c-254">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0146c-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="0146c-256">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="0146c-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0146c-257">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0146c-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0146c-258">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0146c-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0146c-259">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="0146c-259">Test single sign-on</span></span>

<span data-ttu-id="0146c-260">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="0146c-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0146c-261">當您按一下 hello SAP Business ByDesign 磚 hello 存取面板中的時，您應該取得自動登入 tooyour SAP Business ByDesign 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0146c-261">When you click hello SAP Business ByDesign tile in hello Access Panel, you should get automatically signed-on tooyour SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0146c-262">其他資源</span><span class="sxs-lookup"><span data-stu-id="0146c-262">Additional resources</span></span>

* [<span data-ttu-id="0146c-263">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0146c-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0146c-264">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="0146c-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png


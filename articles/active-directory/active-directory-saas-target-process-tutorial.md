---
title: "教學課程：將 Azure Active Directory 與 TargetProcess 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 TargetProcess 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 05c574e2c18d7f73edc6c094093a6e59d46b8e6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a><span data-ttu-id="8f8e4-103">教學課程：將 Azure Active Directory 與 TargetProcess 整合</span><span class="sxs-lookup"><span data-stu-id="8f8e4-103">Tutorial: Azure Active Directory integration with TargetProcess</span></span>

<span data-ttu-id="8f8e4-104">在此教學課程中，您學會如何 toointegrate TargetProcess 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-104">In this tutorial, you learn how toointegrate TargetProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8f8e4-105">與 Azure AD 整合 TargetProcess 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="8f8e4-105">Integrating TargetProcess with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8f8e4-106">您可以控制存取 tooTargetProcess Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="8f8e4-106">You can control in Azure AD who has access tooTargetProcess</span></span>
- <span data-ttu-id="8f8e4-107">您可以啟用您的使用者 tooautomatically get 登入 tooTargetProcess （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="8f8e4-107">You can enable your users tooautomatically get signed-on tooTargetProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8f8e4-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8f8e4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8f8e4-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f8e4-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="8f8e4-110">Prerequisites</span></span>

<span data-ttu-id="8f8e4-111">tooconfigure TargetProcess 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="8f8e4-111">tooconfigure Azure AD integration with TargetProcess, you need hello following items:</span></span>

- <span data-ttu-id="8f8e4-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8f8e4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8f8e4-113">已啟用 TargetProcess 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8f8e4-113">A TargetProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8f8e4-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8f8e4-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="8f8e4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8f8e4-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8f8e4-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8f8e4-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="8f8e4-118">Scenario description</span></span>
<span data-ttu-id="8f8e4-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8f8e4-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="8f8e4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8f8e4-121">從 hello 圖庫新增 TargetProcess</span><span class="sxs-lookup"><span data-stu-id="8f8e4-121">Add TargetProcess from hello gallery</span></span>
2. <span data-ttu-id="8f8e4-122">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8f8e4-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-targetprocess-from-hello-gallery"></a><span data-ttu-id="8f8e4-123">從 hello 圖庫新增 TargetProcess</span><span class="sxs-lookup"><span data-stu-id="8f8e4-123">Add TargetProcess from hello gallery</span></span>
<span data-ttu-id="8f8e4-124">tooconfigure hello 整合 TargetProcess 到 Azure AD，您需要 tooadd TargetProcess hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-124">tooconfigure hello integration of TargetProcess into Azure AD, you need tooadd TargetProcess from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8f8e4-125">**tooadd TargetProcess 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8f8e4-125">**tooadd TargetProcess from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f8e4-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8f8e4-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8f8e4-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="8f8e4-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="8f8e4-133">在 hello 搜尋方塊中，輸入**TargetProcess**，選取**TargetProcess**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-133">In hello search box, type **TargetProcess**, select **TargetProcess**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![從資源庫新增 TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8f8e4-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8f8e4-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="8f8e4-136">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 TargetProcess 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-136">In this section, you configure and test Azure AD single sign-on with TargetProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8f8e4-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 TargetProcess 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TargetProcess is tooa user in Azure AD.</span></span> <span data-ttu-id="8f8e4-138">換句話說，Azure AD 使用者與 hello TargetProcess 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-138">In other words, a link relationship between an Azure AD user and hello related user in TargetProcess needs toobe established.</span></span>

<span data-ttu-id="8f8e4-139">TargetProcess 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-139">In TargetProcess, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8f8e4-140">tooconfigure 及 TargetProcess 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="8f8e4-140">tooconfigure and test Azure AD single sign-on with TargetProcess, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8f8e4-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8f8e4-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8f8e4-143">**[建立測試使用者 TargetProcess](#create-a-targetprocess-test-user)**  -toohave 許 Simon TargetProcess 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-143">**[Create a TargetProcess test user](#create-a-targetprocess-test-user)** - toohave a counterpart of Britta Simon in TargetProcess that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8f8e4-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8f8e4-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8f8e4-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8f8e4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8f8e4-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 TargetProcess 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TargetProcess application.</span></span>

<span data-ttu-id="8f8e4-148">**tooconfigure Azure AD 單一登入與 TargetProcess，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8f8e4-148">**tooconfigure Azure AD single sign-on with TargetProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f8e4-149">在 Azure 入口網站上 hello hello **TargetProcess**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-149">In hello Azure portal, on hello **TargetProcess** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="8f8e4-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML 型登入](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_samlbase.png)

3. <span data-ttu-id="8f8e4-153">在 hello **TargetProcess 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8f8e4-153">On hello **TargetProcess Domain and URLs** section, perform hello following steps:</span></span>

    ![[TargetProcess 網域與 URL] 區段](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_url.png)

    <span data-ttu-id="8f8e4-155">a.</span><span class="sxs-lookup"><span data-stu-id="8f8e4-155">a.</span></span> <span data-ttu-id="8f8e4-156">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="8f8e4-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    <span data-ttu-id="8f8e4-157">b.</span><span class="sxs-lookup"><span data-stu-id="8f8e4-157">b.</span></span> <span data-ttu-id="8f8e4-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="8f8e4-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8f8e4-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-159">These values are not real.</span></span> <span data-ttu-id="8f8e4-160">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8f8e4-161">請連絡[TargetProcess 用戶端支援小組](mailto:support@targetprocess.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-161">Contact [TargetProcess Client support team](mailto:support@targetprocess.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="8f8e4-162">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![[SAML 簽署憑證] 區段](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_certificate.png) 

5. <span data-ttu-id="8f8e4-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-164">Click **Save** button.</span></span>

    ![[儲存] 按鈕](./media/active-directory-saas-target-process-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8f8e4-166">在 hello **TargetProcess 組態**區段中，按一下**設定 TargetProcess** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-166">On hello **TargetProcess Configuration** section, click **Configure TargetProcess** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8f8e4-167">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="8f8e4-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![[TargetProcess 組態] 區段](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_configure.png) 

7. <span data-ttu-id="8f8e4-169">登入 tooyour TargetProcess 應用程式，以系統管理員。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-169">Sign-on tooyour TargetProcess application as an administrator.</span></span>

8. <span data-ttu-id="8f8e4-170">在 hello 最上層顯示 hello 功能表上，按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-170">In hello menu on hello top, click **Setup**.</span></span>
   
    ![設定](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)

9. <span data-ttu-id="8f8e4-172">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-172">Click **Settings**.</span></span>
   
    ![設定](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 

10. <span data-ttu-id="8f8e4-174">按一下 [單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-174">Click **Single Sign-on**.</span></span>
   
    ![按一下 [單一登入]](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 

11. <span data-ttu-id="8f8e4-176">在 hello 單一登入設定 對話方塊，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8f8e4-176">On hello Single Sign-on settings dialog, perform hello following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)
    
    <span data-ttu-id="8f8e4-178">a.</span><span class="sxs-lookup"><span data-stu-id="8f8e4-178">a.</span></span> <span data-ttu-id="8f8e4-179">按一下 [啟用單一登入]。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-179">Click **Enable Single Sign-on**.</span></span>
    
    <span data-ttu-id="8f8e4-180">b.</span><span class="sxs-lookup"><span data-stu-id="8f8e4-180">b.</span></span> <span data-ttu-id="8f8e4-181">在**登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-181">In **Sign-on URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8f8e4-182">c.</span><span class="sxs-lookup"><span data-stu-id="8f8e4-182">c.</span></span> <span data-ttu-id="8f8e4-183">開啟 [記事本]，複製 hello 內容，您所下載的憑證，然後將它貼到 hello**憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-183">Open your downloaded certificate in notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span>
    
    <span data-ttu-id="8f8e4-184">d.</span><span class="sxs-lookup"><span data-stu-id="8f8e4-184">d.</span></span> <span data-ttu-id="8f8e4-185">按一下 [ **啟用 JIT 佈建**]。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-185">click **Enable JIT Provisioning**.</span></span>

    <span data-ttu-id="8f8e4-186">e.</span><span class="sxs-lookup"><span data-stu-id="8f8e4-186">e.</span></span> <span data-ttu-id="8f8e4-187">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="8f8e4-188">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="8f8e4-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8f8e4-189">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8f8e4-190">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8f8e4-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8f8e4-191">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8f8e4-191">Create an Azure AD test user</span></span>
<span data-ttu-id="8f8e4-192">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="8f8e4-194">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8f8e4-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f8e4-195">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-target-process-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8f8e4-197">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![使用者 toodisplay hello 清單](./media/active-directory-saas-target-process-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8f8e4-199">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![[新增] 按鈕](./media/active-directory-saas-target-process-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8f8e4-201">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8f8e4-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![[使用者] 區段](./media/active-directory-saas-target-process-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8f8e4-203">a.</span><span class="sxs-lookup"><span data-stu-id="8f8e4-203">a.</span></span> <span data-ttu-id="8f8e4-204">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8f8e4-205">b.</span><span class="sxs-lookup"><span data-stu-id="8f8e4-205">b.</span></span> <span data-ttu-id="8f8e4-206">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8f8e4-207">c.</span><span class="sxs-lookup"><span data-stu-id="8f8e4-207">c.</span></span> <span data-ttu-id="8f8e4-208">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8f8e4-209">d.</span><span class="sxs-lookup"><span data-stu-id="8f8e4-209">d.</span></span> <span data-ttu-id="8f8e4-210">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-210">Click **Create**.</span></span>
 
### <a name="create-a-targetprocess-test-user"></a><span data-ttu-id="8f8e4-211">建立 TargetProcess 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8f8e4-211">Create a TargetProcess test user</span></span>

<span data-ttu-id="8f8e4-212">hello 本節目標在於 toocreate TargetProcess 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-212">hello objective of this section is toocreate a user called Britta Simon in TargetProcess.</span></span>

<span data-ttu-id="8f8e4-213">TargetProcess 支援 Just-in-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-213">TargetProcess supports just-in-time provisioning.</span></span> <span data-ttu-id="8f8e4-214">您已在 [設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)中啟用。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="8f8e4-215">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-215">There is no action item for you in this section.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="8f8e4-216">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8f8e4-216">Assign hello Azure AD test user</span></span>

<span data-ttu-id="8f8e4-217">在本節中，您可以授與存取 tooTargetProcess 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTargetProcess.</span></span>

![指派使用者][200] 

<span data-ttu-id="8f8e4-219">**tooassign 許 Simon tooTargetProcess，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8f8e4-219">**tooassign Britta Simon tooTargetProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f8e4-220">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="8f8e4-222">在 [hello] 應用程式清單中，選取**TargetProcess**。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-222">In hello applications list, select **TargetProcess**.</span></span>

    ![應用程式清單中的 TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_app.png) 

3. <span data-ttu-id="8f8e4-224">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="8f8e4-226">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-226">Click **Add** button.</span></span> <span data-ttu-id="8f8e4-227">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="8f8e4-229">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8f8e4-230">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8f8e4-231">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8f8e4-232">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="8f8e4-232">Test single sign-on</span></span>

<span data-ttu-id="8f8e4-233">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-233">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8f8e4-234">當您按一下的 hello TargetProcess 磚 hello 存取面板中時，您應該取得自動登入 tooyour TargetProcess 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-234">When you click hello TargetProcess tile in hello Access Panel, you should get automatically signed-on tooyour TargetProcess application.</span></span> <span data-ttu-id="8f8e4-235">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="8f8e4-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8f8e4-236">其他資源</span><span class="sxs-lookup"><span data-stu-id="8f8e4-236">Additional resources</span></span>

* [<span data-ttu-id="8f8e4-237">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8f8e4-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8f8e4-238">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="8f8e4-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_203.png


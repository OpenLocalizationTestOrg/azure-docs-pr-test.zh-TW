---
title: "教學課程：Azure Active Directory 與 OfficeSpace Software 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 OfficeSpace Software 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: b53afb648b8a6057c32c782d857e34c06e152c67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a><span data-ttu-id="75b82-103">教學課程：Azure Active Directory 與 OfficeSpace Software 整合</span><span class="sxs-lookup"><span data-stu-id="75b82-103">Tutorial: Azure Active Directory integration with OfficeSpace Software</span></span>

<span data-ttu-id="75b82-104">在此教學課程中，您學會如何 toointegrate OfficeSpace Software 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="75b82-104">In this tutorial, you learn how toointegrate OfficeSpace Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="75b82-105">整合 Azure AD 與 OfficeSpace Software 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="75b82-105">Integrating OfficeSpace Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="75b82-106">您可以控制存取 tooOfficeSpace 軟體的 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="75b82-106">You can control in Azure AD who has access tooOfficeSpace Software.</span></span>
- <span data-ttu-id="75b82-107">您可以啟用您的使用者 tooautomatically get 登入 tooOfficeSpace （單一登入） 的軟體與他們的 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="75b82-107">You can enable your users tooautomatically get signed-on tooOfficeSpace Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="75b82-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="75b82-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="75b82-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="75b82-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75b82-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="75b82-110">Prerequisites</span></span>

<span data-ttu-id="75b82-111">tooconfigure Azure AD 與 OfficeSpace Software 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="75b82-111">tooconfigure Azure AD integration with OfficeSpace Software, you need hello following items:</span></span>

- <span data-ttu-id="75b82-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="75b82-112">An Azure AD subscription</span></span>
- <span data-ttu-id="75b82-113">已啟用 OfficeSpace Software 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="75b82-113">A OfficeSpace Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="75b82-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="75b82-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="75b82-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="75b82-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="75b82-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="75b82-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="75b82-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="75b82-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="75b82-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="75b82-118">Scenario description</span></span>
<span data-ttu-id="75b82-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="75b82-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="75b82-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="75b82-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="75b82-121">從 hello 圖庫加入 OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="75b82-121">Adding OfficeSpace Software from hello gallery</span></span>
2. <span data-ttu-id="75b82-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="75b82-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-officespace-software-from-hello-gallery"></a><span data-ttu-id="75b82-123">從 hello 圖庫加入 OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="75b82-123">Adding OfficeSpace Software from hello gallery</span></span>
<span data-ttu-id="75b82-124">tooconfigure hello 整合 OfficeSpace Software 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd OfficeSpace Software。</span><span class="sxs-lookup"><span data-stu-id="75b82-124">tooconfigure hello integration of OfficeSpace Software into Azure AD, you need tooadd OfficeSpace Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="75b82-125">**tooadd OfficeSpace Software 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="75b82-125">**tooadd OfficeSpace Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="75b82-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="75b82-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="75b82-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="75b82-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="75b82-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="75b82-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="75b82-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="75b82-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="75b82-133">在 hello 搜尋方塊中，輸入**OfficeSpace Software**，選取**OfficeSpace Software**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="75b82-133">In hello search box, type **OfficeSpace Software**, select **OfficeSpace Software** from result panel then click **Add** button tooadd hello application.</span></span>

    ![在 hello OfficeSpace Software 結果清單](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="75b82-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="75b82-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="75b82-136">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 OfficeSpace Software 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="75b82-136">In this section, you configure and test Azure AD single sign-on with OfficeSpace Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="75b82-137">單一登入 toowork，Azure AD 需要 tooknow OfficeSpace Software 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="75b82-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in OfficeSpace Software is tooa user in Azure AD.</span></span> <span data-ttu-id="75b82-138">換句話說，Azure AD 使用者與 OfficeSpace Software 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="75b82-138">In other words, a link relationship between an Azure AD user and hello related user in OfficeSpace Software needs toobe established.</span></span>

<span data-ttu-id="75b82-139">在 OfficeSpace Software 中，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="75b82-139">In OfficeSpace Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="75b82-140">tooconfigure 和測試 Azure AD 單一登入與 OfficeSpace Software，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="75b82-140">tooconfigure and test Azure AD single sign-on with OfficeSpace Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="75b82-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="75b82-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="75b82-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="75b82-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="75b82-143">**[建立測試使用者 OfficeSpace Software](#create-a-officespace-software-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 OfficeSpace Software 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="75b82-143">**[Create a OfficeSpace Software test user](#create-a-officespace-software-test-user)** - toohave a counterpart of Britta Simon in OfficeSpace Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="75b82-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="75b82-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="75b82-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="75b82-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="75b82-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="75b82-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="75b82-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 OfficeSpace Software 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="75b82-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your OfficeSpace Software application.</span></span>

<span data-ttu-id="75b82-148">**tooconfigure Azure AD 單一登入 OfficeSpace Software 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="75b82-148">**tooconfigure Azure AD single sign-on with OfficeSpace Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="75b82-149">在 Azure 入口網站上 hello hello **OfficeSpace Software**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="75b82-149">In hello Azure portal, on hello **OfficeSpace Software** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="75b82-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="75b82-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_samlbase.png)

3. <span data-ttu-id="75b82-153">在 hello **OfficeSpace 軟體網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="75b82-153">On hello **OfficeSpace Software Domain and URLs** section, perform hello following steps:</span></span>

    ![OfficeSpace Software 網域與 URL 單一登入資訊](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_url.png)

    <span data-ttu-id="75b82-155">a.</span><span class="sxs-lookup"><span data-stu-id="75b82-155">a.</span></span> <span data-ttu-id="75b82-156">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.officespacesoftware.com/users/sign_in/saml`</span><span class="sxs-lookup"><span data-stu-id="75b82-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span></span>

    <span data-ttu-id="75b82-157">b.</span><span class="sxs-lookup"><span data-stu-id="75b82-157">b.</span></span> <span data-ttu-id="75b82-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`<company name>.officespacesoftware.com`</span><span class="sxs-lookup"><span data-stu-id="75b82-158">In hello **Identifier** textbox, type a URL using hello following pattern: `<company name>.officespacesoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="75b82-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="75b82-159">These values are not real.</span></span> <span data-ttu-id="75b82-160">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="75b82-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="75b82-161">請連絡[OfficeSpace 軟體用戶端支援小組](mailto:support@officespacesoftware.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="75b82-161">Contact [OfficeSpace Software Client support team](mailto:support@officespacesoftware.com) tooget these values.</span></span> 

4. <span data-ttu-id="75b82-162">OfficeSpace Software 應用程式預期 hello SAML 判斷提示，以特定格式。</span><span class="sxs-lookup"><span data-stu-id="75b82-162">OfficeSpace Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="75b82-163">請設定下列宣告為此應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="75b82-163">Please configure hello following claims for this application.</span></span> <span data-ttu-id="75b82-164">您可以從 hello 管理 hello 這些屬性的值"**使用者屬性**」 一節，在應用程式整合頁面上。</span><span class="sxs-lookup"><span data-stu-id="75b82-164">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="75b82-165">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="75b82-165">hello following screenshot shows an example for this.</span></span>
    
    ![設定屬性](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_attribute.png)

5. <span data-ttu-id="75b82-167">在 hello**使用者屬性**hello 區段**單一登入**對話方塊中，選取**user.mail**為**使用者識別碼**和每個資料列所示hello 在表中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="75b82-167">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="75b82-168">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="75b82-168">Attribute Name</span></span> | <span data-ttu-id="75b82-169">屬性值</span><span class="sxs-lookup"><span data-stu-id="75b82-169">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="75b82-170">電子郵件</span><span class="sxs-lookup"><span data-stu-id="75b82-170">email</span></span> | <span data-ttu-id="75b82-171">user.mail</span><span class="sxs-lookup"><span data-stu-id="75b82-171">user.mail</span></span> |
    | <span data-ttu-id="75b82-172">名稱</span><span class="sxs-lookup"><span data-stu-id="75b82-172">name</span></span> | <span data-ttu-id="75b82-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="75b82-173">user.displayname</span></span> |
    | <span data-ttu-id="75b82-174">first_name</span><span class="sxs-lookup"><span data-stu-id="75b82-174">first_name</span></span> | <span data-ttu-id="75b82-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="75b82-175">user.givenname</span></span> |
    | <span data-ttu-id="75b82-176">last_name</span><span class="sxs-lookup"><span data-stu-id="75b82-176">last_name</span></span> | <span data-ttu-id="75b82-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="75b82-177">user.surname</span></span> |

    <span data-ttu-id="75b82-178">a.</span><span class="sxs-lookup"><span data-stu-id="75b82-178">a.</span></span> <span data-ttu-id="75b82-179">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="75b82-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![<span data-ttu-id="75b82-180">設定新增</span><span class="sxs-lookup"><span data-stu-id="75b82-180">Configure Add</span></span> ](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_04.png)

    ![設定屬性](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="75b82-182">b.</span><span class="sxs-lookup"><span data-stu-id="75b82-182">b.</span></span> <span data-ttu-id="75b82-183">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="75b82-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="75b82-184">c.</span><span class="sxs-lookup"><span data-stu-id="75b82-184">c.</span></span> <span data-ttu-id="75b82-185">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="75b82-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="75b82-186">d.</span><span class="sxs-lookup"><span data-stu-id="75b82-186">d.</span></span> <span data-ttu-id="75b82-187">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="75b82-187">Click **Ok**</span></span>
 
6. <span data-ttu-id="75b82-188">在 hello **SAML 簽章憑證**區段，複製 hello**指紋**hello 憑證值。</span><span class="sxs-lookup"><span data-stu-id="75b82-188">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of hello certificate.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_certificate.png) 

7. <span data-ttu-id="75b82-190">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="75b82-190">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="75b82-192">在 hello **OfficeSpace 軟體組態**區段中，按一下**設定 OfficeSpace Software** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="75b82-192">On hello **OfficeSpace Software Configuration** section, click **Configure OfficeSpace Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="75b82-193">複製 hello**登出 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="75b82-193">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![OfficeSpace Software 設定](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_configure.png) 

9. <span data-ttu-id="75b82-195">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 OfficeSpace Software 租用戶。</span><span class="sxs-lookup"><span data-stu-id="75b82-195">In a different web browser window, log into your OfficeSpace Software tenant as an administrator.</span></span>

10. <span data-ttu-id="75b82-196">跳過**設定**按一下**連接器**。</span><span class="sxs-lookup"><span data-stu-id="75b82-196">Go too**Settings** and click **Connectors**.</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. <span data-ttu-id="75b82-198">按一下 [SAML 驗證]。</span><span class="sxs-lookup"><span data-stu-id="75b82-198">Click **SAML Authentication**.</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. <span data-ttu-id="75b82-200">在 hello **SAML 驗證**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="75b82-200">In hello **SAML Authentication** section, perform hello following steps:</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    <span data-ttu-id="75b82-202">a.</span><span class="sxs-lookup"><span data-stu-id="75b82-202">a.</span></span> <span data-ttu-id="75b82-203">在 hello**登出提供者 url**文字方塊中，貼上 hello 值**登出 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="75b82-203">In hello **Logout provider url** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="75b82-204">b.</span><span class="sxs-lookup"><span data-stu-id="75b82-204">b.</span></span> <span data-ttu-id="75b82-205">在 hello**用戶端 idp 目標 url**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="75b82-205">In hello **Client idp target url** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="75b82-206">c.</span><span class="sxs-lookup"><span data-stu-id="75b82-206">c.</span></span> <span data-ttu-id="75b82-207">貼上 hello**指紋**值，您從 Azure 入口網站複製到 hello**用戶端 IDP 憑證指紋**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="75b82-207">Paste hello **Thumbprint** value which you have copied from Azure portal, into hello **Client IDP certificate fingerprint** textbox.</span></span> 

    <span data-ttu-id="75b82-208">d.</span><span class="sxs-lookup"><span data-stu-id="75b82-208">d.</span></span> <span data-ttu-id="75b82-209">按一下 [儲存設定] 。</span><span class="sxs-lookup"><span data-stu-id="75b82-209">Click **Save Settings**.</span></span>


> [!TIP]
> <span data-ttu-id="75b82-210">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="75b82-210">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="75b82-211">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="75b82-211">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="75b82-212">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="75b82-212">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="75b82-213">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="75b82-213">Create an Azure AD test user</span></span>

<span data-ttu-id="75b82-214">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="75b82-214">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="75b82-216">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="75b82-216">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="75b82-217">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="75b82-217">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-officespace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="75b82-219">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="75b82-219">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-officespace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="75b82-221">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="75b82-221">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-officespace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="75b82-223">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="75b82-223">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-officespace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="75b82-225">a.</span><span class="sxs-lookup"><span data-stu-id="75b82-225">a.</span></span> <span data-ttu-id="75b82-226">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="75b82-226">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="75b82-227">b.</span><span class="sxs-lookup"><span data-stu-id="75b82-227">b.</span></span> <span data-ttu-id="75b82-228">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="75b82-228">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="75b82-229">c.</span><span class="sxs-lookup"><span data-stu-id="75b82-229">c.</span></span> <span data-ttu-id="75b82-230">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="75b82-230">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="75b82-231">d.</span><span class="sxs-lookup"><span data-stu-id="75b82-231">d.</span></span> <span data-ttu-id="75b82-232">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="75b82-232">Click **Create**.</span></span>
 
### <a name="create-a-officespace-software-test-user"></a><span data-ttu-id="75b82-233">建立 OfficeSpace Software 測試使用者</span><span class="sxs-lookup"><span data-stu-id="75b82-233">Create a OfficeSpace Software test user</span></span>

<span data-ttu-id="75b82-234">hello 本節目標在於 toocreate 呼叫許 Simon OfficeSpace Software 中的使用者。</span><span class="sxs-lookup"><span data-stu-id="75b82-234">hello objective of this section is toocreate a user called Britta Simon in OfficeSpace Software.</span></span> <span data-ttu-id="75b82-235">OfficeSpace Software 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="75b82-235">OfficeSpace Software supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="75b82-236">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="75b82-236">There is no action item for you in this section.</span></span> <span data-ttu-id="75b82-237">如果尚未存在，將會建立新使用者期間嘗試 tooaccess OfficeSpace Software。</span><span class="sxs-lookup"><span data-stu-id="75b82-237">A new user will be created during an attempt tooaccess OfficeSpace Software if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="75b82-238">若要手動 toocreate 使用者，您需要 tooContact [OfficeSpace Software 支援小組](mailto:support@officespacesoftware.com)。</span><span class="sxs-lookup"><span data-stu-id="75b82-238">If you need toocreate an user manually, you need tooContact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="75b82-239">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="75b82-239">Assign hello Azure AD test user</span></span>

<span data-ttu-id="75b82-240">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooOfficeSpace 軟體。</span><span class="sxs-lookup"><span data-stu-id="75b82-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOfficeSpace Software.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="75b82-242">**tooassign 許 Simon tooOfficeSpace 軟體，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="75b82-242">**tooassign Britta Simon tooOfficeSpace Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="75b82-243">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="75b82-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="75b82-245">在 [hello] 應用程式清單中，選取**OfficeSpace Software**。</span><span class="sxs-lookup"><span data-stu-id="75b82-245">In hello applications list, select **OfficeSpace Software**.</span></span>

    ![hello OfficeSpace Software hello 應用程式清單中的連結](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_app.png)  

3. <span data-ttu-id="75b82-247">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="75b82-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="75b82-249">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="75b82-249">Click **Add** button.</span></span> <span data-ttu-id="75b82-250">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="75b82-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="75b82-252">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="75b82-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="75b82-253">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="75b82-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="75b82-254">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="75b82-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="75b82-255">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="75b82-255">Test single sign-on</span></span>

<span data-ttu-id="75b82-256">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="75b82-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="75b82-257">當您按一下的 hello OfficeSpace Software 磚 hello 存取面板中時，您應該取得自動登入 tooyour OfficeSpace Software 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="75b82-257">When you click hello OfficeSpace Software tile in hello Access Panel, you should get automatically signed-on tooyour OfficeSpace Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="75b82-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="75b82-258">Additional resources</span></span>

* [<span data-ttu-id="75b82-259">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="75b82-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="75b82-260">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="75b82-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_203.png


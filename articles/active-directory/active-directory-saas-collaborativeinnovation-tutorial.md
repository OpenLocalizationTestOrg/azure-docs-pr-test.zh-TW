---
title: "教學課程：Azure Active Directory 與 Collaborative Innovation 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與共同作業的創新之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bba95df3-75a4-4a93-8805-b3a8aa3d4861
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: e85fabfe11a380129f319a101aa7c7a9491260f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-collaborative-innovation"></a><span data-ttu-id="1820e-103">教學課程：Azure Active Directory 與 Collaborative Innovation 整合</span><span class="sxs-lookup"><span data-stu-id="1820e-103">Tutorial: Azure Active Directory integration with Collaborative Innovation</span></span>

<span data-ttu-id="1820e-104">在此教學課程中，您學會如何 toointegrate 與 Azure Active Directory (Azure AD) 的共同作業創新。</span><span class="sxs-lookup"><span data-stu-id="1820e-104">In this tutorial, you learn how toointegrate Collaborative Innovation with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1820e-105">整合與 Azure AD 的共同作業的創新可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="1820e-105">Integrating Collaborative Innovation with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1820e-106">您可以控制存取 tooCollaborative 創新的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="1820e-106">You can control in Azure AD who has access tooCollaborative Innovation</span></span>
- <span data-ttu-id="1820e-107">您可以啟用您的使用者 tooautomatically get 登入 tooCollaborative 創新 （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="1820e-107">You can enable your users tooautomatically get signed-on tooCollaborative Innovation (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1820e-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="1820e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1820e-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="1820e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1820e-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1820e-110">Prerequisites</span></span>

<span data-ttu-id="1820e-111">tooconfigure 與共同作業的創新的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="1820e-111">tooconfigure Azure AD integration with Collaborative Innovation, you need hello following items:</span></span>

- <span data-ttu-id="1820e-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1820e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1820e-113">已啟用 Collaborative Innovation 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1820e-113">A Collaborative Innovation single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1820e-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="1820e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1820e-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="1820e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1820e-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1820e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1820e-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="1820e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1820e-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="1820e-118">Scenario description</span></span>
<span data-ttu-id="1820e-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1820e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1820e-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="1820e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1820e-121">加入共同作業的創新從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="1820e-121">Adding Collaborative Innovation from hello gallery</span></span>
2. <span data-ttu-id="1820e-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1820e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-collaborative-innovation-from-hello-gallery"></a><span data-ttu-id="1820e-123">加入共同作業的創新從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="1820e-123">Adding Collaborative Innovation from hello gallery</span></span>
<span data-ttu-id="1820e-124">tooconfigure hello 整合共同作業的創新到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd 共同作業的創新。</span><span class="sxs-lookup"><span data-stu-id="1820e-124">tooconfigure hello integration of Collaborative Innovation into Azure AD, you need tooadd Collaborative Innovation from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1820e-125">**tooadd hello 庫、 共同作業的創新執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1820e-125">**tooadd Collaborative Innovation from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1820e-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="1820e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1820e-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1820e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1820e-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1820e-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="1820e-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="1820e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="1820e-133">在 [hello] 搜尋方塊中，輸入**共同作業的創新**。</span><span class="sxs-lookup"><span data-stu-id="1820e-133">In hello search box, type **Collaborative Innovation**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_search.png)

5. <span data-ttu-id="1820e-135">在 [hello [結果] 窗格中，選取 [**共同作業的創新**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1820e-135">In hello results panel, select **Collaborative Innovation**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1820e-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1820e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1820e-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Collaborative Innovation 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1820e-138">In this section, you configure and test Azure AD single sign-on with Collaborative Innovation based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1820e-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在共同作業的創新是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="1820e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Collaborative Innovation is tooa user in Azure AD.</span></span> <span data-ttu-id="1820e-140">換句話說，Azure AD 使用者與 hello 中共同作業的創新的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="1820e-140">In other words, a link relationship between an Azure AD user and hello related user in Collaborative Innovation needs toobe established.</span></span>

<span data-ttu-id="1820e-141">在共同作業的創新，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1820e-141">In Collaborative Innovation, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1820e-142">tooconfigure 及測試 Azure AD 單一登入與共同作業的創新，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="1820e-142">tooconfigure and test Azure AD single sign-on with Collaborative Innovation, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1820e-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="1820e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1820e-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="1820e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1820e-145">**[建立測試使用者共同作業的創新](#creating-a-collaborative-innovation-test-user)** -toohave 中共同作業是表示連結的 toohello Azure AD 使用者的創新許 Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="1820e-145">**[Creating a Collaborative Innovation test user](#creating-a-collaborative-innovation-test-user)** - toohave a counterpart of Britta Simon in Collaborative Innovation that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1820e-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1820e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1820e-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="1820e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1820e-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1820e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1820e-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並共同作業的創新應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="1820e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Collaborative Innovation application.</span></span>

<span data-ttu-id="1820e-150">**tooconfigure Azure AD 單一登入與共同作業的創新，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1820e-150">**tooconfigure Azure AD single sign-on with Collaborative Innovation, perform hello following steps:**</span></span>

1. <span data-ttu-id="1820e-151">在 Azure 入口網站上 hello hello**共同作業的創新**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="1820e-151">In hello Azure portal, on hello **Collaborative Innovation** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="1820e-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1820e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_samlbase.png)

3. <span data-ttu-id="1820e-155">在 [hello**共同作業的創新網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1820e-155">On hello **Collaborative Innovation Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_url.png)

    <span data-ttu-id="1820e-157">a.</span><span class="sxs-lookup"><span data-stu-id="1820e-157">a.</span></span> <span data-ttu-id="1820e-158">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<instancename>.foundry.<companyname>.com/`</span><span class="sxs-lookup"><span data-stu-id="1820e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.foundry.<companyname>.com/`</span></span>

    <span data-ttu-id="1820e-159">b.</span><span class="sxs-lookup"><span data-stu-id="1820e-159">b.</span></span> <span data-ttu-id="1820e-160">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<instancename>.foundry.<companyname>.com`</span><span class="sxs-lookup"><span data-stu-id="1820e-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.foundry.<companyname>.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="1820e-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="1820e-161">These values are not real.</span></span> <span data-ttu-id="1820e-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="1820e-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1820e-163">請連絡[共同作業的創新用戶端支援小組](https://www.unilever.com/contact/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="1820e-163">Contact [Collaborative Innovation Client support team](https://www.unilever.com/contact/) tooget these values.</span></span>  

4. <span data-ttu-id="1820e-164">共同作業的創新應用程式預期 hello SAML 判斷提示，以特定格式。</span><span class="sxs-lookup"><span data-stu-id="1820e-164">Collaborative Innovation application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="1820e-165">請設定下列宣告為此應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="1820e-165">Please configure hello following claims for this application.</span></span> <span data-ttu-id="1820e-166">您可以從 hello 管理 hello 這些屬性的值"**使用者屬性**」 一節，在應用程式整合頁面上。</span><span class="sxs-lookup"><span data-stu-id="1820e-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="1820e-167">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="1820e-167">hello following screenshot shows an example for this.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/attribute.png)
    
5. <span data-ttu-id="1820e-169">按一下**檢視和編輯所有其他使用者屬性**核取方塊在 hello**使用者屬性**區段 tooexpand hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="1820e-169">Click **View and edit all other user attributes** checkbox in hello **User Attributes** section tooexpand hello attributes.</span></span> <span data-ttu-id="1820e-170">執行下列步驟，在每個顯示 hello 屬性-hello</span><span class="sxs-lookup"><span data-stu-id="1820e-170">Perform hello following steps on each of hello displayed attributes-</span></span>

    | <span data-ttu-id="1820e-171">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="1820e-171">Attribute Name</span></span> | <span data-ttu-id="1820e-172">屬性值</span><span class="sxs-lookup"><span data-stu-id="1820e-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="1820e-173">givenname</span><span class="sxs-lookup"><span data-stu-id="1820e-173">givenname</span></span> | <span data-ttu-id="1820e-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="1820e-174">user.givenname</span></span> |
    | <span data-ttu-id="1820e-175">surname</span><span class="sxs-lookup"><span data-stu-id="1820e-175">surname</span></span> | <span data-ttu-id="1820e-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="1820e-176">user.surname</span></span> |
    | <span data-ttu-id="1820e-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="1820e-177">emailaddress</span></span> | <span data-ttu-id="1820e-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="1820e-178">user.userprincipalname</span></span> |
    | <span data-ttu-id="1820e-179">名稱</span><span class="sxs-lookup"><span data-stu-id="1820e-179">name</span></span> | <span data-ttu-id="1820e-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="1820e-180">user.userprincipalname</span></span> |

    <span data-ttu-id="1820e-181">a.</span><span class="sxs-lookup"><span data-stu-id="1820e-181">a.</span></span> <span data-ttu-id="1820e-182">按一下 hello 屬性 tooopen hello**編輯屬性**視窗。</span><span class="sxs-lookup"><span data-stu-id="1820e-182">Click hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/url_update.png)

    <span data-ttu-id="1820e-184">b.</span><span class="sxs-lookup"><span data-stu-id="1820e-184">b.</span></span> <span data-ttu-id="1820e-185">從 hello 刪除 hello URL 值**命名空間**。</span><span class="sxs-lookup"><span data-stu-id="1820e-185">Delete hello URL value from hello **Namespace**.</span></span>
    
    <span data-ttu-id="1820e-186">c.</span><span class="sxs-lookup"><span data-stu-id="1820e-186">c.</span></span> <span data-ttu-id="1820e-187">按一下**確定**toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="1820e-187">Click **Ok** toosave hello setting.</span></span>

6. <span data-ttu-id="1820e-188">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="1820e-188">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_certificate.png) 

7. <span data-ttu-id="1820e-190">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="1820e-190">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="1820e-192">tooconfigure 單一登入上**共同作業的創新**端，您需要下載 toosend hello**中繼資料 XML**太[共同作業的創新技術支援小組](https://www.unilever.com/contact/)。</span><span class="sxs-lookup"><span data-stu-id="1820e-192">tooconfigure single sign-on on **Collaborative Innovation** side, you need toosend hello downloaded **Metadata XML** too[Collaborative Innovation support team](https://www.unilever.com/contact/).</span></span> <span data-ttu-id="1820e-193">設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。</span><span class="sxs-lookup"><span data-stu-id="1820e-193">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1820e-194">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="1820e-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1820e-195">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="1820e-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1820e-196">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1820e-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1820e-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1820e-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="1820e-198">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="1820e-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="1820e-200">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1820e-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1820e-201">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="1820e-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1820e-203">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="1820e-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1820e-205">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="1820e-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1820e-207">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1820e-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1820e-209">a.</span><span class="sxs-lookup"><span data-stu-id="1820e-209">a.</span></span> <span data-ttu-id="1820e-210">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="1820e-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1820e-211">b.</span><span class="sxs-lookup"><span data-stu-id="1820e-211">b.</span></span> <span data-ttu-id="1820e-212">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="1820e-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1820e-213">c.</span><span class="sxs-lookup"><span data-stu-id="1820e-213">c.</span></span> <span data-ttu-id="1820e-214">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="1820e-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1820e-215">d.</span><span class="sxs-lookup"><span data-stu-id="1820e-215">d.</span></span> <span data-ttu-id="1820e-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1820e-216">Click **Create**.</span></span>
 
### <a name="creating-a-collaborative-innovation-test-user"></a><span data-ttu-id="1820e-217">建立 Collaborative Innovation 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1820e-217">Creating a Collaborative Innovation test user</span></span>

<span data-ttu-id="1820e-218">tooenable Azure AD 使用者 toolog 中 tooCollaborative 創新，它們必須佈建到共同作業的創新。</span><span class="sxs-lookup"><span data-stu-id="1820e-218">tooenable Azure AD users toolog in tooCollaborative Innovation, they must be provisioned into Collaborative Innovation.</span></span>  

<span data-ttu-id="1820e-219">如果此應用程式佈建為自動 hello 應用程式支援即時使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="1820e-219">In case of this application provisioning is automatic as hello application supports just in time user provisioning.</span></span> <span data-ttu-id="1820e-220">因此會有任何需要 tooperform 這裡所有步驟。</span><span class="sxs-lookup"><span data-stu-id="1820e-220">So there is no need tooperform any steps here.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1820e-221">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="1820e-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1820e-222">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooCollaborative 創新。</span><span class="sxs-lookup"><span data-stu-id="1820e-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCollaborative Innovation.</span></span>

![指派使用者][200] 

<span data-ttu-id="1820e-224">**tooassign 許 Simon tooCollaborative 創新，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1820e-224">**tooassign Britta Simon tooCollaborative Innovation, perform hello following steps:**</span></span>

1. <span data-ttu-id="1820e-225">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1820e-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="1820e-227">在 [hello] 應用程式清單中，選取**共同作業的創新**。</span><span class="sxs-lookup"><span data-stu-id="1820e-227">In hello applications list, select **Collaborative Innovation**.</span></span>

    ![設定單一登入](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_app.png) 

3. <span data-ttu-id="1820e-229">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="1820e-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="1820e-231">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1820e-231">Click **Add** button.</span></span> <span data-ttu-id="1820e-232">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1820e-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="1820e-234">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="1820e-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1820e-235">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1820e-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1820e-236">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1820e-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1820e-237">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="1820e-237">Testing single sign-on</span></span>

<span data-ttu-id="1820e-238">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="1820e-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1820e-239">當您按一下 hello 共同作業的創新磚 hello 存取面板中時，您應該取得共同作業的創新應用程式的登入的頁面。</span><span class="sxs-lookup"><span data-stu-id="1820e-239">When you click hello Collaborative Innovation tile in hello Access Panel, you should get login page of Collaborative Innovation application.</span></span>
<span data-ttu-id="1820e-240">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="1820e-240">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1820e-241">其他資源</span><span class="sxs-lookup"><span data-stu-id="1820e-241">Additional resources</span></span>

* [<span data-ttu-id="1820e-242">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1820e-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1820e-243">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="1820e-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_203.png


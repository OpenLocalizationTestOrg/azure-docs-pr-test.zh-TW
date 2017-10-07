---
title: "教學課程：Azure Active Directory 與 Cloud Management Portal for Microsoft Azure 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Microsoft Azure 的雲端管理入口網站之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4ea9f47c-25ca-42b0-a878-9e7aa6f34973
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9596826e3dc1289b95009bf01ec8b86f823ef345
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloud-management-portal-for-microsoft-azure"></a><span data-ttu-id="3fdfc-103">教學課程：Azure Active Directory 與 Cloud Management Portal for Microsoft Azure 整合</span><span class="sxs-lookup"><span data-stu-id="3fdfc-103">Tutorial: Azure Active Directory integration with Cloud Management Portal for Microsoft Azure</span></span>

<span data-ttu-id="3fdfc-104">在此教學課程中，您學會如何 toointegrate 雲端與 Azure Active Directory (Azure AD) 的 Microsoft azure 的管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-104">In this tutorial, you learn how toointegrate Cloud Management Portal for Microsoft Azure with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3fdfc-105">與 Azure AD 整合 Microsoft Azure 的雲端管理入口網站可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="3fdfc-105">Integrating Cloud Management Portal for Microsoft Azure with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3fdfc-106">您可以控制存取 tooCloud Microsoft Azure 管理入口網站的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="3fdfc-106">You can control in Azure AD who has access tooCloud Management Portal for Microsoft Azure</span></span>
- <span data-ttu-id="3fdfc-107">您可以啟用您的使用者 tooautomatically get 登入 tooCloud （單一登入） 的 Microsoft Azure 管理入口網站使用其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="3fdfc-107">You can enable your users tooautomatically get signed-on tooCloud Management Portal for Microsoft Azure (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3fdfc-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="3fdfc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3fdfc-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fdfc-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="3fdfc-110">Prerequisites</span></span>

<span data-ttu-id="3fdfc-111">tooconfigure 與 Microsoft Azure 的雲端管理入口網站的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="3fdfc-111">tooconfigure Azure AD integration with Cloud Management Portal for Microsoft Azure, you need hello following items:</span></span>

- <span data-ttu-id="3fdfc-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3fdfc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3fdfc-113">已啟用 Cloud Management Portal for Microsoft Azure 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3fdfc-113">A Cloud Management Portal for Microsoft Azure single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3fdfc-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3fdfc-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="3fdfc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3fdfc-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3fdfc-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3fdfc-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="3fdfc-118">Scenario description</span></span>
<span data-ttu-id="3fdfc-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3fdfc-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="3fdfc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3fdfc-121">新增 Microsoft Azure 的雲端管理入口網站從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="3fdfc-121">Adding Cloud Management Portal for Microsoft Azure from hello gallery</span></span>
2. <span data-ttu-id="3fdfc-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3fdfc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloud-management-portal-for-microsoft-azure-from-hello-gallery"></a><span data-ttu-id="3fdfc-123">新增 Microsoft Azure 的雲端管理入口網站從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="3fdfc-123">Adding Cloud Management Portal for Microsoft Azure from hello gallery</span></span>
<span data-ttu-id="3fdfc-124">tooconfigure hello 整合 Microsoft Azure 的雲端管理入口網站至 Azure AD，您需要 tooadd 雲端管理入口網站的 Microsoft Azure hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-124">tooconfigure hello integration of Cloud Management Portal for Microsoft Azure into Azure AD, you need tooadd Cloud Management Portal for Microsoft Azure from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3fdfc-125">**tooadd hello 圖庫中，從 Microsoft Azure 的雲端管理入口網站執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3fdfc-125">**tooadd Cloud Management Portal for Microsoft Azure from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3fdfc-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3fdfc-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3fdfc-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="3fdfc-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="3fdfc-133">在 [hello] 搜尋方塊中，輸入**雲端的 Microsoft Azure 的管理入口網站**。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-133">In hello search box, type **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_search.png)

5. <span data-ttu-id="3fdfc-135">在 hello 結果 窗格中，選取**雲端的 Microsoft Azure 的管理入口網站**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-135">In hello results panel, select **Cloud Management Portal for Microsoft Azure**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3fdfc-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3fdfc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3fdfc-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Cloud Management Portal for Microsoft Azure 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-138">In this section, you configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3fdfc-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Microsoft Azure 的雲端管理入口網站中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cloud Management Portal for Microsoft Azure is tooa user in Azure AD.</span></span> <span data-ttu-id="3fdfc-140">換句話說，Azure AD 使用者和 Microsoft azure 雲端管理入口網站中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-140">In other words, a link relationship between an Azure AD user and hello related user in Cloud Management Portal for Microsoft Azure needs toobe established.</span></span>

<span data-ttu-id="3fdfc-141">在 Microsoft Azure 的雲端管理入口網站指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-141">In Cloud Management Portal for Microsoft Azure, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3fdfc-142">tooconfigure 及測試 Azure AD 單一登入雲端管理入口網站與 Microsoft azure，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="3fdfc-142">tooconfigure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3fdfc-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3fdfc-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3fdfc-145">**[建立 Microsoft Azure 測試使用者雲端管理入口網站](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)** -toohave 許 Simon 雲端是表示連結的 toohello Azure AD 使用者的 Microsoft Azure 管理入口網站中的對應項目。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-145">**[Creating a Cloud Management Portal for Microsoft Azure test user](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)** - toohave a counterpart of Britta Simon in Cloud Management Portal for Microsoft Azure that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3fdfc-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3fdfc-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3fdfc-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3fdfc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3fdfc-149">在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Microsoft Azure 應用程式中您雲端的管理入口網站中。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="3fdfc-150">**Microsoft Azure 的雲端管理入口網站與 Azure AD 單一登入 tooconfigure 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3fdfc-150">**tooconfigure Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, perform hello following steps:**</span></span>

1. <span data-ttu-id="3fdfc-151">在 Azure 入口網站上 hello hello**雲端的 Microsoft Azure 的管理入口網站**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-151">In hello Azure portal, on hello **Cloud Management Portal for Microsoft Azure** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="3fdfc-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_samlbase.png)

3. <span data-ttu-id="3fdfc-155">在 hello**雲端管理入口網站，Microsoft Azure 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3fdfc-155">On hello **Cloud Management Portal for Microsoft Azure Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_url.png)

    <span data-ttu-id="3fdfc-157">a.</span><span class="sxs-lookup"><span data-stu-id="3fdfc-157">a.</span></span> <span data-ttu-id="3fdfc-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列的 hello 模式：</span><span class="sxs-lookup"><span data-stu-id="3fdfc-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://portal.newsignature.com/<instancename>` |   
    | `https://portal.igcm.com/<instancename>` |
    
    <span data-ttu-id="3fdfc-159">b.</span><span class="sxs-lookup"><span data-stu-id="3fdfc-159">b.</span></span> <span data-ttu-id="3fdfc-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列的 hello 模式：</span><span class="sxs-lookup"><span data-stu-id="3fdfc-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com` |
    | `https://<subdomain>.newsignature.com` |

    <span data-ttu-id="3fdfc-161">c.</span><span class="sxs-lookup"><span data-stu-id="3fdfc-161">c.</span></span> <span data-ttu-id="3fdfc-162">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列的 hello 模式：</span><span class="sxs-lookup"><span data-stu-id="3fdfc-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com/<instancename>` |
    | `https://<subdomain>.newsignature.com` |
    | `https://<subdomain>.newsignature.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="3fdfc-163">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-163">These values are not real.</span></span> <span data-ttu-id="3fdfc-164">更新這些值與 hello 實際的登入 URL、 識別碼及回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-164">Update these values with hello actual Sign-On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="3fdfc-165">請連絡[雲端管理入口網站的 Microsoft Azure 用戶端支援小組](mailto:jczernuszka@newsignature.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-165">Contact [Cloud Management Portal for Microsoft Azure Client support team](mailto:jczernuszka@newsignature.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="3fdfc-166">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_certificate.png) 

5. <span data-ttu-id="3fdfc-168">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-168">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-newsignature-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3fdfc-170">在 hello **Microsoft Azure 組態的雲端管理入口網站**區段中，按一下**Microsoft azure 中設定雲端管理入口網站**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-170">On hello **Cloud Management Portal for Microsoft Azure Configuration** section, click **Configure Cloud Management Portal for Microsoft Azure** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3fdfc-171">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="3fdfc-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_configure.png) 

7. <span data-ttu-id="3fdfc-173">tooconfigure 單一登入上**雲端的 Microsoft Azure 的管理入口網站**端，您需要下載 toosend hello**憑證**，**登出 URL**， **SAML 單一登入服務 URL**和**SAML 實體識別碼**太[雲端管理入口網站的 Microsoft Azure 支援小組](mailto:jczernuszka@newsignature.com)。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-173">tooconfigure single sign-on on **Cloud Management Portal for Microsoft Azure** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL**, **SAML Single Sign-On Service URL** and **SAML Entity ID** too[Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com).</span></span> <span data-ttu-id="3fdfc-174">設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-174">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3fdfc-175">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="3fdfc-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3fdfc-176">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3fdfc-177">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3fdfc-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3fdfc-178">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3fdfc-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="3fdfc-179">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="3fdfc-181">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3fdfc-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3fdfc-182">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-182">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-newsignature-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3fdfc-184">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-184">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-newsignature-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3fdfc-186">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-186">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-newsignature-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3fdfc-188">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="3fdfc-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-newsignature-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3fdfc-190">a.</span><span class="sxs-lookup"><span data-stu-id="3fdfc-190">a.</span></span> <span data-ttu-id="3fdfc-191">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-191">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3fdfc-192">b.</span><span class="sxs-lookup"><span data-stu-id="3fdfc-192">b.</span></span> <span data-ttu-id="3fdfc-193">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-193">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3fdfc-194">c.</span><span class="sxs-lookup"><span data-stu-id="3fdfc-194">c.</span></span> <span data-ttu-id="3fdfc-195">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3fdfc-196">d.</span><span class="sxs-lookup"><span data-stu-id="3fdfc-196">d.</span></span> <span data-ttu-id="3fdfc-197">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-197">Click **Create**.</span></span>
 
### <a name="creating-a-cloud-management-portal-for-microsoft-azure-test-user"></a><span data-ttu-id="3fdfc-198">建立 Cloud Management Portal for Microsoft Azure 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3fdfc-198">Creating a Cloud Management Portal for Microsoft Azure test user</span></span>

<span data-ttu-id="3fdfc-199">hello 本節目標在於 toocreate 許 Simon 呼叫雲端管理入口網站中，Microsoft azure 的使用者。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-199">hello objective of this section is toocreate a user called Britta Simon in Cloud Management Portal for Microsoft Azure.</span></span> <span data-ttu-id="3fdfc-200">請使用[雲端管理入口網站的 Microsoft Azure 支援小組](mailto:jczernuszka@newsignature.com)tooadd hello 使用者在 Microsoft Azure 帳戶的 hello 雲端管理入口網站中。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-200">Please work with [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com) tooadd hello users in hello Cloud Management Portal for Microsoft Azure account.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3fdfc-201">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="3fdfc-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3fdfc-202">在本節中，您可以授與存取 tooCloud Microsoft Azure 管理入口網站啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCloud Management Portal for Microsoft Azure.</span></span>

![指派使用者][200] 

<span data-ttu-id="3fdfc-204">**tooassign 許 Simon tooCloud Microsoft Azure 管理入口網站執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="3fdfc-204">**tooassign Britta Simon tooCloud Management Portal for Microsoft Azure, perform hello following steps:**</span></span>

1. <span data-ttu-id="3fdfc-205">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="3fdfc-207">在 [hello] 應用程式清單中，選取**雲端的 Microsoft Azure 的管理入口網站**。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-207">In hello applications list, select **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![設定單一登入](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_app.png) 

3. <span data-ttu-id="3fdfc-209">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="3fdfc-211">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-211">Click **Add** button.</span></span> <span data-ttu-id="3fdfc-212">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="3fdfc-214">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3fdfc-215">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3fdfc-216">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3fdfc-217">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="3fdfc-217">Testing single sign-on</span></span>

<span data-ttu-id="3fdfc-218">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-218">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="3fdfc-219">當您按一下 Microsoft Azure 磚 hello 存取面板中的 hello 雲端管理入口網站時，您應該取得 Microsoft Azure 應用程式的自動登入 tooyour 雲端管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-219">When you click hello Cloud Management Portal for Microsoft Azure tile in hello Access Panel, you should get automatically signed-on tooyour Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="3fdfc-220">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="3fdfc-220">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3fdfc-221">其他資源</span><span class="sxs-lookup"><span data-stu-id="3fdfc-221">Additional resources</span></span>

* [<span data-ttu-id="3fdfc-222">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3fdfc-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3fdfc-223">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="3fdfc-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_203.png


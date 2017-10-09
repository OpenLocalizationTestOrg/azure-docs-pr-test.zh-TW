---
title: "教學課程：Azure Active Directory 與 Five9 Plus Adapter 整合 (CTI，Contact Center Agents) | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Five9 加上介面卡 （CTI，請連絡 Center 代理程式） 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: 2e3ea8b5f2a6eaa8ad17d39e03fa490038b14561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a><span data-ttu-id="24259-103">教學課程：Azure Active Directory 與 Five9 Plus Adapter 整合 (CTI，Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="24259-103">Tutorial: Azure Active Directory integration with Five9 Plus Adapter (CTI, Contact Center Agents)</span></span>

<span data-ttu-id="24259-104">在此教學課程中，您學會如何 toointegrate Five9 加上介面卡 （CTI，請連絡 Center 代理程式） 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="24259-104">In this tutorial, you learn how toointegrate Five9 Plus Adapter (CTI, Contact Center Agents) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="24259-105">與 Azure AD 整合 Five9 加上介面卡 （CTI，請連絡 Center 代理程式） 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="24259-105">Integrating Five9 Plus Adapter (CTI, Contact Center Agents) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="24259-106">您可以控制存取 tooFive9 Azure AD，加上介面卡 （CTI，請連絡 Center 代理程式）</span><span class="sxs-lookup"><span data-stu-id="24259-106">You can control in Azure AD who has access tooFive9 Plus Adapter (CTI, Contact Center Agents)</span></span>
- <span data-ttu-id="24259-107">您可以啟用使用者 tooautomatically get 登入 tooFive9 再加上介面卡 （CTI，請連絡 Center 代理程式） （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="24259-107">You can enable your users tooautomatically get signed-on tooFive9 Plus Adapter (CTI, Contact Center Agents) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="24259-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="24259-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="24259-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="24259-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24259-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="24259-110">Prerequisites</span></span>

<span data-ttu-id="24259-111">tooconfigure Azure AD 整合與 Five9 加上介面卡 (CTI，請連絡 Center 代理程式)，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="24259-111">tooconfigure Azure AD integration with Five9 Plus Adapter (CTI, Contact Center Agents), you need hello following items:</span></span>

- <span data-ttu-id="24259-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="24259-112">An Azure AD subscription</span></span>
- <span data-ttu-id="24259-113">已啟用 Five9 Plus Adapter (CTI，Contact Center Agents) 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="24259-113">A Five9 Plus Adapter (CTI, Contact Center Agents) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="24259-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="24259-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="24259-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="24259-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="24259-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="24259-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="24259-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="24259-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="24259-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="24259-118">Scenario description</span></span>
<span data-ttu-id="24259-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="24259-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="24259-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="24259-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="24259-121">從 hello 圖庫加入 Five9 加上介面卡 （CTI，請連絡 Center 代理程式）</span><span class="sxs-lookup"><span data-stu-id="24259-121">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery</span></span>
2. <span data-ttu-id="24259-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="24259-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-hello-gallery"></a><span data-ttu-id="24259-123">從 hello 圖庫加入 Five9 加上介面卡 （CTI，請連絡 Center 代理程式）</span><span class="sxs-lookup"><span data-stu-id="24259-123">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery</span></span>
<span data-ttu-id="24259-124">tooconfigure hello 整合 Five9 加上介面卡 （CTI，請連絡 Center 代理程式） 到 Azure AD，您會需要 tooadd Five9 加上介面卡 （CTI，請連絡 Center 代理程式） 從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單。</span><span class="sxs-lookup"><span data-stu-id="24259-124">tooconfigure hello integration of Five9 Plus Adapter (CTI, Contact Center Agents) into Azure AD, you need tooadd Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="24259-125">**tooadd Five9 加上介面卡 （CTI，請連絡 Center 代理程式） 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="24259-125">**tooadd Five9 Plus Adapter (CTI, Contact Center Agents) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="24259-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="24259-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="24259-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="24259-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="24259-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="24259-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="24259-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="24259-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="24259-133">在 [hello] 搜尋方塊中，輸入**Five9 加上介面卡 （CTI，請連絡 Center 代理程式）**。</span><span class="sxs-lookup"><span data-stu-id="24259-133">In hello search box, type **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-five9-tutorial/tutorial_five9_search.png)

5. <span data-ttu-id="24259-135">在 hello 結果 窗格中，選取  **Five9 加上介面卡 （CTI，請連絡 Center 代理程式）**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24259-135">In hello results panel, select **Five9 Plus Adapter (CTI, Contact Center Agents)**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="24259-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="24259-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="24259-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Five9 Plus Adapter (CTI，Contact Center Agents) 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="24259-138">In this section, you configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="24259-139">單一登入 toowork，Azure AD 需要 tooknow Five9 加上介面卡 （CTI，請連絡 Center 代理程式） 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="24259-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Five9 Plus Adapter (CTI, Contact Center Agents) is tooa user in Azure AD.</span></span> <span data-ttu-id="24259-140">換句話說，Azure AD 使用者與 hello Five9 加上介面卡 （CTI，請連絡 Center 代理程式） 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="24259-140">In other words, a link relationship between an Azure AD user and hello related user in Five9 Plus Adapter (CTI, Contact Center Agents) needs toobe established.</span></span>

<span data-ttu-id="24259-141">在 Five9 加上介面卡 （CTI，請連絡 Center 代理程式），將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="24259-141">In Five9 Plus Adapter (CTI, Contact Center Agents), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="24259-142">tooconfigure 和測試 Azure AD 單一登入與 Five9 加上介面卡 (CTI，請連絡 Center 代理程式)，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="24259-142">tooconfigure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="24259-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="24259-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="24259-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="24259-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="24259-145">**[建立 Five9 加上介面卡 （CTI，請連絡 Center 代理程式） 的測試使用者](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)** -toohave 許 Simon Five9 加上介面卡 （CTI，請連絡 Center 代理程式） 是連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="24259-145">**[Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)** - toohave a counterpart of Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="24259-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="24259-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="24259-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="24259-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="24259-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="24259-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="24259-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Five9 加上介面卡 （CTI，請連絡 Center 代理程式） 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="24259-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>

<span data-ttu-id="24259-150">**tooconfigure Azure AD 單一登入與 Five9 加上介面卡 （CTI，請連絡 Center 代理程式），執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="24259-150">**tooconfigure Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), perform hello following steps:**</span></span>

1. <span data-ttu-id="24259-151">在 Azure 入口網站上 hello hello **Five9 加上介面卡 （CTI，請連絡 Center 代理程式）**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="24259-151">In hello Azure portal, on hello **Five9 Plus Adapter (CTI, Contact Center Agents)** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="24259-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="24259-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-five9-tutorial/tutorial_five9_samlbase.png)

3. <span data-ttu-id="24259-155">在 hello **Five9 加上介面卡 （CTI，請連絡 Center 代理程式） 的網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="24259-155">On hello **Five9 Plus Adapter (CTI, Contact Center Agents) Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-five9-tutorial/tutorial_five9_url.png)
    
    <span data-ttu-id="24259-157">a.</span><span class="sxs-lookup"><span data-stu-id="24259-157">a.</span></span> <span data-ttu-id="24259-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列的 hello 模式：</span><span class="sxs-lookup"><span data-stu-id="24259-158">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>

    |    <span data-ttu-id="24259-159">Environment</span><span class="sxs-lookup"><span data-stu-id="24259-159">Environment</span></span>      |       <span data-ttu-id="24259-160">URL</span><span class="sxs-lookup"><span data-stu-id="24259-160">URL</span></span>      |
    | :-- | :-- |
    | <span data-ttu-id="24259-161">針對「Five9 Plus Adapter for Microsoft Dynamics CRM」</span><span class="sxs-lookup"><span data-stu-id="24259-161">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | <span data-ttu-id="24259-162">針對「Five9 Plus Adapter for Zendesk」</span><span class="sxs-lookup"><span data-stu-id="24259-162">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | <span data-ttu-id="24259-163">針對「Five9 Plus Adapter for Agent Desktop Toolkit」</span><span class="sxs-lookup"><span data-stu-id="24259-163">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    <span data-ttu-id="24259-164">b.</span><span class="sxs-lookup"><span data-stu-id="24259-164">b.</span></span> <span data-ttu-id="24259-165">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="24259-165">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>

    |      <span data-ttu-id="24259-166">Environment</span><span class="sxs-lookup"><span data-stu-id="24259-166">Environment</span></span>     |      <span data-ttu-id="24259-167">URL</span><span class="sxs-lookup"><span data-stu-id="24259-167">URL</span></span>      |
    | :--                  | :--           |
    | <span data-ttu-id="24259-168">針對「Five9 Plus Adapter for Microsoft Dynamics CRM」</span><span class="sxs-lookup"><span data-stu-id="24259-168">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | <span data-ttu-id="24259-169">針對「Five9 Plus Adapter for Zendesk」</span><span class="sxs-lookup"><span data-stu-id="24259-169">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | <span data-ttu-id="24259-170">針對「Five9 Plus Adapter for Agent Desktop Toolkit」</span><span class="sxs-lookup"><span data-stu-id="24259-170">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

4. <span data-ttu-id="24259-171">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="24259-171">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-five9-tutorial/tutorial_five9_certificate.png) 

5. <span data-ttu-id="24259-173">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="24259-173">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-five9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="24259-175">在 hello **Five9 加上介面卡 （CTI，請連絡 Center 代理程式） 設定**區段中，按一下**設定 Five9 加上介面卡 （CTI，請連絡 Center 代理程式）** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="24259-175">On hello **Five9 Plus Adapter (CTI, Contact Center Agents) Configuration** section, click **Configure Five9 Plus Adapter (CTI, Contact Center Agents)** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="24259-176">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="24259-176">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-five9-tutorial/tutorial_five9_configure.png) 

7. <span data-ttu-id="24259-178">tooconfigure 單一登入上**Five9 加上介面卡 （CTI，請連絡 Center 代理程式）**端，您需要下載 toosend hello **Certificate(Base64)、 登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**太[Five9 加上介面卡 （CTI，請連絡 Center 代理程式） 支援小組](https://www.five9.com/about/contact)。</span><span class="sxs-lookup"><span data-stu-id="24259-178">tooconfigure single sign-on on **Five9 Plus Adapter (CTI, Contact Center Agents)** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact).</span></span> <span data-ttu-id="24259-179">也此外，來進一步設定 SSO 請遵循下列步驟，根據 toohello 配接器的 hello:</span><span class="sxs-lookup"><span data-stu-id="24259-179">Also additionally, for configuring SSO further please follow hello below steps according toohello adapter:</span></span>

    <span data-ttu-id="24259-180">a.</span><span class="sxs-lookup"><span data-stu-id="24259-180">a.</span></span> <span data-ttu-id="24259-181">「Five9 Plus Adapter for Agent Desktop Toolkit」系統管理指南：[http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="24259-181">“Five9 Plus Adapter for Agent Desktop Toolkit” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="24259-182">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="24259-182">b.</span></span> <span data-ttu-id="24259-183">「Five9 Plus Adapter for Microsoft Dynamics CRM」系統管理指南：[http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="24259-183">“Five9 Plus Adapter for Microsoft Dynamics CRM” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="24259-184">c.</span><span class="sxs-lookup"><span data-stu-id="24259-184">c.</span></span> <span data-ttu-id="24259-185">「Five9 Plus Adapter for Zendesk」系統管理指南：[http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="24259-185">“Five9 Plus Adapter for Zendesk” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span></span>


> [!TIP]
> <span data-ttu-id="24259-186">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="24259-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="24259-187">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="24259-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="24259-188">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="24259-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="24259-189">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="24259-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="24259-190">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="24259-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="24259-192">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="24259-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="24259-193">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="24259-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-five9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="24259-195">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="24259-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-five9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="24259-197">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="24259-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-five9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="24259-199">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="24259-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-five9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="24259-201">a.</span><span class="sxs-lookup"><span data-stu-id="24259-201">a.</span></span> <span data-ttu-id="24259-202">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="24259-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="24259-203">b.</span><span class="sxs-lookup"><span data-stu-id="24259-203">b.</span></span> <span data-ttu-id="24259-204">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="24259-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="24259-205">c.</span><span class="sxs-lookup"><span data-stu-id="24259-205">c.</span></span> <span data-ttu-id="24259-206">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="24259-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="24259-207">d.</span><span class="sxs-lookup"><span data-stu-id="24259-207">d.</span></span> <span data-ttu-id="24259-208">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="24259-208">Click **Create**.</span></span>
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a><span data-ttu-id="24259-209">建立 Five9 Plus Adapter (CTI，Contact Center Agents) 測試使用者</span><span class="sxs-lookup"><span data-stu-id="24259-209">Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user</span></span>

<span data-ttu-id="24259-210">在本節中，您會在 Five9 Plus Adapter (CTI，Contact Center Agents) 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="24259-210">In this section, you create a user called Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents).</span></span> <span data-ttu-id="24259-211">使用[Five9 加上介面卡 （CTI，請連絡 Center 代理程式） 支援小組](https://www.five9.com/about/contact)新增 hello 使用者在 hello Five9 加上介面卡 （CTI，請連絡 Center 代理程式） 平台。</span><span class="sxs-lookup"><span data-stu-id="24259-211">Work with [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact) to add hello users in hello Five9 Plus Adapter (CTI, Contact Center Agents) platform.</span></span> <span data-ttu-id="24259-212">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="24259-212">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="24259-213">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="24259-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="24259-214">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooFive9 加上介面卡 （CTI，請連絡 Center 代理程式）。</span><span class="sxs-lookup"><span data-stu-id="24259-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFive9 Plus Adapter (CTI, Contact Center Agents).</span></span>

![指派使用者][200] 

<span data-ttu-id="24259-216">**tooassign 許 Simon tooFive9 加上介面卡 （CTI，請連絡 Center 代理程式），執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="24259-216">**tooassign Britta Simon tooFive9 Plus Adapter (CTI, Contact Center Agents), perform hello following steps:**</span></span>

1. <span data-ttu-id="24259-217">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="24259-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="24259-219">在 [hello] 應用程式清單中，選取**Five9 加上介面卡 （CTI，請連絡 Center 代理程式）**。</span><span class="sxs-lookup"><span data-stu-id="24259-219">In hello applications list, select **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![設定單一登入](./media/active-directory-saas-five9-tutorial/tutorial_five9_app.png) 

3. <span data-ttu-id="24259-221">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="24259-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="24259-223">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="24259-223">Click **Add** button.</span></span> <span data-ttu-id="24259-224">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="24259-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="24259-226">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="24259-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="24259-227">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="24259-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="24259-228">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="24259-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="24259-229">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="24259-229">Testing single sign-on</span></span>

<span data-ttu-id="24259-230">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="24259-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="24259-231">當您按一下 hello Five9 加上介面卡 （CTI，請連絡 Center 代理程式） 的圖格 hello 存取面板中時，您應該取得自動登入 tooyour Five9 加上介面卡 （CTI，請連絡 Center 代理程式） 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24259-231">When you click hello Five9 Plus Adapter (CTI, Contact Center Agents) tile in hello Access Panel, you should get automatically signed-on tooyour Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>
<span data-ttu-id="24259-232">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="24259-232">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="24259-233">其他資源</span><span class="sxs-lookup"><span data-stu-id="24259-233">Additional resources</span></span>

* [<span data-ttu-id="24259-234">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="24259-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="24259-235">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="24259-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-five9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-five9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-five9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-five9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-five9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-five9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-five9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-five9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-five9-tutorial/tutorial_general_203.png


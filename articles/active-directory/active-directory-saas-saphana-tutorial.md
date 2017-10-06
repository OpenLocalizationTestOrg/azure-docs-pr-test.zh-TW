---
title: "教學課程：Azure Active Directory 與 SAP HANA 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 SAP HANA 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a><span data-ttu-id="a6f90-103">教學課程：Azure Active Directory 與 SAP HANA 整合</span><span class="sxs-lookup"><span data-stu-id="a6f90-103">Tutorial: Azure Active Directory integration with SAP HANA</span></span>

<span data-ttu-id="a6f90-104">在此教學課程中，您學習如何 toointegrate SAP HANA 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="a6f90-104">In this tutorial, you learn how toointegrate SAP HANA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a6f90-105">整合與 Azure AD 的 SAP HANA 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="a6f90-105">Integrating SAP HANA with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a6f90-106">您可以控制存取 tooSAP HANA Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="a6f90-106">You can control in Azure AD who has access tooSAP HANA</span></span>
- <span data-ttu-id="a6f90-107">您可以啟用您的使用者 tooautomatically get 登入 tooSAP HANA （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="a6f90-107">You can enable your users tooautomatically get signed-on tooSAP HANA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a6f90-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a6f90-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a6f90-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a6f90-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6f90-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a6f90-110">Prerequisites</span></span>

<span data-ttu-id="a6f90-111">tooconfigure 與 SAP HANA 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="a6f90-111">tooconfigure Azure AD integration with SAP HANA, you need hello following items:</span></span>

- <span data-ttu-id="a6f90-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a6f90-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a6f90-113">已啟用 SAP HANA 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a6f90-113">A SAP HANA single sign-on enabled subscription</span></span>
- <span data-ttu-id="a6f90-114">執行中的 HANA 執行個體，無論是位於任何公用 IaaS、內部部署、Azure VM 還是 Azure 中的 SAP 大型執行個體</span><span class="sxs-lookup"><span data-stu-id="a6f90-114">A running HANA Instance either on any public IaaS, on-premises, Azure VMs or SAP Large Instances in Azure</span></span>
- <span data-ttu-id="a6f90-115">hello XSA 管理 Web 介面，以及 HANA Studio hello HANA 執行個體上安裝。</span><span class="sxs-lookup"><span data-stu-id="a6f90-115">hello XSA Administration Web Interface as well as HANA Studio installed on hello HANA instance.</span></span>

> [!NOTE]
> <span data-ttu-id="a6f90-116">本教學課程中的步驟 tootest hello，不建議使用 SAP HANA 的實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="a6f90-116">tootest hello steps in this tutorial, we do not recommend using a production environment of SAP HANA.</span></span> <span data-ttu-id="a6f90-117">開發，或預備環境的 hello 應用程式，然後使用 hello 實際執行環境中的第一次測試 hello 整合。</span><span class="sxs-lookup"><span data-stu-id="a6f90-117">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="a6f90-118">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="a6f90-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a6f90-119">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a6f90-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a6f90-120">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="a6f90-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a6f90-121">案例描述</span><span class="sxs-lookup"><span data-stu-id="a6f90-121">Scenario description</span></span>
<span data-ttu-id="a6f90-122">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a6f90-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a6f90-123">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="a6f90-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a6f90-124">從 hello 圖庫加入 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="a6f90-124">Adding SAP HANA from hello gallery</span></span>
2. <span data-ttu-id="a6f90-125">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a6f90-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-hana-from-hello-gallery"></a><span data-ttu-id="a6f90-126">從 hello 圖庫加入 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="a6f90-126">Adding SAP HANA from hello gallery</span></span>
<span data-ttu-id="a6f90-127">tooconfigure hello 整合 SAP HANA 到 Azure AD，您需要 tooadd SAP HANA hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6f90-127">tooconfigure hello integration of SAP HANA into Azure AD, you need tooadd SAP HANA from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a6f90-128">**tooadd SAP HANA hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a6f90-128">**tooadd SAP HANA from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6f90-129">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a6f90-129">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="a6f90-131">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a6f90-131">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a6f90-132">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a6f90-132">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="a6f90-134">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a6f90-134">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="a6f90-136">在 hello 搜尋方塊中，輸入**SAP HANA**，選取**SAP HANA**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6f90-136">In hello search box, type **SAP HANA**, select **SAP HANA** from result panel then click **Add** button tooadd hello application.</span></span> 

    ![hello 新的應用程式](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a6f90-138">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a6f90-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a6f90-139">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SAP HANA 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a6f90-139">In this section, you configure and test Azure AD single sign-on with SAP HANA based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a6f90-140">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 SAP HANA 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="a6f90-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP HANA is tooa user in Azure AD.</span></span> <span data-ttu-id="a6f90-141">換句話說，Azure AD 使用者與 SAP HANA 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="a6f90-141">In other words, a link relationship between an Azure AD user and hello related user in SAP HANA needs toobe established.</span></span>

<span data-ttu-id="a6f90-142">在 SAP HANA hello hello 值指派**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="a6f90-142">In SAP HANA, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a6f90-143">tooconfigure 及測試 Azure AD 單一登入 SAP HANA，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="a6f90-143">tooconfigure and test Azure AD single sign-on with SAP HANA, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a6f90-144">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="a6f90-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a6f90-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="a6f90-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a6f90-146">**[建立 SAP HANA 測試使用者](#creating-a-sap-hana-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 SAP HANA 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="a6f90-146">**[Creating a SAP HANA test user](#creating-a-sap-hana-test-user)** - toohave a counterpart of Britta Simon in SAP HANA that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a6f90-147">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a6f90-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a6f90-148">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="a6f90-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a6f90-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a6f90-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a6f90-150">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 SAP HANA 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="a6f90-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP HANA application.</span></span>

<span data-ttu-id="a6f90-151">**tooconfigure Azure AD 單一登入 SAP HANA，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a6f90-151">**tooconfigure Azure AD single sign-on with SAP HANA, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6f90-152">在 Azure 入口網站上 hello hello **SAP HANA**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="a6f90-152">In hello Azure portal, on hello **SAP HANA** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="a6f90-154">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a6f90-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. <span data-ttu-id="a6f90-156">在 hello **SAP HANA 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6f90-156">On hello **SAP HANA Domain and URLs** section, perform hello following steps:</span></span>

    ![網域與 URL 單一登入資訊](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    <span data-ttu-id="a6f90-158">a.</span><span class="sxs-lookup"><span data-stu-id="a6f90-158">a.</span></span> <span data-ttu-id="a6f90-159">在 hello**識別碼**文字方塊中，做為輸入：`HA100`</span><span class="sxs-lookup"><span data-stu-id="a6f90-159">In hello **Identifier** textbox, type as: `HA100`</span></span> 

    <span data-ttu-id="a6f90-160">b.</span><span class="sxs-lookup"><span data-stu-id="a6f90-160">b.</span></span> <span data-ttu-id="a6f90-161">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span><span class="sxs-lookup"><span data-stu-id="a6f90-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a6f90-162">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="a6f90-162">These values are not real.</span></span> <span data-ttu-id="a6f90-163">以 hello 實際的識別項和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="a6f90-163">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="a6f90-164">請連絡[SAP HANA 用戶端支援小組](https://cloudplatform.sap.com/contact.html)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="a6f90-164">Contact [SAP HANA Client support team](https://cloudplatform.sap.com/contact.html) tooget these values.</span></span> 

4. <span data-ttu-id="a6f90-165">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="a6f90-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    ><span data-ttu-id="a6f90-167">如果憑證不在作用中然後讓它成為按一下 hello 「 使新憑證作用中 」 的核取方塊 hello Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="a6f90-167">If certificate is not active then make it active by clicking hello “Make new certificate active” checkbox in hello Azure AD.</span></span> 

5. <span data-ttu-id="a6f90-168">SAP HANA 應用程式預期 hello SAML 判斷提示，以特定格式。</span><span class="sxs-lookup"><span data-stu-id="a6f90-168">SAP HANA application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="a6f90-169">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="a6f90-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="a6f90-170">我們已在這裡對應 hello**使用者識別碼**與**ExtractMailPrefix()**函式的**user.mail**。</span><span class="sxs-lookup"><span data-stu-id="a6f90-170">Here we have mapped hello **User Identifier** with **ExtractMailPrefix()** function of **user.mail**.</span></span> <span data-ttu-id="a6f90-171">這可讓 hello 的前置詞值，這是唯一的使用者 id。 hello hello 使用者的電子郵件</span><span class="sxs-lookup"><span data-stu-id="a6f90-171">This gives hello prefix value of email of hello user which is hello unique User ID.</span></span> <span data-ttu-id="a6f90-172">這是在每個成功的回應中傳送 toohello SAP HANA 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6f90-172">This is sent toohello SAP HANA application in every successful response.</span></span>

    ![設定單一登入](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. <span data-ttu-id="a6f90-174">在 hello**使用者屬性**區段 hello**單一登入**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="a6f90-174">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="a6f90-175">a.</span><span class="sxs-lookup"><span data-stu-id="a6f90-175">a.</span></span> <span data-ttu-id="a6f90-176">在 hello**使用者識別碼**下拉式清單中選取**ExtractMailPrefix**。</span><span class="sxs-lookup"><span data-stu-id="a6f90-176">In hello **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>
    
    <span data-ttu-id="a6f90-177">b.</span><span class="sxs-lookup"><span data-stu-id="a6f90-177">b.</span></span> <span data-ttu-id="a6f90-178">在 hello**郵件**下拉式清單中選取**user.mail**。</span><span class="sxs-lookup"><span data-stu-id="a6f90-178">In hello **Mail** dropdown list, select **user.mail**.</span></span>

7. <span data-ttu-id="a6f90-179">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a6f90-179">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="a6f90-181">tooconfigure 單一登入上**SAP HANA** ，登入 tooyour **HANA XSA Web 主控台**toohello 瀏覽個別的 HTTPS 端點。</span><span class="sxs-lookup"><span data-stu-id="a6f90-181">tooconfigure single sign-on on **SAP HANA** side, login tooyour **HANA XSA Web Console**  by browsing toohello respective HTTPS-endpoint.</span></span>

    > [!Note]
    > <span data-ttu-id="a6f90-182">在 hello 預設組態中，hello URL 重新導向 hello 要求 tooa 登入畫面，而這需要 hello 認證已驗證 SAP HANA 資料庫使用者 toocomplete hello 登入處理程序。</span><span class="sxs-lookup"><span data-stu-id="a6f90-182">In hello default configuration, hello URL redirects hello request tooa logon screen, which requires hello credentials of an authenticated SAP HANA database user toocomplete hello logon process.</span></span> <span data-ttu-id="a6f90-183">hello 登入使用者都必須有 hello 權限需要的 tooperform SAML 系統管理工作。</span><span class="sxs-lookup"><span data-stu-id="a6f90-183">hello user who logs on must have hello privileges required tooperform SAML administration tasks.</span></span>

9. <span data-ttu-id="a6f90-184">Hello XSA Web 介面，在瀏覽過**SAML 身分識別提供者**並從該處，按一下 [hello **"+"** -hello hello 螢幕 toodisplay hello 新增身分識別提供者資訊] 窗格底部的按鈕，然後執行hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a6f90-184">In hello XSA Web Interface, navigate too**SAML Identity Provider** and from there, click hello **“+”** -button on hello bottom of hello screen toodisplay hello Add Identity Provider Info pane and perform hello following steps:</span></span>

    ![新增識別提供者](./media/active-directory-saas-saphana-tutorial/sap1.png)

    <span data-ttu-id="a6f90-186">a.</span><span class="sxs-lookup"><span data-stu-id="a6f90-186">a.</span></span> <span data-ttu-id="a6f90-187">在 [hello**新增身分識別提供者資訊**] 窗格中，貼上 hello 內容的中繼資料 XML，您從 Azure 入口網站下載到 hello hello**中繼資料**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a6f90-187">In hello **Add Identity Provider Info** pane, paste hello contents of hello Metadata XML, which you have downloaded from Azure portal into hello **Metadata** textbox.</span></span>

    ![[新增識別提供者] 設定](./media/active-directory-saas-saphana-tutorial/sap2.png)

    <span data-ttu-id="a6f90-189">b.</span><span class="sxs-lookup"><span data-stu-id="a6f90-189">b.</span></span> <span data-ttu-id="a6f90-190">如果 hello hello XML 文件內容有效，hello 剖析程序會 hello 所需的資訊 tooinsert 擷取至 hello**主旨、 實體識別碼和簽發者**hello 一般資料欄位螢幕區域，以及 hello hello URL 欄位目的地的螢幕區域，例如**基底 URL 和單一登入 URL (*)**。</span><span class="sxs-lookup"><span data-stu-id="a6f90-190">If hello contents of hello XML document are valid, hello parsing process extracts hello information required tooinsert into hello **Subject, Entity ID, and Issuer** fields in hello General Data screen area, and hello URL fields in hello Destination screen area, for example, **Base URL and SingleSignOn URL (*)**.</span></span>

    ![[新增識別提供者] 設定](./media/active-directory-saas-saphana-tutorial/sap3.png)

    <span data-ttu-id="a6f90-192">c.</span><span class="sxs-lookup"><span data-stu-id="a6f90-192">c.</span></span> <span data-ttu-id="a6f90-193">在 hello 名稱方塊中的 hello 一般資料畫面區域中，輸入 hello 新 SAML SSO 身分識別提供者的名稱。</span><span class="sxs-lookup"><span data-stu-id="a6f90-193">In hello Name box of hello General Data screen area, enter a name for hello new SAML SSO identity provider.</span></span>

    > [!Note]
    > <span data-ttu-id="a6f90-194">hello SAML IDP hello 名稱是強制性，而且必須是唯一的。它會出現在 hello 清單可用的 SAML IDPs 顯示，如果您選取 SAML 作為 hello SAP HANA XS 應用程式 toouse，驗證方法，例如 hello 驗證畫面區域中的 hello XS 成品管理工具。</span><span class="sxs-lookup"><span data-stu-id="a6f90-194">hello name of hello SAML IDP is mandatory and must be unique; it appears in hello list of available SAML IDPs that is displayed, if you select SAML as hello authentication method for SAP HANA XS applications toouse, for example, in hello Authentication screen area of hello XS Artifact Administration tool.</span></span>

10. <span data-ttu-id="a6f90-195">儲存 hello hello 新 SAML 身分識別提供者的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a6f90-195">Save hello details of hello new SAML identity provider.</span></span> <span data-ttu-id="a6f90-196">選擇**儲存**toosave hello hello SAML 身分識別提供者的詳細資料，並加入 hello 新 SAML IDP toohello 清單的已知 SAML IDPs。</span><span class="sxs-lookup"><span data-stu-id="a6f90-196">Choose **Save** toosave hello details of hello SAML identity provider and add hello new SAML IDP toohello list of known SAML IDPs.</span></span>

    ![[儲存] 按鈕](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. <span data-ttu-id="a6f90-198">HANA Studio 中的 hello hello 系統內容中**組態**索引標籤上，只要篩選設定**saml**並調整 hello **assertion_timeout**從**10 秒**太**120 秒**。</span><span class="sxs-lookup"><span data-stu-id="a6f90-198">In HANA Studio within hello system properties of hello **Configuration** tab, just filter settings by **saml** and adjust hello **assertion_timeout** from **10 sec** too**120 sec**.</span></span>

    ![assertion_timeout 設定](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> <span data-ttu-id="a6f90-200">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="a6f90-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a6f90-201">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="a6f90-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a6f90-202">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a6f90-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a6f90-203">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a6f90-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="a6f90-204">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a6f90-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="a6f90-206">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a6f90-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6f90-207">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a6f90-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a6f90-209">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="a6f90-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a6f90-211">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="a6f90-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![hello [新增] 按鈕](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a6f90-213">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6f90-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a6f90-215">a.</span><span class="sxs-lookup"><span data-stu-id="a6f90-215">a.</span></span> <span data-ttu-id="a6f90-216">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="a6f90-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a6f90-217">b.</span><span class="sxs-lookup"><span data-stu-id="a6f90-217">b.</span></span> <span data-ttu-id="a6f90-218">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="a6f90-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a6f90-219">c.</span><span class="sxs-lookup"><span data-stu-id="a6f90-219">c.</span></span> <span data-ttu-id="a6f90-220">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="a6f90-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a6f90-221">d.</span><span class="sxs-lookup"><span data-stu-id="a6f90-221">d.</span></span> <span data-ttu-id="a6f90-222">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a6f90-222">Click **Create**.</span></span>
 
### <a name="creating-a-sap-hana-test-user"></a><span data-ttu-id="a6f90-223">建立 SAP HANA 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a6f90-223">Creating a SAP HANA test user</span></span>

<span data-ttu-id="a6f90-224">tooenable Azure AD 使用者 toolog 中 tooSAP HANA，它們必須佈建到 SAP HANA。</span><span class="sxs-lookup"><span data-stu-id="a6f90-224">tooenable Azure AD users toolog in tooSAP HANA, they must be provisioned into SAP HANA.</span></span>
<span data-ttu-id="a6f90-225">SAP HANA 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="a6f90-225">SAP HANA supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="a6f90-226">若要手動 toocreate 使用者，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a6f90-226">If you need toocreate a user manually, perform hello following steps:</span></span>

>[!Note]
><span data-ttu-id="a6f90-227">您可以變更 hello hello 使用者所使用的外部驗證。</span><span class="sxs-lookup"><span data-stu-id="a6f90-227">You can change hello external authentication used by hello user.</span></span>
<span data-ttu-id="a6f90-228">外部使用者會使用外部系統 (例如 Kerberos 系統) 來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="a6f90-228">External users are authenticated using an external system, for example a Kerberos system.</span></span> <span data-ttu-id="a6f90-229">如需外部身分識別的詳細資訊，請連絡[網域系統管理員](https://cloudplatform.sap.com/contact.html)。</span><span class="sxs-lookup"><span data-stu-id="a6f90-229">For detailed information about external identities, contact your [domain administrator](https://cloudplatform.sap.com/contact.html).</span></span>

1. <span data-ttu-id="a6f90-230">開啟 hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us)為系統管理員，並且啟用 hello SAML SSO 資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="a6f90-230">Open hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) as an administrator and enable hello DB-User for SAML SSO.</span></span>

    ![建立使用者](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. <span data-ttu-id="a6f90-232">刻度 hello 不可見的核取方塊 toohello 方**SAML**並遵循 hello [設定] 連結。</span><span class="sxs-lookup"><span data-stu-id="a6f90-232">Tick hello invisible checkbox toohello left of **SAML** and follow hello Configure link.</span></span>

3. <span data-ttu-id="a6f90-233">按一下**新增**tooadd hello SAML IDP，然後按一下**確定**選取 hello 適當 SAML IDP。</span><span class="sxs-lookup"><span data-stu-id="a6f90-233">Click **Add** tooadd hello SAML IDP and click **OK** selecting hello appropriate SAML IDP.</span></span>

4. <span data-ttu-id="a6f90-234">新增 hello**外部識別**（例如。</span><span class="sxs-lookup"><span data-stu-id="a6f90-234">Add hello **External Identity** (ex.</span></span> <span data-ttu-id="a6f90-235">這裡 BrittaSimon)，或選擇**"Any"**按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="a6f90-235">BrittaSimon here) or choose **"Any"** and click **OK**.</span></span>

    >[!Note]
    ><span data-ttu-id="a6f90-236">如果未核取 「 任何 」 核取方塊，則 hello HANA 中的使用者名稱需要 tooexactly 符合 hello 名稱之前 hello 網域尾碼 hello UPN 中的 hello 使用者 (亦即BrittaSimon@contoso.com就會變成 BrittaSimon HANA 中的)。</span><span class="sxs-lookup"><span data-stu-id="a6f90-236">If "ANY" check-box is not checked, then hello user name in HANA needs tooexactly match hello name of hello user in hello UPN before hello domain suffix (i.e. BrittaSimon@contoso.com would become BrittaSimon in HANA).</span></span>

5. <span data-ttu-id="a6f90-237">為了測試用途，指派所有**"XS"**角色 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="a6f90-237">For testing purposes, assign all **"XS"** roles toohello user.</span></span>

    ![指派角色](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > <span data-ttu-id="a6f90-239">您只應該提供適用於您使用案例的權限。</span><span class="sxs-lookup"><span data-stu-id="a6f90-239">You should give those permissions appropriate for your use cases, only.</span></span>

6. <span data-ttu-id="a6f90-240">儲存 hello 的使用者。</span><span class="sxs-lookup"><span data-stu-id="a6f90-240">Save hello user.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a6f90-241">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="a6f90-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a6f90-242">在本節中，您可以授與存取 tooSAP HANA 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a6f90-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP HANA.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="a6f90-244">**tooassign 許 Simon tooSAP HANA，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a6f90-244">**tooassign Britta Simon tooSAP HANA, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6f90-245">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a6f90-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="a6f90-247">在 [hello] 應用程式清單中，選取**SAP HANA**。</span><span class="sxs-lookup"><span data-stu-id="a6f90-247">In hello applications list, select **SAP HANA**.</span></span>

    ![指派使用者](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. <span data-ttu-id="a6f90-249">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="a6f90-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202] 

4. <span data-ttu-id="a6f90-251">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a6f90-251">Click **Add** button.</span></span> <span data-ttu-id="a6f90-252">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a6f90-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="a6f90-254">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="a6f90-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a6f90-255">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a6f90-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a6f90-256">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a6f90-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a6f90-257">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="a6f90-257">Testing single sign-on</span></span>

<span data-ttu-id="a6f90-258">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="a6f90-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a6f90-259">當您按一下 hello SAP HANA 磚 hello 存取面板中的時，您應該取得 tooyour 自動登入 SAP HANA 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6f90-259">When you click hello SAP HANA tile in hello Access Panel, you should get automatically signed-on tooyour SAP HANA application.</span></span>
<span data-ttu-id="a6f90-260">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="a6f90-260">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a6f90-261">其他資源</span><span class="sxs-lookup"><span data-stu-id="a6f90-261">Additional resources</span></span>

* [<span data-ttu-id="a6f90-262">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6f90-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a6f90-263">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a6f90-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png


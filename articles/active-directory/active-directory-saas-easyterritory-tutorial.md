---
title: "教學課程：Azure Active Directory 與 EasyTerritory 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 EasyTerritory 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d29b362d-e986-4f67-8ff2-e158e49353aa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 46f99496397e2ed39b1d9410453dac7983ced612
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-easyterritory"></a><span data-ttu-id="9d9d1-103">教學課程：Azure Active Directory 與 EasyTerritory 整合</span><span class="sxs-lookup"><span data-stu-id="9d9d1-103">Tutorial: Azure Active Directory integration with EasyTerritory</span></span>

<span data-ttu-id="9d9d1-104">在本教學課程中，您會了解如何將 EasyTerritory 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-104">In this tutorial, you learn how to integrate EasyTerritory with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9d9d1-105">將 EasyTerritory 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="9d9d1-105">Integrating EasyTerritory with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9d9d1-106">您可以在 Azure AD 中控制可存取 EasyTerritory 的人員。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-106">You can control in Azure AD who has access to EasyTerritory.</span></span>
- <span data-ttu-id="9d9d1-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 EasyTerritory (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-107">You can enable your users to automatically get signed-on to EasyTerritory (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9d9d1-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="9d9d1-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d9d1-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="9d9d1-110">Prerequisites</span></span>

<span data-ttu-id="9d9d1-111">若要設定 Azure AD 與 EasyTerritory 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="9d9d1-111">To configure Azure AD integration with EasyTerritory, you need the following items:</span></span>

- <span data-ttu-id="9d9d1-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9d9d1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9d9d1-113">已啟用 EasyTerritory 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9d9d1-113">A EasyTerritory single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9d9d1-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9d9d1-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="9d9d1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9d9d1-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9d9d1-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9d9d1-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="9d9d1-118">Scenario description</span></span>
<span data-ttu-id="9d9d1-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9d9d1-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="9d9d1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9d9d1-121">從資源庫新增 EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="9d9d1-121">Adding EasyTerritory from the gallery</span></span>
2. <span data-ttu-id="9d9d1-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9d9d1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-easyterritory-from-the-gallery"></a><span data-ttu-id="9d9d1-123">從資源庫新增 EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="9d9d1-123">Adding EasyTerritory from the gallery</span></span>
<span data-ttu-id="9d9d1-124">若要設定將 EasyTerritory 整合到 Azure AD 中，您必須從資源庫將 EasyTerritory 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-124">To configure the integration of EasyTerritory into Azure AD, you need to add EasyTerritory from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9d9d1-125">**若要從資源庫新增 EasyTerritory，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9d9d1-125">**To add EasyTerritory from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9d9d1-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="9d9d1-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9d9d1-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="9d9d1-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="9d9d1-133">在搜尋方塊中，輸入 **EasyTerritory**，從結果面板中選取 [EasyTerritory]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-133">In the search box, type **EasyTerritory**, select **EasyTerritory** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 EasyTerritory](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9d9d1-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9d9d1-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9d9d1-136">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 EasyTerritory 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-136">In this section, you configure and test Azure AD single sign-on with EasyTerritory based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9d9d1-137">若要讓單一登入能夠運作，Azure AD 必須知道 EasyTerritory 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-137">For single sign-on to work, Azure AD needs to know what the counterpart user in EasyTerritory is to a user in Azure AD.</span></span> <span data-ttu-id="9d9d1-138">換句話說，必須在 Azure AD 使用者與 EasyTerritory 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-138">In other words, a link relationship between an Azure AD user and the related user in EasyTerritory needs to be established.</span></span>

<span data-ttu-id="9d9d1-139">在 EasyTerritory 中，將 Azure AD 中 [使用者名稱]的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-139">In EasyTerritory, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9d9d1-140">若要設定及測試與 EasyTerritory 搭配運作的 Azure AD 單一登入，您必須完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="9d9d1-140">To configure and test Azure AD single sign-on with EasyTerritory, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9d9d1-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9d9d1-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9d9d1-143">**[建立 EasyTerritory 測試使用者](#create-a-easyterritory-test-user)** - 在 EasyTerritory 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-143">**[Create a EasyTerritory test user](#create-a-easyterritory-test-user)** - to have a counterpart of Britta Simon in EasyTerritory that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9d9d1-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9d9d1-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9d9d1-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9d9d1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9d9d1-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 EasyTerritory 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EasyTerritory application.</span></span>

<span data-ttu-id="9d9d1-148">**若要設定與 EasyTerritory 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9d9d1-148">**To configure Azure AD single sign-on with EasyTerritory, perform the following steps:**</span></span>

1. <span data-ttu-id="9d9d1-149">在 Azure 入口網站的 [EasyTerritory] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-149">In the Azure portal, on the **EasyTerritory** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="9d9d1-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_samlbase.png)

3. <span data-ttu-id="9d9d1-153">如果您想要以「IDP 起始模式」設定應用程式，請在 [EasyTerritory 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9d9d1-153">On the **EasyTerritory Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![EasyTerritory 網域和 URL 單一登入資訊](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_url.png)

    <span data-ttu-id="9d9d1-155">a.</span><span class="sxs-lookup"><span data-stu-id="9d9d1-155">a.</span></span> <span data-ttu-id="9d9d1-156">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://apps.easyterritory.com/<tenant id>/dev/`</span><span class="sxs-lookup"><span data-stu-id="9d9d1-156">In the **Identifier** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/dev/`</span></span>

    <span data-ttu-id="9d9d1-157">b.</span><span class="sxs-lookup"><span data-stu-id="9d9d1-157">b.</span></span> <span data-ttu-id="9d9d1-158">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`</span><span class="sxs-lookup"><span data-stu-id="9d9d1-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`</span></span>

4. <span data-ttu-id="9d9d1-159">如果您想要以 **SP** 起始模式設定應用程式，請勾選 [顯示進階 URL 設定]，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9d9d1-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![EasyTerritory 網域和 URL 單一登入資訊](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_url1.png)

    <span data-ttu-id="9d9d1-161">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<company name>.easyterritory.com/`</span><span class="sxs-lookup"><span data-stu-id="9d9d1-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.easyterritory.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="9d9d1-162">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-162">These values are not real.</span></span> <span data-ttu-id="9d9d1-163">使用實際的識別碼、回覆 URL 和登入 URL 來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="9d9d1-164">請連絡 [EasyTerritory 客戶支援小組](mailto:sales@easyterritory.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-164">Contact [EasyTerritory Client support team](mailto:sales@easyterritory.com) to get these values.</span></span> 

5. <span data-ttu-id="9d9d1-165">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_certificate.png) 

6. <span data-ttu-id="9d9d1-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-167">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-easyterritory-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="9d9d1-169">若要在 **EasyTerritory** 端設定單一登入，您必須將已下載的**中繼資料 XML** 傳送給 [EasyTerritory 支援小組](mailto:sales@easyterritory.com)。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-169">To configure single sign-on on **EasyTerritory** side, you need to send the downloaded **Metadata XML** to [EasyTerritory support team](mailto:sales@easyterritory.com).</span></span> <span data-ttu-id="9d9d1-170">他們會進行此設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9d9d1-171">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="9d9d1-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9d9d1-172">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9d9d1-173">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9d9d1-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9d9d1-174">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9d9d1-174">Create an Azure AD test user</span></span>

<span data-ttu-id="9d9d1-175">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="9d9d1-177">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9d9d1-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9d9d1-178">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9d9d1-180">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9d9d1-182">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9d9d1-184">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9d9d1-184">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9d9d1-186">a.</span><span class="sxs-lookup"><span data-stu-id="9d9d1-186">a.</span></span> <span data-ttu-id="9d9d1-187">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9d9d1-188">b.</span><span class="sxs-lookup"><span data-stu-id="9d9d1-188">b.</span></span> <span data-ttu-id="9d9d1-189">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="9d9d1-190">c.</span><span class="sxs-lookup"><span data-stu-id="9d9d1-190">c.</span></span> <span data-ttu-id="9d9d1-191">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="9d9d1-192">d.</span><span class="sxs-lookup"><span data-stu-id="9d9d1-192">d.</span></span> <span data-ttu-id="9d9d1-193">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-193">Click **Create**.</span></span>
 
### <a name="create-a-easyterritory-test-user"></a><span data-ttu-id="9d9d1-194">建立 EasyTerritory 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9d9d1-194">Create a EasyTerritory test user</span></span>

<span data-ttu-id="9d9d1-195">在本節中，您要在 EasyTerritory 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-195">In this section, you create a user called Britta Simon in EasyTerritory.</span></span> <span data-ttu-id="9d9d1-196">請與 [EasyTerritory 支援小組](mailto:sales@easyterritory.com)合作，以在 EasyTerritory 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-196">Please work with [EasyTerritory support team](mailto:sales@easyterritory.com) to add the users in the EasyTerritory platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9d9d1-197">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9d9d1-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="9d9d1-198">在本節中，您會將 EasyTerritory 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EasyTerritory.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="9d9d1-200">**若要將 Britta Simon 指派給 EasyTerritory，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9d9d1-200">**To assign Britta Simon to EasyTerritory, perform the following steps:**</span></span>

1. <span data-ttu-id="9d9d1-201">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="9d9d1-203">在應用程式清單中，選取 [EasyTerritory]。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-203">In the applications list, select **EasyTerritory**.</span></span>

    ![應用程式清單中的 [EasyTerritory] 連結](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_app.png)  

3. <span data-ttu-id="9d9d1-205">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-205">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="9d9d1-207">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-207">Click **Add** button.</span></span> <span data-ttu-id="9d9d1-208">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="9d9d1-210">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9d9d1-211">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9d9d1-212">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9d9d1-213">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="9d9d1-213">Test single sign-on</span></span>

<span data-ttu-id="9d9d1-214">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9d9d1-215">當您在「存取面板」中按一下 [EasyTerritory] 磚時，應該會自動登入您的 EasyTerritory 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-215">When you click the EasyTerritory tile in the Access Panel, you should get automatically signed-on to your EasyTerritory application.</span></span>
<span data-ttu-id="9d9d1-216">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="9d9d1-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9d9d1-217">其他資源</span><span class="sxs-lookup"><span data-stu-id="9d9d1-217">Additional resources</span></span>

* [<span data-ttu-id="9d9d1-218">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="9d9d1-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9d9d1-219">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="9d9d1-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)




<!--Image references-->

[1]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_203.png


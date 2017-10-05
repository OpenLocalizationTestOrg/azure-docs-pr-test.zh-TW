---
title: "教學課程：Azure Active Directory 與 Greenhouse 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Greenhouse 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 78ec1766-4f79-4f16-9a66-d5584c4b6151
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: d3aba4aab8ded8749db2bf8197f57a6763008c60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-greenhouse"></a><span data-ttu-id="b1626-103">教學課程：Azure Active Directory 與 Greenhouse 整合</span><span class="sxs-lookup"><span data-stu-id="b1626-103">Tutorial: Azure Active Directory integration with Greenhouse</span></span>

<span data-ttu-id="b1626-104">在本教學課程中，您將了解如何整合 Greenhouse 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="b1626-104">In this tutorial, you learn how to integrate Greenhouse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b1626-105">Greenhouse 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="b1626-105">Integrating Greenhouse with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b1626-106">您可以在 Azure AD 中控制可存取 Greenhouse 的人員。</span><span class="sxs-lookup"><span data-stu-id="b1626-106">You can control in Azure AD who has access to Greenhouse.</span></span>
- <span data-ttu-id="b1626-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Greenhouse (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="b1626-107">You can enable your users to automatically get signed-on to Greenhouse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b1626-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="b1626-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b1626-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b1626-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1626-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b1626-110">Prerequisites</span></span>

<span data-ttu-id="b1626-111">若要設定 Azure AD 與 Greenhouse 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="b1626-111">To configure Azure AD integration with Greenhouse, you need the following items:</span></span>

- <span data-ttu-id="b1626-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b1626-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b1626-113">啟用 Greenhouse 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b1626-113">A Greenhouse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b1626-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b1626-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b1626-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="b1626-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b1626-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b1626-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b1626-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="b1626-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b1626-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="b1626-118">Scenario description</span></span>
<span data-ttu-id="b1626-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b1626-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b1626-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="b1626-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b1626-121">從資源庫新增 Greenhouse</span><span class="sxs-lookup"><span data-stu-id="b1626-121">Adding Greenhouse from the gallery</span></span>
2. <span data-ttu-id="b1626-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b1626-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-greenhouse-from-the-gallery"></a><span data-ttu-id="b1626-123">從資源庫新增 Greenhouse</span><span class="sxs-lookup"><span data-stu-id="b1626-123">Adding Greenhouse from the gallery</span></span>
<span data-ttu-id="b1626-124">若要設定 Greenhouse 與 Azure AD 整合，您需要從資源庫將 Greenhouse 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="b1626-124">To configure the integration of Greenhouse into Azure AD, you need to add Greenhouse from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b1626-125">**若要從資源庫新增 Greenhouse，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b1626-125">**To add Greenhouse from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b1626-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="b1626-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="b1626-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b1626-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b1626-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b1626-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="b1626-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b1626-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="b1626-133">在搜尋方塊中，鍵入 **Greenhouse**，從結果面板中選取 [Greenhouse]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="b1626-133">In the search box, type **Greenhouse**, select **Greenhouse** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Greenhouse](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b1626-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b1626-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b1626-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Greenhouse 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b1626-136">In this section, you configure and test Azure AD single sign-on with Greenhouse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b1626-137">若要讓單一登入運作，Azure AD 必須知道 Greenhouse 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="b1626-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Greenhouse is to a user in Azure AD.</span></span> <span data-ttu-id="b1626-138">換句話說，必須在 Azure AD 使用者與 Greenhouse 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b1626-138">In other words, a link relationship between an Azure AD user and the related user in Greenhouse needs to be established.</span></span>

<span data-ttu-id="b1626-139">在 Greenhouse 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b1626-139">In Greenhouse, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b1626-140">若要使用 Greenhouse 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="b1626-140">To configure and test Azure AD single sign-on with Greenhouse, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b1626-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="b1626-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b1626-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b1626-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b1626-143">**[建立 Greenhouse 測試使用者](#create-a-greenhouse-test-user)** - 在 Greenhouse 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="b1626-143">**[Create a Greenhouse test user](#create-a-greenhouse-test-user)** - to have a counterpart of Britta Simon in Greenhouse that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b1626-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b1626-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b1626-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="b1626-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b1626-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b1626-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b1626-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Greenhouse 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="b1626-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Greenhouse application.</span></span>

<span data-ttu-id="b1626-148">**若要使用 Greenhouse 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b1626-148">**To configure Azure AD single sign-on with Greenhouse, perform the following steps:**</span></span>

1. <span data-ttu-id="b1626-149">在 Azure 入口網站的 [Greenhouse] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="b1626-149">In the Azure portal, on the **Greenhouse** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="b1626-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="b1626-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_samlbase.png)

3. <span data-ttu-id="b1626-153">在 [Springer Link 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b1626-153">On the **Greenhouse Domain and URLs** section, perform the following steps:</span></span>

    ![Greenhouse 網域和 URL 單一登入資訊](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_url.png)

    <span data-ttu-id="b1626-155">a.</span><span class="sxs-lookup"><span data-stu-id="b1626-155">a.</span></span> <span data-ttu-id="b1626-156">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="b1626-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.greenhouse.io`</span></span>

    <span data-ttu-id="b1626-157">b.</span><span class="sxs-lookup"><span data-stu-id="b1626-157">b.</span></span> <span data-ttu-id="b1626-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="b1626-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.greenhouse.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b1626-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="b1626-159">These values are not real.</span></span> <span data-ttu-id="b1626-160">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="b1626-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b1626-161">請連絡 [Greenhouse 用戶端支援小組](https://www.greenhouse.io/contact)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="b1626-161">Contact [Greenhouse Client support team](https://www.greenhouse.io/contact) to get these values.</span></span> 
 


4. <span data-ttu-id="b1626-162">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="b1626-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_certificate.png) 

5. <span data-ttu-id="b1626-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b1626-164">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-greenhouse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b1626-166">若要在 **Greenhouse** 端設定單一登入，您必須將已下載的**中繼資料 XML** 傳送給 [Greenhouse 支援小組](http://www.greenhouse.io/contact)。</span><span class="sxs-lookup"><span data-stu-id="b1626-166">To configure single sign-on on **Greenhouse** side, you need to send the downloaded **Metadata XML** to [Greenhouse support team](http://www.greenhouse.io/contact).</span></span>

> [!TIP]
> <span data-ttu-id="b1626-167">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="b1626-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b1626-168">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="b1626-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b1626-169">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b1626-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b1626-170">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b1626-170">Create an Azure AD test user</span></span>

<span data-ttu-id="b1626-171">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="b1626-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="b1626-173">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b1626-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b1626-174">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b1626-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b1626-176">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="b1626-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b1626-178">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b1626-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b1626-180">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b1626-180">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b1626-182">a.</span><span class="sxs-lookup"><span data-stu-id="b1626-182">a.</span></span> <span data-ttu-id="b1626-183">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b1626-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b1626-184">b.</span><span class="sxs-lookup"><span data-stu-id="b1626-184">b.</span></span> <span data-ttu-id="b1626-185">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="b1626-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b1626-186">c.</span><span class="sxs-lookup"><span data-stu-id="b1626-186">c.</span></span> <span data-ttu-id="b1626-187">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="b1626-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b1626-188">d.</span><span class="sxs-lookup"><span data-stu-id="b1626-188">d.</span></span> <span data-ttu-id="b1626-189">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b1626-189">Click **Create**.</span></span>
 
### <a name="create-a-greenhouse-test-user"></a><span data-ttu-id="b1626-190">建立 Greenhouse 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b1626-190">Create a Greenhouse test user</span></span>

<span data-ttu-id="b1626-191">若要讓 Azure AD 使用者可以登入 Greenhouse，則必須將他們佈建至 Greenhouse。</span><span class="sxs-lookup"><span data-stu-id="b1626-191">In order to enable Azure AD users to log into Greenhouse, they must be provisioned into Greenhouse.</span></span> <span data-ttu-id="b1626-192">在 Greenhouse 的情況下，需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="b1626-192">In the case of Greenhouse, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="b1626-193">您可以使用任何其他的 Greenhouse 使用者帳戶建立工具或 Greenhouse 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="b1626-193">You can use any other Greenhouse user account creation tools or APIs provided by Greenhouse to provision AAD user accounts.</span></span> 

<span data-ttu-id="b1626-194">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b1626-194">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="b1626-195">以系統管理員身分登入您的 **Greenhouse** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="b1626-195">Log in to your **Greenhouse** company site as an administrator.</span></span>

2. <span data-ttu-id="b1626-196">在頂端的功能表中，按一下 [設定]，然後按一下 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="b1626-196">In the menu on the top, click **Configure**, and then click **Users**.</span></span>
   
   <span data-ttu-id="b1626-197">![使用者](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="b1626-197">![Users](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Users")</span></span>

3. <span data-ttu-id="b1626-198">按一下 [新使用者] 。</span><span class="sxs-lookup"><span data-stu-id="b1626-198">Click **New Users**.</span></span>
   
   <span data-ttu-id="b1626-199">![新增使用者](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="b1626-199">![New User](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "New User")</span></span>

4. <span data-ttu-id="b1626-200">在 [新增使用者]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b1626-200">In the **Add New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="b1626-201">![新增使用者](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="b1626-201">![Add New User](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Add New User")</span></span>

   <span data-ttu-id="b1626-202">a.</span><span class="sxs-lookup"><span data-stu-id="b1626-202">a.</span></span> <span data-ttu-id="b1626-203">在 [輸入使用者電子郵件]  文字方塊中，輸入您要佈建之有效 Azure Active Directory 帳戶的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="b1626-203">In the **Enter user emails** textbox, type the email address of a valid Azure Active Directory account you want to provision.</span></span>

   <span data-ttu-id="b1626-204">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b1626-204">b.</span></span> <span data-ttu-id="b1626-205">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b1626-205">Click **Save**.</span></span>    
   
      >[!NOTE]
      ><span data-ttu-id="b1626-206">Azure Active Directory 帳戶的持有者會收到一封包含連結的電子郵件，以在啟用帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="b1626-206">The Azure Active Directory account holders will receive an email including a link to confirm the account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b1626-207">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b1626-207">Assign the Azure AD test user</span></span>

<span data-ttu-id="b1626-208">在本節中，您會將 Greenhouse 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b1626-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Greenhouse.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="b1626-210">**若要將 Britta Simon 指派給 Greenhouse，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b1626-210">**To assign Britta Simon to Greenhouse, perform the following steps:**</span></span>

1. <span data-ttu-id="b1626-211">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b1626-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="b1626-213">在應用程式清單中，選取 [Greenhouse]。</span><span class="sxs-lookup"><span data-stu-id="b1626-213">In the applications list, select **Greenhouse**.</span></span>

    ![應用程式清單中的 Greenhouse 連結](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_app.png)  

3. <span data-ttu-id="b1626-215">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b1626-215">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="b1626-217">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b1626-217">Click **Add** button.</span></span> <span data-ttu-id="b1626-218">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b1626-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="b1626-220">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="b1626-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b1626-221">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b1626-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b1626-222">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b1626-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b1626-223">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="b1626-223">Test single sign-on</span></span>

<span data-ttu-id="b1626-224">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="b1626-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b1626-225">當您在存取面板中按一下 [Greenhouse] 磚時，應該會自動登入您的 Greenhouse 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b1626-225">When you click the Greenhouse tile in the Access Panel, you should get automatically signed-on to your Greenhouse application.</span></span>
<span data-ttu-id="b1626-226">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="b1626-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b1626-227">其他資源</span><span class="sxs-lookup"><span data-stu-id="b1626-227">Additional resources</span></span>

* [<span data-ttu-id="b1626-228">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="b1626-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b1626-229">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b1626-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_203.png


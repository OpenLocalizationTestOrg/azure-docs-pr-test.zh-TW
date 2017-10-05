---
title: "教學課程：Azure Active Directory 與 TigerText Secure Messenger 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 TigerText Secure Messenger 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03f1e128-5bcb-4e49-b6a3-fe22eedc6d5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: e101e5fc84b032b66dd0636bab8bff128791f77c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tigertext-secure-messenger"></a><span data-ttu-id="b3f1c-103">教學課程：Azure Active Directory 與 TigerText Secure Messenger 整合</span><span class="sxs-lookup"><span data-stu-id="b3f1c-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span></span>

<span data-ttu-id="b3f1c-104">在本教學課程中，您將了解如何整合 TigerText Secure Messenger 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-104">In this tutorial, you learn how to integrate TigerText Secure Messenger with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b3f1c-105">將 TigerText Secure Messenger 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="b3f1c-105">Integrating TigerText Secure Messenger with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b3f1c-106">您可以在 Azure AD 中控制可存取 TigerText Secure Messenger 的人員</span><span class="sxs-lookup"><span data-stu-id="b3f1c-106">You can control in Azure AD who has access to TigerText Secure Messenger</span></span>
- <span data-ttu-id="b3f1c-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 TigerText Secure Messenger (單一登入)</span><span class="sxs-lookup"><span data-stu-id="b3f1c-107">You can enable your users to automatically get signed-on to TigerText Secure Messenger (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b3f1c-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="b3f1c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b3f1c-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3f1c-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b3f1c-110">Prerequisites</span></span>

<span data-ttu-id="b3f1c-111">若要設定 Azure AD 與 TigerText Secure Messenger 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="b3f1c-111">To configure Azure AD integration with TigerText Secure Messenger, you need the following items:</span></span>

- <span data-ttu-id="b3f1c-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b3f1c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b3f1c-113">已啟用 TigerText Secure Messenger 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b3f1c-113">A TigerText Secure Messenger single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b3f1c-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b3f1c-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="b3f1c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b3f1c-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b3f1c-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b3f1c-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="b3f1c-118">Scenario description</span></span>
<span data-ttu-id="b3f1c-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b3f1c-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="b3f1c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b3f1c-121">從資源庫新增 TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="b3f1c-121">Add TigerText Secure Messenger from the gallery</span></span>
2. <span data-ttu-id="b3f1c-122">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b3f1c-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tigertext-secure-messenger-from-the-gallery"></a><span data-ttu-id="b3f1c-123">從資源庫新增 TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="b3f1c-123">Add TigerText Secure Messenger from the gallery</span></span>
<span data-ttu-id="b3f1c-124">若要設定將 TigerText Secure Messenger 整合到 Azure AD 中，您需要從資源庫將 TigerText Secure Messenger 新增到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-124">To configure the integration of TigerText Secure Messenger into Azure AD, you need to add TigerText Secure Messenger from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b3f1c-125">**若要從資源庫新增 TigerText Secure Messenger，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b3f1c-125">**To add TigerText Secure Messenger from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b3f1c-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b3f1c-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b3f1c-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="b3f1c-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="b3f1c-133">在搜尋方塊中，輸入 **TigerText Secure Messenger**，從結果面板中選取 [TigerText Secure Messenger]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-133">In the search box, type **TigerText Secure Messenger**, select **TigerText Secure Messenger** from result panel then click **Add** button to add the application.</span></span>

    ![從資源庫新增](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b3f1c-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b3f1c-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="b3f1c-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 TigerText Secure Messenger 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-136">In this section, you configure and test Azure AD single sign-on with TigerText Secure Messenger based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b3f1c-137">若要讓單一登入能夠運作，Azure AD 必須知道 TigerText Secure Messenger 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TigerText Secure Messenger is to a user in Azure AD.</span></span> <span data-ttu-id="b3f1c-138">換句話說，必須在 Azure AD 使用者和 TigerText Secure Messenger 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-138">In other words, a link relationship between an Azure AD user and the related user in TigerText Secure Messenger needs to be established.</span></span>

<span data-ttu-id="b3f1c-139">在 TigerText Secure Messenger 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-139">In TigerText Secure Messenger, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b3f1c-140">若要設定及測試與 TigerText Secure Messenger 搭配運作的 Azure AD 單一登入，您需要完成下列建構元素：</span><span class="sxs-lookup"><span data-stu-id="b3f1c-140">To configure and test Azure AD single sign-on with TigerText Secure Messenger, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b3f1c-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b3f1c-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b3f1c-143">**[建立 TigerText Secure Messenger 測試使用者](#create-a-tigertext-secure-messenger-test-user)** - 使 TigerText Secure Messenger 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-143">**[Create a TigerText Secure Messenger test user](#create-a-tigertext-secure-messenger-test-user)** - to have a counterpart of Britta Simon in TigerText Secure Messenger that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b3f1c-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b3f1c-145">**[測試單一登入](#test-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b3f1c-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b3f1c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b3f1c-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 TigerText Secure Messenger 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TigerText Secure Messenger application.</span></span>

<span data-ttu-id="b3f1c-148">**若要使用 TigerText Secure Messenger 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b3f1c-148">**To configure Azure AD single sign-on with TigerText Secure Messenger, perform the following steps:**</span></span>

1. <span data-ttu-id="b3f1c-149">在 Azure 入口網站的 [TigerText Secure Messenger] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-149">In the Azure portal, on the **TigerText Secure Messenger** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="b3f1c-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML 型登入](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_samlbase.png)

3. <span data-ttu-id="b3f1c-153">在 [TigerText Secure Messenger 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b3f1c-153">On the **TigerText Secure Messenger Domain and URLs** section, perform the following steps:</span></span>

    ![[TigerText Secure Messenger 網域與 URL] 區段](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_url.png)

    <span data-ttu-id="b3f1c-155">a.</span><span class="sxs-lookup"><span data-stu-id="b3f1c-155">a.</span></span> <span data-ttu-id="b3f1c-156">在 [登入 URL] 文字方塊中，輸入 URL：`https://home.tigertext.com`</span><span class="sxs-lookup"><span data-stu-id="b3f1c-156">In the **Sign-on URL** textbox, type URL as: `https://home.tigertext.com`</span></span>

    <span data-ttu-id="b3f1c-157">b.</span><span class="sxs-lookup"><span data-stu-id="b3f1c-157">b.</span></span> <span data-ttu-id="b3f1c-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span><span class="sxs-lookup"><span data-stu-id="b3f1c-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b3f1c-159">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-159">This value is not real.</span></span> <span data-ttu-id="b3f1c-160">請使用實際的「識別碼」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-160">Update this value with the actual Identifier.</span></span> <span data-ttu-id="b3f1c-161">請連絡 [TigerText Secure Messenger 用戶端支援小組](mailTo:prosupport@tigertext.com)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-161">Contact [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to get this value.</span></span> 
 
4. <span data-ttu-id="b3f1c-162">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![[SAML 簽署憑證] 區段](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_certificate.png) 

5. <span data-ttu-id="b3f1c-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-164">Click **Save** button.</span></span>

    ![[儲存] 按鈕](./media/active-directory-saas-tigertext-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b3f1c-166">若要取得為您的應用程式設定的單一登入，請連絡 [TigerText Secure Messenger 支援小組](mailTo:prosupport@tigertext.com)，並提供**下載的中繼資料**。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-166">To get single sign-on configured for your application, contact [TigerText Secure Messenger support team](mailTo:prosupport@tigertext.com) and provide them the **Downloaded metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="b3f1c-167">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="b3f1c-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b3f1c-168">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b3f1c-169">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b3f1c-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b3f1c-170">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b3f1c-170">Create an Azure AD test user</span></span>
<span data-ttu-id="b3f1c-171">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="b3f1c-173">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b3f1c-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b3f1c-174">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tigertext-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b3f1c-176">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![使用者與群組->所有使用者](./media/active-directory-saas-tigertext-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b3f1c-178">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![[新增] 按鈕](./media/active-directory-saas-tigertext-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b3f1c-180">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b3f1c-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![使用者對話方塊](./media/active-directory-saas-tigertext-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b3f1c-182">a.</span><span class="sxs-lookup"><span data-stu-id="b3f1c-182">a.</span></span> <span data-ttu-id="b3f1c-183">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b3f1c-184">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-184">b.</span></span> <span data-ttu-id="b3f1c-185">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b3f1c-186">c.</span><span class="sxs-lookup"><span data-stu-id="b3f1c-186">c.</span></span> <span data-ttu-id="b3f1c-187">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b3f1c-188">d.</span><span class="sxs-lookup"><span data-stu-id="b3f1c-188">d.</span></span> <span data-ttu-id="b3f1c-189">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-189">Click **Create**.</span></span>
 
### <a name="create-a-tigertext-secure-messenger-test-user"></a><span data-ttu-id="b3f1c-190">建立 TigerText Secure Messengerr 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b3f1c-190">Create a TigerText Secure Messenger test user</span></span>

<span data-ttu-id="b3f1c-191">在本節中，您要在 TigerText 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-191">In this section, you create a user called Britta Simon in TigerText.</span></span> <span data-ttu-id="b3f1c-192">請連絡 [TigerText Secure Messenger Client 支援小組](mailTo:prosupport@tigertext.com)，以在 TigerText 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-192">Please reach out to [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to add the users in the TigerText platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b3f1c-193">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b3f1c-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="b3f1c-194">在本節中，您會將 TigerText Secure Messenger 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TigerText Secure Messenger.</span></span>

![指派使用者][200] 

<span data-ttu-id="b3f1c-196">**若要將 Britta Simon 指派到 TigerText Secure Messenger，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="b3f1c-196">**To assign Britta Simon to TigerText Secure Messenger, perform the following steps:**</span></span>

1. <span data-ttu-id="b3f1c-197">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="b3f1c-199">在應用程式清單中，選取 [TigerText Secure Messenger]。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-199">In the applications list, select **TigerText Secure Messenger**.</span></span>

    ![應用程式清單中的 TigerText Secure Messenger](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_app.png) 

3. <span data-ttu-id="b3f1c-201">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-201">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="b3f1c-203">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-203">Click **Add** button.</span></span> <span data-ttu-id="b3f1c-204">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="b3f1c-206">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b3f1c-207">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b3f1c-208">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b3f1c-209">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="b3f1c-209">Test single sign-on</span></span>

<span data-ttu-id="b3f1c-210">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b3f1c-211">當您在存取面板中按一下 [TigerText] 圖格時，應該會自動登入您的 TigerText 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-211">When you click the TigerText tile in the Access Panel, you should get automatically signed-on to your TigerText application.</span></span> <span data-ttu-id="b3f1c-212">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="b3f1c-212">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b3f1c-213">其他資源</span><span class="sxs-lookup"><span data-stu-id="b3f1c-213">Additional resources</span></span>

* [<span data-ttu-id="b3f1c-214">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="b3f1c-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b3f1c-215">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b3f1c-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_203.png


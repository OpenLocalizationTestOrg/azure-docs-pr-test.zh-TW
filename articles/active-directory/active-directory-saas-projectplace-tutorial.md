---
title: "教學課程：Azure Active Directory 與 Projectplace 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Projectplace 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 298059ca-b652-4577-916a-c31393d53d7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: bb9dd10c887cb0e42e544066d9b0dcfa554e10ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-projectplace"></a><span data-ttu-id="36a27-103">教學課程：Azure Active Directory 與 Projectplace 整合</span><span class="sxs-lookup"><span data-stu-id="36a27-103">Tutorial: Azure Active Directory integration with Projectplace</span></span>

<span data-ttu-id="36a27-104">在本教學課程中，您將了解如何整合 Projectplace 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="36a27-104">In this tutorial, you learn how to integrate Projectplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="36a27-105">Projectplace 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="36a27-105">Integrating Projectplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="36a27-106">您可以在 Azure AD 中控制可存取 Projectplace 的人員</span><span class="sxs-lookup"><span data-stu-id="36a27-106">You can control in Azure AD who has access to Projectplace</span></span>
- <span data-ttu-id="36a27-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Projectplace (單一登入)</span><span class="sxs-lookup"><span data-stu-id="36a27-107">You can enable your users to automatically get signed-on to Projectplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="36a27-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="36a27-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="36a27-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="36a27-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36a27-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="36a27-110">Prerequisites</span></span>

<span data-ttu-id="36a27-111">若要設定 Azure AD 與 Projectplace 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="36a27-111">To configure Azure AD integration with Projectplace, you need the following items:</span></span>

- <span data-ttu-id="36a27-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="36a27-112">An Azure AD subscription</span></span>
- <span data-ttu-id="36a27-113">啟用 Projectplace 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="36a27-113">A Projectplace single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="36a27-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="36a27-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="36a27-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="36a27-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="36a27-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="36a27-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="36a27-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="36a27-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="36a27-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="36a27-118">Scenario description</span></span>
<span data-ttu-id="36a27-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="36a27-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="36a27-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="36a27-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="36a27-121">從資源庫新增 Projectplace</span><span class="sxs-lookup"><span data-stu-id="36a27-121">Adding Projectplace from the gallery</span></span>
2. <span data-ttu-id="36a27-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="36a27-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-projectplace-from-the-gallery"></a><span data-ttu-id="36a27-123">從資源庫新增 Projectplace</span><span class="sxs-lookup"><span data-stu-id="36a27-123">Adding Projectplace from the gallery</span></span>
<span data-ttu-id="36a27-124">若要設定將 Projectplace 整合到 Azure AD 中，您需要從資源庫將 Projectplace 加入受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="36a27-124">To configure the integration of Projectplace into Azure AD, you need to add Projectplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="36a27-125">**若要從資源庫新增 Projectplace，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="36a27-125">**To add Projectplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="36a27-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="36a27-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="36a27-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="36a27-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="36a27-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="36a27-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="36a27-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="36a27-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="36a27-133">在搜尋方塊中，輸入 **Projectplace**。</span><span class="sxs-lookup"><span data-stu-id="36a27-133">In the search box, type **Projectplace**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_search.png)

5. <span data-ttu-id="36a27-135">在結果窗格中，選取 [Projectplace]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="36a27-135">In the results panel, select **Projectplace**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="36a27-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="36a27-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="36a27-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Projectplace 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="36a27-138">In this section, you configure and test Azure AD single sign-on with Projectplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="36a27-139">若要讓單一登入運作，Azure AD 必須知道 Projectplace 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="36a27-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Projectplace is to a user in Azure AD.</span></span> <span data-ttu-id="36a27-140">換句話說，必須在 Azure AD 使用者和 Projectplace 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="36a27-140">In other words, a link relationship between an Azure AD user and the related user in Projectplace needs to be established.</span></span>

<span data-ttu-id="36a27-141">在 Projectplace 中，將**使用者名稱**的值指派為 Azure AD 中**使用者名稱**的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="36a27-141">In Projectplace, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="36a27-142">若要使用 Projectplace 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="36a27-142">To configure and test Azure AD single sign-on with Projectplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="36a27-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="36a27-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="36a27-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="36a27-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="36a27-145">**[建立 Projectplace 測試使用者](#creating-a-projectplace-test-user)** - 使 Projectplace 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="36a27-145">**[Creating a Projectplace test user](#creating-a-projectplace-test-user)** - to have a counterpart of Britta Simon in Projectplace that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="36a27-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="36a27-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="36a27-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="36a27-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="36a27-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="36a27-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="36a27-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Projectplace 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="36a27-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Projectplace application.</span></span>

<span data-ttu-id="36a27-150">**若要使用 Projectplace 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="36a27-150">**To configure Azure AD single sign-on with Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="36a27-151">在 Azure 入口網站的 [Projectplace] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="36a27-151">In the Azure portal, on the **Projectplace** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="36a27-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="36a27-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_samlbase.png)

3. <span data-ttu-id="36a27-155">在 [Projectplace 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="36a27-155">On the **Projectplace Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_url.png)

    <span data-ttu-id="36a27-157">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<company>.projectplace.com`</span><span class="sxs-lookup"><span data-stu-id="36a27-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.projectplace.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="36a27-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="36a27-158">This value is not real.</span></span> <span data-ttu-id="36a27-159">請使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="36a27-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="36a27-160">請連絡 [Projectplace 客戶支援小組](https://success.planview.com/Projectplace/Support)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="36a27-160">Contact [Projectplace Client support team](https://success.planview.com/Projectplace/Support) to get this value.</span></span> 
 
4. <span data-ttu-id="36a27-161">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="36a27-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_certificate.png) 

5. <span data-ttu-id="36a27-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="36a27-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-projectplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="36a27-165">若要在 **Projectplace** 端設定單一登入，您必須將已下載的**中繼資料 XML** 傳送給 [Projectplace 支援小組](https://success.planview.com/Projectplace/Support)。</span><span class="sxs-lookup"><span data-stu-id="36a27-165">To configure single sign-on on **Projectplace** side, you need to send the downloaded **Metadata XML** to [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="36a27-166">他們會進行此設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="36a27-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="36a27-167">單一登入設定必須由 [Projectplace 支援小組](https://success.planview.com/Projectplace/Support)執行。</span><span class="sxs-lookup"><span data-stu-id="36a27-167">The single sign-on configuration has to be performed by the [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="36a27-168">設定完成後，您將會收到通知。</span><span class="sxs-lookup"><span data-stu-id="36a27-168">You will get a notification as soon as the configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="36a27-169">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="36a27-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="36a27-170">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="36a27-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="36a27-171">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="36a27-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="36a27-172">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="36a27-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="36a27-173">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="36a27-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="36a27-175">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="36a27-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="36a27-176">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="36a27-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-projectplace-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="36a27-178">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="36a27-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-projectplace-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="36a27-180">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="36a27-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-projectplace-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="36a27-182">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="36a27-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-projectplace-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="36a27-184">a.</span><span class="sxs-lookup"><span data-stu-id="36a27-184">a.</span></span> <span data-ttu-id="36a27-185">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="36a27-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="36a27-186">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="36a27-186">b.</span></span> <span data-ttu-id="36a27-187">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="36a27-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="36a27-188">c.</span><span class="sxs-lookup"><span data-stu-id="36a27-188">c.</span></span> <span data-ttu-id="36a27-189">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="36a27-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="36a27-190">d.</span><span class="sxs-lookup"><span data-stu-id="36a27-190">d.</span></span> <span data-ttu-id="36a27-191">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="36a27-191">Click **Create**.</span></span>
 
### <a name="creating-a-projectplace-test-user"></a><span data-ttu-id="36a27-192">建立 Projectplace 測試使用者</span><span class="sxs-lookup"><span data-stu-id="36a27-192">Creating a Projectplace test user</span></span>

<span data-ttu-id="36a27-193">為了讓 Azure AD 使用者能夠登入 Projectplace，必須將他們佈建到 Projectplace。</span><span class="sxs-lookup"><span data-stu-id="36a27-193">In order to enable Azure AD users to log into Projectplace, they must be provisioned into Projectplace.</span></span> <span data-ttu-id="36a27-194">Projectplace 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="36a27-194">In the case of Projectplace, provisioning is a manual task.</span></span>

<span data-ttu-id="36a27-195">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="36a27-195">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="36a27-196">以系統管理員身分登入您的 **Projectplace** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="36a27-196">Log in to your **Projectplace** company site as an administrator.</span></span>

2. <span data-ttu-id="36a27-197">移至 [人員]，然後按一下 [成員]。</span><span class="sxs-lookup"><span data-stu-id="36a27-197">Go to **People**, and then click **Members**.</span></span>
   
    <span data-ttu-id="36a27-198">![People](./media/active-directory-saas-projectplace-tutorial/ic790228.png "People")</span><span class="sxs-lookup"><span data-stu-id="36a27-198">![People](./media/active-directory-saas-projectplace-tutorial/ic790228.png "People")</span></span>

3. <span data-ttu-id="36a27-199">按一下 [新增成員] 。</span><span class="sxs-lookup"><span data-stu-id="36a27-199">Click **Add Member**.</span></span>
   
    <span data-ttu-id="36a27-200">![新增成員](./media/active-directory-saas-projectplace-tutorial/ic790232.png "新增成員")</span><span class="sxs-lookup"><span data-stu-id="36a27-200">![Add Members](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Add Members")</span></span>

4. <span data-ttu-id="36a27-201">在 [新增成員]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="36a27-201">In the **Add Member** section, perform the following steps:</span></span>
   
    <span data-ttu-id="36a27-202">![新成員](./media/active-directory-saas-projectplace-tutorial/ic790233.png "新成員")</span><span class="sxs-lookup"><span data-stu-id="36a27-202">![New Members](./media/active-directory-saas-projectplace-tutorial/ic790233.png "New Members")</span></span>
   
    <span data-ttu-id="36a27-203">a.</span><span class="sxs-lookup"><span data-stu-id="36a27-203">a.</span></span> <span data-ttu-id="36a27-204">在 [新成員]  文字方塊中，於相關文字方塊中輸入您想要佈建之有效 AAD 帳戶的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="36a27-204">In the **New Members** textbox, type the email address of a valid AAD account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="36a27-205">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="36a27-205">b.</span></span> <span data-ttu-id="36a27-206">按一下 [ **傳送**]。</span><span class="sxs-lookup"><span data-stu-id="36a27-206">Click **Send**.</span></span>

   <span data-ttu-id="36a27-207">系統會傳送一封電子郵件給 Azure Active Directory 帳戶的持有者，郵件中包含用來在啟用帳戶前確認帳戶的連結。</span><span class="sxs-lookup"><span data-stu-id="36a27-207">An email including a link to confirm the account before it becomes active is sent to the Azure Active Directory account holder.</span></span>

>[!NOTE]
><span data-ttu-id="36a27-208">您可以使用任何其他的 Projectplace 使用者帳戶建立工具或 Projectplace 提供的 API，佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="36a27-208">You can use any other Projectplace user account creation tools or APIs provided by Projectplace to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="36a27-209">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="36a27-209">Assigning the Azure AD test user</span></span>

<span data-ttu-id="36a27-210">在本節中，您會將 Projectplace 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="36a27-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Projectplace.</span></span>

![指派使用者][200] 

<span data-ttu-id="36a27-212">**若要將 Britta Simon 指派到 Projectplace，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="36a27-212">**To assign Britta Simon to Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="36a27-213">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="36a27-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="36a27-215">在應用程式清單中，選取 **Projectplace**。</span><span class="sxs-lookup"><span data-stu-id="36a27-215">In the applications list, select **Projectplace**.</span></span>

    ![設定單一登入](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_app.png) 

3. <span data-ttu-id="36a27-217">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="36a27-217">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="36a27-219">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="36a27-219">Click **Add** button.</span></span> <span data-ttu-id="36a27-220">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="36a27-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="36a27-222">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="36a27-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="36a27-223">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="36a27-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="36a27-224">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="36a27-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="36a27-225">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="36a27-225">Testing single sign-on</span></span>

<span data-ttu-id="36a27-226">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="36a27-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="36a27-227">當您在存取面板中按一下 [Projectplace] 圖格時，應該會自動登入您的 Projectplace 應用程式。</span><span class="sxs-lookup"><span data-stu-id="36a27-227">When you click the Projectplace tile in the Access Panel, you should get automatically signed-on to your Projectplace application.</span></span>
<span data-ttu-id="36a27-228">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="36a27-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="36a27-229">其他資源</span><span class="sxs-lookup"><span data-stu-id="36a27-229">Additional resources</span></span>

* [<span data-ttu-id="36a27-230">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="36a27-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="36a27-231">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="36a27-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_203.png


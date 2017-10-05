---
title: "教學課程：Azure Active Directory 與 Wikispaces 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Wikispaces 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 665b95aa-f7f5-4406-9e2a-6fc299a1599c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: d01543955bdf6a274571f67eafdff5f637863d5c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wikispaces"></a><span data-ttu-id="3eb0d-103">教學課程：Azure Active Directory 與 Wikispaces 整合</span><span class="sxs-lookup"><span data-stu-id="3eb0d-103">Tutorial: Azure Active Directory integration with Wikispaces</span></span>

<span data-ttu-id="3eb0d-104">在本教學課程中，您將了解如何整合 Wikispaces 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-104">In this tutorial, you learn how to integrate Wikispaces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3eb0d-105">Wikispaces 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="3eb0d-105">Integrating Wikispaces with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3eb0d-106">您可以在 Azure AD 中控制可存取 Wikispaces 的人員</span><span class="sxs-lookup"><span data-stu-id="3eb0d-106">You can control in Azure AD who has access to Wikispaces</span></span>
- <span data-ttu-id="3eb0d-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Wikispaces (單一登入)</span><span class="sxs-lookup"><span data-stu-id="3eb0d-107">You can enable your users to automatically get signed-on to Wikispaces (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3eb0d-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="3eb0d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3eb0d-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3eb0d-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="3eb0d-110">Prerequisites</span></span>

<span data-ttu-id="3eb0d-111">如要設定 Azure AD 與 Wikispaces 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="3eb0d-111">To configure Azure AD integration with Wikispaces, you need the following items:</span></span>

- <span data-ttu-id="3eb0d-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3eb0d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3eb0d-113">已啟用 Wikispaces 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3eb0d-113">A Wikispaces single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3eb0d-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3eb0d-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="3eb0d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3eb0d-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3eb0d-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3eb0d-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="3eb0d-118">Scenario description</span></span>
<span data-ttu-id="3eb0d-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3eb0d-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="3eb0d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3eb0d-121">從資源庫新增 Wikispaces</span><span class="sxs-lookup"><span data-stu-id="3eb0d-121">Adding Wikispaces from the gallery</span></span>
2. <span data-ttu-id="3eb0d-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3eb0d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wikispaces-from-the-gallery"></a><span data-ttu-id="3eb0d-123">從資源庫新增 Wikispaces</span><span class="sxs-lookup"><span data-stu-id="3eb0d-123">Adding Wikispaces from the gallery</span></span>
<span data-ttu-id="3eb0d-124">若要設定將 Wikispaces 整合到 Azure AD 中，您需要從資源庫將 Wikispaces 新增到受管理的 SaaS app 清單。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-124">To configure the integration of Wikispaces into Azure AD, you need to add Wikispaces from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3eb0d-125">**若要從資源庫新增 Wikispaces，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3eb0d-125">**To add Wikispaces from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3eb0d-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3eb0d-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3eb0d-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="3eb0d-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="3eb0d-133">在搜尋方塊中，輸入 **Wikispaces**。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-133">In the search box, type **Wikispaces**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_search.png)

5. <span data-ttu-id="3eb0d-135">在結果窗格中，選取 [Wikispaces]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-135">In the results panel, select **Wikispaces**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3eb0d-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3eb0d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3eb0d-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Wikispaces 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-138">In this section, you configure and test Azure AD single sign-on with Wikispaces based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3eb0d-139">若要讓單一登入能夠運作，Azure AD 必須知道 Wikispaces 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Wikispaces is to a user in Azure AD.</span></span> <span data-ttu-id="3eb0d-140">換句話說，必須在 Azure AD 使用者和 Wikispaces 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-140">In other words, a link relationship between an Azure AD user and the related user in Wikispaces needs to be established.</span></span>

<span data-ttu-id="3eb0d-141">在 Wikispaces 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-141">In Wikispaces, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3eb0d-142">若要設定及測試與 Wikispaces 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="3eb0d-142">To configure and test Azure AD single sign-on with Wikispaces, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3eb0d-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3eb0d-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3eb0d-145">**[建立 Wikispaces 測試使用者](#creating-a-wikispaces-test-user)** - 在 Wikispaces 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-145">**[Creating a Wikispaces test user](#creating-a-wikispaces-test-user)** - to have a counterpart of Britta Simon in Wikispaces that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3eb0d-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3eb0d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3eb0d-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3eb0d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3eb0d-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Wikispaces 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wikispaces application.</span></span>

<span data-ttu-id="3eb0d-150">**若要使用 Wikispaces 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3eb0d-150">**To configure Azure AD single sign-on with Wikispaces, perform the following steps:**</span></span>

1. <span data-ttu-id="3eb0d-151">在 Azure 入口網站的 [Wikispaces] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-151">In the Azure portal, on the **Wikispaces** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="3eb0d-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_samlbase.png)

3. <span data-ttu-id="3eb0d-155">在 [Wikispaces 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3eb0d-155">On the **Wikispaces Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_url.png)

    <span data-ttu-id="3eb0d-157">a.</span><span class="sxs-lookup"><span data-stu-id="3eb0d-157">a.</span></span> <span data-ttu-id="3eb0d-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.wikispaces.net`</span><span class="sxs-lookup"><span data-stu-id="3eb0d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.wikispaces.net`</span></span>

    <span data-ttu-id="3eb0d-159">b.</span><span class="sxs-lookup"><span data-stu-id="3eb0d-159">b.</span></span> <span data-ttu-id="3eb0d-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://session.wikispaces.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="3eb0d-160">In the **Identifier** textbox, type a URL using the following pattern: `https://session.wikispaces.net/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3eb0d-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-161">These values are not real.</span></span> <span data-ttu-id="3eb0d-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3eb0d-163">請連絡 [Wikispaces 客戶支援小組](https://www.wikispaces.com/site/help)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-163">Contact [Wikispaces Client support team](https://www.wikispaces.com/site/help) to get these values.</span></span> 

4. <span data-ttu-id="3eb0d-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_certificate.png) 

5. <span data-ttu-id="3eb0d-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-wikispaces-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3eb0d-168">若要在 **Wikispaces** 端設定單一登入，您必須將已下載的**中繼資料 XML** 傳送給 [Wikispaces 支援小組](https://www.wikispaces.com/site/help)。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-168">To configure single sign-on on **Wikispaces** side, you need to send the downloaded **Metadata XML** to [Wikispaces support team](https://www.wikispaces.com/site/help).</span></span> <span data-ttu-id="3eb0d-169">設定完成後，您將會收到通知。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-169">You will get a notification as soon as the configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="3eb0d-170">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="3eb0d-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3eb0d-171">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3eb0d-172">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3eb0d-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3eb0d-173">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3eb0d-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="3eb0d-174">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="3eb0d-176">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3eb0d-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3eb0d-177">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3eb0d-179">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3eb0d-181">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3eb0d-183">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3eb0d-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3eb0d-185">a.</span><span class="sxs-lookup"><span data-stu-id="3eb0d-185">a.</span></span> <span data-ttu-id="3eb0d-186">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3eb0d-187">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-187">b.</span></span> <span data-ttu-id="3eb0d-188">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3eb0d-189">c.</span><span class="sxs-lookup"><span data-stu-id="3eb0d-189">c.</span></span> <span data-ttu-id="3eb0d-190">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3eb0d-191">d.</span><span class="sxs-lookup"><span data-stu-id="3eb0d-191">d.</span></span> <span data-ttu-id="3eb0d-192">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-192">Click **Create**.</span></span>
 
### <a name="creating-a-wikispaces-test-user"></a><span data-ttu-id="3eb0d-193">建立 Wikispaces 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3eb0d-193">Creating a Wikispaces test user</span></span>

<span data-ttu-id="3eb0d-194">若要讓 Azure AD 使用者可以登入 Wikispaces，則必須將他們佈建到 Wikispaces。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-194">In order to enable Azure AD users to log in to Wikispaces, they must be provisioned into Wikispaces.</span></span> <span data-ttu-id="3eb0d-195">Wikispaces 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-195">In the case of Wikispaces, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="3eb0d-196">若要佈建使用者帳戶，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3eb0d-196">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="3eb0d-197">以系統管理員身分登入您的 **Wikispaces** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-197">Log in to your **Wikispaces** company site as an administrator.</span></span>

2. <span data-ttu-id="3eb0d-198">移至 [成員] 。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-198">Go to **Members**.</span></span>
   
    <span data-ttu-id="3eb0d-199">![成員](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "成員")</span><span class="sxs-lookup"><span data-stu-id="3eb0d-199">![Members](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "Members")</span></span>

3. <span data-ttu-id="3eb0d-200">按一下 [邀請人員] 。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-200">Click the **Invite People**.</span></span>
   
    <span data-ttu-id="3eb0d-201">![邀請人員](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "邀請人員")</span><span class="sxs-lookup"><span data-stu-id="3eb0d-201">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "Invite People")</span></span>

4. <span data-ttu-id="3eb0d-202">在 [邀請人員]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3eb0d-202">In the **Invite People** section, perform the following steps:</span></span>
   
    <span data-ttu-id="3eb0d-203">![邀請人員](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "邀請人員")</span><span class="sxs-lookup"><span data-stu-id="3eb0d-203">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "Invite People")</span></span>
   
    <span data-ttu-id="3eb0d-204">a.</span><span class="sxs-lookup"><span data-stu-id="3eb0d-204">a.</span></span> <span data-ttu-id="3eb0d-205">在相關的文字方塊中，輸入您想要佈建之有效 AAD 帳戶 **使用者名稱或電子郵件地址** 。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-205">Type the **Usernames or Email Address** of a valid AAD account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="3eb0d-206">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-206">b.</span></span> <span data-ttu-id="3eb0d-207">按一下 [ **傳送**]。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-207">Click **Send**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="3eb0d-208">Azure Active Directory 帳戶的持有者會收到一封包含連結的電子郵件，以在啟用帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-208">The Azure Active Directory account holder receives an email including a link to confirm the account before it becomes active.</span></span>
    
> [!NOTE]
> <span data-ttu-id="3eb0d-209">您可以使用任何其他的 Wikispaces 使用者帳戶建立工具或 Wikispaces 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-209">You can use any other Wikispaces user account creation tools or APIs provided by Wikispaces to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3eb0d-210">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3eb0d-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3eb0d-211">在本節中，您會將 Wikispaces 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wikispaces.</span></span>

![指派使用者][200] 

<span data-ttu-id="3eb0d-213">**若要將 Britta Simon 指派給 Wikispaces，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3eb0d-213">**To assign Britta Simon to Wikispaces, perform the following steps:**</span></span>

1. <span data-ttu-id="3eb0d-214">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="3eb0d-216">在應用程式清單中，選取 [Wikispaces]。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-216">In the applications list, select **Wikispaces**.</span></span>

    ![設定單一登入](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_app.png) 

3. <span data-ttu-id="3eb0d-218">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-218">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="3eb0d-220">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-220">Click **Add** button.</span></span> <span data-ttu-id="3eb0d-221">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="3eb0d-223">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3eb0d-224">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3eb0d-225">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3eb0d-226">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="3eb0d-226">Testing single sign-on</span></span>

<span data-ttu-id="3eb0d-227">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3eb0d-228">當您在「存取面板」中按一下 [Wikispaces] 圖格時，應該會自動登入您的 Wikispaces 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-228">When you click the Wikispaces tile in the Access Panel, you should get automatically signed-on to your Wikispaces application.</span></span>
<span data-ttu-id="3eb0d-229">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="3eb0d-229">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3eb0d-230">其他資源</span><span class="sxs-lookup"><span data-stu-id="3eb0d-230">Additional resources</span></span>

* [<span data-ttu-id="3eb0d-231">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="3eb0d-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3eb0d-232">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="3eb0d-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_203.png

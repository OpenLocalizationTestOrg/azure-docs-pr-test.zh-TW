---
title: "教學課程：Azure Active Directory 與 15Five 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 15Five 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2fb301c2-7d7a-4046-8ee1-7dc9e7684806
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: ea36774747a0fcfa4ace1aefb2d46dba815d92c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-15five"></a><span data-ttu-id="5e179-103">教學課程：Azure Active Directory 與 15Five 整合</span><span class="sxs-lookup"><span data-stu-id="5e179-103">Tutorial: Azure Active Directory integration with 15Five</span></span>

<span data-ttu-id="5e179-104">在本教學課程中，您將了解如何整合 15Five 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="5e179-104">In this tutorial, you learn how to integrate 15Five with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5e179-105">15Five 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="5e179-105">Integrating 15Five with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5e179-106">您可以在 Azure AD 中控制可存取 15Five 的人員</span><span class="sxs-lookup"><span data-stu-id="5e179-106">You can control in Azure AD who has access to 15Five</span></span>
- <span data-ttu-id="5e179-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 15Five (單一登入)</span><span class="sxs-lookup"><span data-stu-id="5e179-107">You can enable your users to automatically get signed-on to 15Five (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5e179-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="5e179-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5e179-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="5e179-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e179-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="5e179-110">Prerequisites</span></span>

<span data-ttu-id="5e179-111">若要設定 Azure AD 與 15Five 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="5e179-111">To configure Azure AD integration with 15Five, you need the following items:</span></span>

- <span data-ttu-id="5e179-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5e179-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5e179-113">啟用 15Five 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5e179-113">A 15Five single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5e179-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5e179-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5e179-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="5e179-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5e179-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5e179-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5e179-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="5e179-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5e179-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="5e179-118">Scenario description</span></span>
<span data-ttu-id="5e179-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5e179-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5e179-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="5e179-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5e179-121">從資源庫新增 15Five</span><span class="sxs-lookup"><span data-stu-id="5e179-121">Adding 15Five from the gallery</span></span>
2. <span data-ttu-id="5e179-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5e179-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-15five-from-the-gallery"></a><span data-ttu-id="5e179-123">從資源庫新增 15Five</span><span class="sxs-lookup"><span data-stu-id="5e179-123">Adding 15Five from the gallery</span></span>
<span data-ttu-id="5e179-124">若要設定 15Five 與 Azure AD 整合，您需要從資源庫將 15Five 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="5e179-124">To configure the integration of 15Five into Azure AD, you need to add 15Five from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5e179-125">**若要從資源庫新增 15Five，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5e179-125">**To add 15Five from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5e179-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="5e179-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5e179-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5e179-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5e179-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5e179-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="5e179-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5e179-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="5e179-133">在搜尋方塊中，鍵入 **15Five**。</span><span class="sxs-lookup"><span data-stu-id="5e179-133">In the search box, type **15Five**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-15five-tutorial/tutorial_15five_search.png)

5. <span data-ttu-id="5e179-135">在結果窗格中，選取 [15Five]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e179-135">In the results panel, select **15Five**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-15five-tutorial/tutorial_15five_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5e179-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5e179-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5e179-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 15Five 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5e179-138">In this section, you configure and test Azure AD single sign-on with 15Five based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5e179-139">若要讓單一登入運作，Azure AD 必須知道 15Five 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="5e179-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 15Five is to a user in Azure AD.</span></span> <span data-ttu-id="5e179-140">換句話說，必須在 Azure AD 使用者和 15Five 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5e179-140">In other words, a link relationship between an Azure AD user and the related user in 15Five needs to be established.</span></span>

<span data-ttu-id="5e179-141">在 15Five 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5e179-141">In 15Five, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5e179-142">若要設定及測試與 15Five 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="5e179-142">To configure and test Azure AD single sign-on with 15Five, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5e179-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="5e179-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5e179-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5e179-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5e179-145">**[建立 15Five 測試使用者](#creating-a-15five-test-user)** - 在 15Five 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="5e179-145">**[Creating a 15Five test user](#creating-a-15five-test-user)** - to have a counterpart of Britta Simon in 15Five that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5e179-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5e179-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5e179-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="5e179-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5e179-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5e179-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5e179-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 15Five 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="5e179-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 15Five application.</span></span>

<span data-ttu-id="5e179-150">**若要設定與 15Five 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5e179-150">**To configure Azure AD single sign-on with 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="5e179-151">在 Azure 入口網站的 [15Five] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="5e179-151">In the Azure portal, on the **15Five** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="5e179-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="5e179-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-15five-tutorial/tutorial_15five_samlbase.png)

3. <span data-ttu-id="5e179-155">在 [15Five 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5e179-155">On the **15Five Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-15five-tutorial/tutorial_15five_url.png)

    <span data-ttu-id="5e179-157">a.</span><span class="sxs-lookup"><span data-stu-id="5e179-157">a.</span></span> <span data-ttu-id="5e179-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.15five.com`</span><span class="sxs-lookup"><span data-stu-id="5e179-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.15five.com`</span></span>

    <span data-ttu-id="5e179-159">b.</span><span class="sxs-lookup"><span data-stu-id="5e179-159">b.</span></span> <span data-ttu-id="5e179-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<companyname>.15five.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="5e179-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.15five.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5e179-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="5e179-161">These values are not real.</span></span> <span data-ttu-id="5e179-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="5e179-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5e179-163">請連絡 [15Five 用戶端支援小組](https://www.15five.com/contact/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="5e179-163">Contact [15Five Client support team](https://www.15five.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="5e179-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="5e179-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-15five-tutorial/tutorial_15five_certificate.png) 

5. <span data-ttu-id="5e179-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="5e179-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-15five-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5e179-168">若要在 **15Five** 端設定單一登入，您必須將已下載的**中繼資料 XML** 傳送給 [15Five 支援小組](https://www.15five.com/contact/)。</span><span class="sxs-lookup"><span data-stu-id="5e179-168">To configure single sign-on on **15Five** side, you need to send the downloaded **Metadata XML** to [15Five support team](https://www.15five.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="5e179-169">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="5e179-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5e179-170">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="5e179-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5e179-171">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5e179-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5e179-172">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5e179-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="5e179-173">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="5e179-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="5e179-175">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5e179-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5e179-176">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="5e179-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-15five-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5e179-178">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="5e179-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-15five-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5e179-180">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5e179-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-15five-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5e179-182">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5e179-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-15five-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5e179-184">a.</span><span class="sxs-lookup"><span data-stu-id="5e179-184">a.</span></span> <span data-ttu-id="5e179-185">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="5e179-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5e179-186">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e179-186">b.</span></span> <span data-ttu-id="5e179-187">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="5e179-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5e179-188">c.</span><span class="sxs-lookup"><span data-stu-id="5e179-188">c.</span></span> <span data-ttu-id="5e179-189">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="5e179-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5e179-190">d.</span><span class="sxs-lookup"><span data-stu-id="5e179-190">d.</span></span> <span data-ttu-id="5e179-191">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5e179-191">Click **Create**.</span></span>
 
### <a name="creating-a-15five-test-user"></a><span data-ttu-id="5e179-192">建立 15Five 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5e179-192">Creating a 15Five test user</span></span>

<span data-ttu-id="5e179-193">若要讓 Azure AD 使用者能夠登入 15Five，必須將他們佈建到 15Five。</span><span class="sxs-lookup"><span data-stu-id="5e179-193">To enable Azure AD users to log in to 15Five, they must be provisioned into 15Five.</span></span> <span data-ttu-id="5e179-194">15Five 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="5e179-194">When 15Five, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="5e179-195">若要設定使用者佈建，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5e179-195">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="5e179-196">以系統管理員身分登入您的 **15Five** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="5e179-196">Log in to your **15Five** company site as administrator.</span></span>

2. <span data-ttu-id="5e179-197">移至 [管理公司] 。</span><span class="sxs-lookup"><span data-stu-id="5e179-197">Go to **Manage Company**.</span></span>
   
    <span data-ttu-id="5e179-198">![管理公司](./media/active-directory-saas-15five-tutorial/IC784675.png "管理公司")</span><span class="sxs-lookup"><span data-stu-id="5e179-198">![Manage Company](./media/active-directory-saas-15five-tutorial/IC784675.png "Manage Company")</span></span>

3. <span data-ttu-id="5e179-199">移至 [人員]\>[新增人員]。</span><span class="sxs-lookup"><span data-stu-id="5e179-199">Go to **People \> Add People**.</span></span>
   
    <span data-ttu-id="5e179-200">![人員](./media/active-directory-saas-15five-tutorial/IC784676.png "人員")</span><span class="sxs-lookup"><span data-stu-id="5e179-200">![People](./media/active-directory-saas-15five-tutorial/IC784676.png "People")</span></span>

4. <span data-ttu-id="5e179-201">在 [新增人員] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5e179-201">In the Add New Person section, perform the following steps:</span></span>
   
    <span data-ttu-id="5e179-202">![新增人員](./media/active-directory-saas-15five-tutorial/IC784677.png "新增人員")</span><span class="sxs-lookup"><span data-stu-id="5e179-202">![Add New Person](./media/active-directory-saas-15five-tutorial/IC784677.png "Add New Person")</span></span>
   
    <span data-ttu-id="5e179-203">a.</span><span class="sxs-lookup"><span data-stu-id="5e179-203">a.</span></span> <span data-ttu-id="5e179-204">在相關的文字方塊中，輸入您想要佈建之有效 Azure Active Directory 帳戶的 [名字]、[姓氏]、[職稱]、[電子郵件地址]。</span><span class="sxs-lookup"><span data-stu-id="5e179-204">Type the **First Name**, **Last Name**, **Title**, **Email address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="5e179-205">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e179-205">b.</span></span> <span data-ttu-id="5e179-206">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="5e179-206">Click **Done**.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="5e179-207">Azure AD 帳戶的持有者會收到一封包含連結的電子郵件，以在啟用帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="5e179-207">The Azure AD account holder receives an email including a link to confirm the account before it becomes active.</span></span>
   
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5e179-208">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5e179-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5e179-209">在本節中，您會將 15Five 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5e179-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 15Five.</span></span>

![指派使用者][200] 

<span data-ttu-id="5e179-211">**若要將 Britta Simon 指派給 15Five，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5e179-211">**To assign Britta Simon to 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="5e179-212">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5e179-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="5e179-214">在應用程式清單中，選取 [15Five]。</span><span class="sxs-lookup"><span data-stu-id="5e179-214">In the applications list, select **15Five**.</span></span>

    ![設定單一登入](./media/active-directory-saas-15five-tutorial/tutorial_15five_app.png) 

3. <span data-ttu-id="5e179-216">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5e179-216">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="5e179-218">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5e179-218">Click **Add** button.</span></span> <span data-ttu-id="5e179-219">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5e179-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="5e179-221">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="5e179-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5e179-222">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5e179-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5e179-223">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5e179-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5e179-224">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="5e179-224">Testing single sign-on</span></span>

<span data-ttu-id="5e179-225">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="5e179-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5e179-226">當您在存取面板中按一下 [15Five] 磚時，應該會看到 15Five 應用程式的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="5e179-226">When you click the 15Five tile in the Access Panel, you should get login page of 15Five application.</span></span>
<span data-ttu-id="5e179-227">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="5e179-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5e179-228">其他資源</span><span class="sxs-lookup"><span data-stu-id="5e179-228">Additional resources</span></span>

* [<span data-ttu-id="5e179-229">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="5e179-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5e179-230">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="5e179-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-15five-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-15five-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-15five-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-15five-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-15five-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-15five-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-15five-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-15five-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-15five-tutorial/tutorial_general_203.png


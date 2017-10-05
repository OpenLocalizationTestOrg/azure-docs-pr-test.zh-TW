---
title: "教學課程：Azure Active Directory 與 EmpCenter 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 EmpCenter 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a00ecf6e-917a-4284-b998-41506931585e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: aa27175165f4b15477bef4e70ad1c25016db31a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-empcenter"></a><span data-ttu-id="e0584-103">教學課程：Azure Active Directory 與 EmpCenter 整合</span><span class="sxs-lookup"><span data-stu-id="e0584-103">Tutorial: Azure Active Directory integration with EmpCenter</span></span>

<span data-ttu-id="e0584-104">在本教學課程中，您將了解如何整合 EmpCenter 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="e0584-104">In this tutorial, you learn how to integrate EmpCenter with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e0584-105">EmpCenter 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="e0584-105">Integrating EmpCenter with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e0584-106">您可以在 Azure AD 中管控可存取 EmpCenter 的人員</span><span class="sxs-lookup"><span data-stu-id="e0584-106">You can control in Azure AD who has access to EmpCenter</span></span>
- <span data-ttu-id="e0584-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 EmpCenter (單一登入)</span><span class="sxs-lookup"><span data-stu-id="e0584-107">You can enable your users to automatically get signed-on to EmpCenter (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e0584-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="e0584-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e0584-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="e0584-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0584-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="e0584-110">Prerequisites</span></span>

<span data-ttu-id="e0584-111">若要設定 Azure AD 與 EmpCenter 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="e0584-111">To configure Azure AD integration with EmpCenter, you need the following items:</span></span>

- <span data-ttu-id="e0584-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e0584-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e0584-113">啟用 EmpCenter 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e0584-113">An EmpCenter single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e0584-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e0584-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e0584-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="e0584-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e0584-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e0584-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e0584-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="e0584-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e0584-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="e0584-118">Scenario description</span></span>
<span data-ttu-id="e0584-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e0584-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e0584-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="e0584-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e0584-121">從資源庫新增 EmpCenter</span><span class="sxs-lookup"><span data-stu-id="e0584-121">Adding EmpCenter from the gallery</span></span>
2. <span data-ttu-id="e0584-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e0584-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-empcenter-from-the-gallery"></a><span data-ttu-id="e0584-123">從資源庫新增 EmpCenter</span><span class="sxs-lookup"><span data-stu-id="e0584-123">Adding EmpCenter from the gallery</span></span>
<span data-ttu-id="e0584-124">若要設定將 EmpCenter 整合到 Azure AD 中，您需要從資源庫將 EmpCenter 新增到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="e0584-124">To configure the integration of EmpCenter into Azure AD, you need to add EmpCenter from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e0584-125">**若要從資源庫新增 EmpCenter，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e0584-125">**To add EmpCenter from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e0584-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e0584-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e0584-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e0584-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e0584-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e0584-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="e0584-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e0584-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="e0584-133">在搜尋方塊中，輸入 **EmpCenter**。</span><span class="sxs-lookup"><span data-stu-id="e0584-133">In the search box, type **EmpCenter**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_search.png)

5. <span data-ttu-id="e0584-135">在結果窗格中，選取 [EmpCenter]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="e0584-135">In the results panel, select **EmpCenter**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e0584-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e0584-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e0584-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 EmpCenter 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e0584-138">In this section, you configure and test Azure AD single sign-on with EmpCenter based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e0584-139">若要讓單一登入能夠運作，Azure AD 必須知道 EmpCenter 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="e0584-139">For single sign-on to work, Azure AD needs to know what the counterpart user in EmpCenter is to a user in Azure AD.</span></span> <span data-ttu-id="e0584-140">換句話說，必須建立 Azure AD 使用者和 EmpCenter 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e0584-140">In other words, a link relationship between an Azure AD user and the related user in EmpCenter needs to be established.</span></span>

<span data-ttu-id="e0584-141">在 EmpCenter 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e0584-141">In EmpCenter, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e0584-142">若要設定及測試與 EmpCenter 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="e0584-142">To configure and test Azure AD single sign-on with EmpCenter, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e0584-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="e0584-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e0584-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e0584-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e0584-145">**[建立 EmpCenter 測試使用者](#creating-an-empcenter-test-user)** - 在 EmpCenter 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="e0584-145">**[Creating an EmpCenter test user](#creating-an-empcenter-test-user)** - to have a counterpart of Britta Simon in EmpCenter that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e0584-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e0584-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e0584-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="e0584-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e0584-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e0584-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e0584-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 EmpCenter 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="e0584-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EmpCenter application.</span></span>

<span data-ttu-id="e0584-150">**若要使用 EmpCenter 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e0584-150">**To configure Azure AD single sign-on with EmpCenter, perform the following steps:**</span></span>

1. <span data-ttu-id="e0584-151">在 Azure 入口網站的 [EmpCenter] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="e0584-151">In the Azure portal, on the **EmpCenter** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="e0584-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="e0584-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_samlbase.png)

3. <span data-ttu-id="e0584-155">在 [EmpCenter 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e0584-155">On the **EmpCenter Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_url.png)

    <span data-ttu-id="e0584-157">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰</span><span class="sxs-lookup"><span data-stu-id="e0584-157">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.EmpCenter.com/<instancename>` |
    | `https://<subdomain>.workforcehosting.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="e0584-158">這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="e0584-158">The value is not real.</span></span> <span data-ttu-id="e0584-159">請使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="e0584-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="e0584-160">請連絡 [EmpCenter 用戶端支援小組](http://www.workforcesoftware.com/services/customer-support/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="e0584-160">Contact [EmpCenter Client support team](http://www.workforcesoftware.com/services/customer-support/) to get the value.</span></span> 
 
4. <span data-ttu-id="e0584-161">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="e0584-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_certificate.png) 

5. <span data-ttu-id="e0584-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e0584-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e0584-165">若要在 **EmpCenter** 端設定單一登入，您必須將已下載的「中繼資料 XML」傳送給 [EmpCenter 支援小組](http://www.workforcesoftware.com/services/customer-support/)。</span><span class="sxs-lookup"><span data-stu-id="e0584-165">To configure single sign-on on **EmpCenter** side, you need to send the downloaded **Metadata XML** to [EmpCenter support team](http://www.workforcesoftware.com/services/customer-support/).</span></span> <span data-ttu-id="e0584-166">他們會進行此設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="e0584-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e0584-167">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="e0584-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e0584-168">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="e0584-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e0584-169">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e0584-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e0584-170">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e0584-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="e0584-171">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="e0584-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="e0584-173">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e0584-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e0584-174">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e0584-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e0584-176">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="e0584-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e0584-178">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e0584-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e0584-180">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e0584-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-EmpCenter-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e0584-182">a.</span><span class="sxs-lookup"><span data-stu-id="e0584-182">a.</span></span> <span data-ttu-id="e0584-183">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="e0584-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e0584-184">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e0584-184">b.</span></span> <span data-ttu-id="e0584-185">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="e0584-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e0584-186">c.</span><span class="sxs-lookup"><span data-stu-id="e0584-186">c.</span></span> <span data-ttu-id="e0584-187">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="e0584-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e0584-188">d.</span><span class="sxs-lookup"><span data-stu-id="e0584-188">d.</span></span> <span data-ttu-id="e0584-189">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="e0584-189">Click **Create**.</span></span>
 
### <a name="creating-an-empcenter-test-user"></a><span data-ttu-id="e0584-190">建立 EmpCenter 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e0584-190">Creating an EmpCenter test user</span></span>

<span data-ttu-id="e0584-191">若要讓 Azure AD 使用者可以登入 EmpCenter，就必須將他們佈建到 EmpCenter。</span><span class="sxs-lookup"><span data-stu-id="e0584-191">In order to enable Azure AD users to log in to EmpCenter, they must be provisioned into EmpCenter.</span></span> <span data-ttu-id="e0584-192">以 EmpCenter 而言，使用者帳戶必須由 [EmpCenter 支援小組](http://www.workforcesoftware.com/services/customer-support/)建立。</span><span class="sxs-lookup"><span data-stu-id="e0584-192">In the case of EmpCenter, the user accounts need to be created by your [EmpCenter support team](http://www.workforcesoftware.com/services/customer-support/).</span></span>

> [!NOTE]
> <span data-ttu-id="e0584-193">您可以使用任何其他的 EmpCenter 使用者帳戶建立工具或 EmpCenter 提供的 API 來佈建 Azure Active Directory 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="e0584-193">You can use any other EmpCenter user account creation tools or APIs provided by EmpCenter to provision Azure Active Directory user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e0584-194">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e0584-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e0584-195">在本節中，您會將 EmpCenter 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e0584-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EmpCenter.</span></span>

![指派使用者][200] 

<span data-ttu-id="e0584-197">**若要將 Britta Simon 指派給 EmpCenter，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e0584-197">**To assign Britta Simon to EmpCenter, perform the following steps:**</span></span>

1. <span data-ttu-id="e0584-198">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e0584-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="e0584-200">在應用程式清單中，選取 [EmpCenter]。</span><span class="sxs-lookup"><span data-stu-id="e0584-200">In the applications list, select **EmpCenter**.</span></span>

    ![設定單一登入](./media/active-directory-saas-EmpCenter-tutorial/tutorial_EmpCenter_app.png) 

3. <span data-ttu-id="e0584-202">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e0584-202">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="e0584-204">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e0584-204">Click **Add** button.</span></span> <span data-ttu-id="e0584-205">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e0584-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="e0584-207">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="e0584-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e0584-208">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e0584-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e0584-209">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e0584-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e0584-210">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="e0584-210">Testing single sign-on</span></span>


<span data-ttu-id="e0584-211">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="e0584-211">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e0584-212">當您在「存取面板」中按一下 [EmpCenter] 圖格時，應該會自動登入您的 EmpCenter 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e0584-212">When you click the EmpCenter tile in the Access Panel, you should get automatically signed-on to your EmpCenter application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e0584-213">其他資源</span><span class="sxs-lookup"><span data-stu-id="e0584-213">Additional resources</span></span>

* [<span data-ttu-id="e0584-214">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="e0584-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e0584-215">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="e0584-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-EmpCenter-tutorial/tutorial_general_203.png


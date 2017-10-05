---
title: "教學課程：Azure Active Directory 與 People 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 People 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c9b6202-11dd-4bb6-a679-8fb0a7a0ef4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: caa287a2ed8774965ef722685e4e950336e5e0ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-people"></a><span data-ttu-id="7aed2-103">教學課程：Azure Active Directory 與 People 整合</span><span class="sxs-lookup"><span data-stu-id="7aed2-103">Tutorial: Azure Active Directory integration with People</span></span>

<span data-ttu-id="7aed2-104">在本教學課程中，您將了解如何整合 People 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="7aed2-104">In this tutorial, you learn how to integrate People with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7aed2-105">People 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="7aed2-105">Integrating People with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7aed2-106">您可以在 Azure AD 中控制可存取 People 的人員</span><span class="sxs-lookup"><span data-stu-id="7aed2-106">You can control in Azure AD who has access to People</span></span>
- <span data-ttu-id="7aed2-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 People (單一登入)</span><span class="sxs-lookup"><span data-stu-id="7aed2-107">You can enable your users to automatically get signed-on to People (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7aed2-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="7aed2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7aed2-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="7aed2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7aed2-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="7aed2-110">Prerequisites</span></span>

<span data-ttu-id="7aed2-111">若要設定 Azure AD 與 People 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="7aed2-111">To configure Azure AD integration with People, you need the following items:</span></span>

- <span data-ttu-id="7aed2-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7aed2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7aed2-113">已啟用 People 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7aed2-113">A People single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7aed2-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7aed2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7aed2-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="7aed2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7aed2-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7aed2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7aed2-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="7aed2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7aed2-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="7aed2-118">Scenario description</span></span>
<span data-ttu-id="7aed2-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7aed2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7aed2-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="7aed2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7aed2-121">從資源庫新增 People</span><span class="sxs-lookup"><span data-stu-id="7aed2-121">Adding People from the gallery</span></span>
2. <span data-ttu-id="7aed2-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7aed2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-people-from-the-gallery"></a><span data-ttu-id="7aed2-123">從資源庫新增 People</span><span class="sxs-lookup"><span data-stu-id="7aed2-123">Adding People from the gallery</span></span>
<span data-ttu-id="7aed2-124">若要設定將 People 整合到 Azure AD 中，您需要從資源庫將 People 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="7aed2-124">To configure the integration of People into Azure AD, you need to add People from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7aed2-125">**若要從資源庫新增 People，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7aed2-125">**To add People from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7aed2-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7aed2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7aed2-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7aed2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7aed2-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7aed2-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="7aed2-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7aed2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="7aed2-133">在搜尋方塊中，輸入 **People**。</span><span class="sxs-lookup"><span data-stu-id="7aed2-133">In the search box, type **People**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-people-tutorial/tutorial_people_search.png)

5. <span data-ttu-id="7aed2-135">在結果窗格中，選取 [People]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="7aed2-135">In the results panel, select **People**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-people-tutorial/tutorial_people_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7aed2-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7aed2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7aed2-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 People 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7aed2-138">In this section, you configure and test Azure AD single sign-on with People based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7aed2-139">若要讓單一登入運作，Azure AD 必須知道 People 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="7aed2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in People is to a user in Azure AD.</span></span> <span data-ttu-id="7aed2-140">換句話說，必須建立 Azure AD 使用者和 People 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7aed2-140">In other words, a link relationship between an Azure AD user and the related user in People needs to be established.</span></span>

<span data-ttu-id="7aed2-141">在 People 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7aed2-141">In People, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7aed2-142">若要設定及測試與 People 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="7aed2-142">To configure and test Azure AD single sign-on with People, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7aed2-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="7aed2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7aed2-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7aed2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7aed2-145">**[建立 People 測試使用者](#creating-a-people-test-user)** - 使 People 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="7aed2-145">**[Creating a People test user](#creating-a-people-test-user)** - to have a counterpart of Britta Simon in People that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7aed2-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7aed2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7aed2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="7aed2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7aed2-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7aed2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7aed2-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 People 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="7aed2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your People application.</span></span>

<span data-ttu-id="7aed2-150">**若要設定與 People 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7aed2-150">**To configure Azure AD single sign-on with People, perform the following steps:**</span></span>

1. <span data-ttu-id="7aed2-151">在 Azure 入口網站的 [People] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="7aed2-151">In the Azure portal, on the **People** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="7aed2-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="7aed2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-people-tutorial/tutorial_people_samlbase.png)

3. <span data-ttu-id="7aed2-155">在 [People 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7aed2-155">On the **People Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-people-tutorial/tutorial_people_url.png)

    <span data-ttu-id="7aed2-157">a.</span><span class="sxs-lookup"><span data-stu-id="7aed2-157">a.</span></span> <span data-ttu-id="7aed2-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<company name>.peoplehr.com/`</span><span class="sxs-lookup"><span data-stu-id="7aed2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.peoplehr.com/`</span></span>

    <span data-ttu-id="7aed2-159">b.</span><span class="sxs-lookup"><span data-stu-id="7aed2-159">b.</span></span> <span data-ttu-id="7aed2-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://www.peoplehr.com`</span><span class="sxs-lookup"><span data-stu-id="7aed2-160">In the **Identifier** textbox, type a URL using the following pattern: `https://www.peoplehr.com`</span></span>

    <span data-ttu-id="7aed2-161">c.</span><span class="sxs-lookup"><span data-stu-id="7aed2-161">c.</span></span> <span data-ttu-id="7aed2-162">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span><span class="sxs-lookup"><span data-stu-id="7aed2-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7aed2-163">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="7aed2-163">These values are not real.</span></span> <span data-ttu-id="7aed2-164">使用實際的識別碼、回覆 URL 和登入 URL 來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="7aed2-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="7aed2-165">請連絡 [People 用戶端支援小組](mailto:customerservices@peoplehr.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="7aed2-165">Contact [People Client support team](mailto:customerservices@peoplehr.com) to get these values.</span></span>

5. <span data-ttu-id="7aed2-166">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="7aed2-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-people-tutorial/tutorial_people_certificate.png) 

6. <span data-ttu-id="7aed2-168">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="7aed2-168">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-people-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="7aed2-170">若要取得為應用程式設定的 SSO，您必須以系統管理員身分登入 People 租用戶。</span><span class="sxs-lookup"><span data-stu-id="7aed2-170">To get SSO configured for your application, you need to sign-on to your People tenant as an administrator.</span></span>
   
8. <span data-ttu-id="7aed2-171">在左側功能表中，按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="7aed2-171">In the menu on the left side, click **Settings**.</span></span>

    ![設定單一登入](./media/active-directory-saas-people-tutorial/tutorial_people_001.png)

9. <span data-ttu-id="7aed2-173">按一下 [公司] 。</span><span class="sxs-lookup"><span data-stu-id="7aed2-173">Click **Company**.</span></span>

    ![設定單一登入](./media/active-directory-saas-people-tutorial/tutorial_people_002.png)

10. <span data-ttu-id="7aed2-175">在 [上傳單衣登入 SAML 中繼資料檔案] 上，按一下 [瀏覽] 上傳下載的中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="7aed2-175">On the **Upload 'Single Sign On' SAML meta-data file**, click **Browse** to upload the downloaded metadata file.</span></span>

    ![設定單一登入](./media/active-directory-saas-people-tutorial/tutorial_people_003.png)

> [!TIP]
> <span data-ttu-id="7aed2-177">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="7aed2-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7aed2-178">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="7aed2-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7aed2-179">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7aed2-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7aed2-180">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7aed2-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="7aed2-181">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="7aed2-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="7aed2-183">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7aed2-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7aed2-184">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7aed2-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-people-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7aed2-186">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="7aed2-186">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-people-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7aed2-188">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="7aed2-188">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-people-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7aed2-190">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7aed2-190">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-people-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7aed2-192">a.</span><span class="sxs-lookup"><span data-stu-id="7aed2-192">a.</span></span> <span data-ttu-id="7aed2-193">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="7aed2-193">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7aed2-194">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7aed2-194">b.</span></span> <span data-ttu-id="7aed2-195">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="7aed2-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7aed2-196">c.</span><span class="sxs-lookup"><span data-stu-id="7aed2-196">c.</span></span> <span data-ttu-id="7aed2-197">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="7aed2-197">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7aed2-198">d.</span><span class="sxs-lookup"><span data-stu-id="7aed2-198">d.</span></span> <span data-ttu-id="7aed2-199">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7aed2-199">Click **Create**.</span></span>
 
### <a name="creating-a-people-test-user"></a><span data-ttu-id="7aed2-200">建立 People 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7aed2-200">Creating a People test user</span></span>

<span data-ttu-id="7aed2-201">在本節中，您要在 People 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="7aed2-201">In this section, you create a user called Britta Simon in People.</span></span> <span data-ttu-id="7aed2-202">請與 [People 客戶支援小組](mailto:customerservices@peoplehr.com)合作，在 People 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="7aed2-202">Work with [People Client support team](mailto:customerservices@peoplehr.com) to add the users in the People platform.</span></span> <span data-ttu-id="7aed2-203">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="7aed2-203">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7aed2-204">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7aed2-204">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7aed2-205">在本節中，您會將 People 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7aed2-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to People.</span></span>

![指派使用者][200] 

<span data-ttu-id="7aed2-207">**若要將 Britta Simon 指派給 People，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7aed2-207">**To assign Britta Simon to People, perform the following steps:**</span></span>

1. <span data-ttu-id="7aed2-208">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7aed2-208">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="7aed2-210">在應用程式清單中，選取[People] 。</span><span class="sxs-lookup"><span data-stu-id="7aed2-210">In the applications list, select **People**.</span></span>

    ![設定單一登入](./media/active-directory-saas-people-tutorial/tutorial_people_app.png) 

3. <span data-ttu-id="7aed2-212">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7aed2-212">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="7aed2-214">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7aed2-214">Click **Add** button.</span></span> <span data-ttu-id="7aed2-215">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7aed2-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="7aed2-217">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="7aed2-217">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7aed2-218">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7aed2-218">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7aed2-219">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7aed2-219">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7aed2-220">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="7aed2-220">Testing single sign-on</span></span>

<span data-ttu-id="7aed2-221">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="7aed2-221">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="7aed2-222">當您在「存取面板」中按一下 [People] 圖格時，應該會自動登入您的 People 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7aed2-222">When you click the People tile in the Access Panel, you should get automatically signed-on to your People application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7aed2-223">其他資源</span><span class="sxs-lookup"><span data-stu-id="7aed2-223">Additional resources</span></span>

* [<span data-ttu-id="7aed2-224">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="7aed2-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7aed2-225">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7aed2-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-people-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-people-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-people-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-people-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-people-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-people-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-people-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-people-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-people-tutorial/tutorial_general_203.png


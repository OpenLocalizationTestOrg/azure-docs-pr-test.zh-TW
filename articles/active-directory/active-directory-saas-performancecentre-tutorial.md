---
title: "教學課程：Azure Active Directory 與 PerformanceCentre 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 PerformanceCentre 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65288c32-f7e6-4eb3-a6dc-523c3d748d1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: e86adaf4bd9b4752f2aece8207a8a423ec5590a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-performancecentre"></a><span data-ttu-id="8396a-103">教學課程：Azure Active Directory 與 PerformanceCentre 整合</span><span class="sxs-lookup"><span data-stu-id="8396a-103">Tutorial: Azure Active Directory integration with PerformanceCentre</span></span>

<span data-ttu-id="8396a-104">在本教學課程中，您將了解如何整合 PerformanceCentre 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="8396a-104">In this tutorial, you learn how to integrate PerformanceCentre with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8396a-105">PerformanceCentre 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="8396a-105">Integrating PerformanceCentre with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8396a-106">您可以在 Azure AD 中控制可存取 PerformanceCentre 的人員</span><span class="sxs-lookup"><span data-stu-id="8396a-106">You can control in Azure AD who has access to PerformanceCentre</span></span>
- <span data-ttu-id="8396a-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 PerformanceCentre (單一登入)</span><span class="sxs-lookup"><span data-stu-id="8396a-107">You can enable your users to automatically get signed-on to PerformanceCentre (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8396a-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="8396a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8396a-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="8396a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8396a-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="8396a-110">Prerequisites</span></span>

<span data-ttu-id="8396a-111">若要設定 Azure AD 與 PerformanceCentre 整合，您需要以下項目：</span><span class="sxs-lookup"><span data-stu-id="8396a-111">To configure Azure AD integration with PerformanceCentre, you need the following items:</span></span>

- <span data-ttu-id="8396a-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8396a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8396a-113">已啟用 PerformanceCentre 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8396a-113">A PerformanceCentre single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8396a-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="8396a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8396a-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="8396a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8396a-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="8396a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8396a-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="8396a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8396a-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="8396a-118">Scenario description</span></span>
<span data-ttu-id="8396a-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8396a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8396a-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="8396a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8396a-121">從資源庫加入 PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="8396a-121">Adding PerformanceCentre from the gallery</span></span>
2. <span data-ttu-id="8396a-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8396a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-performancecentre-from-the-gallery"></a><span data-ttu-id="8396a-123">從資源庫加入 PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="8396a-123">Adding PerformanceCentre from the gallery</span></span>
<span data-ttu-id="8396a-124">若要設定 PerformanceCentre 與 Azure AD 整合，您需要從資源庫將 PerformanceCentre 加入受管理 SaaS 應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="8396a-124">To configure the integration of PerformanceCentre into Azure AD, you need to add PerformanceCentre from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8396a-125">**若要從資源庫加入 PerformanceCentre，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8396a-125">**To add PerformanceCentre from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8396a-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="8396a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8396a-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8396a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8396a-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8396a-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="8396a-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8396a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="8396a-133">在搜尋方塊中，輸入 **PerformanceCentre**。</span><span class="sxs-lookup"><span data-stu-id="8396a-133">In the search box, type **PerformanceCentre**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_search.png)

5. <span data-ttu-id="8396a-135">在結果窗格中，選取 [PerformanceCentre]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="8396a-135">In the results panel, select **PerformanceCentre**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8396a-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8396a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8396a-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 PerformanceCentre 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8396a-138">In this section, you configure and test Azure AD single sign-on with PerformanceCentre based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8396a-139">單一登入若要運作，Azure AD 必須知道 PerformanceCentre 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="8396a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PerformanceCentre is to a user in Azure AD.</span></span> <span data-ttu-id="8396a-140">換句話說，必須在 Azure AD 使用者與 PerformanceCentre 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="8396a-140">In other words, a link relationship between an Azure AD user and the related user in PerformanceCentre needs to be established.</span></span>

<span data-ttu-id="8396a-141">在 PerformanceCentre 中，將**使用者名稱**的值指派為 Azure AD 中**使用者名稱**的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="8396a-141">In PerformanceCentre, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8396a-142">若要使用 PerformanceCentre 設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="8396a-142">To configure and test Azure AD single sign-on with PerformanceCentre, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8396a-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="8396a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8396a-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8396a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8396a-145">**[建立 PerformanceCentre 測試使用者](#creating-a-performancecentre-test-user)** - 使 PerformanceCentre 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="8396a-145">**[Creating a PerformanceCentre test user](#creating-a-performancecentre-test-user)** - to have a counterpart of Britta Simon in PerformanceCentre that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8396a-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8396a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8396a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="8396a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8396a-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8396a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8396a-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 PerformanceCentre 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="8396a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PerformanceCentre application.</span></span>

<span data-ttu-id="8396a-150">**若要使用 PerformanceCentre 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8396a-150">**To configure Azure AD single sign-on with PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="8396a-151">在 Azure 入口網站的 [PerformanceCentre] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="8396a-151">In the Azure portal, on the **PerformanceCentre** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="8396a-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="8396a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_samlbase.png)

3. <span data-ttu-id="8396a-155">在 [PerformanceCentre 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8396a-155">On the **PerformanceCentre Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_url.png)

    <span data-ttu-id="8396a-157">a.</span><span class="sxs-lookup"><span data-stu-id="8396a-157">a.</span></span> <span data-ttu-id="8396a-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`http://companyname.performancecentre.com/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="8396a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://companyname.performancecentre.com/saml/SSO`</span></span>

    <span data-ttu-id="8396a-159">b.</span><span class="sxs-lookup"><span data-stu-id="8396a-159">b.</span></span> <span data-ttu-id="8396a-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`http://companyname.performancecentre.com`</span><span class="sxs-lookup"><span data-stu-id="8396a-160">In the **Identifier** textbox, type a URL using the following pattern: `http://companyname.performancecentre.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8396a-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="8396a-161">These values are not real.</span></span> <span data-ttu-id="8396a-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="8396a-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8396a-163">請連絡 [客戶支援小組](https://www.performancecentre.com/contact-us/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="8396a-163">Contact [PerformanceCentre Client support team](https://www.performancecentre.com/contact-us/) to get these values.</span></span> 

4. <span data-ttu-id="8396a-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="8396a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_certificate.png) 

5. <span data-ttu-id="8396a-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8396a-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-performancecentre-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8396a-168">在 [PerformanceCentre 組態] 區段上，按一下 [設定 PerformanceCentre] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="8396a-168">On the **PerformanceCentre Configuration** section, click **Configure PerformanceCentre** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8396a-169">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="8396a-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_configure.png) 

7. <span data-ttu-id="8396a-171">以系統管理員身分登入您的 **PerformanceCentre** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="8396a-171">Sign-on to your **PerformanceCentre** company site as administrator.</span></span>

8. <span data-ttu-id="8396a-172">在左側索引標籤中，按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="8396a-172">In the tab on the left side, click **Configure**.</span></span>
   
    ![Azure AD 單一登入][10]

9. <span data-ttu-id="8396a-174">在左側索引標籤中，按一下 [其他]，然後按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="8396a-174">In the tab on the left side, click **Miscellaneous**, and then click **Single Sign On**.</span></span>
   
    ![Azure AD 單一登入][11]

10. <span data-ttu-id="8396a-176">針對 [通訊協定]，選取 [SAML]。</span><span class="sxs-lookup"><span data-stu-id="8396a-176">As **Protocol**, select **SAML**.</span></span>
   
    ![Azure AD 單一登入][12]

11. <span data-ttu-id="8396a-178">在記事本中開啟下載的中繼資料檔案，複製其內容，然後貼到 [身分識別提供者中繼資料] 文字方塊，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="8396a-178">Open your downloaded metadata file in notepad, copy the content, paste it into the **Identity Provider Metadata** textbox, and then click **Save**.</span></span>
   
    ![Azure AD 單一登入][13]

12. <span data-ttu-id="8396a-180">確認 [實體基礎 URL]和 [實體識別碼] 的值正確無誤。</span><span class="sxs-lookup"><span data-stu-id="8396a-180">Verify that the values for the **Entity Base URL** and **Entity ID URL** are correct.</span></span>
    
     ![Azure AD 單一登入][14]

> [!TIP]
> <span data-ttu-id="8396a-182">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="8396a-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8396a-183">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="8396a-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8396a-184">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8396a-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8396a-185">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8396a-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="8396a-186">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="8396a-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="8396a-188">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8396a-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8396a-189">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="8396a-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8396a-191">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="8396a-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8396a-193">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="8396a-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8396a-195">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8396a-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8396a-197">a.</span><span class="sxs-lookup"><span data-stu-id="8396a-197">a.</span></span> <span data-ttu-id="8396a-198">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="8396a-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8396a-199">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="8396a-199">b.</span></span> <span data-ttu-id="8396a-200">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="8396a-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8396a-201">c.</span><span class="sxs-lookup"><span data-stu-id="8396a-201">c.</span></span> <span data-ttu-id="8396a-202">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="8396a-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8396a-203">d.</span><span class="sxs-lookup"><span data-stu-id="8396a-203">d.</span></span> <span data-ttu-id="8396a-204">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="8396a-204">Click **Create**.</span></span>
 
### <a name="creating-a-performancecentre-test-user"></a><span data-ttu-id="8396a-205">建立 PerformanceCentre 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8396a-205">Creating a PerformanceCentre test user</span></span>

<span data-ttu-id="8396a-206">本節的目標是在 PerformanceCentre 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="8396a-206">The objective of this section is to create a user called Britta Simon in PerformanceCentre.</span></span>

<span data-ttu-id="8396a-207">**若要在 PerformanceCentre 中建立名為 Britta Simon 的使用者，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="8396a-207">**To create a user called Britta Simon in PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="8396a-208">以系統管理員身分登入您的 PerformanceCentre 公司網站。</span><span class="sxs-lookup"><span data-stu-id="8396a-208">Sign on to your PerformanceCentre company site as administrator.</span></span>

2. <span data-ttu-id="8396a-209">在左側功能表中，按一下 [內部關聯]，然後按一下 [建立參與者]。</span><span class="sxs-lookup"><span data-stu-id="8396a-209">In the menu on the left, click **Interrelate**, and then click **Create Participant**.</span></span>
   
    ![建立使用者][400]

3. <span data-ttu-id="8396a-211">在 [內部關聯 - 建立參與者]  對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8396a-211">On the **Interrelate - Create Participant** dialog, perform the following steps:</span></span>
   
    ![建立使用者][401]
    
    <span data-ttu-id="8396a-213">a.</span><span class="sxs-lookup"><span data-stu-id="8396a-213">a.</span></span> <span data-ttu-id="8396a-214">在相關的文字方塊中為 Britta Simon 輸入必要的屬性。</span><span class="sxs-lookup"><span data-stu-id="8396a-214">Type the required attributes for Britta Simon into related textboxes.</span></span>
    
    >[!IMPORTANT]
    ><span data-ttu-id="8396a-215">在 PerformanceCentre 中，Britta 的使用者名稱屬性必須與 Azure AD 中的使用者名稱相同。</span><span class="sxs-lookup"><span data-stu-id="8396a-215">Britta's User Name attribute in PerformanceCentre must be the same as the User Name in Azure AD.</span></span>
    
    <span data-ttu-id="8396a-216">b.</span><span class="sxs-lookup"><span data-stu-id="8396a-216">b.</span></span> <span data-ttu-id="8396a-217">對 [選擇角色] 選取 [用戶端系統管理員]。</span><span class="sxs-lookup"><span data-stu-id="8396a-217">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="8396a-218">c.</span><span class="sxs-lookup"><span data-stu-id="8396a-218">c.</span></span> <span data-ttu-id="8396a-219">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="8396a-219">Click **Save**.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8396a-220">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8396a-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8396a-221">在本節中，您會將 PerformanceCentre 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8396a-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PerformanceCentre.</span></span>

![指派使用者][200] 

<span data-ttu-id="8396a-223">**若要指派 Britta Simon 到 PerformanceCentre，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="8396a-223">**To assign Britta Simon to PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="8396a-224">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8396a-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="8396a-226">在應用程式清單中，選取 **PerformanceCentre**。</span><span class="sxs-lookup"><span data-stu-id="8396a-226">In the applications list, select **PerformanceCentre**.</span></span>

    ![設定單一登入](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_app.png) 

3. <span data-ttu-id="8396a-228">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="8396a-228">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="8396a-230">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8396a-230">Click **Add** button.</span></span> <span data-ttu-id="8396a-231">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="8396a-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="8396a-233">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="8396a-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8396a-234">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8396a-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8396a-235">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8396a-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8396a-236">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="8396a-236">Testing single sign-on</span></span>

<span data-ttu-id="8396a-237">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="8396a-237">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="8396a-238">當您在存取面板中按一下 PerformanceCentre 磚時，應該會自動登入您的 PerformanceCentre 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8396a-238">When you click the PerformanceCentre tile in the Access Panel, you should get automatically signed-on to your PerformanceCentre application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8396a-239">其他資源</span><span class="sxs-lookup"><span data-stu-id="8396a-239">Additional resources</span></span>

* [<span data-ttu-id="8396a-240">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="8396a-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8396a-241">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="8396a-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_06.png
[11]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_07.png
[12]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_08.png
[13]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_09.png
[14]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_10.png

[100]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_11.png
[401]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_12.png

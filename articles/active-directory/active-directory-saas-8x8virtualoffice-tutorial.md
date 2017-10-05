---
title: "教學課程：Azure Active Directory 與 8x8 Virtual Office 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 8x8 Virtual Office 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d8dcf0171b93fec15347e810a1b525bd815dbf04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a><span data-ttu-id="ed025-103">教學課程：Azure Active Directory 與 8x8 Virtual Office 整合</span><span class="sxs-lookup"><span data-stu-id="ed025-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span></span>

<span data-ttu-id="ed025-104">在本教學課程中，您會了解如何將 8x8 Virtual Office 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="ed025-104">In this tutorial, you learn how to integrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ed025-105">將 8x8 Virtual Office 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="ed025-105">Integrating 8x8 Virtual Office with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ed025-106">您可以在 Azure AD 中管控可存取 8x8 Virtual Office 的人員</span><span class="sxs-lookup"><span data-stu-id="ed025-106">You can control in Azure AD who has access to 8x8 Virtual Office</span></span>
- <span data-ttu-id="ed025-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 8x8 Virtual Office (單一登入)</span><span class="sxs-lookup"><span data-stu-id="ed025-107">You can enable your users to automatically get signed-on to 8x8 Virtual Office (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ed025-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="ed025-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ed025-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ed025-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed025-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ed025-110">Prerequisites</span></span>

<span data-ttu-id="ed025-111">若要設定 Azure AD 與 8x8 Virtual Office 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="ed025-111">To configure Azure AD integration with 8x8 Virtual Office, you need the following items:</span></span>

- <span data-ttu-id="ed025-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ed025-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ed025-113">已啟用 8x8 Virtual Office 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ed025-113">A 8x8 Virtual Office single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ed025-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ed025-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ed025-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="ed025-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ed025-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ed025-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ed025-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="ed025-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ed025-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="ed025-118">Scenario description</span></span>
<span data-ttu-id="ed025-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ed025-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ed025-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="ed025-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ed025-121">從資源庫新增 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="ed025-121">Adding 8x8 Virtual Office from the gallery</span></span>
2. <span data-ttu-id="ed025-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ed025-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-8x8-virtual-office-from-the-gallery"></a><span data-ttu-id="ed025-123">從資源庫新增 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="ed025-123">Adding 8x8 Virtual Office from the gallery</span></span>
<span data-ttu-id="ed025-124">若要設定將 8x8 Virtual Office 整合到 Azure AD 中，您需要從資源庫將 8x8 Virtual Office 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="ed025-124">To configure the integration of 8x8 Virtual Office into Azure AD, you need to add 8x8 Virtual Office from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ed025-125">**若要從資源庫新增 8x8 Virtual Office，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ed025-125">**To add 8x8 Virtual Office from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ed025-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ed025-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ed025-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ed025-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ed025-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ed025-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="ed025-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ed025-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="ed025-133">在搜尋方塊中，輸入 **8x8 Virtual Office**。</span><span class="sxs-lookup"><span data-stu-id="ed025-133">In the search box, type **8x8 Virtual Office**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_search.png)

5. <span data-ttu-id="ed025-135">在結果面板中，選取 [8x8 Virtual Office]，然後按一下 [新增] 按鈕以新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed025-135">In the results panel, select **8x8 Virtual Office**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ed025-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ed025-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ed025-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 8x8 Virtual Office 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ed025-138">In this section, you configure and test Azure AD single sign-on with 8x8 Virtual Office based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ed025-139">若要讓單一登入能夠運作，Azure AD 必須知道 8x8 Virtual Office 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="ed025-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 8x8 Virtual Office is to a user in Azure AD.</span></span> <span data-ttu-id="ed025-140">換句話說，必須在 Azure AD 使用者與 8x8 Virtual Office 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ed025-140">In other words, a link relationship between an Azure AD user and the related user in 8x8 Virtual Office needs to be established.</span></span>

<span data-ttu-id="ed025-141">在 8x8 Virtual Office 中，將 [Username] 的值指派為 Azure AD 中 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ed025-141">In 8x8 Virtual Office, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ed025-142">若要設定及測試與 8x8 Virtual Office 搭配運作的 Microsoft Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="ed025-142">To configure and test Azure AD single sign-on with 8x8 Virtual Office, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ed025-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="ed025-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ed025-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ed025-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ed025-145">**[建立 8x8 Virtual Office 測試使用者](#creating-a-8x8-virtual-office-test-user)** - 在 8x8 Virtual Office 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="ed025-145">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - to have a counterpart of Britta Simon in 8x8 Virtual Office that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ed025-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ed025-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ed025-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="ed025-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ed025-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ed025-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ed025-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 8x8 Virtual Office 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="ed025-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 8x8 Virtual Office application.</span></span>

<span data-ttu-id="ed025-150">**若要設定與 8x8 Virtual Office 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ed025-150">**To configure Azure AD single sign-on with 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="ed025-151">在 Azure 入口網站的 [8x8 Virtual Office] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="ed025-151">In the Azure portal, on the **8x8 Virtual Office** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="ed025-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="ed025-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_samlbase.png)

3. <span data-ttu-id="ed025-155">在 [8x8 Virtual Office 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ed025-155">On the **8x8 Virtual Office Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_url.png)

    <span data-ttu-id="ed025-157">a.</span><span class="sxs-lookup"><span data-stu-id="ed025-157">a.</span></span> <span data-ttu-id="ed025-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="ed025-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="ed025-159">| `https://sso.8x8.com/<companyname>` |
    | `https://www.8x8.com/<companyname>` |
    | `https://sso.8x8pilot.com/<companyname>` |</span><span class="sxs-lookup"><span data-stu-id="ed025-159">| `https://sso.8x8.com/<companyname>` |
 | `https://www.8x8.com/<companyname>` |
 | `https://sso.8x8pilot.com/<companyname>` |</span></span>

    <span data-ttu-id="ed025-160">b.</span><span class="sxs-lookup"><span data-stu-id="ed025-160">b.</span></span> <span data-ttu-id="ed025-161">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="ed025-161">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="ed025-162">| `https://<subdomain>.8x8.com/saml2` |
    | `https://<subdomain>.8x8pilot.com/saml2`|</span><span class="sxs-lookup"><span data-stu-id="ed025-162">| `https://<subdomain>.8x8.com/saml2` |
 | `https://<subdomain>.8x8pilot.com/saml2`|</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ed025-163">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="ed025-163">These values are not real.</span></span> <span data-ttu-id="ed025-164">請使用實際的識別碼和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="ed025-164">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="ed025-165">請連絡 [8x8 Virtual Office 支援小組](https://www.8x8.com/about-us/contact-us)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="ed025-165">Contact [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us) to get these values.</span></span>
 


4. <span data-ttu-id="ed025-166">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (原始)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="ed025-166">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_certificate.png) 

5. <span data-ttu-id="ed025-168">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ed025-168">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ed025-170">在 [8x8 Virtual Office 組態] 區段上，按一下 [設定 8x8 Virtual Office] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="ed025-170">On the **8x8 Virtual Office Configuration** section, click **Configure 8x8 Virtual Office** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ed025-171">從 [快速參考] 區段中複製「登出 URL」、「SAML 實體識別碼」及「SAML 單一登入服務 URL」。</span><span class="sxs-lookup"><span data-stu-id="ed025-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_configure.png) 

7. <span data-ttu-id="ed025-173">以系統管理員身分登入 8x8 Virtual Office 租用戶。</span><span class="sxs-lookup"><span data-stu-id="ed025-173">Sign-on to your 8x8 Virtual Office tenant as an administrator.</span></span>

8. <span data-ttu-id="ed025-174">在 [應用程式面板] 上選取 [Virtual Office 帳戶管理員]  。</span><span class="sxs-lookup"><span data-stu-id="ed025-174">Select **Virtual Office Account Mgr** on Application Panel.</span></span>
   
    ![在應用程式端設定](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)

9. <span data-ttu-id="ed025-176">選取 [商務] 帳戶以進行管理，並按一下 [登入] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ed025-176">Select **Business** account to manage and click **Sign In** button.</span></span>
   
    ![在應用程式端設定](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)

10. <span data-ttu-id="ed025-178">按一下功能表清單中的 [帳戶]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ed025-178">Click **Accounts** tab in the menu list.</span></span>
   
    ![在應用程式端設定](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)

11. <span data-ttu-id="ed025-180">按一下 [帳戶] 清單中的 [單一登入]  。</span><span class="sxs-lookup"><span data-stu-id="ed025-180">Click **Single Sign On** in the list of Accounts.</span></span>
   
    ![在應用程式端設定](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)

12. <span data-ttu-id="ed025-182">選取 [驗證方法] 底下的 [單一登入]，然後按一下 [SAML]。</span><span class="sxs-lookup"><span data-stu-id="ed025-182">Select **Single Sign On** under Authentication method and click **SAML**.</span></span>
    
    ![在應用程式端設定](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)

13. <span data-ttu-id="ed025-184">將 Azure AD 的 [SAML SSO URL]、[單一登出服務 URL] 和 [簽發者 URL] 複製到 8x8 Virtual Office 的 [登入 URL]、[登出 URL] 和 [簽發者 URL]。</span><span class="sxs-lookup"><span data-stu-id="ed025-184">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD to **Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span></span> 
    
    ![在應用程式端設定](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
14. <span data-ttu-id="ed025-186">按一下 [瀏覽器] 按鈕來上傳您從 Azure AD 下載的憑證，然後按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ed025-186">Click **Browser** button to upload the certificate which you downloaded from Azure AD, and click the **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="ed025-187">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="ed025-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ed025-188">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="ed025-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ed025-189">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ed025-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ed025-190">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ed025-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="ed025-191">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ed025-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="ed025-193">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ed025-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ed025-194">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ed025-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ed025-196">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="ed025-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ed025-198">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ed025-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ed025-200">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ed025-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ed025-202">a.</span><span class="sxs-lookup"><span data-stu-id="ed025-202">a.</span></span> <span data-ttu-id="ed025-203">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="ed025-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ed025-204">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed025-204">b.</span></span> <span data-ttu-id="ed025-205">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="ed025-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ed025-206">c.</span><span class="sxs-lookup"><span data-stu-id="ed025-206">c.</span></span> <span data-ttu-id="ed025-207">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="ed025-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ed025-208">d.</span><span class="sxs-lookup"><span data-stu-id="ed025-208">d.</span></span> <span data-ttu-id="ed025-209">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ed025-209">Click **Create**.</span></span>
 
### <a name="creating-a-8x8-virtual-office-test-user"></a><span data-ttu-id="ed025-210">建立 8x8 Virtual Office 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ed025-210">Creating a 8x8 Virtual Office test user</span></span>

<span data-ttu-id="ed025-211">本節的目標是要在 8x8 Virtual Office 中建立一個名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="ed025-211">The objective of this section is to create a user called Britta Simon in 8x8 Virtual Office.</span></span> <span data-ttu-id="ed025-212">8x8 Virtual Office 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="ed025-212">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="ed025-213">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="ed025-213">There is no action item for you in this section.</span></span> <span data-ttu-id="ed025-214">嘗試存取 8x8 Virtual Office 時，如果使用者還不存在，就會建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="ed025-214">A new user is created during an attempt to access 8x8 Virtual Office if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="ed025-215">如果您需要手動建立使用者，則必須連絡 [8x8 Virtual Office 支援小組](https://www.8x8.com/about-us/contact-us)。</span><span class="sxs-lookup"><span data-stu-id="ed025-215">If you need to create a user manually, you need to contact the [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ed025-216">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ed025-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ed025-217">在本節中，您會將 8x8 Virtual Office 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ed025-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 8x8 Virtual Office.</span></span>

![指派使用者][200] 

<span data-ttu-id="ed025-219">**若要將 Britta Simon 指派給 8x8 Virtual Office，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ed025-219">**To assign Britta Simon to 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="ed025-220">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ed025-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="ed025-222">在應用程式清單中，選取 [8x8 Virtual Office ]。</span><span class="sxs-lookup"><span data-stu-id="ed025-222">In the applications list, select **8x8 Virtual Office**.</span></span>

    ![設定單一登入](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_app.png) 

3. <span data-ttu-id="ed025-224">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ed025-224">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="ed025-226">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ed025-226">Click **Add** button.</span></span> <span data-ttu-id="ed025-227">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ed025-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="ed025-229">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="ed025-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ed025-230">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ed025-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ed025-231">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ed025-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ed025-232">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="ed025-232">Testing single sign-on</span></span>

<span data-ttu-id="ed025-233">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="ed025-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ed025-234">當您在「存取面板」中按一下 [8x8 Virtual Office ] 圖格時，應該會自動登入您的 8x8 Virtual Office 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ed025-234">When you click the 8x8 Virtual Office tile in the Access Panel, you should get automatically signed-on to your 8x8 Virtual Office application.</span></span>
<span data-ttu-id="ed025-235">如需有關「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="ed025-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ed025-236">其他資源</span><span class="sxs-lookup"><span data-stu-id="ed025-236">Additional resources</span></span>

* [<span data-ttu-id="ed025-237">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="ed025-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ed025-238">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ed025-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_203.png


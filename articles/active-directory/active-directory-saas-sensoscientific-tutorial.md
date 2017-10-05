---
title: "教學課程︰Azure Active Directory 與 SensoScientific Wireless Temperature Monitoring System 整合 | Microsoft Docs"
description: "了解如何在 Azure Active Directory 與 SensoScientific Wireless Temperature Monitoring System 之間設定單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: fa6242cf7f9559ca394ffde2e5e734cb935b03dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a><span data-ttu-id="0a4ce-103">教學課程︰Azure Active Directory 與 SensoScientific Wireless Temperature Monitoring System 整合</span><span class="sxs-lookup"><span data-stu-id="0a4ce-103">Tutorial: Azure Active Directory integration with SensoScientific Wireless Temperature Monitoring System</span></span>

<span data-ttu-id="0a4ce-104">在本教學課程中，您會了解如何將 SensoScientific Wireless Temperature Monitoring System 與 Azure Active Directory (Azure AD) 進行整合。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-104">In this tutorial, you learn how to integrate SensoScientific Wireless Temperature Monitoring System with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a4ce-105">將 SensoScientific Wireless Temperature Monitoring System 與 Azure AD 整合可以提供下列優點︰</span><span class="sxs-lookup"><span data-stu-id="0a4ce-105">Integrating SensoScientific Wireless Temperature Monitoring System with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0a4ce-106">您可以在 Azure AD 中控制誰能夠存取 SensoScientific Wireless Temperature Monitoring System</span><span class="sxs-lookup"><span data-stu-id="0a4ce-106">You can control in Azure AD who has access to SensoScientific Wireless Temperature Monitoring System</span></span>
- <span data-ttu-id="0a4ce-107">您可以讓使用者使用其 Azure AD 帳戶自動登入 SensoScientific Wireless Temperature Monitoring System (單一登入)</span><span class="sxs-lookup"><span data-stu-id="0a4ce-107">You can enable your users to automatically get signed-on to SensoScientific Wireless Temperature Monitoring System (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0a4ce-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="0a4ce-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0a4ce-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a4ce-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="0a4ce-110">Prerequisites</span></span>

<span data-ttu-id="0a4ce-111">若要設定 Azure AD 與 SensoScientific Wireless Temperature Monitoring System 整合，您需要下列項目︰</span><span class="sxs-lookup"><span data-stu-id="0a4ce-111">To configure Azure AD integration with SensoScientific Wireless Temperature Monitoring System, you need the following items:</span></span>

- <span data-ttu-id="0a4ce-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0a4ce-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0a4ce-113">啟用 SensoScientific Wireless Temperature Monitoring System 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0a4ce-113">A SensoScientific Wireless Temperature Monitoring System single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a4ce-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a4ce-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="0a4ce-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a4ce-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0a4ce-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a4ce-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="0a4ce-118">Scenario description</span></span>
<span data-ttu-id="0a4ce-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a4ce-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="0a4ce-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a4ce-121">從資源庫新增 SensoScientific Wireless Temperature Monitoring System</span><span class="sxs-lookup"><span data-stu-id="0a4ce-121">Adding SensoScientific Wireless Temperature Monitoring System from the gallery</span></span>
2. <span data-ttu-id="0a4ce-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0a4ce-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-the-gallery"></a><span data-ttu-id="0a4ce-123">從資源庫新增 SensoScientific Wireless Temperature Monitoring System</span><span class="sxs-lookup"><span data-stu-id="0a4ce-123">Adding SensoScientific Wireless Temperature Monitoring System from the gallery</span></span>
<span data-ttu-id="0a4ce-124">若要設定將 SensoScientific Wireless Temperature Monitoring System 整合到 Azure AD 中，您需要從資源庫將 SensoScientific Wireless Temperature Monitoring System 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-124">To configure the integration of SensoScientific Wireless Temperature Monitoring System into Azure AD, you need to add SensoScientific Wireless Temperature Monitoring System from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0a4ce-125">**若要從資源庫新增 SensoScientific Wireless Temperature Monitoring System，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0a4ce-125">**To add SensoScientific Wireless Temperature Monitoring System from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0a4ce-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0a4ce-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0a4ce-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="0a4ce-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="0a4ce-133">在搜尋方塊中，輸入 **SensoScientific Wireless Temperature Monitoring System**。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-133">In the search box, type **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. <span data-ttu-id="0a4ce-135">在結果窗格中，選取 [SensoScientific Wireless Temperature Monitoring System]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-135">In the results panel, select **SensoScientific Wireless Temperature Monitoring System**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0a4ce-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0a4ce-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0a4ce-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試透過 SensoScientific Wireless Temperature Monitoring System 使用 Azure AD 單一登入功能。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-138">In this section, you configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0a4ce-139">若要讓單一登入運作，Azure AD 必須知道 SensoScientific Wireless Temperature Monitoring System 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SensoScientific Wireless Temperature Monitoring System is to a user in Azure AD.</span></span> <span data-ttu-id="0a4ce-140">換句話說，必須建立 Azure AD 使用者和 SensoScientific Wireless Temperature Monitoring System 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-140">In other words, a link relationship between an Azure AD user and the related user in SensoScientific Wireless Temperature Monitoring System needs to be established.</span></span>

<span data-ttu-id="0a4ce-141">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指派為 SensoScientific Wireless Temperature Monitoring System 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SensoScientific Wireless Temperature Monitoring System.</span></span>

<span data-ttu-id="0a4ce-142">若要設定及測試對 SensoScientific Wireless Temperature Monitoring System 的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="0a4ce-142">To configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0a4ce-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0a4ce-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0a4ce-145">**[建立 SensoScientific Wireless Temperature Monitoring System 測試使用者](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)** - 使 SensoScientific Wireless Temperature Monitoring System 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-145">**[Creating a SensoScientific Wireless Temperature Monitoring System test user](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)** - to have a counterpart of Britta Simon in SensoScientific Wireless Temperature Monitoring System that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0a4ce-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0a4ce-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0a4ce-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0a4ce-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0a4ce-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 SensoScientific 無線溫度監視系統應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SensoScientific Wireless Temperature Monitoring System application.</span></span>

<span data-ttu-id="0a4ce-150">**若要設定 Azure AD 單一登入與 SensoScientific Wireless Temperature Monitoring System 整合，請執行下列步驟︰**</span><span class="sxs-lookup"><span data-stu-id="0a4ce-150">**To configure Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, perform the following steps:**</span></span>

1. <span data-ttu-id="0a4ce-151">在 Azure 入口網站的 [SensoScientific Wireless Temperature Monitoring System] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-151">In the Azure portal, on the **SensoScientific Wireless Temperature Monitoring System** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="0a4ce-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. <span data-ttu-id="0a4ce-155">在 [SensoScientific Wireless Temperature Monitoring System 網域和 URL] 區段中，不需要執行任何步驟，因為應用程式已經與 Azure 預先整合：</span><span class="sxs-lookup"><span data-stu-id="0a4ce-155">On the **SensoScientific Wireless Temperature Monitoring System Domain and URLs** section, no need to perform any steps as the app is already pre-integrated with Azure:</span></span>

    ![設定單一登入](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. <span data-ttu-id="0a4ce-157">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. <span data-ttu-id="0a4ce-159">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-159">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0a4ce-161">在 [SensoScientific Wireless Temperature Monitoring System 設定] 區段中，按一下 [SensoScientific Wireless Temperature Monitoring System 系統] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-161">On the **SensoScientific Wireless Temperature Monitoring System Configuration** section, click **Configure SensoScientific Wireless Temperature Monitoring System** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0a4ce-162">從 [快速參考] 區段中，將登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL 複製。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-162">Copy the **Sign-Out URL, SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. <span data-ttu-id="0a4ce-164">以系統管理員身分登入您的 SensoScientific Wireless Temperature Monitoring System 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-164">Sign on to your SensoScientific Wireless Temperature Monitoring System application as an administrator.</span></span>

8. <span data-ttu-id="0a4ce-165">在頂端導覽功能表上，按一下 [設定]，然後前往 [單一登入] 下的 [設定] 開啟 [單一登入設定]。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-165">In the navigation menu on the top, click **Configuration** and goto **Configure** under **Single Sign On** to open the Single Sign On Settings.</span></span>

    ![設定單一登入](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. <span data-ttu-id="0a4ce-167">在 [單一登入設定] 表單中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0a4ce-167">In **Single Sign On Settings** form perform the following steps:</span></span>
 
    <span data-ttu-id="0a4ce-168">a.</span><span class="sxs-lookup"><span data-stu-id="0a4ce-168">a.</span></span> <span data-ttu-id="0a4ce-169">選取 [簽發者名稱]作為 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-169">Select **Issuer Name** as Azure AD.</span></span>
    
    <span data-ttu-id="0a4ce-170">b.</span><span class="sxs-lookup"><span data-stu-id="0a4ce-170">b.</span></span> <span data-ttu-id="0a4ce-171">將您從 Azure 入口網站複製的 **SAML 實體識別碼**貼入 [簽發者 URL] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-171">Paste the **SAML Entity ID** which you have copied from Azure portal into Issuer URL textbox.</span></span>
    
    <span data-ttu-id="0a4ce-172">c.</span><span class="sxs-lookup"><span data-stu-id="0a4ce-172">c.</span></span> <span data-ttu-id="0a4ce-173">將您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 貼入 [單一登入服務 URL] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-173">Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal into Single Sign-On Service URL textbox.</span></span>

    <span data-ttu-id="0a4ce-174">d.</span><span class="sxs-lookup"><span data-stu-id="0a4ce-174">d.</span></span> <span data-ttu-id="0a4ce-175">將您從 Azure 入口網站複製的 [登出 URL] 貼入 [單一登出服務 URL] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-175">Paste the **Sign-Out URL** which you have copied from Azure portal into Single Sign-Out Service URL textbox.</span></span>

    <span data-ttu-id="0a4ce-176">e.</span><span class="sxs-lookup"><span data-stu-id="0a4ce-176">e.</span></span> <span data-ttu-id="0a4ce-177">瀏覽您從 Azure 入口網站下載的憑證並在這裡上傳。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-177">Browse the certificate which you have downloaded from Azure portal and upload here.</span></span>
    
    <span data-ttu-id="0a4ce-178">f.</span><span class="sxs-lookup"><span data-stu-id="0a4ce-178">f.</span></span> <span data-ttu-id="0a4ce-179">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-179">Click **Save**.</span></span>
  
> [!TIP]
> <span data-ttu-id="0a4ce-180">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="0a4ce-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0a4ce-181">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0a4ce-182">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0a4ce-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0a4ce-183">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0a4ce-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="0a4ce-184">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="0a4ce-186">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0a4ce-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0a4ce-187">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0a4ce-189">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0a4ce-191">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0a4ce-193">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0a4ce-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0a4ce-195">a.</span><span class="sxs-lookup"><span data-stu-id="0a4ce-195">a.</span></span> <span data-ttu-id="0a4ce-196">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a4ce-197">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-197">b.</span></span> <span data-ttu-id="0a4ce-198">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0a4ce-199">c.</span><span class="sxs-lookup"><span data-stu-id="0a4ce-199">c.</span></span> <span data-ttu-id="0a4ce-200">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0a4ce-201">d.</span><span class="sxs-lookup"><span data-stu-id="0a4ce-201">d.</span></span> <span data-ttu-id="0a4ce-202">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-202">Click **Create**.</span></span>
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a><span data-ttu-id="0a4ce-203">建立 SensoScientific Wireless Temperature Monitoring System 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0a4ce-203">Creating a SensoScientific Wireless Temperature Monitoring System test user</span></span>

<span data-ttu-id="0a4ce-204">若要使 Azure AD 使用者能夠登入 SensoScientific Wireless Temperature Monitoring System，必須將他們佈建到 SensoScientific Wireless Temperature Monitoring System。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-204">To enable Azure AD users to log in to SensoScientific Wireless Temperature Monitoring System, they must be provisioned into SensoScientific Wireless Temperature Monitoring System.</span></span> <span data-ttu-id="0a4ce-205">使用 [SensoScientific Wireless Temperature Monitoring System 支援小組](https://www.sensoscientific.com/contact-us/) 在 SensoScientific Wireless Temperature Monitoring System 平台新增使用者。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-205">Work with [SensoScientific Wireless Temperature Monitoring System support team](https://www.sensoscientific.com/contact-us/) to add the users in the SensoScientific Wireless Temperature Monitoring System platform.</span></span> <span data-ttu-id="0a4ce-206">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-206">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0a4ce-207">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0a4ce-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0a4ce-208">在本節中，您會將 SensoScientific Wireless Temperature Monitoring System 支援小組的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SensoScientific Wireless Temperature Monitoring System.</span></span>

![指派使用者][200] 

<span data-ttu-id="0a4ce-210">**若要將 Britta Simon 指派給 SensoScientific Wireless Temperature Monitoring System，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0a4ce-210">**To assign Britta Simon to SensoScientific Wireless Temperature Monitoring System, perform the following steps:**</span></span>

1. <span data-ttu-id="0a4ce-211">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="0a4ce-213">在應用程式清單中，選取 **SensoScientific Wireless Temperature Monitoring System**。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-213">In the applications list, select **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![設定單一登入](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. <span data-ttu-id="0a4ce-215">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-215">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="0a4ce-217">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-217">Click **Add** button.</span></span> <span data-ttu-id="0a4ce-218">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="0a4ce-220">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0a4ce-221">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0a4ce-222">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0a4ce-223">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="0a4ce-223">Testing single sign-on</span></span>

<span data-ttu-id="0a4ce-224">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="0a4ce-225">在存取面板中按一下 [SensoScientific Wireless Temperature Monitoring System] 圖格，系統會將您自動登入 SensoScientific Wireless Temperature Monitoring System 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-225">Click the SensoScientific Wireless Temperature Monitoring System tile in the Access Panel, you will be automatically signed-on to your SensoScientific Wireless Temperature Monitoring System application.</span></span> <span data-ttu-id="0a4ce-226">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="0a4ce-226">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0a4ce-227">其他資源</span><span class="sxs-lookup"><span data-stu-id="0a4ce-227">Additional resources</span></span>

* [<span data-ttu-id="0a4ce-228">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="0a4ce-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0a4ce-229">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="0a4ce-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png


---
title: "教學課程：Azure Active Directory 與 SAP NetWeaver 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 SAP NetWeaver 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1b9e59e3-e7ae-4e74-b16c-8c1a7ccfdef3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: ad4140eb1183094a67822ad92eabcd35101360b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-netweaver"></a><span data-ttu-id="a8c64-103">教學課程：Azure Active Directory 與 SAP NetWeaver 整合</span><span class="sxs-lookup"><span data-stu-id="a8c64-103">Tutorial: Azure Active Directory integration with SAP NetWeaver</span></span>

<span data-ttu-id="a8c64-104">在本教學課程中，您會了解如何整合 SAP NetWeaver 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="a8c64-104">In this tutorial, you learn how to integrate SAP NetWeaver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a8c64-105">SAP NetWeaver 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="a8c64-105">Integrating SAP NetWeaver with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a8c64-106">您可以在 Azure AD 中控制可存取 SAP NetWeaver 的人員</span><span class="sxs-lookup"><span data-stu-id="a8c64-106">You can control in Azure AD who has access to SAP NetWeaver</span></span>
- <span data-ttu-id="a8c64-107">您可以讓使用者使用其 Azure AD 帳戶自動登入 SAP NetWeaver (單一登入)</span><span class="sxs-lookup"><span data-stu-id="a8c64-107">You can enable your users to automatically get signed-on to SAP NetWeaver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a8c64-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="a8c64-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a8c64-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a8c64-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a8c64-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a8c64-110">Prerequisites</span></span>

<span data-ttu-id="a8c64-111">若要設定 Azure AD 與 SAP NetWeaver 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="a8c64-111">To configure Azure AD integration with SAP NetWeaver, you need the following items:</span></span>

- <span data-ttu-id="a8c64-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a8c64-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a8c64-113">啟用 SAP NetWeaver 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a8c64-113">An SAP NetWeaver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a8c64-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a8c64-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a8c64-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="a8c64-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a8c64-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a8c64-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a8c64-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="a8c64-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a8c64-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="a8c64-118">Scenario description</span></span>
<span data-ttu-id="a8c64-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a8c64-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a8c64-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="a8c64-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a8c64-121">從資源庫新增 SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="a8c64-121">Adding SAP NetWeaver from the gallery</span></span>
2. <span data-ttu-id="a8c64-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a8c64-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-netweaver-from-the-gallery"></a><span data-ttu-id="a8c64-123">從資源庫新增 SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="a8c64-123">Adding SAP NetWeaver from the gallery</span></span>
<span data-ttu-id="a8c64-124">若要設定 SAP NetWeaver 與 Azure AD 整合，您需要從資源庫將 SAP NetWeaver 新增到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="a8c64-124">To configure the integration of SAP NetWeaver into Azure AD, you need to add SAP NetWeaver from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a8c64-125">**若要從資源庫新增 SAP NetWeaver，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a8c64-125">**To add SAP NetWeaver from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a8c64-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="a8c64-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a8c64-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a8c64-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a8c64-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a8c64-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="a8c64-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a8c64-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="a8c64-133">在搜尋方塊中，輸入 **SAP NetWeaver**。</span><span class="sxs-lookup"><span data-stu-id="a8c64-133">In the search box, type **SAP NetWeaver**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_search.png)

5. <span data-ttu-id="a8c64-135">在結果窗格中，選取 [SAP NetWeaver]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="a8c64-135">In the results panel, select **SAP NetWeaver**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a8c64-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a8c64-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a8c64-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 SAP NetWeaver 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a8c64-138">In this section, you configure and test Azure AD single sign-on with SAP NetWeaver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a8c64-139">若要讓單一登入運作，Azure AD 必須知道 SAP NetWeaver 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="a8c64-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP NetWeaver is to a user in Azure AD.</span></span> <span data-ttu-id="a8c64-140">換句話說，必須在 Azure AD 使用者與 SAP NetWeaver 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="a8c64-140">In other words, a link relationship between an Azure AD user and the related user in SAP NetWeaver needs to be established.</span></span>

<span data-ttu-id="a8c64-141">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值，指派為 SAP NetWeaver 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="a8c64-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP NetWeaver.</span></span>

<span data-ttu-id="a8c64-142">若要使用 SAP NetWeaver 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="a8c64-142">To configure and test Azure AD single sign-on with SAP NetWeaver, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a8c64-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="a8c64-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a8c64-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a8c64-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a8c64-145">**[建立 SAP NetWeaver 測試使用者](#creating-an-sap-netweaver-test-user)** - 使 SAP NetWeaver 中 Britta Simon 的對應身分連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="a8c64-145">**[Creating an SAP NetWeaver test user](#creating-an-sap-netweaver-test-user)** - to have a counterpart of Britta Simon in SAP NetWeaver that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a8c64-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a8c64-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a8c64-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="a8c64-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a8c64-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a8c64-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a8c64-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 SAP NetWeaver 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="a8c64-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP NetWeaver application.</span></span>

<span data-ttu-id="a8c64-150">**若要使用 SAP NetWeaver 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a8c64-150">**To configure Azure AD single sign-on with SAP NetWeaver, perform the following steps:**</span></span>

1. <span data-ttu-id="a8c64-151">在 Azure 入口網站的 [SAP NetWeaver] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="a8c64-151">In the Azure portal, on the **SAP NetWeaver** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="a8c64-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="a8c64-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_samlbase.png)

3. <span data-ttu-id="a8c64-155">在 [SAP NetWeaver 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a8c64-155">On the **SAP NetWeaver Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_url.png)

    <span data-ttu-id="a8c64-157">a.</span><span class="sxs-lookup"><span data-stu-id="a8c64-157">a.</span></span> <span data-ttu-id="a8c64-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="a8c64-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="a8c64-159">b.</span><span class="sxs-lookup"><span data-stu-id="a8c64-159">b.</span></span> <span data-ttu-id="a8c64-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="a8c64-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="a8c64-161">c.</span><span class="sxs-lookup"><span data-stu-id="a8c64-161">c.</span></span> <span data-ttu-id="a8c64-162">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span><span class="sxs-lookup"><span data-stu-id="a8c64-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="a8c64-163">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="a8c64-163">These values are not the real.</span></span> <span data-ttu-id="a8c64-164">使用實際的識別碼和回覆 URL 與登入 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="a8c64-164">Update these values with the actual Identifier and Reply URL and Sign-On URL.</span></span> <span data-ttu-id="a8c64-165">在此建議您在 [識別碼] 中使用唯一的字串值。</span><span class="sxs-lookup"><span data-stu-id="a8c64-165">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="a8c64-166">請連絡 [SAP NetWeaver 用戶端支援小組](https://www.sap.com/support.html)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="a8c64-166">Contact [SAP NetWeaver Client support team](https://www.sap.com/support.html) to get these values.</span></span> 

4. <span data-ttu-id="a8c64-167">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="a8c64-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_certificate.png) 

5. <span data-ttu-id="a8c64-169">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a8c64-169">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="a8c64-171">在 [SAP NetWeaver 組態] 區段上，按一下 [設定 SAP NetWeaver] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="a8c64-171">On the **SAP NetWeaver Configuration** section, click **Configure SAP NetWeaver** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a8c64-172">從 [快速參考]  區段複製 [SAML 實體識別碼]。</span><span class="sxs-lookup"><span data-stu-id="a8c64-172">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_configure.png) 

7. <span data-ttu-id="a8c64-174">若要在 **SAP NetWeaver** 端設定單一登入，您需要將所下載的**「中繼資料 XML」**和**「SAML 實體識別碼」**傳送給 [SAP NetWeaver 支援小組](https://www.sap.com/support.html)。</span><span class="sxs-lookup"><span data-stu-id="a8c64-174">To configure single sign-on on **SAP NetWeaver** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [SAP NetWeaver support](https://www.sap.com/support.html).</span></span> 

> [!TIP]
> <span data-ttu-id="a8c64-175">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="a8c64-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a8c64-176">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="a8c64-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a8c64-177">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a8c64-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a8c64-178">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a8c64-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="a8c64-179">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a8c64-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="a8c64-181">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a8c64-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a8c64-182">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="a8c64-182">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a8c64-184">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="a8c64-184">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a8c64-186">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="a8c64-186">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a8c64-188">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a8c64-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a8c64-190">a.</span><span class="sxs-lookup"><span data-stu-id="a8c64-190">a.</span></span> <span data-ttu-id="a8c64-191">在 [名稱] 文字方塊中，輸入 **Britta Simon**。</span><span class="sxs-lookup"><span data-stu-id="a8c64-191">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="a8c64-192">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="a8c64-192">b.</span></span> <span data-ttu-id="a8c64-193">在 [使用者名稱] 文字方塊中，輸入 Britta Simon 的「電子郵件地址」。</span><span class="sxs-lookup"><span data-stu-id="a8c64-193">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="a8c64-194">c.</span><span class="sxs-lookup"><span data-stu-id="a8c64-194">c.</span></span> <span data-ttu-id="a8c64-195">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="a8c64-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a8c64-196">d.</span><span class="sxs-lookup"><span data-stu-id="a8c64-196">d.</span></span> <span data-ttu-id="a8c64-197">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a8c64-197">Click **Create**.</span></span>
 
### <a name="creating-an-sap-netweaver-test-user"></a><span data-ttu-id="a8c64-198">建立 SAP NetWeaver 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a8c64-198">Creating an SAP NetWeaver test user</span></span>

<span data-ttu-id="a8c64-199">在本節中，您要在 SAP NetWeaver 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="a8c64-199">In this section, you create a user called Britta Simon in SAP NetWeaver.</span></span> <span data-ttu-id="a8c64-200">請與您的 [SAP NetWeaver 支援小組](https://www.sap.com/support.html)合作，在 SAP NetWeaver 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="a8c64-200">Work with your [SAP NetWeaver support](https://www.sap.com/support.html) to add the users in the SAP NetWeaver platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a8c64-201">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a8c64-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a8c64-202">在本節中，您會將 SAP NetWeaver 的存取權授與 ，讓 Britta Simon 能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a8c64-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP NetWeaver.</span></span>

![指派使用者][200] 

<span data-ttu-id="a8c64-204">**如要將 Britta Simon 指派給 SAP NetWeaver，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="a8c64-204">**To assign Britta Simon to SAP NetWeaver, perform the following steps:**</span></span>

1. <span data-ttu-id="a8c64-205">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="a8c64-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="a8c64-207">在應用程式清單中，選取 [SAP NetWeaver] 。</span><span class="sxs-lookup"><span data-stu-id="a8c64-207">In the applications list, select **SAP NetWeaver**.</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_app.png) 

3. <span data-ttu-id="a8c64-209">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a8c64-209">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="a8c64-211">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a8c64-211">Click **Add** button.</span></span> <span data-ttu-id="a8c64-212">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a8c64-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="a8c64-214">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="a8c64-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a8c64-215">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a8c64-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a8c64-216">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a8c64-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a8c64-217">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="a8c64-217">Testing single sign-on</span></span>

<span data-ttu-id="a8c64-218">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="a8c64-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a8c64-219">當您在存取面板中按一下 [SAP NetWeaver] 圖格時，應該會自動登入您的 SAP NetWeaver 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a8c64-219">When you click the SAP NetWeaver tile in the Access Panel, you should get automatically signed-on to your SAP NetWeaver application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a8c64-220">其他資源</span><span class="sxs-lookup"><span data-stu-id="a8c64-220">Additional resources</span></span>

* [<span data-ttu-id="a8c64-221">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="a8c64-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a8c64-222">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a8c64-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_203.png


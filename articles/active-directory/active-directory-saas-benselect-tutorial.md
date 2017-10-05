---
title: "教學課程：Azure Active Directory 與 BenSelect 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 BenSelect 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: f8caa023da05863372b7ef92b47a92168445d741
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a><span data-ttu-id="8d01d-103">教學課程：Azure Active Directory 與 BenSelect 整合</span><span class="sxs-lookup"><span data-stu-id="8d01d-103">Tutorial: Azure Active Directory integration with BenSelect</span></span>

<span data-ttu-id="8d01d-104">在本教學課程中，您將了解如何整合 BenSelect 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="8d01d-104">In this tutorial, you learn how to integrate BenSelect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d01d-105">將 BenSelect 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="8d01d-105">Integrating BenSelect with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8d01d-106">您可以在 Azure AD 中管控可存取 BenSelect 的人員</span><span class="sxs-lookup"><span data-stu-id="8d01d-106">You can control in Azure AD who has access to BenSelect</span></span>
- <span data-ttu-id="8d01d-107">您可以讓使用者透過其 Azure AD 帳戶自動登入 BenSelect (單一登入)</span><span class="sxs-lookup"><span data-stu-id="8d01d-107">You can enable your users to automatically get signed-on to BenSelect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8d01d-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="8d01d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8d01d-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="8d01d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d01d-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="8d01d-110">Prerequisites</span></span>

<span data-ttu-id="8d01d-111">若要設定 Azure AD 與 BenSelect 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="8d01d-111">To configure Azure AD integration with BenSelect, you need the following items:</span></span>

- <span data-ttu-id="8d01d-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8d01d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d01d-113">已啟用 BenSelect 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8d01d-113">A BenSelect single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d01d-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="8d01d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8d01d-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="8d01d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8d01d-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="8d01d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d01d-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="8d01d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d01d-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="8d01d-118">Scenario description</span></span>
<span data-ttu-id="8d01d-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8d01d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8d01d-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="8d01d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d01d-121">從資源庫新增 BenSelect</span><span class="sxs-lookup"><span data-stu-id="8d01d-121">Adding BenSelect from the gallery</span></span>
2. <span data-ttu-id="8d01d-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8d01d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benselect-from-the-gallery"></a><span data-ttu-id="8d01d-123">從資源庫新增 BenSelect</span><span class="sxs-lookup"><span data-stu-id="8d01d-123">Adding BenSelect from the gallery</span></span>
<span data-ttu-id="8d01d-124">若要設定將 BenSelect 整合到 Azure AD 中，您需要從資源庫將 BenSelect 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="8d01d-124">To configure the integration of BenSelect into Azure AD, you need to add BenSelect from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8d01d-125">**若要從資源庫加入 BenSelect，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8d01d-125">**To add BenSelect from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8d01d-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="8d01d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8d01d-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8d01d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8d01d-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8d01d-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="8d01d-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8d01d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="8d01d-133">在搜尋方塊中，輸入 **BenSelect**。</span><span class="sxs-lookup"><span data-stu-id="8d01d-133">In the search box, type **BenSelect**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_search.png)

5. <span data-ttu-id="8d01d-135">在結果面板中，選取 [BenSelect]，然後按一下 [新增] 按鈕以新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d01d-135">In the results panel, select **BenSelect**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8d01d-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8d01d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8d01d-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 BenSelect 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8d01d-138">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8d01d-139">若要讓單一登入能夠運作，Azure AD 必須知道 BenSelect 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="8d01d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenSelect is to a user in Azure AD.</span></span> <span data-ttu-id="8d01d-140">換句話說，必須在 Azure AD 使用者與 BenSelect 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="8d01d-140">In other words, a link relationship between an Azure AD user and the related user in BenSelect needs to be established.</span></span>

<span data-ttu-id="8d01d-141">在 BenSelect 中，將 [Username] 的值指派為 Azure AD 中 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="8d01d-141">In BenSelect, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8d01d-142">若要設定及測試與 BenSelect 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="8d01d-142">To configure and test Azure AD single sign-on with BenSelect, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8d01d-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="8d01d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8d01d-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8d01d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8d01d-145">**[建立 BenSelect 測試使用者](#creating-a-benselect-test-user)** - 在 BenSelect 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="8d01d-145">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - to have a counterpart of Britta Simon in BenSelect that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8d01d-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8d01d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8d01d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="8d01d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8d01d-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8d01d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8d01d-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 BenSelect 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="8d01d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenSelect application.</span></span>

<span data-ttu-id="8d01d-150">**若要設定與 BenSelect 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8d01d-150">**To configure Azure AD single sign-on with BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="8d01d-151">在 Azure 入口網站的 [BenSelect] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="8d01d-151">In the Azure portal, on the **BenSelect** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="8d01d-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="8d01d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_samlbase.png)

3. <span data-ttu-id="8d01d-155">在 [BenSelect 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8d01d-155">On the **BenSelect Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_url.png)

    <span data-ttu-id="8d01d-157">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="8d01d-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8d01d-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="8d01d-158">This value is not real.</span></span> <span data-ttu-id="8d01d-159">請使用實際的「回覆 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="8d01d-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="8d01d-160">請連絡 [BenSelect 支援小組](mailto:support@selerix.com)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="8d01d-160">Contact [BenSelect support team](mailto:support@selerix.com) to get this value.</span></span>
 
4. <span data-ttu-id="8d01d-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (原始)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="8d01d-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_certificate.png) 

5. <span data-ttu-id="8d01d-163">BenSelect 應用程式需要特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="8d01d-163">BenSelect application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="8d01d-164">設定此應用程式的下列宣告。</span><span class="sxs-lookup"><span data-stu-id="8d01d-164">Configure the following claims for this application.</span></span> <span data-ttu-id="8d01d-165">您可以在應用程式整合頁面的 [使用者屬性] 區段中，管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="8d01d-165">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="8d01d-166">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="8d01d-166">The following screenshot shows an example for this.</span></span>

    ![設定單一登入](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_06.png)

6. <span data-ttu-id="8d01d-168">在 [單一登入] 對話方塊的 [使用者屬性] 區段中：</span><span class="sxs-lookup"><span data-stu-id="8d01d-168">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="8d01d-169">a.</span><span class="sxs-lookup"><span data-stu-id="8d01d-169">a.</span></span> <span data-ttu-id="8d01d-170">在 [使用者識別碼] 下拉式清單中，選取 [ExtractMailPrefix]。</span><span class="sxs-lookup"><span data-stu-id="8d01d-170">In the **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="8d01d-171">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d01d-171">b.</span></span> <span data-ttu-id="8d01d-172">在 [郵件] 下拉式清單中，選取 [user.userprincipalname]。</span><span class="sxs-lookup"><span data-stu-id="8d01d-172">In the **Mail** dropdown list, select **user.userprincipalname**.</span></span>

7. <span data-ttu-id="8d01d-173">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8d01d-173">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-benselect-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8d01d-175">在 [BenSelect 組態] 區段上，按一下 [設定 BenSelect] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="8d01d-175">On the **BenSelect Configuration** section, click **Configure BenSelect** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8d01d-176">從 [快速參考] 區段中複製「登出 URL」、「SAML 實體識別碼」及「SAML 單一登入服務 URL」。</span><span class="sxs-lookup"><span data-stu-id="8d01d-176">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_configure.png) 

9. <span data-ttu-id="8d01d-178">若要在 **BenSelect** 端設定單一登入，您必須將已下載的「憑證 (原始)」、「登出 URL」、「SAML 實體識別碼」及「SAML 單一登入服務 URL」傳送給 [BenSelect 支援小組](mailto:support@selerix.com)。</span><span class="sxs-lookup"><span data-stu-id="8d01d-178">To configure single sign-on on **BenSelect** side, you need to send the downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [BenSelect support team](mailto:support@selerix.com).</span></span>

   >[!NOTE]
   ><span data-ttu-id="8d01d-179">您必須提到這項整合需要 SHA256 演算法 (不支援 SHA1)，以便在適當的伺服器 (如 app2101 等) 上設定 SSO。</span><span class="sxs-lookup"><span data-stu-id="8d01d-179">You need to mention that this integration requires the SHA256 algorithm (SHA1 is not supported) to set the SSO on the appropriate server like app2101 etc.</span></span> 
   
> [!TIP]
> <span data-ttu-id="8d01d-180">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="8d01d-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8d01d-181">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="8d01d-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8d01d-182">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8d01d-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8d01d-183">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8d01d-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="8d01d-184">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="8d01d-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="8d01d-186">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8d01d-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8d01d-187">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="8d01d-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-benselect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8d01d-189">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="8d01d-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-benselect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8d01d-191">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="8d01d-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-benselect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8d01d-193">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8d01d-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-benselect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8d01d-195">a.</span><span class="sxs-lookup"><span data-stu-id="8d01d-195">a.</span></span> <span data-ttu-id="8d01d-196">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="8d01d-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8d01d-197">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d01d-197">b.</span></span> <span data-ttu-id="8d01d-198">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="8d01d-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8d01d-199">c.</span><span class="sxs-lookup"><span data-stu-id="8d01d-199">c.</span></span> <span data-ttu-id="8d01d-200">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="8d01d-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8d01d-201">d.</span><span class="sxs-lookup"><span data-stu-id="8d01d-201">d.</span></span> <span data-ttu-id="8d01d-202">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="8d01d-202">Click **Create**.</span></span>
 
### <a name="creating-a-benselect-test-user"></a><span data-ttu-id="8d01d-203">建立 BenSelect 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8d01d-203">Creating a BenSelect test user</span></span>

<span data-ttu-id="8d01d-204">本節的目標是要在 BenSelect 中建立一個名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="8d01d-204">The objective of this section is to create a user called Britta Simon in BenSelect.</span></span> <span data-ttu-id="8d01d-205">請與 [BenSelect 支援小組](mailto:support@selerix.com)合作，在 BenSelect 帳戶中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="8d01d-205">Work with [BenSelect support team](mailto:support@selerix.com) to add the users in the BenSelect account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8d01d-206">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8d01d-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8d01d-207">在本節中，您會將 BenSelect 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8d01d-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenSelect.</span></span>

![指派使用者][200] 

<span data-ttu-id="8d01d-209">**若要將 Britta Simon 指派給 BenSelect，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="8d01d-209">**To assign Britta Simon to BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="8d01d-210">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8d01d-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="8d01d-212">在應用程式清單中，選取 [BenSelect]。</span><span class="sxs-lookup"><span data-stu-id="8d01d-212">In the applications list, select **BenSelect**.</span></span>

    ![設定單一登入](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_app.png) 

3. <span data-ttu-id="8d01d-214">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="8d01d-214">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="8d01d-216">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8d01d-216">Click **Add** button.</span></span> <span data-ttu-id="8d01d-217">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="8d01d-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="8d01d-219">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="8d01d-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8d01d-220">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8d01d-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8d01d-221">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8d01d-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8d01d-222">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="8d01d-222">Testing single sign-on</span></span>

<span data-ttu-id="8d01d-223">在本節中，您會使用存取面板來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="8d01d-223">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="8d01d-224">當您在「存取面板」中按一下 [BenSelect] 圖格時，應該會自動登入您的 BenSelect 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d01d-224">When you click the BenSelect tile in the Access Panel, you should get automatically signed-on to your BenSelect application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8d01d-225">其他資源</span><span class="sxs-lookup"><span data-stu-id="8d01d-225">Additional resources</span></span>

* [<span data-ttu-id="8d01d-226">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="8d01d-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8d01d-227">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="8d01d-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_203.png


---
title: "教學課程：Azure Active Directory 與 Absorb LMS 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Absorb LMS 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 3c68c3ac7d6be593476d419f8c015931b206eead
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a><span data-ttu-id="8cd0e-103">教學課程：Azure Active Directory 與 Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="8cd0e-103">Tutorial: Azure Active Directory integration with Absorb LMS</span></span>

<span data-ttu-id="8cd0e-104">在本教學課程中，您將了解如何整合 Absorb LMS 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-104">In this tutorial, you learn how to integrate Absorb LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8cd0e-105">將 Absorb LMS 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="8cd0e-105">Integrating Absorb LMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8cd0e-106">您可以在 Azure AD 中控制可存取 Absorb LMS 的人員</span><span class="sxs-lookup"><span data-stu-id="8cd0e-106">You can control in Azure AD who has access to Absorb LMS</span></span>
- <span data-ttu-id="8cd0e-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Absorb LMS (單一登入)</span><span class="sxs-lookup"><span data-stu-id="8cd0e-107">You can enable your users to automatically get signed-on to Absorb LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8cd0e-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="8cd0e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8cd0e-109">如果您想要知道與 Azure AD 整合的 SaaS 應用程式詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="8cd0e-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="8cd0e-110">[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8cd0e-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="8cd0e-111">Prerequisites</span></span>

<span data-ttu-id="8cd0e-112">若要設定與 Absorb LMS 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="8cd0e-112">To configure Azure AD integration with Absorb LMS, you need the following items:</span></span>

- <span data-ttu-id="8cd0e-113">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8cd0e-113">An Azure AD subscription</span></span>
- <span data-ttu-id="8cd0e-114">已啟用 Absorb LMS 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8cd0e-114">An Absorb LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8cd0e-115">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8cd0e-116">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="8cd0e-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8cd0e-117">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8cd0e-118">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8cd0e-119">案例描述</span><span class="sxs-lookup"><span data-stu-id="8cd0e-119">Scenario description</span></span>
<span data-ttu-id="8cd0e-120">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8cd0e-121">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="8cd0e-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8cd0e-122">從資源庫新增 Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="8cd0e-122">Adding Absorb LMS from the gallery</span></span>
2. <span data-ttu-id="8cd0e-123">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8cd0e-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-absorb-lms-from-the-gallery"></a><span data-ttu-id="8cd0e-124">從資源庫新增 Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="8cd0e-124">Adding Absorb LMS from the gallery</span></span>
<span data-ttu-id="8cd0e-125">若要設定將 Absorb LMS 整合到 Azure AD 中，您需要從資源庫將 Absorb LMS 新增到受管理的 SaaS app 清單。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-125">To configure the integration of Absorb LMS in to Azure AD, you need to add Absorb LMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8cd0e-126">**若要從資源庫新增 Absorb LMS，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8cd0e-126">**To add Absorb LMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8cd0e-127">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="8cd0e-129">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8cd0e-130">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-130">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="8cd0e-132">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="8cd0e-134">在搜尋方塊中，輸入 **Absorb LMS**，從結果面板中選取 [Absorb LMS]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-134">In the search box, type **Absorb LMS**, select **Absorb LMS** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8cd0e-136">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8cd0e-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8cd0e-137">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Absorb LMS 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-137">In this section, you configure and test Azure AD single sign-on with Absorb LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8cd0e-138">若要讓單一登入能夠運作，Azure AD 必須知道 Absorb LMS 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-138">For single sign-on to work, Azure AD needs to know what the counterpart user in Absorb LMS is to a user in Azure AD.</span></span> <span data-ttu-id="8cd0e-139">換句話說，必須在 Azure AD 使用者與 Absorb LMS 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-139">In other words, a link relationship between an Azure AD user and the related user in Absorb LMS needs to be established.</span></span>

<span data-ttu-id="8cd0e-140">建立此連結關聯性的方法，就是將 Absorb LMS 中 [Username] 的值指派為 Azure AD 中 [使用者名稱] 的值。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Absorb LMS.</span></span>

<span data-ttu-id="8cd0e-141">若要設定及測試與 Absorb LMS 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="8cd0e-141">To configure and test Azure AD single sign-on with Absorb LMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8cd0e-142">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-142">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8cd0e-143">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-143">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8cd0e-144">**[建立 Absorb LMS 測試使用者](#create-an-absorb-lms-test-user)** - 使 Absorb LMS 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-144">**[Create an Absorb LMS test user](#create-an-absorb-lms-test-user)** - to have a counterpart of Britta Simon in Absorb LMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8cd0e-145">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-145">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8cd0e-146">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-146">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8cd0e-147">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8cd0e-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8cd0e-148">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Absorb LMS 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Absorb LMS application.</span></span>

<span data-ttu-id="8cd0e-149">**若要設定與 Absorb LMS 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8cd0e-149">**To configure Azure AD single sign-on with Absorb LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="8cd0e-150">在 Azure 入口網站的 [Absorb LMS] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-150">In the Azure portal, on the **Absorb LMS** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="8cd0e-152">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. <span data-ttu-id="8cd0e-154">在 [Absorb LMS 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8cd0e-154">On the **Absorb LMS Domain and URLs** section, perform the following steps:</span></span>

    ![Absorb LMS 網域與 URL 單一登入資訊](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    <span data-ttu-id="8cd0e-156">a.</span><span class="sxs-lookup"><span data-stu-id="8cd0e-156">a.</span></span> <span data-ttu-id="8cd0e-157">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="8cd0e-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>

    <span data-ttu-id="8cd0e-158">b.</span><span class="sxs-lookup"><span data-stu-id="8cd0e-158">b.</span></span> <span data-ttu-id="8cd0e-159">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="8cd0e-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="8cd0e-160">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-160">These values are not the real.</span></span> <span data-ttu-id="8cd0e-161">請使用實際的識別碼和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-161">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="8cd0e-162">請連絡 [Absorb LMS 用戶端支援小組](https://www.absorblms.com/support)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-162">Contact [Absorb LMS Client support team](https://www.absorblms.com/support) to get these values.</span></span> 

4. <span data-ttu-id="8cd0e-163">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. <span data-ttu-id="8cd0e-165">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-165">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="8cd0e-167">在 [Absorb LMS 組態] 區段上，按一下 [設定 Absorb LMS] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-167">On the **Absorb LMS Configuration** section, click **Configure Absorb LMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8cd0e-168">從 [快速參考] 區段中複製 [登出 URL 和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-168">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Absorb LMS 設定](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. <span data-ttu-id="8cd0e-170">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Absorb LMS 公司網站。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-170">In a different web browser window, log in to your Absorb LMS company site as an administrator.</span></span>

9. <span data-ttu-id="8cd0e-171">按一下系統管理介面上的 [帳戶圖示]。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-171">Click the **Account Icon** on the admin interface.</span></span> 

    ![設定單一登入](./media/active-directory-saas-absorblms-tutorial/1.png)

10. <span data-ttu-id="8cd0e-173">按一下 [入口網站設定]。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-173">Click **Portal Settings**.</span></span>

    ![設定單一登入](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. <span data-ttu-id="8cd0e-175">按一下 [使用者] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-175">Click the **Users** tab.</span></span>

    ![設定單一登入](./media/active-directory-saas-absorblms-tutorial/3.png)

12. <span data-ttu-id="8cd0e-177">執行下列步驟以存取單一登入設定欄位：</span><span class="sxs-lookup"><span data-stu-id="8cd0e-177">Perform the following steps to access the Single Sign-On configuration fields:</span></span>

    ![設定單一登入](./media/active-directory-saas-absorblms-tutorial/4.png)

    <span data-ttu-id="8cd0e-179">a.</span><span class="sxs-lookup"><span data-stu-id="8cd0e-179">a.</span></span> <span data-ttu-id="8cd0e-180">選取適當**模式**。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-180">Select the appropriate **Mode**.</span></span>

    <span data-ttu-id="8cd0e-181">b.</span><span class="sxs-lookup"><span data-stu-id="8cd0e-181">b.</span></span> <span data-ttu-id="8cd0e-182">在記事本中開啟您從 Azure 入口網站下載的憑證，移除 **---BEGIN CERTIFICATE---** 和 **---END CERTIFICATE---** 標記，然後在 [金鑰] 文字方塊中貼上其餘內容。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-182">Open the Certificate that you have downloaded from the Azure portal in notepad, remove the **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste the remaining content in the **Key** textbox.</span></span>
    
    <span data-ttu-id="8cd0e-183">c.</span><span class="sxs-lookup"><span data-stu-id="8cd0e-183">c.</span></span> <span data-ttu-id="8cd0e-184">在 [識別碼屬性] 中，選取您已設定為 Azure AD 使用者識別碼的適當屬性 (例如，如果在 Azure AD 中選取 userprinciplename，則這裡會選取使用者名稱)。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-184">In the **Id Property**, select the appropriate attribute which you have configured as the user identifier in the Azure AD (For example, If the userprinciplename is selected in Azure AD, then Username would be selected here.)</span></span>

    <span data-ttu-id="8cd0e-185">d.</span><span class="sxs-lookup"><span data-stu-id="8cd0e-185">d.</span></span> <span data-ttu-id="8cd0e-186">在 [登入 URL] 中，貼上您從 Azure 入口網站的 [設定登入] 視窗所複製的 **SAML 單一登入服務 URL** 值。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-186">In the **Login URL**, paste the **“SAML Single Sign-On Service URL”** value you have copied from the **Configure sign-on** window of the Azure portal.</span></span>

    <span data-ttu-id="8cd0e-187">e.</span><span class="sxs-lookup"><span data-stu-id="8cd0e-187">e.</span></span> <span data-ttu-id="8cd0e-188">在 [登出 URL] 中，貼上您從 Azure 入口網站的 [設定登入] 視窗所複製的**登出 URL** 值。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-188">In the **Logout URL**, paste the **“Sign-Out URL”** value you have copied from the **Configure sign-on** window of the Azure portal.</span></span>

13. <span data-ttu-id="8cd0e-189">啟用 [只允許 SSO 登入]。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-189">Enable **‘Only Allow SSO Login’**.</span></span>

    ![設定單一登入](./media/active-directory-saas-absorblms-tutorial/5.png)

14. <span data-ttu-id="8cd0e-191">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-191">Click **"Save."**</span></span>

> [!TIP]
> <span data-ttu-id="8cd0e-192">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="8cd0e-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8cd0e-193">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8cd0e-194">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8cd0e-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8cd0e-195">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8cd0e-195">Create an Azure AD test user</span></span>

<span data-ttu-id="8cd0e-196">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 測試使用者][100]

<span data-ttu-id="8cd0e-198">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8cd0e-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8cd0e-199">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8cd0e-201">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8cd0e-203">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-203">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![[新增] 按鈕](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8cd0e-205">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8cd0e-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![[使用者] 對話方塊](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8cd0e-207">a.</span><span class="sxs-lookup"><span data-stu-id="8cd0e-207">a.</span></span> <span data-ttu-id="8cd0e-208">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8cd0e-209">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-209">b.</span></span> <span data-ttu-id="8cd0e-210">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8cd0e-211">c.</span><span class="sxs-lookup"><span data-stu-id="8cd0e-211">c.</span></span> <span data-ttu-id="8cd0e-212">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8cd0e-213">d.</span><span class="sxs-lookup"><span data-stu-id="8cd0e-213">d.</span></span> <span data-ttu-id="8cd0e-214">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-214">Click **Create**.</span></span>

### <a name="create-an-absorb-lms-test-user"></a><span data-ttu-id="8cd0e-215">建立 Absorb LMS 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8cd0e-215">Create an Absorb LMS test user</span></span>

<span data-ttu-id="8cd0e-216">若要讓 Azure AD 使用者能夠登入 Absorb LMS，必須將他們佈建到 Absorb LMS。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-216">To enable Azure AD users to log in to Absorb LMS, they must be provisioned in to Absorb LMS.</span></span>  
<span data-ttu-id="8cd0e-217">就 Absorb LMS 而言，需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-217">For Absorb LMS, provisioning is a manual task.</span></span>

<span data-ttu-id="8cd0e-218">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8cd0e-218">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="8cd0e-219">以系統管理員身分登入您的 Absorb LMS 公司網站。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-219">Log in to your Absorb LMS company site as an administrator.</span></span>

2. <span data-ttu-id="8cd0e-220">按一下 [使用者] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-220">Click **Users** tab.</span></span>

    ![邀請人員](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. <span data-ttu-id="8cd0e-222">按一下 [使用者] 索引標籤底下的 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-222">Click **Users** under the **Users** tab.</span></span>

    ![邀請人員](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  <span data-ttu-id="8cd0e-224">從 [新增] 下拉式清單選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-224">Select **User** from **Add New** drop-down.</span></span>

    ![邀請人員](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. <span data-ttu-id="8cd0e-226">在 [新增使用者] 頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8cd0e-226">On the **Add User** page, perform the following steps:</span></span>

    ![邀請人員](./media/active-directory-saas-absorblms-tutorial/user.png)

    <span data-ttu-id="8cd0e-228">a.</span><span class="sxs-lookup"><span data-stu-id="8cd0e-228">a.</span></span> <span data-ttu-id="8cd0e-229">在 [名字] 文字方塊中輸入名字，例如 Britta。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-229">In the **First Name** textbox, type the first name like Britta.</span></span>

    <span data-ttu-id="8cd0e-230">b.</span><span class="sxs-lookup"><span data-stu-id="8cd0e-230">b.</span></span> <span data-ttu-id="8cd0e-231">在 [姓氏] 文字方塊中輸入姓氏，例如 Simon。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-231">In the **Last Name** textbox, type the last name like Simon.</span></span>
    
    <span data-ttu-id="8cd0e-232">c.</span><span class="sxs-lookup"><span data-stu-id="8cd0e-232">c.</span></span> <span data-ttu-id="8cd0e-233">在 [使用者名稱] 文字方塊中輸入使用者名稱，例如 Britta Simon。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-233">In the **Username** textbox, type the user name like Britta Simon.</span></span>

    <span data-ttu-id="8cd0e-234">d.</span><span class="sxs-lookup"><span data-stu-id="8cd0e-234">d.</span></span> <span data-ttu-id="8cd0e-235">在 [密碼] 文字方塊中，輸入 Britta Simon 的密碼。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-235">In the **Password** textbox, type the password of Britta Simon.</span></span>

    <span data-ttu-id="8cd0e-236">e.</span><span class="sxs-lookup"><span data-stu-id="8cd0e-236">e.</span></span> <span data-ttu-id="8cd0e-237">在 [確認密碼] 文字方塊中，輸入相同的密碼。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-237">In the **Confirm Password** textbox, type the same password.</span></span>
    
    <span data-ttu-id="8cd0e-238">f.</span><span class="sxs-lookup"><span data-stu-id="8cd0e-238">f.</span></span> <span data-ttu-id="8cd0e-239">使其 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-239">Make it as **ACTIVE**.</span></span>   

6. <span data-ttu-id="8cd0e-240">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-240">Click **"Save."**</span></span>
 
### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8cd0e-241">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8cd0e-241">Assign the Azure AD test user</span></span>

<span data-ttu-id="8cd0e-242">在本節中，您會將 Absorb LMS 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Absorb LMS.</span></span>

![指派使用者角色][200]

<span data-ttu-id="8cd0e-244">**若要將 Britta Simon 指派給 Absorb LMS，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="8cd0e-244">**To assign Britta Simon to Absorb LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="8cd0e-245">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="8cd0e-247">在應用程式清單中，選取 [Absorb LMS]。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-247">In the applications list, select **Absorb LMS**.</span></span>

    ![應用程式清單中的 Absorb LMS 連結](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. <span data-ttu-id="8cd0e-249">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-249">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202] 

4. <span data-ttu-id="8cd0e-251">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-251">Click **Add** button.</span></span> <span data-ttu-id="8cd0e-252">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="8cd0e-254">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8cd0e-255">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8cd0e-256">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8cd0e-257">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="8cd0e-257">Test single sign-on</span></span>

<span data-ttu-id="8cd0e-258">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8cd0e-259">在存取面板中按一下 [Absorb LMS] 圖格，系統就會自動將您登入 Absorb LMS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-259">Click the Absorb LMS tile in the Access Panel, you will get automatically signed-on to your Absorb LMS application.</span></span> <span data-ttu-id="8cd0e-260">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="8cd0e-260">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8cd0e-261">其他資源</span><span class="sxs-lookup"><span data-stu-id="8cd0e-261">Additional resources</span></span>

* [<span data-ttu-id="8cd0e-262">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="8cd0e-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8cd0e-263">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="8cd0e-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png


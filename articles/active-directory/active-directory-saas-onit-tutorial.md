---
title: "教學課程：Azure Active Directory 與 Onit 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Onit 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bc479a28-8fcd-493f-ac53-681975a5149c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 47c0055b89dbcf6a30a7f9ac5a33913e7bf463fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-onit"></a><span data-ttu-id="7cf29-103">教學課程：Azure Active Directory 與 Onit 整合</span><span class="sxs-lookup"><span data-stu-id="7cf29-103">Tutorial: Azure Active Directory integration with Onit</span></span>

<span data-ttu-id="7cf29-104">在本教學課程中，您將了解如何整合 Onit 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="7cf29-104">In this tutorial, you learn how to integrate Onit with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7cf29-105">Onit 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="7cf29-105">Integrating Onit with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7cf29-106">您可以在 Azure AD 中控制可存取 Onit 的人員。</span><span class="sxs-lookup"><span data-stu-id="7cf29-106">You can control in Azure AD who has access to Onit.</span></span>
- <span data-ttu-id="7cf29-107">您可以讓使用者透過其 Azure AD 帳戶自動登入 Onit (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="7cf29-107">You can enable your users to automatically get signed-on to Onit (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7cf29-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="7cf29-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="7cf29-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="7cf29-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cf29-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="7cf29-110">Prerequisites</span></span>

<span data-ttu-id="7cf29-111">若要設定 Azure AD 與 Onit 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="7cf29-111">To configure Azure AD integration with Onit, you need the following items:</span></span>

- <span data-ttu-id="7cf29-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7cf29-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7cf29-113">啟用 Onit 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7cf29-113">An Onit single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7cf29-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7cf29-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7cf29-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="7cf29-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7cf29-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7cf29-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7cf29-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="7cf29-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7cf29-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="7cf29-118">Scenario description</span></span>

<span data-ttu-id="7cf29-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7cf29-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7cf29-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="7cf29-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7cf29-121">從資源庫新增 Onit</span><span class="sxs-lookup"><span data-stu-id="7cf29-121">Adding Onit from the gallery</span></span>
2. <span data-ttu-id="7cf29-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7cf29-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-onit-from-the-gallery"></a><span data-ttu-id="7cf29-123">從資源庫新增 Onit</span><span class="sxs-lookup"><span data-stu-id="7cf29-123">Adding Onit from the gallery</span></span>
<span data-ttu-id="7cf29-124">若要設定將 Onit 整合到 Azure AD 中，您需要從資源庫將 Onit 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="7cf29-124">To configure the integration of Onit into Azure AD, you need to add Onit from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7cf29-125">**若要從資源庫新增 Onit，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7cf29-125">**To add Onit from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7cf29-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7cf29-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="7cf29-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7cf29-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7cf29-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7cf29-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="7cf29-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7cf29-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="7cf29-133">在搜尋方塊中，輸入 **Onit**，從結果面板中選取 [Onit]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="7cf29-133">In the search box, type **Onit**, select **Onit** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7cf29-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7cf29-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7cf29-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Onit 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7cf29-136">In this section, you configure and test Azure AD single sign-on with Onit based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7cf29-137">若要讓單一登入運作，Azure AD 必須知道 Onit 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="7cf29-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Onit is to a user in Azure AD.</span></span> <span data-ttu-id="7cf29-138">換句話說，必須在 Azure AD 使用者和 Onit 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7cf29-138">In other words, a link relationship between an Azure AD user and the related user in Onit needs to be established.</span></span>

<span data-ttu-id="7cf29-139">在 Onit 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7cf29-139">In Onit, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7cf29-140">若要設定及測試與 Onit 搭配運作的 Azure AD 單一登入，您需要完成下列建構元素：</span><span class="sxs-lookup"><span data-stu-id="7cf29-140">To configure and test Azure AD single sign-on with Onit, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7cf29-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="7cf29-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7cf29-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7cf29-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7cf29-143">**[建立 Onit 測試使用者](#create-an-onit-test-user)** - 使 Onit 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="7cf29-143">**[Create an Onit test user](#create-an-onit-test-user)** - to have a counterpart of Britta Simon in Onit that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7cf29-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7cf29-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7cf29-145">**[測試單一登入](#test-single-sign-on)**驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="7cf29-145">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7cf29-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7cf29-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7cf29-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Onit 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="7cf29-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Onit application.</span></span>

<span data-ttu-id="7cf29-148">**若要使用 Onit 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7cf29-148">**To configure Azure AD single sign-on with Onit, perform the following steps:**</span></span>

1. <span data-ttu-id="7cf29-149">在 Azure 入口網站的 [Onit] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="7cf29-149">In the Azure portal, on the **Onit** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="7cf29-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="7cf29-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-onit-tutorial/tutorial_onit_samlbase.png)

3. <span data-ttu-id="7cf29-153">在 [Onit 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7cf29-153">On the **Onit Domain and URLs** section, perform the following steps:</span></span>

    ![Onit 網域與 URL 單一登入資訊](./media/active-directory-saas-onit-tutorial/tutorial_onit_url.png)

    <span data-ttu-id="7cf29-155">a.</span><span class="sxs-lookup"><span data-stu-id="7cf29-155">a.</span></span> <span data-ttu-id="7cf29-156">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="7cf29-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub-domain>.onit.com`</span></span>

    <span data-ttu-id="7cf29-157">b.</span><span class="sxs-lookup"><span data-stu-id="7cf29-157">b.</span></span> <span data-ttu-id="7cf29-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="7cf29-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<sub-domain>.onit.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7cf29-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="7cf29-159">These values are not real.</span></span> <span data-ttu-id="7cf29-160">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="7cf29-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7cf29-161">請連絡 [Onit 用戶端支援小組](https://www.onit.com/support)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="7cf29-161">Contact [Onit Client support team](https://www.onit.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="7cf29-162">在 [SAML 簽署憑證] 區段上，複製憑證的 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="7cf29-162">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![憑證下載連結](./media/active-directory-saas-onit-tutorial/tutorial_onit_certificate.png) 

5. <span data-ttu-id="7cf29-164">Onit 應用程式需要特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="7cf29-164">Onit application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="7cf29-165">請設定此應用程式的下列宣告。</span><span class="sxs-lookup"><span data-stu-id="7cf29-165">Please configure the following claims for this application.</span></span> <span data-ttu-id="7cf29-166">您可以從應用程式的 [屬性]  索引標籤來管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="7cf29-166">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="7cf29-167">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="7cf29-167">The following screenshot shows an example for this.</span></span> 

    ![設定單一登入](./media/active-directory-saas-onit-tutorial/tutorial_onit_attribute.png) 

6. <span data-ttu-id="7cf29-169">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如圖所示設定 SAML 權杖屬性，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7cf29-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="7cf29-170">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="7cf29-170">Attribute Name</span></span> | <span data-ttu-id="7cf29-171">屬性值</span><span class="sxs-lookup"><span data-stu-id="7cf29-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="7cf29-172">電子郵件</span><span class="sxs-lookup"><span data-stu-id="7cf29-172">email</span></span> | <span data-ttu-id="7cf29-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="7cf29-173">user.mail</span></span> |
    
    <span data-ttu-id="7cf29-174">a.</span><span class="sxs-lookup"><span data-stu-id="7cf29-174">a.</span></span> <span data-ttu-id="7cf29-175">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7cf29-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-onit-tutorial/tutorial_attribute_04.png)

    ![設定單一登入](./media/active-directory-saas-onit-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="7cf29-178">b.</span><span class="sxs-lookup"><span data-stu-id="7cf29-178">b.</span></span> <span data-ttu-id="7cf29-179">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="7cf29-179">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="7cf29-180">c.</span><span class="sxs-lookup"><span data-stu-id="7cf29-180">c.</span></span> <span data-ttu-id="7cf29-181">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="7cf29-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="7cf29-182">d.</span><span class="sxs-lookup"><span data-stu-id="7cf29-182">d.</span></span> <span data-ttu-id="7cf29-183">讓 [命名空間] 保持空白。</span><span class="sxs-lookup"><span data-stu-id="7cf29-183">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="7cf29-184">e.</span><span class="sxs-lookup"><span data-stu-id="7cf29-184">e.</span></span> <span data-ttu-id="7cf29-185">按一下 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="7cf29-185">Click **Ok**.</span></span>

7. <span data-ttu-id="7cf29-186">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="7cf29-186">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-onit-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="7cf29-188">在 [Onit 設定] 區段上，按一下 [設定 Onit] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="7cf29-188">On the **Onit Configuration** section, click **Configure Onit** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7cf29-189">從 [快速參考] 區段中複製 [登出 URL] 和 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="7cf29-189">Copy the **Sign-Out URL, SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Onit 設定](./media/active-directory-saas-onit-tutorial/tutorial_onit_configure.png)

9. <span data-ttu-id="7cf29-191">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Onit 公司網站。</span><span class="sxs-lookup"><span data-stu-id="7cf29-191">In a different web browser window, log into your Onit company site as an administrator.</span></span>

10. <span data-ttu-id="7cf29-192">在頂端的功能表中，按一下 [系統管理] 。</span><span class="sxs-lookup"><span data-stu-id="7cf29-192">In the menu on the top, click **Administration**.</span></span>
   
   <span data-ttu-id="7cf29-193">![管理](./media/active-directory-saas-onit-tutorial/IC791174.png "管理")</span><span class="sxs-lookup"><span data-stu-id="7cf29-193">![Administration](./media/active-directory-saas-onit-tutorial/IC791174.png "Administration")</span></span>
11. <span data-ttu-id="7cf29-194">按一下 [編輯公司] 。</span><span class="sxs-lookup"><span data-stu-id="7cf29-194">Click **Edit Corporation**.</span></span>
   
   <span data-ttu-id="7cf29-195">![編輯公司](./media/active-directory-saas-onit-tutorial/IC791175.png "編輯公司")</span><span class="sxs-lookup"><span data-stu-id="7cf29-195">![Edit Corporation](./media/active-directory-saas-onit-tutorial/IC791175.png "Edit Corporation")</span></span>
   
12. <span data-ttu-id="7cf29-196">按一下 [安全性]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7cf29-196">Click the **Security** tab.</span></span>
    
    <span data-ttu-id="7cf29-197">![編輯公司資訊](./media/active-directory-saas-onit-tutorial/IC791176.png "編輯公司資訊")</span><span class="sxs-lookup"><span data-stu-id="7cf29-197">![Edit Company Information](./media/active-directory-saas-onit-tutorial/IC791176.png "Edit Company Information")</span></span>

13. <span data-ttu-id="7cf29-198">在 [安全性]  索引標籤上執行下列步驟：。</span><span class="sxs-lookup"><span data-stu-id="7cf29-198">On the **Security** tab, perform the following steps:</span></span>

    <span data-ttu-id="7cf29-199">![單一登入](./media/active-directory-saas-onit-tutorial/IC791177.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="7cf29-199">![Single Sign-On](./media/active-directory-saas-onit-tutorial/IC791177.png "Single Sign-On")</span></span>

    <span data-ttu-id="7cf29-200">a.</span><span class="sxs-lookup"><span data-stu-id="7cf29-200">a.</span></span> <span data-ttu-id="7cf29-201">對於**驗證策略**，請選取 [單一登入和密碼]。</span><span class="sxs-lookup"><span data-stu-id="7cf29-201">As **Authentication Strategy**, select **Single Sign On and Password**.</span></span>
    
    <span data-ttu-id="7cf29-202">b.</span><span class="sxs-lookup"><span data-stu-id="7cf29-202">b.</span></span> <span data-ttu-id="7cf29-203">在 [Idp 目標 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="7cf29-203">In **Idp Target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7cf29-204">c.</span><span class="sxs-lookup"><span data-stu-id="7cf29-204">c.</span></span> <span data-ttu-id="7cf29-205">在 [Idp 登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="7cf29-205">In **Idp logout URL** textbox, paste the value of  **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7cf29-206">d.</span><span class="sxs-lookup"><span data-stu-id="7cf29-206">d.</span></span> <span data-ttu-id="7cf29-207">在 [Idp 憑證指紋 (SHA1)] 文字方塊中，貼上您從 Azure 入口網站複製的憑證 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="7cf29-207">In **Idp Cert Fingerprint (SHA1)** textbox, paste the  **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="7cf29-208">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="7cf29-208">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7cf29-209">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="7cf29-209">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7cf29-210">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7cf29-210">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7cf29-211">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7cf29-211">Create an Azure AD test user</span></span>

<span data-ttu-id="7cf29-212">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="7cf29-212">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="7cf29-214">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7cf29-214">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7cf29-215">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7cf29-215">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-onit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7cf29-217">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="7cf29-217">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-onit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7cf29-219">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="7cf29-219">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-onit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7cf29-221">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7cf29-221">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-onit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7cf29-223">a.</span><span class="sxs-lookup"><span data-stu-id="7cf29-223">a.</span></span> <span data-ttu-id="7cf29-224">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="7cf29-224">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7cf29-225">b.</span><span class="sxs-lookup"><span data-stu-id="7cf29-225">b.</span></span> <span data-ttu-id="7cf29-226">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="7cf29-226">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="7cf29-227">c.</span><span class="sxs-lookup"><span data-stu-id="7cf29-227">c.</span></span> <span data-ttu-id="7cf29-228">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="7cf29-228">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="7cf29-229">d.</span><span class="sxs-lookup"><span data-stu-id="7cf29-229">d.</span></span> <span data-ttu-id="7cf29-230">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7cf29-230">Click **Create**.</span></span>
 
### <a name="create-an-onit-test-user"></a><span data-ttu-id="7cf29-231">建立 Onit 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7cf29-231">Create an Onit test user</span></span>

<span data-ttu-id="7cf29-232">為了讓 Azure AD 使用者能夠登入 Onit，必須將他們佈建到 Onit。</span><span class="sxs-lookup"><span data-stu-id="7cf29-232">In order to enable Azure AD users to log into Onit, they must be provisioned into Onit.</span></span>  

<span data-ttu-id="7cf29-233">在 Onit 的情況下，需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="7cf29-233">In the case of Onit, provisioning is a manual task.</span></span>

<span data-ttu-id="7cf29-234">**若要設定使用者佈建，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7cf29-234">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="7cf29-235">以系統管理員身分登入您的 **Onit** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="7cf29-235">Sign on to your **Onit** company site as an administrator.</span></span>
2. <span data-ttu-id="7cf29-236">按一下 [加入使用者] 。</span><span class="sxs-lookup"><span data-stu-id="7cf29-236">Click **Add User**.</span></span>
   
   <span data-ttu-id="7cf29-237">![管理](./media/active-directory-saas-onit-tutorial/IC791180.png "管理")</span><span class="sxs-lookup"><span data-stu-id="7cf29-237">![Administration](./media/active-directory-saas-onit-tutorial/IC791180.png "Administration")</span></span>
3. <span data-ttu-id="7cf29-238">在 [新增使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7cf29-238">On the **Add User** dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="7cf29-239">![新增使用者](./media/active-directory-saas-onit-tutorial/IC791181.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="7cf29-239">![Add User](./media/active-directory-saas-onit-tutorial/IC791181.png "Add User")</span></span>
   
  1. <span data-ttu-id="7cf29-240">在相關的文字方塊中，輸入您想要佈建之有效 Azure AD 帳戶的 [名稱] 與 [電子郵件地址]。</span><span class="sxs-lookup"><span data-stu-id="7cf29-240">Type the **Name** and the **Email Address** of a valid Azure AD account you want to provision into the related textboxes.</span></span>
  2. <span data-ttu-id="7cf29-241">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7cf29-241">Click **Create**.</span></span>    
   
 > [!NOTE]
 > <span data-ttu-id="7cf29-242">Azure Active Directory 帳戶的持有者會收到一封電子郵件，並依照連結在啟用其帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="7cf29-242">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7cf29-243">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7cf29-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="7cf29-244">在本節中，您會將 Onit 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7cf29-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Onit.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="7cf29-246">**若要將 Britta Simon 指派給 Onit，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7cf29-246">**To assign Britta Simon to Onit, perform the following steps:**</span></span>

1. <span data-ttu-id="7cf29-247">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7cf29-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="7cf29-249">在應用程式清單中，選取 [Onit]。</span><span class="sxs-lookup"><span data-stu-id="7cf29-249">In the applications list, select **Onit**.</span></span>

    ![應用程式清單中的 Onit 連結](./media/active-directory-saas-onit-tutorial/tutorial_onit_app.png)  

3. <span data-ttu-id="7cf29-251">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7cf29-251">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="7cf29-253">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7cf29-253">Click **Add** button.</span></span> <span data-ttu-id="7cf29-254">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7cf29-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="7cf29-256">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="7cf29-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7cf29-257">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7cf29-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7cf29-258">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7cf29-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7cf29-259">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="7cf29-259">Test single sign-on</span></span>

<span data-ttu-id="7cf29-260">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="7cf29-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7cf29-261">當您在「存取面板」中按一下 [Onit] 圖格時，應該會自動登入您的 Onit 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7cf29-261">When you click the Onit tile in the Access Panel, you should get automatically signed-on to your Onit application.</span></span>
<span data-ttu-id="7cf29-262">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="7cf29-262">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7cf29-263">其他資源</span><span class="sxs-lookup"><span data-stu-id="7cf29-263">Additional resources</span></span>

* [<span data-ttu-id="7cf29-264">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="7cf29-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7cf29-265">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7cf29-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-onit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-onit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-onit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-onit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-onit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-onit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-onit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-onit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-onit-tutorial/tutorial_general_203.png


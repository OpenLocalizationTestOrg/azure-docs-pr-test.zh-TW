---
title: "教學課程：Azure Active Directory 與 SAP Cloud for Customer 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 SAP Cloud for Customer 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: e4d945525a45704f34e1d9e742220928a516f341
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a><span data-ttu-id="42f34-103">教學課程：Azure Active Directory 與 SAP Cloud for Customer 整合</span><span class="sxs-lookup"><span data-stu-id="42f34-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span></span>

<span data-ttu-id="42f34-104">在本教學課程中，您會了解如何整合 SAP Cloud for Customer 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="42f34-104">In this tutorial, you learn how to integrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42f34-105">SAP Cloud for Customer 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="42f34-105">Integrating SAP Cloud for Customer with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="42f34-106">您可以在 Azure AD 中控制可存取 SAP Cloud for Customer 的人員</span><span class="sxs-lookup"><span data-stu-id="42f34-106">You can control in Azure AD who has access to SAP Cloud for Customer</span></span>
- <span data-ttu-id="42f34-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 SAP Cloud for Customer (單一登入)</span><span class="sxs-lookup"><span data-stu-id="42f34-107">You can enable your users to automatically get signed-on to SAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="42f34-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="42f34-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="42f34-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="42f34-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42f34-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="42f34-110">Prerequisites</span></span>

<span data-ttu-id="42f34-111">若要設定 Azure AD 與 SAP Cloud for Customer 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="42f34-111">To configure Azure AD integration with SAP Cloud for Customer, you need the following items:</span></span>

- <span data-ttu-id="42f34-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="42f34-112">An Azure AD subscription</span></span>
- <span data-ttu-id="42f34-113">啟用 SAP Cloud for Customer 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="42f34-113">A SAP Cloud for Customer single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42f34-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="42f34-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42f34-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="42f34-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42f34-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="42f34-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="42f34-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="42f34-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42f34-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="42f34-118">Scenario description</span></span>
<span data-ttu-id="42f34-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="42f34-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42f34-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="42f34-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42f34-121">從資源庫新增 SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="42f34-121">Adding SAP Cloud for Customer from the gallery</span></span>
2. <span data-ttu-id="42f34-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="42f34-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-cloud-for-customer-from-the-gallery"></a><span data-ttu-id="42f34-123">從資源庫新增 SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="42f34-123">Adding SAP Cloud for Customer from the gallery</span></span>
<span data-ttu-id="42f34-124">若要設定 SAP Cloud for Customer 與 Azure AD 整合，您需要從資源庫將 SAP Cloud for Customer 加入到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="42f34-124">To configure the integration of SAP Cloud for Customer into Azure AD, you need to add SAP Cloud for Customer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="42f34-125">**若要從資源庫加入 SAP Cloud for Customer，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="42f34-125">**To add SAP Cloud for Customer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="42f34-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="42f34-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="42f34-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="42f34-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="42f34-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="42f34-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="42f34-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="42f34-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="42f34-133">在搜尋方塊中輸入 **SAP Cloud for Customer**。</span><span class="sxs-lookup"><span data-stu-id="42f34-133">In the search box, type **SAP Cloud for Customer**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. <span data-ttu-id="42f34-135">在結果面板中，選取 [SAP Cloud for Customer]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="42f34-135">In the results panel, select **SAP Cloud for Customer**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="42f34-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="42f34-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="42f34-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SAP Cloud for Customer 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="42f34-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="42f34-139">若要讓單一登入運作，Azure AD 必須知道 SAP Cloud for Customer 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="42f34-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Cloud for Customer is to a user in Azure AD.</span></span> <span data-ttu-id="42f34-140">換句話說，必須在 Azure AD 使用者與 SAP Cloud for Customer 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="42f34-140">In other words, a link relationship between an Azure AD user and the related user in SAP Cloud for Customer needs to be established.</span></span>

<span data-ttu-id="42f34-141">在 SAP Cloud for Customer 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="42f34-141">In SAP Cloud for Customer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="42f34-142">若要使用 SAP Cloud for Customer 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="42f34-142">To configure and test Azure AD single sign-on with SAP Cloud for Customer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="42f34-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="42f34-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="42f34-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="42f34-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="42f34-145">**[建立 SAP Cloud for Customer 測試使用者](#creating-a-sap-cloud-for-customer-test-user)** - 使 SAP Cloud for Customer 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="42f34-145">**[Creating a SAP Cloud for Customer test user](#creating-a-sap-cloud-for-customer-test-user)** - to have a counterpart of Britta Simon in SAP Cloud for Customer that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="42f34-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="42f34-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="42f34-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="42f34-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="42f34-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="42f34-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="42f34-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 SAP Cloud for Customer 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="42f34-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Cloud for Customer application.</span></span>

<span data-ttu-id="42f34-150">**若要使用 SAP Cloud for Customer 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="42f34-150">**To configure Azure AD single sign-on with SAP Cloud for Customer, perform the following steps:**</span></span>

1. <span data-ttu-id="42f34-151">在 Azure 入口網站的 [SAP Cloud for Customer] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="42f34-151">In the Azure portal, on the **SAP Cloud for Customer** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="42f34-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="42f34-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. <span data-ttu-id="42f34-155">在 [SAP Cloud for Customer 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="42f34-155">On the **SAP Cloud for Customer Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    <span data-ttu-id="42f34-157">a.</span><span class="sxs-lookup"><span data-stu-id="42f34-157">a.</span></span> <span data-ttu-id="42f34-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="42f34-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    <span data-ttu-id="42f34-159">b.</span><span class="sxs-lookup"><span data-stu-id="42f34-159">b.</span></span> <span data-ttu-id="42f34-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="42f34-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="42f34-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="42f34-161">These values are not real.</span></span> <span data-ttu-id="42f34-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="42f34-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="42f34-163">請連絡 [SAP Cloud for Customer 支援小組](https://www.sap.com/about/agreements.sap-cloud-services-customers.html)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="42f34-163">Contact [SAP Cloud for Customer Client support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to get these values.</span></span> 

4. <span data-ttu-id="42f34-164">在 [使用者屬性] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="42f34-164">On the **User Attributes** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    <span data-ttu-id="42f34-166">a.</span><span class="sxs-lookup"><span data-stu-id="42f34-166">a.</span></span> <span data-ttu-id="42f34-167">在 [使用者識別碼] 清單中，選取 **ExtractMailPrefix()** 函式。</span><span class="sxs-lookup"><span data-stu-id="42f34-167">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span></span>

    <span data-ttu-id="42f34-168">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="42f34-168">b.</span></span> <span data-ttu-id="42f34-169">從 [郵件] 清單中，選取您想要用於實作的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="42f34-169">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span>
    <span data-ttu-id="42f34-170">例如，如果您想要使用 EmployeeID 為唯一的使用者識別碼，而且已在 ExtensionAttribute2 中儲存屬性值，則選取 [user.extensionattribute2]。</span><span class="sxs-lookup"><span data-stu-id="42f34-170">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span>  

5. <span data-ttu-id="42f34-171">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="42f34-171">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. <span data-ttu-id="42f34-173">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="42f34-173">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="42f34-175">在 [SAP Cloud for Customer 組態] 區段上，按一下 [設定 SAP Cloud for Customer] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="42f34-175">On the **SAP Cloud for Customer Configuration** section, click **Configure SAP Cloud for Customer** to open **Configure sign-on** window.</span></span> <span data-ttu-id="42f34-176">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="42f34-176">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. <span data-ttu-id="42f34-178">為了設定 SSO，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="42f34-178">To get SSO configured, perform the following steps:</span></span>
   
    <span data-ttu-id="42f34-179">a.</span><span class="sxs-lookup"><span data-stu-id="42f34-179">a.</span></span> <span data-ttu-id="42f34-180">使用系統管理員權限登入 SAP Cloud for Customer 入口網站。</span><span class="sxs-lookup"><span data-stu-id="42f34-180">Login into SAP Cloud for Customer portal with administrator rights.</span></span>
   
    <span data-ttu-id="42f34-181">b.</span><span class="sxs-lookup"><span data-stu-id="42f34-181">b.</span></span> <span data-ttu-id="42f34-182">瀏覽至 [應用程式和使用者管理常見工作]，然後按一下 [識別提供者] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="42f34-182">Navigate to the **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="42f34-183">c.</span><span class="sxs-lookup"><span data-stu-id="42f34-183">c.</span></span> <span data-ttu-id="42f34-184">按一下 [新增識別提供者]，然後選取您從 Azure 入口網站下載的中繼資料 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="42f34-184">Click **New Identity Provider** and select the metadata XML file you have downloaded from the Azure portal.</span></span> <span data-ttu-id="42f34-185">藉由匯入中繼資料，系統會自動上傳所需的簽章憑證和加密憑證。</span><span class="sxs-lookup"><span data-stu-id="42f34-185">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    <span data-ttu-id="42f34-187">d.</span><span class="sxs-lookup"><span data-stu-id="42f34-187">d.</span></span> <span data-ttu-id="42f34-188">Azure Active Directory 需要 SAML 要求中的「判斷提示取用者服務 URL」元素，因此請選取 [包括判斷提示取用者服務 URL] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="42f34-188">Azure Active Directory requires the element Assertion Consumer Service URL in the SAML request, so select the **Include Assertion Consumer Service URL** checkbox.</span></span>
   
    <span data-ttu-id="42f34-189">e.</span><span class="sxs-lookup"><span data-stu-id="42f34-189">e.</span></span> <span data-ttu-id="42f34-190">按一下 [啟用單一登入]。</span><span class="sxs-lookup"><span data-stu-id="42f34-190">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="42f34-191">f.</span><span class="sxs-lookup"><span data-stu-id="42f34-191">f.</span></span> <span data-ttu-id="42f34-192">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="42f34-192">Save your changes.</span></span>
   
    <span data-ttu-id="42f34-193">g.</span><span class="sxs-lookup"><span data-stu-id="42f34-193">g.</span></span> <span data-ttu-id="42f34-194">按一下 [我的系統] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="42f34-194">Click the **My System** tab.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    <span data-ttu-id="42f34-196">h.</span><span class="sxs-lookup"><span data-stu-id="42f34-196">h.</span></span> <span data-ttu-id="42f34-197">在 [Azure AD 登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 **SAML 單一登入服務 URL**。</span><span class="sxs-lookup"><span data-stu-id="42f34-197">In **Azure AD Sign On URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    <span data-ttu-id="42f34-199">i.</span><span class="sxs-lookup"><span data-stu-id="42f34-199">i.</span></span> <span data-ttu-id="42f34-200">透過選取 [手動選取識別提供者]，指定員工是否可以在以使用者識別碼和密碼登入或 SSO 之間進行手動選擇。</span><span class="sxs-lookup"><span data-stu-id="42f34-200">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting the **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="42f34-201">j.</span><span class="sxs-lookup"><span data-stu-id="42f34-201">j.</span></span> <span data-ttu-id="42f34-202">在 [SSO URL] 區段中，指定您的員工應用來登入系統的 URL。</span><span class="sxs-lookup"><span data-stu-id="42f34-202">In the **SSO URL** section, specify the URL that should be used by your employees to sign on to the system.</span></span> 
    <span data-ttu-id="42f34-203">在 [傳送給員工的 URL] 清單中，您可以在下列選項之間做選擇︰</span><span class="sxs-lookup"><span data-stu-id="42f34-203">In the **URL Sent to Employee** list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="42f34-204">**非 SSO URL**</span><span class="sxs-lookup"><span data-stu-id="42f34-204">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="42f34-205">系統只會傳送一般系統 URL 給員工。</span><span class="sxs-lookup"><span data-stu-id="42f34-205">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="42f34-206">員工無法使用 SSO 來登入，而是必須改為使用密碼或憑證。</span><span class="sxs-lookup"><span data-stu-id="42f34-206">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="42f34-207">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="42f34-207">**SSO URL**</span></span> 
   
    <span data-ttu-id="42f34-208">系統只會傳送 SSO URL 給員工。</span><span class="sxs-lookup"><span data-stu-id="42f34-208">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="42f34-209">員工可以使用 SSO 來登入。</span><span class="sxs-lookup"><span data-stu-id="42f34-209">The employee can log on using SSO.</span></span> <span data-ttu-id="42f34-210">驗證要求會透過 IdP 重新導向。</span><span class="sxs-lookup"><span data-stu-id="42f34-210">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="42f34-211">**自動選取**</span><span class="sxs-lookup"><span data-stu-id="42f34-211">**Automatic Selection**</span></span>
   
    <span data-ttu-id="42f34-212">如果未啟用 SSO，系統會傳送一般系統 URL 給員工。</span><span class="sxs-lookup"><span data-stu-id="42f34-212">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="42f34-213">如果已啟用 SSO，系統會檢查員工是否有密碼。</span><span class="sxs-lookup"><span data-stu-id="42f34-213">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="42f34-214">如果有密碼，便會將 SSO URL 和非 SSO URL 傳送給員工。</span><span class="sxs-lookup"><span data-stu-id="42f34-214">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="42f34-215">但如果員工沒有密碼，則只會傳送 SSO URL 給員工。</span><span class="sxs-lookup"><span data-stu-id="42f34-215">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="42f34-216">k.</span><span class="sxs-lookup"><span data-stu-id="42f34-216">k.</span></span> <span data-ttu-id="42f34-217">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="42f34-217">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="42f34-218">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="42f34-218">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="42f34-219">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="42f34-219">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="42f34-220">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="42f34-220">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="42f34-221">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="42f34-221">Creating an Azure AD test user</span></span>
<span data-ttu-id="42f34-222">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="42f34-222">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="42f34-224">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="42f34-224">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="42f34-225">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="42f34-225">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="42f34-227">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="42f34-227">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="42f34-229">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="42f34-229">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="42f34-231">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="42f34-231">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="42f34-233">a.</span><span class="sxs-lookup"><span data-stu-id="42f34-233">a.</span></span> <span data-ttu-id="42f34-234">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="42f34-234">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42f34-235">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="42f34-235">b.</span></span> <span data-ttu-id="42f34-236">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="42f34-236">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="42f34-237">c.</span><span class="sxs-lookup"><span data-stu-id="42f34-237">c.</span></span> <span data-ttu-id="42f34-238">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="42f34-238">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="42f34-239">d.</span><span class="sxs-lookup"><span data-stu-id="42f34-239">d.</span></span> <span data-ttu-id="42f34-240">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="42f34-240">Click **Create**.</span></span>
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a><span data-ttu-id="42f34-241">建立 SAP Cloud for Customer 測試使用者</span><span class="sxs-lookup"><span data-stu-id="42f34-241">Creating a SAP Cloud for Customer test user</span></span>

<span data-ttu-id="42f34-242">在本節中，您要在 SAP Cloud for Customer 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="42f34-242">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span></span> <span data-ttu-id="42f34-243">請與 [SAP Cloud for Customer 支援小組](https://www.sap.com/about/agreements.sap-cloud-services-customers.html)合作，在 SAP Cloud for Customer 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="42f34-243">Please work with [SAP Cloud for Customer support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to add the users in the SAP Cloud for Customer platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="42f34-244">請確定 NameID 值符合 SAP Cloud for Customer 平台中的使用者名稱欄位。</span><span class="sxs-lookup"><span data-stu-id="42f34-244">Please make sure that NameID value should match with the username field in the SAP Cloud for Customer platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="42f34-245">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="42f34-245">Assigning the Azure AD test user</span></span>

<span data-ttu-id="42f34-246">在本節中，您會將 SAP Cloud for Customer 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="42f34-246">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Cloud for Customer.</span></span>

![指派使用者][200] 

<span data-ttu-id="42f34-248">**若要將 Britta Simon 指派到 SAP Cloud for Customer，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="42f34-248">**To assign Britta Simon to SAP Cloud for Customer, perform the following steps:**</span></span>

1. <span data-ttu-id="42f34-249">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="42f34-249">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="42f34-251">在應用程式清單中，選取 [SAP Cloud for Customer] 。</span><span class="sxs-lookup"><span data-stu-id="42f34-251">In the applications list, select **SAP Cloud for Customer**.</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. <span data-ttu-id="42f34-253">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="42f34-253">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="42f34-255">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="42f34-255">Click **Add** button.</span></span> <span data-ttu-id="42f34-256">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="42f34-256">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="42f34-258">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="42f34-258">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="42f34-259">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="42f34-259">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="42f34-260">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="42f34-260">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="42f34-261">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="42f34-261">Testing single sign-on</span></span>

<span data-ttu-id="42f34-262">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="42f34-262">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="42f34-263">在存取面板中按一下 [SAP Cloud for Customer] 圖格，應該會自動登入您的 SAP Cloud for Customer 應用程式。</span><span class="sxs-lookup"><span data-stu-id="42f34-263">When you click the SAP Cloud for Customer tile in the Access Panel, you should get automatically signed-on to your SAP Cloud for Customer application.</span></span>
<span data-ttu-id="42f34-264">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="42f34-264">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="42f34-265">其他資源</span><span class="sxs-lookup"><span data-stu-id="42f34-265">Additional resources</span></span>

* [<span data-ttu-id="42f34-266">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="42f34-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42f34-267">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="42f34-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png


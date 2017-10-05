---
title: "教學課程：Azure Active Directory 與 SAP Business ByDesign 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 SAP Business ByDesign 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ab76a0ac1ef954efd3c66e6f565514b889ed9444
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="82703-103">教學課程：Azure Active Directory 與 SAP Business ByDesign 整合</span><span class="sxs-lookup"><span data-stu-id="82703-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="82703-104">在本教學課程中，您會了解如何整合 SAP Business ByDesign 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="82703-104">In this tutorial, you learn how to integrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="82703-105">SAP Business ByDesign 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="82703-105">Integrating SAP Business ByDesign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="82703-106">您可以在 Azure AD 中控制可存取 SAP Business ByDesign 的人員。</span><span class="sxs-lookup"><span data-stu-id="82703-106">You can control in Azure AD who has access to SAP Business ByDesign.</span></span>
- <span data-ttu-id="82703-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 SAP Business ByDesign (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="82703-107">You can enable your users to automatically get signed-on to SAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="82703-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="82703-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="82703-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="82703-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82703-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="82703-110">Prerequisites</span></span>

<span data-ttu-id="82703-111">若要設定 Azure AD 與 SAP Business ByDesign 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="82703-111">To configure Azure AD integration with SAP Business ByDesign, you need the following items:</span></span>

- <span data-ttu-id="82703-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="82703-112">An Azure AD subscription</span></span>
- <span data-ttu-id="82703-113">已啟用 SAP Business ByDesign 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="82703-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="82703-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="82703-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="82703-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="82703-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="82703-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="82703-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="82703-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="82703-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="82703-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="82703-118">Scenario description</span></span>
<span data-ttu-id="82703-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="82703-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="82703-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="82703-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="82703-121">從資源庫新增 SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="82703-121">Adding SAP Business ByDesign from the gallery</span></span>
2. <span data-ttu-id="82703-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="82703-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-the-gallery"></a><span data-ttu-id="82703-123">從資源庫新增 SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="82703-123">Adding SAP Business ByDesign from the gallery</span></span>
<span data-ttu-id="82703-124">若要設定 SAP Business ByDesign 與 Azure AD 整合，您需要從資源庫將 SAP Business ByDesign 加入到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="82703-124">To configure the integration of SAP Business ByDesign into Azure AD, you need to add SAP Business ByDesign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="82703-125">**若要從資源庫加入 SAP Business ByDesign，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="82703-125">**To add SAP Business ByDesign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="82703-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="82703-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="82703-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="82703-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="82703-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="82703-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="82703-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="82703-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="82703-133">在搜尋方塊中，輸入 **SAP Business ByDesign**，從結果面板中選取 [SAP Business ByDesign]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="82703-133">In the search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="82703-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="82703-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="82703-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SAP Business ByDesign 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="82703-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="82703-137">若要讓單一登入運作，Azure AD 必須知道 SAP Business ByDesign 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="82703-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Business ByDesign is to a user in Azure AD.</span></span> <span data-ttu-id="82703-138">換句話說，必須在 Azure AD 使用者與 SAP Business ByDesign 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="82703-138">In other words, a link relationship between an Azure AD user and the related user in SAP Business ByDesign needs to be established.</span></span>

<span data-ttu-id="82703-139">在 SAP Business ByDesign 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="82703-139">In SAP Business ByDesign, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="82703-140">若要設定及測試對 SAP Business ByDesign 的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="82703-140">To configure and test Azure AD single sign-on with SAP Business ByDesign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="82703-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="82703-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="82703-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="82703-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="82703-143">**[建立 SAP Business ByDesign 測試使用者](#create-an-sap-business-bydesign-test-user)** - 使 SAP Business ByDesign 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="82703-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - to have a counterpart of Britta Simon in SAP Business ByDesign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="82703-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="82703-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="82703-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="82703-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="82703-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="82703-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="82703-147">在本節中，您會於 Azure 入口網站啟用 Azure AD 單一登入，並在您的 SAP Business ByDesign 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="82703-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="82703-148">**若要使用 SAP Business ByDesign 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="82703-148">**To configure Azure AD single sign-on with SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="82703-149">在 Azure 入口網站的 [SAP Business ByDesign] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="82703-149">In the Azure portal, on the **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="82703-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="82703-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. <span data-ttu-id="82703-153">在 [SAP Business ByDesign 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="82703-153">On the **SAP Business ByDesign Domain and URLs** section, perform the following steps:</span></span>

    ![SAP Business ByDesign 網域及 URL 單一登入資訊](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="82703-155">a.</span><span class="sxs-lookup"><span data-stu-id="82703-155">a.</span></span> <span data-ttu-id="82703-156">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="82703-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="82703-157">b.</span><span class="sxs-lookup"><span data-stu-id="82703-157">b.</span></span> <span data-ttu-id="82703-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="82703-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="82703-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="82703-159">These values are not real.</span></span> <span data-ttu-id="82703-160">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="82703-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="82703-161">請連絡 [SAP Business ByDesign 用戶端支援小組](https://www.sap.com/products/cloud-analytics.support.html)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="82703-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to get these values.</span></span>

4. <span data-ttu-id="82703-162">在 [使用者屬性] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="82703-162">On the **User Attributes** section, perform the following steps:</span></span>

    ![[SAP Business ByDesign 屬性] 區段](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="82703-164">a.</span><span class="sxs-lookup"><span data-stu-id="82703-164">a.</span></span> <span data-ttu-id="82703-165">在 [使用者識別碼] 清單中，選取 **ExtractMailPrefix()** 函式。</span><span class="sxs-lookup"><span data-stu-id="82703-165">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="82703-166">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="82703-166">b.</span></span> <span data-ttu-id="82703-167">從 [郵件] 清單中，選取您想要用於實作的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="82703-167">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span> <span data-ttu-id="82703-168">例如，如果您想要使用 EmployeeID 為唯一的使用者識別碼，而且已在 ExtensionAttribute2 中儲存屬性值，則選取 [user.extensionattribute2]。</span><span class="sxs-lookup"><span data-stu-id="82703-168">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span>     

5. <span data-ttu-id="82703-169">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="82703-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. <span data-ttu-id="82703-171">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="82703-171">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="82703-173">在 [SAP Business ByDesign 設定] 區段中，按一下 [設定 SAP Business ByDesign] 可開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="82703-173">On the **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** to open **Configure sign-on** window.</span></span> <span data-ttu-id="82703-174">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="82703-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![SAP Business ByDesign 設定](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. <span data-ttu-id="82703-176">為了設定應用程式的 SSO，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="82703-176">To get SSO configured for your application, perform the following steps:</span></span>
   
    <span data-ttu-id="82703-177">a.</span><span class="sxs-lookup"><span data-stu-id="82703-177">a.</span></span> <span data-ttu-id="82703-178">使用系統管理員權限登入 SAP Business ByDesign 入口網站。</span><span class="sxs-lookup"><span data-stu-id="82703-178">Sign on to your SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="82703-179">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="82703-179">b.</span></span> <span data-ttu-id="82703-180">瀏覽至 [應用程式和使用者管理常見工作]，然後按一下 [識別提供者] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="82703-180">Navigate to **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="82703-181">c.</span><span class="sxs-lookup"><span data-stu-id="82703-181">c.</span></span> <span data-ttu-id="82703-182">按一下 [新增識別提供者]，然後選取您從 Azure 入口網站下載的中繼資料 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="82703-182">Click **New Identity Provider** and select the metadata XML file that you have downloaded from the Azure portal.</span></span> <span data-ttu-id="82703-183">藉由匯入中繼資料，系統會自動上傳所需的簽章憑證和加密憑證。</span><span class="sxs-lookup"><span data-stu-id="82703-183">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="82703-185">d.</span><span class="sxs-lookup"><span data-stu-id="82703-185">d.</span></span> <span data-ttu-id="82703-186">為了在 SAML 要求中包含**判斷提示取用者服務 URL**，請選取 [包含判斷提示取用者服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="82703-186">To include the **Assertion Consumer Service URL** into the SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="82703-187">e.</span><span class="sxs-lookup"><span data-stu-id="82703-187">e.</span></span> <span data-ttu-id="82703-188">按一下 [啟用單一登入]。</span><span class="sxs-lookup"><span data-stu-id="82703-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="82703-189">f.</span><span class="sxs-lookup"><span data-stu-id="82703-189">f.</span></span> <span data-ttu-id="82703-190">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="82703-190">Save your changes.</span></span>
   
    <span data-ttu-id="82703-191">g.</span><span class="sxs-lookup"><span data-stu-id="82703-191">g.</span></span> <span data-ttu-id="82703-192">按一下 [我的系統] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="82703-192">Click the **My System** tab.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="82703-194">h.</span><span class="sxs-lookup"><span data-stu-id="82703-194">h.</span></span> <span data-ttu-id="82703-195">將您從 Azure 入口網站複製的「SAML 單一登入服務 URL」貼到 [Azure AD 登入 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="82703-195">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal it into the **Azure AD Sign On URL** textbox.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="82703-197">i.</span><span class="sxs-lookup"><span data-stu-id="82703-197">i.</span></span> <span data-ttu-id="82703-198">透過選取 [手動選取識別提供者]，指定員工是否可以在以使用者識別碼和密碼登入或 SSO 之間進行手動選擇。</span><span class="sxs-lookup"><span data-stu-id="82703-198">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="82703-199">j.</span><span class="sxs-lookup"><span data-stu-id="82703-199">j.</span></span> <span data-ttu-id="82703-200">在 [SSO URL] 區段中，指定員工應用來登入系統的 URL。</span><span class="sxs-lookup"><span data-stu-id="82703-200">In the **SSO URL** section, specify the URL that should be used by the employee to logon to the system.</span></span> 
    <span data-ttu-id="82703-201">在 [傳送給員工的 URL] 下拉式清單中，您可以在下列選項之間做選擇︰</span><span class="sxs-lookup"><span data-stu-id="82703-201">In the URL Sent to Employee dropdown list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="82703-202">**非 SSO URL**</span><span class="sxs-lookup"><span data-stu-id="82703-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="82703-203">系統只會傳送一般系統 URL 給員工。</span><span class="sxs-lookup"><span data-stu-id="82703-203">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="82703-204">員工無法使用 SSO 來登入，而是必須改為使用密碼或憑證。</span><span class="sxs-lookup"><span data-stu-id="82703-204">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="82703-205">**SSO URL**</span><span class="sxs-lookup"><span data-stu-id="82703-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="82703-206">系統只會傳送 SSO URL 給員工。</span><span class="sxs-lookup"><span data-stu-id="82703-206">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="82703-207">員工可以使用 SSO 來登入。</span><span class="sxs-lookup"><span data-stu-id="82703-207">The employee can log on using SSO.</span></span> <span data-ttu-id="82703-208">驗證要求會透過 IdP 重新導向。</span><span class="sxs-lookup"><span data-stu-id="82703-208">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="82703-209">**自動選取**</span><span class="sxs-lookup"><span data-stu-id="82703-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="82703-210">如果未啟用 SSO，系統會傳送一般系統 URL 給員工。</span><span class="sxs-lookup"><span data-stu-id="82703-210">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="82703-211">如果已啟用 SSO，系統會檢查員工是否有密碼。</span><span class="sxs-lookup"><span data-stu-id="82703-211">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="82703-212">如果有密碼，便會將 SSO URL 和非 SSO URL 傳送給員工。</span><span class="sxs-lookup"><span data-stu-id="82703-212">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="82703-213">但如果員工沒有密碼，則只會傳送 SSO URL 給員工。</span><span class="sxs-lookup"><span data-stu-id="82703-213">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="82703-214">k.</span><span class="sxs-lookup"><span data-stu-id="82703-214">k.</span></span> <span data-ttu-id="82703-215">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="82703-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="82703-216">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="82703-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="82703-217">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="82703-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="82703-218">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="82703-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="82703-219">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="82703-219">Create an Azure AD test user</span></span>

<span data-ttu-id="82703-220">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="82703-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="82703-222">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="82703-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="82703-223">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="82703-223">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="82703-225">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="82703-225">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="82703-227">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="82703-227">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="82703-229">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="82703-229">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="82703-231">a.</span><span class="sxs-lookup"><span data-stu-id="82703-231">a.</span></span> <span data-ttu-id="82703-232">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="82703-232">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="82703-233">b.</span><span class="sxs-lookup"><span data-stu-id="82703-233">b.</span></span> <span data-ttu-id="82703-234">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="82703-234">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="82703-235">c.</span><span class="sxs-lookup"><span data-stu-id="82703-235">c.</span></span> <span data-ttu-id="82703-236">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="82703-236">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="82703-237">d.</span><span class="sxs-lookup"><span data-stu-id="82703-237">d.</span></span> <span data-ttu-id="82703-238">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="82703-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="82703-239">建立 SAP Business ByDesign 測試使用者</span><span class="sxs-lookup"><span data-stu-id="82703-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="82703-240">在本節中，您要在 SAP Business ByDesign 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="82703-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="82703-241">請與 [SAP Business ByDesign 用戶端支援小組](https://www.sap.com/products/cloud-analytics.support.html)合作，以在 SAP Business ByDesign 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="82703-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to add the users in the SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="82703-242">請確定 NameID 值符合 SAP Business ByDesign 平台中的使用者名稱欄位。</span><span class="sxs-lookup"><span data-stu-id="82703-242">Please make sure that NameID value should match with the username field in the SAP Business ByDesign platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="82703-243">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="82703-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="82703-244">在本節中，您會將 SAP Business ByDesign 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="82703-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Business ByDesign.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="82703-246">**若要將 Britta Simon 指派到 SAP Business ByDesign，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="82703-246">**To assign Britta Simon to SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="82703-247">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="82703-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="82703-249">在應用程式清單中，選取 [SAP Business ByDesign] 。</span><span class="sxs-lookup"><span data-stu-id="82703-249">In the applications list, select **SAP Business ByDesign**.</span></span>

    ![應用程式清單中的 SAP Business ByDesign 連結](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. <span data-ttu-id="82703-251">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="82703-251">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="82703-253">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="82703-253">Click **Add** button.</span></span> <span data-ttu-id="82703-254">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="82703-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="82703-256">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="82703-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="82703-257">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="82703-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="82703-258">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="82703-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="82703-259">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="82703-259">Test single sign-on</span></span>

<span data-ttu-id="82703-260">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="82703-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="82703-261">當您在存取面板中按一下 [SAP Business ByDesign ] 圖格時，應該會自動登入您的 SAP Business ByDesign 應用程式。</span><span class="sxs-lookup"><span data-stu-id="82703-261">When you click the SAP Business ByDesign tile in the Access Panel, you should get automatically signed-on to your SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="82703-262">其他資源</span><span class="sxs-lookup"><span data-stu-id="82703-262">Additional resources</span></span>

* [<span data-ttu-id="82703-263">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="82703-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="82703-264">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="82703-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png


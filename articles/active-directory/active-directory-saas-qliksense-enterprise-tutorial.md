---
title: "教學課程：Azure Active Directory 與 Qlik Sense Enterprise 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Qlik Sense Enterprise 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 4964634cd5aaf0dbb98c766f5e12700c4d118750
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a><span data-ttu-id="cbe96-103">教學課程：Azure Active Directory 與 Qlik Sense Enterprise 整合</span><span class="sxs-lookup"><span data-stu-id="cbe96-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span></span>

<span data-ttu-id="cbe96-104">在本教學課程中，您會了解如何整合 Qlik Sense Enterprise 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="cbe96-104">In this tutorial, you learn how to integrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cbe96-105">Qlik Sense Enterprise 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="cbe96-105">Integrating Qlik Sense Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cbe96-106">您可以在 Azure AD 中控制可存取 Qlik Sense Enterprise 的人員。</span><span class="sxs-lookup"><span data-stu-id="cbe96-106">You can control in Azure AD who has access to Qlik Sense Enterprise.</span></span>
- <span data-ttu-id="cbe96-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Qlik Sense Enterprise (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="cbe96-107">You can enable your users to automatically get signed-on to Qlik Sense Enterprise (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="cbe96-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="cbe96-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="cbe96-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="cbe96-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbe96-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="cbe96-110">Prerequisites</span></span>

<span data-ttu-id="cbe96-111">若要設定 Azure AD 與 Qlik Sense Enterprise 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="cbe96-111">To configure Azure AD integration with Qlik Sense Enterprise, you need the following items:</span></span>

- <span data-ttu-id="cbe96-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cbe96-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cbe96-113">已啟用 Qlik Sense Enterprise 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cbe96-113">A Qlik Sense Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cbe96-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="cbe96-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cbe96-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="cbe96-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cbe96-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="cbe96-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cbe96-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="cbe96-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cbe96-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="cbe96-118">Scenario description</span></span>
<span data-ttu-id="cbe96-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cbe96-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cbe96-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="cbe96-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cbe96-121">從資源庫新增 Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="cbe96-121">Adding Qlik Sense Enterprise from the gallery</span></span>
2. <span data-ttu-id="cbe96-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cbe96-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qlik-sense-enterprise-from-the-gallery"></a><span data-ttu-id="cbe96-123">從資源庫新增 Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="cbe96-123">Adding Qlik Sense Enterprise from the gallery</span></span>
<span data-ttu-id="cbe96-124">若要設定將 Qlik Sense Enterprise 整合到 Azure AD 中，您需要從資源庫將 Qlik Sense Enterprise 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="cbe96-124">To configure the integration of Qlik Sense Enterprise into Azure AD, you need to add Qlik Sense Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cbe96-125">**若要從資源庫新增 Qlik Sense Enterprise，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="cbe96-125">**To add Qlik Sense Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cbe96-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="cbe96-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="cbe96-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="cbe96-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cbe96-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="cbe96-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="cbe96-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbe96-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="cbe96-133">在搜尋方塊中，輸入 **Qlik Sense Enterprise**，從結果面板中選取 [Qlik Sense Enterprise]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbe96-133">In the search box, type **Qlik Sense Enterprise**, select **Qlik Sense Enterprise** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Qlik Sense Enterprise](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="cbe96-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cbe96-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="cbe96-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Qlik Sense Enterprise 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cbe96-136">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cbe96-137">若要讓單一登入運作，Azure AD 必須知道 Qlik Sense Enterprise 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="cbe96-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Qlik Sense Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="cbe96-138">換句話說，必須建立 Azure AD 使用者和 Qlik Sense Enterprise 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="cbe96-138">In other words, a link relationship between an Azure AD user and the related user in Qlik Sense Enterprise needs to be established.</span></span>

<span data-ttu-id="cbe96-139">在 Qlik Sense Enterprise 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="cbe96-139">In Qlik Sense Enterprise, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cbe96-140">若要設定及測試與 Qlik Sense Enterprise 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="cbe96-140">To configure and test Azure AD single sign-on with Qlik Sense Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cbe96-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="cbe96-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cbe96-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cbe96-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cbe96-143">**[建立 Qlik Sense Enterprise 測試使用者](#create-a-qlik-sense-enterprise-test-user)** - 使 Qlik Sense Enterprise 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="cbe96-143">**[Create a Qlik Sense Enterprise test user](#create-a-qlik-sense-enterprise-test-user)** - to have a counterpart of Britta Simon in Qlik Sense Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cbe96-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cbe96-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cbe96-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="cbe96-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="cbe96-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cbe96-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="cbe96-147">在本節中，您會於 Azure 入口網站啟用 Azure AD 單一登入，然後在您的 Qlik Sense Enterprise 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="cbe96-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Qlik Sense Enterprise application.</span></span>

<span data-ttu-id="cbe96-148">**若要使用 Qlik Sense Enterprise 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="cbe96-148">**To configure Azure AD single sign-on with Qlik Sense Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="cbe96-149">在 Azure 入口網站的 [Qlik Sense Enterprise] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="cbe96-149">In the Azure portal, on the **Qlik Sense Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="cbe96-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="cbe96-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. <span data-ttu-id="cbe96-153">在 [Qlik Sense Enterprise 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cbe96-153">On the **Qlik Sense Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![Qlik Sense Enterprise 網域與 URL 單一登入資訊](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    <span data-ttu-id="cbe96-155">a.</span><span class="sxs-lookup"><span data-stu-id="cbe96-155">a.</span></span> <span data-ttu-id="cbe96-156">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span><span class="sxs-lookup"><span data-stu-id="cbe96-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="cbe96-157">請注意此 URI 的尾端斜線。</span><span class="sxs-lookup"><span data-stu-id="cbe96-157">Note the trailing slash at the end of this URI.</span></span> <span data-ttu-id="cbe96-158">這是必要的。</span><span class="sxs-lookup"><span data-stu-id="cbe96-158">It is required.</span></span>
    
    <span data-ttu-id="cbe96-159">b.</span><span class="sxs-lookup"><span data-stu-id="cbe96-159">b.</span></span> <span data-ttu-id="cbe96-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="cbe96-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > <span data-ttu-id="cbe96-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="cbe96-161">These values are not real.</span></span> <span data-ttu-id="cbe96-162">請使用實際的「登入 URL」和「識別碼」來更新這些值 (本教學課程稍後會說明)，或連絡 [Qlik Sense Enterprise 用戶端支援小組](https://www.qlik.com/us/services/support)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="cbe96-162">Update these values with the actual Sign-On URL and Identifier, Which are explained later in this tutorial or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to get these values.</span></span> 

4. <span data-ttu-id="cbe96-163">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="cbe96-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. <span data-ttu-id="cbe96-165">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbe96-165">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cbe96-167">準備同盟中繼資料 XML 檔案，以便將該檔案上傳至 Qlik Sense 伺服器。</span><span class="sxs-lookup"><span data-stu-id="cbe96-167">Prepare the Federation Metadata XML file so that you can upload that to Qlik Sense server.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="cbe96-168">將 IdP 中繼資料上傳至 Qlik Sense 伺服器之前，必須先編輯此檔案才能移除資訊，以確保 Azure AD 與 Qlik Sense 伺服器之間的運作正常。</span><span class="sxs-lookup"><span data-stu-id="cbe96-168">Before uploading the IdP metadata to the Qlik Sense server, the file needs to be edited to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span></span>
    
    ![QlikSense][qs24]
   
    <span data-ttu-id="cbe96-170">a.</span><span class="sxs-lookup"><span data-stu-id="cbe96-170">a.</span></span> <span data-ttu-id="cbe96-171">在文字編輯器中開啟從 Azure 入口網站下載的 FederationMetaData.xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="cbe96-171">Open the FederationMetaData.xml file, which you have downloaded from Azure portal in a text editor.</span></span>
   
    <span data-ttu-id="cbe96-172">b.</span><span class="sxs-lookup"><span data-stu-id="cbe96-172">b.</span></span> <span data-ttu-id="cbe96-173">搜尋 **RoleDescriptor** 值。</span><span class="sxs-lookup"><span data-stu-id="cbe96-173">Search for the value **RoleDescriptor**.</span></span>  <span data-ttu-id="cbe96-174">共會有四個項目 (兩對開頭和結尾元素標籤)。</span><span class="sxs-lookup"><span data-stu-id="cbe96-174">There are four entries (two pairs of opening and closing element tags).</span></span>
   
    <span data-ttu-id="cbe96-175">c.</span><span class="sxs-lookup"><span data-stu-id="cbe96-175">c.</span></span> <span data-ttu-id="cbe96-176">從檔案中刪除 RoleDescriptor 標籤與其間的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="cbe96-176">Delete the RoleDescriptor tags and all information in between from the file.</span></span>
   
    <span data-ttu-id="cbe96-177">d.</span><span class="sxs-lookup"><span data-stu-id="cbe96-177">d.</span></span> <span data-ttu-id="cbe96-178">將此檔案存放在附近，以便稍後用於本文件。</span><span class="sxs-lookup"><span data-stu-id="cbe96-178">Save the file and keep it nearby for use later in this document.</span></span>

7. <span data-ttu-id="cbe96-179">以可建立虛擬 Proxy 組態的使用者身分，瀏覽至 Qlik Sense Qlik 管理主控台 (QMC)。</span><span class="sxs-lookup"><span data-stu-id="cbe96-179">Navigate to the Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span></span>

8. <span data-ttu-id="cbe96-180">在 QMC 中，按一下 [虛擬Proxy] 功能表項目。</span><span class="sxs-lookup"><span data-stu-id="cbe96-180">In the QMC, click on the **Virtual Proxies** menu item.</span></span>
   
    ![QlikSense][qs6] 

9. <span data-ttu-id="cbe96-182">按一下畫面底部的 [新建] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbe96-182">At the bottom of the screen, click the **Create new** button.</span></span>
   
    ![QlikSense][qs7]

10. <span data-ttu-id="cbe96-184">虛擬 Proxy 編輯畫面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="cbe96-184">The Virtual proxy edit screen appears.</span></span>  <span data-ttu-id="cbe96-185">畫面右邊的功能表會顯示組態選項。</span><span class="sxs-lookup"><span data-stu-id="cbe96-185">On the right side of the screen is a menu for making configuration options visible.</span></span>
   
    ![QlikSense][qs9]

11. <span data-ttu-id="cbe96-187">勾選 [識別] 功能表選項後，輸入 Azure 虛擬 Proxy 組態的識別資訊。</span><span class="sxs-lookup"><span data-stu-id="cbe96-187">With the Identification menu option checked, enter the identifying information for the Azure virtual proxy configuration.</span></span>
    
    ![QlikSense][qs8]  
    
    <span data-ttu-id="cbe96-189">a.</span><span class="sxs-lookup"><span data-stu-id="cbe96-189">a.</span></span> <span data-ttu-id="cbe96-190">[說明] 欄位是虛擬 Proxy 組態的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="cbe96-190">The **Description** field is a friendly name for the virtual proxy configuration.</span></span>  <span data-ttu-id="cbe96-191">輸入說明的值。</span><span class="sxs-lookup"><span data-stu-id="cbe96-191">Enter a value for a description.</span></span>
    
    <span data-ttu-id="cbe96-192">b.</span><span class="sxs-lookup"><span data-stu-id="cbe96-192">b.</span></span> <span data-ttu-id="cbe96-193">[前置詞] 欄位可識別虛擬 Proxy 端點，以便連接到採用 Azure AD 單一登入的 Qlik Sense。</span><span class="sxs-lookup"><span data-stu-id="cbe96-193">The **Prefix** field identifies the virtual proxy endpoint for connecting to Qlik Sense with Azure AD Single Sign-On.</span></span>  <span data-ttu-id="cbe96-194">輸入此虛擬 Proxy 的獨特前置詞名稱。</span><span class="sxs-lookup"><span data-stu-id="cbe96-194">Enter a unique prefix name for this virtual proxy.</span></span>
    
    <span data-ttu-id="cbe96-195">c.</span><span class="sxs-lookup"><span data-stu-id="cbe96-195">c.</span></span> <span data-ttu-id="cbe96-196">[工作階段閒置逾時 (分鐘)] 是指透過此虛擬 Proxy 連接的逾時值。</span><span class="sxs-lookup"><span data-stu-id="cbe96-196">**Session inactivity timeout (minutes)** is the timeout for connections through this virtual proxy.</span></span>
    
    <span data-ttu-id="cbe96-197">d.</span><span class="sxs-lookup"><span data-stu-id="cbe96-197">d.</span></span> <span data-ttu-id="cbe96-198">[工作階段 cookie 標頭名稱] 是 cookie 名稱，用於儲存使用者在成功驗證後收到的 Qlik Sense 工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="cbe96-198">The **Session cookie header name** is the cookie name storing the session identifier for the Qlik Sense session a user receives after successful authentication.</span></span>  <span data-ttu-id="cbe96-199">此名稱必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="cbe96-199">This name must be unique.</span></span>

12. <span data-ttu-id="cbe96-200">按一下 [驗證] 功能表選項，讓它立即可見。</span><span class="sxs-lookup"><span data-stu-id="cbe96-200">Click on the Authentication menu option to make it visible.</span></span>  <span data-ttu-id="cbe96-201">[驗證] 畫面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="cbe96-201">The Authentication screen appears.</span></span>
    
    ![QlikSense][qs10]
    
    <span data-ttu-id="cbe96-203">a.</span><span class="sxs-lookup"><span data-stu-id="cbe96-203">a.</span></span> <span data-ttu-id="cbe96-204">[匿名存取模式] 下拉式清單可讓您決定匿名使用者是否可透過虛擬 Proxy 存取 Qlik Sense。</span><span class="sxs-lookup"><span data-stu-id="cbe96-204">The **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through the virtual proxy.</span></span>  <span data-ttu-id="cbe96-205">預設選項是 [沒有匿名使用者]。</span><span class="sxs-lookup"><span data-stu-id="cbe96-205">The default option is No anonymous user.</span></span>
    
    <span data-ttu-id="cbe96-206">b.</span><span class="sxs-lookup"><span data-stu-id="cbe96-206">b.</span></span> <span data-ttu-id="cbe96-207">[驗證方法] 下拉式清單可讓您決定虛擬 Proxy 將使用的驗證配置。</span><span class="sxs-lookup"><span data-stu-id="cbe96-207">The **Authentication method** drop-down determines the authentication scheme the virtual proxy will use.</span></span>  <span data-ttu-id="cbe96-208">從下拉式清單選取 [SAML]。</span><span class="sxs-lookup"><span data-stu-id="cbe96-208">Select SAML from the drop-down list.</span></span>  <span data-ttu-id="cbe96-209">此時會顯示更多選項。</span><span class="sxs-lookup"><span data-stu-id="cbe96-209">More options appear as a result.</span></span>
    
    <span data-ttu-id="cbe96-210">c.</span><span class="sxs-lookup"><span data-stu-id="cbe96-210">c.</span></span> <span data-ttu-id="cbe96-211">在 [SAML 主機 URI] 欄位中，輸入使用者必須輸入才可透過此 SAML 虛擬 Proxy 存取 Qlik Sense 的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="cbe96-211">In the **SAML host URI field**, input the hostname users enter to access Qlik Sense through this SAML virtual proxy.</span></span>  <span data-ttu-id="cbe96-212">主機名稱是 Qlik Sense 伺服器的 URI。</span><span class="sxs-lookup"><span data-stu-id="cbe96-212">The hostname is the uri of the Qlik Sense server.</span></span>
    
    <span data-ttu-id="cbe96-213">d.</span><span class="sxs-lookup"><span data-stu-id="cbe96-213">d.</span></span> <span data-ttu-id="cbe96-214">在 [SAML 實體識別碼] 中，輸入與 [SAML 主機 URI] 欄位相同的值。</span><span class="sxs-lookup"><span data-stu-id="cbe96-214">In the **SAML entity ID**, enter the same value entered for the SAML host URI field.</span></span>
    
    <span data-ttu-id="cbe96-215">e.</span><span class="sxs-lookup"><span data-stu-id="cbe96-215">e.</span></span> <span data-ttu-id="cbe96-216">[SAML IdP 中繼資料] 是稍早在 [從 Azure AD 組態編輯同盟中繼資料] 區段中編輯的檔案。</span><span class="sxs-lookup"><span data-stu-id="cbe96-216">The **SAML IdP metadata** is the file edited earlier in the **Edit Federation Metadata from Azure AD Configuration** section.</span></span>  <span data-ttu-id="cbe96-217">**上傳 IdP 中繼資料之前，必須先編輯此檔案**才能移除資訊，以確保 Azure AD 與 Qlik Sense 伺服器之間的運作正常。</span><span class="sxs-lookup"><span data-stu-id="cbe96-217">**Before uploading the IdP metadata, the file needs to be edited** to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span></span>  <span data-ttu-id="cbe96-218">**如果檔案尚未進行編輯，請參閱上述指示。**</span><span class="sxs-lookup"><span data-stu-id="cbe96-218">**Please refer to the instructions above if the file has yet to be edited.**</span></span>  <span data-ttu-id="cbe96-219">如果檔案已經過編輯，請按一下 [瀏覽] 按鈕，然後選取已編輯的中繼資料檔案，將它上傳至虛擬 Proxy 組態。</span><span class="sxs-lookup"><span data-stu-id="cbe96-219">If the file has been edited click on the Browse button and select the edited metadata file to upload it to the virtual proxy configuration.</span></span>
    
    <span data-ttu-id="cbe96-220">f.</span><span class="sxs-lookup"><span data-stu-id="cbe96-220">f.</span></span> <span data-ttu-id="cbe96-221">輸入 SAML 屬性的屬性名稱或結構描述參考，代表 Azure AD 將傳送至 Qlik Sense 伺服器的 **UserID**。</span><span class="sxs-lookup"><span data-stu-id="cbe96-221">Enter the attribute name or schema reference for the SAML attribute representing the **UserID** Azure AD sends to the Qlik Sense server.</span></span>  <span data-ttu-id="cbe96-222">在設定後的 Azure 應用程式畫面中可取得結構描述參考資訊。</span><span class="sxs-lookup"><span data-stu-id="cbe96-222">Schema reference information is available in the Azure app screens post configuration.</span></span>  <span data-ttu-id="cbe96-223">若要使用名稱屬性，請輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`。</span><span class="sxs-lookup"><span data-stu-id="cbe96-223">To use the name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="cbe96-224">g.</span><span class="sxs-lookup"><span data-stu-id="cbe96-224">g.</span></span> <span data-ttu-id="cbe96-225">輸入**使用者目錄**的值，此值會在使用者透過 Azure AD 向 Qlik Sense 伺服器進行驗證時附加至使用者。</span><span class="sxs-lookup"><span data-stu-id="cbe96-225">Enter the value for the **user directory** that will be attached to users when they authenticate to Qlik Sense server through Azure AD.</span></span>  <span data-ttu-id="cbe96-226">硬式編碼值必須以**方括號 []** 括住。</span><span class="sxs-lookup"><span data-stu-id="cbe96-226">Hardcoded values must be surrounded by **square brackets []**.</span></span>  <span data-ttu-id="cbe96-227">若要使用 Azure AD SAML 判斷提示中傳送的屬性，請在此文字方塊中輸入屬性名稱 (**不需**方括號)。</span><span class="sxs-lookup"><span data-stu-id="cbe96-227">To use an attribute sent in the Azure AD SAML assertion, enter the name of the attribute in this text box **without** square brackets.</span></span>
    
    <span data-ttu-id="cbe96-228">h.</span><span class="sxs-lookup"><span data-stu-id="cbe96-228">h.</span></span> <span data-ttu-id="cbe96-229">[SAML 簽章演算法] 可設定虛擬 Proxy 組態的服務提供者 (在此例中是 Qlik Sense 伺服器) 憑證簽署。</span><span class="sxs-lookup"><span data-stu-id="cbe96-229">The **SAML signing algorithm** sets the service provider (in this case Qlik Sense server) certificate signing for the virtual proxy configuration.</span></span>  <span data-ttu-id="cbe96-230">如果 Qlik Sense 伺服器使用透過 Microsoft Enhanced RSA 和 AES 密碼編譯提供者產生的受信任憑證，請將 SAML 簽署演算法變更為 **SHA-256**。</span><span class="sxs-lookup"><span data-stu-id="cbe96-230">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change the SAML signing algorithm to **SHA-256**.</span></span>
    
    <span data-ttu-id="cbe96-231">i.</span><span class="sxs-lookup"><span data-stu-id="cbe96-231">i.</span></span> <span data-ttu-id="cbe96-232">[SAML 屬性對應] 區段可讓其他屬性 (如群組) 傳送到 Qlik Sense，以便用於安全性規則。</span><span class="sxs-lookup"><span data-stu-id="cbe96-232">The SAML attribute mapping section allows for additional attributes like groups to be sent to Qlik Sense for use in security rules.</span></span>

13. <span data-ttu-id="cbe96-233">按一下 [負載平衡] 功能表選項，讓它立即可見。</span><span class="sxs-lookup"><span data-stu-id="cbe96-233">Click on the **LOAD BALANCING** menu option to make it visible.</span></span>  <span data-ttu-id="cbe96-234">[負載平衡] 畫面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="cbe96-234">The Load Balancing screen appears.</span></span>
    
    ![QlikSense][qs11]

14. <span data-ttu-id="cbe96-236">按一下 [新增伺服器節點] 按鈕，選取 Qlik Sense 為了達到負載平衡而會將工作階段傳送至的引擎節點，然後按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbe96-236">Click on the **Add new server node** button, select engine node or nodes Qlik Sense will send sessions to for load balancing purposes, and click the **Add** button.</span></span>
    
    ![QlikSense][qs12]

15. <span data-ttu-id="cbe96-238">按一下 [進階] 功能表選項，讓它立即可見。</span><span class="sxs-lookup"><span data-stu-id="cbe96-238">Click on the Advanced menu option to make it visible.</span></span> <span data-ttu-id="cbe96-239">[進階] 畫面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="cbe96-239">The Advanced screen appears.</span></span>
    
    ![QlikSense][qs13]
    
    <span data-ttu-id="cbe96-241">[主機允許清單] 會識別在連接到 Qlik Sense 伺服器時所接受的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="cbe96-241">The Host white list identifies hostnames that are accepted when connecting to the Qlik Sense server.</span></span>  <span data-ttu-id="cbe96-242">**輸入連接到 Qlik Sense 伺服器時使用者會指定的主機名稱。**</span><span class="sxs-lookup"><span data-stu-id="cbe96-242">**Enter the hostname users will specify when connecting to Qlik Sense server.**</span></span> <span data-ttu-id="cbe96-243">主機名稱是與 SAML 主機 uri 相同的值 (不含 https://)。</span><span class="sxs-lookup"><span data-stu-id="cbe96-243">The hostname is the same value as the SAML host uri without the https://.</span></span>

16. <span data-ttu-id="cbe96-244">按一下 [套用] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbe96-244">Click the **Apply** button.</span></span>
    
    ![QlikSense][qs14]

17. <span data-ttu-id="cbe96-246">按一下 [確定] 以接受警告訊息，該訊息指出將重新啟動連結至虛擬 Proxy 的 Proxy。</span><span class="sxs-lookup"><span data-stu-id="cbe96-246">Click OK to accept the warning message that states proxies linked to the virtual proxy will be restarted.</span></span>
    
    ![QlikSense][qs15]

18. <span data-ttu-id="cbe96-248">畫面右側會出現 [相關聯的項目] 功能表。</span><span class="sxs-lookup"><span data-stu-id="cbe96-248">On the right side of the screen, the Associated items menu appears.</span></span>  <span data-ttu-id="cbe96-249">按一下 [Proxy] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="cbe96-249">Click on the **Proxies** menu option.</span></span>
    
    ![QlikSense][qs16]

19. <span data-ttu-id="cbe96-251">Proxy 畫面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="cbe96-251">The proxy screen appears.</span></span>  <span data-ttu-id="cbe96-252">按一下底部的 [連結] 按鈕，將 Proxy 連結到虛擬 Proxy。</span><span class="sxs-lookup"><span data-stu-id="cbe96-252">Click the **Link** button at the bottom to link a proxy to the virtual proxy.</span></span>
    
    ![QlikSense][qs17]

20. <span data-ttu-id="cbe96-254">選取將會支援此虛擬 Proxy 連線的 Proxy 節點，然後按一下 [連結] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbe96-254">Select the proxy node that will support this virtual proxy connection and click the **Link** button.</span></span>  <span data-ttu-id="cbe96-255">連結之後，Proxy 會列在相關聯的 Proxy 之下。</span><span class="sxs-lookup"><span data-stu-id="cbe96-255">After linking, the proxy will be listed under associated proxies.</span></span>
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. <span data-ttu-id="cbe96-258">大約五到十秒後，[重新整理 QMC] 訊息會出現。</span><span class="sxs-lookup"><span data-stu-id="cbe96-258">After about five to ten seconds, the Refresh QMC message will appear.</span></span>  <span data-ttu-id="cbe96-259">按一下 [重新整理 QMC] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbe96-259">Click the **Refresh QMC** button.</span></span>
    
    ![QlikSense][qs20]

22. <span data-ttu-id="cbe96-261">當 QMC 重新整理時，按一下 [虛擬 Proxy]  功能表項目。</span><span class="sxs-lookup"><span data-stu-id="cbe96-261">When the QMC refreshes, click on the **Virtual proxies** menu item.</span></span> <span data-ttu-id="cbe96-262">新的 SAML 虛擬 Proxy 項目會列在螢幕上的表格中。</span><span class="sxs-lookup"><span data-stu-id="cbe96-262">The new SAML virtual proxy entry is listed in the table on the screen.</span></span>  <span data-ttu-id="cbe96-263">按一下此虛擬 Proxy 項目。</span><span class="sxs-lookup"><span data-stu-id="cbe96-263">Single click on the virtual proxy entry.</span></span>
    
    ![QlikSense][qs51]

23. <span data-ttu-id="cbe96-265">畫面底部的 [下載 SP 中繼資料] 按鈕將會啟用。</span><span class="sxs-lookup"><span data-stu-id="cbe96-265">At the bottom of the screen, the Download SP metadata button will activate.</span></span>  <span data-ttu-id="cbe96-266">按一下 [下載 SP 中繼資料] 按鈕，將中繼資料儲存至檔案。</span><span class="sxs-lookup"><span data-stu-id="cbe96-266">Click the **Download SP metadata** button to save the metadata to a file.</span></span>
    
    ![QlikSense][qs52]

24. <span data-ttu-id="cbe96-268">開啟 SP 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="cbe96-268">Open the sp metadata file.</span></span>  <span data-ttu-id="cbe96-269">觀察 **entityID** 項目和 **AssertionConsumerService** 項目。</span><span class="sxs-lookup"><span data-stu-id="cbe96-269">Observe the **entityID** entry and the **AssertionConsumerService** entry.</span></span>  <span data-ttu-id="cbe96-270">這些值相當於 Azure AD 應用程式組態中的 [識別碼] 和 [登入 URL]。</span><span class="sxs-lookup"><span data-stu-id="cbe96-270">These values are equivalent to the **Identifier** and the **Sign on URL** in the Azure AD application configuration.</span></span> <span data-ttu-id="cbe96-271">如果這些值不相符，請將其貼在 Azure AD 應用程式組態中的 [Qlik Sense Enterprise 網域與 URL] 區段，然後您應該在 Azure AD App 組態精靈中取代這些值。</span><span class="sxs-lookup"><span data-stu-id="cbe96-271">Paste these values in the **Qlik Sense Enterprise Domain and URLs** section in the Azure AD application configuration if they are not matching, then you should replace them in the Azure AD App configuration wizard.</span></span>
    
    ![QlikSense][qs53]

> [!TIP]
> <span data-ttu-id="cbe96-273">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="cbe96-273">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cbe96-274">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="cbe96-274">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cbe96-275">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cbe96-275">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="cbe96-276">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cbe96-276">Create an Azure AD test user</span></span>
<span data-ttu-id="cbe96-277">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="cbe96-277">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 測試使用者][100]

<span data-ttu-id="cbe96-279">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="cbe96-279">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cbe96-280">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbe96-280">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

   ![Azure Active Directory 按鈕](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="cbe96-282">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="cbe96-282">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

   ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="cbe96-284">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cbe96-284">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

   ![[新增] 按鈕](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="cbe96-286">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cbe96-286">In the **User** dialog box, perform the following steps:</span></span>

   ![[使用者] 對話方塊](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   <span data-ttu-id="cbe96-288">a.</span><span class="sxs-lookup"><span data-stu-id="cbe96-288">a.</span></span> <span data-ttu-id="cbe96-289">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="cbe96-289">In the **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="cbe96-290">b.</span><span class="sxs-lookup"><span data-stu-id="cbe96-290">b.</span></span> <span data-ttu-id="cbe96-291">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="cbe96-291">In the **User name** box, type the email address of user Britta Simon.</span></span>

   <span data-ttu-id="cbe96-292">c.</span><span class="sxs-lookup"><span data-stu-id="cbe96-292">c.</span></span> <span data-ttu-id="cbe96-293">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="cbe96-293">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

   <span data-ttu-id="cbe96-294">d.</span><span class="sxs-lookup"><span data-stu-id="cbe96-294">d.</span></span> <span data-ttu-id="cbe96-295">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="cbe96-295">Click **Create**.</span></span>
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a><span data-ttu-id="cbe96-296">建立 Qlik Sense Enterprise 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cbe96-296">Create a Qlik Sense Enterprise test user</span></span>

<span data-ttu-id="cbe96-297">在本節中，您要在 Qlik Sense Enterprise 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="cbe96-297">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span></span> <span data-ttu-id="cbe96-298">請與 [Qlik Sense Enterprise 用戶端支援小組](https://www.qlik.com/us/services/support)合作，以在 Qlik Sense Enterprise 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="cbe96-298">Work with [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to add the users in the Qlik Sense Enterprise platform.</span></span> <span data-ttu-id="cbe96-299">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="cbe96-299">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="cbe96-300">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cbe96-300">Assign the Azure AD test user</span></span>

<span data-ttu-id="cbe96-301">在本節中，您會將 Qlik Sense Enterprise 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cbe96-301">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Qlik Sense Enterprise.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="cbe96-303">**若要將 Britta Simon 指派給 Qlik Sense Enterprise，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="cbe96-303">**To assign Britta Simon to Qlik Sense Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="cbe96-304">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="cbe96-304">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="cbe96-306">在應用程式清單中，選取 [Qlik Sense Enterprise] 。</span><span class="sxs-lookup"><span data-stu-id="cbe96-306">In the applications list, select **Qlik Sense Enterprise**.</span></span>

    ![應用程式清單中的 Qlik Sense Enterprise 連結](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. <span data-ttu-id="cbe96-308">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="cbe96-308">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="cbe96-310">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbe96-310">Click **Add** button.</span></span> <span data-ttu-id="cbe96-311">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="cbe96-311">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="cbe96-313">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="cbe96-313">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cbe96-314">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbe96-314">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cbe96-315">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbe96-315">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="cbe96-316">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="cbe96-316">Test single sign-on</span></span>

<span data-ttu-id="cbe96-317">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="cbe96-317">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cbe96-318">當您在存取面板中按一下 [Qlik Sense Enterprise] 圖格時，應該會自動登入您的 Qlik Sense Enterprise 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbe96-318">When you click the Qlik Sense Enterprise tile in the Access Panel, you should get automatically signed-on to your Qlik Sense Enterprise application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cbe96-319">其他資源</span><span class="sxs-lookup"><span data-stu-id="cbe96-319">Additional resources</span></span>

* [<span data-ttu-id="cbe96-320">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="cbe96-320">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cbe96-321">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="cbe96-321">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png


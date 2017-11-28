---
title: "教學課程：Azure Active Directory 與 Five9 Plus Adapter 整合 (CTI，Contact Center Agents) | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Five9 Plus Adapter (CTI，Contact Center Agents) 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: d75163ea5eb3fa811e07861f06e6c4d5c758b898
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a><span data-ttu-id="6abac-103">教學課程：Azure Active Directory 與 Five9 Plus Adapter 整合 (CTI，Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="6abac-103">Tutorial: Azure Active Directory integration with Five9 Plus Adapter (CTI, Contact Center Agents)</span></span>

<span data-ttu-id="6abac-104">在本教學課程中，您將了解如何整合 Five9 Plus Adapter (CTI，Contact Center Agents) 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="6abac-104">In this tutorial, you learn how to integrate Five9 Plus Adapter (CTI, Contact Center Agents) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6abac-105">Five9 Plus Adapter (CTI，Contact Center Agents) 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="6abac-105">Integrating Five9 Plus Adapter (CTI, Contact Center Agents) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6abac-106">您可以在 Azure AD 中控制可存取 Five9 Plus Adapter (CTI，Contact Center Agents) 的人員</span><span class="sxs-lookup"><span data-stu-id="6abac-106">You can control in Azure AD who has access to Five9 Plus Adapter (CTI, Contact Center Agents)</span></span>
- <span data-ttu-id="6abac-107">您可以讓使用者使用其 Azure AD 帳戶自動登入 Five9 Plus Adapter (CTI，Contact Center Agents) (單一登入)</span><span class="sxs-lookup"><span data-stu-id="6abac-107">You can enable your users to automatically get signed-on to Five9 Plus Adapter (CTI, Contact Center Agents) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6abac-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="6abac-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6abac-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="6abac-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6abac-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6abac-110">Prerequisites</span></span>

<span data-ttu-id="6abac-111">若要設定 Azure AD 與 Five9 Plus Adapter (CTI，Contact Center Agents) 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="6abac-111">To configure Azure AD integration with Five9 Plus Adapter (CTI, Contact Center Agents), you need the following items:</span></span>

- <span data-ttu-id="6abac-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6abac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6abac-113">已啟用 Five9 Plus Adapter (CTI，Contact Center Agents) 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6abac-113">A Five9 Plus Adapter (CTI, Contact Center Agents) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6abac-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6abac-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6abac-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="6abac-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6abac-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6abac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6abac-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="6abac-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6abac-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="6abac-118">Scenario description</span></span>
<span data-ttu-id="6abac-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6abac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6abac-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="6abac-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6abac-121">從資源庫新增 Five9 Plus Adapter (CTI，Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="6abac-121">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery</span></span>
2. <span data-ttu-id="6abac-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6abac-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-the-gallery"></a><span data-ttu-id="6abac-123">從資源庫新增 Five9 Plus Adapter (CTI，Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="6abac-123">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery</span></span>
<span data-ttu-id="6abac-124">若要設定將 Five9 Plus Adapter (CTI，Contact Center Agents) 整合到 Azure AD 中，您需要從資源庫將 Five9 Plus Adapter (CTI，Contact Center Agents) 新增到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="6abac-124">To configure the integration of Five9 Plus Adapter (CTI, Contact Center Agents) into Azure AD, you need to add Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6abac-125">**若要從資源庫新增 Five9 Plus Adapter (CTI，Contact Center Agents)，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6abac-125">**To add Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6abac-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="6abac-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6abac-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6abac-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6abac-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6abac-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="6abac-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6abac-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="6abac-133">在搜尋方塊中，輸入 **Five9 Plus Adapter (CTI, Contact Center Agents)**。</span><span class="sxs-lookup"><span data-stu-id="6abac-133">In the search box, type **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-five9-tutorial/tutorial_five9_search.png)

5. <span data-ttu-id="6abac-135">在結果窗格中，選取 [\Five9 Plus Adapter (CTI，Contact Center Agents)\]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="6abac-135">In the results panel, select **Five9 Plus Adapter (CTI, Contact Center Agents)**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6abac-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6abac-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6abac-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Five9 Plus Adapter (CTI，Contact Center Agents) 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6abac-138">In this section, you configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6abac-139">若要讓單一登入運作，Azure AD 必須知道 Five9 Plus Adapter (CTI，Contact Center Agents) 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="6abac-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Five9 Plus Adapter (CTI, Contact Center Agents) is to a user in Azure AD.</span></span> <span data-ttu-id="6abac-140">換句話說，必須在 Azure AD 使用者和 Five9 Plus Adapter (CTI，Contact Center Agents) 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6abac-140">In other words, a link relationship between an Azure AD user and the related user in Five9 Plus Adapter (CTI, Contact Center Agents) needs to be established.</span></span>

<span data-ttu-id="6abac-141">在 Five9 Plus Adapter (CTI，Contact Center Agents) 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6abac-141">In Five9 Plus Adapter (CTI, Contact Center Agents), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6abac-142">若要設定及測試與 Five9 Plus Adapter (CTI，Contact Center Agents) 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="6abac-142">To configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6abac-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="6abac-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6abac-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6abac-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6abac-145">**[建立 Five9 Plus Adapter (CTI，Contact Center Agents) 測試使用者](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)** - 在 Five9 Plus Adapter (CTI，Contact Center Agents) 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="6abac-145">**[Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)** - to have a counterpart of Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6abac-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6abac-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6abac-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="6abac-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6abac-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6abac-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6abac-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Five9 Plus Adapter (CTI，Contact Center Agents) 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="6abac-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>

<span data-ttu-id="6abac-150">**若要設定 Azure AD 與 Five9 Plus Adapter (CTI，Contact Center Agents) 的整合，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6abac-150">**To configure Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), perform the following steps:**</span></span>

1. <span data-ttu-id="6abac-151">在 Azure 入口網站的 [\Five9 Plus Adapter (CTI，Contact Center Agents)\] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="6abac-151">In the Azure portal, on the **Five9 Plus Adapter (CTI, Contact Center Agents)** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="6abac-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="6abac-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-five9-tutorial/tutorial_five9_samlbase.png)

3. <span data-ttu-id="6abac-155">在 [Five9 Plus Adapter (CTI，Contact Center Agents) 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6abac-155">On the **Five9 Plus Adapter (CTI, Contact Center Agents) Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-five9-tutorial/tutorial_five9_url.png)
    
    <span data-ttu-id="6abac-157">a.</span><span class="sxs-lookup"><span data-stu-id="6abac-157">a.</span></span> <span data-ttu-id="6abac-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="6abac-158">In the **Identifier** textbox, type a URL using the following patterns:</span></span>

    |    <span data-ttu-id="6abac-159">環境</span><span class="sxs-lookup"><span data-stu-id="6abac-159">Environment</span></span>      |       <span data-ttu-id="6abac-160">URL</span><span class="sxs-lookup"><span data-stu-id="6abac-160">URL</span></span>      |
    | :-- | :-- |
    | <span data-ttu-id="6abac-161">針對「Five9 Plus Adapter for Microsoft Dynamics CRM」</span><span class="sxs-lookup"><span data-stu-id="6abac-161">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | <span data-ttu-id="6abac-162">針對「Five9 Plus Adapter for Zendesk」</span><span class="sxs-lookup"><span data-stu-id="6abac-162">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | <span data-ttu-id="6abac-163">針對「Five9 Plus Adapter for Agent Desktop Toolkit」</span><span class="sxs-lookup"><span data-stu-id="6abac-163">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    <span data-ttu-id="6abac-164">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6abac-164">b.</span></span> <span data-ttu-id="6abac-165">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="6abac-165">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>

    |      <span data-ttu-id="6abac-166">環境</span><span class="sxs-lookup"><span data-stu-id="6abac-166">Environment</span></span>     |      <span data-ttu-id="6abac-167">URL</span><span class="sxs-lookup"><span data-stu-id="6abac-167">URL</span></span>      |
    | :--                  | :--           |
    | <span data-ttu-id="6abac-168">針對「Five9 Plus Adapter for Microsoft Dynamics CRM」</span><span class="sxs-lookup"><span data-stu-id="6abac-168">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | <span data-ttu-id="6abac-169">針對「Five9 Plus Adapter for Zendesk」</span><span class="sxs-lookup"><span data-stu-id="6abac-169">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | <span data-ttu-id="6abac-170">針對「Five9 Plus Adapter for Agent Desktop Toolkit」</span><span class="sxs-lookup"><span data-stu-id="6abac-170">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

4. <span data-ttu-id="6abac-171">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="6abac-171">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-five9-tutorial/tutorial_five9_certificate.png) 

5. <span data-ttu-id="6abac-173">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6abac-173">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-five9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6abac-175">在 [\Five9 Plus Adapter (CTI，Contact Center Agents) 設定] 區段中，按一下 [設定 Five9 Plus Adapter (CTI，Contact Center Agents)\] 可開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="6abac-175">On the **Five9 Plus Adapter (CTI, Contact Center Agents) Configuration** section, click **Configure Five9 Plus Adapter (CTI, Contact Center Agents)** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6abac-176">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="6abac-176">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-five9-tutorial/tutorial_five9_configure.png) 

7. <span data-ttu-id="6abac-178">若要在 **Five9 Plus Adapter (CTI，Contact Center Agents)** 端設定單一登入，您必須將已下載的 [憑證]\(Base64)\、[登出 URL]、[SAML 實體識別碼] 及 [SAML 單一登入服務 URL] 傳送給 [Five9 Plus Adapter (CTI，Contact Center Agents) 支援小組](https://www.five9.com/about/contact)。</span><span class="sxs-lookup"><span data-stu-id="6abac-178">To configure single sign-on on **Five9 Plus Adapter (CTI, Contact Center Agents)** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact).</span></span> <span data-ttu-id="6abac-179">此外，若要進一步設定 SSO，請遵循下列根據配接器的步驟：</span><span class="sxs-lookup"><span data-stu-id="6abac-179">Also additionally, for configuring SSO further please follow the below steps according to the adapter:</span></span>

    <span data-ttu-id="6abac-180">a.</span><span class="sxs-lookup"><span data-stu-id="6abac-180">a.</span></span> <span data-ttu-id="6abac-181">「Five9 Plus Adapter for Agent Desktop Toolkit」系統管理指南：[http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="6abac-181">“Five9 Plus Adapter for Agent Desktop Toolkit” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="6abac-182">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6abac-182">b.</span></span> <span data-ttu-id="6abac-183">「Five9 Plus Adapter for Microsoft Dynamics CRM」系統管理指南：[http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="6abac-183">“Five9 Plus Adapter for Microsoft Dynamics CRM” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="6abac-184">c.</span><span class="sxs-lookup"><span data-stu-id="6abac-184">c.</span></span> <span data-ttu-id="6abac-185">「Five9 Plus Adapter for Zendesk」系統管理指南：[http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="6abac-185">“Five9 Plus Adapter for Zendesk” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span></span>


> [!TIP]
> <span data-ttu-id="6abac-186">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="6abac-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6abac-187">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="6abac-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6abac-188">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6abac-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6abac-189">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6abac-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="6abac-190">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="6abac-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="6abac-192">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6abac-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6abac-193">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="6abac-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-five9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6abac-195">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="6abac-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-five9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6abac-197">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="6abac-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-five9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6abac-199">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6abac-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-five9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6abac-201">a.</span><span class="sxs-lookup"><span data-stu-id="6abac-201">a.</span></span> <span data-ttu-id="6abac-202">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="6abac-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6abac-203">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6abac-203">b.</span></span> <span data-ttu-id="6abac-204">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="6abac-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6abac-205">c.</span><span class="sxs-lookup"><span data-stu-id="6abac-205">c.</span></span> <span data-ttu-id="6abac-206">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="6abac-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6abac-207">d.</span><span class="sxs-lookup"><span data-stu-id="6abac-207">d.</span></span> <span data-ttu-id="6abac-208">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6abac-208">Click **Create**.</span></span>
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a><span data-ttu-id="6abac-209">建立 Five9 Plus Adapter (CTI，Contact Center Agents) 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6abac-209">Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user</span></span>

<span data-ttu-id="6abac-210">在本節中，您會在 Five9 Plus Adapter (CTI，Contact Center Agents) 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="6abac-210">In this section, you create a user called Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents).</span></span> <span data-ttu-id="6abac-211">請與 [Five9 Plus Adapter (CTI，Contact Center Agents) 支援小組](https://www.five9.com/about/contact)合作，在 Five9 Plus Adapter (CTI，Contact Center Agents) 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="6abac-211">Work with [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact) to add the users in the Five9 Plus Adapter (CTI, Contact Center Agents) platform.</span></span> <span data-ttu-id="6abac-212">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="6abac-212">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6abac-213">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6abac-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6abac-214">在本節中，您會將 Five9 Plus Adapter (CTI，Contact Center Agents) 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6abac-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Five9 Plus Adapter (CTI, Contact Center Agents).</span></span>

![指派使用者][200] 

<span data-ttu-id="6abac-216">**若要將 Britta Simon 指派給 Five9 Plus Adapter (CTI，Contact Center Agents)，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6abac-216">**To assign Britta Simon to Five9 Plus Adapter (CTI, Contact Center Agents), perform the following steps:**</span></span>

1. <span data-ttu-id="6abac-217">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6abac-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="6abac-219">在應用程式清單中，選取 [\Five9 Plus Adapter (CTI，Contact Center Agents)\]。</span><span class="sxs-lookup"><span data-stu-id="6abac-219">In the applications list, select **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![設定單一登入](./media/active-directory-saas-five9-tutorial/tutorial_five9_app.png) 

3. <span data-ttu-id="6abac-221">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6abac-221">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="6abac-223">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6abac-223">Click **Add** button.</span></span> <span data-ttu-id="6abac-224">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6abac-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="6abac-226">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="6abac-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6abac-227">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6abac-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6abac-228">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6abac-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6abac-229">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="6abac-229">Testing single sign-on</span></span>

<span data-ttu-id="6abac-230">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="6abac-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6abac-231">當您在「存取面板」中按一下 [\Five9 Plus Adapter (CTI，Contact Center Agents)\] 圖格時，應該會自動登入您的 Five9 Plus Adapter (CTI，Contact Center Agents) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6abac-231">When you click the Five9 Plus Adapter (CTI, Contact Center Agents) tile in the Access Panel, you should get automatically signed-on to your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>
<span data-ttu-id="6abac-232">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="6abac-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6abac-233">其他資源</span><span class="sxs-lookup"><span data-stu-id="6abac-233">Additional resources</span></span>

* [<span data-ttu-id="6abac-234">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="6abac-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6abac-235">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="6abac-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-five9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-five9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-five9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-five9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-five9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-five9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-five9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-five9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-five9-tutorial/tutorial_general_203.png


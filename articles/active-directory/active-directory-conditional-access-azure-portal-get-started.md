---
title: "開始使用 Azure Active Directory 中的條件式存取 | Microsoft Docs"
description: "使用位置條件測試條件式存取。"
services: active-directory
keywords: "應用程式的條件式存取, Azure AD 條件式存取, 安全存取公司資源, 條件式存取原則"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: cd53e8be32d1e98aaf9f72177895871dba69df86
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a><span data-ttu-id="1fbeb-104">開始使用 Azure Active Directory 中的條件式存取</span><span class="sxs-lookup"><span data-stu-id="1fbeb-104">Get started with conditional access in Azure Active Directory</span></span>

<span data-ttu-id="1fbeb-105">條件式存取是 Azure Active Directory 的功能，可讓您定義獲得授權的使用者可以存取您的應用程式的條件。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-105">Conditional access is a capability of Azure Active Directory that enables you to define conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="1fbeb-106">本主題根據您環境中的位置條件，為您提供測試條件式存取的指示。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-106">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="1fbeb-107">案例描述</span><span class="sxs-lookup"><span data-stu-id="1fbeb-107">Scenario description</span></span>

<span data-ttu-id="1fbeb-108">許多組織有一個共同需求：只需要 Multi-Factor Authentication，即可存取不是從公司內部網路執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-108">One common requirement in many organizations is to only require multi-factor authentication for access to apps that is not performed from the corporate intranet.</span></span> <span data-ttu-id="1fbeb-109">使用 Azure Active Directory 設定以位置為基礎的條件式存取原則，即可輕鬆地完成此目標。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-109">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="1fbeb-110">本主題提供設定相關原則的詳細指示。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-110">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="1fbeb-111">原則會利用[信任的 IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) 來區別從公司內部網路與所有其他位置進行的存取嘗試。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-111">The policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) to distinguish between access attempts made from the corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="1fbeb-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="1fbeb-112">Prerequisites</span></span>

<span data-ttu-id="1fbeb-113">本主題中概述的案例假設您熟悉 [Azure Active Directory 條件式存取](active-directory-conditional-access-azure-portal.md)中所述的概念。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-113">The scenario outlined in this topic assumes that you are familiar with the concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="1fbeb-114">若要測試此案例，您必須：</span><span class="sxs-lookup"><span data-stu-id="1fbeb-114">To test this scenario, you need to:</span></span>

- <span data-ttu-id="1fbeb-115">建立測試使用者</span><span class="sxs-lookup"><span data-stu-id="1fbeb-115">Create a test user</span></span> 

- <span data-ttu-id="1fbeb-116">將 Azure AD Premium 授權指派給測試使用者</span><span class="sxs-lookup"><span data-stu-id="1fbeb-116">Assign an Azure AD Premium license to the test user</span></span>

- <span data-ttu-id="1fbeb-117">設定受管理的應用程式，並將您的測試使用者指派給它</span><span class="sxs-lookup"><span data-stu-id="1fbeb-117">Configure a managed app and assign your test user to it</span></span>

- <span data-ttu-id="1fbeb-118">設定信任的 IP</span><span class="sxs-lookup"><span data-stu-id="1fbeb-118">Configure trusted IPs</span></span>

<span data-ttu-id="1fbeb-119">如果您需要更多有關信任 IP 的詳細資訊，請參閱[信任的 IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips)。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-119">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="1fbeb-120">原則設定步驟</span><span class="sxs-lookup"><span data-stu-id="1fbeb-120">Policy configuration steps</span></span>

<span data-ttu-id="1fbeb-121">**若要設定條件式存取原則，請執行：**</span><span class="sxs-lookup"><span data-stu-id="1fbeb-121">**To configure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="1fbeb-122">在 Azure 入口網站的左側導覽列上，按一下 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-122">In the Azure portal, on the left navbar, click **Azure Active Directory**.</span></span> 

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="1fbeb-124">在 [Azure Active Directory] 刀鋒視窗的 [管理] 區段中，按一下 [條件式存取]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-124">On the **Azure Active Directory** blade, in the **Manage** section, click **Conditional access**.</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="1fbeb-126">在 [條件式存取] 刀鋒視窗上，若要開啟 [新增] 刀鋒視窗，請在頂端的工具列中按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-126">On the **Conditional Access** blade, to open the **New** blade, in the toolbar on the top, click **Add**.</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="1fbeb-128">在 [新增] 刀鋒視窗的 [名稱] 文字方塊中，輸入您的原則名稱。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-128">On the **New** blade, in the **Name** textbox, type a name for your policy.</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="1fbeb-130">在 [指派] 區段中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-130">In the **Assignment** section, click **Users and groups**.</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="1fbeb-132">在 [使用者和群組] 刀鋒視窗上，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="1fbeb-132">On the **Users and groups** blade, perform the following steps:</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="1fbeb-134">a.</span><span class="sxs-lookup"><span data-stu-id="1fbeb-134">a.</span></span> <span data-ttu-id="1fbeb-135">按一下 [選取使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-135">Click **Select users and groups**.</span></span>

    <span data-ttu-id="1fbeb-136">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-136">b.</span></span> <span data-ttu-id="1fbeb-137">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-137">Click **Select**.</span></span>

    <span data-ttu-id="1fbeb-138">c.</span><span class="sxs-lookup"><span data-stu-id="1fbeb-138">c.</span></span> <span data-ttu-id="1fbeb-139">在 [選取] 刀鋒視窗上，選取您的測試使用者，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-139">On the **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="1fbeb-140">d.</span><span class="sxs-lookup"><span data-stu-id="1fbeb-140">d.</span></span> <span data-ttu-id="1fbeb-141">在 [使用者和群組] 刀鋒視窗上，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-141">On the **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="1fbeb-142">在 [新增] 刀鋒視窗上，若要開啟 [雲端應用程式] 刀鋒視窗，請在 [指派] 區段中，按一下 [雲端應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-142">On the **New** blade, to open the **Cloud apps** blade, in the **Assignment** section, click **Cloud apps**.</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="1fbeb-144">在 [雲端應用程式] 刀鋒視窗上，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="1fbeb-144">On the **Cloud apps** blade, perform the following steps:</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="1fbeb-146">a.</span><span class="sxs-lookup"><span data-stu-id="1fbeb-146">a.</span></span> <span data-ttu-id="1fbeb-147">按一下 [選取應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-147">Click **Select apps**.</span></span>

    <span data-ttu-id="1fbeb-148">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-148">b.</span></span> <span data-ttu-id="1fbeb-149">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-149">Click **Select**.</span></span>

    <span data-ttu-id="1fbeb-150">c.</span><span class="sxs-lookup"><span data-stu-id="1fbeb-150">c.</span></span> <span data-ttu-id="1fbeb-151">在 [選取] 刀鋒視窗上，選取您的雲端應用程式，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-151">On the **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="1fbeb-152">d.</span><span class="sxs-lookup"><span data-stu-id="1fbeb-152">d.</span></span> <span data-ttu-id="1fbeb-153">在 [雲端應用程式] 刀鋒視窗上，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-153">On the **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="1fbeb-154">在 [新增] 刀鋒視窗上，若要開啟 [條件] 刀鋒視窗，請在 [指派] 區段中，按一下 [條件]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-154">On the **New** blade, to open the **Conditions** blade, in the **Assignment** section, click **Conditions**.</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="1fbeb-156">在 [條件] 刀鋒視窗上，若要開啟 [位置] 刀鋒視窗，請按一下 [位置]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-156">On the **Conditions** blade, to open the **Locations** blade, click **Locations**.</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="1fbeb-158">在 [位置] 刀鋒視窗上，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="1fbeb-158">On the **Locations** blade, perform the following steps:</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="1fbeb-160">a.</span><span class="sxs-lookup"><span data-stu-id="1fbeb-160">a.</span></span> <span data-ttu-id="1fbeb-161">在 [設定] 之下，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-161">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="1fbeb-162">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-162">b.</span></span> <span data-ttu-id="1fbeb-163">在 [包含] 之下，按一下 [所有位置]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-163">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="1fbeb-164">c.</span><span class="sxs-lookup"><span data-stu-id="1fbeb-164">c.</span></span> <span data-ttu-id="1fbeb-165">按一下 [排除]，然後按一下 [所有信任的 IP]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-165">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="1fbeb-167">d.</span><span class="sxs-lookup"><span data-stu-id="1fbeb-167">d.</span></span> <span data-ttu-id="1fbeb-168">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-168">Click **Done**.</span></span>

12. <span data-ttu-id="1fbeb-169">在 [條件] 刀鋒視窗上，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-169">On the **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="1fbeb-170">在 [新增] 刀鋒視窗上，若要開啟 [授與] 刀鋒視窗，請在 [控制] 區段中，按一下 [授與]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-170">On the **New** blade, to open the **Grant** blade, in the **Controls** section, click **Grant**.</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="1fbeb-172">在 [授與] 刀鋒視窗上，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="1fbeb-172">On the **Grant** blade, perform the following steps:</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="1fbeb-174">a.</span><span class="sxs-lookup"><span data-stu-id="1fbeb-174">a.</span></span> <span data-ttu-id="1fbeb-175">選取 [需要 Multi-Factor Authentication]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-175">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="1fbeb-176">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-176">b.</span></span> <span data-ttu-id="1fbeb-177">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-177">Click **Select**.</span></span>

15. <span data-ttu-id="1fbeb-178">在 [新增] 刀鋒視窗的 [啟用原則] 之下，按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-178">On the **New** blade, under **Enable policy**, click **On**.</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="1fbeb-180">在 [新增] 刀鋒視窗上，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-180">On the **New** blade, click **Create**.</span></span>


## <a name="testing-the-policy"></a><span data-ttu-id="1fbeb-181">測試原則</span><span class="sxs-lookup"><span data-stu-id="1fbeb-181">Testing the policy</span></span>

<span data-ttu-id="1fbeb-182">若要測試您的原則，您應該從以下裝置存取您的應用程式︰</span><span class="sxs-lookup"><span data-stu-id="1fbeb-182">To test your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="1fbeb-183">具有在您設定的信任 IP 內的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="1fbeb-183">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="1fbeb-184">具有不在您設定的信任 IP 內的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="1fbeb-184">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="1fbeb-185">只有從不在您設定的信任 IP 內的裝置嘗試連線時，才需要 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-185">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="1fbeb-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1fbeb-186">Next steps</span></span>

<span data-ttu-id="1fbeb-187">如果您想要深入了解條件式存取，請參閱 [Azure Active Directory 條件式存取](active-directory-conditional-access-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="1fbeb-187">If you would like to learn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>


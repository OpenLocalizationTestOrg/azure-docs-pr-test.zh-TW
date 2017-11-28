---
title: "開始使用 Azure Active Directory 中的條件式存取的 aaaGet |Microsoft 文件"
description: "使用位置條件測試條件式存取。"
services: active-directory
keywords: "條件式存取 tooapps，Azure AD 中，使用條件式存取保護存取 toocompany 資源，條件式存取原則"
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
ms.openlocfilehash: 4521f5a34f5882e026f5e58a7127d8c55cba2f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a><span data-ttu-id="e3a1d-104">開始使用 Azure Active Directory 中的條件式存取</span><span class="sxs-lookup"><span data-stu-id="e3a1d-104">Get started with conditional access in Azure Active Directory</span></span>

<span data-ttu-id="e3a1d-105">條件式存取是 Azure Active directory，可讓您 toodefine 條件下獲得授權的使用者可以存取您的應用程式的功能。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-105">Conditional access is a capability of Azure Active Directory that enables you toodefine conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="e3a1d-106">本主題根據您環境中的位置條件，為您提供測試條件式存取的指示。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-106">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="e3a1d-107">案例描述</span><span class="sxs-lookup"><span data-stu-id="e3a1d-107">Scenario description</span></span>

<span data-ttu-id="e3a1d-108">在許多組織中的一項常見需求是 tooonly 不會執行從 hello 公司內部網路的存取 tooapps 需要多重要素驗證。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-108">One common requirement in many organizations is tooonly require multi-factor authentication for access tooapps that is not performed from hello corporate intranet.</span></span> <span data-ttu-id="e3a1d-109">使用 Azure Active Directory 設定以位置為基礎的條件式存取原則，即可輕鬆地完成此目標。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-109">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="e3a1d-110">本主題提供設定相關原則的詳細指示。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-110">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="e3a1d-111">hello 原則利用[信任的 Ip](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish 源自 hello 公司的存取嘗試之間的內部網路和所有其他位置。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-111">hello policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish between access attempts made from hello corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e3a1d-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="e3a1d-112">Prerequisites</span></span>

<span data-ttu-id="e3a1d-113">hello 本主題中所述的案例假設您已熟悉中所述的 hello 概念[Azure Active Directory 條件式存取](active-directory-conditional-access-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-113">hello scenario outlined in this topic assumes that you are familiar with hello concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="e3a1d-114">tootest 此案例中，您需要：</span><span class="sxs-lookup"><span data-stu-id="e3a1d-114">tootest this scenario, you need to:</span></span>

- <span data-ttu-id="e3a1d-115">建立測試使用者</span><span class="sxs-lookup"><span data-stu-id="e3a1d-115">Create a test user</span></span> 

- <span data-ttu-id="e3a1d-116">指派給 Azure AD Premium 授權 toohello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e3a1d-116">Assign an Azure AD Premium license toohello test user</span></span>

- <span data-ttu-id="e3a1d-117">設定受管理的應用程式及指派您的測試使用者 tooit</span><span class="sxs-lookup"><span data-stu-id="e3a1d-117">Configure a managed app and assign your test user tooit</span></span>

- <span data-ttu-id="e3a1d-118">設定信任的 IP</span><span class="sxs-lookup"><span data-stu-id="e3a1d-118">Configure trusted IPs</span></span>

<span data-ttu-id="e3a1d-119">如果您需要更多有關信任 IP 的詳細資訊，請參閱[信任的 IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips)。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-119">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="e3a1d-120">原則設定步驟</span><span class="sxs-lookup"><span data-stu-id="e3a1d-120">Policy configuration steps</span></span>

<span data-ttu-id="e3a1d-121">**tooconfigure 您條件式存取原則，執行：**</span><span class="sxs-lookup"><span data-stu-id="e3a1d-121">**tooconfigure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="e3a1d-122">在 [hello hello 左導覽列上的 Azure 入口網站中按一下**Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-122">In hello Azure portal, on hello left navbar, click **Azure Active Directory**.</span></span> 

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="e3a1d-124">在 [hello **Azure Active Directory**刀鋒視窗中的，在 hello**管理**區段中，按一下**條件式存取**。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-124">On hello **Azure Active Directory** blade, in hello **Manage** section, click **Conditional access**.</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="e3a1d-126">在 [hello**條件式存取**刀鋒視窗，tooopen hello**新增**刀鋒視窗中，在 hello 頂端的 hello 工具列中按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-126">On hello **Conditional Access** blade, tooopen hello **New** blade, in hello toolbar on hello top, click **Add**.</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="e3a1d-128">在 [hello**新增**刀鋒視窗中的，在 hello**名稱**文字方塊中，輸入原則的名稱。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-128">On hello **New** blade, in hello **Name** textbox, type a name for your policy.</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="e3a1d-130">在 [hello**指派**區段中，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-130">In hello **Assignment** section, click **Users and groups**.</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="e3a1d-132">在 [hello**使用者和群組**刀鋒視窗中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e3a1d-132">On hello **Users and groups** blade, perform hello following steps:</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="e3a1d-134">a.</span><span class="sxs-lookup"><span data-stu-id="e3a1d-134">a.</span></span> <span data-ttu-id="e3a1d-135">按一下 [選取使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-135">Click **Select users and groups**.</span></span>

    <span data-ttu-id="e3a1d-136">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-136">b.</span></span> <span data-ttu-id="e3a1d-137">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-137">Click **Select**.</span></span>

    <span data-ttu-id="e3a1d-138">c.</span><span class="sxs-lookup"><span data-stu-id="e3a1d-138">c.</span></span> <span data-ttu-id="e3a1d-139">在 [hello**選取**刀鋒視窗中，選取您的測試使用者，然後按一下**選取**。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-139">On hello **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="e3a1d-140">d.</span><span class="sxs-lookup"><span data-stu-id="e3a1d-140">d.</span></span> <span data-ttu-id="e3a1d-141">在 [hello**使用者和群組**刀鋒視窗中，按一下 [**完成**。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-141">On hello **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="e3a1d-142">在 [hello**新增**刀鋒視窗，tooopen hello**雲端應用程式**刀鋒視窗中的，在 hello**指派**區段中，按一下**雲端應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-142">On hello **New** blade, tooopen hello **Cloud apps** blade, in hello **Assignment** section, click **Cloud apps**.</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="e3a1d-144">在 [hello**雲端應用程式**刀鋒視窗中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e3a1d-144">On hello **Cloud apps** blade, perform hello following steps:</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="e3a1d-146">a.</span><span class="sxs-lookup"><span data-stu-id="e3a1d-146">a.</span></span> <span data-ttu-id="e3a1d-147">按一下 [選取應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-147">Click **Select apps**.</span></span>

    <span data-ttu-id="e3a1d-148">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-148">b.</span></span> <span data-ttu-id="e3a1d-149">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-149">Click **Select**.</span></span>

    <span data-ttu-id="e3a1d-150">c.</span><span class="sxs-lookup"><span data-stu-id="e3a1d-150">c.</span></span> <span data-ttu-id="e3a1d-151">在 [hello**選取**刀鋒視窗中，選取您的雲端應用程式，然後按一下**選取**。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-151">On hello **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="e3a1d-152">d.</span><span class="sxs-lookup"><span data-stu-id="e3a1d-152">d.</span></span> <span data-ttu-id="e3a1d-153">在 [hello**雲端應用程式**刀鋒視窗中，按一下 [**完成**。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-153">On hello **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="e3a1d-154">在 [hello**新增**刀鋒視窗，tooopen hello**條件**刀鋒視窗中的，在 hello**指派**區段中，按一下**條件**。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-154">On hello **New** blade, tooopen hello **Conditions** blade, in hello **Assignment** section, click **Conditions**.</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="e3a1d-156">在 [hello**條件**刀鋒視窗，tooopen hello**位置**刀鋒視窗中，按一下 [**位置**。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-156">On hello **Conditions** blade, tooopen hello **Locations** blade, click **Locations**.</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="e3a1d-158">在 [hello**位置**刀鋒視窗中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e3a1d-158">On hello **Locations** blade, perform hello following steps:</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="e3a1d-160">a.</span><span class="sxs-lookup"><span data-stu-id="e3a1d-160">a.</span></span> <span data-ttu-id="e3a1d-161">在 [設定] 之下，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-161">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="e3a1d-162">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-162">b.</span></span> <span data-ttu-id="e3a1d-163">在 [包含] 之下，按一下 [所有位置]。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-163">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="e3a1d-164">c.</span><span class="sxs-lookup"><span data-stu-id="e3a1d-164">c.</span></span> <span data-ttu-id="e3a1d-165">按一下 [排除]，然後按一下 [所有信任的 IP]。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-165">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="e3a1d-167">d.</span><span class="sxs-lookup"><span data-stu-id="e3a1d-167">d.</span></span> <span data-ttu-id="e3a1d-168">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-168">Click **Done**.</span></span>

12. <span data-ttu-id="e3a1d-169">在 [hello**條件**刀鋒視窗中，按一下 [**完成**。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-169">On hello **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="e3a1d-170">在 [hello**新增**刀鋒視窗，tooopen hello**授與**刀鋒視窗中的，在 hello**控制項**區段中，按一下**授與**。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-170">On hello **New** blade, tooopen hello **Grant** blade, in hello **Controls** section, click **Grant**.</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="e3a1d-172">在 [hello **Grant**刀鋒視窗中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e3a1d-172">On hello **Grant** blade, perform hello following steps:</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="e3a1d-174">a.</span><span class="sxs-lookup"><span data-stu-id="e3a1d-174">a.</span></span> <span data-ttu-id="e3a1d-175">選取 [需要 Multi-Factor Authentication]。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-175">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="e3a1d-176">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-176">b.</span></span> <span data-ttu-id="e3a1d-177">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-177">Click **Select**.</span></span>

15. <span data-ttu-id="e3a1d-178">在 [hello**新增**刀鋒視窗下**啟用原則**，按一下**上**。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-178">On hello **New** blade, under **Enable policy**, click **On**.</span></span>

    ![條件式存取](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="e3a1d-180">在 [hello**新增**刀鋒視窗中，按一下 [**建立**。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-180">On hello **New** blade, click **Create**.</span></span>


## <a name="testing-hello-policy"></a><span data-ttu-id="e3a1d-181">測試 hello 原則</span><span class="sxs-lookup"><span data-stu-id="e3a1d-181">Testing hello policy</span></span>

<span data-ttu-id="e3a1d-182">tootest 您的原則，您應該從裝置存取您的應用程式的：</span><span class="sxs-lookup"><span data-stu-id="e3a1d-182">tootest your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="e3a1d-183">具有在您設定的信任 IP 內的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="e3a1d-183">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="e3a1d-184">具有不在您設定的信任 IP 內的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="e3a1d-184">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="e3a1d-185">只有從不在您設定的信任 IP 內的裝置嘗試連線時，才需要 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-185">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="e3a1d-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e3a1d-186">Next steps</span></span>

<span data-ttu-id="e3a1d-187">如果您想要 toolearn 深入了解條件式存取，請參閱[Azure Active Directory 條件式存取](active-directory-conditional-access-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="e3a1d-187">If you would like toolearn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>


---
title: "aaaHow tooconfigure 安全性警示 |Microsoft 文件"
description: "了解如何 tooconfigure 安全性警示 Azure Privileged Identity Management 延伸模組。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4e0c911a-36c6-42a0-8f79-a01c03d2d04f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 1b3c4a7d36fa3f81bb3fe2574d675fdf0ab34909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-security-alerts-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="b5b87-103">在 Azure AD Privileged Identity Management tooconfigure 安全性警示的方式</span><span class="sxs-lookup"><span data-stu-id="b5b87-103">How tooconfigure security alerts in Azure AD Privileged Identity Management</span></span>
## <a name="security-alerts"></a><span data-ttu-id="b5b87-104">安全性警示</span><span class="sxs-lookup"><span data-stu-id="b5b87-104">Security alerts</span></span>
<span data-ttu-id="b5b87-105">當您環境中有可疑或不安全的活動時，Azure Privileged Identity Management (PIM) 會產生警示。</span><span class="sxs-lookup"><span data-stu-id="b5b87-105">Azure Privileged Identity Management (PIM) generates alerts when there is suspicious or unsafe activity in your environment.</span></span> <span data-ttu-id="b5b87-106">警示觸發時，會出現在 hello PIM 儀表板。</span><span class="sxs-lookup"><span data-stu-id="b5b87-106">When an alert is triggered, it shows up on hello PIM dashboard.</span></span> <span data-ttu-id="b5b87-107">選取 hello 警示 toosee 清單 hello 使用者或角色觸發 hello 警示報表。</span><span class="sxs-lookup"><span data-stu-id="b5b87-107">Select hello alert toosee a report that lists hello users or roles that triggered hello alert.</span></span>

![PIM 儀表板安全性警示 - 螢幕擷取畫面][1]

| <span data-ttu-id="b5b87-109">警示</span><span class="sxs-lookup"><span data-stu-id="b5b87-109">Alert</span></span> | <span data-ttu-id="b5b87-110">觸發程序</span><span class="sxs-lookup"><span data-stu-id="b5b87-110">Trigger</span></span> | <span data-ttu-id="b5b87-111">建議</span><span class="sxs-lookup"><span data-stu-id="b5b87-111">Recommendation</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b5b87-112">**在 PIM 外指派角色**</span><span class="sxs-lookup"><span data-stu-id="b5b87-112">**Roles are being assigned outside of PIM**</span></span> |<span data-ttu-id="b5b87-113">系統管理員已永久指派 tooa 角色，hello PIM 介面之外。</span><span class="sxs-lookup"><span data-stu-id="b5b87-113">An administrator was permanently assigned tooa role, outside of hello PIM interface.</span></span> |<span data-ttu-id="b5b87-114">檢閱 hello 新增角色指派。</span><span class="sxs-lookup"><span data-stu-id="b5b87-114">Review hello new role assignment.</span></span> <span data-ttu-id="b5b87-115">因為其他服務只可以指派永久系統管理員，請視需要變更它 tooan 合格的指派。</span><span class="sxs-lookup"><span data-stu-id="b5b87-115">Since other services can only assign permanent administrators, change it tooan eligible assignment if necessary.</span></span> |
| <span data-ttu-id="b5b87-116">**啟用角色的次數太頻繁**</span><span class="sxs-lookup"><span data-stu-id="b5b87-116">**Roles are being activated too frequently**</span></span> |<span data-ttu-id="b5b87-117">沒有太多重新啟動的 hello 的時間內的相同角色允許 hello 設定中的 hello。</span><span class="sxs-lookup"><span data-stu-id="b5b87-117">There were too many reactivations of hello same role within hello time allowed in hello settings.</span></span> |<span data-ttu-id="b5b87-118">請連絡 hello 使用者 toosee 為何他們已啟用 hello 角色太多次。</span><span class="sxs-lookup"><span data-stu-id="b5b87-118">Contact hello user toosee why they have activated hello role so many times.</span></span> <span data-ttu-id="b5b87-119">或許 hello 時間限制太短，toocomplete 其工作，也可能使用指令碼 tooautomatically 啟用角色。</span><span class="sxs-lookup"><span data-stu-id="b5b87-119">Maybe hello time limit is too short for them toocomplete their tasks, or maybe they're using scripts tooautomatically activate a role.</span></span> |
| <span data-ttu-id="b5b87-120">**角色不需要多重要素驗證來進行啟用**</span><span class="sxs-lookup"><span data-stu-id="b5b87-120">**Roles don't require multi-factor authentication for activation**</span></span> |<span data-ttu-id="b5b87-121">有沒有 hello 設定中啟用 MFA 的角色。</span><span class="sxs-lookup"><span data-stu-id="b5b87-121">There are roles without MFA enabled in hello settings.</span></span> |<span data-ttu-id="b5b87-122">我們要求使用 MFA 進行 hello 最高特殊權限角色，但強烈建議您啟用所有角色的啟用 MFA。</span><span class="sxs-lookup"><span data-stu-id="b5b87-122">We require MFA for hello most highly privileged roles, but strongly encourage that you enable MFA for activation of all roles.</span></span> |
| <span data-ttu-id="b5b87-123">**系統管理員未使用其特殊權限角色**</span><span class="sxs-lookup"><span data-stu-id="b5b87-123">**Administrators aren't using their privileged roles**</span></span> |<span data-ttu-id="b5b87-124">有合格的系統管理員最近尚未啟用其角色。</span><span class="sxs-lookup"><span data-stu-id="b5b87-124">There are eligible administrators that haven’t activated their roles recently.</span></span> |<span data-ttu-id="b5b87-125">啟動不再需要存取存取檢閱 toodetermine hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="b5b87-125">Start an access review toodetermine hello users that don't need access anymore.</span></span> |
| <span data-ttu-id="b5b87-126">**全域管理員太多**</span><span class="sxs-lookup"><span data-stu-id="b5b87-126">**There are too many global administrators**</span></span> |<span data-ttu-id="b5b87-127">全域管理員的數目超過建議的數目。</span><span class="sxs-lookup"><span data-stu-id="b5b87-127">There are more global administrators than recommended.</span></span> |<span data-ttu-id="b5b87-128">如果您有大量的全域管理員，使用者可能會取得超過其所需的權限。</span><span class="sxs-lookup"><span data-stu-id="b5b87-128">If you have a high number of global administrators, it's likely that users are getting more permissions than they need.</span></span> <span data-ttu-id="b5b87-129">移動使用者 tooless 特殊權限角色，或其中部分適合 hello 角色，而不是永久指派。</span><span class="sxs-lookup"><span data-stu-id="b5b87-129">Move users tooless privileged roles, or make some of them eligible for hello role instead of permanently assigned.</span></span> |

## <a name="configure-security-alert-settings"></a><span data-ttu-id="b5b87-130">設定安全性警示設定</span><span class="sxs-lookup"><span data-stu-id="b5b87-130">Configure security alert settings</span></span>
<span data-ttu-id="b5b87-131">您可以自訂一些 PIM toowork 與您的環境安全性目標中的 hello 安全性警示。</span><span class="sxs-lookup"><span data-stu-id="b5b87-131">You can customize some of hello security alerts in PIM toowork with your environment and security goals.</span></span> <span data-ttu-id="b5b87-132">請遵循這些步驟 tooreach hello 設定 刀鋒視窗：</span><span class="sxs-lookup"><span data-stu-id="b5b87-132">Follow these steps tooreach hello settings blade:</span></span>

1. <span data-ttu-id="b5b87-133">登入 toohello [Azure 入口網站](https://portal.azure.com/)和選取 hello **Azure AD Privileged Identity Management**從 hello 儀表板磚。</span><span class="sxs-lookup"><span data-stu-id="b5b87-133">Sign in toohello [Azure portal](https://portal.azure.com/) and select hello **Azure AD Privileged Identity Management** tile from hello dashboard.</span></span>
2. <span data-ttu-id="b5b87-134">選取 [受管理的特殊權限角色] > [設定] > [警示設定]。</span><span class="sxs-lookup"><span data-stu-id="b5b87-134">Select **Managed privileged roles** > **Settings** > **Alerts settings**.</span></span>
   
    ![瀏覽 toosecurity 警示設定][2]

### <a name="roles-are-being-activated-too-frequently-alert"></a><span data-ttu-id="b5b87-136">「啟用角色的次數太頻繁」警示</span><span class="sxs-lookup"><span data-stu-id="b5b87-136">"Roles are being activated too frequently" alert</span></span>
<span data-ttu-id="b5b87-137">如果使用者啟動觸發程序在指定期間內多次 hello 相同的特殊權限的角色此警示。</span><span class="sxs-lookup"><span data-stu-id="b5b87-137">This alert triggers if a user activates hello same privileged role multiple times within a specified period.</span></span> <span data-ttu-id="b5b87-138">您可以設定這兩個 hello 時間期限和 hello 啟用次數。</span><span class="sxs-lookup"><span data-stu-id="b5b87-138">You can configure both hello time period and hello number of activations.</span></span>

* <span data-ttu-id="b5b87-139">**啟動更新的時間範圍內**： 指定在天、 小時、 分鐘，而且第二個 hello 時間週期希望 toouse tootrack 可疑續訂。</span><span class="sxs-lookup"><span data-stu-id="b5b87-139">**Activation renewal timeframe**: Specify in days, hours, minutes, and second hello time period you want toouse tootrack suspicious renewals.</span></span>
* <span data-ttu-id="b5b87-140">**啟用更新次數**： 指定 hello 的啟用數，從 2 too100，考量的警示，您所選擇的 hello 時間範圍內。</span><span class="sxs-lookup"><span data-stu-id="b5b87-140">**Number of activation renewals**: Specify hello number of activations, from 2 too100, that you consider worthy of alert, within hello timeframe you chose.</span></span> <span data-ttu-id="b5b87-141">您可以變更此設定所移動的 hello 滑桿，或在 hello 文字方塊中輸入數字。</span><span class="sxs-lookup"><span data-stu-id="b5b87-141">You can change this setting by moving hello slider, or typing a number in hello text box.</span></span>

### <a name="there-are-too-many-global-administrators-alert"></a><span data-ttu-id="b5b87-142">「全域管理員太多」警示</span><span class="sxs-lookup"><span data-stu-id="b5b87-142">"There are too many global administrators" alert</span></span>
<span data-ttu-id="b5b87-143">當符合兩個不同的條件時，PIM 就會觸發此警示，而您可以同時設定這兩個條件。</span><span class="sxs-lookup"><span data-stu-id="b5b87-143">PIM triggers this alert if two different criteria are met, and you can configure both of them.</span></span> <span data-ttu-id="b5b87-144">首先，您需要 tooreach 特定的臨界值的全域管理員。</span><span class="sxs-lookup"><span data-stu-id="b5b87-144">First, you need tooreach a certain threshold of global administrators.</span></span> <span data-ttu-id="b5b87-145">其次，角色指派總數中必須有特定百分比是全域管理員。</span><span class="sxs-lookup"><span data-stu-id="b5b87-145">Second, a certain percentage of your total role assignments must be global administrators.</span></span> <span data-ttu-id="b5b87-146">如果您只符合這些度量的其中一項，hello 警示未出現。</span><span class="sxs-lookup"><span data-stu-id="b5b87-146">If you only meet one of these measurements, hello alert does not appear.</span></span>  

* <span data-ttu-id="b5b87-147">**全域管理員數目下限**： 指定的全域管理員，從 2 too100，請考慮不安全的數量的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="b5b87-147">**Minimum number of Global Administrators**: Specify hello number of global administrators, from 2 too100, that you consider an unsafe amount.</span></span>
* <span data-ttu-id="b5b87-148">**全域管理員佔**： 指定的系統管理員是全域管理員，從 0%的 hello 百分比 too100%不安全環境中。</span><span class="sxs-lookup"><span data-stu-id="b5b87-148">**Percentage of global administrators**: Specify hello percentage of administrators who are global administrators, from 0% too100%, that is unsafe in your environment.</span></span>

### <a name="administrators-arent-using-their-privileged-roles-alert"></a><span data-ttu-id="b5b87-149">「系統管理員未使用其特殊權限角色」警示</span><span class="sxs-lookup"><span data-stu-id="b5b87-149">"Administrators aren't using their privileged roles" alert</span></span>
<span data-ttu-id="b5b87-150">當使用者在經過一段特定時間後仍未啟用角色，就會觸發此警示。</span><span class="sxs-lookup"><span data-stu-id="b5b87-150">This alert triggers if a user goes a certain amount of time without activating a role.</span></span>

* <span data-ttu-id="b5b87-151">**天數**： 指定的天數，從 0 too100，使用者可以前往不啟動角色的 hello。</span><span class="sxs-lookup"><span data-stu-id="b5b87-151">**Number of days**: Specify hello number of days, from 0 too100, that a user can go without activating a role.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5b87-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b5b87-152">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_dash.png
[2]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_settings.png

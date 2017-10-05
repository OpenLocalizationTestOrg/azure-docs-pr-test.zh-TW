---
title: "如何設定安全性警示 | Microsoft Docs"
description: "了解如何為 Azure Privileged Identity Management 擴充功能設定安全性警示。"
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
ms.openlocfilehash: e057120e31eeebc3da274536c09d6d9972854338
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-security-alerts-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="71d82-103">Azure AD Privileged Identity Management：如何設定安全性警示</span><span class="sxs-lookup"><span data-stu-id="71d82-103">How to configure security alerts in Azure AD Privileged Identity Management</span></span>
## <a name="security-alerts"></a><span data-ttu-id="71d82-104">安全性警示</span><span class="sxs-lookup"><span data-stu-id="71d82-104">Security alerts</span></span>
<span data-ttu-id="71d82-105">當您環境中有可疑或不安全的活動時，Azure Privileged Identity Management (PIM) 會產生警示。</span><span class="sxs-lookup"><span data-stu-id="71d82-105">Azure Privileged Identity Management (PIM) generates alerts when there is suspicious or unsafe activity in your environment.</span></span> <span data-ttu-id="71d82-106">觸發警示時，會顯示在 PIM 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="71d82-106">When an alert is triggered, it shows up on the PIM dashboard.</span></span> <span data-ttu-id="71d82-107">選取警示，以查看詳列觸發警示之使用者或角色的報告。</span><span class="sxs-lookup"><span data-stu-id="71d82-107">Select the alert to see a report that lists the users or roles that triggered the alert.</span></span>

![PIM 儀表板安全性警示 - 螢幕擷取畫面][1]

| <span data-ttu-id="71d82-109">警示</span><span class="sxs-lookup"><span data-stu-id="71d82-109">Alert</span></span> | <span data-ttu-id="71d82-110">觸發程序</span><span class="sxs-lookup"><span data-stu-id="71d82-110">Trigger</span></span> | <span data-ttu-id="71d82-111">建議</span><span class="sxs-lookup"><span data-stu-id="71d82-111">Recommendation</span></span> |
| --- | --- | --- |
| <span data-ttu-id="71d82-112">**在 PIM 外指派角色**</span><span class="sxs-lookup"><span data-stu-id="71d82-112">**Roles are being assigned outside of PIM**</span></span> |<span data-ttu-id="71d82-113">在 PIM 介面外將系統管理員永久指派給了某個角色。</span><span class="sxs-lookup"><span data-stu-id="71d82-113">An administrator was permanently assigned to a role, outside of the PIM interface.</span></span> |<span data-ttu-id="71d82-114">請檢閱新的角色指派。</span><span class="sxs-lookup"><span data-stu-id="71d82-114">Review the new role assignment.</span></span> <span data-ttu-id="71d82-115">由於其他服務只能指派永久系統管理員，因此請視需要將它變更成合格指派。</span><span class="sxs-lookup"><span data-stu-id="71d82-115">Since other services can only assign permanent administrators, change it to an eligible assignment if necessary.</span></span> |
| <span data-ttu-id="71d82-116">**啟用角色的次數太頻繁**</span><span class="sxs-lookup"><span data-stu-id="71d82-116">**Roles are being activated too frequently**</span></span> |<span data-ttu-id="71d82-117">在設定所允許的時間內，重複啟用相同角色的次數過多。</span><span class="sxs-lookup"><span data-stu-id="71d82-117">There were too many reactivations of the same role within the time allowed in the settings.</span></span> |<span data-ttu-id="71d82-118">請連絡使用者以了解他們啟用角色這麼多次的原因。</span><span class="sxs-lookup"><span data-stu-id="71d82-118">Contact the user to see why they have activated the role so many times.</span></span> <span data-ttu-id="71d82-119">可能是時間限制太短以致於他們無法完成其工作，或可能是他們使用指令碼來自動啟用角色。</span><span class="sxs-lookup"><span data-stu-id="71d82-119">Maybe the time limit is too short for them to complete their tasks, or maybe they're using scripts to automatically activate a role.</span></span> |
| <span data-ttu-id="71d82-120">**角色不需要多重要素驗證來進行啟用**</span><span class="sxs-lookup"><span data-stu-id="71d82-120">**Roles don't require multi-factor authentication for activation**</span></span> |<span data-ttu-id="71d82-121">設定中有一些未啟用 MFA 功能的角色。</span><span class="sxs-lookup"><span data-stu-id="71d82-121">There are roles without MFA enabled in the settings.</span></span> |<span data-ttu-id="71d82-122">針對特殊權限最高的角色，我們要求必須啟用 MFA，但強烈建議您針對所有角色的啟用都啟用 MFA。</span><span class="sxs-lookup"><span data-stu-id="71d82-122">We require MFA for the most highly privileged roles, but strongly encourage that you enable MFA for activation of all roles.</span></span> |
| <span data-ttu-id="71d82-123">**系統管理員未使用其特殊權限角色**</span><span class="sxs-lookup"><span data-stu-id="71d82-123">**Administrators aren't using their privileged roles**</span></span> |<span data-ttu-id="71d82-124">有合格的系統管理員最近尚未啟用其角色。</span><span class="sxs-lookup"><span data-stu-id="71d82-124">There are eligible administrators that haven’t activated their roles recently.</span></span> |<span data-ttu-id="71d82-125">請開始存取權檢閱，以判斷出不再需要存取權的使用者。</span><span class="sxs-lookup"><span data-stu-id="71d82-125">Start an access review to determine the users that don't need access anymore.</span></span> |
| <span data-ttu-id="71d82-126">**全域管理員太多**</span><span class="sxs-lookup"><span data-stu-id="71d82-126">**There are too many global administrators**</span></span> |<span data-ttu-id="71d82-127">全域管理員的數目超過建議的數目。</span><span class="sxs-lookup"><span data-stu-id="71d82-127">There are more global administrators than recommended.</span></span> |<span data-ttu-id="71d82-128">如果您有大量的全域管理員，使用者可能會取得超過其所需的權限。</span><span class="sxs-lookup"><span data-stu-id="71d82-128">If you have a high number of global administrators, it's likely that users are getting more permissions than they need.</span></span> <span data-ttu-id="71d82-129">請將使用者移至特殊權限較低的角色，或將部分使用者設為符合該角色資格，而不是永久指派。</span><span class="sxs-lookup"><span data-stu-id="71d82-129">Move users to less privileged roles, or make some of them eligible for the role instead of permanently assigned.</span></span> |

## <a name="configure-security-alert-settings"></a><span data-ttu-id="71d82-130">設定安全性警示設定</span><span class="sxs-lookup"><span data-stu-id="71d82-130">Configure security alert settings</span></span>
<span data-ttu-id="71d82-131">您可以在 PIM 中自訂一些安全性警示，以便配合您的環境和安全性目標。</span><span class="sxs-lookup"><span data-stu-id="71d82-131">You can customize some of the security alerts in PIM to work with your environment and security goals.</span></span> <span data-ttu-id="71d82-132">請依照下列步驟來前往 [設定] 刀鋒視窗︰</span><span class="sxs-lookup"><span data-stu-id="71d82-132">Follow these steps to reach the settings blade:</span></span>

1. <span data-ttu-id="71d82-133">登入 [Azure 入口網站](https://portal.azure.com/)，然後從儀表板中選取 [Azure AD Privileged Identity Management] 磚。</span><span class="sxs-lookup"><span data-stu-id="71d82-133">Sign in to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** tile from the dashboard.</span></span>
2. <span data-ttu-id="71d82-134">選取 [受管理的特殊權限角色] > [設定] > [警示設定]。</span><span class="sxs-lookup"><span data-stu-id="71d82-134">Select **Managed privileged roles** > **Settings** > **Alerts settings**.</span></span>
   
    ![瀏覽至安全性警示設定][2]

### <a name="roles-are-being-activated-too-frequently-alert"></a><span data-ttu-id="71d82-136">「啟用角色的次數太頻繁」警示</span><span class="sxs-lookup"><span data-stu-id="71d82-136">"Roles are being activated too frequently" alert</span></span>
<span data-ttu-id="71d82-137">當使用者在指定期間內多次啟用相同的特殊權限角色時，就會觸發此警示。</span><span class="sxs-lookup"><span data-stu-id="71d82-137">This alert triggers if a user activates the same privileged role multiple times within a specified period.</span></span> <span data-ttu-id="71d82-138">您可以同時設定時段和啟用次數。</span><span class="sxs-lookup"><span data-stu-id="71d82-138">You can configure both the time period and the number of activations.</span></span>

* <span data-ttu-id="71d82-139">**啟用更新時間範圍**︰以天、小時、分鐘及秒為單位，指定您想要用來追蹤可疑更新的時段。</span><span class="sxs-lookup"><span data-stu-id="71d82-139">**Activation renewal timeframe**: Specify in days, hours, minutes, and second the time period you want to use to track suspicious renewals.</span></span>
* <span data-ttu-id="71d82-140">**啟用更新次數**︰指定在您選擇的時間範圍內，您視為值得發出警示的啟用次數 (從 2 到 100)。</span><span class="sxs-lookup"><span data-stu-id="71d82-140">**Number of activation renewals**: Specify the number of activations, from 2 to 100, that you consider worthy of alert, within the timeframe you chose.</span></span> <span data-ttu-id="71d82-141">您可以移動滑桿或在文字方塊中輸入數字，以變更此設定。</span><span class="sxs-lookup"><span data-stu-id="71d82-141">You can change this setting by moving the slider, or typing a number in the text box.</span></span>

### <a name="there-are-too-many-global-administrators-alert"></a><span data-ttu-id="71d82-142">「全域管理員太多」警示</span><span class="sxs-lookup"><span data-stu-id="71d82-142">"There are too many global administrators" alert</span></span>
<span data-ttu-id="71d82-143">當符合兩個不同的條件時，PIM 就會觸發此警示，而您可以同時設定這兩個條件。</span><span class="sxs-lookup"><span data-stu-id="71d82-143">PIM triggers this alert if two different criteria are met, and you can configure both of them.</span></span> <span data-ttu-id="71d82-144">首先，您必須達到特定的全域管理員臨界值。</span><span class="sxs-lookup"><span data-stu-id="71d82-144">First, you need to reach a certain threshold of global administrators.</span></span> <span data-ttu-id="71d82-145">其次，角色指派總數中必須有特定百分比是全域管理員。</span><span class="sxs-lookup"><span data-stu-id="71d82-145">Second, a certain percentage of your total role assignments must be global administrators.</span></span> <span data-ttu-id="71d82-146">如果只符合這些測量結果其中之一，就不會出現警示。</span><span class="sxs-lookup"><span data-stu-id="71d82-146">If you only meet one of these measurements, the alert does not appear.</span></span>  

* <span data-ttu-id="71d82-147">**全域管理員數目下限**︰指定您視為不安全數量的全域管理員數目 (從 2 到 100)。</span><span class="sxs-lookup"><span data-stu-id="71d82-147">**Minimum number of Global Administrators**: Specify the number of global administrators, from 2 to 100, that you consider an unsafe amount.</span></span>
* <span data-ttu-id="71d82-148">**全域管理員百分比**：指定在您環境中視為不安全、擔任全域管理員的系統管理員百分比 (從 0% 到 100%)。</span><span class="sxs-lookup"><span data-stu-id="71d82-148">**Percentage of global administrators**: Specify the percentage of administrators who are global administrators, from 0% to 100%, that is unsafe in your environment.</span></span>

### <a name="administrators-arent-using-their-privileged-roles-alert"></a><span data-ttu-id="71d82-149">「系統管理員未使用其特殊權限角色」警示</span><span class="sxs-lookup"><span data-stu-id="71d82-149">"Administrators aren't using their privileged roles" alert</span></span>
<span data-ttu-id="71d82-150">當使用者在經過一段特定時間後仍未啟用角色，就會觸發此警示。</span><span class="sxs-lookup"><span data-stu-id="71d82-150">This alert triggers if a user goes a certain amount of time without activating a role.</span></span>

* <span data-ttu-id="71d82-151">**天數**︰指定使用者可以維持不啟用角色的天數 (從 0 到 100)。</span><span class="sxs-lookup"><span data-stu-id="71d82-151">**Number of days**: Specify the number of days, from 0 to 100, that a user can go without activating a role.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71d82-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="71d82-152">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_dash.png
[2]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_settings.png

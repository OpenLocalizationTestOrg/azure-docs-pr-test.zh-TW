---
title: "在 Windows PowerShell 中調整 Azure 雲端服務 |Microsoft Docs"
description: "(傳統) 了解如何使用 PowerShell 在 Azure 中相應放大或縮小 Web 角色或背景工作角色。"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: ee37dd8c-6714-4c61-adb8-03d6bbf76c9a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: mmccrory
ms.openlocfilehash: a7ae8ff202d403dff19b8c9a6a09492235db27ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-scale-a-cloud-service-in-powershell"></a><span data-ttu-id="7306b-103">如何在 PowerShell 中調整雲端服務</span><span class="sxs-lookup"><span data-stu-id="7306b-103">How to scale a cloud service in PowerShell</span></span>

<span data-ttu-id="7306b-104">您可以使用 Windows PowerShell 來新增或移除執行個體，以相應放大或縮小 Web 角色或背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="7306b-104">You can use Windows PowerShell to scale a web role or worker role in or out by adding or removing instances.</span></span>  

## <a name="log-in-to-azure"></a><span data-ttu-id="7306b-105">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="7306b-105">Log in to Azure</span></span>

<span data-ttu-id="7306b-106">您必須先登入，才能透過 PowerShell 在訂用帳戶上執行任何作業︰</span><span class="sxs-lookup"><span data-stu-id="7306b-106">Before you can perform any operations on your subscription through PowerShell, you must log in:</span></span>

```powershell
Add-AzureAccount
```

<span data-ttu-id="7306b-107">如果您的帳戶有多個相關聯的訂用帳戶，視您的雲端服務所在的位置而定，您可能需要變更目前的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7306b-107">If you have multiple subscriptions associated with your account, you may need to change the current subscription depending on where your cloud service resides.</span></span> <span data-ttu-id="7306b-108">若要檢查目前的訂用帳戶，請執行：</span><span class="sxs-lookup"><span data-stu-id="7306b-108">To check the current subscription, run:</span></span>

```powershell
Get-AzureSubscription -Current
```

<span data-ttu-id="7306b-109">如果您需要變更目前的訂用帳戶，請執行︰</span><span class="sxs-lookup"><span data-stu-id="7306b-109">If you need to change the current subscription, run:</span></span>

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-the-current-instance-count-for-your-role"></a><span data-ttu-id="7306b-110">檢查您的角色目前的執行個體計數</span><span class="sxs-lookup"><span data-stu-id="7306b-110">Check the current instance count for your role</span></span>

<span data-ttu-id="7306b-111">若要檢查您的角色目前的狀態，請執行。</span><span class="sxs-lookup"><span data-stu-id="7306b-111">To check the current state of your role, run:</span></span>

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

<span data-ttu-id="7306b-112">您應該會取回角色的相關資訊，包括其目前的作業系統版本和執行個體計數。</span><span class="sxs-lookup"><span data-stu-id="7306b-112">You should get back information about the role, including its current OS version and instance count.</span></span> <span data-ttu-id="7306b-113">在此案例中，角色具有單一執行個體。</span><span class="sxs-lookup"><span data-stu-id="7306b-113">In this case, the role has a single instance.</span></span>

![角色的相關資訊](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-the-role-by-adding-more-instances"></a><span data-ttu-id="7306b-115">新增更多執行個體以相應放大角色</span><span class="sxs-lookup"><span data-stu-id="7306b-115">Scale out the role by adding more instances</span></span>

<span data-ttu-id="7306b-116">若要相應放大您的角色，請以 **Count** 參數將所需的執行個體數目傳遞至 **Set-AzureRole** Cmdlet︰</span><span class="sxs-lookup"><span data-stu-id="7306b-116">To scale out your role, pass the desired number of instances as the **Count** parameter to the **Set-AzureRole** cmdlet:</span></span>

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

<span data-ttu-id="7306b-117">在佈建和啟動新的執行個體時，Cmdlet 區塊會暫時凍結。</span><span class="sxs-lookup"><span data-stu-id="7306b-117">The cmdlet blocks momentarily while the new instances are provisioned and started.</span></span> <span data-ttu-id="7306b-118">在此期間，如果您開啟新的 PowerShell 視窗，然後如稍早所示呼叫 **Get-AzureRole**，您會看到新的目標執行個體計數。</span><span class="sxs-lookup"><span data-stu-id="7306b-118">During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see the new target instance count.</span></span> <span data-ttu-id="7306b-119">如果您在入口網站中檢查角色狀態，應該會看到新的執行個體正在啟動︰</span><span class="sxs-lookup"><span data-stu-id="7306b-119">And if you inspect the role status in the portal, you should see the new instance starting up:</span></span>

![VM instance starting in portal](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

<span data-ttu-id="7306b-121">當新的執行個體啟動後，Cmdlet 將會順利返回︰</span><span class="sxs-lookup"><span data-stu-id="7306b-121">Once the new instances have started, the cmdlet will return successfully:</span></span>

![角色執行個體成功增加](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-the-role-by-removing-instances"></a><span data-ttu-id="7306b-123">移除執行個體以相應縮小角色</span><span class="sxs-lookup"><span data-stu-id="7306b-123">Scale in the role by removing instances</span></span>

<span data-ttu-id="7306b-124">您可以用相同方式移除執行個體，以相應縮小角色。</span><span class="sxs-lookup"><span data-stu-id="7306b-124">You can scale in a role by removing instances in the same way.</span></span> <span data-ttu-id="7306b-125">將 **Set-AzureRole**的 **Count** 參數設定為您希望相應縮小作業完成之後存在的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="7306b-125">Set the **Count** parameter on **Set-AzureRole** to the number of instances you want to have after the scale in operation is complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7306b-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7306b-126">Next steps</span></span>

<span data-ttu-id="7306b-127">您無法從 PowerShell 設定自動調整雲端服務。</span><span class="sxs-lookup"><span data-stu-id="7306b-127">It is not possible to configure auto-scale for cloud services from PowerShell.</span></span> <span data-ttu-id="7306b-128">若要這麼做，請參閱[如何自動調整雲端服務](cloud-services-how-to-scale-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="7306b-128">To do that, see [How to auto scale a cloud service](cloud-services-how-to-scale-portal.md).</span></span>

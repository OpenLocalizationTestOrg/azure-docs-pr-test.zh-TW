---
title: "Azure Application Insights 中的資源、角色及存取控制 | Microsoft Docs"
description: "您的組織詳細資料的擁有者、參與者及讀者。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: c979a8bfbeecacc7c0bbc112e02a4b68e874c219
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a><span data-ttu-id="cadf5-103">Application Insights 中的資源、角色及存取控制</span><span class="sxs-lookup"><span data-stu-id="cadf5-103">Resources, roles, and access control in Application Insights</span></span>
<span data-ttu-id="cadf5-104">您可以使用 [Microsoft Azure 中的角色型存取控制](../active-directory/role-based-access-control-configure.md) ，控制誰對您在 Azure [Application Insights][start] 中的資料具有讀取和更新存取權。</span><span class="sxs-lookup"><span data-stu-id="cadf5-104">You can control who has read and update access to your data in Azure [Application Insights][start], by using [Role-based access control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cadf5-105">指派存取權給您的應用程式資源所屬之 **資源群組或訂用帳戶** 中的使用者 - 不在資源本身。</span><span class="sxs-lookup"><span data-stu-id="cadf5-105">Assign access to users in the **resource group or subscription** to which your application resource belongs - not in the resource itself.</span></span> <span data-ttu-id="cadf5-106">指派 **Application Insights 元件參與者** 角色。</span><span class="sxs-lookup"><span data-stu-id="cadf5-106">Assign the **Application Insights component contributor** role.</span></span> <span data-ttu-id="cadf5-107">這可確保 Web 測試和警示以及您的應用程式資源的統一存取控制。</span><span class="sxs-lookup"><span data-stu-id="cadf5-107">This ensures uniform control of access to web tests and alerts along with your application resource.</span></span> <span data-ttu-id="cadf5-108">[深入了解](#access)。</span><span class="sxs-lookup"><span data-stu-id="cadf5-108">[Learn more](#access).</span></span>
> 
> 

## <a name="resources-groups-and-subscriptions"></a><span data-ttu-id="cadf5-109">資源、群組和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cadf5-109">Resources, groups and subscriptions</span></span>
<span data-ttu-id="cadf5-110">首先是一些定義：</span><span class="sxs-lookup"><span data-stu-id="cadf5-110">First, some definitions:</span></span>

* <span data-ttu-id="cadf5-111">**資源** - Microsoft Azure 服務的執行個體。</span><span class="sxs-lookup"><span data-stu-id="cadf5-111">**Resource** - An instance of a Microsoft Azure service.</span></span> <span data-ttu-id="cadf5-112">您的 Application Insights 資源會收集、分析及顯示從您的應用程式傳送的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="cadf5-112">Your Application Insights resource collects, analyzes and displays the telemetry data sent from your application.</span></span>  <span data-ttu-id="cadf5-113">其他類型的 Azure 資源包括 Web 應用程式、資料庫和 VM。</span><span class="sxs-lookup"><span data-stu-id="cadf5-113">Other types of Azure resources include web apps, databases, and VMs.</span></span>
  
    <span data-ttu-id="cadf5-114">若要查看資源，請開啟 [Azure 入口網站][portal]，登入並按一下 [所有資源]。</span><span class="sxs-lookup"><span data-stu-id="cadf5-114">To see your resources, open the [Azure Portal][portal], sign in, and click All Resources.</span></span> <span data-ttu-id="cadf5-115">若要尋找的資源，請在篩選欄位中輸入名稱的一部分。</span><span class="sxs-lookup"><span data-stu-id="cadf5-115">To find a resource, type part of its name in the filter field.</span></span>
  
    ![Azure 資源清單](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* <span data-ttu-id="cadf5-117">[資源群組][group] - 每個資源屬於一個群組。</span><span class="sxs-lookup"><span data-stu-id="cadf5-117">[**Resource group**][group] - Every resource belongs to one group.</span></span> <span data-ttu-id="cadf5-118">群組是管理相關資源的便利方式，特別是針對存取控制。</span><span class="sxs-lookup"><span data-stu-id="cadf5-118">A group is a convenient way to manage related resources, particularly for access control.</span></span> <span data-ttu-id="cadf5-119">例如，您可以將 Web 應用程式、Application Insights 資源放到一個資源群組，以監視應用程式，以及放到儲存體資源以保存匯出的資料。</span><span class="sxs-lookup"><span data-stu-id="cadf5-119">For example, into one resource group you could put a Web App, an Application Insights resource to monitor the app, and a Storage resource to keep exported data.</span></span>

    ![選擇 [瀏覽]、[資源群組]，然後選擇 [群組]](./media/app-insights-resources-roles-access-control/11-group.png)

* <span data-ttu-id="cadf5-121">[**訂用帳戶**](https://manage.windowsazure.com) - 若要使用 Application Insights 或其他 Azure 資源，您可以登入 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="cadf5-121">[**Subscription**](https://manage.windowsazure.com) - To use Application Insights or other Azure resources, you sign in to an Azure subscription.</span></span> <span data-ttu-id="cadf5-122">每個資源群組都屬於一個 Azure 訂用帳戶，其中您選擇價格封裝，如果是組織的訂用帳戶，請選擇成員以及其存取權限。</span><span class="sxs-lookup"><span data-stu-id="cadf5-122">Every resource group belongs to one Azure subscription, where you choose your price package and, if it's an organization subscription, choose the members and their access permissions.</span></span>
* <span data-ttu-id="cadf5-123">[**Microsoft 帳戶**][account] - 您用來登入 Microsoft Azure 訂用帳戶、XBox Live、Outlook.com 及其他 Microsoft 服務的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="cadf5-123">[**Microsoft account**][account] - The username and password that you use to sign in to Microsoft Azure subscriptions, XBox Live, Outlook.com, and other Microsoft services.</span></span>

## <span data-ttu-id="cadf5-124"><a name="access"></a> 控制資源群組中的存取</span><span class="sxs-lookup"><span data-stu-id="cadf5-124"><a name="access"></a> Control access in the resource group</span></span>
<span data-ttu-id="cadf5-125">請務必了解除了您為應用程式建立的資源之外，還有警示和 Web 測試的個別隱藏資源。</span><span class="sxs-lookup"><span data-stu-id="cadf5-125">It's important to understand that in addition to the resource you created for your application, there are also separate hidden resources for alerts and web tests.</span></span> <span data-ttu-id="cadf5-126">它們會附加到與您的應用程式相同的 [資源群組](#resource-group) 。</span><span class="sxs-lookup"><span data-stu-id="cadf5-126">They are attached to the same [resource group](#resource-group) as your application.</span></span> <span data-ttu-id="cadf5-127">您也可以在那裡放置其他 Azure 服務，例如網站或儲存體。</span><span class="sxs-lookup"><span data-stu-id="cadf5-127">You might also have put other Azure services in there, such as websites or storage.</span></span>

![Application Insights 中的資源](./media/app-insights-resources-roles-access-control/00-resources.png)

<span data-ttu-id="cadf5-129">為了控制這些資源的存取，因此建議您：</span><span class="sxs-lookup"><span data-stu-id="cadf5-129">To control access to these resources it's therefore recommended to:</span></span>

* <span data-ttu-id="cadf5-130">在 **資源群組或訂用帳戶** 層級控制存取。</span><span class="sxs-lookup"><span data-stu-id="cadf5-130">Control access at the **resource group or subscription** level.</span></span>
* <span data-ttu-id="cadf5-131">指派 **Application Insights 元件參與者** 角色給使用者。</span><span class="sxs-lookup"><span data-stu-id="cadf5-131">Assign the **Application Insights Component contributor** role to users.</span></span> <span data-ttu-id="cadf5-132">這可讓他們編輯 Web 測試、警示和 Application Insights 資源，而不用提供群組中任何其他服務的存取權。</span><span class="sxs-lookup"><span data-stu-id="cadf5-132">This allows them to edit web tests, alerts, and Application Insights resources, without providing access to any other services in the group.</span></span>

## <a name="to-provide-access-to-another-user"></a><span data-ttu-id="cadf5-133">若要提供存取權給其他使用者</span><span class="sxs-lookup"><span data-stu-id="cadf5-133">To provide access to another user</span></span>
<span data-ttu-id="cadf5-134">您必須擁有訂用帳戶或資源群組的擁有者權限。</span><span class="sxs-lookup"><span data-stu-id="cadf5-134">You must have Owner rights to the subscription or the resource group.</span></span>

<span data-ttu-id="cadf5-135">使用者必須擁有 [Microsoft 帳戶][account]，或其[組織的 Microsoft 帳戶](../active-directory/sign-up-organization.md)存取權。</span><span class="sxs-lookup"><span data-stu-id="cadf5-135">The user must have a [Microsoft Account][account], or access to their [organizational Microsoft Account](../active-directory/sign-up-organization.md).</span></span> <span data-ttu-id="cadf5-136">您可以提供存取權給個人，也可以提供給在 Azure Active Directory 中定義的使用者群組。</span><span class="sxs-lookup"><span data-stu-id="cadf5-136">You can provide access to individuals, and also to user groups defined in Azure Active Directory.</span></span>

#### <a name="navigate-to-the-resource-group"></a><span data-ttu-id="cadf5-137">瀏覽至資源群組</span><span class="sxs-lookup"><span data-stu-id="cadf5-137">Navigate to the resource group</span></span>
<span data-ttu-id="cadf5-138">在那裡新增使用者。</span><span class="sxs-lookup"><span data-stu-id="cadf5-138">Add the user there.</span></span>

![在您的應用程式資源刀鋒視窗中，開啟 Essentials、開啟資源群組，然後在該處選取 [設定/使用者]。](./media/app-insights-resources-roles-access-control/01-add-user.png)

<span data-ttu-id="cadf5-141">或者，您可以上移至另一個層級，並且將使用者加入至訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="cadf5-141">Or you could go up another level and add the user to the Subscription.</span></span>

#### <a name="select-a-role"></a><span data-ttu-id="cadf5-142">選取角色</span><span class="sxs-lookup"><span data-stu-id="cadf5-142">Select a role</span></span>
![選取新使用者的角色](./media/app-insights-resources-roles-access-control/03-role.png)

| <span data-ttu-id="cadf5-144">角色</span><span class="sxs-lookup"><span data-stu-id="cadf5-144">Role</span></span> | <span data-ttu-id="cadf5-145">在資源群組中</span><span class="sxs-lookup"><span data-stu-id="cadf5-145">In the resource group</span></span> |
| --- | --- |
| <span data-ttu-id="cadf5-146">擁有者</span><span class="sxs-lookup"><span data-stu-id="cadf5-146">Owner</span></span> |<span data-ttu-id="cadf5-147">可以變更任何項目，包括使用者存取</span><span class="sxs-lookup"><span data-stu-id="cadf5-147">Can change anything, including user access</span></span> |
| <span data-ttu-id="cadf5-148">參與者</span><span class="sxs-lookup"><span data-stu-id="cadf5-148">Contributor</span></span> |<span data-ttu-id="cadf5-149">可以編輯任何項目，包括所有資源</span><span class="sxs-lookup"><span data-stu-id="cadf5-149">Can edit anything, including all resources</span></span> |
| <span data-ttu-id="cadf5-150">Application Insights 元件參與者</span><span class="sxs-lookup"><span data-stu-id="cadf5-150">Application Insights Component contributor</span></span> |<span data-ttu-id="cadf5-151">可以編輯 Application Insights 資源、Web 測試和警示</span><span class="sxs-lookup"><span data-stu-id="cadf5-151">Can edit Application Insights resources, web tests and alerts</span></span> |
| <span data-ttu-id="cadf5-152">讀取者</span><span class="sxs-lookup"><span data-stu-id="cadf5-152">Reader</span></span> |<span data-ttu-id="cadf5-153">可以檢視但無法變更任何項目</span><span class="sxs-lookup"><span data-stu-id="cadf5-153">Can view but not change anything</span></span> |

<span data-ttu-id="cadf5-154">「編輯」包括建立、刪除及更新：</span><span class="sxs-lookup"><span data-stu-id="cadf5-154">'Editing' includes creating, deleting and updating:</span></span>

* <span data-ttu-id="cadf5-155">資源</span><span class="sxs-lookup"><span data-stu-id="cadf5-155">Resources</span></span>
* <span data-ttu-id="cadf5-156">Web 測試</span><span class="sxs-lookup"><span data-stu-id="cadf5-156">Web tests</span></span>
* <span data-ttu-id="cadf5-157">Alerts</span><span class="sxs-lookup"><span data-stu-id="cadf5-157">Alerts</span></span>
* <span data-ttu-id="cadf5-158">連續匯出</span><span class="sxs-lookup"><span data-stu-id="cadf5-158">Continuous export</span></span>

#### <a name="select-the-user"></a><span data-ttu-id="cadf5-159">選取使用者</span><span class="sxs-lookup"><span data-stu-id="cadf5-159">Select the user</span></span>

<span data-ttu-id="cadf5-160">如果您想要的使用者不在目錄中，您可以邀請任何具有 Microsoft 帳戶的使用者。</span><span class="sxs-lookup"><span data-stu-id="cadf5-160">If the user you want isn't in the directory, you can invite anyone with a Microsoft account.</span></span>
<span data-ttu-id="cadf5-161">(如果他們使用 Outlook.com、OneDrive、Windows Phone 或 XBox Live 等服務，他們就會有 Microsoft 帳戶。)</span><span class="sxs-lookup"><span data-stu-id="cadf5-161">(If they use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, they have a Microsoft account.)</span></span>

## <a name="related-content"></a><span data-ttu-id="cadf5-162">相關內容</span><span class="sxs-lookup"><span data-stu-id="cadf5-162">Related content</span></span>

* [<span data-ttu-id="cadf5-163">Azure 中的角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="cadf5-163">Role based access control in Azure</span></span>](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md

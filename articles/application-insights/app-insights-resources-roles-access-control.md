---
title: "在 Azure Application Insights aaaResources、 角色和存取控制 |Microsoft 文件"
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
ms.openlocfilehash: a6f6ca0443b5f60239f094606e124f856967d8ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a><span data-ttu-id="49094-103">Application Insights 中的資源、角色及存取控制</span><span class="sxs-lookup"><span data-stu-id="49094-103">Resources, roles, and access control in Application Insights</span></span>
<span data-ttu-id="49094-104">您可以控制誰具有讀取和更新存取 Azure 中的 tooyour 資料[Application Insights][start]，使用[Microsoft Azure 中的角色型存取控制](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="49094-104">You can control who has read and update access tooyour data in Azure [Application Insights][start], by using [Role-based access control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49094-105">指派在 hello 存取 toousers**資源群組或訂用帳戶**toowhich 應用程式資源所屬-不在 hello 資源本身。</span><span class="sxs-lookup"><span data-stu-id="49094-105">Assign access toousers in hello **resource group or subscription** toowhich your application resource belongs - not in hello resource itself.</span></span> <span data-ttu-id="49094-106">指派 hello **Application Insights 元件參與者**角色。</span><span class="sxs-lookup"><span data-stu-id="49094-106">Assign hello **Application Insights component contributor** role.</span></span> <span data-ttu-id="49094-107">這可確保存取 tooweb 測試和警示，以及您的應用程式資源的統一的控制項。</span><span class="sxs-lookup"><span data-stu-id="49094-107">This ensures uniform control of access tooweb tests and alerts along with your application resource.</span></span> <span data-ttu-id="49094-108">[深入了解](#access)。</span><span class="sxs-lookup"><span data-stu-id="49094-108">[Learn more](#access).</span></span>
> 
> 

## <a name="resources-groups-and-subscriptions"></a><span data-ttu-id="49094-109">資源、群組和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="49094-109">Resources, groups and subscriptions</span></span>
<span data-ttu-id="49094-110">首先是一些定義：</span><span class="sxs-lookup"><span data-stu-id="49094-110">First, some definitions:</span></span>

* <span data-ttu-id="49094-111">**資源** - Microsoft Azure 服務的執行個體。</span><span class="sxs-lookup"><span data-stu-id="49094-111">**Resource** - An instance of a Microsoft Azure service.</span></span> <span data-ttu-id="49094-112">Application Insights 資源會收集、 分析及顯示 hello 遙測資料從您的應用程式傳送。</span><span class="sxs-lookup"><span data-stu-id="49094-112">Your Application Insights resource collects, analyzes and displays hello telemetry data sent from your application.</span></span>  <span data-ttu-id="49094-113">其他類型的 Azure 資源包括 Web 應用程式、資料庫和 VM。</span><span class="sxs-lookup"><span data-stu-id="49094-113">Other types of Azure resources include web apps, databases, and VMs.</span></span>
  
    <span data-ttu-id="49094-114">您的資源，開啟 toosee hello [Azure 入口網站][portal]、 登入，然後按一下 所有資源。</span><span class="sxs-lookup"><span data-stu-id="49094-114">toosee your resources, open hello [Azure Portal][portal], sign in, and click All Resources.</span></span> <span data-ttu-id="49094-115">toofind 資源，其名稱 hello filter 欄位中的類型部分。</span><span class="sxs-lookup"><span data-stu-id="49094-115">toofind a resource, type part of its name in hello filter field.</span></span>
  
    ![Azure 資源清單](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* <span data-ttu-id="49094-117">[**資源群組**] [ group] -每個資源所屬 tooone 群組。</span><span class="sxs-lookup"><span data-stu-id="49094-117">[**Resource group**][group] - Every resource belongs tooone group.</span></span> <span data-ttu-id="49094-118">群組是一種方便的方式 toomanage 相關聯的資源，特別是針對存取控制。</span><span class="sxs-lookup"><span data-stu-id="49094-118">A group is a convenient way toomanage related resources, particularly for access control.</span></span> <span data-ttu-id="49094-119">例如，一個資源群組，您無法將 Web 應用程式，Application Insights 資源 toomonitor hello 應用程式，與儲存體資源 tookeep 匯入資料。</span><span class="sxs-lookup"><span data-stu-id="49094-119">For example, into one resource group you could put a Web App, an Application Insights resource toomonitor hello app, and a Storage resource tookeep exported data.</span></span>

    ![選擇 [瀏覽]、[資源群組]，然後選擇 [群組]](./media/app-insights-resources-roles-access-control/11-group.png)

* <span data-ttu-id="49094-121">[**訂用帳戶**](https://manage.windowsazure.com) -toouse Application Insights 或其他 Azure 資源，請在您登入 tooan Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="49094-121">[**Subscription**](https://manage.windowsazure.com) - toouse Application Insights or other Azure resources, you sign in tooan Azure subscription.</span></span> <span data-ttu-id="49094-122">每個資源群組所屬 tooone Azure 訂用帳戶，其中您選擇價格封裝，如果它是組織訂用帳戶中，選擇 hello 成員和其存取權限。</span><span class="sxs-lookup"><span data-stu-id="49094-122">Every resource group belongs tooone Azure subscription, where you choose your price package and, if it's an organization subscription, choose hello members and their access permissions.</span></span>
* <span data-ttu-id="49094-123">[**Microsoft 帳戶**] [ account] -hello 使用者名稱和密碼，您使用 toosign tooMicrosoft Azure 訂用帳戶、 XBox Live、 Outlook.com 及其他 Microsoft 服務。</span><span class="sxs-lookup"><span data-stu-id="49094-123">[**Microsoft account**][account] - hello username and password that you use toosign in tooMicrosoft Azure subscriptions, XBox Live, Outlook.com, and other Microsoft services.</span></span>

## <span data-ttu-id="49094-124"><a name="access"></a>Hello 資源群組中的控制存取</span><span class="sxs-lookup"><span data-stu-id="49094-124"><a name="access"></a> Control access in hello resource group</span></span>
<span data-ttu-id="49094-125">很重要的 toounderstand 在加法 toohello 資源您建立應用程式中，沒有也分隔 隱藏的警示和 web 測試的資源。</span><span class="sxs-lookup"><span data-stu-id="49094-125">It's important toounderstand that in addition toohello resource you created for your application, there are also separate hidden resources for alerts and web tests.</span></span> <span data-ttu-id="49094-126">它們是附加的 toohello 相同[資源群組](#resource-group)與應用程式。</span><span class="sxs-lookup"><span data-stu-id="49094-126">They are attached toohello same [resource group](#resource-group) as your application.</span></span> <span data-ttu-id="49094-127">您也可以在那裡放置其他 Azure 服務，例如網站或儲存體。</span><span class="sxs-lookup"><span data-stu-id="49094-127">You might also have put other Azure services in there, such as websites or storage.</span></span>

![Application Insights 中的資源](./media/app-insights-resources-roles-access-control/00-resources.png)

<span data-ttu-id="49094-129">因此建議您 toocontrol 存取 toothese 資源：</span><span class="sxs-lookup"><span data-stu-id="49094-129">toocontrol access toothese resources it's therefore recommended to:</span></span>

* <span data-ttu-id="49094-130">控制存取在 hello**資源群組或訂用帳戶**層級。</span><span class="sxs-lookup"><span data-stu-id="49094-130">Control access at hello **resource group or subscription** level.</span></span>
* <span data-ttu-id="49094-131">指派 hello**應用程式 Insights 元件參與者**角色 toousers。</span><span class="sxs-lookup"><span data-stu-id="49094-131">Assign hello **Application Insights Component contributor** role toousers.</span></span> <span data-ttu-id="49094-132">這可讓它們 tooedit web 測試、 警示和 Application Insights 資源，而不需提供存取 tooany hello 群組中的其他服務。</span><span class="sxs-lookup"><span data-stu-id="49094-132">This allows them tooedit web tests, alerts, and Application Insights resources, without providing access tooany other services in hello group.</span></span>

## <a name="tooprovide-access-tooanother-user"></a><span data-ttu-id="49094-133">tooprovide 存取 tooanother 使用者</span><span class="sxs-lookup"><span data-stu-id="49094-133">tooprovide access tooanother user</span></span>
<span data-ttu-id="49094-134">您必須擁有者權限 toohello 訂用帳戶或 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="49094-134">You must have Owner rights toohello subscription or hello resource group.</span></span>

<span data-ttu-id="49094-135">hello 使用者必須擁有[Microsoft 帳戶][account]，或存取 tootheir[組織的 Microsoft 帳戶](../active-directory/sign-up-organization.md)。</span><span class="sxs-lookup"><span data-stu-id="49094-135">hello user must have a [Microsoft Account][account], or access tootheir [organizational Microsoft Account](../active-directory/sign-up-organization.md).</span></span> <span data-ttu-id="49094-136">您可以提供存取 tooindividuals 以及 toouser Azure Active Directory 中定義的群組。</span><span class="sxs-lookup"><span data-stu-id="49094-136">You can provide access tooindividuals, and also toouser groups defined in Azure Active Directory.</span></span>

#### <a name="navigate-toohello-resource-group"></a><span data-ttu-id="49094-137">瀏覽 toohello 資源群組</span><span class="sxs-lookup"><span data-stu-id="49094-137">Navigate toohello resource group</span></span>
<span data-ttu-id="49094-138">將那里 hello 使用者加入。</span><span class="sxs-lookup"><span data-stu-id="49094-138">Add hello user there.</span></span>

![在您的應用程式資源刀鋒視窗中，開啟 Essentials 開啟 hello 資源群組，然後在該處選取 設定/使用者。](./media/app-insights-resources-roles-access-control/01-add-user.png)

<span data-ttu-id="49094-141">或者，您無法向上另一個層級，並加入 hello 使用者 toohello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="49094-141">Or you could go up another level and add hello user toohello Subscription.</span></span>

#### <a name="select-a-role"></a><span data-ttu-id="49094-142">選取角色</span><span class="sxs-lookup"><span data-stu-id="49094-142">Select a role</span></span>
![選取 hello 新使用者角色](./media/app-insights-resources-roles-access-control/03-role.png)

| <span data-ttu-id="49094-144">角色</span><span class="sxs-lookup"><span data-stu-id="49094-144">Role</span></span> | <span data-ttu-id="49094-145">Hello 資源群組中</span><span class="sxs-lookup"><span data-stu-id="49094-145">In hello resource group</span></span> |
| --- | --- |
| <span data-ttu-id="49094-146">擁有者</span><span class="sxs-lookup"><span data-stu-id="49094-146">Owner</span></span> |<span data-ttu-id="49094-147">可以變更任何項目，包括使用者存取</span><span class="sxs-lookup"><span data-stu-id="49094-147">Can change anything, including user access</span></span> |
| <span data-ttu-id="49094-148">參與者</span><span class="sxs-lookup"><span data-stu-id="49094-148">Contributor</span></span> |<span data-ttu-id="49094-149">可以編輯任何項目，包括所有資源</span><span class="sxs-lookup"><span data-stu-id="49094-149">Can edit anything, including all resources</span></span> |
| <span data-ttu-id="49094-150">Application Insights 元件參與者</span><span class="sxs-lookup"><span data-stu-id="49094-150">Application Insights Component contributor</span></span> |<span data-ttu-id="49094-151">可以編輯 Application Insights 資源、Web 測試和警示</span><span class="sxs-lookup"><span data-stu-id="49094-151">Can edit Application Insights resources, web tests and alerts</span></span> |
| <span data-ttu-id="49094-152">讀取者</span><span class="sxs-lookup"><span data-stu-id="49094-152">Reader</span></span> |<span data-ttu-id="49094-153">可以檢視但無法變更任何項目</span><span class="sxs-lookup"><span data-stu-id="49094-153">Can view but not change anything</span></span> |

<span data-ttu-id="49094-154">「編輯」包括建立、刪除及更新：</span><span class="sxs-lookup"><span data-stu-id="49094-154">'Editing' includes creating, deleting and updating:</span></span>

* <span data-ttu-id="49094-155">資源</span><span class="sxs-lookup"><span data-stu-id="49094-155">Resources</span></span>
* <span data-ttu-id="49094-156">Web 測試</span><span class="sxs-lookup"><span data-stu-id="49094-156">Web tests</span></span>
* <span data-ttu-id="49094-157">Alerts</span><span class="sxs-lookup"><span data-stu-id="49094-157">Alerts</span></span>
* <span data-ttu-id="49094-158">連續匯出</span><span class="sxs-lookup"><span data-stu-id="49094-158">Continuous export</span></span>

#### <a name="select-hello-user"></a><span data-ttu-id="49094-159">選取 hello 使用者</span><span class="sxs-lookup"><span data-stu-id="49094-159">Select hello user</span></span>

<span data-ttu-id="49094-160">如果您想要的 hello 使用者不在 hello 目錄中，您可以邀請任何具有 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="49094-160">If hello user you want isn't in hello directory, you can invite anyone with a Microsoft account.</span></span>
<span data-ttu-id="49094-161">(如果他們使用 Outlook.com、OneDrive、Windows Phone 或 XBox Live 等服務，他們就會有 Microsoft 帳戶。)</span><span class="sxs-lookup"><span data-stu-id="49094-161">(If they use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, they have a Microsoft account.)</span></span>

## <a name="related-content"></a><span data-ttu-id="49094-162">相關內容</span><span class="sxs-lookup"><span data-stu-id="49094-162">Related content</span></span>

* [<span data-ttu-id="49094-163">Azure 中的角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="49094-163">Role based access control in Azure</span></span>](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md

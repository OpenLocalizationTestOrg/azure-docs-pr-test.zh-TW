---
title: "aaaMonitor 變更的虛擬機器的 Azure 事件方格 & Logic Apps |Microsoft 文件"
description: "使用 Azure Event Grid 和 Logic Apps 來檢查虛擬機器 (VM) 的組態變更"
keywords: "logic apps, event grids, 虛擬機器, VM"
services: logic-apps
author: ecfan
manager: anneta
ms.assetid: 
ms.workload: logic-apps
ms.service: logic-apps
ms.topic: article
ms.date: 08/16/2017
ms.author: LADocs; estfan
ms.openlocfilehash: f0633e598be6e7880a310e6f8e64f6738cc692b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-changes-with-azure-event-grid-and-logic-apps"></a><span data-ttu-id="26f54-104">使用 Azure Event Grid 和 Logic Apps 監視虛擬機器變更</span><span class="sxs-lookup"><span data-stu-id="26f54-104">Monitor virtual machine changes with Azure Event Grid and Logic Apps</span></span>

<span data-ttu-id="26f54-105">當 Azure 資源或第三方資源發生特定事件時，您可以啟動自動化[邏輯應用程式工作流程](../logic-apps/logic-apps-what-are-logic-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="26f54-105">You can start an automated [logic app workflow](../logic-apps/logic-apps-what-are-logic-apps.md) when specific events happen in Azure resources or third-party resources.</span></span> <span data-ttu-id="26f54-106">這些資源可以發行這些事件 tooan [Azure 事件方格](../event-grid/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="26f54-106">These resources can publish those events tooan [Azure event grid](../event-grid/overview.md).</span></span> <span data-ttu-id="26f54-107">接著，hello 事件方格推播通知已佇列 webhook，這些事件 toosubscribers 或[事件中心](../event-hubs/event-hubs-what-is-event-hubs.md)為端點。</span><span class="sxs-lookup"><span data-stu-id="26f54-107">In turn, hello event grid pushes those events toosubscribers that have queues, webhooks, or [event hubs](../event-hubs/event-hubs-what-is-event-hubs.md) as endpoints.</span></span> <span data-ttu-id="26f54-108">為訂閱者，邏輯應用程式可以等待 hello 事件方格中的這些事件，您撰寫任何程式碼不執行自動化的流程 tooperform 工作-之前。</span><span class="sxs-lookup"><span data-stu-id="26f54-108">As a subscriber, your logic app can wait for those events from hello event grid before running automated workflows tooperform tasks - without you writing any code.</span></span>

<span data-ttu-id="26f54-109">例如，以下是 「 發行者 」 可以傳送 hello Azure 事件方格服務透過 toosubscribers 某些事件：</span><span class="sxs-lookup"><span data-stu-id="26f54-109">For example, here are some events that publishers can send toosubscribers through hello Azure Event Grid service:</span></span>

* <span data-ttu-id="26f54-110">建立、讀取、更新或刪除資源。</span><span class="sxs-lookup"><span data-stu-id="26f54-110">Create, read, update, or delete a resource.</span></span> <span data-ttu-id="26f54-111">例如，您可以監視可能會產生 Azure 訂用帳戶費用並會影響帳單的變更。</span><span class="sxs-lookup"><span data-stu-id="26f54-111">For example, you can monitor changes that might incur charges on your Azure subscription and affect your bill.</span></span> 
* <span data-ttu-id="26f54-112">從 Azure 訂用帳戶中新增或移除人員。</span><span class="sxs-lookup"><span data-stu-id="26f54-112">Add or remove a person from an Azure subscription.</span></span>
* <span data-ttu-id="26f54-113">您的應用程式會執行特定動作。</span><span class="sxs-lookup"><span data-stu-id="26f54-113">Your app performs a particular action.</span></span>
* <span data-ttu-id="26f54-114">新的訊息會出現在佇列中。</span><span class="sxs-lookup"><span data-stu-id="26f54-114">A new message appears in a queue.</span></span>

<span data-ttu-id="26f54-115">本教學課程中建立邏輯應用程式，監視變更 tooa 虛擬機器，並將傳送電子郵件有關這些變更。</span><span class="sxs-lookup"><span data-stu-id="26f54-115">This tutorial creates a logic app that monitors changes tooa virtual machine and sends emails about those changes.</span></span> <span data-ttu-id="26f54-116">當您建立邏輯應用程式與 Azure 資源的事件訂閱時，事件流程從事件方格 toohello 邏輯應用程式透過該資源。</span><span class="sxs-lookup"><span data-stu-id="26f54-116">When you create a logic app with an event subscription for an Azure resource, events flow from that resource through an event grid toohello logic app.</span></span> <span data-ttu-id="26f54-117">hello 教學課程會引導您建立此邏輯應用程式：</span><span class="sxs-lookup"><span data-stu-id="26f54-117">hello tutorial walks you through building this logic app:</span></span>

![概觀 - 使用 Event Grid 和邏輯應用程式來監視虛擬機器](./media/monitor-virtual-machine-changes-event-grid-logic-app/monitor-virtual-machine-event-grid-logic-app-overview.png)

<span data-ttu-id="26f54-119">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="26f54-119">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="26f54-120">建立可從 Event Grid 監視事件的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="26f54-120">Create a logic app that monitors events from an event grid.</span></span>
> * <span data-ttu-id="26f54-121">新增可特別檢查虛擬機器變更的條件。</span><span class="sxs-lookup"><span data-stu-id="26f54-121">Add a condition that specifically checks for virtual machine changes.</span></span>
> * <span data-ttu-id="26f54-122">在虛擬機器變更時傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="26f54-122">Send email when your virtual machine changes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26f54-123">必要條件</span><span class="sxs-lookup"><span data-stu-id="26f54-123">Prerequisites</span></span>

* <span data-ttu-id="26f54-124">來自 [Azure Logic Apps 所支援的任何電子郵件提供者](../connectors/apis-list.md)的電子郵件帳戶，例如 Office 365 Outlook、Outlook.com 或 Gmail，以傳送通知。</span><span class="sxs-lookup"><span data-stu-id="26f54-124">An email account from [any email provider supported by Azure Logic Apps](../connectors/apis-list.md), such as Office 365 Outlook, Outlook.com, or Gmail, for sending notifications.</span></span> <span data-ttu-id="26f54-125">本教學課程是使用 Office 365 Outlook。</span><span class="sxs-lookup"><span data-stu-id="26f54-125">This tutorial uses Office 365 Outlook.</span></span>

* <span data-ttu-id="26f54-126">[虛擬機器](https://azure.microsoft.com/services/virtual-machines)。</span><span class="sxs-lookup"><span data-stu-id="26f54-126">A [virtual machine](https://azure.microsoft.com/services/virtual-machines).</span></span> <span data-ttu-id="26f54-127">如果您尚未這樣做，請透過[建立 VM 教學課程](https://docs.microsoft.com/azure/virtual-machines/)來建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="26f54-127">If you haven't already done so, create a virtual machine through a [Create a VM tutorial](https://docs.microsoft.com/azure/virtual-machines/).</span></span> <span data-ttu-id="26f54-128">toomake hello 虛擬機器發行事件，您[不需要任何其他 toodo](../event-grid/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="26f54-128">toomake hello virtual machine publish events, you [don't need toodo anything else](../event-grid/overview.md).</span></span>

## <a name="create-a-logic-app-that-monitors-events-from-an-event-grid"></a><span data-ttu-id="26f54-129">建立可從 Event Grid 監視事件的邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="26f54-129">Create a logic app that monitors events from an event grid</span></span>

<span data-ttu-id="26f54-130">首先，建立邏輯應用程式，並加入您的虛擬機器的 hello 資源群組會監視事件方格觸發程序。</span><span class="sxs-lookup"><span data-stu-id="26f54-130">First, create a logic app and add an Event grid trigger that monitors hello resource group for your virtual machine.</span></span> 

1. <span data-ttu-id="26f54-131">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="26f54-131">Sign in toohello [Azure portal](https://portal.azure.com).</span></span> 

2. <span data-ttu-id="26f54-132">從 hello 的左上角 hello 主要 Azure 功能表，選擇 **新增** > **企業整合** > **邏輯應用程式**。</span><span class="sxs-lookup"><span data-stu-id="26f54-132">From hello upper left corner of hello main Azure menu, choose **New** > **Enterprise Integration** > **Logic App**.</span></span>

   ![建立邏輯應用程式](./media/monitor-virtual-machine-changes-event-grid-logic-app/azure-portal-create-logic-app.png)

3. <span data-ttu-id="26f54-134">建立邏輯應用程式指定 hello 下表中的 hello 設定：</span><span class="sxs-lookup"><span data-stu-id="26f54-134">Create your logic app with hello settings specified in hello following table:</span></span>

   ![提供邏輯應用程式詳細資料](./media/monitor-virtual-machine-changes-event-grid-logic-app/create-logic-app-for-event-grid.png)

   | <span data-ttu-id="26f54-136">設定</span><span class="sxs-lookup"><span data-stu-id="26f54-136">Setting</span></span> | <span data-ttu-id="26f54-137">建議的值</span><span class="sxs-lookup"><span data-stu-id="26f54-137">Suggested value</span></span> | <span data-ttu-id="26f54-138">說明</span><span class="sxs-lookup"><span data-stu-id="26f54-138">Description</span></span> | 
   | ------- | --------------- | ----------- | 
   | <span data-ttu-id="26f54-139">**名稱**</span><span class="sxs-lookup"><span data-stu-id="26f54-139">**Name**</span></span> | <span data-ttu-id="26f54-140">{your-logic-app-name}</span><span class="sxs-lookup"><span data-stu-id="26f54-140">*{your-logic-app-name}*</span></span> | <span data-ttu-id="26f54-141">提供唯一的邏輯應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="26f54-141">Provide a unique logic app name.</span></span> | 
   | <span data-ttu-id="26f54-142">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="26f54-142">**Subscription**</span></span> | <span data-ttu-id="26f54-143">{your-Azure-subscription}</span><span class="sxs-lookup"><span data-stu-id="26f54-143">*{your-Azure-subscription}*</span></span> | <span data-ttu-id="26f54-144">選取 hello 相同 Azure 訂用帳戶的所有服務在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="26f54-144">Select hello same Azure subscription for all services in this tutorial.</span></span> | 
   | <span data-ttu-id="26f54-145">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="26f54-145">**Resource group**</span></span> | <span data-ttu-id="26f54-146">{your-Azure-resource-group}</span><span class="sxs-lookup"><span data-stu-id="26f54-146">*{your-Azure-resource-group}*</span></span> | <span data-ttu-id="26f54-147">選取 hello 本教學課程中的所有服務相同的 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="26f54-147">Select hello same Azure resource group for all services in this tutorial.</span></span> | 
   | <span data-ttu-id="26f54-148">**位置**</span><span class="sxs-lookup"><span data-stu-id="26f54-148">**Location**</span></span> | <span data-ttu-id="26f54-149">{your-Azure-region}</span><span class="sxs-lookup"><span data-stu-id="26f54-149">*{your-Azure-region}*</span></span> | <span data-ttu-id="26f54-150">選取 hello 本教學課程中的所有服務都有相同的區域。</span><span class="sxs-lookup"><span data-stu-id="26f54-150">Select hello same region for all services in this tutorial.</span></span> | 
   | | | 

4. <span data-ttu-id="26f54-151">當您準備好時，選取**Pin toodashboard**，然後選擇 **建立**。</span><span class="sxs-lookup"><span data-stu-id="26f54-151">When you're ready, select **Pin toodashboard**, and choose **Create**.</span></span>

   <span data-ttu-id="26f54-152">您現在已經為您的應用程式邏輯建立一項 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="26f54-152">You've now created an Azure resource for your logic app.</span></span> 
   <span data-ttu-id="26f54-153">Azure 會將您的邏輯應用程式部署之後，hello 邏輯應用程式的設計工具顯示您範本的一般模式讓您可以更快開始。</span><span class="sxs-lookup"><span data-stu-id="26f54-153">After Azure deploys your logic app, hello Logic Apps Designer shows you templates for common patterns so you can get started faster.</span></span>

   > [!NOTE] 
   > <span data-ttu-id="26f54-154">當您選取**Pin toodashboard**，應用程式邏輯會自動開啟邏輯應用程式的設計工具中。</span><span class="sxs-lookup"><span data-stu-id="26f54-154">When you select **Pin toodashboard**, your logic app automatically opens in Logic Apps Designer.</span></span> <span data-ttu-id="26f54-155">不然，您可以手動尋找並開啟您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="26f54-155">Otherwise, you can manually find and open your logic app.</span></span>

5. <span data-ttu-id="26f54-156">立即選擇邏輯應用程式範本。</span><span class="sxs-lookup"><span data-stu-id="26f54-156">Now choose a logic app template.</span></span> <span data-ttu-id="26f54-157">在 [範本] 之下，選擇 [空白邏輯應用程式]，以便從頭建置邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="26f54-157">Under **Templates**, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

   ![選擇 [邏輯應用程式] 範本](./media/monitor-virtual-machine-changes-event-grid-logic-app/choose-logic-app-template.png)

   <span data-ttu-id="26f54-159">hello 邏輯應用程式的設計工具現在會顯示您[*連接器*](../connectors/apis-list.md)和[*觸發程序*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)邏輯應用程式，並也動作，您可以使用 toostart您可以新增觸發程序 tooperform 工作之後。</span><span class="sxs-lookup"><span data-stu-id="26f54-159">hello Logic Apps Designer now shows you [*connectors*](../connectors/apis-list.md) and [*triggers*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) that you can use toostart your logic app, and also actions that you can add after a trigger tooperform tasks.</span></span> <span data-ttu-id="26f54-160">觸發程序是可建立邏輯應用程式執行個體並啟動邏輯應用程式工作流程的事件。</span><span class="sxs-lookup"><span data-stu-id="26f54-160">A trigger is an event that creates a logic app instance and starts your logic app workflow.</span></span> 
   <span data-ttu-id="26f54-161">邏輯應用程式需要觸發程序為 hello 第一個項目。</span><span class="sxs-lookup"><span data-stu-id="26f54-161">Your logic app needs a trigger as hello first item.</span></span>

6. <span data-ttu-id="26f54-162">Hello 搜尋方塊中，輸入 「 事件方格 」 做為您的篩選器。</span><span class="sxs-lookup"><span data-stu-id="26f54-162">In hello search box, enter "event grid" as your filter.</span></span> <span data-ttu-id="26f54-163">選取此觸發程序：**Azure Event Grid - 在資源事件上**</span><span class="sxs-lookup"><span data-stu-id="26f54-163">Select this trigger: **Azure Event Grid - On a resource event**</span></span>

   ![選取此觸發程序：「Azure Event Grid - 在資源事件上」](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger.png)

7. <span data-ttu-id="26f54-165">出現提示時，登入與您的 Azure 認證 tooAzure 事件方格。</span><span class="sxs-lookup"><span data-stu-id="26f54-165">When prompted, sign in tooAzure Event Grid with your Azure credentials.</span></span>

   ![利用您的 Azure 認證登入](./media/monitor-virtual-machine-changes-event-grid-logic-app/sign-in-event-grid.png)

   > [!NOTE]
   > <span data-ttu-id="26f54-167">如果您已經登入個人 Microsoft 帳戶，例如@outlook.com或@hotmail.com，hello 事件方格觸發程序可能無法正確顯示。</span><span class="sxs-lookup"><span data-stu-id="26f54-167">If you're signed in with a personal Microsoft account, such as @outlook.com or @hotmail.com, hello Event Grid trigger might not appear correctly.</span></span> <span data-ttu-id="26f54-168">因應措施，請選擇[連線與服務主體](/azure-resource-manager/resource-group-create-service-principal-portal.md)，或驗證 hello 與您 Azure 訂用帳戶，例如相關的 Azure Active Directory 的成員身分*使用者名稱*@emailoutlook.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="26f54-168">As a workaround, choose [Connect with Service Principal](/azure-resource-manager/resource-group-create-service-principal-portal.md), or authenticate as a member of hello Azure Active Directory that's associated with your Azure subscription, for example, *user-name*@emailoutlook.onmicrosoft.com.</span></span>

8. <span data-ttu-id="26f54-169">現在訂閱您 toopublisher 邏輯應用程式的事件。</span><span class="sxs-lookup"><span data-stu-id="26f54-169">Now subscribe your logic app toopublisher events.</span></span> <span data-ttu-id="26f54-170">提供您 hello 下表中所指定的事件訂閱 hello 詳細資料：</span><span class="sxs-lookup"><span data-stu-id="26f54-170">Provide hello details for your event subscription as specified in hello following table:</span></span>

   ![提供事件訂閱的詳細資料](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details-generic.png)

   | <span data-ttu-id="26f54-172">設定</span><span class="sxs-lookup"><span data-stu-id="26f54-172">Setting</span></span> | <span data-ttu-id="26f54-173">建議的值</span><span class="sxs-lookup"><span data-stu-id="26f54-173">Suggested value</span></span> | <span data-ttu-id="26f54-174">說明</span><span class="sxs-lookup"><span data-stu-id="26f54-174">Description</span></span> | 
   | ------- | --------------- | ----------- | 
   | <span data-ttu-id="26f54-175">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="26f54-175">**Subscription**</span></span> | <span data-ttu-id="26f54-176">{virtual-machine-Azure-subscription}</span><span class="sxs-lookup"><span data-stu-id="26f54-176">*{virtual-machine-Azure-subscription}*</span></span> | <span data-ttu-id="26f54-177">選取 hello 事件發行者的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="26f54-177">Select hello event publisher's Azure subscription.</span></span> <span data-ttu-id="26f54-178">此教學課程中，選取 hello 虛擬機器的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="26f54-178">For this tutorial, select hello Azure subscription for your virtual machine.</span></span> | 
   | <span data-ttu-id="26f54-179">**資源類型**</span><span class="sxs-lookup"><span data-stu-id="26f54-179">**Resource Type**</span></span> | <span data-ttu-id="26f54-180">Microsoft.Resources.resourceGroups</span><span class="sxs-lookup"><span data-stu-id="26f54-180">Microsoft.Resources.resourceGroups</span></span> | <span data-ttu-id="26f54-181">選取 hello 事件發行者的資源類型。</span><span class="sxs-lookup"><span data-stu-id="26f54-181">Select hello event publisher's resource type.</span></span> <span data-ttu-id="26f54-182">此教學課程中，選取 hello 指定的值，因此邏輯應用程式監視只資源群組。</span><span class="sxs-lookup"><span data-stu-id="26f54-182">For this tutorial, select hello specified value so your logic app monitors only resource groups.</span></span> | 
   | <span data-ttu-id="26f54-183">**資源名稱**</span><span class="sxs-lookup"><span data-stu-id="26f54-183">**Resource Name**</span></span> | <span data-ttu-id="26f54-184">{virtual-machine-resource-group-name}</span><span class="sxs-lookup"><span data-stu-id="26f54-184">*{virtual-machine-resource-group-name}*</span></span> | <span data-ttu-id="26f54-185">選取 hello 發行者的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="26f54-185">Select hello publisher's resource name.</span></span> <span data-ttu-id="26f54-186">此教學課程中，選取 hello hello 資源群組名稱為虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="26f54-186">For this tutorial, select hello name of hello resource group for your virtual machine.</span></span> | 
   | <span data-ttu-id="26f54-187">針對選擇性設定，選擇 [顯示進階選項]。</span><span class="sxs-lookup"><span data-stu-id="26f54-187">For optional settings, choose **Show advanced options**.</span></span> | <span data-ttu-id="26f54-188">{see descriptions}</span><span class="sxs-lookup"><span data-stu-id="26f54-188">*{see descriptions}*</span></span> | <span data-ttu-id="26f54-189">* **前置詞篩選條件**：在此教學課程中，將此設定保留空白。</span><span class="sxs-lookup"><span data-stu-id="26f54-189">* **Prefix Filter**: For this tutorial, leave this setting empty.</span></span> <span data-ttu-id="26f54-190">hello 預設行為會比對所有的值。</span><span class="sxs-lookup"><span data-stu-id="26f54-190">hello default behavior matches all values.</span></span> <span data-ttu-id="26f54-191">不過，您可以指定前置詞字串作為篩選條件，例如，特定資源的路徑和參數。</span><span class="sxs-lookup"><span data-stu-id="26f54-191">However, you can specify a prefix string as a filter, for example, a path and a parameter for a specific resource.</span></span> <p><span data-ttu-id="26f54-192">* **後置詞篩選條件**：在此教學課程中，將此設定保留空白。</span><span class="sxs-lookup"><span data-stu-id="26f54-192">* **Suffix Filter**: For this tutorial, leave this setting empty.</span></span> <span data-ttu-id="26f54-193">hello 預設行為會比對所有的值。</span><span class="sxs-lookup"><span data-stu-id="26f54-193">hello default behavior matches all values.</span></span> <span data-ttu-id="26f54-194">不過，您可以指定前置詞字串作為篩選條件，例如，副檔名 (如果只想要特定檔案類型)。</span><span class="sxs-lookup"><span data-stu-id="26f54-194">However, you can specify a suffix string as a filter, for example, a file name extension, when you want only specific file types.</span></span><p><span data-ttu-id="26f54-195">* **訂用帳戶名稱**：提供事件訂用帳戶的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="26f54-195">* **Subscription Name**: Provide a unique name for your event subscription.</span></span> |
   | | | 

   <span data-ttu-id="26f54-196">當您完成時，Event Grid 觸發程序可能如此範例所示︰</span><span class="sxs-lookup"><span data-stu-id="26f54-196">When you're done, your event grid trigger might look like this example:</span></span>
   
   ![範例 Event Grid 觸發程序詳細資料](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details.png)

9. <span data-ttu-id="26f54-198">儲存您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="26f54-198">Save your logic app.</span></span> <span data-ttu-id="26f54-199">Hello 設計工具工具列上，選擇**儲存**。</span><span class="sxs-lookup"><span data-stu-id="26f54-199">On hello designer toolbar, choose **Save**.</span></span> <span data-ttu-id="26f54-200">toocollapse 和隱藏動作的詳細資料，在邏輯應用程式，然後選擇 hello 動作的標題列。</span><span class="sxs-lookup"><span data-stu-id="26f54-200">toocollapse and hide an action's details in your logic app, choose hello action's title bar.</span></span>

   ![儲存您的邏輯應用程式](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save.png)

   <span data-ttu-id="26f54-202">當您儲存應用程式邏輯與事件方格的觸發程序時，Azure 會自動建立邏輯應用程式選取 tooyour 資源事件訂閱。</span><span class="sxs-lookup"><span data-stu-id="26f54-202">When you save your logic app with an event grid trigger, Azure automatically creates an event subscription for your logic app tooyour selected resource.</span></span> <span data-ttu-id="26f54-203">因此當 hello 資源發行事件 toohello 事件方格時，該事件方格自動推入 hello 事件 tooyour 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="26f54-203">So when hello resource publishes an event toohello event grid, that event grid automatically pushes hello event tooyour logic app.</span></span> <span data-ttu-id="26f54-204">此事件觸發程序邏輯應用程式，然後建立及執行您在下面的步驟中定義的 hello 工作流程執行個體。</span><span class="sxs-lookup"><span data-stu-id="26f54-204">This event triggers your logic app, then creates and runs an instance of hello workflow that you define in these next steps.</span></span>

<span data-ttu-id="26f54-205">邏輯應用程式現在是即時和會接聽 tooevents hello 事件方格中，但不會加入動作 toohello 工作流程之前執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="26f54-205">Your logic app is now live and listens tooevents from hello event grid, but doesn't do anything until you add actions toohello workflow.</span></span> 

## <a name="add-a-condition-that-checks-for-virtual-machine-changes"></a><span data-ttu-id="26f54-206">新增可檢查虛擬機器變更的條件</span><span class="sxs-lookup"><span data-stu-id="26f54-206">Add a condition that checks for virtual machine changes</span></span>

<span data-ttu-id="26f54-207">toorun 邏輯應用程式工作流程的特定事件發生時，才會加入條件來檢查虛擬機器的 「 寫入 」 作業。</span><span class="sxs-lookup"><span data-stu-id="26f54-207">toorun your logic app workflow only when a specific event happens, add a condition that checks for virtual machine "write" operations.</span></span> <span data-ttu-id="26f54-208">此條件為 true 時，應用程式邏輯會將傳送您電子郵件傳送嗨更新虛擬機器的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="26f54-208">When this condition is true, your logic app sends you email with details about hello updated virtual machine.</span></span>

1. <span data-ttu-id="26f54-209">邏輯應用程式的設計工具，在 hello 事件方格觸發程序，在選擇**新步驟** > **加入條件**。</span><span class="sxs-lookup"><span data-stu-id="26f54-209">In Logic App Designer, under hello event grid trigger, choose **New step** > **Add a condition**.</span></span>

   ![新增條件 tooyour 邏輯應用程式](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-add-condition-step.png)

   <span data-ttu-id="26f54-211">hello 邏輯應用程式的設計工具加入了空白的條件 tooyour 工作流程，包括動作路徑 toofollow 根據是否 hello 條件為 true 或 false。</span><span class="sxs-lookup"><span data-stu-id="26f54-211">hello Logic App Designer adds an empty condition tooyour workflow, including action paths toofollow based whether hello condition is true or false.</span></span>

   ![空白條件](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-add-empty-condition.png)

2. <span data-ttu-id="26f54-213">在 hello**條件**方塊中，選擇**在進階模式中編輯**。</span><span class="sxs-lookup"><span data-stu-id="26f54-213">In hello **Condition** box, choose **Edit in advanced mode**.</span></span>
<span data-ttu-id="26f54-214">輸入此運算式：</span><span class="sxs-lookup"><span data-stu-id="26f54-214">Enter this expression:</span></span>

   `@equals(triggerBody()?['data']['operationName'], 'Microsoft.Compute/virtualMachines/write')`

   <span data-ttu-id="26f54-215">您的條件現在看起來就像下面這個範例︰</span><span class="sxs-lookup"><span data-stu-id="26f54-215">Your condition now looks like this example:</span></span>

   ![空白條件](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-expression.png)

   <span data-ttu-id="26f54-217">這個運算式會檢查 hello 事件`body`如`data`物件在 hello`operationName`屬性為 hello`Microsoft.Compute/virtualMachines/write`作業。</span><span class="sxs-lookup"><span data-stu-id="26f54-217">This expression checks hello event `body` for a `data` object where hello `operationName` property is hello `Microsoft.Compute/virtualMachines/write` operation.</span></span> 
   <span data-ttu-id="26f54-218">深入了解 [Event Grid 事件結構描述](../event-grid/event-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="26f54-218">Learn more about [Event Grid event schema](../event-grid/event-schema.md).</span></span>

3. <span data-ttu-id="26f54-219">tooprovide hello 條件的描述選擇 hello**省略符號**(**...**) 按鈕上 hello 條件 」 圖形，然後選擇**重新命名**。</span><span class="sxs-lookup"><span data-stu-id="26f54-219">tooprovide a description for hello condition, choose hello **ellipses** (**...**) button on hello condition shape, then choose **Rename**.</span></span>

   > [!NOTE] 
   > <span data-ttu-id="26f54-220">hello 稍後在本教學課程的範例也會提供描述 hello 邏輯應用程式工作流程中的步驟。</span><span class="sxs-lookup"><span data-stu-id="26f54-220">hello later examples in this tutorial also provide descriptions for steps in hello logic app workflow.</span></span>

4. <span data-ttu-id="26f54-221">現在選擇**在基本模式中編輯**以便 hello 運算式自動解決所示：</span><span class="sxs-lookup"><span data-stu-id="26f54-221">Now choose **Edit in basic mode** so that hello expression automatically resolves as shown:</span></span>

   ![邏輯應用程式條件](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-1.png)

5. <span data-ttu-id="26f54-223">儲存您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="26f54-223">Save your logic app.</span></span>

## <a name="send-email-when-your-virtual-machine-changes"></a><span data-ttu-id="26f54-224">在虛擬機器變更時傳送電子郵件</span><span class="sxs-lookup"><span data-stu-id="26f54-224">Send email when your virtual machine changes</span></span>

<span data-ttu-id="26f54-225">現在，加入[*動作*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)以便 hello 指定條件為 true 時，收到電子郵件。</span><span class="sxs-lookup"><span data-stu-id="26f54-225">Now add an [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) so that you get an email when hello specified condition is true.</span></span>

1. <span data-ttu-id="26f54-226">在 hello 條件**如果為 true**方塊中，選擇**將動作加入**。</span><span class="sxs-lookup"><span data-stu-id="26f54-226">In hello condition's **If true** box, choose **Add an action**.</span></span>

   ![新增條件為 true 時的動作](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-2.png)

2. <span data-ttu-id="26f54-228">在 hello 搜尋方塊中輸入"email"做為您的篩選器。</span><span class="sxs-lookup"><span data-stu-id="26f54-228">In hello search box, enter "email" as your filter.</span></span> <span data-ttu-id="26f54-229">根據您的電子郵件提供者，尋找並選取 hello 比對的連接器。</span><span class="sxs-lookup"><span data-stu-id="26f54-229">Based on your email provider, find and select hello matching connector.</span></span> <span data-ttu-id="26f54-230">然後選取您連接器的 hello 「 傳送電子郵件 」 動作。</span><span class="sxs-lookup"><span data-stu-id="26f54-230">Then select hello "send email" action for your connector.</span></span> <span data-ttu-id="26f54-231">例如：</span><span class="sxs-lookup"><span data-stu-id="26f54-231">For example:</span></span> 

   * <span data-ttu-id="26f54-232">Azure 工作或學校帳戶，請選取 hello Office 365 Outlook 連接器。</span><span class="sxs-lookup"><span data-stu-id="26f54-232">For an Azure work or school account, select hello Office 365 Outlook connector.</span></span> 
   * <span data-ttu-id="26f54-233">個人的 Microsoft 帳戶中，選取 hello Outlook.com 連接器。</span><span class="sxs-lookup"><span data-stu-id="26f54-233">For personal Microsoft accounts, select hello Outlook.com connector.</span></span> 
   * <span data-ttu-id="26f54-234">Gmail 帳戶選取 hello Gmail 連接器。</span><span class="sxs-lookup"><span data-stu-id="26f54-234">For Gmail accounts, select hello Gmail connector.</span></span> 

   <span data-ttu-id="26f54-235">我們 toocontinue 與 hello Office 365 Outlook 連接器。</span><span class="sxs-lookup"><span data-stu-id="26f54-235">We're going toocontinue with hello Office 365 Outlook connector.</span></span> 
   <span data-ttu-id="26f54-236">如果您使用不同的提供者，步驟的 hello hello 相同，但您的 UI 可能會出現不同。</span><span class="sxs-lookup"><span data-stu-id="26f54-236">If you use a different provider, hello steps remain hello same, but your UI might appear different.</span></span> 

   ![選取 [傳送電子郵件] 動作](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email.png)

3. <span data-ttu-id="26f54-238">如果您還沒有為電子郵件提供者連接，登入 tooyour 電子郵件帳戶時詢問您進行驗證。</span><span class="sxs-lookup"><span data-stu-id="26f54-238">If you don't already have a connection for your email provider, sign in tooyour email account when you're asked for authentication.</span></span>

4. <span data-ttu-id="26f54-239">Hello hello 下表中所指定的電子郵件中提供詳細資料：</span><span class="sxs-lookup"><span data-stu-id="26f54-239">Provide details for hello email as specified in hello following table:</span></span>

   ![空白的電子郵件動作](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-empty-email-action.png)

   > [!TIP]
   > <span data-ttu-id="26f54-241">從您的工作流程中可用的欄位 tooselect 按一下編輯方塊中因此該 hello**動態內容**清單隨即開啟，或選擇**加入動態內容**。</span><span class="sxs-lookup"><span data-stu-id="26f54-241">tooselect from fields available in your workflow, click in an edit box so that hello **Dynamic content** list opens, or choose **Add dynamic content**.</span></span> <span data-ttu-id="26f54-242">取得更多的欄位，選擇 **看到更多**hello 清單中每個區段。</span><span class="sxs-lookup"><span data-stu-id="26f54-242">For more fields, choose **See more** for each section in hello list.</span></span> <span data-ttu-id="26f54-243">tooclose hello**動態內容**清單中，選擇**加入動態內容**。</span><span class="sxs-lookup"><span data-stu-id="26f54-243">tooclose hello **Dynamic content** list, choose **Add dynamic content**.</span></span>

   | <span data-ttu-id="26f54-244">設定</span><span class="sxs-lookup"><span data-stu-id="26f54-244">Setting</span></span> | <span data-ttu-id="26f54-245">建議的值</span><span class="sxs-lookup"><span data-stu-id="26f54-245">Suggested value</span></span> | <span data-ttu-id="26f54-246">說明</span><span class="sxs-lookup"><span data-stu-id="26f54-246">Description</span></span> | 
   | ------- | --------------- | ----------- | 
   | <span data-ttu-id="26f54-247">**To**</span><span class="sxs-lookup"><span data-stu-id="26f54-247">**To**</span></span> | <span data-ttu-id="26f54-248">{recipient-email-address}</span><span class="sxs-lookup"><span data-stu-id="26f54-248">*{recipient-email-address}*</span></span> |<span data-ttu-id="26f54-249">輸入 hello 收件者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="26f54-249">Enter hello recipient's email address.</span></span> <span data-ttu-id="26f54-250">為了測試用途，您可以使用自己的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="26f54-250">For testing purposes, you can use your own email address.</span></span> | 
   | <span data-ttu-id="26f54-251">**主旨**</span><span class="sxs-lookup"><span data-stu-id="26f54-251">**Subject**</span></span> | <span data-ttu-id="26f54-252">更新的資源：**主旨**</span><span class="sxs-lookup"><span data-stu-id="26f54-252">Resource updated: **Subject**</span></span>| <span data-ttu-id="26f54-253">輸入 hello 電子郵件主旨 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="26f54-253">Enter hello content for hello email's subject.</span></span> <span data-ttu-id="26f54-254">此教學課程中，輸入 hello 建議的文字和選取 hello 事件**主旨**欄位。</span><span class="sxs-lookup"><span data-stu-id="26f54-254">For this tutorial, enter hello suggested text and select hello event's **Subject** field.</span></span> <span data-ttu-id="26f54-255">在這裡，您的電子郵件主旨包含 hello hello 更新資源 （虛擬機器） 的名稱。</span><span class="sxs-lookup"><span data-stu-id="26f54-255">Here, your email subject includes hello name for hello updated resource (virtual machine).</span></span> | 
   | <span data-ttu-id="26f54-256">**內文**</span><span class="sxs-lookup"><span data-stu-id="26f54-256">**Body**</span></span> | <span data-ttu-id="26f54-257">資源群組：**主題**</span><span class="sxs-lookup"><span data-stu-id="26f54-257">Resource group: **Topic**</span></span> <p><span data-ttu-id="26f54-258">事件類型：**事件類型**</span><span class="sxs-lookup"><span data-stu-id="26f54-258">Event type: **Event Type**</span></span><p><span data-ttu-id="26f54-259">事件識別碼：**識別碼**</span><span class="sxs-lookup"><span data-stu-id="26f54-259">Event ID: **ID**</span></span><p><span data-ttu-id="26f54-260">時間：**事件時間**</span><span class="sxs-lookup"><span data-stu-id="26f54-260">Time: **Event Time**</span></span> | <span data-ttu-id="26f54-261">輸入 hello 內容 hello 電子郵件內文。</span><span class="sxs-lookup"><span data-stu-id="26f54-261">Enter hello content for hello email's body.</span></span> <span data-ttu-id="26f54-262">此教學課程中，輸入 hello 建議的文字和選取 hello 事件**主題**，**事件類型**，**識別碼**，和**事件時間**欄位以便您的電子郵件包含 hello 資源群組名稱、 事件類型、 事件時間戳記，以及 hello 更新的事件識別碼。</span><span class="sxs-lookup"><span data-stu-id="26f54-262">For this tutorial, enter hello suggested text and select hello event's **Topic**, **Event Type**, **ID**, and **Event Time** fields so that your email includes hello resource group name, event type, event timestamp, and event ID for hello update.</span></span> <p><span data-ttu-id="26f54-263">tooadd 空白行，在您的內容，請按 Shift + Enter。</span><span class="sxs-lookup"><span data-stu-id="26f54-263">tooadd blank lines in your content, press Shift + Enter.</span></span> | 
   | | | 

   > [!NOTE] 
   > <span data-ttu-id="26f54-264">如果您選取的欄位，代表陣列，hello 設計工具會自動將加入**每個**參考 hello 陣列的 hello 動作的迴圈。</span><span class="sxs-lookup"><span data-stu-id="26f54-264">If you select a field that represents an array, hello designer automatically adds a **For each** loop around hello action that references hello array.</span></span> <span data-ttu-id="26f54-265">如此一來，應用程式邏輯會在每個陣列項目上執行該動作。</span><span class="sxs-lookup"><span data-stu-id="26f54-265">That way, your logic app performs that action on each array item.</span></span>

   <span data-ttu-id="26f54-266">現在，您的電子郵件動作看起來可能就像下面這個範例︰</span><span class="sxs-lookup"><span data-stu-id="26f54-266">Now, your email action might look like this example:</span></span>

   ![選取電子郵件中的輸出 tooinclude](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email-details.png)

   <span data-ttu-id="26f54-268">完成的邏輯應用程式可能如此範例所示︰</span><span class="sxs-lookup"><span data-stu-id="26f54-268">And your finished logic app might look like this example:</span></span>

   ![完成的邏輯應用程式](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-completed.png)

5. <span data-ttu-id="26f54-270">儲存您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="26f54-270">Save your logic app.</span></span> <span data-ttu-id="26f54-271">toocollapse] 和 [隱藏每個動作的詳細資料，在邏輯應用程式，然後選擇 hello 動作的標題列。</span><span class="sxs-lookup"><span data-stu-id="26f54-271">toocollapse and hide each action's details in your logic app, choose hello action's title bar.</span></span>

   ![儲存您的邏輯應用程式](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save-completed.png)

   <span data-ttu-id="26f54-273">邏輯應用程式現在是即時的但是會等候變更 tooyour 虛擬機器執行的任何項目之前。</span><span class="sxs-lookup"><span data-stu-id="26f54-273">Your logic app is now live, but waits for changes tooyour virtual machine before doing anything.</span></span> 
   <span data-ttu-id="26f54-274">tootest 邏輯應用程式現在繼續 toohello 下一節。</span><span class="sxs-lookup"><span data-stu-id="26f54-274">tootest your logic app now, continue toohello next section.</span></span>

## <a name="test-your-logic-app-workflow"></a><span data-ttu-id="26f54-275">測試邏輯應用程式工作流程</span><span class="sxs-lookup"><span data-stu-id="26f54-275">Test your logic app workflow</span></span>

1. <span data-ttu-id="26f54-276">邏輯應用程式即將 hello toocheck 指定事件，請更新您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="26f54-276">toocheck that your logic app is getting hello specified events, update your virtual machine.</span></span> 

   <span data-ttu-id="26f54-277">例如，您可以調整大小 hello Azure 入口網站中的虛擬機器或[調整您的 VM 使用 Azure PowerShell](../virtual-machines/windows/resize-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="26f54-277">For example, you can resize your virtual machine in hello Azure portal or [resize your VM with Azure PowerShell](../virtual-machines/windows/resize-vm.md).</span></span> 

   <span data-ttu-id="26f54-278">一會兒之後，您應可取得電子郵件。</span><span class="sxs-lookup"><span data-stu-id="26f54-278">After a few moments, you should get an email.</span></span> <span data-ttu-id="26f54-279">例如：</span><span class="sxs-lookup"><span data-stu-id="26f54-279">For example:</span></span>

   ![關於虛擬機器更新的電子郵件](./media/monitor-virtual-machine-changes-event-grid-logic-app/email.png)

2. <span data-ttu-id="26f54-281">tooreview hello 執行，並選擇邏輯應用程式，在邏輯應用程式功能表上的觸發程序記錄**概觀**。</span><span class="sxs-lookup"><span data-stu-id="26f54-281">tooreview hello runs and trigger history for your logic app, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="26f54-282">tooview 詳細執行中，在該回合的選擇 hello 資料列。</span><span class="sxs-lookup"><span data-stu-id="26f54-282">tooview more details about a run, choose hello row for that run.</span></span>

   ![邏輯應用程式執行記錄](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history.png)

3. <span data-ttu-id="26f54-284">tooview hello 輸入和輸出的每個步驟中，展開您想 tooreview hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="26f54-284">tooview hello inputs and outputs for each step, expand hello step that you want tooreview.</span></span> <span data-ttu-id="26f54-285">此資訊可協助您診斷和偵錯應用程式邏輯中的問題。</span><span class="sxs-lookup"><span data-stu-id="26f54-285">This information can help you diagnose and debug problems in your logic app.</span></span>
 
   ![邏輯應用程式執行記錄詳細資料](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history-details.png)

<span data-ttu-id="26f54-287">恭喜，您已建立並執行邏輯應用程式，該邏輯應用程式可透過 Event Grid 監視資源事件，以及在這些事件發生時監視電子郵件。</span><span class="sxs-lookup"><span data-stu-id="26f54-287">Congratulations, you've created and run a logic app that monitors resource events through an event grid and emails you when those events happen.</span></span> <span data-ttu-id="26f54-288">您也了解如何輕鬆地建立工作流程，以自動執行程序並整合系統與雲端服務。</span><span class="sxs-lookup"><span data-stu-id="26f54-288">You also learned how easily you can create workflows that automate processes and integrate systems and cloud services.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="26f54-289">清除資源</span><span class="sxs-lookup"><span data-stu-id="26f54-289">Clean up resources</span></span>

<span data-ttu-id="26f54-290">本教學課程使用會資源並執行會產生 Azure 訂用帳戶費用的動作。</span><span class="sxs-lookup"><span data-stu-id="26f54-290">This tutorial uses resources and performs actions that incur charges on your Azure subscription.</span></span> <span data-ttu-id="26f54-291">因此當您完成時的 hello 教學課程和測試，請確定您停用或刪除，您不想 tooincur 費用的任何資源。</span><span class="sxs-lookup"><span data-stu-id="26f54-291">So when you're done with hello tutorial and testing, make sure that you disable or delete any resources where you don't want tooincur charges.</span></span>

<span data-ttu-id="26f54-292">您可以停止執行，然後傳送電子郵件，而不刪除 hello 應用程式從應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="26f54-292">You can stop your logic app from running and sending email without deleting hello app.</span></span> <span data-ttu-id="26f54-293">在邏輯應用程式功能表上，選擇 [概觀]。</span><span class="sxs-lookup"><span data-stu-id="26f54-293">On your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="26f54-294">在 hello 工具列上選擇 **停用**。</span><span class="sxs-lookup"><span data-stu-id="26f54-294">On hello toolbar, choose **Disable**.</span></span>

![關閉應用程式邏輯](./media/monitor-virtual-machine-changes-event-grid-logic-app/turn-off-disable-logic-app.png)

## <a name="faq"></a><span data-ttu-id="26f54-296">常見問題集</span><span class="sxs-lookup"><span data-stu-id="26f54-296">FAQ</span></span>

<span data-ttu-id="26f54-297">**問：**：我可以使用 Event Grid 和邏輯應用程式執行其他哪些虛擬機器監視工作？</span><span class="sxs-lookup"><span data-stu-id="26f54-297">**Q**: What other virtual machine monitoring tasks can I perform with event grids and logic apps?</span></span> </br><span data-ttu-id="26f54-298">
**答**：您可以監視其他組態變更，例如：</span><span class="sxs-lookup"><span data-stu-id="26f54-298">
**A**: You can monitor other configuration changes, for example:</span></span>

* <span data-ttu-id="26f54-299">虛擬機器取得角色型存取控制 (RBAC) 權限。</span><span class="sxs-lookup"><span data-stu-id="26f54-299">A virtual machine gets role-based access control (RBAC) rights.</span></span>
* <span data-ttu-id="26f54-300">Tooa 網路安全性群組 (NSG) 上的網路介面 (NIC) 時，會進行變更。</span><span class="sxs-lookup"><span data-stu-id="26f54-300">Changes are made tooa network security group (NSG) on a network interface (NIC).</span></span>
* <span data-ttu-id="26f54-301">已新增或移除虛擬機器的磁碟。</span><span class="sxs-lookup"><span data-stu-id="26f54-301">Disks for a virtual machine are added or removed.</span></span>
* <span data-ttu-id="26f54-302">公用 IP 位址指派 tooa 虛擬機器 nic。</span><span class="sxs-lookup"><span data-stu-id="26f54-302">A public IP address is assigned tooa virtual machine NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26f54-303">後續步驟</span><span class="sxs-lookup"><span data-stu-id="26f54-303">Next steps</span></span>

* [<span data-ttu-id="26f54-304">Event Grid 概觀</span><span class="sxs-lookup"><span data-stu-id="26f54-304">Event Grid Overview</span></span>](../event-grid/overview.md)
* [<span data-ttu-id="26f54-305">Event Grid 概念</span><span class="sxs-lookup"><span data-stu-id="26f54-305">Event Grid Concepts</span></span>](../event-grid/concepts.md)
* [<span data-ttu-id="26f54-306">快速入門：使用 Event Grid 建立和路由傳送自訂事件</span><span class="sxs-lookup"><span data-stu-id="26f54-306">Quickstart: Create and route custom events with Event Grid</span></span>](../event-grid/custom-event-quickstart.md)
* [<span data-ttu-id="26f54-307">Event Grid 事件結構描述</span><span class="sxs-lookup"><span data-stu-id="26f54-307">Event Grid event schema</span></span>](../event-grid/event-schema.md)
* [<span data-ttu-id="26f54-308">Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="26f54-308">Azure Logic Apps</span></span>](../logic-apps/logic-apps-what-are-logic-apps.md)
* [<span data-ttu-id="26f54-309">使用預先定義的範本來建立邏輯應用程式工作流程</span><span class="sxs-lookup"><span data-stu-id="26f54-309">Create logic app workflows with predefined templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
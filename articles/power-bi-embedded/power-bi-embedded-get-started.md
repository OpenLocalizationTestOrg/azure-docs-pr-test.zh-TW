---
title: "開始使用 Microsoft Power BI Embedded"
description: "對於 Power BI Embedded，將互動式 Power BI 報告加入至您的商務智慧應用程式"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 4afa8d2c7f8ec1942521ba5fa131967dfd581c91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a><span data-ttu-id="b02c4-103">開始使用 Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="b02c4-103">Get started with Microsoft Power BI Embedded</span></span>

<span data-ttu-id="b02c4-104">**Power BI Embedded** 是一項 Azure 服務，可讓應用程式開發人員將互動式 Power BI 報告加入至自己的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b02c4-104">**Power BI Embedded** is an Azure service that enables application developers to add interactive Power BI reports into their own applications.</span></span> <span data-ttu-id="b02c4-105">**Power BI Embedded** 會與現有的應用程式一同運作，而不需要重新設計或變更使用者登入的方式。</span><span class="sxs-lookup"><span data-stu-id="b02c4-105">**Power BI Embedded** works with existing applications without needing redesign or changing the way users sign in.</span></span>

<span data-ttu-id="b02c4-106">**Microsoft Power BI Embedded** 的資源也是透過 [Azure ARM API](https://msdn.microsoft.com/library/mt712306.aspx)佈建。</span><span class="sxs-lookup"><span data-stu-id="b02c4-106">Resources for **Microsoft Power BI Embedded** are provisioned through the [Azure ARM APIs](https://msdn.microsoft.com/library/mt712306.aspx).</span></span> <span data-ttu-id="b02c4-107">在此情況下，您佈建的資源是 **Power BI 工作區集合**。</span><span class="sxs-lookup"><span data-stu-id="b02c4-107">In this case, the resource you provision is a **Power BI Workspace Collection**.</span></span>

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a><span data-ttu-id="b02c4-108">建立工作區集合</span><span class="sxs-lookup"><span data-stu-id="b02c4-108">Create a workspace collection</span></span>

<span data-ttu-id="b02c4-109">**工作區集合** 是最上層的 Azure 資源，而內容的容器將會內嵌在您的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="b02c4-109">A **Workspace Collection** is the top-level Azure resource and a container for the content that will be embedded in your application.</span></span> <span data-ttu-id="b02c4-110">建立 **工作區集合** 的方式有兩種︰</span><span class="sxs-lookup"><span data-stu-id="b02c4-110">A **Workspace Collection** can be created in two ways::</span></span>

* <span data-ttu-id="b02c4-111">以手動方式使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b02c4-111">Manually using the Azure Portal</span></span>
* <span data-ttu-id="b02c4-112">以程式設計方式使用 Azure Resource Manager (ARM) API</span><span class="sxs-lookup"><span data-stu-id="b02c4-112">Programmatically using the Azure Resource Manager(ARM) APIs</span></span>

<span data-ttu-id="b02c4-113">讓我們逐步解說使用 Azure 入口網站建立 **工作區集合** 的步驟。</span><span class="sxs-lookup"><span data-stu-id="b02c4-113">Let's walk through the steps to build a **Workspace Collection** using the Azure Portal.</span></span>

1. <span data-ttu-id="b02c4-114">開啟並登入 **Azure 入口網站**： [http://portal.azure.com](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b02c4-114">Open and sign into **Azure Portal**: [http://portal.azure.com](http://portal.azure.com).</span></span>
2. <span data-ttu-id="b02c4-115">按一下頂端面板上的 [+ 新增]  。</span><span class="sxs-lookup"><span data-stu-id="b02c4-115">Click **+ New** on the top panel.</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. <span data-ttu-id="b02c4-116">按一下 [資料 + 分析] 之下的 [Power BI Embedded]。</span><span class="sxs-lookup"><span data-stu-id="b02c4-116">Under **Data + Analytics** click **Power BI Embedded**.</span></span>
4. <span data-ttu-id="b02c4-117">在 [工作區集合] 刀鋒視窗上輸入必要資訊。</span><span class="sxs-lookup"><span data-stu-id="b02c4-117">On the **Workspace Collection Blade**, enter the required information.</span></span> <span data-ttu-id="b02c4-118">如需**價格**，請參閱 [Power BI Embedded 價格](http://go.microsoft.com/fwlink/?LinkID=760527)。</span><span class="sxs-lookup"><span data-stu-id="b02c4-118">For **Pricing**, see [Power BI Embedded pricing](http://go.microsoft.com/fwlink/?LinkID=760527).</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. <span data-ttu-id="b02c4-119">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b02c4-119">Click **Create**.</span></span>

<span data-ttu-id="b02c4-120">**工作區集合** 會花費一些時間來佈建。</span><span class="sxs-lookup"><span data-stu-id="b02c4-120">The **Workspace Collection** will take a few moments to provision.</span></span> <span data-ttu-id="b02c4-121">完成後，您將會進入 [工作區集合刀鋒視窗] 。</span><span class="sxs-lookup"><span data-stu-id="b02c4-121">When completed, you'll be taken to the **Workspace Collection Blade**.</span></span>

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

<span data-ttu-id="b02c4-122">[建立刀鋒視窗]  包含呼叫 API 所需的資訊，以建立工作區並將內容部署到這些工作區。</span><span class="sxs-lookup"><span data-stu-id="b02c4-122">The **Creation Blade** contains the information you need to call the APIs that create workspaces and deploy content to them.</span></span>

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a><span data-ttu-id="b02c4-123">檢視 Power BI API 存取金鑰</span><span class="sxs-lookup"><span data-stu-id="b02c4-123">View Power BI API access keys</span></span>

<span data-ttu-id="b02c4-124">呼叫 Power BI REST API 所需的其中一項最重要資訊是**存取金鑰**。</span><span class="sxs-lookup"><span data-stu-id="b02c4-124">One of the most important pieces of information needed to call the Power BI REST APIs are the **Access Keys**.</span></span> <span data-ttu-id="b02c4-125">這些存取金鑰用來產生**應用程式權杖**，而這些權杖用來驗證 API 要求。</span><span class="sxs-lookup"><span data-stu-id="b02c4-125">These are used to generate the **app tokens** that are used to authenticate your API requests.</span></span> <span data-ttu-id="b02c4-126">若要檢視您的**存取金鑰**，請按一下 [設定刀鋒視窗] 上的 [存取金鑰]。</span><span class="sxs-lookup"><span data-stu-id="b02c4-126">To view your **Access Keys**, click **Access Keys** on the **Settings Blade**.</span></span> <span data-ttu-id="b02c4-127">若要深入了解**應用程式權杖**，請參閱 [使用 Power BI Embedded 驗證和授權](power-bi-embedded-app-token-flow.md)。</span><span class="sxs-lookup"><span data-stu-id="b02c4-127">For more about **app tokens**, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

   ![](media/power-bi-embedded-get-started/access-keys.png)

<span data-ttu-id="b02c4-128">您會發現您有兩個金鑰。</span><span class="sxs-lookup"><span data-stu-id="b02c4-128">You'll'notice that you have two keys.</span></span>

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

<span data-ttu-id="b02c4-129">複製這些金鑰並將它們安全地儲存在您的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="b02c4-129">Copy these keys and store them securely in your application.</span></span> <span data-ttu-id="b02c4-130">請務必如同密碼一樣處理這些金鑰，因為這些金鑰可供存取您的 **工作區集合**中的所有內容。</span><span class="sxs-lookup"><span data-stu-id="b02c4-130">It's very important that you treat these keys as you would a password, because they'll provide access to all the content in your **Workspace Collection**.</span></span>

<span data-ttu-id="b02c4-131">雖已列出兩個金鑰，但特定時間只需要一個金鑰。</span><span class="sxs-lookup"><span data-stu-id="b02c4-131">While two keys are listed, only one key is needed at a particular time.</span></span> <span data-ttu-id="b02c4-132">系統會提供第二個金鑰，以便您定期重新產生金鑰，而不需中斷對服務的存取。</span><span class="sxs-lookup"><span data-stu-id="b02c4-132">The second key is provided so you can periodically regenerate keys without interrupting access to the service.</span></span>

<span data-ttu-id="b02c4-133">您現在已有應用程式的 Power BI 執行個體以及 **存取金鑰**，您可以將報告匯入自己的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="b02c4-133">Now that you have an instance of Power BI for your application, and **Access Keys**, you can import a report into your own app.</span></span> <span data-ttu-id="b02c4-134">在了解如何匯入報告之前，下一節說明如何建立要內嵌到應用程式中的 Power BI 資料集和報告。</span><span class="sxs-lookup"><span data-stu-id="b02c4-134">Before you learn how to import a report, the next section describes creating Power BI datasets and reports to embed into an app.</span></span>

## <a name="working-with-workspaces"></a><span data-ttu-id="b02c4-135">使用工作區</span><span class="sxs-lookup"><span data-stu-id="b02c4-135">Working with workspaces</span></span>

<span data-ttu-id="b02c4-136">建立工作區集合之後，您必須建立將存放報告和資料集的工作區。</span><span class="sxs-lookup"><span data-stu-id="b02c4-136">After you have created your workspace collection, you will need to create a workspace that will house your reports and datasets.</span></span> <span data-ttu-id="b02c4-137">若要建立工作區，您必須使用 [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b02c4-137">To create a workspace, you will need to use the [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-to-embed-into-an-app-using-power-bi-desktop"></a><span data-ttu-id="b02c4-138">使用 Power BI Desktop 建立要內嵌到應用程式中的 Power BI 資料集和報告</span><span class="sxs-lookup"><span data-stu-id="b02c4-138">Create Power BI datasets and reports to embed into an app using Power BI Desktop</span></span>

<span data-ttu-id="b02c4-139">您現已為您的應用程式建立 Power BI 執行個體，而且有 **存取金鑰**，您必須建立想要內嵌的 Power BI 資料集和報告。</span><span class="sxs-lookup"><span data-stu-id="b02c4-139">Now that you have created an instance of Power BI for your application, and have **Access Keys**, you will need to create the Power BI datasets and reports that you want to embed.</span></span> <span data-ttu-id="b02c4-140">使用 **Power BI Desktop**可以建立資料集和報告。</span><span class="sxs-lookup"><span data-stu-id="b02c4-140">Datasets and reports can be created by using **Power BI Desktop**.</span></span> <span data-ttu-id="b02c4-141">您可以下載 [免費的 Power BI Desktop](https://go.microsoft.com/fwlink/?LinkId=521662)。</span><span class="sxs-lookup"><span data-stu-id="b02c4-141">You can download [Power BI Desktop for free](https://go.microsoft.com/fwlink/?LinkId=521662).</span></span> <span data-ttu-id="b02c4-142">或者，若要快速開始，您可以下載 [零售分析範例 PBIX](http://go.microsoft.com/fwlink/?LinkID=780547)。</span><span class="sxs-lookup"><span data-stu-id="b02c4-142">Or, to quickly get started, you can download the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>

> [!NOTE]
> <span data-ttu-id="b02c4-143">若要深入了解如何使用 **Power BI Desktop**，請參閱[開始使用 Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop)。</span><span class="sxs-lookup"><span data-stu-id="b02c4-143">To learn more about how to use **Power BI Desktop**, see [Getting Started with Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span></span>

<span data-ttu-id="b02c4-144">透過 **Power BI Desktop**，將資料複本匯入 **Power BI Desktop** 或使用 **DirectQuery** 直接連接到資料來源，即可連接到資料來源。</span><span class="sxs-lookup"><span data-stu-id="b02c4-144">With **Power BI Desktop**, you connect to your data source by importing a copy of the data into **Power BI Desktop** or connecting directly to the data source using **DirectQuery**.</span></span>

<span data-ttu-id="b02c4-145">以下是使用 **Import** 和 **DirectQuery** 之間的差異。</span><span class="sxs-lookup"><span data-stu-id="b02c4-145">Here are the differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="b02c4-146">Import</span><span class="sxs-lookup"><span data-stu-id="b02c4-146">Import</span></span> | <span data-ttu-id="b02c4-147">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="b02c4-147">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="b02c4-148">資料表、資料行和資料  會匯入或複製到 **Power BI Desktop**中。</span><span class="sxs-lookup"><span data-stu-id="b02c4-148">Tables, columns, *and data* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="b02c4-149">當您使用視覺效果時， **Power BI Desktop** 會查詢資料的複本。</span><span class="sxs-lookup"><span data-stu-id="b02c4-149">As you work with visualizations, **Power BI Desktop** queries a copy of the data.</span></span> <span data-ttu-id="b02c4-150">若要查看基礎資料所發生的任何變更，您必須重新整理或再次匯入完整的目前資料集。</span><span class="sxs-lookup"><span data-stu-id="b02c4-150">To see any changes that occurred to the underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="b02c4-151">只有資料表和資料行  會匯入或複製到 **Power BI Desktop**中。</span><span class="sxs-lookup"><span data-stu-id="b02c4-151">Only *tables and columns* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="b02c4-152">當您使用視覺效果時， **Power BI Desktop** 會查詢基礎資料來源，這表示您一直在檢視目前的資料。</span><span class="sxs-lookup"><span data-stu-id="b02c4-152">As you work with visualizations, **Power BI Desktop** queries the underlying data source, which means you're always viewing current data.</span></span> |

<span data-ttu-id="b02c4-153">如需有關連接到資料來源的詳細資訊，請參閱 [連接到資料來源](power-bi-embedded-connect-datasource.md)。</span><span class="sxs-lookup"><span data-stu-id="b02c4-153">For more about connecting to a data source, see [Connect to a data source](power-bi-embedded-connect-datasource.md).</span></span>

<span data-ttu-id="b02c4-154">在 **Power BI Desktop**中儲存您的工作之後，會建立一個 PBIX 檔案。</span><span class="sxs-lookup"><span data-stu-id="b02c4-154">After you save your work in **Power BI Desktop**, a PBIX file is created.</span></span> <span data-ttu-id="b02c4-155">此檔案包含您的報告。</span><span class="sxs-lookup"><span data-stu-id="b02c4-155">This file contains your report.</span></span> <span data-ttu-id="b02c4-156">此外，如果您匯入資料，則 PBIX 會包含完整的資料集，或如果您使用 **DirectQuery**，則 PBIX 只包含資料集結構描述。</span><span class="sxs-lookup"><span data-stu-id="b02c4-156">In addition, if you import data the PBIX contains the complete dataset, or if you use **DirectQuery**, the PBIX contains just a dataset schema.</span></span> <span data-ttu-id="b02c4-157">您會使用 [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx)，以程式設計方式將 PBIX 部署到您工作區。</span><span class="sxs-lookup"><span data-stu-id="b02c4-157">You programmatically deploy the PBIX into your workspace using the [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="b02c4-158">**Power BI Embedded** 有其他 API 可變更您的資料集所指向的伺服器和資料庫，以及設定資料集將用來連接到您的資料庫的服務帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="b02c4-158">**Power BI Embedded** has additional APIs to change the server and database that your dataset is pointing to and set a service account credential that the dataset will use to connect to your database.</span></span> <span data-ttu-id="b02c4-159">請參閱 [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) 和 [Patch 閘道資料來源](https://msdn.microsoft.com/library/mt711498.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b02c4-159">See [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) and [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-using-apis"></a><span data-ttu-id="b02c4-160">使用 API 建立 Power BI 資料集和報告</span><span class="sxs-lookup"><span data-stu-id="b02c4-160">Create Power BI datasets and reports using APIs</span></span>

### <a name="datsets"></a><span data-ttu-id="b02c4-161">資料集</span><span class="sxs-lookup"><span data-stu-id="b02c4-161">Datsets</span></span>

<span data-ttu-id="b02c4-162">您可以使用 REST API 在 Power BI Embedded 內建立資料集。</span><span class="sxs-lookup"><span data-stu-id="b02c4-162">You can create datasets within Power BI Embedded using the REST API.</span></span> <span data-ttu-id="b02c4-163">接著，將資料推送至資料集。</span><span class="sxs-lookup"><span data-stu-id="b02c4-163">You can then push data into your dataset.</span></span> <span data-ttu-id="b02c4-164">這可讓您不需要 Power BI Desktop 即可處理資料。</span><span class="sxs-lookup"><span data-stu-id="b02c4-164">This allows you to work with data without the need of Power BI Desktop.</span></span> <span data-ttu-id="b02c4-165">如需詳細資訊，請參閱[公佈資料集](https://msdn.microsoft.com/library/azure/mt778875.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b02c4-165">For more information, see [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span></span>

### <a name="reports"></a><span data-ttu-id="b02c4-166">報告</span><span class="sxs-lookup"><span data-stu-id="b02c4-166">Reports</span></span>

<span data-ttu-id="b02c4-167">您可以使用 JavaScript API，直接在應用程式中從資料集建立報告。</span><span class="sxs-lookup"><span data-stu-id="b02c4-167">You can create a report from a dataset directly in your application using the JavaScript API.</span></span> <span data-ttu-id="b02c4-168">如需詳細資訊，請參閱[在 Power BI Embedded 中從資料集建立新的報告](power-bi-embedded-create-report-from-dataset.md)。</span><span class="sxs-lookup"><span data-stu-id="b02c4-168">For more information, see [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="b02c4-169">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b02c4-169">See Also</span></span>

[<span data-ttu-id="b02c4-170">開始使用範例</span><span class="sxs-lookup"><span data-stu-id="b02c4-170">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="b02c4-171">在 Power BI Embedded 中驗證和授權</span><span class="sxs-lookup"><span data-stu-id="b02c4-171">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="b02c4-172">內嵌報告</span><span class="sxs-lookup"><span data-stu-id="b02c4-172">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
<span data-ttu-id="b02c4-173">[在 Power BI Embedded 中從資料集建立新的報告](power-bi-embedded-create-report-from-dataset.md)
[儲存報告](power-bi-embedded-save-reports.md)</span><span class="sxs-lookup"><span data-stu-id="b02c4-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Save reports](power-bi-embedded-save-reports.md)</span></span>  
[<span data-ttu-id="b02c4-174">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="b02c4-174">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="b02c4-175">JavaScript 內嵌範例</span><span class="sxs-lookup"><span data-stu-id="b02c4-175">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="b02c4-176">有其他疑問？</span><span class="sxs-lookup"><span data-stu-id="b02c4-176">More questions?</span></span> [<span data-ttu-id="b02c4-177">試用 Power BI 社群</span><span class="sxs-lookup"><span data-stu-id="b02c4-177">Try the Power BI Community</span></span>](http://community.powerbi.com/)


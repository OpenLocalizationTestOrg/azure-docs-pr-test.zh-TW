---
title: "開始使用 Microsoft Power BI Embedded aaaGet"
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
ms.openlocfilehash: ebb550cb4eba761dde3c23e4dd0314fc885817e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a><span data-ttu-id="04cb4-103">開始使用 Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="04cb4-103">Get started with Microsoft Power BI Embedded</span></span>

<span data-ttu-id="04cb4-104">**Power BI Embedded**互動式 Power BI 報表到其自身應用程式，可讓應用程式開發人員 tooadd 是一項 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="04cb4-104">**Power BI Embedded** is an Azure service that enables application developers tooadd interactive Power BI reports into their own applications.</span></span> <span data-ttu-id="04cb4-105">**Power BI Embedded**可搭配現有的應用程式，而不需要重新設計，或變更 hello 方式使用者登入。</span><span class="sxs-lookup"><span data-stu-id="04cb4-105">**Power BI Embedded** works with existing applications without needing redesign or changing hello way users sign in.</span></span>

<span data-ttu-id="04cb4-106">資源**Microsoft Power BI Embedded**經由 hello [Azure ARM Api](https://msdn.microsoft.com/library/mt712306.aspx)。</span><span class="sxs-lookup"><span data-stu-id="04cb4-106">Resources for **Microsoft Power BI Embedded** are provisioned through hello [Azure ARM APIs](https://msdn.microsoft.com/library/mt712306.aspx).</span></span> <span data-ttu-id="04cb4-107">在此情況下，您佈建的 hello 資源是**Power BI 工作區集合**。</span><span class="sxs-lookup"><span data-stu-id="04cb4-107">In this case, hello resource you provision is a **Power BI Workspace Collection**.</span></span>

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a><span data-ttu-id="04cb4-108">建立工作區集合</span><span class="sxs-lookup"><span data-stu-id="04cb4-108">Create a workspace collection</span></span>

<span data-ttu-id="04cb4-109">A**工作區集合**是 hello 最上層的 Azure 資源和會內嵌在應用程式中的 hello 內容的容器。</span><span class="sxs-lookup"><span data-stu-id="04cb4-109">A **Workspace Collection** is hello top-level Azure resource and a container for hello content that will be embedded in your application.</span></span> <span data-ttu-id="04cb4-110">建立 **工作區集合** 的方式有兩種︰</span><span class="sxs-lookup"><span data-stu-id="04cb4-110">A **Workspace Collection** can be created in two ways::</span></span>

* <span data-ttu-id="04cb4-111">使用手動 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="04cb4-111">Manually using hello Azure Portal</span></span>
* <span data-ttu-id="04cb4-112">以程式設計方式使用 hello Azure 資源 Manager(ARM) Api</span><span class="sxs-lookup"><span data-stu-id="04cb4-112">Programmatically using hello Azure Resource Manager(ARM) APIs</span></span>

<span data-ttu-id="04cb4-113">讓我們逐步解說 hello 步驟 toobuild**工作區集合**使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="04cb4-113">Let's walk through hello steps toobuild a **Workspace Collection** using hello Azure Portal.</span></span>

1. <span data-ttu-id="04cb4-114">開啟並登入 **Azure 入口網站**： [http://portal.azure.com](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="04cb4-114">Open and sign into **Azure Portal**: [http://portal.azure.com](http://portal.azure.com).</span></span>
2. <span data-ttu-id="04cb4-115">按一下**+ 新增**hello 上方面板上。</span><span class="sxs-lookup"><span data-stu-id="04cb4-115">Click **+ New** on hello top panel.</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. <span data-ttu-id="04cb4-116">按一下 [資料 + 分析] 之下的 [Power BI Embedded]。</span><span class="sxs-lookup"><span data-stu-id="04cb4-116">Under **Data + Analytics** click **Power BI Embedded**.</span></span>
4. <span data-ttu-id="04cb4-117">在 hello**刀鋒視窗中的工作區集合**，輸入 hello 所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="04cb4-117">On hello **Workspace Collection Blade**, enter hello required information.</span></span> <span data-ttu-id="04cb4-118">如需**價格**，請參閱 [Power BI Embedded 價格](http://go.microsoft.com/fwlink/?LinkID=760527)。</span><span class="sxs-lookup"><span data-stu-id="04cb4-118">For **Pricing**, see [Power BI Embedded pricing](http://go.microsoft.com/fwlink/?LinkID=760527).</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. <span data-ttu-id="04cb4-119">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="04cb4-119">Click **Create**.</span></span>

<span data-ttu-id="04cb4-120">hello**工作區集合**需要幾分鐘的時間 tooprovision。</span><span class="sxs-lookup"><span data-stu-id="04cb4-120">hello **Workspace Collection** will take a few moments tooprovision.</span></span> <span data-ttu-id="04cb4-121">完成時，您將會進入 toohello**刀鋒視窗中的工作區集合**。</span><span class="sxs-lookup"><span data-stu-id="04cb4-121">When completed, you'll be taken toohello **Workspace Collection Blade**.</span></span>

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

<span data-ttu-id="04cb4-122">hello**刀鋒視窗中建立**包含需要 toocall hello Api，建立工作區和部署內容 toothem hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="04cb4-122">hello **Creation Blade** contains hello information you need toocall hello APIs that create workspaces and deploy content toothem.</span></span>

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a><span data-ttu-id="04cb4-123">檢視 Power BI API 存取金鑰</span><span class="sxs-lookup"><span data-stu-id="04cb4-123">View Power BI API access keys</span></span>

<span data-ttu-id="04cb4-124">其中一個最重要的部分所需的資訊 toocall hello Power BI REST Api 的 hello 是 hello**便捷鍵**。</span><span class="sxs-lookup"><span data-stu-id="04cb4-124">One of hello most important pieces of information needed toocall hello Power BI REST APIs are hello **Access Keys**.</span></span> <span data-ttu-id="04cb4-125">這些是使用的 toogenerate hello**應用程式權杖**所使用的 tooauthenticate API 要求。</span><span class="sxs-lookup"><span data-stu-id="04cb4-125">These are used toogenerate hello **app tokens** that are used tooauthenticate your API requests.</span></span> <span data-ttu-id="04cb4-126">tooview 您**便捷鍵**，按一下 [**便捷鍵**上 hello**設定] 刀鋒視窗**。</span><span class="sxs-lookup"><span data-stu-id="04cb4-126">tooview your **Access Keys**, click **Access Keys** on hello **Settings Blade**.</span></span> <span data-ttu-id="04cb4-127">若要深入了解**應用程式權杖**，請參閱 [使用 Power BI Embedded 驗證和授權](power-bi-embedded-app-token-flow.md)。</span><span class="sxs-lookup"><span data-stu-id="04cb4-127">For more about **app tokens**, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

   ![](media/power-bi-embedded-get-started/access-keys.png)

<span data-ttu-id="04cb4-128">您會發現您有兩個金鑰。</span><span class="sxs-lookup"><span data-stu-id="04cb4-128">You'll'notice that you have two keys.</span></span>

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

<span data-ttu-id="04cb4-129">複製這些金鑰並將它們安全地儲存在您的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="04cb4-129">Copy these keys and store them securely in your application.</span></span> <span data-ttu-id="04cb4-130">它是非常重要，您這些機碼平常一樣處理密碼，因為它們會提供存取 tooall hello 內容，在您**工作區集合**。</span><span class="sxs-lookup"><span data-stu-id="04cb4-130">It's very important that you treat these keys as you would a password, because they'll provide access tooall hello content in your **Workspace Collection**.</span></span>

<span data-ttu-id="04cb4-131">雖已列出兩個金鑰，但特定時間只需要一個金鑰。</span><span class="sxs-lookup"><span data-stu-id="04cb4-131">While two keys are listed, only one key is needed at a particular time.</span></span> <span data-ttu-id="04cb4-132">hello 第二個主要被為了讓您可以不需中斷存取 toohello 服務會定期重新產生金鑰。</span><span class="sxs-lookup"><span data-stu-id="04cb4-132">hello second key is provided so you can periodically regenerate keys without interrupting access toohello service.</span></span>

<span data-ttu-id="04cb4-133">您現在已有應用程式的 Power BI 執行個體以及 **存取金鑰**，您可以將報告匯入自己的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="04cb4-133">Now that you have an instance of Power BI for your application, and **Access Keys**, you can import a report into your own app.</span></span> <span data-ttu-id="04cb4-134">之前，您學習如何 tooimport 的報表，hello 下一節會說明建立 Power BI 資料集和報表 tooembed 到應用程式。</span><span class="sxs-lookup"><span data-stu-id="04cb4-134">Before you learn how tooimport a report, hello next section describes creating Power BI datasets and reports tooembed into an app.</span></span>

## <a name="working-with-workspaces"></a><span data-ttu-id="04cb4-135">使用工作區</span><span class="sxs-lookup"><span data-stu-id="04cb4-135">Working with workspaces</span></span>

<span data-ttu-id="04cb4-136">建立您的工作區集合之後，您將需要 toocreate 將裝載您的報表和資料集的工作區。</span><span class="sxs-lookup"><span data-stu-id="04cb4-136">After you have created your workspace collection, you will need toocreate a workspace that will house your reports and datasets.</span></span> <span data-ttu-id="04cb4-137">toocreate 工作區，您將需要 toouse hello [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx)。</span><span class="sxs-lookup"><span data-stu-id="04cb4-137">toocreate a workspace, you will need toouse hello [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-tooembed-into-an-app-using-power-bi-desktop"></a><span data-ttu-id="04cb4-138">建立 Power BI 資料集和報表 tooembed 到應用程式中使用 Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="04cb4-138">Create Power BI datasets and reports tooembed into an app using Power BI Desktop</span></span>

<span data-ttu-id="04cb4-139">既然您已經建立您的應用程式的 Power BI 執行個體，且有**便捷鍵**，您將需要 toocreate hello Power BI 資料集和您想 tooembed 的報表。</span><span class="sxs-lookup"><span data-stu-id="04cb4-139">Now that you have created an instance of Power BI for your application, and have **Access Keys**, you will need toocreate hello Power BI datasets and reports that you want tooembed.</span></span> <span data-ttu-id="04cb4-140">使用 **Power BI Desktop**可以建立資料集和報告。</span><span class="sxs-lookup"><span data-stu-id="04cb4-140">Datasets and reports can be created by using **Power BI Desktop**.</span></span> <span data-ttu-id="04cb4-141">您可以下載 [免費的 Power BI Desktop](https://go.microsoft.com/fwlink/?LinkId=521662)。</span><span class="sxs-lookup"><span data-stu-id="04cb4-141">You can download [Power BI Desktop for free](https://go.microsoft.com/fwlink/?LinkId=521662).</span></span> <span data-ttu-id="04cb4-142">或者，tooquickly 開始，您可以下載 hello[零售分析範例 PBIX](http://go.microsoft.com/fwlink/?LinkID=780547)。</span><span class="sxs-lookup"><span data-stu-id="04cb4-142">Or, tooquickly get started, you can download hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>

> [!NOTE]
> <span data-ttu-id="04cb4-143">深入了解如何 toolearn toouse **Power BI Desktop**，請參閱[開始使用 Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop)。</span><span class="sxs-lookup"><span data-stu-id="04cb4-143">toolearn more about how toouse **Power BI Desktop**, see [Getting Started with Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span></span>

<span data-ttu-id="04cb4-144">與**Power BI Desktop**，您藉由匯入到 hello 資料的複本連接 tooyour 資料來源**Power BI Desktop**或直接連接 toohello 資料來源使用**DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="04cb4-144">With **Power BI Desktop**, you connect tooyour data source by importing a copy of hello data into **Power BI Desktop** or connecting directly toohello data source using **DirectQuery**.</span></span>

<span data-ttu-id="04cb4-145">以下是使用的 hello 差異**匯入**和**DirectQuery**。</span><span class="sxs-lookup"><span data-stu-id="04cb4-145">Here are hello differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="04cb4-146">Import</span><span class="sxs-lookup"><span data-stu-id="04cb4-146">Import</span></span> | <span data-ttu-id="04cb4-147">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="04cb4-147">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="04cb4-148">資料表、資料行和資料  會匯入或複製到 **Power BI Desktop**中。</span><span class="sxs-lookup"><span data-stu-id="04cb4-148">Tables, columns, *and data* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="04cb4-149">當您使用的視覺效果， **Power BI Desktop**查詢 hello 資料的複本。</span><span class="sxs-lookup"><span data-stu-id="04cb4-149">As you work with visualizations, **Power BI Desktop** queries a copy of hello data.</span></span> <span data-ttu-id="04cb4-150">toosee 發生的 toohello 基礎資料的任何變更，您必須重新整理，或匯入完成，目前資料集一次。</span><span class="sxs-lookup"><span data-stu-id="04cb4-150">toosee any changes that occurred toohello underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="04cb4-151">只有資料表和資料行  會匯入或複製到 **Power BI Desktop**中。</span><span class="sxs-lookup"><span data-stu-id="04cb4-151">Only *tables and columns* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="04cb4-152">當您使用的視覺效果， **Power BI Desktop**查詢 hello 基礎資料來源，這表示您一定要檢視目前的資料。</span><span class="sxs-lookup"><span data-stu-id="04cb4-152">As you work with visualizations, **Power BI Desktop** queries hello underlying data source, which means you're always viewing current data.</span></span> |

<span data-ttu-id="04cb4-153">如需有關連接 tooa 資料來源，請參閱[連接 tooa 資料來源](power-bi-embedded-connect-datasource.md)。</span><span class="sxs-lookup"><span data-stu-id="04cb4-153">For more about connecting tooa data source, see [Connect tooa data source](power-bi-embedded-connect-datasource.md).</span></span>

<span data-ttu-id="04cb4-154">在 **Power BI Desktop**中儲存您的工作之後，會建立一個 PBIX 檔案。</span><span class="sxs-lookup"><span data-stu-id="04cb4-154">After you save your work in **Power BI Desktop**, a PBIX file is created.</span></span> <span data-ttu-id="04cb4-155">此檔案包含您的報告。</span><span class="sxs-lookup"><span data-stu-id="04cb4-155">This file contains your report.</span></span> <span data-ttu-id="04cb4-156">此外，如果您匯入資料 hello PBIX 包含 hello 完整資料集，或如果您使用**DirectQuery**，hello PBIX 包含只資料集的結構描述。</span><span class="sxs-lookup"><span data-stu-id="04cb4-156">In addition, if you import data hello PBIX contains hello complete dataset, or if you use **DirectQuery**, hello PBIX contains just a dataset schema.</span></span> <span data-ttu-id="04cb4-157">您以程式設計方式部署到您工作區中使用 hello hello PBIX [Power BI 匯入 API](https://msdn.microsoft.com/library/mt711504.aspx)。</span><span class="sxs-lookup"><span data-stu-id="04cb4-157">You programmatically deploy hello PBIX into your workspace using hello [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="04cb4-158">**Power BI Embedded**有其他應用程式開發介面 toochange hello 伺服器和資料庫，您的資料集指 tooand 組 hello 資料集的服務帳戶認證將會使用 tooconnect tooyour 資料庫。</span><span class="sxs-lookup"><span data-stu-id="04cb4-158">**Power BI Embedded** has additional APIs toochange hello server and database that your dataset is pointing tooand set a service account credential that hello dataset will use tooconnect tooyour database.</span></span> <span data-ttu-id="04cb4-159">請參閱 [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) 和 [Patch 閘道資料來源](https://msdn.microsoft.com/library/mt711498.aspx)。</span><span class="sxs-lookup"><span data-stu-id="04cb4-159">See [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) and [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-using-apis"></a><span data-ttu-id="04cb4-160">使用 API 建立 Power BI 資料集和報告</span><span class="sxs-lookup"><span data-stu-id="04cb4-160">Create Power BI datasets and reports using APIs</span></span>

### <a name="datsets"></a><span data-ttu-id="04cb4-161">資料集</span><span class="sxs-lookup"><span data-stu-id="04cb4-161">Datsets</span></span>

<span data-ttu-id="04cb4-162">您可以建立 Power BI Embedded 使用 hello REST API 資料集。</span><span class="sxs-lookup"><span data-stu-id="04cb4-162">You can create datasets within Power BI Embedded using hello REST API.</span></span> <span data-ttu-id="04cb4-163">接著，將資料推送至資料集。</span><span class="sxs-lookup"><span data-stu-id="04cb4-163">You can then push data into your dataset.</span></span> <span data-ttu-id="04cb4-164">這可讓您 toowork 而 hello 需要在 Power BI Desktop 的資料。</span><span class="sxs-lookup"><span data-stu-id="04cb4-164">This allows you toowork with data without hello need of Power BI Desktop.</span></span> <span data-ttu-id="04cb4-165">如需詳細資訊，請參閱[公佈資料集](https://msdn.microsoft.com/library/azure/mt778875.aspx)。</span><span class="sxs-lookup"><span data-stu-id="04cb4-165">For more information, see [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span></span>

### <a name="reports"></a><span data-ttu-id="04cb4-166">報告</span><span class="sxs-lookup"><span data-stu-id="04cb4-166">Reports</span></span>

<span data-ttu-id="04cb4-167">您可以直接在您使用 hello JavaScript API 的應用程式中，從資料集建立報表。</span><span class="sxs-lookup"><span data-stu-id="04cb4-167">You can create a report from a dataset directly in your application using hello JavaScript API.</span></span> <span data-ttu-id="04cb4-168">如需詳細資訊，請參閱[在 Power BI Embedded 中從資料集建立新的報告](power-bi-embedded-create-report-from-dataset.md)。</span><span class="sxs-lookup"><span data-stu-id="04cb4-168">For more information, see [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="04cb4-169">另請參閱</span><span class="sxs-lookup"><span data-stu-id="04cb4-169">See Also</span></span>

[<span data-ttu-id="04cb4-170">開始使用範例</span><span class="sxs-lookup"><span data-stu-id="04cb4-170">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="04cb4-171">在 Power BI Embedded 中驗證和授權</span><span class="sxs-lookup"><span data-stu-id="04cb4-171">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="04cb4-172">內嵌報告</span><span class="sxs-lookup"><span data-stu-id="04cb4-172">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
<span data-ttu-id="04cb4-173">[在 Power BI Embedded 中從資料集建立新的報告](power-bi-embedded-create-report-from-dataset.md)
[儲存報告](power-bi-embedded-save-reports.md)</span><span class="sxs-lookup"><span data-stu-id="04cb4-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Save reports](power-bi-embedded-save-reports.md)</span></span>  
[<span data-ttu-id="04cb4-174">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="04cb4-174">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="04cb4-175">JavaScript 內嵌範例</span><span class="sxs-lookup"><span data-stu-id="04cb4-175">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="04cb4-176">有其他疑問？</span><span class="sxs-lookup"><span data-stu-id="04cb4-176">More questions?</span></span> [<span data-ttu-id="04cb4-177">再試一次 hello Power BI 社群</span><span class="sxs-lookup"><span data-stu-id="04cb4-177">Try hello Power BI Community</span></span>](http://community.powerbi.com/)


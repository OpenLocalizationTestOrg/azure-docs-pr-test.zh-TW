---
title: "aaaAzure 小組資料科學程序概觀 |Microsoft 文件"
description: "提供資料科學方法 toodeliver 預測分析解決方案和智慧型應用程式。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b1f677bb-eef5-4acb-9b3b-8a5819fb0e78
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev;
ms.openlocfilehash: 2ba03585a6f6f855faaa3b5c0c75149cad0a88bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="team-data-science-process-overview"></a><span data-ttu-id="64c81-103">Team Data Science Process 概觀</span><span class="sxs-lookup"><span data-stu-id="64c81-103">Team Data Science Process overview</span></span>

<span data-ttu-id="64c81-104">hello 小組資料科學程序 (TDSP) 會是 agile 反覆資料科學方法 toodeliver 預測性分析方案和智慧型應用程式有效。</span><span class="sxs-lookup"><span data-stu-id="64c81-104">hello Team Data Science Process (TDSP) is an agile, iterative data science methodology toodeliver predictive analytics solutions and intelligent applications efficiently.</span></span> <span data-ttu-id="64c81-105">TDSP 有助於改善團隊共同作業和學習。</span><span class="sxs-lookup"><span data-stu-id="64c81-105">TDSP helps improve team collaboration and learning.</span></span> <span data-ttu-id="64c81-106">它包含 hello 最佳作法和結構的 Microsoft 和其他 hello 產業中，以便資料科學開發案的 hello 成功實作提煉過程中若是。</span><span class="sxs-lookup"><span data-stu-id="64c81-106">It contains a distillation of hello best practices and structures from Microsoft and others in hello industry that facilitate hello successful implementation of data science initiatives.</span></span> <span data-ttu-id="64c81-107">hello 目標是 toohelp 公司完全了解的分析程式的 hello 優點。</span><span class="sxs-lookup"><span data-stu-id="64c81-107">hello goal is toohelp companies fully realize hello benefits of their analytics program.</span></span>

<span data-ttu-id="64c81-108">本文提供 TDSP 和其主要元件的概觀。</span><span class="sxs-lookup"><span data-stu-id="64c81-108">This article provides an overview of TDSP and its main components.</span></span> <span data-ttu-id="64c81-109">我們可以實作的 hello 程序的一般描述提供各種工具。</span><span class="sxs-lookup"><span data-stu-id="64c81-109">We provide a generic description of hello process here that can be implemented with a variety of tools.</span></span> <span data-ttu-id="64c81-110">其他連結的主題提供的 hello 專案工作和角色 hello hello 程序生命週期中所涉及的更詳細的描述。</span><span class="sxs-lookup"><span data-stu-id="64c81-110">A more detailed description of hello project tasks and roles involved in hello lifecycle of hello process is provided in additional linked topics.</span></span> <span data-ttu-id="64c81-111">指引也提供 tooimplement hello TDSP 使用一組特定的 Microsoft 工具與基礎結構，我們會在我們的團隊使用 tooimplement hello TDSP 的方式。</span><span class="sxs-lookup"><span data-stu-id="64c81-111">Guidance on how tooimplement hello TDSP using a specific set of Microsoft tools and infrastructure that we use tooimplement hello TDSP in our teams is also provided.</span></span>

## <a name="key-components-of-hello-tdsp"></a><span data-ttu-id="64c81-112">Hello TDSP 的重要元件</span><span class="sxs-lookup"><span data-stu-id="64c81-112">Key components of hello TDSP</span></span>

<span data-ttu-id="64c81-113">TDSP 共有的 hello 下列主要元件：</span><span class="sxs-lookup"><span data-stu-id="64c81-113">TDSP comprises of hello following key components:</span></span>

- <span data-ttu-id="64c81-114">**資料科學生命週期**定義</span><span class="sxs-lookup"><span data-stu-id="64c81-114">A **data science lifecycle** definition</span></span>
- <span data-ttu-id="64c81-115">**標準化專案結構**</span><span class="sxs-lookup"><span data-stu-id="64c81-115">A **standardized project structure**</span></span>
- <span data-ttu-id="64c81-116">資料科學專案的**基礎結構和資源**</span><span class="sxs-lookup"><span data-stu-id="64c81-116">**Infrastructure and resources** for data science projects</span></span>
- <span data-ttu-id="64c81-117">專案執行的**工具和公用程式**</span><span class="sxs-lookup"><span data-stu-id="64c81-117">**Tools and utilities** for project execution</span></span>


## <a name="data-science-lifecycle"></a><span data-ttu-id="64c81-118">資料科學生命週期</span><span class="sxs-lookup"><span data-stu-id="64c81-118">Data science lifecycle</span></span>

<span data-ttu-id="64c81-119">hello 小組資料科學程序 (TDSP) 提供資料科學專案的生命週期 toostructure hello 的開發。</span><span class="sxs-lookup"><span data-stu-id="64c81-119">hello Team Data Science Process (TDSP) provides a lifecycle toostructure hello development of your data science projects.</span></span> <span data-ttu-id="64c81-120">hello 生命週期概述 hello 步驟，從開始 toofinish 專案通常會遵循在執行時。</span><span class="sxs-lookup"><span data-stu-id="64c81-120">hello lifecycle outlines hello steps, from start toofinish, that projects usually follow when they are executed.</span></span>

<span data-ttu-id="64c81-121">如果您使用另一個資料科學生命週期，例如[CRISP-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining)， [KDD](https://wikipedia.org/wiki/Data_mining#Process)或您組織本身的自訂程序，您仍然可以使用以工作為基礎的 TDSP，這些開發 hello 內容中的 hello生命週期。</span><span class="sxs-lookup"><span data-stu-id="64c81-121">If you are using another data science lifecycle, such as [CRISP-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) or your organization's own custom process, you can still use hello task-based TDSP in hello context of those development lifecycles.</span></span> <span data-ttu-id="64c81-122">大致而言，這些不同的方法有許多共通點。</span><span class="sxs-lookup"><span data-stu-id="64c81-122">At a high level, these different methodologies have much in common.</span></span> 

<span data-ttu-id="64c81-123">此生命週期是針對在智慧型應用程式中隨附的資料科學專案所設計。</span><span class="sxs-lookup"><span data-stu-id="64c81-123">This lifecycle has been designed for data science projects that ship as part of intelligent applications.</span></span> <span data-ttu-id="64c81-124">這些應用程式會部署機器學習服務或人工智慧模型來做預測性分析。</span><span class="sxs-lookup"><span data-stu-id="64c81-124">These applications deploy machine learning or artificial intelligence models for predictive analytics.</span></span> <span data-ttu-id="64c81-125">探勘資料科學專案或臨機操作分析專案也可以從使用此程序而獲益。</span><span class="sxs-lookup"><span data-stu-id="64c81-125">Exploratory data science projects or ad hoc analytics projects can also benefit from using this process.</span></span> <span data-ttu-id="64c81-126">但是，在這種情況下的部分所述的 hello 步驟可能不需要。</span><span class="sxs-lookup"><span data-stu-id="64c81-126">But in such cases some of hello steps described may not be needed.</span></span>    

<span data-ttu-id="64c81-127">hello TDSP 生命週期包含會反覆執行的五個主要階段：</span><span class="sxs-lookup"><span data-stu-id="64c81-127">hello TDSP lifecycle is composed of five major stages that are executed iteratively:</span></span>

* <span data-ttu-id="64c81-128">**了解商務**</span><span class="sxs-lookup"><span data-stu-id="64c81-128">**Business Understanding**</span></span>
* <span data-ttu-id="64c81-129">**資料取得與認知**</span><span class="sxs-lookup"><span data-stu-id="64c81-129">**Data Acquisition and Understanding**</span></span>
* <span data-ttu-id="64c81-130">**模型化**</span><span class="sxs-lookup"><span data-stu-id="64c81-130">**Modeling**</span></span>
* <span data-ttu-id="64c81-131">**部署**</span><span class="sxs-lookup"><span data-stu-id="64c81-131">**Deployment**</span></span>
* <span data-ttu-id="64c81-132">**客戶接受度**</span><span class="sxs-lookup"><span data-stu-id="64c81-132">**Customer Acceptance**</span></span>

<span data-ttu-id="64c81-133">以下是 hello 的視覺表示法**小組資料科學程序生命週期**。</span><span class="sxs-lookup"><span data-stu-id="64c81-133">Here is a visual representation of hello **Team Data Science Process lifecycle**.</span></span> 

![TDSP-Lifecycle](./media/data-science-process-overview/tdsp-lifecycle.png) 

<span data-ttu-id="64c81-135">hello 目標、 工作和文件的成品以利在 TDSP hello 生命週期的每個階段所述 hello[小組資料科學程序生命週期](data-science-process-lifecycle.md)主題。</span><span class="sxs-lookup"><span data-stu-id="64c81-135">hello goals, tasks, and documentation artifacts for each stage of hello lifecycle in TDSP are described in hello [Team Data Science Process lifecycle](data-science-process-lifecycle.md) topic.</span></span> <span data-ttu-id="64c81-136">這些工作和構件與專案角色相關聯：</span><span class="sxs-lookup"><span data-stu-id="64c81-136">These tasks and artifacts are associated with project roles:</span></span>

- <span data-ttu-id="64c81-137">解決方案架構師</span><span class="sxs-lookup"><span data-stu-id="64c81-137">Solution architect</span></span>
- <span data-ttu-id="64c81-138">專案經理</span><span class="sxs-lookup"><span data-stu-id="64c81-138">Project manager</span></span>
- <span data-ttu-id="64c81-139">資料科學家</span><span class="sxs-lookup"><span data-stu-id="64c81-139">Data scientist</span></span>
- <span data-ttu-id="64c81-140">專案負責人</span><span class="sxs-lookup"><span data-stu-id="64c81-140">Project lead</span></span> 

<span data-ttu-id="64c81-141">hello 下列圖表提供 hello 工作 （以藍色） 和 （在 hello 垂直軸） 上的這些角色相關聯 （在 hello 水平軸） 的 hello 生命週期的每個階段 （以綠色） 成品的方格檢視。</span><span class="sxs-lookup"><span data-stu-id="64c81-141">hello following diagram provides a grid view of hello tasks (in blue) and artifacts (in green) associated with each stage of hello lifecycle (on hello horizontal axis) for these roles (on hello vertical axis).</span></span> 

![TDSP - 角色和工作](./media/data-science-process-overview/tdsp-tasks-by-roles.png)

## <a name="standardized-project-structure"></a><span data-ttu-id="64c81-143">標準化專案結構</span><span class="sxs-lookup"><span data-stu-id="64c81-143">Standardized project structure</span></span>

<span data-ttu-id="64c81-144">具有共用的目錄結構，並使用適用於專案文件範本的所有專案，可輕鬆有關 hello 小組成員 toofind 其專案。</span><span class="sxs-lookup"><span data-stu-id="64c81-144">Having all projects share a directory structure and use templates for project documents makes it easy for hello team members toofind information about their projects.</span></span> <span data-ttu-id="64c81-145">所有的程式碼和文件會儲存在版本控制系統，(VC) 例如 Git、 TFS 或 Subversion tooenable 小組共同作業。</span><span class="sxs-lookup"><span data-stu-id="64c81-145">All code and documents are stored in a version control system (VCS) like Git, TFS, or Subversion tooenable team collaboration.</span></span> <span data-ttu-id="64c81-146">追蹤工作和功能追蹤系統，例如 Jira 敏捷式軟體開發專案中的，集結，Visual Studio Team Services 可讓更接近追蹤 hello 個別功能的程式碼。</span><span class="sxs-lookup"><span data-stu-id="64c81-146">Tracking tasks and features in an agile project tracking system like Jira, Rally, Visual Studio Team Services allows closer tracking of hello code for individual features.</span></span> <span data-ttu-id="64c81-147">這類追蹤也可讓您小組 tooobtain 更好的成本估計值。</span><span class="sxs-lookup"><span data-stu-id="64c81-147">Such tracking also enables teams tooobtain better cost estimates.</span></span> <span data-ttu-id="64c81-148">TDSP 建議 hello VC 版本控制、 資訊安全和共同作業上建立個別的儲存機制，每個專案。</span><span class="sxs-lookup"><span data-stu-id="64c81-148">TDSP recommends creating a separate repository for each project on hello VCS for versioning, information security, and collaboration.</span></span> <span data-ttu-id="64c81-149">hello 標準化 hello 組織內的所有專案有助於建置機構知識的結構。</span><span class="sxs-lookup"><span data-stu-id="64c81-149">hello standardized structure for all projects helps build institutional knowledge across hello organization.</span></span>

<span data-ttu-id="64c81-150">我們 hello 資料夾結構和必要的文件標準位置中提供的範本。</span><span class="sxs-lookup"><span data-stu-id="64c81-150">We provide templates for hello folder structure and required documents in standard locations.</span></span> <span data-ttu-id="64c81-151">此資料夾結構會組織 hello 檔案包含程式碼進行資料探索和擷取特徵，並會記錄模型反覆項目。</span><span class="sxs-lookup"><span data-stu-id="64c81-151">This folder structure organizes hello files that contain code for data exploration and feature extraction, and that record model iterations.</span></span> <span data-ttu-id="64c81-152">這些範本可讓您更容易為其他人所完成的小組成員 toounderstand 工作及新成員 tooteams tooadd。</span><span class="sxs-lookup"><span data-stu-id="64c81-152">These templates make it easier for team members toounderstand work done by others and tooadd new members tooteams.</span></span> <span data-ttu-id="64c81-153">它是簡單 tooview 和更新文件範本 markdown 格式。</span><span class="sxs-lookup"><span data-stu-id="64c81-153">It is easy tooview and update document templates in markdown format.</span></span> <span data-ttu-id="64c81-154">重要的問題與用於每個專案 tooinsure hello 問題妥善定義，而且該交付項目符合預期的 hello 品質範本 tooprovide 檢查清單。</span><span class="sxs-lookup"><span data-stu-id="64c81-154">Use templates tooprovide checklists with key questions for each project tooinsure that hello problem is well-defined and that deliverables meet hello quality expected.</span></span> <span data-ttu-id="64c81-155">範例包括：</span><span class="sxs-lookup"><span data-stu-id="64c81-155">Examples include:</span></span>

- <span data-ttu-id="64c81-156">專案教授 toodocument hello 商務問題和 hello 專案的範圍</span><span class="sxs-lookup"><span data-stu-id="64c81-156">a project charter toodocument hello business problem and scope of hello project</span></span>
- <span data-ttu-id="64c81-157">資料會報告 toodocument hello 結構和 hello 原始資料的統計資料</span><span class="sxs-lookup"><span data-stu-id="64c81-157">data reports toodocument hello structure and statistics of hello raw data</span></span>
- <span data-ttu-id="64c81-158">模型報表 toodocument hello 衍生功能</span><span class="sxs-lookup"><span data-stu-id="64c81-158">model reports toodocument hello derived features</span></span>
- <span data-ttu-id="64c81-159">模型效能計量，例如 ROC 曲線或 MSE</span><span class="sxs-lookup"><span data-stu-id="64c81-159">model performance metrics such as ROC curves or MSE</span></span>


![TDSP 目錄](./media/data-science-process-overview/tdsp-dir-structure.png)

<span data-ttu-id="64c81-161">hello 目錄結構可以被複製從[Github](https://github.com/Azure/Azure-TDSP-ProjectTemplate)。</span><span class="sxs-lookup"><span data-stu-id="64c81-161">hello directory structure can be cloned from [Github](https://github.com/Azure/Azure-TDSP-ProjectTemplate).</span></span>

## <a name="infrastructure-and-resources-for-data-science-projects"></a><span data-ttu-id="64c81-162">資料科學專案的基礎結構和資源</span><span class="sxs-lookup"><span data-stu-id="64c81-162">Infrastructure and resources for data science projects</span></span>

<span data-ttu-id="64c81-163">TDSP 提供管理共用分析和儲存體基礎結構的建議，例如：</span><span class="sxs-lookup"><span data-stu-id="64c81-163">TDSP provides recommendations for managing shared analytics and storage infrastructure such as:</span></span>

- <span data-ttu-id="64c81-164">儲存資料集的雲端檔案系統、</span><span class="sxs-lookup"><span data-stu-id="64c81-164">cloud file systems for storing datasets,</span></span> 
- <span data-ttu-id="64c81-165">資料庫</span><span class="sxs-lookup"><span data-stu-id="64c81-165">databases</span></span>
- <span data-ttu-id="64c81-166">巨量資料 (Hadoop 或 Spark) 叢集</span><span class="sxs-lookup"><span data-stu-id="64c81-166">big data (Hadoop or Spark) clusters</span></span> 
- <span data-ttu-id="64c81-167">機器學習服務。</span><span class="sxs-lookup"><span data-stu-id="64c81-167">machine learning services.</span></span> 

<span data-ttu-id="64c81-168">hello 分析和儲存體基礎結構可以在 hello 雲端或內部部署中。</span><span class="sxs-lookup"><span data-stu-id="64c81-168">hello analytics and storage infrastructure can be in hello cloud or on-premises.</span></span> <span data-ttu-id="64c81-169">這裡儲存著原始資料集和處理後的資料集。</span><span class="sxs-lookup"><span data-stu-id="64c81-169">This is where raw and processed datasets are stored.</span></span> <span data-ttu-id="64c81-170">這個基礎架構能夠進行可重現的分析。</span><span class="sxs-lookup"><span data-stu-id="64c81-170">This infrastructure enables reproducible analysis.</span></span> <span data-ttu-id="64c81-171">它也可避免重複，這可能會導致 tooinconsistencies 及不必要的基礎結構成本。</span><span class="sxs-lookup"><span data-stu-id="64c81-171">It also avoids duplication, which can lead tooinconsistencies and unnecessary infrastructure costs.</span></span> <span data-ttu-id="64c81-172">工具會提供 tooprovision hello 共用的資源、 追蹤，並允許每個小組成員 tooconnect toothose 資源安全。</span><span class="sxs-lookup"><span data-stu-id="64c81-172">Tools are provided tooprovision hello shared resources, track them, and allow each team member tooconnect toothose resources securely.</span></span> <span data-ttu-id="64c81-173">讓專案成員建立一致的運算環境也是個不錯的做法。</span><span class="sxs-lookup"><span data-stu-id="64c81-173">It is also a good practice have project members create a consistent compute environment.</span></span> <span data-ttu-id="64c81-174">不同的小組成員可以複寫和驗證實驗。</span><span class="sxs-lookup"><span data-stu-id="64c81-174">Different team members can then replicate and validate experiments.</span></span>

<span data-ttu-id="64c81-175">以下是小組處理多個專案並共用各種雲端分析基礎結構元件的範例。</span><span class="sxs-lookup"><span data-stu-id="64c81-175">Here is an example of a team working on multiple projects and sharing various cloud analytics infrastructure components.</span></span>

![TDSP 基礎結構](./media/data-science-process-overview/tdsp-analytics-infra.png)


## <a name="tools-and-utilities-for-project-execution"></a><span data-ttu-id="64c81-177">專案執行的工具和公用程式</span><span class="sxs-lookup"><span data-stu-id="64c81-177">Tools and utilities for project execution</span></span>

<span data-ttu-id="64c81-178">在大部分的組織中引進流程是相當有挑戰性。</span><span class="sxs-lookup"><span data-stu-id="64c81-178">Introducing processes in most organizations is challenging.</span></span> <span data-ttu-id="64c81-179">所提供的工具 tooimplement hello 資料科學程序和生命週期協助較低的 hello 障礙 tooand 增加其採用的 hello 一致性。</span><span class="sxs-lookup"><span data-stu-id="64c81-179">Tools provided tooimplement hello data science process and lifecycle help lower hello barriers tooand increase hello consistency of their adoption.</span></span> <span data-ttu-id="64c81-180">TDSP 在團隊內 TDSP toojump 開始採用提供一組初始的工具和指令碼。</span><span class="sxs-lookup"><span data-stu-id="64c81-180">TDSP provides an initial set of tools and scripts toojump-start adoption of TDSP within a team.</span></span> <span data-ttu-id="64c81-181">這也有助於將部分 hello hello 資料科學生命週期，例如資料探索和基準模型中的常見工作自動化。</span><span class="sxs-lookup"><span data-stu-id="64c81-181">It also helps automate some of hello common tasks in hello data science lifecycle such as data exploration and baseline modeling.</span></span> <span data-ttu-id="64c81-182">提供的個人 toocontribute 共用工具和公用程式到他們的小組共用的程式碼儲存機制，沒有正確定義的結構。</span><span class="sxs-lookup"><span data-stu-id="64c81-182">There is a well-defined structure provided for individuals toocontribute shared tools and utilities into their team’s shared code repository.</span></span> <span data-ttu-id="64c81-183">這些資源可以加以利用 hello 小組或 hello 組織內的其他專案。</span><span class="sxs-lookup"><span data-stu-id="64c81-183">These resources can then be leveraged by other projects within hello team or hello organization.</span></span> <span data-ttu-id="64c81-184">TDSP 也計劃工具和公用程式 toohello 整個社群的 tooenable hello 比重。</span><span class="sxs-lookup"><span data-stu-id="64c81-184">TDSP also plans tooenable hello contributions of tools and utilities toohello whole community.</span></span> <span data-ttu-id="64c81-185">hello TDSP 公用程式可以複製從[Github](https://github.com/Azure/Azure-TDSP-Utilities)。</span><span class="sxs-lookup"><span data-stu-id="64c81-185">hello TDSP utilities can be cloned from [Github](https://github.com/Azure/Azure-TDSP-Utilities).</span></span>


## <a name="next-steps"></a><span data-ttu-id="64c81-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64c81-186">Next steps</span></span>

<span data-ttu-id="64c81-187">[小組資料科學程序： 角色和工作](https://github.com/Azure/Microsoft-TDSP/blob/master/Docs/roles-tasks.md)概述 hello 金鑰的人員角色，以及如需這個程序標準化資料科學團隊及其相關的工作。</span><span class="sxs-lookup"><span data-stu-id="64c81-187">[Team Data Science Process: Roles and tasks](https://github.com/Azure/Microsoft-TDSP/blob/master/Docs/roles-tasks.md) Outlines hello key personnel roles and their associated tasks for a data science team that standardizes on this process.</span></span> 

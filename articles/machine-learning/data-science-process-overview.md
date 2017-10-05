---
title: "Azure Team Data Science Process 概觀 | Microsoft Docs"
description: "提供資料科學方法，用以產出預測分析解決方案和智慧型應用程式。"
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
ms.openlocfilehash: 006a1465a7cdced1878111beee709c8da4bc310f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="team-data-science-process-overview"></a><span data-ttu-id="9a049-103">Team Data Science Process 概觀</span><span class="sxs-lookup"><span data-stu-id="9a049-103">Team Data Science Process overview</span></span>

<span data-ttu-id="9a049-104">Team Data Science Process (TDSP) 是一種敏捷式反覆資料科學方法，可有效產出預測分析解決方案和智慧型應用程式。</span><span class="sxs-lookup"><span data-stu-id="9a049-104">The Team Data Science Process (TDSP) is an agile, iterative data science methodology to deliver predictive analytics solutions and intelligent applications efficiently.</span></span> <span data-ttu-id="9a049-105">TDSP 有助於改善團隊共同作業和學習。</span><span class="sxs-lookup"><span data-stu-id="9a049-105">TDSP helps improve team collaboration and learning.</span></span> <span data-ttu-id="9a049-106">其中包含 Microsoft 及業界其他公司的最佳做法和結構，有助於順利實作資料科學計劃。</span><span class="sxs-lookup"><span data-stu-id="9a049-106">It contains a distillation of the best practices and structures from Microsoft and others in the industry that facilitate the successful implementation of data science initiatives.</span></span> <span data-ttu-id="9a049-107">目標是協助公司完全了解其分析程式的優點。</span><span class="sxs-lookup"><span data-stu-id="9a049-107">The goal is to help companies fully realize the benefits of their analytics program.</span></span>

<span data-ttu-id="9a049-108">本文提供 TDSP 和其主要元件的概觀。</span><span class="sxs-lookup"><span data-stu-id="9a049-108">This article provides an overview of TDSP and its main components.</span></span> <span data-ttu-id="9a049-109">本文對於程序提供的一般描述可以使用各種工具實作。</span><span class="sxs-lookup"><span data-stu-id="9a049-109">We provide a generic description of the process here that can be implemented with a variety of tools.</span></span> <span data-ttu-id="9a049-110">其他連結的主題詳細描述流程的生命週期中涉及的專案工作與角色。</span><span class="sxs-lookup"><span data-stu-id="9a049-110">A more detailed description of the project tasks and roles involved in the lifecycle of the process is provided in additional linked topics.</span></span> <span data-ttu-id="9a049-111">另外也指引如何使用我們團隊實作 TDSP 所用的一組特定 Microsoft 工具和基礎結構實作 TDSP。</span><span class="sxs-lookup"><span data-stu-id="9a049-111">Guidance on how to implement the TDSP using a specific set of Microsoft tools and infrastructure that we use to implement the TDSP in our teams is also provided.</span></span>

## <a name="key-components-of-the-tdsp"></a><span data-ttu-id="9a049-112">TDSP 的重要元件</span><span class="sxs-lookup"><span data-stu-id="9a049-112">Key components of the TDSP</span></span>

<span data-ttu-id="9a049-113">TDSP 包含下列主要元件：</span><span class="sxs-lookup"><span data-stu-id="9a049-113">TDSP comprises of the following key components:</span></span>

- <span data-ttu-id="9a049-114">**資料科學生命週期**定義</span><span class="sxs-lookup"><span data-stu-id="9a049-114">A **data science lifecycle** definition</span></span>
- <span data-ttu-id="9a049-115">**標準化專案結構**</span><span class="sxs-lookup"><span data-stu-id="9a049-115">A **standardized project structure**</span></span>
- <span data-ttu-id="9a049-116">資料科學專案的**基礎結構和資源**</span><span class="sxs-lookup"><span data-stu-id="9a049-116">**Infrastructure and resources** for data science projects</span></span>
- <span data-ttu-id="9a049-117">專案執行的**工具和公用程式**</span><span class="sxs-lookup"><span data-stu-id="9a049-117">**Tools and utilities** for project execution</span></span>


## <a name="data-science-lifecycle"></a><span data-ttu-id="9a049-118">資料科學生命週期</span><span class="sxs-lookup"><span data-stu-id="9a049-118">Data science lifecycle</span></span>

<span data-ttu-id="9a049-119">Team Data Science Process (TDSP) 會提供建構資料科學專案開發的生命週期。</span><span class="sxs-lookup"><span data-stu-id="9a049-119">The Team Data Science Process (TDSP) provides a lifecycle to structure the development of your data science projects.</span></span> <span data-ttu-id="9a049-120">生命週期會概述專案在執行時通常會遵循之從開始到完成的步驟。</span><span class="sxs-lookup"><span data-stu-id="9a049-120">The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed.</span></span>

<span data-ttu-id="9a049-121">如果您正在使用另一個資料科學生命週期 (例如 [CRISP-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining)、[KDD](https://wikipedia.org/wiki/Data_mining#Process) 或您組織本身的自訂程序)，您仍可在這些開發生命週期的內容中使用工作型 TDSP。</span><span class="sxs-lookup"><span data-stu-id="9a049-121">If you are using another data science lifecycle, such as [CRISP-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) or your organization's own custom process, you can still use the task-based TDSP in the context of those development lifecycles.</span></span> <span data-ttu-id="9a049-122">大致而言，這些不同的方法有許多共通點。</span><span class="sxs-lookup"><span data-stu-id="9a049-122">At a high level, these different methodologies have much in common.</span></span> 

<span data-ttu-id="9a049-123">此生命週期是針對在智慧型應用程式中隨附的資料科學專案所設計。</span><span class="sxs-lookup"><span data-stu-id="9a049-123">This lifecycle has been designed for data science projects that ship as part of intelligent applications.</span></span> <span data-ttu-id="9a049-124">這些應用程式會部署機器學習服務或人工智慧模型來做預測性分析。</span><span class="sxs-lookup"><span data-stu-id="9a049-124">These applications deploy machine learning or artificial intelligence models for predictive analytics.</span></span> <span data-ttu-id="9a049-125">探勘資料科學專案或臨機操作分析專案也可以從使用此程序而獲益。</span><span class="sxs-lookup"><span data-stu-id="9a049-125">Exploratory data science projects or ad hoc analytics projects can also benefit from using this process.</span></span> <span data-ttu-id="9a049-126">但是，在這種情況下，可能不需要所述的某些步驟。</span><span class="sxs-lookup"><span data-stu-id="9a049-126">But in such cases some of the steps described may not be needed.</span></span>    

<span data-ttu-id="9a049-127">TDSP 生命週期是由反覆執行的五個主要階段所組成：</span><span class="sxs-lookup"><span data-stu-id="9a049-127">The TDSP lifecycle is composed of five major stages that are executed iteratively:</span></span>

* <span data-ttu-id="9a049-128">**了解商務**</span><span class="sxs-lookup"><span data-stu-id="9a049-128">**Business Understanding**</span></span>
* <span data-ttu-id="9a049-129">**資料取得與認知**</span><span class="sxs-lookup"><span data-stu-id="9a049-129">**Data Acquisition and Understanding**</span></span>
* <span data-ttu-id="9a049-130">**模型化**</span><span class="sxs-lookup"><span data-stu-id="9a049-130">**Modeling**</span></span>
* <span data-ttu-id="9a049-131">**部署**</span><span class="sxs-lookup"><span data-stu-id="9a049-131">**Deployment**</span></span>
* <span data-ttu-id="9a049-132">**客戶接受度**</span><span class="sxs-lookup"><span data-stu-id="9a049-132">**Customer Acceptance**</span></span>

<span data-ttu-id="9a049-133">以下是 **Team Data Science Process 生命週期**的視覺化呈現。</span><span class="sxs-lookup"><span data-stu-id="9a049-133">Here is a visual representation of the **Team Data Science Process lifecycle**.</span></span> 

![TDSP-Lifecycle](./media/data-science-process-overview/tdsp-lifecycle.png) 

<span data-ttu-id="9a049-135">[小組資料科學程序生命週期](data-science-process-lifecycle.md)主題說明 TDSP 生命週期每個階段的目標、工作和文件構件。</span><span class="sxs-lookup"><span data-stu-id="9a049-135">The goals, tasks, and documentation artifacts for each stage of the lifecycle in TDSP are described in the [Team Data Science Process lifecycle](data-science-process-lifecycle.md) topic.</span></span> <span data-ttu-id="9a049-136">這些工作和構件與專案角色相關聯：</span><span class="sxs-lookup"><span data-stu-id="9a049-136">These tasks and artifacts are associated with project roles:</span></span>

- <span data-ttu-id="9a049-137">解決方案架構師</span><span class="sxs-lookup"><span data-stu-id="9a049-137">Solution architect</span></span>
- <span data-ttu-id="9a049-138">專案經理</span><span class="sxs-lookup"><span data-stu-id="9a049-138">Project manager</span></span>
- <span data-ttu-id="9a049-139">資料科學家</span><span class="sxs-lookup"><span data-stu-id="9a049-139">Data scientist</span></span>
- <span data-ttu-id="9a049-140">專案負責人</span><span class="sxs-lookup"><span data-stu-id="9a049-140">Project lead</span></span> 

<span data-ttu-id="9a049-141">下圖以格線檢視呈現這些角色 (水平軸) 的生命週期每個階段 (垂直軸) 相關聯的工作 (藍色) 和構件 (綠色)。</span><span class="sxs-lookup"><span data-stu-id="9a049-141">The following diagram provides a grid view of the tasks (in blue) and artifacts (in green) associated with each stage of the lifecycle (on the horizontal axis) for these roles (on the vertical axis).</span></span> 

![TDSP - 角色和工作](./media/data-science-process-overview/tdsp-tasks-by-roles.png)

## <a name="standardized-project-structure"></a><span data-ttu-id="9a049-143">標準化專案結構</span><span class="sxs-lookup"><span data-stu-id="9a049-143">Standardized project structure</span></span>

<span data-ttu-id="9a049-144">使所有專案共用目錄結構，並使用專案文件的範本讓小組成員能輕易找到其專案的資訊。</span><span class="sxs-lookup"><span data-stu-id="9a049-144">Having all projects share a directory structure and use templates for project documents makes it easy for the team members to find information about their projects.</span></span> <span data-ttu-id="9a049-145">Git、TFS 或 Subversion 之類的版本控制系統 (VCS) 儲存所有的程式碼和文件，有助於小組共同作業。</span><span class="sxs-lookup"><span data-stu-id="9a049-145">All code and documents are stored in a version control system (VCS) like Git, TFS, or Subversion to enable team collaboration.</span></span> <span data-ttu-id="9a049-146">在 Jira、Rally、Visual Studio Team Services 之類的敏捷式軟體開發專案中追蹤工作和功能，追蹤系統，能夠更密切追蹤個別功能的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9a049-146">Tracking tasks and features in an agile project tracking system like Jira, Rally, Visual Studio Team Services allows closer tracking of the code for individual features.</span></span> <span data-ttu-id="9a049-147">這類追蹤也可讓小組獲得進一步的成本估計。</span><span class="sxs-lookup"><span data-stu-id="9a049-147">Such tracking also enables teams to obtain better cost estimates.</span></span> <span data-ttu-id="9a049-148">TDSP 建議在 VCS 上對於每個專案建立個別的儲存機制，以利版本控制、資訊安全和共同作業。</span><span class="sxs-lookup"><span data-stu-id="9a049-148">TDSP recommends creating a separate repository for each project on the VCS for versioning, information security, and collaboration.</span></span> <span data-ttu-id="9a049-149">所有專案的標準化結構有助於累積整個組織的機構知識。</span><span class="sxs-lookup"><span data-stu-id="9a049-149">The standardized structure for all projects helps build institutional knowledge across the organization.</span></span>

<span data-ttu-id="9a049-150">我們提供資料夾結構提供範本和標準位置的必要文件。</span><span class="sxs-lookup"><span data-stu-id="9a049-150">We provide templates for the folder structure and required documents in standard locations.</span></span> <span data-ttu-id="9a049-151">此資料夾結構包括內含資料探索和功能擷取程式碼的檔案，以及記錄模型反覆項目的檔案。</span><span class="sxs-lookup"><span data-stu-id="9a049-151">This folder structure organizes the files that contain code for data exploration and feature extraction, and that record model iterations.</span></span> <span data-ttu-id="9a049-152">這些範本讓小組成員更容易了解其他人完成的工作，並且更容易將新成員加入至小組中。</span><span class="sxs-lookup"><span data-stu-id="9a049-152">These templates make it easier for team members to understand work done by others and to add new members to teams.</span></span> <span data-ttu-id="9a049-153">Markdown 格式的文件範本很容易檢視和更新。</span><span class="sxs-lookup"><span data-stu-id="9a049-153">It is easy to view and update document templates in markdown format.</span></span> <span data-ttu-id="9a049-154">範本可用來對於每個專案提供重要問題的檢查清單，確保問題獲得妥善定義，而且交付項目符合預期的品質。</span><span class="sxs-lookup"><span data-stu-id="9a049-154">Use templates to provide checklists with key questions for each project to insure that the problem is well-defined and that deliverables meet the quality expected.</span></span> <span data-ttu-id="9a049-155">範例包括：</span><span class="sxs-lookup"><span data-stu-id="9a049-155">Examples include:</span></span>

- <span data-ttu-id="9a049-156">記錄商務問題和專案範圍的專案許可</span><span class="sxs-lookup"><span data-stu-id="9a049-156">a project charter to document the business problem and scope of the project</span></span>
- <span data-ttu-id="9a049-157">記錄原始資料結構和統計資料的資料報告</span><span class="sxs-lookup"><span data-stu-id="9a049-157">data reports to document the structure and statistics of the raw data</span></span>
- <span data-ttu-id="9a049-158">記錄衍生功能的模型報告</span><span class="sxs-lookup"><span data-stu-id="9a049-158">model reports to document the derived features</span></span>
- <span data-ttu-id="9a049-159">模型效能計量，例如 ROC 曲線或 MSE</span><span class="sxs-lookup"><span data-stu-id="9a049-159">model performance metrics such as ROC curves or MSE</span></span>


![TDSP 目錄](./media/data-science-process-overview/tdsp-dir-structure.png)

<span data-ttu-id="9a049-161">可以從 [Github](https://github.com/Azure/Azure-TDSP-ProjectTemplate) 複製目錄結構。</span><span class="sxs-lookup"><span data-stu-id="9a049-161">The directory structure can be cloned from [Github](https://github.com/Azure/Azure-TDSP-ProjectTemplate).</span></span>

## <a name="infrastructure-and-resources-for-data-science-projects"></a><span data-ttu-id="9a049-162">資料科學專案的基礎結構和資源</span><span class="sxs-lookup"><span data-stu-id="9a049-162">Infrastructure and resources for data science projects</span></span>

<span data-ttu-id="9a049-163">TDSP 提供管理共用分析和儲存體基礎結構的建議，例如：</span><span class="sxs-lookup"><span data-stu-id="9a049-163">TDSP provides recommendations for managing shared analytics and storage infrastructure such as:</span></span>

- <span data-ttu-id="9a049-164">儲存資料集的雲端檔案系統、</span><span class="sxs-lookup"><span data-stu-id="9a049-164">cloud file systems for storing datasets,</span></span> 
- <span data-ttu-id="9a049-165">資料庫</span><span class="sxs-lookup"><span data-stu-id="9a049-165">databases</span></span>
- <span data-ttu-id="9a049-166">巨量資料 (Hadoop 或 Spark) 叢集</span><span class="sxs-lookup"><span data-stu-id="9a049-166">big data (Hadoop or Spark) clusters</span></span> 
- <span data-ttu-id="9a049-167">機器學習服務。</span><span class="sxs-lookup"><span data-stu-id="9a049-167">machine learning services.</span></span> 

<span data-ttu-id="9a049-168">分析和儲存體基礎結構可以在雲端，也可以是內部部署。</span><span class="sxs-lookup"><span data-stu-id="9a049-168">The analytics and storage infrastructure can be in the cloud or on-premises.</span></span> <span data-ttu-id="9a049-169">這裡儲存著原始資料集和處理後的資料集。</span><span class="sxs-lookup"><span data-stu-id="9a049-169">This is where raw and processed datasets are stored.</span></span> <span data-ttu-id="9a049-170">這個基礎架構能夠進行可重現的分析。</span><span class="sxs-lookup"><span data-stu-id="9a049-170">This infrastructure enables reproducible analysis.</span></span> <span data-ttu-id="9a049-171">它也可避免重複，重複可能會導致不一致和不必要的基礎結構成本。</span><span class="sxs-lookup"><span data-stu-id="9a049-171">It also avoids duplication, which can lead to inconsistencies and unnecessary infrastructure costs.</span></span> <span data-ttu-id="9a049-172">提供的工具可用來佈建和追蹤共用的資源，並允許每個小組成員安全地連線到這些資源。</span><span class="sxs-lookup"><span data-stu-id="9a049-172">Tools are provided to provision the shared resources, track them, and allow each team member to connect to those resources securely.</span></span> <span data-ttu-id="9a049-173">讓專案成員建立一致的運算環境也是個不錯的做法。</span><span class="sxs-lookup"><span data-stu-id="9a049-173">It is also a good practice have project members create a consistent compute environment.</span></span> <span data-ttu-id="9a049-174">不同的小組成員可以複寫和驗證實驗。</span><span class="sxs-lookup"><span data-stu-id="9a049-174">Different team members can then replicate and validate experiments.</span></span>

<span data-ttu-id="9a049-175">以下是小組處理多個專案並共用各種雲端分析基礎結構元件的範例。</span><span class="sxs-lookup"><span data-stu-id="9a049-175">Here is an example of a team working on multiple projects and sharing various cloud analytics infrastructure components.</span></span>

![TDSP 基礎結構](./media/data-science-process-overview/tdsp-analytics-infra.png)


## <a name="tools-and-utilities-for-project-execution"></a><span data-ttu-id="9a049-177">專案執行的工具和公用程式</span><span class="sxs-lookup"><span data-stu-id="9a049-177">Tools and utilities for project execution</span></span>

<span data-ttu-id="9a049-178">在大部分的組織中引進流程是相當有挑戰性。</span><span class="sxs-lookup"><span data-stu-id="9a049-178">Introducing processes in most organizations is challenging.</span></span> <span data-ttu-id="9a049-179">對於實作資料科學流程和生命週期所提供的工具有助於降低採用的障礙，並提升採用的一致性。</span><span class="sxs-lookup"><span data-stu-id="9a049-179">Tools provided to implement the data science process and lifecycle help lower the barriers to and increase the consistency of their adoption.</span></span> <span data-ttu-id="9a049-180">TDSP 提供一組初始的工具和指令碼，可供團隊快速採用 TDSP。</span><span class="sxs-lookup"><span data-stu-id="9a049-180">TDSP provides an initial set of tools and scripts to jump-start adoption of TDSP within a team.</span></span> <span data-ttu-id="9a049-181">這也有助於資料科學開發週期中部分常見的工作自動進行，例如資料探索和基準模型。</span><span class="sxs-lookup"><span data-stu-id="9a049-181">It also helps automate some of the common tasks in the data science lifecycle such as data exploration and baseline modeling.</span></span> <span data-ttu-id="9a049-182">提供妥善定義的結構，以供個人將共用的工具和公用程式貢獻到小組共用的程式碼儲存機制。</span><span class="sxs-lookup"><span data-stu-id="9a049-182">There is a well-defined structure provided for individuals to contribute shared tools and utilities into their team’s shared code repository.</span></span> <span data-ttu-id="9a049-183">小組或組織內的其他專案接著即可使用這些資源。</span><span class="sxs-lookup"><span data-stu-id="9a049-183">These resources can then be leveraged by other projects within the team or the organization.</span></span> <span data-ttu-id="9a049-184">TDSP 也計畫向整個社群貢獻工具和公用程式。</span><span class="sxs-lookup"><span data-stu-id="9a049-184">TDSP also plans to enable the contributions of tools and utilities to the whole community.</span></span> <span data-ttu-id="9a049-185">可以從 [Github](https://github.com/Azure/Azure-TDSP-Utilities) 複製 TDSP 公用程式。</span><span class="sxs-lookup"><span data-stu-id="9a049-185">The TDSP utilities can be cloned from [Github](https://github.com/Azure/Azure-TDSP-Utilities).</span></span>


## <a name="next-steps"></a><span data-ttu-id="9a049-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9a049-186">Next steps</span></span>

<span data-ttu-id="9a049-187">[小組資料科學流程：角色和工作](https://github.com/Azure/Microsoft-TDSP/blob/master/Docs/roles-tasks.md)概述依據此流程進行標準化的資料科學團隊之中的重要人員角色及其相關工作。</span><span class="sxs-lookup"><span data-stu-id="9a049-187">[Team Data Science Process: Roles and tasks](https://github.com/Azure/Microsoft-TDSP/blob/master/Docs/roles-tasks.md) Outlines the key personnel roles and their associated tasks for a data science team that standardizes on this process.</span></span> 

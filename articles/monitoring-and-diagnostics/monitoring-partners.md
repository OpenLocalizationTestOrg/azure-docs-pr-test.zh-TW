---
title: "aaaAzure 監視器夥伴整合 |Microsoft 文件"
description: "了解 Azure Monitor 的監視合作夥伴以及如何存取與合作夥伴進行整合的文件。"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 01ee13ac-66fc-4edc-8b0c-32f69b986a26
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: johnkem
ms.openlocfilehash: df3af300bff702c49b1ce66216bc44670ac11938
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-partner-integrations"></a><span data-ttu-id="b40ee-103">Azure 監視器合作夥伴整合</span><span class="sxs-lookup"><span data-stu-id="b40ee-103">Azure Monitor partner integrations</span></span>
| <span data-ttu-id="b40ee-104">合作夥伴</span><span class="sxs-lookup"><span data-stu-id="b40ee-104">Partners</span></span> |  |  |
| --- | --- | --- |
| <span data-ttu-id="b40ee-105">[![合作夥伴標誌][alertlogic-logo]<br/>**AlertLogic**][alertlogic-anchor]</span><span class="sxs-lookup"><span data-stu-id="b40ee-105">[![Partner Logo][alertlogic-logo]<br/>**AlertLogic**][alertlogic-anchor]</span></span> | <span data-ttu-id="b40ee-106">[![合作夥伴標誌][appdynamics-logo]<br/>**AppDynamics**][appdynamics-anchor]</span><span class="sxs-lookup"><span data-stu-id="b40ee-106">[![Partner Logo][appdynamics-logo]<br/>**AppDynamics**][appdynamics-anchor]</span></span> | <span data-ttu-id="b40ee-107">[![合作夥伴標誌][atlassian-logo]<br/>**Atlassian**][atlassian-anchor]</span><span class="sxs-lookup"><span data-stu-id="b40ee-107">[![Partner Logo][atlassian-logo]<br/>**Atlassian**][atlassian-anchor]</span></span> |
| <span data-ttu-id="b40ee-108">[![Partner Logo][circonus-logo]<br/>**Circonus**][circonus-anchor]</span><span class="sxs-lookup"><span data-stu-id="b40ee-108">[![Partner Logo][circonus-logo]<br/>**Circonus**][circonus-anchor]</span></span> | <span data-ttu-id="b40ee-109">[![合作夥伴標誌][cloudhealth-logo]<br/>**CloudHealth**][cloudhealth-anchor]</span><span class="sxs-lookup"><span data-stu-id="b40ee-109">[![Partner Logo][cloudhealth-logo]<br/>**CloudHealth**][cloudhealth-anchor]</span></span> | <span data-ttu-id="b40ee-110">[![合作夥伴標誌][cloudmonix-logo]<br/>**CloudMonix**][cloudmonix-anchor]</span><span class="sxs-lookup"><span data-stu-id="b40ee-110">[![Partner Logo][cloudmonix-logo]<br/>**CloudMonix**][cloudmonix-anchor]</span></span> |
| <span data-ttu-id="b40ee-111">[![合作夥伴標誌][cloudyn-logo]<br/>**Cloudyn**][cloudyn-anchor]</span><span class="sxs-lookup"><span data-stu-id="b40ee-111">[![Partner Logo][cloudyn-logo]<br/>**Cloudyn**][cloudyn-anchor]</span></span> | <span data-ttu-id="b40ee-112">[![Partner Logo][datadog-logo]<br/>**Datadog**][datadog-anchor]</span><span class="sxs-lookup"><span data-stu-id="b40ee-112">[![Partner Logo][datadog-logo]<br/>**Datadog**][datadog-anchor]</span></span> | <span data-ttu-id="b40ee-113">[![合作夥伴標誌][dynatrace-logo]<br/>**Dynatrace**][dynatrace-anchor]</span><span class="sxs-lookup"><span data-stu-id="b40ee-113">[![Partner Logo][dynatrace-logo]<br/>**Dynatrace**][dynatrace-anchor]</span></span> |
| <span data-ttu-id="b40ee-114">[![合作夥伴標誌][newrelic-logo]<br/>**NewRelic**][newrelic-anchor]</span><span class="sxs-lookup"><span data-stu-id="b40ee-114">[![Partner Logo][newrelic-logo]<br/>**NewRelic**][newrelic-anchor]</span></span> | <span data-ttu-id="b40ee-115">[![合作夥伴標誌][opsgenie-logo]<br/>**OpsGenie**][opsgenie-anchor]</span><span class="sxs-lookup"><span data-stu-id="b40ee-115">[![Partner Logo][opsgenie-logo]<br/>**OpsGenie**][opsgenie-anchor]</span></span> | <span data-ttu-id="b40ee-116">[![合作夥伴標誌][pagerduty-logo]<br/>**PagerDuty**][pagerduty-anchor]</span><span class="sxs-lookup"><span data-stu-id="b40ee-116">[![Partner Logo][pagerduty-logo]<br/>**PagerDuty**][pagerduty-anchor]</span></span> |
| <span data-ttu-id="b40ee-117">[![合作夥伴標誌][sciencelogic-logo]<br/>**ScienceLogic**][sciencelogic-anchor]</span><span class="sxs-lookup"><span data-stu-id="b40ee-117">[![Partner Logo][sciencelogic-logo]<br/>**ScienceLogic**][sciencelogic-anchor]</span></span> | <span data-ttu-id="b40ee-118">[![合作夥伴標誌][splunk-logo]<br/>**Splunk**][splunk-anchor]</span><span class="sxs-lookup"><span data-stu-id="b40ee-118">[![Partner Logo][splunk-logo]<br/>**Splunk**][splunk-anchor]</span></span> | <span data-ttu-id="b40ee-119">[![合作夥伴標誌][sumologic-logo]<br/>**Sumo Logic**][sumologic-anchor]</span><span class="sxs-lookup"><span data-stu-id="b40ee-119">[![Partner Logo][sumologic-logo]<br/>**Sumo Logic**][sumologic-anchor]</span></span> | |

## <a name="alertlogic-log-manager"></a><span data-ttu-id="b40ee-120">AlertLogic Log Manager</span><span class="sxs-lookup"><span data-stu-id="b40ee-120">AlertLogic Log Manager</span></span>
<span data-ttu-id="b40ee-121">警示的邏輯記錄檔管理員收集安全性分析和保留，包括透過 hello Azure 監視應用程式開發介面的 hello Azure 活動記錄檔的 VM、 應用程式，以及 Azure 平台記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b40ee-121">Alert Logic Log Manager collects VM, Application, and Azure platform logs for security analysis and retention, including hello Azure Activity Log via hello Azure Monitor API.</span></span>  <span data-ttu-id="b40ee-122">這項資訊是使用的 toodetect malfeasance 和符合相容性需求。</span><span class="sxs-lookup"><span data-stu-id="b40ee-122">This information is used toodetect malfeasance and meet compliance requirements.</span></span>

<span data-ttu-id="b40ee-123">[移 toohello 文件。][alertlogic-doc]</span><span class="sxs-lookup"><span data-stu-id="b40ee-123">[Go toohello documentation.][alertlogic-doc]</span></span>

## <a name="appdynamics"></a><span data-ttu-id="b40ee-124">AppDynamics</span><span class="sxs-lookup"><span data-stu-id="b40ee-124">AppDynamics</span></span>
<span data-ttu-id="b40ee-125">AppDynamics 的應用程式效能管理 (APM) 可讓應用程式擁有者 toorapidly 疑難排解效能瓶頸，並使其在 Azure 環境中執行的應用程式 hello 效能最佳化。</span><span class="sxs-lookup"><span data-stu-id="b40ee-125">AppDynamics Application Performance Management (APM) enables application owners toorapidly troubleshoot performance bottlenecks and optimize hello performance of their applications running in Azure environment.</span></span> <span data-ttu-id="b40ee-126">AppDynamics APM 與 Azure Marketplace 順暢地進行整合，並可供監視 Azure 雲端服務 (PaaS) (包括 web 和背景工作角色)、虛擬機器 (IaaS)、遠端服務偵測 (Microsoft Azure 服務匯流排)、Microsoft Azure 佇列 Microsoft Azure 遠端服務 (Azure Blob)、Azure 佇列 (Microsoft 服務匯流排)、資料儲存體及 Microsoft Azure Blob 儲存體使用。</span><span class="sxs-lookup"><span data-stu-id="b40ee-126">AppDynamics APM is seamlessly integrated with Azure Marketplace and available for monitor Azure Cloud Services (PaaS) (Including web & worker roles), Virtual Machines (IaaS), Remote Service Detection (Microsoft Azure Service Bus), Microsoft Azure Queue Microsoft Azure Remote Services (Azure Blob), Azure Queue (Microsoft Service Bus), Data Storage, Microsoft Azure Blob Storage.</span></span>

<span data-ttu-id="b40ee-127">[移 toohello 文件。][appdynamics-doc]</span><span class="sxs-lookup"><span data-stu-id="b40ee-127">[Go toohello documentation.][appdynamics-doc]</span></span>

## <a name="atlassian-jira"></a><span data-ttu-id="b40ee-128">Atlassian JIRA</span><span class="sxs-lookup"><span data-stu-id="b40ee-128">Atlassian JIRA</span></span>
<span data-ttu-id="b40ee-129">您可以對 Azure 監視器警示建立 JIRA 票證。</span><span class="sxs-lookup"><span data-stu-id="b40ee-129">You can create JIRA tickets on Azure Monitor alerts.</span></span>

<span data-ttu-id="b40ee-130">[移 toohello 文件。][atlassian-doc]</span><span class="sxs-lookup"><span data-stu-id="b40ee-130">[Go toohello documentation.][atlassian-doc]</span></span>

## <a name="circonus"></a><span data-ttu-id="b40ee-131">Circonus</span><span class="sxs-lookup"><span data-stu-id="b40ee-131">Circonus</span></span>
<span data-ttu-id="b40ee-132">Circonus 是針對內部部署或 SaaS 部署建置的微服務監視和分析平台。</span><span class="sxs-lookup"><span data-stu-id="b40ee-132">Circonus is a microservices monitoring and analytics platform built for on premises or SaaS deployment.</span></span> <span data-ttu-id="b40ee-133">其以 API 為主的完整自動化平台比其監視的系統更具擴充性和且更可靠。</span><span class="sxs-lookup"><span data-stu-id="b40ee-133">Its fully automatable API-Centric platform is more scalable and reliable than systems it monitors.</span></span> <span data-ttu-id="b40ee-134">Circonus 開發 DevOps hello 需求，提供百分位數為基礎的警示、 圖表、 儀表板及啟用商業最佳化的機器學習智慧。</span><span class="sxs-lookup"><span data-stu-id="b40ee-134">Developed for hello requirements of DevOps, Circonus delivers percentile-based alerts, graphs, dashboards, and machine-learning intelligence that enable business optimization.</span></span> <span data-ttu-id="b40ee-135">Circonus 會即時監視 Microsoft Azure 雲端資源和其應用程式。</span><span class="sxs-lookup"><span data-stu-id="b40ee-135">Circonus monitors your Microsoft Azure cloud resources and their applications in real time.</span></span> <span data-ttu-id="b40ee-136">您可以使用 Circonus toocollect 和追蹤度量 hello 變數您想要 toomeasure 為您的資源和應用程式。</span><span class="sxs-lookup"><span data-stu-id="b40ee-136">You can use Circonus toocollect and track metrics for hello variables you want toomeasure for your resources and applications.</span></span> <span data-ttu-id="b40ee-137">您可以使用 Circonus 來查看整個系統，了解 Azure 的資源使用量、應用程式效能和操作健康情況。</span><span class="sxs-lookup"><span data-stu-id="b40ee-137">With Circonus, you gain system-wide visibility into Azure’s resource utilization, application performance, and operational health.</span></span>

<span data-ttu-id="b40ee-138">[移 toohello 文件。][circonus-doc]</span><span class="sxs-lookup"><span data-stu-id="b40ee-138">[Go toohello documentation.][circonus-doc]</span></span>

## <a name="cloudhealth"></a><span data-ttu-id="b40ee-139">CloudHealth</span><span class="sxs-lookup"><span data-stu-id="b40ee-139">CloudHealth</span></span>
<span data-ttu-id="b40ee-140">聯集，及自動化您的雲端與內建的平台 toosave 嚴重時間和金錢。</span><span class="sxs-lookup"><span data-stu-id="b40ee-140">Unite and automate your cloud with a platform built toosave serious time and money.</span></span> <span data-ttu-id="b40ee-141">使用前所未有的可見性、直覺式最佳化和穩固控管的作法，CloudHealth 會重新定義雲端管理。</span><span class="sxs-lookup"><span data-stu-id="b40ee-141">With unparalleled visibility, intuitive optimization and rock-solid governance practices, CloudHealth is redefining cloud management.</span></span> <span data-ttu-id="b40ee-142">hello Cloudhealth 平台可讓企業而且 MSPs toomaximize 雲端投資報酬率，並確信做出成本、 使用量、 效能和安全性。</span><span class="sxs-lookup"><span data-stu-id="b40ee-142">hello Cloudhealth platform enables enterprises and MSPs toomaximize return on cloud investments and make confident decisions around cost, usage, performance and security.</span></span>

<span data-ttu-id="b40ee-143">[深入了解。][cloudhealth-doc]</span><span class="sxs-lookup"><span data-stu-id="b40ee-143">[Learn More.][cloudhealth-doc]</span></span>

## <a name="cloudmonix"></a><span data-ttu-id="b40ee-144">CloudMonix</span><span class="sxs-lookup"><span data-stu-id="b40ee-144">CloudMonix</span></span>
<span data-ttu-id="b40ee-145">CloudMonix 提供 Microsoft Azure 平台的監視、自動化和自我修復服務。</span><span class="sxs-lookup"><span data-stu-id="b40ee-145">CloudMonix offers monitoring, automation and self-healing services for Microsoft Azure platform.</span></span>

<span data-ttu-id="b40ee-146">[移 toohello 文件。][cloudmonix-doc]</span><span class="sxs-lookup"><span data-stu-id="b40ee-146">[Go toohello documentation.][cloudmonix-doc]</span></span>

## <a name="cloudyn"></a><span data-ttu-id="b40ee-147">Cloudyn</span><span class="sxs-lookup"><span data-stu-id="b40ee-147">Cloudyn</span></span>
<span data-ttu-id="b40ee-148">Cloudyn 管理並最佳化多平台，混合式雲端部署 toohelp 企業完全了解其雲端可能性。</span><span class="sxs-lookup"><span data-stu-id="b40ee-148">Cloudyn manages and optimizes multi-platform, hybrid cloud deployments toohelp enterprises fully realize their cloud potential.</span></span> <span data-ttu-id="b40ee-149">hello SaaS 解決方案提供可見性使用量、 效能和成本，結合 insights 和智慧的最佳化和雲端控管可採取動作的建議。</span><span class="sxs-lookup"><span data-stu-id="b40ee-149">hello SaaS solution delivers visibility into usage, performance and cost, coupled with insights and actionable recommendations for smart optimization and cloud governance.</span></span> <span data-ttu-id="b40ee-150">Cloudyn 可透過精確的退款和階層式成本配置管理來提供權責。</span><span class="sxs-lookup"><span data-stu-id="b40ee-150">Cloudyn enables accountability through accurate chargeback and hierarchical cost allocation management.</span></span> <span data-ttu-id="b40ee-151">Cloudyn 是與整合 Azure 監視順序 tooprovide insights 中，可採取動作的建議事項中排序 toooptimize 您的 Azure 部署。</span><span class="sxs-lookup"><span data-stu-id="b40ee-151">Cloudyn is integrated with Azure Monitoring in order tooprovide insights and actionable recommendations in order toooptimize your Azure deployment.</span></span>

<span data-ttu-id="b40ee-152">[移 toohello 文件。][cloudyn-doc]</span><span class="sxs-lookup"><span data-stu-id="b40ee-152">[Go toohello documentation.][cloudyn-doc]</span></span>

## <a name="datadog"></a><span data-ttu-id="b40ee-153">Datadog</span><span class="sxs-lookup"><span data-stu-id="b40ee-153">Datadog</span></span>
<span data-ttu-id="b40ee-154">Datadog 監視雲端規模的應用程式服務的 hello world 前置將從伺服器、 資料庫、 工具、 結合在一起的資料，而且服務 toopresent 您整個堆疊的統一檢視。</span><span class="sxs-lookup"><span data-stu-id="b40ee-154">Datadog is hello world’s leading monitoring service for cloud-scale applications, bringing together data from servers, databases, tools, and services toopresent a unified view of your entire stack.</span></span> <span data-ttu-id="b40ee-155">這些功能會提供可讓開發人員和 Ops 小組 toowork 共同的 SaaS 基礎的資料分析平台上 tooavoid 停機時間，解決效能問題，並確保開發和部署週期完成。</span><span class="sxs-lookup"><span data-stu-id="b40ee-155">These capabilities are provided on a SaaS-based data analytics platform that enables Dev and Ops teams toowork collaboratively tooavoid downtime, resolve performance problems, and ensure that development and deployment cycles finish on time.</span></span> <span data-ttu-id="b40ee-156">藉由整合 Datadog 和 Azure，您可以從整個基礎結構收集並檢視度量、將 VM 度量與應用程式層級的度量互相關聯，並使用任何組合的屬性和自訂標籤將您度量進行配量及分解。</span><span class="sxs-lookup"><span data-stu-id="b40ee-156">By integrating Datadog and Azure, you can collect and view metrics from across your infrastructure, correlate VM metrics with application-level metrics, and slice and dice your metrics using any combination of properties and custom tags.</span></span>

<span data-ttu-id="b40ee-157">[移 toohello 文件。][datadog-doc]</span><span class="sxs-lookup"><span data-stu-id="b40ee-157">[Go toohello documentation.][datadog-doc]</span></span>

## <a name="dynatrace"></a><span data-ttu-id="b40ee-158">Dynatrace</span><span class="sxs-lookup"><span data-stu-id="b40ee-158">Dynatrace</span></span>
<span data-ttu-id="b40ee-159">hello Dynatrace OneAgent 透過 hello Azure 的延伸模組機制會與 Azure Vm 和服務應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="b40ee-159">hello Dynatrace OneAgent integrates with Azure VMs and App Services via hello Azure extension mechanism.</span></span> <span data-ttu-id="b40ee-160">如此一來，Dynatrace OneAgent 便可以收集有關主機、網路和服務的效能計量。</span><span class="sxs-lookup"><span data-stu-id="b40ee-160">This way Dynatrace OneAgent can gather performance metrics about hosts, network, and services.</span></span> <span data-ttu-id="b40ee-161">除了只顯示度量 Dynatrace 視覺化環境端對端，顯示 hello 用戶端端 toohello 資料庫層級的交易。</span><span class="sxs-lookup"><span data-stu-id="b40ee-161">Besides just displaying metrics Dynatrace visualizes environments end-to-end, showing transactions from hello client side toohello database layer.</span></span> <span data-ttu-id="b40ee-162">以 AI 為基礎的問題相互關連與完全整合式根本原因分析，包括程式碼和資料庫的方法層級深入見解，讓疑難排解和效能最佳化工作更輕鬆。</span><span class="sxs-lookup"><span data-stu-id="b40ee-162">AI-based correlation of problems and fully integrated root-cause-analysis, including method level insights into code and database, make troubleshooting and performance optimizations much easier.</span></span>

<span data-ttu-id="b40ee-163">[移 toohello 文件。][dynatrace-doc]</span><span class="sxs-lookup"><span data-stu-id="b40ee-163">[Go toohello documentation.][dynatrace-doc]</span></span>

## <a name="newrelic"></a><span data-ttu-id="b40ee-164">NewRelic</span><span class="sxs-lookup"><span data-stu-id="b40ee-164">NewRelic</span></span>
<span data-ttu-id="b40ee-165">[深入了解。][newrelic-doc]</span><span class="sxs-lookup"><span data-stu-id="b40ee-165">[Learn more.][newrelic-doc]</span></span>

## <a name="opsgenie"></a><span data-ttu-id="b40ee-166">OpsGenie</span><span class="sxs-lookup"><span data-stu-id="b40ee-166">OpsGenie</span></span>
<span data-ttu-id="b40ee-167">OpsGenie 作用，如同由 Azure 產生 hello 警示的發送器。</span><span class="sxs-lookup"><span data-stu-id="b40ee-167">OpsGenie acts as a dispatcher for hello alerts generated by Azure.</span></span> <span data-ttu-id="b40ee-168">OpsGenie 決定 hello 適當人員 toonotify 根據上呼叫排程和擴大議題，通知他們使用電子郵件、 簡訊 (SMS)、 電話，將推播通知。</span><span class="sxs-lookup"><span data-stu-id="b40ee-168">OpsGenie determines hello right people toonotify based on on-call schedules and escalations, by notifying them using email, text messages (SMS), phone calls, push notifications.</span></span> <span data-ttu-id="b40ee-169">只要，Azure 會產生警示的 [偵測到的問題，並 OpsGenie 可確保 hello 適當人員處理這些。</span><span class="sxs-lookup"><span data-stu-id="b40ee-169">Simply, Azure generates alerts for detected problems, and OpsGenie ensures hello right people are working on them.</span></span>

<span data-ttu-id="b40ee-170">[移 toohello 文件。][opsgenie-doc]</span><span class="sxs-lookup"><span data-stu-id="b40ee-170">[Go toohello documentation.][opsgenie-doc]</span></span>

## <a name="pagerduty"></a><span data-ttu-id="b40ee-171">PagerDuty</span><span class="sxs-lookup"><span data-stu-id="b40ee-171">PagerDuty</span></span>
<span data-ttu-id="b40ee-172">PagerDuty，hello 開頭事件的管理解決方案，提供第一級支援 Azure 警示的度量。</span><span class="sxs-lookup"><span data-stu-id="b40ee-172">PagerDuty, hello leading incident management solution, has provided first-class support for Azure Alerts on metrics.</span></span> <span data-ttu-id="b40ee-173">現在，PagerDuty 現在支援通知 Azure 監視警示、 自動調整規模通知及稽核記錄檔事件，在加法 toonotifications 上 Azure 服務的平台層級度量。</span><span class="sxs-lookup"><span data-stu-id="b40ee-173">Today, PagerDuty now supports notifications on Azure Monitor Alerts, Autoscale Notifications, and Audit Log Events, in addition toonotifications on platform-level metrics for Azure services.</span></span> <span data-ttu-id="b40ee-174">這些增強功能授與使用者進一步的掌握 hello 核心 Azure 平台時啟用它們 tootake 充分利用即時回應 PagerDuty 的事件管理功能。</span><span class="sxs-lookup"><span data-stu-id="b40ee-174">These enhancements give users increased visibility into hello core Azure Platform while enabling them tootake full advantage of PagerDuty’s incident management capabilities for real-time response.</span></span> <span data-ttu-id="b40ee-175">我們透過 webhook 實現擴充的 Azure 整合，以供快速且輕鬆的設定與自訂。</span><span class="sxs-lookup"><span data-stu-id="b40ee-175">Our expanded Azure integration is made possible via webhooks, allowing for quick and easy set-up and customization.</span></span>

<span data-ttu-id="b40ee-176">[移 toohello 文件。][pagerduty-doc]</span><span class="sxs-lookup"><span data-stu-id="b40ee-176">[Go toohello documentation.][pagerduty-doc]</span></span>

## <a name="sciencelogic"></a><span data-ttu-id="b40ee-177">ScienceLogic</span><span class="sxs-lookup"><span data-stu-id="b40ee-177">ScienceLogic</span></span>
<span data-ttu-id="b40ee-178">ScienceLogic 傳送 hello 新一代 IT 服務保證平台來管理任何技術，任何位置。</span><span class="sxs-lookup"><span data-stu-id="b40ee-178">ScienceLogic delivers hello next generation IT service assurance platform for managing any technology, anywhere.</span></span>  <span data-ttu-id="b40ee-179">一個平台，ScienceLogic 傳送 hello 小數位數、 安全性、 自動化和恢復功能所需的 toosimplify hello 不斷擴充的工作管理 IT 資源、 服務和應用程式在常數。</span><span class="sxs-lookup"><span data-stu-id="b40ee-179">In one platform, ScienceLogic delivers hello scale, security, automation, and resiliency necessary toosimplify hello ever-expanding task of managing IT resources, services, and applications that are in constant motion.</span></span>  <span data-ttu-id="b40ee-180">hello ScienceLogic 平台會使用 Microsoft Azure 中的 Azure 應用程式開發介面 toointerface。</span><span class="sxs-lookup"><span data-stu-id="b40ee-180">hello ScienceLogic platform uses Azure APIs toointerface with Microsoft Azure.</span></span>  <span data-ttu-id="b40ee-181">ScienceLogic 可讓您即時掌握您的 Azure 服務和資源，以便您知道項目沒有運作，且可以更快速修正它。</span><span class="sxs-lookup"><span data-stu-id="b40ee-181">ScienceLogic gives you real-time visibility into your Azure services and resources so you know when something’s not working and can fix it faster.</span></span> <span data-ttu-id="b40ee-182">您也可以與其他雲端和資料中心系統和服務管理 Azure。</span><span class="sxs-lookup"><span data-stu-id="b40ee-182">You can also manage Azure alongside your other clouds and data center systems and services.</span></span>

<span data-ttu-id="b40ee-183">[深入了解。][sciencelogic-doc]</span><span class="sxs-lookup"><span data-stu-id="b40ee-183">[Learn more.][sciencelogic-doc]</span></span>

## <a name="azure-monitor-add-on-for-splunk"></a><span data-ttu-id="b40ee-184">Splunk 適用的 Azure 監視器附加元件</span><span class="sxs-lookup"><span data-stu-id="b40ee-184">Azure Monitor Add-on for Splunk</span></span>
<span data-ttu-id="b40ee-185">hello Splunk 的 Azure 監視附加元件是[用於 hello 這裡 Splunkbase](https://splunkbase.splunk.com/app/3534/)。</span><span class="sxs-lookup"><span data-stu-id="b40ee-185">hello Azure Monitor Add-on for Splunk is [available in hello Splunkbase here](https://splunkbase.splunk.com/app/3534/).</span></span>

<span data-ttu-id="b40ee-186">[移 toohello 文件。][splunk-doc]</span><span class="sxs-lookup"><span data-stu-id="b40ee-186">[Go toohello documentation.][splunk-doc]</span></span>

## <a name="sumo-logic"></a><span data-ttu-id="b40ee-187">Sumo Logic</span><span class="sxs-lookup"><span data-stu-id="b40ee-187">Sumo Logic</span></span>
<span data-ttu-id="b40ee-188">Sumo Logic 是安全、 雲端原生機器資料分析服務，將即時、 連續智慧跨 hello 整個應用程式生命週期和堆疊傳遞結構化、 半結構化及未結構化資料。</span><span class="sxs-lookup"><span data-stu-id="b40ee-188">Sumo Logic is a secure, cloud-native, machine data analytics service, delivering real-time, continuous intelligence from structured, semi-structured, and unstructured data across hello entire application lifecycle and stack.</span></span> <span data-ttu-id="b40ee-189">Hello 全球各地的超過 1,000 個客戶保證 Sumo Logic hello 分析和深入觀點 toobuild，執行，並保護其的現代應用程式和雲端基礎結構。</span><span class="sxs-lookup"><span data-stu-id="b40ee-189">More than 1,000 customers around hello globe rely on Sumo Logic for hello analytics and insights toobuild, run, and secure their modern applications and cloud infrastructures.</span></span> <span data-ttu-id="b40ee-190">使用 Sumo Logic 客戶取得多租用戶，服務模型利用 tooaccelerate 其 shift toocontinuous 的創新，增加競爭優勢、 商務價值和成長。</span><span class="sxs-lookup"><span data-stu-id="b40ee-190">With Sumo Logic, customers gain a multi-tenant, service-model advantage tooaccelerate their shift toocontinuous innovation, increasing competitive advantage, business value, and growth.</span></span>

<span data-ttu-id="b40ee-191">[深入了解。][sumologic-doc]</span><span class="sxs-lookup"><span data-stu-id="b40ee-191">[Learn more.][sumologic-doc]</span></span>

## <a name="next-steps"></a><span data-ttu-id="b40ee-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b40ee-192">Next Steps</span></span>
* [<span data-ttu-id="b40ee-193">深入了解 Azure 監視器</span><span class="sxs-lookup"><span data-stu-id="b40ee-193">Learn more about Azure Monitor</span></span>](monitoring-overview.md)
* [<span data-ttu-id="b40ee-194">使用 hello REST API 的存取度量</span><span class="sxs-lookup"><span data-stu-id="b40ee-194">Access metrics using hello REST API</span></span>](monitoring-rest-api-walkthrough.md)
* [<span data-ttu-id="b40ee-195">資料流 hello 活動記錄檔 tooa 協力廠商服務</span><span class="sxs-lookup"><span data-stu-id="b40ee-195">Stream hello Activity Log tooa third party service</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="b40ee-196">資料流診斷記錄檔 tooa 協力廠商服務</span><span class="sxs-lookup"><span data-stu-id="b40ee-196">Stream Diagnostic Logs tooa third party service</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

<!--Partner Anchors-->
[alertlogic-anchor]: #alertlogic-log-manager "AlertLogic"
[appdynamics-anchor]: #appdynamics "AppDynamics"
[atlassian-anchor]: #atlassian-jira "Atlassian"
[circonus-anchor]: #circonus "Circonus"
[cloudhealth-anchor]: #cloudhealth "CloudHealth"
[cloudmonix-anchor]: #cloudmonix "CloudMonix"
[cloudyn-anchor]: #cloudyn "Cloudyn"
[datadog-anchor]: #datadog "Datadog"
[dynatrace-anchor]: #dynatrace "Dynatrace"
[newrelic-anchor]: #newrelic "NewRelic"
[opsgenie-anchor]: #opsgenie "OpsGenie"
[pagerduty-anchor]: #pagerduty "PagerDuty"
[sciencelogic-anchor]: #sciencelogic "ScienceLogic"
[splunk-anchor]: #azure-monitor-add-on-for-splunk "Splunk"
[sumologic-anchor]: #sumo-logic "Sumo Logic"

<!--Icon references-->
[alertlogic-logo]: ./media/partner-logos/alertlogic.png
[appdynamics-logo]: ./media/partner-logos/appdynamics.png
[atlassian-logo]: ./media/partner-logos/atlassian.png
[circonus-logo]: ./media/partner-logos/circonus.png
[cloudhealth-logo]: ./media/partner-logos/cloudhealth.png
[cloudmonix-logo]: ./media/partner-logos/cloudmonix.png
[cloudyn-logo]: ./media/partner-logos/cloudyn.png
[datadog-logo]: ./media/partner-logos/datadog.png
[dynatrace-logo]: ./media/partner-logos/dynatrace.png
[newrelic-logo]: ./media/partner-logos/newrelic.png
[opsgenie-logo]: ./media/partner-logos/opsgenie.png
[pagerduty-logo]: ./media/partner-logos/pagerduty.png
[sciencelogic-logo]: ./media/partner-logos/sciencelogic.png
[splunk-logo]: ./media/partner-logos/splunk.png
[sumologic-logo]: ./media/partner-logos/sumologic.png

<!--Partner Documentation-->
[alertlogic-doc]: https://docs.alertlogic.com/userGuides/log-manager-collection-sources.htm "AlertLogic 文件。"
[appdynamics-doc]: https://www.appdynamics.com/net/azure/ "AppDynamics 文件。"
[atlassian-doc]: https://azure.microsoft.com/blog/automated-notifications-from-azure-monitor-for-atlassian-jira/
[circonus-doc]: https://support.circonus.com/support/solutions/articles/24000013515-azure-integration 
[cloudhealth-doc]: https://www.cloudhealthtech.com/azure
[cloudmonix-doc]: http://cloudmonix.com/features/azure-management/ "CloudMonix 簡介。"
[cloudyn-doc]: https://www.cloudyn.com/azure-monitoring "Cloudyn 簡介。"
[datadog-doc]: http://docs.datadoghq.com/integrations/azure/ "Datadog 文件。"
[dynatrace-doc]: https://help.dynatrace.com/infrastructure-monitoring/paas/how-do-i-monitor-microsoft-azure-web-apps/ "Dynatrace 文件。"
[newrelic-doc]: https://newrelic.com/azure "NewRelic 文件。"
[opsgenie-doc]: https://www.opsgenie.com/docs/integrations/azure-integration "OpsGenie 文件。"
[pagerduty-doc]: https://www.pagerduty.com/docs/guides/azure-integration-guide/ "PagerDuty 文件。"
[sciencelogic-doc]: https://www.sciencelogic.com/product/technologies/microsoft/azure "ScienceLogic 文件。"
[splunk-doc]: https://github.com/Microsoft/AzureMonitorAddonForSplunk/wiki/Azure-Monitor-Addon-For-Splunk "Splunk 文件。"
[sumologic-doc]: https://www.sumologic.com/azure "SumoLogic 文件。"

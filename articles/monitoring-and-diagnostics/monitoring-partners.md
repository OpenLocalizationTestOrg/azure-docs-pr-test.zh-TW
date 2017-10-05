---
title: "Azure 監視器合作夥伴整合 | Microsoft Docs"
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
ms.openlocfilehash: 46b6ec12655b64b8fce6e103d5d71a4e8021890e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-monitor-partner-integrations"></a><span data-ttu-id="38ccc-103">Azure 監視器合作夥伴整合</span><span class="sxs-lookup"><span data-stu-id="38ccc-103">Azure Monitor partner integrations</span></span>
| <span data-ttu-id="38ccc-104">合作夥伴</span><span class="sxs-lookup"><span data-stu-id="38ccc-104">Partners</span></span> |  |  |
| --- | --- | --- |
| <span data-ttu-id="38ccc-105">[![合作夥伴標誌][alertlogic-logo]<br/>**AlertLogic**][alertlogic-anchor]</span><span class="sxs-lookup"><span data-stu-id="38ccc-105">[![Partner Logo][alertlogic-logo]<br/>**AlertLogic**][alertlogic-anchor]</span></span> | <span data-ttu-id="38ccc-106">[![合作夥伴標誌][appdynamics-logo]<br/>**AppDynamics**][appdynamics-anchor]</span><span class="sxs-lookup"><span data-stu-id="38ccc-106">[![Partner Logo][appdynamics-logo]<br/>**AppDynamics**][appdynamics-anchor]</span></span> | <span data-ttu-id="38ccc-107">[![合作夥伴標誌][atlassian-logo]<br/>**Atlassian**][atlassian-anchor]</span><span class="sxs-lookup"><span data-stu-id="38ccc-107">[![Partner Logo][atlassian-logo]<br/>**Atlassian**][atlassian-anchor]</span></span> |
| <span data-ttu-id="38ccc-108">[![Partner Logo][circonus-logo]<br/>**Circonus**][circonus-anchor]</span><span class="sxs-lookup"><span data-stu-id="38ccc-108">[![Partner Logo][circonus-logo]<br/>**Circonus**][circonus-anchor]</span></span> | <span data-ttu-id="38ccc-109">[![合作夥伴標誌][cloudhealth-logo]<br/>**CloudHealth**][cloudhealth-anchor]</span><span class="sxs-lookup"><span data-stu-id="38ccc-109">[![Partner Logo][cloudhealth-logo]<br/>**CloudHealth**][cloudhealth-anchor]</span></span> | <span data-ttu-id="38ccc-110">[![合作夥伴標誌][cloudmonix-logo]<br/>**CloudMonix**][cloudmonix-anchor]</span><span class="sxs-lookup"><span data-stu-id="38ccc-110">[![Partner Logo][cloudmonix-logo]<br/>**CloudMonix**][cloudmonix-anchor]</span></span> |
| <span data-ttu-id="38ccc-111">[![合作夥伴標誌][cloudyn-logo]<br/>**Cloudyn**][cloudyn-anchor]</span><span class="sxs-lookup"><span data-stu-id="38ccc-111">[![Partner Logo][cloudyn-logo]<br/>**Cloudyn**][cloudyn-anchor]</span></span> | <span data-ttu-id="38ccc-112">[![Partner Logo][datadog-logo]<br/>**Datadog**][datadog-anchor]</span><span class="sxs-lookup"><span data-stu-id="38ccc-112">[![Partner Logo][datadog-logo]<br/>**Datadog**][datadog-anchor]</span></span> | <span data-ttu-id="38ccc-113">[![合作夥伴標誌][dynatrace-logo]<br/>**Dynatrace**][dynatrace-anchor]</span><span class="sxs-lookup"><span data-stu-id="38ccc-113">[![Partner Logo][dynatrace-logo]<br/>**Dynatrace**][dynatrace-anchor]</span></span> |
| <span data-ttu-id="38ccc-114">[![合作夥伴標誌][newrelic-logo]<br/>**NewRelic**][newrelic-anchor]</span><span class="sxs-lookup"><span data-stu-id="38ccc-114">[![Partner Logo][newrelic-logo]<br/>**NewRelic**][newrelic-anchor]</span></span> | <span data-ttu-id="38ccc-115">[![合作夥伴標誌][opsgenie-logo]<br/>**OpsGenie**][opsgenie-anchor]</span><span class="sxs-lookup"><span data-stu-id="38ccc-115">[![Partner Logo][opsgenie-logo]<br/>**OpsGenie**][opsgenie-anchor]</span></span> | <span data-ttu-id="38ccc-116">[![合作夥伴標誌][pagerduty-logo]<br/>**PagerDuty**][pagerduty-anchor]</span><span class="sxs-lookup"><span data-stu-id="38ccc-116">[![Partner Logo][pagerduty-logo]<br/>**PagerDuty**][pagerduty-anchor]</span></span> |
| <span data-ttu-id="38ccc-117">[![合作夥伴標誌][sciencelogic-logo]<br/>**ScienceLogic**][sciencelogic-anchor]</span><span class="sxs-lookup"><span data-stu-id="38ccc-117">[![Partner Logo][sciencelogic-logo]<br/>**ScienceLogic**][sciencelogic-anchor]</span></span> | <span data-ttu-id="38ccc-118">[![合作夥伴標誌][splunk-logo]<br/>**Splunk**][splunk-anchor]</span><span class="sxs-lookup"><span data-stu-id="38ccc-118">[![Partner Logo][splunk-logo]<br/>**Splunk**][splunk-anchor]</span></span> | <span data-ttu-id="38ccc-119">[![合作夥伴標誌][sumologic-logo]<br/>**Sumo Logic**][sumologic-anchor]</span><span class="sxs-lookup"><span data-stu-id="38ccc-119">[![Partner Logo][sumologic-logo]<br/>**Sumo Logic**][sumologic-anchor]</span></span> | |

## <a name="alertlogic-log-manager"></a><span data-ttu-id="38ccc-120">AlertLogic Log Manager</span><span class="sxs-lookup"><span data-stu-id="38ccc-120">AlertLogic Log Manager</span></span>
<span data-ttu-id="38ccc-121">Alert Logic Log Manager 會收集 VM、應用程式和 Azure 平台記錄來進行安全分析和保留，包括透過 Azure 監視器 API 的 Azure 活動記錄。</span><span class="sxs-lookup"><span data-stu-id="38ccc-121">Alert Logic Log Manager collects VM, Application, and Azure platform logs for security analysis and retention, including the Azure Activity Log via the Azure Monitor API.</span></span>  <span data-ttu-id="38ccc-122">這項資訊用於偵測 malfeasance 及符合法務遵循需求。</span><span class="sxs-lookup"><span data-stu-id="38ccc-122">This information is used to detect malfeasance and meet compliance requirements.</span></span>

<span data-ttu-id="38ccc-123">[請移至文件。][alertlogic-doc]</span><span class="sxs-lookup"><span data-stu-id="38ccc-123">[Go to the documentation.][alertlogic-doc]</span></span>

## <a name="appdynamics"></a><span data-ttu-id="38ccc-124">AppDynamics</span><span class="sxs-lookup"><span data-stu-id="38ccc-124">AppDynamics</span></span>
<span data-ttu-id="38ccc-125">AppDynamics 應用程式效能管理 (APM) 可讓應用程式擁有者快速針對效能瓶頸進行疑難排解，並將其在 Azure 環境中執行的應用程式效能進行最佳化。</span><span class="sxs-lookup"><span data-stu-id="38ccc-125">AppDynamics Application Performance Management (APM) enables application owners to rapidly troubleshoot performance bottlenecks and optimize the performance of their applications running in Azure environment.</span></span> <span data-ttu-id="38ccc-126">AppDynamics APM 與 Azure Marketplace 順暢地進行整合，並可供監視 Azure 雲端服務 (PaaS) (包括 web 和背景工作角色)、虛擬機器 (IaaS)、遠端服務偵測 (Microsoft Azure 服務匯流排)、Microsoft Azure 佇列 Microsoft Azure 遠端服務 (Azure Blob)、Azure 佇列 (Microsoft 服務匯流排)、資料儲存體及 Microsoft Azure Blob 儲存體使用。</span><span class="sxs-lookup"><span data-stu-id="38ccc-126">AppDynamics APM is seamlessly integrated with Azure Marketplace and available for monitor Azure Cloud Services (PaaS) (Including web & worker roles), Virtual Machines (IaaS), Remote Service Detection (Microsoft Azure Service Bus), Microsoft Azure Queue Microsoft Azure Remote Services (Azure Blob), Azure Queue (Microsoft Service Bus), Data Storage, Microsoft Azure Blob Storage.</span></span>

<span data-ttu-id="38ccc-127">[請移至文件。][appdynamics-doc]</span><span class="sxs-lookup"><span data-stu-id="38ccc-127">[Go to the documentation.][appdynamics-doc]</span></span>

## <a name="atlassian-jira"></a><span data-ttu-id="38ccc-128">Atlassian JIRA</span><span class="sxs-lookup"><span data-stu-id="38ccc-128">Atlassian JIRA</span></span>
<span data-ttu-id="38ccc-129">您可以對 Azure 監視器警示建立 JIRA 票證。</span><span class="sxs-lookup"><span data-stu-id="38ccc-129">You can create JIRA tickets on Azure Monitor alerts.</span></span>

<span data-ttu-id="38ccc-130">[請移至文件。][atlassian-doc]</span><span class="sxs-lookup"><span data-stu-id="38ccc-130">[Go to the documentation.][atlassian-doc]</span></span>

## <a name="circonus"></a><span data-ttu-id="38ccc-131">Circonus</span><span class="sxs-lookup"><span data-stu-id="38ccc-131">Circonus</span></span>
<span data-ttu-id="38ccc-132">Circonus 是針對內部部署或 SaaS 部署建置的微服務監視和分析平台。</span><span class="sxs-lookup"><span data-stu-id="38ccc-132">Circonus is a microservices monitoring and analytics platform built for on premises or SaaS deployment.</span></span> <span data-ttu-id="38ccc-133">其以 API 為主的完整自動化平台比其監視的系統更具擴充性和且更可靠。</span><span class="sxs-lookup"><span data-stu-id="38ccc-133">Its fully automatable API-Centric platform is more scalable and reliable than systems it monitors.</span></span> <span data-ttu-id="38ccc-134">Circonus 是針對 DevOps 需求所開發，能提供以百分位數為基礎的警示、圖表、儀表板及讓商業最佳化的機器學習智慧。</span><span class="sxs-lookup"><span data-stu-id="38ccc-134">Developed for the requirements of DevOps, Circonus delivers percentile-based alerts, graphs, dashboards, and machine-learning intelligence that enable business optimization.</span></span> <span data-ttu-id="38ccc-135">Circonus 會即時監視 Microsoft Azure 雲端資源和其應用程式。</span><span class="sxs-lookup"><span data-stu-id="38ccc-135">Circonus monitors your Microsoft Azure cloud resources and their applications in real time.</span></span> <span data-ttu-id="38ccc-136">您可以使用 Circonus 來收集並追蹤您需要針對資源和應用程式測量之變數的計量。</span><span class="sxs-lookup"><span data-stu-id="38ccc-136">You can use Circonus to collect and track metrics for the variables you want to measure for your resources and applications.</span></span> <span data-ttu-id="38ccc-137">您可以使用 Circonus 來查看整個系統，了解 Azure 的資源使用量、應用程式效能和操作健康情況。</span><span class="sxs-lookup"><span data-stu-id="38ccc-137">With Circonus, you gain system-wide visibility into Azure’s resource utilization, application performance, and operational health.</span></span>

<span data-ttu-id="38ccc-138">[請移至文件。][circonus-doc]</span><span class="sxs-lookup"><span data-stu-id="38ccc-138">[Go to the documentation.][circonus-doc]</span></span>

## <a name="cloudhealth"></a><span data-ttu-id="38ccc-139">CloudHealth</span><span class="sxs-lookup"><span data-stu-id="38ccc-139">CloudHealth</span></span>
<span data-ttu-id="38ccc-140">使用建置來節省嚴重的時間和金錢的平台聯集並自動化您的雲端。</span><span class="sxs-lookup"><span data-stu-id="38ccc-140">Unite and automate your cloud with a platform built to save serious time and money.</span></span> <span data-ttu-id="38ccc-141">使用前所未有的可見性、直覺式最佳化和穩固控管的作法，CloudHealth 會重新定義雲端管理。</span><span class="sxs-lookup"><span data-stu-id="38ccc-141">With unparalleled visibility, intuitive optimization and rock-solid governance practices, CloudHealth is redefining cloud management.</span></span> <span data-ttu-id="38ccc-142">Cloudhealth 平台可讓企業和 MSP 最大化雲端的投資報酬率，並確信成本、使用狀況、效能和安全性的決定。</span><span class="sxs-lookup"><span data-stu-id="38ccc-142">The Cloudhealth platform enables enterprises and MSPs to maximize return on cloud investments and make confident decisions around cost, usage, performance and security.</span></span>

<span data-ttu-id="38ccc-143">[深入了解。][cloudhealth-doc]</span><span class="sxs-lookup"><span data-stu-id="38ccc-143">[Learn More.][cloudhealth-doc]</span></span>

## <a name="cloudmonix"></a><span data-ttu-id="38ccc-144">CloudMonix</span><span class="sxs-lookup"><span data-stu-id="38ccc-144">CloudMonix</span></span>
<span data-ttu-id="38ccc-145">CloudMonix 提供 Microsoft Azure 平台的監視、自動化和自我修復服務。</span><span class="sxs-lookup"><span data-stu-id="38ccc-145">CloudMonix offers monitoring, automation and self-healing services for Microsoft Azure platform.</span></span>

<span data-ttu-id="38ccc-146">[請移至文件。][cloudmonix-doc]</span><span class="sxs-lookup"><span data-stu-id="38ccc-146">[Go to the documentation.][cloudmonix-doc]</span></span>

## <a name="cloudyn"></a><span data-ttu-id="38ccc-147">Cloudyn</span><span class="sxs-lookup"><span data-stu-id="38ccc-147">Cloudyn</span></span>
<span data-ttu-id="38ccc-148">Cloudyn 管理並最佳化 Multi-Platform、Hybrid Cloud Deployment 以協助企業完全了解它們的雲端潛力。</span><span class="sxs-lookup"><span data-stu-id="38ccc-148">Cloudyn manages and optimizes multi-platform, hybrid cloud deployments to help enterprises fully realize their cloud potential.</span></span> <span data-ttu-id="38ccc-149">SaaS 解決方案可讓您看見使用量、效能和成本，並提供深入見解及可行的建議，以進行智慧的最佳化和雲端控管。</span><span class="sxs-lookup"><span data-stu-id="38ccc-149">The SaaS solution delivers visibility into usage, performance and cost, coupled with insights and actionable recommendations for smart optimization and cloud governance.</span></span> <span data-ttu-id="38ccc-150">Cloudyn 可透過精確的退款和階層式成本配置管理來提供權責。</span><span class="sxs-lookup"><span data-stu-id="38ccc-150">Cloudyn enables accountability through accurate chargeback and hierarchical cost allocation management.</span></span> <span data-ttu-id="38ccc-151">Cloudyn 與 Azure 監視進行整合，以提供深入見解及可行的建議，將您的 Azure 部署進行最佳化。</span><span class="sxs-lookup"><span data-stu-id="38ccc-151">Cloudyn is integrated with Azure Monitoring in order to provide insights and actionable recommendations in order to optimize your Azure deployment.</span></span>

<span data-ttu-id="38ccc-152">[請移至文件。][cloudyn-doc]</span><span class="sxs-lookup"><span data-stu-id="38ccc-152">[Go to the documentation.][cloudyn-doc]</span></span>

## <a name="datadog"></a><span data-ttu-id="38ccc-153">Datadog</span><span class="sxs-lookup"><span data-stu-id="38ccc-153">Datadog</span></span>
<span data-ttu-id="38ccc-154">Datadog 是全球領先的雲端規模應用程式監視服務，將伺服器、資料庫、工具和服務的資料進行結合，呈現您整個堆疊的統一檢視。</span><span class="sxs-lookup"><span data-stu-id="38ccc-154">Datadog is the world’s leading monitoring service for cloud-scale applications, bringing together data from servers, databases, tools, and services to present a unified view of your entire stack.</span></span> <span data-ttu-id="38ccc-155">這些功能會提供於以 SaaS 為基礎的資料分析平台上，讓開發和作業團隊可協同運作，以避免停機時間、解決效能問題，並確保開發及部署週期能準時完成。</span><span class="sxs-lookup"><span data-stu-id="38ccc-155">These capabilities are provided on a SaaS-based data analytics platform that enables Dev and Ops teams to work collaboratively to avoid downtime, resolve performance problems, and ensure that development and deployment cycles finish on time.</span></span> <span data-ttu-id="38ccc-156">藉由整合 Datadog 和 Azure，您可以從整個基礎結構收集並檢視度量、將 VM 度量與應用程式層級的度量互相關聯，並使用任何組合的屬性和自訂標籤將您度量進行配量及分解。</span><span class="sxs-lookup"><span data-stu-id="38ccc-156">By integrating Datadog and Azure, you can collect and view metrics from across your infrastructure, correlate VM metrics with application-level metrics, and slice and dice your metrics using any combination of properties and custom tags.</span></span>

<span data-ttu-id="38ccc-157">[請移至文件。][datadog-doc]</span><span class="sxs-lookup"><span data-stu-id="38ccc-157">[Go to the documentation.][datadog-doc]</span></span>

## <a name="dynatrace"></a><span data-ttu-id="38ccc-158">Dynatrace</span><span class="sxs-lookup"><span data-stu-id="38ccc-158">Dynatrace</span></span>
<span data-ttu-id="38ccc-159">Dynatrace OneAgent 會透過 Azure 延伸模組機制來與 Azure VM 和應用程式服務進行整合。</span><span class="sxs-lookup"><span data-stu-id="38ccc-159">The Dynatrace OneAgent integrates with Azure VMs and App Services via the Azure extension mechanism.</span></span> <span data-ttu-id="38ccc-160">如此一來，Dynatrace OneAgent 便可以收集有關主機、網路和服務的效能計量。</span><span class="sxs-lookup"><span data-stu-id="38ccc-160">This way Dynatrace OneAgent can gather performance metrics about hosts, network, and services.</span></span> <span data-ttu-id="38ccc-161">除了只顯示計量之外，Dynatrace 還會針對環境進行端對端視覺化，顯示從用戶端至資料庫層級的交易。</span><span class="sxs-lookup"><span data-stu-id="38ccc-161">Besides just displaying metrics Dynatrace visualizes environments end-to-end, showing transactions from the client side to the database layer.</span></span> <span data-ttu-id="38ccc-162">以 AI 為基礎的問題相互關連與完全整合式根本原因分析，包括程式碼和資料庫的方法層級深入見解，讓疑難排解和效能最佳化工作更輕鬆。</span><span class="sxs-lookup"><span data-stu-id="38ccc-162">AI-based correlation of problems and fully integrated root-cause-analysis, including method level insights into code and database, make troubleshooting and performance optimizations much easier.</span></span>

<span data-ttu-id="38ccc-163">[請移至文件。][dynatrace-doc]</span><span class="sxs-lookup"><span data-stu-id="38ccc-163">[Go to the documentation.][dynatrace-doc]</span></span>

## <a name="newrelic"></a><span data-ttu-id="38ccc-164">NewRelic</span><span class="sxs-lookup"><span data-stu-id="38ccc-164">NewRelic</span></span>
<span data-ttu-id="38ccc-165">[深入了解。][newrelic-doc]</span><span class="sxs-lookup"><span data-stu-id="38ccc-165">[Learn more.][newrelic-doc]</span></span>

## <a name="opsgenie"></a><span data-ttu-id="38ccc-166">OpsGenie</span><span class="sxs-lookup"><span data-stu-id="38ccc-166">OpsGenie</span></span>
<span data-ttu-id="38ccc-167">OpsGenie 作為由 Azure 所產生警示發送器。</span><span class="sxs-lookup"><span data-stu-id="38ccc-167">OpsGenie acts as a dispatcher for the alerts generated by Azure.</span></span> <span data-ttu-id="38ccc-168">OpsGenie 會根據值勤排程及呈核來決定要通知的適當人員，並使用電子郵件、簡訊 (SMS)、電話、推播通知對他們進行通知。</span><span class="sxs-lookup"><span data-stu-id="38ccc-168">OpsGenie determines the right people to notify based on on-call schedules and escalations, by notifying them using email, text messages (SMS), phone calls, push notifications.</span></span> <span data-ttu-id="38ccc-169">簡言之，Azure 會針對偵測到的問題產生警示，OpsGenie 則會確保安排適當人員處理這些問題。</span><span class="sxs-lookup"><span data-stu-id="38ccc-169">Simply, Azure generates alerts for detected problems, and OpsGenie ensures the right people are working on them.</span></span>

<span data-ttu-id="38ccc-170">[請移至文件。][opsgenie-doc]</span><span class="sxs-lookup"><span data-stu-id="38ccc-170">[Go to the documentation.][opsgenie-doc]</span></span>

## <a name="pagerduty"></a><span data-ttu-id="38ccc-171">PagerDuty</span><span class="sxs-lookup"><span data-stu-id="38ccc-171">PagerDuty</span></span>
<span data-ttu-id="38ccc-172">PagerDuty 是業界領先的事件管理解決方案，針對 Azure 度量警示提供第一級支援。</span><span class="sxs-lookup"><span data-stu-id="38ccc-172">PagerDuty, the leading incident management solution, has provided first-class support for Azure Alerts on metrics.</span></span> <span data-ttu-id="38ccc-173">現今，PagerDuty 除了 Azure 服務的平台層級計量通知之外，還支援「Azure 監視器警示」、「自動調整規模通知」及「稽核記錄事件」的通知。</span><span class="sxs-lookup"><span data-stu-id="38ccc-173">Today, PagerDuty now supports notifications on Azure Monitor Alerts, Autoscale Notifications, and Audit Log Events, in addition to notifications on platform-level metrics for Azure services.</span></span> <span data-ttu-id="38ccc-174">這些增強功能讓使用者能進一步地掌握核心 Azure 平台，同時讓他們充分利用 PagerDuty 的即時回應事件管理功能。</span><span class="sxs-lookup"><span data-stu-id="38ccc-174">These enhancements give users increased visibility into the core Azure Platform while enabling them to take full advantage of PagerDuty’s incident management capabilities for real-time response.</span></span> <span data-ttu-id="38ccc-175">我們透過 webhook 實現擴充的 Azure 整合，以供快速且輕鬆的設定與自訂。</span><span class="sxs-lookup"><span data-stu-id="38ccc-175">Our expanded Azure integration is made possible via webhooks, allowing for quick and easy set-up and customization.</span></span>

<span data-ttu-id="38ccc-176">[請移至文件。][pagerduty-doc]</span><span class="sxs-lookup"><span data-stu-id="38ccc-176">[Go to the documentation.][pagerduty-doc]</span></span>

## <a name="sciencelogic"></a><span data-ttu-id="38ccc-177">ScienceLogic</span><span class="sxs-lookup"><span data-stu-id="38ccc-177">ScienceLogic</span></span>
<span data-ttu-id="38ccc-178">ScienceLogic 提供新一代 IT 服務保證平台，可在任何位置管理任何技術。</span><span class="sxs-lookup"><span data-stu-id="38ccc-178">ScienceLogic delivers the next generation IT service assurance platform for managing any technology, anywhere.</span></span>  <span data-ttu-id="38ccc-179">ScienceLogic 可在一個平台為簡化持續管理 IT 資源、服務和應用程式不斷擴展的工作提供級別、安全性、自動化和恢復功能。</span><span class="sxs-lookup"><span data-stu-id="38ccc-179">In one platform, ScienceLogic delivers the scale, security, automation, and resiliency necessary to simplify the ever-expanding task of managing IT resources, services, and applications that are in constant motion.</span></span>  <span data-ttu-id="38ccc-180">ScienceLogic 平台會使用 Azure API 做為 Microsoft Azure 的介面。</span><span class="sxs-lookup"><span data-stu-id="38ccc-180">The ScienceLogic platform uses Azure APIs to interface with Microsoft Azure.</span></span>  <span data-ttu-id="38ccc-181">ScienceLogic 可讓您即時掌握您的 Azure 服務和資源，以便您知道項目沒有運作，且可以更快速修正它。</span><span class="sxs-lookup"><span data-stu-id="38ccc-181">ScienceLogic gives you real-time visibility into your Azure services and resources so you know when something’s not working and can fix it faster.</span></span> <span data-ttu-id="38ccc-182">您也可以與其他雲端和資料中心系統和服務管理 Azure。</span><span class="sxs-lookup"><span data-stu-id="38ccc-182">You can also manage Azure alongside your other clouds and data center systems and services.</span></span>

<span data-ttu-id="38ccc-183">[深入了解。][sciencelogic-doc]</span><span class="sxs-lookup"><span data-stu-id="38ccc-183">[Learn more.][sciencelogic-doc]</span></span>

## <a name="azure-monitor-add-on-for-splunk"></a><span data-ttu-id="38ccc-184">Splunk 適用的 Azure 監視器附加元件</span><span class="sxs-lookup"><span data-stu-id="38ccc-184">Azure Monitor Add-on for Splunk</span></span>
<span data-ttu-id="38ccc-185">Splunk 適用的 Azure 監視器附加元件的下載位置：[Splunkbase](https://splunkbase.splunk.com/app/3534/)。</span><span class="sxs-lookup"><span data-stu-id="38ccc-185">The Azure Monitor Add-on for Splunk is [available in the Splunkbase here](https://splunkbase.splunk.com/app/3534/).</span></span>

<span data-ttu-id="38ccc-186">[請移至文件。][splunk-doc]</span><span class="sxs-lookup"><span data-stu-id="38ccc-186">[Go to the documentation.][splunk-doc]</span></span>

## <a name="sumo-logic"></a><span data-ttu-id="38ccc-187">Sumo Logic</span><span class="sxs-lookup"><span data-stu-id="38ccc-187">Sumo Logic</span></span>
<span data-ttu-id="38ccc-188">Sumo Logic 是安全、雲端原生的電腦資料分析服務，能橫跨整個應用程式生命週期與堆疊，提供結構化、半結構化和非結構化資料即時、不間斷的智慧服務。</span><span class="sxs-lookup"><span data-stu-id="38ccc-188">Sumo Logic is a secure, cloud-native, machine data analytics service, delivering real-time, continuous intelligence from structured, semi-structured, and unstructured data across the entire application lifecycle and stack.</span></span> <span data-ttu-id="38ccc-189">全球超過 1,000 個客戶都仰賴 Sumo Logic 進行分析及洞察，以建置、執行並保護他們的新式應用程式與雲端架構。</span><span class="sxs-lookup"><span data-stu-id="38ccc-189">More than 1,000 customers around the globe rely on Sumo Logic for the analytics and insights to build, run, and secure their modern applications and cloud infrastructures.</span></span> <span data-ttu-id="38ccc-190">透過 Sumo Logic，客戶可取得多租用戶、服務模型的優點，來加速他們持續創新的腳步，提升競爭優勢、商業價值及發展。</span><span class="sxs-lookup"><span data-stu-id="38ccc-190">With Sumo Logic, customers gain a multi-tenant, service-model advantage to accelerate their shift to continuous innovation, increasing competitive advantage, business value, and growth.</span></span>

<span data-ttu-id="38ccc-191">[深入了解。][sumologic-doc]</span><span class="sxs-lookup"><span data-stu-id="38ccc-191">[Learn more.][sumologic-doc]</span></span>

## <a name="next-steps"></a><span data-ttu-id="38ccc-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="38ccc-192">Next Steps</span></span>
* [<span data-ttu-id="38ccc-193">深入了解 Azure 監視器</span><span class="sxs-lookup"><span data-stu-id="38ccc-193">Learn more about Azure Monitor</span></span>](monitoring-overview.md)
* [<span data-ttu-id="38ccc-194">使用 REST API 存取計量</span><span class="sxs-lookup"><span data-stu-id="38ccc-194">Access metrics using the REST API</span></span>](monitoring-rest-api-walkthrough.md)
* [<span data-ttu-id="38ccc-195">將活動記錄串流至第三方服務</span><span class="sxs-lookup"><span data-stu-id="38ccc-195">Stream the Activity Log to a third party service</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="38ccc-196">將診斷記錄串流至第三方服務</span><span class="sxs-lookup"><span data-stu-id="38ccc-196">Stream Diagnostic Logs to a third party service</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

<!--Partner Anchors-->
<span data-ttu-id="38ccc-197">[alertlogic-anchor]: #alertlogic-log-manager "AlertLogic"</span><span class="sxs-lookup"><span data-stu-id="38ccc-197">[alertlogic-anchor]: #alertlogic-log-manager "AlertLogic"</span></span>
<span data-ttu-id="38ccc-198">[appdynamics-anchor]: #appdynamics "AppDynamics"</span><span class="sxs-lookup"><span data-stu-id="38ccc-198">[appdynamics-anchor]: #appdynamics "AppDynamics"</span></span>
<span data-ttu-id="38ccc-199">[atlassian-anchor]: #atlassian-jira "Atlassian"</span><span class="sxs-lookup"><span data-stu-id="38ccc-199">[atlassian-anchor]: #atlassian-jira "Atlassian"</span></span>
<span data-ttu-id="38ccc-200">[circonus-anchor]: #circonus "Circonus"</span><span class="sxs-lookup"><span data-stu-id="38ccc-200">[circonus-anchor]: #circonus "Circonus"</span></span>
<span data-ttu-id="38ccc-201">[cloudhealth-anchor]: #cloudhealth "CloudHealth"</span><span class="sxs-lookup"><span data-stu-id="38ccc-201">[cloudhealth-anchor]: #cloudhealth "CloudHealth"</span></span>
<span data-ttu-id="38ccc-202">[cloudmonix-anchor]: #cloudmonix "CloudMonix"</span><span class="sxs-lookup"><span data-stu-id="38ccc-202">[cloudmonix-anchor]: #cloudmonix "CloudMonix"</span></span>
<span data-ttu-id="38ccc-203">[cloudyn-anchor]: #cloudyn "Cloudyn"</span><span class="sxs-lookup"><span data-stu-id="38ccc-203">[cloudyn-anchor]: #cloudyn "Cloudyn"</span></span>
<span data-ttu-id="38ccc-204">[datadog-anchor]: #datadog "Datadog"</span><span class="sxs-lookup"><span data-stu-id="38ccc-204">[datadog-anchor]: #datadog "Datadog"</span></span>
<span data-ttu-id="38ccc-205">[dynatrace-anchor]: #dynatrace "Dynatrace"</span><span class="sxs-lookup"><span data-stu-id="38ccc-205">[dynatrace-anchor]: #dynatrace "Dynatrace"</span></span>
<span data-ttu-id="38ccc-206">[newrelic-anchor]: #newrelic "NewRelic"</span><span class="sxs-lookup"><span data-stu-id="38ccc-206">[newrelic-anchor]: #newrelic "NewRelic"</span></span>
<span data-ttu-id="38ccc-207">[opsgenie-anchor]: #opsgenie "OpsGenie"</span><span class="sxs-lookup"><span data-stu-id="38ccc-207">[opsgenie-anchor]: #opsgenie "OpsGenie"</span></span>
<span data-ttu-id="38ccc-208">[pagerduty-anchor]: #pagerduty "PagerDuty"</span><span class="sxs-lookup"><span data-stu-id="38ccc-208">[pagerduty-anchor]: #pagerduty "PagerDuty"</span></span>
<span data-ttu-id="38ccc-209">[sciencelogic-anchor]: #sciencelogic "ScienceLogic"</span><span class="sxs-lookup"><span data-stu-id="38ccc-209">[sciencelogic-anchor]: #sciencelogic "ScienceLogic"</span></span>
<span data-ttu-id="38ccc-210">[splunk-anchor]: #azure-monitor-add-on-for-splunk "Splunk"</span><span class="sxs-lookup"><span data-stu-id="38ccc-210">[splunk-anchor]: #azure-monitor-add-on-for-splunk "Splunk"</span></span>
<span data-ttu-id="38ccc-211">[sumologic-anchor]: #sumo-logic "Sumo Logic"</span><span class="sxs-lookup"><span data-stu-id="38ccc-211">[sumologic-anchor]: #sumo-logic "Sumo Logic"</span></span>

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
<span data-ttu-id="38ccc-212">[alertlogic-doc]: https://docs.alertlogic.com/userGuides/log-manager-collection-sources.htm "AlertLogic 文件。"</span><span class="sxs-lookup"><span data-stu-id="38ccc-212">[alertlogic-doc]: https://docs.alertlogic.com/userGuides/log-manager-collection-sources.htm "AlertLogic documentation."</span></span>
<span data-ttu-id="38ccc-213">[appdynamics-doc]: https://www.appdynamics.com/net/azure/ "AppDynamics 文件。"</span><span class="sxs-lookup"><span data-stu-id="38ccc-213">[appdynamics-doc]: https://www.appdynamics.com/net/azure/ "AppDynamics documentation."</span></span>
[atlassian-doc]: https://azure.microsoft.com/blog/automated-notifications-from-azure-monitor-for-atlassian-jira/
[circonus-doc]: https://support.circonus.com/support/solutions/articles/24000013515-azure-integration 
[cloudhealth-doc]: https://www.cloudhealthtech.com/azure
<span data-ttu-id="38ccc-214">[cloudmonix-doc]: http://cloudmonix.com/features/azure-management/ "CloudMonix 簡介。"</span><span class="sxs-lookup"><span data-stu-id="38ccc-214">[cloudmonix-doc]: http://cloudmonix.com/features/azure-management/ "CloudMonix introduction."</span></span>
<span data-ttu-id="38ccc-215">[cloudyn-doc]: https://www.cloudyn.com/azure-monitoring "Cloudyn 簡介。"</span><span class="sxs-lookup"><span data-stu-id="38ccc-215">[cloudyn-doc]: https://www.cloudyn.com/azure-monitoring "Cloudyn introduction."</span></span>
<span data-ttu-id="38ccc-216">[datadog-doc]: http://docs.datadoghq.com/integrations/azure/ "Datadog 文件。"</span><span class="sxs-lookup"><span data-stu-id="38ccc-216">[datadog-doc]: http://docs.datadoghq.com/integrations/azure/ "Datadog documentation."</span></span>
<span data-ttu-id="38ccc-217">[dynatrace-doc]: https://help.dynatrace.com/infrastructure-monitoring/paas/how-do-i-monitor-microsoft-azure-web-apps/ "Dynatrace 文件。"</span><span class="sxs-lookup"><span data-stu-id="38ccc-217">[dynatrace-doc]: https://help.dynatrace.com/infrastructure-monitoring/paas/how-do-i-monitor-microsoft-azure-web-apps/ "Dynatrace documentation."</span></span>
<span data-ttu-id="38ccc-218">[newrelic-doc]: https://newrelic.com/azure "NewRelic 文件。"</span><span class="sxs-lookup"><span data-stu-id="38ccc-218">[newrelic-doc]: https://newrelic.com/azure "NewRelic documentation."</span></span>
<span data-ttu-id="38ccc-219">[opsgenie-doc]: https://www.opsgenie.com/docs/integrations/azure-integration "OpsGenie 文件。"</span><span class="sxs-lookup"><span data-stu-id="38ccc-219">[opsgenie-doc]: https://www.opsgenie.com/docs/integrations/azure-integration "OpsGenie documentation."</span></span>
<span data-ttu-id="38ccc-220">[pagerduty-doc]: https://www.pagerduty.com/docs/guides/azure-integration-guide/ "PagerDuty 文件。"</span><span class="sxs-lookup"><span data-stu-id="38ccc-220">[pagerduty-doc]: https://www.pagerduty.com/docs/guides/azure-integration-guide/ "PagerDuty documentation."</span></span>
<span data-ttu-id="38ccc-221">[sciencelogic-doc]: https://www.sciencelogic.com/product/technologies/microsoft/azure "ScienceLogic 文件。"</span><span class="sxs-lookup"><span data-stu-id="38ccc-221">[sciencelogic-doc]: https://www.sciencelogic.com/product/technologies/microsoft/azure "ScienceLogic documentation."</span></span>
<span data-ttu-id="38ccc-222">[splunk-doc]: https://github.com/Microsoft/AzureMonitorAddonForSplunk/wiki/Azure-Monitor-Addon-For-Splunk "Splunk 文件。"</span><span class="sxs-lookup"><span data-stu-id="38ccc-222">[splunk-doc]: https://github.com/Microsoft/AzureMonitorAddonForSplunk/wiki/Azure-Monitor-Addon-For-Splunk "Splunk documentation."</span></span>
<span data-ttu-id="38ccc-223">[sumologic-doc]: https://www.sumologic.com/azure "SumoLogic 文件。"</span><span class="sxs-lookup"><span data-stu-id="38ccc-223">[sumologic-doc]: https://www.sumologic.com/azure "SumoLogic documentation."</span></span>

---
title: "Azure Log Analytics 中的容器監視解決方案 | Microsoft Docs"
description: "Log Analytics 中的容器監視方案可協助您在單一位置檢視及管理 Docker 和 Windows 容器主機。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte;banders
ms.openlocfilehash: b2e03531ee401f4552198e5dd50fbfe1d970f0e5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a><span data-ttu-id="21f49-103">Log Analytics 中的容器監視解決方案</span><span class="sxs-lookup"><span data-stu-id="21f49-103">Container Monitoring solution in Log Analytics</span></span>

![容器符號](./media/log-analytics-containers/containers-symbol.png)

<span data-ttu-id="21f49-105">本文說明如何設定及使用 Log Analytics 中的容器監視方案，協助您在單一位置檢視及管理 Docker 和 Windows 容器主機。</span><span class="sxs-lookup"><span data-stu-id="21f49-105">This article describes how to set up and use the Container Monitoring solution in Log Analytics, which helps you view and manage your Docker and Windows container hosts in a single location.</span></span> <span data-ttu-id="21f49-106">Docker 是用來建立容器的軟體虛擬化系統，自動將軟體部署至其 IT 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="21f49-106">Docker is a software virtualization system used to create containers that automate software deployment to their IT infrastructure.</span></span>

<span data-ttu-id="21f49-107">解決方案會顯示哪些容器正在執行、它們正在執行的是哪些容器映像，以及容器執行的位置。</span><span class="sxs-lookup"><span data-stu-id="21f49-107">The solution shows which containers are running, what container image they’re running, and where containers are running.</span></span> <span data-ttu-id="21f49-108">您可以檢視詳細的稽核資訊，其中顯示搭配容器使用的命令。</span><span class="sxs-lookup"><span data-stu-id="21f49-108">You can view detailed audit information showing commands used with containers.</span></span> <span data-ttu-id="21f49-109">而且，藉由檢視及搜尋集中式記錄檔，而不需從遠端檢視 Docker 或 Windows 主機，即可針對容器進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="21f49-109">And, you can troubleshoot containers by viewing and searching centralized logs without having to remotely view Docker or Windows hosts.</span></span> <span data-ttu-id="21f49-110">您可能會找到有雜訊且耗用過多主機資源的容器。</span><span class="sxs-lookup"><span data-stu-id="21f49-110">You can find containers that may be noisy and consuming excess resources on a host.</span></span> <span data-ttu-id="21f49-111">而且，您可以檢視容器的集中式 CPU、記憶體、儲存體以及網路使用量和效能資訊。</span><span class="sxs-lookup"><span data-stu-id="21f49-111">And, you can view centralized CPU, memory, storage, and network usage and performance information for containers.</span></span> <span data-ttu-id="21f49-112">您可以在執行 Windows 的電腦上集中管理，並從 Windows Server、HYPER-V 和 Docker 容器比較記錄檔。</span><span class="sxs-lookup"><span data-stu-id="21f49-112">On computers running Windows, you can centralize and compare logs from Windows Server, Hyper-V, and Docker containers.</span></span> <span data-ttu-id="21f49-113">解決方案支援下列容器協調者：</span><span class="sxs-lookup"><span data-stu-id="21f49-113">The solution supports the following container orchestrators:</span></span>

- <span data-ttu-id="21f49-114">Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="21f49-114">Docker Swarm</span></span>
- <span data-ttu-id="21f49-115">DC/OS</span><span class="sxs-lookup"><span data-stu-id="21f49-115">DC/OS</span></span>
- <span data-ttu-id="21f49-116">Kubernetes</span><span class="sxs-lookup"><span data-stu-id="21f49-116">Kubernetes</span></span>
- <span data-ttu-id="21f49-117">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="21f49-117">Service Fabric</span></span>
- <span data-ttu-id="21f49-118">Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="21f49-118">Red Hat OpenShift</span></span>


<span data-ttu-id="21f49-119">下圖顯示各種容器主機和代理程式與 OMS 之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="21f49-119">The following diagram shows the relationships between various container hosts and agents with OMS.</span></span>

![容器圖表](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a><span data-ttu-id="21f49-121">系統需求</span><span class="sxs-lookup"><span data-stu-id="21f49-121">System requirements</span></span>

<span data-ttu-id="21f49-122">開始之前請檢閱下列詳細資料，以確認符合必要條件。</span><span class="sxs-lookup"><span data-stu-id="21f49-122">Before starting, review the following details to verify you meet the prerequisites.</span></span>

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a><span data-ttu-id="21f49-123">容器監視解決方案支援 Docker Orchestrator 和作業系統平台</span><span class="sxs-lookup"><span data-stu-id="21f49-123">Container monitoring solution support for Docker Orchestrator and OS platform</span></span>
<span data-ttu-id="21f49-124">下表概述對於使用 Log Analytics 之容器清查、效能和記錄的 Docker 協調流程和作業系統監視支援。</span><span class="sxs-lookup"><span data-stu-id="21f49-124">The following table outlines the Docker orchestration and operating system monitoring support of container inventory, performance, and logs with Log Analytics.</span></span>   

| | <span data-ttu-id="21f49-125">ACS</span><span class="sxs-lookup"><span data-stu-id="21f49-125">ACS</span></span> | <span data-ttu-id="21f49-126">Linux</span><span class="sxs-lookup"><span data-stu-id="21f49-126">Linux</span></span> | <span data-ttu-id="21f49-127">Windows</span><span class="sxs-lookup"><span data-stu-id="21f49-127">Windows</span></span> | <span data-ttu-id="21f49-128">容器</span><span class="sxs-lookup"><span data-stu-id="21f49-128">Container</span></span><br><span data-ttu-id="21f49-129">清查</span><span class="sxs-lookup"><span data-stu-id="21f49-129">Inventory</span></span> | <span data-ttu-id="21f49-130">映像</span><span class="sxs-lookup"><span data-stu-id="21f49-130">Image</span></span><br><span data-ttu-id="21f49-131">清查</span><span class="sxs-lookup"><span data-stu-id="21f49-131">Inventory</span></span> | <span data-ttu-id="21f49-132">節點</span><span class="sxs-lookup"><span data-stu-id="21f49-132">Node</span></span><br><span data-ttu-id="21f49-133">清查</span><span class="sxs-lookup"><span data-stu-id="21f49-133">Inventory</span></span> | <span data-ttu-id="21f49-134">容器</span><span class="sxs-lookup"><span data-stu-id="21f49-134">Container</span></span><br><span data-ttu-id="21f49-135">效能</span><span class="sxs-lookup"><span data-stu-id="21f49-135">Performance</span></span> | <span data-ttu-id="21f49-136">容器</span><span class="sxs-lookup"><span data-stu-id="21f49-136">Container</span></span><br><span data-ttu-id="21f49-137">Event</span><span class="sxs-lookup"><span data-stu-id="21f49-137">Event</span></span> | <span data-ttu-id="21f49-138">Event</span><span class="sxs-lookup"><span data-stu-id="21f49-138">Event</span></span><br><span data-ttu-id="21f49-139">記錄檔</span><span class="sxs-lookup"><span data-stu-id="21f49-139">Log</span></span> | <span data-ttu-id="21f49-140">容器</span><span class="sxs-lookup"><span data-stu-id="21f49-140">Container</span></span><br><span data-ttu-id="21f49-141">記錄檔</span><span class="sxs-lookup"><span data-stu-id="21f49-141">Log</span></span> |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| <span data-ttu-id="21f49-142">Kubernetes</span><span class="sxs-lookup"><span data-stu-id="21f49-142">Kubernetes</span></span> | <span data-ttu-id="21f49-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-143">&#8226;</span></span> | <span data-ttu-id="21f49-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-144">&#8226;</span></span> | | <span data-ttu-id="21f49-145">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-145">&#8226;</span></span> | <span data-ttu-id="21f49-146">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-146">&#8226;</span></span> | <span data-ttu-id="21f49-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-147">&#8226;</span></span> | <span data-ttu-id="21f49-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-148">&#8226;</span></span> | <span data-ttu-id="21f49-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-149">&#8226;</span></span> | <span data-ttu-id="21f49-150">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-150">&#8226;</span></span> | <span data-ttu-id="21f49-151">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-151">&#8226;</span></span> |
| <span data-ttu-id="21f49-152">Mesosphere</span><span class="sxs-lookup"><span data-stu-id="21f49-152">Mesosphere</span></span><br><span data-ttu-id="21f49-153">DC/OS</span><span class="sxs-lookup"><span data-stu-id="21f49-153">DC/OS</span></span> | <span data-ttu-id="21f49-154">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-154">&#8226;</span></span> | <span data-ttu-id="21f49-155">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-155">&#8226;</span></span> | | <span data-ttu-id="21f49-156">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-156">&#8226;</span></span> | <span data-ttu-id="21f49-157">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-157">&#8226;</span></span> | <span data-ttu-id="21f49-158">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-158">&#8226;</span></span> | <span data-ttu-id="21f49-159">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-159">&#8226;</span></span>| <span data-ttu-id="21f49-160">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-160">&#8226;</span></span> | <span data-ttu-id="21f49-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-161">&#8226;</span></span> | <span data-ttu-id="21f49-162">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-162">&#8226;</span></span> |
| <span data-ttu-id="21f49-163">Docker</span><span class="sxs-lookup"><span data-stu-id="21f49-163">Docker</span></span><br><span data-ttu-id="21f49-164">Swarm</span><span class="sxs-lookup"><span data-stu-id="21f49-164">Swarm</span></span> | <span data-ttu-id="21f49-165">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-165">&#8226;</span></span> | <span data-ttu-id="21f49-166">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-166">&#8226;</span></span> | <span data-ttu-id="21f49-167">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-167">&#8226;</span></span> | <span data-ttu-id="21f49-168">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-168">&#8226;</span></span> | <span data-ttu-id="21f49-169">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-169">&#8226;</span></span> | <span data-ttu-id="21f49-170">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-170">&#8226;</span></span> | <span data-ttu-id="21f49-171">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-171">&#8226;</span></span> | <span data-ttu-id="21f49-172">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-172">&#8226;</span></span> | | <span data-ttu-id="21f49-173">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-173">&#8226;</span></span> |
| <span data-ttu-id="21f49-174">服務</span><span class="sxs-lookup"><span data-stu-id="21f49-174">Service</span></span><br><span data-ttu-id="21f49-175">網狀架構</span><span class="sxs-lookup"><span data-stu-id="21f49-175">Fabric</span></span> | | | <span data-ttu-id="21f49-176">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-176">&#8226;</span></span> | <span data-ttu-id="21f49-177">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-177">&#8226;</span></span> | <span data-ttu-id="21f49-178">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-178">&#8226;</span></span> | <span data-ttu-id="21f49-179">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-179">&#8226;</span></span> | <span data-ttu-id="21f49-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-180">&#8226;</span></span> | <span data-ttu-id="21f49-181">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-181">&#8226;</span></span> | <span data-ttu-id="21f49-182">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-182">&#8226;</span></span> | <span data-ttu-id="21f49-183">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-183">&#8226;</span></span> |
| <span data-ttu-id="21f49-184">Red Hat 開啟</span><span class="sxs-lookup"><span data-stu-id="21f49-184">Red Hat Open</span></span><br><span data-ttu-id="21f49-185">移位</span><span class="sxs-lookup"><span data-stu-id="21f49-185">Shift</span></span> | | <span data-ttu-id="21f49-186">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-186">&#8226;</span></span> | | <span data-ttu-id="21f49-187">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-187">&#8226;</span></span> | <span data-ttu-id="21f49-188">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-188">&#8226;</span></span>| <span data-ttu-id="21f49-189">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-189">&#8226;</span></span> | <span data-ttu-id="21f49-190">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-190">&#8226;</span></span> | <span data-ttu-id="21f49-191">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-191">&#8226;</span></span> | | <span data-ttu-id="21f49-192">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-192">&#8226;</span></span> |
| <span data-ttu-id="21f49-193">Windows Server</span><span class="sxs-lookup"><span data-stu-id="21f49-193">Windows Server</span></span><br><span data-ttu-id="21f49-194">(獨立)</span><span class="sxs-lookup"><span data-stu-id="21f49-194">(standalone)</span></span> | | | <span data-ttu-id="21f49-195">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-195">&#8226;</span></span> | <span data-ttu-id="21f49-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-196">&#8226;</span></span> | <span data-ttu-id="21f49-197">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-197">&#8226;</span></span> | <span data-ttu-id="21f49-198">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-198">&#8226;</span></span> | <span data-ttu-id="21f49-199">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-199">&#8226;</span></span> | <span data-ttu-id="21f49-200">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-200">&#8226;</span></span> | | <span data-ttu-id="21f49-201">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-201">&#8226;</span></span> |
| <span data-ttu-id="21f49-202">Linux 伺服器</span><span class="sxs-lookup"><span data-stu-id="21f49-202">Linux Server</span></span><br><span data-ttu-id="21f49-203">(獨立)</span><span class="sxs-lookup"><span data-stu-id="21f49-203">(standalone)</span></span> | | <span data-ttu-id="21f49-204">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-204">&#8226;</span></span> | | <span data-ttu-id="21f49-205">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-205">&#8226;</span></span> | <span data-ttu-id="21f49-206">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-206">&#8226;</span></span> | <span data-ttu-id="21f49-207">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-207">&#8226;</span></span> | <span data-ttu-id="21f49-208">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-208">&#8226;</span></span> | <span data-ttu-id="21f49-209">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-209">&#8226;</span></span> | | <span data-ttu-id="21f49-210">&#8226;</span><span class="sxs-lookup"><span data-stu-id="21f49-210">&#8226;</span></span> |


### <a name="docker-versions-supported-on-linux"></a><span data-ttu-id="21f49-211">在 Linux 上支援的 Docker 版本</span><span class="sxs-lookup"><span data-stu-id="21f49-211">Docker versions supported on Linux</span></span>

- <span data-ttu-id="21f49-212">Docker 1.11 至 1.13</span><span class="sxs-lookup"><span data-stu-id="21f49-212">Docker 1.11 to 1.13</span></span>
- <span data-ttu-id="21f49-213">Docker CE 和 EE v17.06</span><span class="sxs-lookup"><span data-stu-id="21f49-213">Docker CE and EE v17.06</span></span>

### <a name="x64-linux-distributions-supported-as-container-hosts"></a><span data-ttu-id="21f49-214">x64 Linux 散發套件可支援作為容器主機</span><span class="sxs-lookup"><span data-stu-id="21f49-214">x64 Linux distributions supported as container hosts</span></span>

- <span data-ttu-id="21f49-215">Ubuntu 14.04 LTS 和 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="21f49-215">Ubuntu 14.04 LTS and 16.04 LTS</span></span>
- <span data-ttu-id="21f49-216">CoreOS (穩定版)</span><span class="sxs-lookup"><span data-stu-id="21f49-216">CoreOS(stable)</span></span>
- <span data-ttu-id="21f49-217">Amazon Linux 2016.09.0</span><span class="sxs-lookup"><span data-stu-id="21f49-217">Amazon Linux 2016.09.0</span></span>
- <span data-ttu-id="21f49-218">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="21f49-218">openSUSE 13.2</span></span>
- <span data-ttu-id="21f49-219">openSUSE LEAP 42.2</span><span class="sxs-lookup"><span data-stu-id="21f49-219">openSUSE LEAP 42.2</span></span>
- <span data-ttu-id="21f49-220">CentOS 7.2 和 7.3</span><span class="sxs-lookup"><span data-stu-id="21f49-220">CentOS 7.2 and 7.3</span></span>
- <span data-ttu-id="21f49-221">SLES 12</span><span class="sxs-lookup"><span data-stu-id="21f49-221">SLES 12</span></span>
- <span data-ttu-id="21f49-222">RHEL 7.2 和 7.3</span><span class="sxs-lookup"><span data-stu-id="21f49-222">RHEL 7.2 and 7.3</span></span>
- <span data-ttu-id="21f49-223">Red Hat OpenShift Container Platform (OCP) 3.4 和 3.5</span><span class="sxs-lookup"><span data-stu-id="21f49-223">Red Hat OpenShift Container Platform (OCP) 3.4 and 3.5</span></span>
- <span data-ttu-id="21f49-224">ACS Mesosphere DC/OS 1.7.3 至 1.8.8</span><span class="sxs-lookup"><span data-stu-id="21f49-224">ACS Mesosphere DC/OS 1.7.3 to 1.8.8</span></span>
- <span data-ttu-id="21f49-225">ACS Kubernetes 1.4.5 至 1.6</span><span class="sxs-lookup"><span data-stu-id="21f49-225">ACS Kubernetes 1.4.5 to 1.6</span></span>
- <span data-ttu-id="21f49-226">ACS Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="21f49-226">ACS Docker Swarm</span></span>

### <a name="supported-windows-operating-system"></a><span data-ttu-id="21f49-227">支援的 Windows 作業系統</span><span class="sxs-lookup"><span data-stu-id="21f49-227">Supported Windows operating system</span></span>

- <span data-ttu-id="21f49-228">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="21f49-228">Windows Server 2016</span></span>
- <span data-ttu-id="21f49-229">Windows 10 年度版 (Professional 或 Enterprise)</span><span class="sxs-lookup"><span data-stu-id="21f49-229">Windows 10 Anniversary Edition (Professional or Enterprise)</span></span>

### <a name="docker-versions-supported-on-windows"></a><span data-ttu-id="21f49-230">在 Windows 上支援 Docker 版本</span><span class="sxs-lookup"><span data-stu-id="21f49-230">Docker versions supported on Windows</span></span>

- <span data-ttu-id="21f49-231">Docker 1.12 和 1.13</span><span class="sxs-lookup"><span data-stu-id="21f49-231">Docker 1.12 and 1.13</span></span>
- <span data-ttu-id="21f49-232">Docker 17.03.0 和更新版本</span><span class="sxs-lookup"><span data-stu-id="21f49-232">Docker 17.03.0 and later</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="21f49-233">安裝和設定方案</span><span class="sxs-lookup"><span data-stu-id="21f49-233">Installing and configuring the solution</span></span>
<span data-ttu-id="21f49-234">請使用下列資訊來安裝和設定方案。</span><span class="sxs-lookup"><span data-stu-id="21f49-234">Use the following information to install and configure the solution.</span></span>

1. <span data-ttu-id="21f49-235">從 [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) 或使用[從方案庫新增 Log Analytics 方案](log-analytics-add-solutions.md)中所述的程序，將容器監視解決方案新增至您的 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="21f49-235">Add the Container Monitoring solution to your OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

2. <span data-ttu-id="21f49-236">安裝和使用 Docker 搭配 OMS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="21f49-236">Install and use Docker with an OMS agent.</span></span>  <span data-ttu-id="21f49-237">以您的作業系統作為基礎，您可以從下列方法選擇：</span><span class="sxs-lookup"><span data-stu-id="21f49-237">Based on your operating system, you can choose from the following methods:</span></span>

  * <span data-ttu-id="21f49-238">在支援的 Linux 作業系統上，安裝和執行 Docker，然後安裝並設定 [OMS Agent for Linux](log-analytics-agent-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="21f49-238">On supported Linux operating systems, install and run Docker and then install and configure the [OMS Agent for Linux](log-analytics-agent-linux.md).</span></span>  
  * <span data-ttu-id="21f49-239">在 CoreOS 上，您無法執行 OMS Agent for Linux。</span><span class="sxs-lookup"><span data-stu-id="21f49-239">On CoreOS, you cannot run the OMS Agent for Linux.</span></span> <span data-ttu-id="21f49-240">相反地，您可以執行 OMS Agent for Linux 的容器化版本。</span><span class="sxs-lookup"><span data-stu-id="21f49-240">Instead, you run a containerized version of the OMS Agent for Linux.</span></span> <span data-ttu-id="21f49-241">檢閱 [Linux 容器主機，包括 CoreOS](#for-all-linux-container-hosts-including-coreos) 或 [Azure Government Linux 容器主機，包括 CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos)，如果您正在使用 Azure Government Cloud 中的容器。</span><span class="sxs-lookup"><span data-stu-id="21f49-241">Review [Linux container hosts including CoreOS](#for-all-linux-container-hosts-including-coreos) or [Azure Government Linux container hosts including CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) if you are working with containers in Azure Government Cloud.</span></span>
  * <span data-ttu-id="21f49-242">在 Windows Server 2016 和 Windows 10 上，安裝 Docker 引擎及用戶端，然後連接代理程式以收集資訊，並將它傳送至 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="21f49-242">On Windows Server 2016 and Windows 10, install the Docker Engine and client then connect an agent to gather information and send it to Log Analytics.</span></span>  

### <a name="container-services"></a><span data-ttu-id="21f49-243">容器服務</span><span class="sxs-lookup"><span data-stu-id="21f49-243">Container services</span></span>

- <span data-ttu-id="21f49-244">如果您有 Red Hat OpenShift 環境，請檢閱[針對 Red Hat OpenShift 設定 OMS 代理程式](#configure-an-oms-agent-for-red-hat-openshift)。</span><span class="sxs-lookup"><span data-stu-id="21f49-244">If you have a Red Hat OpenShift environment, review [Configure an OMS agent for Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span></span>
- <span data-ttu-id="21f49-245">如果您有使用 Azure Container Service 的 Kubernetes 叢集，請檢閱[使用 Microsoft Operations Management Suite (OMS) 監視 Azure Container Service 叢集](../container-service/kubernetes/container-service-kubernetes-oms.md)。</span><span class="sxs-lookup"><span data-stu-id="21f49-245">If you have a Kubernetes cluster using the Azure Container Service, review [Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span></span>
- <span data-ttu-id="21f49-246">如果您擁有 Azure Container Service DC/OS 叢集，請深入了解[使用 Operations Management Suite 監視 Azure Container Service DC/OS 叢集](../container-service/dcos-swarm/container-service-monitoring-oms.md)。</span><span class="sxs-lookup"><span data-stu-id="21f49-246">If you have an Azure Container Service DC/OS cluster, learn more at [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span></span>
- <span data-ttu-id="21f49-247">如果您有 Docker Swarm 模式環境，詳細資訊請參閱[為 Docker Swarm 設定 OMS 代理程式](#configure-an-oms-agent-for-docker-swarm)。</span><span class="sxs-lookup"><span data-stu-id="21f49-247">If you have a Docker Swarm mode environment, learn more at [Configure an OMS agent for Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span></span>
- <span data-ttu-id="21f49-248">如果您搭配 Service Fabric 使用容器，請參閱 [Azure Service Fabric 概觀](../service-fabric/service-fabric-overview.md)以深入了解。</span><span class="sxs-lookup"><span data-stu-id="21f49-248">If you use containers with Service Fabric, learn more at [Overview of Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span></span>
- <span data-ttu-id="21f49-249">檢閱 [Windows 上的 Docker 引擎](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon)文章，以取得有關如何在執行 Windows 的電腦上安裝和設定您 Docker 引擎的資訊。</span><span class="sxs-lookup"><span data-stu-id="21f49-249">Review the [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article for additional information about how to install and configure your Docker Engines on computers running Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21f49-250">在容器主機上安裝 [OMS Agent for Linux](log-analytics-agent-linux.md)**之前**，Docker 必須已在執行中。</span><span class="sxs-lookup"><span data-stu-id="21f49-250">Docker must be running **before** you install the [OMS Agent for Linux](log-analytics-agent-linux.md) on your container hosts.</span></span> <span data-ttu-id="21f49-251">如果您已在安裝 Docker 前安裝此代理程式，您必須重新安裝 OMS Agent for Linux。</span><span class="sxs-lookup"><span data-stu-id="21f49-251">If you've already installed the agent before installing Docker, you need to reinstall the OMS Agent for Linux.</span></span> <span data-ttu-id="21f49-252">如需 Docker 的詳細資訊，請參閱 [Docker 網站](https://www.docker.com)。</span><span class="sxs-lookup"><span data-stu-id="21f49-252">For more information about Docker, see the [Docker website](https://www.docker.com).</span></span>


## <a name="linux-container-hosts"></a><span data-ttu-id="21f49-253">Linux 容器主機</span><span class="sxs-lookup"><span data-stu-id="21f49-253">Linux container hosts</span></span>

<span data-ttu-id="21f49-254">在您安裝 Docker 之後，使用容器主機的下列設定來設定可搭配 Docker 使用的代理程式。</span><span class="sxs-lookup"><span data-stu-id="21f49-254">After you've installed Docker, use the following settings for your container host to configure the agent for use with Docker.</span></span> <span data-ttu-id="21f49-255">首先您需要 OMS 工作區識別碼和金鑰，這可以在 Azure 入口網站中找到。</span><span class="sxs-lookup"><span data-stu-id="21f49-255">First you need your OMS workspace ID and key, which you can find in the Azure portal.</span></span> <span data-ttu-id="21f49-256">在您的工作區中，按一下 [快速啟動] > [電腦] 來檢視您的 [工作區識別碼] 和 [主索引鍵]。</span><span class="sxs-lookup"><span data-stu-id="21f49-256">In your workspace, click **Quick Start** > **Computers** to view your **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="21f49-257">將兩者複製並貼到您最愛的編輯器。</span><span class="sxs-lookup"><span data-stu-id="21f49-257">Copy and paste both into your favorite editor.</span></span>

### <a name="for-all-linux-container-hosts-except-coreos"></a><span data-ttu-id="21f49-258">適用於 CoreOS 以外的所有 Linux 容器主機</span><span class="sxs-lookup"><span data-stu-id="21f49-258">For all Linux container hosts except CoreOS</span></span>

- <span data-ttu-id="21f49-259">如需如何安裝 OMS Agent for Linux 的詳細資訊和步驟，請參閱[將 Linux 電腦連線至 Operations Management Suite (OMS)](log-analytics-agent-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="21f49-259">For more information and steps on how to install the OMS Agent for Linux, see [Connect your Linux Computers to Operations Management Suite (OMS)](log-analytics-agent-linux.md).</span></span>

### <a name="for-all-linux-container-hosts-including-coreos"></a><span data-ttu-id="21f49-260">適用於包含 CoreOS 的所有 Linux 容器主機</span><span class="sxs-lookup"><span data-stu-id="21f49-260">For all Linux container hosts including CoreOS</span></span>

<span data-ttu-id="21f49-261">啟動您要監視的 OMS 容器。</span><span class="sxs-lookup"><span data-stu-id="21f49-261">Start the OMS container that you want to monitor.</span></span> <span data-ttu-id="21f49-262">修改並使用下列範例：</span><span class="sxs-lookup"><span data-stu-id="21f49-262">Modify and use the following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a><span data-ttu-id="21f49-263">適用於包含 CoreOS 的所有 Azure Government Linux 容器主機</span><span class="sxs-lookup"><span data-stu-id="21f49-263">For all Azure Government Linux container hosts including CoreOS</span></span>

<span data-ttu-id="21f49-264">啟動您要監視的 OMS 容器。</span><span class="sxs-lookup"><span data-stu-id="21f49-264">Start the OMS container that you want to monitor.</span></span> <span data-ttu-id="21f49-265">修改並使用下列範例：</span><span class="sxs-lookup"><span data-stu-id="21f49-265">Modify and use the following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-to-one-in-a-container"></a><span data-ttu-id="21f49-266">從使用已安裝的代理程式切換為使用容器中的 Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="21f49-266">Switching from using an installed Linux agent to one in a container</span></span>
<span data-ttu-id="21f49-267">如果您先前使用了直接安裝的代理程式，而且想要改為使用在容器中執行的代理程式，您必須先移除 OMS Agent for Linux。</span><span class="sxs-lookup"><span data-stu-id="21f49-267">If you previously used the directly-installed agent and want to instead use an agent running in a container, you must first remove the OMS Agent for Linux.</span></span> <span data-ttu-id="21f49-268">請參閱[解除安裝 OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) 來了解如何順利解除安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="21f49-268">See [Uninstalling the OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) to understand how to successfully uninstall the agent.</span></span>  

### <a name="configure-an-oms-agent-for-docker-swarm"></a><span data-ttu-id="21f49-269">為 Docker Swarm 設定 OMS 代理程式</span><span class="sxs-lookup"><span data-stu-id="21f49-269">Configure an OMS agent for Docker Swarm</span></span>

<span data-ttu-id="21f49-270">您可以在 Docker Swarm 上以全域服務的方式執行 OMS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="21f49-270">You can run the OMS Agent as a global service on Docker Swarm.</span></span> <span data-ttu-id="21f49-271">使用下列資訊建立 OMS 代理程式服務。</span><span class="sxs-lookup"><span data-stu-id="21f49-271">Use the following information to create an OMS Agent service.</span></span> <span data-ttu-id="21f49-272">您需要插入 OMS 工作區識別碼與主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="21f49-272">You need to insert your OMS Workspace ID and Primary Key.</span></span>

- <span data-ttu-id="21f49-273">在主要節點上執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="21f49-273">Run the following on the master node.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a><span data-ttu-id="21f49-274">為 Red Hat Openshift 設定 OMS 代理程式</span><span class="sxs-lookup"><span data-stu-id="21f49-274">Configure an OMS Agent for Red Hat OpenShift</span></span>
<span data-ttu-id="21f49-275">有三種方式可將 OMS 代理程式新增至 Red Hat OpenShift 以開始收集容器監視資料。</span><span class="sxs-lookup"><span data-stu-id="21f49-275">There are three ways to add the OMS Agent to Red Hat OpenShift to start collecting container monitoring data.</span></span>

* <span data-ttu-id="21f49-276">直接在每個 OpenShift 節點上[安裝 OMS Agent for Linux](log-analytics-agent-linux.md)</span><span class="sxs-lookup"><span data-stu-id="21f49-276">[Install the OMS Agent for Linux](log-analytics-agent-linux.md) directly on each OpenShift node</span></span>  
* <span data-ttu-id="21f49-277">在位於 Azure 中的每個 OpenShift 節點上[啟用記錄分析 VM 延伸模組](log-analytics-azure-vm-extension.md)</span><span class="sxs-lookup"><span data-stu-id="21f49-277">[Enable Log Analytics VM Extension](log-analytics-azure-vm-extension.md) on each OpenShift node residing in Azure</span></span>  
* <span data-ttu-id="21f49-278">安裝 OMS 代理程式作為 OpenShift 精靈集</span><span class="sxs-lookup"><span data-stu-id="21f49-278">Install the OMS Agent as a OpenShift daemon-set</span></span>  

<span data-ttu-id="21f49-279">在本節中，我們會討論安裝 OMS 代理程式作為 OpenShift 精靈集所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="21f49-279">In this section we cover the steps required to install the OMS Agent as an OpenShift daemon-set.</span></span>  

1. <span data-ttu-id="21f49-280">登入 OpenShift 主要節點，並從 GitHub 複製 YAML 檔 [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) 到您的主要節點，然後以 OMS 工作區識別碼和主索引鍵修改值。</span><span class="sxs-lookup"><span data-stu-id="21f49-280">Sign on to the OpenShift master node and copy the yaml file [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) from GitHub to your master node and modify the value with your OMS Workspace ID and with your Primary Key.</span></span>
2. <span data-ttu-id="21f49-281">執行下列命令來建立 OMS 的專案，並設定使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="21f49-281">Run the following commands to create a project for OMS and set the user account.</span></span>

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="21f49-282">若要部署精靈集，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="21f49-282">To deploy the daemon-set, run the following:</span></span>

    `oc create -f ocp-omsagent.yaml`

5. <span data-ttu-id="21f49-283">若要驗證它已設定並正常運作，請輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="21f49-283">To verify it is configured and working correctly, type the following:</span></span>

    `oc describe daemonset omsagent`  

    <span data-ttu-id="21f49-284">輸出會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="21f49-284">and the output should resemble:</span></span>

    ```
    [ocpadmin@khm-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

<span data-ttu-id="21f49-285">如果在使用 OMS 代理程式精靈集 YAML 檔案時，您想要使用密碼來保護您的 OMS 工作區識別碼及主索引鍵，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="21f49-285">If you want to use secrets to secure your OMS Workspace ID and Primary Key when using the OMS Agent daemon-set yaml file, perform the following steps.</span></span>

1. <span data-ttu-id="21f49-286">登入 OpenShift 主要節點，並從 GitHub 複製 YAML 檔 [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) 和密碼產生指令碼 [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh)。</span><span class="sxs-lookup"><span data-stu-id="21f49-286">Sign on to the OpenShift master node and copy the yaml file [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) and secret generating script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) from GitHub.</span></span>  <span data-ttu-id="21f49-287">這個指令碼會產生 OMS 工作區識別碼及主索引鍵的密碼 YAML 檔案，來保護您的密碼資訊。</span><span class="sxs-lookup"><span data-stu-id="21f49-287">This script will generate the secrets yaml file for OMS Workspace ID and Primary Key to secure your secrete information.</span></span>  
2. <span data-ttu-id="21f49-288">執行下列命令來建立 OMS 的專案，並設定使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="21f49-288">Run the following commands to create a project for OMS and set the user account.</span></span> <span data-ttu-id="21f49-289">密碼產生指令碼會要求您的 OMS 工作區識別碼 <WSID> 和主索引鍵 <KEY>，並且在完成時，它會建立 ocp-secret.yaml 檔案。</span><span class="sxs-lookup"><span data-stu-id="21f49-289">The secret generating script asks for your OMS Workspace ID <WSID> and Primary Key <KEY> and upon completion, it creates the ocp-secret.yaml file.</span></span>  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="21f49-290">執行下列命令以開啟密碼檔案：</span><span class="sxs-lookup"><span data-stu-id="21f49-290">Deploy the secret file by running the following:</span></span>

    `oc create -f ocp-secret.yaml`

5. <span data-ttu-id="21f49-291">執行下列命令以驗證部署：</span><span class="sxs-lookup"><span data-stu-id="21f49-291">Verify deployment by running the following:</span></span>

    `oc describe secret omsagent-secret`  

    <span data-ttu-id="21f49-292">輸出會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="21f49-292">and the  output should resemble:</span></span>  

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

6. <span data-ttu-id="21f49-293">執行下列命令以部署 OMS 代理程式精靈集 YAML 檔案：</span><span class="sxs-lookup"><span data-stu-id="21f49-293">Deploy the OMS Agent daemon-set yaml file by running the following:</span></span>

    `oc create -f ocp-ds-omsagent.yaml`  

7. <span data-ttu-id="21f49-294">執行下列命令以驗證部署：</span><span class="sxs-lookup"><span data-stu-id="21f49-294">Verify deployment by running the following:</span></span>

    `oc describe ds oms`

    <span data-ttu-id="21f49-295">輸出會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="21f49-295">and the output should resemble:</span></span>

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe secret omsagent-secret  
    Name:           omsagent-secret  
    Namespace:      omslogging  
    Labels:         <none>  
    Annotations:    <none>  

    Type:   Opaque  

     Data  
     ====  
     KEY:    89 bytes  
     WSID:   37 bytes  
    ```

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a><span data-ttu-id="21f49-296">保護 Docker Swarm 和 Kubernetes 的密碼資訊</span><span class="sxs-lookup"><span data-stu-id="21f49-296">Secure your secret information for Docker Swarm and Kubernetes</span></span>

<span data-ttu-id="21f49-297">您可以針對 Docker Swarm 和 Kubernetes 容器服務保護密碼 OMS 工作區識別碼與主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="21f49-297">You can secure your secret OMS Workspace ID and Primary Keys for Docker Swarm and Kubernetes container services.</span></span>

#### <a name="secure-secrets-for-docker-swarm"></a><span data-ttu-id="21f49-298">保護 Docker Swarm 的祕密</span><span class="sxs-lookup"><span data-stu-id="21f49-298">Secure secrets for Docker Swarm</span></span>

<span data-ttu-id="21f49-299">針對 Docker Swarm，建立工作區識別碼與主索引鍵的祕密後，您便可為 OMSagent 建立 Docker 服務。</span><span class="sxs-lookup"><span data-stu-id="21f49-299">For Docker Swarm, once the secret for Workspace ID and Primary Key is created, you can run the create the Docker service for OMSagent.</span></span> <span data-ttu-id="21f49-300">使用下列資訊建立您的祕密資訊。</span><span class="sxs-lookup"><span data-stu-id="21f49-300">Use the following information to create your secret information.</span></span>

1. <span data-ttu-id="21f49-301">在主要節點上執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="21f49-301">Run the following on the master node.</span></span>

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. <span data-ttu-id="21f49-302">確認已正確建立祕密。</span><span class="sxs-lookup"><span data-stu-id="21f49-302">Verify that secrets were created properly.</span></span>

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. <span data-ttu-id="21f49-303">執行下列命令，將祕密掛接至容器化的 OMS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="21f49-303">Run the following command to mount the secrets to the containerized OMS Agent.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a><span data-ttu-id="21f49-304">使用 yaml 檔案保護 Kubernetes 的祕密</span><span class="sxs-lookup"><span data-stu-id="21f49-304">Secure secrets for Kubernetes with yaml files</span></span>

<span data-ttu-id="21f49-305">針對 Kubernetes，您可以使用指令碼為工作區識別碼與主索引鍵產生密碼 YAML 檔案。</span><span class="sxs-lookup"><span data-stu-id="21f49-305">For Kubernetes, you use a script to generate the secrets yaml file for your Workspace ID and Primary Key.</span></span> <span data-ttu-id="21f49-306">[OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) 頁面含有您可以在有或無祕密資訊的情況下使用的檔案。</span><span class="sxs-lookup"><span data-stu-id="21f49-306">At the [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) page, there are files that you can use with or without your secret information.</span></span>

- <span data-ttu-id="21f49-307">預設 OMS 代理程式精靈集 (omsagent.yaml) 沒有密碼資訊</span><span class="sxs-lookup"><span data-stu-id="21f49-307">The Default OMS Agent DaemonSet does not have secret information (omsagent.yaml)</span></span>
- <span data-ttu-id="21f49-308">OMS 代理程式精靈集YAML 檔案使用密碼資訊 (omsagent-ds-secrets.yaml) 搭配密碼產生指令碼來產生密碼 YAML (omsagentsecret.yaml) 檔案。</span><span class="sxs-lookup"><span data-stu-id="21f49-308">The OMS Agent DaemonSet yaml file uses secret information (omsagent-ds-secrets.yaml) with secret generation scripts to generate the secrets yaml (omsagentsecret.yaml) file.</span></span>

<span data-ttu-id="21f49-309">您可以選擇在有或無祕密的情況下建立 omsagent DaemonSet。</span><span class="sxs-lookup"><span data-stu-id="21f49-309">You can choose to create omsagent DaemonSets with or without secrets.</span></span>

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a><span data-ttu-id="21f49-310">沒有祕密的預設 OMSagent DaemonSet yaml 檔案</span><span class="sxs-lookup"><span data-stu-id="21f49-310">Default OMSagent DaemonSet yaml file without secrets</span></span>

- <span data-ttu-id="21f49-311">針對預設 OMS 代理程式 DaemonSet yaml 檔案，用您的 WSID 和索引鍵取代 `<WSID>` 和 `<KEY>`。</span><span class="sxs-lookup"><span data-stu-id="21f49-311">For the default OMS Agent DaemonSet yaml file, replace the `<WSID>` and `<KEY>` to your WSID and KEY.</span></span> <span data-ttu-id="21f49-312">將檔案複製到您的主要節點，並執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="21f49-312">Copy the file to your master node and run the following:</span></span>

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a><span data-ttu-id="21f49-313">有祕密的預設 OMSagent DaemonSet yaml 檔案</span><span class="sxs-lookup"><span data-stu-id="21f49-313">Default OMSagent DaemonSet yaml file with secrets</span></span>

1. <span data-ttu-id="21f49-314">若要使用具有祕密資訊的 OMS 代理程式 DaemonSet，請先建立祕密。</span><span class="sxs-lookup"><span data-stu-id="21f49-314">To use OMS Agent DaemonSet using secret information, create the secrets first.</span></span>
    1. <span data-ttu-id="21f49-315">複製指令碼和祕密範本檔案，並確定它們位於相同的目錄。</span><span class="sxs-lookup"><span data-stu-id="21f49-315">Copy the script and secret template file and make sure they are on the same directory.</span></span>
        - <span data-ttu-id="21f49-316">祕密產生指令碼 - secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="21f49-316">Secret generating script - secret-gen.sh</span></span>
        - <span data-ttu-id="21f49-317">祕密範本 - secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="21f49-317">secret template - secret-template.yaml</span></span>
    2. <span data-ttu-id="21f49-318">執行指令碼，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="21f49-318">Run the script, like the following example.</span></span> <span data-ttu-id="21f49-319">指令碼會要求 OMS 工作區識別碼與主索引鍵，在您輸入這兩個資訊之後，指令碼會建立一個密碼 YAML 檔案讓您能夠執行它。</span><span class="sxs-lookup"><span data-stu-id="21f49-319">The script asks for the OMS Workspace ID and Primary Key and after you enter them, the script creates a secret yaml file so you can run it.</span></span>   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. <span data-ttu-id="21f49-320">執行以下命令來建立祕密 Pod：</span><span class="sxs-lookup"><span data-stu-id="21f49-320">Create the secrets pod by running the following:</span></span>
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. <span data-ttu-id="21f49-321">若要確認，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="21f49-321">To verify, run the following:</span></span>

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        <span data-ttu-id="21f49-322">輸出會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="21f49-322">Output should resemble:</span></span>

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        <span data-ttu-id="21f49-323">輸出會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="21f49-323">Output should resemble:</span></span>

        ```
        Name:           omsagent-secret
        Namespace:      default
        Labels:         <none>
        Annotations:    <none>

        Type:   Opaque

        Data
        ====
        WSID:   36 bytes
        KEY:    88 bytes
        ```

    5. <span data-ttu-id="21f49-324">執行 ``` sudo kubectl create -f omsagent-ds-secrets.yaml ``` 以建立您的 omsagent daemon-set</span><span class="sxs-lookup"><span data-stu-id="21f49-324">Create your omsagent daemon-set by running ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

2. <span data-ttu-id="21f49-325">確認 OMS 代理程式 DaemonSet 正在執行，如下所示：</span><span class="sxs-lookup"><span data-stu-id="21f49-325">Verify that the OMS Agent DaemonSet is running, similar to the following:</span></span>

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


<span data-ttu-id="21f49-326">針對 Kubernetes，使用指令碼為工作區識別碼與主索引鍵產生祕密 yaml 檔案。</span><span class="sxs-lookup"><span data-stu-id="21f49-326">For Kubernetes, use a script to generate the secrets yaml file for Workspace ID and Primary Key.</span></span> <span data-ttu-id="21f49-327">搭配 [omsagent yaml 檔案](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml)使用下列範例資訊來保護您的祕密資訊。</span><span class="sxs-lookup"><span data-stu-id="21f49-327">Use the following example information with the [omsagent yaml file](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) to secure your secret information.</span></span>

```
keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
Name:           omsagent-secret
Namespace:      default
Labels:         <none>
Annotations:    <none>

Type:   Opaque

Data
====
WSID:   36 bytes
KEY:    88 bytes
```

## <a name="windows-container-hosts"></a><span data-ttu-id="21f49-328">Windows 容器主機</span><span class="sxs-lookup"><span data-stu-id="21f49-328">Windows container hosts</span></span>

### <a name="preparation-before-installing-windows-agents"></a><span data-ttu-id="21f49-329">安裝 Windows 代理程式之前的準備動作</span><span class="sxs-lookup"><span data-stu-id="21f49-329">Preparation before installing Windows agents</span></span>

<span data-ttu-id="21f49-330">在執行 Windows 的電腦上安裝代理程式之前，您需要設定 Docker 服務。</span><span class="sxs-lookup"><span data-stu-id="21f49-330">Before you install agents on computers running Windows, you need to configure the Docker service.</span></span> <span data-ttu-id="21f49-331">組態可讓 Windows 代理程式或 Log Analytics 虛擬機器擴充功能使用 Docker TCP 通訊端，讓代理程式可以從遠端存取的 Docker 精靈並擷取監視資料。</span><span class="sxs-lookup"><span data-stu-id="21f49-331">The configuration allows the Windows agent or the Log Analytics virtual machine extension to use the Docker TCP socket so that the agents can access the Docker daemon remotely and to capture data for monitoring.</span></span>

#### <a name="to-start-docker-and-verify-its-configuration"></a><span data-ttu-id="21f49-332">若要啟動 Docker 並確認其組態</span><span class="sxs-lookup"><span data-stu-id="21f49-332">To start Docker and verify its configuration</span></span>

<span data-ttu-id="21f49-333">若要設定 Windows Server 的 TCP 具名管道，需要執行一些步驟︰</span><span class="sxs-lookup"><span data-stu-id="21f49-333">There are steps needed to set up TCP named pipe for Windows Server:</span></span>

1. <span data-ttu-id="21f49-334">在 Windows PowerShell 中啟用 TCP 管道和具名的管道。</span><span class="sxs-lookup"><span data-stu-id="21f49-334">In Windows PowerShell, enable TCP pipe and named pipe.</span></span>

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. <span data-ttu-id="21f49-335">使用 TCP 管道和具名管道的組態檔來設定 Docker。</span><span class="sxs-lookup"><span data-stu-id="21f49-335">Configure Docker with the configuration file for TCP pipe and named pipe.</span></span> <span data-ttu-id="21f49-336">此組態檔位於 C:\ProgramData\docker\config\daemon.json。</span><span class="sxs-lookup"><span data-stu-id="21f49-336">The configuration file is located at C:\ProgramData\docker\config\daemon.json.</span></span>

    <span data-ttu-id="21f49-337">在 daemon.json 檔案中，您將需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="21f49-337">In the daemon.json file, you will need the following:</span></span>

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

<span data-ttu-id="21f49-338">如需 Windows 容器使用之 Docker 精靈組態的詳細資訊，請參閱 [Windows 上的 Docker 引擎](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon)。</span><span class="sxs-lookup"><span data-stu-id="21f49-338">For more information about the Docker daemon configuration used with Windows Containers, see [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span></span>


### <a name="install-windows-agents"></a><span data-ttu-id="21f49-339">安裝 Windows 代理程式</span><span class="sxs-lookup"><span data-stu-id="21f49-339">Install Windows agents</span></span>

<span data-ttu-id="21f49-340">若要啟用 Windows 和 Hyper-V 容器監視，請在容器主機的 Windows 電腦上安裝 Microsoft Monitoring Agent (MMA)。</span><span class="sxs-lookup"><span data-stu-id="21f49-340">To enable Windows and Hyper-V container monitoring, install the Microsoft Monitoring Agent (MMA) on Windows computers that are container hosts.</span></span> <span data-ttu-id="21f49-341">若需要在內部部署環境中執行 Windows 的電腦，請參閱[連接 Windows 電腦至 Log Analytics](log-analytics-windows-agents.md)。</span><span class="sxs-lookup"><span data-stu-id="21f49-341">For computers running Windows in your on-premises environment, see [Connect Windows computers to Log Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="21f49-342">若需要在 Azure 中執行的虛擬機器，可使用[虛擬機器擴充功能](log-analytics-azure-vm-extension.md)將它們連接至 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="21f49-342">For virtual machines running in Azure, connect them to Log Analytics using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="21f49-343">您可以監視 Service Fabric 上執行的 Windows 容器。</span><span class="sxs-lookup"><span data-stu-id="21f49-343">You can monitor Windows containers running on Service Fabric.</span></span> <span data-ttu-id="21f49-344">不過，Service Fabric 目前只支援 [Azure 中執行的虛擬機器](log-analytics-azure-vm-extension.md)和[在內部部署環境中執行 Windows 的電腦](log-analytics-windows-agents.md)。</span><span class="sxs-lookup"><span data-stu-id="21f49-344">However, only [virtual machines running in Azure](log-analytics-azure-vm-extension.md) and [computers running Windows in your on-premises environment](log-analytics-windows-agents.md) are currently supported for Service Fabric.</span></span>

<span data-ttu-id="21f49-345">您可以確認容器監視解決方案已針對 Windows 正確設定。</span><span class="sxs-lookup"><span data-stu-id="21f49-345">You can verify that the Container Monitoring solution is set correctly for Windows.</span></span> <span data-ttu-id="21f49-346">若要檢查管理組件是否正確下載，請找出 ContainerManagement.xxx。</span><span class="sxs-lookup"><span data-stu-id="21f49-346">To check whether the management pack was download properly, look for *ContainerManagement.xxx*.</span></span> <span data-ttu-id="21f49-347">這些檔案應在 C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs 資料夾。</span><span class="sxs-lookup"><span data-stu-id="21f49-347">The files should be in the C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs folder.</span></span>


## <a name="solution-components"></a><span data-ttu-id="21f49-348">方案元件</span><span class="sxs-lookup"><span data-stu-id="21f49-348">Solution components</span></span>

<span data-ttu-id="21f49-349">如果您是使用 Windows 代理程式，當您新增這個解決方案時，就會使用代理程式在每部電腦上安裝下列管理組件。</span><span class="sxs-lookup"><span data-stu-id="21f49-349">If you are using Windows agents, then the following management pack is installed on each computer with an agent when you add this solution.</span></span> <span data-ttu-id="21f49-350">管理組件不需要任何設定或維護。</span><span class="sxs-lookup"><span data-stu-id="21f49-350">No configuration or maintenance is required for the management pack.</span></span>

- <span data-ttu-id="21f49-351">C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs 中所安裝的 ContainerManagement.xxx</span><span class="sxs-lookup"><span data-stu-id="21f49-351">*ContainerManagement.xxx* installed in C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span></span>

## <a name="container-data-collection-details"></a><span data-ttu-id="21f49-352">容器資料收集詳細資料</span><span class="sxs-lookup"><span data-stu-id="21f49-352">Container data collection details</span></span>
<span data-ttu-id="21f49-353">容器監視解決方案會從使用您已啟用之代理程式的容器主機和容器中，收集各種效能計量和記錄資料。</span><span class="sxs-lookup"><span data-stu-id="21f49-353">The Container Monitoring solution collects various performance metrics and log data from container hosts and containers using agents that you enable.</span></span>

<span data-ttu-id="21f49-354">每隔三分鐘會依下列代理程式類型收集資料。</span><span class="sxs-lookup"><span data-stu-id="21f49-354">Data is collected every three minutes by the following agent types.</span></span>

- [<span data-ttu-id="21f49-355">OMS Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="21f49-355">OMS Agent for Linux</span></span>](log-analytics-linux-agents.md)
- [<span data-ttu-id="21f49-356">Windows 代理程式</span><span class="sxs-lookup"><span data-stu-id="21f49-356">Windows agent</span></span>](log-analytics-windows-agents.md)
- [<span data-ttu-id="21f49-357">Log Analytics VM 延伸模組</span><span class="sxs-lookup"><span data-stu-id="21f49-357">Log Analytics VM extension</span></span>](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a><span data-ttu-id="21f49-358">容器資料列</span><span class="sxs-lookup"><span data-stu-id="21f49-358">Container records</span></span>

<span data-ttu-id="21f49-359">下表顯示的範例是容器監視解決方案所收集的資料列，以及記錄搜尋結果中所顯示之資料類型。</span><span class="sxs-lookup"><span data-stu-id="21f49-359">The following table shows examples of records collected by the Container Monitoring solution and the data types that appear in log search results.</span></span>

| <span data-ttu-id="21f49-360">資料類型</span><span class="sxs-lookup"><span data-stu-id="21f49-360">Data type</span></span> | <span data-ttu-id="21f49-361">記錄檔搜尋中的資料類型</span><span class="sxs-lookup"><span data-stu-id="21f49-361">Data type in Log Search</span></span> | <span data-ttu-id="21f49-362">欄位</span><span class="sxs-lookup"><span data-stu-id="21f49-362">Fields</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f49-363">主機和容器的效能</span><span class="sxs-lookup"><span data-stu-id="21f49-363">Performance for hosts and containers</span></span> | `Type=Perf` | <span data-ttu-id="21f49-364">Computer、ObjectName、CounterName &#40;%Processor Time、Disk Reads MB、Disk Writes MB、Memory Usage MB、Network Receive Bytes、Network Send Bytes、Processor Usage sec、Network&#41;、CounterValue、TimeGenerated、CounterPath、SourceSystem</span><span class="sxs-lookup"><span data-stu-id="21f49-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span></span> |
| <span data-ttu-id="21f49-365">容器清查</span><span class="sxs-lookup"><span data-stu-id="21f49-365">Container inventory</span></span> | `Type=ContainerInventory` | <span data-ttu-id="21f49-366">TimeGenerated、Computer、container name、ContainerHostname、Image、ImageTag、ContainerState、ExitCode、EnvironmentVar、Command、CreatedTime、StartedTime、FinishedTime、SourceSystem、ContainerID、ImageID</span><span class="sxs-lookup"><span data-stu-id="21f49-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span></span> |
| <span data-ttu-id="21f49-367">容器映像清查</span><span class="sxs-lookup"><span data-stu-id="21f49-367">Container image inventory</span></span> | `Type=ContainerImageInventory` | <span data-ttu-id="21f49-368">TimeGenerated、Computer、Image、ImageTag、ImageSize、VirtualSize、Running、Paused、Stopped、Failed、SourceSystem、ImageID、TotalContainer</span><span class="sxs-lookup"><span data-stu-id="21f49-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span></span> |
| <span data-ttu-id="21f49-369">容器記錄檔</span><span class="sxs-lookup"><span data-stu-id="21f49-369">Container log</span></span> | `Type=ContainerLog` | <span data-ttu-id="21f49-370">TimeGenerated、Computer、image ID、container name、LogEntrySource、LogEntry、SourceSystem、ContainerID</span><span class="sxs-lookup"><span data-stu-id="21f49-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="21f49-371">容器服務記錄檔</span><span class="sxs-lookup"><span data-stu-id="21f49-371">Container service log</span></span> | `Type=ContainerServiceLog`  | <span data-ttu-id="21f49-372">TimeGenerated、Computer、TimeOfCommand、Image、Command、SourceSystem、ContainerID</span><span class="sxs-lookup"><span data-stu-id="21f49-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="21f49-373">容器節點清查</span><span class="sxs-lookup"><span data-stu-id="21f49-373">Container node inventory</span></span> | `Type=ContainerNodeInventory_CL`| <span data-ttu-id="21f49-374">TimeGenerated、Computer、ClassName_s、DockerVersion_s、OperatingSystem_s、Volume_s、Network_s、NodeRole_s、OrchestratorType_s、InstanceID_g、SourceSystem</span><span class="sxs-lookup"><span data-stu-id="21f49-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span></span>|
| <span data-ttu-id="21f49-375">Kubernetes 清查</span><span class="sxs-lookup"><span data-stu-id="21f49-375">Kubernetes inventory</span></span> | `Type=KubePodInventory_CL` | <span data-ttu-id="21f49-376">TimeGenerated、Computer、PodLabel_deployment_s、PodLabel_deploymentconfig_s、PodLabel_docker_registry_s、Name_s、Namespace_s、PodStatus_s、PodIp_s、PodUid_g、PodCreationTimeStamp_t、SourceSystem</span><span class="sxs-lookup"><span data-stu-id="21f49-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span></span> |
| <span data-ttu-id="21f49-377">容器流程</span><span class="sxs-lookup"><span data-stu-id="21f49-377">Container process</span></span> | `Type=ContainerProcess_CL` | <span data-ttu-id="21f49-378">TimeGenerated、Computer、Pod_s、Namespace_s、ClassName_s、InstanceID_s、Uid_s、PID_s、PPID_s、C_s、STIME_s、Tty_s、TIME_s、Cmd_s、Id_s、Name_s、SourceSystem</span><span class="sxs-lookup"><span data-stu-id="21f49-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span></span> |
| <span data-ttu-id="21f49-379">Kubernetes 事件</span><span class="sxs-lookup"><span data-stu-id="21f49-379">Kubernetes events</span></span> | `Type=KubeEvents_CL` | <span data-ttu-id="21f49-380">TimeGenerated、Computer、Name_s、ObjectKind_s、Namespace_s、Reason_s、Type_s、SourceComponent_s、SourceSystem、Message</span><span class="sxs-lookup"><span data-stu-id="21f49-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span></span> |

<span data-ttu-id="21f49-381">附加到 PodLabel 資料類型的標籤是您自己的自訂標籤。</span><span class="sxs-lookup"><span data-stu-id="21f49-381">Labels appended to *PodLabel* data types are your own custom labels.</span></span> <span data-ttu-id="21f49-382">資料表中所顯示的附加 PodLabel 標籤就是範例。</span><span class="sxs-lookup"><span data-stu-id="21f49-382">The appended PodLabel labels shown in the table are examples.</span></span> <span data-ttu-id="21f49-383">因此，`PodLabel_deployment_s`、`PodLabel_deploymentconfig_s`、`PodLabel_docker_registry_s` 在環境的資料集中會有所不同，且一般而言會類似 `PodLabel_yourlabel_s`。</span><span class="sxs-lookup"><span data-stu-id="21f49-383">So, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` will differ in your environment's data set and generically resemble `PodLabel_yourlabel_s`.</span></span>


## <a name="monitor-containers"></a><span data-ttu-id="21f49-384">監視容器</span><span class="sxs-lookup"><span data-stu-id="21f49-384">Monitor containers</span></span>
<span data-ttu-id="21f49-385">在 OMS 入口網站中啟用此解決方案之後，[容器] 圖格會顯示容器主機和主機中執行之容器的相關摘要資訊。</span><span class="sxs-lookup"><span data-stu-id="21f49-385">After you have the solution enabled in the OMS portal, the **Containers** tile shows summary information about your container hosts and the containers running in hosts.</span></span>

![容器圖格](./media/log-analytics-containers/containers-title.png)

<span data-ttu-id="21f49-387">此圖格顯示環境中有多少容器以及其為失敗、執行中或已停止的概觀。</span><span class="sxs-lookup"><span data-stu-id="21f49-387">The tile shows an overview of how many containers you have in the environment and whether they're failed, running, or stopped.</span></span>

### <a name="using-the-containers-dashboard"></a><span data-ttu-id="21f49-388">使用容器儀表板</span><span class="sxs-lookup"><span data-stu-id="21f49-388">Using the Containers dashboard</span></span>
<span data-ttu-id="21f49-389">按一下 [容器] 圖格。</span><span class="sxs-lookup"><span data-stu-id="21f49-389">Click the **Containers** tile.</span></span> <span data-ttu-id="21f49-390">在這裡，您會看到依下列各項組織的檢視︰</span><span class="sxs-lookup"><span data-stu-id="21f49-390">From there you'll see views organized by:</span></span>

- <span data-ttu-id="21f49-391">**容器事件** - 會顯示容器狀態和包含失敗容器的電腦。</span><span class="sxs-lookup"><span data-stu-id="21f49-391">**Container Events** - Shows container status and computers with failed containers.</span></span>
- <span data-ttu-id="21f49-392">**容器記錄** - 會顯示一段時間所產生的容器記錄檔圖表，和包含最大量記錄檔的電腦清單。</span><span class="sxs-lookup"><span data-stu-id="21f49-392">**Container Logs** - Shows a chart of container log files generated over time and a list of computers with the highest number of log files.</span></span>
- <span data-ttu-id="21f49-393">**Kubernetes 事件** - 會顯示一段時間所產生的 Kubernetes 事件圖表，和 Pod 產生事件的原因清單。</span><span class="sxs-lookup"><span data-stu-id="21f49-393">**Kubernetes Events** - Shows a chart of Kubernetes events generated over time and a list of the reasons why pods generated the events.</span></span> <span data-ttu-id="21f49-394">只有在 Linux 環境中才會使用此資料集。</span><span class="sxs-lookup"><span data-stu-id="21f49-394">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="21f49-395">**Kubernetes 命名空間清查** - 會顯示命名空間和 Pod 的數目，並顯示其階層。</span><span class="sxs-lookup"><span data-stu-id="21f49-395">**Kubernetes Namespace Inventory** - Shows the number of namespaces and pods and shows their hierarchy.</span></span> <span data-ttu-id="21f49-396">只有在 Linux 環境中才會使用此資料集。</span><span class="sxs-lookup"><span data-stu-id="21f49-396">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="21f49-397">**容器節點清查** - 會顯示容器節點/主機上使用的協調流程類型數目。</span><span class="sxs-lookup"><span data-stu-id="21f49-397">**Container Node Inventory** - Shows the number of orchestration types used on container nodes/hosts.</span></span> <span data-ttu-id="21f49-398">還會依容器數目列出電腦節點/主機。</span><span class="sxs-lookup"><span data-stu-id="21f49-398">The computer nodes/hosts are also listed by the number of containers.</span></span> <span data-ttu-id="21f49-399">只有在 Linux 環境中才會使用此資料集。</span><span class="sxs-lookup"><span data-stu-id="21f49-399">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="21f49-400">**容器映像庫存** - 會顯示已使用的容器映像總數和映像類型的數目。</span><span class="sxs-lookup"><span data-stu-id="21f49-400">**Container Images Inventory** - Shows the total number of container images used and number of image types.</span></span> <span data-ttu-id="21f49-401">還會依影像標籤列出映像數目。</span><span class="sxs-lookup"><span data-stu-id="21f49-401">The number of images are also listed by the image tag.</span></span>
- <span data-ttu-id="21f49-402">**容器狀態** - 會顯示具有執行中容器的容器節點/主機電腦總數。</span><span class="sxs-lookup"><span data-stu-id="21f49-402">**Containers Status** - Shows the total number of container nodes/host computers that have running containers.</span></span> <span data-ttu-id="21f49-403">還會依執行中主機的數目列出電腦。</span><span class="sxs-lookup"><span data-stu-id="21f49-403">Computers are also listed by the number of running hosts.</span></span>
- <span data-ttu-id="21f49-404">**容器流程** - 會顯示一段時間執行的容器流程折線圖。</span><span class="sxs-lookup"><span data-stu-id="21f49-404">**Container Process** - Shows a line chart of container processes running over time.</span></span> <span data-ttu-id="21f49-405">還會依容器內的執行命令/流程列出容器。</span><span class="sxs-lookup"><span data-stu-id="21f49-405">Containers are also listed by running command/process within containers.</span></span> <span data-ttu-id="21f49-406">只有在 Linux 環境中才會使用此資料集。</span><span class="sxs-lookup"><span data-stu-id="21f49-406">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="21f49-407">**容器 CPU 效能** - 會顯示一段時間電腦節點/主機的平均 CPU 使用率折線圖。</span><span class="sxs-lookup"><span data-stu-id="21f49-407">**Container CPU Performance** - Shows a line chart of the average CPU utilization over time for computer nodes/hosts.</span></span> <span data-ttu-id="21f49-408">還會以平均 CPU 使用率作為基礎列出電腦節點/主機。</span><span class="sxs-lookup"><span data-stu-id="21f49-408">Also lists the computer nodes/hosts based on average CPU utilization.</span></span>
- <span data-ttu-id="21f49-409">**容器記憶體效能** - 會顯示一段時間的記憶體使用量折線圖。</span><span class="sxs-lookup"><span data-stu-id="21f49-409">**Container Memory Performance** - Shows a line chart of memory usage over time.</span></span> <span data-ttu-id="21f49-410">還會以執行個體名稱作為基礎列出電腦記憶體使用率。</span><span class="sxs-lookup"><span data-stu-id="21f49-410">Also lists computer memory utilization based on instance name.</span></span>
- <span data-ttu-id="21f49-411">**電腦效能** - 會顯示一段時間的 CPU 效能百分比、一段時間的記憶體使用量百分比，以及一段時間的可用磁碟空間 MB 等折線圖。</span><span class="sxs-lookup"><span data-stu-id="21f49-411">**Computer Performance** - Shows line charts of the percent of CPU performance over time, percent of memory usage over time, and megabytes of free disk space over time.</span></span> <span data-ttu-id="21f49-412">您可以將滑鼠停留在圖表中的任一行，以檢視更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="21f49-412">You can hover over any line in a chart to view more details.</span></span>


<span data-ttu-id="21f49-413">儀表板中的每個區域都是對所收集資料執行之搜尋的視覺表示方式。</span><span class="sxs-lookup"><span data-stu-id="21f49-413">Each area of the dashboard is a visual representation of a search that is run on collected data.</span></span>

![容器儀表板](./media/log-analytics-containers/containers-dash01.png)

![容器儀表板](./media/log-analytics-containers/containers-dash02.png)

<span data-ttu-id="21f49-416">在 [容器狀態] 區域中，按一下頂端區域，如下所示。</span><span class="sxs-lookup"><span data-stu-id="21f49-416">In the **Container Status** area, click the top area, as shown below.</span></span>

![容器狀態](./media/log-analytics-containers/containers-status.png)

<span data-ttu-id="21f49-418">[記錄搜尋] 隨即開啟，其中顯示您容器狀態的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="21f49-418">Log Search opens, displaying information about the state of your containers.</span></span>

![容器的記錄檔搜尋](./media/log-analytics-containers/containers-log-search.png)

<span data-ttu-id="21f49-420">在這裡，您可以編輯搜尋查詢來進行修改，以尋找您感興趣的特定資訊。</span><span class="sxs-lookup"><span data-stu-id="21f49-420">From here, you can edit the search query to modify it to find the specific information you're interested in.</span></span> <span data-ttu-id="21f49-421">如需記錄檔搜尋的詳細資訊，請參閱 [Log Analytics 中的記錄檔搜尋](log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="21f49-421">For more information about Log Searches, see [Log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

## <a name="troubleshoot-by-finding-a-failed-container"></a><span data-ttu-id="21f49-422">尋找失敗的容器以進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="21f49-422">Troubleshoot by finding a failed container</span></span>

<span data-ttu-id="21f49-423">如果容器已透過非零結束代碼結束，則 Log Analytics 會將容器標示為 [失敗]。</span><span class="sxs-lookup"><span data-stu-id="21f49-423">Log Analytics marks a container as **Failed** if it has exited with a non-zero exit code.</span></span> <span data-ttu-id="21f49-424">您可以在 [失敗的容器] 區域中，大致了解環境中的錯誤和失敗。</span><span class="sxs-lookup"><span data-stu-id="21f49-424">You can see an overview of the errors and failures in the environment in the **Failed Containers** area.</span></span>

### <a name="to-find-failed-containers"></a><span data-ttu-id="21f49-425">尋找失敗的容器</span><span class="sxs-lookup"><span data-stu-id="21f49-425">To find failed containers</span></span>
1. <span data-ttu-id="21f49-426">按一下 [容器狀態] 區域。</span><span class="sxs-lookup"><span data-stu-id="21f49-426">Click the **Container Status** area.</span></span>  
   <span data-ttu-id="21f49-427">![容器狀態](./media/log-analytics-containers/containers-status.png)</span><span class="sxs-lookup"><span data-stu-id="21f49-427">![containers status](./media/log-analytics-containers/containers-status.png)</span></span>
2. <span data-ttu-id="21f49-428">[記錄搜尋] 隨即開啟並顯示如下所示的容器狀態。</span><span class="sxs-lookup"><span data-stu-id="21f49-428">Log Search opens and displays the state of your containers, similar to the following.</span></span>  
   ![容器狀態](./media/log-analytics-containers/containers-log-search.png)
3. <span data-ttu-id="21f49-430">接下來，按一下失敗容器的彙總值，以檢視其他的資訊。</span><span class="sxs-lookup"><span data-stu-id="21f49-430">Next, click the aggregated value of failed containers to view additional information.</span></span> <span data-ttu-id="21f49-431">展開 [顯示更多] 以檢視映像識別碼。</span><span class="sxs-lookup"><span data-stu-id="21f49-431">Expand **show more** to view the image ID.</span></span>  
   <span data-ttu-id="21f49-432">![失敗的容器](./media/log-analytics-containers/containers-state-failed.png)</span><span class="sxs-lookup"><span data-stu-id="21f49-432">![failed containers](./media/log-analytics-containers/containers-state-failed.png)</span></span>  
4. <span data-ttu-id="21f49-433">接下來，在搜尋查詢中輸入下列內容。</span><span class="sxs-lookup"><span data-stu-id="21f49-433">Next, type the following in the search query.</span></span> <span data-ttu-id="21f49-434">`Type=ContainerInventory <ImageID>`可查看關於映像的詳細資料，例如停止和失敗映像的映像大小與數目。</span><span class="sxs-lookup"><span data-stu-id="21f49-434">`Type=ContainerInventory <ImageID>` to see details about the image such as image size and number of stopped and failed images.</span></span>  
   <span data-ttu-id="21f49-435">![失敗的容器](./media/log-analytics-containers/containers-failed04.png)</span><span class="sxs-lookup"><span data-stu-id="21f49-435">![failed containers](./media/log-analytics-containers/containers-failed04.png)</span></span>

## <a name="search-logs-for-container-data"></a><span data-ttu-id="21f49-436">搜尋容器資料的記錄檔</span><span class="sxs-lookup"><span data-stu-id="21f49-436">Search logs for container data</span></span>
<span data-ttu-id="21f49-437">當您針對特定錯誤進行疑難排解時，這助於查看您的環境中發生此錯誤的位置。</span><span class="sxs-lookup"><span data-stu-id="21f49-437">When you're troubleshooting a specific error, it can help to see where it is occurring in your environment.</span></span> <span data-ttu-id="21f49-438">下列記錄檔類型將協助您建立查詢，以傳回您想要的資訊。</span><span class="sxs-lookup"><span data-stu-id="21f49-438">The following log types will help you create queries to return the information you want.</span></span>


- <span data-ttu-id="21f49-439">**ContainerImageInventory** – 當您嘗試尋找依照映像組織的資訊，以及檢視映像資訊 (例如映像識別碼或大小) 時，請使用這個類型。</span><span class="sxs-lookup"><span data-stu-id="21f49-439">**ContainerImageInventory** – Use this type when you're trying to find information organized by image and to view image information such as image IDs or sizes.</span></span>
- <span data-ttu-id="21f49-440">**ContainerInventory** – 當您需要有關容器位置、其名稱，以及所執行映像的資訊時，請使用這個類型。</span><span class="sxs-lookup"><span data-stu-id="21f49-440">**ContainerInventory** – Use this type when you want information about container location, what their names are, and what images they're running.</span></span>
- <span data-ttu-id="21f49-441">**ContainerLog** – 當您想要尋找特定錯誤記錄檔資訊和項目時，請使用這個類型。</span><span class="sxs-lookup"><span data-stu-id="21f49-441">**ContainerLog** – Use this type when you want to find specific error log information and entries.</span></span>
- <span data-ttu-id="21f49-442">**ContainerNodeInventory_CL**  當您需要容器所在之主機/節點的相關資訊時，請使用這個類型。</span><span class="sxs-lookup"><span data-stu-id="21f49-442">**ContainerNodeInventory_CL**  Use this type when you want the information about host/node where containers are residing.</span></span> <span data-ttu-id="21f49-443">它會提供 Docker 版本、協調流程類型、儲存體和網路資訊。</span><span class="sxs-lookup"><span data-stu-id="21f49-443">It provides you Docker version, orchestration type, storage, and network information.</span></span>
- <span data-ttu-id="21f49-444">**ContainerProcess_CL** 使用此類型可快速查看容器內執行的流程。</span><span class="sxs-lookup"><span data-stu-id="21f49-444">**ContainerProcess_CL** Use this type to quickly see the process running within the container.</span></span>
- <span data-ttu-id="21f49-445">**ContainerServiceLog** – 當您嘗試尋找 Docker 精靈的稽核追蹤資訊 (例如啟動、停止、刪除或提取命令) 時，請使用這個類型。</span><span class="sxs-lookup"><span data-stu-id="21f49-445">**ContainerServiceLog** – Use this type when you're trying to find audit trail information for the Docker daemon, such as start, stop, delete, or pull commands.</span></span>
- <span data-ttu-id="21f49-446">**KubeEvents_CL**  使用此類型可查看 Kubernetes 事件。</span><span class="sxs-lookup"><span data-stu-id="21f49-446">**KubeEvents_CL**  Use this type to see the Kubernetes events.</span></span>
- <span data-ttu-id="21f49-447">**KubePodInventory_CL**  當您需要了解叢集階層資訊時，請使用此類型。</span><span class="sxs-lookup"><span data-stu-id="21f49-447">**KubePodInventory_CL**  Use this type when you want to understand the cluster hierarchy information.</span></span>


### <a name="to-search-logs-for-container-data"></a><span data-ttu-id="21f49-448">搜尋容器資料的記錄檔</span><span class="sxs-lookup"><span data-stu-id="21f49-448">To search logs for container data</span></span>
* <span data-ttu-id="21f49-449">選擇您知道最近失敗的映像並尋找其錯誤記錄檔。</span><span class="sxs-lookup"><span data-stu-id="21f49-449">Choose an image that you know has failed recently and find the error logs for it.</span></span> <span data-ttu-id="21f49-450">首先，透過 **ContainerInventory** 搜尋來尋找正在執行該映像的容器名稱。</span><span class="sxs-lookup"><span data-stu-id="21f49-450">Start by finding a container name that is running that image with a **ContainerInventory** search.</span></span> <span data-ttu-id="21f49-451">例如，搜尋 `Type=ContainerInventory ubuntu Failed`</span><span class="sxs-lookup"><span data-stu-id="21f49-451">For example, search for `Type=ContainerInventory ubuntu Failed`</span></span>  
    <span data-ttu-id="21f49-452">![搜尋 Ubuntu 容器](./media/log-analytics-containers/search-ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="21f49-452">![Search for Ubuntu containers](./media/log-analytics-containers/search-ubuntu.png)</span></span>

  <span data-ttu-id="21f49-453">[名稱] 旁的容器名稱，並搜尋其記錄。</span><span class="sxs-lookup"><span data-stu-id="21f49-453">The name of the container next to **Name**, and search for those logs.</span></span> <span data-ttu-id="21f49-454">在此範例中為 `Type=ContainerLog cranky_stonebreaker`。</span><span class="sxs-lookup"><span data-stu-id="21f49-454">In this example, it is `Type=ContainerLog cranky_stonebreaker`.</span></span>

<span data-ttu-id="21f49-455">**檢視效能資訊**</span><span class="sxs-lookup"><span data-stu-id="21f49-455">**View performance information**</span></span>

<span data-ttu-id="21f49-456">當您開始建構查詢時，這有助於先查看各種可能。</span><span class="sxs-lookup"><span data-stu-id="21f49-456">When you're beginning to construct queries, it can help to see what's possible first.</span></span> <span data-ttu-id="21f49-457">例如，若要查看所有效能資料，請輸入下列搜尋查詢，嘗試進行廣泛查詢。</span><span class="sxs-lookup"><span data-stu-id="21f49-457">For example, to see all performance data, try a broad query by typing the following search query.</span></span>

```
Type=Perf
```

![容器效能](./media/log-analytics-containers/containers-perf01.png)

<span data-ttu-id="21f49-459">您可以輸入查詢右邊的名稱，將您所見的效能資料範圍限制於特定容器。</span><span class="sxs-lookup"><span data-stu-id="21f49-459">You can scope the performance data you're seeing to a specific container by typing the name of it to the right of your query.</span></span>

```
Type=Perf <containerName>
```

<span data-ttu-id="21f49-460">其顯示針對個別容器所收集的效能計量清單。</span><span class="sxs-lookup"><span data-stu-id="21f49-460">That shows the list of performance metrics that are collected for an individual container.</span></span>

![容器效能](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a><span data-ttu-id="21f49-462">範例記錄檔搜尋查詢</span><span class="sxs-lookup"><span data-stu-id="21f49-462">Example log search queries</span></span>
<span data-ttu-id="21f49-463">從一或兩個範例開始建置查詢，然後加以修改以符合您的環境，通常很實用。</span><span class="sxs-lookup"><span data-stu-id="21f49-463">It's often useful to build queries starting with an example or two and then modifying them to fit your environment.</span></span> <span data-ttu-id="21f49-464">首先，您可以實驗 [查詢範例] 區域，協助您建置更進階的查詢。</span><span class="sxs-lookup"><span data-stu-id="21f49-464">As a starting point, you can experiment with the **Sample Queries** area to help you build more advanced queries.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![容器查詢](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a><span data-ttu-id="21f49-466">儲存記錄檔搜尋查詢</span><span class="sxs-lookup"><span data-stu-id="21f49-466">Saving log search queries</span></span>
<span data-ttu-id="21f49-467">儲存查詢是 Log Analytics 的標準功能。</span><span class="sxs-lookup"><span data-stu-id="21f49-467">Saving queries is a standard feature in Log Analytics.</span></span> <span data-ttu-id="21f49-468">藉由儲存查詢，您可將您覺得有用的查詢放在容易取得的地方，以便日後使用。</span><span class="sxs-lookup"><span data-stu-id="21f49-468">By saving them, you'll have those that you've found useful handy for future use.</span></span>

<span data-ttu-id="21f49-469">建立您覺得有用的查詢之後，按一下 [記錄檔搜尋] 頁面頂端的 [我的最愛] 來儲存它。</span><span class="sxs-lookup"><span data-stu-id="21f49-469">After you create a query that you find useful, save it by clicking **Favorites** at the top of the Log Search page.</span></span> <span data-ttu-id="21f49-470">然後您稍後即可輕易地從 [我的儀表板] 頁面進行存取。</span><span class="sxs-lookup"><span data-stu-id="21f49-470">Then you can easily access it later from the **My Dashboard** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21f49-471">後續步驟</span><span class="sxs-lookup"><span data-stu-id="21f49-471">Next steps</span></span>
* <span data-ttu-id="21f49-472">[搜尋記錄檔](log-analytics-log-searches.md)以檢視詳細的容器資料記錄。</span><span class="sxs-lookup"><span data-stu-id="21f49-472">[Search logs](log-analytics-log-searches.md) to view detailed container data records.</span></span>

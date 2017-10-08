---
title: "aaaContainer 監控 Azure 記錄分析解決方案 |Microsoft 文件"
description: "hello 容器監視方案中記錄分析可協助您檢視及管理您的 Docker 和 Windows 容器主機的單一位置。"
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
ms.openlocfilehash: 2eed1dd81c22faef78a375fca3ebece9e5300c09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a><span data-ttu-id="e14b9-103">Log Analytics 中的容器監視解決方案</span><span class="sxs-lookup"><span data-stu-id="e14b9-103">Container Monitoring solution in Log Analytics</span></span>

![容器符號](./media/log-analytics-containers/containers-symbol.png)

<span data-ttu-id="e14b9-105">本文說明如何向上 tooset 並用 hello 容器監視方案中記錄分析，可協助您檢視和管理您的 Docker 和 Windows 容器主機的單一位置。</span><span class="sxs-lookup"><span data-stu-id="e14b9-105">This article describes how tooset up and use hello Container Monitoring solution in Log Analytics, which helps you view and manage your Docker and Windows container hosts in a single location.</span></span> <span data-ttu-id="e14b9-106">Docker 的軟體虛擬化系統使用 toocreate 容器自動化軟體部署 tootheir IT 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="e14b9-106">Docker is a software virtualization system used toocreate containers that automate software deployment tootheir IT infrastructure.</span></span>

<span data-ttu-id="e14b9-107">hello 方案顯示哪些容器正在執行，它們正在執行時，哪些容器映像和容器執行的位置。</span><span class="sxs-lookup"><span data-stu-id="e14b9-107">hello solution shows which containers are running, what container image they’re running, and where containers are running.</span></span> <span data-ttu-id="e14b9-108">您可以檢視詳細的稽核資訊，其中顯示搭配容器使用的命令。</span><span class="sxs-lookup"><span data-stu-id="e14b9-108">You can view detailed audit information showing commands used with containers.</span></span> <span data-ttu-id="e14b9-109">此外，您可以透過檢視和搜尋而不需要 tooremotely 檢視 Docker 或 Windows 主機的集中式記錄檔來疑難排解容器。</span><span class="sxs-lookup"><span data-stu-id="e14b9-109">And, you can troubleshoot containers by viewing and searching centralized logs without having tooremotely view Docker or Windows hosts.</span></span> <span data-ttu-id="e14b9-110">您可能會找到有雜訊且耗用過多主機資源的容器。</span><span class="sxs-lookup"><span data-stu-id="e14b9-110">You can find containers that may be noisy and consuming excess resources on a host.</span></span> <span data-ttu-id="e14b9-111">而且，您可以檢視容器的集中式 CPU、記憶體、儲存體以及網路使用量和效能資訊。</span><span class="sxs-lookup"><span data-stu-id="e14b9-111">And, you can view centralized CPU, memory, storage, and network usage and performance information for containers.</span></span> <span data-ttu-id="e14b9-112">您可以在執行 Windows 的電腦上集中管理，並從 Windows Server、HYPER-V 和 Docker 容器比較記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e14b9-112">On computers running Windows, you can centralize and compare logs from Windows Server, Hyper-V, and Docker containers.</span></span> <span data-ttu-id="e14b9-113">hello 解決方案支援下列容器 orchestrators hello:</span><span class="sxs-lookup"><span data-stu-id="e14b9-113">hello solution supports hello following container orchestrators:</span></span>

- <span data-ttu-id="e14b9-114">Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="e14b9-114">Docker Swarm</span></span>
- <span data-ttu-id="e14b9-115">DC/OS</span><span class="sxs-lookup"><span data-stu-id="e14b9-115">DC/OS</span></span>
- <span data-ttu-id="e14b9-116">Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e14b9-116">Kubernetes</span></span>
- <span data-ttu-id="e14b9-117">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e14b9-117">Service Fabric</span></span>
- <span data-ttu-id="e14b9-118">Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="e14b9-118">Red Hat OpenShift</span></span>


<span data-ttu-id="e14b9-119">hello 下列圖表顯示 hello 各種容器主機和與 OMS 的代理程式之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="e14b9-119">hello following diagram shows hello relationships between various container hosts and agents with OMS.</span></span>

![容器圖表](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a><span data-ttu-id="e14b9-121">系統需求</span><span class="sxs-lookup"><span data-stu-id="e14b9-121">System requirements</span></span>

<span data-ttu-id="e14b9-122">開始之前，請檢閱下列符合 hello 必要條件的詳細資料 tooverify hello。</span><span class="sxs-lookup"><span data-stu-id="e14b9-122">Before starting, review hello following details tooverify you meet hello prerequisites.</span></span>

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a><span data-ttu-id="e14b9-123">容器監視解決方案支援 Docker Orchestrator 和作業系統平台</span><span class="sxs-lookup"><span data-stu-id="e14b9-123">Container monitoring solution support for Docker Orchestrator and OS platform</span></span>
<span data-ttu-id="e14b9-124">hello 表概述 hello Docker 協調流程和監視的容器清查、 效能和記錄檔記錄分析的支援的作業系統。</span><span class="sxs-lookup"><span data-stu-id="e14b9-124">hello following table outlines hello Docker orchestration and operating system monitoring support of container inventory, performance, and logs with Log Analytics.</span></span>   

| | <span data-ttu-id="e14b9-125">ACS</span><span class="sxs-lookup"><span data-stu-id="e14b9-125">ACS</span></span> | <span data-ttu-id="e14b9-126">Linux</span><span class="sxs-lookup"><span data-stu-id="e14b9-126">Linux</span></span> | <span data-ttu-id="e14b9-127">Windows</span><span class="sxs-lookup"><span data-stu-id="e14b9-127">Windows</span></span> | <span data-ttu-id="e14b9-128">容器</span><span class="sxs-lookup"><span data-stu-id="e14b9-128">Container</span></span><br><span data-ttu-id="e14b9-129">清查</span><span class="sxs-lookup"><span data-stu-id="e14b9-129">Inventory</span></span> | <span data-ttu-id="e14b9-130">映像</span><span class="sxs-lookup"><span data-stu-id="e14b9-130">Image</span></span><br><span data-ttu-id="e14b9-131">清查</span><span class="sxs-lookup"><span data-stu-id="e14b9-131">Inventory</span></span> | <span data-ttu-id="e14b9-132">節點</span><span class="sxs-lookup"><span data-stu-id="e14b9-132">Node</span></span><br><span data-ttu-id="e14b9-133">清查</span><span class="sxs-lookup"><span data-stu-id="e14b9-133">Inventory</span></span> | <span data-ttu-id="e14b9-134">容器</span><span class="sxs-lookup"><span data-stu-id="e14b9-134">Container</span></span><br><span data-ttu-id="e14b9-135">效能</span><span class="sxs-lookup"><span data-stu-id="e14b9-135">Performance</span></span> | <span data-ttu-id="e14b9-136">容器</span><span class="sxs-lookup"><span data-stu-id="e14b9-136">Container</span></span><br><span data-ttu-id="e14b9-137">Event</span><span class="sxs-lookup"><span data-stu-id="e14b9-137">Event</span></span> | <span data-ttu-id="e14b9-138">Event</span><span class="sxs-lookup"><span data-stu-id="e14b9-138">Event</span></span><br><span data-ttu-id="e14b9-139">記錄檔</span><span class="sxs-lookup"><span data-stu-id="e14b9-139">Log</span></span> | <span data-ttu-id="e14b9-140">容器</span><span class="sxs-lookup"><span data-stu-id="e14b9-140">Container</span></span><br><span data-ttu-id="e14b9-141">記錄檔</span><span class="sxs-lookup"><span data-stu-id="e14b9-141">Log</span></span> |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| <span data-ttu-id="e14b9-142">Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e14b9-142">Kubernetes</span></span> | <span data-ttu-id="e14b9-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-143">&#8226;</span></span> | <span data-ttu-id="e14b9-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-144">&#8226;</span></span> | | <span data-ttu-id="e14b9-145">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-145">&#8226;</span></span> | <span data-ttu-id="e14b9-146">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-146">&#8226;</span></span> | <span data-ttu-id="e14b9-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-147">&#8226;</span></span> | <span data-ttu-id="e14b9-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-148">&#8226;</span></span> | <span data-ttu-id="e14b9-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-149">&#8226;</span></span> | <span data-ttu-id="e14b9-150">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-150">&#8226;</span></span> | <span data-ttu-id="e14b9-151">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-151">&#8226;</span></span> |
| <span data-ttu-id="e14b9-152">Mesosphere</span><span class="sxs-lookup"><span data-stu-id="e14b9-152">Mesosphere</span></span><br><span data-ttu-id="e14b9-153">DC/OS</span><span class="sxs-lookup"><span data-stu-id="e14b9-153">DC/OS</span></span> | <span data-ttu-id="e14b9-154">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-154">&#8226;</span></span> | <span data-ttu-id="e14b9-155">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-155">&#8226;</span></span> | | <span data-ttu-id="e14b9-156">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-156">&#8226;</span></span> | <span data-ttu-id="e14b9-157">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-157">&#8226;</span></span> | <span data-ttu-id="e14b9-158">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-158">&#8226;</span></span> | <span data-ttu-id="e14b9-159">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-159">&#8226;</span></span>| <span data-ttu-id="e14b9-160">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-160">&#8226;</span></span> | <span data-ttu-id="e14b9-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-161">&#8226;</span></span> | <span data-ttu-id="e14b9-162">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-162">&#8226;</span></span> |
| <span data-ttu-id="e14b9-163">Docker</span><span class="sxs-lookup"><span data-stu-id="e14b9-163">Docker</span></span><br><span data-ttu-id="e14b9-164">Swarm</span><span class="sxs-lookup"><span data-stu-id="e14b9-164">Swarm</span></span> | <span data-ttu-id="e14b9-165">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-165">&#8226;</span></span> | <span data-ttu-id="e14b9-166">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-166">&#8226;</span></span> | <span data-ttu-id="e14b9-167">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-167">&#8226;</span></span> | <span data-ttu-id="e14b9-168">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-168">&#8226;</span></span> | <span data-ttu-id="e14b9-169">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-169">&#8226;</span></span> | <span data-ttu-id="e14b9-170">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-170">&#8226;</span></span> | <span data-ttu-id="e14b9-171">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-171">&#8226;</span></span> | <span data-ttu-id="e14b9-172">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-172">&#8226;</span></span> | | <span data-ttu-id="e14b9-173">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-173">&#8226;</span></span> |
| <span data-ttu-id="e14b9-174">服務</span><span class="sxs-lookup"><span data-stu-id="e14b9-174">Service</span></span><br><span data-ttu-id="e14b9-175">網狀架構</span><span class="sxs-lookup"><span data-stu-id="e14b9-175">Fabric</span></span> | | | <span data-ttu-id="e14b9-176">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-176">&#8226;</span></span> | <span data-ttu-id="e14b9-177">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-177">&#8226;</span></span> | <span data-ttu-id="e14b9-178">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-178">&#8226;</span></span> | <span data-ttu-id="e14b9-179">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-179">&#8226;</span></span> | <span data-ttu-id="e14b9-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-180">&#8226;</span></span> | <span data-ttu-id="e14b9-181">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-181">&#8226;</span></span> | <span data-ttu-id="e14b9-182">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-182">&#8226;</span></span> | <span data-ttu-id="e14b9-183">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-183">&#8226;</span></span> |
| <span data-ttu-id="e14b9-184">Red Hat 開啟</span><span class="sxs-lookup"><span data-stu-id="e14b9-184">Red Hat Open</span></span><br><span data-ttu-id="e14b9-185">移位</span><span class="sxs-lookup"><span data-stu-id="e14b9-185">Shift</span></span> | | <span data-ttu-id="e14b9-186">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-186">&#8226;</span></span> | | <span data-ttu-id="e14b9-187">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-187">&#8226;</span></span> | <span data-ttu-id="e14b9-188">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-188">&#8226;</span></span>| <span data-ttu-id="e14b9-189">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-189">&#8226;</span></span> | <span data-ttu-id="e14b9-190">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-190">&#8226;</span></span> | <span data-ttu-id="e14b9-191">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-191">&#8226;</span></span> | | <span data-ttu-id="e14b9-192">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-192">&#8226;</span></span> |
| <span data-ttu-id="e14b9-193">Windows Server</span><span class="sxs-lookup"><span data-stu-id="e14b9-193">Windows Server</span></span><br><span data-ttu-id="e14b9-194">(獨立)</span><span class="sxs-lookup"><span data-stu-id="e14b9-194">(standalone)</span></span> | | | <span data-ttu-id="e14b9-195">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-195">&#8226;</span></span> | <span data-ttu-id="e14b9-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-196">&#8226;</span></span> | <span data-ttu-id="e14b9-197">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-197">&#8226;</span></span> | <span data-ttu-id="e14b9-198">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-198">&#8226;</span></span> | <span data-ttu-id="e14b9-199">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-199">&#8226;</span></span> | <span data-ttu-id="e14b9-200">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-200">&#8226;</span></span> | | <span data-ttu-id="e14b9-201">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-201">&#8226;</span></span> |
| <span data-ttu-id="e14b9-202">Linux 伺服器</span><span class="sxs-lookup"><span data-stu-id="e14b9-202">Linux Server</span></span><br><span data-ttu-id="e14b9-203">(獨立)</span><span class="sxs-lookup"><span data-stu-id="e14b9-203">(standalone)</span></span> | | <span data-ttu-id="e14b9-204">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-204">&#8226;</span></span> | | <span data-ttu-id="e14b9-205">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-205">&#8226;</span></span> | <span data-ttu-id="e14b9-206">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-206">&#8226;</span></span> | <span data-ttu-id="e14b9-207">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-207">&#8226;</span></span> | <span data-ttu-id="e14b9-208">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-208">&#8226;</span></span> | <span data-ttu-id="e14b9-209">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-209">&#8226;</span></span> | | <span data-ttu-id="e14b9-210">&#8226;</span><span class="sxs-lookup"><span data-stu-id="e14b9-210">&#8226;</span></span> |


### <a name="docker-versions-supported-on-linux"></a><span data-ttu-id="e14b9-211">在 Linux 上支援的 Docker 版本</span><span class="sxs-lookup"><span data-stu-id="e14b9-211">Docker versions supported on Linux</span></span>

- <span data-ttu-id="e14b9-212">Docker 1.11 too1.13</span><span class="sxs-lookup"><span data-stu-id="e14b9-212">Docker 1.11 too1.13</span></span>
- <span data-ttu-id="e14b9-213">Docker CE 和 EE v17.06</span><span class="sxs-lookup"><span data-stu-id="e14b9-213">Docker CE and EE v17.06</span></span>

### <a name="x64-linux-distributions-supported-as-container-hosts"></a><span data-ttu-id="e14b9-214">x64 Linux 散發套件可支援作為容器主機</span><span class="sxs-lookup"><span data-stu-id="e14b9-214">x64 Linux distributions supported as container hosts</span></span>

- <span data-ttu-id="e14b9-215">Ubuntu 14.04 LTS 和 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="e14b9-215">Ubuntu 14.04 LTS and 16.04 LTS</span></span>
- <span data-ttu-id="e14b9-216">CoreOS (穩定版)</span><span class="sxs-lookup"><span data-stu-id="e14b9-216">CoreOS(stable)</span></span>
- <span data-ttu-id="e14b9-217">Amazon Linux 2016.09.0</span><span class="sxs-lookup"><span data-stu-id="e14b9-217">Amazon Linux 2016.09.0</span></span>
- <span data-ttu-id="e14b9-218">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="e14b9-218">openSUSE 13.2</span></span>
- <span data-ttu-id="e14b9-219">openSUSE LEAP 42.2</span><span class="sxs-lookup"><span data-stu-id="e14b9-219">openSUSE LEAP 42.2</span></span>
- <span data-ttu-id="e14b9-220">CentOS 7.2 和 7.3</span><span class="sxs-lookup"><span data-stu-id="e14b9-220">CentOS 7.2 and 7.3</span></span>
- <span data-ttu-id="e14b9-221">SLES 12</span><span class="sxs-lookup"><span data-stu-id="e14b9-221">SLES 12</span></span>
- <span data-ttu-id="e14b9-222">RHEL 7.2 和 7.3</span><span class="sxs-lookup"><span data-stu-id="e14b9-222">RHEL 7.2 and 7.3</span></span>
- <span data-ttu-id="e14b9-223">Red Hat OpenShift Container Platform (OCP) 3.4 和 3.5</span><span class="sxs-lookup"><span data-stu-id="e14b9-223">Red Hat OpenShift Container Platform (OCP) 3.4 and 3.5</span></span>
- <span data-ttu-id="e14b9-224">ACS Mesosphere DC/OS 1.7.3 too1.8.8</span><span class="sxs-lookup"><span data-stu-id="e14b9-224">ACS Mesosphere DC/OS 1.7.3 too1.8.8</span></span>
- <span data-ttu-id="e14b9-225">ACS Kubernetes 1.4.5 too1.6</span><span class="sxs-lookup"><span data-stu-id="e14b9-225">ACS Kubernetes 1.4.5 too1.6</span></span>
- <span data-ttu-id="e14b9-226">ACS Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="e14b9-226">ACS Docker Swarm</span></span>

### <a name="supported-windows-operating-system"></a><span data-ttu-id="e14b9-227">支援的 Windows 作業系統</span><span class="sxs-lookup"><span data-stu-id="e14b9-227">Supported Windows operating system</span></span>

- <span data-ttu-id="e14b9-228">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="e14b9-228">Windows Server 2016</span></span>
- <span data-ttu-id="e14b9-229">Windows 10 年度版 (Professional 或 Enterprise)</span><span class="sxs-lookup"><span data-stu-id="e14b9-229">Windows 10 Anniversary Edition (Professional or Enterprise)</span></span>

### <a name="docker-versions-supported-on-windows"></a><span data-ttu-id="e14b9-230">在 Windows 上支援 Docker 版本</span><span class="sxs-lookup"><span data-stu-id="e14b9-230">Docker versions supported on Windows</span></span>

- <span data-ttu-id="e14b9-231">Docker 1.12 和 1.13</span><span class="sxs-lookup"><span data-stu-id="e14b9-231">Docker 1.12 and 1.13</span></span>
- <span data-ttu-id="e14b9-232">Docker 17.03.0 和更新版本</span><span class="sxs-lookup"><span data-stu-id="e14b9-232">Docker 17.03.0 and later</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="e14b9-233">安裝和設定 hello 方案</span><span class="sxs-lookup"><span data-stu-id="e14b9-233">Installing and configuring hello solution</span></span>
<span data-ttu-id="e14b9-234">使用下列資訊 tooinstall hello 並設定 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="e14b9-234">Use hello following information tooinstall and configure hello solution.</span></span>

1. <span data-ttu-id="e14b9-235">新增 hello 容器監視解決方案 tooyour OMS 工作區從[Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview)或使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="e14b9-235">Add hello Container Monitoring solution tooyour OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

2. <span data-ttu-id="e14b9-236">安裝和使用 Docker 搭配 OMS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="e14b9-236">Install and use Docker with an OMS agent.</span></span>  <span data-ttu-id="e14b9-237">根據您的作業系統，您可以選擇從 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="e14b9-237">Based on your operating system, you can choose from hello following methods:</span></span>

  * <span data-ttu-id="e14b9-238">在支援 Linux 作業系統上安裝和執行 Docker，然後安裝並設定 hello [OMS Agent for Linux](log-analytics-agent-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="e14b9-238">On supported Linux operating systems, install and run Docker and then install and configure hello [OMS Agent for Linux](log-analytics-agent-linux.md).</span></span>  
  * <span data-ttu-id="e14b9-239">CoreOS，您無法執行 hello OMS Agent for Linux。</span><span class="sxs-lookup"><span data-stu-id="e14b9-239">On CoreOS, you cannot run hello OMS Agent for Linux.</span></span> <span data-ttu-id="e14b9-240">相反地，您可執行容器化的版本的 hello OMS Agent for Linux。</span><span class="sxs-lookup"><span data-stu-id="e14b9-240">Instead, you run a containerized version of hello OMS Agent for Linux.</span></span> <span data-ttu-id="e14b9-241">檢閱 [Linux 容器主機，包括 CoreOS](#for-all-linux-container-hosts-including-coreos) 或 [Azure Government Linux 容器主機，包括 CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos)，如果您正在使用 Azure Government Cloud 中的容器。</span><span class="sxs-lookup"><span data-stu-id="e14b9-241">Review [Linux container hosts including CoreOS](#for-all-linux-container-hosts-including-coreos) or [Azure Government Linux container hosts including CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) if you are working with containers in Azure Government Cloud.</span></span>
  * <span data-ttu-id="e14b9-242">在 Windows Server 2016 和 Windows 10 中，安裝 hello Docker 引擎與用戶端，然後連接的代理程式 toogather 資訊並傳送它 tooLog 分析。</span><span class="sxs-lookup"><span data-stu-id="e14b9-242">On Windows Server 2016 and Windows 10, install hello Docker Engine and client then connect an agent toogather information and send it tooLog Analytics.</span></span>  

### <a name="container-services"></a><span data-ttu-id="e14b9-243">容器服務</span><span class="sxs-lookup"><span data-stu-id="e14b9-243">Container services</span></span>

- <span data-ttu-id="e14b9-244">如果您有 Red Hat OpenShift 環境，請檢閱[針對 Red Hat OpenShift 設定 OMS 代理程式](#configure-an-oms-agent-for-red-hat-openshift)。</span><span class="sxs-lookup"><span data-stu-id="e14b9-244">If you have a Red Hat OpenShift environment, review [Configure an OMS agent for Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span></span>
- <span data-ttu-id="e14b9-245">如果您有使用 hello Azure 容器服務的 Kubernetes 叢集，檢閱[監視 Azure 容器服務叢集與 Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md)。</span><span class="sxs-lookup"><span data-stu-id="e14b9-245">If you have a Kubernetes cluster using hello Azure Container Service, review [Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span></span>
- <span data-ttu-id="e14b9-246">如果您擁有 Azure Container Service DC/OS 叢集，請深入了解[使用 Operations Management Suite 監視 Azure Container Service DC/OS 叢集](../container-service/dcos-swarm/container-service-monitoring-oms.md)。</span><span class="sxs-lookup"><span data-stu-id="e14b9-246">If you have an Azure Container Service DC/OS cluster, learn more at [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span></span>
- <span data-ttu-id="e14b9-247">如果您有 Docker Swarm 模式環境，詳細資訊請參閱[為 Docker Swarm 設定 OMS 代理程式](#configure-an-oms-agent-for-docker-swarm)。</span><span class="sxs-lookup"><span data-stu-id="e14b9-247">If you have a Docker Swarm mode environment, learn more at [Configure an OMS agent for Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span></span>
- <span data-ttu-id="e14b9-248">如果您搭配 Service Fabric 使用容器，請參閱 [Azure Service Fabric 概觀](../service-fabric/service-fabric-overview.md)以深入了解。</span><span class="sxs-lookup"><span data-stu-id="e14b9-248">If you use containers with Service Fabric, learn more at [Overview of Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span></span>
- <span data-ttu-id="e14b9-249">檢閱 hello [Windows 上的 Docker 引擎](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon)發行項，如需有關如何 tooinstall 和執行 Windows 的電腦上設定 Docker 引擎。</span><span class="sxs-lookup"><span data-stu-id="e14b9-249">Review hello [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article for additional information about how tooinstall and configure your Docker Engines on computers running Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e14b9-250">必須執行 docker**之前**安裝 hello [OMS Agent for Linux](log-analytics-agent-linux.md)容器主機上。</span><span class="sxs-lookup"><span data-stu-id="e14b9-250">Docker must be running **before** you install hello [OMS Agent for Linux](log-analytics-agent-linux.md) on your container hosts.</span></span> <span data-ttu-id="e14b9-251">如果您已經安裝 hello 代理程式安裝 Docker 之前，您需要 tooreinstall hello OMS Agent for Linux。</span><span class="sxs-lookup"><span data-stu-id="e14b9-251">If you've already installed hello agent before installing Docker, you need tooreinstall hello OMS Agent for Linux.</span></span> <span data-ttu-id="e14b9-252">如需有關 Docker 的詳細資訊，請參閱 hello [Docker 網站](https://www.docker.com)。</span><span class="sxs-lookup"><span data-stu-id="e14b9-252">For more information about Docker, see hello [Docker website](https://www.docker.com).</span></span>


## <a name="linux-container-hosts"></a><span data-ttu-id="e14b9-253">Linux 容器主機</span><span class="sxs-lookup"><span data-stu-id="e14b9-253">Linux container hosts</span></span>

<span data-ttu-id="e14b9-254">安裝 Docker 之後，使用下列設定容器主機 tooconfigure hello 代理程式用於 Docker 的 hello。</span><span class="sxs-lookup"><span data-stu-id="e14b9-254">After you've installed Docker, use hello following settings for your container host tooconfigure hello agent for use with Docker.</span></span> <span data-ttu-id="e14b9-255">首先您需要您的 OMS 工作區識別碼和金鑰，您可以在 hello Azure 入口網站中找到。</span><span class="sxs-lookup"><span data-stu-id="e14b9-255">First you need your OMS workspace ID and key, which you can find in hello Azure portal.</span></span> <span data-ttu-id="e14b9-256">在您的工作區中，按一下**快速入門** > **電腦**tooview 您**工作區識別碼**和**主索引鍵**。</span><span class="sxs-lookup"><span data-stu-id="e14b9-256">In your workspace, click **Quick Start** > **Computers** tooview your **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="e14b9-257">將兩者複製並貼到您最愛的編輯器。</span><span class="sxs-lookup"><span data-stu-id="e14b9-257">Copy and paste both into your favorite editor.</span></span>

### <a name="for-all-linux-container-hosts-except-coreos"></a><span data-ttu-id="e14b9-258">適用於 CoreOS 以外的所有 Linux 容器主機</span><span class="sxs-lookup"><span data-stu-id="e14b9-258">For all Linux container hosts except CoreOS</span></span>

- <span data-ttu-id="e14b9-259">如需詳細資訊和如何 tooinstall hello 適用於 Linux 的 OMS 代理程式上的步驟，請參閱[連接您的 Linux 電腦 tooOperations Management Suite (OMS)](log-analytics-agent-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="e14b9-259">For more information and steps on how tooinstall hello OMS Agent for Linux, see [Connect your Linux Computers tooOperations Management Suite (OMS)](log-analytics-agent-linux.md).</span></span>

### <a name="for-all-linux-container-hosts-including-coreos"></a><span data-ttu-id="e14b9-260">適用於包含 CoreOS 的所有 Linux 容器主機</span><span class="sxs-lookup"><span data-stu-id="e14b9-260">For all Linux container hosts including CoreOS</span></span>

<span data-ttu-id="e14b9-261">啟動您想 toomonitor hello OMS 容器。</span><span class="sxs-lookup"><span data-stu-id="e14b9-261">Start hello OMS container that you want toomonitor.</span></span> <span data-ttu-id="e14b9-262">修改並使用下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="e14b9-262">Modify and use hello following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a><span data-ttu-id="e14b9-263">適用於包含 CoreOS 的所有 Azure Government Linux 容器主機</span><span class="sxs-lookup"><span data-stu-id="e14b9-263">For all Azure Government Linux container hosts including CoreOS</span></span>

<span data-ttu-id="e14b9-264">啟動您想 toomonitor hello OMS 容器。</span><span class="sxs-lookup"><span data-stu-id="e14b9-264">Start hello OMS container that you want toomonitor.</span></span> <span data-ttu-id="e14b9-265">修改並使用下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="e14b9-265">Modify and use hello following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-tooone-in-a-container"></a><span data-ttu-id="e14b9-266">從使用已安裝的 Linux 代理程式 tooone 容器中切換</span><span class="sxs-lookup"><span data-stu-id="e14b9-266">Switching from using an installed Linux agent tooone in a container</span></span>
<span data-ttu-id="e14b9-267">如果您先前使用 hello 直接安裝代理程式，而想 tooinstead 使用容器中執行的代理程式，您必須先會移除 hello OMS Agent for Linux。</span><span class="sxs-lookup"><span data-stu-id="e14b9-267">If you previously used hello directly-installed agent and want tooinstead use an agent running in a container, you must first remove hello OMS Agent for Linux.</span></span> <span data-ttu-id="e14b9-268">請參閱[解除安裝 hello OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand toosuccessfully 的解除安裝 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="e14b9-268">See [Uninstalling hello OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand how toosuccessfully uninstall hello agent.</span></span>  

### <a name="configure-an-oms-agent-for-docker-swarm"></a><span data-ttu-id="e14b9-269">為 Docker Swarm 設定 OMS 代理程式</span><span class="sxs-lookup"><span data-stu-id="e14b9-269">Configure an OMS agent for Docker Swarm</span></span>

<span data-ttu-id="e14b9-270">您可以執行以全域服務的 hello OMS 代理程式上 Docker Swarm。</span><span class="sxs-lookup"><span data-stu-id="e14b9-270">You can run hello OMS Agent as a global service on Docker Swarm.</span></span> <span data-ttu-id="e14b9-271">使用下列資訊 toocreate OMS 代理程式服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="e14b9-271">Use hello following information toocreate an OMS Agent service.</span></span> <span data-ttu-id="e14b9-272">您需要 tooinsert OMS 工作區識別碼及主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e14b9-272">You need tooinsert your OMS Workspace ID and Primary Key.</span></span>

- <span data-ttu-id="e14b9-273">Hello 下列 hello 主要在節點上執行。</span><span class="sxs-lookup"><span data-stu-id="e14b9-273">Run hello following on hello master node.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a><span data-ttu-id="e14b9-274">為 Red Hat Openshift 設定 OMS 代理程式</span><span class="sxs-lookup"><span data-stu-id="e14b9-274">Configure an OMS Agent for Red Hat OpenShift</span></span>
<span data-ttu-id="e14b9-275">有三種方式 tooadd hello OMS Agent tooRed Hat OpenShift toostart 容器監視資料收集。</span><span class="sxs-lookup"><span data-stu-id="e14b9-275">There are three ways tooadd hello OMS Agent tooRed Hat OpenShift toostart collecting container monitoring data.</span></span>

* <span data-ttu-id="e14b9-276">[安裝 hello OMS Agent for Linux](log-analytics-agent-linux.md)直接在每個 OpenShift 節點上</span><span class="sxs-lookup"><span data-stu-id="e14b9-276">[Install hello OMS Agent for Linux](log-analytics-agent-linux.md) directly on each OpenShift node</span></span>  
* <span data-ttu-id="e14b9-277">在位於 Azure 中的每個 OpenShift 節點上[啟用記錄分析 VM 延伸模組](log-analytics-azure-vm-extension.md)</span><span class="sxs-lookup"><span data-stu-id="e14b9-277">[Enable Log Analytics VM Extension](log-analytics-azure-vm-extension.md) on each OpenShift node residing in Azure</span></span>  
* <span data-ttu-id="e14b9-278">Hello OMS 代理程式安裝為 OpenShift 精靈集</span><span class="sxs-lookup"><span data-stu-id="e14b9-278">Install hello OMS Agent as a OpenShift daemon-set</span></span>  

<span data-ttu-id="e14b9-279">在本節中，我們會討論 hello 步驟需要的 tooinstall hello OMS 代理程式 OpenShift 精靈設定。</span><span class="sxs-lookup"><span data-stu-id="e14b9-279">In this section we cover hello steps required tooinstall hello OMS Agent as an OpenShift daemon-set.</span></span>  

1. <span data-ttu-id="e14b9-280">登入 toohello OpenShift 主節點，然後複製 hello yaml 檔案[ocp omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml)從 GitHub tooyour 主要節點和修改 hello 值與您的 OMS 工作區識別碼和主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e14b9-280">Sign on toohello OpenShift master node and copy hello yaml file [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) from GitHub tooyour master node and modify hello value with your OMS Workspace ID and with your Primary Key.</span></span>
2. <span data-ttu-id="e14b9-281">執行下列命令 toocreate hello oms 的專案，然後設定 hello 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="e14b9-281">Run hello following commands toocreate a project for OMS and set hello user account.</span></span>

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="e14b9-282">toodeploy hello 精靈集執行 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="e14b9-282">toodeploy hello daemon-set, run hello following:</span></span>

    `oc create -f ocp-omsagent.yaml`

5. <span data-ttu-id="e14b9-283">tooverify 它已設定且運作正常，hello 下列輸入：</span><span class="sxs-lookup"><span data-stu-id="e14b9-283">tooverify it is configured and working correctly, type hello following:</span></span>

    `oc describe daemonset omsagent`  

    <span data-ttu-id="e14b9-284">和 hello 輸出應該類似：</span><span class="sxs-lookup"><span data-stu-id="e14b9-284">and hello output should resemble:</span></span>

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

<span data-ttu-id="e14b9-285">如果您想 toouse 密碼 toosecure 您的 OMS 工作區識別碼及主要金鑰使用 hello OMS 代理程式協助程式組 yaml 檔案時，，執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="e14b9-285">If you want toouse secrets toosecure your OMS Workspace ID and Primary Key when using hello OMS Agent daemon-set yaml file, perform hello following steps.</span></span>

1. <span data-ttu-id="e14b9-286">登入 toohello OpenShift 主節點，然後複製 hello yaml 檔案[ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml)和密碼產生指令碼[ocp secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh)從 GitHub。</span><span class="sxs-lookup"><span data-stu-id="e14b9-286">Sign on toohello OpenShift master node and copy hello yaml file [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) and secret generating script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) from GitHub.</span></span>  <span data-ttu-id="e14b9-287">此指令碼會產生 OMS 工作區識別碼及主要金鑰 toosecure hello 密碼 yaml 檔案您 secrete 資訊。</span><span class="sxs-lookup"><span data-stu-id="e14b9-287">This script will generate hello secrets yaml file for OMS Workspace ID and Primary Key toosecure your secrete information.</span></span>  
2. <span data-ttu-id="e14b9-288">執行下列命令 toocreate hello oms 的專案，然後設定 hello 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="e14b9-288">Run hello following commands toocreate a project for OMS and set hello user account.</span></span> <span data-ttu-id="e14b9-289">hello 密碼產生指令碼會要求您的 OMS 工作區識別碼<WSID>和主索引鍵<KEY>和完成時，它會建立 hello ocp secret.yaml 檔案。</span><span class="sxs-lookup"><span data-stu-id="e14b9-289">hello secret generating script asks for your OMS Workspace ID <WSID> and Primary Key <KEY> and upon completion, it creates hello ocp-secret.yaml file.</span></span>  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="e14b9-290">執行 hello 下列部署 hello 密碼檔案：</span><span class="sxs-lookup"><span data-stu-id="e14b9-290">Deploy hello secret file by running hello following:</span></span>

    `oc create -f ocp-secret.yaml`

5. <span data-ttu-id="e14b9-291">確認執行 hello 下列部署：</span><span class="sxs-lookup"><span data-stu-id="e14b9-291">Verify deployment by running hello following:</span></span>

    `oc describe secret omsagent-secret`  

    <span data-ttu-id="e14b9-292">和 hello 輸出應該類似：</span><span class="sxs-lookup"><span data-stu-id="e14b9-292">and hello  output should resemble:</span></span>  

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

6. <span data-ttu-id="e14b9-293">執行 hello 下列部署 hello OMS 代理程式協助程式組 yaml 檔：</span><span class="sxs-lookup"><span data-stu-id="e14b9-293">Deploy hello OMS Agent daemon-set yaml file by running hello following:</span></span>

    `oc create -f ocp-ds-omsagent.yaml`  

7. <span data-ttu-id="e14b9-294">確認執行 hello 下列部署：</span><span class="sxs-lookup"><span data-stu-id="e14b9-294">Verify deployment by running hello following:</span></span>

    `oc describe ds oms`

    <span data-ttu-id="e14b9-295">和 hello 輸出應該類似：</span><span class="sxs-lookup"><span data-stu-id="e14b9-295">and hello output should resemble:</span></span>

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

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a><span data-ttu-id="e14b9-296">保護 Docker Swarm 和 Kubernetes 的密碼資訊</span><span class="sxs-lookup"><span data-stu-id="e14b9-296">Secure your secret information for Docker Swarm and Kubernetes</span></span>

<span data-ttu-id="e14b9-297">您可以針對 Docker Swarm 和 Kubernetes 容器服務保護密碼 OMS 工作區識別碼與主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e14b9-297">You can secure your secret OMS Workspace ID and Primary Keys for Docker Swarm and Kubernetes container services.</span></span>

#### <a name="secure-secrets-for-docker-swarm"></a><span data-ttu-id="e14b9-298">保護 Docker Swarm 的祕密</span><span class="sxs-lookup"><span data-stu-id="e14b9-298">Secure secrets for Docker Swarm</span></span>

<span data-ttu-id="e14b9-299">Docker Swarm，一旦建立工作區識別碼及主要金鑰的 hello 密碼之後，您可以針對執行 hello 建立的 OMSagent hello Docker 服務。</span><span class="sxs-lookup"><span data-stu-id="e14b9-299">For Docker Swarm, once hello secret for Workspace ID and Primary Key is created, you can run hello create hello Docker service for OMSagent.</span></span> <span data-ttu-id="e14b9-300">使用下列資訊 toocreate hello 秘密資訊。</span><span class="sxs-lookup"><span data-stu-id="e14b9-300">Use hello following information toocreate your secret information.</span></span>

1. <span data-ttu-id="e14b9-301">Hello 下列 hello 主要在節點上執行。</span><span class="sxs-lookup"><span data-stu-id="e14b9-301">Run hello following on hello master node.</span></span>

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. <span data-ttu-id="e14b9-302">確認已正確建立祕密。</span><span class="sxs-lookup"><span data-stu-id="e14b9-302">Verify that secrets were created properly.</span></span>

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. <span data-ttu-id="e14b9-303">執行下列命令 toomount hello 密碼 toohello 的 hello 容器化 OMS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="e14b9-303">Run hello following command toomount hello secrets toohello containerized OMS Agent.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a><span data-ttu-id="e14b9-304">使用 yaml 檔案保護 Kubernetes 的祕密</span><span class="sxs-lookup"><span data-stu-id="e14b9-304">Secure secrets for Kubernetes with yaml files</span></span>

<span data-ttu-id="e14b9-305">Kubernetes，如中，您可以使用指令碼 toogenerate hello 密碼 yaml 檔案的工作區識別碼和主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e14b9-305">For Kubernetes, you use a script toogenerate hello secrets yaml file for your Workspace ID and Primary Key.</span></span> <span data-ttu-id="e14b9-306">在 hello [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)頁面上，您可以使用，不論您的機密資訊的檔案。</span><span class="sxs-lookup"><span data-stu-id="e14b9-306">At hello [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) page, there are files that you can use with or without your secret information.</span></span>

- <span data-ttu-id="e14b9-307">預設 OMS 代理程式 DaemonSet hello 沒有機密資訊 (omsagent.yaml)</span><span class="sxs-lookup"><span data-stu-id="e14b9-307">hello Default OMS Agent DaemonSet does not have secret information (omsagent.yaml)</span></span>
- <span data-ttu-id="e14b9-308">hello OMS 代理程式 DaemonSet yaml 檔案會使用密碼產生指令碼 toogenerate hello 密碼 yaml (omsagentsecret.yaml) 檔案中的機密資訊 (omsagent-ds-secrets.yaml)。</span><span class="sxs-lookup"><span data-stu-id="e14b9-308">hello OMS Agent DaemonSet yaml file uses secret information (omsagent-ds-secrets.yaml) with secret generation scripts toogenerate hello secrets yaml (omsagentsecret.yaml) file.</span></span>

<span data-ttu-id="e14b9-309">您可以選擇 toocreate omsagent DaemonSets 含密碼。</span><span class="sxs-lookup"><span data-stu-id="e14b9-309">You can choose toocreate omsagent DaemonSets with or without secrets.</span></span>

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a><span data-ttu-id="e14b9-310">沒有祕密的預設 OMSagent DaemonSet yaml 檔案</span><span class="sxs-lookup"><span data-stu-id="e14b9-310">Default OMSagent DaemonSet yaml file without secrets</span></span>

- <span data-ttu-id="e14b9-311">Hello 預設 OMS 代理程式 DaemonSet yaml 檔案取代 hello`<WSID>`和`<KEY>`tooyour WSID 和金鑰。</span><span class="sxs-lookup"><span data-stu-id="e14b9-311">For hello default OMS Agent DaemonSet yaml file, replace hello `<WSID>` and `<KEY>` tooyour WSID and KEY.</span></span> <span data-ttu-id="e14b9-312">複製 hello 檔案 tooyour 主要節點，然後執行的 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="e14b9-312">Copy hello file tooyour master node and run hello following:</span></span>

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a><span data-ttu-id="e14b9-313">有祕密的預設 OMSagent DaemonSet yaml 檔案</span><span class="sxs-lookup"><span data-stu-id="e14b9-313">Default OMSagent DaemonSet yaml file with secrets</span></span>

1. <span data-ttu-id="e14b9-314">toouse 使用機密資訊的 OMS 代理程式 DaemonSet 建立 hello 機密資料第一次。</span><span class="sxs-lookup"><span data-stu-id="e14b9-314">toouse OMS Agent DaemonSet using secret information, create hello secrets first.</span></span>
    1. <span data-ttu-id="e14b9-315">複製 hello 指令碼和密碼的範本檔案，並確定它們是在 hello 相同的目錄。</span><span class="sxs-lookup"><span data-stu-id="e14b9-315">Copy hello script and secret template file and make sure they are on hello same directory.</span></span>
        - <span data-ttu-id="e14b9-316">祕密產生指令碼 - secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="e14b9-316">Secret generating script - secret-gen.sh</span></span>
        - <span data-ttu-id="e14b9-317">祕密範本 - secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="e14b9-317">secret template - secret-template.yaml</span></span>
    2. <span data-ttu-id="e14b9-318">執行 hello 指令碼，如下列範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="e14b9-318">Run hello script, like hello following example.</span></span> <span data-ttu-id="e14b9-319">hello 指令碼會要求輸入 hello，OMS 工作區識別碼及主要金鑰，並輸入它們之後，hello 指令碼建立密碼 yaml 檔案，因此您可以在執行。</span><span class="sxs-lookup"><span data-stu-id="e14b9-319">hello script asks for hello OMS Workspace ID and Primary Key and after you enter them, hello script creates a secret yaml file so you can run it.</span></span>   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. <span data-ttu-id="e14b9-320">建立 hello 密碼 pod 執行 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="e14b9-320">Create hello secrets pod by running hello following:</span></span>
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. <span data-ttu-id="e14b9-321">tooverify，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="e14b9-321">tooverify, run hello following:</span></span>

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        <span data-ttu-id="e14b9-322">輸出會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="e14b9-322">Output should resemble:</span></span>

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        <span data-ttu-id="e14b9-323">輸出會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="e14b9-323">Output should resemble:</span></span>

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

    5. <span data-ttu-id="e14b9-324">執行 ``` sudo kubectl create -f omsagent-ds-secrets.yaml ``` 以建立您的 omsagent daemon-set</span><span class="sxs-lookup"><span data-stu-id="e14b9-324">Create your omsagent daemon-set by running ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

2. <span data-ttu-id="e14b9-325">請確認正在執行 OMS Agent DaemonSet，類似下列的 toohello 該 hello:</span><span class="sxs-lookup"><span data-stu-id="e14b9-325">Verify that hello OMS Agent DaemonSet is running, similar toohello following:</span></span>

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


<span data-ttu-id="e14b9-326">Kubernetes，使用指令碼 toogenerate hello 密碼 yaml 檔案中的工作區識別碼及主要金鑰的內容。</span><span class="sxs-lookup"><span data-stu-id="e14b9-326">For Kubernetes, use a script toogenerate hello secrets yaml file for Workspace ID and Primary Key.</span></span> <span data-ttu-id="e14b9-327">下列範例與 hello 的資訊的使用 hello [omsagent yaml 檔案](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml)toosecure 您的機密資訊。</span><span class="sxs-lookup"><span data-stu-id="e14b9-327">Use hello following example information with hello [omsagent yaml file](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure your secret information.</span></span>

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

## <a name="windows-container-hosts"></a><span data-ttu-id="e14b9-328">Windows 容器主機</span><span class="sxs-lookup"><span data-stu-id="e14b9-328">Windows container hosts</span></span>

### <a name="preparation-before-installing-windows-agents"></a><span data-ttu-id="e14b9-329">安裝 Windows 代理程式之前的準備動作</span><span class="sxs-lookup"><span data-stu-id="e14b9-329">Preparation before installing Windows agents</span></span>

<span data-ttu-id="e14b9-330">您在執行 Windows 的電腦上安裝代理程式之前，您會需要 tooconfigure hello Docker 服務。</span><span class="sxs-lookup"><span data-stu-id="e14b9-330">Before you install agents on computers running Windows, you need tooconfigure hello Docker service.</span></span> <span data-ttu-id="e14b9-331">hello 組態可讓您 hello Windows 代理程式 」 或 「 hello 記錄分析的虛擬機器擴充功能 toouse hello Docker TCP 通訊端以便 hello 代理程式可以從遠端存取 hello Docker 精靈和 toocapture 資料監視。</span><span class="sxs-lookup"><span data-stu-id="e14b9-331">hello configuration allows hello Windows agent or hello Log Analytics virtual machine extension toouse hello Docker TCP socket so that hello agents can access hello Docker daemon remotely and toocapture data for monitoring.</span></span>

#### <a name="toostart-docker-and-verify-its-configuration"></a><span data-ttu-id="e14b9-332">toostart Docker 並確認其組態</span><span class="sxs-lookup"><span data-stu-id="e14b9-332">toostart Docker and verify its configuration</span></span>

<span data-ttu-id="e14b9-333">沒有所需的步驟 tooset 向上 TCP Windows Server 的具名管道：</span><span class="sxs-lookup"><span data-stu-id="e14b9-333">There are steps needed tooset up TCP named pipe for Windows Server:</span></span>

1. <span data-ttu-id="e14b9-334">在 Windows PowerShell 中啟用 TCP 管道和具名的管道。</span><span class="sxs-lookup"><span data-stu-id="e14b9-334">In Windows PowerShell, enable TCP pipe and named pipe.</span></span>

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. <span data-ttu-id="e14b9-335">使用 TCP 管道 hello 組態檔來設定 Docker 及具名管道。</span><span class="sxs-lookup"><span data-stu-id="e14b9-335">Configure Docker with hello configuration file for TCP pipe and named pipe.</span></span> <span data-ttu-id="e14b9-336">hello 設定檔是位於 C:\ProgramData\docker\config\daemon.json。</span><span class="sxs-lookup"><span data-stu-id="e14b9-336">hello configuration file is located at C:\ProgramData\docker\config\daemon.json.</span></span>

    <span data-ttu-id="e14b9-337">在 hello daemon.json 檔案中，您需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="e14b9-337">In hello daemon.json file, you will need hello following:</span></span>

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

<span data-ttu-id="e14b9-338">如需搭配 Windows 容器的 hello Docker 精靈設定的詳細資訊，請參閱[Windows 上的 Docker 引擎](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon)。</span><span class="sxs-lookup"><span data-stu-id="e14b9-338">For more information about hello Docker daemon configuration used with Windows Containers, see [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span></span>


### <a name="install-windows-agents"></a><span data-ttu-id="e14b9-339">安裝 Windows 代理程式</span><span class="sxs-lookup"><span data-stu-id="e14b9-339">Install Windows agents</span></span>

<span data-ttu-id="e14b9-340">tooenable Windows 和 HYPER-V 容器監視，請容器主機的 Windows 電腦上安裝 hello Microsoft Monitoring Agent (MMA)。</span><span class="sxs-lookup"><span data-stu-id="e14b9-340">tooenable Windows and Hyper-V container monitoring, install hello Microsoft Monitoring Agent (MMA) on Windows computers that are container hosts.</span></span> <span data-ttu-id="e14b9-341">在內部部署環境中執行 Windows 的電腦，請參閱[連接的 Windows 電腦 tooLog 分析](log-analytics-windows-agents.md)。</span><span class="sxs-lookup"><span data-stu-id="e14b9-341">For computers running Windows in your on-premises environment, see [Connect Windows computers tooLog Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="e14b9-342">虛擬機器的執行在 Azure 中，將它們連接 tooLog 分析使用 hello[虛擬機器擴充功能](log-analytics-azure-vm-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="e14b9-342">For virtual machines running in Azure, connect them tooLog Analytics using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="e14b9-343">您可以監視 Service Fabric 上執行的 Windows 容器。</span><span class="sxs-lookup"><span data-stu-id="e14b9-343">You can monitor Windows containers running on Service Fabric.</span></span> <span data-ttu-id="e14b9-344">不過，Service Fabric 目前只支援 [Azure 中執行的虛擬機器](log-analytics-azure-vm-extension.md)和[在內部部署環境中執行 Windows 的電腦](log-analytics-windows-agents.md)。</span><span class="sxs-lookup"><span data-stu-id="e14b9-344">However, only [virtual machines running in Azure](log-analytics-azure-vm-extension.md) and [computers running Windows in your on-premises environment](log-analytics-windows-agents.md) are currently supported for Service Fabric.</span></span>

<span data-ttu-id="e14b9-345">您可以確認該 hello 容器監視解決方案會針對 Windows 設定正確。</span><span class="sxs-lookup"><span data-stu-id="e14b9-345">You can verify that hello Container Monitoring solution is set correctly for Windows.</span></span> <span data-ttu-id="e14b9-346">toocheck hello 管理組件正常運作，是下載尋找*ContainerManagement.xxx*。</span><span class="sxs-lookup"><span data-stu-id="e14b9-346">toocheck whether hello management pack was download properly, look for *ContainerManagement.xxx*.</span></span> <span data-ttu-id="e14b9-347">hello 檔案應該在 hello C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs 資料夾。</span><span class="sxs-lookup"><span data-stu-id="e14b9-347">hello files should be in hello C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs folder.</span></span>


## <a name="solution-components"></a><span data-ttu-id="e14b9-348">方案元件</span><span class="sxs-lookup"><span data-stu-id="e14b9-348">Solution components</span></span>

<span data-ttu-id="e14b9-349">如果您使用 Windows 代理程式，然後 hello 下列管理組件是每部電腦上安裝代理程式時將方案加入。</span><span class="sxs-lookup"><span data-stu-id="e14b9-349">If you are using Windows agents, then hello following management pack is installed on each computer with an agent when you add this solution.</span></span> <span data-ttu-id="e14b9-350">不不需要 hello 管理組件的任何設定或維護。</span><span class="sxs-lookup"><span data-stu-id="e14b9-350">No configuration or maintenance is required for hello management pack.</span></span>

- <span data-ttu-id="e14b9-351">C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs 中所安裝的 ContainerManagement.xxx</span><span class="sxs-lookup"><span data-stu-id="e14b9-351">*ContainerManagement.xxx* installed in C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span></span>

## <a name="container-data-collection-details"></a><span data-ttu-id="e14b9-352">容器資料收集詳細資料</span><span class="sxs-lookup"><span data-stu-id="e14b9-352">Container data collection details</span></span>
<span data-ttu-id="e14b9-353">hello 容器監視解決方案會從容器主機和容器，使用您所啟用的代理程式收集各種效能度量和記錄資料。</span><span class="sxs-lookup"><span data-stu-id="e14b9-353">hello Container Monitoring solution collects various performance metrics and log data from container hosts and containers using agents that you enable.</span></span>

<span data-ttu-id="e14b9-354">資料會收集下列代理程式類型的 hello 每隔三分鐘。</span><span class="sxs-lookup"><span data-stu-id="e14b9-354">Data is collected every three minutes by hello following agent types.</span></span>

- [<span data-ttu-id="e14b9-355">OMS Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="e14b9-355">OMS Agent for Linux</span></span>](log-analytics-linux-agents.md)
- [<span data-ttu-id="e14b9-356">Windows 代理程式</span><span class="sxs-lookup"><span data-stu-id="e14b9-356">Windows agent</span></span>](log-analytics-windows-agents.md)
- [<span data-ttu-id="e14b9-357">Log Analytics VM 延伸模組</span><span class="sxs-lookup"><span data-stu-id="e14b9-357">Log Analytics VM extension</span></span>](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a><span data-ttu-id="e14b9-358">容器資料列</span><span class="sxs-lookup"><span data-stu-id="e14b9-358">Container records</span></span>

<span data-ttu-id="e14b9-359">hello 下表顯示 hello 容器監視解決方案和會出現在記錄搜尋結果中的 hello 資料型別所收集的記錄的範例。</span><span class="sxs-lookup"><span data-stu-id="e14b9-359">hello following table shows examples of records collected by hello Container Monitoring solution and hello data types that appear in log search results.</span></span>

| <span data-ttu-id="e14b9-360">資料類型</span><span class="sxs-lookup"><span data-stu-id="e14b9-360">Data type</span></span> | <span data-ttu-id="e14b9-361">記錄檔搜尋中的資料類型</span><span class="sxs-lookup"><span data-stu-id="e14b9-361">Data type in Log Search</span></span> | <span data-ttu-id="e14b9-362">欄位</span><span class="sxs-lookup"><span data-stu-id="e14b9-362">Fields</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e14b9-363">主機和容器的效能</span><span class="sxs-lookup"><span data-stu-id="e14b9-363">Performance for hosts and containers</span></span> | `Type=Perf` | <span data-ttu-id="e14b9-364">Computer、ObjectName、CounterName &#40;%Processor Time、Disk Reads MB、Disk Writes MB、Memory Usage MB、Network Receive Bytes、Network Send Bytes、Processor Usage sec、Network&#41;、CounterValue、TimeGenerated、CounterPath、SourceSystem</span><span class="sxs-lookup"><span data-stu-id="e14b9-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span></span> |
| <span data-ttu-id="e14b9-365">容器清查</span><span class="sxs-lookup"><span data-stu-id="e14b9-365">Container inventory</span></span> | `Type=ContainerInventory` | <span data-ttu-id="e14b9-366">TimeGenerated、Computer、container name、ContainerHostname、Image、ImageTag、ContainerState、ExitCode、EnvironmentVar、Command、CreatedTime、StartedTime、FinishedTime、SourceSystem、ContainerID、ImageID</span><span class="sxs-lookup"><span data-stu-id="e14b9-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span></span> |
| <span data-ttu-id="e14b9-367">容器映像清查</span><span class="sxs-lookup"><span data-stu-id="e14b9-367">Container image inventory</span></span> | `Type=ContainerImageInventory` | <span data-ttu-id="e14b9-368">TimeGenerated、Computer、Image、ImageTag、ImageSize、VirtualSize、Running、Paused、Stopped、Failed、SourceSystem、ImageID、TotalContainer</span><span class="sxs-lookup"><span data-stu-id="e14b9-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span></span> |
| <span data-ttu-id="e14b9-369">容器記錄檔</span><span class="sxs-lookup"><span data-stu-id="e14b9-369">Container log</span></span> | `Type=ContainerLog` | <span data-ttu-id="e14b9-370">TimeGenerated、Computer、image ID、container name、LogEntrySource、LogEntry、SourceSystem、ContainerID</span><span class="sxs-lookup"><span data-stu-id="e14b9-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="e14b9-371">容器服務記錄檔</span><span class="sxs-lookup"><span data-stu-id="e14b9-371">Container service log</span></span> | `Type=ContainerServiceLog`  | <span data-ttu-id="e14b9-372">TimeGenerated、Computer、TimeOfCommand、Image、Command、SourceSystem、ContainerID</span><span class="sxs-lookup"><span data-stu-id="e14b9-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="e14b9-373">容器節點清查</span><span class="sxs-lookup"><span data-stu-id="e14b9-373">Container node inventory</span></span> | `Type=ContainerNodeInventory_CL`| <span data-ttu-id="e14b9-374">TimeGenerated、Computer、ClassName_s、DockerVersion_s、OperatingSystem_s、Volume_s、Network_s、NodeRole_s、OrchestratorType_s、InstanceID_g、SourceSystem</span><span class="sxs-lookup"><span data-stu-id="e14b9-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span></span>|
| <span data-ttu-id="e14b9-375">Kubernetes 清查</span><span class="sxs-lookup"><span data-stu-id="e14b9-375">Kubernetes inventory</span></span> | `Type=KubePodInventory_CL` | <span data-ttu-id="e14b9-376">TimeGenerated、Computer、PodLabel_deployment_s、PodLabel_deploymentconfig_s、PodLabel_docker_registry_s、Name_s、Namespace_s、PodStatus_s、PodIp_s、PodUid_g、PodCreationTimeStamp_t、SourceSystem</span><span class="sxs-lookup"><span data-stu-id="e14b9-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span></span> |
| <span data-ttu-id="e14b9-377">容器流程</span><span class="sxs-lookup"><span data-stu-id="e14b9-377">Container process</span></span> | `Type=ContainerProcess_CL` | <span data-ttu-id="e14b9-378">TimeGenerated、Computer、Pod_s、Namespace_s、ClassName_s、InstanceID_s、Uid_s、PID_s、PPID_s、C_s、STIME_s、Tty_s、TIME_s、Cmd_s、Id_s、Name_s、SourceSystem</span><span class="sxs-lookup"><span data-stu-id="e14b9-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span></span> |
| <span data-ttu-id="e14b9-379">Kubernetes 事件</span><span class="sxs-lookup"><span data-stu-id="e14b9-379">Kubernetes events</span></span> | `Type=KubeEvents_CL` | <span data-ttu-id="e14b9-380">TimeGenerated、Computer、Name_s、ObjectKind_s、Namespace_s、Reason_s、Type_s、SourceComponent_s、SourceSystem、Message</span><span class="sxs-lookup"><span data-stu-id="e14b9-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span></span> |

<span data-ttu-id="e14b9-381">標籤太附加*PodLabel*資料型別是您自己的自訂標籤。</span><span class="sxs-lookup"><span data-stu-id="e14b9-381">Labels appended too*PodLabel* data types are your own custom labels.</span></span> <span data-ttu-id="e14b9-382">hello hello 表所示的附加的 PodLabel 標籤是範例。</span><span class="sxs-lookup"><span data-stu-id="e14b9-382">hello appended PodLabel labels shown in hello table are examples.</span></span> <span data-ttu-id="e14b9-383">因此，`PodLabel_deployment_s`、`PodLabel_deploymentconfig_s`、`PodLabel_docker_registry_s` 在環境的資料集中會有所不同，且一般而言會類似 `PodLabel_yourlabel_s`。</span><span class="sxs-lookup"><span data-stu-id="e14b9-383">So, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` will differ in your environment's data set and generically resemble `PodLabel_yourlabel_s`.</span></span>


## <a name="monitor-containers"></a><span data-ttu-id="e14b9-384">監視容器</span><span class="sxs-lookup"><span data-stu-id="e14b9-384">Monitor containers</span></span>
<span data-ttu-id="e14b9-385">您已啟用 hello OMS 入口網站中的 hello 方案之後，hello**容器**磚會顯示您的容器主機和 hello 容器主機中執行的摘要資訊。</span><span class="sxs-lookup"><span data-stu-id="e14b9-385">After you have hello solution enabled in hello OMS portal, hello **Containers** tile shows summary information about your container hosts and hello containers running in hosts.</span></span>

![容器圖格](./media/log-analytics-containers/containers-title.png)

<span data-ttu-id="e14b9-387">hello 磚會顯示您有多少容器的概觀 hello 環境中失敗之是否正在執行或已停止。</span><span class="sxs-lookup"><span data-stu-id="e14b9-387">hello tile shows an overview of how many containers you have in hello environment and whether they're failed, running, or stopped.</span></span>

### <a name="using-hello-containers-dashboard"></a><span data-ttu-id="e14b9-388">使用 hello 容器儀表板</span><span class="sxs-lookup"><span data-stu-id="e14b9-388">Using hello Containers dashboard</span></span>
<span data-ttu-id="e14b9-389">按一下 hello**容器**磚。</span><span class="sxs-lookup"><span data-stu-id="e14b9-389">Click hello **Containers** tile.</span></span> <span data-ttu-id="e14b9-390">在這裡，您會看到依下列各項組織的檢視︰</span><span class="sxs-lookup"><span data-stu-id="e14b9-390">From there you'll see views organized by:</span></span>

- <span data-ttu-id="e14b9-391">**容器事件** - 會顯示容器狀態和包含失敗容器的電腦。</span><span class="sxs-lookup"><span data-stu-id="e14b9-391">**Container Events** - Shows container status and computers with failed containers.</span></span>
- <span data-ttu-id="e14b9-392">**容器的記錄檔**-顯示以 hello 高數目的記錄檔產生一段時間和的電腦清單的容器記錄檔的圖表。</span><span class="sxs-lookup"><span data-stu-id="e14b9-392">**Container Logs** - Shows a chart of container log files generated over time and a list of computers with hello highest number of log files.</span></span>
- <span data-ttu-id="e14b9-393">**Kubernetes 事件**-顯示 Kubernetes 產生的事件時間和的 hello 原因為何 pod 產生 hello 事件清單的圖表。</span><span class="sxs-lookup"><span data-stu-id="e14b9-393">**Kubernetes Events** - Shows a chart of Kubernetes events generated over time and a list of hello reasons why pods generated hello events.</span></span> <span data-ttu-id="e14b9-394">只有在 Linux 環境中才會使用此資料集。</span><span class="sxs-lookup"><span data-stu-id="e14b9-394">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="e14b9-395">**Kubernetes 命名空間清查**-顯示命名空間和 pod 的 hello 數目，並顯示其階層。</span><span class="sxs-lookup"><span data-stu-id="e14b9-395">**Kubernetes Namespace Inventory** - Shows hello number of namespaces and pods and shows their hierarchy.</span></span> <span data-ttu-id="e14b9-396">只有在 Linux 環境中才會使用此資料集。</span><span class="sxs-lookup"><span data-stu-id="e14b9-396">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="e14b9-397">**容器節點清查**-顯示 hello 數目的容器節點主機上使用的協調流程類型。</span><span class="sxs-lookup"><span data-stu-id="e14b9-397">**Container Node Inventory** - Shows hello number of orchestration types used on container nodes/hosts.</span></span> <span data-ttu-id="e14b9-398">節點主機方式 hello 電腦也會列出由 hello 數目的容器。</span><span class="sxs-lookup"><span data-stu-id="e14b9-398">hello computer nodes/hosts are also listed by hello number of containers.</span></span> <span data-ttu-id="e14b9-399">只有在 Linux 環境中才會使用此資料集。</span><span class="sxs-lookup"><span data-stu-id="e14b9-399">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="e14b9-400">**容器映像庫存**-顯示 hello 總數使用容器映像和映像類型數目。</span><span class="sxs-lookup"><span data-stu-id="e14b9-400">**Container Images Inventory** - Shows hello total number of container images used and number of image types.</span></span> <span data-ttu-id="e14b9-401">映像的 hello 數目也會列出由 hello 影像標記。</span><span class="sxs-lookup"><span data-stu-id="e14b9-401">hello number of images are also listed by hello image tag.</span></span>
- <span data-ttu-id="e14b9-402">**容器狀態**-顯示 hello 總數容器具有執行中的容器節點/主機電腦。</span><span class="sxs-lookup"><span data-stu-id="e14b9-402">**Containers Status** - Shows hello total number of container nodes/host computers that have running containers.</span></span> <span data-ttu-id="e14b9-403">由主機執行中的 hello 數目也會列出電腦。</span><span class="sxs-lookup"><span data-stu-id="e14b9-403">Computers are also listed by hello number of running hosts.</span></span>
- <span data-ttu-id="e14b9-404">**容器流程** - 會顯示一段時間執行的容器流程折線圖。</span><span class="sxs-lookup"><span data-stu-id="e14b9-404">**Container Process** - Shows a line chart of container processes running over time.</span></span> <span data-ttu-id="e14b9-405">還會依容器內的執行命令/流程列出容器。</span><span class="sxs-lookup"><span data-stu-id="e14b9-405">Containers are also listed by running command/process within containers.</span></span> <span data-ttu-id="e14b9-406">只有在 Linux 環境中才會使用此資料集。</span><span class="sxs-lookup"><span data-stu-id="e14b9-406">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="e14b9-407">**容器的 CPU 效能**-顯示經過一段時間的電腦節點主控 hello 平均 CPU 使用率的折線圖。</span><span class="sxs-lookup"><span data-stu-id="e14b9-407">**Container CPU Performance** - Shows a line chart of hello average CPU utilization over time for computer nodes/hosts.</span></span> <span data-ttu-id="e14b9-408">也列出 hello 電腦節點/主控根據平均 CPU 使用率。</span><span class="sxs-lookup"><span data-stu-id="e14b9-408">Also lists hello computer nodes/hosts based on average CPU utilization.</span></span>
- <span data-ttu-id="e14b9-409">**容器記憶體效能** - 會顯示一段時間的記憶體使用量折線圖。</span><span class="sxs-lookup"><span data-stu-id="e14b9-409">**Container Memory Performance** - Shows a line chart of memory usage over time.</span></span> <span data-ttu-id="e14b9-410">還會以執行個體名稱作為基礎列出電腦記憶體使用率。</span><span class="sxs-lookup"><span data-stu-id="e14b9-410">Also lists computer memory utilization based on instance name.</span></span>
- <span data-ttu-id="e14b9-411">**電腦效能**-顯示一段時間的一段時間和可用磁碟空間的 mb 記憶體使用量的百分比 hello %的 CPU 效能隨著時間的折線圖。</span><span class="sxs-lookup"><span data-stu-id="e14b9-411">**Computer Performance** - Shows line charts of hello percent of CPU performance over time, percent of memory usage over time, and megabytes of free disk space over time.</span></span> <span data-ttu-id="e14b9-412">您可以將滑鼠停留在任何列中圖表 tooview 更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e14b9-412">You can hover over any line in a chart tooview more details.</span></span>


<span data-ttu-id="e14b9-413">Hello 儀表板的每個區域是收集的資料執行搜尋的視覺表示法。</span><span class="sxs-lookup"><span data-stu-id="e14b9-413">Each area of hello dashboard is a visual representation of a search that is run on collected data.</span></span>

![容器儀表板](./media/log-analytics-containers/containers-dash01.png)

![容器儀表板](./media/log-analytics-containers/containers-dash02.png)

<span data-ttu-id="e14b9-416">在 hello**容器狀態**區域中，按一下 hello 最上層區域中，如下所示。</span><span class="sxs-lookup"><span data-stu-id="e14b9-416">In hello **Container Status** area, click hello top area, as shown below.</span></span>

![容器狀態](./media/log-analytics-containers/containers-status.png)

<span data-ttu-id="e14b9-418">此時會開啟 記錄搜尋，顯示 hello 狀態，您的容器的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e14b9-418">Log Search opens, displaying information about hello state of your containers.</span></span>

![容器的記錄檔搜尋](./media/log-analytics-containers/containers-log-search.png)

<span data-ttu-id="e14b9-420">您可以從這裡編輯 hello 搜尋查詢 toomodify 它您感興趣的 toofind hello 特定資訊。</span><span class="sxs-lookup"><span data-stu-id="e14b9-420">From here, you can edit hello search query toomodify it toofind hello specific information you're interested in.</span></span> <span data-ttu-id="e14b9-421">如需記錄檔搜尋的詳細資訊，請參閱 [Log Analytics 中的記錄檔搜尋](log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="e14b9-421">For more information about Log Searches, see [Log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

## <a name="troubleshoot-by-finding-a-failed-container"></a><span data-ttu-id="e14b9-422">尋找失敗的容器以進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="e14b9-422">Troubleshoot by finding a failed container</span></span>

<span data-ttu-id="e14b9-423">如果容器已透過非零結束代碼結束，則 Log Analytics 會將容器標示為 [失敗]。</span><span class="sxs-lookup"><span data-stu-id="e14b9-423">Log Analytics marks a container as **Failed** if it has exited with a non-zero exit code.</span></span> <span data-ttu-id="e14b9-424">您可以看到的 hello 錯誤或失敗發生在 hello hello 環境概觀**失敗容器**區域。</span><span class="sxs-lookup"><span data-stu-id="e14b9-424">You can see an overview of hello errors and failures in hello environment in hello **Failed Containers** area.</span></span>

### <a name="toofind-failed-containers"></a><span data-ttu-id="e14b9-425">失敗的 toofind 容器</span><span class="sxs-lookup"><span data-stu-id="e14b9-425">toofind failed containers</span></span>
1. <span data-ttu-id="e14b9-426">按一下 hello**容器狀態**區域。</span><span class="sxs-lookup"><span data-stu-id="e14b9-426">Click hello **Container Status** area.</span></span>  
   <span data-ttu-id="e14b9-427">![容器狀態](./media/log-analytics-containers/containers-status.png)</span><span class="sxs-lookup"><span data-stu-id="e14b9-427">![containers status](./media/log-analytics-containers/containers-status.png)</span></span>
2. <span data-ttu-id="e14b9-428">記錄搜尋會開啟，並顯示 hello 狀態的程式的容器，類似下列的 toohello。</span><span class="sxs-lookup"><span data-stu-id="e14b9-428">Log Search opens and displays hello state of your containers, similar toohello following.</span></span>  
   ![容器狀態](./media/log-analytics-containers/containers-log-search.png)
3. <span data-ttu-id="e14b9-430">接下來，按一下失敗的容器 tooview 更多資訊 hello 的彙總資料值。</span><span class="sxs-lookup"><span data-stu-id="e14b9-430">Next, click hello aggregated value of failed containers tooview additional information.</span></span> <span data-ttu-id="e14b9-431">展開**顯示更多**tooview hello 映像識別碼。</span><span class="sxs-lookup"><span data-stu-id="e14b9-431">Expand **show more** tooview hello image ID.</span></span>  
   <span data-ttu-id="e14b9-432">![失敗的容器](./media/log-analytics-containers/containers-state-failed.png)</span><span class="sxs-lookup"><span data-stu-id="e14b9-432">![failed containers](./media/log-analytics-containers/containers-state-failed.png)</span></span>  
4. <span data-ttu-id="e14b9-433">接著，輸入 hello 下列 hello 搜尋查詢中。</span><span class="sxs-lookup"><span data-stu-id="e14b9-433">Next, type hello following in hello search query.</span></span> <span data-ttu-id="e14b9-434">`Type=ContainerInventory <ImageID>`toosee 詳細資料 hello 映像，例如停止和失敗的映像的映像大小與數目。</span><span class="sxs-lookup"><span data-stu-id="e14b9-434">`Type=ContainerInventory <ImageID>` toosee details about hello image such as image size and number of stopped and failed images.</span></span>  
   <span data-ttu-id="e14b9-435">![失敗的容器](./media/log-analytics-containers/containers-failed04.png)</span><span class="sxs-lookup"><span data-stu-id="e14b9-435">![failed containers](./media/log-analytics-containers/containers-failed04.png)</span></span>

## <a name="search-logs-for-container-data"></a><span data-ttu-id="e14b9-436">搜尋容器資料的記錄檔</span><span class="sxs-lookup"><span data-stu-id="e14b9-436">Search logs for container data</span></span>
<span data-ttu-id="e14b9-437">當您正在排除特定的錯誤時，它可讓的 toosee 發生在您的環境中。</span><span class="sxs-lookup"><span data-stu-id="e14b9-437">When you're troubleshooting a specific error, it can help toosee where it is occurring in your environment.</span></span> <span data-ttu-id="e14b9-438">下列記錄類型的 hello 將協助您建立查詢，您想要的 tooreturn hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="e14b9-438">hello following log types will help you create queries tooreturn hello information you want.</span></span>


- <span data-ttu-id="e14b9-439">**ContainerImageInventory** – 當您嘗試依映像和 tooview 映像資訊，例如映像識別碼或大小 toofind 資訊，請使用此類型。</span><span class="sxs-lookup"><span data-stu-id="e14b9-439">**ContainerImageInventory** – Use this type when you're trying toofind information organized by image and tooview image information such as image IDs or sizes.</span></span>
- <span data-ttu-id="e14b9-440">**ContainerInventory** – 當您需要有關容器位置、其名稱，以及所執行映像的資訊時，請使用這個類型。</span><span class="sxs-lookup"><span data-stu-id="e14b9-440">**ContainerInventory** – Use this type when you want information about container location, what their names are, and what images they're running.</span></span>
- <span data-ttu-id="e14b9-441">**ContainerLog** – 當您想 toofind 特定錯誤記錄檔資訊和項目，請使用這個型別。</span><span class="sxs-lookup"><span data-stu-id="e14b9-441">**ContainerLog** – Use this type when you want toofind specific error log information and entries.</span></span>
- <span data-ttu-id="e14b9-442">**ContainerNodeInventory_CL**此類型要使用 hello/主控件 節點的資訊位於容器的位置。</span><span class="sxs-lookup"><span data-stu-id="e14b9-442">**ContainerNodeInventory_CL**  Use this type when you want hello information about host/node where containers are residing.</span></span> <span data-ttu-id="e14b9-443">它會提供 Docker 版本、協調流程類型、儲存體和網路資訊。</span><span class="sxs-lookup"><span data-stu-id="e14b9-443">It provides you Docker version, orchestration type, storage, and network information.</span></span>
- <span data-ttu-id="e14b9-444">**ContainerProcess_CL**使用這個型別 tooquickly 看到 hello hello 容器內執行的處理程序。</span><span class="sxs-lookup"><span data-stu-id="e14b9-444">**ContainerProcess_CL** Use this type tooquickly see hello process running within hello container.</span></span>
- <span data-ttu-id="e14b9-445">**ContainerServiceLog** – 當您嘗試 toofind 稽核追蹤資訊的 hello Docker 精靈，例如啟動、 停止、 刪除或提取命令使用這個類型。</span><span class="sxs-lookup"><span data-stu-id="e14b9-445">**ContainerServiceLog** – Use this type when you're trying toofind audit trail information for hello Docker daemon, such as start, stop, delete, or pull commands.</span></span>
- <span data-ttu-id="e14b9-446">**KubeEvents_CL**使用這個型別 toosee hello Kubernetes 事件。</span><span class="sxs-lookup"><span data-stu-id="e14b9-446">**KubeEvents_CL**  Use this type toosee hello Kubernetes events.</span></span>
- <span data-ttu-id="e14b9-447">**KubePodInventory_CL**當您想 toounderstand hello 叢集階層資訊，請使用這個型別。</span><span class="sxs-lookup"><span data-stu-id="e14b9-447">**KubePodInventory_CL**  Use this type when you want toounderstand hello cluster hierarchy information.</span></span>


### <a name="toosearch-logs-for-container-data"></a><span data-ttu-id="e14b9-448">toosearch 記錄檔以取得容器資料</span><span class="sxs-lookup"><span data-stu-id="e14b9-448">toosearch logs for container data</span></span>
* <span data-ttu-id="e14b9-449">選擇的映像，您知道最近失敗，並為其尋找 hello 錯誤記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e14b9-449">Choose an image that you know has failed recently and find hello error logs for it.</span></span> <span data-ttu-id="e14b9-450">首先，透過 **ContainerInventory** 搜尋來尋找正在執行該映像的容器名稱。</span><span class="sxs-lookup"><span data-stu-id="e14b9-450">Start by finding a container name that is running that image with a **ContainerInventory** search.</span></span> <span data-ttu-id="e14b9-451">例如，搜尋 `Type=ContainerInventory ubuntu Failed`</span><span class="sxs-lookup"><span data-stu-id="e14b9-451">For example, search for `Type=ContainerInventory ubuntu Failed`</span></span>  
    <span data-ttu-id="e14b9-452">![搜尋 Ubuntu 容器](./media/log-analytics-containers/search-ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="e14b9-452">![Search for Ubuntu containers](./media/log-analytics-containers/search-ubuntu.png)</span></span>

  <span data-ttu-id="e14b9-453">hello hello 容器的名稱旁邊太**名稱**，然後在搜尋這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e14b9-453">hello name of hello container next too**Name**, and search for those logs.</span></span> <span data-ttu-id="e14b9-454">在此範例中為 `Type=ContainerLog cranky_stonebreaker`。</span><span class="sxs-lookup"><span data-stu-id="e14b9-454">In this example, it is `Type=ContainerLog cranky_stonebreaker`.</span></span>

<span data-ttu-id="e14b9-455">**檢視效能資訊**</span><span class="sxs-lookup"><span data-stu-id="e14b9-455">**View performance information**</span></span>

<span data-ttu-id="e14b9-456">當您開始 tooconstruct 查詢時，它可以協助 toosee 是什麼可能第一次。</span><span class="sxs-lookup"><span data-stu-id="e14b9-456">When you're beginning tooconstruct queries, it can help toosee what's possible first.</span></span> <span data-ttu-id="e14b9-457">例如，toosee 所有效能資料，再試一次輸入廣泛查詢 hello 下列都搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="e14b9-457">For example, toosee all performance data, try a broad query by typing hello following search query.</span></span>

```
Type=Perf
```

![容器效能](./media/log-analytics-containers/containers-perf01.png)

<span data-ttu-id="e14b9-459">您可以為範圍 hello 效能資料，您看見 tooa 特定容器輸入 hello 目的 toohello 查詢的權限。</span><span class="sxs-lookup"><span data-stu-id="e14b9-459">You can scope hello performance data you're seeing tooa specific container by typing hello name of it toohello right of your query.</span></span>

```
Type=Perf <containerName>
```

<span data-ttu-id="e14b9-460">顯示 hello 針對個別的容器所收集的效能度量的清單。</span><span class="sxs-lookup"><span data-stu-id="e14b9-460">That shows hello list of performance metrics that are collected for an individual container.</span></span>

![容器效能](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a><span data-ttu-id="e14b9-462">範例記錄檔搜尋查詢</span><span class="sxs-lookup"><span data-stu-id="e14b9-462">Example log search queries</span></span>
<span data-ttu-id="e14b9-463">它通常很有用 toobuild 開頭範例或兩個，然後修改這些 toofit 查詢您的環境。</span><span class="sxs-lookup"><span data-stu-id="e14b9-463">It's often useful toobuild queries starting with an example or two and then modifying them toofit your environment.</span></span> <span data-ttu-id="e14b9-464">做為起點，您可以試驗 hello**查詢範例**區域 toohelp 建置更進階的查詢。</span><span class="sxs-lookup"><span data-stu-id="e14b9-464">As a starting point, you can experiment with hello **Sample Queries** area toohelp you build more advanced queries.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![容器查詢](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a><span data-ttu-id="e14b9-466">儲存記錄檔搜尋查詢</span><span class="sxs-lookup"><span data-stu-id="e14b9-466">Saving log search queries</span></span>
<span data-ttu-id="e14b9-467">儲存查詢是 Log Analytics 的標準功能。</span><span class="sxs-lookup"><span data-stu-id="e14b9-467">Saving queries is a standard feature in Log Analytics.</span></span> <span data-ttu-id="e14b9-468">藉由儲存查詢，您可將您覺得有用的查詢放在容易取得的地方，以便日後使用。</span><span class="sxs-lookup"><span data-stu-id="e14b9-468">By saving them, you'll have those that you've found useful handy for future use.</span></span>

<span data-ttu-id="e14b9-469">您建立查詢，您有幫助之後，按一下以儲存它**我的最愛**hello 頁面頂端的 hello 記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="e14b9-469">After you create a query that you find useful, save it by clicking **Favorites** at hello top of hello Log Search page.</span></span> <span data-ttu-id="e14b9-470">然後您可以輕鬆地存取稍後從 hello**我的儀表板**頁面。</span><span class="sxs-lookup"><span data-stu-id="e14b9-470">Then you can easily access it later from hello **My Dashboard** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e14b9-471">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e14b9-471">Next steps</span></span>
* <span data-ttu-id="e14b9-472">[搜尋記錄](log-analytics-log-searches.md)tooview 詳細容器資料記錄。</span><span class="sxs-lookup"><span data-stu-id="e14b9-472">[Search logs](log-analytics-log-searches.md) tooview detailed container data records.</span></span>

---
title: "快速入門：在 Azure 虛擬機器上手動安裝單一執行個體 SAP HANA | Microsoft Docs"
description: "在 Azure 虛擬機器上手動安裝單一執行個體 SAP HANA 的快速入門指南"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: c51a2a06-6e97-429b-a346-b433a785c9f0
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 05fb31007e1e4c2243f93169129ec5b2c93099e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-manual-installation-of-single-instance-sap-hana-on-azure-vms"></a><span data-ttu-id="c3b2f-103">快速入門：在 Azure VM 上手動安裝單一執行個體 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="c3b2f-103">Quickstart: Manual installation of single-instance SAP HANA on Azure VMs</span></span>
## <a name="introduction"></a><span data-ttu-id="c3b2f-104">簡介</span><span class="sxs-lookup"><span data-stu-id="c3b2f-104">Introduction</span></span>
<span data-ttu-id="c3b2f-105">當您手動安裝 SAP NetWeaver 7.5 和 SAP HANA 1.0 SP12 時，本指南可協助您在 Azure 虛擬機器 (VM) 上設定單一執行個體的 SAP HANA。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-105">This guide helps you set up a single-instance SAP HANA on Azure virtual machines (VMs) when you install SAP NetWeaver 7.5 and SAP HANA 1.0 SP12 manually.</span></span> <span data-ttu-id="c3b2f-106">本指南的重點是在 Azure 上部署 SAP HANA。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-106">The focus of this guide is on deploying SAP HANA on Azure.</span></span> <span data-ttu-id="c3b2f-107">它不會取代 SAP 文件。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-107">It does not replace SAP documentation.</span></span> 

>[!Note]
><span data-ttu-id="c3b2f-108">本指南說明如何將 SAP HANA 部署到 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-108">This guide describes deployments of SAP HANA into Azure VMs.</span></span> <span data-ttu-id="c3b2f-109">如需將 SAP HANA 部署至 HANA 大型執行個體上的資訊，請參閱[在 Azure 虛擬機器 (VM) 上使用 SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/get-started)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-109">For information on deploying SAP HANA into HANA large instances, see [Using SAP on Azure virtual machines (VMs)](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/get-started).</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="c3b2f-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="c3b2f-110">Prerequisites</span></span>
<span data-ttu-id="c3b2f-111">本指南假設您已熟悉如下的這類基礎結構即服務 (IaaS) 基本知識：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-111">This guide assumes that you are familiar with such infrastructure as a service (IaaS) basics as:</span></span>
 * <span data-ttu-id="c3b2f-112">如何透過 Azure 入口網站或 PowerShell 部署虛擬機器或虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-112">How to deploy virtual machines or virtual networks via the Azure portal or PowerShell.</span></span>
 * <span data-ttu-id="c3b2f-113">Azure 跨平台命令列介面 (CLI)，包括使用 JavaScript 物件通知 (JSON) 範本的選項。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-113">The Azure cross-platform command-line interface (CLI), including the option to use JavaScript Object Notation (JSON) templates.</span></span>

<span data-ttu-id="c3b2f-114">本指南也假設您已熟悉：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-114">This guide also assumes that you are familiar with:</span></span>
* <span data-ttu-id="c3b2f-115">SAP HANA 與 SAP NetWeaver，以及如何加以內部部署安裝。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-115">SAP HANA and SAP NetWeaver and how to install them on-premises.</span></span>
* <span data-ttu-id="c3b2f-116">安裝和操作 SAP HANA，以及在 Azure 上的 SAP 應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-116">Installing and operating SAP HANA and SAP application instances on Azure.</span></span>
* <span data-ttu-id="c3b2f-117">下列概念和程序：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-117">The following concepts and procedures:</span></span>
   * <span data-ttu-id="c3b2f-118">在 Azure 上規劃 SAP 部署，包括 Azure 虛擬網路規劃和 Azure 儲存體使用方式。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-118">Planning for SAP deployment on Azure, including Azure Virtual Network  planning and Azure Storage usage.</span></span> <span data-ttu-id="c3b2f-119">請參閱 [Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/planning-guide)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-119">See [SAP NetWeaver on Azure Virtual Machines (VMs) - Planning and implementation guide](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/planning-guide).</span></span>
   * <span data-ttu-id="c3b2f-120">部署原則及在 Azure 中部署 VM 的方式。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-120">Deployment principles and ways to deploy VMs in Azure.</span></span> <span data-ttu-id="c3b2f-121">請參閱[適用於 SAP 的 Azure 虛擬機器部署](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/deployment-guide)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-121">See [Azure Virtual Machines deployment for SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/deployment-guide).</span></span>
   * <span data-ttu-id="c3b2f-122">Azure 上的 SAP NetWeaver ASCS (ABAP SAP 中央服務)、SCS (SAP 中央服務)，以及 ERS (評估的收貨結算) 高可用性。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-122">High availability for SAP NetWeaver ASCS (ABAP SAP Central Services), SCS (SAP Central Services), and ERS (Evaluated Receipt Settlement) on Azure.</span></span> <span data-ttu-id="c3b2f-123">請參閱 [Azure VM 上的 SAP NetWeaver 高可用性](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-123">See [High availability for SAP NetWeaver on Azure VMs](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide).</span></span>
   * <span data-ttu-id="c3b2f-124">如何運用 Azure 上的 ASCS/SCS 多重 SID 安裝改善效率的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-124">Details on how to improve efficiency in leveraging a multi-SID installation of ASCS/SCS on Azure.</span></span> <span data-ttu-id="c3b2f-125">請參閱[建立 SAP NetWeaver 多 SID 組態](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-multi-sid)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-125">See [Create a SAP NetWeaver multi-SID configuration](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-multi-sid).</span></span> 
   * <span data-ttu-id="c3b2f-126">Azure 中以 Linux 驅動的 VM 作為基礎執行 SAP NetWeaver 的準則。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-126">Principles of running SAP NetWeaver based on Linux-driven VMs in Azure.</span></span> <span data-ttu-id="c3b2f-127">請參閱[在 Microsoft Azure SUSE Linux VM 上執行 SAP NetWeaver](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/suse-quickstart)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-127">See [Running SAP NetWeaver on Microsoft Azure SUSE Linux VMs](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/suse-quickstart).</span></span> <span data-ttu-id="c3b2f-128">本指南提供 Azure VM 中 Linux 的特定設定，以及如何正確地將 Azure 儲存體磁碟連結至 Linux VM 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-128">This guide provides specific settings for Linux in Azure VMs and details on how to properly attach Azure storage disks to Linux VMs.</span></span>

<span data-ttu-id="c3b2f-129">此時，SAP 僅認證 Azure VM 適用於 SAP HANA 相應增加設定。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-129">At this time, Azure VMs are certified by SAP for SAP HANA scale-up configurations only.</span></span> <span data-ttu-id="c3b2f-130">尚未支援適合 SAP HANA 工作負載的相應放大設定。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-130">Scale-out configurations with SAP HANA workloads are not yet supported.</span></span> <span data-ttu-id="c3b2f-131">針對相應增加組態案例中的 SAP HANA 高可用性，請參閱 [Azure 虛擬機器 (VM) 上 SAP HANA 的高可用性](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-high-availability)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-131">For SAP HANA high availability in cases of scale-up configurations, see [High availability of SAP HANA on Azure virtual machines (VMs)](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-high-availability).</span></span>

<span data-ttu-id="c3b2f-132">如果您想要取得 SAP HANA 執行個體或 S/4HANA，或是在非常快速時間內部署的 BW/4HANA 系統，應該考慮使用 [SAP 雲端應用裝置程式庫](http://cal.sap.com)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-132">If you are seeking to get an SAP HANA instance or S/4HANA, or BW/4HANA system deployed in very fast time, you should consider the usage of [SAP Cloud Appliance Library](http://cal.sap.com).</span></span> <span data-ttu-id="c3b2f-133">例如，您可以在[本指南](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h)中找到在 Azure 上透過 SAP CAL 部署 S/4HANA 系統的相關文件。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-133">You can find documentation about deploying, for example, an S/4HANA system through SAP CAL on Azure in [this guide](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h).</span></span> <span data-ttu-id="c3b2f-134">您只需要具有可以向 SAP 雲端應用裝置程式庫註冊的 Azure 訂用帳戶和 SAP 使用者。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-134">All you need to have is an Azure subscription and an SAP user that can be registered with SAP Cloud Appliance Library.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c3b2f-135">其他資源</span><span class="sxs-lookup"><span data-stu-id="c3b2f-135">Additional resources</span></span>
### <a name="sap-hana-backup"></a><span data-ttu-id="c3b2f-136">SAP HANA 備份</span><span class="sxs-lookup"><span data-stu-id="c3b2f-136">SAP HANA backup</span></span>
<span data-ttu-id="c3b2f-137">如需在 Azure VM 上備份 SAP HANA 資料庫的資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-137">For information on backing up SAP HANA databases on Azure VMs, see:</span></span>
* [<span data-ttu-id="c3b2f-138">Azure 虛擬機器上的 SAP HANA 備份指南</span><span class="sxs-lookup"><span data-stu-id="c3b2f-138">Backup guide for SAP HANA on Azure Virtual Machines</span></span>](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-guide)
* [<span data-ttu-id="c3b2f-139">檔案層級的 SAP HANA Azure 備份</span><span class="sxs-lookup"><span data-stu-id="c3b2f-139">SAP HANA Azure Backup on file level</span></span>](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-file-level)
* [<span data-ttu-id="c3b2f-140">以儲存體快照集為基礎的 SAP HANA 備份</span><span class="sxs-lookup"><span data-stu-id="c3b2f-140">SAP HANA backup based on storage snapshots</span></span>](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-storage-snapshots)

### <a name="sap-cloud-appliance-library"></a><span data-ttu-id="c3b2f-141">SAP 雲端應用裝置程式庫</span><span class="sxs-lookup"><span data-stu-id="c3b2f-141">SAP Cloud Appliance Library</span></span>
<span data-ttu-id="c3b2f-142">如需使用 SAP 雲端應用裝置程式庫部署 S/4HANA 或 BW/4HANA 的資訊，請參閱[在 Microsoft Azure 上部署 SAP S/4HANA 或 BW/4HANA](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-142">For information on using SAP Cloud Appliance Library to deploy S/4HANA or BW/4HANA, see [Deploy SAP S/4HANA or BW/4HANA on Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h).</span></span>

### <a name="sap-hana-supported-operating-systems"></a><span data-ttu-id="c3b2f-143">SAP HANA 支援的作業系統</span><span class="sxs-lookup"><span data-stu-id="c3b2f-143">SAP HANA-supported operating systems</span></span>
<span data-ttu-id="c3b2f-144">如需 SAP HANA 支援作業系統的資訊，請參閱 [SAP 支援附註 #2235581 - SAP HANA︰支援的作業系統](https://launchpad.support.sap.com/#/notes/2235581/E)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-144">For information on SAP HANA-supported operating systems, see [SAP Support Note #2235581 - SAP HANA: Supported Operating Systems](https://launchpad.support.sap.com/#/notes/2235581/E).</span></span> <span data-ttu-id="c3b2f-145">Azure VM 僅支援這些作業系統的其中一部份。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-145">Azure VMs support only a subset of these operating systems.</span></span> <span data-ttu-id="c3b2f-146">支援下列作業系統在 Azure 上部署 SAP HANA︰</span><span class="sxs-lookup"><span data-stu-id="c3b2f-146">The following operating systems are supported to deploy SAP HANA on Azure:</span></span> 

* <span data-ttu-id="c3b2f-147">SUSE Linux Enterprise Server 12.x</span><span class="sxs-lookup"><span data-stu-id="c3b2f-147">SUSE Linux Enterprise Server 12.x</span></span>
* <span data-ttu-id="c3b2f-148">Red Hat Enterprise Linux 7.2</span><span class="sxs-lookup"><span data-stu-id="c3b2f-148">Red Hat Enterprise Linux 7.2</span></span>

<span data-ttu-id="c3b2f-149">如需關於 SAP HANA 和不同 Linux 作業系統的其他 SAP 文件，請參閱：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-149">For additional SAP documentation about SAP HANA and different Linux operating systems, see:</span></span>

* [<span data-ttu-id="c3b2f-150">SAP 支援附註 #171356 - 在 Linux 上的 SAP 軟體︰一般資訊</span><span class="sxs-lookup"><span data-stu-id="c3b2f-150">SAP Support Note #171356 - SAP Software on Linux:  General Information</span></span>](https://launchpad.support.sap.com/#/notes/1984787)
* [<span data-ttu-id="c3b2f-151">SAP 支援附註 #1944799 - SLES 作業系統安裝的 SAP HANA 指南</span><span class="sxs-lookup"><span data-stu-id="c3b2f-151">SAP Support Note #1944799 - SAP HANA Guidelines for SLES Operating System Installation</span></span>](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html)
* [<span data-ttu-id="c3b2f-152">SAP 支援附註 #2205917 - 針對 SLES 12 for SAP 應用程式的 SAP HANA DB 建議作業系統設定</span><span class="sxs-lookup"><span data-stu-id="c3b2f-152">SAP Support Note #2205917 - SAP HANA DB Recommended OS Settings for SLES 12 for SAP Applications</span></span>](https://launchpad.support.sap.com/#/notes/2205917/E)
* [<span data-ttu-id="c3b2f-153">SAP 支援附註 #1984787 - SUSE Linux Enterprise Server 12：安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="c3b2f-153">SAP Support Note #1984787 - SUSE Linux Enterprise Server 12:  Installation Notes</span></span>](https://launchpad.support.sap.com/#/notes/1984787)
* [<span data-ttu-id="c3b2f-154">SAP 支援附註 #1391070 - Linux UUID 解決方案</span><span class="sxs-lookup"><span data-stu-id="c3b2f-154">SAP Support Note #1391070 - Linux UUID Solutions</span></span>](https://launchpad.support.sap.com/#/notes/1391070)
* [<span data-ttu-id="c3b2f-155">SAP 支援附註 #2009879 - 適用於 Red Hat Enterprise Linux (RHEL) 作業系統的 SAP HANA 指南</span><span class="sxs-lookup"><span data-stu-id="c3b2f-155">SAP Support Note #2009879 - SAP HANA Guidelines for Red Hat Enterprise Linux (RHEL) Operating System</span></span>](https://launchpad.support.sap.com/#/notes/2009879)
* [<span data-ttu-id="c3b2f-156">2292690 - SAP HANA DB：適用於 RHEL 7 的建議作業系統設定</span><span class="sxs-lookup"><span data-stu-id="c3b2f-156">2292690 - SAP HANA DB: Recommended OS settings for RHEL 7</span></span>](https://launchpad.support.sap.com/#/notes/2292690/E)

### <a name="sap-monitoring-in-azure"></a><span data-ttu-id="c3b2f-157">Azure 中的 SAP 監視</span><span class="sxs-lookup"><span data-stu-id="c3b2f-157">SAP monitoring in Azure</span></span>
<span data-ttu-id="c3b2f-158">如需 Azure 中之 SAP 監視的相關資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-158">For information about SAP monitoring in Azure, see:</span></span>

* <span data-ttu-id="c3b2f-159">[SAP 附註 2191498](https://launchpad.support.sap.com/#/notes/2191498/E)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-159">[SAP Note 2191498](https://launchpad.support.sap.com/#/notes/2191498/E).</span></span> <span data-ttu-id="c3b2f-160">本附註討論對 Azure 上的 Linux VM 進行 SAP「增強型監視」。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-160">This note discusses SAP "enhanced monitoring" with Linux VMs on Azure.</span></span> 
* <span data-ttu-id="c3b2f-161">[SAP 附註 1102124](https://launchpad.support.sap.com/#/notes/1102124/E)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-161">[SAP Note 1102124](https://launchpad.support.sap.com/#/notes/1102124/E).</span></span> <span data-ttu-id="c3b2f-162">本附註討論 Linux 上之 SAPOSCOL 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-162">This note discusses information about SAPOSCOL on Linux.</span></span> 
* <span data-ttu-id="c3b2f-163">[SAP 附註 2178632](https://launchpad.support.sap.com/#/notes/2178632/E)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-163">[SAP Note 2178632](https://launchpad.support.sap.com/#/notes/2178632/E).</span></span> <span data-ttu-id="c3b2f-164">本附註討論 Microsoft Azure 上的 SAP 主要監視計量。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-164">This note discusses key monitoring metrics for SAP on Microsoft Azure.</span></span>

### <a name="azure-vm-types"></a><span data-ttu-id="c3b2f-165">Azure VM 類型</span><span class="sxs-lookup"><span data-stu-id="c3b2f-165">Azure VM types</span></span>
<span data-ttu-id="c3b2f-166">與 SAP HANA 搭配使用的 Azure VM 類型與SAP 支援的工作負載情節，都記載於 [SAP 認證的 IaaS 平台](https://www.sap.com/dmc/exp/2014-09-02-hana-hardware/enEN/iaas.html)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-166">Azure VM types and SAP-supported workload scenarios used with SAP HANA are documented in [SAP certified IaaS Platforms](https://www.sap.com/dmc/exp/2014-09-02-hana-hardware/enEN/iaas.html).</span></span> 

<span data-ttu-id="c3b2f-167">經過 SAP 認證適用於 SAP NetWeaver 或 S/4HANA 應用程式層級的 Azure VM 類型，記載在 [SAP 附註 1928533 - Azure 上的 SAP 應用程式︰支援的產品和 Azure VM 類型](https://launchpad.support.sap.com/#/notes/1928533/E)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-167">Azure VM types that are certified by SAP for SAP NetWeaver or the S/4HANA application layer are documented in [SAP Note 1928533 - SAP Applications on Azure: Supported Products and Azure VM types](https://launchpad.support.sap.com/#/notes/1928533/E).</span></span>

>[!Note]
><span data-ttu-id="c3b2f-168">只有 Azure Resource Manager 支援 SAP-Linux-Azure 整合，傳統部署模型並不支援。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-168">SAP-Linux-Azure integration is supported only on Azure Resource Manager and not the classic deployment model.</span></span> 

## <a name="manual-installation-of-sap-hana"></a><span data-ttu-id="c3b2f-169">手動安裝 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="c3b2f-169">Manual installation of SAP HANA</span></span>
<span data-ttu-id="c3b2f-170">本指南說明如何在 Azure VM 上，以下列兩種不同方式手動安裝 SAP HANA：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-170">This guide describes how to manually install SAP HANA on Azure VMs in two different ways:</span></span>

* <span data-ttu-id="c3b2f-171">在「安裝資料庫執行個體」步驟的分散式 NetWeaver 安裝過程中使用 SAP 軟體佈建管理員 (SWPM)</span><span class="sxs-lookup"><span data-stu-id="c3b2f-171">By using SAP Software Provisioning Manager (SWPM) as part of a distributed NetWeaver installation in the "install database instance" step</span></span>
* <span data-ttu-id="c3b2f-172">使用 SAP HANA 資料庫生命週期管理員工具 HDBLCM，然後安裝 NetWeaver</span><span class="sxs-lookup"><span data-stu-id="c3b2f-172">By using the SAP HANA database lifecycle manager tool, HDBLCM, and then installing NetWeaver</span></span>

<span data-ttu-id="c3b2f-173">您也可以使用 SWPM 在單一 VM 中安裝所有元件 (SAP HANA、SAP 應用程式伺服器、ASCS 執行個體)，如本 [SAP HANA 部落格通知](https://blogs.saphana.com/2013/12/31/announcement-sap-hana-and-sap-netweaver-as-abap-deployed-on-one-server-is-generally-available/)所述。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-173">You can also use SWPM to install all components (SAP HANA, the SAP application server, and the ASCS instance) in one single VM, as described in this [SAP HANA blog announcement](https://blogs.saphana.com/2013/12/31/announcement-sap-hana-and-sap-netweaver-as-abap-deployed-on-one-server-is-generally-available/).</span></span> <span data-ttu-id="c3b2f-174">這個選項並未於本快速入門指南中說明，但您必須納入考量的問題都一樣。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-174">This option isn't described in this Quickstart guide, but the issues that you must take into consideration are the same.</span></span>

<span data-ttu-id="c3b2f-175">開始安裝之前，建議您先閱讀本指南稍後的＜準備 Azure VM 進行 SAP HANA 手動安裝＞一節。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-175">Before you start an installation, we recommend that you read the "Preparing Azure VMs for manual installation of SAP HANA" section later in this guide.</span></span> <span data-ttu-id="c3b2f-176">當您只使用預設的 Azure VM 設定時，這樣做有助於避免數個可能發生的基本錯誤。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-176">Doing so can help prevent several basic mistakes that might occur when you use only a default Azure VM configuration.</span></span>

## <a name="key-steps-for-sap-hana-installation-when-you-use-sap-swpm"></a><span data-ttu-id="c3b2f-177">當您使用 SAP SWPM 時，SAP HANA 安裝的主要步驟</span><span class="sxs-lookup"><span data-stu-id="c3b2f-177">Key steps for SAP HANA installation when you use SAP SWPM</span></span>
<span data-ttu-id="c3b2f-178">本節會列出當您使用 SAP SWPM 執行分散式 SAP NetWeaver 7.5 安裝時，適用於手動、單一執行個體 SAP HANA 安裝的主要步驟。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-178">This section lists the key steps for a manual, single-instance SAP HANA installation when you use SAP SWPM to perform a distributed SAP NetWeaver 7.5 installation.</span></span> <span data-ttu-id="c3b2f-179">本指南稍後會以螢幕擷取畫面形式更詳細說明個別步驟。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-179">The individual steps are explained in more detail in screenshots later in this guide.</span></span>

1. <span data-ttu-id="c3b2f-180">建立包含這兩個測試 VM 的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-180">Create an Azure virtual network that includes two test VMs.</span></span>
2. <span data-ttu-id="c3b2f-181">根據 Azure Resource Manager 模型，在作業系統上 (在我們的範例中是 SUSE Linux Enterprise Server (SLES) 和 SLES for SAP Applications 12 SP1) 部署兩個 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-181">Deploy the two Azure VMs with operating systems (in our example, SUSE Linux Enterprise Server (SLES) and SLES for SAP Applications 12 SP1), according to the Azure Resource Manager model.</span></span>
3. <span data-ttu-id="c3b2f-182">將兩個 Azure 標準或進階儲存體磁碟連結至應用程式伺服器 VM (例如 75-GB 或 500-GB 的磁碟)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-182">Attach two Azure standard or premium storage disks (for example, 75-GB or 500-GB disks) to the application server VM.</span></span>
4. <span data-ttu-id="c3b2f-183">將進階儲存體連結至 HANA DB 伺服器 VM。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-183">Attach premium storage disks to the HANA DB server VM.</span></span> <span data-ttu-id="c3b2f-184">如需詳細資訊，請參閱本指南稍後的＜磁碟設定＞一節。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-184">For details, see the "Disk setup" section later in this guide.</span></span>
5. <span data-ttu-id="c3b2f-185">根據大小或輸送量需求連接多個磁碟，然後在 VM 內部的 OS 層級，使用邏輯磁碟區管理或多個裝置的系統管理工具 (MDADM) 來建立等量磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-185">Depending on size or throughput requirements, attach multiple disks, and then create striped volumes by using either logical volume management or a multiple-devices administration tool (MDADM) at the OS level inside the VM.</span></span>
6. <span data-ttu-id="c3b2f-186">在連接的磁碟或邏輯磁碟區上建立 XFS 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-186">Create XFS file systems on the attached disks or logical volumes.</span></span>
7. <span data-ttu-id="c3b2f-187">在 OS 層級上掛接新的 XFS 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-187">Mount the new XFS file systems at the OS level.</span></span> <span data-ttu-id="c3b2f-188">將一個檔案系統用於所有 SAP 軟體。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-188">Use one file system for all the SAP software.</span></span> <span data-ttu-id="c3b2f-189">例如，將其他檔案系統用於 /sapmnt 目錄和備份。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-189">Use the other file system for the /sapmnt directory and backups, for example.</span></span> <span data-ttu-id="c3b2f-190">在 SAP HANA DB 伺服器的進階儲存體磁碟上，將 XFS 檔案系統掛接為 /hana 和 /usr/sap。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-190">On the SAP HANA DB server, mount the XFS file systems on the premium storage disks as /hana and /usr/sap.</span></span> <span data-ttu-id="c3b2f-191">您必須執行此程序，才能防止 Linux Azure VM 上不算大的根目錄檔案系統遭到填滿。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-191">This process is necessary to prevent the root file system, which isn't large on Linux Azure VMs, from filling up.</span></span>
8. <span data-ttu-id="c3b2f-192">在 /etc/hosts 檔案中輸入測試 VM 的本機 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-192">Enter the local IP addresses of the test VMs in the /etc/hosts file.</span></span>
9. <span data-ttu-id="c3b2f-193">在 /etc/fstab 檔案中輸入 **nofail** 參數。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-193">Enter the **nofail** parameter in the /etc/fstab file.</span></span>
10. <span data-ttu-id="c3b2f-194">根據您使用的 Linux 作業系統版本，設定 Linux 核心參數。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-194">Set Linux kernel parameters according to the Linux OS release you are using.</span></span> <span data-ttu-id="c3b2f-195">如需詳細資訊，請參閱討論 HANA 的適當 SAP 附註，以及本指南的＜核心參數＞一節。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-195">For more information, see the appropriate SAP notes that discuss HANA and the "Kernel parameters" section in this guide.</span></span>
11. <span data-ttu-id="c3b2f-196">新增交換空間。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-196">Add swap space.</span></span>
12. <span data-ttu-id="c3b2f-197">(選擇性) 在測試 VM 上安裝圖形化桌面。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-197">Optionally, install a graphical desktop on the test VMs.</span></span> <span data-ttu-id="c3b2f-198">否則，請使用遠端 SAPinst 安裝。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-198">Otherwise, use a remote SAPinst installation.</span></span>
13. <span data-ttu-id="c3b2f-199">從 SAP Service Marketplace 下載 SAP 軟體。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-199">Download the SAP software from the SAP Service Marketplace.</span></span>
14. <span data-ttu-id="c3b2f-200">在應用程式伺服器 VM 上安裝 SAP ASCS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-200">Install the SAP ASCS instance on the app server VM.</span></span>
15. <span data-ttu-id="c3b2f-201">使用 NFS，在測試 VM 之間共用 /sapmnt 目錄。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-201">Share the /sapmnt directory among the test VMs by using NFS.</span></span> <span data-ttu-id="c3b2f-202">應用程式伺服器 VM 為 NFS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-202">The application server VM is the NFS server.</span></span>
16. <span data-ttu-id="c3b2f-203">在 DB 伺服器 VM 上，使用 SWPM 來安裝資料庫執行個體 (包括 HANA)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-203">Install the database instance, including HANA, by using SWPM on the DB server VM.</span></span>
17. <span data-ttu-id="c3b2f-204">在應用程式伺服器 VM 上，安裝主要應用程式伺服器 (PAS)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-204">Install the primary application server (PAS) on the application server VM.</span></span>
18. <span data-ttu-id="c3b2f-205">啟動 SAP 管理主控台 (SAP MC)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-205">Start SAP Management Console (SAP MC).</span></span> <span data-ttu-id="c3b2f-206">例如，連線到 SAP GUI 或 HANA Studio。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-206">Connect with SAP GUI or HANA Studio, for example.</span></span>

## <a name="key-steps-for-sap-hana-installation-when-you-use-hdblcm"></a><span data-ttu-id="c3b2f-207">當您使用 HDBLCM 時，SAP HANA 安裝的主要步驟</span><span class="sxs-lookup"><span data-stu-id="c3b2f-207">Key steps for SAP HANA installation when you use HDBLCM</span></span>
<span data-ttu-id="c3b2f-208">本節會列出當您使用 SAP HDBLCM 執行分散式 SAP NetWeaver 7.5 安裝時，適用於手動、單一執行個體 SAP HANA 安裝的主要步驟。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-208">This section lists the key steps for a manual, single-instance SAP HANA installation when you use SAP HDBLCM to perform a distributed SAP NetWeaver 7.5 installation.</span></span> <span data-ttu-id="c3b2f-209">整份指南會以螢幕擷取畫面形式更詳細說明個別步驟。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-209">The individual steps are explained in more detail in screenshots throughout this guide.</span></span>

1. <span data-ttu-id="c3b2f-210">建立包含這兩個測試 VM 的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-210">Create an Azure virtual network that includes two test VMs.</span></span>
2. <span data-ttu-id="c3b2f-211">根據 Azure Resource Manager 模型，在作業系統上 (在我們的範例中是 SLES 和 SLES for SAP Applications 12 SP1) 部署兩個 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-211">Deploy two Azure VMs with operating systems (in our example, SLES and SLES for SAP Applications 12 SP1) according to the Azure Resource Manager model.</span></span>
3. <span data-ttu-id="c3b2f-212">將兩個 Azure 標準或進階儲存體磁碟連結至應用程式伺服器 VM (例如 75-GB 或 500-GB 的磁碟)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-212">Attach two Azure standard or premium storage disks (for example, 75-GB or 500-GB disks) to the app server VM.</span></span>
4. <span data-ttu-id="c3b2f-213">將進階儲存體連結至 HANA DB 伺服器 VM。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-213">Attach premium storage disks to the HANA DB server VM.</span></span> <span data-ttu-id="c3b2f-214">如需詳細資訊，請參閱本指南稍後的＜磁碟設定＞一節。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-214">For details, see the "Disk setup" section later in this guide.</span></span>
5. <span data-ttu-id="c3b2f-215">根據大小或輸送量需求連接多個磁碟，然後在 VM 內部的 OS 層級，使用邏輯磁碟區管理或多個裝置的系統管理工具 (MDADM) 來建立等量磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-215">Depending on size or throughput requirements, attach multiple disks and create striped volumes by using either logical volume management or a multiple-devices administration tool (MDADM) at the OS level inside the VM.</span></span>
6. <span data-ttu-id="c3b2f-216">在連接的磁碟或邏輯磁碟區上建立 XFS 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-216">Create XFS file systems on the attached disks or logical volumes.</span></span>
7. <span data-ttu-id="c3b2f-217">在 OS 層級上掛接新的 XFS 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-217">Mount the new XFS file systems at the OS level.</span></span> <span data-ttu-id="c3b2f-218">將一個檔案系統用於所有 SAP 軟體，並將另一個檔案系統用於 /sapmnt 目錄 (舉例說明) 及備份。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-218">Use one file system for all the SAP software, and use the other one for the /sapmnt directory and backups, for example.</span></span> <span data-ttu-id="c3b2f-219">在 SAP HANA DB 伺服器的進階儲存體磁碟上，將 XFS 檔案系統掛接為 /hana 和 /usr/sap。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-219">On the SAP HANA DB server, mount the XFS file systems on the premium storage disks as /hana and /usr/sap.</span></span> <span data-ttu-id="c3b2f-220">您必須執行此程序，以協助防止 Linux Azure VM 上不算大的根目錄檔案系統遭到填滿。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-220">This process is necessary to help prevent the root file system, which isn't large on Linux Azure VMs, from filling up.</span></span>
8. <span data-ttu-id="c3b2f-221">在 /etc/hosts 檔案中輸入測試 VM 的本機 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-221">Enter the local IP addresses of the test VMs in the /etc/hosts file.</span></span>
9. <span data-ttu-id="c3b2f-222">在 /etc/fstab 檔案中輸入 **nofail** 參數。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-222">Enter the **nofail** parameter in the /etc/fstab file.</span></span>
10. <span data-ttu-id="c3b2f-223">根據您使用的 Linux 作業系統版本，設定核心參數。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-223">Set kernel parameters according to the Linux OS release you are using.</span></span> <span data-ttu-id="c3b2f-224">如需詳細資訊，請參閱討論 HANA 的適當 SAP 附註，以及本指南的＜核心參數＞一節。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-224">For more information, see the appropriate SAP notes that discuss HANA and the "Kernel parameters" section in this guide.</span></span>
11. <span data-ttu-id="c3b2f-225">新增交換空間。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-225">Add swap space.</span></span>
12. <span data-ttu-id="c3b2f-226">(選擇性) 在測試 VM 上安裝圖形化桌面。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-226">Optionally, install a graphical desktop on the test VMs.</span></span> <span data-ttu-id="c3b2f-227">否則，請使用遠端 SAPinst 安裝。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-227">Otherwise, use a remote SAPinst installation.</span></span>
13. <span data-ttu-id="c3b2f-228">從 SAP Service Marketplace 下載 SAP 軟體。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-228">Download the SAP software from the SAP Service Marketplace.</span></span>
14. <span data-ttu-id="c3b2f-229">在 HANA DB 伺服器 VM 上，建立群組識別碼為 1001 的群組 "sapsys"。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-229">Create a group, sapsys, with group ID 1001, on the HANA DB server VM.</span></span>
15. <span data-ttu-id="c3b2f-230">使用 HANA 資料庫生命週期管理員 (HDBLCM)，在 DB 伺服器 VM 上安裝 SAP HANA。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-230">Install SAP HANA on the DB server VM by using HANA Database Lifecycle Manager (HDBLCM).</span></span>
16. <span data-ttu-id="c3b2f-231">在應用程式伺服器 VM 上安裝 SAP ASCS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-231">Install the SAP ASCS instance on the app server VM.</span></span>
17. <span data-ttu-id="c3b2f-232">使用 NFS，在測試 VM 之間共用 /sapmnt 目錄。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-232">Share the /sapmnt directory among the test VMs by using NFS.</span></span> <span data-ttu-id="c3b2f-233">應用程式伺服器 VM 為 NFS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-233">The application server VM is the NFS server.</span></span>
18. <span data-ttu-id="c3b2f-234">在 HANA DB 伺服器 VM 上，使用 SWPM 安裝資料庫執行個體 (包括 HANA)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-234">Install the database instance, including HANA, by using SWPM on the HANA DB server VM.</span></span>
19. <span data-ttu-id="c3b2f-235">在應用程式伺服器 VM 上，安裝主要應用程式伺服器 (PAS)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-235">Install the primary application server (PAS) on the application server VM.</span></span>
20. <span data-ttu-id="c3b2f-236">啟動 SAP MC。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-236">Start SAP MC.</span></span> <span data-ttu-id="c3b2f-237">透過 SAP GUI 或 HANA Studio 連線。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-237">Connect through SAP GUI or HANA Studio.</span></span>

## <a name="preparing-azure-vms-for-a-manual-installation-of-sap-hana"></a><span data-ttu-id="c3b2f-238">準備 Azure VM 以便手動安裝 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="c3b2f-238">Preparing Azure VMs for a manual installation of SAP HANA</span></span>
<span data-ttu-id="c3b2f-239">本節包含下列主題：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-239">This section covers the following topics:</span></span>

* <span data-ttu-id="c3b2f-240">OS 更新</span><span class="sxs-lookup"><span data-stu-id="c3b2f-240">OS updates</span></span>
* <span data-ttu-id="c3b2f-241">磁碟設定</span><span class="sxs-lookup"><span data-stu-id="c3b2f-241">Disk setup</span></span>
* <span data-ttu-id="c3b2f-242">核心參數</span><span class="sxs-lookup"><span data-stu-id="c3b2f-242">Kernel parameters</span></span>
* <span data-ttu-id="c3b2f-243">檔案系統</span><span class="sxs-lookup"><span data-stu-id="c3b2f-243">File systems</span></span>
* <span data-ttu-id="c3b2f-244">/etc/hosts 檔案</span><span class="sxs-lookup"><span data-stu-id="c3b2f-244">The /etc/hosts file</span></span>
* <span data-ttu-id="c3b2f-245">/etc/fstab 檔案</span><span class="sxs-lookup"><span data-stu-id="c3b2f-245">The /etc/fstab file</span></span>

### <a name="os-updates"></a><span data-ttu-id="c3b2f-246">OS 更新</span><span class="sxs-lookup"><span data-stu-id="c3b2f-246">OS updates</span></span>
<span data-ttu-id="c3b2f-247">請先檢查 Linux 作業系統更新和修正程式，然後再安裝其他軟體。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-247">Check for Linux OS updates and fixes before installing additional software.</span></span> <span data-ttu-id="c3b2f-248">安裝修補程式可能讓您避免呼叫支援人員。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-248">By installing a patch, you might be able to avoid a call to the support desk.</span></span>

<span data-ttu-id="c3b2f-249">請確定您是使用︰</span><span class="sxs-lookup"><span data-stu-id="c3b2f-249">Make sure that you are using:</span></span>
* <span data-ttu-id="c3b2f-250">適用於 SAP 應用程式的 SUSE Linux Enterprise Server。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-250">SUSE Linux Enterprise Server for SAP Applications.</span></span>
* <span data-ttu-id="c3b2f-251">適用於 SAP 應用程式的 Red Hat Enterprise Linux 或適用於 SAP HANA 的 Red Hat Enterprise Linux。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-251">Red Hat Enterprise Linux for SAP Applications or Red Hat Enterprise Linux for SAP HANA.</span></span> 

<span data-ttu-id="c3b2f-252">可以透過 Linux 廠商提供的 Linux 訂用帳戶登錄 OS 部署 (如果您還沒這樣做)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-252">If you haven't already, register the OS deployment with your Linux subscription from the Linux vendor.</span></span> <span data-ttu-id="c3b2f-253">請注意，SUSE 具有適用於 SAP 應用程式的 OS 映像，已經包含服務且會自動註冊。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-253">Note that SUSE has OS images for SAP applications that already include services and which are registered automatically.</span></span>

<span data-ttu-id="c3b2f-254">以下是使用 **zypper** 命令檢查 SUSE Linux 可用修補程式的範例：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-254">Here is an example of checking for available patches for SUSE Linux by using the **zypper** command:</span></span>

 `sudo zypper list-patches`

<span data-ttu-id="c3b2f-255">視問題的種類而定，修補程式會依分類和嚴重性歸類。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-255">Depending on the kind of issue, patches are classified by category and severity.</span></span> <span data-ttu-id="c3b2f-256">常用的分類值為：**security (安全性)**、**recommended (建議)**、**optional (選用)**、**feature (功能)**、**document (文件)** 或 **yast**。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-256">Commonly used values for category are: **security**, **recommended**, **optional**, **feature**, **document**, or **yast**.</span></span>
<span data-ttu-id="c3b2f-257">常用的嚴重性值為：**critical (嚴重)**、**important (重要)**、**moderate (中)**、**low (低)** 或 **unspecified (未指定)**。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-257">Commonly used values for severity are: **critical**, **important**, **moderate**, **low**, or **unspecified**.</span></span>

<span data-ttu-id="c3b2f-258">**Zypper** 命令只會尋找已安裝套件所需要的更新。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-258">The **zypper** command looks only for the updates that your installed packages need.</span></span> <span data-ttu-id="c3b2f-259">例如，您可以使用此命令：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-259">For example, you could use this command:</span></span>

`sudo zypper patch  --category=security,recommended --severity=critical,important`

<span data-ttu-id="c3b2f-260">您可以新增 `--dry-run` 參數來測試更新，而不需實際更新系統。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-260">You can add the parameter `--dry-run` to test the update without actually updating the system.</span></span>


### <a name="disk-setup"></a><span data-ttu-id="c3b2f-261">磁碟設定</span><span class="sxs-lookup"><span data-stu-id="c3b2f-261">Disk setup</span></span>
<span data-ttu-id="c3b2f-262">Azure 上 Linux VM 中的根目錄檔案系統有大小限制。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-262">The root file system in a Linux VM on Azure has a size limitation.</span></span> <span data-ttu-id="c3b2f-263">因此，必須將額外的磁碟空間連結至 Azure VM 才能執行 SAP。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-263">Therefore, it's necessary to attach additional disk space to an Azure VM for running SAP.</span></span> <span data-ttu-id="c3b2f-264">若是 SAP 應用程式伺服器 Azure VM，使用 Azure 標準儲存體磁碟的使用量可能就已經夠用。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-264">For SAP application server Azure VMs, the use of Azure standard storage disks might be sufficient.</span></span> <span data-ttu-id="c3b2f-265">不過，若是 SAP HANA DBMS Azure VM，使用 Azure 進階儲存體磁碟用於生產與非生產實作的使用量是必要的。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-265">However, for SAP HANA DBMS Azure VMs, the use of Azure Premium Storage disks for production and non-production implementations is mandatory.</span></span>

<span data-ttu-id="c3b2f-266">根據 [SAP HANA TDI 儲存體需求](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html)，建議使用下列的 Azure 進階儲存體組態︰</span><span class="sxs-lookup"><span data-stu-id="c3b2f-266">Based on the [SAP HANA TDI Storage Requirements](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html), the following Azure Premium Storage configuration is suggested:</span></span> 

| <span data-ttu-id="c3b2f-267">VM SKU</span><span class="sxs-lookup"><span data-stu-id="c3b2f-267">VM SKU</span></span> | <span data-ttu-id="c3b2f-268">RAM</span><span class="sxs-lookup"><span data-stu-id="c3b2f-268">RAM</span></span> |  <span data-ttu-id="c3b2f-269">/hana/data 和 /hana/log</span><span class="sxs-lookup"><span data-stu-id="c3b2f-269">/hana/data and /hana/log</span></span> <br /> <span data-ttu-id="c3b2f-270">與 LVM 或 MDADM 等量</span><span class="sxs-lookup"><span data-stu-id="c3b2f-270">striped with LVM or MDADM</span></span> | <span data-ttu-id="c3b2f-271">HANA/shared</span><span class="sxs-lookup"><span data-stu-id="c3b2f-271">/hana/shared</span></span> | <span data-ttu-id="c3b2f-272">/root volume</span><span class="sxs-lookup"><span data-stu-id="c3b2f-272">/root volume</span></span> | <span data-ttu-id="c3b2f-273">/usr/sap</span><span class="sxs-lookup"><span data-stu-id="c3b2f-273">/usr/sap</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="c3b2f-274">GS5</span><span class="sxs-lookup"><span data-stu-id="c3b2f-274">GS5</span></span> | <span data-ttu-id="c3b2f-275">448 GB</span><span class="sxs-lookup"><span data-stu-id="c3b2f-275">448 GB</span></span> | <span data-ttu-id="c3b2f-276">2 x P30</span><span class="sxs-lookup"><span data-stu-id="c3b2f-276">2 x P30</span></span> | <span data-ttu-id="c3b2f-277">1 x P20</span><span class="sxs-lookup"><span data-stu-id="c3b2f-277">1 x P20</span></span> | <span data-ttu-id="c3b2f-278">1 x P10</span><span class="sxs-lookup"><span data-stu-id="c3b2f-278">1 x P10</span></span> | <span data-ttu-id="c3b2f-279">1 x P10</span><span class="sxs-lookup"><span data-stu-id="c3b2f-279">1 x P10</span></span> | 

<span data-ttu-id="c3b2f-280">在建議的磁碟組態中，HANA 資料磁碟區和記錄磁碟區會放在相同的 Azure 進階儲存體磁碟中，而此種磁碟會與 LVM 或 MDADM 等量。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-280">In the suggested disk configuration, the HANA data volume and log volume are placed on the same set of Azure premium storage disks that are striped with LVM or MDADM.</span></span> <span data-ttu-id="c3b2f-281">不需要定義任何 RAID 備援層級，因為 Azure 進階儲存體基於備援會保留磁碟的三個映像。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-281">It is not necessary to define any RAID redundancy level because Azure Premium Storage keeps three images of the disks for redundancy.</span></span> <span data-ttu-id="c3b2f-282">若要確定您設定足夠的儲存體，請參閱 [SAP HANA TDI 儲存體需求](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html)和 [SAP HANA Server 安裝與更新指南](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-282">To make sure that you configure enough storage, consult the [SAP HANA TDI Storage Requirements](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) and [SAP HANA Server Installation and Update Guide](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm).</span></span> <span data-ttu-id="c3b2f-283">也請考慮不同的 Azure 進階儲存體磁碟的不同虛擬硬碟 (VHD) 輸送量，如 [VM 高效能進階儲存體與受控磁碟](https://docs.microsoft.com/azure/storage/storage-premium-storage)中所述。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-283">Also consider the different virtual hard disk (VHD) throughput volumes of the different Azure premium storage disks as documented in [High-performance Premium Storage and managed disks for VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span></span> 

<span data-ttu-id="c3b2f-284">您可以將額外的進階儲存體磁碟新增至 HANA DBMS VM，用於儲存資料庫或交易記錄備份。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-284">You can add more premium storage disks to the HANA DBMS VMs for storing database or transaction log backups.</span></span>

<span data-ttu-id="c3b2f-285">如需這兩個用於設定等量的主要工具詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-285">For more information about the two main tools used to configure striping, see the following articles:</span></span>

* [<span data-ttu-id="c3b2f-286">在 Linux 上設定軟體 RAID</span><span class="sxs-lookup"><span data-stu-id="c3b2f-286">Configure software RAID on Linux</span></span>](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="c3b2f-287">設定 Azure 中 Linux VM 的 LVM</span><span class="sxs-lookup"><span data-stu-id="c3b2f-287">Configure LVM on a Linux VM in Azure</span></span>](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="c3b2f-288">針對將磁碟連結至執行 Linux 客體 OS 的 Azure VM，如需詳細資訊請參閱[將磁碟新增至 Linux VM](../../linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-288">For more information on attaching disks to Azure VMs running Linux as a guest OS, see [Add a disk to a Linux VM](../../linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="c3b2f-289">Azure 進階儲存體可讓您定義磁碟快取模式。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-289">Azure Premium Storage allows you to define disk caching modes.</span></span> <span data-ttu-id="c3b2f-290">針對存放 /hana/data 和 /hana/log 的等量集，應停用磁碟快取。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-290">For the striped set holding /hana/data and /hana/log, disk caching should be disabled.</span></span> <span data-ttu-id="c3b2f-291">針對其他磁碟區 (磁碟)，快取模式應設為**唯讀**。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-291">For the other volumes (disks), the caching mode should be set to **ReadOnly**.</span></span>

<span data-ttu-id="c3b2f-292">如需詳細資訊，請參閱[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../../../storage/common/storage-premium-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-292">For more information, see [Premium Storage: High-performance storage for Azure Virtual Machine workloads](../../../storage/common/storage-premium-storage.md).</span></span>

<span data-ttu-id="c3b2f-293">若要尋找用於建立 VM 的範例 JSON 範本，請移至 [Azure 快速入門範本 (英文)](https://github.com/Azure/azure-quickstart-templates)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-293">To find sample JSON templates for creating VMs, go to [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="c3b2f-294">vm-simple-sles 範本是基本的範本。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-294">The vm-simple-sles template is a basic template.</span></span> <span data-ttu-id="c3b2f-295">它包含儲存體區段與其他 100 GB 的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-295">It includes a storage section, with an additional 100-GB data disk.</span></span> <span data-ttu-id="c3b2f-296">此範本可用來當做基底。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-296">This template can be used as a base.</span></span> <span data-ttu-id="c3b2f-297">您可以針對特定的組態採用範本。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-297">You can adapt the template to your specific configuration.</span></span>

>[!Note]
><span data-ttu-id="c3b2f-298">請務必使用 UUID 來連結 Azure 儲存體磁碟，如[在 Microsoft Azure SUSE Linux VM 上執行 SAP NetWeaver](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 中所述。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-298">It is important to attach the Azure storage disk by using a UUID as documented in [Running SAP NetWeaver on Microsoft Azure SUSE Linux VMs](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="c3b2f-299">在測試環境中，已將兩個 Azure 標準儲存體磁碟連接至 SAP 應用程式伺服器 VM，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-299">In the test environment, two Azure standard storage disks were attached to the SAP app server VM, as shown in the following screenshot.</span></span> <span data-ttu-id="c3b2f-300">其中一個磁碟用來儲存所有可供安裝的 SAP 軟體 (包括 NetWeaver 7.5、SAP GUI 和 SAP HANA)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-300">One disk stored all the SAP software (including NetWeaver 7.5, SAP GUI, and SAP HANA) for installation.</span></span> <span data-ttu-id="c3b2f-301">第二個磁碟確保有足夠的可用空間可用於其他需求 (例如，備份和測試資料)，以及要在所有屬於同一個 SAP 環境的 VM 之間共用的 /sapmnt 目錄 (也就是 SAP 設定檔)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-301">The second disk ensured that enough free space would be available for additional requirements (for example, backup and test data) and for the /sapmnt directory (that is, SAP profiles) to be shared among all VMs that belong to the same SAP landscape.</span></span>

![SAP HANA 應用程式伺服器的 [磁碟] 視窗，其中顯示兩個資料磁碟及其大小](./media/hana-get-started/image003.jpg)


### <a name="kernel-parameters"></a><span data-ttu-id="c3b2f-303">核心參數</span><span class="sxs-lookup"><span data-stu-id="c3b2f-303">Kernel parameters</span></span>
<span data-ttu-id="c3b2f-304">SAP HANA 需要不屬於標準 Azure 資源庫映像且必須手動設定的特定 Linux 核心設定。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-304">SAP HANA requires specific Linux kernel settings, which are not part of the standard Azure gallery images and must be set manually.</span></span> <span data-ttu-id="c3b2f-305">依據您是使用 SUSE 還是 Red Hat，參數可能不一樣。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-305">Depending on whether you use SUSE or Red Hat, the parameters might be different.</span></span> <span data-ttu-id="c3b2f-306">稍早列出的 SAP 附註中提供關於這些參數的資訊。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-306">The SAP Notes listed earlier give information about those parameters.</span></span> <span data-ttu-id="c3b2f-307">在顯示的螢幕擷取畫面中，使用 SUSE Linux 12 SP1。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-307">In the screenshots shown, SUSE Linux 12 SP1 was used.</span></span> 

<span data-ttu-id="c3b2f-308">SLES for SAP Applications 12 GA 和 SLES for SAP Applications 12 SP1 具有一個可取代舊 **sapconf** 工具的新工具 **tuned-adm**。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-308">SLES for SAP Applications 12 GA and SLES for SAP Applications 12 SP1 have a new tool, **tuned-adm**, that replaces the old **sapconf** tool.</span></span> <span data-ttu-id="c3b2f-309">**tuned-adm** 有特別的 SAP HANA 設定檔可供其使用。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-309">A special SAP HANA profile is available for **tuned-adm**.</span></span> <span data-ttu-id="c3b2f-310">若要針對 SAP HANA 調整系統，請輸入下列內容作為根使用者：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-310">To tune the system for SAP HANA, enter the following as a root user:</span></span>

   `tuned-adm profile sap-hana`

<span data-ttu-id="c3b2f-311">如需有關 **tuned-adm** 的詳細資訊，請參閱[關於 tuned-adm 的 SUSE 文件](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-311">For more information about **tuned-adm**, see the [SUSE documentation about tuned-adm](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip).</span></span>

<span data-ttu-id="c3b2f-312">在下列螢幕擷取畫面中，您可以看到 **tuned-adm** 如何根據必要的 SAP HANA 設定來變更 `transparent_hugepage` 和 `numa_balancing` 值。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-312">In the following screenshot, you can see how **tuned-adm** changed the `transparent_hugepage` and `numa_balancing` values, according to the required SAP HANA settings.</span></span>

![tuned-adm 工具會根據必要的 SAP HANA 設定來變更值](./media/hana-get-started/image005.jpg)

<span data-ttu-id="c3b2f-314">若要永久保留 SAP HANA 核心設定，請在 SLES 12 上使用 **grub2**。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-314">To make the SAP HANA kernel settings permanent, use **grub2** on SLES 12.</span></span> <span data-ttu-id="c3b2f-315">如需 **grub2** 的詳細資訊，請移至 SUSE 文件的[＜組態檔結構＞](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip)一節。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-315">For more information about **grub2**, go to the [Configuration File Structure](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) section of the SUSE documentation.</span></span>

<span data-ttu-id="c3b2f-316">下列螢幕擷取畫面顯示如何在組態檔中變更核心設定，然後使用 **grub2-mkconfig** 進行編譯：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-316">The following screenshot shows how the kernel settings were changed in the configuration file and then compiled by using **grub2-mkconfig**:</span></span>

![在組態檔中變更核心設定，然後使用 grub2-mkconfig 進行編譯](./media/hana-get-started/image006.jpg)

<span data-ttu-id="c3b2f-318">另一個選項是使用 YaST 和 [開機載入器] > [核心參數] 設定來變更這些設定：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-318">Another option is to change the settings by using YaST and the **Boot Loader** > **Kernel Parameters** settings:</span></span>

![YaST 開機載入器中的 [核心參數] 設定索引標籤](./media/hana-get-started/image007.jpg)

### <a name="file-systems"></a><span data-ttu-id="c3b2f-320">檔案系統</span><span class="sxs-lookup"><span data-stu-id="c3b2f-320">File systems</span></span>
<span data-ttu-id="c3b2f-321">下列螢幕擷取畫面顯示兩個檔案系統，這兩者均建立於這兩個連接之 Azure 標準儲存體磁碟上的 SAP 應用程式伺服器 VM 上。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-321">The following screenshot shows two file systems that were created on the SAP app server VM on top of the two attached Azure standard storage disks.</span></span> <span data-ttu-id="c3b2f-322">這兩個檔案系統都屬 XFS 類型，且掛接至 /sapdata 和 /sapsoftware。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-322">Both file systems are of type XFS and are mounted to /sapdata and /sapsoftware.</span></span>

<span data-ttu-id="c3b2f-323">您不一定要使用這種方式來建構檔案系統。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-323">It is not mandatory to structure your file systems in this way.</span></span> <span data-ttu-id="c3b2f-324">您有其他選項可用來建構磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-324">You have other options for structuring the disk space.</span></span> <span data-ttu-id="c3b2f-325">最重要的考量是防止根目錄檔案系統的可用空間用盡。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-325">The most important consideration is to prevent the root file system from running out of free space.</span></span>

![在 SAP 應用程式伺服器 VM 上建立兩個檔案系統](./media/hana-get-started/image008.jpg)

<span data-ttu-id="c3b2f-327">關於 SAP HANA DB VM，在資料庫安裝期間，當您使用 SAPinst (SWPM) 和**標準**安裝選項時，會在 /hana 和 /usr/sap 之下安裝所有東西。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-327">Regarding the SAP HANA DB VM, during a database installation, when you use SAPinst (SWPM) and the **typical** installation option, everything is installed under /hana and /usr/sap.</span></span> <span data-ttu-id="c3b2f-328">SAP HANA 記錄備份的預設位置是在 /usr/sap 之下。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-328">The default location for the SAP HANA log backup is under /usr/sap.</span></span> <span data-ttu-id="c3b2f-329">同樣地，因為必須防止根檔案系統的可用空間用盡，所以在使用 SWPM 安裝 SAP HANA 之前，請先確定 /hana 和 /usr/sap 之下有足夠的可用空間。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-329">Again, because it's important to prevent the root file system from running out of storage space, make sure that there is enough free space under /hana and /usr/sap before you install SAP HANA by using SWPM.</span></span>

<span data-ttu-id="c3b2f-330">如需 SAP HANA 的標準檔案系統配置說明，請參閱 [SAP HANA 伺服器安裝與更新指南 (英文)](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-330">For a description of the standard file-system layout of SAP HANA, see the [SAP HANA Server Installation and Update Guide](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm).</span></span>

![在 SAP 應用程式伺服器 VM 上建立的其他檔案系統](./media/hana-get-started/image009.jpg)

<span data-ttu-id="c3b2f-332">當您在標準 SLES/SLES for SAP Applications 12 Azure 資源庫映像上安裝 SAP NetWeaver 時，會顯示一則指出沒有交換空間的訊息，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-332">When you install SAP NetWeaver on a standard SLES/SLES for SAP Applications 12 Azure gallery image, a message is displayed that says  there is no swap space, as shown in the following screenshot.</span></span> <span data-ttu-id="c3b2f-333">若要關閉此訊息，您可以使用 **dd**、**mkswap** 和 **swapon** 手動新增分頁檔。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-333">To dismiss this message, you can manually add a swap file by using **dd**, **mkswap**, and **swapon**.</span></span> <span data-ttu-id="c3b2f-334">若要了解做法，請在 SUSE 文件的[＜使用 YaST Partitioner＞](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip)一節中搜尋「手動新增分頁檔」。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-334">To learn how, search for "Adding a swap file manually" in the [Using the YaST Partitioner](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) section of the SUSE documentation.</span></span>

<span data-ttu-id="c3b2f-335">另一個選項是使用 Linux VM 代理程式設定交換空間。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-335">Another option is to configure swap space by using the Linux VM agent.</span></span> <span data-ttu-id="c3b2f-336">如需詳細資訊，請參閱 [Azure Linux 代理程式使用者指南](../../linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-336">For more information, see the [Azure Linux Agent User Guide](../../linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

![指出沒有足夠交換空間的快顯訊息](./media/hana-get-started/image010.jpg)


### <a name="the-etchosts-file"></a><span data-ttu-id="c3b2f-338">/etc/hosts 檔案</span><span class="sxs-lookup"><span data-stu-id="c3b2f-338">The /etc/hosts file</span></span>
<span data-ttu-id="c3b2f-339">開始安裝 SAP 前，請確定在 /etc/hosts 檔案中包含 SAP VM 的主機名稱和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-339">Before you start to install SAP, make sure you include the host names and IP addresses of the SAP VMs in the /etc/hosts file.</span></span> <span data-ttu-id="c3b2f-340">在一個 Azure 虛擬網路內部署所有的 SAP VM，然後使用內部 IP 位址，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-340">Deploy all the SAP VMs within one Azure virtual network, and then use the internal IP addresses, as shown here:</span></span>

![SAP VM 的主機名稱和 IP 位址會列於 /etc/hosts 檔案中](./media/hana-get-started/image011.jpg)

### <a name="the-etcfstab-file"></a><span data-ttu-id="c3b2f-342">/etc/fstab 檔案</span><span class="sxs-lookup"><span data-stu-id="c3b2f-342">The /etc/fstab file</span></span>

<span data-ttu-id="c3b2f-343">將 **nofail** 參數新增至 fstab 檔案很實用。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-343">It is helpful to add the **nofail** parameter to the fstab file.</span></span> <span data-ttu-id="c3b2f-344">如此一來，如果磁碟發生錯誤，VM 不會在開機程序中停止回應。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-344">This way, if something goes wrong with the disks, the VM does not hang in the boot process.</span></span> <span data-ttu-id="c3b2f-345">但請記得，可能無法取得額外的磁碟空間，而且程序可能會填滿根目錄檔案系統。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-345">But remember that additional disk space might not be available, and processes might fill up the root file system.</span></span> <span data-ttu-id="c3b2f-346">如果遺失 /hana，SAP HANA 將無法啟動。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-346">If /hana is missing, SAP HANA won't start.</span></span>

![將 nofail 參數新增至 fstab 檔案](./media/hana-get-started/image000c.jpg)

## <a name="graphical-gnome-desktop-on-sles-12sles-for-sap-applications-12"></a><span data-ttu-id="c3b2f-348">SLES 12/SLES for SAP Applications 12 上的圖形化 GNOME 桌面</span><span class="sxs-lookup"><span data-stu-id="c3b2f-348">Graphical GNOME desktop on SLES 12/SLES for SAP Applications 12</span></span>
<span data-ttu-id="c3b2f-349">本節包含下列主題：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-349">This section covers the following topics:</span></span>

* <span data-ttu-id="c3b2f-350">在 xrdp on SLES 12/SLES for SAP Applications 12 上安裝 GNOME 桌面和 xrdp</span><span class="sxs-lookup"><span data-stu-id="c3b2f-350">Installing the GNOME desktop and xrdp on SLES 12/SLES for SAP Applications 12</span></span>
* <span data-ttu-id="c3b2f-351">在 SLES 12/SLES for SAP Applications 12 上使用 Firefox 來執行以 Java 為基礎的 SAP MC</span><span class="sxs-lookup"><span data-stu-id="c3b2f-351">Running Java-based SAP MC by using Firefox on SLES 12/SLES for SAP Applications 12</span></span>

<span data-ttu-id="c3b2f-352">您也可以使用替代項目，例如 Xterminal 或 VNC (不在本指南中說明)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-352">You can also use alternatives such as Xterminal or VNC (not described in this guide).</span></span>

### <a name="installing-the-gnome-desktop-and-xrdp-on-sles-12sles-for-sap-applications-12"></a><span data-ttu-id="c3b2f-353">在 xrdp on SLES 12/SLES for SAP Applications 12 上安裝 GNOME 桌面和 xrdp</span><span class="sxs-lookup"><span data-stu-id="c3b2f-353">Installing the GNOME desktop and xrdp on SLES 12/SLES for SAP Applications 12</span></span>
<span data-ttu-id="c3b2f-354">如果您具備 Windows 背景，就可以輕鬆地在 SAP Linux VM 內，直接使用圖形化桌面來執行 Firefox、SAPinst、SAP GUI、SAP MC 或 HANA Studio，並從 Windows 電腦透過遠端桌面通訊協定 (RDP) 連線到 VM。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-354">If you have a Windows background, you can easily use a graphical desktop directly within the SAP Linux VMs to run Firefox, SAPinst, SAP GUI, SAP MC, or HANA Studio, and connect to the VM through the Remote Desktop Protocol (RDP) from a Windows computer.</span></span> <span data-ttu-id="c3b2f-355">依貴公司關於將圖形化使用者介面新增到以 Linux 為基礎的生產環境與非生產環境系統之原則而定，您將需要在伺服器上安裝 GNOME。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-355">Dependent on your company policies about adding graphical user interfaces to production and non-production Linux based systems, you might want to install GNOME on your server.</span></span> <span data-ttu-id="c3b2f-356">若要在 Azure SLES 12/SLES for SAP Applications 12 VM 上安裝 GNOME 桌面：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-356">To install the GNOME desktop on an Azure SLES 12/SLES for SAP Applications 12 VM:</span></span>

1. <span data-ttu-id="c3b2f-357">輸入下列命令 (例如在 PuTTY 視窗中) 來安裝 GNOME 桌面：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-357">Install the GNOME desktop by entering the following command (for example, in a PuTTY window):</span></span>

   `zypper in -t pattern gnome-basic`

2. <span data-ttu-id="c3b2f-358">安裝 xrdp 以允許透過 RDP 連接到 VM：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-358">Install xrdp to allow a connection to the VM through RDP:</span></span>

   `zypper in xrdp`

3. <span data-ttu-id="c3b2f-359">編輯 /etc/sysconfig/windowmanager，並將預設的視窗管理員設定為 GNOME：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-359">Edit /etc/sysconfig/windowmanager, and set the default window manager to GNOME:</span></span>

   `DEFAULT_WM="gnome"`

4. <span data-ttu-id="c3b2f-360">執行 **chkconfig** 以確保 xrdp 會在重新開機後自動啟動：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-360">Run **chkconfig** to make sure that xrdp starts automatically after a reboot:</span></span>

   `chkconfig -level 3 xrdp on`

5. <span data-ttu-id="c3b2f-361">如果發生 RDP 連線問題，請嘗試重新啟動 (例如，從 PuTTY 視窗)：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-361">If you have an issue with the RDP connection, try to restart (from a PuTTY window, for example):</span></span>

   `/etc/xrdp/xrdp.sh restart`

6. <span data-ttu-id="c3b2f-362">如果上一個步驟中所述的 xrdp 重新啟動無法運作，請檢查 .pid 檔案：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-362">If an xrdp restart mentioned in the previous step doesn't work, check for a .pid file:</span></span>

   `check /var/run` 

   <span data-ttu-id="c3b2f-363">尋找 `xrdp.pid`。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-363">Look for `xrdp.pid`.</span></span> <span data-ttu-id="c3b2f-364">如果找到的話，請將它移除，並嘗試重新啟動。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-364">If you find it, remove it, and try to restart again.</span></span>

### <a name="starting-sap-mc"></a><span data-ttu-id="c3b2f-365">啟動 SAP MC</span><span class="sxs-lookup"><span data-stu-id="c3b2f-365">Starting SAP MC</span></span>
<span data-ttu-id="c3b2f-366">在安裝 GNOME 桌面之後，在 Azure SLES 12/SLES for SAP Applications 12 VM 中執行時，從 Firefox 啟動圖形化以 Linux 為基礎的 SAP MC 可能會因為遺失 Java 瀏覽器外掛程式而顯示錯誤。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-366">After you install the GNOME desktop, starting the graphical Java-based SAP MC from Firefox while running in an Azure SLES 12/SLES for SAP Applications 12 VM might display an error because of the missing Java-browser plug-in.</span></span>

<span data-ttu-id="c3b2f-367">啟動 SAP MC 的 URL 為 `<server>:5<instance_number>13`。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-367">The URL to start the SAP MC is `<server>:5<instance_number>13`.</span></span>

<span data-ttu-id="c3b2f-368">如需詳細資訊，請參閱[啟動 Web 型 SAP 管理主控台 (英文)](https://help.sap.com/saphelp_nwce10/helpdata/en/48/6b7c6178dc4f93e10000000a42189d/frameset.htm)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-368">For more information, see [Starting the Web-Based SAP Management Console](https://help.sap.com/saphelp_nwce10/helpdata/en/48/6b7c6178dc4f93e10000000a42189d/frameset.htm).</span></span>

<span data-ttu-id="c3b2f-369">下列螢幕擷取畫面顯示遺失 Java 瀏覽器外掛程式時所顯示的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-369">The following screenshot shows the error message that is displayed when the Java-browser plug-in is missing:</span></span>

![指出遺失 Java 瀏覽器外掛程式的錯誤訊息](./media/hana-get-started/image013.jpg)

<span data-ttu-id="c3b2f-371">解決這個問題的其中一種方式，是使用 YaST 安裝遺失的外掛程式，如下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-371">One way to solve the problem is to install the missing plug-in by using YaST, as shown in the following screenshot:</span></span>

![使用 YaST 安裝遺失的外掛程式](./media/hana-get-started/image014.jpg)

<span data-ttu-id="c3b2f-373">當您重新輸入 SAP 管理主控台 URL 時，會出現訊息要求您啟用外掛程式：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-373">When you re-enter the SAP Management Console URL, a message appears asking you to activate the plug-in:</span></span>

![要求啟用外掛程式的對話方塊](./media/hana-get-started/image015.jpg)

<span data-ttu-id="c3b2f-375">您可能也會收到關於遺失檔案 (javafx.properties) 的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-375">You might also receive an error message about a missing file, javafx.properties.</span></span> <span data-ttu-id="c3b2f-376">這與「適用於 SAP GUI 7.4 的 Oracle Java 1.8」的需求有關。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-376">This is related to the requirement of Oracle Java 1.8 for SAP GUI 7.4.</span></span> <span data-ttu-id="c3b2f-377">(請參閱 [SAP 附註 2059429](https://launchpad.support.sap.com/#/notes/2059424)。)IBM Java 版本或 SLES/SLES for SAP Applications 12 隨附的 openjdk 套件皆未包含所需的 javafx.properties 檔案。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-377">(See [SAP Note 2059429](https://launchpad.support.sap.com/#/notes/2059424).) Neither the IBM Java version nor the openjdk package delivered with SLES/SLES for SAP Applications 12 includes the needed javafx.properties file.</span></span> <span data-ttu-id="c3b2f-378">解決方案是從 Oracle 下載 Java SE 8。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-378">The solution is to download and install Java SE 8 from Oracle.</span></span>

<span data-ttu-id="c3b2f-379">如需與 OpenSUSE 上 openjdk 類似問題的相關資訊，請參閱討論區對話 [SAPGui 7.4 Java for openSUSE 42.1 Leap](https://scn.sap.com/thread/3908306)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-379">For information about a similar issue with openjdk on openSUSE, see the discussion thread [SAPGui 7.4 Java for openSUSE 42.1 Leap](https://scn.sap.com/thread/3908306).</span></span>

## <a name="manual-installation-of-sap-hana-swpm"></a><span data-ttu-id="c3b2f-380">手動安裝 SAP HANA：SWPM</span><span class="sxs-lookup"><span data-stu-id="c3b2f-380">Manual installation of SAP HANA: SWPM</span></span>
<span data-ttu-id="c3b2f-381">本節中一系列的螢幕擷取畫面顯示當您使用 SWPM (SAPinst) 時，安裝 SAP NetWeaver 7.5 和 SAP HANA SP12 的主要步驟。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-381">The series of screenshots in this section shows the key steps for installing SAP NetWeaver 7.5 and SAP HANA SP12 when you use SWPM (SAPinst).</span></span> <span data-ttu-id="c3b2f-382">在 NetWeaver 7.5 安裝過程中，SWPM 也可將 HANA 資料庫安裝為單一執行個體。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-382">As part of a NetWeaver 7.5 installation, SWPM can also install the HANA database as a single instance.</span></span>

<span data-ttu-id="c3b2f-383">在範例測試環境中，我們只安裝了一部進階商業應用程式程式設計 (ABAP) 應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-383">In a sample test environment, we installed just one Advanced Business Application Programming (ABAP) app server.</span></span> <span data-ttu-id="c3b2f-384">如下列螢幕擷取畫面所示，我們使用了 [分散式系統] 選項，在一個 Azure VM 上安裝 ASCS 和主要應用程式伺服器執行個體，並在另一個 Azure VM 上安裝 SAP HANA 作為資料庫系統。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-384">As shown in the following screenshot, we used the **Distributed System** option to install the ASCS and primary application server instances in one Azure VM and SAP HANA as the database system in another Azure VM.</span></span>

![使用 [分散式系統] 選項安裝 ASCS 和主要應用程式伺服器執行個體](./media/hana-get-started/image012.jpg)

<span data-ttu-id="c3b2f-386">將 ASCS 執行個體安裝於應用程式伺服器 VM 上，並在 SAP 管理主控台 (如下列螢幕擷取畫面所顯示) 中設定為「綠色」之後，必須將包含 SAP 設定檔目錄的 /sapmnt 目錄與 SAP HANA DB 伺服器 VM 共用。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-386">After the ASCS instance is installed on the app server VM and is set to "green" in the SAP Management Console (shown in the following screenshot), the /sapmnt directory (including the SAP profile directory) must be shared with the SAP HANA DB server VM.</span></span> <span data-ttu-id="c3b2f-387">DB 安裝步驟需要存取此資訊。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-387">The DB installation step needs access to this information.</span></span> <span data-ttu-id="c3b2f-388">提供存取的最佳方式是使用可利用 YaST 設定的 NFS。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-388">The best way to provide access is to use NFS, which can be configured by using YaST.</span></span>

![顯示 ASCS 執行個體已安裝於應用程式伺服器 VM 上並設定為「綠色」的 SAP 管理主控台](./media/hana-get-started/image016.jpg)

<span data-ttu-id="c3b2f-390">在應用程式伺服器 VM 上，應透過 NFS 使用 **rw** 和 **no_root_squash** 選項來共用 /sapmnt 目錄。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-390">On the app server VM, the /sapmnt directory should be shared via NFS by using the **rw** and **no_root_squash** options.</span></span> <span data-ttu-id="c3b2f-391">預設值為 **ro** 和 **root_squash**，這可能導致安裝資料庫執行個體時發生問題。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-391">The defaults are **ro** and **root_squash**, which might lead to problems when you install the database instance.</span></span>

![透過 NFS 使用 rw 和 no_root_squash 選項共用 /sapmnt 目錄](./media/hana-get-started/image017b.jpg)

<span data-ttu-id="c3b2f-393">如下列螢幕擷取畫面所示，必須在 SAP HANA DB 伺服器 VM 上使用 **NFS 用戶端** (和 YaST)，來設定應用程式伺服器 VM 中的 /sapmnt 共用。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-393">As the next screenshot shows, the /sapmnt share from the app server VM must be configured on the SAP HANA DB server VM by using **NFS Client** (and YaST).</span></span>

![使用 NFS 用戶端來設定 /sapmnt 共用](./media/hana-get-started/image018b.jpg)

<span data-ttu-id="c3b2f-395">為了如下列螢幕擷取畫面所示執行分散式 NetWeaver 7.5 安裝 (**資料庫執行個體**)，會登入 SAP HANA 資料庫伺服器 VM 並啟動 SWPM。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-395">To perform a distributed NetWeaver 7.5 installation (**Database Instance**), as shown in the following screenshot, sign in to the SAP HANA DB server VM and start SWPM.</span></span>

![登入 SAP HANA DB 伺服器 VM，然後啟動 SWPM，藉以安裝資料庫執行個體](./media/hana-get-started/image019.jpg)

<span data-ttu-id="c3b2f-397">選取**標準**安裝和安裝媒體的路徑之後，請輸入 DB SID、主機名稱、執行個體號碼及 DB 系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-397">After you select **typical** installation and the path to the installation media, enter a DB SID, the host name, the instance number, and the DB system administrator password.</span></span>

![SAP HANA 資料庫系統管理員登入頁面](./media/hana-get-started/image035b.jpg)

<span data-ttu-id="c3b2f-399">輸入 DBACOCKPIT 結構描述的密碼：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-399">Enter the password for the DBACOCKPIT schema:</span></span>

![DBACOCKPIT 結構描述的密碼輸入方塊](./media/hana-get-started/image036b.jpg)

<span data-ttu-id="c3b2f-401">輸入 SAPABAP1 結構描述密碼的問題：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-401">Enter a question for the SAPABAP1 schema password:</span></span>

![輸入 SAPABAP1 結構描述密碼的問題](./media/hana-get-started/image037b.jpg)

<span data-ttu-id="c3b2f-403">完成每個工作之後，就會在 DB 安裝程序的每個階段旁邊顯示綠色核取記號。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-403">After each task is completed, a green check mark is displayed next to each phase of the DB installation process.</span></span> <span data-ttu-id="c3b2f-404">訊息「執行...資料庫執行個體已完成。」隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-404">The message "Execution of ... Database Instance has completed" is displayed.</span></span>

![含有確認訊息的完成工作視窗](./media/hana-get-started/image023.jpg)

<span data-ttu-id="c3b2f-406">安裝成功後，SAP 管理主控台也應該將 DB 執行個體顯示為「綠色」，並顯示完整的 SAP HANA 程序清單 (hdbindexserver、hdbcompileserver 等)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-406">After successful installation, the SAP Management Console should also show the DB instance as "green" and display the full list of SAP HANA processes (hdbindexserver, hdbcompileserver, and so forth).</span></span>

![含有 SAP HANA 程序清單的 SAP 管理主控台視窗](./media/hana-get-started/image024.jpg)

<span data-ttu-id="c3b2f-408">下列螢幕擷取畫面會顯示 SWPM 在 HANA 安裝期間於 /hana/shared 目錄下所建立的部分檔案結構。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-408">The following screenshot shows the parts of the file structure under the /hana/shared directory that SWPM created during the HANA installation.</span></span> <span data-ttu-id="c3b2f-409">因為沒有任何選項可指定不同的路徑，所以請務必在安裝 SAP HANA 之前，使用 SWPM 在 /hana 目錄之下掛接額外的磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-409">Because there is no option to specify a different path, it's important to mount additional disk space under the /hana directory before the SAP HANA installation by using SWPM.</span></span> <span data-ttu-id="c3b2f-410">這可以避免根檔案系統的可用空間不足。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-410">This prevents the root file system from running out of free space.</span></span>

![在 HANA 安裝期間建立 /hana/shared 目錄檔案結構](./media/hana-get-started/image025.jpg)

<span data-ttu-id="c3b2f-412">這個螢幕擷取畫面會顯示 /usr/sap 目錄的檔案結構：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-412">This screenshot shows the file structure of the /usr/sap directory:</span></span>

![/usr/sap 目錄檔案結構](./media/hana-get-started/image026.jpg)

<span data-ttu-id="c3b2f-414">分散式 ABAP 安裝的最後一個步驟，是安裝主要應用程式伺服器執行個體：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-414">The last step of the distributed ABAP installation is to install the primary application server instance:</span></span>

![將主要應用程式伺服器執行個體顯示為最後一個步驟的 ABAP 安裝](./media/hana-get-started/image027b.jpg)

<span data-ttu-id="c3b2f-416">安裝主要應用程式伺服器執行個體和 SAP GUI 之後，使用 **DBA Cockpit** 交易來確認已正確完成 SAP HANA 安裝：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-416">After the primary application server instance and SAP GUI are installed, use the **DBA Cockpit** transaction to confirm that the SAP HANA installation has finished correctly:</span></span>

![確認安裝成功的 DBA Cockpit 視窗](./media/hana-get-started/image028b.jpg)

<span data-ttu-id="c3b2f-418">在最後一個步驟中，您將需要先在 SAP 應用程式伺服器 VM 中安裝 HANA Studio，然後連線至 DB 伺服器 VM 上執行的 SAP HANA 執行個體：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-418">As a final step, you might want to first install HANA Studio in the SAP app server VM, and then connect to the SAP HANA instance that's running on the DB server VM:</span></span>

![在 SAP 應用程式伺服器 VM 中安裝 SAP HANA Studio](./media/hana-get-started/image038b.jpg)

## <a name="manual-installation-of-sap-hana-hdblcm"></a><span data-ttu-id="c3b2f-420">手動安裝 SAP HANA：HDBLCM</span><span class="sxs-lookup"><span data-stu-id="c3b2f-420">Manual installation of SAP HANA: HDBLCM</span></span>
<span data-ttu-id="c3b2f-421">除了使用 SWPM 在分散式安裝過程中安裝 SAP HANA 之外，您還能使用 HDBLCM，先獨立安裝 HANA。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-421">In addition to installing SAP HANA as part of a distributed installation by using SWPM, you can install the HANA standalone first, by using HDBLCM.</span></span> <span data-ttu-id="c3b2f-422">例如，您接著可以安裝 SAP NetWeaver 7.5。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-422">You can then install SAP NetWeaver 7.5, for example.</span></span> <span data-ttu-id="c3b2f-423">本節中的螢幕擷取畫面會顯示此程序的運作方式。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-423">The screenshots in this section show how this process works.</span></span>

<span data-ttu-id="c3b2f-424">如需有關 HANA HDBLCM 工具的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-424">For more information about the HANA HDBLCM tool, see:</span></span>

* [<span data-ttu-id="c3b2f-425">為您的工作選擇正確的 SAP HANA HDBLCM</span><span class="sxs-lookup"><span data-stu-id="c3b2f-425">Choosing the Correct SAP HANA HDBLCM for Your Task</span></span>](https://help.sap.com/saphelp_hanaplatform/helpdata/en/68/5cff570bb745d48c0ab6d50123ca60/content.htm)
* [<span data-ttu-id="c3b2f-426">SAP HANA 生命週期管理工具</span><span class="sxs-lookup"><span data-stu-id="c3b2f-426">SAP HANA Lifecycle Management Tools</span></span>](http://saphanatutorial.com/sap-hana-lifecycle-management-tools/)
* [<span data-ttu-id="c3b2f-427">SAP HANA 伺服器安裝與更新指南</span><span class="sxs-lookup"><span data-stu-id="c3b2f-427">SAP HANA Server Installation and Update Guide</span></span>](http://help.sap.com/hana/SAP_HANA_Server_Installation_Guide_en.pdf)

<span data-ttu-id="c3b2f-428">為了避免 `\<HANA SID\>adm user` (由 HDBLCM 工具建立) 的預設群組識別碼設定發生問題，請在透過 HDBLCM 安裝 SAP HANA 之前，先使用群組識別碼 `1001` 定義名為 `sapsys` 的新群組：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-428">To avoid problems with a default group ID setting for the `\<HANA SID\>adm user` (created by the HDBLCM tool), define a new group called `sapsys` by using group ID `1001` before you install SAP HANA via HDBLCM:</span></span>

![使用群組識別碼 1001 定義的新群組 "sapsys"](./media/hana-get-started/image030.jpg)

<span data-ttu-id="c3b2f-430">當您第一次啟動 HDBLCM 時，會顯示簡易的開始功能表。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-430">When you start HDBLCM the first time, a simple start menu is displayed.</span></span> <span data-ttu-id="c3b2f-431">選取項目 1 [安裝新的系統]，如下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-431">Select item 1, **Install new system**, as shown in the following screenshot:</span></span>

![HDBLCM 開始視窗中的 [安裝新的系統] 選項](./media/hana-get-started/image031.jpg)

<span data-ttu-id="c3b2f-433">下列螢幕擷取畫面顯示您先前選取的所有重要選項。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-433">The following screenshot displays all the key options that you selected previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3b2f-434">針對 HANA 記錄和資料磁碟區命名的目錄以及安裝路徑 (此範例中的 /hana/shared) 不應為根目錄檔案系統的一部分。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-434">Directories that are named for HANA log and data volumes, as well as the installation path (/hana/shared in this sample) and /usr/sap, should not be part of the root file system.</span></span> <span data-ttu-id="c3b2f-435">這些目錄屬於連結至 VM 的 Azure 資料磁碟 (如＜磁碟安裝＞小節中所述)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-435">These directories belong to the Azure data disks that were attached to the VM (described in the "Disk setup" section).</span></span> <span data-ttu-id="c3b2f-436">這個方法有助於避免根檔案系統的空間不足。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-436">This approach helps prevent the root file system from running out of space.</span></span> <span data-ttu-id="c3b2f-437">在下列螢幕擷取畫面中，您可以看到 HANA 系統管理員具有使用者識別碼 `1005`，並且屬於安裝前所定義的 `sapsys` 群組 (識別碼 `1001`)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-437">In the following screenshot, you can see that the HANA system administrator has user ID `1005` and is part of the `sapsys` group (ID `1001`) that was defined before the installation.</span></span>

![先前選取的所有重要 SAP HANA 元件清單](./media/hana-get-started/image032.jpg)

<span data-ttu-id="c3b2f-439">您可以在 /etc/hosts passwd 目錄中檢查`\<HANA SID\>adm user` (下列螢幕擷取畫面中的 `azdadm`) 的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-439">You can check the `\<HANA SID\>adm user` (`azdadm` in the following screenshot) details in the /etc/passwd directory:</span></span>

![HANA \<HANA SID\>adm 使用者詳細資料會列於 /etc/passwd 目錄中](./media/hana-get-started/image033.jpg)

<span data-ttu-id="c3b2f-441">使用 HDBLCM 安裝 SAP HANA 之後，您就能在 SAP HANA Studio 中看見檔案結構，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-441">After you install SAP HANA by using HDBLCM, you can see the file structure in SAP HANA Studio, as shown in the following screenshot.</span></span> <span data-ttu-id="c3b2f-442">尚未提供 SAPABAP1 結構描述 (其中包括所有的 SAP NetWeaver 資料表)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-442">The SAPABAP1 schema, which includes all the SAP NetWeaver tables, isn't available yet.</span></span>

![SAP HANA Studio 中的 SAP HANA 檔案結構](./media/hana-get-started/image034.jpg)

<span data-ttu-id="c3b2f-444">安裝 SAP HANA 之後，就能在其上安裝 SAP NetWeaver。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-444">After you install SAP HANA, you can install SAP NetWeaver on top of it.</span></span> <span data-ttu-id="c3b2f-445">如下列螢幕擷取畫面所示，已使用 SWPM 來將安裝作為分散式安裝執行 (如上一節所述)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-445">As shown in the following screenshot, the installation was performed as a distributed installation by using SWPM (as described in the previous section).</span></span> <span data-ttu-id="c3b2f-446">當您使用 SWPM 安裝資料庫執行個體時，可以使用 HDBLCM 輸入相同的資料 (例如，主機名稱、HANA SID 和執行個體號碼)。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-446">When you install the database instance by using SWPM, you enter the same data by using HDBLCM (for example, host name, HANA SID, and instance number).</span></span> <span data-ttu-id="c3b2f-447">SWPM 接著會使用現有的 HANA 安裝，並加入多個結構描述。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-447">SWPM then uses the existing HANA installation and adds more schemas.</span></span>

![使用 SWPM 執行分散式安裝](./media/hana-get-started/image035b.jpg)

<span data-ttu-id="c3b2f-449">下列螢幕擷取畫面會顯示 SWPM 安裝步驟，您可以在其中輸入 DBACOCKPIT 結構描述的相關資料：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-449">The following screenshot shows the SWPM installation step where you enter data about the DBACOCKPIT schema:</span></span>

![輸入 DBACOCKPIT 結構描述資料的 SWPM 安裝步驟](./media/hana-get-started/image036b.jpg)

<span data-ttu-id="c3b2f-451">輸入 SAPABAP1 結構描述的相關資料：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-451">Enter data about the SAPABAP1 schema:</span></span>

![輸入 SAPABAP1 結構描述的相關資料](./media/hana-get-started/image037b.jpg)

<span data-ttu-id="c3b2f-453">完成 SWPM 資料庫執行個體安裝後，就能在 SAP HANA Studio 中看見 SAPABAP1 結構描述：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-453">After the SWPM database instance installation is completed, you can see the SAPABAP1 schema in SAP HANA Studio:</span></span>

![SAP HANA Studio 中的 SAPABAP1 結構描述](./media/hana-get-started/image038b.jpg)

<span data-ttu-id="c3b2f-455">最後，在完成 SAP 應用程式伺服器和 SAP GUI 安裝後，您就能使用 **DBA Cockpit** 交易來驗證 HANA DB 執行個體：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-455">Finally, after the SAP app server and SAP GUI installations are completed, you can verify the HANA DB instance by using the **DBA Cockpit** transaction:</span></span>

![使用 DBA Cockpit 來交易驗證 HANA DB 執行個體](./media/hana-get-started/image039b.jpg)


## <a name="sap-software-downloads"></a><span data-ttu-id="c3b2f-457">SAP 軟體下載</span><span class="sxs-lookup"><span data-stu-id="c3b2f-457">SAP software downloads</span></span>
<span data-ttu-id="c3b2f-458">您可以從 SAP Service Marketplace 下載軟體，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="c3b2f-458">You can download software from the SAP Service Marketplace, as shown in the following screenshots.</span></span>

<span data-ttu-id="c3b2f-459">下載適用於 Linux/HANA 的 NetWeaver 7.5：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-459">Download NetWeaver 7.5 for Linux/HANA:</span></span>

 ![用於下載 NetWeaver 7.5 的 SAP 服務安裝和升級視窗](./media/hana-get-started/image001.jpg)

<span data-ttu-id="c3b2f-461">下載 HANA SP12 平台版本：</span><span class="sxs-lookup"><span data-stu-id="c3b2f-461">Download HANA SP12 Platform Edition:</span></span>

 ![用於下載 HANA SP12 平台版本的 SAP 服務安裝和升級視窗](./media/hana-get-started/image002.jpg)


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
ms.openlocfilehash: 57b58b8e07379eed5641f5f89d55b38f52c69e44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-manual-installation-of-single-instance-sap-hana-on-azure-vms"></a><span data-ttu-id="590d0-103">快速入門：在 Azure VM 上手動安裝單一執行個體 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="590d0-103">Quickstart: Manual installation of single-instance SAP HANA on Azure VMs</span></span>
## <a name="introduction"></a><span data-ttu-id="590d0-104">簡介</span><span class="sxs-lookup"><span data-stu-id="590d0-104">Introduction</span></span>
<span data-ttu-id="590d0-105">當您手動安裝 SAP NetWeaver 7.5 和 SAP HANA 1.0 SP12 時，本指南可協助您在 Azure 虛擬機器 (VM) 上設定單一執行個體的 SAP HANA。</span><span class="sxs-lookup"><span data-stu-id="590d0-105">This guide helps you set up a single-instance SAP HANA on Azure virtual machines (VMs) when you install SAP NetWeaver 7.5 and SAP HANA 1.0 SP12 manually.</span></span> <span data-ttu-id="590d0-106">本指南的 hello 重點是在部署在 Azure 上 SAP HANA。</span><span class="sxs-lookup"><span data-stu-id="590d0-106">hello focus of this guide is on deploying SAP HANA on Azure.</span></span> <span data-ttu-id="590d0-107">它不會取代 SAP 文件。</span><span class="sxs-lookup"><span data-stu-id="590d0-107">It does not replace SAP documentation.</span></span> 

>[!Note]
><span data-ttu-id="590d0-108">本指南說明如何將 SAP HANA 部署到 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="590d0-108">This guide describes deployments of SAP HANA into Azure VMs.</span></span> <span data-ttu-id="590d0-109">如需將 SAP HANA 部署至 HANA 大型執行個體上的資訊，請參閱[在 Azure 虛擬機器 (VM) 上使用 SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/get-started)。</span><span class="sxs-lookup"><span data-stu-id="590d0-109">For information on deploying SAP HANA into HANA large instances, see [Using SAP on Azure virtual machines (VMs)](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/get-started).</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="590d0-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="590d0-110">Prerequisites</span></span>
<span data-ttu-id="590d0-111">本指南假設您已熟悉如下的這類基礎結構即服務 (IaaS) 基本知識：</span><span class="sxs-lookup"><span data-stu-id="590d0-111">This guide assumes that you are familiar with such infrastructure as a service (IaaS) basics as:</span></span>
 * <span data-ttu-id="590d0-112">如何 toodeploy 虛擬機器或虛擬網路透過 hello Azure 入口網站或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="590d0-112">How toodeploy virtual machines or virtual networks via hello Azure portal or PowerShell.</span></span>
 * <span data-ttu-id="590d0-113">hello Azure 跨平台命令列介面 (CLI)，包括 hello 選項 toouse JavaScript Object Notation (JSON) 範本。</span><span class="sxs-lookup"><span data-stu-id="590d0-113">hello Azure cross-platform command-line interface (CLI), including hello option toouse JavaScript Object Notation (JSON) templates.</span></span>

<span data-ttu-id="590d0-114">本指南也假設您已熟悉：</span><span class="sxs-lookup"><span data-stu-id="590d0-114">This guide also assumes that you are familiar with:</span></span>
* <span data-ttu-id="590d0-115">SAP HANA 及 SAP NetWeaver 和如何 tooinstall 它們在內部部署。</span><span class="sxs-lookup"><span data-stu-id="590d0-115">SAP HANA and SAP NetWeaver and how tooinstall them on-premises.</span></span>
* <span data-ttu-id="590d0-116">安裝和操作 SAP HANA，以及在 Azure 上的 SAP 應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="590d0-116">Installing and operating SAP HANA and SAP application instances on Azure.</span></span>
* <span data-ttu-id="590d0-117">hello 下列概念和程序：</span><span class="sxs-lookup"><span data-stu-id="590d0-117">hello following concepts and procedures:</span></span>
   * <span data-ttu-id="590d0-118">在 Azure 上規劃 SAP 部署，包括 Azure 虛擬網路規劃和 Azure 儲存體使用方式。</span><span class="sxs-lookup"><span data-stu-id="590d0-118">Planning for SAP deployment on Azure, including Azure Virtual Network  planning and Azure Storage usage.</span></span> <span data-ttu-id="590d0-119">請參閱 [Azure 虛擬機器 (VM) 上的 SAP NetWeaver - 規劃和實作指南](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/planning-guide)。</span><span class="sxs-lookup"><span data-stu-id="590d0-119">See [SAP NetWeaver on Azure Virtual Machines (VMs) - Planning and implementation guide](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/planning-guide).</span></span>
   * <span data-ttu-id="590d0-120">部署原則和方式 toodeploy Azure 中的 Vm。</span><span class="sxs-lookup"><span data-stu-id="590d0-120">Deployment principles and ways toodeploy VMs in Azure.</span></span> <span data-ttu-id="590d0-121">請參閱[適用於 SAP 的 Azure 虛擬機器部署](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/deployment-guide)。</span><span class="sxs-lookup"><span data-stu-id="590d0-121">See [Azure Virtual Machines deployment for SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/deployment-guide).</span></span>
   * <span data-ttu-id="590d0-122">Azure 上的 SAP NetWeaver ASCS (ABAP SAP 中央服務)、SCS (SAP 中央服務)，以及 ERS (評估的收貨結算) 高可用性。</span><span class="sxs-lookup"><span data-stu-id="590d0-122">High availability for SAP NetWeaver ASCS (ABAP SAP Central Services), SCS (SAP Central Services), and ERS (Evaluated Receipt Settlement) on Azure.</span></span> <span data-ttu-id="590d0-123">請參閱 [Azure VM 上的 SAP NetWeaver 高可用性](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide)。</span><span class="sxs-lookup"><span data-stu-id="590d0-123">See [High availability for SAP NetWeaver on Azure VMs](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide).</span></span>
   * <span data-ttu-id="590d0-124">有關如何運用 ASCS/SCS 在 Azure 上的多重 SID 安裝 tooimprove 效率。</span><span class="sxs-lookup"><span data-stu-id="590d0-124">Details on how tooimprove efficiency in leveraging a multi-SID installation of ASCS/SCS on Azure.</span></span> <span data-ttu-id="590d0-125">請參閱[建立 SAP NetWeaver 多 SID 組態](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-multi-sid)。</span><span class="sxs-lookup"><span data-stu-id="590d0-125">See [Create a SAP NetWeaver multi-SID configuration](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-multi-sid).</span></span> 
   * <span data-ttu-id="590d0-126">Azure 中以 Linux 驅動的 VM 作為基礎執行 SAP NetWeaver 的準則。</span><span class="sxs-lookup"><span data-stu-id="590d0-126">Principles of running SAP NetWeaver based on Linux-driven VMs in Azure.</span></span> <span data-ttu-id="590d0-127">請參閱[在 Microsoft Azure SUSE Linux VM 上執行 SAP NetWeaver](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/suse-quickstart)。</span><span class="sxs-lookup"><span data-stu-id="590d0-127">See [Running SAP NetWeaver on Microsoft Azure SUSE Linux VMs](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/suse-quickstart).</span></span> <span data-ttu-id="590d0-128">本指南提供在 Azure Vm 和詳細資料中的 Linux 特定設定 tooproperly 將 Azure 儲存體磁碟 tooLinux Vm 的連接。</span><span class="sxs-lookup"><span data-stu-id="590d0-128">This guide provides specific settings for Linux in Azure VMs and details on how tooproperly attach Azure storage disks tooLinux VMs.</span></span>

<span data-ttu-id="590d0-129">此時，SAP 僅認證 Azure VM 適用於 SAP HANA 相應增加設定。</span><span class="sxs-lookup"><span data-stu-id="590d0-129">At this time, Azure VMs are certified by SAP for SAP HANA scale-up configurations only.</span></span> <span data-ttu-id="590d0-130">尚未支援適合 SAP HANA 工作負載的相應放大設定。</span><span class="sxs-lookup"><span data-stu-id="590d0-130">Scale-out configurations with SAP HANA workloads are not yet supported.</span></span> <span data-ttu-id="590d0-131">針對相應增加組態案例中的 SAP HANA 高可用性，請參閱 [Azure 虛擬機器 (VM) 上 SAP HANA 的高可用性](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-high-availability)。</span><span class="sxs-lookup"><span data-stu-id="590d0-131">For SAP HANA high availability in cases of scale-up configurations, see [High availability of SAP HANA on Azure virtual machines (VMs)](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-high-availability).</span></span>

<span data-ttu-id="590d0-132">如果您搜尋 tooget SAP HANA 執行個體或 S/4HANA 或 BW/4HANA 系統部署在非常快速的時間，您應該考慮的 hello 使用量[SAP 雲端應用裝置程式庫](http://cal.sap.com)。</span><span class="sxs-lookup"><span data-stu-id="590d0-132">If you are seeking tooget an SAP HANA instance or S/4HANA, or BW/4HANA system deployed in very fast time, you should consider hello usage of [SAP Cloud Appliance Library](http://cal.sap.com).</span></span> <span data-ttu-id="590d0-133">例如，您可以在[本指南](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h)中找到在 Azure 上透過 SAP CAL 部署 S/4HANA 系統的相關文件。</span><span class="sxs-lookup"><span data-stu-id="590d0-133">You can find documentation about deploying, for example, an S/4HANA system through SAP CAL on Azure in [this guide](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h).</span></span> <span data-ttu-id="590d0-134">您只需要 toohave 是 Azure 訂用帳戶和 SAP 使用者可以向 SAP 雲端應用裝置程式庫。</span><span class="sxs-lookup"><span data-stu-id="590d0-134">All you need toohave is an Azure subscription and an SAP user that can be registered with SAP Cloud Appliance Library.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="590d0-135">其他資源</span><span class="sxs-lookup"><span data-stu-id="590d0-135">Additional resources</span></span>
### <a name="sap-hana-backup"></a><span data-ttu-id="590d0-136">SAP HANA 備份</span><span class="sxs-lookup"><span data-stu-id="590d0-136">SAP HANA backup</span></span>
<span data-ttu-id="590d0-137">如需在 Azure VM 上備份 SAP HANA 資料庫的資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="590d0-137">For information on backing up SAP HANA databases on Azure VMs, see:</span></span>
* [<span data-ttu-id="590d0-138">Azure 虛擬機器上的 SAP HANA 備份指南</span><span class="sxs-lookup"><span data-stu-id="590d0-138">Backup guide for SAP HANA on Azure Virtual Machines</span></span>](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-guide)
* [<span data-ttu-id="590d0-139">檔案層級的 SAP HANA Azure 備份</span><span class="sxs-lookup"><span data-stu-id="590d0-139">SAP HANA Azure Backup on file level</span></span>](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-file-level)
* [<span data-ttu-id="590d0-140">以儲存體快照集為基礎的 SAP HANA 備份</span><span class="sxs-lookup"><span data-stu-id="590d0-140">SAP HANA backup based on storage snapshots</span></span>](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-storage-snapshots)

### <a name="sap-cloud-appliance-library"></a><span data-ttu-id="590d0-141">SAP 雲端應用裝置程式庫</span><span class="sxs-lookup"><span data-stu-id="590d0-141">SAP Cloud Appliance Library</span></span>
<span data-ttu-id="590d0-142">如需使用 SAP 雲端應用裝置程式庫 toodeploy S/4HANA 或 BW/4HANA 資訊，請參閱[部署 SAP S/4HANA 或 Microsoft Azure 上的 BW/4HANA](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h)。</span><span class="sxs-lookup"><span data-stu-id="590d0-142">For information on using SAP Cloud Appliance Library toodeploy S/4HANA or BW/4HANA, see [Deploy SAP S/4HANA or BW/4HANA on Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h).</span></span>

### <a name="sap-hana-supported-operating-systems"></a><span data-ttu-id="590d0-143">SAP HANA 支援的作業系統</span><span class="sxs-lookup"><span data-stu-id="590d0-143">SAP HANA-supported operating systems</span></span>
<span data-ttu-id="590d0-144">如需 SAP HANA 支援作業系統的資訊，請參閱 [SAP 支援附註 #2235581 - SAP HANA︰支援的作業系統](https://launchpad.support.sap.com/#/notes/2235581/E)。</span><span class="sxs-lookup"><span data-stu-id="590d0-144">For information on SAP HANA-supported operating systems, see [SAP Support Note #2235581 - SAP HANA: Supported Operating Systems](https://launchpad.support.sap.com/#/notes/2235581/E).</span></span> <span data-ttu-id="590d0-145">Azure VM 僅支援這些作業系統的其中一部份。</span><span class="sxs-lookup"><span data-stu-id="590d0-145">Azure VMs support only a subset of these operating systems.</span></span> <span data-ttu-id="590d0-146">hello 下列作業系統都支援的 toodeploy 在 Azure 上 SAP HANA:</span><span class="sxs-lookup"><span data-stu-id="590d0-146">hello following operating systems are supported toodeploy SAP HANA on Azure:</span></span> 

* <span data-ttu-id="590d0-147">SUSE Linux Enterprise Server 12.x</span><span class="sxs-lookup"><span data-stu-id="590d0-147">SUSE Linux Enterprise Server 12.x</span></span>
* <span data-ttu-id="590d0-148">Red Hat Enterprise Linux 7.2</span><span class="sxs-lookup"><span data-stu-id="590d0-148">Red Hat Enterprise Linux 7.2</span></span>

<span data-ttu-id="590d0-149">如需關於 SAP HANA 和不同 Linux 作業系統的其他 SAP 文件，請參閱：</span><span class="sxs-lookup"><span data-stu-id="590d0-149">For additional SAP documentation about SAP HANA and different Linux operating systems, see:</span></span>

* [<span data-ttu-id="590d0-150">SAP 支援附註 #171356 - 在 Linux 上的 SAP 軟體︰一般資訊</span><span class="sxs-lookup"><span data-stu-id="590d0-150">SAP Support Note #171356 - SAP Software on Linux:  General Information</span></span>](https://launchpad.support.sap.com/#/notes/1984787)
* [<span data-ttu-id="590d0-151">SAP 支援附註 #1944799 - SLES 作業系統安裝的 SAP HANA 指南</span><span class="sxs-lookup"><span data-stu-id="590d0-151">SAP Support Note #1944799 - SAP HANA Guidelines for SLES Operating System Installation</span></span>](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html)
* [<span data-ttu-id="590d0-152">SAP 支援附註 #2205917 - 針對 SLES 12 for SAP 應用程式的 SAP HANA DB 建議作業系統設定</span><span class="sxs-lookup"><span data-stu-id="590d0-152">SAP Support Note #2205917 - SAP HANA DB Recommended OS Settings for SLES 12 for SAP Applications</span></span>](https://launchpad.support.sap.com/#/notes/2205917/E)
* [<span data-ttu-id="590d0-153">SAP 支援附註 #1984787 - SUSE Linux Enterprise Server 12：安裝注意事項</span><span class="sxs-lookup"><span data-stu-id="590d0-153">SAP Support Note #1984787 - SUSE Linux Enterprise Server 12:  Installation Notes</span></span>](https://launchpad.support.sap.com/#/notes/1984787)
* [<span data-ttu-id="590d0-154">SAP 支援附註 #1391070 - Linux UUID 解決方案</span><span class="sxs-lookup"><span data-stu-id="590d0-154">SAP Support Note #1391070 - Linux UUID Solutions</span></span>](https://launchpad.support.sap.com/#/notes/1391070)
* [<span data-ttu-id="590d0-155">SAP 支援附註 #2009879 - 適用於 Red Hat Enterprise Linux (RHEL) 作業系統的 SAP HANA 指南</span><span class="sxs-lookup"><span data-stu-id="590d0-155">SAP Support Note #2009879 - SAP HANA Guidelines for Red Hat Enterprise Linux (RHEL) Operating System</span></span>](https://launchpad.support.sap.com/#/notes/2009879)
* [<span data-ttu-id="590d0-156">2292690 - SAP HANA DB：適用於 RHEL 7 的建議作業系統設定</span><span class="sxs-lookup"><span data-stu-id="590d0-156">2292690 - SAP HANA DB: Recommended OS settings for RHEL 7</span></span>](https://launchpad.support.sap.com/#/notes/2292690/E)

### <a name="sap-monitoring-in-azure"></a><span data-ttu-id="590d0-157">Azure 中的 SAP 監視</span><span class="sxs-lookup"><span data-stu-id="590d0-157">SAP monitoring in Azure</span></span>
<span data-ttu-id="590d0-158">如需 Azure 中之 SAP 監視的相關資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="590d0-158">For information about SAP monitoring in Azure, see:</span></span>

* <span data-ttu-id="590d0-159">[SAP 附註 2191498](https://launchpad.support.sap.com/#/notes/2191498/E)。</span><span class="sxs-lookup"><span data-stu-id="590d0-159">[SAP Note 2191498](https://launchpad.support.sap.com/#/notes/2191498/E).</span></span> <span data-ttu-id="590d0-160">本附註討論對 Azure 上的 Linux VM 進行 SAP「增強型監視」。</span><span class="sxs-lookup"><span data-stu-id="590d0-160">This note discusses SAP "enhanced monitoring" with Linux VMs on Azure.</span></span> 
* <span data-ttu-id="590d0-161">[SAP 附註 1102124](https://launchpad.support.sap.com/#/notes/1102124/E)。</span><span class="sxs-lookup"><span data-stu-id="590d0-161">[SAP Note 1102124](https://launchpad.support.sap.com/#/notes/1102124/E).</span></span> <span data-ttu-id="590d0-162">本附註討論 Linux 上之 SAPOSCOL 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="590d0-162">This note discusses information about SAPOSCOL on Linux.</span></span> 
* <span data-ttu-id="590d0-163">[SAP 附註 2178632](https://launchpad.support.sap.com/#/notes/2178632/E)。</span><span class="sxs-lookup"><span data-stu-id="590d0-163">[SAP Note 2178632](https://launchpad.support.sap.com/#/notes/2178632/E).</span></span> <span data-ttu-id="590d0-164">本附註討論 Microsoft Azure 上的 SAP 主要監視計量。</span><span class="sxs-lookup"><span data-stu-id="590d0-164">This note discusses key monitoring metrics for SAP on Microsoft Azure.</span></span>

### <a name="azure-vm-types"></a><span data-ttu-id="590d0-165">Azure VM 類型</span><span class="sxs-lookup"><span data-stu-id="590d0-165">Azure VM types</span></span>
<span data-ttu-id="590d0-166">與 SAP HANA 搭配使用的 Azure VM 類型與SAP 支援的工作負載情節，都記載於 [SAP 認證的 IaaS 平台](https://www.sap.com/dmc/exp/2014-09-02-hana-hardware/enEN/iaas.html)。</span><span class="sxs-lookup"><span data-stu-id="590d0-166">Azure VM types and SAP-supported workload scenarios used with SAP HANA are documented in [SAP certified IaaS Platforms](https://www.sap.com/dmc/exp/2014-09-02-hana-hardware/enEN/iaas.html).</span></span> 

<span data-ttu-id="590d0-167">Azure VM 類型經過驗證的 SAP 適用於 SAP NetWeaver 或 hello S/4HANA 應用程式層會記載於[SAP 附註 1928533 Azure 上的 SAP 應用程式： 支援產品與 Azure VM 類型](https://launchpad.support.sap.com/#/notes/1928533/E)。</span><span class="sxs-lookup"><span data-stu-id="590d0-167">Azure VM types that are certified by SAP for SAP NetWeaver or hello S/4HANA application layer are documented in [SAP Note 1928533 - SAP Applications on Azure: Supported Products and Azure VM types](https://launchpad.support.sap.com/#/notes/1928533/E).</span></span>

>[!Note]
><span data-ttu-id="590d0-168">Azure 資源管理員，且 hello 傳統部署模型上才支援 SAP Linux Azure 整合。</span><span class="sxs-lookup"><span data-stu-id="590d0-168">SAP-Linux-Azure integration is supported only on Azure Resource Manager and not hello classic deployment model.</span></span> 

## <a name="manual-installation-of-sap-hana"></a><span data-ttu-id="590d0-169">手動安裝 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="590d0-169">Manual installation of SAP HANA</span></span>
<span data-ttu-id="590d0-170">本指南說明如何 toomanually SAP HANA 上安裝 Azure Vm 中兩個不同的方式：</span><span class="sxs-lookup"><span data-stu-id="590d0-170">This guide describes how toomanually install SAP HANA on Azure VMs in two different ways:</span></span>

* <span data-ttu-id="590d0-171">使用分散式 NetWeaver 安裝在 hello 安裝資料庫執行個體 」 的步驟一部分的 SAP 軟體佈建 Manager (SWPM)</span><span class="sxs-lookup"><span data-stu-id="590d0-171">By using SAP Software Provisioning Manager (SWPM) as part of a distributed NetWeaver installation in hello "install database instance" step</span></span>
* <span data-ttu-id="590d0-172">使用 hello SAP HANA 資料庫生命週期管理員工具 HDBLCM，，然後安裝 NetWeaver</span><span class="sxs-lookup"><span data-stu-id="590d0-172">By using hello SAP HANA database lifecycle manager tool, HDBLCM, and then installing NetWeaver</span></span>

<span data-ttu-id="590d0-173">您也可以使用 SWPM tooinstall 一個的單一 VM 中的所有元件 （SAP HANA、 hello SAP 應用程式伺服器和 hello ASCS 執行個體） 中所述[SAP HANA 部落格通知](https://blogs.saphana.com/2013/12/31/announcement-sap-hana-and-sap-netweaver-as-abap-deployed-on-one-server-is-generally-available/)。</span><span class="sxs-lookup"><span data-stu-id="590d0-173">You can also use SWPM tooinstall all components (SAP HANA, hello SAP application server, and hello ASCS instance) in one single VM, as described in this [SAP HANA blog announcement](https://blogs.saphana.com/2013/12/31/announcement-sap-hana-and-sap-netweaver-as-abap-deployed-on-one-server-is-generally-available/).</span></span> <span data-ttu-id="590d0-174">這個選項不說明本快速入門指南中，但必須納入考量的問題是的 hello hello 相同。</span><span class="sxs-lookup"><span data-stu-id="590d0-174">This option isn't described in this Quickstart guide, but hello issues that you must take into consideration are hello same.</span></span>

<span data-ttu-id="590d0-175">開始安裝之前，我們建議您先閱讀 hello"準備 Azure Vm 的 SAP HANA 的手動安裝 」 一節稍後在本指南。</span><span class="sxs-lookup"><span data-stu-id="590d0-175">Before you start an installation, we recommend that you read hello "Preparing Azure VMs for manual installation of SAP HANA" section later in this guide.</span></span> <span data-ttu-id="590d0-176">當您只使用預設的 Azure VM 設定時，這樣做有助於避免數個可能發生的基本錯誤。</span><span class="sxs-lookup"><span data-stu-id="590d0-176">Doing so can help prevent several basic mistakes that might occur when you use only a default Azure VM configuration.</span></span>

## <a name="key-steps-for-sap-hana-installation-when-you-use-sap-swpm"></a><span data-ttu-id="590d0-177">當您使用 SAP SWPM 時，SAP HANA 安裝的主要步驟</span><span class="sxs-lookup"><span data-stu-id="590d0-177">Key steps for SAP HANA installation when you use SAP SWPM</span></span>
<span data-ttu-id="590d0-178">當您使用 SAP SWPM tooperform 分散式的 SAP NetWeaver 7.5 安裝時，此區段會列出 hello 手動、 單一執行個體的 SAP HANA 安裝的主要步驟。</span><span class="sxs-lookup"><span data-stu-id="590d0-178">This section lists hello key steps for a manual, single-instance SAP HANA installation when you use SAP SWPM tooperform a distributed SAP NetWeaver 7.5 installation.</span></span> <span data-ttu-id="590d0-179">hello 個別步驟的更多詳細資料螢幕擷取畫面，稍後在本指南中說明。</span><span class="sxs-lookup"><span data-stu-id="590d0-179">hello individual steps are explained in more detail in screenshots later in this guide.</span></span>

1. <span data-ttu-id="590d0-180">建立包含這兩個測試 VM 的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="590d0-180">Create an Azure virtual network that includes two test VMs.</span></span>
2. <span data-ttu-id="590d0-181">部署 hello 兩個 Azure Vm 的作業系統 （在本例中，SUSE Linux Enterprise Server (SLES) 和 SAP 應用程式 12 sp1 SLES），根據 toohello Azure 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="590d0-181">Deploy hello two Azure VMs with operating systems (in our example, SUSE Linux Enterprise Server (SLES) and SLES for SAP Applications 12 SP1), according toohello Azure Resource Manager model.</span></span>
3. <span data-ttu-id="590d0-182">附加兩個 Azure 標準或高階儲存體磁碟 （例如，75 GB 或 500 GB 磁碟） toohello 應用程式伺服器 VM。</span><span class="sxs-lookup"><span data-stu-id="590d0-182">Attach two Azure standard or premium storage disks (for example, 75-GB or 500-GB disks) toohello application server VM.</span></span>
4. <span data-ttu-id="590d0-183">附加 premium 儲存體磁碟 toohello HANA DB 伺服器 VM。</span><span class="sxs-lookup"><span data-stu-id="590d0-183">Attach premium storage disks toohello HANA DB server VM.</span></span> <span data-ttu-id="590d0-184">如需詳細資訊，請參閱本指南稍後的 hello 磁碟 < 安裝 > 一節。</span><span class="sxs-lookup"><span data-stu-id="590d0-184">For details, see hello "Disk setup" section later in this guide.</span></span>
5. <span data-ttu-id="590d0-185">根據大小或輸送量需求，附加多個磁碟，然後再建立等量磁碟區在 hello 作業系統層級 hello VM 內使用邏輯磁碟區管理或多個裝置管理工具 (MDADM)。</span><span class="sxs-lookup"><span data-stu-id="590d0-185">Depending on size or throughput requirements, attach multiple disks, and then create striped volumes by using either logical volume management or a multiple-devices administration tool (MDADM) at hello OS level inside hello VM.</span></span>
6. <span data-ttu-id="590d0-186">Hello 附加磁碟或邏輯磁碟區上建立 XFS 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="590d0-186">Create XFS file systems on hello attached disks or logical volumes.</span></span>
7. <span data-ttu-id="590d0-187">掛接 hello 新 XFS 檔案系統 hello 作業系統層級。</span><span class="sxs-lookup"><span data-stu-id="590d0-187">Mount hello new XFS file systems at hello OS level.</span></span> <span data-ttu-id="590d0-188">使用所有的 hello SAP 軟體的一個檔案系統。</span><span class="sxs-lookup"><span data-stu-id="590d0-188">Use one file system for all hello SAP software.</span></span> <span data-ttu-id="590d0-189">使用例如 hello hello /sapmnt 目錄和備份，其他檔案系統。</span><span class="sxs-lookup"><span data-stu-id="590d0-189">Use hello other file system for hello /sapmnt directory and backups, for example.</span></span> <span data-ttu-id="590d0-190">Hello SAP HANA 資料庫在伺服器上，將 hello XFS 檔案系統掛接 /hana 以及 /usr/sap hello 高階儲存體磁碟。</span><span class="sxs-lookup"><span data-stu-id="590d0-190">On hello SAP HANA DB server, mount hello XFS file systems on hello premium storage disks as /hana and /usr/sap.</span></span> <span data-ttu-id="590d0-191">此程序是必要的 tooprevent hello 根檔案系統，這並不是大型 Linux 的 Azure Vm 上填滿。</span><span class="sxs-lookup"><span data-stu-id="590d0-191">This process is necessary tooprevent hello root file system, which isn't large on Linux Azure VMs, from filling up.</span></span>
8. <span data-ttu-id="590d0-192">輸入 hello /etc/hosts hosts 檔案中的 hello 測試 Vm 的 hello 本機 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="590d0-192">Enter hello local IP addresses of hello test VMs in hello /etc/hosts file.</span></span>
9. <span data-ttu-id="590d0-193">輸入 hello **nofail** hello /etc/hosts fstab 檔案中的參數。</span><span class="sxs-lookup"><span data-stu-id="590d0-193">Enter hello **nofail** parameter in hello /etc/fstab file.</span></span>
10. <span data-ttu-id="590d0-194">設定 Linux 核心參數，根據您使用 toohello Linux 作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="590d0-194">Set Linux kernel parameters according toohello Linux OS release you are using.</span></span> <span data-ttu-id="590d0-195">如需詳細資訊，請參閱 hello 適當 SAP 附註會討論 HANA hello 本指南的 < 核心參數 > 一節。</span><span class="sxs-lookup"><span data-stu-id="590d0-195">For more information, see hello appropriate SAP notes that discuss HANA and hello "Kernel parameters" section in this guide.</span></span>
11. <span data-ttu-id="590d0-196">新增交換空間。</span><span class="sxs-lookup"><span data-stu-id="590d0-196">Add swap space.</span></span>
12. <span data-ttu-id="590d0-197">（選擇性） 在 hello 測試 Vm 上安裝圖形化的桌面。</span><span class="sxs-lookup"><span data-stu-id="590d0-197">Optionally, install a graphical desktop on hello test VMs.</span></span> <span data-ttu-id="590d0-198">否則，請使用遠端 SAPinst 安裝。</span><span class="sxs-lookup"><span data-stu-id="590d0-198">Otherwise, use a remote SAPinst installation.</span></span>
13. <span data-ttu-id="590d0-199">從 hello SAP 服務 Marketplace 下載 hello SAP 軟體。</span><span class="sxs-lookup"><span data-stu-id="590d0-199">Download hello SAP software from hello SAP Service Marketplace.</span></span>
14. <span data-ttu-id="590d0-200">Hello 應用程式伺服器 VM 上安裝 hello SAP ASCS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="590d0-200">Install hello SAP ASCS instance on hello app server VM.</span></span>
15. <span data-ttu-id="590d0-201">Hello 之間共用 hello /sapmnt 目錄使用 NFS 測試 Vm。</span><span class="sxs-lookup"><span data-stu-id="590d0-201">Share hello /sapmnt directory among hello test VMs by using NFS.</span></span> <span data-ttu-id="590d0-202">hello NFS 伺服器 hello 應用程式伺服器 VM。</span><span class="sxs-lookup"><span data-stu-id="590d0-202">hello application server VM is hello NFS server.</span></span>
16. <span data-ttu-id="590d0-203">安裝 hello 資料庫執行個體，包括 HANA、 使用 SWPM hello DB 伺服器 VM 上。</span><span class="sxs-lookup"><span data-stu-id="590d0-203">Install hello database instance, including HANA, by using SWPM on hello DB server VM.</span></span>
17. <span data-ttu-id="590d0-204">Hello 應用程式伺服器 VM 上安裝 hello 主應用程式伺服器 (PAS)。</span><span class="sxs-lookup"><span data-stu-id="590d0-204">Install hello primary application server (PAS) on hello application server VM.</span></span>
18. <span data-ttu-id="590d0-205">啟動 SAP 管理主控台 (SAP MC)。</span><span class="sxs-lookup"><span data-stu-id="590d0-205">Start SAP Management Console (SAP MC).</span></span> <span data-ttu-id="590d0-206">例如，連線到 SAP GUI 或 HANA Studio。</span><span class="sxs-lookup"><span data-stu-id="590d0-206">Connect with SAP GUI or HANA Studio, for example.</span></span>

## <a name="key-steps-for-sap-hana-installation-when-you-use-hdblcm"></a><span data-ttu-id="590d0-207">當您使用 HDBLCM 時，SAP HANA 安裝的主要步驟</span><span class="sxs-lookup"><span data-stu-id="590d0-207">Key steps for SAP HANA installation when you use HDBLCM</span></span>
<span data-ttu-id="590d0-208">當您使用 SAP HDBLCM tooperform 分散式的 SAP NetWeaver 7.5 安裝時，此區段會列出 hello 手動、 單一執行個體的 SAP HANA 安裝的主要步驟。</span><span class="sxs-lookup"><span data-stu-id="590d0-208">This section lists hello key steps for a manual, single-instance SAP HANA installation when you use SAP HDBLCM tooperform a distributed SAP NetWeaver 7.5 installation.</span></span> <span data-ttu-id="590d0-209">hello 個別步驟的更多詳細資料螢幕擷取畫面，本指南中說明。</span><span class="sxs-lookup"><span data-stu-id="590d0-209">hello individual steps are explained in more detail in screenshots throughout this guide.</span></span>

1. <span data-ttu-id="590d0-210">建立包含這兩個測試 VM 的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="590d0-210">Create an Azure virtual network that includes two test VMs.</span></span>
2. <span data-ttu-id="590d0-211">將兩個 Azure Vm （在本例中，SLES 和 SLES SAP 應用程式 12 sp1） 作業系統部署，根據 toohello Azure 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="590d0-211">Deploy two Azure VMs with operating systems (in our example, SLES and SLES for SAP Applications 12 SP1) according toohello Azure Resource Manager model.</span></span>
3. <span data-ttu-id="590d0-212">附加兩個 Azure 標準或高階儲存體磁碟 （例如，75 GB 或 500 GB 磁碟） toohello 應用程式伺服器 VM。</span><span class="sxs-lookup"><span data-stu-id="590d0-212">Attach two Azure standard or premium storage disks (for example, 75-GB or 500-GB disks) toohello app server VM.</span></span>
4. <span data-ttu-id="590d0-213">附加 premium 儲存體磁碟 toohello HANA DB 伺服器 VM。</span><span class="sxs-lookup"><span data-stu-id="590d0-213">Attach premium storage disks toohello HANA DB server VM.</span></span> <span data-ttu-id="590d0-214">如需詳細資訊，請參閱本指南稍後的 hello 磁碟 < 安裝 > 一節。</span><span class="sxs-lookup"><span data-stu-id="590d0-214">For details, see hello "Disk setup" section later in this guide.</span></span>
5. <span data-ttu-id="590d0-215">根據大小或輸送量需求，附加多個磁碟，並使用在 hello OS hello VM 內的層級的邏輯磁碟區管理或多個裝置管理工具 (MDADM) 來建立等量磁碟區。</span><span class="sxs-lookup"><span data-stu-id="590d0-215">Depending on size or throughput requirements, attach multiple disks and create striped volumes by using either logical volume management or a multiple-devices administration tool (MDADM) at hello OS level inside hello VM.</span></span>
6. <span data-ttu-id="590d0-216">Hello 附加磁碟或邏輯磁碟區上建立 XFS 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="590d0-216">Create XFS file systems on hello attached disks or logical volumes.</span></span>
7. <span data-ttu-id="590d0-217">掛接 hello 新 XFS 檔案系統 hello 作業系統層級。</span><span class="sxs-lookup"><span data-stu-id="590d0-217">Mount hello new XFS file systems at hello OS level.</span></span> <span data-ttu-id="590d0-218">使用一個檔案系統的所有 hello SAP 軟體，並使用 hello 另一個則用於 hello /sapmnt 目錄和備份，例如。</span><span class="sxs-lookup"><span data-stu-id="590d0-218">Use one file system for all hello SAP software, and use hello other one for hello /sapmnt directory and backups, for example.</span></span> <span data-ttu-id="590d0-219">Hello SAP HANA 資料庫在伺服器上，將 hello XFS 檔案系統掛接 /hana 以及 /usr/sap hello 高階儲存體磁碟。</span><span class="sxs-lookup"><span data-stu-id="590d0-219">On hello SAP HANA DB server, mount hello XFS file systems on hello premium storage disks as /hana and /usr/sap.</span></span> <span data-ttu-id="590d0-220">此程序是必要 toohelp 防止 hello 根檔案系統，它不是大型 Linux 的 Azure Vm 上，填滿。</span><span class="sxs-lookup"><span data-stu-id="590d0-220">This process is necessary toohelp prevent hello root file system, which isn't large on Linux Azure VMs, from filling up.</span></span>
8. <span data-ttu-id="590d0-221">輸入 hello /etc/hosts hosts 檔案中的 hello 測試 Vm 的 hello 本機 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="590d0-221">Enter hello local IP addresses of hello test VMs in hello /etc/hosts file.</span></span>
9. <span data-ttu-id="590d0-222">輸入 hello **nofail** hello /etc/hosts fstab 檔案中的參數。</span><span class="sxs-lookup"><span data-stu-id="590d0-222">Enter hello **nofail** parameter in hello /etc/fstab file.</span></span>
10. <span data-ttu-id="590d0-223">設定核心參數，根據您使用 toohello Linux 作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="590d0-223">Set kernel parameters according toohello Linux OS release you are using.</span></span> <span data-ttu-id="590d0-224">如需詳細資訊，請參閱 hello 適當 SAP 附註會討論 HANA hello 本指南的 < 核心參數 > 一節。</span><span class="sxs-lookup"><span data-stu-id="590d0-224">For more information, see hello appropriate SAP notes that discuss HANA and hello "Kernel parameters" section in this guide.</span></span>
11. <span data-ttu-id="590d0-225">新增交換空間。</span><span class="sxs-lookup"><span data-stu-id="590d0-225">Add swap space.</span></span>
12. <span data-ttu-id="590d0-226">（選擇性） 在 hello 測試 Vm 上安裝圖形化的桌面。</span><span class="sxs-lookup"><span data-stu-id="590d0-226">Optionally, install a graphical desktop on hello test VMs.</span></span> <span data-ttu-id="590d0-227">否則，請使用遠端 SAPinst 安裝。</span><span class="sxs-lookup"><span data-stu-id="590d0-227">Otherwise, use a remote SAPinst installation.</span></span>
13. <span data-ttu-id="590d0-228">從 hello SAP 服務 Marketplace 下載 hello SAP 軟體。</span><span class="sxs-lookup"><span data-stu-id="590d0-228">Download hello SAP software from hello SAP Service Marketplace.</span></span>
14. <span data-ttu-id="590d0-229">建立群組，sapsys，與群組識別碼 1001 hello HANA 資料庫伺服器 VM 上。</span><span class="sxs-lookup"><span data-stu-id="590d0-229">Create a group, sapsys, with group ID 1001, on hello HANA DB server VM.</span></span>
15. <span data-ttu-id="590d0-230">使用 HANA 資料庫生命週期管理員 (HDBLCM) hello DB 伺服器 VM 上安裝 SAP HANA。</span><span class="sxs-lookup"><span data-stu-id="590d0-230">Install SAP HANA on hello DB server VM by using HANA Database Lifecycle Manager (HDBLCM).</span></span>
16. <span data-ttu-id="590d0-231">Hello 應用程式伺服器 VM 上安裝 hello SAP ASCS 執行個體。</span><span class="sxs-lookup"><span data-stu-id="590d0-231">Install hello SAP ASCS instance on hello app server VM.</span></span>
17. <span data-ttu-id="590d0-232">Hello 之間共用 hello /sapmnt 目錄使用 NFS 測試 Vm。</span><span class="sxs-lookup"><span data-stu-id="590d0-232">Share hello /sapmnt directory among hello test VMs by using NFS.</span></span> <span data-ttu-id="590d0-233">hello NFS 伺服器 hello 應用程式伺服器 VM。</span><span class="sxs-lookup"><span data-stu-id="590d0-233">hello application server VM is hello NFS server.</span></span>
18. <span data-ttu-id="590d0-234">安裝 hello 資料庫執行個體，包括 HANA、 使用 SWPM hello HANA 資料庫伺服器 VM 上。</span><span class="sxs-lookup"><span data-stu-id="590d0-234">Install hello database instance, including HANA, by using SWPM on hello HANA DB server VM.</span></span>
19. <span data-ttu-id="590d0-235">Hello 應用程式伺服器 VM 上安裝 hello 主應用程式伺服器 (PAS)。</span><span class="sxs-lookup"><span data-stu-id="590d0-235">Install hello primary application server (PAS) on hello application server VM.</span></span>
20. <span data-ttu-id="590d0-236">啟動 SAP MC。</span><span class="sxs-lookup"><span data-stu-id="590d0-236">Start SAP MC.</span></span> <span data-ttu-id="590d0-237">透過 SAP GUI 或 HANA Studio 連線。</span><span class="sxs-lookup"><span data-stu-id="590d0-237">Connect through SAP GUI or HANA Studio.</span></span>

## <a name="preparing-azure-vms-for-a-manual-installation-of-sap-hana"></a><span data-ttu-id="590d0-238">準備 Azure VM 以便手動安裝 SAP HANA</span><span class="sxs-lookup"><span data-stu-id="590d0-238">Preparing Azure VMs for a manual installation of SAP HANA</span></span>
<span data-ttu-id="590d0-239">本章節涵蓋下列主題中的 hello:</span><span class="sxs-lookup"><span data-stu-id="590d0-239">This section covers hello following topics:</span></span>

* <span data-ttu-id="590d0-240">OS 更新</span><span class="sxs-lookup"><span data-stu-id="590d0-240">OS updates</span></span>
* <span data-ttu-id="590d0-241">磁碟設定</span><span class="sxs-lookup"><span data-stu-id="590d0-241">Disk setup</span></span>
* <span data-ttu-id="590d0-242">核心參數</span><span class="sxs-lookup"><span data-stu-id="590d0-242">Kernel parameters</span></span>
* <span data-ttu-id="590d0-243">檔案系統</span><span class="sxs-lookup"><span data-stu-id="590d0-243">File systems</span></span>
* <span data-ttu-id="590d0-244">hello /etc/hosts 主機檔案</span><span class="sxs-lookup"><span data-stu-id="590d0-244">hello /etc/hosts file</span></span>
* <span data-ttu-id="590d0-245">hello /etc/hosts fstab 檔案</span><span class="sxs-lookup"><span data-stu-id="590d0-245">hello /etc/fstab file</span></span>

### <a name="os-updates"></a><span data-ttu-id="590d0-246">OS 更新</span><span class="sxs-lookup"><span data-stu-id="590d0-246">OS updates</span></span>
<span data-ttu-id="590d0-247">請先檢查 Linux 作業系統更新和修正程式，然後再安裝其他軟體。</span><span class="sxs-lookup"><span data-stu-id="590d0-247">Check for Linux OS updates and fixes before installing additional software.</span></span> <span data-ttu-id="590d0-248">藉由安裝修補程式時，您可能會無法 tooavoid 呼叫 toohello 的技術支援。</span><span class="sxs-lookup"><span data-stu-id="590d0-248">By installing a patch, you might be able tooavoid a call toohello support desk.</span></span>

<span data-ttu-id="590d0-249">請確定您是使用︰</span><span class="sxs-lookup"><span data-stu-id="590d0-249">Make sure that you are using:</span></span>
* <span data-ttu-id="590d0-250">適用於 SAP 應用程式的 SUSE Linux Enterprise Server。</span><span class="sxs-lookup"><span data-stu-id="590d0-250">SUSE Linux Enterprise Server for SAP Applications.</span></span>
* <span data-ttu-id="590d0-251">適用於 SAP 應用程式的 Red Hat Enterprise Linux 或適用於 SAP HANA 的 Red Hat Enterprise Linux。</span><span class="sxs-lookup"><span data-stu-id="590d0-251">Red Hat Enterprise Linux for SAP Applications or Red Hat Enterprise Linux for SAP HANA.</span></span> 

<span data-ttu-id="590d0-252">如果您還沒有這麼做，您的 Linux 訂閱 hello Linux 廠商登錄 hello 作業系統部署。</span><span class="sxs-lookup"><span data-stu-id="590d0-252">If you haven't already, register hello OS deployment with your Linux subscription from hello Linux vendor.</span></span> <span data-ttu-id="590d0-253">請注意，SUSE 具有適用於 SAP 應用程式的 OS 映像，已經包含服務且會自動註冊。</span><span class="sxs-lookup"><span data-stu-id="590d0-253">Note that SUSE has OS images for SAP applications that already include services and which are registered automatically.</span></span>

<span data-ttu-id="590d0-254">以下是檢查 for SUSE Linux 使用 hello 可用的修補程式的範例**zypper**命令：</span><span class="sxs-lookup"><span data-stu-id="590d0-254">Here is an example of checking for available patches for SUSE Linux by using hello **zypper** command:</span></span>

 `sudo zypper list-patches`

<span data-ttu-id="590d0-255">Hello 問題類型而定，依類別和嚴重性分類修補程式。</span><span class="sxs-lookup"><span data-stu-id="590d0-255">Depending on hello kind of issue, patches are classified by category and severity.</span></span> <span data-ttu-id="590d0-256">常用的分類值為：**security (安全性)**、**recommended (建議)**、**optional (選用)**、**feature (功能)**、**document (文件)** 或 **yast**。</span><span class="sxs-lookup"><span data-stu-id="590d0-256">Commonly used values for category are: **security**, **recommended**, **optional**, **feature**, **document**, or **yast**.</span></span>
<span data-ttu-id="590d0-257">常用的嚴重性值為：**critical (嚴重)**、**important (重要)**、**moderate (中)**、**low (低)** 或 **unspecified (未指定)**。</span><span class="sxs-lookup"><span data-stu-id="590d0-257">Commonly used values for severity are: **critical**, **important**, **moderate**, **low**, or **unspecified**.</span></span>

<span data-ttu-id="590d0-258">hello **zypper**命令看起來只 hello 更新，您已安裝的封裝需要。</span><span class="sxs-lookup"><span data-stu-id="590d0-258">hello **zypper** command looks only for hello updates that your installed packages need.</span></span> <span data-ttu-id="590d0-259">例如，您可以使用此命令：</span><span class="sxs-lookup"><span data-stu-id="590d0-259">For example, you could use this command:</span></span>

`sudo zypper patch  --category=security,recommended --severity=critical,important`

<span data-ttu-id="590d0-260">您可以加入 hello 參數`--dry-run`tootest hello 更新，而不需實際更新 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="590d0-260">You can add hello parameter `--dry-run` tootest hello update without actually updating hello system.</span></span>


### <a name="disk-setup"></a><span data-ttu-id="590d0-261">磁碟設定</span><span class="sxs-lookup"><span data-stu-id="590d0-261">Disk setup</span></span>
<span data-ttu-id="590d0-262">在 Azure 上的 Linux VM 中的 hello 根檔案系統有大小限制。</span><span class="sxs-lookup"><span data-stu-id="590d0-262">hello root file system in a Linux VM on Azure has a size limitation.</span></span> <span data-ttu-id="590d0-263">因此，它是必要的 tooattach 額外的磁碟空間 tooan Azure VM 執行 SAP。</span><span class="sxs-lookup"><span data-stu-id="590d0-263">Therefore, it's necessary tooattach additional disk space tooan Azure VM for running SAP.</span></span> <span data-ttu-id="590d0-264">Azure Vm SAP 應用程式伺服器，可能就已經夠用 hello 使用標準的 Azure 儲存體磁碟。</span><span class="sxs-lookup"><span data-stu-id="590d0-264">For SAP application server Azure VMs, hello use of Azure standard storage disks might be sufficient.</span></span> <span data-ttu-id="590d0-265">不過，對於 SAP HANA DBMS 的 Azure Vm，hello 使用 Azure 高階儲存體磁碟，生產環境和非生產實作是必要的。</span><span class="sxs-lookup"><span data-stu-id="590d0-265">However, for SAP HANA DBMS Azure VMs, hello use of Azure Premium Storage disks for production and non-production implementations is mandatory.</span></span>

<span data-ttu-id="590d0-266">根據 hello [SAP HANA TDI 存放裝置需求](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html)，建議 hello 下列 Azure 高階儲存體組態：</span><span class="sxs-lookup"><span data-stu-id="590d0-266">Based on hello [SAP HANA TDI Storage Requirements](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html), hello following Azure Premium Storage configuration is suggested:</span></span> 

| <span data-ttu-id="590d0-267">VM SKU</span><span class="sxs-lookup"><span data-stu-id="590d0-267">VM SKU</span></span> | <span data-ttu-id="590d0-268">RAM</span><span class="sxs-lookup"><span data-stu-id="590d0-268">RAM</span></span> |  <span data-ttu-id="590d0-269">/hana/data 和 /hana/log</span><span class="sxs-lookup"><span data-stu-id="590d0-269">/hana/data and /hana/log</span></span> <br /> <span data-ttu-id="590d0-270">與 LVM 或 MDADM 等量</span><span class="sxs-lookup"><span data-stu-id="590d0-270">striped with LVM or MDADM</span></span> | <span data-ttu-id="590d0-271">HANA/shared</span><span class="sxs-lookup"><span data-stu-id="590d0-271">/hana/shared</span></span> | <span data-ttu-id="590d0-272">/root volume</span><span class="sxs-lookup"><span data-stu-id="590d0-272">/root volume</span></span> | <span data-ttu-id="590d0-273">/usr/sap</span><span class="sxs-lookup"><span data-stu-id="590d0-273">/usr/sap</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="590d0-274">GS5</span><span class="sxs-lookup"><span data-stu-id="590d0-274">GS5</span></span> | <span data-ttu-id="590d0-275">448 GB</span><span class="sxs-lookup"><span data-stu-id="590d0-275">448 GB</span></span> | <span data-ttu-id="590d0-276">2 x P30</span><span class="sxs-lookup"><span data-stu-id="590d0-276">2 x P30</span></span> | <span data-ttu-id="590d0-277">1 x P20</span><span class="sxs-lookup"><span data-stu-id="590d0-277">1 x P20</span></span> | <span data-ttu-id="590d0-278">1 x P10</span><span class="sxs-lookup"><span data-stu-id="590d0-278">1 x P10</span></span> | <span data-ttu-id="590d0-279">1 x P10</span><span class="sxs-lookup"><span data-stu-id="590d0-279">1 x P10</span></span> | 

<span data-ttu-id="590d0-280">在 hello 建議的磁碟組態中，hello HANA 資料磁碟區與記錄檔磁碟區會放在相同設定的 Azure 高階儲存體磁碟會等量散佈 LVM 或 MDADM hello。</span><span class="sxs-lookup"><span data-stu-id="590d0-280">In hello suggested disk configuration, hello HANA data volume and log volume are placed on hello same set of Azure premium storage disks that are striped with LVM or MDADM.</span></span> <span data-ttu-id="590d0-281">不需要 toodefine 任何 RAID 備援層級，因為 Azure 高階儲存體保持 hello 磁碟備援的三個映像。</span><span class="sxs-lookup"><span data-stu-id="590d0-281">It is not necessary toodefine any RAID redundancy level because Azure Premium Storage keeps three images of hello disks for redundancy.</span></span> <span data-ttu-id="590d0-282">toomake 確定您已設定足夠的儲存空間，請參閱 hello [SAP HANA TDI 存放裝置需求](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html)和[SAP HANA 伺服器安裝及更新指南](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm)。</span><span class="sxs-lookup"><span data-stu-id="590d0-282">toomake sure that you configure enough storage, consult hello [SAP HANA TDI Storage Requirements](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) and [SAP HANA Server Installation and Update Guide](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm).</span></span> <span data-ttu-id="590d0-283">也請考慮 hello hello 的其他虛擬硬碟 (VHD) 輸送量磁碟區不同的 Azure 高階儲存體磁碟中所述[高效能高階儲存體和受管理的 Vm 磁碟](https://docs.microsoft.com/azure/storage/storage-premium-storage)。</span><span class="sxs-lookup"><span data-stu-id="590d0-283">Also consider hello different virtual hard disk (VHD) throughput volumes of hello different Azure premium storage disks as documented in [High-performance Premium Storage and managed disks for VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span></span> 

<span data-ttu-id="590d0-284">您可以加入更多的進階儲存體磁碟 toohello HANA DBMS Vm 來儲存資料庫或交易記錄備份。</span><span class="sxs-lookup"><span data-stu-id="590d0-284">You can add more premium storage disks toohello HANA DBMS VMs for storing database or transaction log backups.</span></span>

<span data-ttu-id="590d0-285">如需 hello 兩個主要工具 tooconfigure 等量的詳細資訊，請參閱下列發行項的 hello:</span><span class="sxs-lookup"><span data-stu-id="590d0-285">For more information about hello two main tools used tooconfigure striping, see hello following articles:</span></span>

* [<span data-ttu-id="590d0-286">在 Linux 上設定軟體 RAID</span><span class="sxs-lookup"><span data-stu-id="590d0-286">Configure software RAID on Linux</span></span>](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="590d0-287">設定 Azure 中 Linux VM 的 LVM</span><span class="sxs-lookup"><span data-stu-id="590d0-287">Configure LVM on a Linux VM in Azure</span></span>](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="590d0-288">如需有關附加磁碟 tooAzure Vm 執行 Linux 作為客體作業系統、 請參閱 <<c0> [ 新增磁碟 tooa Linux VM](../../linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="590d0-288">For more information on attaching disks tooAzure VMs running Linux as a guest OS, see [Add a disk tooa Linux VM](../../linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="590d0-289">Azure 高階儲存體可讓您 toodefine 磁碟快取模式。</span><span class="sxs-lookup"><span data-stu-id="590d0-289">Azure Premium Storage allows you toodefine disk caching modes.</span></span> <span data-ttu-id="590d0-290">持有 /hana/data 和 /hana/log hello 等量集，磁碟快取應該停用。</span><span class="sxs-lookup"><span data-stu-id="590d0-290">For hello striped set holding /hana/data and /hana/log, disk caching should be disabled.</span></span> <span data-ttu-id="590d0-291">應該設定太的 hello 其他磁碟區 （磁碟），hello 快取模式**ReadOnly**。</span><span class="sxs-lookup"><span data-stu-id="590d0-291">For hello other volumes (disks), hello caching mode should be set too**ReadOnly**.</span></span>

<span data-ttu-id="590d0-292">如需詳細資訊，請參閱[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../../../storage/common/storage-premium-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="590d0-292">For more information, see [Premium Storage: High-performance storage for Azure Virtual Machine workloads](../../../storage/common/storage-premium-storage.md).</span></span>

<span data-ttu-id="590d0-293">toofind 範例 JSON 範本建立的 Vm，跳過[Azure 快速入門範本](https://github.com/Azure/azure-quickstart-templates)。</span><span class="sxs-lookup"><span data-stu-id="590d0-293">toofind sample JSON templates for creating VMs, go too[Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
<span data-ttu-id="590d0-294">hello vm-簡單-sles 範本是基本的範本。</span><span class="sxs-lookup"><span data-stu-id="590d0-294">hello vm-simple-sles template is a basic template.</span></span> <span data-ttu-id="590d0-295">它包含儲存體區段與其他 100 GB 的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="590d0-295">It includes a storage section, with an additional 100-GB data disk.</span></span> <span data-ttu-id="590d0-296">此範本可用來當做基底。</span><span class="sxs-lookup"><span data-stu-id="590d0-296">This template can be used as a base.</span></span> <span data-ttu-id="590d0-297">您可以調整 hello 範本 tooyour 特定設定。</span><span class="sxs-lookup"><span data-stu-id="590d0-297">You can adapt hello template tooyour specific configuration.</span></span>

>[!Note]
><span data-ttu-id="590d0-298">如中所述，使用 UUID 是重要的 tooattach hello Azure 儲存體磁碟[執行 SAP NetWeaver on Microsoft Azure SUSE Linux Vm](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="590d0-298">It is important tooattach hello Azure storage disk by using a UUID as documented in [Running SAP NetWeaver on Microsoft Azure SUSE Linux VMs](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="590d0-299">在 hello 測試環境中，兩個標準的 Azure 儲存體中的磁碟附加的 toohello SAP 應用程式伺服器 VM，hello 下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="590d0-299">In hello test environment, two Azure standard storage disks were attached toohello SAP app server VM, as shown in hello following screenshot.</span></span> <span data-ttu-id="590d0-300">一個磁碟儲存所有 hello SAP 軟體 （包括 NetWeaver 7.5，SAP GUI 與 SAP HANA） 安裝。</span><span class="sxs-lookup"><span data-stu-id="590d0-300">One disk stored all hello SAP software (including NetWeaver 7.5, SAP GUI, and SAP HANA) for installation.</span></span> <span data-ttu-id="590d0-301">足夠的可用空間會是可用的其他需求 （例如，備份和測試資料），和相同的 SAP 版圖的 hello /sapmnt 目錄 （也就是 SAP 設定檔） toobe 隸屬 toohello 的所有 Vm 之間共用，同時能確保 hello 第二個磁碟。</span><span class="sxs-lookup"><span data-stu-id="590d0-301">hello second disk ensured that enough free space would be available for additional requirements (for example, backup and test data) and for hello /sapmnt directory (that is, SAP profiles) toobe shared among all VMs that belong toohello same SAP landscape.</span></span>

![SAP HANA 應用程式伺服器的 [磁碟] 視窗，其中顯示兩個資料磁碟及其大小](./media/hana-get-started/image003.jpg)


### <a name="kernel-parameters"></a><span data-ttu-id="590d0-303">核心參數</span><span class="sxs-lookup"><span data-stu-id="590d0-303">Kernel parameters</span></span>
<span data-ttu-id="590d0-304">SAP HANA 需要特定 Linux 核心設定，這不是 hello 標準 Azure 資源庫映像的一部分，而且必須手動設定。</span><span class="sxs-lookup"><span data-stu-id="590d0-304">SAP HANA requires specific Linux kernel settings, which are not part of hello standard Azure gallery images and must be set manually.</span></span> <span data-ttu-id="590d0-305">根據您是否使用 SUSE 或 Red Hat，hello 參數可能不同。</span><span class="sxs-lookup"><span data-stu-id="590d0-305">Depending on whether you use SUSE or Red Hat, hello parameters might be different.</span></span> <span data-ttu-id="590d0-306">稍早所列的 hello SAP 附註會提供這些參數的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="590d0-306">hello SAP Notes listed earlier give information about those parameters.</span></span> <span data-ttu-id="590d0-307">在 hello 螢幕擷取畫面所示，已用 SUSE Linux 12 SP1。</span><span class="sxs-lookup"><span data-stu-id="590d0-307">In hello screenshots shown, SUSE Linux 12 SP1 was used.</span></span> 

<span data-ttu-id="590d0-308">SLES SAP 應用程式 12 GA 如和 SLES SAP 應用程式 12 sp1 有全新的工具、**微調 adm**，取代 hello 舊**sapconf**工具。</span><span class="sxs-lookup"><span data-stu-id="590d0-308">SLES for SAP Applications 12 GA and SLES for SAP Applications 12 SP1 have a new tool, **tuned-adm**, that replaces hello old **sapconf** tool.</span></span> <span data-ttu-id="590d0-309">**tuned-adm** 有特別的 SAP HANA 設定檔可供其使用。</span><span class="sxs-lookup"><span data-stu-id="590d0-309">A special SAP HANA profile is available for **tuned-adm**.</span></span> <span data-ttu-id="590d0-310">SAP hana tootune hello 系統以根使用者身分輸入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="590d0-310">tootune hello system for SAP HANA, enter hello following as a root user:</span></span>

   `tuned-adm profile sap-hana`

<span data-ttu-id="590d0-311">如需有關**微調 adm**，請參閱 hello [SUSE 文件中的有關微調 adm](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip)。</span><span class="sxs-lookup"><span data-stu-id="590d0-311">For more information about **tuned-adm**, see hello [SUSE documentation about tuned-adm](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip).</span></span>

<span data-ttu-id="590d0-312">在下列螢幕擷取畫面的 hello，您可以查看如何**微調 adm**變更的 hello`transparent_hugepage`和`numa_balancing`值，根據 toohello 必要 SAP HANA 設定。</span><span class="sxs-lookup"><span data-stu-id="590d0-312">In hello following screenshot, you can see how **tuned-adm** changed hello `transparent_hugepage` and `numa_balancing` values, according toohello required SAP HANA settings.</span></span>

![hello 微調 adm 工具根據 toorequired SAP HANA 設定的值變更。](./media/hana-get-started/image005.jpg)

<span data-ttu-id="590d0-314">toomake hello SAP HANA 核心設定永久性的會使用**grub2** SLES 12 上。</span><span class="sxs-lookup"><span data-stu-id="590d0-314">toomake hello SAP HANA kernel settings permanent, use **grub2** on SLES 12.</span></span> <span data-ttu-id="590d0-315">如需有關**grub2**，go toohello[組態檔結構](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip)hello SUSE 文件的區段。</span><span class="sxs-lookup"><span data-stu-id="590d0-315">For more information about **grub2**, go toohello [Configuration File Structure](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) section of hello SUSE documentation.</span></span>

<span data-ttu-id="590d0-316">hello 下列螢幕擷取畫面顯示如何 hello 核心設定已變更 hello 組態檔中，以及接著編譯使用**grub2 mkconfig**:</span><span class="sxs-lookup"><span data-stu-id="590d0-316">hello following screenshot shows how hello kernel settings were changed in hello configuration file and then compiled by using **grub2-mkconfig**:</span></span>

![Hello 組態檔中變更，並且使用 grub2 mkconfig 編譯的核心設定](./media/hana-get-started/image006.jpg)

<span data-ttu-id="590d0-318">另一個選項是使用 YaST 和 hello toochange hello 設定**開機載入器** > **核心參數**設定：</span><span class="sxs-lookup"><span data-stu-id="590d0-318">Another option is toochange hello settings by using YaST and hello **Boot Loader** > **Kernel Parameters** settings:</span></span>

![hello 核心參數設定 索引標籤中 YaST 開機載入器](./media/hana-get-started/image007.jpg)

### <a name="file-systems"></a><span data-ttu-id="590d0-320">檔案系統</span><span class="sxs-lookup"><span data-stu-id="590d0-320">File systems</span></span>
<span data-ttu-id="590d0-321">hello 下列螢幕擷取畫面顯示 hello SAP 應用程式伺服器 VM 之上 hello 兩個連接標準的 Azure 儲存體磁碟所建立的兩個檔案系統。</span><span class="sxs-lookup"><span data-stu-id="590d0-321">hello following screenshot shows two file systems that were created on hello SAP app server VM on top of hello two attached Azure standard storage disks.</span></span> <span data-ttu-id="590d0-322">這兩個檔案系統的型別 XFS 且已掛接太/sapdata 和 /sapsoftware。</span><span class="sxs-lookup"><span data-stu-id="590d0-322">Both file systems are of type XFS and are mounted too/sapdata and /sapsoftware.</span></span>

<span data-ttu-id="590d0-323">它是不必要的 toostructure 以這種方式在檔案系統。</span><span class="sxs-lookup"><span data-stu-id="590d0-323">It is not mandatory toostructure your file systems in this way.</span></span> <span data-ttu-id="590d0-324">您必須建構 hello 磁碟空間的其他選項。</span><span class="sxs-lookup"><span data-stu-id="590d0-324">You have other options for structuring hello disk space.</span></span> <span data-ttu-id="590d0-325">hello 最重要的考量是 tooprevent hello 根檔案系統的可用空間不足。</span><span class="sxs-lookup"><span data-stu-id="590d0-325">hello most important consideration is tooprevent hello root file system from running out of free space.</span></span>

![Hello SAP 應用程式伺服器 VM 上建立兩個檔案系統](./media/hana-get-started/image008.jpg)

<span data-ttu-id="590d0-327">關於 hello SAP HANA 資料庫 VM，資料庫在安裝期間，當您使用 SAPinst (SWPM) 和 hello**一般**安裝選項時，一切都已安裝 /hana 和 /usr/sap 底下。</span><span class="sxs-lookup"><span data-stu-id="590d0-327">Regarding hello SAP HANA DB VM, during a database installation, when you use SAPinst (SWPM) and hello **typical** installation option, everything is installed under /hana and /usr/sap.</span></span> <span data-ttu-id="590d0-328">hello hello SAP HANA 記錄備份的預設位置是在 /usr/sap 之下。</span><span class="sxs-lookup"><span data-stu-id="590d0-328">hello default location for hello SAP HANA log backup is under /usr/sap.</span></span> <span data-ttu-id="590d0-329">同樣地，因為它是重要的 tooprevent hello 根檔案系統的儲存空間不足，請確定有足夠的可用空間 /hana 和 /usr/sap 下再使用 SWPM 安裝 SAP HANA。</span><span class="sxs-lookup"><span data-stu-id="590d0-329">Again, because it's important tooprevent hello root file system from running out of storage space, make sure that there is enough free space under /hana and /usr/sap before you install SAP HANA by using SWPM.</span></span>

<span data-ttu-id="590d0-330">如需 hello 標準檔案系統配置的 SAP HANA 的說明，請參閱 hello [SAP HANA 伺服器安裝及更新指南](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm)。</span><span class="sxs-lookup"><span data-stu-id="590d0-330">For a description of hello standard file-system layout of SAP HANA, see hello [SAP HANA Server Installation and Update Guide](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm).</span></span>

![建立 hello SAP 應用程式伺服器 VM 上的其他檔案系統](./media/hana-get-started/image009.jpg)

<span data-ttu-id="590d0-332">當您在標準 SLES/SLES 的 SAP 應用程式 12 Azure 資源庫映像上安裝 SAP NetWeaver 時，會顯示訊息，指出沒有交換空間，如下列螢幕擷取畫面的 hello 中所示。</span><span class="sxs-lookup"><span data-stu-id="590d0-332">When you install SAP NetWeaver on a standard SLES/SLES for SAP Applications 12 Azure gallery image, a message is displayed that says  there is no swap space, as shown in hello following screenshot.</span></span> <span data-ttu-id="590d0-333">toodismiss 這個訊息，您可以使用，以手動新增分頁檔**dd**， **mkswap**，和**swapon**。</span><span class="sxs-lookup"><span data-stu-id="590d0-333">toodismiss this message, you can manually add a swap file by using **dd**, **mkswap**, and **swapon**.</span></span> <span data-ttu-id="590d0-334">toolearn 作法，請搜尋 「 交換檔手動新增 「 在 hello[使用 hello YaST Partitioner](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) hello SUSE 文件的區段。</span><span class="sxs-lookup"><span data-stu-id="590d0-334">toolearn how, search for "Adding a swap file manually" in hello [Using hello YaST Partitioner](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) section of hello SUSE documentation.</span></span>

<span data-ttu-id="590d0-335">另一個選項是使用 hello Linux VM 代理程式 tooconfigure 交換空間。</span><span class="sxs-lookup"><span data-stu-id="590d0-335">Another option is tooconfigure swap space by using hello Linux VM agent.</span></span> <span data-ttu-id="590d0-336">如需詳細資訊，請參閱 hello [Azure Linux 代理程式使用者指南](../../linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="590d0-336">For more information, see hello [Azure Linux Agent User Guide](../../linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

![指出沒有足夠交換空間的快顯訊息](./media/hana-get-started/image010.jpg)


### <a name="hello-etchosts-file"></a><span data-ttu-id="590d0-338">hello /etc/hosts 主機檔案</span><span class="sxs-lookup"><span data-stu-id="590d0-338">hello /etc/hosts file</span></span>
<span data-ttu-id="590d0-339">啟動 tooinstall SAP 之前，請確定您包含 hello 主機名稱和 IP 位址的 hello SAP Vm hello /etc/hosts 檔案中。</span><span class="sxs-lookup"><span data-stu-id="590d0-339">Before you start tooinstall SAP, make sure you include hello host names and IP addresses of hello SAP VMs in hello /etc/hosts file.</span></span> <span data-ttu-id="590d0-340">將一個 Azure 虛擬網路內的所有 hello SAP Vm 都部署，然後使用 hello 內部 IP 位址，如下所示：</span><span class="sxs-lookup"><span data-stu-id="590d0-340">Deploy all hello SAP VMs within one Azure virtual network, and then use hello internal IP addresses, as shown here:</span></span>

![Hello /etc/hosts 檔案中列出的主機名稱和 IP 位址的 hello SAP Vm](./media/hana-get-started/image011.jpg)

### <a name="hello-etcfstab-file"></a><span data-ttu-id="590d0-342">hello /etc/hosts fstab 檔案</span><span class="sxs-lookup"><span data-stu-id="590d0-342">hello /etc/fstab file</span></span>

<span data-ttu-id="590d0-343">它是很有幫助 tooadd hello **nofail**參數 toohello fstab 檔案。</span><span class="sxs-lookup"><span data-stu-id="590d0-343">It is helpful tooadd hello **nofail** parameter toohello fstab file.</span></span> <span data-ttu-id="590d0-344">如此一來，如果出錯 hello 磁碟 hello VM 不會不停止回應 hello 開機程序。</span><span class="sxs-lookup"><span data-stu-id="590d0-344">This way, if something goes wrong with hello disks, hello VM does not hang in hello boot process.</span></span> <span data-ttu-id="590d0-345">但是請記住，額外的磁碟空間可能無法使用，而且處理程序可能會填滿 hello 根檔案系統。</span><span class="sxs-lookup"><span data-stu-id="590d0-345">But remember that additional disk space might not be available, and processes might fill up hello root file system.</span></span> <span data-ttu-id="590d0-346">如果遺失 /hana，SAP HANA 將無法啟動。</span><span class="sxs-lookup"><span data-stu-id="590d0-346">If /hana is missing, SAP HANA won't start.</span></span>

![新增 hello nofail 參數 toohello fstab 檔案](./media/hana-get-started/image000c.jpg)

## <a name="graphical-gnome-desktop-on-sles-12sles-for-sap-applications-12"></a><span data-ttu-id="590d0-348">SLES 12/SLES for SAP Applications 12 上的圖形化 GNOME 桌面</span><span class="sxs-lookup"><span data-stu-id="590d0-348">Graphical GNOME desktop on SLES 12/SLES for SAP Applications 12</span></span>
<span data-ttu-id="590d0-349">本章節涵蓋下列主題中的 hello:</span><span class="sxs-lookup"><span data-stu-id="590d0-349">This section covers hello following topics:</span></span>

* <span data-ttu-id="590d0-350">Hello GNOME 桌面和 xrdp 上安裝 SLES 12/SLES SAP 應用程式 12</span><span class="sxs-lookup"><span data-stu-id="590d0-350">Installing hello GNOME desktop and xrdp on SLES 12/SLES for SAP Applications 12</span></span>
* <span data-ttu-id="590d0-351">在 SLES 12/SLES for SAP Applications 12 上使用 Firefox 來執行以 Java 為基礎的 SAP MC</span><span class="sxs-lookup"><span data-stu-id="590d0-351">Running Java-based SAP MC by using Firefox on SLES 12/SLES for SAP Applications 12</span></span>

<span data-ttu-id="590d0-352">您也可以使用替代項目，例如 Xterminal 或 VNC (不在本指南中說明)。</span><span class="sxs-lookup"><span data-stu-id="590d0-352">You can also use alternatives such as Xterminal or VNC (not described in this guide).</span></span>

### <a name="installing-hello-gnome-desktop-and-xrdp-on-sles-12sles-for-sap-applications-12"></a><span data-ttu-id="590d0-353">Hello GNOME 桌面和 xrdp 上安裝 SLES 12/SLES SAP 應用程式 12</span><span class="sxs-lookup"><span data-stu-id="590d0-353">Installing hello GNOME desktop and xrdp on SLES 12/SLES for SAP Applications 12</span></span>
<span data-ttu-id="590d0-354">如果您有 Windows 背景時，可以輕鬆地使用直接在 hello SAP Linux Vm toorun Firefox、 SAPinst、 SAP GUI、 SAP MC 或 HANA Studio 中的圖形化桌面，並透過從 Windows 電腦的 hello 遠端桌面通訊協定 (RDP) 連線 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="590d0-354">If you have a Windows background, you can easily use a graphical desktop directly within hello SAP Linux VMs toorun Firefox, SAPinst, SAP GUI, SAP MC, or HANA Studio, and connect toohello VM through hello Remote Desktop Protocol (RDP) from a Windows computer.</span></span> <span data-ttu-id="590d0-355">取決於您的公司原則，關於新增圖形化使用者介面 tooproduction 和非實際執行的 Linux 系統，您可能想 tooinstall GNOME 您伺服器上。</span><span class="sxs-lookup"><span data-stu-id="590d0-355">Dependent on your company policies about adding graphical user interfaces tooproduction and non-production Linux based systems, you might want tooinstall GNOME on your server.</span></span> <span data-ttu-id="590d0-356">在 SAP 應用程式 12 VM Azure SLES 12/SLES tooinstall hello GNOME 桌面：</span><span class="sxs-lookup"><span data-stu-id="590d0-356">tooinstall hello GNOME desktop on an Azure SLES 12/SLES for SAP Applications 12 VM:</span></span>

1. <span data-ttu-id="590d0-357">輸入下列命令 （例如，在 PuTTY 視窗） 中的 hello 安裝 hello GNOME 桌面：</span><span class="sxs-lookup"><span data-stu-id="590d0-357">Install hello GNOME desktop by entering hello following command (for example, in a PuTTY window):</span></span>

   `zypper in -t pattern gnome-basic`

2. <span data-ttu-id="590d0-358">安裝 xrdp tooallow 連接 toohello 透過 RDP 的 VM:</span><span class="sxs-lookup"><span data-stu-id="590d0-358">Install xrdp tooallow a connection toohello VM through RDP:</span></span>

   `zypper in xrdp`

3. <span data-ttu-id="590d0-359">編輯 /etc/sysconfig/windowmanager，並設定 hello 預設視窗管理員 tooGNOME︰</span><span class="sxs-lookup"><span data-stu-id="590d0-359">Edit /etc/sysconfig/windowmanager, and set hello default window manager tooGNOME:</span></span>

   `DEFAULT_WM="gnome"`

4. <span data-ttu-id="590d0-360">執行**chkconfig** toomake 確定該 xrdp 重新開機後自動啟動：</span><span class="sxs-lookup"><span data-stu-id="590d0-360">Run **chkconfig** toomake sure that xrdp starts automatically after a reboot:</span></span>

   `chkconfig -level 3 xrdp on`

5. <span data-ttu-id="590d0-361">如果您擁有 hello RDP 連線的問題，請再試一次 toorestart （從 PuTTY 視窗，例如）：</span><span class="sxs-lookup"><span data-stu-id="590d0-361">If you have an issue with hello RDP connection, try toorestart (from a PuTTY window, for example):</span></span>

   `/etc/xrdp/xrdp.sh restart`

6. <span data-ttu-id="590d0-362">如果 xrdp 重新啟動中所述 hello 上一個步驟無效，檢查.pid 檔案：</span><span class="sxs-lookup"><span data-stu-id="590d0-362">If an xrdp restart mentioned in hello previous step doesn't work, check for a .pid file:</span></span>

   `check /var/run` 

   <span data-ttu-id="590d0-363">尋找 `xrdp.pid`。</span><span class="sxs-lookup"><span data-stu-id="590d0-363">Look for `xrdp.pid`.</span></span> <span data-ttu-id="590d0-364">如果找到的話，移除它，然後再試一次 toorestart。</span><span class="sxs-lookup"><span data-stu-id="590d0-364">If you find it, remove it, and try toorestart again.</span></span>

### <a name="starting-sap-mc"></a><span data-ttu-id="590d0-365">啟動 SAP MC</span><span class="sxs-lookup"><span data-stu-id="590d0-365">Starting SAP MC</span></span>
<span data-ttu-id="590d0-366">安裝 hello GNOME 桌面之後，開始圖形 hello Firefox Azure SLES 12/SLES 中執行的 SAP 應用程式 12 VM 時從 Java 為基礎 SAP MC 可能會顯示錯誤因為 hello 遺漏 Java 瀏覽器外掛程式。</span><span class="sxs-lookup"><span data-stu-id="590d0-366">After you install hello GNOME desktop, starting hello graphical Java-based SAP MC from Firefox while running in an Azure SLES 12/SLES for SAP Applications 12 VM might display an error because of hello missing Java-browser plug-in.</span></span>

<span data-ttu-id="590d0-367">SAP MC 是 hello URL toostart hello `<server>:5<instance_number>13`。</span><span class="sxs-lookup"><span data-stu-id="590d0-367">hello URL toostart hello SAP MC is `<server>:5<instance_number>13`.</span></span>

<span data-ttu-id="590d0-368">如需詳細資訊，請參閱[起始 hello SAP 網頁型管理主控台](https://help.sap.com/saphelp_nwce10/helpdata/en/48/6b7c6178dc4f93e10000000a42189d/frameset.htm)。</span><span class="sxs-lookup"><span data-stu-id="590d0-368">For more information, see [Starting hello Web-Based SAP Management Console](https://help.sap.com/saphelp_nwce10/helpdata/en/48/6b7c6178dc4f93e10000000a42189d/frameset.htm).</span></span>

<span data-ttu-id="590d0-369">hello 下列螢幕擷取畫面顯示 hello hello Java 瀏覽器外掛程式遺漏時所顯示的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="590d0-369">hello following screenshot shows hello error message that is displayed when hello Java-browser plug-in is missing:</span></span>

![指出遺失 Java 瀏覽器外掛程式的錯誤訊息](./media/hana-get-started/image013.jpg)

<span data-ttu-id="590d0-371">其中一種方式 toosolve hello 問題是 tooinstall hello 缺少外掛程式使用 YaST，hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="590d0-371">One way toosolve hello problem is tooinstall hello missing plug-in by using YaST, as shown in hello following screenshot:</span></span>

![使用 YaST tooinstall 缺少外掛程式](./media/hana-get-started/image014.jpg)

<span data-ttu-id="590d0-373">當您重新輸入 hello SAP 管理主控台 URL 時，出現下列訊息詢問您 tooactivate hello 外掛程式：</span><span class="sxs-lookup"><span data-stu-id="590d0-373">When you re-enter hello SAP Management Console URL, a message appears asking you tooactivate hello plug-in:</span></span>

![要求啟用外掛程式的對話方塊](./media/hana-get-started/image015.jpg)

<span data-ttu-id="590d0-375">您可能也會收到關於遺失檔案 (javafx.properties) 的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="590d0-375">You might also receive an error message about a missing file, javafx.properties.</span></span> <span data-ttu-id="590d0-376">這是 Oracle Java 1.8 的 SAP GUI 7.4 相關的 toohello 需求。</span><span class="sxs-lookup"><span data-stu-id="590d0-376">This is related toohello requirement of Oracle Java 1.8 for SAP GUI 7.4.</span></span> <span data-ttu-id="590d0-377">(請參閱 [SAP 附註 2059429](https://launchpad.support.sap.com/#/notes/2059424)。)Hello IBM Java 版本都具有 SLES/SLES 所傳送的 SAP 應用程式 12 hello openjdk 封裝包括 hello 需要的 javafx.properties 檔案。</span><span class="sxs-lookup"><span data-stu-id="590d0-377">(See [SAP Note 2059429](https://launchpad.support.sap.com/#/notes/2059424).) Neither hello IBM Java version nor hello openjdk package delivered with SLES/SLES for SAP Applications 12 includes hello needed javafx.properties file.</span></span> <span data-ttu-id="590d0-378">hello 方案是 toodownload，然後安裝 Oracle Java SE 8。</span><span class="sxs-lookup"><span data-stu-id="590d0-378">hello solution is toodownload and install Java SE 8 from Oracle.</span></span>

<span data-ttu-id="590d0-379">OpenSUSE openjdk 類似問題的相關資訊，請參閱 hello 討論[openSUSE 42.1 的 SAPGui 7.4 Java Leap](https://scn.sap.com/thread/3908306)。</span><span class="sxs-lookup"><span data-stu-id="590d0-379">For information about a similar issue with openjdk on openSUSE, see hello discussion thread [SAPGui 7.4 Java for openSUSE 42.1 Leap](https://scn.sap.com/thread/3908306).</span></span>

## <a name="manual-installation-of-sap-hana-swpm"></a><span data-ttu-id="590d0-380">手動安裝 SAP HANA：SWPM</span><span class="sxs-lookup"><span data-stu-id="590d0-380">Manual installation of SAP HANA: SWPM</span></span>
<span data-ttu-id="590d0-381">本節中的螢幕擷取畫面的 hello 數列會顯示 hello 安裝 SAP NetWeaver 7.5 和 SAP HANA SP12，當您使用 SWPM (SAPinst) 的關鍵步驟。</span><span class="sxs-lookup"><span data-stu-id="590d0-381">hello series of screenshots in this section shows hello key steps for installing SAP NetWeaver 7.5 and SAP HANA SP12 when you use SWPM (SAPinst).</span></span> <span data-ttu-id="590d0-382">NetWeaver 7.5 安裝的一部分，SWPM 也可以安裝 hello HANA 資料庫的單一執行個體。</span><span class="sxs-lookup"><span data-stu-id="590d0-382">As part of a NetWeaver 7.5 installation, SWPM can also install hello HANA database as a single instance.</span></span>

<span data-ttu-id="590d0-383">在範例測試環境中，我們只安裝了一部進階商業應用程式程式設計 (ABAP) 應用程式伺服器。</span><span class="sxs-lookup"><span data-stu-id="590d0-383">In a sample test environment, we installed just one Advanced Business Application Programming (ABAP) app server.</span></span> <span data-ttu-id="590d0-384">Hello 下列螢幕擷取畫面所示，我們使用 hello**分散式系統**選項 tooinstall hello ASCS 和一個 Azure VM 與 SAP HANA 中的主要應用程式伺服器執行個體做為另一個 Azure VM 中的 hello 資料庫系統。</span><span class="sxs-lookup"><span data-stu-id="590d0-384">As shown in hello following screenshot, we used hello **Distributed System** option tooinstall hello ASCS and primary application server instances in one Azure VM and SAP HANA as hello database system in another Azure VM.</span></span>

![ASCS 和使用 hello 分散式系統選項來安裝主要應用程式伺服器執行個體](./media/hana-get-started/image012.jpg)

<span data-ttu-id="590d0-386">Hello ASCS 執行個體安裝在 hello 應用程式伺服器 VM 上，而之後設定太 「 綠色 」 hello SAP 管理主控台 （如 hello 下列螢幕擷取畫面所示），在 hello /sapmnt 目錄 （包括 hello SAP 設定檔的目錄） 必須與共用 hello SAP HANA 資料庫伺服器 VM。</span><span class="sxs-lookup"><span data-stu-id="590d0-386">After hello ASCS instance is installed on hello app server VM and is set too"green" in hello SAP Management Console (shown in hello following screenshot), hello /sapmnt directory (including hello SAP profile directory) must be shared with hello SAP HANA DB server VM.</span></span> <span data-ttu-id="590d0-387">hello DB 安裝步驟需要存取 toothis 資訊。</span><span class="sxs-lookup"><span data-stu-id="590d0-387">hello DB installation step needs access toothis information.</span></span> <span data-ttu-id="590d0-388">toouse NFS 可設定使用 YaST hello 最佳方式 tooprovide 存取。</span><span class="sxs-lookup"><span data-stu-id="590d0-388">hello best way tooprovide access is toouse NFS, which can be configured by using YaST.</span></span>

![SAP 管理主控台顯示 hello ASCS 執行個體 hello 應用程式伺服器 VM 上安裝和設定太 「 綠色的"](./media/hana-get-started/image016.jpg)

<span data-ttu-id="590d0-390">在應用程式伺服器 VM hello、 hello/sapmnt 目錄應該透過 NFS 共用，使用 hello **rw**和**no_root_squash**選項。</span><span class="sxs-lookup"><span data-stu-id="590d0-390">On hello app server VM, hello /sapmnt directory should be shared via NFS by using hello **rw** and **no_root_squash** options.</span></span> <span data-ttu-id="590d0-391">hello 的預設值為**ro**和**root_squash**，這可能會導致 tooproblems，當您安裝 hello 資料庫執行個體。</span><span class="sxs-lookup"><span data-stu-id="590d0-391">hello defaults are **ro** and **root_squash**, which might lead tooproblems when you install hello database instance.</span></span>

![透過使用 hello rw 和 no_root_squash 選項共用透過 NFS hello /sapmnt 目錄](./media/hana-get-started/image017b.jpg)

<span data-ttu-id="590d0-393">如 hello 的下一個螢幕擷取畫面所示，從 hello 應用程式伺服器 VM 的 hello /sapmnt 共用必須設定 hello SAP HANA 資料庫伺服器 VM 上使用**NFS 用戶端**（和 YaST）。</span><span class="sxs-lookup"><span data-stu-id="590d0-393">As hello next screenshot shows, hello /sapmnt share from hello app server VM must be configured on hello SAP HANA DB server VM by using **NFS Client** (and YaST).</span></span>

![設定使用 NFS 用戶端 hello /sapmnt 共用](./media/hana-get-started/image018b.jpg)

<span data-ttu-id="590d0-395">分散式的 NetWeaver 7.5 tooperform 安裝 (**資料庫執行個體**)，下列螢幕擷取畫面所示的 hello，為登入 toohello SAP HANA 資料庫伺服器 VM 並啟動 SWPM。</span><span class="sxs-lookup"><span data-stu-id="590d0-395">tooperform a distributed NetWeaver 7.5 installation (**Database Instance**), as shown in hello following screenshot, sign in toohello SAP HANA DB server VM and start SWPM.</span></span>

![安裝的資料庫執行個體，登入 toohello SAP HANA 資料庫伺服器 VM，然後啟動 SWPM](./media/hana-get-started/image019.jpg)

<span data-ttu-id="590d0-397">選取後**一般**安裝與 hello 路徑 toohello 安裝媒體上，輸入 DB SID、 hello 主機名稱、 hello 執行個體數目和 hello DB 系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="590d0-397">After you select **typical** installation and hello path toohello installation media, enter a DB SID, hello host name, hello instance number, and hello DB system administrator password.</span></span>

![hello SAP HANA 資料庫系統管理員登入頁面](./media/hana-get-started/image035b.jpg)

<span data-ttu-id="590d0-399">Hello DBACOCKPIT 結構描述，請輸入 hello 密碼：</span><span class="sxs-lookup"><span data-stu-id="590d0-399">Enter hello password for hello DBACOCKPIT schema:</span></span>

![hello DBACOCKPIT 結構描述的 hello 密碼項目方塊](./media/hana-get-started/image036b.jpg)

<span data-ttu-id="590d0-401">輸入 hello SAPABAP1 結構描述密碼問題：</span><span class="sxs-lookup"><span data-stu-id="590d0-401">Enter a question for hello SAPABAP1 schema password:</span></span>

![輸入 hello SAPABAP1 結構描述密碼問題](./media/hana-get-started/image037b.jpg)

<span data-ttu-id="590d0-403">每個工作完成後，綠色的核取記號會顯示 hello DB 安裝程序的下一個 tooeach 階段。</span><span class="sxs-lookup"><span data-stu-id="590d0-403">After each task is completed, a green check mark is displayed next tooeach phase of hello DB installation process.</span></span> <span data-ttu-id="590d0-404">hello 訊息 」 執行的...資料庫執行個體已完成。」隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="590d0-404">hello message "Execution of ... Database Instance has completed" is displayed.</span></span>

![含有確認訊息的完成工作視窗](./media/hana-get-started/image023.jpg)

<span data-ttu-id="590d0-406">安裝成功後，hello SAP 管理主控台應該也會顯示 hello 與 「 綠色 」 的資料庫執行個體，並顯示 hello 的 SAP HANA 處理程序 （hdbindexserver、 hdbcompileserver，等等） 的完整清單。</span><span class="sxs-lookup"><span data-stu-id="590d0-406">After successful installation, hello SAP Management Console should also show hello DB instance as "green" and display hello full list of SAP HANA processes (hdbindexserver, hdbcompileserver, and so forth).</span></span>

![含有 SAP HANA 程序清單的 SAP 管理主控台視窗](./media/hana-get-started/image024.jpg)

<span data-ttu-id="590d0-408">hello 下列螢幕擷取畫面顯示 hello 部分 hello SWPM hello HANA 安裝期間所建立的 hello /hana/shared 目錄下的檔案結構。</span><span class="sxs-lookup"><span data-stu-id="590d0-408">hello following screenshot shows hello parts of hello file structure under hello /hana/shared directory that SWPM created during hello HANA installation.</span></span> <span data-ttu-id="590d0-409">沒有任何選項 toospecify 不同的路徑，因為它是重要 toomount hello SAP HANA 安裝之前的 hello /hana 目錄下的額外磁碟空間使用 SWPM。</span><span class="sxs-lookup"><span data-stu-id="590d0-409">Because there is no option toospecify a different path, it's important toomount additional disk space under hello /hana directory before hello SAP HANA installation by using SWPM.</span></span> <span data-ttu-id="590d0-410">這樣可避免 hello 根檔案系統用完可用空間。</span><span class="sxs-lookup"><span data-stu-id="590d0-410">This prevents hello root file system from running out of free space.</span></span>

![HANA 安裝期間建立的 hello /hana/shared 目錄檔案結構](./media/hana-get-started/image025.jpg)

<span data-ttu-id="590d0-412">這個螢幕擷取畫面顯示 hello 檔案 hello /usr/sap 目錄結構：</span><span class="sxs-lookup"><span data-stu-id="590d0-412">This screenshot shows hello file structure of hello /usr/sap directory:</span></span>

![hello /usr/sap 目錄檔案結構](./media/hana-get-started/image026.jpg)

<span data-ttu-id="590d0-414">hello hello 分散式 ABAP 安裝最後一個步驟是 tooinstall hello 主要應用程式伺服器執行個體：</span><span class="sxs-lookup"><span data-stu-id="590d0-414">hello last step of hello distributed ABAP installation is tooinstall hello primary application server instance:</span></span>

![ABAP 安裝顯示主要的應用程式伺服器執行個體 hello 最後一個步驟](./media/hana-get-started/image027b.jpg)

<span data-ttu-id="590d0-416">Hello 主要應用程式伺服器執行個體和 SAP GUI 安裝之後，請使用 hello **DBA Cockpit** hello SAP HANA 安裝的交易 tooconfirm 已正確完成：</span><span class="sxs-lookup"><span data-stu-id="590d0-416">After hello primary application server instance and SAP GUI are installed, use hello **DBA Cockpit** transaction tooconfirm that hello SAP HANA installation has finished correctly:</span></span>

![確認安裝成功的 DBA Cockpit 視窗](./media/hana-get-started/image028b.jpg)

<span data-ttu-id="590d0-418">最後一個步驟中，您可能會想 toofirst 安裝 HANA Studio hello SAP 應用程式伺服器 VM，並再連線 toohello hello DB 伺服器 VM 執行的 SAP HANA 執行個體：</span><span class="sxs-lookup"><span data-stu-id="590d0-418">As a final step, you might want toofirst install HANA Studio in hello SAP app server VM, and then connect toohello SAP HANA instance that's running on hello DB server VM:</span></span>

![在 hello SAP 應用程式伺服器 VM 中安裝 SAP HANA Studio](./media/hana-get-started/image038b.jpg)

## <a name="manual-installation-of-sap-hana-hdblcm"></a><span data-ttu-id="590d0-420">手動安裝 SAP HANA：HDBLCM</span><span class="sxs-lookup"><span data-stu-id="590d0-420">Manual installation of SAP HANA: HDBLCM</span></span>
<span data-ttu-id="590d0-421">在加法 tooinstalling 分散式安裝中使用 SWPM 一部分的 SAP HANA，您可以安裝 hello HANA 獨立首先，使用 HDBLCM。</span><span class="sxs-lookup"><span data-stu-id="590d0-421">In addition tooinstalling SAP HANA as part of a distributed installation by using SWPM, you can install hello HANA standalone first, by using HDBLCM.</span></span> <span data-ttu-id="590d0-422">例如，您接著可以安裝 SAP NetWeaver 7.5。</span><span class="sxs-lookup"><span data-stu-id="590d0-422">You can then install SAP NetWeaver 7.5, for example.</span></span> <span data-ttu-id="590d0-423">本節中的 hello 螢幕擷取畫面顯示此程序的運作方式。</span><span class="sxs-lookup"><span data-stu-id="590d0-423">hello screenshots in this section show how this process works.</span></span>

<span data-ttu-id="590d0-424">如需 hello HANA HDBLCM 工具的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="590d0-424">For more information about hello HANA HDBLCM tool, see:</span></span>

* [<span data-ttu-id="590d0-425">選擇 hello 更正您工作的 SAP HANA HDBLCM</span><span class="sxs-lookup"><span data-stu-id="590d0-425">Choosing hello Correct SAP HANA HDBLCM for Your Task</span></span>](https://help.sap.com/saphelp_hanaplatform/helpdata/en/68/5cff570bb745d48c0ab6d50123ca60/content.htm)
* [<span data-ttu-id="590d0-426">SAP HANA 生命週期管理工具</span><span class="sxs-lookup"><span data-stu-id="590d0-426">SAP HANA Lifecycle Management Tools</span></span>](http://saphanatutorial.com/sap-hana-lifecycle-management-tools/)
* [<span data-ttu-id="590d0-427">SAP HANA 伺服器安裝與更新指南</span><span class="sxs-lookup"><span data-stu-id="590d0-427">SAP HANA Server Installation and Update Guide</span></span>](http://help.sap.com/hana/SAP_HANA_Server_Installation_Guide_en.pdf)

<span data-ttu-id="590d0-428">tooavoid 問題，預設值群組識別碼設定 hello `\<HANA SID\>adm user` （hello HDBLCM 工具所建立），定義新的群組稱為`sapsys`使用群組識別碼`1001`安裝 SAP HANA 透過 HDBLCM 之前：</span><span class="sxs-lookup"><span data-stu-id="590d0-428">tooavoid problems with a default group ID setting for hello `\<HANA SID\>adm user` (created by hello HDBLCM tool), define a new group called `sapsys` by using group ID `1001` before you install SAP HANA via HDBLCM:</span></span>

![使用群組識別碼 1001 定義的新群組 "sapsys"](./media/hana-get-started/image030.jpg)

<span data-ttu-id="590d0-430">當您第一次啟動 HDBLCM hello 時，會顯示簡單 [開始] 功能表。</span><span class="sxs-lookup"><span data-stu-id="590d0-430">When you start HDBLCM hello first time, a simple start menu is displayed.</span></span> <span data-ttu-id="590d0-431">選取的項目 1，**安裝新的系統**hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="590d0-431">Select item 1, **Install new system**, as shown in hello following screenshot:</span></span>

![Hello HDBLCM 開始視窗中的 [安裝新的系統] 選項](./media/hana-get-started/image031.jpg)

<span data-ttu-id="590d0-433">hello 下列螢幕擷取畫面會顯示您先前選取所有 hello 金鑰選項。</span><span class="sxs-lookup"><span data-stu-id="590d0-433">hello following screenshot displays all hello key options that you selected previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="590d0-434">目錄會在名為 HANA 記錄檔和資料磁碟區，以及 hello 安裝路徑 （hana/這個範例中為 shared） 和 /usr/sap，不應該 hello 根檔案系統的一部分。</span><span class="sxs-lookup"><span data-stu-id="590d0-434">Directories that are named for HANA log and data volumes, as well as hello installation path (/hana/shared in this sample) and /usr/sap, should not be part of hello root file system.</span></span> <span data-ttu-id="590d0-435">這些目錄屬於 toohello Azure 資料磁碟所連接的 toohello VM （hello 磁碟 < 安裝 > 一節所述）。</span><span class="sxs-lookup"><span data-stu-id="590d0-435">These directories belong toohello Azure data disks that were attached toohello VM (described in hello "Disk setup" section).</span></span> <span data-ttu-id="590d0-436">這種方法可避免用完空間 hello 根檔案系統。</span><span class="sxs-lookup"><span data-stu-id="590d0-436">This approach helps prevent hello root file system from running out of space.</span></span> <span data-ttu-id="590d0-437">在下列螢幕擷取畫面的 hello，您可以看到該 hello HANA 系統管理員具有使用者 ID`1005`屬於 hello`sapsys`群組 (識別碼`1001`)，定義 hello 安裝之前。</span><span class="sxs-lookup"><span data-stu-id="590d0-437">In hello following screenshot, you can see that hello HANA system administrator has user ID `1005` and is part of hello `sapsys` group (ID `1001`) that was defined before hello installation.</span></span>

![先前選取的所有重要 SAP HANA 元件清單](./media/hana-get-started/image032.jpg)

<span data-ttu-id="590d0-439">您可以檢查 hello `\<HANA SID\>adm user` (`azdadm` hello 下列螢幕擷取畫面中) 中目錄 hello /etc/hosts passwd 詳細資料：</span><span class="sxs-lookup"><span data-stu-id="590d0-439">You can check hello `\<HANA SID\>adm user` (`azdadm` in hello following screenshot) details in hello /etc/passwd directory:</span></span>

![HANA \<HANA SID\>adm 使用者詳細資料列在 hello /etc/hosts passwd 目錄](./media/hana-get-started/image033.jpg)

<span data-ttu-id="590d0-441">使用 HDBLCM 安裝 SAP HANA 之後，您可以看到在 SAP HANA Studio 中的 hello 檔案結構，hello 下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="590d0-441">After you install SAP HANA by using HDBLCM, you can see hello file structure in SAP HANA Studio, as shown in hello following screenshot.</span></span> <span data-ttu-id="590d0-442">hello SAPABAP1 結構描述，其中包含所有 hello SAP NetWeaver 資料表，尚無法使用。</span><span class="sxs-lookup"><span data-stu-id="590d0-442">hello SAPABAP1 schema, which includes all hello SAP NetWeaver tables, isn't available yet.</span></span>

![SAP HANA Studio 中的 SAP HANA 檔案結構](./media/hana-get-started/image034.jpg)

<span data-ttu-id="590d0-444">安裝 SAP HANA 之後，就能在其上安裝 SAP NetWeaver。</span><span class="sxs-lookup"><span data-stu-id="590d0-444">After you install SAP HANA, you can install SAP NetWeaver on top of it.</span></span> <span data-ttu-id="590d0-445">下列螢幕擷取畫面所示的 hello，為已做為分散式安裝使用 SWPM （如 hello 前一節中所述） 執行 hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="590d0-445">As shown in hello following screenshot, hello installation was performed as a distributed installation by using SWPM (as described in hello previous section).</span></span> <span data-ttu-id="590d0-446">當您使用 SWPM 安裝 hello 資料庫執行個體時，您會輸入 hello 使用 HDBLCM （例如，主機名稱、 HANA SID 和執行個體號碼） 相同的資料。</span><span class="sxs-lookup"><span data-stu-id="590d0-446">When you install hello database instance by using SWPM, you enter hello same data by using HDBLCM (for example, host name, HANA SID, and instance number).</span></span> <span data-ttu-id="590d0-447">SWPM 然後使用 hello 現有 HANA 安裝，並加入更多結構描述。</span><span class="sxs-lookup"><span data-stu-id="590d0-447">SWPM then uses hello existing HANA installation and adds more schemas.</span></span>

![使用 SWPM 執行分散式安裝](./media/hana-get-started/image035b.jpg)

<span data-ttu-id="590d0-449">hello 下列螢幕擷取畫面顯示 hello SWPM 安裝步驟，您輸入 hello DBACOCKPIT 結構描述相關的資料：</span><span class="sxs-lookup"><span data-stu-id="590d0-449">hello following screenshot shows hello SWPM installation step where you enter data about hello DBACOCKPIT schema:</span></span>

![其中輸入 DBACOCKPIT 結構描述資料 hello SWPM 安裝步驟](./media/hana-get-started/image036b.jpg)

<span data-ttu-id="590d0-451">輸入 hello SAPABAP1 結構描述相關的資料：</span><span class="sxs-lookup"><span data-stu-id="590d0-451">Enter data about hello SAPABAP1 schema:</span></span>

![輸入 hello SAPABAP1 結構描述相關的資料](./media/hana-get-started/image037b.jpg)

<span data-ttu-id="590d0-453">Hello SWPM 資料庫執行個體安裝完成之後，您可以看到在 SAP HANA Studio 中的 hello SAPABAP1 結構描述：</span><span class="sxs-lookup"><span data-stu-id="590d0-453">After hello SWPM database instance installation is completed, you can see hello SAPABAP1 schema in SAP HANA Studio:</span></span>

![SAP HANA Studio 中的 hello SAPABAP1 結構描述](./media/hana-get-started/image038b.jpg)

<span data-ttu-id="590d0-455">最後，hello SAP 應用程式伺服器和 SAP GUI 安裝完成之後，您可以確認 hello HANA 資料庫執行個體使用 hello **DBA Cockpit**交易：</span><span class="sxs-lookup"><span data-stu-id="590d0-455">Finally, after hello SAP app server and SAP GUI installations are completed, you can verify hello HANA DB instance by using hello **DBA Cockpit** transaction:</span></span>

![DBA Cockpit 交易 hello hello HANA 資料庫執行個體驗證](./media/hana-get-started/image039b.jpg)


## <a name="sap-software-downloads"></a><span data-ttu-id="590d0-457">SAP 軟體下載</span><span class="sxs-lookup"><span data-stu-id="590d0-457">SAP software downloads</span></span>
<span data-ttu-id="590d0-458">您可以從 hello SAP 服務商場，下載軟體，hello 下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="590d0-458">You can download software from hello SAP Service Marketplace, as shown in hello following screenshots.</span></span>

<span data-ttu-id="590d0-459">下載適用於 Linux/HANA 的 NetWeaver 7.5：</span><span class="sxs-lookup"><span data-stu-id="590d0-459">Download NetWeaver 7.5 for Linux/HANA:</span></span>

 ![用於下載 NetWeaver 7.5 的 SAP 服務安裝和升級視窗](./media/hana-get-started/image001.jpg)

<span data-ttu-id="590d0-461">下載 HANA SP12 平台版本：</span><span class="sxs-lookup"><span data-stu-id="590d0-461">Download HANA SP12 Platform Edition:</span></span>

 ![用於下載 HANA SP12 平台版本的 SAP 服務安裝和升級視窗](./media/hana-get-started/image002.jpg)


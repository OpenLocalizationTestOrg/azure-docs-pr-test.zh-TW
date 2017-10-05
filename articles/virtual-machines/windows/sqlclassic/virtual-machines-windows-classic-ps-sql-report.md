---
title: "使用 PowerShell 建立具有原生模式報表伺服器的 VM | Microsoft Docs"
description: "本主題說明並逐步引導您在 Azure 虛擬機器中，部署並設定 SQL Server Reporting Services 原生模式報表伺服器。 "
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: 5e5c11251cd316e8161dbe362b300be76927ac01
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-create-an-azure-vm-with-a-native-mode-report-server"></a><span data-ttu-id="d2494-103">使用 PowerShell 建立具有原生模式報表伺服器的 Azure VM</span><span class="sxs-lookup"><span data-stu-id="d2494-103">Use PowerShell to Create an Azure VM With a Native Mode Report Server</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="d2494-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="d2494-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d2494-105">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="d2494-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="d2494-106">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="d2494-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="d2494-107">本主題說明並逐步引導您在 Azure 虛擬機器中，部署並設定 SQL Server Reporting Services 原生模式報表伺服器。</span><span class="sxs-lookup"><span data-stu-id="d2494-107">This topic describes and walks you through the deployment and configuration of a SQL Server Reporting Services native mode report server in an Azure Virtual Machine.</span></span> <span data-ttu-id="d2494-108">本文件的步驟採用一連串手動步驟的組合建立虛擬機器，並使用 Windows PowerShell 指令碼設定 VM 上的 Reporting Services。</span><span class="sxs-lookup"><span data-stu-id="d2494-108">The steps in this document use a combination of manual steps to create the virtual machine and a Windows PowerShell script to configure Reporting Services on the VM.</span></span> <span data-ttu-id="d2494-109">組態指令碼包含針對 HTTP 或 HTTPS 開啟防火牆連接埠。</span><span class="sxs-lookup"><span data-stu-id="d2494-109">The configuration script includes opening a firewall port for HTTP or HTTPs.</span></span>

> [!NOTE]
> <span data-ttu-id="d2494-110">如果報表伺服器不需要 **HTTPS**，請**略過步驟 2**。</span><span class="sxs-lookup"><span data-stu-id="d2494-110">If you do not require **HTTPS** on the report server, **skip step 2**.</span></span>
> 
> <span data-ttu-id="d2494-111">在步驟 1 建立 VM 之後，請移至＜使用指令碼設定報表伺服器和 HTTP＞一節。</span><span class="sxs-lookup"><span data-stu-id="d2494-111">After creating the VM in step 1, go to the section Use script to configure the report server and HTTP.</span></span> <span data-ttu-id="d2494-112">執行指令碼之後，就可以使用報表伺服器。</span><span class="sxs-lookup"><span data-stu-id="d2494-112">After you run the script, the report server is ready to use.</span></span>

## <a name="prerequisites-and-assumptions"></a><span data-ttu-id="d2494-113">必要條件與假設</span><span class="sxs-lookup"><span data-stu-id="d2494-113">Prerequisites and Assumptions</span></span>
* <span data-ttu-id="d2494-114">**Azure 訂用帳戶**：確認您的 Azure 訂用帳戶中可用的核心數量。</span><span class="sxs-lookup"><span data-stu-id="d2494-114">**Azure Subscription**: Verify the number of cores available in your Azure Subscription.</span></span> <span data-ttu-id="d2494-115">若要建立建議的 VM 大小 **A3**，將需要 **4** 個可用的核心。</span><span class="sxs-lookup"><span data-stu-id="d2494-115">If you create the recommended VM size of **A3**, you need **4** available cores.</span></span> <span data-ttu-id="d2494-116">若您採用 **A2** 的 VM 大小，則需要 **2** 個可用的核心。</span><span class="sxs-lookup"><span data-stu-id="d2494-116">If you use a VM size of **A2**, you need **2** available cores.</span></span>
  
  * <span data-ttu-id="d2494-117">若要確認訂用帳戶的核心限制，請在 Azure 傳統入口網站中按一下左窗格中的 [設定]，然後按一下上層功能表中的 [使用方式]。</span><span class="sxs-lookup"><span data-stu-id="d2494-117">To verify the core limit of your subscription, in the Azure classic portal, click SETTINGS in the left pane and then Click USAGE in the top menu.</span></span>
  * <span data-ttu-id="d2494-118">若要增加核心配額，請連絡 [Azure 支援](https://azure.microsoft.com/support/options/)。</span><span class="sxs-lookup"><span data-stu-id="d2494-118">To increase the core quota, contact [Azure Support](https://azure.microsoft.com/support/options/).</span></span> <span data-ttu-id="d2494-119">如需 VM 大小的資訊，請參閱 [Azure 的虛擬機器大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d2494-119">For VM size information, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="d2494-120">**Windows PowerShell 指令碼**：本主題假設您對 Windows PowerShell 已有基本的技術知識。</span><span class="sxs-lookup"><span data-stu-id="d2494-120">**Windows PowerShell Scripting**: The topic assumes that you have a basic working knowledge of Windows PowerShell.</span></span> <span data-ttu-id="d2494-121">如需有關如何使用 Windows PowerShell 的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="d2494-121">For more information about using Windows PowerShell, see the following:</span></span>
  
  * [<span data-ttu-id="d2494-122">在 Windows Server 上啟動 Windows PowerShell (英文)</span><span class="sxs-lookup"><span data-stu-id="d2494-122">Starting Windows PowerShell on Windows Server</span></span>](https://technet.microsoft.com/library/hh847814.aspx)
  * [<span data-ttu-id="d2494-123">開始使用 Windows PowerShell (英文)</span><span class="sxs-lookup"><span data-stu-id="d2494-123">Getting Started with Windows PowerShell</span></span>](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a><span data-ttu-id="d2494-124">步驟 1：佈建 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d2494-124">Step 1: Provision an Azure Virtual Machine</span></span>
1. <span data-ttu-id="d2494-125">瀏覽到 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="d2494-125">Browse to the Azure classic portal.</span></span>
2. <span data-ttu-id="d2494-126">按一下左窗格中的 [虛擬機器]  。</span><span class="sxs-lookup"><span data-stu-id="d2494-126">Click **Virtual Machines** in the left pane.</span></span>
   
    ![Microsoft Azure 虛擬機器](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. <span data-ttu-id="d2494-128">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="d2494-128">Click **New**.</span></span>
   
    ![新增按鈕](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. <span data-ttu-id="d2494-130">按一下 [從資源庫] 。</span><span class="sxs-lookup"><span data-stu-id="d2494-130">Click **From Gallery**.</span></span>
   
    ![從資源庫新增 VM](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. <span data-ttu-id="d2494-132">按一下 [SQL Server 2014 RTM Standard – Windows Server 2012 R2]  ，然後按一下箭頭以繼續。</span><span class="sxs-lookup"><span data-stu-id="d2494-132">Click **SQL Server 2014 RTM Standard – Windows Server 2012 R2** and then click the arrow to continue.</span></span>
   
    ![下一步](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    <span data-ttu-id="d2494-134">如果您需要 Reporting Services 資料驅動的訂用帳戶功能，請選擇 [SQL Server 2014 RTM Enterprise – Windows Server 2012 R2] 。</span><span class="sxs-lookup"><span data-stu-id="d2494-134">If you need the Reporting Services data driven subscriptions feature, choose **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span></span> <span data-ttu-id="d2494-135">如需有關 SQL Server 版本及功能支援的詳細資訊，請參閱 [SQL Server 2012 版本支援的功能](https://msdn.microsoft.com/library/cc645993.aspx#Reporting)。</span><span class="sxs-lookup"><span data-stu-id="d2494-135">For more information on SQL Server editions and feature support, see [Features Supported by the Editions of SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span></span>
6. <span data-ttu-id="d2494-136">在 [虛擬機器組態]  頁面中，編輯下列欄位：</span><span class="sxs-lookup"><span data-stu-id="d2494-136">On the **Virtual machine configuration** page, edit the following fields:</span></span>
   
   * <span data-ttu-id="d2494-137">如果有多個 [版本發行日期] ，請選取最新版本。</span><span class="sxs-lookup"><span data-stu-id="d2494-137">If there is more than one **VERSION RELEASE DATE**, select the most recent version.</span></span>
   * <span data-ttu-id="d2494-138">[虛擬機器名稱]：下一個組態頁面中也使用此機器名稱，作為預設的雲端服務 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="d2494-138">**Virtual Machine Name**: The machine name is also used on the next configuration page as the default Cloud Service DNS name.</span></span> <span data-ttu-id="d2494-139">DNS 名稱在 Azure 服務中必須是獨一無二的。</span><span class="sxs-lookup"><span data-stu-id="d2494-139">The DNS name must be unique across the Azure service.</span></span> <span data-ttu-id="d2494-140">請考慮以能夠描述 VM 用途的電腦名稱命名 VM。</span><span class="sxs-lookup"><span data-stu-id="d2494-140">Consider configuring the VM with a computer name that describes what the VM is used for.</span></span> <span data-ttu-id="d2494-141">例如 ssrsnativecloud。</span><span class="sxs-lookup"><span data-stu-id="d2494-141">For example ssrsnativecloud.</span></span>
   * <span data-ttu-id="d2494-142">[層]：標準</span><span class="sxs-lookup"><span data-stu-id="d2494-142">**Tier**: Standard</span></span>
   * <span data-ttu-id="d2494-143"> 是建議 SQL Server 工作負載採用的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="d2494-143">**Size:A3** is the recommended VM size for SQL Server workloads.</span></span> <span data-ttu-id="d2494-144">若 VM 只作為報表伺服器使用，那麼除非報表伺服器需處理大量的工作負載，否則 A2 的 VM 大小就已經足夠。</span><span class="sxs-lookup"><span data-stu-id="d2494-144">If a VM is only used as a report server, a VM size of A2 is sufficient unless the report server experiences a large workload.</span></span> <span data-ttu-id="d2494-145">如需 VM 的價格資訊，請參閱 [虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/)。</span><span class="sxs-lookup"><span data-stu-id="d2494-145">For VM pricing information, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
   * <span data-ttu-id="d2494-146">[新的使用者名稱]：系統會使用您提供的名稱建立 VM 上的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="d2494-146">**New User Name**: the name you provide is created as an administrator on the VM.</span></span>
   * <span data-ttu-id="d2494-147">[新增密碼] 並**確認**。</span><span class="sxs-lookup"><span data-stu-id="d2494-147">**New Password** and **confirm**.</span></span> <span data-ttu-id="d2494-148">此密碼將用於新的系統管理員帳戶，因此建議您使用強式密碼。</span><span class="sxs-lookup"><span data-stu-id="d2494-148">This password is used for the new administrator account and it is recommended you use a strong password.</span></span>
   * <span data-ttu-id="d2494-149">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="d2494-149">Click **Next**.</span></span> <span data-ttu-id="d2494-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span><span class="sxs-lookup"><span data-stu-id="d2494-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span></span>
7. <span data-ttu-id="d2494-151">在下一個頁面中，編輯下列欄位：</span><span class="sxs-lookup"><span data-stu-id="d2494-151">On the next page, edit the following fields:</span></span>
   
   * <span data-ttu-id="d2494-152">[雲端服務]：選取 [建立新的雲端服務]。</span><span class="sxs-lookup"><span data-stu-id="d2494-152">**Cloud Service**: select **Create a new Cloud Service**.</span></span>
   * <span data-ttu-id="d2494-153">[雲端服務 DNS 名稱]：這是與 VM 相關聯的雲端服務的公用 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="d2494-153">**Cloud Service DNS Name**: This is the public DNS name of the Cloud Service that is associated with the VM.</span></span> <span data-ttu-id="d2494-154">預設名稱就是您為 VM 名稱鍵入的名稱。</span><span class="sxs-lookup"><span data-stu-id="d2494-154">The default name is the name you typed in for the VM name.</span></span> <span data-ttu-id="d2494-155">如果您在本主題的後續步驟中建立信任的 SSL 憑證，系統會將 DNS 名稱作為該憑證的 [核發給]值。</span><span class="sxs-lookup"><span data-stu-id="d2494-155">If in later steps of the topic, you create a trusted SSL certificate and then the DNS name is used for the value of the “**Issued to**” of the certificate.</span></span>
   * <span data-ttu-id="d2494-156">[區域/同質群組/虛擬網路]：選擇最靠近您使用者的區域。</span><span class="sxs-lookup"><span data-stu-id="d2494-156">**Region/Affinity Group/Virtual Network**: Choose the region closest to your end users.</span></span>
   * <span data-ttu-id="d2494-157">[儲存體帳戶]：使用自動產生的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d2494-157">**Storage Account**: Use an automatically generated storage account.</span></span>
   * <span data-ttu-id="d2494-158">[可用性設定組]：無。</span><span class="sxs-lookup"><span data-stu-id="d2494-158">**Availability Set**: None.</span></span>
   * <span data-ttu-id="d2494-159">[端點]：保留 [遠端桌面] 和 [PowerShell] 端點，然後根據您的環境新增 HTTP 或 HTTPS 端點。</span><span class="sxs-lookup"><span data-stu-id="d2494-159">**ENDPOINTS** Keep the **Remote Desktop** and **PowerShell** endpoints and then add either an HTTP or HTTPS endpoint, depending on your environment.</span></span>
     
     * <span data-ttu-id="d2494-160">[HTTP]：預設的公用和私人連接埠都是 **80**。</span><span class="sxs-lookup"><span data-stu-id="d2494-160">**HTTP**: The default public and private ports are **80**.</span></span> <span data-ttu-id="d2494-161">請注意，如果您使用的私人連接埠不是 80，請修改 http 指令碼中的 **$HTTPport = 80** 。</span><span class="sxs-lookup"><span data-stu-id="d2494-161">Note that if you use a private port other than 80, modify **$HTTPport = 80** in the http script.</span></span>
     * <span data-ttu-id="d2494-162">[HTTPS]：預設的公用和私人連接埠都是 **443**。</span><span class="sxs-lookup"><span data-stu-id="d2494-162">**HTTPS**: The default public and private ports are **443**.</span></span> <span data-ttu-id="d2494-163">安全性最佳作法就是變更私用連接埠，並將防火牆和報表伺服器設為使用私用連接埠。</span><span class="sxs-lookup"><span data-stu-id="d2494-163">A security best practice is to change the private port and configure your firewall and the report server to use the private port.</span></span> <span data-ttu-id="d2494-164">如需有關端點的詳細資訊，請參閱 [如何設定與虛擬機器的通訊](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d2494-164">For more information on endpoints, see [How to Set Up Communication with a Virtual Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="d2494-165">請注意，如果您使用的連接埠不是 443，請變更 HTTPS 指令碼中的 **$HTTPsport = 443** 參數。</span><span class="sxs-lookup"><span data-stu-id="d2494-165">Note that if you use a port other than 443, change the parameter **$HTTPsport = 443** in the HTTPS script.</span></span>
   * <span data-ttu-id="d2494-166">按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d2494-166">Click next .</span></span> ![下一步](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. <span data-ttu-id="d2494-168">在精靈的最後一頁，保持選取預設值 [安裝 VM 代理程式]  。</span><span class="sxs-lookup"><span data-stu-id="d2494-168">On the last page of the wizard, keep the default **Install the VM agent** selected.</span></span> <span data-ttu-id="d2494-169">本主題的步驟不會使用 VM 代理程式，但若您打算保留此 VM，VM 代理程式和延伸模組可讓您增強 CM。</span><span class="sxs-lookup"><span data-stu-id="d2494-169">The steps in this topic do not utilize the VM agent but if you plan to keep this VM, the VM agent and extensions will allow you to enhance he CM.</span></span>  <span data-ttu-id="d2494-170">如需有關 VM 代理程式的詳細資訊，請參閱 [VM 代理程式和延伸模組 – 第 1 部分](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/)。</span><span class="sxs-lookup"><span data-stu-id="d2494-170">For more information on the VM agent, see [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span></span> <span data-ttu-id="d2494-171">其中一個已安裝並執行的預設延伸模組是「BGINFO」延伸模組，它會在 VM 桌面上顯示系統資訊，例如內部 IP 和可用磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="d2494-171">One of the default extensions installed ad running is the “BGINFO” extension that displays on the VM desktop, system information such as internal IP and free drive space.</span></span>
9. <span data-ttu-id="d2494-172">按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="d2494-172">Click complete .</span></span> ![Ok](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. <span data-ttu-id="d2494-174">VM 的 [狀態] 在佈建程序進行期間會顯示為 [啟動中 (佈建中)]，然後在 VM 已佈建完成，可供使用時顯示為 [正在執行]。</span><span class="sxs-lookup"><span data-stu-id="d2494-174">The **Status** of the VM displays as **Starting (Provisioning)** during the provision process and then displays as **Running** when the VM is provisioned and ready to use.</span></span>

## <a name="step-2-create-a-server-certificate"></a><span data-ttu-id="d2494-175">步驟 2：建立伺服器憑證</span><span class="sxs-lookup"><span data-stu-id="d2494-175">Step 2: Create a Server Certificate</span></span>
> [!NOTE]
> <span data-ttu-id="d2494-176">如果報表伺服器不需要 HTTPS，可以**略過步驟 2**，並移至**使用指令碼設定報表伺服器和 HTTP** 一節。</span><span class="sxs-lookup"><span data-stu-id="d2494-176">If you do not require HTTPS on the report server, you can **skip step 2** and go to the section **Use script to configure the report server and HTTP**.</span></span> <span data-ttu-id="d2494-177">透過 HTTP 指令碼快速設定報表伺服器，報表伺服器即可供使用。</span><span class="sxs-lookup"><span data-stu-id="d2494-177">Use the HTTP script to quickly configure the report server and the report server will be ready to use.</span></span>

<span data-ttu-id="d2494-178">您需要信任的 SSL 憑證，才能在 VM 上使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="d2494-178">In order to use HTTPS on the VM, you need a trusted SSL certificate.</span></span> <span data-ttu-id="d2494-179">您可以根據您的情況，使用下列其中一種方法：</span><span class="sxs-lookup"><span data-stu-id="d2494-179">Depending on your scenario, you can use one of the following two methods:</span></span>

* <span data-ttu-id="d2494-180">由憑證授權單位 (CA) 核發，且受到 Microsoft 信任的有效 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="d2494-180">A valid SSL certificate issued by a Certification Authority (CA) and trusted by Microsoft.</span></span> <span data-ttu-id="d2494-181">CA 根憑證必須透過 Microsoft 根憑證計劃散發。</span><span class="sxs-lookup"><span data-stu-id="d2494-181">The CA root certificates are required to be distributed via the Microsoft Root Certificate Program.</span></span> <span data-ttu-id="d2494-182">如需有關此計劃的詳細資訊，請參閱 [Windows 和 Windows Phone 8 SSL 根憑證計劃 (成員 CA)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx)，以及 [Microsoft 根憑證計劃簡介](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d2494-182">For more information about this program, see [Windows and Windows Phone 8 SSL Root Certificate Program (Member CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) and [Introduction to The Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span></span>
* <span data-ttu-id="d2494-183">自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="d2494-183">A self-signed certificate.</span></span> <span data-ttu-id="d2494-184">不建議將自我簽署憑證用於生產環境。</span><span class="sxs-lookup"><span data-stu-id="d2494-184">Self-signed certificates are not recommended for production environments.</span></span>

### <a name="to-use-a-certificate-created-by-a-trusted-certificate-authority-ca"></a><span data-ttu-id="d2494-185">使用由信任的憑證授權單位 (CA) 所建立的憑證</span><span class="sxs-lookup"><span data-stu-id="d2494-185">To use a certificate created by a trusted Certificate Authority (CA)</span></span>
1. <span data-ttu-id="d2494-186">**針對網站向憑證授權單位要求伺服器憑證**。</span><span class="sxs-lookup"><span data-stu-id="d2494-186">**Request a server certificate for the website from a certification authority**.</span></span> 
   
    <span data-ttu-id="d2494-187">您可以使用 Web 伺服器憑證精靈，產生傳送至憑證授權單位的憑證要求檔案 (Certreq.txt)，或產生給線上憑證授權單位的要求。</span><span class="sxs-lookup"><span data-stu-id="d2494-187">You can use the Web Server Certificate Wizard either to generate a certificate request file (Certreq.txt) that you send to a certification authority, or to generate a request for an online certification authority.</span></span> <span data-ttu-id="d2494-188">例如 Windows Server 2012 中的 Microsoft Certificate Services。</span><span class="sxs-lookup"><span data-stu-id="d2494-188">For example, Microsoft Certificate Services in Windows Server 2012.</span></span> <span data-ttu-id="d2494-189">視您伺服器憑證提供的識別保證層級而定，憑證授權單位核准您的要求並將憑證檔案傳送給您的時間，可能需要幾天或幾個月。</span><span class="sxs-lookup"><span data-stu-id="d2494-189">Depending on the level of identification assurance offered by your server certificate, it is several days to several months for the certification authority to approve your request and send you a certificate file.</span></span> 
   
    <span data-ttu-id="d2494-190">如需有關如何要求伺服器憑證的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="d2494-190">For more information about requesting a server certificates, see the following:</span></span> 
   
   * <span data-ttu-id="d2494-191">使用 [Certreq](https://technet.microsoft.com/library/cc725793.aspx)、[Certreq](https://technet.microsoft.com/library/cc725793.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d2494-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span></span>
   * <span data-ttu-id="d2494-192">管理 Windows Server 2012 的安全性工具 (英文)。</span><span class="sxs-lookup"><span data-stu-id="d2494-192">Security Tools to Administer Windows Server 2012.</span></span>
     
     [<span data-ttu-id="d2494-193">管理 Windows Server 2012 的安全性工具 (英文)</span><span class="sxs-lookup"><span data-stu-id="d2494-193">Security Tools to Administer Windows Server 2012</span></span>](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > <span data-ttu-id="d2494-194">信任的 SSL 憑證的 [核發給] 欄位應該與新 VM 的 [雲端服務 DNS 名稱] 相同。</span><span class="sxs-lookup"><span data-stu-id="d2494-194">The **issued to** field of the trusted SSL certificate should be the same as the **Cloud Service DNS NAME** you used for the new VM.</span></span>

2. <span data-ttu-id="d2494-195">**在 Web 伺服器上安裝伺服器憑證**。</span><span class="sxs-lookup"><span data-stu-id="d2494-195">**Install the server certificate on the Web server**.</span></span> <span data-ttu-id="d2494-196">此案例中的 Web 伺服器是作為裝載報表伺服器的 VM，而我們會在後面設定 Reporting Services 的步驟中建立網站。</span><span class="sxs-lookup"><span data-stu-id="d2494-196">The Web server in this case is the VM that hosts the report server and the website is created in later steps when you configure Reporting Services.</span></span> <span data-ttu-id="d2494-197">如需有關如何使用憑證 MMC 嵌入式管理單元，在 Web 伺服器上安裝伺服器憑證的詳細資訊，請參閱 [安裝伺服器憑證](https://technet.microsoft.com/library/cc740068)。</span><span class="sxs-lookup"><span data-stu-id="d2494-197">For more information about installing the server certificate on the Web server by using the Certificate MMC snap-in, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
    <span data-ttu-id="d2494-198">若您要使用本主題中的指令碼設定報表伺服器，需將 [指紋]  憑證的值做為指令碼的參數。</span><span class="sxs-lookup"><span data-stu-id="d2494-198">If you want to use the script included with this topic, to configure the report server, the value of the certificates **Thumbprint** is required as a parameter of the script.</span></span> <span data-ttu-id="d2494-199">有關如何取得憑證指紋的詳細資料，請參閱下一節。</span><span class="sxs-lookup"><span data-stu-id="d2494-199">See the next section for details on how to obtain the thumbprint of the certificate.</span></span>
3. <span data-ttu-id="d2494-200">將伺服器憑證指派給報表伺服器。</span><span class="sxs-lookup"><span data-stu-id="d2494-200">Assign the server certificate to the report server.</span></span> <span data-ttu-id="d2494-201">當您在下一節設定報表伺服器時，便會完成指派。</span><span class="sxs-lookup"><span data-stu-id="d2494-201">The assignment is completed in the next section when you configure the report server.</span></span>

### <a name="to-use-the-virtual-machines-self-signed-certificate"></a><span data-ttu-id="d2494-202">使用虛擬機器的自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="d2494-202">To use the Virtual Machines Self-signed Certificate</span></span>
<span data-ttu-id="d2494-203">佈建 VM 時，會在 VM 上建立自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="d2494-203">A self-signed certificate was created on the VM when the VM was provisioned.</span></span> <span data-ttu-id="d2494-204">憑證名稱與 VM DNS 名稱相同。</span><span class="sxs-lookup"><span data-stu-id="d2494-204">The certificate has the same name as the VM DNS name.</span></span> <span data-ttu-id="d2494-205">為了避免憑證錯誤，VM 本身以及網站的所有使用者都必須信任憑證。</span><span class="sxs-lookup"><span data-stu-id="d2494-205">In order to avoid certificate errors, it is required that the certificate is trusted on the VM itself, and also by all users of the site.</span></span>

1. <span data-ttu-id="d2494-206">若要信任本機 VM 的憑證根 CA，請將憑證新增至 [信任的根憑證授權單位] 。</span><span class="sxs-lookup"><span data-stu-id="d2494-206">To trust the root CA of the certificate on the Local VM, add the certificate to the **Trusted Root Certification Authorities**.</span></span> <span data-ttu-id="d2494-207">以下是所需步驟的摘要。</span><span class="sxs-lookup"><span data-stu-id="d2494-207">The following is a summary of the steps required.</span></span> <span data-ttu-id="d2494-208">如需有關如何信任 CA 的詳細步驟，請參閱 [安裝伺服器憑證](https://technet.microsoft.com/library/cc740068)。</span><span class="sxs-lookup"><span data-stu-id="d2494-208">For detailed steps on how to trust the CA, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
   1. <span data-ttu-id="d2494-209">在 Azure 傳統入口網站中選取 VM，然後按一下 [連接]。</span><span class="sxs-lookup"><span data-stu-id="d2494-209">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="d2494-210">根據您的瀏覽器設定，可能會提示您儲存 .rdp 檔案以連接至 VM。</span><span class="sxs-lookup"><span data-stu-id="d2494-210">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
      
       ![連接至 Azure 虛擬機器](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="d2494-212">請使用您建立 VM 時所設定的使用者 VM 名稱、使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="d2494-212">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
      
       <span data-ttu-id="d2494-213">例如，下圖的 VM 名稱是 **ssrsnativecloud**，而使用者名稱是 **testuser**。</span><span class="sxs-lookup"><span data-stu-id="d2494-213">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
      
       ![登入包括 VM 名稱](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. <span data-ttu-id="d2494-215">執行 mmc.exe。</span><span class="sxs-lookup"><span data-stu-id="d2494-215">Run mmc.exe.</span></span> <span data-ttu-id="d2494-216">如需詳細資訊，請參閱 [做法：使用 MMC 嵌入式管理單元檢視憑證](https://msdn.microsoft.com/library/ms788967.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d2494-216">For more information, see [How to: View Certificates with the MMC Snap-in](https://msdn.microsoft.com/library/ms788967.aspx).</span></span>
   3. <span data-ttu-id="d2494-217">在主控台應用程式的 [檔案] 功能表中，新增 [憑證] 嵌入式管理單元，在系統提示時選取 [電腦帳戶]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d2494-217">In the console application **File** menu, add the **Certificates** snap-in, select **Computer Account** when prompted, and then click **Next**.</span></span>
   4. <span data-ttu-id="d2494-218">選取要管理的 [本機電腦]，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="d2494-218">Select **Local Computer** to manage and then click **Finish**.</span></span>
   5. <span data-ttu-id="d2494-219">按一下 [確認]，展開 [憑證 - 個人] 節點，然後按一下 [憑證]。</span><span class="sxs-lookup"><span data-stu-id="d2494-219">Click **Ok** and then expand the **Certificates -Personal** nodes and then click **Certificates**.</span></span> <span data-ttu-id="d2494-220">憑證是以 VM 的 DNS 名稱來命名，並以**cloudapp.net** 結尾。</span><span class="sxs-lookup"><span data-stu-id="d2494-220">The certificate is named after the DNS name of the VM and ends with **cloudapp.net**.</span></span> <span data-ttu-id="d2494-221">以滑鼠右鍵按一下憑證名稱，並按一下 [複製]。</span><span class="sxs-lookup"><span data-stu-id="d2494-221">Right-click the certificate name and click **Copy**.</span></span>
   6. <span data-ttu-id="d2494-222">展開 [信任的根憑證授權] 節點，接著以滑鼠右鍵按一下 [憑證]，然後按一下 [貼上]。</span><span class="sxs-lookup"><span data-stu-id="d2494-222">Expand the **Trusted Root Certification Authorities** node and then right-click **Certificates** and then click **Paste**.</span></span>
   7. <span data-ttu-id="d2494-223">若要驗證，請按兩下 [信任的根憑證授權]  下的憑證名稱，確認沒有任何錯誤，且您能看到您的憑證。</span><span class="sxs-lookup"><span data-stu-id="d2494-223">To validate, double click on the certificate name under **Trusted Root Certification Authorities** and verify that there are no errors and you see your certificate.</span></span> <span data-ttu-id="d2494-224">若您要使用本主題中的 HTTPS 指令碼設定報表伺服器，需將 [指紋] 憑證的值作為指令碼的參數。</span><span class="sxs-lookup"><span data-stu-id="d2494-224">If you want to use the HTTPS script included with this topic, to configure the report server, the value of the certificates **Thumbprint** is required as a parameter of the script.</span></span> <span data-ttu-id="d2494-225">**若要取得憑證指紋值**，請完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="d2494-225">**To get the thumbprint value**, complete the following.</span></span> <span data-ttu-id="d2494-226">在[使用指令碼設定報表伺服器和 HTTPS](#use-script-to-configure-the-report-server-and-HTTPS)一節中，還有可擷取憑證指紋的 PowerShell 範例。</span><span class="sxs-lookup"><span data-stu-id="d2494-226">There is also a PowerShell sample to retrieve the thumbprint in section [Use script to configure the report server and HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span></span>
      
      1. <span data-ttu-id="d2494-227">按兩下憑證名稱，例如 ssrsnativecloud.cloudapp.net。</span><span class="sxs-lookup"><span data-stu-id="d2494-227">Double-click the name of the certificate, for example ssrsnativecloud.cloudapp.net.</span></span>
      2. <span data-ttu-id="d2494-228">按一下 [詳細資料]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d2494-228">Click the **Details** tab.</span></span>
      3. <span data-ttu-id="d2494-229">按一下 [指紋] 。</span><span class="sxs-lookup"><span data-stu-id="d2494-229">Click **Thumbprint**.</span></span> <span data-ttu-id="d2494-230">憑證指紋的值會顯示在 [詳細資料] 欄位中，例如 ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f。</span><span class="sxs-lookup"><span data-stu-id="d2494-230">The value of the thumbprint is displayed in the details field, for example ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span></span>
      4. <span data-ttu-id="d2494-231">複製憑證指紋並儲存其值，即可在稍後或現在編輯指令碼。</span><span class="sxs-lookup"><span data-stu-id="d2494-231">Copy the thumbprint and save the value for later or edit the script now.</span></span>
      5. <span data-ttu-id="d2494-232">(*) 執行指令碼之前，請先移除每一組值之間的空格。</span><span class="sxs-lookup"><span data-stu-id="d2494-232">(*) Before you run the script, remove the spaces in between the pairs of values.</span></span> <span data-ttu-id="d2494-233">例如，之前記下的憑證指紋會成為 a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f。</span><span class="sxs-lookup"><span data-stu-id="d2494-233">For example the thumbprint noted before would now be ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span></span>
      6. <span data-ttu-id="d2494-234">將伺服器憑證指派給報表伺服器。</span><span class="sxs-lookup"><span data-stu-id="d2494-234">Assign the server certificate to the report server.</span></span> <span data-ttu-id="d2494-235">當您在下一節設定報表伺服器時，便會完成指派。</span><span class="sxs-lookup"><span data-stu-id="d2494-235">The assignment is completed in the next section when you configure the report server.</span></span>

<span data-ttu-id="d2494-236">如果您使用自我簽署 SSL 憑證，則憑證的名稱已經符合 VM 的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="d2494-236">If you are using a self-signed SSL certificate, the name on the certificate already matches the hostname of the VM.</span></span> <span data-ttu-id="d2494-237">因此，機器的 DNS 已在全域註冊，且可從任何用戶端存取。</span><span class="sxs-lookup"><span data-stu-id="d2494-237">Therefore, the DNS of the machine is already registered globally and can be accessed from any client.</span></span>

## <a name="step-3-configure-the-report-server"></a><span data-ttu-id="d2494-238">步驟 3：設定報表伺服器</span><span class="sxs-lookup"><span data-stu-id="d2494-238">Step 3: Configure the Report Server</span></span>
<span data-ttu-id="d2494-239">本節將引導您把 VM 設為 Reporting Services 原生模式報表伺服器。</span><span class="sxs-lookup"><span data-stu-id="d2494-239">This section walks you through configuring the VM as a Reporting Services native mode report server.</span></span> <span data-ttu-id="d2494-240">您可以使用下列方法之一來設定報表伺服器：</span><span class="sxs-lookup"><span data-stu-id="d2494-240">You can use one of the following methods to configure the report server:</span></span>

* <span data-ttu-id="d2494-241">使用指令碼設定報表伺服器</span><span class="sxs-lookup"><span data-stu-id="d2494-241">Use the script to configure the report server</span></span>
* <span data-ttu-id="d2494-242">使用組態管理員設定報表伺服器。</span><span class="sxs-lookup"><span data-stu-id="d2494-242">Use Configuration Manager to Configure the Report Server.</span></span>

<span data-ttu-id="d2494-243">更詳細的步驟請參閱 [連接到虛擬機器並啟動 Reporting Services 組態管理員](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager)一節。</span><span class="sxs-lookup"><span data-stu-id="d2494-243">For more detailed steps, see the section [Connect to the Virtual Machine and Start the Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span></span>

<span data-ttu-id="d2494-244">**驗證注意事項：** 建議的驗證方法是 Windows 驗證，它也是預設的 Reporting Services 驗證。</span><span class="sxs-lookup"><span data-stu-id="d2494-244">**Authentication Note:** Windows authentication is the recommended authentication method and it is the default Reporting Services authentication.</span></span> <span data-ttu-id="d2494-245">只有在 VM 上設定的使用者，才能夠存取 Reporting Services 及 Reporting Services 角色指派。</span><span class="sxs-lookup"><span data-stu-id="d2494-245">Only users that are configured on the VM can access Reporting Services and assigned to Reporting Services roles.</span></span>

### <a name="use-script-to-configure-the-report-server-and-http"></a><span data-ttu-id="d2494-246">使用指令碼設定報表伺服器和 HTTP</span><span class="sxs-lookup"><span data-stu-id="d2494-246">Use script to configure the report server and HTTP</span></span>
<span data-ttu-id="d2494-247">若要使用 Windows PowerShell 指令碼設定報表伺服器，請完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="d2494-247">To use the Windows PowerShell script to configure the report server, complete the following steps.</span></span> <span data-ttu-id="d2494-248">設定包括 HTTP 而非 HTTPS：</span><span class="sxs-lookup"><span data-stu-id="d2494-248">The configuration includes HTTP, not HTTPS:</span></span>

1. <span data-ttu-id="d2494-249">在 Azure 傳統入口網站中選取 VM，然後按一下 [連接]。</span><span class="sxs-lookup"><span data-stu-id="d2494-249">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="d2494-250">根據您的瀏覽器設定，可能會提示您儲存 .rdp 檔案以連接至 VM。</span><span class="sxs-lookup"><span data-stu-id="d2494-250">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
   
    ![連接至 Azure 虛擬機器](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="d2494-252">請使用您建立 VM 時所設定的使用者 VM 名稱、使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="d2494-252">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
   
    <span data-ttu-id="d2494-253">例如，下圖的 VM 名稱是 **ssrsnativecloud**，而使用者名稱是 **testuser**。</span><span class="sxs-lookup"><span data-stu-id="d2494-253">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
   
    ![登入包括 VM 名稱](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="d2494-255">在 VM 上，以系統管理權限開啟 **Windows PowerShell ISE** 。</span><span class="sxs-lookup"><span data-stu-id="d2494-255">On the VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="d2494-256">Windows Server 2012 預設會安裝 PowerShell ISE。</span><span class="sxs-lookup"><span data-stu-id="d2494-256">The PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="d2494-257">建議您使用 ISE 代替標準 Windows PowerShell 視窗，以便將指令碼貼到 ISE、修改指令碼，並接著執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="d2494-257">It is recommended you use the ISE instead of a standard Windows PowerShell window so that you can paste the script into the ISE, modify the script, and then run the script.</span></span>
3. <span data-ttu-id="d2494-258">在 Windows PowerShell ISE 中，按一下 [檢視] 功能表，然後按一下 [顯示指令碼窗格]。</span><span class="sxs-lookup"><span data-stu-id="d2494-258">In Windows PowerShell ISE, click the **View** menu and then click **Show Script Pane**.</span></span>
4. <span data-ttu-id="d2494-259">複製下列指令碼，然後將指令碼貼到 [Windows PowerShell ISE 指令碼] 窗格。</span><span class="sxs-lookup"><span data-stu-id="d2494-259">Copy the following script, and paste the script into the Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change the value if you used a different port for the private HTTP endpoint when the VM was created.
   
        ## Set PowerShell execution policy to be able to run scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change the version portion of the path to "v11" to use the script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting the web service URL ##
        write-host -foregroundcolor green "Setting the web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting the Database ##
        write-host -foregroundcolor green "Setting the Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating the database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script to create the database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes to sqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting the Report Manager URL ##
   
        write-host -foregroundcolor green "Setting the Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. <span data-ttu-id="d2494-260">如果您用來建立 VM 的 HTTP 連接埠不是 80，請修改參數 $HTTPport = 80。</span><span class="sxs-lookup"><span data-stu-id="d2494-260">If you created the VM with an HTTP port other than 80, modify the parameter $HTTPport = 80.</span></span>
6. <span data-ttu-id="d2494-261">已針對 Reporting Services 設定指令碼。</span><span class="sxs-lookup"><span data-stu-id="d2494-261">The script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="d2494-262">如果您要執行 Reporting Services 的指令碼，請在 Get-WmiObject 陳述式上，將命名空間的路徑版本部分修改為 "v11"。</span><span class="sxs-lookup"><span data-stu-id="d2494-262">If you want to run the script for  Reporting Services, modify the version portion of the path to the namespace to “v11”, on the Get-WmiObject statement.</span></span>
7. <span data-ttu-id="d2494-263">執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="d2494-263">Run the script.</span></span>

<span data-ttu-id="d2494-264">**驗證**：若要確認報表伺服器基本功能正常運作，請參閱本主題後半部的 [驗證組態](#verify-the-configuration) 一節。</span><span class="sxs-lookup"><span data-stu-id="d2494-264">**Validation**: To verify that the basic report server functionality is working, see the [Verify the configuration](#verify-the-configuration) section later in this topic.</span></span>

### <a name="use-script-to-configure-the-report-server-and-https"></a><span data-ttu-id="d2494-265">使用指令碼設定報表伺服器和 HTTPS</span><span class="sxs-lookup"><span data-stu-id="d2494-265">Use script to configure the report server and HTTPS</span></span>
<span data-ttu-id="d2494-266">若要使用 Windows PowerShell 設定報表伺服器，請完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="d2494-266">To use Windows PowerShell to configure the report server, complete the following steps.</span></span> <span data-ttu-id="d2494-267">設定包括 HTTP 而非 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="d2494-267">The configuration includes HTTPS, not HTTP.</span></span>

1. <span data-ttu-id="d2494-268">在 Azure 傳統入口網站中選取 VM，然後按一下 [連接]。</span><span class="sxs-lookup"><span data-stu-id="d2494-268">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="d2494-269">根據您的瀏覽器設定，可能會提示您儲存 .rdp 檔案以連接至 VM。</span><span class="sxs-lookup"><span data-stu-id="d2494-269">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
   
    ![連接至 Azure 虛擬機器](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="d2494-271">請使用您建立 VM 時所設定的使用者 VM 名稱、使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="d2494-271">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
   
    <span data-ttu-id="d2494-272">例如，下圖的 VM 名稱是 **ssrsnativecloud**，而使用者名稱是 **testuser**。</span><span class="sxs-lookup"><span data-stu-id="d2494-272">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
   
    ![登入包括 VM 名稱](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="d2494-274">在 VM 上，以系統管理權限開啟 **Windows PowerShell ISE** 。</span><span class="sxs-lookup"><span data-stu-id="d2494-274">On the VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="d2494-275">Windows Server 2012 預設會安裝 PowerShell ISE。</span><span class="sxs-lookup"><span data-stu-id="d2494-275">The PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="d2494-276">建議您使用 ISE 代替標準 Windows PowerShell 視窗，以便將指令碼貼到 ISE、修改指令碼，並接著執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="d2494-276">It is recommended you use the ISE instead of a standard Windows PowerShell window so that you can paste the script into the ISE, modify the script, and then run the script.</span></span>
3. <span data-ttu-id="d2494-277">若要允許執行指令碼，請執行下列 Windows PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="d2494-277">To enable running scripts, run the following Windows PowerShell command:</span></span>
   
        Set-ExecutionPolicy RemoteSigned
   
    <span data-ttu-id="d2494-278">然後您就能夠執行下列命令以驗證原則：</span><span class="sxs-lookup"><span data-stu-id="d2494-278">You can then run the following to verify the policy:</span></span>
   
        Get-ExecutionPolicy
4. <span data-ttu-id="d2494-279">在 [Windows PowerShell ISE] 中，按一下 [檢視]功能表，然後按一下 [顯示指令碼窗格]。</span><span class="sxs-lookup"><span data-stu-id="d2494-279">In **Windows PowerShell ISE**, click the **View** menu and then click **Show Script Pane**.</span></span>
5. <span data-ttu-id="d2494-280">複製下列指令碼，並將指令碼貼到 [Windows PowerShell ISE 指令碼] 窗格。</span><span class="sxs-lookup"><span data-stu-id="d2494-280">Copy the following script and paste it into the Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures the report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when the HTTPS endpoint was created.
   
        # You can run the following command to get (.cloudapp.net certificates) so you can copy the thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # The certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # the certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If the certificate is not a wildcard certificate, comment out the following line, and enable the full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "The script will use $DNSNameAndPort as the DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change the version portion of the path to "v11" to use the script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting the web service URL ##
        write-host -foregroundcolor green "Setting the web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting the Database ##
        write-host -foregroundcolor green "Setting the Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating the database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script to create the database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes to sqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting the Report Manager URL ##
   
        write-host -foregroundcolor green "Setting the Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. <span data-ttu-id="d2494-281">修改指令碼中的 **$certificatehash** 參數：</span><span class="sxs-lookup"><span data-stu-id="d2494-281">Modify the **$certificatehash** parameter in the script:</span></span>
   
   * <span data-ttu-id="d2494-282">這是 **必要** 參數。</span><span class="sxs-lookup"><span data-stu-id="d2494-282">This is a **required** parameter.</span></span> <span data-ttu-id="d2494-283">如果您未在先前步驟儲存憑證值，可使用下列方法之一，從憑證指紋複製憑證雜湊值：</span><span class="sxs-lookup"><span data-stu-id="d2494-283">If you did not save the certificate value from the previous steps, use one of the following methods to copy the certificate hash value from the certificates thumbprint.:</span></span>
     
       <span data-ttu-id="d2494-284">在 VM 上開啟 Windows PowerShell ISE 並執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="d2494-284">On the VM, open Windows PowerShell ISE and run the following command:</span></span>
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       <span data-ttu-id="d2494-285">輸出類似如下範例。</span><span class="sxs-lookup"><span data-stu-id="d2494-285">The output will look similar to the following.</span></span> <span data-ttu-id="d2494-286">如果指令碼傳回空白行，可能表示 VM 沒有設定憑證；請參閱 [使用虛擬機器的自我簽署憑證](#to-use-the-virtual-machines-self-signed-certificate)一節。</span><span class="sxs-lookup"><span data-stu-id="d2494-286">If the script returns a blank line, the VM does not have a certificate configured for example, see the section [To use the Virtual Machines Self-signed Certificate](#to-use-the-virtual-machines-self-signed-certificate).</span></span>
     
     <span data-ttu-id="d2494-287">或</span><span class="sxs-lookup"><span data-stu-id="d2494-287">OR</span></span>
   * <span data-ttu-id="d2494-288">在 VM 上執行 mmc.exe，然後新增 [憑證]  嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="d2494-288">On the VM Run mmc.exe and then add the **Certificates** snap-in.</span></span>
   * <span data-ttu-id="d2494-289">在 [信任的根憑證授權] 節點下，按兩下您的憑證名稱。</span><span class="sxs-lookup"><span data-stu-id="d2494-289">Under the **Trusted Root Certificate Authorities** node double-click your certificate name.</span></span> <span data-ttu-id="d2494-290">如果您使用 VM 的自我簽署憑證，則憑證是以 VM 的 DNS 名稱來命名，並以 **cloudapp.net** 結尾。</span><span class="sxs-lookup"><span data-stu-id="d2494-290">If you are using the self-signed certificate of the VM, the certificate is named after the DNS name of the VM and ends with **cloudapp.net**.</span></span>
   * <span data-ttu-id="d2494-291">按一下 [詳細資料]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d2494-291">Click the **Details** tab.</span></span>
   * <span data-ttu-id="d2494-292">按一下 [指紋] 。</span><span class="sxs-lookup"><span data-stu-id="d2494-292">Click **Thumbprint**.</span></span> <span data-ttu-id="d2494-293">憑證指紋的值會顯示在 [詳細資料] 欄位中，例如 af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span><span class="sxs-lookup"><span data-stu-id="d2494-293">The value of the thumbprint is displayed in the details field, for example af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span></span>
   * <span data-ttu-id="d2494-294">**執行指令碼之前**，請先移除每一組值之間的空格。</span><span class="sxs-lookup"><span data-stu-id="d2494-294">**Before you run the script**, remove the spaces in between the pairs of values.</span></span> <span data-ttu-id="d2494-295">例如 af1160b64b288d890a8212ff6ba9c3664f319048</span><span class="sxs-lookup"><span data-stu-id="d2494-295">For example af1160b64b288d890a8212ff6ba9c3664f319048</span></span>
7. <span data-ttu-id="d2494-296">修改 **$httpsport** 參數：</span><span class="sxs-lookup"><span data-stu-id="d2494-296">Modify the **$httpsport** parameter:</span></span> 
   
   * <span data-ttu-id="d2494-297">如果您將連接埠 443 用於 HTTPS 端點，則不需要在指令碼中更新此參數。</span><span class="sxs-lookup"><span data-stu-id="d2494-297">If you used port 443 for the HTTPS endpoint, then you do not need to update this parameter in the script.</span></span> <span data-ttu-id="d2494-298">否則請使用您在 VM 上設定 HTTPS 私用端點時所設定的連接埠值。</span><span class="sxs-lookup"><span data-stu-id="d2494-298">Otherwise use the port value you selected when you configured the HTTPS private endpoint on the VM.</span></span>
8. <span data-ttu-id="d2494-299">修改 **$DNSName** 參數：</span><span class="sxs-lookup"><span data-stu-id="d2494-299">Modify the **$DNSName** parameter:</span></span> 
   
   * <span data-ttu-id="d2494-300">指令碼設定為萬用字元憑證 $DNSName="+"。</span><span class="sxs-lookup"><span data-stu-id="d2494-300">The script is configured for a wild card certificate $DNSName="+".</span></span> <span data-ttu-id="d2494-301">如果您不想設定萬用字元憑證繫結，請將 $DNSName="+" 標記為註解，並啟用以下這一行完整 $DNSNAme 參考：##$DNSName="$server.cloudapp.net"。</span><span class="sxs-lookup"><span data-stu-id="d2494-301">If you do no want to configure for a wildcard certificate binding, comment out $DNSName="+" and enable the following line, the full $DNSNAme reference, ##$DNSName="$server.cloudapp.net".</span></span>
     
       <span data-ttu-id="d2494-302">如果您不想將虛擬機器的 DNS 名稱用於 Reporting Services，請變更 $DNSName 值。</span><span class="sxs-lookup"><span data-stu-id="d2494-302">Change the $DNSName value if you do not want to use the virtual machine’s DNS name for Reporting Services.</span></span> <span data-ttu-id="d2494-303">如果您使用此參數，則憑證也必須使用這個名稱，且您必須在 DNS 伺服器全域註冊該名稱。</span><span class="sxs-lookup"><span data-stu-id="d2494-303">If you use the parameter, the certificate must also use this name and you register the name globally on a DNS server.</span></span>
9. <span data-ttu-id="d2494-304">已針對 Reporting Services 設定指令碼。</span><span class="sxs-lookup"><span data-stu-id="d2494-304">The script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="d2494-305">如果您要執行 Reporting Services 的指令碼，請在 Get-WmiObject 陳述式上，將命名空間的路徑版本部分修改為 "v11"。</span><span class="sxs-lookup"><span data-stu-id="d2494-305">If you want to run the script for  Reporting Services, modify the version portion of the path to the namespace to “v11”, on the Get-WmiObject statement.</span></span>
10. <span data-ttu-id="d2494-306">執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="d2494-306">Run the script.</span></span>

<span data-ttu-id="d2494-307">**驗證**：若要確認報表伺服器基本功能正常運作，請參閱本主題後半部的 [驗證組態](#verify-the-connection) 一節。</span><span class="sxs-lookup"><span data-stu-id="d2494-307">**Validation**: To verify that the basic report server functionality is working, see the [Verify the configuration](#verify-the-connection) section later in this topic.</span></span> <span data-ttu-id="d2494-308">若要確認憑證繫結，請以系統管理權限開啟命令提示字元，然後執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="d2494-308">To verify the certificate binding open a command prompt with administrative privileges, and then run the following command:</span></span>

    netsh http show sslcert

<span data-ttu-id="d2494-309">結果將包含下列項目：</span><span class="sxs-lookup"><span data-stu-id="d2494-309">The result will include the following:</span></span>

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-to-configure-the-report-server"></a><span data-ttu-id="d2494-310">使用組態管理員設定報表伺服器</span><span class="sxs-lookup"><span data-stu-id="d2494-310">Use Configuration Manager to Configure the Report Server</span></span>
<span data-ttu-id="d2494-311">如果您不想執行 PowerShell 指令碼設定報表伺服器，請遵循本節的步驟，使用 Reporting Services 原生模式組態管理員設定報表伺服器。</span><span class="sxs-lookup"><span data-stu-id="d2494-311">If you do not want to run the PowerShell script to configure the report server, follow the steps in this section to use the Reporting Services native mode configuration manager to configure the report server.</span></span>

1. <span data-ttu-id="d2494-312">在 Azure 傳統入口網站中選取 VM，然後按一下 [連接]。</span><span class="sxs-lookup"><span data-stu-id="d2494-312">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="d2494-313">請使用您建立 VM 時所設定的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="d2494-313">Use the user name and password you configured when you created the VM.</span></span>
   
    ![連接至 Azure 虛擬機器](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. <span data-ttu-id="d2494-315">執行 Windows Update 並安裝 VM 的更新。</span><span class="sxs-lookup"><span data-stu-id="d2494-315">Run Windows update and install updates to the VM.</span></span> <span data-ttu-id="d2494-316">如果需要重新啟動 VM，請重新啟動 VM，並從 Azure 傳統入口網站重新連接到 VM。</span><span class="sxs-lookup"><span data-stu-id="d2494-316">If a restart of the VM is required, restart the VM and reconnect to the VM from the Azure classic portal.</span></span>
3. <span data-ttu-id="d2494-317">在 VM 的 [開始] 功能表中，鍵入 **Reporting Services**，並開啟 [Reporting Services 組態管理員]。</span><span class="sxs-lookup"><span data-stu-id="d2494-317">From the Start menu on the VM, type **Reporting Services** and open **Reporting Services Configuration Manager**.</span></span>
4. <span data-ttu-id="d2494-318">保留 [伺服器名稱] 和 [報表伺服器執行個體] 的預設值。</span><span class="sxs-lookup"><span data-stu-id="d2494-318">Leave the default values for **Server Name** and **Report Server Instance**.</span></span> <span data-ttu-id="d2494-319">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="d2494-319">Click **Connect**.</span></span>
5. <span data-ttu-id="d2494-320">按一下左窗格中的 [Web 服務 URL] 。</span><span class="sxs-lookup"><span data-stu-id="d2494-320">In the left pane, click **Web Service URL**.</span></span>
6. <span data-ttu-id="d2494-321">根據預設，RS 會設定為 HTTP 連接埠 80，而 IP 為全部指派。</span><span class="sxs-lookup"><span data-stu-id="d2494-321">By default, RS is configured for HTTP port 80 with IP “All Assigned”.</span></span> <span data-ttu-id="d2494-322">若要新增 HTTPS：</span><span class="sxs-lookup"><span data-stu-id="d2494-322">To add HTTPS:</span></span>
   
   1. <span data-ttu-id="d2494-323">在 [SSL 憑證] 中：選取您要使用的憑證，例如 [VM 名稱].cloudapp.net。</span><span class="sxs-lookup"><span data-stu-id="d2494-323">In **SSL Certificate**: select the certificate you want to use, for example [VM name].cloudapp.net.</span></span> <span data-ttu-id="d2494-324">如果未列出憑證，請參閱**步驟 2：建立伺服器憑證**一節，以取得有關如何在 VM 上安裝和信任憑證的資訊。</span><span class="sxs-lookup"><span data-stu-id="d2494-324">If no certificates are listed, see the section **Step 2: Create a Server Certificate** for information on how to install and trust the certificate on the VM.</span></span>
   2. <span data-ttu-id="d2494-325">在 [SSL 連接埠：] 下選擇 443。</span><span class="sxs-lookup"><span data-stu-id="d2494-325">Under **SSL Port**: choose 443.</span></span> <span data-ttu-id="d2494-326">如果您在 VM 中，以不同的私用連接埠設定 HTTPS 私用端點，請在此處使用該值。</span><span class="sxs-lookup"><span data-stu-id="d2494-326">If you configured the HTTPS private endpoint in the VM with a different private port, use that value here.</span></span>
   3. <span data-ttu-id="d2494-327">按一下 [套用]  ，並等候作業完成。</span><span class="sxs-lookup"><span data-stu-id="d2494-327">Click **Apply** and wait for the operation to complete.</span></span>
7. <span data-ttu-id="d2494-328">在左窗格中，按一下 [資料庫] 。</span><span class="sxs-lookup"><span data-stu-id="d2494-328">In the left pane, click **Database**.</span></span>
   
   1. <span data-ttu-id="d2494-329">按一下 [變更資料庫] 。</span><span class="sxs-lookup"><span data-stu-id="d2494-329">Click **Change Databas**e.</span></span>
   2. <span data-ttu-id="d2494-330">按一下 [建立新的報告伺服器資料庫]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d2494-330">Click **Create a new report server database** and then click **Next**.</span></span>
   3. <span data-ttu-id="d2494-331">將預設的 [伺服器名稱] 保留為 VM 名稱，並將預設的 [驗證類型] 保留為 [目前使用者 – 整合式安全性]。</span><span class="sxs-lookup"><span data-stu-id="d2494-331">Leave the default **Server Name**: as the VM name and leave the default **Authentication Type** as **Current User** – **Integrated Security**.</span></span> <span data-ttu-id="d2494-332">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="d2494-332">Click **Next**.</span></span>
   4. <span data-ttu-id="d2494-333">將預設的 [資料庫名稱] 保留為 **ReportServer**，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d2494-333">Leave the default **Database Name** as **ReportServer** and click **Next**.</span></span>
   5. <span data-ttu-id="d2494-334">將預設的 [驗證類型] 保留為 [服務認證]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d2494-334">Leave the default **Authentication Type** as **Service Credentials** and click **Next**.</span></span>
   6. <span data-ttu-id="d2494-335">按一下左窗格中的 [虛擬機器]  on the  。</span><span class="sxs-lookup"><span data-stu-id="d2494-335">Click **Next** on the **Summary** page.</span></span>
   7. <span data-ttu-id="d2494-336">組態設定完成後，按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="d2494-336">When the configuration is complete, click **Finish**.</span></span>
8. <span data-ttu-id="d2494-337">在左窗格中，按一下 [報告管理員 URL] 。</span><span class="sxs-lookup"><span data-stu-id="d2494-337">In the left pane, click **Report Manager URL**.</span></span> <span data-ttu-id="d2494-338">將預設的 [虛擬目錄] 保留為 [報告]，然後按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="d2494-338">Leave the default **Virtual Directory** as **Reports** and click **Apply**.</span></span>
9. <span data-ttu-id="d2494-339">按一下 [結束]  ，關閉 Reporting Services 組態管理員。</span><span class="sxs-lookup"><span data-stu-id="d2494-339">Click **Exit** to close the Reporting Services Configuration Manager.</span></span>

## <a name="step-4-open-windows-firewall-port"></a><span data-ttu-id="d2494-340">步驟 4：開啟 Windows 防火牆連接埠</span><span class="sxs-lookup"><span data-stu-id="d2494-340">Step 4: Open Windows Firewall Port</span></span>
> [!NOTE]
> <span data-ttu-id="d2494-341">如果您使用其中一個指令碼來設定報表伺服器，則可略過本節。</span><span class="sxs-lookup"><span data-stu-id="d2494-341">If you used one of the scripts to configure the report server, you can skip this section.</span></span> <span data-ttu-id="d2494-342">指令碼已包含可開啟防火牆連接埠的步驟。</span><span class="sxs-lookup"><span data-stu-id="d2494-342">The script included a step to open the firewall port.</span></span> <span data-ttu-id="d2494-343">預設值為連接埠 80 用於 HTTP，而連接埠 443 用於 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="d2494-343">The default was port 80 for HTTP and port 443 for HTTPS.</span></span>
> 
> 

<span data-ttu-id="d2494-344">若要遠端連接報表管理員或虛擬機器上的報表伺服器，則 VM 必須有 TCP 端點。</span><span class="sxs-lookup"><span data-stu-id="d2494-344">To connect remotely to Report Manager or the Report Server on the virtual machine, a TCP Endpoint is required on the VM.</span></span> <span data-ttu-id="d2494-345">必須在 VM 的防火牆中開啟相同的連接埠。</span><span class="sxs-lookup"><span data-stu-id="d2494-345">It is required to open the same port in the VM’s firewall.</span></span> <span data-ttu-id="d2494-346">端點是在佈建 VM 時建立。</span><span class="sxs-lookup"><span data-stu-id="d2494-346">The endpoint was created when the VM was provisioned.</span></span>

<span data-ttu-id="d2494-347">本節提供有關如何開啟防火牆連接埠的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="d2494-347">This section provides basic information on how to open the firewall port.</span></span> <span data-ttu-id="d2494-348">如需詳細資訊，請參閱 [為報告伺服器存取設定防火牆](https://technet.microsoft.com/library/bb934283.aspx)</span><span class="sxs-lookup"><span data-stu-id="d2494-348">For more information, see [Configure a Firewall for Report Server Access](https://technet.microsoft.com/library/bb934283.aspx)</span></span>

> [!NOTE]
> <span data-ttu-id="d2494-349">如果您使用指令碼來設定報表伺服器，則可略過本節。</span><span class="sxs-lookup"><span data-stu-id="d2494-349">If you used the script to configure the report server, you can skip this section.</span></span> <span data-ttu-id="d2494-350">指令碼已包含可開啟防火牆連接埠的步驟。</span><span class="sxs-lookup"><span data-stu-id="d2494-350">The script included a step to open the firewall port.</span></span>
> 
> 

<span data-ttu-id="d2494-351">如果您為 HTTPS 設定的私用連接埠不是 443，請據以修改下列指令碼。</span><span class="sxs-lookup"><span data-stu-id="d2494-351">If you configured a private port for HTTPS other than 443, modify the following script appropriately.</span></span> <span data-ttu-id="d2494-352">若要開啟 Windows 防火牆上的連接埠 **443** ，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d2494-352">To open port **443** on the Windows Firewall, complete the following:</span></span>

1. <span data-ttu-id="d2494-353">以系統管理權限開啟 Windows PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="d2494-353">Open a Windows PowerShell window with administrative privileges.</span></span>
2. <span data-ttu-id="d2494-354">如果您在 VM 上設定 HTTPS 端點時使用 443 以外的連接埠，請在下列命令中更新連接埠，然後執行命令：</span><span class="sxs-lookup"><span data-stu-id="d2494-354">If you used a port other than 443 when you configured the HTTPS endpoint on the VM, update the port in the following command and then run the command:</span></span>
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. <span data-ttu-id="d2494-355">命令完成時，命令提示字元會顯示 **Ok** 。</span><span class="sxs-lookup"><span data-stu-id="d2494-355">When the command completes, **Ok** is displayed in the command prompt.</span></span>

<span data-ttu-id="d2494-356">若要確認連接埠已開啟，請開啟 Windows PowerShell 視窗並執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="d2494-356">To verify that the port is opened, open a Windows PowerShell window and run the following command:</span></span>

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-the-configuration"></a><span data-ttu-id="d2494-357">驗證組態</span><span class="sxs-lookup"><span data-stu-id="d2494-357">Verify the configuration</span></span>
<span data-ttu-id="d2494-358">若要確認報表伺服器基本功能現已正常運作，請以系統管理權限開啟瀏覽器，並瀏覽至下列報表伺服器和報表管理員 URL：</span><span class="sxs-lookup"><span data-stu-id="d2494-358">To verify that the basic report server functionality is now working, open your browser with administrative privileges and then browse to the following report server ad report manager URLS:</span></span>

* <span data-ttu-id="d2494-359">在 VM 上，瀏覽至報表伺服器 URL：</span><span class="sxs-lookup"><span data-stu-id="d2494-359">On the VM, browse to the report server URL:</span></span>
  
        http://localhost/reportserver
* <span data-ttu-id="d2494-360">在 VM 上，瀏覽至報表管理員 URL：</span><span class="sxs-lookup"><span data-stu-id="d2494-360">On the VM, browse to the report manger URL:</span></span>
  
        http://localhost/Reports
* <span data-ttu-id="d2494-361">從本機電腦瀏覽至 VM 上的 **遠端** 報告管理員。</span><span class="sxs-lookup"><span data-stu-id="d2494-361">From your local computer, browse to the **remote** report Manager on the VM.</span></span> <span data-ttu-id="d2494-362">視需要更新下列範例中的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="d2494-362">Update the DNS name in the following example as appropriate.</span></span> <span data-ttu-id="d2494-363">如果系統提示輸入密碼，請使用您佈建 VM 時所建立的系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="d2494-363">When prompted for a password, use the administrator credentials you created when the VM was provisioned.</span></span> <span data-ttu-id="d2494-364">使用者名稱的格式是 [網域]\[使用者名稱]，其中的網域是 VM 電腦名稱，例如 ssrsnativecloud\testuser。</span><span class="sxs-lookup"><span data-stu-id="d2494-364">The user name is in the [Domain]\[user name] format, where the domain is the VM computer name, for example ssrsnativecloud\testuser.</span></span> <span data-ttu-id="d2494-365">如果您不是使用 HTTP**S**，請移除 URL 中的 **s**。</span><span class="sxs-lookup"><span data-stu-id="d2494-365">If you are not using HTTP**S**, remove the **s** in the URL.</span></span> <span data-ttu-id="d2494-366">如需有關如何在 VM 上建立其他使用者的資訊，請參閱下一節。</span><span class="sxs-lookup"><span data-stu-id="d2494-366">See the next section for information on creating additional users on VM.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/Reports
* <span data-ttu-id="d2494-367">從本機電腦瀏覽至遠端報表伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="d2494-367">From your local computer, browse to the remote report server URL.</span></span> <span data-ttu-id="d2494-368">視需要更新下列範例中的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="d2494-368">Update the DNS name in the following example as appropriate.</span></span> <span data-ttu-id="d2494-369">如果您不是使用 HTTPS，請移除 URL 中的 s。</span><span class="sxs-lookup"><span data-stu-id="d2494-369">If you are not using HTTPS, remove the s in the URL.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a><span data-ttu-id="d2494-370">建立使用者和指派角色</span><span class="sxs-lookup"><span data-stu-id="d2494-370">Create Users and Assign Roles</span></span>
<span data-ttu-id="d2494-371">設定和確認報表伺服器之後的一件常見管理工作，就是建立一或多個使用者，並將使用者指派給 Reporting Services 角色。</span><span class="sxs-lookup"><span data-stu-id="d2494-371">After configuring and verifying the report server, a common administrative task is to create one or more users and assign users to Reporting Services roles.</span></span> <span data-ttu-id="d2494-372">如需詳細資訊，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="d2494-372">For more information, see the following:</span></span>

* [<span data-ttu-id="d2494-373">建立本機使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="d2494-373">Create a local user account</span></span>](https://technet.microsoft.com/library/cc770642.aspx)
* <span data-ttu-id="d2494-374">[將報告伺服器存取權授與使用者 (報告管理員)](https://msdn.microsoft.com/library/ms156034.aspx))</span><span class="sxs-lookup"><span data-stu-id="d2494-374">[Grant User Access to a Report Server (Report Manager)](https://msdn.microsoft.com/library/ms156034.aspx))</span></span>
* [<span data-ttu-id="d2494-375">建立和管理角色指派</span><span class="sxs-lookup"><span data-stu-id="d2494-375">Create and Manage Role Assignments</span></span>](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="to-create-and-publish-reports-to-the-azure-virtual-machine"></a><span data-ttu-id="d2494-376">建立報表並發佈至 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d2494-376">To Create and Publish Reports to the Azure Virtual Machine</span></span>
<span data-ttu-id="d2494-377">下表摘要列出一些選項，可將現有報表從內部部署電腦發佈至 Microsoft Azure 虛擬機器上託管的報表伺服器：</span><span class="sxs-lookup"><span data-stu-id="d2494-377">The following table summarizes some of the options available to publish existing reports from an on-premises computer to the report server hosted on the Microsoft Azure Virtual Machine:</span></span>

* <span data-ttu-id="d2494-378">**RS.exe 指令碼**：使用 RS.exe 指令碼，將報告項目從現有報告伺服器複製到 Microsoft Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d2494-378">**RS.exe script**: Use RS.exe script to copy report items from and existing report server to your Microsoft Azure Virtual Machine.</span></span> <span data-ttu-id="d2494-379">如需詳細資訊，請參閱 [在報告伺服器之間移轉內容的範例 Reporting Services rs.exe 指令碼](https://msdn.microsoft.com/library/dn531017.aspx)的「原生模式到原生模式 – Microsoft Azure 虛擬機器」一節。</span><span class="sxs-lookup"><span data-stu-id="d2494-379">For more information, see the section “Native mode to Native Mode – Microsoft Azure Virtual Machine” in [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>
* <span data-ttu-id="d2494-380">**報告產生器**：虛擬機器包含 Click Once 版本的 Microsoft SQL Server 報告產生器。</span><span class="sxs-lookup"><span data-stu-id="d2494-380">**Report Builder**: The virtual machine includes the click-once version of Microsoft SQL Server Report Builder.</span></span> <span data-ttu-id="d2494-381">若要在虛擬機器上首次啟動報表產生器：</span><span class="sxs-lookup"><span data-stu-id="d2494-381">To start Report builder the first time on the virtual machine:</span></span>
  
  1. <span data-ttu-id="d2494-382">以管理權限啟動瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="d2494-382">Start your browser with administrative privileges.</span></span>
  2. <span data-ttu-id="d2494-383">瀏覽至虛擬機器上的報表管理員，然後按一下功能區中的 [報表產生器] 。</span><span class="sxs-lookup"><span data-stu-id="d2494-383">Browse to report manager on the virtual machine and click **Report Builder**  in the ribbon.</span></span>
     
     <span data-ttu-id="d2494-384">如需詳細資訊，請參閱 [安裝、解除安裝和支援報告產生器](https://technet.microsoft.com/library/dd207038.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d2494-384">For more information, see [Installing, Uninstalling, and Supporting Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span></span>
* <span data-ttu-id="d2494-385">**SQL Server Data Tools：VM**：如果您使用 SQL Server 2012 建立 VM，則會在虛擬機器上安裝 SQL Server Data Tools，且可在虛擬機器上用來建立**報告伺服器專案**與報告。</span><span class="sxs-lookup"><span data-stu-id="d2494-385">**SQL Server Data Tools: VM**:  If you created the VM with SQL Server 2012, then SQL Server Data Tools is installed on the virtual machine and can be used to create **Report Server Projects** and reports on the virtual machine.</span></span> <span data-ttu-id="d2494-386">SQL Server Data Tools 可將報表發佈至虛擬機器上的報表伺服器。</span><span class="sxs-lookup"><span data-stu-id="d2494-386">SQL Server Data Tools can publish the reports to the report server on the virtual machine.</span></span>
  
    <span data-ttu-id="d2494-387">如果您使用 SQL Server 2014 建立 VM，則可安裝 SQL Server Data Tools - BI for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="d2494-387">If you created the VM with SQL server 2014, you can install SQL Server Data Tools- BI for visual Studio.</span></span> <span data-ttu-id="d2494-388">如需詳細資訊，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="d2494-388">For more information, see the following:</span></span>
  
  * [<span data-ttu-id="d2494-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d2494-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span></span>](https://www.microsoft.com/download/details.aspx?id=42313)
  * [<span data-ttu-id="d2494-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="d2494-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=36843)
  * [<span data-ttu-id="d2494-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span><span class="sxs-lookup"><span data-stu-id="d2494-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span></span>](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* <span data-ttu-id="d2494-392">**SQL Server Data Tools：遠端**：在本機電腦上，以 SQL Server Data Tools 建立含有 Reporting Services 報告的 Reporting Services 專案。</span><span class="sxs-lookup"><span data-stu-id="d2494-392">**SQL Server Data Tools: Remote**:  On your local computer, create a Reporting Services project in SQL Server Data Tools that contains Reporting Services reports.</span></span> <span data-ttu-id="d2494-393">設定專案以連接至 Web 服務 URL。</span><span class="sxs-lookup"><span data-stu-id="d2494-393">Configure the project to connect to the web service URL.</span></span>
  
    ![SSRS 專案的 SSDT 專案屬性](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* <span data-ttu-id="d2494-395">**使用指令碼**：使用指令碼複製報告伺服器內容。</span><span class="sxs-lookup"><span data-stu-id="d2494-395">**Use script**: Use script to copy report server content.</span></span> <span data-ttu-id="d2494-396">如需詳細資訊，請參閱 [在報告伺服器之間移轉內容的 Reporting Services rs.exe 指令碼範例](https://msdn.microsoft.com/library/dn531017.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d2494-396">For more information, see [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>

## <a name="minimize-cost-if-you-are-not-using-the-vm"></a><span data-ttu-id="d2494-397">在不使用 VM 時將成本降至最低</span><span class="sxs-lookup"><span data-stu-id="d2494-397">Minimize cost if you are not using the VM</span></span>
> [!NOTE]
> <span data-ttu-id="d2494-398">若要在不使用 Azure 虛擬機器時將費用降至最低，請從 Azure 傳統入口網站關閉 VM。</span><span class="sxs-lookup"><span data-stu-id="d2494-398">To minimize charges for your Azure Virtual Machines when not in use, shut down the VM from the Azure classic portal.</span></span> <span data-ttu-id="d2494-399">如果您使用 VM 內的 Windows 電源選項關閉 VM，則仍需針對 VM 支付相同金額。</span><span class="sxs-lookup"><span data-stu-id="d2494-399">If you use the Windows power options inside a VM to shut down the VM, you are still charged the same amount for the VM.</span></span> <span data-ttu-id="d2494-400">為了降低費用，您必須在 Azure 傳統入口網站關閉 VM。</span><span class="sxs-lookup"><span data-stu-id="d2494-400">To reduce charges, you need to shut down the VM in the Azure classic portal.</span></span> <span data-ttu-id="d2494-401">如果您不再需要 VM，請記得刪除 VM 和相關聯的 .vhd 檔案，以節省儲存空間費用。如需詳細資訊，請參閱[虛擬機器價格詳細資料](https://azure.microsoft.com/pricing/details/virtual-machines/)的＜常見問題集＞一節。</span><span class="sxs-lookup"><span data-stu-id="d2494-401">If you no longer need the VM, remember to delete the VM and the associated .vhd files to avoid storage charges.For more information, see the FAQ section at [Virtual Machines Pricing Details](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>

## <a name="more-information"></a><span data-ttu-id="d2494-402">相關資訊</span><span class="sxs-lookup"><span data-stu-id="d2494-402">More Information</span></span>
### <a name="resources"></a><span data-ttu-id="d2494-403">資源</span><span class="sxs-lookup"><span data-stu-id="d2494-403">Resources</span></span>
* <span data-ttu-id="d2494-404">如需與 SQL Server Business Intelligence 及 SharePoint 2013 單一伺服器部署相關的類似內容，請參閱 [使用 Windows PowerShell 建立 Azure VM 搭配 SQL Server BI 及 SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d2494-404">For similar content related to a single server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Use Windows PowerShell to Create an Azure VM With SQL Server BI and SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span></span>
* <span data-ttu-id="d2494-405">如需與 SQL Server Business Intelligence 及 SharePoint 2013 多伺服器部署相關的類似內容，請參閱 [在 Azure 虛擬機器部署 SQL Server Business Intelligence](https://msdn.microsoft.com/library/dn321998.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d2494-405">For similar content related to a multi-server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Deploy SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span></span>
* <span data-ttu-id="d2494-406">如需與 Azure 虛擬機器的 SQL Server Business Intelligence 部署相關的一般資訊，請參閱 [Azure 虛擬機器的 SQL Server Business Intelligence](virtual-machines-windows-classic-ps-sql-bi.md)。</span><span class="sxs-lookup"><span data-stu-id="d2494-406">For General information related to deployments of SQL Server Business Intelligence in Azure Virtual Machines, see [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span></span>
* <span data-ttu-id="d2494-407">如需有關 Azure 計算費用成本的詳細資訊，請參閱 [Azure 價格計算機](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines)中的 [虛擬機器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d2494-407">For more information about the cost of Azure compute charges, see the Virtual Machines tab of [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span></span>

### <a name="community-content"></a><span data-ttu-id="d2494-408">社群內容</span><span class="sxs-lookup"><span data-stu-id="d2494-408">Community Content</span></span>
* <span data-ttu-id="d2494-409">如需有關如何不使用指令碼來建立 Reporting Services 原生模式報告伺服器的逐步指示，請參閱 [在 Azure 虛擬機器上託管 SQL Reporting Services](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html)。</span><span class="sxs-lookup"><span data-stu-id="d2494-409">For step by step instructions on how to create a Reporting Services Native mode report server without using script, see [Hosting SQL Reporting Service on Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span></span>

### <a name="links-to-other-resources-for-sql-server-in-azure-vms"></a><span data-ttu-id="d2494-410">Azure VM 中的 SQL Server 的其他資源連結</span><span class="sxs-lookup"><span data-stu-id="d2494-410">Links to other resources for SQL Server in Azure VMs</span></span>
[<span data-ttu-id="d2494-411">Azure 虛擬機器上的 SQL Server 概觀</span><span class="sxs-lookup"><span data-stu-id="d2494-411">SQL Server on Azure Virtual Machines Overview</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)


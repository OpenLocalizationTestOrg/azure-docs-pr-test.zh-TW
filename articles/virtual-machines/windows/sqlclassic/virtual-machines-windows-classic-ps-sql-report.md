---
title: "aaaUse PowerShell tooCreate VM 具有原生模式報表伺服器 |Microsoft 文件"
description: "本主題說明並引導您完成 hello 部署和 SQL Server Reporting Services 原生模式報表伺服器在 Azure 虛擬機器的組態。 "
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
ms.openlocfilehash: e7791199c87dff106132f1535da12de40a8dbc9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-vm-with-a-native-mode-report-server"></a><span data-ttu-id="1e1fc-103">使用 PowerShell tooCreate Azure VM 具有原生模式報表伺服器</span><span class="sxs-lookup"><span data-stu-id="1e1fc-103">Use PowerShell tooCreate an Azure VM With a Native Mode Report Server</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="1e1fc-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1e1fc-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="1e1fc-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="1e1fc-107">本主題說明並引導您完成 hello 部署和 SQL Server Reporting Services 原生模式報表伺服器在 Azure 虛擬機器的組態。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-107">This topic describes and walks you through hello deployment and configuration of a SQL Server Reporting Services native mode report server in an Azure Virtual Machine.</span></span> <span data-ttu-id="1e1fc-108">步驟在此文件使用的手動步驟 toocreate hello 虛擬機器和 Windows PowerShell 指令碼組合 hello hello VM 上 tooconfigure Reporting Services。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-108">hello steps in this document use a combination of manual steps toocreate hello virtual machine and a Windows PowerShell script tooconfigure Reporting Services on hello VM.</span></span> <span data-ttu-id="1e1fc-109">hello 組態指令碼包含開啟 HTTP 或 HTTPs 的防火牆連接埠。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-109">hello configuration script includes opening a firewall port for HTTP or HTTPs.</span></span>

> [!NOTE]
> <span data-ttu-id="1e1fc-110">如果您不需要**HTTPS** hello 報表伺服器上，**略過步驟 2**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-110">If you do not require **HTTPS** on hello report server, **skip step 2**.</span></span>
> 
> <span data-ttu-id="1e1fc-111">之後在步驟 1 中建立 hello VM，請前往 toohello 區段使用指令碼 tooconfigure hello 報表伺服器 HTTP。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-111">After creating hello VM in step 1, go toohello section Use script tooconfigure hello report server and HTTP.</span></span> <span data-ttu-id="1e1fc-112">執行 hello 指令碼之後，hello 報表伺服器是準備 toouse。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-112">After you run hello script, hello report server is ready toouse.</span></span>

## <a name="prerequisites-and-assumptions"></a><span data-ttu-id="1e1fc-113">必要條件與假設</span><span class="sxs-lookup"><span data-stu-id="1e1fc-113">Prerequisites and Assumptions</span></span>
* <span data-ttu-id="1e1fc-114">**Azure 訂用帳戶**： 驗證您的 Azure 訂閱中可用的核心 hello 號碼。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-114">**Azure Subscription**: Verify hello number of cores available in your Azure Subscription.</span></span> <span data-ttu-id="1e1fc-115">如果您建立建議的 VM 大小的 hello **A3**，您需要**4**可用的核心。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-115">If you create hello recommended VM size of **A3**, you need **4** available cores.</span></span> <span data-ttu-id="1e1fc-116">若您採用 **A2** 的 VM 大小，則需要 **2** 個可用的核心。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-116">If you use a VM size of **A2**, you need **2** available cores.</span></span>
  
  * <span data-ttu-id="1e1fc-117">tooverify hello 核心限制 hello Azure 傳統入口網站，在您訂用帳戶，按一下 hello 上方功能表中 hello 左的窗格，然後按一下 使用方式的設定。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-117">tooverify hello core limit of your subscription, in hello Azure classic portal, click SETTINGS in hello left pane and then Click USAGE in hello top menu.</span></span>
  * <span data-ttu-id="1e1fc-118">tooincrease hello 核心配額，請連絡[Azure 支援](https://azure.microsoft.com/support/options/)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-118">tooincrease hello core quota, contact [Azure Support](https://azure.microsoft.com/support/options/).</span></span> <span data-ttu-id="1e1fc-119">如需 VM 大小的資訊，請參閱 [Azure 的虛擬機器大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-119">For VM size information, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="1e1fc-120">**Windows PowerShell 指令碼**: hello 主題假設您有基本的 Windows PowerShell 的實用知識。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-120">**Windows PowerShell Scripting**: hello topic assumes that you have a basic working knowledge of Windows PowerShell.</span></span> <span data-ttu-id="1e1fc-121">如需有關如何使用 Windows PowerShell 的詳細資訊，請參閱 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="1e1fc-121">For more information about using Windows PowerShell, see hello following:</span></span>
  
  * [<span data-ttu-id="1e1fc-122">在 Windows Server 上啟動 Windows PowerShell (英文)</span><span class="sxs-lookup"><span data-stu-id="1e1fc-122">Starting Windows PowerShell on Windows Server</span></span>](https://technet.microsoft.com/library/hh847814.aspx)
  * [<span data-ttu-id="1e1fc-123">開始使用 Windows PowerShell (英文)</span><span class="sxs-lookup"><span data-stu-id="1e1fc-123">Getting Started with Windows PowerShell</span></span>](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a><span data-ttu-id="1e1fc-124">步驟 1：佈建 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="1e1fc-124">Step 1: Provision an Azure Virtual Machine</span></span>
1. <span data-ttu-id="1e1fc-125">瀏覽 toohello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-125">Browse toohello Azure classic portal.</span></span>
2. <span data-ttu-id="1e1fc-126">按一下**虛擬機器**hello 左窗格中。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-126">Click **Virtual Machines** in hello left pane.</span></span>
   
    ![Microsoft Azure 虛擬機器](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. <span data-ttu-id="1e1fc-128">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-128">Click **New**.</span></span>
   
    ![新增按鈕](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. <span data-ttu-id="1e1fc-130">按一下 [從資源庫] 。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-130">Click **From Gallery**.</span></span>
   
    ![從資源庫新增 VM](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. <span data-ttu-id="1e1fc-132">按一下**SQL Server 2014 RTM Standard – Windows Server 2012 R2**然後按一下hello 箭號 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-132">Click **SQL Server 2014 RTM Standard – Windows Server 2012 R2** and then click hello arrow toocontinue.</span></span>
   
    ![下一步](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    <span data-ttu-id="1e1fc-134">如果您需要 hello Reporting Services 資料驅動訂閱功能，請選擇**SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-134">If you need hello Reporting Services data driven subscriptions feature, choose **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span></span> <span data-ttu-id="1e1fc-135">如需有關 SQL Server 版本及支援功能的詳細資訊，請參閱[hello SQL Server 2012 版本所支援的功能](https://msdn.microsoft.com/library/cc645993.aspx#Reporting)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-135">For more information on SQL Server editions and feature support, see [Features Supported by hello Editions of SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span></span>
6. <span data-ttu-id="1e1fc-136">在 hello**虛擬機器組態**頁面上，編輯下列欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e1fc-136">On hello **Virtual machine configuration** page, edit hello following fields:</span></span>
   
   * <span data-ttu-id="1e1fc-137">如果有一個以上**版本發行日期**，選取 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-137">If there is more than one **VERSION RELEASE DATE**, select hello most recent version.</span></span>
   * <span data-ttu-id="1e1fc-138">**虛擬機器名稱**: hello 機器的名稱也會 hello 下一個組態頁面與 hello 預設雲端服務 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-138">**Virtual Machine Name**: hello machine name is also used on hello next configuration page as hello default Cloud Service DNS name.</span></span> <span data-ttu-id="1e1fc-139">跨 hello Azure 服務，hello DNS 名稱必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-139">hello DNS name must be unique across hello Azure service.</span></span> <span data-ttu-id="1e1fc-140">請考慮使用描述哪些 hello 用於 VM 的電腦名稱設定 hello VM。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-140">Consider configuring hello VM with a computer name that describes what hello VM is used for.</span></span> <span data-ttu-id="1e1fc-141">例如 ssrsnativecloud。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-141">For example ssrsnativecloud.</span></span>
   * <span data-ttu-id="1e1fc-142">[層]：標準</span><span class="sxs-lookup"><span data-stu-id="1e1fc-142">**Tier**: Standard</span></span>
   * <span data-ttu-id="1e1fc-143">**大小： A3** hello 建議用於 SQL Server 工作負載的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-143">**Size:A3** is hello recommended VM size for SQL Server workloads.</span></span> <span data-ttu-id="1e1fc-144">若 VM 只當做報表伺服器，則 A2 的 VM 大小已足夠，除非 hello 報表伺服器會面臨大量的工作負載。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-144">If a VM is only used as a report server, a VM size of A2 is sufficient unless hello report server experiences a large workload.</span></span> <span data-ttu-id="1e1fc-145">如需 VM 的價格資訊，請參閱 [虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-145">For VM pricing information, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
   * <span data-ttu-id="1e1fc-146">**新的使用者名稱**: hello 您所提供的名稱會建立為 hello VM 上的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-146">**New User Name**: hello name you provide is created as an administrator on hello VM.</span></span>
   * <span data-ttu-id="1e1fc-147">[新增密碼] 並**確認**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-147">**New Password** and **confirm**.</span></span> <span data-ttu-id="1e1fc-148">此密碼用於 hello 新系統管理員帳戶，並建議使用強式密碼。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-148">This password is used for hello new administrator account and it is recommended you use a strong password.</span></span>
   * <span data-ttu-id="1e1fc-149">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-149">Click **Next**.</span></span> <span data-ttu-id="1e1fc-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span><span class="sxs-lookup"><span data-stu-id="1e1fc-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span></span>
7. <span data-ttu-id="1e1fc-151">在 hello 下一個頁面上，編輯下列欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e1fc-151">On hello next page, edit hello following fields:</span></span>
   
   * <span data-ttu-id="1e1fc-152">[雲端服務]：選取 [建立新的雲端服務]。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-152">**Cloud Service**: select **Create a new Cloud Service**.</span></span>
   * <span data-ttu-id="1e1fc-153">**雲端服務 DNS 名稱**： 這是 hello 與 hello VM 相關聯的雲端服務的 hello 公開 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-153">**Cloud Service DNS Name**: This is hello public DNS name of hello Cloud Service that is associated with hello VM.</span></span> <span data-ttu-id="1e1fc-154">hello 預設名稱是您在輸入中的 hello VM 名稱的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-154">hello default name is hello name you typed in for hello VM name.</span></span> <span data-ttu-id="1e1fc-155">如果您於稍後步驟中的 hello 主題，您可以建立受信任的 SSL 憑證並再 hello DNS 名稱 hello hello 值"**發給**"hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-155">If in later steps of hello topic, you create a trusted SSL certificate and then hello DNS name is used for hello value of hello “**Issued to**” of hello certificate.</span></span>
   * <span data-ttu-id="1e1fc-156">**區域/同質群組/虛擬網路**： 選擇 hello 區域最接近 tooyour 終端使用者。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-156">**Region/Affinity Group/Virtual Network**: Choose hello region closest tooyour end users.</span></span>
   * <span data-ttu-id="1e1fc-157">[儲存體帳戶]：使用自動產生的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-157">**Storage Account**: Use an automatically generated storage account.</span></span>
   * <span data-ttu-id="1e1fc-158">[可用性設定組]：無。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-158">**Availability Set**: None.</span></span>
   * <span data-ttu-id="1e1fc-159">**端點**保持 hello**遠端桌面**和**PowerShell**端點然後再加入 HTTP 或 HTTPS 端點，根據您的環境。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-159">**ENDPOINTS** Keep hello **Remote Desktop** and **PowerShell** endpoints and then add either an HTTP or HTTPS endpoint, depending on your environment.</span></span>
     
     * <span data-ttu-id="1e1fc-160">**HTTP**: hello 公用及私用通訊埠為的預設**80**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-160">**HTTP**: hello default public and private ports are **80**.</span></span> <span data-ttu-id="1e1fc-161">請注意，如果您使用 80 以外的私用連接埠修改**$HTTPport = 80** hello http 指令碼中。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-161">Note that if you use a private port other than 80, modify **$HTTPport = 80** in hello http script.</span></span>
     * <span data-ttu-id="1e1fc-162">**HTTPS**: hello 公用及私用通訊埠為的預設**443**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-162">**HTTPS**: hello default public and private ports are **443**.</span></span> <span data-ttu-id="1e1fc-163">安全性最佳作法是 toochange hello 私用連接埠，並設定防火牆與 hello 報表伺服器 toouse hello 私用連接埠。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-163">A security best practice is toochange hello private port and configure your firewall and hello report server toouse hello private port.</span></span> <span data-ttu-id="1e1fc-164">如需有關端點的詳細資訊，請參閱[如何 tooSet 與虛擬機器的通訊](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-164">For more information on endpoints, see [How tooSet Up Communication with a Virtual Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="1e1fc-165">請注意，如果您使用 443 以外的連接埠變更 hello 參數**$HTTPsport = 443** hello HTTPS 指令碼中。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-165">Note that if you use a port other than 443, change hello parameter **$HTTPsport = 443** in hello HTTPS script.</span></span>
   * <span data-ttu-id="1e1fc-166">按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-166">Click next .</span></span> ![下一步](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. <span data-ttu-id="1e1fc-168">在 hello hello 精靈的最後一個頁面上，保留 hello 預設**安裝 hello VM 代理程式**選取。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-168">On hello last page of hello wizard, keep hello default **Install hello VM agent** selected.</span></span> <span data-ttu-id="1e1fc-169">hello 本主題中的步驟不會使用 hello VM 代理程式，但如果您計劃 tookeep 此 VM，hello VM 代理程式和擴充功能可讓您 tooenhance 他 CM。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-169">hello steps in this topic do not utilize hello VM agent but if you plan tookeep this VM, hello VM agent and extensions will allow you tooenhance he CM.</span></span>  <span data-ttu-id="1e1fc-170">如需有關 hello VM 代理程式的詳細資訊，請參閱[VM 代理程式和延伸模組 – 第 1 部分](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-170">For more information on hello VM agent, see [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span></span> <span data-ttu-id="1e1fc-171">其中一個執行 hello 預設安裝的擴充功能 ad hello VM 桌面上會顯示 hello"BGINFO"延伸模組，系統資訊，例如內部 IP 和可用磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-171">One of hello default extensions installed ad running is hello “BGINFO” extension that displays on hello VM desktop, system information such as internal IP and free drive space.</span></span>
9. <span data-ttu-id="1e1fc-172">按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-172">Click complete .</span></span> ![Ok](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. <span data-ttu-id="1e1fc-174">hello**狀態**的 VM 會顯示為 hello**啟動 （正在佈建）**期間 hello 佈建程序，則將顯示為**執行**當 hello VM 已佈建並就緒toouse。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-174">hello **Status** of hello VM displays as **Starting (Provisioning)** during hello provision process and then displays as **Running** when hello VM is provisioned and ready toouse.</span></span>

## <a name="step-2-create-a-server-certificate"></a><span data-ttu-id="1e1fc-175">步驟 2：建立伺服器憑證</span><span class="sxs-lookup"><span data-stu-id="1e1fc-175">Step 2: Create a Server Certificate</span></span>
> [!NOTE]
> <span data-ttu-id="1e1fc-176">如果您不需要 HTTPS hello 報表伺服器上，您可以**略過步驟 2**並移 toohello 區段**使用指令碼 tooconfigure hello 報表伺服器和 HTTP**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-176">If you do not require HTTPS on hello report server, you can **skip step 2** and go toohello section **Use script tooconfigure hello report server and HTTP**.</span></span> <span data-ttu-id="1e1fc-177">使用 hello HTTP 指令碼 tooquickly 設定 hello 報表伺服器和伺服器會準備 toouse hello 報表。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-177">Use hello HTTP script tooquickly configure hello report server and hello report server will be ready toouse.</span></span>

<span data-ttu-id="1e1fc-178">在訂單 toouse HTTPS hello VM 上，您會需要受信任的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-178">In order toouse HTTPS on hello VM, you need a trusted SSL certificate.</span></span> <span data-ttu-id="1e1fc-179">根據您的案例中，您可以使用下列兩種方法的 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="1e1fc-179">Depending on your scenario, you can use one of hello following two methods:</span></span>

* <span data-ttu-id="1e1fc-180">由憑證授權單位 (CA) 核發，且受到 Microsoft 信任的有效 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-180">A valid SSL certificate issued by a Certification Authority (CA) and trusted by Microsoft.</span></span> <span data-ttu-id="1e1fc-181">hello CA 根憑證會經由 Microsoft 根憑證計劃 hello 散發的必要的 toobe。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-181">hello CA root certificates are required toobe distributed via hello Microsoft Root Certificate Program.</span></span> <span data-ttu-id="1e1fc-182">如需此計劃的詳細資訊，請參閱[Windows 和 Windows Phone 8 SSL 根憑證計劃 (成員 Ca)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx)和[簡介 toohello Microsoft 根憑證計劃](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-182">For more information about this program, see [Windows and Windows Phone 8 SSL Root Certificate Program (Member CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) and [Introduction toohello Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span></span>
* <span data-ttu-id="1e1fc-183">自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-183">A self-signed certificate.</span></span> <span data-ttu-id="1e1fc-184">不建議將自我簽署憑證用於生產環境。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-184">Self-signed certificates are not recommended for production environments.</span></span>

### <a name="toouse-a-certificate-created-by-a-trusted-certificate-authority-ca"></a><span data-ttu-id="1e1fc-185">toouse 由受信任憑證授權單位 (CA) 所建立的憑證</span><span class="sxs-lookup"><span data-stu-id="1e1fc-185">toouse a certificate created by a trusted Certificate Authority (CA)</span></span>
1. <span data-ttu-id="1e1fc-186">**要求 hello 網站的伺服器憑證的憑證授權單位**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-186">**Request a server certificate for hello website from a certification authority**.</span></span> 
   
    <span data-ttu-id="1e1fc-187">您可以使用任一 toogenerate 憑證要求檔案 (Certreq.txt) 的線上憑證授權單位的要求時，都需要傳送 tooa 憑證授權單位或 toogenerate hello Web 伺服器憑證精靈。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-187">You can use hello Web Server Certificate Wizard either toogenerate a certificate request file (Certreq.txt) that you send tooa certification authority, or toogenerate a request for an online certification authority.</span></span> <span data-ttu-id="1e1fc-188">例如 Windows Server 2012 中的 Microsoft Certificate Services。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-188">For example, Microsoft Certificate Services in Windows Server 2012.</span></span> <span data-ttu-id="1e1fc-189">根據您的伺服器憑證所提供的識別保證 hello 等級，hello 憑證授權單位 tooapprove 數天 tooseveral 月您的要求，並將憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-189">Depending on hello level of identification assurance offered by your server certificate, it is several days tooseveral months for hello certification authority tooapprove your request and send you a certificate file.</span></span> 
   
    <span data-ttu-id="1e1fc-190">如需有關申請伺服器憑證的詳細資訊，請參閱 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="1e1fc-190">For more information about requesting a server certificates, see hello following:</span></span> 
   
   * <span data-ttu-id="1e1fc-191">使用 [Certreq](https://technet.microsoft.com/library/cc725793.aspx)、[Certreq](https://technet.microsoft.com/library/cc725793.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span></span>
   * <span data-ttu-id="1e1fc-192">安全性工具 tooAdminister Windows Server 2012。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-192">Security Tools tooAdminister Windows Server 2012.</span></span>
     
     [<span data-ttu-id="1e1fc-193">安全性工具 tooAdminister Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="1e1fc-193">Security Tools tooAdminister Windows Server 2012</span></span>](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > <span data-ttu-id="1e1fc-194">hello**發給**欄位 hello 信任 SSL 憑證應該是 hello 相同為 hello**雲端服務 DNS 名稱**的 hello 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-194">hello **issued to** field of hello trusted SSL certificate should be hello same as hello **Cloud Service DNS NAME** you used for hello new VM.</span></span>

2. <span data-ttu-id="1e1fc-195">**Hello 網頁伺服器上安裝 hello 伺服器憑證**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-195">**Install hello server certificate on hello Web server**.</span></span> <span data-ttu-id="1e1fc-196">在此情況下則 hello VM 主機 hello 報表伺服器，並在稍後步驟中建立 hello 網站時設定 Reporting Services hello 網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-196">hello Web server in this case is hello VM that hosts hello report server and hello website is created in later steps when you configure Reporting Services.</span></span> <span data-ttu-id="1e1fc-197">如需 hello 伺服器憑證安裝在 hello Web 伺服器上，使用 hello 憑證 MMC 嵌入式管理單元的詳細資訊，請參閱[安裝伺服器憑證](https://technet.microsoft.com/library/cc740068)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-197">For more information about installing hello server certificate on hello Web server by using hello Certificate MMC snap-in, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
    <span data-ttu-id="1e1fc-198">如果您想 toouse hello 指令碼包含本主題中，tooconfigure hello 報表伺服器，hello hello 憑證值**指紋**無須為 hello 指令碼的參數。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-198">If you want toouse hello script included with this topic, tooconfigure hello report server, hello value of hello certificates **Thumbprint** is required as a parameter of hello script.</span></span> <span data-ttu-id="1e1fc-199">上如何 tooobtain hello hello 憑證的指紋，請參閱 hello 下一節，如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-199">See hello next section for details on how tooobtain hello thumbprint of hello certificate.</span></span>
3. <span data-ttu-id="1e1fc-200">指派 hello 伺服器憑證 toohello 報表伺服器。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-200">Assign hello server certificate toohello report server.</span></span> <span data-ttu-id="1e1fc-201">當您設定 hello 報表伺服器 hello 分派完成 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-201">hello assignment is completed in hello next section when you configure hello report server.</span></span>

### <a name="toouse-hello-virtual-machines-self-signed-certificate"></a><span data-ttu-id="1e1fc-202">toouse hello 虛擬機器自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="1e1fc-202">toouse hello Virtual Machines Self-signed Certificate</span></span>
<span data-ttu-id="1e1fc-203">Hello VM 佈建時 hello VM 上建立自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-203">A self-signed certificate was created on hello VM when hello VM was provisioned.</span></span> <span data-ttu-id="1e1fc-204">hello 憑證具有名稱為 hello VM DNS 名稱相同的 hello。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-204">hello certificate has hello same name as hello VM DNS name.</span></span> <span data-ttu-id="1e1fc-205">在訂單 tooavoid 憑證錯誤，就需要該 hello 憑證受到信任 hello VM 本身，還要受到 hello 站台的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-205">In order tooavoid certificate errors, it is required that hello certificate is trusted on hello VM itself, and also by all users of hello site.</span></span>

1. <span data-ttu-id="1e1fc-206">hello 本機的 VM 上的 hello 憑證 tootrust hello 根 CA 加入 hello 憑證 toohello**受信任的根憑證授權單位**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-206">tootrust hello root CA of hello certificate on hello Local VM, add hello certificate toohello **Trusted Root Certification Authorities**.</span></span> <span data-ttu-id="1e1fc-207">hello 以下是摘要 hello 所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-207">hello following is a summary of hello steps required.</span></span> <span data-ttu-id="1e1fc-208">如需如何 tootrust hello CA 的詳細步驟，請參閱[安裝伺服器憑證](https://technet.microsoft.com/library/cc740068)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-208">For detailed steps on how tootrust hello CA, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
   1. <span data-ttu-id="1e1fc-209">從 hello Azure 傳統入口網站，選取 hello VM，然後按一下 連線。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-209">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="1e1fc-210">根據瀏覽器的設定，您可能會提示的 toosave.rdp 檔案，以連接 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-210">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
      
       ![tooazure 虛擬機器連線](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="1e1fc-212">使用 hello 使用者 VM 名稱、 使用者名稱和密碼建立 hello VM 時設定。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-212">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
      
       <span data-ttu-id="1e1fc-213">例如，在下列映像的 hello，hello VM 名稱是**ssrsnativecloud**而 hello 使用者名稱為**testuser**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-213">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
      
       ![登入包括 VM 名稱](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. <span data-ttu-id="1e1fc-215">執行 mmc.exe。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-215">Run mmc.exe.</span></span> <span data-ttu-id="1e1fc-216">如需詳細資訊，請參閱[How to： 使用 hello MMC 嵌入式管理單元檢視憑證](https://msdn.microsoft.com/library/ms788967.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-216">For more information, see [How to: View Certificates with hello MMC Snap-in](https://msdn.microsoft.com/library/ms788967.aspx).</span></span>
   3. <span data-ttu-id="1e1fc-217">Hello 主控台應用程式中**檔案**功能表上，新增 hello**憑證**嵌入式管理單元中，選取**電腦帳戶**當出現提示，然後按一下**下一步**.</span><span class="sxs-lookup"><span data-stu-id="1e1fc-217">In hello console application **File** menu, add hello **Certificates** snap-in, select **Computer Account** when prompted, and then click **Next**.</span></span>
   4. <span data-ttu-id="1e1fc-218">選取**本機電腦**toomanage，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-218">Select **Local Computer** toomanage and then click **Finish**.</span></span>
   5. <span data-ttu-id="1e1fc-219">按一下**確定**然後展開 hello**憑證-個人**節點，然後按一下**憑證**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-219">Click **Ok** and then expand hello **Certificates -Personal** nodes and then click **Certificates**.</span></span> <span data-ttu-id="1e1fc-220">hello 憑證 hello 的 hello VM 的 DNS 名稱來命名，並結束**.cloudapp.net**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-220">hello certificate is named after hello DNS name of hello VM and ends with **cloudapp.net**.</span></span> <span data-ttu-id="1e1fc-221">以滑鼠右鍵按一下 hello 憑證名稱，然後按一下**複製**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-221">Right-click hello certificate name and click **Copy**.</span></span>
   6. <span data-ttu-id="1e1fc-222">展開 hello**受信任的根憑證授權單位**節點，然後以滑鼠右鍵按一下**憑證**，然後按一下**貼上**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-222">Expand hello **Trusted Root Certification Authorities** node and then right-click **Certificates** and then click **Paste**.</span></span>
   7. <span data-ttu-id="1e1fc-223">hello 下的憑證名稱按一下雙 toovalidate**受信任的根憑證授權單位**，並確定沒有任何錯誤，而且您會看到您的憑證。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-223">toovalidate, double click on hello certificate name under **Trusted Root Certification Authorities** and verify that there are no errors and you see your certificate.</span></span> <span data-ttu-id="1e1fc-224">如果您想 toouse hello HTTPS 指令碼包含本主題中，tooconfigure hello 報表伺服器，hello hello 憑證值**指紋**無須為 hello 指令碼的參數。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-224">If you want toouse hello HTTPS script included with this topic, tooconfigure hello report server, hello value of hello certificates **Thumbprint** is required as a parameter of hello script.</span></span> <span data-ttu-id="1e1fc-225">**tooget hello 指紋值**，完成下列 hello。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-225">**tooget hello thumbprint value**, complete hello following.</span></span> <span data-ttu-id="1e1fc-226">區段中還有 PowerShell 範例 tooretrieve hello 指紋[使用指令碼 tooconfigure hello 報表伺服器和 HTTPS](#use-script-to-configure-the-report-server-and-HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-226">There is also a PowerShell sample tooretrieve hello thumbprint in section [Use script tooconfigure hello report server and HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span></span>
      
      1. <span data-ttu-id="1e1fc-227">按兩下 hello 憑證，例如 ssrsnativecloud.cloudapp.net hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-227">Double-click hello name of hello certificate, for example ssrsnativecloud.cloudapp.net.</span></span>
      2. <span data-ttu-id="1e1fc-228">按一下 hello**詳細資料** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-228">Click hello **Details** tab.</span></span>
      3. <span data-ttu-id="1e1fc-229">按一下 [指紋] 。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-229">Click **Thumbprint**.</span></span> <span data-ttu-id="1e1fc-230">hello hello 指紋值欄位中所顯示 hello 詳細資料，例如 a6 08 3c df f9 0b f7 e3 7 c 25 ed a4 ed 7e ac 91 9 c 2c fb 2f。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-230">hello value of hello thumbprint is displayed in hello details field, for example ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span></span>
      4. <span data-ttu-id="1e1fc-231">複製 hello 指紋並儲存供稍後 hello 值或現在編輯 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-231">Copy hello thumbprint and save hello value for later or edit hello script now.</span></span>
      5. <span data-ttu-id="1e1fc-232">(*)執行 hello 指令碼之前，請移除 hello 配對值中間的 hello 空格。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-232">(*) Before you run hello script, remove hello spaces in between hello pairs of values.</span></span> <span data-ttu-id="1e1fc-233">例如 hello 前述的憑證指紋現在會是 a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-233">For example hello thumbprint noted before would now be ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span></span>
      6. <span data-ttu-id="1e1fc-234">指派 hello 伺服器憑證 toohello 報表伺服器。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-234">Assign hello server certificate toohello report server.</span></span> <span data-ttu-id="1e1fc-235">當您設定 hello 報表伺服器 hello 分派完成 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-235">hello assignment is completed in hello next section when you configure hello report server.</span></span>

<span data-ttu-id="1e1fc-236">如果您使用自我簽署的 SSL 憑證，hello hello 憑證名稱就會與 hello hello VM 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-236">If you are using a self-signed SSL certificate, hello name on hello certificate already matches hello hostname of hello VM.</span></span> <span data-ttu-id="1e1fc-237">因此，hello hello 機器的 DNS 已向全球註冊，而且可以從任何用戶端存取。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-237">Therefore, hello DNS of hello machine is already registered globally and can be accessed from any client.</span></span>

## <a name="step-3-configure-hello-report-server"></a><span data-ttu-id="1e1fc-238">步驟 3： 設定報表伺服器 hello</span><span class="sxs-lookup"><span data-stu-id="1e1fc-238">Step 3: Configure hello Report Server</span></span>
<span data-ttu-id="1e1fc-239">本節將引導您完成設定 hello VM 做為 Reporting Services 原生模式報表伺服器。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-239">This section walks you through configuring hello VM as a Reporting Services native mode report server.</span></span> <span data-ttu-id="1e1fc-240">您可以使用下列方法 tooconfigure hello 報表伺服器的 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="1e1fc-240">You can use one of hello following methods tooconfigure hello report server:</span></span>

* <span data-ttu-id="1e1fc-241">使用 hello 指令碼 tooconfigure hello 報表伺服器</span><span class="sxs-lookup"><span data-stu-id="1e1fc-241">Use hello script tooconfigure hello report server</span></span>
* <span data-ttu-id="1e1fc-242">使用 Configuration Manager tooConfigure hello 報表伺服器。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-242">Use Configuration Manager tooConfigure hello Report Server.</span></span>

<span data-ttu-id="1e1fc-243">如需詳細步驟，請參閱 hello 節[連接 toohello 虛擬機器並啟動 hello Reporting Services 組態管理員](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-243">For more detailed steps, see hello section [Connect toohello Virtual Machine and Start hello Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span></span>

<span data-ttu-id="1e1fc-244">**驗證注意事項：** Windows 驗證是建議使用的驗證方法的 hello，而且它是 hello 預設 Reporting Services 的驗證。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-244">**Authentication Note:** Windows authentication is hello recommended authentication method and it is hello default Reporting Services authentication.</span></span> <span data-ttu-id="1e1fc-245">Hello VM 所設定的使用者可以存取 Reporting Services，並且指派 tooReporting Services 角色。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-245">Only users that are configured on hello VM can access Reporting Services and assigned tooReporting Services roles.</span></span>

### <a name="use-script-tooconfigure-hello-report-server-and-http"></a><span data-ttu-id="1e1fc-246">使用指令碼 tooconfigure hello 報表伺服器和 HTTP</span><span class="sxs-lookup"><span data-stu-id="1e1fc-246">Use script tooconfigure hello report server and HTTP</span></span>
<span data-ttu-id="1e1fc-247">toouse hello Windows PowerShell 指令碼 tooconfigure hello 報表伺服器時，完成下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-247">toouse hello Windows PowerShell script tooconfigure hello report server, complete hello following steps.</span></span> <span data-ttu-id="1e1fc-248">hello 組態包含 HTTP，而不是 HTTPS:</span><span class="sxs-lookup"><span data-stu-id="1e1fc-248">hello configuration includes HTTP, not HTTPS:</span></span>

1. <span data-ttu-id="1e1fc-249">從 hello Azure 傳統入口網站，選取 hello VM，然後按一下 連線。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-249">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="1e1fc-250">根據瀏覽器的設定，您可能會提示的 toosave.rdp 檔案，以連接 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-250">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
   
    ![tooazure 虛擬機器連線](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="1e1fc-252">使用 hello 使用者 VM 名稱、 使用者名稱和密碼建立 hello VM 時設定。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-252">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
   
    <span data-ttu-id="1e1fc-253">例如，在下列映像的 hello，hello VM 名稱是**ssrsnativecloud**而 hello 使用者名稱為**testuser**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-253">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
   
    ![登入包括 VM 名稱](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="1e1fc-255">開啟 hello VM， **Windows PowerShell ISE**具有系統管理權限。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-255">On hello VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="1e1fc-256">在 Windows server 2012 預設會安裝 PowerShell ISE hello。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-256">hello PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="1e1fc-257">建議您將使用 hello ISE 代替標準 Windows PowerShell 視窗，以便您可以將 hello 指令碼貼到 hello ISE，修改 hello 指令碼，然後再執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-257">It is recommended you use hello ISE instead of a standard Windows PowerShell window so that you can paste hello script into hello ISE, modify hello script, and then run hello script.</span></span>
3. <span data-ttu-id="1e1fc-258">在 Windows PowerShell ISE 中，按一下 hello**檢視**功能表，然後按一下**顯示指令碼窗格**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-258">In Windows PowerShell ISE, click hello **View** menu and then click **Show Script Pane**.</span></span>
4. <span data-ttu-id="1e1fc-259">複製下列指令碼，hello hello 指令碼並貼到 hello Windows PowerShell ISE 指令碼窗格。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-259">Copy hello following script, and paste hello script into hello Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change hello value if you used a different port for hello private HTTP endpoint when hello VM was created.
   
        ## Set PowerShell execution policy toobe able toorun scripts
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
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
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
   
        ## Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes toosqlserver provider
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
   
        ## Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
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
5. <span data-ttu-id="1e1fc-260">如果您使用 80 以外的 HTTP 連接埠建立 hello VM，修改 hello 參數 $HTTPport = 80。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-260">If you created hello VM with an HTTP port other than 80, modify hello parameter $HTTPport = 80.</span></span>
6. <span data-ttu-id="1e1fc-261">Reporting Services 目前是設定成 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-261">hello script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="1e1fc-262">如果您想 toorun hello 指令碼適用於 Reporting Services 時，修改 hello 路徑 toohello 命名空間的 hello 版本部分太"v11"，hello Get-wmiobject 陳述式。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-262">If you want toorun hello script for  Reporting Services, modify hello version portion of hello path toohello namespace too“v11”, on hello Get-WmiObject statement.</span></span>
7. <span data-ttu-id="1e1fc-263">執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-263">Run hello script.</span></span>

<span data-ttu-id="1e1fc-264">**驗證**: tooverify 正在 hello 報表伺服器基本功能，請參閱 hello[確認 hello 組態](#verify-the-configuration)本主題稍後的章節。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-264">**Validation**: tooverify that hello basic report server functionality is working, see hello [Verify hello configuration](#verify-the-configuration) section later in this topic.</span></span>

### <a name="use-script-tooconfigure-hello-report-server-and-https"></a><span data-ttu-id="1e1fc-265">使用指令碼 tooconfigure hello 報表伺服器和 HTTPS</span><span class="sxs-lookup"><span data-stu-id="1e1fc-265">Use script tooconfigure hello report server and HTTPS</span></span>
<span data-ttu-id="1e1fc-266">toouse Windows PowerShell tooconfigure hello 報表伺服器時，完成下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-266">toouse Windows PowerShell tooconfigure hello report server, complete hello following steps.</span></span> <span data-ttu-id="1e1fc-267">hello 組態包含 HTTPS，而不是 HTTP。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-267">hello configuration includes HTTPS, not HTTP.</span></span>

1. <span data-ttu-id="1e1fc-268">從 hello Azure 傳統入口網站，選取 hello VM，然後按一下 連線。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-268">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="1e1fc-269">根據瀏覽器的設定，您可能會提示的 toosave.rdp 檔案，以連接 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-269">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
   
    ![tooazure 虛擬機器連線](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="1e1fc-271">使用 hello 使用者 VM 名稱、 使用者名稱和密碼建立 hello VM 時設定。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-271">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
   
    <span data-ttu-id="1e1fc-272">例如，在下列映像的 hello，hello VM 名稱是**ssrsnativecloud**而 hello 使用者名稱為**testuser**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-272">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
   
    ![登入包括 VM 名稱](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="1e1fc-274">開啟 hello VM， **Windows PowerShell ISE**具有系統管理權限。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-274">On hello VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="1e1fc-275">在 Windows server 2012 預設會安裝 PowerShell ISE hello。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-275">hello PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="1e1fc-276">建議您將使用 hello ISE 代替標準 Windows PowerShell 視窗，以便您可以將 hello 指令碼貼到 hello ISE，修改 hello 指令碼，然後再執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-276">It is recommended you use hello ISE instead of a standard Windows PowerShell window so that you can paste hello script into hello ISE, modify hello script, and then run hello script.</span></span>
3. <span data-ttu-id="1e1fc-277">執行指令碼，執行下列 Windows PowerShell 命令的 hello tooenable:</span><span class="sxs-lookup"><span data-stu-id="1e1fc-277">tooenable running scripts, run hello following Windows PowerShell command:</span></span>
   
        Set-ExecutionPolicy RemoteSigned
   
    <span data-ttu-id="1e1fc-278">然後，您可以執行下列 tooverify hello 原則 hello:</span><span class="sxs-lookup"><span data-stu-id="1e1fc-278">You can then run hello following tooverify hello policy:</span></span>
   
        Get-ExecutionPolicy
4. <span data-ttu-id="1e1fc-279">在**Windows PowerShell ISE**，按一下 hello**檢視**功能表，然後按一下**顯示指令碼窗格**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-279">In **Windows PowerShell ISE**, click hello **View** menu and then click **Show Script Pane**.</span></span>
5. <span data-ttu-id="1e1fc-280">複製下列指令碼，並將它貼到 hello Windows PowerShell ISE 指令碼窗格中的 hello。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-280">Copy hello following script and paste it into hello Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures hello report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when hello HTTPS endpoint was created.
   
        # You can run hello following command tooget (.cloudapp.net certificates) so you can copy hello thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # hello certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # hello certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If hello certificate is not a wildcard certificate, comment out hello following line, and enable hello full $DNSNAme reference.
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
   
        write-host "hello script will use $DNSNameAndPort as hello DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
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
   
        ## 2. Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes toosqlserver provider
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
   
        ## 3. Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
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
6. <span data-ttu-id="1e1fc-281">修改 hello **$certificatehash** hello 指令碼中的參數：</span><span class="sxs-lookup"><span data-stu-id="1e1fc-281">Modify hello **$certificatehash** parameter in hello script:</span></span>
   
   * <span data-ttu-id="1e1fc-282">這是 **必要** 參數。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-282">This is a **required** parameter.</span></span> <span data-ttu-id="1e1fc-283">如果您沒有儲存 hello 憑證值 hello 先前步驟中，使用其中一個 hello hello 憑證指紋的下列方法 toocopy hello 憑證雜湊值。:</span><span class="sxs-lookup"><span data-stu-id="1e1fc-283">If you did not save hello certificate value from hello previous steps, use one of hello following methods toocopy hello certificate hash value from hello certificates thumbprint.:</span></span>
     
       <span data-ttu-id="1e1fc-284">上 hello VM，開啟 Windows PowerShell ISE 並執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e1fc-284">On hello VM, open Windows PowerShell ISE and run hello following command:</span></span>
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       <span data-ttu-id="1e1fc-285">hello 輸出看起來類似 toohello 下列。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-285">hello output will look similar toohello following.</span></span> <span data-ttu-id="1e1fc-286">如果 hello 指令碼傳回空白行，hello VM 沒有憑證，例如設定，請參閱 hello 節[toouse hello 虛擬機器自我簽署憑證](#to-use-the-virtual-machines-self-signed-certificate)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-286">If hello script returns a blank line, hello VM does not have a certificate configured for example, see hello section [toouse hello Virtual Machines Self-signed Certificate](#to-use-the-virtual-machines-self-signed-certificate).</span></span>
     
     <span data-ttu-id="1e1fc-287">或</span><span class="sxs-lookup"><span data-stu-id="1e1fc-287">OR</span></span>
   * <span data-ttu-id="1e1fc-288">在 hello VM 執行 mmc.exe，然後再加入 hello**憑證**嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-288">On hello VM Run mmc.exe and then add hello **Certificates** snap-in.</span></span>
   * <span data-ttu-id="1e1fc-289">在 hello**受信任的根憑證授權單位**節點按兩下憑證名稱。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-289">Under hello **Trusted Root Certificate Authorities** node double-click your certificate name.</span></span> <span data-ttu-id="1e1fc-290">如果您使用 hello 的 hello VM 的自我簽署的憑證，hello 憑證 hello 的 hello VM 的 DNS 名稱來命名，並以結束**.cloudapp.net**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-290">If you are using hello self-signed certificate of hello VM, hello certificate is named after hello DNS name of hello VM and ends with **cloudapp.net**.</span></span>
   * <span data-ttu-id="1e1fc-291">按一下 hello**詳細資料** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-291">Click hello **Details** tab.</span></span>
   * <span data-ttu-id="1e1fc-292">按一下 [指紋] 。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-292">Click **Thumbprint**.</span></span> <span data-ttu-id="1e1fc-293">hello hello 指紋值欄位中所顯示 hello 詳細資料，例如 af 11 60 b6 4b 28 8 d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span><span class="sxs-lookup"><span data-stu-id="1e1fc-293">hello value of hello thumbprint is displayed in hello details field, for example af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span></span>
   * <span data-ttu-id="1e1fc-294">**Hello 指令碼執行之前**，移除 hello 配對值中間的 hello 空格。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-294">**Before you run hello script**, remove hello spaces in between hello pairs of values.</span></span> <span data-ttu-id="1e1fc-295">例如 af1160b64b288d890a8212ff6ba9c3664f319048</span><span class="sxs-lookup"><span data-stu-id="1e1fc-295">For example af1160b64b288d890a8212ff6ba9c3664f319048</span></span>
7. <span data-ttu-id="1e1fc-296">修改 hello **$httpsport**參數：</span><span class="sxs-lookup"><span data-stu-id="1e1fc-296">Modify hello **$httpsport** parameter:</span></span> 
   
   * <span data-ttu-id="1e1fc-297">如果您使用連接埠 443 hello HTTPS 端點，然後您不需要 tooupdate hello 指令碼中的這個參數。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-297">If you used port 443 for hello HTTPS endpoint, then you do not need tooupdate this parameter in hello script.</span></span> <span data-ttu-id="1e1fc-298">否則使用 hello hello VM 上設定 hello HTTPS 私用端點時，您選取的連接埠值。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-298">Otherwise use hello port value you selected when you configured hello HTTPS private endpoint on hello VM.</span></span>
8. <span data-ttu-id="1e1fc-299">修改 hello **$DNSName**參數：</span><span class="sxs-lookup"><span data-stu-id="1e1fc-299">Modify hello **$DNSName** parameter:</span></span> 
   
   * <span data-ttu-id="1e1fc-300">hello 指令碼已針對萬用字元憑證 $DNSName ="+"。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-300">hello script is configured for a wild card certificate $DNSName="+".</span></span> <span data-ttu-id="1e1fc-301">如果您不想 tooconfigure 萬用字元憑證繫結，標記為註解 $DNSName ="+"和啟用下列行，hello $DNSNAme 完整參考，# # $DNSName="$server.cloudapp.net hello"。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-301">If you do no want tooconfigure for a wildcard certificate binding, comment out $DNSName="+" and enable hello following line, hello full $DNSNAme reference, ##$DNSName="$server.cloudapp.net".</span></span>
     
       <span data-ttu-id="1e1fc-302">如果不想讓 Reporting Services 的 toouse hello 虛擬機器的 DNS 名稱，請變更 hello $DNSName 值。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-302">Change hello $DNSName value if you do not want toouse hello virtual machine’s DNS name for Reporting Services.</span></span> <span data-ttu-id="1e1fc-303">如果您使用 hello 參數，hello 憑證也必須使用此名稱，並註冊的 DNS 伺服器上的全域 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-303">If you use hello parameter, hello certificate must also use this name and you register hello name globally on a DNS server.</span></span>
9. <span data-ttu-id="1e1fc-304">Reporting Services 目前是設定成 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-304">hello script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="1e1fc-305">如果您想 toorun hello 指令碼適用於 Reporting Services 時，修改 hello 路徑 toohello 命名空間的 hello 版本部分太"v11"，hello Get-wmiobject 陳述式。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-305">If you want toorun hello script for  Reporting Services, modify hello version portion of hello path toohello namespace too“v11”, on hello Get-WmiObject statement.</span></span>
10. <span data-ttu-id="1e1fc-306">執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-306">Run hello script.</span></span>

<span data-ttu-id="1e1fc-307">**驗證**: tooverify 正在 hello 報表伺服器基本功能，請參閱 hello[確認 hello 組態](#verify-the-connection)本主題稍後的章節。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-307">**Validation**: tooverify that hello basic report server functionality is working, see hello [Verify hello configuration](#verify-the-connection) section later in this topic.</span></span> <span data-ttu-id="1e1fc-308">tooverify hello 憑證繫結使用系統管理權限開啟命令提示字元並執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e1fc-308">tooverify hello certificate binding open a command prompt with administrative privileges, and then run hello following command:</span></span>

    netsh http show sslcert

<span data-ttu-id="1e1fc-309">hello 結果將包含 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="1e1fc-309">hello result will include hello following:</span></span>

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-tooconfigure-hello-report-server"></a><span data-ttu-id="1e1fc-310">使用 Configuration Manager tooConfigure hello 報表伺服器</span><span class="sxs-lookup"><span data-stu-id="1e1fc-310">Use Configuration Manager tooConfigure hello Report Server</span></span>
<span data-ttu-id="1e1fc-311">若不想使用 toorun hello PowerShell 指令碼 tooconfigure hello 報表伺服器，請遵循此節 toouse hello Reporting Services 原生模式組態管理員 tooconfigure hello 報表伺服器中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-311">If you do not want toorun hello PowerShell script tooconfigure hello report server, follow hello steps in this section toouse hello Reporting Services native mode configuration manager tooconfigure hello report server.</span></span>

1. <span data-ttu-id="1e1fc-312">從 hello Azure 傳統入口網站，選取 hello VM，然後按一下 連線。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-312">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="1e1fc-313">使用 hello 使用者名稱和密碼建立 hello VM 時設定。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-313">Use hello user name and password you configured when you created hello VM.</span></span>
   
    ![tooazure 虛擬機器連線](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. <span data-ttu-id="1e1fc-315">執行 Windows update 並安裝更新 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-315">Run Windows update and install updates toohello VM.</span></span> <span data-ttu-id="1e1fc-316">如果需要 hello VM 重新啟動，重新啟動 hello VM，然後重新連線 toohello VM 從 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-316">If a restart of hello VM is required, restart hello VM and reconnect toohello VM from hello Azure classic portal.</span></span>
3. <span data-ttu-id="1e1fc-317">從在 hello VM hello 開始功能表中，輸入**Reporting Services**並開啟**Reporting Services 組態管理員**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-317">From hello Start menu on hello VM, type **Reporting Services** and open **Reporting Services Configuration Manager**.</span></span>
4. <span data-ttu-id="1e1fc-318">保留預設值 hello**伺服器名稱**和**報表伺服器執行個體**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-318">Leave hello default values for **Server Name** and **Report Server Instance**.</span></span> <span data-ttu-id="1e1fc-319">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-319">Click **Connect**.</span></span>
5. <span data-ttu-id="1e1fc-320">在 hello 左窗格中，按一下  **Web 服務 URL**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-320">In hello left pane, click **Web Service URL**.</span></span>
6. <span data-ttu-id="1e1fc-321">根據預設，RS 會設定為 HTTP 連接埠 80，而 IP 為全部指派。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-321">By default, RS is configured for HTTP port 80 with IP “All Assigned”.</span></span> <span data-ttu-id="1e1fc-322">tooadd HTTPS:</span><span class="sxs-lookup"><span data-stu-id="1e1fc-322">tooadd HTTPS:</span></span>
   
   1. <span data-ttu-id="1e1fc-323">在**SSL 憑證**： 您想 toouse，例如 [VM 名稱] 選取 hello 憑證。.cloudapp.net。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-323">In **SSL Certificate**: select hello certificate you want toouse, for example [VM name].cloudapp.net.</span></span> <span data-ttu-id="1e1fc-324">如果未列出憑證，請參閱 hello 節**步驟 2： 建立伺服器憑證**如需有關如何 tooinstall 和信任 hello hello VM 上的憑證資訊。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-324">If no certificates are listed, see hello section **Step 2: Create a Server Certificate** for information on how tooinstall and trust hello certificate on hello VM.</span></span>
   2. <span data-ttu-id="1e1fc-325">在 [SSL 連接埠：] 下選擇 443。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-325">Under **SSL Port**: choose 443.</span></span> <span data-ttu-id="1e1fc-326">如果您在 hello VM 不同的私用通訊埠設定 HTTPS 私用端點時，hello，此處使用該值。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-326">If you configured hello HTTPS private endpoint in hello VM with a different private port, use that value here.</span></span>
   3. <span data-ttu-id="1e1fc-327">按一下**套用**並等候 hello 作業 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-327">Click **Apply** and wait for hello operation toocomplete.</span></span>
7. <span data-ttu-id="1e1fc-328">在 hello 左窗格中，按一下 **資料庫**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-328">In hello left pane, click **Database**.</span></span>
   
   1. <span data-ttu-id="1e1fc-329">按一下 [變更資料庫] 。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-329">Click **Change Databas**e.</span></span>
   2. <span data-ttu-id="1e1fc-330">按一下 [建立新的報告伺服器資料庫]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-330">Click **Create a new report server database** and then click **Next**.</span></span>
   3. <span data-ttu-id="1e1fc-331">保留預設值，hello**伺服器名稱**: hello VM 名稱，並保留預設值，hello**驗證類型**為**目前使用者**–**整合式安全性**.</span><span class="sxs-lookup"><span data-stu-id="1e1fc-331">Leave hello default **Server Name**: as hello VM name and leave hello default **Authentication Type** as **Current User** – **Integrated Security**.</span></span> <span data-ttu-id="1e1fc-332">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-332">Click **Next**.</span></span>
   4. <span data-ttu-id="1e1fc-333">保留預設值，hello**資料庫名稱**為**ReportServer**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-333">Leave hello default **Database Name** as **ReportServer** and click **Next**.</span></span>
   5. <span data-ttu-id="1e1fc-334">保留預設值，hello**驗證類型**為**服務認證**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-334">Leave hello default **Authentication Type** as **Service Credentials** and click **Next**.</span></span>
   6. <span data-ttu-id="1e1fc-335">按一下**下一步**上 hello**摘要**頁面。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-335">Click **Next** on hello **Summary** page.</span></span>
   7. <span data-ttu-id="1e1fc-336">Hello 組態完成時，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-336">When hello configuration is complete, click **Finish**.</span></span>
8. <span data-ttu-id="1e1fc-337">在 hello 左窗格中，按一下 **報表管理員 URL**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-337">In hello left pane, click **Report Manager URL**.</span></span> <span data-ttu-id="1e1fc-338">保留預設值，hello**虛擬目錄**為**報表**按一下**套用**。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-338">Leave hello default **Virtual Directory** as **Reports** and click **Apply**.</span></span>
9. <span data-ttu-id="1e1fc-339">按一下**結束**tooclose hello Reporting Services 組態管理員。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-339">Click **Exit** tooclose hello Reporting Services Configuration Manager.</span></span>

## <a name="step-4-open-windows-firewall-port"></a><span data-ttu-id="1e1fc-340">步驟 4：開啟 Windows 防火牆連接埠</span><span class="sxs-lookup"><span data-stu-id="1e1fc-340">Step 4: Open Windows Firewall Port</span></span>
> [!NOTE]
> <span data-ttu-id="1e1fc-341">如果您使用其中一個 hello 指令碼 tooconfigure hello 報表伺服器，您可以略過本節。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-341">If you used one of hello scripts tooconfigure hello report server, you can skip this section.</span></span> <span data-ttu-id="1e1fc-342">hello 指令碼包含的步驟 tooopen hello 防火牆連接埠。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-342">hello script included a step tooopen hello firewall port.</span></span> <span data-ttu-id="1e1fc-343">hello 預設是連接埠 80 用於 HTTP 和 https 連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-343">hello default was port 80 for HTTP and port 443 for HTTPS.</span></span>
> 
> 

<span data-ttu-id="1e1fc-344">tooconnect 遠端 tooReport 管理員或 hello 報告上 hello VM 需要 hello 虛擬機器上的伺服器、 TCP 端點。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-344">tooconnect remotely tooReport Manager or hello Report Server on hello virtual machine, a TCP Endpoint is required on hello VM.</span></span> <span data-ttu-id="1e1fc-345">它是必要的 tooopen hello 相同的 hello VM 防火牆連接埠。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-345">It is required tooopen hello same port in hello VM’s firewall.</span></span> <span data-ttu-id="1e1fc-346">hello VM 佈建時，已建立 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-346">hello endpoint was created when hello VM was provisioned.</span></span>

<span data-ttu-id="1e1fc-347">本節提供如何 tooopen hello 防火牆連接埠上的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-347">This section provides basic information on how tooopen hello firewall port.</span></span> <span data-ttu-id="1e1fc-348">如需詳細資訊，請參閱 [為報告伺服器存取設定防火牆](https://technet.microsoft.com/library/bb934283.aspx)</span><span class="sxs-lookup"><span data-stu-id="1e1fc-348">For more information, see [Configure a Firewall for Report Server Access](https://technet.microsoft.com/library/bb934283.aspx)</span></span>

> [!NOTE]
> <span data-ttu-id="1e1fc-349">如果您使用 hello 指令碼 tooconfigure hello 報表伺服器，您可以略過本節。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-349">If you used hello script tooconfigure hello report server, you can skip this section.</span></span> <span data-ttu-id="1e1fc-350">hello 指令碼包含的步驟 tooopen hello 防火牆連接埠。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-350">hello script included a step tooopen hello firewall port.</span></span>
> 
> 

<span data-ttu-id="1e1fc-351">如果您針對 HTTPS 設定私用連接埠 443 以外時，修改下列指令碼適當的 hello。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-351">If you configured a private port for HTTPS other than 443, modify hello following script appropriately.</span></span> <span data-ttu-id="1e1fc-352">tooopen 連接埠**443** hello Windows 防火牆，在完成 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="1e1fc-352">tooopen port **443** on hello Windows Firewall, complete hello following:</span></span>

1. <span data-ttu-id="1e1fc-353">以系統管理權限開啟 Windows PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-353">Open a Windows PowerShell window with administrative privileges.</span></span>
2. <span data-ttu-id="1e1fc-354">如果您使用 443 以外的通訊埠 hello VM 上設定 hello HTTPS 端點時，更新 hello hello 下列命令中的連接埠，然後執行 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="1e1fc-354">If you used a port other than 443 when you configured hello HTTPS endpoint on hello VM, update hello port in hello following command and then run hello command:</span></span>
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. <span data-ttu-id="1e1fc-355">Hello 命令完成時，**確定**hello 命令提示字元中顯示。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-355">When hello command completes, **Ok** is displayed in hello command prompt.</span></span>

<span data-ttu-id="1e1fc-356">tooverify，hello 通訊埠已開啟，開啟 Windows PowerShell 視窗並執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="1e1fc-356">tooverify that hello port is opened, open a Windows PowerShell window and run hello following command:</span></span>

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-hello-configuration"></a><span data-ttu-id="1e1fc-357">確認 hello 組態</span><span class="sxs-lookup"><span data-stu-id="1e1fc-357">Verify hello configuration</span></span>
<span data-ttu-id="1e1fc-358">tooverify 現在使用 hello 報表伺服器基本功能，以系統管理權限開啟瀏覽器，然後瀏覽 toohello 下列報表伺服器和報表管理員 URL:</span><span class="sxs-lookup"><span data-stu-id="1e1fc-358">tooverify that hello basic report server functionality is now working, open your browser with administrative privileges and then browse toohello following report server ad report manager URLS:</span></span>

* <span data-ttu-id="1e1fc-359">在 hello VM，瀏覽 toohello 報表伺服器 URL:</span><span class="sxs-lookup"><span data-stu-id="1e1fc-359">On hello VM, browse toohello report server URL:</span></span>
  
        http://localhost/reportserver
* <span data-ttu-id="1e1fc-360">在 hello VM，瀏覽 toohello 報表管理員 URL:</span><span class="sxs-lookup"><span data-stu-id="1e1fc-360">On hello VM, browse toohello report manger URL:</span></span>
  
        http://localhost/Reports
* <span data-ttu-id="1e1fc-361">從本機電腦，瀏覽 toohello**遠端**hello VM 在報表管理員。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-361">From your local computer, browse toohello **remote** report Manager on hello VM.</span></span> <span data-ttu-id="1e1fc-362">更新 hello hello 下列適當的範例中的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-362">Update hello DNS name in hello following example as appropriate.</span></span> <span data-ttu-id="1e1fc-363">出現提示時輸入密碼，請使用 hello hello VM 已佈建時所建立的系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-363">When prompted for a password, use hello administrator credentials you created when hello VM was provisioned.</span></span> <span data-ttu-id="1e1fc-364">hello [Domain] 中的 hello 使用者名稱為\[使用者名稱] 格式，其中 hello 網域是 hello VM 電腦名稱，例如 ssrsnativecloud\testuser。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-364">hello user name is in hello [Domain]\[user name] format, where hello domain is hello VM computer name, for example ssrsnativecloud\testuser.</span></span> <span data-ttu-id="1e1fc-365">如果您不想要使用 HTTP**S**，移除 hello **s** hello URL 中。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-365">If you are not using HTTP**S**, remove hello **s** in hello URL.</span></span> <span data-ttu-id="1e1fc-366">在 VM 上建立額外的使用者，請參閱 hello 下一節的資訊。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-366">See hello next section for information on creating additional users on VM.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/Reports
* <span data-ttu-id="1e1fc-367">從本機電腦，瀏覽 toohello 遠端報表伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-367">From your local computer, browse toohello remote report server URL.</span></span> <span data-ttu-id="1e1fc-368">更新 hello hello 下列適當的範例中的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-368">Update hello DNS name in hello following example as appropriate.</span></span> <span data-ttu-id="1e1fc-369">如果您未使用 HTTPS，移除 hello s hello URL 中。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-369">If you are not using HTTPS, remove hello s in hello URL.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a><span data-ttu-id="1e1fc-370">建立使用者和指派角色</span><span class="sxs-lookup"><span data-stu-id="1e1fc-370">Create Users and Assign Roles</span></span>
<span data-ttu-id="1e1fc-371">設定和驗證 hello 報表伺服器之後，一般的管理工作是 toocreate 一或多個使用者，並將使用者指派 tooReporting Services 角色。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-371">After configuring and verifying hello report server, a common administrative task is toocreate one or more users and assign users tooReporting Services roles.</span></span> <span data-ttu-id="1e1fc-372">如需詳細資訊，請參閱 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="1e1fc-372">For more information, see hello following:</span></span>

* [<span data-ttu-id="1e1fc-373">建立本機使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="1e1fc-373">Create a local user account</span></span>](https://technet.microsoft.com/library/cc770642.aspx)
* <span data-ttu-id="1e1fc-374">[授與使用者存取權 tooa 報表伺服器 （報表管理員）](https://msdn.microsoft.com/library/ms156034.aspx))</span><span class="sxs-lookup"><span data-stu-id="1e1fc-374">[Grant User Access tooa Report Server (Report Manager)](https://msdn.microsoft.com/library/ms156034.aspx))</span></span>
* [<span data-ttu-id="1e1fc-375">建立和管理角色指派</span><span class="sxs-lookup"><span data-stu-id="1e1fc-375">Create and Manage Role Assignments</span></span>](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a><span data-ttu-id="1e1fc-376">tooCreate 和發行報表 toohello Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="1e1fc-376">tooCreate and Publish Reports toohello Azure Virtual Machine</span></span>
<span data-ttu-id="1e1fc-377">hello 下表將摘要列出一些 hello Microsoft Azure 虛擬機器上裝載在內部部署電腦 toohello 報表伺服器中的 hello 選項可用 toopublish 現有報表：</span><span class="sxs-lookup"><span data-stu-id="1e1fc-377">hello following table summarizes some of hello options available toopublish existing reports from an on-premises computer toohello report server hosted on hello Microsoft Azure Virtual Machine:</span></span>

* <span data-ttu-id="1e1fc-378">**RS.exe 指令碼**： 使用 RS.exe 指令碼 toocopy 報表項目從和現有的報表伺服器 tooyour Microsoft Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-378">**RS.exe script**: Use RS.exe script toocopy report items from and existing report server tooyour Microsoft Azure Virtual Machine.</span></span> <span data-ttu-id="1e1fc-379">如需詳細資訊，請參閱 hello 節 「 原生模式 tooNative 模式 – Microsoft Azure 虛擬機器 」 中[Sample Reporting Services rs.exe 指令碼 tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-379">For more information, see hello section “Native mode tooNative Mode – Microsoft Azure Virtual Machine” in [Sample Reporting Services rs.exe Script tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>
* <span data-ttu-id="1e1fc-380">**報表產生器**: hello 虛擬機器包含 hello 按一下-click-once 版本的 Microsoft SQL Server 報表產生器。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-380">**Report Builder**: hello virtual machine includes hello click-once version of Microsoft SQL Server Report Builder.</span></span> <span data-ttu-id="1e1fc-381">toostart 報表產生器 hello hello 虛擬機器上的第一次：</span><span class="sxs-lookup"><span data-stu-id="1e1fc-381">toostart Report builder hello first time on hello virtual machine:</span></span>
  
  1. <span data-ttu-id="1e1fc-382">以管理權限啟動瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-382">Start your browser with administrative privileges.</span></span>
  2. <span data-ttu-id="1e1fc-383">瀏覽 tooreport 管理員 hello 虛擬機器上的，按一下**報表產生器**hello 功能區中。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-383">Browse tooreport manager on hello virtual machine and click **Report Builder**  in hello ribbon.</span></span>
     
     <span data-ttu-id="1e1fc-384">如需詳細資訊，請參閱 [安裝、解除安裝和支援報告產生器](https://technet.microsoft.com/library/dd207038.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-384">For more information, see [Installing, Uninstalling, and Supporting Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span></span>
* <span data-ttu-id="1e1fc-385">**SQL Server Data Tools: VM**： 如果您建立 hello VM 與 SQL Server 2012，則 SQL Server Data Tools 安裝在 hello 虛擬機器上，而且可以是使用的 toocreate**報表伺服器專案**與 hello 虛擬報表機器。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-385">**SQL Server Data Tools: VM**:  If you created hello VM with SQL Server 2012, then SQL Server Data Tools is installed on hello virtual machine and can be used toocreate **Report Server Projects** and reports on hello virtual machine.</span></span> <span data-ttu-id="1e1fc-386">SQL Server Data Tools 可以發佈 hello 報表 toohello hello 虛擬機器上的報表伺服器。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-386">SQL Server Data Tools can publish hello reports toohello report server on hello virtual machine.</span></span>
  
    <span data-ttu-id="1e1fc-387">如果您使用 SQL server 2014 建立 hello VM，您可以安裝 SQL Server Data Tools-BI for visual Studio。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-387">If you created hello VM with SQL server 2014, you can install SQL Server Data Tools- BI for visual Studio.</span></span> <span data-ttu-id="1e1fc-388">如需詳細資訊，請參閱 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="1e1fc-388">For more information, see hello following:</span></span>
  
  * [<span data-ttu-id="1e1fc-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="1e1fc-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span></span>](https://www.microsoft.com/download/details.aspx?id=42313)
  * [<span data-ttu-id="1e1fc-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="1e1fc-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=36843)
  * [<span data-ttu-id="1e1fc-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span><span class="sxs-lookup"><span data-stu-id="1e1fc-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span></span>](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* <span data-ttu-id="1e1fc-392">**SQL Server Data Tools：遠端**：在本機電腦上，以 SQL Server Data Tools 建立含有 Reporting Services 報告的 Reporting Services 專案。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-392">**SQL Server Data Tools: Remote**:  On your local computer, create a Reporting Services project in SQL Server Data Tools that contains Reporting Services reports.</span></span> <span data-ttu-id="1e1fc-393">設定 hello 專案 tooconnect toohello web 服務 URL。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-393">Configure hello project tooconnect toohello web service URL.</span></span>
  
    ![SSRS 專案的 ssdt 專案屬性](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* <span data-ttu-id="1e1fc-395">**使用指令碼**： 使用指令碼 toocopy 報表伺服器內容。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-395">**Use script**: Use script toocopy report server content.</span></span> <span data-ttu-id="1e1fc-396">如需詳細資訊，請參閱[Sample Reporting Services rs.exe 指令碼 tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-396">For more information, see [Sample Reporting Services rs.exe Script tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>

## <a name="minimize-cost-if-you-are-not-using-hello-vm"></a><span data-ttu-id="1e1fc-397">如果您不想要使用 hello VM，將成本降至最低</span><span class="sxs-lookup"><span data-stu-id="1e1fc-397">Minimize cost if you are not using hello VM</span></span>
> [!NOTE]
> <span data-ttu-id="1e1fc-398">toominimize 費用的 Azure 虛擬機器不在使用中，當關閉 hello VM 從 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-398">toominimize charges for your Azure Virtual Machines when not in use, shut down hello VM from hello Azure classic portal.</span></span> <span data-ttu-id="1e1fc-399">如果您使用內部 hello VM 關閉 VM tooshut hello Windows 電源選項時，您仍會收取的 hello 相同數量的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-399">If you use hello Windows power options inside a VM tooshut down hello VM, you are still charged hello same amount for hello VM.</span></span> <span data-ttu-id="1e1fc-400">tooreduce 費用，您需要 tooshut hello Azure 傳統入口網站中的 hello VM 關閉。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-400">tooreduce charges, you need tooshut down hello VM in hello Azure classic portal.</span></span> <span data-ttu-id="1e1fc-401">如果您不再需要 hello VM，請記住 toodelete hello VM 和 hello 相關聯的.vhd 檔案 tooavoid 儲存體費用。如需詳細資訊，請參閱 hello 常見問題集 > 一節[虛擬機器定價詳細資料](https://azure.microsoft.com/pricing/details/virtual-machines/)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-401">If you no longer need hello VM, remember toodelete hello VM and hello associated .vhd files tooavoid storage charges.For more information, see hello FAQ section at [Virtual Machines Pricing Details](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>

## <a name="more-information"></a><span data-ttu-id="1e1fc-402">相關資訊</span><span class="sxs-lookup"><span data-stu-id="1e1fc-402">More Information</span></span>
### <a name="resources"></a><span data-ttu-id="1e1fc-403">資源</span><span class="sxs-lookup"><span data-stu-id="1e1fc-403">Resources</span></span>
* <span data-ttu-id="1e1fc-404">如需類似內容相關 tooa 單一伺服器部署的 SQL Server Business Intelligence 及 SharePoint 2013，請參閱[使用 Windows PowerShell tooCreate Azure VM 與 SQL Server BI 和 SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-404">For similar content related tooa single server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Use Windows PowerShell tooCreate an Azure VM With SQL Server BI and SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span></span>
* <span data-ttu-id="1e1fc-405">類似的內容相關 tooa 多重伺服器部署的 SQL Server Business Intelligence 及 SharePoint 2013，請參閱[部署 SQL Server Business Intelligence Azure 虛擬機器中](https://msdn.microsoft.com/library/dn321998.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-405">For similar content related tooa multi-server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Deploy SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span></span>
* <span data-ttu-id="1e1fc-406">如需一般資訊相關的 toodeployments 的 SQL Server Business Intelligence Azure 虛擬機器中，請參閱[Azure 虛擬機器中 SQL Server Business Intelligence](virtual-machines-windows-classic-ps-sql-bi.md)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-406">For General information related toodeployments of SQL Server Business Intelligence in Azure Virtual Machines, see [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span></span>
* <span data-ttu-id="1e1fc-407">如需 hello 成本的 Azure 計算費用，請參閱 hello 虛擬機器 索引標籤的[Azure 定價計算機](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-407">For more information about hello cost of Azure compute charges, see hello Virtual Machines tab of [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span></span>

### <a name="community-content"></a><span data-ttu-id="1e1fc-408">社群內容</span><span class="sxs-lookup"><span data-stu-id="1e1fc-408">Community Content</span></span>
* <span data-ttu-id="1e1fc-409">如需 toocreate Reporting Services 原生模式報表伺服器不使用指令碼的方式的逐步指示，請參閱[託管 SQL Reporting 服務在 Azure 虛擬機器](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html)。</span><span class="sxs-lookup"><span data-stu-id="1e1fc-409">For step by step instructions on how toocreate a Reporting Services Native mode report server without using script, see [Hosting SQL Reporting Service on Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span></span>

### <a name="links-tooother-resources-for-sql-server-in-azure-vms"></a><span data-ttu-id="1e1fc-410">在 Azure Vm 中的 SQL Server 的連結 tooother 資源</span><span class="sxs-lookup"><span data-stu-id="1e1fc-410">Links tooother resources for SQL Server in Azure VMs</span></span>
[<span data-ttu-id="1e1fc-411">Azure 虛擬機器上的 SQL Server 概觀</span><span class="sxs-lookup"><span data-stu-id="1e1fc-411">SQL Server on Azure Virtual Machines Overview</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)


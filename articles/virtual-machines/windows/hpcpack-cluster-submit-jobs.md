---
title: "在 Azure 中的 aaaSubmit 作業 tooan HPC Pack 叢集 |Microsoft 文件"
description: "了解如何註冊內部部署電腦 toosubmit tooset 作業 tooan Azure 中的 HPC Pack 叢集"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 2918cf633917d8730487152e6a5ddb863eb8bb5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-tooan-hpc-pack-cluster-deployed-in-azure"></a><span data-ttu-id="f3fd8-103">提交從內部部署電腦 tooan HPC Pack 叢集中部署在 Azure 中的 HPC 工作</span><span class="sxs-lookup"><span data-stu-id="f3fd8-103">Submit HPC jobs from an on-premises computer tooan HPC Pack cluster deployed in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="f3fd8-104">設定內部部署用戶端電腦 toosubmit 作業 tooa [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029)在 Azure 中的叢集。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-104">Configure an on-premises client computer toosubmit jobs tooa [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure.</span></span> <span data-ttu-id="f3fd8-105">本文示範 tooset 本機電腦與用戶端如何透過在 Azure 中 HTTPS toohello 叢集工具 toosubmit 作業。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-105">This article shows you how tooset up a local computer with client tools toosubmit job over HTTPS toohello cluster in Azure.</span></span> <span data-ttu-id="f3fd8-106">如此一來，數個叢集使用者可以提交作業 tooa 雲端 HPC Pack 叢集中，但不會直接連接 toohello 前端節點 VM，或存取 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-106">In this way, several cluster users can submit jobs tooa cloud-based HPC Pack cluster, but without connecting directly toohello head node VM or accessing an Azure subscription.</span></span>

![提交 Azure 中的工作 tooa 叢集][jobsubmit]

## <a name="prerequisites"></a><span data-ttu-id="f3fd8-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="f3fd8-108">Prerequisites</span></span>
* <span data-ttu-id="f3fd8-109">**在 Azure VM 中部署 HPC Pack 前端節點**-我們建議您使用自動化的工具例如[Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)或[Azure PowerShell 指令碼](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)toodeploy hello 前端節點和叢集。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-109">**HPC Pack head node deployed in an Azure VM** - We recommend that you use automated tools such as an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/) or an [Azure PowerShell script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toodeploy hello head node and cluster.</span></span> <span data-ttu-id="f3fd8-110">您需要 hello 的 hello 前端節點的 DNS 名稱 」 和 「 叢集管理員來完成這篇文章中的 hello 步驟 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-110">You need hello DNS name of hello head node and hello credentials of a cluster administrator to complete hello steps in this article.</span></span>
* <span data-ttu-id="f3fd8-111">**用戶端電腦** - 您必須要有可執行 HPC Pack 用戶端公用程式的 Windows 或 Windows Server 用戶端電腦 (請參閱[系統需求](https://technet.microsoft.com/library/dn535781.aspx))。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-111">**Client computer** - You need a Windows or Windows Server client computer that can run HPC Pack client utilities (see [system requirements](https://technet.microsoft.com/library/dn535781.aspx)).</span></span> <span data-ttu-id="f3fd8-112">如果您只想 toouse hello HPC Pack web 入口網站或 REST API toosubmit 作業，您可以使用您選擇的任何用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-112">If you only want toouse hello HPC Pack web portal or REST API toosubmit jobs, you can use any client computer of your choice.</span></span>
* <span data-ttu-id="f3fd8-113">**HPC Pack 安裝媒體**-tooinstall hello HPC Pack 用戶端公用程式，hello 可用的安裝套件，可從 HPC Pack (HPC Pack 2012 R2) 的最新版本為[Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024)。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-113">**HPC Pack installation media** - tooinstall hello HPC Pack client utilities, hello free installation package for the latest version of HPC Pack (HPC Pack 2012 R2) is available from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="f3fd8-114">請確定您下載 hello 相同的 hello 前端節點 VM 上安裝 HPC Pack 版本。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-114">Make sure that you download hello same version of HPC Pack that is installed on hello head node VM.</span></span>

## <a name="step-1-install-and-configure-hello-web-components-on-hello-head-node"></a><span data-ttu-id="f3fd8-115">步驟 1： 安裝及設定 hello 前端節點上的 hello web 元件</span><span class="sxs-lookup"><span data-stu-id="f3fd8-115">Step 1: Install and configure hello web components on hello head node</span></span>
<span data-ttu-id="f3fd8-116">tooenable REST 介面 toosubmit 作業 toohello 叢集透過 HTTPS，請確定 hello HPC Pack web 元件進行設定 hello HPC Pack 前端節點上。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-116">tooenable a REST interface toosubmit jobs toohello cluster over HTTPS, ensure that hello HPC Pack web components are configured on hello HPC Pack head node.</span></span> <span data-ttu-id="f3fd8-117">如果它們尚未安裝，先執行 HpcWebComponents.msi 安裝檔案以 hello 安裝 hello web 元件。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-117">If they aren't already installed, first install hello web components by running hello HpcWebComponents.msi installation file.</span></span> <span data-ttu-id="f3fd8-118">然後，執行 hello HPC PowerShell 指令碼設定 hello 元件**Set-hpcwebcomponents.ps1**。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-118">Then, configure hello components by running hello HPC PowerShell script **Set-HPCWebComponents.ps1**.</span></span>

<span data-ttu-id="f3fd8-119">如需詳細的程序，請參閱[安裝 hello Microsoft HPC Pack Web 元件](http://technet.microsoft.com/library/hh314627.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-119">For detailed procedures, see [Install hello Microsoft HPC Pack Web Components](http://technet.microsoft.com/library/hh314627.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="f3fd8-120">某些 Azure 快速入門範本為 HPC Pack 安裝和自動設定 hello web 元件。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-120">Certain Azure quickstart templates for HPC Pack install and configure hello web components automatically.</span></span> <span data-ttu-id="f3fd8-121">如果您使用 hello [HPC Pack IaaS 部署指令碼](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)toocreate hello 叢集中，您可以選擇性地安裝和設定 hello web 元件為 hello 部署的一部分。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-121">If you use hello [HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate hello cluster, you can optionally install and configure hello web components as part of hello deployment.</span></span>
> 
> 

<span data-ttu-id="f3fd8-122">**tooinstall hello web 元件**</span><span class="sxs-lookup"><span data-stu-id="f3fd8-122">**tooinstall hello web components**</span></span>

1. <span data-ttu-id="f3fd8-123">使用叢集系統管理員認證 hello 連接 toohello 前端節點 VM。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-123">Connect toohello head node VM by using hello credentials of a cluster administrator.</span></span>
2. <span data-ttu-id="f3fd8-124">Hello HPC Pack 安裝程式資料夾中，請在 hello 前端節點上執行 HpcWebComponents.msi。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-124">From hello HPC Pack Setup folder, run HpcWebComponents.msi on hello head node.</span></span>
3. <span data-ttu-id="f3fd8-125">Hello 精靈 tooinstall hello web 元件中的 hello 步驟</span><span class="sxs-lookup"><span data-stu-id="f3fd8-125">Follow hello steps in hello wizard tooinstall hello web components</span></span>

<span data-ttu-id="f3fd8-126">**tooconfigure hello web 元件**</span><span class="sxs-lookup"><span data-stu-id="f3fd8-126">**tooconfigure hello web components**</span></span>

1. <span data-ttu-id="f3fd8-127">Hello 前端節點上，系統管理員身分啟動 HPC PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-127">On hello head node, start HPC PowerShell as an administrator.</span></span>
2. <span data-ttu-id="f3fd8-128">toochange 目錄 toohello hello 組態指令碼，下列命令的型別 hello 的位置：</span><span class="sxs-lookup"><span data-stu-id="f3fd8-128">toochange directory toohello location of hello configuration script, type hello following command:</span></span>
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. <span data-ttu-id="f3fd8-129">tooconfigure hello REST 介面，並啟動 hello HPC Web 服務，下列命令的型別 hello:</span><span class="sxs-lookup"><span data-stu-id="f3fd8-129">tooconfigure hello REST interface and start hello HPC Web Service, type hello following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. <span data-ttu-id="f3fd8-130">當提示的 tooselect 憑證時，選擇 hello 憑證對應 toohello 公開 DNS 名稱的 hello 前端節點。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-130">When prompted tooselect a certificate, choose hello certificate that corresponds toohello public DNS name of hello head node.</span></span> <span data-ttu-id="f3fd8-131">例如，如果您部署的 hello 前端節點 VM 使用 hello 傳統部署模型，hello 憑證名稱看起來像 CN =&lt;*HeadNodeDnsName*&gt;。.cloudapp.net。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-131">For example, if you deploy hello head node VM using hello classic deployment model, hello certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net.</span></span> <span data-ttu-id="f3fd8-132">如果您使用 hello Resource Manager 部署模型，hello 憑證名稱看起來像 CN =&lt;*HeadNodeDnsName*&gt;。&lt;*區域*&gt;。 cloudapp.azure.com。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-132">If you use hello Resource Manager deployment model, hello certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.&lt;*region*&gt;.cloudapp.azure.com.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f3fd8-133">您選取此憑證，稍後當您提交從內部部署電腦作業 toohello 前端節點。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-133">You select this certificate later when you submit jobs toohello head node from an on-premises computer.</span></span> <span data-ttu-id="f3fd8-134">請勿選取或設定對應 toohello hello Active Directory 網域中的 hello 前端節點電腦名稱的憑證 (例如，CN =*MyHPCHeadNode.HpcAzure.local*)。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-134">Don't select or configure a certificate that corresponds toohello computer name of hello head node in hello Active Directory domain (for example, CN=*MyHPCHeadNode.HpcAzure.local*).</span></span>
   > 
   > 
5. <span data-ttu-id="f3fd8-135">tooconfigure hello 入口網站提交作業，下列命令的型別 hello:</span><span class="sxs-lookup"><span data-stu-id="f3fd8-135">tooconfigure hello web portal for job submission, type hello following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. <span data-ttu-id="f3fd8-136">Hello 指令碼完成之後，停止並重新啟動請輸入下列命令的 hello hello HPC 工作排程器服務：</span><span class="sxs-lookup"><span data-stu-id="f3fd8-136">After hello script completes, stop and restart hello HPC Job Scheduler Service by typing hello following commands:</span></span>
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-hello-hpc-pack-client-utilities-on-an-on-premises-computer"></a><span data-ttu-id="f3fd8-137">步驟 2： 在內部部署電腦上安裝 hello HPC Pack 用戶端公用程式</span><span class="sxs-lookup"><span data-stu-id="f3fd8-137">Step 2: Install hello HPC Pack client utilities on an on-premises computer</span></span>
<span data-ttu-id="f3fd8-138">如果您想 tooinstall hello HPC Pack 用戶端公用程式在您的電腦上，下載 HPC Pack 安裝檔案 （完整安裝） 從 hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024)。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-138">If you want tooinstall hello HPC Pack client utilities on your computer, download the HPC Pack setup files (full installation) from hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="f3fd8-139">當您開始 hello 安裝時，請選擇 hello hello 安裝選項**HPC Pack 用戶端公用程式**。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-139">When you begin hello installation, choose hello setup option for hello **HPC Pack client utilities**.</span></span>

<span data-ttu-id="f3fd8-140">toouse hello HPC Pack 用戶端工具 toosubmit 作業 toohello 前端節點 VM，您也需要 tooexport hello 前端節點的憑證，並在 hello 用戶端電腦上安裝它。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-140">toouse hello HPC Pack client tools toosubmit jobs toohello head node VM, you also need tooexport a certificate from hello head node and install it on hello client computer.</span></span> <span data-ttu-id="f3fd8-141">hello 憑證必須位於中。CER 格式。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-141">hello certificate must be in .CER format.</span></span>

<span data-ttu-id="f3fd8-142">**tooexport hello 憑證從 hello 前端節點**</span><span class="sxs-lookup"><span data-stu-id="f3fd8-142">**tooexport hello certificate from hello head node**</span></span>

1. <span data-ttu-id="f3fd8-143">Hello 前端節點上，新增 hello 憑證嵌入式管理單元 tooa Microsoft Management Console hello 本機電腦帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-143">On hello head node, add hello Certificates snap-in tooa Microsoft Management Console for hello Local Computer account.</span></span> <span data-ttu-id="f3fd8-144">如需 tooadd hello 嵌入式管理單元的步驟，請參閱[新增憑證嵌入式管理單元 tooan hello MMC](https://technet.microsoft.com/library/cc754431.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-144">For steps tooadd hello snap-in, see [Add hello Certificates Snap-in tooan MMC](https://technet.microsoft.com/library/cc754431.aspx).</span></span>
2. <span data-ttu-id="f3fd8-145">在 hello 主控台樹狀目錄中，展開**憑證-本機電腦** > **個人**，然後按一下**憑證**。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-145">In hello console tree, expand **Certificates – Local Computer** > **Personal**, and then click **Certificates**.</span></span>
3. <span data-ttu-id="f3fd8-146">找出您設定 hello HPC Pack web 元件中的 hello 憑證[步驟 1： 安裝及設定 hello 前端節點上的 hello web 元件](#step-1:-install-and-configure-the-web-components-on-the-head-node)(例如，CN =&lt;*HeadNodeDnsName* &gt;。.cloudapp.net)。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-146">Locate hello certificate that you configured for hello HPC Pack web components in [Step 1: Install and configure hello web components on hello head node](#step-1:-install-and-configure-the-web-components-on-the-head-node) (for example, CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net).</span></span>
4. <span data-ttu-id="f3fd8-147">以滑鼠右鍵按一下 hello 憑證，然後按一下**所有工作** > **匯出**。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-147">Right-click hello certificate, and click **All Tasks** > **Export**.</span></span>
5. <span data-ttu-id="f3fd8-148">在 [hello 憑證匯出精靈] 中，按一下 [**下一步]**，並確定**否，不要匯出 hello 私密金鑰**已選取。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-148">In hello Certificate Export Wizard, click **Next**, and ensure that **No, do not export hello private key** is selected.</span></span>
6. <span data-ttu-id="f3fd8-149">後續 hello 剩餘步驟，以 DER hello 精靈 tooexport hello 憑證編碼的二進位 X.509 (。CER) 格式。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-149">Follow hello remaining steps of hello wizard tooexport hello certificate in DER encoded binary X.509 (.CER) format.</span></span>

<span data-ttu-id="f3fd8-150">**hello 用戶端電腦上的 tooimport hello 憑證**</span><span class="sxs-lookup"><span data-stu-id="f3fd8-150">**tooimport hello certificate on hello client computer**</span></span>

1. <span data-ttu-id="f3fd8-151">複製 hello hello 用戶端電腦上的 hello 前端節點 tooa 資料夾從匯出的憑證。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-151">Copy hello certificate that you exported from hello head node tooa folder on hello client computer.</span></span>
2. <span data-ttu-id="f3fd8-152">Hello 用戶端電腦上，執行 certmgr.msc。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-152">On hello client computer, run certmgr.msc.</span></span>
3. <span data-ttu-id="f3fd8-153">在 憑證管理員 中，展開 憑證 - 目前的使用者  >  受信任的根憑證授權單位，在 憑證 上按一下滑鼠右鍵，然後按一下所有工作  >  匯入。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-153">In Certificate Manager, expand **Certificates – Current user** > **Trusted Root Certification Authorities**, right-click **Certificates**, and then click **All Tasks** > **Import**.</span></span>
4. <span data-ttu-id="f3fd8-154">在 hello 憑證匯入精靈，按一下 **下一步**和後續 hello 步驟 tooimport hello 憑證從信任的根憑證授權單位存放區的 hello 前端節點 toohello 匯出。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-154">In hello Certificate Import Wizard, click **Next** and follow hello steps tooimport hello certificate that you exported from hello head node toohello Trusted Root Certification Authorities store.</span></span>

> [!TIP]
> <span data-ttu-id="f3fd8-155">您可能會看到安全性警告，因為 hello 用戶端電腦不辨識 hello hello 前端節點上的憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-155">You might see a security warning, because hello certification authority on hello head node isn't recognized by hello client computer.</span></span> <span data-ttu-id="f3fd8-156">為了測試用途，您可以忽略此警告和完整 hello 憑證匯入。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-156">For testing purposes, you can ignore this warning and complete hello certificate import.</span></span>
> 
> 

## <a name="step-3-run-test-jobs-on-hello-cluster"></a><span data-ttu-id="f3fd8-157">Hello 叢集上的步驟 3： 執行測試工作</span><span class="sxs-lookup"><span data-stu-id="f3fd8-157">Step 3: Run test jobs on hello cluster</span></span>
<span data-ttu-id="f3fd8-158">您的設定，再試一次執行中的作業上 hello 叢集在 Azure 中從 hello tooverify 內部部署電腦。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-158">tooverify your configuration, try running jobs on hello cluster in Azure from hello on-premises computer.</span></span> <span data-ttu-id="f3fd8-159">例如，您可以使用 HPC Pack GUI 工具或命令列命令 toosubmit 作業 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-159">For example, you can use HPC Pack GUI tools or command-line commands toosubmit jobs toohello cluster.</span></span> <span data-ttu-id="f3fd8-160">您也可以使用網頁型入口網站 toosubmit 作業。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-160">You can also use a web-based portal toosubmit jobs.</span></span>

<span data-ttu-id="f3fd8-161">**hello 用戶端電腦上的 toorun 作業提交命令**</span><span class="sxs-lookup"><span data-stu-id="f3fd8-161">**toorun job submission commands on hello client computer**</span></span>

1. <span data-ttu-id="f3fd8-162">用戶端電腦上安裝 hello HPC Pack 用戶端公用程式，啟動 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-162">On a client computer where hello HPC Pack client utilities are installed, start a Command Prompt.</span></span>
2. <span data-ttu-id="f3fd8-163">輸入範例命令。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-163">Type a sample command.</span></span> <span data-ttu-id="f3fd8-164">例如，toolist hello 叢集上的所有工作都輸入 hello 接下來，根據 hello 前端節點的 hello 完整 DNS 名稱的命令類似 tooone:</span><span class="sxs-lookup"><span data-stu-id="f3fd8-164">For example, toolist all jobs on hello cluster, type a command similar tooone of hello following, depending on hello full DNS name of hello head node:</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    <span data-ttu-id="f3fd8-165">或</span><span class="sxs-lookup"><span data-stu-id="f3fd8-165">or</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > <span data-ttu-id="f3fd8-166">Hello 排程器的 URL 中使用 hello 前端節點之後，不 hello IP 位址，hello 完整 DNS 的名稱。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-166">Use hello full DNS name of hello head node, not hello IP address, in hello scheduler URL.</span></span> <span data-ttu-id="f3fd8-167">如果您指定 hello IP 位址，錯誤會出現類似太"hello 伺服器憑證必須 tooeither 具有有效信任或 toobe 放入 hello 受信任的根存放區的鏈結。 」</span><span class="sxs-lookup"><span data-stu-id="f3fd8-167">If you specify hello IP address, an error appears similar too"hello server certificate needs tooeither have a valid chain of trust or toobe placed in hello trusted root store."</span></span>
   > 
   > 
3. <span data-ttu-id="f3fd8-168">出現提示時，輸入 hello 使用者名稱 (hello 形式&lt;DomainName&gt;\\&lt;UserName&gt;) 和 hello HPC 叢集管理員或另一個您所設定之叢集使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-168">When prompted, type hello user name (in hello form &lt;DomainName&gt;\\&lt;UserName&gt;) and password of hello HPC cluster administrator or another cluster user that you configured.</span></span> <span data-ttu-id="f3fd8-169">您可以選擇 toostore hello 認證，在本機供更多作業。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-169">You can choose toostore hello credentials locally for more job operations.</span></span>
   
    <span data-ttu-id="f3fd8-170">工作清單隨即出現。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-170">A list of jobs appears.</span></span>

<span data-ttu-id="f3fd8-171">**hello 用戶端電腦上的 toouse HPC 作業管理員**</span><span class="sxs-lookup"><span data-stu-id="f3fd8-171">**toouse HPC Job Manager on hello client computer**</span></span>

1. <span data-ttu-id="f3fd8-172">如果您先前沒有儲存叢集使用者的網域認證提交作業時，您可以加入 hello 認證在認證管理員。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-172">If you didn't previously store domain credentials for a cluster user when submitting a job, you can add hello credentials in Credential Manager.</span></span>
   
    <span data-ttu-id="f3fd8-173">a.</span><span class="sxs-lookup"><span data-stu-id="f3fd8-173">a.</span></span> <span data-ttu-id="f3fd8-174">在控制台中 hello 用戶端電腦上啟動認證管理員。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-174">In Control Panel on hello client computer, start Credential Manager.</span></span>
   
    <span data-ttu-id="f3fd8-175">b.</span><span class="sxs-lookup"><span data-stu-id="f3fd8-175">b.</span></span> <span data-ttu-id="f3fd8-176">按一下 [Windows 認證] >  [新增一般認證]。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-176">Click **Windows Credentials** > **Add a generic credential**.</span></span>
   
    <span data-ttu-id="f3fd8-177">c.</span><span class="sxs-lookup"><span data-stu-id="f3fd8-177">c.</span></span> <span data-ttu-id="f3fd8-178">指定 hello 網際網路位址 (例如 https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler 或 https://&lt;HeadNodeDnsName&gt;。&lt;區域&gt;.cloudapp.azure.com/HpcScheduler)，和 hello 使用者名稱 (&lt;DomainName&gt;\\&lt;UserName&gt;) 和密碼的 hello 叢集系統管理員或另一個您所設定之叢集使用者。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-178">Specify hello Internet address (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com/HpcScheduler), and hello user name (&lt;DomainName&gt;\\&lt;UserName&gt;) and password of hello cluster administrator or another cluster user that you configured.</span></span>
2. <span data-ttu-id="f3fd8-179">Hello 用戶端電腦上，啟動 HPC 作業管理員。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-179">On hello client computer, start HPC Job Manager.</span></span>
3. <span data-ttu-id="f3fd8-180">在 hello**選取前端節點**對話方塊中，型別 hello URL toohello Azure 前端節點 (例如 https://&lt;HeadNodeDnsName&gt;。.cloudapp.net 或 https://&lt;HeadNodeDnsName&gt;.&lt;區域&gt;。 cloudapp.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-180">In hello **Select Head Node** dialog box, type hello URL toohello head node in Azure (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com).</span></span>
   
    <span data-ttu-id="f3fd8-181">HPC 作業管理員隨即開啟，並顯示 hello 前端節點上的 工作清單。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-181">HPC Job Manager opens and shows a list of jobs on hello head node.</span></span>

<span data-ttu-id="f3fd8-182">**hello 前端節點上執行的 toouse hello web 入口網站**</span><span class="sxs-lookup"><span data-stu-id="f3fd8-182">**toouse hello web portal running on hello head node**</span></span>

1. <span data-ttu-id="f3fd8-183">Hello 用戶端電腦上，啟動 web 瀏覽器並輸入下列位址，根據 hello 完整 DNS 名稱的 hello 前端節點的 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="f3fd8-183">Start a web browser on hello client computer, and enter one of hello following addresses, depending on hello full DNS name of hello head node:</span></span>
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    <span data-ttu-id="f3fd8-184">或</span><span class="sxs-lookup"><span data-stu-id="f3fd8-184">or</span></span>
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. <span data-ttu-id="f3fd8-185">在出現 hello 安全性對話方塊中，輸入 hello hello HPC 叢集管理員的網域認證。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-185">In hello security dialog box that appears, type hello domain credentials of hello HPC cluster administrator.</span></span> <span data-ttu-id="f3fd8-186">(您也可以在不同的角色中新增其他叢集使用者。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-186">(You can also add other cluster users in different roles.</span></span> <span data-ttu-id="f3fd8-187">請參閱[管理叢集使用者](https://technet.microsoft.com/library/ff919335.aspx)。)</span><span class="sxs-lookup"><span data-stu-id="f3fd8-187">See [Managing Cluster Users](https://technet.microsoft.com/library/ff919335.aspx).)</span></span>
   
    <span data-ttu-id="f3fd8-188">hello web 入口網站開啟 toohello 工作清單 檢視。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-188">hello web portal opens toohello job list view.</span></span>
3. <span data-ttu-id="f3fd8-189">按一下 toosubmit hello 叢集中，從傳回 hello 字串"Hello World"的範例作業**新工作**hello 左側功能窗格中。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-189">toosubmit a sample job that returns hello string “Hello World” from hello cluster, click **New job** in hello left-hand navigation.</span></span>
4. <span data-ttu-id="f3fd8-190">在 hello**新工作**頁面的 **從提交頁面**，按一下  **HelloWorld**。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-190">On hello **New Job** page, under **From submission pages**, click **HelloWorld**.</span></span> <span data-ttu-id="f3fd8-191">hello 作業提交頁面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-191">hello job submission page appears.</span></span>
5. <span data-ttu-id="f3fd8-192">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-192">Click **Submit**.</span></span> <span data-ttu-id="f3fd8-193">如果出現提示，提供 hello hello HPC 叢集管理員的網域認證。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-193">If prompted, provide hello domain credentials of hello HPC cluster administrator.</span></span> <span data-ttu-id="f3fd8-194">送出 hello 作業，且 hello 作業識別碼會顯示在 hello**我的工作**頁面。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-194">hello job is submitted, and hello job ID appears on hello **My Jobs** page.</span></span>
6. <span data-ttu-id="f3fd8-195">您送出的 hello 工作 tooview hello 結果按一下 hello 作業識別碼，然後按一下**檢視工作**tooview hello 命令輸出 (下**輸出**)。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-195">tooview hello results of hello job that you submitted, click hello job ID, and then click **View Tasks** tooview hello command output (under **Output**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3fd8-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f3fd8-196">Next steps</span></span>
* <span data-ttu-id="f3fd8-197">您也可以提交作業 toohello Azure 叢集概略以 hello [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-197">You can also submit jobs toohello Azure cluster with hello [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span>
* <span data-ttu-id="f3fd8-198">如果您想從 Linux 用戶端 toosubmit 叢集作業，請參閱 hello Python hello 範例[HPC Pack 2012 R2 SDK 和範例程式碼](https://www.microsoft.com/download/details.aspx?id=41633)。</span><span class="sxs-lookup"><span data-stu-id="f3fd8-198">If you want toosubmit cluster jobs from a Linux client, see hello Python sample in hello [HPC Pack 2012 R2 SDK and Sample Code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span>

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png

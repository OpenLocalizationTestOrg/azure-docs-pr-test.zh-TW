---
title: "Azure 至 Azure 複寫問題和錯誤的 Azure Site Recovery 疑難排解 | Microsoft Docs"
description: "對於複寫 Azure 虛擬機器進行嚴重損壞修復時發生的錯誤和問題進行疑難排解"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/10/2017
ms.author: sujayt
ms.openlocfilehash: 4e4e8b097fbab3ddce551eb93945d0880f8c457f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-to-azure-vm-replication-issues"></a><span data-ttu-id="445b5-103">Azure 至 Azure VM 複寫問題的疑難排解</span><span class="sxs-lookup"><span data-stu-id="445b5-103">Troubleshoot Azure-to-Azure VM replication issues</span></span>

<span data-ttu-id="445b5-104">本文說明從一個區域將 Azure 虛擬機器複寫和復原到另一個區域時，關於 Azure Site Recovery 的常見問題，並解說如何進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="445b5-104">This article describes the common issues in Azure Site Recovery when replicating and recovering Azure virtual machines from one region to another region and explains how to troubleshoot them.</span></span> <span data-ttu-id="445b5-105">如需受支援組態的詳細資訊，請參閱[複寫 Azure VM 的支援矩陣](site-recovery-support-matrix-azure-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="445b5-105">For more information about supported configurations, see the [support matrix for replicating Azure VMs](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="azure-resource-quota-issues-error-code-150097"></a><span data-ttu-id="445b5-106">Azure 資源配額問題 (錯誤碼 150097)</span><span class="sxs-lookup"><span data-stu-id="445b5-106">Azure resource quota issues (error code 150097)</span></span>
<span data-ttu-id="445b5-107">您的訂用帳戶應該啟用，才能在要做為災害復原區域的目標區域中建立 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="445b5-107">Your subscription should be enabled to create Azure VMs in the target region that you plan to use as your disaster recovery region.</span></span> <span data-ttu-id="445b5-108">此外，您的訂用帳戶應該已啟用足夠的配額，才能建立特定大小的 VM。</span><span class="sxs-lookup"><span data-stu-id="445b5-108">Also, your subscription should have sufficient quota enabled to create VMs of specific size.</span></span> <span data-ttu-id="445b5-109">根據預設，Site Recovery 會取用相同大小的目標 VM 做為來源 VM。</span><span class="sxs-lookup"><span data-stu-id="445b5-109">By default, Site Recovery picks the same size for the target VM as the source VM.</span></span> <span data-ttu-id="445b5-110">如果沒有相符大小，系統會自動挑選最接近的大小。</span><span class="sxs-lookup"><span data-stu-id="445b5-110">If the matching size isn't available, the closest possible size is picked automatically.</span></span> <span data-ttu-id="445b5-111">如果沒有支援來源 VM 組態的相符大小，則會出現下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="445b5-111">If there's no matching size that supports source VM configuration, this error message appears:</span></span>

<span data-ttu-id="445b5-112">**錯誤碼**</span><span class="sxs-lookup"><span data-stu-id="445b5-112">**Error code**</span></span> | <span data-ttu-id="445b5-113">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="445b5-113">**Possible causes**</span></span> | <span data-ttu-id="445b5-114">**建議**</span><span class="sxs-lookup"><span data-stu-id="445b5-114">**Recommendation**</span></span>
--- | --- | ---
<span data-ttu-id="445b5-115">150097</span><span class="sxs-lookup"><span data-stu-id="445b5-115">150097</span></span><br></br><span data-ttu-id="445b5-116">**訊息**：虛擬機器 VmName 無法啟用複寫。</span><span class="sxs-lookup"><span data-stu-id="445b5-116">**Message**: Replication couldn't be enabled for the virtual machine VmName.</span></span> | <span data-ttu-id="445b5-117">- 可能未啟用您的訂用帳戶 ID 在目標區域位置中建立任何 VM。</span><span class="sxs-lookup"><span data-stu-id="445b5-117">- Your subscription ID might not be enabled to create any VMs in the target region location.</span></span></br></br><span data-ttu-id="445b5-118">- 可能未啟用您的訂用帳戶 ID 或沒有足夠的配額可在目標區域位置中建立特定 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="445b5-118">- Your subscription ID might not be enabled or doesn't have sufficient quota to create specific VM sizes in the target region location.</span></span></br></br><span data-ttu-id="445b5-119">- 對於目標區域位置中的訂用帳戶 ID，找不到符合來源 VM NIC 計數 (2) 的適當 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="445b5-119">- A suitable target VM size that matches the source VM NIC count (2) isn't found for the subscription ID in the target region location.</span></span>| <span data-ttu-id="445b5-120">對於訂用帳戶的目標位置之中的所需 VM 大小，請連絡 [Azure 計費支援](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request)啟用 VM。</span><span class="sxs-lookup"><span data-stu-id="445b5-120">Contact [Azure billing support](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) to enable VM creation for the required VM sizes in the target location for your subscription.</span></span> <span data-ttu-id="445b5-121">啟用後，請重試失敗的作業。</span><span class="sxs-lookup"><span data-stu-id="445b5-121">After it's enabled, retry the failed operation.</span></span>

### <a name="fix-the-problem"></a><span data-ttu-id="445b5-122">修正問題</span><span class="sxs-lookup"><span data-stu-id="445b5-122">Fix the problem</span></span>
<span data-ttu-id="445b5-123">您可以連絡 [Azure 計費支援](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request)啟用訂用帳戶，在目標位置中建立所需大小的 VM。</span><span class="sxs-lookup"><span data-stu-id="445b5-123">You can contact [Azure billing support](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) to enable your subscription to create VMs of required sizes in the target location.</span></span>

<span data-ttu-id="445b5-124">如果目標位置有容量限制，請停用複寫，並對於訂用帳戶有足夠配額的不同位置啟用複寫，以建立所需大小的 VM。</span><span class="sxs-lookup"><span data-stu-id="445b5-124">If the target location has a capacity constraint, disable replication and enable it to a different location where your subscription has sufficient quota to create VMs of the required sizes.</span></span>

## <a name="trusted-root-certificates-error-code-151066"></a><span data-ttu-id="445b5-125">受信任的根憑證 (錯誤碼 151066)</span><span class="sxs-lookup"><span data-stu-id="445b5-125">Trusted root certificates (error code 151066)</span></span>

<span data-ttu-id="445b5-126">如果 VM 沒有所有最新的受信任根憑證，「啟用複寫」工作可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="445b5-126">If all the latest trusted root certificates aren't present on the VM, your "enable replication" job might fail.</span></span> <span data-ttu-id="445b5-127">如果沒有憑證，對於從 VM 的 Site Recovery 服務呼叫進行的驗證和授權會失敗。</span><span class="sxs-lookup"><span data-stu-id="445b5-127">Without the certificates, the authentication and authorization of Site Recovery service calls from the VM fail.</span></span> <span data-ttu-id="445b5-128">失敗的「啟用複寫」Site Recovery 工作的錯誤訊息會出現：</span><span class="sxs-lookup"><span data-stu-id="445b5-128">The error message for the failed "enable replication" Site Recovery job appears:</span></span>

<span data-ttu-id="445b5-129">**錯誤碼**</span><span class="sxs-lookup"><span data-stu-id="445b5-129">**Error code**</span></span> | <span data-ttu-id="445b5-130">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="445b5-130">**Possible cause**</span></span> | <span data-ttu-id="445b5-131">**建議**</span><span class="sxs-lookup"><span data-stu-id="445b5-131">**Recommendations**</span></span>
--- | --- | ---
<span data-ttu-id="445b5-132">151066</span><span class="sxs-lookup"><span data-stu-id="445b5-132">151066</span></span><br></br><span data-ttu-id="445b5-133">**訊息**：Site Recovery 組態失敗。</span><span class="sxs-lookup"><span data-stu-id="445b5-133">**Message**: Site Recovery configuration failed.</span></span> | <span data-ttu-id="445b5-134">機器上不存在用於授權和驗證的受信任根憑證。</span><span class="sxs-lookup"><span data-stu-id="445b5-134">The required trusted root certificates used for authorization and authentication aren't present on the machine.</span></span> | <span data-ttu-id="445b5-135">- 對於執行 Windows 作業系統的 VM，請確定機器上存在受信任根憑證。</span><span class="sxs-lookup"><span data-stu-id="445b5-135">- For a VM running the Windows operating system, ensure that the trusted root certificates are present on the machine.</span></span> <span data-ttu-id="445b5-136">如需資訊，請參閱[設定受信任根目錄和不允許的憑證](https://technet.microsoft.com/library/dn265983.aspx)。</span><span class="sxs-lookup"><span data-stu-id="445b5-136">For information, see  [Configure trusted roots and disallowed certificates](https://technet.microsoft.com/library/dn265983.aspx).</span></span><br></br><span data-ttu-id="445b5-137">- 對於執行 Linux 作業系統的 VM，請依照 Linux 作業系統版本散發者發行的受信任根憑證適用的指引。</span><span class="sxs-lookup"><span data-stu-id="445b5-137">- For a VM running the Linux operating system, follow the guidance for trusted root certificates published by the Linux operating system version distributor.</span></span>

### <a name="fix-the-problem"></a><span data-ttu-id="445b5-138">修正問題</span><span class="sxs-lookup"><span data-stu-id="445b5-138">Fix the problem</span></span>
<span data-ttu-id="445b5-139">**Windows**</span><span class="sxs-lookup"><span data-stu-id="445b5-139">**Windows**</span></span>

<span data-ttu-id="445b5-140">在 VM 上安裝所有最新的 Windows 更新，使機器上存在所有的受信任根憑證。</span><span class="sxs-lookup"><span data-stu-id="445b5-140">Install all the latest Windows updates on the VM so that all the trusted root certificates are present on the machine.</span></span> <span data-ttu-id="445b5-141">如果您是在中斷連線的環境，請遵循您組織的標準 Windows 更新程序來取得憑證。</span><span class="sxs-lookup"><span data-stu-id="445b5-141">If you're in a disconnected environment, follow the standard Windows update process in your organization to get the certificates.</span></span> <span data-ttu-id="445b5-142">如果 VM 上不存在所需的憑證，對於 Site Recovery 進行的呼叫將而於安全性因素而失敗。</span><span class="sxs-lookup"><span data-stu-id="445b5-142">If the required certificates aren't present on the VM, the calls to the Site Recovery service fail for security reasons.</span></span>

<span data-ttu-id="445b5-143">遵循您組織的一般 Windows 更新管理或憑證更新管理程序，取得所有最新的根憑證以及 VM 上更新的憑證撤銷清單。</span><span class="sxs-lookup"><span data-stu-id="445b5-143">Follow the typical Windows update management or certificate update management process in your organization to get all the latest root certificates and the updated certificate revocation list on the VMs.</span></span>

<span data-ttu-id="445b5-144">若要確認問題已解決，請在 VM 中從瀏覽器移至 login.microsoftonline.com。</span><span class="sxs-lookup"><span data-stu-id="445b5-144">To verify that the issue is resolved, go to login.microsoftonline.com from a browser in your VM.</span></span>

<span data-ttu-id="445b5-145">**Linux**</span><span class="sxs-lookup"><span data-stu-id="445b5-145">**Linux**</span></span>

<span data-ttu-id="445b5-146">請遵循 Linux 散發者提供的指引，取得最新的受信任根憑證以及 VM 上最新的憑證撤銷清單。</span><span class="sxs-lookup"><span data-stu-id="445b5-146">Follow the guidance provided by your Linux distributor to get the latest trusted root certificates and the latest certificate revocation list on the VM.</span></span>

<span data-ttu-id="445b5-147">因為 SuSE Linux 使用符號連結來維護憑證清單，因此請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="445b5-147">Because SuSE Linux uses symlinks to maintain a certificate list, follow these steps:</span></span>

1.  <span data-ttu-id="445b5-148">以根使用者身分登入。</span><span class="sxs-lookup"><span data-stu-id="445b5-148">Sign in as a root user.</span></span>

2.  <span data-ttu-id="445b5-149">請執行這個命令：</span><span class="sxs-lookup"><span data-stu-id="445b5-149">Run this command:</span></span>

      ``# cd /etc/ssl/certs``

3.  <span data-ttu-id="445b5-150">若要查看 Symantec 根 CA 憑證是否存在，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="445b5-150">To see if the Symantec root CA certificate is present or not, run this command:</span></span>

      ``# ls VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

4.  <span data-ttu-id="445b5-151">如果找不到檔案，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="445b5-151">If the file isn't found, run these commands:</span></span>

      ``# wget https://www.symantec.com/content/dam/symantec/docs/other-resources/verisign-class-3-public-primary-certification-authority-g5-en.pem -O VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

      ``# c_rehash``

5.  <span data-ttu-id="445b5-152">若要使用 b204d74a.0 建立符號連結 -> VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="445b5-152">To create a symlink with b204d74a.0 -> VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem, run this command:</span></span>

      ``# ln -s  VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem b204d74a.0``

6.  <span data-ttu-id="445b5-153">請檢查此命令是否有下列的輸出。</span><span class="sxs-lookup"><span data-stu-id="445b5-153">Check to see if this command has the following output.</span></span> <span data-ttu-id="445b5-154">如果沒有，則您必須建立符號連結：</span><span class="sxs-lookup"><span data-stu-id="445b5-154">If not, you have to create a symlink:</span></span>

      ``# ls -l | grep Baltimore
      -rw-r--r-- 1 root root   1303 Apr  7  2016 Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 04:47 3ad48a91.0 -> Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 05:01 653b494a.0 -> Baltimore_CyberTrust_Root.pem``

7. <span data-ttu-id="445b5-155">如果符號連結 653b494a.0 不存在，請使用此命令建立符號連結：</span><span class="sxs-lookup"><span data-stu-id="445b5-155">If symlink 653b494a.0 isn't present, use this command to create a symlink:</span></span>

      ``# ln -s Baltimore_CyberTrust_Root.pem 653b494a.0``


## <a name="outbound-connectivity-for-site-recovery-urls-or-ip-ranges-error-code-151037-or-151072"></a><span data-ttu-id="445b5-156">Site Recovery URL 或 IP 範圍的輸出連線能力 (錯誤碼 151037 或 151072)</span><span class="sxs-lookup"><span data-stu-id="445b5-156">Outbound connectivity for Site Recovery URLs or IP ranges (error code 151037 or 151072)</span></span>

<span data-ttu-id="445b5-157">若要使 Site Recovery 複寫正常運作，VM 需要特定 URL 或 IP 範圍的輸出連線能力。</span><span class="sxs-lookup"><span data-stu-id="445b5-157">For Site Recovery replication to work, outbound connectivity to specific URLs or IP ranges is required from the VM.</span></span> <span data-ttu-id="445b5-158">如果您的 VM 位於防火牆後方，或使用網路安全性群組 (NSG) 規則控制輸出連線能力，您可能會看到下列其中一個錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="445b5-158">If your VM is behind a firewall or uses network security group (NSG) rules to control outbound connectivity, you might see one of these error messages:</span></span>

<span data-ttu-id="445b5-159">**錯誤碼**</span><span class="sxs-lookup"><span data-stu-id="445b5-159">**Error codes**</span></span> | <span data-ttu-id="445b5-160">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="445b5-160">**Possible causes**</span></span> | <span data-ttu-id="445b5-161">**建議**</span><span class="sxs-lookup"><span data-stu-id="445b5-161">**Recommendations**</span></span>
--- | --- | ---
<span data-ttu-id="445b5-162">151037</span><span class="sxs-lookup"><span data-stu-id="445b5-162">151037</span></span><br></br><span data-ttu-id="445b5-163">**訊息**：無法向 Site Recovery 註冊 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="445b5-163">**Message**: Failed to register Azure virtual machine with Site Recovery.</span></span> | <span data-ttu-id="445b5-164">- 您使用 NSG 控制傳出 VM 的存取，而且所需的 IP 範圍並未列在傳出存取的白名單中。</span><span class="sxs-lookup"><span data-stu-id="445b5-164">- You're using NSG to control outbound access on the VM and the required IP ranges aren't whitelisted for outbound access.</span></span></br></br><span data-ttu-id="445b5-165">- 您使用第三方防火牆工具，而且所需的 IP 範圍/URL 並未列在白名單中。</span><span class="sxs-lookup"><span data-stu-id="445b5-165">- You're using third-party firewall tools and the required IP ranges/URLs are not whitelisted.</span></span></br>| <span data-ttu-id="445b5-166">- 如果您使用防火牆 Proxy 控制 VM 上的傳出網路連線能力，請確定必要條件 URL 或資料中心 IP 範圍列在白名單中。</span><span class="sxs-lookup"><span data-stu-id="445b5-166">- If you're using firewall proxy to control outbound network connectivity on the VM, ensure that the prerequisite URLs or datacenter IP ranges are whitelisted.</span></span> <span data-ttu-id="445b5-167">如需資訊，請參閱[防火牆 Proxy 指引](https://aka.ms/a2a-firewall-proxy-guidance)。</span><span class="sxs-lookup"><span data-stu-id="445b5-167">For information, see [firewall proxy guidance](https://aka.ms/a2a-firewall-proxy-guidance).</span></span></br></br><span data-ttu-id="445b5-168">- 如果您使用 NSG 規則控制 VM 上的傳出網路連線能力，請確定必要條件資料中心 IP 範圍列在白名單中。</span><span class="sxs-lookup"><span data-stu-id="445b5-168">- If you're using NSG rules to control outbound network connectivity on the VM, ensure that the prerequisite datacenter IP ranges are whitelisted.</span></span> <span data-ttu-id="445b5-169">如需資訊，請參閱[網路安全性群組指引](https://aka.ms/a2a-nsg-guidance)。</span><span class="sxs-lookup"><span data-stu-id="445b5-169">For information, see [network security group guidance](https://aka.ms/a2a-nsg-guidance).</span></span>
<span data-ttu-id="445b5-170">151072</span><span class="sxs-lookup"><span data-stu-id="445b5-170">151072</span></span><br></br><span data-ttu-id="445b5-171">**訊息**：Site Recovery 組態失敗。</span><span class="sxs-lookup"><span data-stu-id="445b5-171">**Message**: Site Recovery configuration failed.</span></span> | <span data-ttu-id="445b5-172">無法在連線至 Site Recovery 服務端點。</span><span class="sxs-lookup"><span data-stu-id="445b5-172">Connection cannot be established to Site Recovery service endpoints.</span></span> | <span data-ttu-id="445b5-173">- 如果您使用防火牆 Proxy 控制 VM 上的傳出網路連線能力，請確定必要條件 URL 或資料中心 IP 範圍列在白名單中。</span><span class="sxs-lookup"><span data-stu-id="445b5-173">- If you're using firewall proxy to control outbound network connectivity on the VM, ensure that the prerequisite URLs or datacenter IP ranges are whitelisted.</span></span> <span data-ttu-id="445b5-174">如需資訊，請參閱[防火牆 Proxy 指引](https://aka.ms/a2a-firewall-proxy-guidance)。</span><span class="sxs-lookup"><span data-stu-id="445b5-174">For information, see [firewall proxy guidance](https://aka.ms/a2a-firewall-proxy-guidance).</span></span></br></br><span data-ttu-id="445b5-175">- 如果您使用 NSG 規則控制 VM 上的傳出網路連線能力，請確定必要條件資料中心 IP 範圍列在白名單中。</span><span class="sxs-lookup"><span data-stu-id="445b5-175">- If you're using NSG rules to control outbound network connectivity on the VM, ensure that the prerequisite datacenter IP ranges are whitelisted.</span></span> <span data-ttu-id="445b5-176">如需資訊，請參閱[網路安全性群組指引](https://aka.ms/a2a-nsg-guidance)。</span><span class="sxs-lookup"><span data-stu-id="445b5-176">For information, see [network security group guidance](https://aka.ms/a2a-nsg-guidance).</span></span>

### <a name="fix-the-problem"></a><span data-ttu-id="445b5-177">修正問題</span><span class="sxs-lookup"><span data-stu-id="445b5-177">Fix the problem</span></span>
<span data-ttu-id="445b5-178">若要將[所需的 URL](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-urls) 或[所需的 IP 範圍](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-ip-ranges)列入白名單中，請依照[網路指引文件](site-recovery-azure-to-azure-networking-guidance.md)中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="445b5-178">To whitelist [the required URLs](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-urls) or the [required IP ranges](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-ip-ranges), follow the steps in the [networking guidance document](site-recovery-azure-to-azure-networking-guidance.md).</span></span>

## <a name="disk-not-found-in-the-machine-error-code-150039"></a><span data-ttu-id="445b5-179">在機器中找不到磁碟 (錯誤碼 150039)</span><span class="sxs-lookup"><span data-stu-id="445b5-179">Disk not found in the machine (error code 150039)</span></span>

<span data-ttu-id="445b5-180">必須先將連接到 VM 的新磁碟初始化。</span><span class="sxs-lookup"><span data-stu-id="445b5-180">A new disk attached to the VM must be initialized.</span></span>

<span data-ttu-id="445b5-181">**錯誤碼**</span><span class="sxs-lookup"><span data-stu-id="445b5-181">**Error code**</span></span> | <span data-ttu-id="445b5-182">**可能的原因**</span><span class="sxs-lookup"><span data-stu-id="445b5-182">**Possible causes**</span></span> | <span data-ttu-id="445b5-183">**建議**</span><span class="sxs-lookup"><span data-stu-id="445b5-183">**Recommendations**</span></span>
--- | --- | ---
<span data-ttu-id="445b5-184">150039</span><span class="sxs-lookup"><span data-stu-id="445b5-184">150039</span></span><br></br><span data-ttu-id="445b5-185">**訊息**：邏輯單元編號 (LUN) 為 (LUNValue) 的 Azure 資料磁碟 (DiskName) (DiskURI) 未對應到從 LUN 值相同的 VM 內回報的對應磁碟。</span><span class="sxs-lookup"><span data-stu-id="445b5-185">**Message**: Azure data disk (DiskName) (DiskURI) with logical unit number (LUN) (LUNValue) was not mapped to a corresponding disk being reported from within the VM that has the same LUN value.</span></span> | <span data-ttu-id="445b5-186">- 新的資料磁碟連接到 VM，但是未初始化。</span><span class="sxs-lookup"><span data-stu-id="445b5-186">- A new data disk was attached to the VM but it wasn't initialized.</span></span></br></br><span data-ttu-id="445b5-187">- VM 內的資料磁碟不當回報 LUN 值，該磁碟已連接到 VM。</span><span class="sxs-lookup"><span data-stu-id="445b5-187">- The data disk inside the VM is not correctly reporting the LUN value at which the disk was attached to the VM.</span></span>| <span data-ttu-id="445b5-188">請確定資料磁碟都已初始化，然後再次嘗試操作。</span><span class="sxs-lookup"><span data-stu-id="445b5-188">Ensure that the data disks are initialized, and then retry the operation.</span></span></br></br><span data-ttu-id="445b5-189">對於 Windows：[連接並初始化新的磁碟](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk)。</span><span class="sxs-lookup"><span data-stu-id="445b5-189">For Windows: [Attach and initialize a new disk](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk).</span></span></br></br><span data-ttu-id="445b5-190">對於 Linux：[在 Linux 中初始化新的資料磁碟](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux)。</span><span class="sxs-lookup"><span data-stu-id="445b5-190">For Linux: [Initialize a new data disk in Linux](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux).</span></span>

### <a name="fix-the-problem"></a><span data-ttu-id="445b5-191">修正問題</span><span class="sxs-lookup"><span data-stu-id="445b5-191">Fix the problem</span></span>
<span data-ttu-id="445b5-192">請確定資料磁碟都已初始化，然後再次嘗試操作：</span><span class="sxs-lookup"><span data-stu-id="445b5-192">Ensure that the data disks have been initialized, and then retry the operation:</span></span>

- <span data-ttu-id="445b5-193">對於 Windows：[連接並初始化新的磁碟](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk)。</span><span class="sxs-lookup"><span data-stu-id="445b5-193">For Windows: [Attach and initialize a new disk](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk).</span></span>
- <span data-ttu-id="445b5-194">對於 Linux：[在 Linux 中初始化新的資料磁碟](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux)。</span><span class="sxs-lookup"><span data-stu-id="445b5-194">For Linux: [Initialize a new data disk in Linux](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux).</span></span>

<span data-ttu-id="445b5-195">若問題持續發生，請連絡支援服務。</span><span class="sxs-lookup"><span data-stu-id="445b5-195">If the problem persists, contact support.</span></span>


## <a name="unable-to-see-the-azure-vm-for-selection-in-enable-replication"></a><span data-ttu-id="445b5-196">看不見 Azure VM，無法在「啟用複寫」中選取</span><span class="sxs-lookup"><span data-stu-id="445b5-196">Unable to see the Azure VM for selection in "enable replication"</span></span>

<span data-ttu-id="445b5-197">您可能看不見您的 Azure VM，因此無法在[啟用複寫：步驟 2](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines) 中選取。</span><span class="sxs-lookup"><span data-stu-id="445b5-197">You might not see your Azure VM for selection in [Enable replication: Step 2](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines).</span></span> <span data-ttu-id="445b5-198">此問題可能是由於 Azure VM 上保留過時的 Site Recovery 組態。</span><span class="sxs-lookup"><span data-stu-id="445b5-198">This issue could be due to stale Site Recovery configuration left on the Azure VM.</span></span> <span data-ttu-id="445b5-199">在下列情況中，Azure VM 可能保留過時的組態：</span><span class="sxs-lookup"><span data-stu-id="445b5-199">The stale configuration could be left on an Azure VM in the following cases:</span></span>

- <span data-ttu-id="445b5-200">您使用 Site Recovery 啟用 Azure VM 的複寫，然後刪除 Site Recovery 保存庫，但是並未明確停用 VM 上的複寫。</span><span class="sxs-lookup"><span data-stu-id="445b5-200">You enabled replication for the Azure VM by using Site Recovery and then deleted the Site Recovery vault without explicitly disabling replication on the VM.</span></span>
- <span data-ttu-id="445b5-201">您使用 Site Recovery 啟用 Azure VM 的複寫，然後刪除包含 Site Recovery 保存庫的資源群組，但是並未明確停用 VM 上的複寫。</span><span class="sxs-lookup"><span data-stu-id="445b5-201">You enabled replication for the Azure VM by using Site Recovery and then deleted the resource group containing the Site Recovery vault without explicitly disabling replication on the VM.</span></span>

### <a name="fix-the-problem"></a><span data-ttu-id="445b5-202">修正問題</span><span class="sxs-lookup"><span data-stu-id="445b5-202">Fix the problem</span></span>

<span data-ttu-id="445b5-203">您可以使用[移除過時 ASR 組態指令碼](https://gallery.technet.microsoft.com/Azure-Recovery-ASR-script-3a93f412)，並移除 Azure VM 上的過時 Site Recovery 組態。</span><span class="sxs-lookup"><span data-stu-id="445b5-203">You can use [Remove stale ASR configuration script](https://gallery.technet.microsoft.com/Azure-Recovery-ASR-script-3a93f412) and remove the stale Site Recovery configuration on the Azure VM.</span></span> <span data-ttu-id="445b5-204">移除過時的組態後，您應該會在[啟用複寫：步驟 2](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines) 中看見 VM。</span><span class="sxs-lookup"><span data-stu-id="445b5-204">You should see the VM in [Enable replication: Step 2](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines) after removing the stale configuration.</span></span>


## <a name="next-steps"></a><span data-ttu-id="445b5-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="445b5-205">Next steps</span></span>
[<span data-ttu-id="445b5-206">複寫 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="445b5-206">Replicate Azure virtual machines</span></span>](site-recovery-replicate-azure-to-azure.md)

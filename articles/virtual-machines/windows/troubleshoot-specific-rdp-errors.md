---
title: "Azure Vm aaaSpecific RDP 的錯誤訊息 |Microsoft 文件"
description: "了解特定的錯誤訊息，您可能會收到時，嘗試在 Azure 中使用遠端桌面連線 tooa Windows 虛擬機器"
keywords: "遠端桌面的錯誤，遠端桌面連線錯誤，無法連接 tooVM，遠端桌面的疑難排解"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 5feb1d64-ee6f-4907-949a-a7cffcbc6153
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 8e1551be23e696bd60adbd76c3e1ea86d9dd11aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-specific-rdp-error-messages-tooa-windows-vm-in-azure"></a><span data-ttu-id="ac402-104">疑難排解特定的 RDP 錯誤訊息 tooa Windows Azure 中的 VM</span><span class="sxs-lookup"><span data-stu-id="ac402-104">Troubleshooting specific RDP error messages tooa Windows VM in Azure</span></span>
<span data-ttu-id="ac402-105">在 Azure 中使用遠端桌面連線 tooa Windows 虛擬機器 (VM) 時，您可能會收到特定的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="ac402-105">You may receive a specific error message when using Remote Desktop connection tooa Windows virtual machine (VM) in Azure.</span></span> <span data-ttu-id="ac402-106">本文詳細說明的某些 hello 較常見的錯誤訊息發生，以及疑難排解步驟 tooresolve 它們。</span><span class="sxs-lookup"><span data-stu-id="ac402-106">This article details some of hello more common error messages encountered, along with troubleshooting steps tooresolve them.</span></span> <span data-ttu-id="ac402-107">如果您在連接時發生問題 tooyour VM 不使用 RDP 但發生特定的錯誤訊息，請參閱 hello[疑難排解指南針對遠端桌面](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="ac402-107">If you are having issues connecting tooyour VM using RDP but do not encounter a specific error message, see hello [troubleshooting guide for Remote Desktop](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="ac402-108">如需特定的錯誤訊息資訊，請參閱 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="ac402-108">For information on specific error messages, see hello following:</span></span>

* <span data-ttu-id="ac402-109">[hello 遠端工作階段中斷，因為沒有任何遠端桌面授權伺服器的可用 tooprovide 授權](#rdplicense)。</span><span class="sxs-lookup"><span data-stu-id="ac402-109">[hello remote session was disconnected because there are no Remote Desktop License Servers available tooprovide a license](#rdplicense).</span></span>
* <span data-ttu-id="ac402-110">[遠端桌面找不到 hello 電腦 「 名稱 」](#rdpname)。</span><span class="sxs-lookup"><span data-stu-id="ac402-110">[Remote Desktop can't find hello computer "name"](#rdpname).</span></span>
* <span data-ttu-id="ac402-111">[發生驗證錯誤。hello 本機安全性授權無法連絡](#rdpauth)。</span><span class="sxs-lookup"><span data-stu-id="ac402-111">[An authentication error has occurred. hello Local Security Authority cannot be contacted](#rdpauth).</span></span>
* <span data-ttu-id="ac402-112">[Windows 安全性錯誤：您的認證無法運作](#wincred)。</span><span class="sxs-lookup"><span data-stu-id="ac402-112">[Windows Security error: Your credentials did not work](#wincred).</span></span>
* <span data-ttu-id="ac402-113">[這部電腦無法連線遠端電腦的 toohello](#rdpconnect)。</span><span class="sxs-lookup"><span data-stu-id="ac402-113">[This computer can't connect toohello remote computer](#rdpconnect).</span></span>

<a id="rdplicense"></a>

## <a name="hello-remote-session-was-disconnected-because-there-are-no-remote-desktop-license-servers-available-tooprovide-a-license"></a><span data-ttu-id="ac402-114">hello 遠端工作階段中斷，因為沒有任何遠端桌面授權伺服器使用 tooprovide 授權。</span><span class="sxs-lookup"><span data-stu-id="ac402-114">hello remote session was disconnected because there are no Remote Desktop License Servers available tooprovide a license.</span></span>
<span data-ttu-id="ac402-115">原因： hello 120 天授權寬限期 hello 遠端桌面伺服器角色已過期，您需要 tooinstall 授權。</span><span class="sxs-lookup"><span data-stu-id="ac402-115">Cause: hello 120-day licensing grace period for hello Remote Desktop Server role has expired and you need tooinstall licenses.</span></span>

<span data-ttu-id="ac402-116">因應措施，儲存 hello RDP 檔案的本機副本從 hello 入口網站並執行此命令在 PowerShell 命令提示字元 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="ac402-116">As a workaround, save a local copy of hello RDP file from hello portal and run this command at a PowerShell command prompt tooconnect.</span></span> <span data-ttu-id="ac402-117">此步驟只會停用該連線的授權：</span><span class="sxs-lookup"><span data-stu-id="ac402-117">This step disables licensing for just that connection:</span></span>

        mstsc <File name>.RDP /admin

<span data-ttu-id="ac402-118">如果您實際上不需要超過兩個同時遠端桌面連線 toohello VM，您可以使用伺服器管理員 tooremove hello 遠端桌面伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="ac402-118">If you don't actually need more than two simultaneous Remote Desktop connections toohello VM, you can use Server Manager tooremove hello Remote Desktop Server role.</span></span>

<span data-ttu-id="ac402-119">如需詳細資訊，請參閱 hello 部落格文章[失敗 」 沒有遠端桌面授權伺服器可以使用 「 Azure VM](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/)。</span><span class="sxs-lookup"><span data-stu-id="ac402-119">For more information, see hello blog post [Azure VM fails with "No Remote Desktop License Servers available"](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).</span></span>

<a id="rdpname"></a>

## <a name="remote-desktop-cant-find-hello-computer-name"></a><span data-ttu-id="ac402-120">遠端桌面找不到 hello 電腦 「 名稱 」。</span><span class="sxs-lookup"><span data-stu-id="ac402-120">Remote Desktop can't find hello computer "name".</span></span>
<span data-ttu-id="ac402-121">原因： hello 遠端桌面用戶端電腦上的無法解析 hello hello 設定 hello RDP 檔案中的 hello 電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="ac402-121">Cause: hello Remote Desktop client on your computer can't resolve hello name of hello computer in hello settings of hello RDP file.</span></span>

<span data-ttu-id="ac402-122">可能的解決方案：</span><span class="sxs-lookup"><span data-stu-id="ac402-122">Possible solutions:</span></span>

* <span data-ttu-id="ac402-123">如果您在組織內部網路上，請確定您的電腦具有存取 toohello proxy 伺服器，並且可以傳送 HTTPS 流量 tooit。</span><span class="sxs-lookup"><span data-stu-id="ac402-123">If you're on an organization's intranet, make sure that your computer has access toohello proxy server and can send HTTPS traffic tooit.</span></span>
* <span data-ttu-id="ac402-124">如果您使用儲存在本機上的 RDP 檔案，請嘗試使用 hello 一個 hello 入口網站所產生。</span><span class="sxs-lookup"><span data-stu-id="ac402-124">If you're using a locally stored RDP file, try using hello one that's generated by hello portal.</span></span> <span data-ttu-id="ac402-125">這個步驟可確保您擁有 hello 正確的 DNS 名稱 hello 虛擬機器，或 hello 雲端服務和 hello VM hello 端點連接埠。</span><span class="sxs-lookup"><span data-stu-id="ac402-125">This step ensures that you have hello correct DNS name for hello virtual machine, or hello cloud service and hello endpoint port of hello VM.</span></span> <span data-ttu-id="ac402-126">以下是 hello 入口網站所產生的範例 RDP 檔案：</span><span class="sxs-lookup"><span data-stu-id="ac402-126">Here is a sample RDP file generated by hello portal:</span></span>
  
        full address:s:tailspin-azdatatier.cloudapp.net:55919
        prompt for credentials:i:1

<span data-ttu-id="ac402-127">具有此 RDP 檔 hello 位址部分：</span><span class="sxs-lookup"><span data-stu-id="ac402-127">hello address portion of this RDP file has:</span></span>

* <span data-ttu-id="ac402-128">hello 完整 hello 包含 hello VM (「 tailspin-azdatatier.cloudapp.net 「 在此範例中) 的雲端服務的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ac402-128">hello fully qualified domain name of hello cloud service that contains hello VM ("tailspin-azdatatier.cloudapp.net" in this example).</span></span>
* <span data-ttu-id="ac402-129">hello 外部 TCP 連接埠的遠端桌面流量 (55919) hello 端點。</span><span class="sxs-lookup"><span data-stu-id="ac402-129">hello external TCP port of hello endpoint for Remote Desktop traffic (55919).</span></span>

<a id="rdpauth"></a>

## <a name="an-authentication-error-has-occurred-hello-local-security-authority-cannot-be-contacted"></a><span data-ttu-id="ac402-130">發生驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="ac402-130">An authentication error has occurred.</span></span> <span data-ttu-id="ac402-131">無法連絡 hello 本機安全性授權。</span><span class="sxs-lookup"><span data-stu-id="ac402-131">hello Local Security Authority cannot be contacted.</span></span>
<span data-ttu-id="ac402-132">原因： hello 目標 VM 找不到您的認證 hello 使用者名稱部分中的 hello 安全性授權。</span><span class="sxs-lookup"><span data-stu-id="ac402-132">Cause: hello target VM can't locate hello security authority in hello user name portion of your credentials.</span></span>

<span data-ttu-id="ac402-133">當您的使用者名稱處於 hello 表單*SecurityAuthority*\\*UserName* (範例： CORP\User1)，hello *SecurityAuthority*部分為任一 hello VM（適用於 hello 本機安全性授權） 的電腦名稱或 Active Directory 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ac402-133">When your user name is in hello form *SecurityAuthority*\\*UserName* (example: CORP\User1), hello *SecurityAuthority* portion is either hello VM's computer name (for hello local security authority) or an Active Directory domain name.</span></span>

<span data-ttu-id="ac402-134">可能的解決方案：</span><span class="sxs-lookup"><span data-stu-id="ac402-134">Possible solutions:</span></span>

* <span data-ttu-id="ac402-135">如果 hello 帳戶是本機 toohello VM，請確定該 hello VM 名稱拼寫正確。</span><span class="sxs-lookup"><span data-stu-id="ac402-135">If hello account is local toohello VM, make sure that hello VM name is spelled correctly.</span></span>
* <span data-ttu-id="ac402-136">如果 hello 帳戶位於 Active Directory 網域，請檢查 hello hello 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ac402-136">If hello account is on an Active Directory domain, check hello spelling of hello domain name.</span></span>
* <span data-ttu-id="ac402-137">如果這是 Active Directory 網域帳戶，而且 hello 網域名稱的拼字正確，請確認該網域中的網域控制站為可用。</span><span class="sxs-lookup"><span data-stu-id="ac402-137">If it is an Active Directory domain account and hello domain name is spelled correctly, verify that a domain controller is available in that domain.</span></span> <span data-ttu-id="ac402-138">其為包含網域控制站的 Azure 虛擬網路中常見的問題，網域控制站無法使用的原因是其尚未啟動為因應措施。</span><span class="sxs-lookup"><span data-stu-id="ac402-138">It's a common issue in Azure virtual networks that contain domain controllers that a domain controller is unavailable because it hasn't been started.</span></span> <span data-ttu-id="ac402-139">您可以使用本機系統管理員帳戶做為因應措施，而非網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="ac402-139">As a workaround, you can use a local administrator account instead of a domain account.</span></span>

<a id="wincred"></a>

## <a name="windows-security-error-your-credentials-did-not-work"></a><span data-ttu-id="ac402-140">Windows 安全性錯誤：您的認證無法運作。</span><span class="sxs-lookup"><span data-stu-id="ac402-140">Windows Security error: Your credentials did not work.</span></span>
<span data-ttu-id="ac402-141">原因： hello 目標 VM 無法驗證您的帳戶名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="ac402-141">Cause: hello target VM can't validate your account name and password.</span></span>

<span data-ttu-id="ac402-142">Windows 的電腦可以驗證 hello 的本機帳戶或網域帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="ac402-142">A Windows-based computer can validate hello credentials of either a local account or a domain account.</span></span>

* <span data-ttu-id="ac402-143">對於本機帳戶，請使用 hello *ComputerName*\\*UserName*語法 (範例： SQL1\Admin4798)。</span><span class="sxs-lookup"><span data-stu-id="ac402-143">For local accounts, use hello *ComputerName*\\*UserName* syntax (example: SQL1\Admin4798).</span></span>
* <span data-ttu-id="ac402-144">網域帳戶使用 hello *DomainName*\\*UserName*語法 (範例： CONTOSO\peterodman)。</span><span class="sxs-lookup"><span data-stu-id="ac402-144">For domain accounts, use hello *DomainName*\\*UserName* syntax (example: CONTOSO\peterodman).</span></span>

<span data-ttu-id="ac402-145">如果您升級新的 Active Directory 樹系中 VM tooa 網域控制站，會轉換 hello 本機系統管理員帳戶登入的 tooan 對等帳戶以 hello 相同 hello 新樹系和網域中的密碼。</span><span class="sxs-lookup"><span data-stu-id="ac402-145">If you have promoted your VM tooa domain controller in a new Active Directory forest, hello local administrator account that you signed in with is converted tooan equivalent account with hello same password in hello new forest and domain.</span></span> <span data-ttu-id="ac402-146">然後刪除 hello 本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="ac402-146">hello local account is then deleted.</span></span>

<span data-ttu-id="ac402-147">例如，如果在 hello 本機帳戶 DC1\DCAdmin，登入，然後為新樹系中的 hello corp.contoso.com 網域的網域控制站升級 hello 虛擬機器 hello 的 DC1\DCAdmin 本機帳戶已刪除和新的網域帳戶 (CORP\DCAdmin) 會透過 hello 相同密碼。</span><span class="sxs-lookup"><span data-stu-id="ac402-147">For example, if you signed in with hello local account DC1\DCAdmin, and then promoted hello virtual machine as a domain controller in a new forest for hello corp.contoso.com domain, hello DC1\DCAdmin local account gets deleted and a new domain account (CORP\DCAdmin) is created with hello same password.</span></span>

<span data-ttu-id="ac402-148">請確定該 hello 帳戶名稱就會確認 hello 虛擬機器可以驗證為有效的帳戶，而且 hello 密碼是正確的名稱。</span><span class="sxs-lookup"><span data-stu-id="ac402-148">Make sure that hello account name is a name that hello virtual machine can verify as a valid account, and that hello password is correct.</span></span>

<span data-ttu-id="ac402-149">如果您需要 toochange hello hello 本機系統管理員帳戶密碼，請參閱[tooreset 密碼或 hello 遠端桌面服務的 Windows 虛擬機器的方式](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="ac402-149">If you need toochange hello password of hello local administrator account, see [How tooreset a password or hello Remote Desktop service for Windows virtual machines](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<a id="rdpconnect"></a>

## <a name="this-computer-cant-connect-toohello-remote-computer"></a><span data-ttu-id="ac402-150">這部電腦無法連線 toohello 遠端電腦。</span><span class="sxs-lookup"><span data-stu-id="ac402-150">This computer can't connect toohello remote computer.</span></span>
<span data-ttu-id="ac402-151">原因： 用 tooconnect hello 帳戶並沒有遠端桌面登入權限。</span><span class="sxs-lookup"><span data-stu-id="ac402-151">Cause: hello account that's used tooconnect does not have Remote Desktop sign-in rights.</span></span>

<span data-ttu-id="ac402-152">每一部 Windows 電腦有遠端桌面使用者本機群組，其中包含 hello 帳戶和群組，可以從遠端登入它。</span><span class="sxs-lookup"><span data-stu-id="ac402-152">Every Windows computer has a Remote Desktop users local group, which contains hello accounts and groups that can sign into it remotely.</span></span> <span data-ttu-id="ac402-153">Hello 本機 administrators 群組的成員具有存取，即使這些帳戶不會列在 hello 遠端桌面使用者本機群組。</span><span class="sxs-lookup"><span data-stu-id="ac402-153">Members of hello local administrators group also have access, even though those accounts are not listed in hello Remote Desktop users local group.</span></span> <span data-ttu-id="ac402-154">已加入網域的機器，hello 本機 administrators 群組也包含 hello hello 網域的網域系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ac402-154">For domain-joined machines, hello local administrators group also contains hello domain administrators for hello domain.</span></span>

<span data-ttu-id="ac402-155">請確定您使用與 tooconnect hello 帳戶具有遠端桌面登入權限。</span><span class="sxs-lookup"><span data-stu-id="ac402-155">Make sure that hello account you're using tooconnect with has Remote Desktop sign-in rights.</span></span> <span data-ttu-id="ac402-156">因應措施是，使用網域或本機系統管理員帳戶 tooconnect 透過遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="ac402-156">As a workaround, use a domain or local administrator account tooconnect over Remote Desktop.</span></span> <span data-ttu-id="ac402-157">tooadd hello 所需的帳戶 toohello 遠端桌面使用者本機群組，請使用 hello Microsoft Management Console 嵌入式管理單元 (**系統工具 > 本機使用者和群組 > 群組 > Remote Desktop Users**)。</span><span class="sxs-lookup"><span data-stu-id="ac402-157">tooadd hello desired account toohello Remote Desktop users local group, use hello Microsoft Management Console snap-in (**System Tools > Local Users and Groups > Groups > Remote Desktop Users**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac402-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ac402-158">Next steps</span></span>
<span data-ttu-id="ac402-159">如果無這些錯誤發生，而且有未知的問題，與使用 RDP 連線，請參閱 hello[疑難排解指南針對遠端桌面](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="ac402-159">If none of these errors occurred and you have an unknown issue with connecting using RDP, see hello [troubleshooting guide for Remote Desktop](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="ac402-160">如需疑難排解存取 VM 上執行的應用程式的步驟，請參閱[疑難排解存取 tooan 應用程式在 Azure VM 上執行](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="ac402-160">For troubleshooting steps in accessing applications running on a VM, see [Troubleshoot access tooan application running on an Azure VM](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="ac402-161">如果您有使用安全殼層 (SSH) tooconnect tooa Linux VM 在 Azure 中的問題，請參閱[疑難排解 SSH 連線 tooa 在 Azure 中的 Linux VM](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="ac402-161">If you are having issues using Secure Shell (SSH) tooconnect tooa Linux VM in Azure, see [Troubleshoot SSH connections tooa Linux VM in Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


---
title: "Azure VM 的特定 RDP 錯誤訊息 | Microsoft Docs"
description: "了解在 Azure 中嘗試針對 Windows 虛擬機器使用遠端桌面連線時，可能會接收到的特定錯誤訊息"
keywords: "遠端桌面錯誤、遠端桌面連線錯誤、無法連接到 VM、遠端桌面疑難排解"
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
ms.openlocfilehash: e7c049106726a15e96d4ebe7c7c0388a29c546c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-specific-rdp-error-messages-to-a-windows-vm-in-azure"></a><span data-ttu-id="b6e35-104">針對 Azure 中 Windows VM 的特定 RDP 錯誤訊息進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="b6e35-104">Troubleshooting specific RDP error messages to a Windows VM in Azure</span></span>
<span data-ttu-id="b6e35-105">您在 Azure 中針對 Windows 虛擬機器 (VM) 使用遠端桌面連線時，可能會接收到特定錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="b6e35-105">You may receive a specific error message when using Remote Desktop connection to a Windows virtual machine (VM) in Azure.</span></span> <span data-ttu-id="b6e35-106">本文將詳述一些較常發生的錯誤訊息，並提供解決它們的疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="b6e35-106">This article details some of the more common error messages encountered, along with troubleshooting steps to resolve them.</span></span> <span data-ttu-id="b6e35-107">如果您無法使用 RDP 連線到 VM，但沒有遇到特定錯誤訊息，請參閱[遠端桌面的疑難排解指南](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b6e35-107">If you are having issues connecting to your VM using RDP but do not encounter a specific error message, see the [troubleshooting guide for Remote Desktop](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="b6e35-108">如需特定錯誤訊息的資訊，請參閱下列內容：</span><span class="sxs-lookup"><span data-stu-id="b6e35-108">For information on specific error messages, see the following:</span></span>

* <span data-ttu-id="b6e35-109">[遠端工作階段中斷，因為沒有提供授權的遠端桌面授權伺服器可以使用](#rdplicense)。</span><span class="sxs-lookup"><span data-stu-id="b6e35-109">[The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license](#rdplicense).</span></span>
* <span data-ttu-id="b6e35-110">[遠端桌面找不到電腦「名稱」](#rdpname)。</span><span class="sxs-lookup"><span data-stu-id="b6e35-110">[Remote Desktop can't find the computer "name"](#rdpname).</span></span>
* <span data-ttu-id="b6e35-111">[發生驗證錯誤。無法連絡本機安全性授權](#rdpauth)。</span><span class="sxs-lookup"><span data-stu-id="b6e35-111">[An authentication error has occurred. The Local Security Authority cannot be contacted](#rdpauth).</span></span>
* <span data-ttu-id="b6e35-112">[Windows 安全性錯誤：您的認證無法運作](#wincred)。</span><span class="sxs-lookup"><span data-stu-id="b6e35-112">[Windows Security error: Your credentials did not work](#wincred).</span></span>
* <span data-ttu-id="b6e35-113">[這部電腦無法連線到遠端電腦](#rdpconnect)。</span><span class="sxs-lookup"><span data-stu-id="b6e35-113">[This computer can't connect to the remote computer](#rdpconnect).</span></span>

<a id="rdplicense"></a>

## <a name="the-remote-session-was-disconnected-because-there-are-no-remote-desktop-license-servers-available-to-provide-a-license"></a><span data-ttu-id="b6e35-114">遠端工作階段中斷，因為沒有提供授權的遠端桌面授權伺服器可以使用。</span><span class="sxs-lookup"><span data-stu-id="b6e35-114">The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license.</span></span>
<span data-ttu-id="b6e35-115">原因：遠端桌面角色的 120 天授權寬限期已過期，您需要安裝授權。</span><span class="sxs-lookup"><span data-stu-id="b6e35-115">Cause: The 120-day licensing grace period for the Remote Desktop Server role has expired and you need to install licenses.</span></span>

<span data-ttu-id="b6e35-116">作為因應措施，請從入口網站儲存 RDP 檔案的本機複本，並在 PowerShell 命令提示字元執行該命令來連接。</span><span class="sxs-lookup"><span data-stu-id="b6e35-116">As a workaround, save a local copy of the RDP file from the portal and run this command at a PowerShell command prompt to connect.</span></span> <span data-ttu-id="b6e35-117">此步驟只會停用該連線的授權：</span><span class="sxs-lookup"><span data-stu-id="b6e35-117">This step disables licensing for just that connection:</span></span>

        mstsc <File name>.RDP /admin

<span data-ttu-id="b6e35-118">如果您並非真的需要多於兩個對 VM 的同步遠端桌面連線，則您可以使用伺服器管理員來移除遠端桌面伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="b6e35-118">If you don't actually need more than two simultaneous Remote Desktop connections to the VM, you can use Server Manager to remove the Remote Desktop Server role.</span></span>

<span data-ttu-id="b6e35-119">如需詳細資訊，請參閱部落格文章： [Azure VM fails with "No Remote Desktop License Servers available" (Azure VM 因「沒有可用的遠端桌面授權伺服器」而失敗)](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/)。</span><span class="sxs-lookup"><span data-stu-id="b6e35-119">For more information, see the blog post [Azure VM fails with "No Remote Desktop License Servers available"](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).</span></span>

<a id="rdpname"></a>

## <a name="remote-desktop-cant-find-the-computer-name"></a><span data-ttu-id="b6e35-120">遠端桌面找不到電腦「名稱」。</span><span class="sxs-lookup"><span data-stu-id="b6e35-120">Remote Desktop can't find the computer "name".</span></span>
<span data-ttu-id="b6e35-121">原因：您電腦上的遠端桌面用戶端無法解析此 RDP 檔案設定中的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="b6e35-121">Cause: The Remote Desktop client on your computer can't resolve the name of the computer in the settings of the RDP file.</span></span>

<span data-ttu-id="b6e35-122">可能的解決方案：</span><span class="sxs-lookup"><span data-stu-id="b6e35-122">Possible solutions:</span></span>

* <span data-ttu-id="b6e35-123">如果您位於組織內部網路，請確保您的電腦能存取 Proxy 伺服器，並能將 HTTPS 流量傳送給 Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b6e35-123">If you're on an organization's intranet, make sure that your computer has access to the proxy server and can send HTTPS traffic to it.</span></span>
* <span data-ttu-id="b6e35-124">如果您使用本機儲存的 RDP 檔案，請嘗試使用入口網站所產生的檔案。</span><span class="sxs-lookup"><span data-stu-id="b6e35-124">If you're using a locally stored RDP file, try using the one that's generated by the portal.</span></span> <span data-ttu-id="b6e35-125">此步驟可確保您擁有虛擬機器的正確 DNS 名稱，或是 VM 的雲端服務和端點連接埠。</span><span class="sxs-lookup"><span data-stu-id="b6e35-125">This step ensures that you have the correct DNS name for the virtual machine, or the cloud service and the endpoint port of the VM.</span></span> <span data-ttu-id="b6e35-126">以下是由入口網站產生的 RDP 檔案範例：</span><span class="sxs-lookup"><span data-stu-id="b6e35-126">Here is a sample RDP file generated by the portal:</span></span>
  
        full address:s:tailspin-azdatatier.cloudapp.net:55919
        prompt for credentials:i:1

<span data-ttu-id="b6e35-127">此 RDP 檔案的位址部分包含︰</span><span class="sxs-lookup"><span data-stu-id="b6e35-127">The address portion of this RDP file has:</span></span>

* <span data-ttu-id="b6e35-128">雲端服務的完整網域名稱，其中包含 VM (本例中為 "tailspin-azdatatier.cloudapp.net")。</span><span class="sxs-lookup"><span data-stu-id="b6e35-128">The fully qualified domain name of the cloud service that contains the VM ("tailspin-azdatatier.cloudapp.net" in this example).</span></span>
* <span data-ttu-id="b6e35-129">遠端桌面流量 (55919) 端點的外部 TCP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="b6e35-129">The external TCP port of the endpoint for Remote Desktop traffic (55919).</span></span>

<a id="rdpauth"></a>

## <a name="an-authentication-error-has-occurred-the-local-security-authority-cannot-be-contacted"></a><span data-ttu-id="b6e35-130">發生驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="b6e35-130">An authentication error has occurred.</span></span> <span data-ttu-id="b6e35-131">無法連絡本機安全性授權。</span><span class="sxs-lookup"><span data-stu-id="b6e35-131">The Local Security Authority cannot be contacted.</span></span>
<span data-ttu-id="b6e35-132">原因：目標 VM 在認證的使用者名稱部分找不到安全性授權。</span><span class="sxs-lookup"><span data-stu-id="b6e35-132">Cause: The target VM can't locate the security authority in the user name portion of your credentials.</span></span>

<span data-ttu-id="b6e35-133">當您的使用者名稱格式為 *SecurityAuthority*\\*UserName* (範例：CORP\User1) 時，*SecurityAuthority* 部分會是 VM 的電腦名稱 (針對本機安全性授權) 或 Active Directory 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="b6e35-133">When your user name is in the form *SecurityAuthority*\\*UserName* (example: CORP\User1), the *SecurityAuthority* portion is either the VM's computer name (for the local security authority) or an Active Directory domain name.</span></span>

<span data-ttu-id="b6e35-134">可能的解決方案：</span><span class="sxs-lookup"><span data-stu-id="b6e35-134">Possible solutions:</span></span>

* <span data-ttu-id="b6e35-135">如果帳戶是 VM 的本機帳戶，請確認 VM 名稱拼寫正確。</span><span class="sxs-lookup"><span data-stu-id="b6e35-135">If the account is local to the VM, make sure that the VM name is spelled correctly.</span></span>
* <span data-ttu-id="b6e35-136">如果該帳戶位於 Active Directory 網域，請檢查網域名稱的拼字。</span><span class="sxs-lookup"><span data-stu-id="b6e35-136">If the account is on an Active Directory domain, check the spelling of the domain name.</span></span>
* <span data-ttu-id="b6e35-137">如果該帳戶是 Active Directory 網域帳戶且網域名稱的拼字正確，請確認該網域內可以使用網域控制站。</span><span class="sxs-lookup"><span data-stu-id="b6e35-137">If it is an Active Directory domain account and the domain name is spelled correctly, verify that a domain controller is available in that domain.</span></span> <span data-ttu-id="b6e35-138">其為包含網域控制站的 Azure 虛擬網路中常見的問題，網域控制站無法使用的原因是其尚未啟動為因應措施。</span><span class="sxs-lookup"><span data-stu-id="b6e35-138">It's a common issue in Azure virtual networks that contain domain controllers that a domain controller is unavailable because it hasn't been started.</span></span> <span data-ttu-id="b6e35-139">您可以使用本機系統管理員帳戶做為因應措施，而非網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="b6e35-139">As a workaround, you can use a local administrator account instead of a domain account.</span></span>

<a id="wincred"></a>

## <a name="windows-security-error-your-credentials-did-not-work"></a><span data-ttu-id="b6e35-140">Windows 安全性錯誤：您的認證無法運作。</span><span class="sxs-lookup"><span data-stu-id="b6e35-140">Windows Security error: Your credentials did not work.</span></span>
<span data-ttu-id="b6e35-141">原因：目標 VM 無法驗證您的帳戶名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b6e35-141">Cause: The target VM can't validate your account name and password.</span></span>

<span data-ttu-id="b6e35-142">以 Windows 為基礎的電腦可以驗證本機帳戶或網域帳戶之認證。</span><span class="sxs-lookup"><span data-stu-id="b6e35-142">A Windows-based computer can validate the credentials of either a local account or a domain account.</span></span>

* <span data-ttu-id="b6e35-143">如果是本機帳戶，請使用 *ComputerName*\\*UserName* 語法 (範例：SQL1\Admin4798)。</span><span class="sxs-lookup"><span data-stu-id="b6e35-143">For local accounts, use the *ComputerName*\\*UserName* syntax (example: SQL1\Admin4798).</span></span>
* <span data-ttu-id="b6e35-144">針對網域帳戶，請使用 *DomainName*\\*UserName* 語法 (範例：CONTOSO\peterodman)。</span><span class="sxs-lookup"><span data-stu-id="b6e35-144">For domain accounts, use the *DomainName*\\*UserName* syntax (example: CONTOSO\peterodman).</span></span>

<span data-ttu-id="b6e35-145">如果您在新的 Active Directory 樹系將 VM 提升為網域控制站，您用來登入的本機系統管理員帳戶會轉換為對等的帳戶，在新樹系和網域中使用相同的密碼。</span><span class="sxs-lookup"><span data-stu-id="b6e35-145">If you have promoted your VM to a domain controller in a new Active Directory forest, the local administrator account that you signed in with is converted to an equivalent account with the same password in the new forest and domain.</span></span> <span data-ttu-id="b6e35-146">本機帳戶隨即刪除。</span><span class="sxs-lookup"><span data-stu-id="b6e35-146">The local account is then deleted.</span></span>

<span data-ttu-id="b6e35-147">例如，如果您以本機帳戶 DC1\DCAdmin 登入，然後將此虛擬機器提升為 corp.contoso.com 網域中新樹系的網域控制器，則會刪除 DC1\DCAdmin 本機帳戶，並且以相同密碼建立一個新的網域帳戶 (CORP\DCAdmin)。</span><span class="sxs-lookup"><span data-stu-id="b6e35-147">For example, if you signed in with the local account DC1\DCAdmin, and then promoted the virtual machine as a domain controller in a new forest for the corp.contoso.com domain, the DC1\DCAdmin local account gets deleted and a new domain account (CORP\DCAdmin) is created with the same password.</span></span>

<span data-ttu-id="b6e35-148">請確保帳戶名稱為虛擬機器可驗證為有效帳戶的名稱，且密碼正確。</span><span class="sxs-lookup"><span data-stu-id="b6e35-148">Make sure that the account name is a name that the virtual machine can verify as a valid account, and that the password is correct.</span></span>

<span data-ttu-id="b6e35-149">如果您需要變更本機系統管理員帳戶的密碼，請參閱 [如何重設 Windows 虛擬機器的密碼或遠端桌面服務](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b6e35-149">If you need to change the password of the local administrator account, see [How to reset a password or the Remote Desktop service for Windows virtual machines](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<a id="rdpconnect"></a>

## <a name="this-computer-cant-connect-to-the-remote-computer"></a><span data-ttu-id="b6e35-150">這部電腦無法連線到遠端電腦。</span><span class="sxs-lookup"><span data-stu-id="b6e35-150">This computer can't connect to the remote computer.</span></span>
<span data-ttu-id="b6e35-151">原因：用來連接的帳戶並沒有遠端桌面的登入權限。</span><span class="sxs-lookup"><span data-stu-id="b6e35-151">Cause: The account that's used to connect does not have Remote Desktop sign-in rights.</span></span>

<span data-ttu-id="b6e35-152">每部 Windows 電腦都有遠端桌面使用者本機群組，其中包含能夠遠端登入的帳戶和群組。</span><span class="sxs-lookup"><span data-stu-id="b6e35-152">Every Windows computer has a Remote Desktop users local group, which contains the accounts and groups that can sign into it remotely.</span></span> <span data-ttu-id="b6e35-153">本機系統管理員群組成員也有權限，即使這些帳戶未列在遠端桌面使用者本機群組中。</span><span class="sxs-lookup"><span data-stu-id="b6e35-153">Members of the local administrators group also have access, even though those accounts are not listed in the Remote Desktop users local group.</span></span> <span data-ttu-id="b6e35-154">對於加入網域的機器，本機系統管理員群組也包含此網域的網域系統管理員。</span><span class="sxs-lookup"><span data-stu-id="b6e35-154">For domain-joined machines, the local administrators group also contains the domain administrators for the domain.</span></span>

<span data-ttu-id="b6e35-155">請確保您用於連接的帳戶具有遠端桌面登入權限。</span><span class="sxs-lookup"><span data-stu-id="b6e35-155">Make sure that the account you're using to connect with has Remote Desktop sign-in rights.</span></span> <span data-ttu-id="b6e35-156">因應措施是使用網域或本機系統管理員帳戶透過遠端桌面進行連接。</span><span class="sxs-lookup"><span data-stu-id="b6e35-156">As a workaround, use a domain or local administrator account to connect over Remote Desktop.</span></span> <span data-ttu-id="b6e35-157">若要將所需帳戶新增至「遠端桌面」使用者本機群組，請使用 Microsoft Management Console 嵌入式管理單元 ([系統工具] > [本機使用者和群組] > [群組] > [遠端桌面使用者])。</span><span class="sxs-lookup"><span data-stu-id="b6e35-157">To add the desired account to the Remote Desktop users local group, use the Microsoft Management Console snap-in (**System Tools > Local Users and Groups > Groups > Remote Desktop Users**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6e35-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b6e35-158">Next steps</span></span>
<span data-ttu-id="b6e35-159">如果您在使用 RDP 進行連線時沒有發生上述錯誤，而是遇到未知的問題，請參閱[遠端桌面的疑難排解指南](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b6e35-159">If none of these errors occurred and you have an unknown issue with connecting using RDP, see the [troubleshooting guide for Remote Desktop](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="b6e35-160">如需存取在 VM 上執行之應用程式的疑難排解步驟，請參閱[針對在 Azure VM 上執行之應用程式的存取進行疑難排解](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b6e35-160">For troubleshooting steps in accessing applications running on a VM, see [Troubleshoot access to an application running on an Azure VM](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="b6e35-161">如果您在 Azure 中使用安全殼層 (SSH) 連線到 Linux VM 時遇到問題，請參閱[針對 Azure 中對 Linux VM 的 SSH 連線進行疑難排解](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b6e35-161">If you are having issues using Secure Shell (SSH) to connect to a Linux VM in Azure, see [Troubleshoot SSH connections to a Linux VM in Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


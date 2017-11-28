---
title: "aaaPrepare Windows VHD tooupload tooAzure |Microsoft 文件"
description: "如何上傳 tooAzure 之前 tooprepare Windows VHD 或 VHDX"
services: virtual-machines-windows
documentationcenter: 
author: glimoli
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7802489d-33ec-4302-82a4-91463d03887a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: genli
ms.openlocfilehash: 530390e4c6a4f66ddfd4da23338f9bb3708c299f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-windows-vhd-or-vhdx-tooupload-tooazure"></a><span data-ttu-id="b703d-103">準備 Windows VHD 或 VHDX tooupload tooAzure</span><span class="sxs-lookup"><span data-stu-id="b703d-103">Prepare a Windows VHD or VHDX tooupload tooAzure</span></span>
<span data-ttu-id="b703d-104">您上傳 Windows 虛擬機器 (VM) 從內部部署 tooMicrosoft Azure 之前，您必須準備 hello 虛擬硬碟 （VHD 或 VHDX）。</span><span class="sxs-lookup"><span data-stu-id="b703d-104">Before you upload a Windows  virtual machines (VM) from on-premises tooMicrosoft Azure, you must prepare hello virtual hard disk (VHD or VHDX).</span></span> <span data-ttu-id="b703d-105">Azure 支援 hello VHD 檔案格式而且有固定大小的磁碟第 1 代 Vm。</span><span class="sxs-lookup"><span data-stu-id="b703d-105">Azure supports only generation 1 VMs that are in hello VHD file format and have a fixed sized disk.</span></span> <span data-ttu-id="b703d-106">hello 最大允許 hello VHD 為 1023 GB。</span><span class="sxs-lookup"><span data-stu-id="b703d-106">hello maximum size allowed for hello VHD is 1,023 GB.</span></span> <span data-ttu-id="b703d-107">您可以將轉換層代 1 的 VM 從 hello VHDX 檔案系統 tooVHD 和 toofixed 大小動態擴充磁碟。</span><span class="sxs-lookup"><span data-stu-id="b703d-107">You can convert a generation 1 VM from hello VHDX file system tooVHD and from a dynamically expanding disk toofixed-sized.</span></span> <span data-ttu-id="b703d-108">但您無法變更 VM 的世代。</span><span class="sxs-lookup"><span data-stu-id="b703d-108">But you can't change a VM's generation.</span></span> <span data-ttu-id="b703d-109">如需詳細資訊，請參閱[應該在 Hyper-V 中建立第 1 代還是第 2 代的 VM](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="b703d-109">For more information, see [Should I create a generation 1 or 2 VM in Hyper-V](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>

<span data-ttu-id="b703d-110">Azure vm hello 支援原則的相關資訊，請參閱[Microsoft 伺服器軟體支援的 Microsoft Azure Vm](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)。</span><span class="sxs-lookup"><span data-stu-id="b703d-110">For more information about hello support policy for Azure VM, see [Microsoft server software support for Microsoft Azure VMs](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).</span></span>

> [!Note]
> <span data-ttu-id="b703d-111">本文章中的 hello 指示適用於 toohello 64 位元版本的 Windows Server 2008 R2 或更新版本的 Windows 伺服器作業系統。</span><span class="sxs-lookup"><span data-stu-id="b703d-111">hello instructions in this article apply toohello 64-bit version of Windows Server 2008 R2 and later Windows server operating system.</span></span> <span data-ttu-id="b703d-112">如需 Azure 中執行 32 位元版本的作業系統相關資訊，請參閱[在 Azure 虛擬機器中對 32 位元作業系統的支援](https://support.microsoft.com/help/4021388/support-for-32-bit-operating-systems-in-azure-virtual-machines) \(機器翻譯\)。</span><span class="sxs-lookup"><span data-stu-id="b703d-112">For information about running 32-bit version of operating system in Azure, see [Support for 32-bit operating systems in Azure virtual machines](https://support.microsoft.com/help/4021388/support-for-32-bit-operating-systems-in-azure-virtual-machines).</span></span>

## <a name="convert-hello-virtual-disk-toovhd-and-fixed-size-disk"></a><span data-ttu-id="b703d-113">轉換 hello 虛擬磁碟 tooVHD 和固定的大小磁碟</span><span class="sxs-lookup"><span data-stu-id="b703d-113">Convert hello virtual disk tooVHD and fixed size disk</span></span> 
<span data-ttu-id="b703d-114">如果您需要 tooconvert 虛擬磁碟 toohello 所需格式 Azure 中，使用本節中的 hello 方法之一。</span><span class="sxs-lookup"><span data-stu-id="b703d-114">If you need tooconvert your virtual disk toohello required format for Azure, use one of hello methods in this section.</span></span> <span data-ttu-id="b703d-115">您執行 hello 虛擬磁碟轉換程序，並確定該 hello Windows VHD hello 本機伺服器運作正常之前，請備份 hello VM。</span><span class="sxs-lookup"><span data-stu-id="b703d-115">Back up hello VM before you run hello virtual disk conversion process and make sure that hello Windows VHD works correctly on hello local server.</span></span> <span data-ttu-id="b703d-116">請解決所有錯誤 hello VM 本身內 tooconvert 再試一次，或將它上傳 tooAzure 之前。</span><span class="sxs-lookup"><span data-stu-id="b703d-116">Resolve any errors within hello VM itself before you try tooconvert or upload it tooAzure.</span></span>

<span data-ttu-id="b703d-117">在轉換 hello 磁碟之後，建立會使用轉換的 hello 磁碟的 VM。</span><span class="sxs-lookup"><span data-stu-id="b703d-117">After you convert hello disk, create a VM that uses hello converted disk.</span></span> <span data-ttu-id="b703d-118">啟動和登入 toohello VM toofinish hello VM 準備上傳。</span><span class="sxs-lookup"><span data-stu-id="b703d-118">Start and sign in toohello VM toofinish preparing hello VM for upload.</span></span>

### <a name="convert-disk-using-hyper-v-manager"></a><span data-ttu-id="b703d-119">使用 HYPER-V 管理員轉換磁碟</span><span class="sxs-lookup"><span data-stu-id="b703d-119">Convert disk using Hyper-V Manager</span></span>
1. <span data-ttu-id="b703d-120">開啟 HYPER-V 管理員，然後選取 本機電腦上 hello 左邊。</span><span class="sxs-lookup"><span data-stu-id="b703d-120">Open Hyper-V Manager and select your local computer on hello left.</span></span> <span data-ttu-id="b703d-121">在 hello hello 電腦清單上方的功能表，按一下 **動作** > **編輯磁碟**。</span><span class="sxs-lookup"><span data-stu-id="b703d-121">In hello menu above hello computer list, click **Action** > **Edit Disk**.</span></span>
2. <span data-ttu-id="b703d-122">在 hello**尋找虛擬硬碟**畫面上，找出並選取您的虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="b703d-122">On hello **Locate Virtual Hard Disk** screen, locate and select your virtual disk.</span></span>
3. <span data-ttu-id="b703d-123">在 hello**選擇動作**畫面上，，然後選取**轉換**和**下一步**。</span><span class="sxs-lookup"><span data-stu-id="b703d-123">On hello **Choose Action** screen, and then select **Convert** and **Next**.</span></span>
4. <span data-ttu-id="b703d-124">如果您需要從 VHDX tooconvert，選取**VHD** ，然後按一下**下一步**</span><span class="sxs-lookup"><span data-stu-id="b703d-124">If you need tooconvert from VHDX, select **VHD** and then click **Next**</span></span>
5. <span data-ttu-id="b703d-125">如果您需要從動態擴充磁碟 tooconvert，選取**固定大小**，然後按一下**下一步**</span><span class="sxs-lookup"><span data-stu-id="b703d-125">If you need tooconvert from a dynamically expanding disk, select **Fixed size** and then click **Next**</span></span>
6. <span data-ttu-id="b703d-126">找出並選取路徑 toosave hello 新 VHD 的檔案。</span><span class="sxs-lookup"><span data-stu-id="b703d-126">Locate and select a path toosave hello new VHD file to.</span></span>
7. <span data-ttu-id="b703d-127">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="b703d-127">Click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="b703d-128">這篇文章中的 hello 命令必須以提高權限的 PowerShell 工作階段執行。</span><span class="sxs-lookup"><span data-stu-id="b703d-128">hello commands in this article must be run on an elevated PowerShell session.</span></span>

### <a name="convert-disk-by-using-powershell"></a><span data-ttu-id="b703d-129">使用 PowerShell 轉換磁碟</span><span class="sxs-lookup"><span data-stu-id="b703d-129">Convert disk by using PowerShell</span></span>
<span data-ttu-id="b703d-130">您可以將虛擬磁碟轉換使用 hello [CONVERT-VHD](http://technet.microsoft.com/library/hh848454.aspx) Windows PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="b703d-130">You can convert a virtual disk by using hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) command in Windows PowerShell.</span></span> <span data-ttu-id="b703d-131">當您啟動 PowerShell 時，選取 [以系統管理員身分執行]。</span><span class="sxs-lookup"><span data-stu-id="b703d-131">Select **Run as administrator** when you start PowerShell.</span></span> 

<span data-ttu-id="b703d-132">hello 下列範例命令會將轉換從 VHDX tooVHD 及動態擴充磁碟 toofixed 大小：</span><span class="sxs-lookup"><span data-stu-id="b703d-132">hello following example command converts from VHDX tooVHD, and from a dynamically expanding disk toofixed-size:</span></span>

```Powershell
Convert-VHD –Path c:\test\MY-VM.vhdx –DestinationPath c:\test\MY-NEW-VM.vhd -VHDType Fixed
```
<span data-ttu-id="b703d-133">此命令中取代 hello 值"-路徑"hello 路徑 toohello 虛擬硬碟，您想要 tooconvert 和 hello 值為"-DestinationPath"hello 新路徑和名稱 hello 轉換磁碟。</span><span class="sxs-lookup"><span data-stu-id="b703d-133">In this command, replace hello value for "-Path" with hello path toohello virtual hard disk that you want tooconvert and hello value for "-DestinationPath" with hello new path and name of hello converted disk.</span></span>

### <a name="convert-from-vmware-vmdk-disk-format"></a><span data-ttu-id="b703d-134">從 VMware VMDK 磁碟格式進行轉換</span><span class="sxs-lookup"><span data-stu-id="b703d-134">Convert from VMware VMDK disk format</span></span>
<span data-ttu-id="b703d-135">如果您的 Windows VM 映像在 hello [VMDK 檔案格式](https://en.wikipedia.org/wiki/VMDK)，會將其轉換 tooa VHD 使用 hello [Microsoft VM 轉換器](https://www.microsoft.com/download/details.aspx?id=42497)。</span><span class="sxs-lookup"><span data-stu-id="b703d-135">If you have a Windows VM image in hello [VMDK file format](https://en.wikipedia.org/wiki/VMDK), convert it tooa VHD by using hello [Microsoft VM Converter](https://www.microsoft.com/download/details.aspx?id=42497).</span></span> <span data-ttu-id="b703d-136">如需詳細資訊，請參閱 hello 部落格文章[如何 tooConvert VMware VMDK tooHyper V VHD](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b703d-136">For more information, see hello blog article [How tooConvert a VMware VMDK tooHyper-V VHD](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx).</span></span>

## <a name="set-windows-configurations-for-azure"></a><span data-ttu-id="b703d-137">設定適用於 Azure 的 Windows 設定</span><span class="sxs-lookup"><span data-stu-id="b703d-137">Set Windows configurations for Azure</span></span>

<span data-ttu-id="b703d-138">在 hello 您計劃的 VM 上 tooupload tooAzure，執行所有的命令在 hello 下列步驟從[提升權限的命令提示字元視窗](https://technet.microsoft.com/library/cc947813.aspx):</span><span class="sxs-lookup"><span data-stu-id="b703d-138">On hello VM that you plan tooupload tooAzure, run all commands in hello following steps from an [elevated Command Prompt window](https://technet.microsoft.com/library/cc947813.aspx):</span></span>

1. <span data-ttu-id="b703d-139">移除任何持續性的靜態路由，在 hello 路由表：</span><span class="sxs-lookup"><span data-stu-id="b703d-139">Remove any static persistent route on hello routing table:</span></span>
   
   * <span data-ttu-id="b703d-140">tooview hello 路由表執行`route print`hello 的命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="b703d-140">tooview hello route table, run `route print` at hello command prompt.</span></span>
   * <span data-ttu-id="b703d-141">檢查 hello**持續性路由**區段。</span><span class="sxs-lookup"><span data-stu-id="b703d-141">Check hello **Persistence Routes** sections.</span></span> <span data-ttu-id="b703d-142">如果持續性的路由，請使用[路由刪除](https://technet.microsoft.com/library/cc739598.apx)tooremove 它。</span><span class="sxs-lookup"><span data-stu-id="b703d-142">If there is a persistent route, use [route delete](https://technet.microsoft.com/library/cc739598.apx) tooremove it.</span></span>
2. <span data-ttu-id="b703d-143">移除 hello WinHTTP proxy:</span><span class="sxs-lookup"><span data-stu-id="b703d-143">Remove hello WinHTTP proxy:</span></span>
   
    ```PowerShell
    netsh winhttp reset proxy
    ```
3. <span data-ttu-id="b703d-144">設定得 hello 磁碟 SAN 原則[Onlineall](https://technet.microsoft.com/library/gg252636.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b703d-144">Set hello disk SAN policy too[Onlineall](https://technet.microsoft.com/library/gg252636.aspx).</span></span> 
   
    ```PowerShell
    diskpart 
    ```
    <span data-ttu-id="b703d-145">在 hello 開啟命令提示字元視窗中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b703d-145">In hello open Command Prompt window, type hello following commands:</span></span>

     ```DISKPART
    san policy=onlineall
    exit   
    ```

4. <span data-ttu-id="b703d-146">設定適用於 Windows 的國際標準時間 (UTC) 時間和太 hello hello (w32time) 的 Windows 時間服務的啟動類型**自動**:</span><span class="sxs-lookup"><span data-stu-id="b703d-146">Set Coordinated Universal Time (UTC) time for Windows and hello startup type of hello Windows Time (w32time) service too**Automatically**:</span></span>
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\TimeZoneInformation' -name "RealTimeIsUniversal" 1 -Type DWord

    Set-Service -Name w32time -StartupType Auto
    ```
5. <span data-ttu-id="b703d-147">設定 hello 電源設定檔 toohello**高效能**:</span><span class="sxs-lookup"><span data-stu-id="b703d-147">Set hello power profile toohello **High Performance**:</span></span>

    ```PowerShell
    powercfg /setactive SCHEME_MIN
    ```

## <a name="check-hello-windows-services"></a><span data-ttu-id="b703d-148">檢查 hello Windows 服務</span><span class="sxs-lookup"><span data-stu-id="b703d-148">Check hello Windows services</span></span>
<span data-ttu-id="b703d-149">請確定每個 hello 下列 Windows 服務已設定 toohello **Windows 預設值**。</span><span class="sxs-lookup"><span data-stu-id="b703d-149">Make sure that each of hello following Windows services is set toohello **Windows default values**.</span></span> <span data-ttu-id="b703d-150">這些是必須設定 toomake 確定該 hello VM 已連線的服務的 hello 最小的數字。</span><span class="sxs-lookup"><span data-stu-id="b703d-150">These are hello minimum numbers of services that must be set up toomake sure that hello VM has connectivity.</span></span> <span data-ttu-id="b703d-151">tooreset hello 啟動設定，請執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b703d-151">tooreset hello startup settings, run hello following commands:</span></span>
   
```PowerShell
Set-Service -Name bfe -StartupType Auto
Set-Service -Name dhcp -StartupType Auto
Set-Service -Name dnscache -StartupType Auto
Set-Service -Name IKEEXT -StartupType Auto
Set-Service -Name iphlpsvc -StartupType Auto
Set-Service -Name netlogon -StartupType Manual
Set-Service -Name netman -StartupType Manual
Set-Service -Name nsi -StartupType Auto
Set-Service -Name termService -StartupType Manual
Set-Service -Name MpsSvc -StartupType Auto
Set-Service -Name RemoteRegistry -StartupType Auto
```

## <a name="update-remote-desktop-registry-settings"></a><span data-ttu-id="b703d-152">更新遠端桌面登錄設定</span><span class="sxs-lookup"><span data-stu-id="b703d-152">Update Remote Desktop registry settings</span></span>
<span data-ttu-id="b703d-153">請確定該 hello 下列設定已正確設定遠端桌面連線：</span><span class="sxs-lookup"><span data-stu-id="b703d-153">Make sure that hello following settings are configured correctly for remote desktop connection:</span></span>

>[!Note] 
><span data-ttu-id="b703d-154">您可能會收到錯誤訊息，當您執行 hello **Set-itemproperty-路徑 ' HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal 服務-名稱&lt;物件名稱&gt;&lt;值&gt;**在這些步驟。</span><span class="sxs-lookup"><span data-stu-id="b703d-154">You may receive an error message when you run hello **Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services -name &lt;object name&gt; &lt;value&gt;** in these steps.</span></span> <span data-ttu-id="b703d-155">hello 錯誤訊息可以放心忽略。</span><span class="sxs-lookup"><span data-stu-id="b703d-155">hello error message can be safely ignored.</span></span> <span data-ttu-id="b703d-156">這表示只有該 hello 網域不會將推送透過群組原則物件，該組態。</span><span class="sxs-lookup"><span data-stu-id="b703d-156">It means only that hello domain is not pushing that configuration through a Group Policy object.</span></span>
>
>

1. <span data-ttu-id="b703d-157">遠端桌面通訊協定 (RDP) 已啟用：</span><span class="sxs-lookup"><span data-stu-id="b703d-157">Remote Desktop Protocol (RDP) is enabled:</span></span>
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDenyTSConnections" -Value 0 -Type DWord
    ```
   
2. <span data-ttu-id="b703d-158">hello RDP 連接埠已正確設定時 （預設連接埠 3389）：</span><span class="sxs-lookup"><span data-stu-id="b703d-158">hello RDP port is set up correctly (Default port 3389):</span></span>
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "PortNumber" 3389 -Type DWord
    ```
    <span data-ttu-id="b703d-159">當您部署 VM 時，則會針對連接埠 3389 建立 hello 預設規則。</span><span class="sxs-lookup"><span data-stu-id="b703d-159">When you deploy a VM, hello default rules are created against port 3389.</span></span> <span data-ttu-id="b703d-160">如果您想 toochange hello 連接埠號碼，可在動作 hello VM 部署在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="b703d-160">If you want toochange hello port number,  do that after hello VM is deployed in Azure.</span></span>

3. <span data-ttu-id="b703d-161">hello 接聽項接聽中的每個網路介面：</span><span class="sxs-lookup"><span data-stu-id="b703d-161">hello listener is listening in every network interface:</span></span>
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "LanAdapter" 0 -Type DWord
   ```
4. <span data-ttu-id="b703d-162">設定 hello hello RDP 連線的網路層級驗證模式：</span><span class="sxs-lookup"><span data-stu-id="b703d-162">Configure hello Network Level Authentication mode for hello RDP connections:</span></span>
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SecurityLayer" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "fAllowSecProtocolNegotiation" 1 -Type DWord
     ```

5. <span data-ttu-id="b703d-163">設定 hello 持續作用值：</span><span class="sxs-lookup"><span data-stu-id="b703d-163">Set hello keep-alive value：</span></span>
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveEnable" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveInterval" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "KeepAliveTimeout" 1 -Type DWord
    ```
6. <span data-ttu-id="b703d-164">重新連線：</span><span class="sxs-lookup"><span data-stu-id="b703d-164">Reconnect：</span></span>
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDisableAutoReconnect" 0 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fInheritReconnectSame" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fReconnectSame" 0 -Type DWord
    ```
7. <span data-ttu-id="b703d-165">限制並行連線數目 hello:</span><span class="sxs-lookup"><span data-stu-id="b703d-165">Limit hello number of concurrent connections：</span></span>
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "MaxInstanceCount" 4294967295 -Type DWord
    ```
8. <span data-ttu-id="b703d-166">如果有任何自我簽署的憑證繫結 toohello RDP 接聽程式，請將它們移除：</span><span class="sxs-lookup"><span data-stu-id="b703d-166">If there are any self-signed certificates tied toohello RDP listener, remove them:</span></span>
    
    ```PowerShell
    Remove-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SSLCertificateSHA1Hash"
    ```
    <span data-ttu-id="b703d-167">這是 toomake 確定當您部署的 hello VM 可以連接您在 hello 開頭。</span><span class="sxs-lookup"><span data-stu-id="b703d-167">This is toomake sure that you can connect at hello beginning when you deploy hello VM.</span></span> <span data-ttu-id="b703d-168">您也可以檢閱這在稍後階段之後視需要在 Azure 中部署 VM 的 hello。</span><span class="sxs-lookup"><span data-stu-id="b703d-168">You can also review this on a later stage after hello VM is deployed in Azure if needed.</span></span>

9. <span data-ttu-id="b703d-169">如果 hello VM 是網域的一部分，請檢查所有 hello 下列設定 toomake 確定 hello 先前的設定不會還原。</span><span class="sxs-lookup"><span data-stu-id="b703d-169">If hello VM will be part of a Domain, check all hello following settings toomake sure that hello former settings are not reverted.</span></span> <span data-ttu-id="b703d-170">您必須核取的 hello 原則包括 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="b703d-170">hello policies that must be checked are hello following:</span></span>
    
    - <span data-ttu-id="b703d-171">RDP 已啟用：</span><span class="sxs-lookup"><span data-stu-id="b703d-171">RDP is enabled:</span></span>

         <span data-ttu-id="b703d-172">電腦設定\原則\Windows 設定\系統管理範本\元件\遠端桌面服務\遠端桌面工作階段主機\連線：</span><span class="sxs-lookup"><span data-stu-id="b703d-172">Computer Configuration\Policies\Windows Settings\Administrative Templates\ Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span></span>
         
         <span data-ttu-id="b703d-173">**允許使用者 tooconnect 從遠端使用遠端桌面**</span><span class="sxs-lookup"><span data-stu-id="b703d-173">**Allow users tooconnect remotely by using Remote Desktop**</span></span>

    - <span data-ttu-id="b703d-174">NLA 群組原則：</span><span class="sxs-lookup"><span data-stu-id="b703d-174">NLA group policy:</span></span>

        <span data-ttu-id="b703d-175">設定\系統管理範本\元件\遠端桌面服務\遠端桌面工作階段主機\安全性：</span><span class="sxs-lookup"><span data-stu-id="b703d-175">Settings\Administrative Templates\Components\Remote Desktop Services\Remote Desktop Session Host\Security:</span></span> 
        
        <span data-ttu-id="b703d-176">**透過使用網路層級驗證以要求對遠端連線進行使用者驗證**</span><span class="sxs-lookup"><span data-stu-id="b703d-176">**Require user Authentication for remote connections by using Network Level Authentication**</span></span>
    
    - <span data-ttu-id="b703d-177">Keep Alive 設定：</span><span class="sxs-lookup"><span data-stu-id="b703d-177">Keep Alive settings:</span></span>

        <span data-ttu-id="b703d-178">電腦設定\原則\Windows 設定\系統管理範本\Windows 元件\遠端桌面服務\遠端桌面工作階段主機\連線：</span><span class="sxs-lookup"><span data-stu-id="b703d-178">Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span></span> 
        
        <span data-ttu-id="b703d-179">**設定 Keep-Alive 連線間隔**</span><span class="sxs-lookup"><span data-stu-id="b703d-179">**Configure keep-alive connection interval**</span></span>

    - <span data-ttu-id="b703d-180">重新連線設定：</span><span class="sxs-lookup"><span data-stu-id="b703d-180">Reconnect settings:</span></span>

        <span data-ttu-id="b703d-181">電腦設定\原則\Windows 設定\系統管理範本\Windows 元件\遠端桌面服務\遠端桌面工作階段主機\連線：</span><span class="sxs-lookup"><span data-stu-id="b703d-181">Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span></span> 
        
        <span data-ttu-id="b703d-182">**自動重新連線**</span><span class="sxs-lookup"><span data-stu-id="b703d-182">**Automatic reconnection**</span></span>

    - <span data-ttu-id="b703d-183">Hello 的數目限制設定連線：</span><span class="sxs-lookup"><span data-stu-id="b703d-183">Limit hello number of connections settings:</span></span>

        <span data-ttu-id="b703d-184">電腦設定\原則\Windows 設定\系統管理範本\Windows 元件\遠端桌面服務\遠端桌面工作階段主機\連線：</span><span class="sxs-lookup"><span data-stu-id="b703d-184">Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span></span> 
        
        <span data-ttu-id="b703d-185">**限制連線數目**</span><span class="sxs-lookup"><span data-stu-id="b703d-185">**Limit number of connections**</span></span>

## <a name="configure-windows-firewall-rules"></a><span data-ttu-id="b703d-186">設定 Windows 防火牆規則</span><span class="sxs-lookup"><span data-stu-id="b703d-186">Configure Windows Firewall rules</span></span>
1. <span data-ttu-id="b703d-187">開啟 Windows 防火牆 （網域、 標準和公用） 的 hello 三個設定檔：</span><span class="sxs-lookup"><span data-stu-id="b703d-187">Turn on Windows Firewall on hello three profiles (Domain, Standard, and Public):</span></span>

   ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\DomainProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\PublicProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\Standardprofile' -name "EnableFirewall" -Value 1 -Type DWord
   ```

2. <span data-ttu-id="b703d-188">執行下列命令在 PowerShell tooallow WinRM 透過 hello 三個防火牆設定檔 （網域、 私人和公用） 中的 hello 和啟用 PowerShell 遠端服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="b703d-188">Run hello following command in PowerShell tooallow WinRM through hello three firewall profiles (Domain, Private, and Public) and enable hello PowerShell Remote service:</span></span>
   
   ```PowerShell
    Enable-PSRemoting -force
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
   ```
3. <span data-ttu-id="b703d-189">啟用下列防火牆規則 tooallow hello RDP 流量 hello</span><span class="sxs-lookup"><span data-stu-id="b703d-189">Enable hello following firewall rules tooallow hello RDP traffic</span></span> 

   ```PowerShell
    netsh advfirewall firewall set rule group="Remote Desktop" new enable=yes
   ```   
4. <span data-ttu-id="b703d-190">啟用 hello 檔案和印表機共用規則 hello VM 可以回應 hello 虛擬網路內的 tooa ping 命令：</span><span class="sxs-lookup"><span data-stu-id="b703d-190">Enable hello File and Printer Sharing rule so that hello VM can respond tooa ping command inside hello Virtual Network:</span></span>

   ```PowerShell
    netsh advfirewall firewall set rule dir=in name="File and Printer Sharing (Echo Request - ICMPv4-In)" new enable=yes
   ``` 
5. <span data-ttu-id="b703d-191">如果 hello VM 是網域的一部分，請檢查下列設定 toomake 確定 hello 先前的設定不會還原 hello。</span><span class="sxs-lookup"><span data-stu-id="b703d-191">If hello VM  will be part of a Domain, check hello following settings toomake sure that hello former settings are not reverted.</span></span> <span data-ttu-id="b703d-192">您必須核取的 hello AD 原則包括 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="b703d-192">hello AD policies that must be checked are hello following:</span></span>

    - <span data-ttu-id="b703d-193">啟用 hello Windows 防火牆設定檔</span><span class="sxs-lookup"><span data-stu-id="b703d-193">Enable hello Windows Firewall profiles</span></span>

        <span data-ttu-id="b703d-194">電腦設定\原則\Windows 設定\系統管理範本\網路\網路連線\Windows 防火牆\網域設定檔\Windows 防火牆: **保護所有網路連線**</span><span class="sxs-lookup"><span data-stu-id="b703d-194">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **Protect all network connections**</span></span>

       <span data-ttu-id="b703d-195">電腦設定\原則\Windows 設定\系統管理範本\網路\網路連線\Windows 防火牆\標準設定檔\Windows 防火牆: **保護所有網路連線**</span><span class="sxs-lookup"><span data-stu-id="b703d-195">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **Protect all network connections**</span></span>

    - <span data-ttu-id="b703d-196">啟用 RDP</span><span class="sxs-lookup"><span data-stu-id="b703d-196">Enable RDP</span></span> 

        <span data-ttu-id="b703d-197">電腦設定\原則\Windows 設定\系統管理範本\網路\網路連線\Windows 防火牆\網域設定檔\Windows 防火牆: **允許輸入的遠端桌面例外**</span><span class="sxs-lookup"><span data-stu-id="b703d-197">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **Allow inbound Remote Desktop exceptions**</span></span>

        <span data-ttu-id="b703d-198">電腦設定\原則\Windows 設定\系統管理範本\網路\網路連線\Windows 防火牆\標準設定檔\Windows 防火牆: **允許輸入的遠端桌面例外**</span><span class="sxs-lookup"><span data-stu-id="b703d-198">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **Allow inbound Remote Desktop exceptions**</span></span>

    - <span data-ttu-id="b703d-199">啟用 ICMP-V4</span><span class="sxs-lookup"><span data-stu-id="b703d-199">Enable ICMP-V4</span></span>

        <span data-ttu-id="b703d-200">電腦設定\原則\Windows 設定\系統管理範本\網路\網路連線\Windows 防火牆\網域設定檔\Windows 防火牆: **允許 ICMP 例外**</span><span class="sxs-lookup"><span data-stu-id="b703d-200">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **Allow ICMP exceptions**</span></span>

        <span data-ttu-id="b703d-201">電腦設定\原則\Windows 設定\系統管理範本\網路\網路連線\Windows 防火牆\標準設定檔\Windows 防火牆: **允許 ICMP 例外**</span><span class="sxs-lookup"><span data-stu-id="b703d-201">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **Allow ICMP exceptions**</span></span>

## <a name="verify-vm-is-healthy-secure-and-accessible-with-rdp"></a><span data-ttu-id="b703d-202">確認 VM 處於狀況良好、安全且可使用 RDP 存取</span><span class="sxs-lookup"><span data-stu-id="b703d-202">Verify VM is healthy, secure, and accessible with RDP</span></span> 
1. <span data-ttu-id="b703d-203">確定 hello 磁碟 toomake 是狀況良好且維持一致，在 hello 下次 VM 重新啟動執行檢查磁碟作業：</span><span class="sxs-lookup"><span data-stu-id="b703d-203">toomake sure hello disk is healthy and consistent, run a check disk operation at hello next VM restart:</span></span>

    ```PowerShell
    Chkdsk /f
    ```
    <span data-ttu-id="b703d-204">請確定 hello 報告會顯示清除且狀況良好的磁碟。</span><span class="sxs-lookup"><span data-stu-id="b703d-204">Make sure that hello report shows a clean and healthy disk.</span></span>

2. <span data-ttu-id="b703d-205">設定 hello 開機設定資料 (BCD) 設定。</span><span class="sxs-lookup"><span data-stu-id="b703d-205">Set hello Boot Configuration Data (BCD) settings.</span></span> 

    > [!Note]
    > <span data-ttu-id="b703d-206">請確定您是在提升權限的 CMD 視窗上執行這些命令，而**不是**在 PowerShell 上：</span><span class="sxs-lookup"><span data-stu-id="b703d-206">Make sure you run these commands on an elevated CMD window and **NOT** on PowerShell:</span></span>
   
   ```CMD
   bcdedit /set {bootmgr} integrityservices enable
   
   bcdedit /set {default} device partition=C:
   
   bcdedit /set {default} integrityservices enable
   
   bcdedit /set {default} recoveryenabled Off
   
   bcdedit /set {default} osdevice partition=C:
   
   bcdedit /set {default} bootstatuspolicy IgnoreAllFailures
   ```
3. <span data-ttu-id="b703d-207">請確認該 hello Windows 管理 Instrumentations 存放庫是一致。</span><span class="sxs-lookup"><span data-stu-id="b703d-207">Verify that hello Windows Management Instrumentations repository is consistent.</span></span> <span data-ttu-id="b703d-208">tooperform 下列命令，執行的 hello:</span><span class="sxs-lookup"><span data-stu-id="b703d-208">tooperform this, run hello following command:</span></span>

    ```PowerShell
    winmgmt /verifyrepository
    ```
    <span data-ttu-id="b703d-209">如果 hello 儲存機制已損毀，請參閱[WMI： 資料庫損毀，或不](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not)。</span><span class="sxs-lookup"><span data-stu-id="b703d-209">If hello repository is corrupted, see [WMI: Repository Corruption, or Not](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not).</span></span>

4. <span data-ttu-id="b703d-210">請確定任何應用程式不使用 hello 連接埠 3389。</span><span class="sxs-lookup"><span data-stu-id="b703d-210">Make sure that any other application is not using hello port 3389.</span></span> <span data-ttu-id="b703d-211">Hello RDP 服務在 Azure 中使用此連接埠。</span><span class="sxs-lookup"><span data-stu-id="b703d-211">This port is used for hello RDP service in Azure.</span></span> <span data-ttu-id="b703d-212">您可以執行**netstat anob** toosee 使用的通訊埠是在 hello VM:</span><span class="sxs-lookup"><span data-stu-id="b703d-212">You can run **netstat -anob** toosee which ports are in used on hello VM:</span></span>

    ```PowerShell
    netstat -anob
    ```

5. <span data-ttu-id="b703d-213">如果您想 tooupload Windows VHD hello 網域控制站，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b703d-213">If hello Windows VHD that you want tooupload is a domain controller, then follow these steps:</span></span>

    <span data-ttu-id="b703d-214">A.</span><span class="sxs-lookup"><span data-stu-id="b703d-214">A.</span></span> <span data-ttu-id="b703d-215">請遵循[這些額外的步驟](https://support.microsoft.com/kb/2904015)tooprepare hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="b703d-215">Follow [these extra steps](https://support.microsoft.com/kb/2904015) tooprepare hello disk.</span></span>

    <span data-ttu-id="b703d-216">B.</span><span class="sxs-lookup"><span data-stu-id="b703d-216">B.</span></span> <span data-ttu-id="b703d-217">請確定您知道 hello DSRM 密碼，如果您有 DSRM toostart hello VM 在某個時間點。</span><span class="sxs-lookup"><span data-stu-id="b703d-217">Make sure that you know hello DSRM password in case you have toostart hello VM in DSRM at some point.</span></span> <span data-ttu-id="b703d-218">您可能會想 toorefer toothis 連結 tooset hello [DSRM 密碼](https://technet.microsoft.com/library/cc754363(v=ws.11).aspx)。</span><span class="sxs-lookup"><span data-stu-id="b703d-218">You may want toorefer toothis link tooset hello [DSRM password](https://technet.microsoft.com/library/cc754363(v=ws.11).aspx).</span></span>

6. <span data-ttu-id="b703d-219">請確定 hello 內建系統管理員帳戶和密碼已知 tooyou。</span><span class="sxs-lookup"><span data-stu-id="b703d-219">Make sure that hello Built-in Administrator account and password are known tooyou.</span></span> <span data-ttu-id="b703d-220">您可能想 tooreset hello 目前本機系統管理員密碼，並確定您可以透過 RDP 連線 hello tooWindows 中使用此帳戶 toosign。</span><span class="sxs-lookup"><span data-stu-id="b703d-220">You may want tooreset hello current local administrator password and make sure that you can use this account toosign in tooWindows through hello RDP connection.</span></span> <span data-ttu-id="b703d-221">此存取權限是由 hello 「 允許登入遠端桌面服務透過 「 群組原則物件所控制。</span><span class="sxs-lookup"><span data-stu-id="b703d-221">This access permission is controlled by hello "Allow log on through Remote Desktop Services" Group Policy object.</span></span> <span data-ttu-id="b703d-222">您可以在 hello 本機群組原則編輯器中檢視此物件下：</span><span class="sxs-lookup"><span data-stu-id="b703d-222">You can view this object in hello Local Group Policy Editor under:</span></span>

    <span data-ttu-id="b703d-223">電腦設定\Windows 設定\安全性設定\本機原則\使用者權限指派</span><span class="sxs-lookup"><span data-stu-id="b703d-223">Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment</span></span>

7. <span data-ttu-id="b703d-224">請檢查下列 AD hello 原則 toomake 確定您不會封鎖您的 RDP 存取透過 RDP 或從 hello 網路：</span><span class="sxs-lookup"><span data-stu-id="b703d-224">Check hello following AD polices toomake sure that you are not blocking your RDP access through RDP nor from hello network:</span></span>

    - <span data-ttu-id="b703d-225">電腦設定 \windows 設定 \ 安全性設定 \ 原則 \ 使用者權限 Assignment\Deny 存取 toothis 電腦從 hello 網路</span><span class="sxs-lookup"><span data-stu-id="b703d-225">Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Deny access toothis computer from hello network</span></span>

    - <span data-ttu-id="b703d-226">電腦設定\Windows 設定\安全性設定\本機原則\使用者權限指派\拒絕從遠端桌面服務登入</span><span class="sxs-lookup"><span data-stu-id="b703d-226">Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Deny log on through Remote Desktop Services</span></span>


8. <span data-ttu-id="b703d-227">確定 Windows 是仍狀況良好的重新啟動 hello VM toomake 可以達到使用 hello RDP 連接。</span><span class="sxs-lookup"><span data-stu-id="b703d-227">Restart hello VM toomake sure that Windows is still healthy can be reached by using hello RDP connection.</span></span> <span data-ttu-id="b703d-228">此時，您可能想在您本機 HYPER-V toomake 確定 hello VM 正在啟動完全 toocreate VM，然後測試是否可以連線的 RDP。</span><span class="sxs-lookup"><span data-stu-id="b703d-228">At this point, you may want toocreate a VM in your local Hyper-V toomake sure hello VM is starting completely and then test whether it is RDP reachable.</span></span>

9. <span data-ttu-id="b703d-229">移除任何額外的傳輸驅動程式介面篩選，例如分析 TCP 封包的軟體或額外的防火牆。</span><span class="sxs-lookup"><span data-stu-id="b703d-229">Remove any extra Transport Driver Interface filters, such as software that analyzes TCP packets or extra firewalls.</span></span> <span data-ttu-id="b703d-230">您也可以檢閱這在稍後階段之後視需要在 Azure 中部署 VM 的 hello。</span><span class="sxs-lookup"><span data-stu-id="b703d-230">You can also review this on a later stage after hello VM is deployed in Azure if needed.</span></span>

10. <span data-ttu-id="b703d-231">解除安裝任何其他第三方軟體及相關的 toophysical 元件或其他虛擬化技術的驅動程式。</span><span class="sxs-lookup"><span data-stu-id="b703d-231">Uninstall any other third-party software and driver that is related toophysical components or any other virtualization technology.</span></span>

### <a name="install-windows-updates"></a><span data-ttu-id="b703d-232">安裝 Windows 更新</span><span class="sxs-lookup"><span data-stu-id="b703d-232">Install Windows Updates</span></span>
<span data-ttu-id="b703d-233">hello 的理想組態太**有在最新 hello hello 機器 hello 修補程式等級**。</span><span class="sxs-lookup"><span data-stu-id="b703d-233">hello ideal configuration is too**have hello patch level of hello machine at hello latest**.</span></span> <span data-ttu-id="b703d-234">如果不可行，請確定已安裝下列更新該 hello:</span><span class="sxs-lookup"><span data-stu-id="b703d-234">If this is not possible, make sure that hello following updates are installed:</span></span>

|                       |                   |           |                                       <span data-ttu-id="b703d-235">最低檔案版本 x64</span><span class="sxs-lookup"><span data-stu-id="b703d-235">Minimum file version x64</span></span>       |                                      |                                      |                            |
|-------------------------|-------------------|------------------------------------|---------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|
| <span data-ttu-id="b703d-236">元件</span><span class="sxs-lookup"><span data-stu-id="b703d-236">Component</span></span>               | <span data-ttu-id="b703d-237">Binary</span><span class="sxs-lookup"><span data-stu-id="b703d-237">Binary</span></span>            | <span data-ttu-id="b703d-238">Windows 7 & Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="b703d-238">Windows 7 & Windows Server 2008 R2</span></span> | <span data-ttu-id="b703d-239">Windows 8 & Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="b703d-239">Windows 8 & Windows Server 2012</span></span>             | <span data-ttu-id="b703d-240">Windows 8.1 & Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="b703d-240">Windows 8.1 & Windows Server 2012 R2</span></span> | <span data-ttu-id="b703d-241">Windows 10 & Windows Server 2016 RS1</span><span class="sxs-lookup"><span data-stu-id="b703d-241">Windows 10 & Windows Server 2016 RS1</span></span> | <span data-ttu-id="b703d-242">Windows 10 RS2</span><span class="sxs-lookup"><span data-stu-id="b703d-242">Windows 10 RS2</span></span>             |
| <span data-ttu-id="b703d-243">儲存體</span><span class="sxs-lookup"><span data-stu-id="b703d-243">Storage</span></span>                 | <span data-ttu-id="b703d-244">disk.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-244">disk.sys</span></span>          | <span data-ttu-id="b703d-245">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b703d-245">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b703d-246">6.2.9200.17638 / 6.2.9200.21757 - KB3137061</span><span class="sxs-lookup"><span data-stu-id="b703d-246">6.2.9200.17638 / 6.2.9200.21757 - KB3137061</span></span> | <span data-ttu-id="b703d-247">6.3.9600.18203 - KB3137061</span><span class="sxs-lookup"><span data-stu-id="b703d-247">6.3.9600.18203 - KB3137061</span></span>           | -                                    | -                          |
|                         | <span data-ttu-id="b703d-248">storport.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-248">storport.sys</span></span>      | <span data-ttu-id="b703d-249">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b703d-249">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b703d-250">6.2.9200.17188 / 6.2.9200.21306 - KB3018489</span><span class="sxs-lookup"><span data-stu-id="b703d-250">6.2.9200.17188 / 6.2.9200.21306 - KB3018489</span></span> | <span data-ttu-id="b703d-251">6.3.9600.18573 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b703d-251">6.3.9600.18573 - KB4022726</span></span>           | <span data-ttu-id="b703d-252">10.0.14393.1358 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b703d-252">10.0.14393.1358 - KB4022715</span></span>          | <span data-ttu-id="b703d-253">10.0.15063.332</span><span class="sxs-lookup"><span data-stu-id="b703d-253">10.0.15063.332</span></span>             |
|                         | <span data-ttu-id="b703d-254">ntfs.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-254">ntfs.sys</span></span>          | <span data-ttu-id="b703d-255">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b703d-255">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b703d-256">6.2.9200.17623 / 6.2.9200.21743 - KB3121255</span><span class="sxs-lookup"><span data-stu-id="b703d-256">6.2.9200.17623 / 6.2.9200.21743 - KB3121255</span></span> | <span data-ttu-id="b703d-257">6.3.9600.18654 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b703d-257">6.3.9600.18654 - KB4022726</span></span>           | <span data-ttu-id="b703d-258">10.0.14393.1198 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b703d-258">10.0.14393.1198 - KB4022715</span></span>          | <span data-ttu-id="b703d-259">10.0.15063.447</span><span class="sxs-lookup"><span data-stu-id="b703d-259">10.0.15063.447</span></span>             |
|                         | <span data-ttu-id="b703d-260">Iologmsg.dll</span><span class="sxs-lookup"><span data-stu-id="b703d-260">Iologmsg.dll</span></span>      | <span data-ttu-id="b703d-261">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b703d-261">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b703d-262">6.2.9200.16384 - KB2995387</span><span class="sxs-lookup"><span data-stu-id="b703d-262">6.2.9200.16384 - KB2995387</span></span>                  | -                                    | -                                    | -                          |
|                         | <span data-ttu-id="b703d-263">Classpnp.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-263">Classpnp.sys</span></span>      | <span data-ttu-id="b703d-264">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b703d-264">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b703d-265">6.2.9200.17061 / 6.2.9200.21180 - KB2995387</span><span class="sxs-lookup"><span data-stu-id="b703d-265">6.2.9200.17061 / 6.2.9200.21180 - KB2995387</span></span> | <span data-ttu-id="b703d-266">6.3.9600.18334 - KB3172614</span><span class="sxs-lookup"><span data-stu-id="b703d-266">6.3.9600.18334 - KB3172614</span></span>           | <span data-ttu-id="b703d-267">10.0.14393.953 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b703d-267">10.0.14393.953 - KB4022715</span></span>           | -                          |
|                         | <span data-ttu-id="b703d-268">Volsnap.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-268">Volsnap.sys</span></span>       | <span data-ttu-id="b703d-269">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b703d-269">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b703d-270">6.2.9200.17047 / 6.2.9200.21165 - KB2975331</span><span class="sxs-lookup"><span data-stu-id="b703d-270">6.2.9200.17047 / 6.2.9200.21165 - KB2975331</span></span> | <span data-ttu-id="b703d-271">6.3.9600.18265 - KB3145384</span><span class="sxs-lookup"><span data-stu-id="b703d-271">6.3.9600.18265 - KB3145384</span></span>           | -                                    | <span data-ttu-id="b703d-272">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="b703d-272">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="b703d-273">partmgr.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-273">partmgr.sys</span></span>       | <span data-ttu-id="b703d-274">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b703d-274">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b703d-275">6.2.9200.16681 - KB2877114</span><span class="sxs-lookup"><span data-stu-id="b703d-275">6.2.9200.16681 - KB2877114</span></span>                  | <span data-ttu-id="b703d-276">6.3.9600.17401 - KB3000850</span><span class="sxs-lookup"><span data-stu-id="b703d-276">6.3.9600.17401 - KB3000850</span></span>           | <span data-ttu-id="b703d-277">10.0.14393.953 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b703d-277">10.0.14393.953 - KB4022715</span></span>           | <span data-ttu-id="b703d-278">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="b703d-278">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="b703d-279">volmgr.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-279">volmgr.sys</span></span>        |                                    |                                             |                                      |                                      | <span data-ttu-id="b703d-280">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="b703d-280">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="b703d-281">Volmgrx.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-281">Volmgrx.sys</span></span>       | <span data-ttu-id="b703d-282">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b703d-282">6.1.7601.23403 - KB3125574</span></span>         | -                                           | -                                    | -                                    | <span data-ttu-id="b703d-283">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="b703d-283">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="b703d-284">Msiscsi.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-284">Msiscsi.sys</span></span>       | <span data-ttu-id="b703d-285">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b703d-285">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b703d-286">6.2.9200.21006 - KB2955163</span><span class="sxs-lookup"><span data-stu-id="b703d-286">6.2.9200.21006 - KB2955163</span></span>                  | <span data-ttu-id="b703d-287">6.3.9600.18624 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b703d-287">6.3.9600.18624 - KB4022726</span></span>           | <span data-ttu-id="b703d-288">10.0.14393.1066 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b703d-288">10.0.14393.1066 - KB4022715</span></span>          | <span data-ttu-id="b703d-289">10.0.15063.447</span><span class="sxs-lookup"><span data-stu-id="b703d-289">10.0.15063.447</span></span>             |
|                         | <span data-ttu-id="b703d-290">Msdsm.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-290">Msdsm.sys</span></span>         | <span data-ttu-id="b703d-291">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b703d-291">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b703d-292">6.2.9200.21474 - KB3046101</span><span class="sxs-lookup"><span data-stu-id="b703d-292">6.2.9200.21474 - KB3046101</span></span>                  | <span data-ttu-id="b703d-293">6.3.9600.18592 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b703d-293">6.3.9600.18592 - KB4022726</span></span>           | -                                    | -                          |
|                         | <span data-ttu-id="b703d-294">Mpio.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-294">Mpio.sys</span></span>          | <span data-ttu-id="b703d-295">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b703d-295">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b703d-296">6.2.9200.21190 - KB3046101</span><span class="sxs-lookup"><span data-stu-id="b703d-296">6.2.9200.21190 - KB3046101</span></span>                  | <span data-ttu-id="b703d-297">6.3.9600.18616 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b703d-297">6.3.9600.18616 - KB4022726</span></span>           | <span data-ttu-id="b703d-298">10.0.14393.1198 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b703d-298">10.0.14393.1198 - KB4022715</span></span>          | -                          |
|                         | <span data-ttu-id="b703d-299">Fveapi.dll</span><span class="sxs-lookup"><span data-stu-id="b703d-299">Fveapi.dll</span></span>        | <span data-ttu-id="b703d-300">6.1.7601.23311 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b703d-300">6.1.7601.23311 - KB3125574</span></span>         | <span data-ttu-id="b703d-301">6.2.9200.20930 - KB2930244</span><span class="sxs-lookup"><span data-stu-id="b703d-301">6.2.9200.20930 - KB2930244</span></span>                  | <span data-ttu-id="b703d-302">6.3.9600.18294 - KB3172614</span><span class="sxs-lookup"><span data-stu-id="b703d-302">6.3.9600.18294 - KB3172614</span></span>           | <span data-ttu-id="b703d-303">10.0.14393.576 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b703d-303">10.0.14393.576 - KB4022715</span></span>           | -                          |
|                         | <span data-ttu-id="b703d-304">Fveapibase.dll</span><span class="sxs-lookup"><span data-stu-id="b703d-304">Fveapibase.dll</span></span>    | <span data-ttu-id="b703d-305">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b703d-305">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b703d-306">6.2.9200.20930 - KB2930244</span><span class="sxs-lookup"><span data-stu-id="b703d-306">6.2.9200.20930 - KB2930244</span></span>                  | <span data-ttu-id="b703d-307">6.3.9600.17415 - KB3172614</span><span class="sxs-lookup"><span data-stu-id="b703d-307">6.3.9600.17415 - KB3172614</span></span>           | <span data-ttu-id="b703d-308">10.0.14393.206 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b703d-308">10.0.14393.206 - KB4022715</span></span>           | -                          |
| <span data-ttu-id="b703d-309">網路</span><span class="sxs-lookup"><span data-stu-id="b703d-309">Network</span></span>                 | <span data-ttu-id="b703d-310">netvsc.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-310">netvsc.sys</span></span>        | -                                  | -                                           | -                                    | <span data-ttu-id="b703d-311">10.0.14393.1198 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b703d-311">10.0.14393.1198 - KB4022715</span></span>          | <span data-ttu-id="b703d-312">10.0.15063.250 - KB4020001</span><span class="sxs-lookup"><span data-stu-id="b703d-312">10.0.15063.250 - KB4020001</span></span> |
|                         | <span data-ttu-id="b703d-313">mrxsmb10.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-313">mrxsmb10.sys</span></span>      | <span data-ttu-id="b703d-314">6.1.7601.23816 - KB4022722</span><span class="sxs-lookup"><span data-stu-id="b703d-314">6.1.7601.23816 - KB4022722</span></span>         | <span data-ttu-id="b703d-315">6.2.9200.22108 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="b703d-315">6.2.9200.22108 - KB4022724</span></span>                  | <span data-ttu-id="b703d-316">6.3.9600.18603 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b703d-316">6.3.9600.18603 - KB4022726</span></span>           | <span data-ttu-id="b703d-317">10.0.14393.479 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b703d-317">10.0.14393.479 - KB4022715</span></span>           | <span data-ttu-id="b703d-318">10.0.15063.483</span><span class="sxs-lookup"><span data-stu-id="b703d-318">10.0.15063.483</span></span>             |
|                         | <span data-ttu-id="b703d-319">mrxsmb20.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-319">mrxsmb20.sys</span></span>      | <span data-ttu-id="b703d-320">6.1.7601.23816 - KB4022722</span><span class="sxs-lookup"><span data-stu-id="b703d-320">6.1.7601.23816 - KB4022722</span></span>         | <span data-ttu-id="b703d-321">6.2.9200.21548 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="b703d-321">6.2.9200.21548 - KB4022724</span></span>                  | <span data-ttu-id="b703d-322">6.3.9600.18586 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b703d-322">6.3.9600.18586 - KB4022726</span></span>           | <span data-ttu-id="b703d-323">10.0.14393.953 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b703d-323">10.0.14393.953 - KB4022715</span></span>           | <span data-ttu-id="b703d-324">10.0.15063.483</span><span class="sxs-lookup"><span data-stu-id="b703d-324">10.0.15063.483</span></span>             |
|                         | <span data-ttu-id="b703d-325">mrxsmb.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-325">mrxsmb.sys</span></span>        | <span data-ttu-id="b703d-326">6.1.7601.23816 - KB4022722</span><span class="sxs-lookup"><span data-stu-id="b703d-326">6.1.7601.23816 - KB4022722</span></span>         | <span data-ttu-id="b703d-327">6.2.9200.22074 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="b703d-327">6.2.9200.22074 - KB4022724</span></span>                  | <span data-ttu-id="b703d-328">6.3.9600.18586 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b703d-328">6.3.9600.18586 - KB4022726</span></span>           | <span data-ttu-id="b703d-329">10.0.14393.953 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b703d-329">10.0.14393.953 - KB4022715</span></span>           | <span data-ttu-id="b703d-330">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="b703d-330">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="b703d-331">tcpip.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-331">tcpip.sys</span></span>         | <span data-ttu-id="b703d-332">6.1.7601.23761 - KB4022722</span><span class="sxs-lookup"><span data-stu-id="b703d-332">6.1.7601.23761 - KB4022722</span></span>         | <span data-ttu-id="b703d-333">6.2.9200.22070 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="b703d-333">6.2.9200.22070 - KB4022724</span></span>                  | <span data-ttu-id="b703d-334">6.3.9600.18478 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b703d-334">6.3.9600.18478 - KB4022726</span></span>           | <span data-ttu-id="b703d-335">10.0.14393.1358 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b703d-335">10.0.14393.1358 - KB4022715</span></span>          | <span data-ttu-id="b703d-336">10.0.15063.447</span><span class="sxs-lookup"><span data-stu-id="b703d-336">10.0.15063.447</span></span>             |
|                         | <span data-ttu-id="b703d-337">http.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-337">http.sys</span></span>          | <span data-ttu-id="b703d-338">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b703d-338">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b703d-339">6.2.9200.17285 - KB3042553</span><span class="sxs-lookup"><span data-stu-id="b703d-339">6.2.9200.17285 - KB3042553</span></span>                  | <span data-ttu-id="b703d-340">6.3.9600.18574 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b703d-340">6.3.9600.18574 - KB4022726</span></span>           | <span data-ttu-id="b703d-341">10.0.14393.251 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b703d-341">10.0.14393.251 - KB4022715</span></span>           | <span data-ttu-id="b703d-342">10.0.15063.483</span><span class="sxs-lookup"><span data-stu-id="b703d-342">10.0.15063.483</span></span>             |
|                         | <span data-ttu-id="b703d-343">vmswitch.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-343">vmswitch.sys</span></span>      | <span data-ttu-id="b703d-344">6.1.7601.23727 - KB4022719</span><span class="sxs-lookup"><span data-stu-id="b703d-344">6.1.7601.23727 - KB4022719</span></span>         | <span data-ttu-id="b703d-345">6.2.9200.22117 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="b703d-345">6.2.9200.22117 - KB4022724</span></span>                  | <span data-ttu-id="b703d-346">6.3.9600.18654 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b703d-346">6.3.9600.18654 - KB4022726</span></span>           | <span data-ttu-id="b703d-347">10.0.14393.1358 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b703d-347">10.0.14393.1358 - KB4022715</span></span>          | <span data-ttu-id="b703d-348">10.0.15063.138</span><span class="sxs-lookup"><span data-stu-id="b703d-348">10.0.15063.138</span></span>             |
| <span data-ttu-id="b703d-349">核心</span><span class="sxs-lookup"><span data-stu-id="b703d-349">Core</span></span>                    | <span data-ttu-id="b703d-350">ntoskrnl.exe</span><span class="sxs-lookup"><span data-stu-id="b703d-350">ntoskrnl.exe</span></span>      | <span data-ttu-id="b703d-351">6.1.7601.23807 - KB4022719</span><span class="sxs-lookup"><span data-stu-id="b703d-351">6.1.7601.23807 - KB4022719</span></span>         | <span data-ttu-id="b703d-352">6.2.9200.22170 - KB4022718</span><span class="sxs-lookup"><span data-stu-id="b703d-352">6.2.9200.22170 - KB4022718</span></span>                  | <span data-ttu-id="b703d-353">6.3.9600.18696 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b703d-353">6.3.9600.18696 - KB4022726</span></span>           | <span data-ttu-id="b703d-354">10.0.14393.1358 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b703d-354">10.0.14393.1358 - KB4022715</span></span>          | <span data-ttu-id="b703d-355">10.0.15063.483</span><span class="sxs-lookup"><span data-stu-id="b703d-355">10.0.15063.483</span></span>             |
| <span data-ttu-id="b703d-356">遠端桌面服務問題</span><span class="sxs-lookup"><span data-stu-id="b703d-356">Remote Desktop Services</span></span> | <span data-ttu-id="b703d-357">rdpcorets.dll</span><span class="sxs-lookup"><span data-stu-id="b703d-357">rdpcorets.dll</span></span>     | <span data-ttu-id="b703d-358">6.2.9200.21506 - KB4022719</span><span class="sxs-lookup"><span data-stu-id="b703d-358">6.2.9200.21506 - KB4022719</span></span>         | <span data-ttu-id="b703d-359">6.2.9200.22104 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="b703d-359">6.2.9200.22104 - KB4022724</span></span>                  | <span data-ttu-id="b703d-360">6.3.9600.18619 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b703d-360">6.3.9600.18619 - KB4022726</span></span>           | <span data-ttu-id="b703d-361">10.0.14393.1198 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b703d-361">10.0.14393.1198 - KB4022715</span></span>          | <span data-ttu-id="b703d-362">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="b703d-362">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="b703d-363">termsrv.dll</span><span class="sxs-lookup"><span data-stu-id="b703d-363">termsrv.dll</span></span>       | <span data-ttu-id="b703d-364">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b703d-364">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="b703d-365">6.2.9200.17048 - KB2973501</span><span class="sxs-lookup"><span data-stu-id="b703d-365">6.2.9200.17048 - KB2973501</span></span>                  | <span data-ttu-id="b703d-366">6.3.9600.17415 - KB3000850</span><span class="sxs-lookup"><span data-stu-id="b703d-366">6.3.9600.17415 - KB3000850</span></span>           | <span data-ttu-id="b703d-367">10.0.14393.0 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b703d-367">10.0.14393.0 - KB4022715</span></span>             | <span data-ttu-id="b703d-368">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="b703d-368">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="b703d-369">termdd.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-369">termdd.sys</span></span>        | <span data-ttu-id="b703d-370">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b703d-370">6.1.7601.23403 - KB3125574</span></span>         | -                                           | -                                    | -                                    | -                          |
|                         | <span data-ttu-id="b703d-371">win32k.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-371">win32k.sys</span></span>        | <span data-ttu-id="b703d-372">6.1.7601.23807 - KB4022719</span><span class="sxs-lookup"><span data-stu-id="b703d-372">6.1.7601.23807 - KB4022719</span></span>         | <span data-ttu-id="b703d-373">6.2.9200.22168 - KB4022718</span><span class="sxs-lookup"><span data-stu-id="b703d-373">6.2.9200.22168 - KB4022718</span></span>                  | <span data-ttu-id="b703d-374">6.3.9600.18698 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="b703d-374">6.3.9600.18698 - KB4022726</span></span>           | <span data-ttu-id="b703d-375">10.0.14393.594 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="b703d-375">10.0.14393.594 - KB4022715</span></span>           | -                          |
|                         | <span data-ttu-id="b703d-376">rdpdd.dll</span><span class="sxs-lookup"><span data-stu-id="b703d-376">rdpdd.dll</span></span>         | <span data-ttu-id="b703d-377">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b703d-377">6.1.7601.23403 - KB3125574</span></span>         | -                                           | -                                    | -                                    | -                          |
|                         | <span data-ttu-id="b703d-378">rdpwd.sys</span><span class="sxs-lookup"><span data-stu-id="b703d-378">rdpwd.sys</span></span>         | <span data-ttu-id="b703d-379">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="b703d-379">6.1.7601.23403 - KB3125574</span></span>         | -                                           | -                                    | -                                    | -                          |
| <span data-ttu-id="b703d-380">安全性</span><span class="sxs-lookup"><span data-stu-id="b703d-380">Security</span></span>                | <span data-ttu-id="b703d-381">到期 tooWannaCrypt</span><span class="sxs-lookup"><span data-stu-id="b703d-381">Due tooWannaCrypt</span></span> | <span data-ttu-id="b703d-382">KB4012212</span><span class="sxs-lookup"><span data-stu-id="b703d-382">KB4012212</span></span>                          | <span data-ttu-id="b703d-383">KB4012213</span><span class="sxs-lookup"><span data-stu-id="b703d-383">KB4012213</span></span>                                   | <span data-ttu-id="b703d-384">KB4012213</span><span class="sxs-lookup"><span data-stu-id="b703d-384">KB4012213</span></span>                            | <span data-ttu-id="b703d-385">KB4012606</span><span class="sxs-lookup"><span data-stu-id="b703d-385">KB4012606</span></span>                            | <span data-ttu-id="b703d-386">KB4012606</span><span class="sxs-lookup"><span data-stu-id="b703d-386">KB4012606</span></span>                  |
|                         |                   |                                    | <span data-ttu-id="b703d-387">KB4012216</span><span class="sxs-lookup"><span data-stu-id="b703d-387">KB4012216</span></span>                                   |                                      | <span data-ttu-id="b703d-388">KB4013198</span><span class="sxs-lookup"><span data-stu-id="b703d-388">KB4013198</span></span>                            | <span data-ttu-id="b703d-389">KB4013198</span><span class="sxs-lookup"><span data-stu-id="b703d-389">KB4013198</span></span>                  |
|                         |                   | <span data-ttu-id="b703d-390">KB4012215</span><span class="sxs-lookup"><span data-stu-id="b703d-390">KB4012215</span></span>                          | <span data-ttu-id="b703d-391">KB4012214</span><span class="sxs-lookup"><span data-stu-id="b703d-391">KB4012214</span></span>                                   | <span data-ttu-id="b703d-392">KB4012216</span><span class="sxs-lookup"><span data-stu-id="b703d-392">KB4012216</span></span>                            | <span data-ttu-id="b703d-393">KB4013429</span><span class="sxs-lookup"><span data-stu-id="b703d-393">KB4013429</span></span>                            | <span data-ttu-id="b703d-394">KB4013429</span><span class="sxs-lookup"><span data-stu-id="b703d-394">KB4013429</span></span>                  |
|                         |                   |                                    | <span data-ttu-id="b703d-395">KB4012217</span><span class="sxs-lookup"><span data-stu-id="b703d-395">KB4012217</span></span>                                   |                                      | <span data-ttu-id="b703d-396">KB4013429</span><span class="sxs-lookup"><span data-stu-id="b703d-396">KB4013429</span></span>                            | <span data-ttu-id="b703d-397">KB4013429</span><span class="sxs-lookup"><span data-stu-id="b703d-397">KB4013429</span></span>                  |
       
### <span data-ttu-id="b703d-398">當 toouse sysprep<a id="step23"></a></span><span class="sxs-lookup"><span data-stu-id="b703d-398">When toouse sysprep <a id="step23"></a></span></span>    

<span data-ttu-id="b703d-399">Sysprep 是您可能會遇到將會重設 hello 安裝 hello 系統也會提供 「 全新 hello 體驗 」 移除所有的個人資料，以及重設數個元件的 windows 安裝程序。</span><span class="sxs-lookup"><span data-stu-id="b703d-399">Sysprep is a process that you could run into a windows installation that will reset hello installation of hello system and will provide an “out of hello box experience” by removing all personal data and resetting several components.</span></span> <span data-ttu-id="b703d-400">您通常這樣如果您想 toocreate 範本，您可以用來部署數個其他的 Vm，有特定的設定。</span><span class="sxs-lookup"><span data-stu-id="b703d-400">You typically do this if you want toocreate a template from which you can deploy several other VMs that have a specific configuration.</span></span> <span data-ttu-id="b703d-401">這稱為**一般化映像**。</span><span class="sxs-lookup"><span data-stu-id="b703d-401">This is called a **generalized image**.</span></span>

<span data-ttu-id="b703d-402">相反地，若要唯一 toocreate 其中一個 VM 從一個磁碟，您不需要 toouse sysprep。</span><span class="sxs-lookup"><span data-stu-id="b703d-402">If, instead, you want only toocreate one VM from one disk, you don’t have toouse sysprep.</span></span> <span data-ttu-id="b703d-403">在此情況下，您就可以建立從什麼 VM 就所謂的 hello**特製化映像**。</span><span class="sxs-lookup"><span data-stu-id="b703d-403">In this situation, you can just create hello VM from what is known as a **specialized image**.</span></span>

<span data-ttu-id="b703d-404">如需有關如何 toocreate 將 VM 從專用的磁碟，請參閱：</span><span class="sxs-lookup"><span data-stu-id="b703d-404">For more information about how toocreate a VM from a specialized disk, see:</span></span>

- [<span data-ttu-id="b703d-405">從特殊化磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="b703d-405">Create a VM from a specialized disk</span></span>](create-vm-specialized.md)
- [<span data-ttu-id="b703d-406">從特殊化 VHD 磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="b703d-406">Create a VM from a specialized VHD disk</span></span>](https://azure.microsoft.com/resources/templates/201-vm-specialized-vhd/)

<span data-ttu-id="b703d-407">如果您想 toocreate 一般化映像，您會需要 toorun sysprep。</span><span class="sxs-lookup"><span data-stu-id="b703d-407">If you want toocreate a generalized image, you need toorun sysprep.</span></span> <span data-ttu-id="b703d-408">如需 Sysprep 的詳細資訊，請參閱[如何 tooUse Sysprep： 簡介](http://technet.microsoft.com/library/bb457073.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b703d-408">For more information about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span> 

<span data-ttu-id="b703d-409">並非 Windows 電腦上安裝的每個角色或應用程式都支援這個一般化。</span><span class="sxs-lookup"><span data-stu-id="b703d-409">Not every role or application that’s installed on a Windows-based computer supports this generalization.</span></span> <span data-ttu-id="b703d-410">之前在將您執行此程序，請參閱下列文章 toomake 確定 toohello 該電腦的該 hello 角色支援 sysprep。</span><span class="sxs-lookup"><span data-stu-id="b703d-410">So before you run this procedure, refer toohello following article toomake sure that hello role of that computer is supported by sysprep.</span></span> <span data-ttu-id="b703d-411">如需詳細資訊，請參閱[伺服器角色的 Sysprep 支援](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="b703d-411">For more information, [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

### <a name="steps-toogeneralize-a-vhd"></a><span data-ttu-id="b703d-412">步驟 toogeneralize VHD</span><span class="sxs-lookup"><span data-stu-id="b703d-412">Steps toogeneralize a VHD</span></span>

>[!NOTE]
> <span data-ttu-id="b703d-413">您當做下列步驟中所指定的 hello 執行 sysprep.exe 之後，關閉 hello VM，並請勿開啟它回直到您從它建立映像在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="b703d-413">After you run sysprep.exe as specified  in hello following steps, turn off hello VM, and do not turn it back on until you create an image from it in Azure.</span></span>

1. <span data-ttu-id="b703d-414">登入 toohello Windows VM。</span><span class="sxs-lookup"><span data-stu-id="b703d-414">Sign in toohello Windows VM.</span></span>
2. <span data-ttu-id="b703d-415">以系統管理員身分執行**命令提示字元**。</span><span class="sxs-lookup"><span data-stu-id="b703d-415">Run **Command Prompt** as an administrator.</span></span> 
3. <span data-ttu-id="b703d-416">若要變更 hello 目錄： **%windir%\system32\sysprep**，然後執行**sysprep.exe**。</span><span class="sxs-lookup"><span data-stu-id="b703d-416">Change hello directory to: **%windir%\system32\sysprep**, and then run **sysprep.exe**.</span></span>
3. <span data-ttu-id="b703d-417">在 hello**系統準備工具**對話方塊中，選取**進入系統的全新體驗 (OOBE)**，並確定該 hello**一般化**選取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="b703d-417">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>

    ![系統準備工具](media/prepare-for-upload-vhd-image/syspre.png)
4. <span data-ttu-id="b703d-419">在 [關機選項] 中選取 [關機]。</span><span class="sxs-lookup"><span data-stu-id="b703d-419">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="b703d-420">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="b703d-420">Click **OK**.</span></span>
6. <span data-ttu-id="b703d-421">Sysprep 完成時，關閉 hello VM。</span><span class="sxs-lookup"><span data-stu-id="b703d-421">When Sysprep completes, shut down hello VM.</span></span> <span data-ttu-id="b703d-422">請勿使用**重新啟動**tooshut hello VM 關閉。</span><span class="sxs-lookup"><span data-stu-id="b703d-422">Do not use **Restart** tooshut down hello VM.</span></span>
7. <span data-ttu-id="b703d-423">Hello VHD 已準備好 toobe 上傳。</span><span class="sxs-lookup"><span data-stu-id="b703d-423">Now hello VHD is ready toobe uploaded.</span></span> <span data-ttu-id="b703d-424">如需有關如何 toocreate 將 VM 從一般化磁碟，請參閱[一般化的 VHD 上傳，並在 Azure 中使用新的 Vm toocreate](sa-upload-generalized.md)。</span><span class="sxs-lookup"><span data-stu-id="b703d-424">For more information about how toocreate a VM from a generalized disk, see [Upload a generalized VHD and use it toocreate a new VMs in Azure](sa-upload-generalized.md).</span></span>


## <a name="complete-recommended-configurations"></a><span data-ttu-id="b703d-425">完成建議的設定</span><span class="sxs-lookup"><span data-stu-id="b703d-425">Complete recommended configurations</span></span>
<span data-ttu-id="b703d-426">下列設定的 hello 不會影響上傳 VHD。</span><span class="sxs-lookup"><span data-stu-id="b703d-426">hello following settings do not affect VHD uploading.</span></span> <span data-ttu-id="b703d-427">不過，我們強烈建議您設定它們。</span><span class="sxs-lookup"><span data-stu-id="b703d-427">However, we strongly recommend that you configured them.</span></span>

* <span data-ttu-id="b703d-428">安裝 hello [Azure Vm 代理程式](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="b703d-428">Install hello [Azure VMs Agent](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="b703d-429">然後您可以啟用 VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="b703d-429">Then you can enable VM extensions.</span></span> <span data-ttu-id="b703d-430">hello VM 延伸模組實作大部分的 hello 重要功能，您可能會想 toouse 要與您的 Vm，例如，重設密碼、 設定 RDP，等等。</span><span class="sxs-lookup"><span data-stu-id="b703d-430">hello VM extensions implement most of hello critical functionality that you might want toouse with your VMs such as resetting passwords, configuring RDP, and so on.</span></span> <span data-ttu-id="b703d-431">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="b703d-431">For more information, see:</span></span>

    - <span data-ttu-id="b703d-432">[VM 代理程式與擴充功能 - 第 1 部分](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-1/) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="b703d-432">[VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-1/)</span></span>
    - <span data-ttu-id="b703d-433">[VM 代理程式與擴充功能 - 第 2 部分](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="b703d-433">[VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/)</span></span>
* <span data-ttu-id="b703d-434">hello 傾印記錄檔可以是 Windows 損毀問題的疑難排解很有幫助。</span><span class="sxs-lookup"><span data-stu-id="b703d-434">hello Dump log can be helpful in troubleshooting Windows crash issues.</span></span> <span data-ttu-id="b703d-435">啟用 hello 傾印記錄檔收集：</span><span class="sxs-lookup"><span data-stu-id="b703d-435">Enable hello Dump log collection:</span></span>
  
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "AutoReboot" -Value 0 -Type DWord
    New-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps'
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
    <span data-ttu-id="b703d-436">如果您收到本文章中步驟的任何 hello 程序期間所發生的任何錯誤，這表示相同的 hello 登錄機碼已存在。</span><span class="sxs-lookup"><span data-stu-id="b703d-436">If you receive any errors during any of hello procedural steps in this article, this means that hello registry keys already exists.</span></span> <span data-ttu-id="b703d-437">在此情況下，使用 hello 改用下列命令：</span><span class="sxs-lookup"><span data-stu-id="b703d-437">In this situation, use hello following commands instead:</span></span>

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
*  <span data-ttu-id="b703d-438">Hello VM 在 Azure 中建立之後，我們建議您將 hello 分頁檔放在 hello 「 暫存磁碟機 」 磁碟區 tooimprove 效能。</span><span class="sxs-lookup"><span data-stu-id="b703d-438">After hello VM is created in Azure, we recommend that you put hello pagefile on hello ”Temporal drive” volume tooimprove performance.</span></span> <span data-ttu-id="b703d-439">您可以如下方式設定這部分：</span><span class="sxs-lookup"><span data-stu-id="b703d-439">You can set up this as follows:</span></span>

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management' -name "PagingFiles" -Value "D:\pagefile"
    ```
<span data-ttu-id="b703d-440">如果沒有任何資料磁碟附加的 toohello VM，hello 暫存磁碟機磁碟區的磁碟機代號通常是 「 D."</span><span class="sxs-lookup"><span data-stu-id="b703d-440">If there’s any data disk that is attached toohello VM, hello Temporal drive volume's drive letter is typically "D."</span></span> <span data-ttu-id="b703d-441">這項指定可能是根據 hello 數目可用的磁碟機和 hello 進行設定，而不同。</span><span class="sxs-lookup"><span data-stu-id="b703d-441">This designation could be different, depending on hello number of available drives and hello settings that you  make.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b703d-442">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b703d-442">Next steps</span></span>
* [<span data-ttu-id="b703d-443">上傳 Windows VM 映像 tooAzure 資源管理員部署</span><span class="sxs-lookup"><span data-stu-id="b703d-443">Upload a Windows VM image tooAzure for Resource Manager deployments</span></span>](upload-generalized-managed.md)

